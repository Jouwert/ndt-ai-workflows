# Pseudonymisation summary

The assistant-side sandbox uses a deterministic transformation pipeline between production data and sandbox data.

## Core rules
- the same real-world entity always maps to the same pseudonym
- related records stay linkable across lists
- the production environment remains the source of truth
- the assistant works against sandboxed data only
- reverse mapping stays tightly controlled inside the transformation layer

## Data flow

```text
Production M365 / SharePoint data
  -> Graph API access from the VPS
  -> transformer service
  -> SQLite mapping state
  -> sandbox lists and datasets
  -> assistant runtime
```

## Runtime components
This workflow runs through a transformer on a self-hosted VPS.

The runtime shape is:
- production SharePoint data stays on the production side
- the VPS transformer fetches and transforms data
- a SQLite identity bridge stores the pseudonym mapping state
- the sandbox receives the transformed records
- OpenClaw reads only from the sandbox side

## Access and transformation path
- Microsoft Graph app-only access connects Microsoft 365 to the VPS transformer
- the transformer service fetches, pseudonymises, resolves lookups, and writes to the sandbox
- the SQLite mapping database keeps identity mappings stable over time
- the sandbox SharePoint environment provides the assistant-safe read layer

## Supervised new-entity handling
The workflow also supports a supervised path for names that appear during later write support.

That path is:
- the transformer detects a possible new name in a prompt
- a user confirms whether the entity is actually new
- the identity is pseudonymised first
- a proposal can then be generated from the already pseudonymised identity

## Field treatment matrix

| Class | Treatment | Typical examples | Result |
|---|---|---|---|
| A | Preserve as-is | dates, times, durations, statuses, non-sensitive technical IDs | keeps operational structure intact |
| B | Pseudonymise deterministically | person names, organisation names, email addresses, contact labels | keeps cross-list consistency without exposing real identities |
| C | Preserve structure, mask value | addresses, phone numbers, sensitive notes, formatted identifiers | keeps shape and emptiness patterns while hiding content |
| D | Exclude entirely | attachments, private case notes, unnecessary audit detail | removes high-risk content from the sandbox |

## Mapping model
The transformation layer maintains stable mappings for the entities that need to stay consistent across the sandbox.

Examples:
- `real organisation -> Organisation 001`
- `real contact -> Contact 001`
- `real email -> contact001@example.test`

The exact labels matter less than consistency.

## Relational integrity
The sandbox keeps the relationships that make the workflow testable:
- person-to-organisation links
- activity-to-contact links
- lookup and reference chains
- list-to-list navigation paths

Without that consistency, the sandbox stops behaving like the real system and the assistant becomes much less useful.

## Practical effect
This design reduces direct exposure of private information while keeping enough structure for support work, testing, and workflow inspection.

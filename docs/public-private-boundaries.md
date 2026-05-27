# Public / Private Boundaries

## Purpose
This document defines what should and should not be published in the public `ndt-ai-workflows` repository.

The goal is credibility, not maximum disclosure.
A strong portfolio repository explains architecture and judgement clearly **without** exposing sensitive organisational detail.

## Scope of the public case
This public repository describes one connected workflow built around:
- the **OpenClaw NDT AI assistant**;
- the **Hermes Power App support project**;
- the surrounding **Microsoft 365 / SharePoint environment** that shaped both.

That means the public repo should explain how these pieces relate.
It should **not** expose raw internal data from any of them.

## Publication rule
When deciding whether something belongs in the public repo, ask:
1. Does this improve credibility?
2. Does it explain deployment judgement, workflow design, or architecture?
3. Can it be shared without exposing private operational detail?
4. Would a careful external reviewer reasonably expect this to be public?

If the answer is unclear, keep it private until it is sanitized properly.

## Public now
These are good candidates for direct public inclusion.

### Framing and documentation
- repository README
- architecture summary written for external readers
- deployment-decision notes
- privacy/governance explanation at a high level
- lessons learned
- concise workflow descriptions showing how assistant, Power App support, and SharePoint context fit together

### Sanitized technical material
- selected code snippets with secrets removed
- pseudocode or simplified flow descriptions
- sanitized configuration examples
- non-sensitive folder structures
- diagrams showing system components, data boundaries, and workflow relationships

### Credibility artifacts
- evidence that the work was tied to a real organisational context
- explanations of bounded assistant scope
- explanations of why some SharePoint-connected data remained off-limits
- support workflow documentation that does not expose internal content

## Public after cleanup or anonymisation
These can be useful, but only after review and sanitisation.

### Screenshots
- Power App screenshots with names and private details removed
- screenshots of support outputs with sensitive text removed
- diagrams derived from internal systems but redrawn for public use
- sanitized examples of SharePoint structures if they reveal workflow logic without exposing actual internal content

### Technical examples
- selected scripts or excerpts after removing organisation identifiers
- example prompts or system behaviour excerpts after checking for private references
- deployment notes after stripping hostnames, tokens, and internal paths
- sample data only if clearly anonymised and not reversible

### Workflow examples
- support cases rewritten into generic examples
- example queries and outputs based on sandbox-safe or synthetic data
- summarised change logs that describe the type of work without exposing operational specifics
- SharePoint-related examples rewritten at structure level rather than raw content level

## Private only
These should stay out of the public repo.

### Secrets and infrastructure details
- API keys, tokens, secrets, certificates
- private hostnames and internal endpoints
- internal container/runtime secrets
- access credentials or auth configuration that could be abused

### Organisation-sensitive operational detail
- real SharePoint content
- real Power App data exports
- internal volunteer, client, or contact information
- operational notes that reveal private identity or case details
- logs containing private prompts, payloads, or message content
- raw M365 tenant details beyond what is needed to explain the architecture

### Internals that create unnecessary risk
- raw runtime ledgers
- internal queue files
- unsanitized webhook payloads
- internal monitoring traces
- anything that reveals too much about bounded internal workflows

## Special rule for GDPR wording
Public wording should stay careful.

Prefer:
- *designed for GDPR-conscious deployment*
- *privacy-first, self-hosted setup*
- *architected to support responsible handling of sensitive organisational data*

Avoid strong legal claims like:
- *fully GDPR-compliant*

Unless the public repository also documents the controls that justify that claim.

## Recommended public evidence mix
A strong public repository probably needs only:
- one concise README;
- one architecture overview;
- one privacy/governance note;
- one or two sanitized technical artifacts;
- one small lessons-learned section.

That is enough to feel real without turning the repo into an overstuffed documentation archive.

## Reviewer mindset to optimise for
The public repo should make a reviewer think:
- this is real work;
- this person understands deployment trade-offs;
- this person knows what to keep private;
- this person can connect assistant design, Power App support, and SharePoint/M365 reality into one workflow story;
- this is a credible applied AI case, not a generated documentation performance.

## Practical default
When in doubt:
- publish the explanation;
- keep the raw artifact private;
- use a sanitized excerpt instead of the full internal file.

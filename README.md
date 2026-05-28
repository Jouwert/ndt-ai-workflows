# ndt-ai-workflows

Documentation for an AI-supported workflow around **Nu De Toekomst**'s Microsoft 365 environment.

## What is in scope
This repository brings together three related parts of the workflow:
- an **OpenClaw-based NDT assistant**;
- a **Hermes-era Power App support workflow**;
- the surrounding **SharePoint / Microsoft 365 setup**.

## Background
Stichting Nu De Toekomst is a community organisation in Wageningen that grew from a small local initiative into a broader place for meeting, personal growth, making things together, and local networking. In its current 700m² space, it provides room for resident-led initiatives and start-ups that want to contribute to a stronger local community. More context: https://nudetoekomst.nl/

Nu De Toekomst already used:
- Microsoft 365
- SharePoint
- Power Apps

SharePoint is used to structure and manage operational information such as volunteers, activities, space rental, and client-related administration. The Power App supports that workflow, including the entry and management of activities and related operational records.

The assistant work and the Power App support work both sat inside that existing environment.
This repository documents how those parts relate to each other.

## Components

### OpenClaw assistant
The OpenClaw side explored an internal assistant with bounded access and a support-oriented role.

Topics:
- assistant scope;
- deployment setup;
- access boundaries;
- privacy-aware use.

### Hermes Power App support
The Hermes-side work focused on understanding and supporting a live operational Power App more reliably.

Topics:
- extraction of Power App and Flow context;
- support and troubleshooting;
- documentation for safer future changes.

### SharePoint / Microsoft 365 context
This is the shared environment around both parts.

Topics:
- SharePoint structures;
- M365 platform context;
- Power App dependencies;
- governance and access boundaries.

## Repository scope
This repository focuses on:
- workflow structure;
- component boundaries;
- deployment decisions;
- public documentation of the relationship between assistant logic, support tooling, and the underlying M365 environment.

It does not include raw internal system data.

## Repository contents
```text
ndt-ai-workflows/
├── assets/
│   └── images/
│       └── generated/
│           └── ndt-assistant-demo-chat.png
├── README.md
└── docs/
    ├── architecture-overview.md
    ├── deployment-decisions.md
    ├── public-private-boundaries.md
    ├── sanitized-technical-artifacts.md
    └── artifacts/
        ├── access-model-summary.md
        ├── extractor-walkthrough.md
        ├── minimal-vps-compose.yaml
        ├── minimal-vps-deployment-snippet.md
        ├── pseudonymisation-summary.md
        ├── synthetic-power-app-output-example.md
        └── synthetic-output/
            ├── app_structure.sample.json
            ├── datasources_index.sample.json
            ├── edges.sample.json
            └── golden_context.sample.txt
```

## Public / private boundary
This repository documents architecture and workflow logic.
It does not publish:
- raw SharePoint content;
- internal Power App data;
- secrets or private endpoints;
- sensitive runtime logs or payloads.

See [`docs/public-private-boundaries.md`](docs/public-private-boundaries.md).

## Current status
This is currently a curated public documentation layer for the workflow, with a first set of sanitized technical artifacts derived from the real source projects.

## Impact
- Core staff now have a mobile-accessible source of truth for activities, volunteers, and clients, without exposing sensitive details to people who do not need access.
- Support and iteration became much faster: bugs are typically resolved in under 10 minutes, and small workflow improvements can often be released within 30–60 minutes.
- This reduces dependency on slow external change cycles and makes the Power App behave more like a live operational tool than a static system.
- The bounded support architecture improves privacy while still allowing rapid diagnosis and release work.

## Next likely additions
Likely next additions:
- additional sanitized artifacts from the remaining candidate set
- one simple access or hosting diagram if it improves clarity

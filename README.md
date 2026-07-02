# ndt-ai-workflows

Documentation for a privacy-aware AI-supported workflow around **Nu De Toekomst**'s Microsoft 365 environment.

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

## Recent development snapshot
One current line of work in this project is an **AI-assisted financial workflow** for a non-profit running on Microsoft 365, SharePoint, and Power Apps.

The working goal is:
- let staff and volunteers submit finance requests in natural language;
- pull the relevant structured SharePoint context;
- construct a proposed request or list-item shape for review;
- keep human approval in the final loop.

This is being approached as a **privacy-first** workflow with bounded assistant access rather than a direct free-form agent on production data.

Current stack in this case:
- **OpenClaw** for the assistant layer
- **Hermes** for Power App support and troubleshooting
- a **pseudonymisation pipeline** between production data and the assistant-side sandbox

See [`docs/field-notes-financial-workflow.md`](docs/field-notes-financial-workflow.md).

## Relationship to the private NDT project cluster
This repository is the **public/sanitized documentation layer** for a wider private NDT project cluster.

It is derived from operational work around:
- the private Power App / finance support project;
- the private Hermes volunteer-intake AI/runtime project;
- legacy OpenClaw/Teddie assistant material;
- the surrounding Microsoft 365 / SharePoint environment.

This repo is **not** the operational source of truth. Keep private paths, raw SharePoint data, internal app exports, secrets, tokens, private endpoints, runtime databases, and sensitive logs out of this repository.

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
    ├── field-notes-financial-workflow.md
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

The most recent public direction documented here is a finance-workflow case where deterministic context extraction and pseudonymisation have proved more reliable than direct browser-driven or canvas-level agent integration.

## Impact
- Core staff now have a mobile-accessible source of truth for activities, volunteers, and clients, without exposing sensitive details to people who do not need access.
- Support and iteration became much faster: bugs are typically resolved in under 10 minutes, and small workflow improvements can often be released within 30–60 minutes.
- This reduces dependency on slow external change cycles and makes the Power App behave more like a live operational tool than a static system.
- The bounded support architecture improves privacy while still allowing rapid diagnosis and release work.

## What we learned so far
- Direct MCP-style integration into the Power App canvas has not yet proved reliable enough in this project.
- Browser-based control remains useful for inspection and troubleshooting, but too flaky and token-heavy as the main production path.
- The most reliable pattern so far is deterministic extraction of app and SharePoint context, structured transformation, and pseudonymisation before assistant-side use.

## Next likely additions
Likely next additions:
- one or two more public notes from the same finance-workflow line of work

A first reimbursement-oriented public diagram is now included here:
- [`assets/images/generated/reimbursement-workflow-architecture.svg`](assets/images/generated/reimbursement-workflow-architecture.svg)

# Architecture overview

## Scope
This document gives a high-level view of the workflow documented in `ndt-ai-workflows`.

It covers:
- the **Microsoft 365 / SharePoint / Power App environment** at Nu De Toekomst;
- the **OpenClaw-based NDT assistant**;
- the **Hermes Power App support workflow**.

## Organisational system context
Nu De Toekomst already used a Microsoft-based operational stack built around:
- **Microsoft 365** as the wider platform context;
- **SharePoint** for structured operational information;
- **Power Apps** for day-to-day handling of activities and related records.

In practice, SharePoint held structured information such as:
- volunteers;
- activities;
- space rental / room usage;
- clients and related administrative context.

The Power App sat on top of that environment and supported operational entry and management of activities and related workflow data.

The newer workflow line documented here extends that environment into an AI-assisted finance-request path where natural-language requests can be turned into structured proposals for later human approval.

## Architecture
The workflow consists of three layers: **operational data management**, **bounded assistant access**, and **support/documentation tooling**.

## Main layers

### 1. Operational layer: M365, SharePoint, and Power App
This is the base environment.

It includes:
- the organisation's Microsoft 365 setup;
- SharePoint lists and structures used for operational administration;
- the Power App used to work with that data in practice.

This layer is the source of truth for day-to-day work.
It is not a public artifact, and raw internal data from this layer should not be exposed in the public repository.

### 2. Assistant layer: OpenClaw NDT assistant
The OpenClaw side explored a bounded assistant role around the existing workflow.

A central design choice was that the assistant should **not** have broad direct access to production organisational data.
Instead, the architecture introduced a safer pattern based on:
- sandboxed or transformed data;
- bounded assistant scope;
- support-oriented rather than unrestricted behaviour.

The assistant architecture included:
- a production SharePoint environment;
- a transformed / pseudonymised sandbox environment;
- a bridge/API layer used for sandbox-safe queries;
- an OpenClaw/Teddie execution layer that worked against the safer sandboxed view.

### 3. Support layer: Hermes Power App support workflow
The Hermes-side work focused on understanding and supporting the existing Power App more reliably.

This layer was less about direct end-user assistance and more about:
- extracting app and flow context deterministically;
- building reusable documentation and indexes;
- making future troubleshooting and changes safer;
- supporting real support questions and feature work from an existing baseline.

In the finance-workflow case, this support layer also became the place where the practical integration strategy was tested:
- direct canvas-level agent integration looked attractive but did not prove stable enough;
- browser-driven control stayed useful for inspection, not as the main production path;
- deterministic extraction and transformation of app context proved much more reliable.

## Current practical pattern
The most credible current pattern in this project is:
- production SharePoint and Power App stay the operational source of truth;
- structured context is extracted through supported Microsoft access paths;
- sensitive context is transformed or pseudonymised before assistant-side use where needed;
- the assistant works from the structured representation;
- a human approval step remains in the write path.

## Layer summary

### Operational layer
- holds the live organisational workflow and records
- remains the main system of record

### Assistant layer
- provides bounded AI support around the workflow
- should not bypass privacy and governance constraints
- relies on safer access patterns rather than unrestricted production access

### Support layer
- helps operators understand and maintain the application environment
- improves future support and co-development work
- documents structure rather than trying to replace the operational system itself

## Simplified flow
```text
Nu De Toekomst staff and operations
            │
            ▼
Microsoft 365 / SharePoint / Power App environment
            │
     ┌──────┴────────┐
     │               │
     ▼               ▼
OpenClaw assistant   Hermes Power App support workflow
(bounded AI use)     (context extraction, support, documentation)
     │               │
     └──────┬────────┘
            ▼
Public documentation of workflow, boundaries, and deployment decisions
```

## Assistant-side access model
The assistant-side access model used a stricter access split:

```text
Production SharePoint
(real identities and operational relationships)
            │
            ▼
Transformer / pseudonymisation layer
            │
            ▼
Sandbox SharePoint view
(masked identities, operationally useful structure)
            │
            ▼
OpenClaw assistant
```

In that design:
- production data stays outside direct OpenClaw visibility;
- the assistant works against a safer transformed representation;
- the bridge/API layer becomes the controlled access path for queries.

## Public documentation boundary
This repository documents:
- the relationship between the layers;
- the role of SharePoint and Power Apps in the workflow;
- the bounded assistant design;
- the support/documentation role of the Hermes project;
- the shift toward deterministic context extraction as the most reliable integration path so far;
- the deployment and privacy decisions that shaped the setup.

This repository does not publish:
- raw SharePoint records;
- private Power App content;
- internal endpoints, credentials, or secrets;
- sensitive runtime artifacts;
- detailed operational data that belongs inside the organisation.

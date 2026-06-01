# Deployment decisions

## Scope
This document records the main deployment and documentation decisions in `ndt-ai-workflows`.

It focuses on how the workflow is deployed, bounded, and documented across:
- the Microsoft 365 / SharePoint / Power App environment at Nu De Toekomst;
- the OpenClaw-based NDT assistant;
- the Hermes Power App support workflow.

## The existing M365 environment remains the operational base
The workflow builds on an existing Microsoft 365 environment instead of replacing it with a separate AI-first application.

That means:
- SharePoint remains the main operational data layer;
- the Power App remains the operational interface for day-to-day work;
- the assistant and support tooling sit around that environment rather than replacing it.

This keeps the deployment close to the organisation's real workflow.

## The assistant runs as a bounded layer, not as a direct front end to production data
The OpenClaw assistant does not act as a broad direct interface to the live organisational environment.

The deployment keeps the assistant in a bounded role:
- limited scope;
- support-oriented behaviour;
- constrained access patterns;
- no assumption of unrestricted production visibility.

This keeps assistant behaviour aligned with privacy, governance, and operational caution.

## The assistant works against a transformed or sandboxed view
The assistant side uses a stricter access model than direct production access.

The workflow includes:
- a production SharePoint environment;
- a transformed or pseudonymised sandbox view;
- a bridge or API layer for controlled queries;
- an OpenClaw execution layer working against the safer view.

This keeps the assistant useful without depending on unrestricted access to internal records.

## The architecture keeps operations, assistant access, and support work separate
The deployment uses three connected but separate layers:
- operational data management;
- bounded assistant access;
- support and documentation tooling.

This avoids turning the workflow into one opaque "AI app".

Each layer keeps its own role:
- the operational layer stores and manages live records;
- the assistant layer provides bounded support around that workflow;
- the support layer helps maintain, troubleshoot, and document the application environment.

## The Hermes work supports the Power App instead of hiding it behind the assistant
The Hermes-side work focuses on Power App support, context extraction, troubleshooting, and documentation.

The Power App remains a real operational component in the workflow rather than disappearing behind the assistant.

This keeps the workflow grounded in actual organisational tooling instead of turning everything into one generic assistant product.

## Native canvas-level agent integration is not currently treated as a production path
In this project, direct MCP-style integration into the Power App canvas has not yet been reliable enough to treat as the main production path.

That does not mean the idea is permanently impossible.
It means the documented workflow should not pretend that a fragile path is production-ready when repeated real-world work says otherwise.

## Browser automation remains a support tool, not the foundation
Browser-driven access remains useful for:
- inspection
- troubleshooting
- visual checks

But it is still weaker than a deterministic structured access path for repeated operational use.

In this case, browser control has been too flaky and too token-heavy to act as the primary integration layer.

## Deterministic extraction and transformation is the preferred path
The most reliable path so far is to:
- extract app and data context through supported Microsoft interfaces;
- transform it into a structured working representation;
- pseudonymise where needed before assistant-side use;
- keep human approval in the final operational flow.

This is slower to build than a direct agent-on-canvas dream, but more stable and more defensible.

## The assistant runs in a self-hosted VPS setup
The OpenClaw assistant runs in a self-hosted VPS context.

This deployment choice keeps the assistant close to the operational environment while preserving a separate execution layer.

It supports:
- direct control over the runtime environment;
- bounded integration with the surrounding workflow;
- a deployment shape that fits privacy-aware organisational use.

## Practical result
The deployment documented in this workflow has a clear shape:
- Microsoft 365, SharePoint, and the Power App form the operational environment;
- the OpenClaw assistant adds bounded AI support around that environment;
- the Hermes support workflow improves maintenance, troubleshooting, and documentation;
- Graph-backed extraction and transformation currently provide the most reliable bridge between the operational system and the assistant-side workflow.

## Related documents
- [`README.md`](../README.md)
- [`architecture-overview.md`](architecture-overview.md)
- [`public-private-boundaries.md`](public-private-boundaries.md)
- [`field-notes-financial-workflow.md`](field-notes-financial-workflow.md)

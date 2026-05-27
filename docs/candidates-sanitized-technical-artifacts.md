# Candidate sanitized technical artifacts

This document tracks the remaining artifact candidates that have not yet been implemented in the public repo.

The implemented first-wave artifacts now live in:
- [`sanitized-technical-artifacts.md`](sanitized-technical-artifacts.md)
- [`artifacts/`](artifacts/)

## Remaining candidates

### Diagram for access layers
**Source material**
- OpenClaw access strategy notes (`ndt-ai-assistant/03-access-auth/ACCESS_STRATEGY.md`)
- Current public summary in this repo (`docs/artifacts/access-model-summary.md`)

**Possible public form**
- one small diagram showing browser access vs app/API access vs sandbox pipeline

**Why it is useful**
- it makes the access split readable at a glance
- it reinforces why browser automation is only a fallback layer

**Why it still needs work**
- it should add clarity without turning into architecture theatre

### Field classification example
**Source material**
- OpenClaw field classification notes (`ndt-ai-assistant/02-data-model/FIELD_CLASSIFICATION_MATRIX.md`)

**Possible public form**
- one generic classification table

**Why it is useful**
- it makes privacy handling more concrete
- it shows how structured transformation decisions are made

**Why it still needs work**
- the public version needs careful abstraction away from internal field names

### Hosting decision note
**Source material**
- OpenClaw hosting decision notes (`ndt-ai-assistant/04-privacy-governance/POC_HOSTING_DECISION.md`)
- VPS setup planning notes (`ndt-ai-assistant/06-hosting-deployment/VPS_SETUP_PLAN.md`)
- VPS isolation requirements (`ndt-ai-assistant/06-hosting-deployment/VPS_ISOLATION_REQUIREMENTS.md`)

**Possible public form**
- one short hosting decision note
- optionally one small infrastructure diagram

**Why it is useful**
- it explains why the workflow uses a self-hosted VPS shape
- it supports the privacy-aware deployment story with real operational choices

**Why it still needs work**
- the public version should stay short and avoid turning into infrastructure theatre

## Keep private or use only indirectly
These are not good direct public artifacts.

### Internal or risky by default
- Power App extracted normalized context output
- Power App diagnostics output
- Power App flow index output
- Power App formula index output
- Power App datasource index output
- OpenClaw environment template
- OpenClaw privacy / DPA checklist
- OpenClaw lookup map

**Why they stay private or indirect**
- they are too close to the internal runtime or real operational structure
- they may reveal connectors, field names, flows, or assumptions more precisely than needed
- they are better used as internal source material for smaller public derivative artifacts

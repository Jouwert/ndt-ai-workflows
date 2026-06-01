# Field notes: AI-assisted financial workflow

## Current public case
A recent line of work in this project focuses on an AI-assisted financial workflow for a non-profit running on Microsoft 365, SharePoint, and Power Apps.

The goal is practical rather than magical:
- let staff or volunteers describe a finance request in natural language
- pull the relevant structured context from SharePoint
- construct a proposed list item or request shape for review
- keep a human approval step in the loop

This is designed as a privacy-first workflow, not a direct free-form agent sitting on top of production data.

## Stack in this case
- **OpenClaw** as the assistant layer
- **Hermes** as the Power App support and troubleshooting layer
- a **pseudonymisation pipeline** between production data and the assistant-side sandbox

## What has worked poorly so far

### Native MCP-style integration into the Power App canvas
In this project, direct MCP-style integration into the Power App canvas has not yet been reliable enough to treat as a production path.

It was an attractive idea in theory, but in practice it repeatedly broke during real workflow work.

### Browser-driven control as the main integration path
Hermes browser control has still been useful for:
- inspection
- troubleshooting
- visual verification

But it has been too flaky and too token-heavy to treat as the main production integration path.

## What has worked best so far
The most reliable pattern has been:
1. extract app and list context deterministically through supported Microsoft access paths
2. transform that context into a structured support-friendly view
3. pseudonymise it before assistant-side use where needed
4. let the assistant work from that cleaner structured representation
5. keep human approval on the final write path

In practice, Microsoft Graph-backed extraction and transformation has been much slower to build than direct browser or canvas experimentation, but much more stable to run.

## Main takeaway
The interesting part of this work is not proving that an agent can do something once.

The interesting part is finding which path remains understandable, privacy-aware, and reliable inside the actual limits of the Microsoft ecosystem.

That gap between "this should work in theory" and "this works repeatedly in production" is where most of the engineering judgment lives.

## Public boundary reminder
This repository documents the workflow shape and the lessons learned.
It does not publish raw organisational data, live secrets, or private approval records.

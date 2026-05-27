# Access model summary

This workflow uses a layered access model around Microsoft 365, SharePoint, and the assistant runtime.

## Access layers

### Human browser access
Human browser access is used for:
- first-time setup
- permission checks
- visual inspection
- UI-only admin tasks

This layer is necessary, but it is not the foundation of the workflow.

### Assistant browser control
Assistant browser control is useful for:
- one-off inspection
- quick visual verification
- checking UI settings
- discovering field labels when no better interface is available yet

This layer is a fallback and support tool.
It is not the main integration path.

### Microsoft API / app access
The workflow uses a machine-usable Microsoft access path for repeatable data work.

In practice this means:
- app-scoped access is preferred over session-bound browser access
- mailbox and list access should use supported Microsoft interfaces
- access stays permission-bounded and more auditable than browser-driven work

Microsoft Graph is the key access shape in this workflow.

### Export and transformation pipeline
The workflow also uses a controlled transformation path between source data and the assistant-side sandbox.

That path allows:
- selective extraction
- deterministic transformation
- pseudonymisation before assistant-side use
- sandbox refreshes without giving the assistant direct production-side reads

## Decision rule
The workflow follows this order:
1. supported API or app access
2. supported export or connector paths
3. controlled manual exports for limited cases
4. browser automation only as fallback

## Practical split
In this setup:
- browser access supports inspection and administration
- API or app access supports repeatable system access
- the transformation pipeline prepares sandbox-safe data
- the assistant works on the sandbox side, not directly on unrestricted production data

## Why this matters
This keeps the workflow more stable than a browser-only setup.

It also keeps access narrower, more repeatable, and easier to reason about during support work, testing, and deployment.
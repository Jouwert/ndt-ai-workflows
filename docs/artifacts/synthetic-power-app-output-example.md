# Synthetic Power App support output example

This example shows the output shape produced by the Power App support extractor in a fully synthetic form.

## Files in this example
- [`synthetic-output/app_structure.sample.json`](synthetic-output/app_structure.sample.json)
- [`synthetic-output/edges.sample.json`](synthetic-output/edges.sample.json)
- [`synthetic-output/datasources_index.sample.json`](synthetic-output/datasources_index.sample.json)
- [`synthetic-output/golden_context.sample.txt`](synthetic-output/golden_context.sample.txt)

## Output roles
- `app_structure.sample.json` shows the screen tree and key event properties
- `edges.sample.json` shows navigation and dependency relationships
- `datasources_index.sample.json` shows the app's data-source inventory
- `golden_context.sample.txt` shows the readable support summary that sits next to the machine-readable outputs

## Mini flow

```text
app export + flow exports
  -> extractor
  -> structure, edges, and data source indexes
  -> readable support summary
```

## Why both machine-readable and readable outputs exist
The machine-readable files support search, inspection, and follow-on tooling.
The readable context file supports quick human orientation during support and change analysis.

## Example shape
The synthetic sample keeps the same output pattern as the real workflow:
- one app structure file
- one edge map
- one data-source inventory
- one readable context summary

That combination is enough to understand how the app is put together without exposing the live internal system.

# Extractor walkthrough

The Power App support workflow turns exported Power App and Power Automate archives into a small, stable output set.

## Input shape
- one Power App export zip
- zero or more related Power Automate flow export zips

## Processing flow

```text
Power App export zip + flow export zips
  -> archive classification
  -> .msapp and flow definition parsing
  -> extraction of screens, flows, data sources, references, and edges
  -> machine-readable output files
  -> readable golden_context.txt
```

## Sanitized excerpt
This excerpt keeps the real control flow of the live extractor while omitting project-specific internals.

```python
def parse_inputs(self, paths: List[Path]) -> None:
    for path in paths:
        kind = self.classify_outer_zip(path)
        self.archives.append(ArchiveArtifact(label=path.name, path=str(path), kind=kind))
        if kind == "power_app_export":
            self.parse_power_app_export(path)
        elif kind == "flow_export":
            self.parse_standalone_flow_export(path)
        else:
            self.warn(f"Skipping unrecognized archive type: {path}")

    self.references["connectors"] = sorted(set(self.references["connectors"]))
    self.references["variables"] = sorted(set(self.references["variables"]))
    self.references["collections"] = sorted(set(self.references["collections"]))
    self.data_sources = sorted(self.data_sources, key=lambda d: d.get("name", ""))
    self.flows = sorted(self.flows, key=lambda f: (f.get("name") or f.get("sourcePath") or ""))
    self.app["screenOrder"] = [screen["name"] for screen in self.app["screens"]]


def write_outputs(self) -> None:
    self.output_dir.mkdir(parents=True, exist_ok=True)
    payload = {
        "version": "hermes-v1",
        "source": {"archives": [arc.__dict__ for arc in self.archives]},
        "app": self.app,
        "flows": self.flows,
        "dataSources": self.data_sources,
        "references": self.references,
        "edges": self.edges,
        "diagnostics": self.diagnostics,
    }
    (self.output_dir / "app_structure.json").write_text(json.dumps({"app": self.app}, indent=2), encoding="utf-8")
    (self.output_dir / "flows_index.json").write_text(json.dumps(self.flows, indent=2), encoding="utf-8")
    (self.output_dir / "datasources_index.json").write_text(json.dumps(self.data_sources, indent=2), encoding="utf-8")
    (self.output_dir / "formula_index.json").write_text(json.dumps(self._formula_index(), indent=2), encoding="utf-8")
    (self.output_dir / "edges.json").write_text(json.dumps(self.edges, indent=2), encoding="utf-8")
    (self.output_dir / "diagnostics.json").write_text(json.dumps(self.diagnostics, indent=2), encoding="utf-8")
    (self.output_dir / "normalized_context.json").write_text(json.dumps(payload, indent=2), encoding="utf-8")
    (self.output_dir / "golden_context.txt").write_text(self.render_golden_context(), encoding="utf-8")
```

## What the extractor captures
- archive type
- app screens and screen order
- flow definitions
- data sources
- references such as connectors, variables, and collections
- navigation and dependency edges
- diagnostics and parsing warnings

## Output set
The extractor writes a small set of outputs with distinct roles:

- `app_structure.json` — app-level structure and screen tree
- `flows_index.json` — flow definitions in normalized form
- `datasources_index.json` — data source inventory
- `formula_index.json` — extracted event formulas and references
- `edges.json` — navigation and dependency edges
- `diagnostics.json` — parse warnings and counts
- `normalized_context.json` — combined machine-readable payload
- `golden_context.txt` — readable summary for human support work

## Why this matters in the workflow
This extractor gives the Hermes support side a deterministic way to inspect a live Power App without relying on vague natural-language summaries or one-off screenshots.

The result is a repeatable context package that can be checked, diffed, and reused during support and change analysis.

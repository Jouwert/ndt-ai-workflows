# Sanitized technical artifacts

This repository includes a small set of sanitized technical artifacts derived from the real NDT source projects.

## Implemented artifacts

### Extractor walkthrough
[`artifacts/extractor-walkthrough.md`](artifacts/extractor-walkthrough.md)

Shows how the Power App support workflow turns exported Power App and Flow archives into structured outputs and a readable support context.

### Minimal VPS deployment snippet
- [`artifacts/minimal-vps-deployment-snippet.md`](artifacts/minimal-vps-deployment-snippet.md)
- [`artifacts/minimal-vps-compose.yaml`](artifacts/minimal-vps-compose.yaml)

Shows the one-service VPS shape used for the transformer PoC.

### Pseudonymisation summary
[`artifacts/pseudonymisation-summary.md`](artifacts/pseudonymisation-summary.md)

Summarises the transformation rules that keep sandbox data usable while reducing direct exposure of private information.

### Access model summary
[`artifacts/access-model-summary.md`](artifacts/access-model-summary.md)

Summarises the layered access model behind the workflow, including browser access, app/API access, and the transformation path into the assistant-side sandbox.

### Synthetic bot chat visual
- [`artifacts/synthetic-bot-chat-visual.md`](artifacts/synthetic-bot-chat-visual.md)
- [`../assets/images/generated/ndt-assistant-demo-chat.png`](../assets/images/generated/ndt-assistant-demo-chat.png)

Shows the chat-shaped interaction surface of the assistant in a synthetic Telegram-like screenshot built for public documentation.

### Synthetic Power App support output example
- [`artifacts/synthetic-power-app-output-example.md`](artifacts/synthetic-power-app-output-example.md)
- [`artifacts/synthetic-output/app_structure.sample.json`](artifacts/synthetic-output/app_structure.sample.json)
- [`artifacts/synthetic-output/edges.sample.json`](artifacts/synthetic-output/edges.sample.json)
- [`artifacts/synthetic-output/datasources_index.sample.json`](artifacts/synthetic-output/datasources_index.sample.json)
- [`artifacts/synthetic-output/golden_context.sample.txt`](artifacts/synthetic-output/golden_context.sample.txt)

Shows the output shape produced by the extractor in a synthetic but structurally faithful form.

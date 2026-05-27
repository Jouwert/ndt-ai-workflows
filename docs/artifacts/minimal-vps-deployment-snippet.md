# Minimal VPS deployment snippet

This deployment shape keeps the transformer PoC small, inspectable, and manually controllable.

## Compose file
See [`minimal-vps-compose.yaml`](minimal-vps-compose.yaml).

```yaml
services:
  transformer:
    container_name: ndt-transformer
    build:
      context: ./app
    working_dir: /app
    env_file:
      - ./env/transformer.env
    volumes:
      - ./app:/app
      - ./config:/app/config
      - ./data/mappings:/app/data/mappings
      - ./data/state:/app/data/state
      - ./data/logs:/app/data/logs
      - ./data/tmp:/app/data/tmp
    restart: "no"
    command: ["python", "main.py", "--help"]
```

## Design choices

### One service
The deployment stays focused on the transformer itself.
There are no extra sidecars or orchestration layers in this PoC shape.

### Mounted state
The container keeps mounted directories for:
- configuration
- mapping state
- runtime state
- logs
- temporary files

That makes the flow easier to inspect and easier to recover.

### Host env file
The environment file stays on the host so secrets and runtime configuration are not baked into the image.

### Manual restart policy
`restart: "no"` is deliberate.
This PoC is run under manual control instead of pretending it is already an always-on production service.

## Operational shape

```text
VPS
  -> one transformer container
  -> mounted state on host
  -> controlled runs for sync and inspection
```

## Why this fits the workflow
This setup matches the rest of the NDT assistant design:
- bounded scope
- self-hosted control
- persistent transformation state
- no unnecessary platform sprawl

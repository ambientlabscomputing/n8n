# n8n

[n8n](https://n8n.io) is a workflow automation platform. This Underleaf app deploys n8n from the official Docker image with persistent storage for workflows and credentials.

## Deploy with Underleaf

```bash
ufctl deploy gh:ambientlabscomputing/n8n
```

The `.underleaf/deploy.yaml` manifest uses `image:` to pull the official `n8nio/n8n:latest` image — no build step required.

## Verify

```bash
# Health / editor UI
curl http://<your-server>:5678/healthz

# Or open the n8n editor in a browser
open http://<your-server>:5678
```

## Data Persistence

A named Docker volume (`n8n_data`) is mounted at `/home/node/.n8n` inside the container. This stores:

- Workflows and credentials (SQLite database by default)
- Encryption keys
- Installed community nodes

The volume survives container restarts and redeployments.

## Environment Variables

The deploy manifest sets a few defaults. You can override or extend them as needed:

| Variable | Default | Description |
|---|---|---|
| `NODE_ENV` | `production` | Node.js environment |
| `N8N_PORT` | `5678` | Port n8n listens on |
| `GENERIC_TIMEZONE` | `UTC` | Timezone for scheduling |

See the [n8n environment variables reference](https://docs.n8n.io/hosting/configuration/environment-variables/) for the full list.

## Project Layout

```
.underleaf/deploy.yaml   # Underleaf manifest
README.md                # This file
```
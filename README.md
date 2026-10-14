# n8n-docker

Minimal configuration to self-host [n8n](https://n8n.io) with Docker — locally or on
Railway — set to Bangkok time and with workflows persisted on a volume.

## Run locally

```bash
docker compose up -d
# http://localhost:5678
```

For local use without HTTPS, override `N8N_PROTOCOL=http` and drop the two
`RAILWAY_PUBLIC_DOMAIN` lines in `docker-compose.yml`.

## Deploy on Railway

Deploy the repo; Railway builds the `Dockerfile` and injects `RAILWAY_PUBLIC_DOMAIN`, which
`WEBHOOK_URL` and `N8N_EDITOR_BASE_URL` use so webhook URLs point at the public domain.
Attach a volume at `/home/node/.n8n`, otherwise workflows and credentials are lost on redeploy.

## Notes

- `n8nio/n8n:latest` is used for simplicity; pin a version tag for production.
- Set `N8N_ENCRYPTION_KEY` yourself and keep it — credentials saved by n8n cannot be
  decrypted without it.

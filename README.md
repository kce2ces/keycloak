# IAM Configuration

This repository contains the Docker Compose and Keycloak configuration for Identity and Access Management (IAM).

## Structure
- `docker-compose.yml` — Service orchestration
- `keycloak/` — Keycloak realm and client configs
- `postgres/` — Postgres database configs (excluding runtime data)
- `whitestone/` — Project-specific extensions
- `.env` / `.env.secret` — Ignored for security
- `backups/` — Ignored, local only

## Usage
1. Create `.env` and `.env.secret` locally with credentials.
2. Run:
   ```bash
   docker compose up -d

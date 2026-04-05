# Morgenruf — Docker Compose

Quickest way to self-host Morgenruf on any Linux/Mac server.

## Requirements
- Docker + Docker Compose
- A domain with HTTPS (ngrok or Cloudflare Tunnel work for local dev)

## Setup

```bash
# 1. Clone this repo
git clone https://github.com/morgenruf/deploy
cd deploy/docker

# 2. Configure
cp .env.example .env
nano .env   # fill in SLACK_CLIENT_ID, SLACK_CLIENT_SECRET, etc.

# 3. Start
docker compose up -d

# 4. Check health
curl http://localhost:3000/healthz
```

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `SLACK_CLIENT_ID` | ✅ | Slack app client ID |
| `SLACK_CLIENT_SECRET` | ✅ | Slack app client secret |
| `SLACK_SIGNING_SECRET` | ✅ | Slack app signing secret |
| `APP_URL` | ✅ | Public HTTPS URL (e.g. https://standup.mycompany.com) |
| `DATABASE_URL` | ✅ | PostgreSQL URL (auto-set if using bundled postgres) |
| `FLASK_SECRET_KEY` | ✅ | Run: `openssl rand -hex 32` |
| `OPENAI_API_KEY` | ❌ | For AI standup summaries |
| `RESEND_API_KEY` | ❌ | For welcome emails |

## Expose to Slack (local dev)

```bash
# Option A: Cloudflare Tunnel (free)
cloudflared tunnel --url http://localhost:3000

# Option B: ngrok
ngrok http 3000
```

Use the HTTPS URL as your `APP_URL` and in Slack app settings.

## Update

```bash
docker compose pull && docker compose up -d
```

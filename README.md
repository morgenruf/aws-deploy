# Morgenruf — Deploy

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Release](https://img.shields.io/github/v/release/morgenruf/morgenruf?label=morgenruf&color=brightgreen)](https://github.com/morgenruf/morgenruf/releases)

One-click deployment templates for [Morgenruf](https://morgenruf.dev) — the open-source self-hosted Slack standup bot.

## 🚀 Deploy Options

| Method | Cost | Complexity | Best For |
|--------|------|------------|----------|
| [**AWS Starter**](./aws/) | ~$15/mo | Low | Small teams |
| [**AWS Production**](./aws/) | ~$25/mo | Low | Growing teams |
| [**Helm (k8s)**](./helm/) | Infra cost | Medium | k8s users |
| [**Docker Compose**](./docker/) | Infra cost | Low | Self-hosted |

---

## ☁️ AWS — One-Click CloudFormation

### Starter (~$15/mo)
EC2 t3.small + docker-compose. Single server, zero management overhead.

[![Launch Starter](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=morgenruf-starter&templateURL=https://raw.githubusercontent.com/morgenruf/deploy/main/aws/starter.yaml)

### Production (~$25/mo)
ECS Fargate Spot + RDS t4g.micro + ALB. Auto-healing, no servers to manage.

[![Launch Production](https://s3.amazonaws.com/cloudformation-examples/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=morgenruf-prod&templateURL=https://raw.githubusercontent.com/morgenruf/deploy/main/aws/production.yaml)

→ [Full AWS setup guide](./aws/README.md)

---

## ⎈ Helm (Kubernetes)

```bash
helm repo add morgenruf https://charts.morgenruf.dev
helm repo update
helm install morgenruf morgenruf/morgenruf \
  --set slack.clientId=YOUR_CLIENT_ID \
  --set slack.clientSecret=YOUR_SECRET \
  --set slack.signingSecret=YOUR_SIGNING_SECRET \
  --set app.url=https://your-domain.com \
  --set externalDatabase.url=postgresql://user:pass@host:5432/morgenruf \
  --set flaskSecretKey=$(openssl rand -hex 32)
```

→ [Full Helm guide](./helm/README.md)

---

## 🐳 Docker Compose

```bash
git clone https://github.com/morgenruf/deploy
cd deploy/docker
cp .env.example .env   # fill in your Slack credentials
docker compose up -d
```

→ [Full Docker Compose guide](./docker/README.md)

---

## Links

- 🌐 [morgenruf.dev](https://morgenruf.dev)
- 📖 [Docs](https://docs.morgenruf.dev)
- 💻 [Source](https://github.com/morgenruf/morgenruf)
- 📦 [Helm Charts](https://github.com/morgenruf/helm-charts)

# Morgenruf — Helm Chart

Deploy Morgenruf on any Kubernetes cluster.

## Install

```bash
helm repo add morgenruf https://charts.morgenruf.dev
helm repo update

helm install morgenruf morgenruf/morgenruf \
  --namespace morgenruf --create-namespace \
  --set slack.clientId=YOUR_CLIENT_ID \
  --set slack.clientSecret=YOUR_CLIENT_SECRET \
  --set slack.signingSecret=YOUR_SIGNING_SECRET \
  --set app.url=https://your-domain.com \
  --set externalDatabase.url=postgresql://user:pass@host:5432/morgenruf \
  --set flaskSecretKey=$(openssl rand -hex 32)
```

## Upgrade

```bash
helm repo update
helm upgrade morgenruf morgenruf/morgenruf
```

## Full values reference

See [charts.morgenruf.dev](https://charts.morgenruf.dev) or:

```bash
helm show values morgenruf/morgenruf
```

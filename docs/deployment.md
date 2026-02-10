# Deployment

## Initial Setup

1. Deploy the original Grafana Stack template from Railway:

   https://railway.com/deploy/grafana-stack

2. Once deployed, go to each service's settings in the Railway dashboard
3. Under **Source**, change the repository to your forked version of this repo
4. Redeploy all services

This ensures Railway provisions the infrastructure (volumes, networking, env vars) from the official template, and then your fork takes over with custom configs, dashboards, and alerting.

## Environment Variables

These are set directly in the Railway dashboard per service (not in the repo, since they contain secrets):

### Grafana

| Variable | Description | Example |
|----------|-------------|---------|
| `GF_SECURITY_ADMIN_USER` | Admin username | `admin` |
| `GF_SECURITY_ADMIN_PASSWORD` | Admin password | Auto-generated |
| `GF_DEFAULT_INSTANCE_NAME` | Instance name | `Grafana` |
| `GF_INSTALL_PLUGINS` | Comma-separated plugins | See docker-compose.yml |
| `LOKI_INTERNAL_URL` | Internal Loki URL | `http://loki:3100` |
| `PROMETHEUS_INTERNAL_URL` | Internal Prometheus URL | `http://prometheus:9090` |
| `TEMPO_INTERNAL_URL` | Internal Tempo URL | `http://tempo:3200` |

For SMTP and alerting variables, see the [Grafana service docs](services/grafana.md).

## Redeploying

After pushing changes to your fork, Railway will automatically redeploy the affected services.

## Version Control

Each service pins a Docker image version via `ARG VERSION` in its Dockerfile:

- Grafana: `11.5.2`
- Prometheus: `v3.2.1`
- Loki: `3.4`
- Tempo: `2.9.0`

To upgrade, update the `ARG VERSION` line in the corresponding Dockerfile and redeploy.

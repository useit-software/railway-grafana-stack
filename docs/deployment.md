# Deployment Guide

## Initial Deployment

1. Go to the original Railway template and deploy it:
   **https://railway.com/deploy/grafana-stack**

2. Once deployed, fork this repository to your own GitHub account.

3. In the Railway dashboard, for each service (Grafana, Prometheus, Loki, Tempo), change the **repo source** to your forked repository:
   - Go to the service settings
   - Under "Source", click "Connect Repo"
   - Select your forked repository
   - Set the appropriate root directory for each service (`/grafana`, `/prometheus`, `/loki`, `/tempo`)

4. Railway will redeploy each service using your fork, which includes all custom provisioning (dashboards, alerts, datasources).

## Environment Variables

The following environment variables are configured in the Grafana service:

| Variable | Description | Default |
|----------|-------------|---------|
| `GF_SECURITY_ADMIN_USER` | Grafana admin username | `admin` |
| `GF_SECURITY_ADMIN_PASSWORD` | Grafana admin password | `yourpassword123` |
| `GF_DEFAULT_INSTANCE_NAME` | Grafana instance name | `Grafana` |
| `GF_INSTALL_PLUGINS` | Comma-separated plugins to install | See docker-compose.yml |
| `LOKI_INTERNAL_URL` | Internal URL for Loki | `http://loki:3100` |
| `PROMETHEUS_INTERNAL_URL` | Internal URL for Prometheus | `http://prometheus:9090` |
| `TEMPO_INTERNAL_URL` | Internal URL for Tempo | `http://tempo:3200` |
| `ALERT_EMAIL_ADDRESSES` | Email addresses for alert notifications | Required for alerting |

## Updating

After making changes to your fork (dashboards, alerts, configs), push to your repository. Railway will automatically redeploy the affected services.

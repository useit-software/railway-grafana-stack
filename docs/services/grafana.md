# Grafana

Central visualization and dashboarding platform.

- **Image**: `grafana/grafana-oss:11.5.2`
- **Port**: `3000`
- **Volume**: `grafana_data:/var/lib/grafana`

## Provisioning

All provisioning files are copied into the container at build time via the Dockerfile (`grafana/dockerfile`).

### Datasources

Configured in `grafana/provisioning/datasources/datasources.yml`. Three datasources are pre-configured:

| Name | Type | UID | URL | Default |
|------|------|-----|-----|---------|
| Loki | loki | `grafana_lokiq` | `$LOKI_INTERNAL_URL` | Yes |
| Prometheus | prometheus | `grafana_prometheus` | `$PROMETHEUS_INTERNAL_URL` | No |
| Tempo | tempo | `grafana_tempo` | `$TEMPO_INTERNAL_URL` | No |

### Dashboards

Dashboard provisioning is configured in `grafana/provisioning/dashboards/dashboards.yml`. It loads all JSON files from the `json/` subdirectory.

Dashboard JSON files go in `grafana/provisioning/dashboards/json/`.

See [Dashboards documentation](../dashboards.md) for details on each dashboard.

### Alerting

Alerting is configured via three files in `grafana/provisioning/alerting/`:

- **`contactpoints.yml`**: Defines an `email-team` contact point that sends alerts to `${ALERT_EMAIL_ADDRESSES}`
- **`notification-policies.yml`**: Routes alerts with `team=backend` label to the `email-team` contact point, grouped by `alertname` and `project_uuid`
- **`portal_light_alerts.yml`**: Defines an alert rule `Portal Lights Count Dropped` that fires when `portal_lights_up` drops compared to the previous minute

## SMTP Configuration

For email alerts to work, you must set the following environment variables in the Grafana service on Railway:

| Variable | Description | Example |
|----------|-------------|---------|
| `GF_SMTP_ENABLED` | Enable SMTP | `true` |
| `GF_SMTP_HOST` | SMTP server host and port | `smtp.gmail.com:587` |
| `GF_SMTP_USER` | SMTP username | `your-email@gmail.com` |
| `GF_SMTP_PASSWORD` | SMTP password or app password | `your-app-password` |
| `GF_SMTP_FROM_ADDRESS` | Sender email address | `your-email@gmail.com` |
| `GF_SMTP_FROM_NAME` | Sender display name | `Grafana Alerts` |
| `ALERT_EMAIL_ADDRESSES` | Recipient addresses for the `email-team` contact point | `team@example.com` |

These are set as environment variables directly in Railway (not in the Dockerfile or docker-compose), since they contain secrets.

## Installed Plugins

- `grafana-simple-json-datasource`
- `grafana-piechart-panel`
- `grafana-worldmap-panel`
- `grafana-clock-panel`

# Prometheus

Time-series database for metrics collection and storage.

- **Image**: `prom/prometheus:v3.2.1`
- **Port**: `9090`
- **Volume**: `prometheus_data:/prometheus`

## Configuration

Configured in `prometheus/prom.yml`.

- **Scrape interval**: 15s
- **OTLP receiver**: Enabled via `--web.enable-otlp-receiver` flag

### Scrape Configs

By default, Prometheus scrapes itself at `localhost:9090`.

To add your own services, edit `prometheus/prom.yml` and add scrape targets:

```yaml
scrape_configs:
  - job_name: 'your-service'
    scheme: https
    static_configs:
      - targets: ['your-service-url']
    basic_auth:
      username: YOUR_USERNAME
      password: YOUR_PASSWORD
```

## Metrics Used

The following custom metrics are used in dashboards and alerts:

| Metric | Description |
|--------|-------------|
| `portal_lights_up` | Raw count of portal lights up per project |
| `portal_lights_up_ratio` | Ratio of portal lights up per project |
| `assignations_created_ratio` | Ratio of assignations created per project |
| `devices_up_ratio` | Ratio of devices up per project |

All metrics are labeled with `project_uuid`.

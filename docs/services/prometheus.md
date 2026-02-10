# Prometheus

Time-series database for metrics collection and storage.

- **Image**: `prom/prometheus:v3.2.1`
- **Port**: `9090`
- **Volume**: `prometheus_data:/prometheus`

## Configuration

Config file: `prometheus/prom.yml`

- **Scrape interval**: 15s
- **OTLP receiver**: Enabled (`--web.enable-otlp-receiver`)

### Scrape Targets

By default, Prometheus only scrapes itself:

```yaml
scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']
```

To add your own services, edit `prometheus/prom.yml` and add a new `job_name` block:

```yaml
- job_name: 'your-service'
  scheme: https
  static_configs:
    - targets: ['your-service-url']
  basic_auth:
    username: YOUR_USERNAME
    password: YOUR_PASSWORD
```

## Metrics Used

The following custom metrics are queried in the provisioned dashboards:

| Metric | Dashboard Panel |
|--------|----------------|
| `portal_lights_up_ratio` | PORTAL LIGHTS UP |
| `assignations_created_ratio` | ASSIGNATIONS CREATED |
| `devices_up_ratio` | DEVICES UP |

The `portal_lights_up` metric is also used in the alert rule `Portal Lights Count Dropped`.

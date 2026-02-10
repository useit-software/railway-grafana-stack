# Dashboards

All provisioned dashboards are stored as JSON files in `grafana/provisioning/dashboards/json/`.

The provisioning config (`grafana/provisioning/dashboards/dashboards.yml`) automatically loads all JSON files from that directory.

## Main SH Dashboard

- **File**: `grafana/provisioning/dashboards/json/main-sh-dashboard.json`
- **UID**: `main-sh-dashboard`
- **Datasource**: Prometheus (`grafana_prometheus`)
- **Refresh**: 30s
- **Time range**: Last 6 hours

### Panels

#### 1. PORTAL LIGHTS UP

- **Type**: Time series
- **Query**: `portal_lights_up_ratio`
- **Legend**: One line per `project_uuid`
- **Y-axis**: Min 0, Max 30

Displays the portal lights up ratio over time, with a separate line for each project.

#### 2. ASSIGNATIONS CREATED

- **Type**: Time series
- **Query**: `assignations_created_ratio`
- **Legend**: One line per `project_uuid`
- **Y-axis**: Min 0, Max 20

Displays the assignations created ratio over time, with a separate line for each project.

#### 3. DEVICES UP

- **Type**: Time series
- **Query**: `devices_up_ratio`
- **Legend**: One line per `project_uuid`
- **Y-axis**: Min 0, Max 60

Displays the devices up ratio over time, with a separate line for each project.

## Adding a New Dashboard

1. Create a JSON file in `grafana/provisioning/dashboards/json/`
2. Use a unique `uid` for the dashboard
3. Reference datasources by their UID (e.g., `grafana_prometheus`)
4. Push and redeploy

You can also export a dashboard from the Grafana UI (Share > Export > Save to file) and place the JSON in the directory.

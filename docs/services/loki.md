# Loki

Log aggregation system.

- **Image**: `grafana/loki:3.4`
- **Port**: `3100`
- **Volume**: `loki_data:/loki`

## Configuration

Config file: `loki/loki.yml`

- **Auth**: Disabled (`auth_enabled: false`)
- **Storage**: Filesystem with TSDB index
- **Schema**: v13
- **Retention**: 720h (30 days)
- **Compaction interval**: 10m

### Storage Layout

| Path | Purpose |
|------|---------|
| `/loki/tsdb-index` | Active TSDB index |
| `/loki/tsdb-cache` | TSDB cache |
| `/loki/chunks` | Log chunk data |
| `/loki/compactor` | Compactor working directory |

## Sending Logs

Point your application's logging library to `http://loki:3100` (internal) or the Railway-provided URL (external).

Example with [winston-loki](https://www.npmjs.com/package/winston-loki) (Node.js):

```javascript
import LokiTransport from 'winston-loki';

new LokiTransport({
  host: 'http://loki:3100',
  labels: { app: 'my-service' }
});
```

You can also use [Locomotive](https://railway.com/template/jP9r-f) to ingest all Railway service logs into Loki without code changes.

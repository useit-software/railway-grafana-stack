# Loki

Log aggregation system.

- **Image**: `grafana/loki:3.4`
- **Port**: `3100`
- **Volume**: `loki_data:/loki`

## Configuration

Configured in `loki/loki.yml`.

- **Auth**: Disabled (`auth_enabled: false`)
- **Storage**: Filesystem with TSDB index
- **Schema**: v13 (from 2025-01-01)
- **Retention**: 720h (30 days)
- **Compaction interval**: 10m

### Storage Paths

| Path | Purpose |
|------|---------|
| `/loki/tsdb-index` | Active TSDB index directory |
| `/loki/tsdb-cache` | TSDB cache |
| `/loki/chunks` | Log chunks (filesystem object store) |
| `/loki/compactor` | Compactor working directory |

## Sending Logs to Loki

Use any Loki-compatible client. The example API uses `winston-loki`:

```javascript
import LokiTransport from 'winston-loki';

new LokiTransport({
  host: 'http://loki:3100',
  labels: { app: 'your-app' }
});
```

You can also use [Locomotive](https://railway.com/template/jP9r-f) to ingest Railway service logs into Loki without code changes.

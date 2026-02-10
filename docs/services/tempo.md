# Tempo

Distributed tracing backend.

- **Image**: `grafana/tempo:2.9.0`
- **Volume**: `tempo_data:/var/tempo`

## Ports

| Port | Protocol | Purpose |
|------|----------|---------|
| `3200` | HTTP | Query API |
| `4317` | gRPC | OTLP ingest |
| `4318` | HTTP | OTLP ingest |

## Configuration

Config file: `tempo/tempo.yml`

- **Storage**: Local filesystem at `/var/tempo/traces`
- **Log received spans**: Enabled

## Sending Traces

Use OpenTelemetry SDKs to send traces to Tempo. The ingest endpoint for HTTP is:

```
http://tempo:4318/v1/traces
```

For gRPC:

```
http://tempo:4317
```

### Node.js Example

```javascript
import { OTLPTraceExporter } from '@opentelemetry/exporter-trace-otlp-http';

const exporter = new OTLPTraceExporter({
  url: 'http://tempo:4318/v1/traces'
});
```

See `examples/api/tracer.js` for a full working example.

### Known Issues

Tempo v2.10.0 has a bug where the `compactor` config block is not recognized. This project is pinned to v2.9.0 until a fix is released.

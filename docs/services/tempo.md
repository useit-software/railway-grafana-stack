# Tempo

Distributed tracing backend.

- **Image**: `grafana/tempo:2.9.0`
- **Ports**:
  - `3200` - HTTP server for querying
  - `4317` - gRPC server for OTLP ingest
  - `4318` - HTTP server for OTLP ingest
- **Volume**: `tempo_data:/var/tempo`

> **Note**: Tempo v2.10.0 has a known issue with the `compactor` config block. This project is pinned to v2.9.0.

## Configuration

Configured in `tempo/tempo.yml`.

- **Storage**: Local filesystem at `/var/tempo/traces`
- **Receivers**: OTLP over gRPC (`:4317`) and HTTP (`:4318`)
- **Span logging**: Enabled

## Sending Traces to Tempo

Use OpenTelemetry SDK. The HTTP ingest endpoint is:

```
http://tempo:4318/v1/traces
```

Example with `@opentelemetry/exporter-trace-otlp-http`:

```javascript
import { OTLPTraceExporter } from "@opentelemetry/exporter-trace-otlp-http";

const traceExporter = new OTLPTraceExporter({
  url: "http://tempo:4318/v1/traces"
});
```

See `examples/api/tracer.js` for a complete working example.

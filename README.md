# Padhaipal Infra

Shared infrastructure configuration for the Padhaipal Railway project.

This repository contains the OpenTelemetry internal collector used by both:

- `wabot-sketch`
- `pp-sketch`

Architecture:

`wabot` + `pp` -> `alloy` (internal collector) -> Grafana Cloud

## Deploy on Railway

1. Create a Railway service from `alloy/`.
2. Add env vars on that service:
   - `GRAFANA_CLOUD_OTLP_ENDPOINT`
   - `GRAFANA_CLOUD_INSTANCE_ID`
   - `GRAFANA_CLOUD_API_TOKEN`
3. Deploy.

## App service env vars

Set these on both `wabot` and `pp` services:

- `OTEL_EXPORTER_OTLP_ENDPOINT=http://alloy.railway.internal:4318`
- `OTEL_EXPORTER_OTLP_PROTOCOL=http/protobuf`
- `OTEL_TRACES_EXPORTER=otlp`
- `OTEL_METRICS_EXPORTER=otlp`
- `OTEL_LOGS_EXPORTER=otlp`

Set service-specific name:

- wabot: `OTEL_SERVICE_NAME=wabot`
- pp: `OTEL_SERVICE_NAME=pp`

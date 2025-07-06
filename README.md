# OpenTelemetry Collector Setup

This project sets up an OpenTelemetry Collector using Docker Compose. It includes configuration for receiving telemetry data over OTLP (gRPC and HTTP) and exposes a Prometheus-compatible metrics endpoint.

## 📦 Services

### `otel-collector`
This service runs the OpenTelemetry Collector with a custom configuration.

- **Image**: `otel/opentelemetry-collector-contrib:latest`
- **Command**: Uses the custom config file mounted from the host.
- **Ports**:
  - `4317`: OTLP gRPC receiver
  - `4318`: OTLP HTTP receiver
  - `8889`: Prometheus metrics endpoint

### 🔧 Volumes

- The file `otel-collector-config.yaml` is mounted into the container at `/etc/otel-collector-config.yaml`.

Make sure your local file exists and is properly configured before starting the service.

## 🔗 Network

The collector connects to an **external Docker network** named `super_network`. Ensure this network exists before running the stack:

```
docker network create super_network
```

## 🚀 Getting Started

1. Clone this repository or copy the `docker-compose.yaml` and `otel-collector-config.yaml` into your project directory.

2. Create the external Docker network if you haven’t already:

    ```
    docker network create super_network
    ```

3. Start the service:

    ```
    docker compose up -d
    ```

4. Check that the collector is running:

    ```
    docker compose ps
    ```

5. Inspect logs (optional):

    ```
    docker compose logs -f otel-collector
    ```

## 📁 File Structure

```
.
├── docker-compose.yaml
└── otel-collector-config.yaml
```

## 🧪 Testing

You can test OTLP ingestion with tools like [OpenTelemetry Demo](https://github.com/open-telemetry/opentelemetry-demo), `curl`, or `otel-cli`.

## 📝 Notes

- Make sure the `otel-collector-config.yaml` file is valid and tailored to your observability pipeline (e.g., exporters like Prometheus, Jaeger, etc.).
- This setup assumes you want to use an existing shared Docker network (`super_network`). If you don't, remove or modify the `networks` section.

## 📚 References

- [OpenTelemetry Collector](https://opentelemetry.io/docs/collector/)
- [OpenTelemetry Collector Contrib GitHub](https://github.com/open-telemetry/opentelemetry-collector-contrib)

---

Happy Observing! 🚀

# OCI Monitoring Datadog Forwarder

This is a **sample** program to forward metrics data from OCI Monitoring to Datadog.

## How to use

### OCI Functions mode

Set config.(func.yaml)

```yaml
schema_version: 20180708
name: datadog-monitoring-integration
version: 0.0.1
runtime: python
build_image: fnproject/python:3.9-dev
run_image: fnproject/python:3.9
entrypoint: /python/bin/fdk /function/func.py handler
memory: 256
config:
  DATADOG_METRICS_API_ENDPOINT: <your-datadog-metrics-api-endpoint>
  DATADOG_API_KEY: <your-datadog-api-key>
```

Deploy function.

```bash
export APP_NAME=<your-application-name>
fn deploy --app $APP_NAME [--no-bump]
```

### Local debug mode

Set the environment values.

```bash
export DATADOG_METRICS_API_ENDPOINT=<your-datadog-metrics-api-endpoint>
export DATADOG_API_KEY=<your-datadog-api-key>
# Optional
export LOGGING_LEVEL=DEBUG
```

Execute the Python program.

```bash
python3 func.py
```

## Configs

- Required
  - DATADOG_METRICS_API_ENDPOINT
  - DATADOG_API_KEY
- Optional
  - FORWARD_TO_DATADOG
  - LOGGING_LEVEL
  - ENABLE_TRACING

### DATADOG_METRICS_API_ENDPOINT

You can check the metrics endpoint: [https://docs.datadoghq.com/ja/api/latest/metrics/](https://docs.datadoghq.com/ja/api/latest/metrics/)

### DATADOG_API_KEY

Obtain your Datadog API KEY and set value.

### FORWARD_TO_DATADOG

Whether to forward metrics to Datadog. Mainly used for debug purposes.

### LOGGING_LEVEL

Log level.

### ENABLE_TRACING

Whether to output the contents of the Exception to the stack trace or not.

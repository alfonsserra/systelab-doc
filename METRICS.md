# Application Metrics

In today's world, metrics collection is mandatory in order to effective monitoring. 

To do so, it is quite common to use Prometheus and Grafana: Prometheus is a powerful metrics collection and alerting system, and Grafana is one of the best visualization 
tools which can be used with Prometheus. 

In order to setup an initial environment, read to the documentation at the [systelab/prometheus-monitoring](https://github.com/systelab/prometheus-monitoring) repository.

## Design Considerations
It is usually implemented as an API endpoint (e.g. HTTP /metrics) that returns the metrics of the service in an specific format.
It is possible to have different endpoints each one with metrics related to a specific category.
It is quite common to have an API endpoint (e.g. HTTP /metrics/prometehus) to return metrics in Prometheus format.


### Prometheus metrics / OpenMetrics format
Prometheus metrics text-based format is line oriented. Lines are separated by a line feed character (\n). 
The last line must end with a line feed character. Empty lines are ignored.

A metric is composed by several fields:

- Metric name
- Any number of labels (can be 0), represented as a key-value array
- Current metric value
- Optional metric timestamp

A Prometheus metric can be as simple as:

```
http_requests 2
```

Or, including all the mentioned components:

```
http_requests_total{method="post",code="400"}  3   1395066363000
```

Metric output is typically preceded with # HELP and # TYPE metadata lines.

The HELP string identifies the metric name and a brief description of it. The TYPE string identifies the type of metric. 
If there’s no TYPE before a metric, the metric is set to untyped. Everything else that starts with a # is parsed as a comment.

```
# HELP metric_name Description of the metric
# TYPE metric_name type
# Comment that's not parsed by prometheus
http_requests_total{method="post",code="400"}  3   1395066363000
```
Prometheus metrics / OpenMetrics represents multi-dimensional data using labels or tags:

```
traefik_entrypoint_request_duration_seconds_count{code="404",entrypoint="traefik",method="GET",protocol="http"} 44
```

The key advantage of this notation is that all these dimensional labels can be used by the metric consumer to dynamically 
perform metric aggregation, scoping and segmentation. 

Check the [prometheus repository official documentation for metrics format](https://github.com/prometheus/docs/blob/master/content/docs/instrumenting/exposition_formats.md).

Using these labels and metadata to slice and dice your metrics is an absolute requirement when deploying the application in production, specially if it involves many instances.

## Implementations
Check [MicroProfile Metrics](https://github.com/eclipse/microprofile-metrics) and [Micrometer](https://micrometer.io/docs/registry/prometheus)



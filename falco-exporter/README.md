# falco-exporter Helm Chart

[falco-exporter](https://github.com/falcosecurity/falco-exporter) is a Prometheus Metrics Exporter for Falco output events.

Before using this chart, you need [Falco installed](https://falco.org/docs/installation/) and running with the [gRPC Output](https://falco.org/docs/grpc/) enabled (over Unix socket by default).

This chart is compatible with the [Falco Chart](https://github.com/falcosecurity/charts/tree/master/falco) version `v1.2.0` or greater. Instructions to enable the gRPC Output in the Falco Helm Chart can be found [here](https://github.com/falcosecurity/charts/tree/master/falco#enabling-grpc). We also strongly recommend using [gRPC over Unix socket](https://github.com/falcosecurity/charts/tree/master/falco#grpc-over-unix-socket-default).


## Introduction

The chart deploys **falco-exporter** as Daemon Set on your the Kubernetes cluster. If a [Prometheus installation](https://github.com/helm/charts/tree/master/stable/prometheus) is running within your cluster, metrics provided by **falco-exporter** will be automatically discovered.

## Adding `falcosecurity` repository

Prior to installing the chart, add the `falcosecurity` charts repository:

```bash
helm repo add falcosecurity https://falcosecurity.github.io/charts
helm repo update
```

## Installing the Chart

To install the chart with the release name `falco-exporter` run:

```bash
helm install falco-exporter falcosecurity/falco-exporter
```

After a few seconds, **falco-exporter** should be running.

> **Tip**: List all releases using `helm list`, a release is a name used to track a specific deployment

## Uninstalling the Chart

To uninstall the `falco-exporter` deployment:

```bash
helm uninstall falco-exporter
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the main configurable parameters of the chart and their default values.

| Parameter                        | Description                                                         | Default                                        |
| ---                              | ---                                                                 | ---                                            |
| `image.repository`               | The image repository to pull from                                   | `falcosecurity/falco-exporter`                 |
| `image.tag`                      | The image tag to pull                                               | `0.3.0`                                        |
| `image.pullPolicy`               | The image pull policy                                               | `IfNotPresent`                                 |
| `falco.grpcUnixSocketPath`       | Unix socket path for connecting to a Falco gRPC server              | `unix:///var/run/falco/falco.sock`             |
| `falco.grpcTimeout`              | The image tag to pull                                               | `2m`                                           |
| `serviceMonitor.enabled`         | Enabled deployment of a Prometheus operator Service Monitor         | `false`                                        |
| `serviceMonitor.additionalLabels`| Add additional Labels to the Service Monitor                        | `{}`                                           |
| `serviceMonitor.interval`        | Specify a user defined interval for the Service Monitor             | `""`                                           |
| `serviceMonitor.scrapeTimeout`   | Specify a user defined scrape timeout for the Service Monitor       | `""`                                           |

Please, refer to [values.yaml](./values.yaml) for the full list of configurable parameters.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
helm install falco --set falco.jsonOutput=true falcosecurity/falco
```

Alternatively, a YAML file that specifies the parameters' values can be provided while installing the chart. For example,

```bash
helm install falco-exporter -f values.yaml falcosecurity/falco-exporter
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Using falco-exporter with Grafana

See the [Grafana section](https://github.com/falcosecurity/falco-exporter#grafana) in the [falco-exporter](https://github.com/falcosecurity/falco-exporter) documentation.

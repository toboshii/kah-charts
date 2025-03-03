# adguard-home

![Version: 5.0.3](https://img.shields.io/badge/Version-5.0.3-informational?style=flat-square) ![AppVersion: v0.106.3](https://img.shields.io/badge/AppVersion-v0.106.3-informational?style=flat-square)

DNS proxy as ad-blocker for local network

**This chart is not maintained by the upstream project and any issues with the chart should be raised [here](https://github.com/k8s-at-home/charts/issues/new/choose)**

## Source Code

* <https://github.com/AdguardTeam/AdGuardHome>

## Requirements

Kubernetes: `>=1.16.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| https://library-charts.k8s-at-home.com | common | 4.0.1 |

## TL;DR

```console
helm repo add k8s-at-home https://k8s-at-home.com/charts/
helm repo update
helm install adguard-home k8s-at-home/adguard-home
```

## Installing the Chart

To install the chart with the release name `adguard-home`

```console
helm install adguard-home k8s-at-home/adguard-home
```

## Uninstalling the Chart

To uninstall the `adguard-home` deployment

```console
helm uninstall adguard-home
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common/values.yaml) from the [common library](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install adguard-home \
  --set env.TZ="America/New York" \
    k8s-at-home/adguard-home
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install adguard-home k8s-at-home/adguard-home -f values.yaml
```

## Custom configuration

N/A

## Values

**Important**: When deploying an application Helm chart you can add more values from our common library chart [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| args | list | `["--config","/opt/adguardhome/conf/AdGuardHome.yaml","--work-dir","/opt/adguardhome/work","--no-check-update"]` | arguments passed to the adguard-home command line. |
| config | string | See values.yaml | AdGuard Home configuration. For a full list of options see https://github.com/AdguardTeam/AdGuardHome/wiki/Configuration. |
| controller.replicas | int | `1` | Number of pods to load balance between |
| env | object | See below | environment variables. |
| env.TZ | string | `"UTC"` | Set the container timezone |
| image.pullPolicy | string | `"IfNotPresent"` | image pull policy |
| image.repository | string | `"adguard/adguardhome"` | image repository |
| image.tag | string | `"v0.106.3"` | image tag |
| initContainers.copy-configmap | object | See values.yaml | Configures an initContainer that copies the configmap to the AdGuardHome conf directory It does NOT overwrite when the file already exists. |
| persistence | object | See values.yaml | Configure persistence settings for the chart under this key. |
| service | object | See values.yaml | Configures service settings for the chart. |

## Changelog

All notable changes to this application Helm chart will be documented in this file but does not include changes from our common library. To read those click [here](https://github.com/k8s-at-home/library-charts/tree/main/charts/stable/common#changelog).

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

### [5.1.0]

#### Removed

- Removed serviceMonitor since AdguardHome doesn't have prometheus metrics. An exporter would be needed instead.

### [5.0.1]

#### Changed

- Add `pullPolicy` to initContainer

### [5.0.0]

#### Changed

- Upgraded the common library dependency to version 4.0.0. This introduced (potentially) breaking changes to `initContainers` and `additionalContainers`. Be sure to check out the [library chart](https://github.com/k8s-at-home/library-charts/blob/common-4.0.0/charts/stable/common/) for the up-to-date values.

### [4.0.1]

#### Fixed

- Fixed the default protocol for the `dns-udp` port.

### [4.0.0]

#### Changed

- **BREAKING**: Upgraded the common library dependency to version 3.0.1. This introduces several breaking changes (`service`, `ingress` and `persistence` keys have been refactored).
  Be sure to check out the [library chart](https://github.com/k8s-at-home/library-charts/blob/common-3.0.0/charts/stable/common/) for the up-to-date values.
- Updated the image tag to v0.106.3.

### [3.3.1]

#### Changed

- Updated `work-dir` arg to point to the correct directory within the container

### [3.0.0]

#### Added

- N/A

#### Changed

- **BREAKING** Migrate Adguard Home to the common library, a lot of configuration has changed.

#### Removed

- N/A

[5.1.0]: #510
[5.0.1]: #501
[5.0.0]: #500
[4.0.1]: #401
[4.0.0]: #400
[3.3.1]: #331
[3.0.0]: #300

## Support

- See the [Docs](https://docs.k8s-at-home.com/our-helm-charts/getting-started/)
- Open an [issue](https://github.com/k8s-at-home/charts/issues/new/choose)
- Ask a [question](https://github.com/k8s-at-home/organization/discussions)
- Join our [Discord](https://discord.gg/sTMX7Vh) community

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.5.0](https://github.com/norwoodj/helm-docs/releases/v1.5.0)

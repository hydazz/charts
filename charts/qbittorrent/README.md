# qBittorrent

<img src="https://avatars.githubusercontent.com/u/2131270" align="right" width="92" alt="qbittorrent logo">

![Version: 0.1.6](https://img.shields.io/badge/Version-0.1.6-informational?style=flat)
![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat)
![AppVersion: 5.1.0](https://img.shields.io/badge/AppVersion-5.1.0-informational?style=flat)

qBittorrent is a bittorrent client programmed in C++ / Qt that uses libtorrent

**Homepage:** <https://charts.hydaz.com/charts/qbittorrent/>

**This chart is not maintained by the upstream project and any issues with the chart should be raised
[here](https://github.com/hydazz/charts/issues/new?assignees=hydazz&labels=bug&template=bug_report.yaml&name=qbittorrent&version=0.1.6)**

## Source Code

* <https://github.com/qbittorrent/qBittorrent>

## Requirements

Kubernetes: `>=1.22.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| <https://bjw-s-labs.github.io/helm-charts> | common | 1.5.1 |

## Installing the Chart

To install the chart with the release name `qbittorrent`

### OCI (Recommended)

```console
helm install qbittorrent oci://ghcr.io/hydazz/charts/qbittorrent
```

### Traditional

```console
helm repo add hydaz https://charts.hydaz.com
helm repo update
helm install qbittorrent hydaz/qbittorrent
```

## Uninstalling the Chart

To uninstall the `qbittorrent` deployment

```console
helm uninstall qbittorrent
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/bjw-s-labs/helm-charts/tree/a081de5/charts/library/common/values.yaml) from the [bjw-s common library](https://github.com/bjw-s-labs/helm-charts/tree/a081de5/charts/library/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install qbittorrent \
  --set env.TZ="America/New York" \
    hydaz/qbittorrent
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install qbittorrent hydaz/qbittorrent -f values.yaml
```

## Custom configuration

## Values

**Important**: When deploying an application Helm chart you can add more values from the bjw-s common library chart [here](https://github.com/bjw-s-labs/helm-charts/tree/a081de5/charts/library/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| gluetun | object | `{"enabled":false,"env":null,"image":{"repository":"ghcr.io/qdm12/gluetun","tag":"v3.40.0"},"secretRef":"qbittorrent-vpn-secret"}` | Gluetun VPN container settings |
| gluetun.enabled | bool | true | Enable Gluetun sidecar |
| gluetun.secretRef | string | qbittorrent-vpn-secret | Secret containing Wireguard or OpenVPN Environment Variables |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"ghcr.io/home-operations/qbittorrent"` | Image repository |
| image.tag | string | `"5.1.0"` | Image tag |
| ingress.main | object | See [values.yaml](./values.yaml) | Enable and configure ingress settings for the chart under this key. |
| persistence.addons.enabled | bool | `true` |  |
| persistence.addons.mountPath | string | `"/addons"` |  |
| persistence.addons.type | string | `"emptyDir"` |  |
| persistence.data | object | See [values.yaml](./values.yaml) | Configure data volume settings for the chart under this key. |
| persistence.downloads | object | See [values.yaml](./values.yaml) | Configure downloads volume settings for the chart under this key. |
| podSecurityContext.fsGroup | int | `1001` |  |
| podSecurityContext.fsGroupChangePolicy | string | `"OnRootMismatch"` |  |
| portForward | object | `{"enabled":false,"env":{"CRON_ENABLED":true,"CRON_SCHEDULE":"*/5 * * * *","GLUETUN_CONTROL_SERVER_HOST":"localhost","GLUETUN_CONTROL_SERVER_PORT":8000,"LOG_TIMESTAMP":false,"QBITTORRENT_HOST":"localhost","QBITTORRENT_WEBUI_PORT":8080},"image":{"repository":"ghcr.io/bjw-s-labs/gluetun-qb-port-sync","tag":"0.0.4"}}` | Port forwarding sync settings |
| portForward.enabled | bool | true | Enable port-forward sidecar |
| portForward.env.GLUETUN_CONTROL_SERVER_HOST | string | See [values.yaml](./values.yaml) | Configure Port forwarding settings under this key.    [ref]](https://github.com/bjw-s-labs/container-images/blob/main/apps/gluetun-qb-port-sync/script.sh) |
| securityContext | object | See [values.yaml](./values.yaml) | Security Context for the qBittorrent container |
| service.main | object | See [values.yaml](./values.yaml) | Configures service settings for the chart. |
| vuetorrent | object | `{"enabled":true,"image":{"repository":"registry.k8s.io/git-sync/git-sync","tag":"v4.4.1"},"link":"vuetorrent","period":"6h","ref":"latest-release","repo":"https://github.com/VueTorrent/VueTorrent.git","root":"/addons"}` | VueTorrent Git sync settings |
| vuetorrent.enabled | bool | true | Enable VueTorrent sidecar (install theme) |

---
Autogenerated from chart metadata using [helm-docs](https://github.com/norwoodj/helm-docs)

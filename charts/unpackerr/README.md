# Unpackerr

<img src="https://unpackerr.zip/img/icon.png" align="right" width="92" alt="unpackerr logo">

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat)
![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat)
![AppVersion: 0.14.5](https://img.shields.io/badge/AppVersion-0.14.5-informational?style=flat)

Unpackerr runs as a daemon on your download host or seedbox. It checks for completed downloads and extracts them so Lidarr, Radarr, Readarr, and Sonarr may import them.

**Homepage:** <https://charts.hydaz.com/charts/unpackerr/>

**This chart is not maintained by the upstream project and any issues with the chart should be raised
[here](https://github.com/hydazz/charts/issues/new?assignees=hydazz&labels=bug&template=bug_report.yaml&name=unpackerr&version=0.1.0)**

## Source Code

* <https://github.com/unpackerr/unpackerr>

## Requirements

Kubernetes: `>=1.22.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| <https://bjw-s-labs.github.io/helm-charts> | common | 1.5.1 |

## Installing the Chart

To install the chart with the release name `unpackerr`

### OCI (Recommended)

```console
helm install unpackerr oci://ghcr.io/hydazz/charts/unpackerr
```

### Traditional

```console
helm repo add hydaz https://charts.hydaz.com
helm repo update
helm install unpackerr hydaz/unpackerr
```

## Uninstalling the Chart

To uninstall the `unpackerr` deployment

```console
helm uninstall unpackerr
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/bjw-s-labs/helm-charts/tree/a081de5/charts/library/common/values.yaml) from the [bjw-s common library](https://github.com/bjw-s-labs/helm-charts/tree/a081de5/charts/library/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install unpackerr \
  --set env.TZ="America/New York" \
    hydaz/unpackerr
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install unpackerr hydaz/unpackerr -f values.yaml
```

## Custom configuration

## Values

**Important**: When deploying an application Helm chart you can add more values from the bjw-s common library chart [here](https://github.com/bjw-s-labs/helm-charts/tree/a081de5/charts/library/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"ghcr.io/unpackerr/unpackerr"` | Image repository |
| image.tag | string | `"0.14.5"` | Image tag |
| persistence.downloads | object | See [values.yaml](./values.yaml) | Configure downloads volume settings for the chart under this key. |
| podSecurityContext.fsGroup | int | `1001` |  |
| podSecurityContext.fsGroupChangePolicy | string | `"OnRootMismatch"` |  |
| securityContext | object | See [values.yaml](./values.yaml) | Security Context for the Unpackerr container |
| service.main | object | See [values.yaml](./values.yaml) | Configures service settings for the chart. |
| unpackerr | object | See [values.yaml](./values.yaml) | Unpackerr configuration [[ref]](https://unpackerr.zip/docs/install/configuration/) |
| unpackerr.folder | list | [] | List of folder configurations to monitor |
| unpackerr.global.activity | bool | false | Display activity in logs |
| unpackerr.global.debug | bool | false | Enable debug logging |
| unpackerr.global.dir_mode | string | "0755" | Directory permissions for extracted folders |
| unpackerr.global.error_stderr | bool | false | Log errors to stderr |
| unpackerr.global.file_mode | string | "0644" | File permissions for extracted files |
| unpackerr.global.interval | string | "2m" | How often to scan for extracted files |
| unpackerr.global.log_file_mb | int | 10 | Maximum log file size in MB |
| unpackerr.global.log_files | int | 10 | Number of log files to retain |
| unpackerr.global.log_queues | string | "1m" | How often to log queue sizes |
| unpackerr.global.parallel | int | 1 | Number of folders to process in parallel |
| unpackerr.global.quiet | bool | false | Enable quiet mode (suppresses most logs) |
| unpackerr.global.retry_delay | string | "5m" | Retry delay when extraction fails |
| unpackerr.global.start_delay | string | "1m" | Delay before starting the first scan |
| unpackerr.lidarr | list | [] | List of Lidarr instances |
| unpackerr.radarr[0] | object | [] | List of Radarr instances to use for extracting files |
| unpackerr.radarr[0].apiKeySecret | object | `{"key":"radarrApiKey","name":"unpackarr-secrets"}` | Existing Secret settings |
| unpackerr.radarr[0].apiKeySecret.key | string | "" | Define the key within the existing Secret containing the api key |
| unpackerr.radarr[0].apiKeySecret.name | string | "" | Define the name of an existing Secret containing the api key |
| unpackerr.radarr[0].protocols | string | `"torrent"` | Supported protocols (e.g. torrent, usenet) |
| unpackerr.radarr[1].apiKey | string | `"abcdefg123456"` | API key as a string (not recommended; use `apiKeySecret`) |
| unpackerr.readarr | list | [] | List of Readarr instances |
| unpackerr.sonarr | list | [] | List of Sonarr instances |
| unpackerr.webhook[0] | object | [] | List of webhooks to call on events |
| unpackerr.webhook[0].events | list | [0] | List of event IDs to trigger this webhook |
| unpackerr.webhook[0].exclude | list | [] | List of paths or items to exclude |
| unpackerr.webhook[0].ignore_ssl | bool | false | Ignore SSL errors |
| unpackerr.webhook[0].name | string | `"Notifiarr"` | Name for this webhook configuration |
| unpackerr.webhook[0].silent | bool | false | Suppress event output |
| unpackerr.webhook[0].url.secretRef | object | `{"key":"url","name":"webhook-secret"}` | Existing Secret settings |
| unpackerr.webhook[0].url.secretRef.key | string | "" | Define the key within the existing Secret containing the webhook url |
| unpackerr.webhook[0].url.secretRef.name | string | "" | Define the name of an existing Secret containing the webhook url |
| unpackerr.webserver.listen_addr | string | "0.0.0.0:5656" | Address and port for the web UI and metrics endpoint |
| unpackerr.webserver.log_file | string | "" | Path to log file (if empty, logs to stdout) |
| unpackerr.webserver.log_file_mb | int | 10 | Max size (in MB) of each webserver log file |
| unpackerr.webserver.log_files | int | 10 | Number of log files to retain for web server |
| unpackerr.webserver.metrics | bool | false | Enable Prometheus metrics endpoint |
| unpackerr.webserver.ssl_cert_file | string | "" | Path to SSL certificate file (if using HTTPS) |
| unpackerr.webserver.ssl_key_file | string | "" | Path to SSL key file (if using HTTPS) |
| unpackerr.webserver.upstreams | string | "" | List of upstream services (e.g. nginx or Caddy) |
| unpackerr.webserver.urlbase | string | "/" | Web UI URL base path |
| unpackerr.whisparr | list | [] | List of Whisparr instances |

---
Autogenerated from chart metadata using [helm-docs](https://github.com/norwoodj/helm-docs)

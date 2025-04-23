# unifi-protect-backup

![Version: 0.1.3](https://img.shields.io/badge/Version-0.1.3-informational?style=flat)
![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat)
![AppVersion: 0.13.0](https://img.shields.io/badge/AppVersion-0.13.0-informational?style=flat)

Python tool to backup unifi event clips in realtime

**Homepage:** <https://charts.hydaz.com/charts/unifi-protect-backup/>

**This chart is not maintained by the upstream project and any issues with the chart should be raised
[here](https://github.com/hydazz/charts/issues/new?assignees=hydazz&labels=bug&template=bug_report.yaml&name=unifi-protect-backup&version=0.1.3)**

## Source Code

* <https://github.com/ep1cman/unifi-protect-backup>

## Requirements

Kubernetes: `>=1.22.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| <https://bjw-s.github.io/helm-charts> | common | 1.5.1 |

## Installing the Chart

To install the chart with the release name `unifi-protect-backup`

### OCI (Recommended)

```console
helm install unifi-protect-backup oci://ghcr.io/hydazz/charts/unifi-protect-backup
```

### Traditional

```console
helm repo add hydaz https://charts.hydaz.com
helm repo update
helm install unifi-protect-backup hydaz/unifi-protect-backup
```

## Uninstalling the Chart

To uninstall the `unifi-protect-backup` deployment

```console
helm uninstall unifi-protect-backup
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/bjw-s/helm-charts/tree/a081de5/charts/library/common/values.yaml) from the [bjw-s common library](https://github.com/bjw-s/helm-charts/tree/a081de5/charts/library/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install unifi-protect-backup \
  --set env.TZ="America/New York" \
    hydaz/unifi-protect-backup
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install unifi-protect-backup hydaz/unifi-protect-backup -f values.yaml
```

## Custom configuration

## Values

**Important**: When deploying an application Helm chart you can add more values from the bjw-s common library chart [here](https://github.com/bjw-s/helm-charts/tree/a081de5/charts/library/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| env.PGID | int | `1001` |  |
| env.PUID | int | `1001` |  |
| env.TZ | string | `"UTC"` | Set the container timezone |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"ghcr.io/ep1cman/unifi-protect-backup"` | Image repository |
| image.tag | string | `"0.13.0"` | Image tag |
| persistence.data | object | See [values.yaml](./values.yaml) | Configure data volume settings for the chart under this key. |
| service.main.enabled | bool | `false` |  |
| upb.appriseNotifiers | string | `""` | Notification configuration |
| upb.camera | object | `{"ignore":"","include":""}` | Camera filtering settings |
| upb.camera.ignore | string | "" | Cameras to ignore |
| upb.camera.include | string | "" | Cameras to include |
| upb.colorLogging | bool | `false` | Logging and purge settings |
| upb.detectionTypes | string | `""` |  |
| upb.downloadBufferSize | string | `"512MiB"` |  |
| upb.downloadRateLimit | string | `""` |  |
| upb.experimentalDownloader | bool | `false` |  |
| upb.fileStructureFormat | string | `"{camera_name}/{event.start:%Y-%m-%d}/{event.end:%Y-%m-%dT%H-%M-%S} {detection_type}.mp4"` | Event and download settings |
| upb.maxEventLength | string | `"7200"` |  |
| upb.purgeInterval | string | `"1d"` |  |
| upb.rclone | object | `{"args":"","config":"[cloudflare]\ntype = s3\nprovider = Cloudflare\naccess_key_id =\nsecret_access_key =\nendpoint =\n","destination":"","existingSecret":{"name":"","rcloneConfigKey":"rclone.conf"},"parallelUploads":"1","purgeArgs":"","retention":"7d"}` | Rclone settings |
| upb.rclone.args | string | "" | Extra Rclone arguments |
| upb.rclone.config | string | See [values.yaml](./values.yaml) | Rclone config file.    This will create/overwrite the existing Rclone config.    [[ref]](https://rclone.org/docs/) |
| upb.rclone.destination | string | "" | Destination path for Rclone |
| upb.rclone.existingSecret | object | `{"name":"","rcloneConfigKey":"rclone.conf"}` | Existing Secret settings |
| upb.rclone.existingSecret.name | string | "" | Define the name of an existing Secret containing the rclone config |
| upb.rclone.existingSecret.rcloneConfigKey | string | "" | Define the key within the existing Secret containing the rclone config |
| upb.rclone.parallelUploads | string | "" | Number of parallel uploads |
| upb.rclone.purgeArgs | string | "" | Extra Rclone purge arguments |
| upb.rclone.retention | string | "" | Rclone retention policy |
| upb.skipMissing | bool | `false` |  |
| upb.sqlitePath | string | `"/config/events.sqlite"` |  |
| upb.ufp | object | `{"address":"","existingSecret":{"name":"","passwordKey":"","usernameKey":""},"password":"","port":443,"sslVerify":true,"username":""}` | UniFi Protect credentials and connection settings |
| upb.ufp.address | string | "" | UFP controller address |
| upb.ufp.existingSecret | object | `{"name":"","passwordKey":"","usernameKey":""}` | Existing Secret settings |
| upb.ufp.existingSecret.name | string | "" | Define the name of an existing Secret containing the username and password |
| upb.ufp.existingSecret.passwordKey | string | "" | Secret key to use for the UFP password |
| upb.ufp.existingSecret.usernameKey | string | "" | Secret key to use for the UFP username |
| upb.ufp.password | string | `""` | UFP password (plain value, ignored if existingSecret is set) |
| upb.ufp.port | int | 443 | UFP controller port |
| upb.ufp.sslVerify | bool | true | Verify SSL certificate |
| upb.ufp.username | string | `""` | UFP username (plain value, ignored if existingSecret is set) |

---
Autogenerated from chart metadata using [helm-docs](https://github.com/norwoodj/helm-docs)

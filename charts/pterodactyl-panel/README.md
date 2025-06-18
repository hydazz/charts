# Pterodactyl Panel

<img src="https://pterodactyl.io/logos/pterry.svg" align="right" width="92" alt="pterodactyl-panel logo">

![Version: 0.2.3](https://img.shields.io/badge/Version-0.2.3-informational?style=flat)
![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat)
![AppVersion: v1.11.11](https://img.shields.io/badge/AppVersion-v1.11.11-informational?style=flat)

Pterodactyl® is a free, open-source game server management panel built with PHP, React, and Go.

**Homepage:** <https://charts.hydaz.com/charts/pterodactyl-panel/>

**This chart is not maintained by the upstream project and any issues with the chart should be raised
[here](https://github.com/hydazz/charts/issues/new?assignees=hydazz&labels=bug&template=bug_report.yaml&name=pterodactyl-panel&version=0.2.3)**

## Source Code

* <https://github.com/pterodactyl/panel>

## Requirements

Kubernetes: `>=1.22.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| <https://bjw-s-labs.github.io/helm-charts> | common | 1.5.1 |
| <https://charts.bitnami.com/bitnami> | redis | 21.0.0 |

## Installing the Chart

To install the chart with the release name `pterodactyl-panel`

### OCI (Recommended)

```console
helm install pterodactyl-panel oci://ghcr.io/hydazz/charts/pterodactyl-panel
```

### Traditional

```console
helm repo add hydaz https://charts.hydaz.com
helm repo update
helm install pterodactyl-panel hydaz/pterodactyl-panel
```

## Uninstalling the Chart

To uninstall the `pterodactyl-panel` deployment

```console
helm uninstall pterodactyl-panel
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/bjw-s-labs/helm-charts/tree/a081de5/charts/library/common/values.yaml) from the [bjw-s common library](https://github.com/bjw-s-labs/helm-charts/tree/a081de5/charts/library/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install pterodactyl-panel \
  --set env.TZ="America/New York" \
    hydaz/pterodactyl-panel
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install pterodactyl-panel hydaz/pterodactyl-panel -f values.yaml
```

## Custom configuration

## Values

**Important**: When deploying an application Helm chart you can add more values from the bjw-s common library chart [here](https://github.com/bjw-s-labs/helm-charts/tree/a081de5/charts/library/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"ghcr.io/pterodactyl/panel"` | Image repository |
| image.tag | string | `"v1.11.11"` | Image tag |
| ingress.main | object | See [values.yaml](./values.yaml) | Enable and configure ingress settings for the chart under this key. |
| panel.app | object | `{"leEmail":"","timezone":"UTC"}` | Application settings |
| panel.app.leEmail | string | "" | The email used for Let's Encrypt certificate generation |
| panel.app.timezone | string | "UTC" | The timezone to use for the panel |
| panel.cache | object | `{"driver":"redis"}` | Cache and Session settings |
| panel.cache.driver | string | "redis" | The cache driver [[ref]](https://github.com/pterodactyl/panel/tree/1.0-develop/.github/docker#mail-drivers) |
| panel.database | object | `{"existingSecret":{"name":"","passwordKey":"","usernameKey":""},"host":"","name":"","password":"","port":3306,"username":""}` | Database settings |
| panel.database.existingSecret | object | `{"name":"","passwordKey":"","usernameKey":""}` | Existing Secret settings for MySQL credentials |
| panel.database.existingSecret.name | string | "" | Define the name of an existing Secret containing the MySQL username and password |
| panel.database.existingSecret.passwordKey | string | "" | Secret key to use for the MySQL password |
| panel.database.existingSecret.usernameKey | string | "" | Secret key to use for the MySQL username |
| panel.database.host | string | "" | The host of the MySQL instance |
| panel.database.name | string | "" | The name of the MySQL database |
| panel.database.password | string | `""` | The MySQL password for the specified user (plain value, ignored if existingSecret is set) |
| panel.database.port | int | 3306 | The port of the MySQL instance |
| panel.database.username | string | `""` | The MySQL user (plain value, ignored if existingSecret is set) |
| panel.mail | object | `{"driver":"smtp","existingSecret":{"name":"","passwordKey":"","usernameKey":""},"from":"","host":"","password":"","port":587,"username":""}` | Mail settings |
| panel.mail.driver | string | "smtp" | The email driver [[ref]](https://github.com/pterodactyl/panel/tree/1.0-develop/.github/docker#cache-drivers) |
| panel.mail.existingSecret | object | `{"name":"","passwordKey":"","usernameKey":""}` | Existing Secret settings for Mail credentials |
| panel.mail.existingSecret.name | string | "" | Define the name of an existing Secret containing the mail username and password |
| panel.mail.existingSecret.passwordKey | string | "" | Secret key to use for the mail password |
| panel.mail.existingSecret.usernameKey | string | "" | Secret key to use for the mail username |
| panel.mail.from | string | "" | The email that should be used as the sender email |
| panel.mail.host | string | "" | The host of your mail driver instance |
| panel.mail.password | string | `""` | The password for your mail driver (plain value, ignored if existingSecret is set) |
| panel.mail.port | int | 587 | The port of your mail driver instance |
| panel.mail.username | string | `""` | The username for your mail driver (plain value, ignored if existingSecret is set) |
| panel.queue.driver | string | "redis" | The queue driver |
| panel.redis | object | `{"existingSecret":{"name":"","passwordKey":""},"host":"localhost","password":"","port":6379}` | Redis settings |
| panel.redis.existingSecret | object | `{"name":"","passwordKey":""}` | Existing Secret settings for Redis password |
| panel.redis.existingSecret.name | string | "" | Define the name of an existing Secret containing the Redis password |
| panel.redis.existingSecret.passwordKey | string | "" | Secret key to use for the Redis password |
| panel.redis.host | string | "localhost" | The hostname or IP address of the Redis database |
| panel.redis.password | string | `""` | The password used to secure the Redis database (plain value, ignored if existingSecret is set) |
| panel.redis.port | int | 6379 | The port the Redis database is using on the host |
| panel.session.driver | string | "redis" | The session driver |
| persistence.certs | object | See [values.yaml](./values.yaml) | Configure letsencrypt certificate volume settings for the chart under this key. |
| persistence.data | object | See [values.yaml](./values.yaml) | Configure data volume settings for the chart under this key. |
| persistence.logs | object | See [values.yaml](./values.yaml) | Configure logs volume settings for the chart under this key. |
| persistence.nginx | object | See [values.yaml](./values.yaml) | Configure nginx volume settings for the chart under this key. |
| redis | object | See [values.yaml](./values.yaml) | Enable and configure redis subchart under this key.    If enabled, the app's Redis env will be set for you.    [[ref]](https://github.com/bitnami/charts/tree/main/bitnami/redis) |
| service.main | object | See [values.yaml](./values.yaml) | Configures service settings for the chart. |
| wings | object | See [values.yaml](./values.yaml) | Setup proxying wings under this key. |
| wings.corsAllowOrigin | string | `"https://pterodactyl.example.com"` | The CORS `Access-Control-Allow-Origin` domain. MUST match the domain used to access the panel! |
| wings.enabled | bool | `false` | Enable Ingress and proxy config generation for wings |
| wings.ingressClassName | string | `""` | Ingress class to use for all wing routes |
| wings.instances | list | `[{"ip":"192.168.100.7","name":"wing1","port":8080,"to":"wing1.example.com"}]` | List of wing instances to proxy to |
| wings.instances[0].ip | string | `"192.168.100.7"` | The IP address of the wing |
| wings.instances[0].port | int | `8080` | The port the wing listens on |
| wings.instances[0].to | string | `"wing1.example.com"` | The external domain name to use for this wing |
| wings.tlsSecretName | string | `""` | TLS secret to use for all domains defined in wings |

---
Autogenerated from chart metadata using [helm-docs](https://github.com/norwoodj/helm-docs)

# Paperless-AI

![Version: 0.25.0](https://img.shields.io/badge/Version-0.25.0-informational?style=flat)
![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat)
![AppVersion: 2.14.7](https://img.shields.io/badge/AppVersion-2.14.7-informational?style=flat)

A community-supported supercharged version of paperless: scan, index and archive all your physical documents

**Homepage:** <https://charts.gabe565.com/charts/paperless-ngx/>

**This chart is not maintained by the upstream project and any issues with the chart should be raised
[here](https://github.com/gabe565/charts/issues/new?assignees=gabe565&labels=bug&template=bug_report.yaml&name=paperless-ai&version=0.25.0)**

## Source Code

* <https://github.com/clusterzx/paperless-ai>

## Requirements

Kubernetes: `>=1.22.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| <https://bjw-s.github.io/helm-charts> | common | 3.7.3 |

## Installing the Chart

To install the chart with the release name `paperless-ai`

### OCI (Recommended)

```console
helm install paperless-ai oci://ghcr.io/gabe565/charts/paperless-ai
```

### Traditional

```console
helm repo add gabe565 https://charts.gabe565.com
helm repo update
helm install paperless-ai gabe565/paperless-ai
```

## Uninstalling the Chart

To uninstall the `paperless-ai` deployment

```console
helm uninstall paperless-ai
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/bjw-s/helm-charts/tree/main/charts/library/common/values.yaml) from the [bjw-s common library](https://github.com/bjw-s/helm-charts/tree/main/charts/library/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install paperless-ai \
  --set env.TZ="America/New York" \
    gabe565/paperless-ai
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install paperless-ai gabe565/paperless-ai -f values.yaml
```

## Custom configuration

### Database Installation

Paperless-ngx supports PostgreSQL and MariaDB.
This chart can install PostgreSQL or MariaDB and configure Paperless-ngx automatically.
See each database section in [`values.yaml`](./values.yaml) for configuration examples.

## Values

**Important**: When deploying an application Helm chart you can add more values from the bjw-s common library chart [here](https://github.com/bjw-s/helm-charts/tree/main/charts/library/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| addAiProcessedTag | string | no | Add a tag to AI-processed documents |
| aiProcessedTagName | string | ai-processed | Tag name to be used for AI-processed documents |
| azure | object | false | Enable Azure API |
| azure.apiKey | string | "" | Azure API key |
| azure.apiVersion | string | "" | Azure API version |
| azure.deploymentName | string | "" | Azure deployment name |
| azure.endpoint | string | "" | Azure OpenAI endpoint |
| disableAutomaticProcessing | string | no | Disable automatic processing |
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"docker.io/clusterzx/paperless-ai"` | Image repository |
| image.tag | string | `"2.14.7"` | Image tag |
| ingress.main | object | See [values.yaml](./values.yaml) | Enable and configure ingress settings for the chart under this key. |
| ollama | object | false | Enable Ollama API |
| ollama.model | string | llama3.2 | Ollama model |
| ollama.url | string | http://localhost:11434 | Ollama API URL |
| openai | object | false | Enable OpenAI API |
| openai.apiKey | string | "" | OpenAI API key |
| openai.model | string | gpt-4o-mini | OpenAI model |
| paperlessApiToken | string | "" | Paperless API token |
| paperlessApiUrl | string | http://localhost:8000 | Paperless API URL |
| paperlessUsername | string | "" | Paperless username |
| persistence.data | object | See [values.yaml](./values.yaml) | Configure data volume settings for the chart under this key. |
| processOnlyNewDocuments | string | yes | Process only new documents |
| processPredefinedDocuments | string | no | Enable processing of predefined documents |
| promptTags | list | [] | Tags to trigger prompt selection |
| scanInterval | string | "*/30 * * * *" | Scan interval in cron format |
| service.main | object | See [values.yaml](./values.yaml) | Configures service settings for the chart. |
| systemPrompt | string | "" | Custom system prompt for document processing |
| tags | list | [] | Tags for document processing |
| useExistingData | string | no | Use existing data (skip fresh download) |
| usePromptTags | string | no | Enable prompt-based tags |

---
Autogenerated from chart metadata using [helm-docs](https://github.com/norwoodj/helm-docs)

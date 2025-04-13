# Paperless-AI

<img src="https://clusterzx.github.io/paperless-ai/ppai_icon.png" align="right" width="92" alt="paperless-ai logo">

![Version: 0.1.4](https://img.shields.io/badge/Version-0.1.4-informational?style=flat)
![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat)
![AppVersion: 2.14.7](https://img.shields.io/badge/AppVersion-2.14.7-informational?style=flat)

An automated document analyzer for Paperless-ngx using OpenAI API, Ollama and all OpenAI API compatible Services to automatically analyze and tag your documents.

**Homepage:** <https://charts.hydaz.com/charts/paperless-ai/>

**This chart is not maintained by the upstream project and any issues with the chart should be raised
[here](https://github.com/hydazz/charts/issues/new?assignees=hydazz&labels=bug&template=bug_report.yaml&name=paperless-ai&version=0.1.4)**

## Source Code

* <https://github.com/clusterzx/paperless-ai>

## Requirements

Kubernetes: `>=1.22.0-0`

## Dependencies

| Repository | Name | Version |
|------------|------|---------|
| <https://bjw-s.github.io/helm-charts> | common | 1.5.1 |

## Installing the Chart

To install the chart with the release name `paperless-ai`

### OCI (Recommended)

```console
helm install paperless-ai oci://ghcr.io/hydazz/charts/paperless-ai
```

### Traditional

```console
helm repo add hydaz https://charts.hydaz.com
helm repo update
helm install paperless-ai hydaz/paperless-ai
```

## Uninstalling the Chart

To uninstall the `paperless-ai` deployment

```console
helm uninstall paperless-ai
```

The command removes all the Kubernetes components associated with the chart **including persistent volumes** and deletes the release.

## Configuration

Read through the [values.yaml](./values.yaml) file. It has several commented out suggested values.
Other values may be used from the [values.yaml](https://github.com/bjw-s/helm-charts/tree/a081de5/charts/library/common/values.yaml) from the [bjw-s common library](https://github.com/bjw-s/helm-charts/tree/a081de5/charts/library/common).

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

```console
helm install paperless-ai \
  --set env.TZ="America/New York" \
    hydaz/paperless-ai
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart.

```console
helm install paperless-ai hydaz/paperless-ai -f values.yaml
```

## Custom configuration

## Values

**Important**: When deploying an application Helm chart you can add more values from the bjw-s common library chart [here](https://github.com/bjw-s/helm-charts/tree/a081de5/charts/library/common)

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| image.pullPolicy | string | `"IfNotPresent"` | Image pull policy |
| image.repository | string | `"docker.io/clusterzx/paperless-ai"` | Image repository |
| image.tag | string | `"2.14.7"` | Image tag |
| ingress.main | object | See [values.yaml](./values.yaml) | Enable and configure ingress settings for the chart under this key. |
| paperlessai.addAiProcessedTag | string | no | Add a tag to AI-processed documents |
| paperlessai.aiProcessedTagName | string | ai-processed | Tag name to be used for AI-processed documents |
| paperlessai.azure.apiKey | string | "" | Azure API key |
| paperlessai.azure.apiVersion | string | "" | Azure API version |
| paperlessai.azure.deploymentName | string | "" | Azure deployment name |
| paperlessai.azure.enable | bool | false | Enable Azure API |
| paperlessai.azure.endpoint | string | "" | Azure OpenAI endpoint |
| paperlessai.azure.existingSecret | string | "" | The name of existing secret containing a `azureApiKey` key to configure Azure API key |
| paperlessai.disableAutomaticProcessing | string | no | Disable automatic processing |
| paperlessai.ollama.enable | bool | false | Enable Ollama API |
| paperlessai.ollama.model | string | llama3.2 | Ollama model |
| paperlessai.ollama.url | string | http://localhost:11434 | Ollama API URL |
| paperlessai.openai.apiKey | string | "" | OpenAI API key |
| paperlessai.openai.enable | bool | false | Enable OpenAI API |
| paperlessai.openai.existingSecret | string | "" | The name of existing secret containing a `openaiApiKey` key to configure OpenAI API key |
| paperlessai.openai.model | string | gpt-4o-mini | OpenAI model |
| paperlessai.paperless | object | `{"apiToken":"","apiUrl":"http://localhost:8000","existingSecret":{"apiTokenKey":"","name":"","usernameKey":""},"username":""}` | Paperless Authentication Settings |
| paperlessai.paperless.apiToken | string | "" | Paperless API token |
| paperlessai.paperless.apiUrl | string | http://localhost:8000 | Paperless API URL |
| paperlessai.paperless.existingSecret | object | `{"apiTokenKey":"","name":"","usernameKey":""}` | An existing secret containing the paperless credentials |
| paperlessai.paperless.existingSecret.apiTokenKey | string | "" | Define the key within the Secret for the API Token for Paperless |
| paperlessai.paperless.existingSecret.name | string | "" | Define the name of an existing Secret |
| paperlessai.paperless.existingSecret.usernameKey | string | "" | Define the key within the Secret for the username for Paperless |
| paperlessai.paperless.username | string | "" | Paperless username |
| paperlessai.processOnlyNewDocuments | string | yes | Process only new documents |
| paperlessai.processPredefinedDocuments | string | no | Enable processing of predefined documents |
| paperlessai.promptTags | string | "" | Tags to trigger prompt selection |
| paperlessai.scanInterval | string | "*/30 * * * *" | Scan interval in cron format |
| paperlessai.systemPrompt | string | "" | Custom system prompt for document processing |
| paperlessai.tags | string | "" | Tags for document processing |
| paperlessai.useExistingData | string | no | Use existing data (skip fresh download) |
| paperlessai.usePromptTags | string | no | Enable prompt-based tags |
| persistence.data | object | See [values.yaml](./values.yaml) | Configure data volume settings for the chart under this key. |
| service.main | object | See [values.yaml](./values.yaml) | Configures service settings for the chart. |

---
Autogenerated from chart metadata using [helm-docs](https://github.com/norwoodj/helm-docs)

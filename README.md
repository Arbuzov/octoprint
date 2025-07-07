# OctoPrint Helm Chart

![Version: 0.2.2](https://img.shields.io/badge/Version-0.2.2-informational?style=flat-square)
![AppVersion: 1.11.0](https://img.shields.io/badge/AppVersion-1.11.0-informational?style=flat-square)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/octoprint)](https://artifacthub.io/packages/search?repo=octoprint)

OctoPrint is the snappy web interface for your 3D printer that allows you to control and monitor all aspects of your printer and print jobs, right from your browser.

**Homepage:** <https://octoprint.org/>

The original maintainers stopped updating this chart, so this repository revives it to keep deployments running with recent versions of OctoPrint and Helm. Contributions are welcome!

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| Gavin Mogan | <helm@gavinmogan.com> |  |
| Serge Arbuzov | <info@whitediver.com> |  |

## Source Code

* <https://github.com/Arbuzov/octoprint>
* <https://hub.docker.com/r/octoprint/octoprint>

## Helm Repository

Add this chart repository with:

```sh
helm repo add octoprint https://arbuzov.github.io/octoprint
helm repo update
```

Install the chart with:

```sh
helm install my-octoprint octoprint/octoprint
```

Upgrade using:

```sh
helm repo update
helm upgrade my-octoprint octoprint/octoprint
```

## Configuration

All configurable values are documented in [`values.yaml`](./values.yaml). Key options include:

- `persistence.enabled` – enable to store configuration on a Persistent Volume.
- `ingress.enabled` – expose OctoPrint via an Ingress controller.
- `resourcesPreset` – choose from predefined resource limits (e.g., `micro`, `small`).

You can supply a custom `config.overlay` to merge with OctoPrint's default configuration.

### Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| config.overlay | string | `"# This is a config overlay file for OctoPrint. It is used to override the default configuration with custom settings."` |  |
| device | string | `"/dev/ttyACM0"` |  |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"octoprint/octoprint"` |  |
| image.tag | string | `"1.11.0"` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths | list | `[]` |  |
| ingress.tls | list | `[]` |  |
| livenessProbe.enabled | bool | `true` |  |
| livenessProbe.failureThreshold | int | `3` |  |
| livenessProbe.initialDelaySeconds | int | `30` |  |
| livenessProbe.periodSeconds | int | `10` |  |
| livenessProbe.successThreshold | int | `1` |  |
| livenessProbe.timeoutSeconds | int | `5` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| persistence.accessModes[0] | string | `"ReadWriteOnce"` |  |
| persistence.enabled | bool | `false` |  |
| persistence.existingClaim | string | `nil` |  |
| persistence.size | string | `"1Gi"` |  |
| persistence.storageClassName | string | `nil` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| readinessProbe.enabled | bool | `true` |  |
| readinessProbe.failureThreshold | int | `3` |  |
| readinessProbe.initialDelaySeconds | int | `30` |  |
| readinessProbe.periodSeconds | int | `10` |  |
| readinessProbe.successThreshold | int | `1` |  |
| readinessProbe.timeoutSeconds | int | `5` |  |
| replicaCount | int | `1` |  |
| resources | object | `{}` |  |
| resourcesPreset | string | `"micro"` |  |
| securityContext.privileged | bool | `true` |  |
| service.port | int | `5000` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.create | bool | `true` |  |
| serviceAccount.name | string | `nil` |  |
| startupProbe.enabled | bool | `true` |  |
| startupProbe.failureThreshold | int | `3` |  |
| startupProbe.initialDelaySeconds | int | `30` |  |
| startupProbe.periodSeconds | int | `10` |  |
| startupProbe.successThreshold | int | `1` |  |
| startupProbe.timeoutSeconds | int | `5` |  |
| tolerations | list | `[]` |  |

## Development

Run basic checks before submitting changes:

```sh
helm lint .
helm template test-release .
```

When creating a new release, package the chart and update the repository index:

```sh
helm package . -d .deploy
helm repo index .deploy --url https://your.github.io/octoprint
```

The GitHub Actions release workflow lints the chart, packages it, regenerates the
`index.yaml`, and automatically commits everything to the `gh-pages` branch.

## License

This project is licensed under the [MIT License](./LICENSE).

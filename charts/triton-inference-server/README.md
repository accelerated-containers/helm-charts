# triton-inference-server

NVIDIA Triton Inference Server

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 2.55.0](https://img.shields.io/badge/AppVersion-2.55.0-informational?style=flat-square)

## Documentation

For Triton Inference Server documentation please see [https://github.com/triton-inference-server/server).

## Installing the Chart

First add the ClowdHaus repository to Helm:

```bash
helm repo add clowdhaus https://clowdhaus.github.io/helm-charts
```

To install the chart with the release name `triton-inference-server` in the `triton` namespace and default configuration:

```bash
helm install triton-inference-server \
    --namespace triton \
    --create-namespace \
    clowdhaus/triton-inference-server
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{"nodeAffinity":{"requiredDuringSchedulingIgnoredDuringExecution":{"nodeSelectorTerms":[{"matchExpressions":[{"key":"nvidia.com/gpu.present","operator":"In","values":["true"]}]},{"matchExpressions":[{"key":"aws.amazon.com/neuron.present","operator":"In","values":["true"]}]}]}}}` | Affinity rules for scheduling the pod. |
| args | list | `["--model-store=/models","--model-control-mode=poll","--repository-poll-secs=30"]` | Arguments for the inference server pod. |
| autoscaling.behavior.scaleDown.policies[0].periodSeconds | int | `60` |  |
| autoscaling.behavior.scaleDown.policies[0].type | string | `"Percent"` |  |
| autoscaling.behavior.scaleDown.policies[0].value | int | `50` |  |
| autoscaling.behavior.scaleDown.stabilizationWindowSeconds | int | `180` |  |
| autoscaling.behavior.scaleUp.policies[0].periodSeconds | int | `15` |  |
| autoscaling.behavior.scaleUp.policies[0].type | string | `"Percent"` |  |
| autoscaling.behavior.scaleUp.policies[0].value | int | `100` |  |
| autoscaling.behavior.scaleUp.stabilizationWindowSeconds | int | `60` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `3` |  |
| autoscaling.metrics | list | `[]` |  |
| autoscaling.minReplicas | int | `1` |  |
| env | list | `[]` | Additional environment variables for the inference server pod. |
| envFrom | list | `[]` |  |
| fullnameOverride | string | `""` | Overrides the chart's computed fullname. |
| image.pullPolicy | string | `"IfNotPresent"` |  |
| image.repository | string | `"nvcr.io/nvidia/tritonserver"` |  |
| image.tag | string | `"25.02-py3"` |  |
| imagePullSecrets | list | `[]` | Image pull secrets for Docker images. |
| ingress.annotations | object | `{}` |  |
| ingress.className | string | `""` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"ImplementationSpecific"` |  |
| ingress.tls | list | `[]` |  |
| livenessProbe.httpGet.path | string | `"/v2/health/live"` |  |
| livenessProbe.httpGet.port | string | `"http"` |  |
| nameOverride | string | `""` | Overrides the chart's name. |
| nodeSelector | object | `{}` | Node selectors to schedule the pod to nodes with labels. |
| podAnnotations | object | `{}` | Additional annotations for the pod. |
| podDisruptionBudget.create | bool | `false` | Specifies whether a pod disruption budget should be created |
| podDisruptionBudget.maxUnavailable | int | `1` |  |
| podLabels | object | `{}` | Additional labels for the pod. |
| podSecurityContext | object | `{"fsGroup":65532,"runAsNonRoot":true,"seccompProfile":{"type":"RuntimeDefault"}}` | SecurityContext for the pod. |
| readinessProbe.httpGet.path | string | `"/v2/health/ready"` |  |
| readinessProbe.httpGet.port | string | `"http"` |  |
| readinessProbe.initialDelaySeconds | int | `5` |  |
| readinessProbe.periodSeconds | int | `5` |  |
| replicaCount | int | `1` | Number of replicas. |
| resources.limits."nvidia.com/gpu" | int | `1` |  |
| securityContext.appArmorProfile | object | `{}` | AppArmor profile for the container. |
| securityContext.seLinuxOptions | object | `{}` | SELinux options for the container. |
| securityContext.seccompProfile | object | `{}` | Seccomp profile for the container. |
| service.annotations | object | `{}` | Additional annotations to add to the service |
| service.ports.grpc | int | `8001` |  |
| service.ports.http | int | `8000` |  |
| service.ports.metrics | int | `8002` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` | Additional annotations to add to the service account |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name is generated using the fullname template |
| tolerations[0].effect | string | `"NoSchedule"` |  |
| tolerations[0].key | string | `"nvidia.com/gpu"` |  |
| tolerations[0].operator | string | `"Exists"` |  |
| tolerations[1].effect | string | `"NoSchedule"` |  |
| tolerations[1].key | string | `"aws.amazon.com/neuron"` |  |
| tolerations[1].operator | string | `"Exists"` |  |
| volumeMounts | list | `[]` | Additional volumeMounts on the output Deployment definition. |
| volumes | list | `[]` | Additional volumes on the output Deployment definition. |

----------------------------------------------

Autogenerated from chart metadata using [helm-docs](https://github.com/norwoodj/helm-docs/).

# my-app

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.0.0](https://img.shields.io/badge/AppVersion-1.0.0-informational?style=flat-square)

A template Helm chart for Kubernetes.

1. Copy all files from this `chart` directory to `your-app-repo/helm/myapp-name`
2. Edit name, description and versions in the `Chart.yaml` file.
3. Replace `image.repository` in the `values.yaml` file.
4. Edit `values.<env>.yaml` as you need.
5. Checkout generated manifests via command: `helm template myapp your-app-repo/helm/myapp-name -f your-app-repo/helm/myapp-name/values.production.yaml`

See detailed reference in the `values.yaml`.

* For using `configMapFiles` create files directory like `chart/files`.
* `ExternalSecret` have been tested using the [External Secret Operator](https://external-secrets.io/latest/) in combination with [Yandex Lockbox](https://yandex.cloud/com/docs/managed-kubernetes/tutorials/kubernetes-lockbox-secrets)

---

If you need `ExternalSecret` create SecretStore first.
Example for Yandex Lockbox ([see more info here](https://yandex.cloud/ru/docs/managed-kubernetes/tutorials/kubernetes-lockbox-secrets)):

```shell
# https://external-secrets.io/latest/introduction/getting-started/
helm repo add external-secrets https://charts.external-secrets.io
helm install external-secrets external-secrets/external-secrets -n default

# Create yc-auth secret with service account json key before command below
# https://yandex.cloud/ru/docs/managed-kubernetes/tutorials/kubernetes-lockbox-secrets

kubectl --namespace default apply -f - <<< '
apiVersion: external-secrets.io/v1beta1
kind: SecretStore
metadata:
  name: yc-lockbox-secret-store
spec:
  provider:
    yandexlockbox:
      auth:
        authorizedKeySecretRef:
          name: yc-auth
          key: authorized-key'
```

---

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].key | string | `"nodeType"` |  |
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].operator | string | `"In"` |  |
| affinity.nodeAffinity.requiredDuringSchedulingIgnoredDuringExecution.nodeSelectorTerms[0].matchExpressions[0].values[0] | string | `"worker"` |  |
| autoscaling.enabled | bool | `false` |  |
| autoscaling.maxReplicas | int | `2` |  |
| autoscaling.minReplicas | int | `1` |  |
| autoscaling.targetCPUUtilizationPercentage | int | `80` |  |
| commonLabels | object | `{}` |  |
| configMapFiles.enabled | bool | `false` |  |
| containerProps.args | list | `[]` |  |
| containerProps.command | list | `[]` |  |
| containerProps.lifecycle | object | `{}` |  |
| deployStrategy.rollingUpdate.maxSurge | int | `1` |  |
| deployStrategy.rollingUpdate.maxUnavailable | int | `0` |  |
| deployStrategy.type | string | `"RollingUpdate"` |  |
| deploymentAnnotations | object | `{}` |  |
| env | object | `{}` |  |
| externalSecrets.annotations | object | `{}` |  |
| externalSecrets.decodingStrategy | string | `"None"` |  |
| externalSecrets.enabled | bool | `false` |  |
| externalSecrets.refreshInterval | string | `"1h"` |  |
| externalSecrets.storeName | string | `"yc-lockbox-secret-store"` |  |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"Always"` |  |
| image.repository | string | `"<cr.yandex/images/REPLACE_ME>"` |  |
| image.tag | string | `""` |  |
| imagePullSecrets | list | `[]` |  |
| ingress.annotations | object | `{}` |  |
| ingress.className | string | `"nginx"` |  |
| ingress.enabled | bool | `false` |  |
| ingress.hosts[0].host | string | `"chart-example.local"` |  |
| ingress.hosts[0].paths[0].path | string | `"/"` |  |
| ingress.hosts[0].paths[0].pathType | string | `"Prefix"` |  |
| ingress.tls | list | `[]` |  |
| livenessProbe | object | `{}` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podLabels | object | `{}` |  |
| readinessProbe | object | `{}` |  |
| replicaCount | int | `1` |  |
| resources.limits.cpu | string | `"500m"` |  |
| resources.limits.memory | string | `"256Mi"` |  |
| resources.requests.cpu | string | `"100m"` |  |
| resources.requests.memory | string | `"256Mi"` |  |
| secretsToEnv | object | `{}` |  |
| securityContext.allowPrivilegeEscalation | bool | `false` |  |
| securityContext.capabilities.drop[0] | string | `"ALL"` |  |
| securityContext.privileged | bool | `false` |  |
| securityContext.readOnlyRootFilesystem | bool | `true` |  |
| securityContext.runAsGroup | int | `65532` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `65532` |  |
| service.annotations | object | `{}` |  |
| service.enabled | bool | `false` |  |
| service.port | int | `80` |  |
| service.portName | string | `"http"` |  |
| service.protocol | string | `"TCP"` |  |
| service.targetPort | int | `8080` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` |  |
| serviceAccount.automount | bool | `true` |  |
| serviceAccount.create | bool | `false` |  |
| serviceAccount.name | string | `""` |  |
| startupProbe | object | `{}` |  |
| tolerations | list | `[]` |  |
| volumeMounts | list | `[]` |  |
| volumes | list | `[]` |  |

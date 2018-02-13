# NAME

ConfigMaps allow to decouple configuration artifacts from image content to keep containerized applications portable.

## Resources
* [Documentation](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)
* [API Reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/#configmap-v1-core)

## Kubectl commands

`kubectl get configmap`

`kubectl create configmap <MAP_NAME> --from-file=<DIRECTORY_PATH>`

`kubectl create configmap <MAP_NAME> --from-file=<FILE_PATH>`

`kubectl create configmap <MAP_NAME> --from-file=<KEY_NAME>=<FILE_PATH>`

`kubectl create configmap <MAP_NAME> --from-literal=<KEY1>=<VALUE1> --from-literal=<KEY2>=<VALUE2>` 

## Manifests

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: example-config
  namespace: default
data:
  # example of a simple property defined using --from-literal
  example.property.1: hello
  example.property.2: world
  # example of a complex property defined using --from-file
  example.property.file: |-
    property.1=value-1
    property.2=value-2
    property.3=value-3
```

ConfigMap usage in Pod: [pod_configmap.yaml](../pod/pod_configmap.yaml)


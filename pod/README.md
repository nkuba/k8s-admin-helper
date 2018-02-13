# Pods

## Resources
* [Documentation](https://kubernetes.io/docs/concepts/workloads/pods/pod/)
* [API Reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/#pod-v1-core)

## Kubectl commands

```bash
kubectl label pod my-pod new-label=awesome                      # Add a Label
kubectl annotate pod my-pod icon-url=http://goo.gl/XXBTWq       # Add an annotation

kubectl get pods --show-labels
kubectl get pods -LKEY

kubectl port-forward POD_NAME LOCAL_PORT:POD_PORT

kubectl exec -ti POD_NAME -- /bin/sh
kubectl run -it --rm --restart=Never busybox --image=busybox sh
```

* Get all pods for node `<NODE_NAME>`
```bash
kubectl get pods -o jsonpath='{range .items[?(@.spec.nodeName=="<NODE_NAME>")]}{.metadata.name}{"\n"}' --all-namespaces
```

* Get pods with _pod name_ and _node names_ sort by second column
```bash
kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.nodeName}{"\n"}' --all-namespaces | sort -k 2
```

## Manifests

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  namespace: default
spec:
  containers:
  - name: busybox
    image: busybox
    command:
    - sleep
    - "3600"
```

# DaemonSet

A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. 
As nodes are removed from the cluster, those Pods are garbage collected.

## Resources
* [Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)
* [API Reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/#daemonset-v1-apps)

## Manifests

[daemonset.yaml](daemonset.yaml)
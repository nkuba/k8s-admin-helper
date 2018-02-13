# NAME

A **PersistentVolume** (PV) is a piece of storage in the cluster that has been provisioned by an administrator.
PVs are volume plugins like Volumes, but have a lifecycle independent of any individual pod that uses the PV.

A **PersistentVolumeClaim** (PVC) is a request for storage by a user.

## Resources
* [Documentation](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)
* [API Reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/#persistentvolume-v1-core)

## Kubectl commands

`kubectl get pv`

`kubectl get pvc`

## Manifests

Sample PersistentVolume manifest: [persistentvolume.yaml](persistentvolume.yaml) <br>
Sample PersistentVolumeClaim manifest: [persistentvolumeclaim.yaml](persistentvolumeclaim.yaml)

Usage of PersistentVolumeClaim in Pod: [pod_persistentvolumeclaim.yaml](../pod/pod_persistentvolumeclaim.yaml)
# Kubernetes Admin Helper

This project contains selection of resources helpful for Kubernetes Administrators.

## Manifests
Manifests templates are created based on official Kubernetes [Documentation](https://kubernetes.io/docs/) 
and [API Reference v1.9](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/)

## Cheat Sheet
Cheat sheet commands are based on official [kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)

### Autocompletion
```bash
source <(kubectl completion bash)
```

### Configuration and Maintenance
```bash
kubectl config view
kubectl config current-context
kubectl config use-context CONTEXT

kubectl cluster-info
kubectl get componentstatuses
kubectl get events

# Logs
kubectl logs --namespace=NAMESPACE --container=CONTAINER POD_NAME
kubectl logs --previous ${POD_NAME} -c ${CONTAINER_NAME}

# Namespaces
kubectl get namespace
kubectl create namespace NAMESPACE
```

### Resource lifecycle operations

#### Create
```bash
kubectl create -f my-manifest.yaml            # create from file
kubectl create -f my1.yaml -f my2.yaml        # create from multiple files
kubectl create -f dir                         # create from files in dir
```

#### Read
```bash
kubectl get pods                              # List all pods in the namespace
kubectl get pods --all-namespaces             # List all pods in all namespaces
kubectl get pods -o wide                      # List all pods in the namespace, with more details
kubectl get pods --include-uninitialized      # List all pods in the namespace, including uninitialized ones
kubectl get pods --watch                      # List all pods and watch changes
kubectl get pod my-pod                        # List a particular deployment

kubectl describe nodes my-node

kubectl get services --sort-by=.metadata.name # List Services Sorted by Name

# List pods Sorted by Restart Count
kubectl get pods --sort-by='.status.containerStatuses[0].restartCount'

# Get the version label of all pods with label app=cassandra
kubectl get pods --selector=app=cassandra -o jsonpath='{.items[*].metadata.labels.version}'

# Get all running pods in the namespace
kubectl get pods --field-selector=status.phase=Running

# Get ExternalIPs of all nodes
kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="ExternalIP")].address}'

# List Names of Pods that belong to Particular Deployment
# "jq" command useful for transformations that are too complex for jsonpath, it can be found at https://stedolan.github.io/jq/
sel=$(kubectl get deployment nginx-deployment -o=json | jq -j '.spec.selector.matchLabels | to_entries | map([.key,.value] | join("=")) | join(",")')
kubectl get pods -l=$sel -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}'
```
#### Update
```bash
# Force replace, delete and then re-create the resource. Will cause a service outage.
kubectl replace --force -f ./pod.json
```

### Node
```bash
kubectl label node NODE KEY=VALUE

kubectl get nodes --show-labels

kubectl get nodes -o jsonpath="{$.items[*].metadata.labels}"

# Taint
kubectl taint node NODE_NAME LABEL_KEY=LABEL_VALUE:NoSchedule


# Drain and Uncordon
kubectl drain NODE_NAME
kubectl uncordon NODE_NAME
```

### etcd
* [Operating etcd clusters for Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)
GitHub:
* [etcd](https://github.com/coreos/etcd)
* [etcdctl](https://github.com/coreos/etcd/tree/master/etcdctl#etcdctl)

```bash
ETCDCTL_API=3 etcdctl member list

etcdctl ls
etcdctl ls /registry

ETCDCTL_API=3 etcdctl --endpoints <ENDPOINT> snapshot save snapshotdb
ETCDCTL_API=3 etcdctl --write-out=table snapshot status snapshotdb
```

### systemd
```bash
systemctl list-units | grep kube

systemctl status kube-apiserver

journalctl -u kubelet
```

### Minikube
```bash
minikube start
minikube ip
minikube version
minikube ssh
```

### containerd
```bash
sudo ctr -n k8s.io containers list
```
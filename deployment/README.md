# Deployment

A Deployment controller provides declarative updates for Pods and ReplicaSets.

You describe a desired state in a Deployment object, and the Deployment controller changes the actual state to the desired state at a controlled rate. You can define Deployments to create new ReplicaSets, or to remove existing Deployments and adopt all their resources with new Deployments.

## Resources
* [Documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
* [API Reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/#deployment-v1-apps)

## Kubectl commands

`kubectl create --record -f  <FILE_PATH>`

Append --record to this command to record the current command in the annotations of the created or updated resource.

### Updating a Deployment

```bash
kubectl rollout status deployment/<DEPLOYMENT_NAME>

kubectl set image deployment/<DEPLOYMENT_NAME> <CONTAINER_NAME>=<IMAGE_NAME>:<IMAGE_VERSION>

kubectl edit deployment/<DEPLOYMENT_NAME>

kubectl set resources deployment nginx-deployment -c=nginx --limits=cpu=200m,memory=512Mi
```

### Rolling Back a Deployment

```bash
kubectl rollout history deployment/<DEPLOYMENT_NAME>

kubectl rollout history deployment/<DEPLOYMENT_NAME> --revision=<REVISION_NUMBER>

kubectl rollout undo deployment/<DEPLOYMENT_NAME>

kubectl rollout undo deployment/<DEPLOYMENT_NAME> --to-revision=<REVISION_NUMBER>
```

### Scaling a Deployment

`kubectl scale deployment <DEPLOYMENT_NAME> --replicas=<REPLICAS_NUMBER>`

`kubectl autoscale deployment <DEPLOYMENT_NAME> --min=<MIN_PODS> --max=<MAX_PODS> --cpu-percent=<CPU_USAGE>`

### Pausing and Resuming a Deployment

`kubectl rollout pause deployment/<DEPLOYMENT_NAME>`

`kubectl rollout resume deployment/<DEPLOYMENT_NAME>`

## Manifests

```yaml
xxx
```
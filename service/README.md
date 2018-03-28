# Service

A Kubernetes Service is an abstraction which defines a logical set of Pods and a policy by which to access them - 
sometimes called a micro-service.

The set of Pods targeted by a Service is (usually) determined by a Label Selector.

## Resources
* [Documentation](https://kubernetes.io/docs/concepts/services-networking/service/)
* [API Reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/#service-v1-core)

## Kubectl commands

`kubectl get service`

`kubectl expose deployment/<NAME>`

`kubectl​ ​expose​ ​deployment/<NAME​> ​--port=<PORT>​ ​--type=NodePort`

## Manifests

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  selector:
    app: nginx
  type: NodePort
  ports:
  - port: 80
    
    nodePort: 8080
```
## Service Types

[Documentation](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services---service-types)

* **ClusterIp** (default) - Exposes the service on cluster-internal IP. The service is only reachable from within the cluster.

* **NodePort** - Exposes the service on each Node’s IP at a static port. You’ll be able to contact the NodePort service, 
from outside the cluster, by requesting `<NodeIP>:<NodePort>`. 
Sample manifest: [service_node_port.yaml](service_node_port.yaml)

* **LoadBalancer** - Exposes the service externally using a cloud provider’s load balancer.
Sample manifest: [service_load_balancer.yaml](service_load_balancer.yaml)

* **ExternalName** - Maps the service to the contents of the `externalName` field (e.g. _foo.bar.example.com_), by returning a _CNAME_ record with its value.
[service_external_ip.yaml](service_external_ip.yaml)

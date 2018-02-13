# Network Policy
A network policy is a specification of how groups of pods are allowed to communicate with each other and other network endpoints.

**NetworkPolicy** resources use labels to select pods and define rules which specify what traffic is allowed to the selected pods.

By default, pods are non-isolated, they accept traffic from any source.
Pods become isolated by having a NetworkPolicy that selects them.

## Resources
* [Documentation: Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
* [Documentation: Declare Network Policy](https://kubernetes.io/docs/tasks/administer-cluster/declare-network-policy/)
* [API Reference](https://kubernetes.io/docs/api-reference/v1.9/#networkpolicy-v1-networking)
* [Blog: Securing Kubernetes Cluster Networking](https://ahmet.im/blog/kubernetes-network-policy/)

## Kubectl commands

`kubectl get networkpolicies`

## Manifests

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: access-nginx
  namespace: default
spec:
  podSelector:
    matchLabels:
      run: nginx
  ingress:
  - from:
    - podSelector:
        matchLabels:
          access: "true"
    - ipBlock:
        cidr: 172.17.0.0/16
        except:
        - 172.17.1.0/24
    - namespaceSelector:
        matchLabels:
          project: myproject
    ports:
    - protocol: TCP
      port: 6379
  egress:
  - to:
    - ipBlock:
        cidr: 10.0.0.0/24
    ports:
    - protocol: TCP
      port: 5978
```



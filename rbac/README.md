# Role-Based Access Control

Role-Based Access Control (“RBAC”) uses the “rbac.authorization.k8s.io” API group to drive authorization decisions, allowing admins to 
dynamically configure policies through the Kubernetes API.

To enable RBAC, start the apiserver with `--authorization-mode=RBAC`.

## Resources
* [Documentation](https://kubernetes.io/docs/admin/authorization/rbac/)
* API References:
    * [Role](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/#role-v1-rbac)
    * [ClusterRole](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/#clusterrole-v1-rbac)
    * [RoleBinding](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/#rolebinding-v1-rbac)
    * [ClusterRoleBinding](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.9/#clusterrolebinding-v1-rbac)


## Kubectl commands

`kubectl create rolebinding <ROLE_BINDING_NAME> --clusterrole=<CLUSTER_ROLE_NAME> --user=<USER_NAME> --namespace=<NAMESPACE>`

`kubectl create clusterrolebinding <ROLE_BINDING_NAME> --clusterrole=<CLUSTER_ROLE_NAME> --serviceaccount=<SERVICE_ACCOUNT_NAME>`

## Role and ClusterRole
[Documentation](https://kubernetes.io/docs/admin/authorization/rbac/#role-and-clusterrole)

**Role** can only be used to grant access to resources within a single namespace. Sample manifest: [role.yaml](role.yaml)

**ClusterRole** can be used to grant the same permissions as a Role, but because they are cluster-scoped, they can also be used to grant access to:
* cluster-scoped resources (like nodes)
* non-resource endpoints (like “/healthz”)
* namespaced resources (like pods) across all namespaces (needed to run `kubectl get pods --all-namespaces`).
Sample manifest: [cluster_role.yaml](clusterrole.yaml)

## RoleBinding and ClusterRoleBinding
[Documentation](https://kubernetes.io/docs/admin/authorization/rbac/#rolebinding-and-clusterrolebinding)

A role binding grants the permissions defined in a role to a user or set of users. 

Permissions can be granted within a namespace with a **RoleBinding**, or cluster-wide with a **ClusterRoleBinding**.

* A **RoleBinding** may reference a **Role** in the same namespace. Sample manifest: [rolebinding.yaml](rolebinding.yaml)

* A **RoleBinding** may reference a **ClusterRole** to grant the permissions within the *RoleBinding* namespace. Sample manifest: [rolebinding_ref_clusterrole.yaml](rolebinding_ref_clusterrole.yaml)

* A **ClusterRoleBinding** may be used to grant permission at the cluster level and in all namespaces. Sample manifest: [clusterrolebinding.yaml](clusterrolebinding.yaml)

## Aggregated ClusterRoles
[Documentation](https://kubernetes.io/docs/admin/authorization/rbac/#aggregated-clusterroles)

ClusterRoles can be created by combining other ClusterRoles using an `aggregationRule`

Sample manifest: [clusterrole_aggregated.yaml](clusterrole_aggregated.yaml)




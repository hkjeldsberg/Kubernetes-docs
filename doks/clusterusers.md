(cluster)=

# `ClusterRoles` and `ClusterRolebindings` for `Users`

## `ClusterRole`

Creating a `ClusterRole` role imperatvely:

```console
kubectl create clusterrole NAME --verb=[get,list,create,..] --resource=[pods,deployments,service,..]
```

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: tmp-cluster-role
rules:
  - apiGroups:
      - ""
    resources:
      - pods
    verbs:
      - '*'
  - apiGroups:
      - apps
    resources:
      - deployments
    verbs:
      - get
      - create
      - delete
```

## `ClusterRolebinding`

Match a `User` with a `Role` in a `Rolebinding`:

```console
kubectl create clusterrolebinding NAME --clusterrole=NAME --user=USERNAME  
```

Or declarative:

```yaml
# dev-binding.yaml
kind: ClusterRoleBinding
subjects: # User details
  - kind: User
    name: dev-user
    apiGroup: rbac.authorization.k8s.io
roleRef: # Role definitions
  - kind: ClusterRole
    name: developer
    apiGroup: rbac.authorization.k8s.io
```


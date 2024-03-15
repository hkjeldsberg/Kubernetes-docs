(users)=

# `Roles` and `Rolebindings` for `Users`

## `Roles`

Creating a role imperatvely:

```console
kubectl create role NAME --verb=[get,list,create,..] --resource=[pods,deployments,service,..]
```

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: tmp-role
rules:
  - apiGroups:
      - ""
    resources:
      - pods
    resourceNames: [ "pod1", "pod4" ] # Optional to specify resource
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

## `RoleBinding`

Match a `User` with a `Role` in a `Rolebinding`:

```console
kubectl create rolebinding NAME --role=NAME --user=USERNAME  
```

Or declarative:

```yaml
# dev-binding.yaml
kind: RoleBinding
subjects: # User details
  - kind: User
    name: dev-user
    apiGroup: rbac.authorization.k8s.io
roleRef: # Role definitions
  - kind: Role
    name: developer
    apiGroup: rbac.authorization.k8s.io
```

## User authentication and monitoring:

Check what acces `User` has:

```console
kubectl auth can-i create RESOURCE --as USER-TYPE
```

Authenticate a `User`:

```console
curl −v −k https://master−node−ip:6443/api/v1/pods −u "user1:password1"
```

or from a `Token` file:

```console
curl −v −k https://master−node−ip:6443/api/v1/pods −-token-auth-file=TOKEN-DETAILS.csv
```

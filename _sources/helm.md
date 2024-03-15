(helm)=

# `Helm` configuration

`Helm` is a package manager for Kubernetes. 

## Charts
Assuming `Helm` is installed, it will use `charts` based on *aliases* in our
resource definitions:

```yaml
# pv-definition:
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv0003
spec:
  capacity:
    storage: { { .Values.storage } }
```

Where `.Values.storage` is defined in`values.yaml`:

```yaml
# values.yaml
storage: 20Gi
```

## Searching for Charts
Search for charts using: 
```console
helm search hub wordpress
```
And install chart using:
```console
helm install RELESE-NAME CHART-NAME
```
And update charts:
```console
helm upgrade [RELEASE] [CHART] [flags]
```

View charts:
```console
helm list
```


Deployment strategy is either `Recreate` or `RollingUpdate` (default).

Set depoyment stratergy

```yaml
# deployment-definitiion.yaml
spec:
  strategy:
    rollingUpdate:
      maxSurge: 1 # or 15 % 
      maxUnavailable: 2 # or 25 %
    type: RollingUpdate
```


(taints)=

# Taints, Tolerations, Labels, and Selectors

## Taints

**Nodes** have taints, and **pods** have tolerations.

Add taint with `TAINT-EFFECT` $\in$ [`NoSchedule`, `PreferNoSchedule`, `NoExecute`]

``` console
kubectl taint nodes NODENAME KEY=VALUE:TAINT-EFFECT
```

Remove taint:

``` console
kubectl taint nodes NODENAME KEY-
```

## Tolerations

Set toleration (declarative)

```yaml
# pod-definition.yaml
spec:
  tolerations:
    - key: "app"
      operator: "Equal"
      value: "blue"
      effect: "NoSchedule"
```

## Labels and Selectors

Setting `nodeSelector`:

```yaml
# pod-definition.yaml
spec:
  nodeSelector:
    size: Large # Labels assigned to nodes
```

Setting `nodeAffinity`

```yaml
# pod-definition.yaml
spec:
  affinity:
    nodeAffinity:
      [ AffinityType ]:
        nodeSelectorTerms:
          - matchExpressions:
              - key: size
                operator: In # [In, NotIn, Exists]
                values: # [Small, Medium, Large, YourLabelHere]
                  - Large
                  - Medium
```

with `AffinityTypes`:

```console
requiredDuringSchedulingIgnoredDuringExecution
preferreDuringSchedulingIgnoredDuringExecution
requiredDuringSchedulingRequiredDuringExecution
```

## Labels on other Kubernetes resources

Labels can also be set to **resources**. Check these with

``` console
kubectl get pods --selector KEY=VALUE
```

And set labels:

```yaml
# pod-definition.yaml
metadata:
  name: myapp
  labels:
    app: App1
    function: Front-end
```

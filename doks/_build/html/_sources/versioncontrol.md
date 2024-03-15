(vc)=

# Deployment strategy, Rollouts, and Rollbacks

## Deployment strategy

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

## Rollouts and Rollbacks

Rollout is triggered when a new version of the application is deployed.

Update image:

``` console
kubectl set image deployment DEPLOYMENT-NAME nginx-container=nginx:1.17
```

Rollback:

``` console
kubectl rollout undo deployment DEPLOYMENT-NAME
```

Check status:

``` console
kubectl rollout status/history deploy DEPLOYMENT-NAME
```


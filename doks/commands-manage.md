(cmd)=

# Monitoring resources with `kubectl`

## Monitoring

Create a TMP busybox image and enter shell:

```console
kubectl run busybox --image busybox --restart=Never -it --rm -- sh
```

Check resource

``` console
kubectl describe RESOURCE RESOURCE-NAME
```

Copy resources from `Pod` to local

```console
kubectl cp PODNAME:FILE-PATH-ON-POD LOCAL-PATH
```

Check number and names of secrets on volume

```console
kubectl exec −it POD-NAME −− ls /var/run/secrets/kubernetes.io/serviceaccount
```

Ping one POD from another POD

```console
kubectl exec −it POD-NAME −− sh
nc -v -z -w 2 SERVICE-TO-PING SERVICE-PORT
```

Check logs

```console
kubectl logs POD-NAME
```


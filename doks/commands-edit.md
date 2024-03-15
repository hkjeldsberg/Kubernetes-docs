(cmd-edit)=

# Editing resources with `kubectl`


## Editing resources
 
Change context

``` console
kubectl config use-context prod-user@production
```

Change namespace

``` console
kubectl config set-context --current --namespace=NAMESPACE
```

Add new labels to pods with specific label

```console
kubectl label po -l "KEY in(VALUE1,VALUE2)" NEW_KEY=NEW_VALUE
```

Scale resource

``` console
kubectl scale --replicas=10 RESOURCE RESOURCE-NAME
```

Edit resource

``` console
kubectl edit RESOURCE RESOURCE-NAME
```

Replace resource
```console
kubectl replace --force -f /tmp/my-config-tmp-file.yaml
```

Expose pod through service:
```console
kubectl expose pod POD-NAME −−port=PORT −−name SERVICE-NAME −−dry−run=client −o yaml
```

Edit `AdmissionController` in `kube-apiserver.yaml`, located here: `/etc/kubernetes/manifests/kube-apiserver.yaml`
````yaml
--enable-admission-plugin=AC1,AC2,ect.
````
Edit `authorization-mode`:
````yaml
--authorization-mode=Node,RBA
````
Edit `--runtime-config`:
````yaml
--runtime-config=batch/v2alpha2
````



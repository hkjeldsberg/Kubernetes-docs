(cmd-imp)=

# Imperative `kubectl` commands

## Imperative commands to create resources

Pods:

``` console
kubectl run NAME --image IMAGE:VERSION  --dry-run=client -o yaml > mypod.yaml
```

Containers:

``` console
kubectl create deployment --image=IMAGE:VERSION --port=EXPOSE-PORT --replicas=3 --dry-run=client -o yaml > mypod.yaml
```

Service (NodePort):

``` console
kubectl create svc nodeport NAME --tcp=PORT:TARGETPORT --node-port=NODEPORT 
```

Service (ClusterIP):

``` console
kubectl create svc clusterip NAME --tcp=PORT:TARGETPORT --node-port=NODEPORT 
```

ConfigMaps:

``` console
kubectl create cm CONFIG-NAME --from-literal=KEY=VALUE
kubectl create cm CONFIG-NAME --from-file=PATH-TO-FILE
```

Namespace

``` console
kubectl create ns NAMESPACE
```

Service account:

``` console
kubectl create serviceaccount NAME
```

Token:

``` console
kubectl create token SERVICEACCOUNT-NAME
```

Role:

```console
kubectl create role NAME --verb=[get,list,create,..] --resource=[pods,deployments,service,..]
```

Rolebinding:

```console
kubectl create rolebinding NAME --role=NAME --user=USERNAME  
```

Job

````console
kubectl create job NAME --image=image [--from=cronjob/name] -- [COMMAND] [args...] [options]
````

CronJob:

```console
kubectl create cronjob NAME --image=image --schedule='0/5 * * * ?' -- [COMMAND] [args...] [flags] [options]
```

Create a pod and expose it thorugh a service (will create both `Pod` and `Service`)

```console
kubectl run nginx --image=nginx --restart=Never --port=PORT-NUMBER --expose
```

Expose service to a deployment in different namespace:

```console
kubectl expose deployment redis --port=6379 --name=messaging-service --namespace=marketing
```

Create a API token for `ServiceAccount` user

```console
 kubectl create token SA-NAME
```

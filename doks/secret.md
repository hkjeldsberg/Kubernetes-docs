(secret)=

# `Secrets` and `SecurityContext`

## Secrets

Create secret:

``` console
kubectl create secret generic SECRET-NAME --from-literal=KEY=VALUE
kubectl create secret generic SECRET-NAME --from-file=FILE-PATH
```

Example `secrets-data.yaml` file:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
data:
  DB_Host: bXlzcWw=
  DB_User: cm0vdA==
  DB_Password: cGFzd3Jk
```

## Encoding and Decoding:

Encode using base64:

``` console
echo -n 'myphrase' | base64
```

Decode using base64:

``` console
echo -n 'bxLzcWw=' | base64 --decode
```

## Security context

Setting security context on POD level:

```yaml
# pod-configuration.yaml
spec:
  securityContext:
    runAsUser: 1000
```

or container level

```yaml
# pod-configuration.yaml
spec:
  containers:
    - name: ubuntu
      securityContext:
        runAsUser:1000
        capabilities:
          add: [ "MAC_ADMIN" ]
```


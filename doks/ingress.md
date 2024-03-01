(ingress)=

# `Ingress` and `NetworkPolicy`

## Ingress

Use a `Ingress` controller` with `Ingress` resource. `Ingress` resource can be created as follows:

```console
kubectl create ingress INGRESS-NAME −−rule="host/path=service:port"
```

Alternative declarative way:

```yaml
# ingress-def.yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  # URL SPLITTING
  rules:
    - http:
        paths:
          - path: /wear
            pathType: Prefix
            backend:
              service:
                name: wear-service
                port:
                  number: 80
  # DOMAIN AND HOST NAMES
  rules:
    - host: wear.mysyore.com
      http:
        paths:
          - pathType: Prefix
            path: /wear
            backend:
              service:
                name: wear-service
                port:
                  number: 80
```

## Network policies

Create a `NetworkPolicy` (`netpol`) with:

```yaml
# netpol-def.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: test-network-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
    - Ingress
    - Egress
  ingress:
    - from:
        - ipBlock:
            cidr: 172.17.0.0/16
            except:
              - 172.17.1.0/24
        - namespaceSelector:
            matchLabels:
              project: myproject
        - podSelector:
            matchLabels:
              role: frontend
     ports:
        - protocol: TCP
          port: 6379
  egress:
    # Using IP
    - to:
        - ipBlock:
            cidr: 10.0.0.0/24
    # Using labels / namespace
    - to:
      - namespaceSelector:
          matchLabels:
           kubernetes.io/metadata.name: space2
     ports:
        - protocol: TCP
          port: 5978
```


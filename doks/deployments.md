(deploy)=

# `Deployments`

The following `Deployment` template contains the most common `Deployment` fields, including `Pod` definition:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx-deploy
    type: front-end
  name: nginx-deploy
spec:
  replicas: 5
  selector:
    matchLabels:
      app: nginx-deploy
      type: front-end
  strategy: { }
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: nginx-deploy
        type: front-end
    spec:
      containers:
        - image: nginx:1.16
          name: nginx
          ports:
            - containerPort: 1337
          resources: { }
          # env: 
          # volumeMounts:  
          # command:
      # volumes:
```


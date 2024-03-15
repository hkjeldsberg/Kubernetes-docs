(replica)=

# `ReplicaSets`

A `ReplicaSet`'s purpose is to maintain a stable set of replica `Pods` running at any given time. As such, it is often
used to guarantee the availability of a specified number of identical `Pods`. The following `ReplicaSet` template
contains the most common `ReplicaSet` fields:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend
  labels:
    app: guestbook
    tier: frontend
spec:
  # modify replicas according to your case
  replicas: 3
  selector:
    matchLabels:
      tier: frontend
  template:
    metadata:
      labels:
        tier: frontend
    spec:
      containers:
        - name: nginx
          image: nginx:alpine
```


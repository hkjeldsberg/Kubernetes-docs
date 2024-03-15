(pods)=

# `Pods`

The following `Pod` template contains the most common `Pod` fields:

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: nginx
  name: nginx
spec:
  serviceAccountName: SA-NAME # Optional
  containers:
    - image: nginx:1.16
      name: nginx
      # PORST
      ports:
        - containerPort: 80
      # RESOURCES
      resources:
        requests:
          memory: "64Mi"
          cpu: "0.5"
        limits:
          memory: "128Mi"
          cpu: "500m"
      # COMMANDS
      command: [ '/bin/sh', '-c', "echo hello > myfile.log" ] # ENTRYPOINT in Dockerfile
      args: [ "10" ] # CMD in Dockerfile
      # ENVIRONMENTAL VARIABLES
      env: # Plain key value
        - name: APP_COLOR
          value: pink
        - name: TIME_CLOCK
          valueFrom:
            configMapKeyRef: # OR secretKeyRef
              name: my-config
              key: TIME_CLOCK_KEY
      # ENVIRONMENTAL VARIABLES from FILE
      envFrom:
        - configMapRef:
            name: env-configmap
        - secretRef:
            name: env-secrets
      # VOLUMES   
      volumeMounts:
        - name: host-volume
          mountPath: /foo
        - name: empty-volume
          mountPath: /opt/www/html
        - name: app-config-volume
          mountPath: /ect/config
  volumes:
    - name: host-volume
      hostPath:
        path: /data/mydata
    - name: empty-volume
      emptyDir: { }
    - name: app-config-volume
      configMap:
        name: app-config
    - name: secret-volume
      secret:
        secretName: mysecret2

```


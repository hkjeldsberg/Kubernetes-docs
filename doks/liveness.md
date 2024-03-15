(live)=

# `Readiness` and `Liveness` probes

## `Readiness` probe

Used to check readiness of containers. Alternatives include checking a HTTP request, a TCP socket or by executing a
command:

````yaml
# pod-definition.yaml
spec:
  # HTTP request
  containers:
    readinessProbe:
      httpGet:
        path: /api/ready
        port: 8080
  #  TCP socket 
  containers:
    readinessProbe:
      tcpSocket:
        port: 8080
  # Execute command 
  containers:
  readinessProbe:
    exec:
      command:
        - cat
        - /app/is_ready
````

## `Liveness` probe

A `Liveness` probe will check if a container is "healthy" or not. Can be configured declartively:

```yaml
spec:
  containers:
    livenessProbe:
      initialDelaySeconds: 10
      periodSeconds: 5
      failureThreshold: 8
      httpGet:
          path: /api/healthy
          port: 8008

```
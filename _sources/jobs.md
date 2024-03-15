(jobs)=

# `Jobs` and `CronJobs`

## Jobs in Kubernetes

First, adjust parameter `restartPolicy`, either `Always` or `Never` or `OnFailure` in POD definition. Then, add job
config:

````console
kubectl create job NAME --image=image [--from=cronjob/name] -- [COMMAND] [args...] [options]
````

Or declarative:

```yaml
# job-definition.yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: math-add-job
spec:
  completions: 3 # Optional! Determines the number of pods created
  parallelism: 3 # Optional. Adds parallel jobs
  backoffLimit: 6 # Optional. Number of retries before job is considered failed
  activeDeadlineSeconds: 30 # Determines how many seconds job is alive before terminated
  template:
    spec:
      containers:
        - name: math-add
          image: ubuntu
          command: [ ’expr’, ’3’, ’+’, ’2’ ]
      restartPolicy: Never
```

Create job, and observe:

```console
kubectl get jobs
```

## CronJobs in Kubernetes

Normal jobs run instantly, `CronJob``s run when scheduler:

```console
kubectl create cronjob NAME --image=image --schedule='0/5 * * * ?' -- [COMMAND] [args...] [flags] [options]
```

Or declarative:

```yaml
# cron-job-definition.yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: reporting-cron-job
spec:
  startingDeadlineSeconds: 17 # Terminate after 17 seconds
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      completions:3
    # Content of job-definiition.yaml
```

A normal `Job` can also be started using a `CronJob` as starting point:
```console
kubectl create job --from=cronjob/CRONJOB-NAME JOB-NAME
```




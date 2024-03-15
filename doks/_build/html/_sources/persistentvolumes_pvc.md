(pvc)=

# `PersistentVolume` and `PVC`

Standard volumes created in config file requires this for each POD. Not ideal for multiple PODS on multiple nodes.
Instead: manage storage more centrally using `PersistentVolumeClaim` (`pvc`) claiming a `PersistentVolume` (`pv`).

## `PersistentVolume`

Create a `PersistentVolume` with the following template:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: example-pv
spec:
  storageClassName: local-storage # Optional
  accessModes:
    - ReadWriteOnce # 
  capacity:
    storage: 1Gi
  # HOST PATH
  hostPath:
    path: /tmp/data
  # LOCAL PATH
  local:
    path: /mnt/disks/ssd1
  # BLOCK STORES
  awsElasticBlockStore: # Alternative to hostPath (!)
    volumeID: <vol-id>
  fsType: ext4
    persistentVolumeReclaimPolicy: Retain # [Delete, Retain, Recycle]
```

## `PersistentVolumeClaim`

And a corresponding `PersistentVolumeClaim`:

```yaml
# pvc-definition.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: myclaim
spec:
  storageClassName: local-storage # Optional
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 500Mi
```

## `Pod` claiming `PVC`

`PVC` is referenced to in a `Pod` definition:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pvc-pod
spec:
  containers:
    - name: myapp
      image: nginx
      volumeMounts:
        - mountPath: "/var/www/htlm"
          name: mypd
  volumes:
    - name: mypd
      persistentVolumeClaim:
      claimName: myclaim
```

## Access mode abbreviations:

```console
RWO - ReadWriteOnce
ROX - ReadOnlyMany
RWX - ReadWriteMany
RWOP - ReadWriteOncePod
```

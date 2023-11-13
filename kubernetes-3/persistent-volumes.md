```
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-datacenter
spec:
  storageClassName: "manual"
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/itadmin
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-datacenter
spec:
  storageClassName: "manual"
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
---
apiVersion: v1
kind: Pod
metadata:
  name: pod-data-center
  labels:
    app.kubernetes.io/name: pod-datacenter
spec:
  containers:
    - name: container-datacenter
      image: nginx:latest
      volumeMounts:
        - mountPath: /usr/local/apache2/htdocs
          name: shared-logs
  volumes:
    - name: shared-logs
      persistentVolumeClaim:
        claimName: pvc-datacenter
  restartPolicy: Always
---
apiVersion: v1
kind: Service
metadata:
  name: web-datacenter
spec:
  selector:
    app.kubernetes.io/name: pod-datacenter
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30008
  type: NodePort
```
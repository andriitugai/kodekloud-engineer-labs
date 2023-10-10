## Time Check

The Nautilus DevOps team want to create a time check pod in a particular Kubernetes namespace and record the logs. This might be initially used only for testing purposes, but later can be implemented in an existing cluster. Please find more details below about the task and perform it.


Create a pod called <span style='color:cyan'>**time-check**</span> in the <span style='color:cyan'>**nautilus**</span> namespace. This pod should run a container called time-check, container should use the busybox image with latest tag only and remember to mention tag i.e <span style='color:cyan'>**busybox:latest**</span>.

Create a config map called <span style='color:cyan'>**time-config**</span> with the data <span style='color:cyan'>**TIME_FREQ=3**</span> in the same namespace.

The time-check container should run the command: <span style='color:cyan'>**while true; do date; sleep $TIME_FREQ;done**</span> and should write the result to the location <span style='color:cyan'>**/opt/dba/time/time-check.log**</span>. Remember you will also need to add an environmental variable TIME_FREQ in the container, which should pick value from the config map TIME_FREQ key.

Create a volume <span style='color:cyan'>**log-volume**</span> and mount the same on <span style='color:cyan'>**/opt/dba/time**</span> within the container.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

### Solution
1. Create files

```nautilus-namespace.yaml```
```
apiVersion: v1
kind: Namespace
metadata:
  name: nautilus
  labels:
    name: nautilus
```
Or just
```
kubectl create namespace nautilus
```


```time-config-map.yaml```
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: time-config
  namespace: nautilus
data:
  TIME_FREQ: "3"
```

```time-check-box.yaml```
```
piVersion: v1
kind: Pod
metadata:
  name: time-check
  namespace: nautilus
  labels:
    app: time-check
spec:
  containers:
  - name: time-check
    image: busybox:latest
    command:
    - /bin/sh
    - -c
    - while true; do date; sleep $TIME_FREQ;done > /opt/dba/time/time-check.log
    env:
    - name: TIME_FREQ
      valueFrom:
        configMapKeyRef:
          name: time-config
          key: TIME_FREQ
    volumeMounts:
    - name: log-volume
      mountPath: "/opt/dba/time"
  volumes:
  - name: log-volume
```

2. Run
```
kubectl create -f nautilus-namespace.yaml
```
```
kubectl create -f time-config-map.yaml --namespace=nautilus
```
```
kubectl create -f time-check-pod.yaml --namespace=nautilus
```

3. Check
```
kubectl get pods --namespace=nautilus
```
```
kubectl exec -it --namespace=nautilus time-check -- /bin/sh
```
inside the Pod:
```
cat /opt/dba/time/time-check.log
```
```
exit
```

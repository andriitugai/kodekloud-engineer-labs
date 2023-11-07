### Solution

1. Create ```pod.yaml```:
```
apiVersion: v1
kind: Pod
metadata:
  labels:
  name: volume-share-nautilus
spec:
  containers:
  - image: centos:latest
    name: volume-container-nautilus-1
    command:
    - sleep
    - "3600"
    volumeMounts:
    - mountPath: /tmp/blog
      name: volume-share
  - image: centos:latest
    name: volume-container-nautilus-2
    command:
    - sleep
    - "3600"
    volumeMounts:
    - mountPath: /tmp/cluster
      name: volume-share
  volumes:
  - name: volume-share
    emptyDir: {}
```

2. Exec into the first container:
```
kubectl exec --stdin --tty volume-share-nautilus --container=volume-container-nautilus-1 -- /bin/bash
```
3. Create the file in the required directory:
```
echo "Hello" > /tmp/blog/blog.txt
```
4. Check:
```
cat /tmp/blog/blog.txt
```
5. Return to the ```jump_host```:
```
exit
```
6. Exec into the second container:
```
kubectl exec --stdin --tty volume-share-nautilus --container=volume-container-nautilus-2 -- /bin/bash
```
7. Check the file:
```
cat /tmp/cluster/blog.txt
```
8. Return to the ```jump_host```:
```
exit
```
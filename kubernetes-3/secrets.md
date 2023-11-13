```
k create secret generic blog --from-file=/opt/blog.txt 
```

```
export do="-o yaml --dry-run=client"
k run secret-nautilus --image=fedora:latest $do > pod.yaml
```

```
piVersion: v1
kind: Pod
metadata:
  labels:
    run: secret-nautilus
  name: secret-nautilus
spec:
  containers:
  - image: fedora:latest
    name: secret-container-nautilus
    command: ["sleep", "3600"]
    volumeMounts:
        - name: secret-volume
          readOnly: true
          mountPath: "/opt/games"
  volumes:
  - name: secret-volume
    secret:
      secretName: blog
```
## Create Replicaset in Kubernetes Cluster

The Nautilus DevOps team is going to deploy some applications on kubernetes cluster as they are planning to migrate some of their existing applications there. Recently one of the team members has been assigned a task to write a template as per details mentioned below:



Create a ReplicaSet using <span style='color:cyan'>**httpd**</span> image with <span style='color:cyan'>**latest**</span> tag only and remember to mention tag i.e <span style='color:cyan'>**httpd:latest**</span> and name it as <span style='color:cyan'>**httpd-replicaset**</span>.


Labels <span style='color:cyan'>**app**</span> should be <span style='color:cyan'>**httpd_app**</span>, labels <span style='color:cyan'>**type**</span> should be <span style='color:cyan'>**front-end**</span>.


The container should be named as <span style='color:cyan'>**httpd-container**</span>; also make sure replicas counts are <span style='color:cyan'>**4**</span>.


Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

### Solution

1. Create `httpd-replicaset.yaml`
```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: httpd-replicaset
  labels:
    app: httpd_app
    type: front-end
spec:
  selector:
    matchLabels:
      app: httpd_app
      type: front-end
  replicas: 4
  template:
    metadata:
      name: httpd-pod
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest
```

2. Run  
```
kubectl apply -f httpd-replicaset.yaml 
```
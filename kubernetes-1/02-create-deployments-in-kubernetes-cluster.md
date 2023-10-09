## Create Deployments in Kubernetes Cluster

The Nautilus DevOps team has started practicing some pods and services deployment on Kubernetes platform, as they are planning to migrate most of their applications on Kubernetes. Recently one of the team members has been assigned a task to create a deployment as per details mentioned below:


Create a deployment named <span style='color:cyan'>**nginx**</span> to deploy the application <span style='color:cyan'>**nginx**</span> using the image <span style='color:cyan'>**nginx:latest**</span> (remember to mention the tag as well)

_Note_: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

---------------------------------------------
### Solution
1. Create `nginx-deployment.yaml`
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
  labels:
    app: nginx
    tier: front-end
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2
  template:
    metadata:
      name: nginx-pod
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:latest
```

2. Run
`kubectl apply -f nginx-deployment.yaml`
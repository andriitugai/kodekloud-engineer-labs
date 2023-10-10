## Set Limits for Resources in Kubernetes

Recently some of the performance issues were observed with some applications hosted on Kubernetes cluster. The Nautilus DevOps team has observed some resources constraints, where some of the applications are running out of resources like memory, cpu etc., and some of the applications are consuming more resources than needed. Therefore, the team has decided to add some limits for resources utilization. Below you can find more details.


Create a pod named <span style='color:cyan'>**httpd-pod**</span> and a container under it named as <span style='color:cyan'>**httpd-container**</span>, use httpd image with latest tag only and remember to mention tag i.e <span style='color:cyan'>**httpd:latest**</span> and set the following limits:

Requests: <span style='color:cyan'>**Memory**</span>: <span style='color:cyan'>**15Mi**</span>, <span style='color:cyan'>**CPU**</span>: <span style='color:cyan'>**100m**</span>

Limits: <span style='color:cyan'>**Memory**</span>: <span style='color:cyan'>**20Mi**</span>, <span style='color:cyan'>**CPU**</span>: <span style='color:cyan'>**100m**</span>

Note: The <span style='color:cyan'>**kubectl**</span> utility on jump_host has been configured to work with the kubernetes cluster.

### Solution

1. Create ```httpd-pod.yaml```
```
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
  labels:
    app: httpd-app
    tier: front-end
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
    resources:
      requests:
        memory: "15Mi"
        cpu: "100m"
      limits:
        memory: "20Mi"
        cpu: "100m"
```

2. Run
```
kubectl apply -f httpd-pod.yaml
```
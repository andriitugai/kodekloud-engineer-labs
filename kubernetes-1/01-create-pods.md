## Create Pods

The Nautilus DevOps team has started practicing some pods and services deployment on Kubernetes platform as they are planning to migrate most of their applications on Kubernetes platform. Recently one of the team members has been assigned a task to create a pod as per details mentioned below:


Create a pod named <span style="color:cyan">**pod-httpd**</span> using <span style="color:cyan">**httpd**</span> image with <span style='color:cyan'>**latest**</span> tag only and remember to mention the tag i.e <span style="color:cyan">**httpd:latest**</span>.

Labels <span style='color:cyan'>**app**</span> should be set to <span style="color:cyan">**httpd_app**</span>, also container should be named as <span style="color:cyan">**httpd-container**</span>.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

---------------------------------------------
### Solution

1. Create `pod.yaml`
```
apiVersion: v1
kind: Pod
metadata:
  name: pod-httpd
  labels:
    app: httpd_app
spec:
  containers:
  - name: httpd-container
    image: httpd:latest
```

2. Run   
`kubectl apply -f pod.yaml`

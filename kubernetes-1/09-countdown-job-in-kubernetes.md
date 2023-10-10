## Countdown Job in Kubernetes

The Nautilus DevOps team is working on to create few jobs in Kubernetes cluster. They might come up with some real scripts/commands to use, but for now they are preparing the templates and testing the jobs with dummy commands. Please create a job template as per details given below:


Create a job <span style='color:cyan'>**countdown-datacenter**</span>.

The spec template should be named as <span style='color:cyan'>**countdown-datacenter**</span> (under metadata), and the container should be named as <span style='color:cyan'>**container-countdown-datacenter**</span>

Use image ubuntu with latest tag only and remember to mention tag i.e <span style='color:cyan'>**ubuntu:latest**</span>, and restart policy should be <span style='color:cyan'>**Never**</span>.

Use command <span style='color:cyan'>**sleep 5**</span>

Note: The <span style='color:cyan'>**kubectl**</span> utility on jump_host has been configured to work with the kubernetes cluster.

### Solution

1. Create ```countdown-datacenter-job.yaml```
```
apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-datacenter
spec:
  template:
    metadata:
      name: countdown-datacenter
    spec:
      containers:
      - name: container-countdown-datacenter
        image: ubuntu:latest
        command:
        - /bin/sh
        - -c
        - sleep 5
      restartPolicy: Never
```

2. Create the job:
```
kubectl apply -f countdown-datacenter-job.yaml
```

3. Check:
```
kubectl get jobs
```
```
kubectl describe jobs countdown-datacenter
```

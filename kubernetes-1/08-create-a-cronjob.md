## Create a CronJob

There are some jobs/tasks that need to be run regularly on different schedules. Currently the Nautilus DevOps team is working on developing some scripts that will be executed on different schedules, but for the time being the team is creating some cron jobs in Kubernetes cluster with some dummy commands (which will be replaced by original scripts later). Create a cronjob as per details given below:



Create a cronjob named <span style='color:cyan'>**nautilus**</span>.


Set Its schedule to something like <span style='color:cyan'>***/10 * * * ***</span>, you set any schedule for now.


Container name should be <span style='color:cyan'>**cron-nautilus**</span>.


Use httpd image with latest tag only and remember to mention the tag i.e <span style='color:cyan'>**httpd:latest**</span>.


Run a dummy command <span style='color:cyan'>**echo Welcome to xfusioncorp!**</span>.


Ensure restart policy is <span style='color:cyan'>**OnFailure**</span>.


Note: The <span style='color:cyan'>**kubectl**</span> utility on jump_host has been configured to work with the kubernetes cluster.

### Solution

1. Create ```nautilus-cronjob.yaml```
```
apiVersion: batch/v1
kind: CronJob
metadata:
  name: nautilus
spec:
  schedule: "*/10 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: cron-nautilus
            image: httpd:latest
            command:
            - /bin/sh
            - -c
            - echo Welcome to xfusioncorp!
          restartPolicy: OnFailure
```
2. Run
```
kubectl apply -f nautilus-cronjob.yaml 
```

3. Watch for a job:
```
kubectl get jobs --watch
``` 
Around 10 minutes we'll get
```
NAME                COMPLETIONS   DURATION   AGE
nautilus-28282160   0/1                      0s
nautilus-28282160   0/1           0s         0s
nautilus-28282160   0/1           4s         4s
nautilus-28282160   1/1           4s         4s
```

```
export pods=$(kubectl get pods --selector=job-name=nautilus-28282160 --output=jsonpath={.items[*].metadata.name})

kubectl logs $pods
```
Output
```
Welcome to xfusioncorp!
```
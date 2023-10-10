## Replication Controller

The Nautilus DevOps team wants to create a ReplicationController to deploy several pods. They are going to deploy applications on these pods, these applications need highly available infrastructure. Below you can find exact details, create the ReplicationController accordingly.


Create a ReplicationController using <span style='color:cyan'>**httpd**</span> image, preferably with <span style='color:cyan'>**latest**</span> tag, and name it as <span style='color:cyan'>**httpd-replicationcontroller**</span>.

Labels <span style='color:cyan'>**app**</span> should be <span style='color:cyan'>**httpd_app**</span>, and labels <span style='color:cyan'>**type**</span> should be <span style='color:cyan'>**front-end**</span>. The container should be named as <span style='color:cyan'>**httpd-container**</span> and also make sure replica counts are <span style='color:cyan'>**3**</span>.


All pods should be running state after deployment.


Note: The <span style='color:cyan'>**kubectl**</span> utility on jump_host has been configured to work with the kubernetes cluster.

### Solution

1. Create ```httpd-replicationcontroller.yaml```

```
apiVersion: v1
kind: ReplicationController
metadata:
  name: httpd-replicationcontroller
  labels:
    app: httpd_app
    type: front-end
spec:
  replicas: 3
  selector:
    app: httpd_app
    type: front-end
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
kubectl apply -f httpd-replicationcontroller.yaml
```

3. Check
## Rolling Updates in Kubernetes

We have an application running on Kubernetes cluster using nginx web server. The Nautilus application development team has pushed some of the latest changes and those changes need be deployed. The Nautilus DevOps team has created an image <span style='color:cyan'>**nginx:1.18**</span> with the latest changes.


Perform a rolling update for this application and incorporate <span style='color:cyan'>**nginx:1.18**</span> image. The deployment name is <span style='color:cyan'>**nginx-deployment**</span>

Make sure all pods are up and running after the update.

Note: The <span style='color:cyan'>**kubectl**</span> utility on jump_host has been configured to work with the kubernetes cluster.

### Solution
1. Run 
```
kubectl describe deployments nginx-deployment
```
Output:
```
Name:                   nginx-deployment
Namespace:              default
CreationTimestamp:      Tue, 10 Oct 2023 06:58:17 +0000
Labels:                 app=nginx-app
                        type=front-end
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=nginx-app
Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=nginx-app
  Containers:
   nginx-container:
    Image:        nginx:1.16
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   nginx-deployment-989f57c54 (3/3 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  5m1s  deployment-controller  Scaled up replica set nginx-deployment-989f57c54 to 3
```
2. Run
```
kubectl edit deployments nginx-deployment --record
```
3. Replace containers.image value
4. Check
```
kubectl describe deployments nginx-deployment
```

### Another way
1. Run
```
kubectl set image deployment nginx-deployment nginx-container:nginx:1.18 --record
```
2. Check 
```
kubectl rollout history deployment nginx-deployment
```
and 
```
kubectl describe deployments nginx-deployment
```




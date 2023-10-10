## Update Existing Deployment in Kubernetes

There is an application deployed on Kubernetes cluster. Recently, the Nautilus application development team developed a new version of the application that needs to be deployed now. As per new updates some new changes need to be made in this existing setup. So update the deployment and service as per details mentioned below:


We already have a deployment named nginx-deployment and service named nginx-service. Some changes need to be made in this deployment and service, make sure not to delete the deployment and service.

1.) Change the service nodeport from <span style='color:cyan'>**30008**</span> to <span style='color:cyan'>**32165**</span>

2.) Change the replicas count from <span style='color:cyan'>**1**</span> to <span style='color:cyan'>**5**</span>

3.) Change the image from <span style='color:cyan'>**nginx:1.19**</span> to <span style='color:cyan'>**nginx:latest**</span>

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

### Solution
Use
```
kubectl edit service ...
```
and
```
kubectl edit deployment ...
```
commands
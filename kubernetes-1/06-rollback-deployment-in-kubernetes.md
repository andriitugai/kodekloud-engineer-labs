## Rollback Deployment in Kubernetes

This morning the Nautilus DevOps team rolled out a new release for one of the applications. Recently one of the customers logged a complaint which seems to be about a bug related to the recent release. Therefore, the team wants to rollback the recent release.


There is a deployment named <span style='color:cyan'>**nginx-deployment**</span>; roll it back to the previous revision.

Note: The <span style='color:cyan'>**kubectl**</span> utility on jump_host has been configured to work with the kubernetes cluster.

### Solution

1. Run
```
kubectl rollout history deployments nginx-deployment
```

2. Run
```
kubectl rollout undo deployments nginx-deployment
```

3. Check
```
kubectl rollout history deployments nginx-deployment
```

## Create NameSpace in Kubernetes Cluster

The Nautilus DevOps team is planning to deploy some micro services on Kubernetes platform. The team has already set up a Kubernetes cluster and now they want set up some namespaces, deployments etc. Based on the current requirements, the team has shared some details as below:


Create a namespace named <span style='color:cyan'>**dev**</span> and create a POD under it; name the pod <span style='color:cyan'>**dev-nginx-pod**</span> and use <span style='color:cyan'>**nginx**</span> image with <span style='color:cyan'>**latest**</span> tag only and remember to mention tag i.e <span style='color:cyan'>**nginx:latest**</span>.

Note: The <span style='color:cyan'>**kubectl**</span> utility on jump_host has been configured to work with the kubernetes cluster.

### Solution

1. Create ```dev-ns.yaml```
```
apiVersion: v1
kind: Namespace
metadata:
  name: dev
  labels:
    name: dev
```

2. Run  
```
kubectl apply -f dev-ns.yaml
```

3. Create ```dev-nginx-pod.yaml```
```
apiVersion: v1
kind: Pod
metadata:
  name: dev-nginx-pod
  labels:
    app: nginx-app
    tier: front-end
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
```

4. Run  
```
kubectl apply -f dev-nginx-pod.yaml --namespace=dev
```

5. Check
```
kubectl describe pods dev-nginx-pod --namespace=dev
```
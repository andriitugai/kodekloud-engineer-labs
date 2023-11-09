### Rolling Updates and Rolling Back Deployments in Kubernetes

1. Create ```deploy.yaml```:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  namespace: datacenter
  name: httpd-deploy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: httpd
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxUnavailable: 2
      maxSurge: 1
  template:
    metadata:
      labels:
        app: httpd
    spec:
      containers:
      - name: httpd
        image: httpd:2.4.27
```

2. Create ```svc.yaml```:
```
apiVersion: v1
kind: Service
metadata:
  name: httpd-service
  namespace: datacenter
spec:
  type: NodePort
  selector:
    app: httpd
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```

3. Check deployment:
```
kubectl describe deployment httpd-deploy -n datacenter
```
Look at container.image

4. Upgrade the image:
```
kubectl set image deploy httpd-deploy httpd=httpd:2.4.43 -n datacenter --record=true
```

5. Check deployment:
```
kubectl describe deployment httpd-deploy -n datacenter
```
Look at container.image

6. Undo the last rollout:
```
kubectl rollout undo deployment httpd-deploy -n datacenter
```

7. Check deployment:
```
kubectl describe deployment httpd-deploy -n datacenter
```
Look at container.image
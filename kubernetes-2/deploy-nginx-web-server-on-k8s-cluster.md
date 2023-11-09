### Deploy NGINX web-server on K8s cluster

1. Create ```nginx.yaml```:
```
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx-app
    type: front-end
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30011

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx-app
    type: front-end
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-app
      type: front-end
  template:
    metadata:
      labels:
        app: nginx-app
        type: front-end
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
```

2.
```
kubectl apply -f nginx.yaml
```

3.
```
kubectl get pods
```

4. Check. Exec ```curl http://localhost``` on one of pods:
```
kubectl exec nginx-deployment-56cdb5d774-49rqs -- curl http://localhost
```
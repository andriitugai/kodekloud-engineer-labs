

1. Create namespace:
```
kubectl create ns jenkins
```

2. Create ```deploy-jenkins.yaml```:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: jenkins
  name: jenkins-deployment
  namespace: jenkins
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jenkins
  template:
    metadata:
      labels:
        app: jenkins
    spec:
      containers:
      - name: jenkins-container
        image: jenkins/jenkins
        ports:
        - containerPort: 8080
```

3. Create ```svc-jenkins.yaml```:
```
apiVersion: v1
kind: Service
metadata:
  name: jenkins-service
  namespace: jenkins
spec:
  type: NodePort
  selector:
    app: httpd
  ports:
    - port: 8080
      targetPort: 8080
      nodePort: 30008
```

4. 
```
kubectl apply -f svc-jenkins.yaml
```

5. 
```
kubectl apply -f deploy-jenkins.yaml
```

6. Check deployment, service

7. Check pods

8. Check:
```
kubectl exec jenkins-deployment-667887d68c-64bqt -n jenkins -- curl http://localhost:8080
```
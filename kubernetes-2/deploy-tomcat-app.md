### Deploy Tomcat Application on Kubernetes Cluster

1. Crete namespace:
```
kubectl create ns 
```

2. Create deployment:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: tomcat-deployment-devops
  name: tomcat-deployment-devops
  namespace: tomcat-namespace-devops
spec:
  replicas: 1
  selector:
    matchLabels:
      app: tomcat-devops
  template:
    metadata:
      labels:
        app: tomcat-devops
    spec:
      containers:
      - image: gcr.io/kodekloud/centos-ssh-enabled:tomcat
        name: centos-ssh-enabled
        ports:
        - containerPort: 8080
```

3. Create service:
```
apiVersion: v1
kind: Service
metadata:
  labels:
    app: tomcat-service-devops
  name: tomcat-service-devops
  namespace: tomcat-namespace-devops
spec:
  ports:
  - nodePort: 32227
    port: 8080
    protocol: TCP
    targetPort: 8080
  selector:
    app: tomcat-devops
  type: NodePort
```

4. Apply and Check
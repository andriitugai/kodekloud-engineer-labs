### Deploy Node Application

1. Create deployment:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nodeapp-deploy
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nodeapp
  template:
    metadata:
      labels:
        app: nodeapp
    spec:
      containers:
      - image: gcr.io/kodekloud/centos-ssh-enabled:node
        name: nodeapp-container
        ports:
        - containerPort: 8080
```

2. Create service:
```
apiVersion: v1
kind: Service
metadata:
  name: nodeapp-service
spec:
  ports:
  - nodePort: 30012
    port: 8080
    protocol: TCP
    targetPort: 8080
  selector:
    app: nodeapp
  type: NodePort
```

3. Apply and Check

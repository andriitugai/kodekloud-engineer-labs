### Deploy Grafana on Kubernetes Cluster

1. Create deployment:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-datacenter
spec:
  replicas: 2
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
      - image: grafana/grafana:latest
        name: grafana-container
        resources: {}
```

2. Create service:
```
apiVersion: v1
kind: Service
metadata:
  name: grafana-svc-datacenter
spec:
  ports:
  - nodePort: 32000
    port: 3000
    protocol: TCP
    targetPort: 3000
  selector:
    app: grafana
  type: NodePort
```

3. 
```
k apply -f <deployment>.yaml
k apply -f <service>.yaml
```

4. Check
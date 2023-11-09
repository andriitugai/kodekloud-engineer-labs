### Print Environment Variables

1. Create the file ```pod.yaml```

```
piVersion: v1
kind: Pod
metadata:
  name: print-envars-greeting
spec:
  containers:
  - image: bash
    name: print-env-container
    env:
    - name: GREETING
      value: "Welcome to"
    - name: COMPANY
      value: "DevOps"
    - name: GROUP
      value: "Industries"
    command: ["echo"]
    args: ["$(GREETING) $(COMPANY) $(GROUP)"]
```

2. Create the pod:
```
kubectl apply -f pod.yaml
```

3. Check:
```
kubectl get pods
```

4. Check
```
kubectl logs -f print-envars-greeting
```
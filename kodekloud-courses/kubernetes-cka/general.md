## Create YAML Template using kubectl

#### Create Pod template
```
kubectl run mypod --image=nginx:latest \
            --labels type=web \
            --dry-run=client -o yaml > mypod.yaml
```

#### Create Service template
```
kubectl create service nodeport mypod \
    --tcp=80:80 \
    --node-port=30001 \
    --dry-run=client -o yaml > mypod-service.yaml
```

#### Create Deployment template
```
kubectl create deployment mydeployment \
    --image=nginx:latest \
    --dry-run=client -o yaml > mydeployment.yaml
```

#### Create Job template
```
kubectl create job myjob \
    --image=nginx:latest \
    --dry-run=client -o yaml
```

#### Create CronJob template
```
kubectl create cj mycronjob \
    --image=nginx:latest \
    --schedule="* * * * *" \
    --dry-run=client -o yaml
```


## Aliases

```
alias k=kubectl
```

```
alias kdr='kubectl --dry-run=client -o yaml'
```


You can run it (CHECK IT!)
```
kdr create deployment my-deployment \
       --image=nginx:latest > deployment-definition.yaml
```
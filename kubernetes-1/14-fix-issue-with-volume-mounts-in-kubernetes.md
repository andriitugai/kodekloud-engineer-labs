## Fix Issue with Volume Mounts

We deployed a Nginx and PHP-FPM based setup on Kubernetes cluster last week and it had been working fine so far. This morning one of the team members made a change somewhere which caused some issues, and it stopped working. Please look into the issue and fix it:



The pod name is <span style='color:cyan'>**nginx-phpfpm**</span> and configmap name is <span style='color:cyan'>**nginx-config**</span>. Figure out the issue and fix the same.


Once issue is fixed, copy <span style='color:cyan'>**/home/thor/index.php**</span> file from the jump host to the nginx-container under nginx document root and you should be able to access the website using Website button on top bar.


Note: The <span style='color:cyan'>**kubectl**</span> utility on jump_host has been configured to work with the kubernetes cluster.

### Solution

```
kubectl describe configmap nginx-config
```

```
kubectl describe pod nginx-phpfpm
```

```
kubectl get pod nginx-phpfpm -o yaml  > /tmp/nginx.yaml
```

Edit the file /tmp/nginx.yaml.
Replace ALL entries of /usr/share/nginx/html with /var/www/html

```
kubectl replace -f /tmp/nginx.yaml --force
```

```
/home/thor/index.php  nginx-phpfpm:/var/www/html -c nginx-container
```

Check.

Or check with ```curl```:
```
kubectl exec -it nginx-phpfpm -c nginx-container  -- curl -I  http://localhost:8099
```
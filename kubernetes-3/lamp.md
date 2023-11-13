

```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: lamp-wp
  name: lamp-wp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: lamp-wp
  template:
    metadata:
      labels:
        app: lamp-wp
    spec:
      containers:
      - image: webdevops/php-apache:alpine-3-php7
        name: httpd-php-container
        ports:
        - containerPort: 80
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: database
              key: MYSQL_ROOT_PASSWORD
        - name: MYSQL_DATABASE
          valueFrom:
            secretKeyRef:
              name: database
              key: MYSQL_DATABASE
        - name: MYSQL_USER
          valueFrom:
            secretKeyRef:
              name: database
              key: MYSQL_USER
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: database
              key: MYSQL_PASSWORD
        - name: MYSQL_HOST
          valueFrom:
            secretKeyRef:
              name: database
              key: MYSQL_HOST
        volumeMounts:
        - name: php-ini
          mountPath: /opt/docker/etc/php/php.ini
          subPath: php.ini
               
      - image: mysql:5.6
        name: mysql-container
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: database
              key: MYSQL_ROOT_PASSWORD
        - name: MYSQL_DATABASE
          valueFrom:
            secretKeyRef:
              name: database
              key: MYSQL_DATABASE
        - name: MYSQL_USER
          valueFrom:
            secretKeyRef:
              name: database
              key: MYSQL_USER
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: database
              key: MYSQL_PASSWORD
        - name: MYSQL_HOST
          valueFrom:
            secretKeyRef:
              name: database
              key: MYSQL_HOST
        ports:
        - containerPort: 3306
      volumes:
      - name: php-ini
        configMap:
          name: php-config
```

```
apiVersion: v1
kind: Service
metadata:
  name: mysql-service
spec:
  selector:
    app: lamp-wp
  ports:
    - protocol: TCP
      port: 3306
      targetPort: 3306
```

```
apiVersion: v1
kind: ConfigMap
metadata:
  creationTimestamp: null
  name: php-config
data:
  php.ini:
    variables_order = "EGPCS"
```

```
apiVersion: v1
kind: Service
metadata:
  labels:
    app: lamp-wp
  name: lamp-service
spec:
  ports:
  - nodePort: 30008
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: lamp-wp
  type: NodePort
```
```
k create secret generic database --from-literal MYSQL_ROOT_PASSWORD=admin123 --from-literal MYSQL_DATABASE=kodekloud --from-literal MYSQL_USER=dbuser --from-literal MYSQL_PASSWORD=password123 --from-literal MYSQL_HOST=mysql-service
```
```
<?php
$dbname = $_ENV["MYSQL_DATABASE"];
$dbuser = $_ENV["MYSQL_USER"];
$dbpass = $_ENV["MYSQL_PASSWORD"];
$dbhost = $_ENV["MYSQL_HOST"];

$connect = mysqli_connect($dbhost, $dbuser, $dbpass) or die("Unable to Connect to '$dbhost'");

$test_query = "SHOW TABLES FROM $dbname";
$result = mysqli_query($test_query);

if ($result->connect_error) {
   die("Connection failed: " . $conn->connect_error);
}
  echo "Connected successfully";
```
## Apache Troubleshooting

xFusionCorp Industries uses some monitoring tools to check the status of every service, application, etc running on the systems. Recently, the monitoring system identified that <span style='color:cyan'>**Apache service**</span> is not running on some of the Nautilus Application Servers in Stratos Datacenter.



1. Identify the faulty Nautilus Application Server and fix the issue. Also, make sure Apache service is up and running on all Nautilus Application Servers. Do not try to stop any kind of firewall that is already running.


2. Apache is running on 8083 port on all Nautilus Application Servers and its document root must be <span style='color:cyan'>**/var/www/html**</span> on all app servers.


3. Finally you can test from jump host using curl command to access Apache on all app servers and it should be reachable and you should get some static page. E.g. <span style='color:cyan'>**curl http://172.16.238.10:8083/**</span>.

### Solution 
1. SSH to the servers

2. Try to start ```httpd``` service:
```
sudo systemctl status httpd
sudo sytemctl start httpd
```
3. In case of issue arises:

* look at the error
```
sudo systemctl status httpd.service
```

* locate the error:
```
cat -n /etc/httpd/conf/httpd.conf | grep 34
```
( 34 here is number of line with the error)

* fix the error
```
sudo vi /etc/httpd/conf/httpd.conf 
```

* try to start ```httpd``` again
```
sudo systemctl start httpd
```
4. Enable ```httpd```
```
sudo systemctl enable httpd
```

5. Check (from jump server)
```
curl http://172.16.238.10:8083
```

6. That's it folks!

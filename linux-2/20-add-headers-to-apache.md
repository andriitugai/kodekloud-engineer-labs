## Add headers

We are working on hardening Apache web server on <span style='color:cyan'>**all app servers**</span>. As a part of this process we want to add some of the Apache response headers for security purpose. We are testing the settings one by one on all app servers. As per details mentioned below enable these headers for Apache:


Install httpd package on App Server 2 using yum and configure it to run on <span style='color:cyan'>**8086**</span> port, make sure to start its service.


Create an <span style='color:cyan'>**index.html**</span> file under Apache's default document root i.e <span style='color:cyan'>**/var/www/html**</span> and add below given content in it.


Welcome to the xFusionCorp Industries!


Configure Apache to enable below mentioned headers:


<span style='color:cyan'>**X-XSS-Protection**</span> header with value <span style='color:cyan'>**1**</span>; mode=block


<span style='color:cyan'>**X-Frame-Options**</span> header with value <span style='color:cyan'>**SAMEORIGIN**</span>


<span style='color:cyan'>**X-Content-Type-Options**</span> header with value <span style='color:cyan'>**nosniff**</span>


Note: You can test using <span style='color:cyan'>**curl**</span> on the given app server as LBR URL will not work for this task.

### Solution

1. SSH to the server

2. 
```
sudo yum install -y httpd
```
3.
```
sudo vi /var/www/html/index.html
```
Add ```Welcome to the xFusionCorp Industries!``` line to the file

4.
```
sudo vi /etc/httpd/conf/httpd.conf
```
* Update ```Listen 80``` line to ```Listen 8086```
* Append lines
```
Header set X-XSS-Protection "1; mode=block"
Header always append X-Frame-Options SAMEORIGIN
Header set X-Content-Type-Options nosniff
```
in the very end.

5. Enable and start httpd.

6. Logout from the server

7. Check the headers:
```
curl -i http://stapp02:8086
``` 


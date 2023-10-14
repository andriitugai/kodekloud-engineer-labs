## Linux firewalld setup

To secure our Nautilus infrastructure in Stratos Datacenter we have decided to install and configure <span style='color:cyan'>**firewalld**</span> on <span style='color:cyan'>**all app servers**</span>. We have Apache and Nginx services running on these apps. Nginx is running as a reverse proxy server for Apache. We might have more robust firewall settings in the future, but for now we have decided to go with the given requirements listed below:



a. Allow all incoming connections on Nginx port, i.e <span style='color:cyan'>**80**</span>.

b. Block all incoming connections on Apache port, i.e <span style='color:cyan'>**8080**</span>.

c. All rules must be permanent.

d. Zone should be public.

e. If Apache or Nginx services aren't running already, please make sure to start them.

### Solution
1. SSH to servers
2. Install firewalld
```
sudo yum install -y firewalld 
sudo systemctl start firewalld
sudo systemctl enable firewalld
```

```
sudo systemctl enable nginx
sudo systemctl enable httpd
```
```
sudo firewall-cmd --permanent --zone=public --add-port=80/tcp
sudo firewall-cmd --permanent --zone=public --remove-port=8080/tcp
```


```
sudo grep -i Listen /etc/httpd/conf/ht*
```
```
sudo systemctl restart firewalld
sudo systemctl status firewalld
sudo firewall-cmd --list-all --zone=public
```
3. Done
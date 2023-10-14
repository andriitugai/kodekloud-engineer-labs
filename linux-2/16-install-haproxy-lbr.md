## Install HAproxy LBR

There is a static website running in Stratos Datacenter. They have already configured the app servers and code is already deployed there. To make it work properly, they need to configure LBR server. There are number of options for that, but team has decided to go with HAproxy. FYI, apache is running on port 8084 on all app servers. Complete this task as per below details.



a. Install and configure HAproxy on LBR server using yum only and make sure all app servers are added to HAproxy load balancer. HAproxy must serve on default http port (Note: Please do not remove stats socket /var/lib/haproxy/stats entry from haproxy default config.).

b. Once done, you can access the website using StaticApp button on the top bar.

### Solution
1. Enable ```httpd``` services on all App servers. Note http port listening
2. SSH to ```stlb01``` server
3. Install ```haproxy```
```
sudo yum install -y haproxy
```
```
sudo vi /etc/haproxy/haproxy.cfg
```
Set frontend port to listen to to 80
Edit backend info:
server stapp01 172.16.238.10:8084 check
server stapp02 172.16.238.11:8084 check
server stapp03 172.16.238.12:8084 check

```
sudo haproxy -f /etc/haproxy/haproxy.conf
```
```
sudo systemctl enable haproxy 
sudo systemctl start haproxy 
sudo systemctl status haproxy 
```
4. Logout from Loki

5. Check
```
curl 172.16.238.14:80
```
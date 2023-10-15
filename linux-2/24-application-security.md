## Application Security

We have a backup management application UI hosted on Nautilus's <span style='color:cyan'>**backup server**</span> in Stratos DC. That backup management application code is deployed under Apache on the backup server itself, and Nginx is running as a reverse proxy on the same server. Apache and Nginx ports are <span style='color:cyan'>**8082**</span> and <span style='color:cyan'>**8095**</span>, respectively. We have iptables firewall installed on this server. Make the appropriate changes to fulfill the requirements mentioned below:



We want to open all incoming connections to Nginx's port and block all incoming connections to Apache's port. Also make sure rules are permanent.

## Solution

1. SSH to ```stbkp01```

2. 
Check the status of ```iptables```

```
sudo systemctl status iptables
```
Start it (if any)
```
sudo systemctl start iptables
```
Look at existing rules
```
sudo iptables -L --line-numbers
```
Add the new rules
```
sudo iptables -A INPUT -p tcp --destination-port 8082 -j DROP
```
```
sudo iptables -A INPUT -p tcp --destination-port 8095 -j ACCEPT
```
Check rules
```
sudo iptables -L -n -v
```
Save new rules
```
sudo service iptables save
```
```
sudo systemctl enable iptables
sudo systemctl status iptables
```   
The Nautilus system admins team recently deployed a web UI application for their backup utility running on the Nautilus backup server in Stratos Datacenter. The application is running on port 8087. They have firewalld installed on that server. The requirements that have come up include the following:



Open all incoming connection on <span style='color:cyan'>**8087/tcp**</span> port. Zone should be <span style='color:cyan'>**public**</span>.


### Solution
1. SSH to the server
2. Run
```
sudo firewall-cmd --zone=public --add-port=8087/tcp
```
3. Done
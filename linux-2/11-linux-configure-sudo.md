## Linux configure sudo

We have some users on all app servers in Stratos Datacenter. Some of them have been assigned some new roles and responsibilities, therefore their users need to be upgraded with sudo access so that they can perform admin level tasks.



a. Provide sudo access to user <span style='color:cyan'>**mark**</span> on all app servers.


b. Make sure you have set up password-less <span style='color:cyan'>**sudo**</span> for the user.


### Solution

1. SSH to the servers
2. Check if mark exists 
```
sudo id mark
```
3. Add mark to the ```/etc/sudoers```
```
sudo visudo
```
```
sudo cat /etc/sudoers | grep mark
```
```
mark     ALL=(ALL)   NOPASSWD:ALL
```

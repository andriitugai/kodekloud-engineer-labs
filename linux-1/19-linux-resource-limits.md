On our <span style='color:cyan'>**Storage**</span> server in Stratos Datacenter we are having some issues where <span style='color:cyan'>**nfsuser**</span> user is holding hundred of processes, which is degrading the performance of the server. Therefore, we have a requirement to limit its maximum processes. Please set its maximum process limits as below:



a. soft limit = <span style='color:cyan'>**1024**</span>


b. hard_limit = <span style='color:cyan'>**2025**</span>


### Solution
1. SSH to the server
2. Edit file 
```
/etc/security/limits.conf
```
add
```
nfsuser           soft    nproc           1024
nfsuser           hard    nproc           2025
```
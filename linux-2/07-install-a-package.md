## Install a Package

As per new application requirements shared by the Nautilus project development team, serveral new packages need to be installed on all app servers in Stratos Datacenter. Most of them are completed except for net-tools.



Therefore, install the <span style='color:cyan'>**net-tools**</span> package on all <span style='color:cyan'>**app-servers**</span>.

### Solution
1. SSH to the servers
2. Run
```
sudo yum update -y
sudo yum install -y net-tools
```
## Linux services

As per details shared by the development team, the new application release has some dependencies on the back end. There are some packages/services that need to be installed on all app servers under Stratos Datacenter. As per requirements please perform the following steps:



a. Install <span style='color:cyan'>**httpd**</span> package on <span style='color:cyan'>**all the application servers**</span>.


b. Once installed, make sure it is enabled to start during boot.

### Solution

1. SSH to the servers
2. Run
```
sudo yum install -y httpd
```

3. Start and enable ```httpd```:
```
sudo systemctl start httpd
```
```
sudo systemctl enable httpd
```

4. Check:
```
sudo systemctl status httpd
```
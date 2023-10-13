## Linux Collaborative Directories

The Nautilus team doesn't want its data to be accessed by any of the other groups/teams due to security reasons and want their data to be strictly accessed by the <span style='color:cyan'>**devops**</span> group of the team.



Setup a collaborative directory <span style='color:cyan'>**/devops/data**</span> on <span style='color:cyan'>**app server 3**</span> in Stratos Datacenter.


The directory should be group owned by the group <span style='color:cyan'>**devops**</span> and the group should own the files inside the directory. The directory should be read/write/execute to the user and group owners, and others should not have any access.

### Solution
1. SSH to the server
2. Run
```
sudo mkdir -p /devops/data
```
3. Change dir's owner group to the ```devops```:
```
sudo chgrp -R devops /devops/data
```
4. Modify the file permissions in the directory:
```
sudo chmod -R 2770 /devops/data 
```
Here 2 is special permissions set group ID - files are executed with the authority of user's group. 
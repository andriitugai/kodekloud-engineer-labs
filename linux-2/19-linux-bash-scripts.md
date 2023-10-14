## Linux Bash Scripts

The production support team of xFusionCorp Industries is working on developing some bash scripts to automate different day to day tasks. One is to create a bash script for taking websites backup. They have a static website running on App Server 1 in Stratos Datacenter, and they need to create a bash script named <span style='color:cyan'>**ecommerce_backup.sh**</span> which should accomplish the following tasks. (Also remember to place the script under <span style='color:cyan'>**/scripts**</span> directory on <span style='color:cyan'>**App Server 1**</span>).



a. Create a zip archive named <span style='color:cyan'>**xfusioncorp_ecommerce.zip**</span> of <span style='color:cyan'>**/var/www/html/ecommerce**</span> directory.


b. Save the archive in <span style='color:cyan'>**/backup/**</span> on App Server 1. This is a temporary storage, as backups from this location will be clean on weekly basis. Therefore, we also need to save this backup archive on <span style='color:cyan'>**Nautilus Backup Server**</span>.


c. Copy the created archive to <span style='color:cyan'>**Nautilus Backup Server**</span> server in <span style='color:cyan'>**/backup/**</span> location.


d. Please make sure script won't ask for password while copying the archive file. Additionally, the respective server user (for example, tony in case of App Server 1) must be able to run it.

### Solution
1. SSH to the server
2. Create backup script
```
vi /scripts/blog_backup.sh
```
```
cat /scripts/blog_backup.sh
```
```
#!/bin/bash
zip -r /backup/xfusion_blog.zip /var/www/html/blog
scp /backup/xfusion_blog.zip clint@stbkp01:/backup
```
3. Generate ssh key
```
ssh-keygen
```
```
ssh-copy-id clint@stbkp01
```
Now you can login into ```stbkp01``` as ```clint``` without password. Check:
```
ssh clint@stbkp01
```
close connection to the ```stbkp01```

4. Run script
5. SSH to the ```stbkp01``` and check the result.

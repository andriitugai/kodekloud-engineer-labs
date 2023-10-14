## Configure Local YUM repos

The Nautilus production support team and security team had a meeting last month in which they decided to use local yum repositories for maintaing packages needed for their servers. For now they have decided to configure a local yum repo on <span style='color:cyan'>**Nautilus Backup Server**</span>. This is one of the pending items from last month, so please configure a local yum repository on <span style='color:cyan'>**Nautilus Backup Server**</span> as per details given below.



a. We have some packages already present at location <span style='color:cyan'>**/packages/downloaded_rpms/**</span> on <span style='color:cyan'>**Nautilus Backup Server**</span>.


b. Create a yum repo named <span style='color:cyan'>**local_yum**</span> and make sure to set <span style='color:cyan'>**Repository ID**</span> to <span style='color:cyan'>**local_yum**</span>. Configure it to use package's location <span style='color:cyan'>**/packages/downloaded_rpms/**</span>.


c. Install package <span style='color:cyan'>**vim-enhanced**</span> from this newly created repo.

### Solution
1. SSH to the server
2. Check if any repo is available:
```
sudo yum repolist
```
```
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

No repositories available
```
3. Create the local repo
```
sudo vi /etc/yum.repos.d/local_yum.repo
```
Insert the lines
```
[local_yum]
name=local_yum
baseurl=file:///packages/downloaded_rpms/
enabled=1
gpgcheck=0
```
4. Check 
```
sudo yum repolist
```
```
Updating Subscription Management repositories.
Unable to read consumer identity

This system is not registered with an entitlement server. You can use subscription-manager to register.

repo id                                             repo name
local_yum                                           local_yum
```
5. Run 
```
sudo yum install -y vim-enhanced
```

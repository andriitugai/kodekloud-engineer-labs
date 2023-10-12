
To stick with the security compliances, the Nautilus project team has decided to apply some restrictions on crontab access so that only allowed users can create/update the cron jobs. Limit crontab access to below specified users on <span style='color:cyan'>**App Server 3**</span>.



Allow crontab access to <span style='color:cyan'>**javed**</span> user and deny the same to <span style='color:cyan'>**jerome**</span> user.

### Solution
1. SSH to the server
2. Create ```/etc/cron.deny``` and ```/etc/cron.allow``` files
3. The files have to contain usernames who are allowed and denied access to the crontab. If file ```/etc/cron.allow``` exists - only listed users can use ```crontab```
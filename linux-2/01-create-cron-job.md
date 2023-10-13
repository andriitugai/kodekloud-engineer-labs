The Nautilus system admins team has prepared scripts to automate several day-to-day tasks. They want them to be deployed on <span style='color:cyan'>**all app servers**</span> in Stratos DC on a set schedule. Before that they need to test similar functionality with a sample cron job. Therefore, perform the steps below:



a. Install ```cronie``` package on all Nautilus app servers and start ```crond``` service.


b. Add a cron ```*/5 * * * * echo hello > /tmp/cron_text``` for root user.

### Solution
1. SSH to the server
2. Run
```
sudo yum install -y cronie
```
3.
```
sudo systemctl start crond
```
```
sudo systemctl status crond
```

4. Open crontab editor with
```
sudo crontab -e
```
Add a line ```*/5 * * * * echo hello > /tmp/cron_text``` and save the file

5. After 5 min look at ```/tmp/cron_text```
## Linux Log Rotate

The Nautilus DevOps team is ready to launch a new application, which they will deploy on app servers in Stratos Datacenter. They are expecting significant traffic/usage of <span style='color:cyan'>**httpd**</span> on app servers after that. This will generate massive logs, creating huge log files. To utilise the storage efficiently, they need to compress the log files and need to rotate old logs. Check the requirements shared below:



a. In <span style='color:cyan'>**all app servers**</span> install <span style='color:cyan'>**squid**</span> package.


b. Using <span style='color:cyan'>**logrotate**</span> configure <span style='color:cyan'>**squid**</span> logs rotation to monthly and keep only <span style='color:cyan'>**3**</span> rotated logs.


(If by default log rotation is set, then please update configuration as needed)

### Solution

1. SSH to the servers
2. 
```
sudo yum install -y squid
```
3. 
```
sudo vi /etc/logrotate.d/squid
```
```
sudo cat /etc/logrotate.d/squid
```
```
/var/log/squid/*.log {
    monthly
    rotate 3
    compress
    notifempty
    missingok
    nocreate
    sharedscripts
    postrotate
      # Asks squid to reopen its logs. (logfile_rotate 0 is set in squid.conf)
      # errors redirected to make it silent if squid is not running
      /usr/sbin/squid -k rotate 2>/dev/null
      # Wait a little to allow Squid to catch up before the logs is compressed
      sleep 1
    endscript
}
```

4. Make ```squid``` service enabled and started.
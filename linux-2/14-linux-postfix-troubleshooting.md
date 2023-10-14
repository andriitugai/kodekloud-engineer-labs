## Linux Postfix troubleshooting


xFusionCorp Industries has planned to set up a common email server in Stork DC. After several meetings and recommendations they have decided to use <span style='color:cyan'>**postfix**</span> as their <span style='color:cyan'>**mail transfer agent**</span> and <span style='color:cyan'>**dovecot**</span> as an <span style='color:cyan'>**IMAP/POP3 server**</span>. We would like you to perform the following steps:



1. Install and configure <span style='color:cyan'>**postfix**</span> on Stork DC mail server.


2. Create an email account <span style='color:cyan'>**jim@stratos.xfusioncorp.com**</span> identified by <span style='color:cyan'>**YchZHRcLkL**</span>.


3. Set its mail directory to <span style='color:cyan'>**/home/jim/Maildir**</span>.


4. Install and configure <span style='color:cyan'>**dovecot**</span> on the same server.

### Solution

sudo yum install -y postfix
    5  sudo yum install -y dovecot
    6  sudo systemctl status postfix
    7  sudo systemctl start postfix
    8  sudo systemctl status postfix.service
    9  sudo vi /etc/postfix/main.cf
   10  sudo systemctl start postfix
   11  sudo systemctl enable postfix
   12  sudo systemctl start dovecot
   13  sudo systemctl enable dovecot
   14  sudo useradd jim
   15  sudo passwd jim
   16  sudo ls /home/jim
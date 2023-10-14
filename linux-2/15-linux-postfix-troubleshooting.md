## Linux postfix troubleshooting

Some users of the monitoring app have reported issues with xFusionCorp Industries mail server. They have a mail server in Stork DC where they are using <span style='color:cyan'>**postfix**</span> mail transfer agent. Postfix service seems to fail. Try to identify the root cause and fix it.

### Solution

1. SSH to the server
2. Comment on ```local_interfaces: localhost``` line
```
sudo vi /etc/postfix/main.cf
```
3. Done



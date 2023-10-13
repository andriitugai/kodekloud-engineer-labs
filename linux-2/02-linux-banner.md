## Linux Banner

During the monthly compliance meeting, it was pointed out that several servers in the Stratos DC do not have a valid banner. The security team has provided serveral approved templates which should be applied to the servers to maintain compliance. These will be displayed to the user upon a successful login.



Update the message of the day on <span style='color:cyan'>**all application and db servers**</span> for Nautilus. Make use of the approved template located at <span style='color:cyan'>**/home/thor/nautilus_banner**</span> on jump host

### Solution

1. Coppy the banner_file to all the application and db servers with comman like:
```
scp /home/thor/nautilus_banner tony@172.16.238.10:/home/tony/
```
2. SSH to the server
3. Run
```
sudo cp nautilus_banner /etc/
```
4. In file ```/etc/ssh/sshd_config``` replace line
```#Banner none``` to ```Banner /etc/nautilus_banner```

5. Restart `sshd` daemon
```
sudo systemctl restart sshd
```
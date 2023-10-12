## Linux Archives

On Nautilus storage server in Stratos DC, there is a storage location named /data, which is used by different developers to keep their data (non confidential data). One of the developers named john has raised a ticket and asked for a copy of their data present in /data/john directory on storage server. /home is a FTP location on storage server itself where developers can download their data. Below are the instructions shared by the system admin team to accomplish this task.



a. Make a <span style='color:cyan'>**john.tar.gz**</span> compressed archive of <span style='color:cyan'>**/data/john**</span> directory and move the archive to <span style='color:cyan'>**/home**</span> directory on Storage Server.

### Solution
SSH to storage server, than

```
sudo ls -la /data
```
```
sudo tar -czvf john.tar.gz /data/john
```
```
sudo ls -la
```
```
sudo mv john.tar.gz /home/
```
Check
```
sudo ls -la /home/
```

Done.
## Linux Find Command

During a routine security audit, the team identified an issue on the Nautilus App Server. Some malicious content was identified within the website code. After digging into the issue they found that there might be more infected files. Before doing a cleanup they would like to find all similar files and copy them to a safe location for further investigation. Accomplish the task as per the following requirements:



a. On <span style='color:cyan'>**App Server 3 at**</span> location <span style='color:cyan'>**/var/www/html/blog**</span> find out all files (not directories) having .php extension.


b. Copy all those files along with their <span style='color:cyan'>**parent directory structure **</span>to location <span style='color:cyan'>**/blog**</span> on same server.


c. Please make sure not to copy the entire <span style='color:cyan'>**/var/www/html/blog**</span> directory content.


### Solution

1. SSH to the server
2. Go to the directory:
```
sudo cd /var/www/html/blog
```

3. Run
```
sudo find . -type f -name "*.php" -exec cp --parents {} /blog \;
```

4. Check
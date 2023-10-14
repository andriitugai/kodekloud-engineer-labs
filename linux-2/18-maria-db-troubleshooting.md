## Maria DB Troubleshooting

There is a critical issue going on with the Nautilus application in Stratos DC. The production support team identified that the application is unable to connect to the database. After digging into the issue, the team found that <span style='color:cyan'>**mariadb**</span> service is down on the <span style='color:cyan'>**database**</span> server.



Look into the issue and fix the same.

### Solution 

1. SSH to DB Server

2. The issue, as I realise, can be different, so try to check ownership of dirs
```/var/lib/mysql``` and ```/var/run/mariadb```
They should be owned by mysql
Fix (if any) with command 
```
sudo chown mysql:mysql /var/lib/mysql
```

3. Good luck


One of the Nautilus project developers need access to run docker commands on App Server 3. This user is already created on the server. Accomplish this task as per details given below:



User yousuf is not able to run docker commands on App Server 3 in Stratos DC, make the required changes so that this user can run docker commands without sudo.

```
sudo getent group docker
```

```
sudo usermod -aG docker yousuf
```

To check login as root:

```
sudo su -
```

and then login as ```yousuf```

```
docker --version
```

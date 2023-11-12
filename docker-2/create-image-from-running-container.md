One of the Nautilus developer was working to test new changes on a container. He wants to keep a backup of his changes to the container. A new request has been raised for the DevOps team to create a new image from this container. Below are more details about it:


a. Create an image ```beta:devops``` on Application Server 1 from a container ```ubuntu_latest``` that is running on same server.

1. Check the current state:
```
docker ps
```

```
docker
```

2. Save all the changes to the container:
```
docker commit <name_of_the_running_container>
```

3. Check:
```
docker images
```

```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
<none>              <none>              23331b185a62        6 seconds ago       124MB
ubuntu              latest              e4c58958181a        5 weeks ago         77.8MB
```

4. Tag the new image:
```
docker tag 23331b185a62 beta:devops
```

5. Check:
```
docker images
```

```
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
beta                devops              23331b185a62        About a minute ago   124MB
ubuntu              latest              e4c58958181a        5 weeks ago          77.8MB
```
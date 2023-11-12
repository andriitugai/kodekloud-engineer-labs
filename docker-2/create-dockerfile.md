### Description

As per recent requirements shared by the Nautilus application development team, they need custom images created for one of their projects. Several of the initial testing requirements are already been shared with DevOps team. Therefore, create a docker file /opt/docker/Dockerfile (please keep D capital of Dockerfile) on App server 1 in Stratos DC and configure to build an image with the following requirements:



a. Use ubuntu as the base image.


b. Install apache2 and configure it to work on 5003 port. (do not update any other Apache configuration settings like document root etc).

1. Create ```/opt/docker/Dockerfile```

```
FROM ubuntu:latest
RUN apt-get update && apt-get install -y apache2
RUN echo "Listen 5003" >> /etc/apache2/ports.conf
RUN sed -i 's/Listen 80/Listen 5003/g' /etc/apache2/sites-available/000-default.conf
EXPOSE 5003
CMD ["apachectl", "-D", "FOREGROUND"]
```

2. 
```
cd /opt/docker/Dockerfile
```

```
sudo docker build -t custom-apache2-image
```

3. Run the container:
```
sudo docker run -d -p 5003:5003 apache-custom-image:latest
```

4. Check:
```
curl -I http://localhost:5003
```

```
HTTP/1.1 200 OK
Date: Sun, 12 Nov 2023 16:12:56 GMT
Server: Apache/2.4.52 (Ubuntu)
Last-Modified: Sun, 12 Nov 2023 16:05:22 GMT
ETag: "29af-609f6b87bf480"
Accept-Ranges: bytes
Content-Length: 10671
Vary: Accept-Encoding
Content-Type: text/html
```
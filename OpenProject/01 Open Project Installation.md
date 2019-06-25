### Install Docker
[Install Docker and Docker Compose (Centos 7) · NaturalHistoryMuseum/scratchpads2 Wiki · GitHub](https://github.com/NaturalHistoryMuseum/scratchpads2/wiki/Install-Docker-and-Docker-Compose-(Centos-7))


### Install OpenProject
```bash
docker run -d -p 8080:80 -e SECRET_KEY_BASE=secret\
openproject/community:8
```
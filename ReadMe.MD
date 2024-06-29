# Docker Containers

Container is a runtime version of a docker image
It is completely isolated from the host and has its own file system
It can be stopped, restart and delete at any point in time.

# Docker Desktop

It is a containerization software for developers and teams.

Install Docker Desktop -> https://www.docker.com/products/docker-desktop/

- docker build -t getting-started .
- docker run -dp 127.0.0.1:3000:3000 getting-started
- docker ps
- docker rm container-id
- docker rm -f $(docker ps -aq)

## Docker Containers

Container is a runtime version of a docker image
It is completely isolated from the host and has its own file system
It can be stopped, restart and delete at any point in time.

## Docker Desktop

It is a containerization software for developers and teams.

Install Docker Desktop -> https://www.docker.com/products/docker-desktop/

- docker build -t getting-started .
- docker run -dp 127.0.0.1:3000:3000 getting-started
- docker ps
- docker rm container-id
- docker rm -f $(docker ps -aq)
- docker volume create todo-app
- docker exec -it containerid
- docker run -it containerid ls

- docker run -d ubuntu bash -c "shuf -i 1-10000 -n 1 -o /data.txt && tail -f /dev/null"

### to persist the data in db

- docker run -dp 127.0.0.1:3000:3000 --mount type=volume,src=todo-db,target=/etc/todos getting-started

### to connect multiple container together we need network

- docker network create todo-app

- docker run -d \
   --network todo-app --network-alias mysql \
   -v todo-mysql-data:/var/lib/mysql \
   -e MYSQL_ROOT_PASSWORD=secret \
   -e MYSQL_DATABASE=todos \
   mysql:8.0

- docker exec -it containeridofmysql mysql -u root -p

### Now to connect getting started with mysql do the following

- Stop the running container of getting-started or your application

- docker run -dp 127.0.0.1:3000:3000 \
  -w /app -v "$(pwd):/app" \
  --network todo-app \
  -e MYSQL_HOST=mysql \
  -e MYSQL_USER=root \
  -e MYSQL_PASSWORD=secret \
  -e MYSQL_DB=todos \
  node:18-alpine \
  sh -c "yarn install && yarn run dev"

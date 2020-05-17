Dockerizing full-stack project
===================
## Table of Contents

- [Prerequisities](#prerequisities)
- [DockerFile](#dockerfile)
- [Docker-compose](#docker-compose)
- [Docker Run](#docker-run)

## Prerequisities


In order to run this container you'll need docker installed.

* [Windows](https://docs.docker.com/windows/started)
* [OS X](https://docs.docker.com/mac/started/)
* [Linux](https://docs.docker.com/linux/started/)


## DockerFile

Dockerfile is used to create a docker container.

```bash
# command for build front image
docker build -t frontend -f DockerFile .

# command for build back image
docker build -t backend -f DockerFile .
```

## Docker-compose

Compose is a tool for defining and running multi-container Docker applications.

`services` uses an image that’s built from the Dockerfile in the current directory. It then connects the container and the host machine to the exposed port, 3000 for the frontend and 8080 for the backend.

`links` allows to connect the backend service to the mongodb service

```bash
version: "2"
services:
  frontend:
    build: frontend
    ports:
      - "3000:3000"
  backend:
    build: backend
    ports:
      - "8080:8080"
    links:
      - mongodb
  mongodb:
    container_name: mongodb
    image: mongo
    ports:
      - 27017:27017

```

## Docker Run

```bash
# command for starts the containers
docker-compose up --build
```

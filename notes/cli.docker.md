---
id: d8271043-f2b8-4bba-8227-9bf0e0556491
title: Docker
desc: ''
updated: 1643447549550
created: 1626794728508
---

# Docker
Docker commands

## Examples
```bash
## Test out Docker is working
docker run hello-world

## Run bash in container
docker run -it <container> /bin/bash

## Run bash in container that is already started
docker exec -it <container> /bin/bash
```

## Issues

### Got permission denied while trying to connect to the Docker daemon socket
Full Error might look like the following
`Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.40/containers/json: dial unix /var/run/docker.sock: connect: permission denied`
Fix by running the following in terminal:
```bash
sudo chmod 666 /var/run/docker.sock
```

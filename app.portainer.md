---
id: b25f543e-1cbd-45c1-814d-2d245f4a12c5
title: Portainer
desc: ''
updated: 1634663059678
created: 1613837966053
---

# Portainer

## Runing in Docker
```sh
## Create a volume
docker volume create portainer_data

## Install and run in portainer
docker run -d \
-p 8000:8000 \
-p 9000:9000 \
--name=portainer \
--restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v portainer_data:/data \
portainer/portainer

## Install and run portainer agent (can then use portainer to connect to the agent)
docker run -d \
-p 9001:9001 \
--name portainer_agent \
--restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v portainer_agent_data:/var/lib/docker/volumes \
portainer/agent:latest

## Now that your new Portainer container is up and running, you can access it at http://dockerhostip:9000.


```
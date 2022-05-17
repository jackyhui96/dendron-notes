---
id: 502bf670-56f4-41ef-ab3b-5b05703bd407
title: Tautulli
desc: ''
updated: 1613464001557
created: 1613463997632
---

# Tautulli

## Running using Docker
```sh
docker run -d \
  --name=tautulli \
  --restart=unless-stopped \
  -v <path to data>:/config \
  -e PUID=<uid> \
  -e PGID=<gid> \
  -e TZ=<timezone> \
  -p 8181:8181 \
  tautulli/tautulli

## e.g.

docker run -d \
  --name=tautulli \
  --restart=unless-stopped \
  -v /usr/local/docker_apps/tautulli/config:/config \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/London \
  -p 8181:8181 \
  tautulli/tautulli
```
## Updating with docker
- Stop the Tautulli container: `docker stop tautulli`
- Remove the Tautulli container: `docker rm tautulli`
- Pull the latest update `docker pull tautulli/tautulli`
- Run the Tautulli container with the same parameters as before: `docker run -d ...`
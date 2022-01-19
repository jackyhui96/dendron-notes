---
created: 2022-01-19T21:19:17+00:00
modified: 2022-01-19T21:41:12+00:00
---

# Grocy

```sh
docker run -d \
  --name=grocy \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Europe/London \
  -p 9283:80 \
  -v /usr/local/docker_apps/grocy/config:/config \
  --restart unless-stopped \
  lscr.io/linuxserver/grocy:arm32v7-latest
```

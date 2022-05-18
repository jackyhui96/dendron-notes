---
id: ynvyojd8rxo87nwy7gxj3ea
title: Grocy
desc: ''
updated: 1652817063128
created: '2022-01-19T21:19:17.000Z'
modified: '2022-01-19T21:52:45.000Z'
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

Fixed libseccomp following https://docs.linuxserver.io/faq#libseccomp

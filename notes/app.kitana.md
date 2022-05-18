---
id: 25210a99-0d6a-4df6-af95-8ed2835f1063
title: Kitana
desc: ''
updated: 1624538644094
created: 1619952139691
---

# Kitana
Kitana is used for plex plugins


## install with Docker
```sh
docker run --name kitana --restart unless-stopped -v kitana_data:/usr/local/docker_apps/kitana -d -p 0.0.0.0:31337:31337 pannal/kitana:latest -B 0.0.0.0:31337
```

---
id: 19b67356-8767-4a7e-bb63-9176afa9f1f2
title: Plexmediaserver
desc: ''
updated: 1636054762895
created: 1599322955852
---

# Plexmediaserver

## $PLEX_HOME Location
/var/lib/plexmediaserver/

## Move the installation
Steps work for linux Plex Media Server (**PMS**), see reference for other OS.
1. Disable emptying of trash on **source PMS**
  1.1 disabe `Settings > Library > Empty trash automatically after every scan` preference for server
2. Install **PMS** on the **destination** server
3. Sign out and stop the **destination PMS**, sign out using `settings > server > general`
4. Copy Server Data from **source PMS**
  4.1 stop the plex server
  4.2 data is stored at `/var/lib/plexmediaserver/Library/Application Support/Plex Media Server/`
  4.3 compress the files by using `tar`, then copy to **destination PMS**, 
5. Copy additional settings - **\*Not needed for linux, as done in previous step\***
6. Make sure the copied files are owned by `plex:plex`
7. Reboot the **destination PMS** server
8. Start the **destination PMS** application
9. Open Plex Web App **(PWA)**
10. Sign Out and Back into the Server
11. Edit your libraries, 
  11.1 edit library and add appropriate folder for where content is located on the **destination PMS**
12. Scan the library, click on `Scan Library Files` on the Plex Media App
13. Remove old content location, when you can verify that all of your content is working
14. Final Maintenance
  14.1 Turn `Empty trash automatically after every scan` in the **PWA**
  14.2 `Empty Trash` on the **PWA**
  14.3 `Clean Bundles` on the **PWA**, wait couple of minutes after dialog exits
  14.4 `Optimize Database` on the **PWA**

_Reference: https://support.plex.tv/articles/201370363-move-an-install-to-another-system/_

## Repair a Corrupt Database
Follow the steps in the reference to fix issues with media getting stuck in the 'Continue Watching' section despite being marked as unplayed.

_Reference: [Plex:Repair a Corrupt Database](https://support.plex.tv/articles/201100678-repair-a-corrupt-database/?_ga=2.121149832.1231479726.1601827334-1128507795.1600200934)_


## Docker install
```sh
docker run -d \
  --name=plex \
  --net=host \
  -e PUID=1000 \
  -e PGID=1000 \
  -e VERSION=docker \
  -v /usr/local/docker_apps/plex/config:/config \
  -v /media/usb1:/media \
  --restart unless-stopped \
  linuxserver/plex:arm32v7-latest
```

### Support
```sh
## Shell access whilst the container is running:
docker exec -it plex /bin/bash

## To monitor the logs of the container in realtime:
docker logs -f plex

## Container version number
docker inspect -f '{{ index .Config.Labels "build_version" }}' plex

## Image version number
docker inspect -f '{{ index .Config.Labels "build_version" }}' linuxserver/plex:arm32v7-latest
```

### Error update libseccomp2
`libc++abi: terminating with uncaught exception of type std::__2::system_error: clock_gettime(CLOCK_MONOTONIC) failed: Operation not permitted`

Add the backports repo for DebianBuster:
```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 04EE7237B7D453EC 648ACFD622F3D138
echo "deb http://deb.debian.org/debian buster-backports main" | sudo tee -a /etc/apt/sources.list.d/buster-backports.list
sudo apt update
sudo apt install -t buster-backports libseccomp2
```

---
id: e363cde0-76cb-4f3b-91c9-7709ebbbc04f
title: Pihole
desc: ''
updated: 1614422739147
created: 1613900690739
---

# PiHole

## Running in Docker
```sh
## Create persistent volumes
docker volume create pihole
docker volume create dnsmasq

## Pull the armv7 build (https://hub.docker.com/layers/pihole/pihole/latest/images/sha256-6f8e902adb26cf10220763d1ab027b0b2c64e2df3a397e4f015ead7a1c40d96c?context=explore) - doing this as --platform linux/arm/v7 could not find image, despite it being on DockerHub
docker pull pihole/pihole@sha256:6f8e902adb26cf10220763d1ab027b0b2c64e2df3a397e4f015ead7a1c40d96c

## Docker tag 
docker tag 1b529812cd4b pihole/pihole:armv7

## Run pihole
docker run -d \
--name=pihole \
-e TZ=Europe/London \
-e WEBPASSWORD=YOURPASS \
-e ServerIP=YOUR.SERVER.IP \
-v pihole:/etc/pihole \
-v dnsmasq:/etc/dnsmasq.d \
-p 80:80 \
-p 192.168.208.102:53:53/tcp \
-p 192.168.208.102:53:53/udp \
--restart=unless-stopped \
pihole/pihole:armv7

## e.g.

docker run -d \
--name=pihole \
-e TZ=Europe/London \
-e WEBPASSWORD=change_this_password \
-e ServerIP=192.168.208.102 \
-v pihole:/etc/pihole \
-v dnsmasq:/etc/dnsmasq.d \
-p 80:80 \
-p 192.168.208.102:53:53/tcp \
-p 192.168.208.102:53:53/udp \
--restart=unless-stopped \
pihole/pihole:armv7
```

## Solve DNS resolution in other containers when using PiHole in Docker
Found that when using wireguard in docker on the the same docker host as pihole.
wireguard could not correctly use pihole.
This is solved in the the following link:
_https://discourse.pi-hole.net/t/solve-dns-resolution-in-other-containers-when-using-docker-pihole/31413/2_

## Adding custom DNS entries
Write a file ending in `.conf` in the dnsmasq folder - defautls to `/etc/dnsmasq.d`
The file should have the following syntax:
```sh
host-record=mydomain.duckdns.org,192.168.1.10
address=/printer.lan/192.168.2.9
```
After making changes, run th follwing to restart the pihole dns
`pihole restartdns`

## Whitelist the following on this URL
_https://discourse.pi-hole.net/t/commonly-whitelisted-domains/212_

## Blacklist the following (optional)
Based on `/u/AtariDump` reddit comment https://www.reddit.com/r/pihole/comments/jtr6eb/default_adlists/
`/u/Wally3K` https://firebog.net/
`/u/LightSwitch05` https://www.github.developerdan.com/hosts/
Regex list: https://github.com/mmotti/pihole-regex/blob/master/regex.list


## Seeing lots of queries for lb._dns-sd._udp.<IP_ADDRESS>.in-addr.arpa
_https://github.com/pi-hole/pi-hole/issues/2654_

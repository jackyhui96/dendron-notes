---
id: 792ced21-aea6-42c6-ac34-c4e613bbb374
title: Wireguard
desc: ''
updated: 1614451360150
created: 1613812652776
---

# Wireguard

## Possible pre-req
After getting a vague error which said `Kernel headers not available, sleeping now`, the following possible solution is below
```sh
## Not sure if the below fixed it or not but this was run first
sudo apt install --reinstall libraspberrypi0 libraspberrypi-{bin,dev,doc} raspberrypi-bootloader raspberrypi-kernel

## Running the below and restarting fixed the issue 
sudo apt update && sudo apt upgrade -y

```

## Running with Docker
```sh
docker run -d \
--name=wireguard \
--cap-add=NET_ADMIN \
--cap-add=SYS_MODULE \
-e PUID=1000 \
-e PGID=1000 \
-e TZ=[YOURTZ] \
-e SERVERURL=[YOURIP] \
-e SERVERPORT=51820 \
-e PEERS=[PEERS] \
-e PEERDNS=auto \
-e INTERNAL_SUBNET=10.13.13.0 \
-p 51820:51820/udp \
-v [VOLUME]:/config \
-v /lib/modules:/lib/modules \
--restart unless-stopped \
linuxserver/wireguard

## e.g.

docker run -d \
--name=wireguard \
--cap-add=NET_ADMIN \
--cap-add=SYS_MODULE \
-e PUID=1000 \
-e PGID=1000 \
-e TZ=Europe/London \
-e SERVERURL=xujunjie-pi.hopto.org \
-e SERVERPORT=51820 \
-e PEERS=3 \
-e PEERDNS=192.168.208.102 \
-e INTERNAL_SUBNET=10.13.13.0 \
-p 51820:51820/udp \
-v /usr/local/docker_apps/wireguard/config:/config \
-v /lib/modules:/lib/modules \
--restart unless-stopped \
linuxserver/wireguard
```

## Output
After you execute the docker run command, the container will install the required kernel headers for your operating system to be able to effectively run Wireguard. Depending on your system this process could take a few minutes.

After the container setup process is completed, the terminal will display QR codes. Do not close your window, you will need to scan these QR codes later. You can scan these QR codes with the mobile applications to instantly create the Wireguard profile on your mobile devices. The QR codes are the easiest and quickest way to get Wireguard up and running on your mobile devices.

## MTU fixes
```sh
## Add the below to the PostUp section of the server config
iptables -A FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu

## Add the below to the PostDown section of the server config
iptables -D FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --clamp-mss-to-pmtu
```
_Reference: https://keremerkan.net/posts/wireguard-mtu-fixes/_


## References
_https://codeopolis.com/posts/installing-wireguard-in-docker/_
_https://github.com/linuxserver/docker-wireguard_

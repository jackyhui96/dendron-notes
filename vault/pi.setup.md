---
id: 67215e28-78b6-443a-916e-43d247a4dd2d
title: Setup
desc: ''
updated: 1613464414649
created: 1613464405744
---

# Setting up the Raspberri Pi

## Setup Steps
- Flash SD card
- Enable ssh following the instructions below
- Change password using `passwd` for the pi user
- Set the country using `raspi-config` in the locale options select `en_GB.UTF-8` and `en_US.UTF-8`
- Install vim `sudo apt install vim`
- Install docker 

## Enable SSH
SSH is disabled by default, enable this by adding an empty file named `ssh` to the boot partition of the SD card (this is the only folder that will appear to Windows)

## Installing Docker
1. Update and upgrade `sudo apt-get update && sudo apt-get upgrade -y`
2. Download install script `curl -fsSL https://get.docker.com -o get-docker.sh` and execute `sudo sh get-docker.sh`
3. Add `pi` user to the docker group `sudo usermod -aG docker pi` (log out and in for changes to take place)
4. Check docker version and info: `docker version` and `docker info`
5. Run hello world test container `docker run hello-world`

## Uninstalling Docker
Delete using package manager: 
`sudo apt-get purge docker-ce`
Remove leftover images, containers, volumes and other data: 
`sudo rm -rf /var/lib/docker`
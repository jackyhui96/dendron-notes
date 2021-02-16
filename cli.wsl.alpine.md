---
id: c671e95d-c5ee-4567-90af-de3931accfd8
title: Alpine
desc: ''
updated: 1613403910534
created: 1613387590453
---

# Alpine

## Setup
```bash
## VSCode
apk update && apk add libstdc++

## Bash
apk update && apk upgrade && apk add bash
apk add bash-doc
apk add bash-completion

## Set Bash as login shell
vi /etc/passwd

### Docker Desktop setup to WSL2
## Install ca-certificates and wget
apk add ca-certificates wget

## Download install package key
wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub

## Download package
wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.32-r0/glibc-2.32-r0.apk

## Install package
apk add glibc-2.32-r0.apk

## Set alpine as default wsl distro (run in powershell)
wsl --set-default alpine

## Install Docker Desktop (https://docs.docker.com/docker-for-windows/wsl/)

## Install Docker CLI
apk add docker-cli

```


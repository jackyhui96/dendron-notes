---
id: dht3mkak28doa7e54t57fvz
title: Yum
desc: ''
updated: 1656674990367
created: 1656674876193
---

# yum
* package manager for centos
* uses `rpms`

## Examples
```bash
## Install a new package:
yum install <package>

## Install a new package and assume yes to all questions (also works with update, great for automated updates):
yum -y install <package>

## Find the package that provides a particular command:
yum provides <command>

## Remove a package:
yum remove <package>

## Display available updates for installed packages:
yum check-update

## Upgrade installed packages to the newest available versions:
yum upgrade

## List installed packages
yum list installed
```

---
id: c3acb8fd-fcae-4210-8129-ab295e8d29e6
title: Ip
desc: ''
updated: 1614422554848
created: 1599406268504
---

# IP Address
Stuff about IP Address and setting the configuration

## Static IP Address
Setting a static IP addres will ensure that the server will use the same IP address all the time.
### Get Current IP Address
```sh
hostname -I
```

### Set a Static IP Address
Edit `/etc/network/interfaces` command and set your configuration
#### Example
```sh
auto eth0
iface eth0 inet static
        address 192.168.1.100 # current device ip
        netmask 255.255.255.0
        gateway 192.168.1.1 # modem gateway
```

#### Example using /etc/dhcpcd.conf
```sh
interface eth0

static ip_address=192.168.208.103/24
static routers=192.168.208.1
static domain_name_servers=8.8.8.8
```


### Connecting 2 routers together, one as DumbAP
_Reference: https://openwrt.org/docs/guide-user/network/wifi/dumbap_

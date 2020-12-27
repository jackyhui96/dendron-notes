---
id: c3acb8fd-fcae-4210-8129-ab295e8d29e6
title: Ip
desc: ''
updated: 1599406268504
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
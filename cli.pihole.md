---
id: ddee1e18-8001-4197-b214-056473af01ab
title: Pihole
desc: ''
updated: 1599318777035
created: 1599318777035
---

# PiHole

## Adding custom DNS entries
Write a file ending in `.conf` in the dnsmasq folder - defautls to `/etc/dnsmasq.d`
The file should have the following syntax:
```sh
host-record=mydomain.duckdns.org,192.168.1.10
address=/printer.lan/192.168.2.9
```
After making changes, run th follwing to restart the pihole dns
`pihole restartdns`
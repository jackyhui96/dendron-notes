---
id: 93a5dc42-8663-4d3c-924f-82e8faa35a67
title: Net
desc: ''
updated: 1609405007800
created: 1599406259569
---

## Network stuff

```sh
dzdo sh -c  firewall-cmd

dzdo sh -c "firewall-cmd --zone=public --add-port=1111/tcp"

nohup python -m SimpleHTTPServer 1111 &

dzdo sh -c "su -"

iptables -t nat -A PREROUTING -p tcp --dport 8888 -j REDIRECT --to-port 3860
```
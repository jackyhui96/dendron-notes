---
id: 93a5dc42-8663-4d3c-924f-82e8faa35a67
title: Net
desc: ''
updated: 1619436847216
created: 1599406259569
---

# Network stuff

```sh
dzdo sh -c  firewall-cmd

dzdo sh -c "firewall-cmd --zone=public --add-port=1111/tcp"

nohup python -m SimpleHTTPServer 1111 &
python -m SimpleHTTPServer 1111

dzdo sh -c "su -"

iptables -t nat -A PREROUTING -p tcp --dport 8888 -j REDIRECT --to-port 3860
```

## Test connections
```sh
# Connection successful:
$ timeout 1 bash -c 'cat < /dev/null > /dev/tcp/google.com/80'; echo $?
0

# Connection failure prior to the timeout
$ timeout 1 bash -c 'cat < /dev/null > /dev/tcp/google.com/80'
bash: google.com: Name or service not known
bash: /dev/tcp/google.com/80: Invalid argument
$ echo $?
1

# Connection not established by the timeout
$ timeout 1 bash -c 'cat < /dev/null > /dev/tcp/google.com/81'
$ echo $?
124

# master one liner
H=google.com; P=80; \
timeout 1 bash -c "cat < /dev/null > \"/dev/tcp/${H}/${P}\" "; RC=$?; \
[ "${RC}" == "0" ] && echo "${RC}: Connection successful"; \
[ "${RC}" == "1" ] && echo "${RC}: Connection failure prior to the timeout"; \
[ "${RC}" == "124" ] && echo "${RC}: Connection not established by the timeout"; \
[ "${RC}" != "0" -a "${RC}" != "1" -a "${RC}" != "124" ] && echo "${RC}: unknown result code";
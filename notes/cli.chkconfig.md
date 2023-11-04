---
id: 9ee14e63-98a6-4ac0-ba74-e7cea15966d8
title: Chkconfig
desc: ''
updated: 1657871153885
created: 1623228439638
---

# chkconfig
Used to autostart services on startup of linux servers

```sh
chkconfig --list collectd
chkconfig --add collectd
chkconfig collectd on
chkconfig metricbeat on

## for centos 7
systemctl is-enabled collectd
systemctl enable collectd
```

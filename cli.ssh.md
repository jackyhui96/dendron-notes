---
id: efc3885a-03cf-478f-9e3b-89b0c1810d72
title: Ssh
desc: ''
updated: 1609237660464
created: 1599322339965
---

# SSH

## No host checking and suppress SSH messages
```sh
ssh -qo "StrictHostKeyChecking no" ${TMUXHOST}
```

## Copying SSH key to remote-host
```sh
ssh-copy-id user@remote-host
```

## Copying SSH key to remote-host (Powershell one-liner)
```sh
type $env:USERPROFILE\.ssh\id_rsa.pub | ssh {IP-ADDRESS-OR-FQDN} "cat >> .ssh/authorized_keys"
```
## Bad owner or permission on c:\\Users\\user/.ssh/config (domain_name not used)
You get this error when you try to ssh in Windows 10 Powershell and the username and device name are the same i.e. jacky is the username, Jacky is name of the computer.
Fixed this by renaming the computer name.
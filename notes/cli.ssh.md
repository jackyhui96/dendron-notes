---
id: efc3885a-03cf-478f-9e3b-89b0c1810d72
title: Ssh
desc: ''
updated: 1647247921382
created: 1599322339965
---

# SSH

## No host checking and suppress SSH messages
```sh
ssh -qo "StrictHostKeyChecking no" ${TMUXHOST}

if [ ! -z "${TMUXHOST}" ]; then ssh -qo "StrictHostKeyChecking no" ${TMUXHOST}; fi
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

## Generating SSH keys
### Check for existing keys
```sh
## List files in .ssh directory
ls -al ~/.ssh

## Look for filenames such as:
# - id_rsa.pub
# - id_ecdsa.pub
# - id_ed25519.pub
```

### Generate new SSH key
```sh
ssh-keygen -t ed25519 -C "your_email@example.com"

## For legacy systems that can't run the above, use:
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

## Press enter for all prompts, or add a passphrase
```

### Add SSH key to ssh-agent
```sh
eval `ssh-agent -s`

## replaced filename with your private keyfile
ssh-add ~/.ssh/id_ed25519
```

### Add SSH key to GitHub
Copy contents of public file e.g. `~/.ssh/id_ed25519.pub`
Go to settings of GitHub and add new ssh key and paste contents.
SSH key looks like the following:
`ssh-ed25519 <HASH> <EMAIL_ADDRESS>`

### WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
`ssh-keygen -R [hostname]`

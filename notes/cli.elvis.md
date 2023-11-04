---
id: 69f94154-a07b-40e2-8322-14230a441697
title: Elvis
desc: ''
updated: 1665151104341
created: 1611321032487
---


# Elivis
## Run elvis against changes since git commit
elvis git-branch origin/HEAD


## my command
```sh
REPO=~/other-git-repos/elvis; ELVIS=${REPO}/_build/default/bin/elvis; CONFIG="${REPO}/elvis.config";
$ELVIS rock "src/refdata/gmi_refdata_config_ets.erl" --config $CONFIG
```

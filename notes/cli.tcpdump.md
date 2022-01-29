---
id: 90bd478b-7a43-4919-a4df-d0882e332b7e
title: Tcpdump
desc: ''
updated: 1652951770055
created: 1603122336925
---

# Tcpdump

## Examples

### Display traffic to and from a host
```sh
tcpdump -i any host 192.168.1.11
```

### Display incoming traffic on certain
```sh
tcpdump -i any port 8501 or port 8000 and dst host `hostname -s`
```

### grep http and awk tcp to be grepable
```
tcpdump -s 0 -nA 'tcp[((tcp[12:1] & 0xf0) >> 2):4] = 0x47455420' | awk '{ if (match($0, /^[0-9]/, _)) { printf (NR == 1 ? "%s " : "\n%s "), $0; fflush() } else { sub(/^\s+0x[0-9a-z]+:\s+/, " "); gsub(" ", ""); printf "%s", $0 } } END { print ""; fflush() }' | grep icl
```

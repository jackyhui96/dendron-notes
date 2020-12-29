---
id: af877716-9ab3-464e-a575-cde8d8ebbd8c
title: Awk
desc: ''
updated: 1609237758648
created: 1609237754433
---

# AWK

## Sum up lines
```sh
awk '{ sum += $NF } END { if (NR > 0) print sum }'
```
---
id: af877716-9ab3-464e-a575-cde8d8ebbd8c
title: Awk
desc: ''
updated: 1624981451424
created: 1609237754433
---

# AWK

## Sum up lines
```sh
awk '{ sum += $NF } END { if (NR > 0) print sum }'
```

## Sort by line length
```sh
awk '{ print length, $0 }' | sort -n -s | cut -d" " -f2-
```

## print line length
```sh
awk '{ print length }'
```

## Average of lines
```sh
awk '{ sum += $1; n++ } END { if (n > 0) print sum / n; }'
```
---
id: 92b8f111-16ee-460f-82f5-8f84c46ffcc0
title: Column
desc: ''
updated: 1609277308072
created: 1599590418255
---

# Column
Useful for tablulating data and padding whitespace between columns

## Flags
- -s, takes a separator to split the columns
- -t, creates a table (pretty prints columns with padded whitespace)

## Examples
```sh
cat file.csv | column -ts,
```

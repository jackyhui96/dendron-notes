---
id: 760405d2-be1b-478f-9002-9ec19f2fcd75
title: Tmux
desc: ''
updated: 1652951791613
created: 1609924416641
---

# Tmux

## Enable CTRL keys temp
```sh
C-b :set-window-option xterm-keys on
```

## Enter clock mode (useful for syncing a subset of panes)
* panes in clock mode ignore key strokes that are synced to all panes
* Enter clock mode: `C-b t`
* Exit clock mode: press any key in that pane

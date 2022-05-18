---
id: 013cdd92-74f7-45a0-850a-446b0364efb4
title: Wsl
desc: ''
updated: 1601825550232
created: 1601825550232
---

# Windows Subsystem for Linux (WSL)

## Common problems
### ls: cannot access '/mnt/c': Input/output error
Run the following command in Powershell to restart WSL:
```powershell
wsl.exe --shutdown
```
_Reference: https://github.com/microsoft/WSL/issues/4377_

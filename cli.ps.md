---
id: 070c81bd-10c7-4106-b57c-1a2691be1aeb
title: Ps
desc: ''
updated: 1618821259957
created: 1616503302967
---

# Powershell

## List services 
```powershell
Get-Service

# Don't truncate output
Get-Service | ft -auto
```
## Get Diskspace
```powershell
Get-CimInstance -Class CIM_LogicalDisk | Select-Object @{Name="Size(GB)";Expression={$_.size/1gb}}, @{Name="Free Space(GB)";Expression={$_.freespace/1gb}}, @{Name="Free (%)";Expression={"{0,6:P0}" -f(($_.freespace/1gb) / ($_.size/1gb))}}, DeviceID, DriveType | Where-Object DriveType -EQ '3'
```

## Find PID of service
```Powershell
$p=Tasklist /svc /fi "SERVICES eq <NAMW>" /fo csv | convertfrom-csv
$p.PID
```


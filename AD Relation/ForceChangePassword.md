```
$UserPassword = ConvertTo-SecureString 'Password123!' -AsPlainText -Force
Set-DomainUserPassword -Identity andy -AccountPassword $UserPassword -Credential $Cred
```
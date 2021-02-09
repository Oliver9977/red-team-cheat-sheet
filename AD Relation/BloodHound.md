```
Assembly /assemblyname:"SharpHound3" /parameters:"-c All GPOLocalGroup"
execute-assembly C:\tools\SharpHound3\SharpHound3\bin\Release\SharpHound.exe -c All GPOLocalGroup -D AMAZECORP.LOCAL
```
```
execute-assembly C:\NewTools\BloodHound-master\BloodHound-master\Ingestors\SharpHound.exe -c All
MATCH (c:Computer) where c.domain = "LAB.LOCAL" RETURN c
MATCH (c:User) where c.domain = "LAB.LOCAL" RETURN c
MATCH (c:Group) where c.domain = "LAB.LOCAL" RETURN c
```

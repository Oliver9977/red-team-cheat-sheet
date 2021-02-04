* hta + vba will be in ``32bit``
* There is x64 office just like  there is x64 windows xp ...

* Rundll32 with C# dll (https://blog.xpnsec.com/rundll32-your-dotnet/)
  * Rundll32 will require DLL_PROCESS_ATTACH to return
  * Ruldll32 will auto exit if entry point function exit 

```
ildasm.exe /out:TestUnmanaged.il CSharpDll.dll
ilasm.exe TestUnmanaged.il /DLL /output=TestUnamanged.dll /x64
```


* launch c# dll from c++ dll
```
HMODULE managedDLL = LoadLibraryA(targetedDll);
TestMethod managedMethod = (TestMethod)GetProcAddress(managedDLL, "MainFunc");
managedMethod();
```

* single cs file or c# dll to hta/js/vba/vbs
```
GadgetToJScript.exe -c test.cs -w [hta/js/vba/vbs]
GadgetToJScript.exe -a test.dll -w [hta/js/vba/vbs]
```
* GadgetToJScript requirement
  * entry point class is the first one in cs file
    ```
    public class MainClass{
        public MainClass(){
            //code here
        }
    }
    ```
  *  

* Net exe to shellcode
  * ```
    donut.exe test.exe
    $filename = "C:\tools\donut\loader.bin"
    [system.Convert]::toBase64string([IO.File]::ReadAllBytes($filename)) | Clip
    ```
  * 
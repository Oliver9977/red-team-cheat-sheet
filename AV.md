## Defender detailed behavior

* You are safe with powershell + AMSI bypassed (not mimikatz)
* ``explorer``'s ``CreateProcess`` function is not scaned
* Need to use at least ``AES`` for shellcodes
* ``Add-Type`` blocked by AMSI on server 2019

## List of blocked ps1
* powerview (need remove comments)

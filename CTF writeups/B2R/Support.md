HTB - Support (Easy) 
AD/Windows

**nmap**
`sudo nmap -sVC -p- -Pn -T5 10.10.11.174 -oN nmap`



---
**SMB**

check shares with `netexec
`nxc smb rhost -u '' -p '' --shares`

check shares with `anonymous/guest` user
`nxc smb rhost -u 'anonymous' -p '' --shares`
![[Pasted image 20250506122620.png]]

we can see ``IPC`` is a `Relative Identifier (rid)` so we can bruteforce it 
`nxc smb rhost -u 'anonymous' -p '' --shares --rid-brute


we can also see `support-tools` is also readable, so we can see its contents
`smbclient -U anonymous //rhost/support-tools`

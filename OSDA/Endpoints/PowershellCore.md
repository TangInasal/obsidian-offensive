## Remote Access with Powershell Core
Use powershell to connect remotely to other windows computers

**In Kali**
```
pwsh
Enter-PSSession -ComputerName  192.168.179.1 -Credential diox -Authentication Negotiate
```

## Remote Access with Powershell Core
Use powershell to connect remotely to other windows computers

**In Kali**
```
pwsh
Enter-PSSession -ComputerName  192.168.179.1 -Credential diox -Authentication Negotiate
```

---
#### Remote Access via Evil-WinRM
```
evil-winrm -i 192.168.179.1 -u Diox -p '<PASSWORD>'
```

**NOTE:** to be able to connect via Evil-WinRM
in local machine

check LocalAccountTokenFilterPolicy
```
Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "LocalAccountTokenFilterPolicy"
```

enable LocalAccountTokenFilterPolicy
```
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "LocalAccountTokenFilterPolicy" -Value 1 -Force
```

disable LocalAccountTokenFilterPolicy
```
Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" -Name "LocalAccountTokenFilterPolicy" -Value 0 -Force
```
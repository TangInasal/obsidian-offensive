## Custom Powershell scripts for shortcut modules
**NOTE: ** 
Import Modules
```
Import-Module C:\Path\to\file.ps1
```
Check imported modules**
```
Get-Module
```

**Re-import module**
```
Remove-Module <Modulename>
Import-Module <Modulename>
```


---
#### Get-AVInfo
identify Active AV
```powershell
function Get-AVInfo {
    gcim -Namespace root/SecurityCenter2 -ClassName AntivirusProduct
}
```
Run cmdlet
```
Get-AVInfo
```

![[Pasted image 20260217211349.png]]

---
#### Get-SysmonEvent
```powershell
function Get-SysmonEvent {
    Get-WinEvent -LogName "Microsoft-Windows-Sysmon/Operational"
} 
```

Run cmdlet
```
Get-SysmonEvent
```



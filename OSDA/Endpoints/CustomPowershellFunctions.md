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
    param (
        $eventid,
        $start,
        $end
    )
    $filters = @{LogName = "Microsoft-Windows-Sysmon/Operational"}

    if ($eventid -ne $null) {
        $filters.ID = $eventid
    }

    if ($start -ne $null) {
        $filters.StartTime = $start
    }

    if ($end -ne $null) {
        $filters.EndTime = $end
    }

    Get-WinEvent -FilterHashtable $filters
}
```

Run cmdlet
```
Get-SysmonEvent
```


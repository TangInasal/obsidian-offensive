### Querying sysmon with powershell
**NOTE:**  refer to [this resource ](CustomPowershellFunctions####Get-SysmonEvent)for context

---
#### Get-SysmonEvent

**Filter with timeframe**
```powershell
Get-SysmonEvent $null "11/29/2021 15:40:00" "11/29/2021 16:00:00"
```

**Identify Sysmon Event IDs were most active during a specific timeframe**)
```powershell
Get-SysmonEvent $null "11/29/2021 15:40:00" "11/29/2021 16:00:00" | Group-Object -Property ID | Sort-Object Count -Descending
```

**Filter with FileCreate event**
(can spot malware execution)
```powershell
Get-SysmonEvent 11 "11/29/2021 15:45:00" "11/29/2021 15:46:00" | Format-List
```
![[Pasted image 20260217223436.png]]

**Hunt for specific PID**
```powershell
Get-SysmonEvent 1 $null "11/29/2021 15:45:32" | Where-Object { $_.properties[3].value -eq 4512 } | Format-List
```
![[Pasted image 20260217225123.png]]

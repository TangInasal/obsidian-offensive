## Event Files Collection via Powershell

select first 10 entries on Security.evtx
```powershell
Get-WinEvent -LogName Security | Select-Object -First 10
```

Select only logon events via (ID column) Event ID "4624"  and message
```powershell
Get-WinEvent -LogName Security | Where-Object { $_.id -eq "4624" } | Select-Object -Property TimeCreated,Message -first 10
```
```output
TimeCreated          Message
-----------          -------
2/17/2026 5:26:01 PM An account was successfully logged on....
2/17/2026 5:25:50 PM An account was successfully logged on....
2/17/2026 5:25:42 PM An account was successfully logged on....
2/17/2026 5:17:15 PM An account was successfully logged on....
2/17/2026 5:14:34 PM An account was successfully logged on....
2/17/2026 5:07:31 PM An account was successfully logged on....
...
```

Filter Security log by Time and Event ID
```powershell
Get-WinEvent -FilterHashtable @{Logname='Security'; ID=4624; StartTime='2/17/2026 00:00:00'; EndTime='2/17/2026 23:59:59'} | Select-Object TimeCreated, Message -First 10
```


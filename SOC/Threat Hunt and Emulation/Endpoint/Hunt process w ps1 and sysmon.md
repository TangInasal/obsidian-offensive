**NOTE: endpoint must have sysmon installed**

**Scenario**
You are looking for a windows utility called `mshta.exe`

Look at one log for an example
`get-winevent -FileHashtable @{logname='Microsoft-Windows-Sysmon/Operational';ID='1'} -maxevents 1| Select-Object *`
![[Pasted image 20250704133341.png]]

Look for logs containing the string "mshta"
`$event1 | Where-Object {$_.message -match 'mshta'}`

Expand all the fields for more details
`$event1 | Where-Object {$_.message -match 'mshta'} | Select-Object -ExpandProperty message`

Filter the output for clean listing
`$event1 | Where-Object {$_.message -match 'mshta'} | Select-Object -ExpandProperty message | findstr CommandLine`

![[Pasted image 20250704133255.png]]




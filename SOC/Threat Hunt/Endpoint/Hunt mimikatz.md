**NOTE: endpoint must have SYSMON installed**

set variable
`$event1 = get-winevent -logname Microsoft-Windows-Sysmon/Operational | Where-Object {$_.id -like '1'}`

look for logs with `sekurlsa`
`$even1 | Where-Object {$_.message -match 'sekurlsa'}`
![[Pasted image 20250704155304.png]]

expand field for details
`$even1 | Where-Object {$_.message -match 'sekurlsa'} | Select-Object -ExpandProperty message`

![[Pasted image 20250704155354.png]]

Filter for cleaner list
`$even1 | Where-Object {$_.message -match 'sekurlsa'} | Select-Object -ExpandProperty message | findstr CommandLine`

![[Pasted image 20250704155417.png]]


-----
<h3> Hunt for KIrbi Files</h3>
**NOTE: Not a very effective way for threat hunt
due to resource intensive process**

Direct search of the filesystem
`cmd /c where /r c:\Users *.kirbi`
![[Pasted image 20250704155731.png]]
krbtgt has been compromised
can be used for golden ticket attack



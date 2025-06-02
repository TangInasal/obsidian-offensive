Database for storing configuration info

**Location:**
System Registry:
`%SystemRoot%\System32\Config`
User Registry:
`%UserProfile%\NTUSER.dat`

![[Pasted image 20250602212823.png]]


**Specific Locations:**
Recently Opened Programs/Files/URLS
`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDIg32\OpenSaveMRU`
Files opened directly from Windows Explorer
`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs`
Start>Run
`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU`
Typed URLS
`HKCU\Software\Microsoft\Internet Explorer\TypedURLs`
Installed Programs
`HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall`
`HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\App Paths`
Mounted Drives 
`HKLM\SYSTEM\MountedDevices`
Recently Mapped Network Devices
`HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Map Network Drive MRU`
USB Storage
`HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR`
Autorun
`HKLM\SOFTWARE\Microsoft\CurrentVersion\Run`
Services
`HKLM\SYSTEM\CurrentControlSet\Services`
Last user logged in
`SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LoginUI\LastLoggedOnUser`


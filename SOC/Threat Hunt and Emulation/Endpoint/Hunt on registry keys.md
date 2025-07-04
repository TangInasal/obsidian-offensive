Hunt for registry key entries
Local Machine`Get-Item -Path 'HKLM:\Software\Microsoft\Windows\CurrentVersion\Run'` 
Local User: `Get-Item -Path 'HKCU:\Software\Microsoft\Windows\CurrentVersion\Run'`
Local Machine `Get-Item -Path 'HKLM:\Software\Microsoft\Windows\CurrentVersion\RunOnce'`
Local User: `Get-Item -Path 'HKCU:\Software\Microsoft\Windows\CurrentVersion\RunOnce'`


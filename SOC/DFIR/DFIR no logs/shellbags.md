set of windows registry keys 
maintains view, icons, positions, size of folders when using windows explorer
stored in `NTUser.dat` or `USRClass.dat`

You can see change history on applications such as
When a user tries to configure windows firewall

**Location:**
`HKCU\Software\Microsoft\Windows Shell\bags`
`HKCU\Software\Microsoft\Windows\Shell\BagMRU (ntuser.dat)`
`HKCU\Software\Microsoft\Windows\ShellNoRoam\Bags`

Under NTUser.dat
`HKCU\Software\Microsoft\Windows\ShellNoRoam\BagMRU`

Under USERCLASS.dat
`HKCU\Software\Classes\Local Settings\Software\Microsoft\Windows\Shell\BagMRU
`HKCU\Software\Classes\Local Settings\Software\Microsoft\Windows\Shell\Bags`


**Tool:**
ShellBags Explorer

[sharphound](https://github.com/SpecterOps/SharpHound/releases/download/v2.6.7/SharpHound_v2.6.7_windows_x86.zip)
[bloodhound](https://github.com/SpecterOps/BloodHound)

**LOOK FOR MALICIOUS GPO**

importing data from bloodhound
refer here: [[FIND KERBEROASTABLE ACCOUNT]]

open bloodhound
search for service account/computer
click computer icon
go to overview
select `Effective Inbound GPOs`

**LIST ALL GPOs INSIDE THE DOMAIN**

Powershell
Show all GPOs inside domain
`Get-GPO -all`

check specific GPO permission
`Get-GPPermission "GPO-name -all"`
![[Pasted image 20250706181551.png]]
**NOTE: Being able to modify GPO
has an ADMIN PRIVILEGE to any system that it applies**

In the photo
all authenticated users CAN EDIT GPO
user domain dom CAN EDIT-DELETE-MODIFY GPO


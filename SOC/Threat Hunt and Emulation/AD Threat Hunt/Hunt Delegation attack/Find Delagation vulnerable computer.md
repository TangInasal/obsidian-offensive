**CHECK FOR COMPUTERS WITH TRUSTEDFORDELEGATION PRIVELEGE**

Powershell:
`Get-ADComputer -Filter {TrustedForDelagation -eq $True}`

**NOTE: Domain Controllers are vulnerable to this by default**
![[Pasted image 20250706164619.png]]

**CHECK WITH ACTIVE DIRECTORY USERS AND COMPUTERS**

Open Active Directory and Computers
Select Globo_Servers
Select vulnerable computer
select `delegation` tab

**NOTE: DO NOT FIX IT RIGHT AWAY
YOU MIGHT NOT KNOW WHY IS IT CONFIGURED IN THAT MANNER
YOU MIGHT DISRUPT BUSINESS OPERATIONS**
![[Pasted image 20250706164833.png]]


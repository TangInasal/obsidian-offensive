
**CHECK FOR KERBEROASTABLE ACCOUNT**
[sharphound](https://github.com/SpecterOps/SharpHound/releases/download/v2.6.7/SharpHound_v2.6.7_windows_x86.zip)
[bloodhound](https://github.com/SpecterOps/BloodHound)

run sharphound
import sharphound data to bloodhound
go to database info 
go to Analysis tab
select kerberoastable accounts under kerberos interaction
![[Pasted image 20250706162839.png]]

Bonus:
select shortest paths from kerberoastable users
select domain
select user you want to map

[atomic-red-team](https://github.com/redcanaryco/atomic-red-team)
[atomic index](https://github.com/redcanaryco/atomic-red-team/tree/master/atomics)

**USAGE:**
used for populating SEIM/XDR/EDR/ logs
test overall security and detection
just copy commands to the environment

**OR
use invoke-atomic-red-team**
[invoke-atomicredteam](https://github.com/redcanaryco/invoke-atomicredteam)

open cmd/powershell
install it (there's a ps1 file in the repo)

Run 
`Ivoke-AtomicTest <TTP>`

sample TTP: T1218.005
Show TTP brief
`Ivoke-AtomicTest T1218.005 -ShowDetailsBrief`

![[Pasted image 20250705001941.png]]

Run test on all procedure
`Ivoke-AtomicTest T1218.005`
![[Pasted image 20250705002617.png]]

Specify test number (show details)
`Ivoke-AtomicTest T1218.005 -TestNumbers 2 -ShowDetailsBrief
![[Pasted image 20250705002042.png]]

Test TTP number
`Ivoke-AtomicTest T1218.005 -TestNumbers 2

![[Pasted image 20250705002146.png]]


---
**pre-requesites**
Check Pre-requisites
`Ivoke-AtomicTest T1218.005 -CheckPrereqs 

![[Pasted image 20250705002333.png]]


Get pre-requisites
`InvokeAtomicTest -GetPrereqs`


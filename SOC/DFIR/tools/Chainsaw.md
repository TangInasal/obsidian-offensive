Chainsaw is built for one thing: rapidly searching and analysing Windows Event Logs. 
During incident response, you often end up with gigabytes of `.evtx` files and need to find evidence of lateral movement, privilege escalation, persistence, or credential access buried across Security, System, PowerShell, Sysmon, and dozens of other log channels.
Chainsaw makes this fast.

It uses Sigma detection rules as its primary detection logic, which means it benefits from the entire open-source Sigma rule community. 
It also supports custom detection rules in its own YAML-based format and keyword searching.

A typical Chainsaw hunt across gigabytes of event logs completes in seconds. 
It will flag events like:
- Pass-the-hash and pass-the-ticket authentication (Event ID 4624 with logon type 9)
- Suspicious service installations (Event ID 7045)
- PowerShell script block logging showing encoded commands (Event ID 4104)
- Sysmon process creation with suspicious parent-child chains (Event ID 1)
- Scheduled task creation for persistence (Event ID 4698)
- Security log clearing (Event ID 1102)
#### **When to use it:** 
- Any time you have Windows Event Logs to analyse. 
- It is the fastest way to get from a pile of `.evtx` files to a list of suspicious events ranked by severity. 
- Pairs well with log collection tools like KAPE.

---

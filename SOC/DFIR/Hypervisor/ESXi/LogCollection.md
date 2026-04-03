Log collection playbook for ESXi
Useful for responding Ransomware attacking hosts inside ESXi hypervisor

----
### 1. Immediate Containment & Access

- Power off non-essential VMs if safe (preserve memory if possible via suspend).
- Enable SSH only if console is too slow: 
```
esxcli system ssh set --enabled true (via console).```
```
- Note current time (date) and NTP status for timeline skew.
- Do **not** reboot yet unless required for collection.
#### Log Collection via Console

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
### Log Collection via Console
#### Quick Volatile Collection (first 5-10 mins)

Run these in one go (script if possible):

Bash

```
date > /tmp/collection_start.txt
hostname > /tmp/hostname.txt
esxcli system version get > /tmp/esxi_version.txt
esxcli system stats uptime get >> /tmp/uptime.txt
ps -c > /tmp/ps.txt
netstat -anp > /tmp/netstat.txt
esxcli network ip connection list > /tmp/connections.txt
lsof -a > /tmp/lsof.txt
vmkload_mod -l > /tmp/modules.txt
esxcli software vib list > /tmp/vibs.txt
```

Copy /tmp/ output immediately to external USB/NFS share or datastore.

#### Core Log Collection

Key paths (logs roll fast — copy **now**):

- /var/log/ (main)
- /var/run/log/ (runtime)
- /scratch/log/ (if persistent scratch configured)
- /tmp/ (ephemeral logs)

Critical files to tar/cp:
cd /var/log
```tar -czf /vmfs/volumes/<datastore>/evidence/logs_var.tar.gz \
  hostd.log* vmkernel.log* vmkwarning.log* shell.log* auth.log* syslog.log* \
  vpxa.log* hostd-probe.log* rhttpproxy.log* esxupdate.log* \
  audit.*.log  # if audit logging enabled
```
Also grab:
- VM logs: For each VM dir on datastore → vmware.log* and .vmss/.vmem if suspended.
- Config: /etc/vmware/ (esp. hostd/config.xml, esx.conf)

Use vm-support for bundled collection (best single command, includes most logs + diagnostics):
```vm-support
vm-support -d /vmfs/volumes/<datastore>/evidence/ -s  # or without -s for full
```
It creates a .tgz with logs, configs, dumps. Run it — takes time, monitor disk space.

#### Full Forensic Preservation (if time/disk allows)

- Image critical partitions (risky on live system):
```
dd if=/dev/disks/<device> of=/vmfs/volumes/<external_datastore>/esxi_image.dd bs=4M conv=sync,noerror status=progress
```
- Target bootbank, scratch, etc. Use external USB/SAS drive attached directly.
- Or remove physical disks post-shutdown for offline imaging (FTK Imager, dd on Linux with vmfs-fuse).

#### Transfer & Chain of Custody

- Copy everything to external media via:
    - SCP to air-gapped collection laptop on same switch (direct cable if possible).
    - USB drive formatted FAT32/exFAT (mounted via esxcli storage filesystem).
- Hash everything on collection (md5sum or sha256sum).
- Document: timestamps, commands run, hashes, collector identity.
---
#### Key Artifacts to Hunt Post-Collection (offline analysis)

- **hostd.log**: API calls, VM ops, config changes, attacker actions via vSphere/SSH.
- **shell.log**: Direct shell commands (root access).
- **vmkernel.log / vmkwarning.log**: Kernel events, suspicious modules, disk/IO anomalies.
- **auth.log / syslog**: Logins, SSH, sudo.
- **vibs list + /var/log/esxupdate.log**: Tampered/added VIBs (common persistence).
- **audit logs** (if enabled): High-fidelity actions.
- Unusual processes, open VMCI sockets, modified /etc/inetd.conf, rogue cron.

#### Pro Tips from Real ESXi IR

- If attacker touched it, logs may be wiped/rotated — compare with any prior backups or vCenter side.
- Persistent logging must have been on; otherwise /var/run/log is gone on reboot.
- For full host image: shutdown cleanly if possible, then image disks.
- Tools like QELP or DFIR4vSphere module help parsing later — feed the tarballs there.

Do this fast. ESXi logs are volatile by default. Once collected, shut down, image, and analyze offline. 


---
#### [Priority Logs to Collect](./PriorityLogs)

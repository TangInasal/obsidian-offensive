Log Collection Playbook for ESXi 6.5
#### 1. Quick Volatile Snapshot (via console/SSH as root)

```
date > /tmp/start.txt
esxcli system version get > /tmp/esxi_version.txt
uptime > /tmp/uptime.txt
ps -c > /tmp/ps.txt
esxcli network ip connection list > /tmp/conns.txt
netstat -anp > /tmp/netstat.txt
lsof > /tmp/lsof.txt
vmkload_mod -l > /tmp/modules.txt
esxcli software vib list > /tmp/vibs.txt          # ← flag for tampered VIBs
esxcli system settings advanced list | grep -E 'Scratch|Syslog|Acceptance' > /tmp/config.txt
```

Copy /tmp/ contents to external USB/datastore.

#### 2. Core Log Collection (tar everything before rotation/loss)


```
# Create evidence dir on a datastore with space (e.g. datastore1)
mkdir -p /vmfs/volumes/datastore1/evidence/logs_$(date +%Y%m%d_%H%M)

cd /var/log
tar -czf /vmfs/volumes/datastore1/evidence/logs_var.tar.gz \
  *.log* auth.log* shell.log* hostd.log* vmkernel.log* vmkwarning.log* \
  syslog.log* rhttpproxy.log* esxupdate.log* vpxa.log* hostd-probe.log*

# Also grab runtime logs if present
cp -r /var/run/log/* /vmfs/volumes/datastore1/evidence/logs_run/ 2>/dev/null || true

# Persistent scratch if configured
if [ -d "/scratch/log" ]; then
  tar -czf /vmfs/volumes/datastore1/evidence/logs_scratch.tar.gz -C /scratch/log .
fi
```

**Key 6.5 logs to prioritize in analysis:**

- shell.log — every command typed (SSH/console)
- auth.log — logins (SSH, DCUI, console)
- hostd.log — management actions, VM ops, API calls, user activity
- vmkernel.log / vmkwarning.log — kernel events, suspicious modules, IO anomalies
- syslog.log — general system
- VIB list + esxupdate.log — malicious VIB installation (common in 6.5 compromises)

#### 3. Best single command: vm-support bundle (recommended for 6.5)

```
vm-support -d /vmfs/volumes/datastore1/evidence/ 
# Or with VM focus if needed: vm-support -v <vmname>
```

This bundles most logs, configs, dumps into a .tgz. Runs for minutes — monitor space. Copy the resulting bundle off-host immediately.

#### 4. Additional Artifacts (6.5 specific)

- VM logs: For each VM folder on datastores → copy vmware.log*
- Configs: cp -r /etc/vmware/ /vmfs/volumes/datastore1/evidence/configs/
- Check VIB acceptance (tampering indicator):
```
esxcli software acceptance get
```
- If time: esxcli system syslog config get and /etc/vmware/hostd/config.xml

#### 5. Transfer (air-gapped)

- Mount USB: esxcli storage filesystem list then copy to mounted volume.
- Or SCP to directly connected collection laptop (no internet).
- Hash on-host: md5sum or sha256sum every tar/bundle.
- Document: exact commands, timestamps (note any clock skew), hashes, your actions.

#### 6. Post-Collection (offline)

- Shut down host cleanly if possible → image disks for full FS.
- Analyze with: QELP (Quick ESXi Log Parser), DFIR4vSphere, or grep/timeline on the tars.
- Hunt: root logins in auth.log → commands in shell.log → VIB installs → hostd API abuse → vmkernel anomalies.


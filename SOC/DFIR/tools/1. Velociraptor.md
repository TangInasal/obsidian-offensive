---

---
---
DFIR platform that goes beyond a single-purpose tool. 
It provides endpoint visibility, artifact collection, and threat hunting across an entire fleet through a server-agent architecture. 
Think of it as an open-source alternative to commercial EDR forensic capabilities.

Velociraptor can be deployed as a standalone binary for single-system triage or as a full server deployment for fleet-wide hunting. 
In incident response, the common pattern is to deploy the server rapidly, push agents to affected systems, and run targeted artifact collections, all within minutes.

### **When to use it:** 
- When you need to investigate and collect artefacts from multiple systems simultaneously
- Or when you need ongoing monitoring capability during an active incident.
- It fills the gap between manual forensic tools and full commercial EDR platforms.

---
#### Collect prefetch files for evidence of execution
```
SELECT * FROM Artifact.Windows.Forensics.Prefetch()
```
#### Hunt for persistence mechanisms
```
SELECT * FROM Artifact.Windows.Sys.StartupItems()
```
#### Collect browser history
```
SELECT * FROM Artifact.Windows.Applications.Chrome.History()
```
#### Search for YARA matches across the filesystem
```
SELECT * FROM Artifact.Generic.Detection.Yara.Glob(
  PathGlob="C:/Users/**",
  YaraRule="rule test { strings: $a = \"mimikatz\" condition: $a }"
)
```
#### Collect memory from a Linux endpoint using AVML
```
SELECT * FROM Artifact.Windows.Memory.Acquisition()
```
#### Collect memory from a Linux endpoint using AVML
```
SELECT * FROM Artifact.Linux.Memory.Acquisition()
```

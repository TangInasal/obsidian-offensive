it is a collection tool. 
Rapidly collects forensic artefacts from a live Windows system or mounted image and packages them for analysis. 
KAPE is often the first tool deployed to a compromised system because it gathers everything an analyst needs without requiring a full disk image.

KAPE collects the following:
- event logs
- registry hives
- prefetch files
- browser data
- jump lists
- SRUDB
- $MFT
- amcach
- shimcache
- scheduled tasks
- and dozens of other forensic artefact categories. 
A full triage collection typically takes 5-15 minutes and produces a package of a few gigabytes rather than a full disk image of hundreds of gigabytes.

### **When to use it:** 
First step in any Windows incident response. 
- Collect artefacts with KAPE, 
- Analyse them with Chainsaw (event logs), 
- Hayabusa (timelines), 
- Zimmerman’s parsers (registry, prefetch, shellbags, etc.).
---
#### Collect common triage artefacts
```
kape.exe --tsource C: --tdest E:\collection\ --tflush --target !SANS_Triage
```
#### Collect and process with multiple parsers
```
kape.exe --tsource C: --tdest E:\collection\ --target !SANS_Triage --mdest E:\processed\ --module !EZParser
```


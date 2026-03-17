
These tools are most effective when used together. Practical IR toolkit workflow:

**1. Collection:** 
- Deploy [KAPE](./tools/KAPE) on Windows systems to gather forensic artefacts. 
- On Linux, use targeted collection scripts or Velociraptor artifacts. 
- Acquire memory using AVML where needed.

**2. Scanning:** 
- Run [THOR-lite](./tools/thor-lite) (or Loki if licensing is a constraint) against live systems or collected artefacts to identify known malware, attacker tools, and suspicious anomalies.

**3. Log Analysis:** 
- Feed collected event logs through both Chainsaw and Hayabusa. 
- Chainsaw for rapid hunting and specific searches, 
- Hayabusa for comprehensive timeline generation.

**4. Fleet-Wide Hunting:** 
- If the incident spans multiple systems, 
- deploy Velociraptor to hunt for indicators across the environment simultaneously rather than investigating one system at a time.

**5. Deep Dive:** 
- Use findings from the above tools to guide targeted forensic analysis, including memory forensics, registry analysis, and malware reverse engineering as needed.

The value of these tools is that they bring the collective detection knowledge of the DFIR community (through Sigma rules, YARA rules, and IOC databases) to bear on your specific incident, without requiring every analyst to carry that knowledge in their head. Keep them updated, keep them accessible, and practice using them before you need them.
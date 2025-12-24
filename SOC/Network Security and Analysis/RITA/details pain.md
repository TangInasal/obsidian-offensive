<h3>Threat Modifiers</h3>
These are criteria to determine the severity and likelihood of a potential threat. The following modifiers are available:

- **MIME type/URI mismatch:** Flags connections where the MIME type reported in the HTTP header doesn't match the URI. This can indicate an attacker is trying to trick the browser or a security tool.
- **Rare signature:** Points to unusual patterns that attackers might overlook, such as a unique user agent string that is not seen in any other connections on the network.
- **Prevalence:** Analyzes the number of internal hosts communicating with a specific external host. A low percentage of internal hosts communicating with an external one can be suspicious.
- **First Seen:** Checks the date an external host was first observed on the network. A new host on the network is more likely to be a potential threat.
- **Missing host header:** Identifies HTTP connections that are missing the host header, which is often an oversight by attackers or a sign of a misconfigured system.
- **Large amount of outgoing data**: Flags connections that send a very large amount of data out from the network.
- **No direct connections:** Flags connections that don't have any direct connections, which can be a sign of a more complex or hidden command and control communication.

---

<h3>Connection Info</h3>
Here, we can find the connections' metadata and basic connection info like:

- **Connection count:** Shows the number of connections initiated between the source and destination. A very high number can be an indicator of C2 beacon activity.
- **Total bytes sent:** Displays the total amount of bytes sent from source to destination. If this is a very high number, it could be an indication of data exfiltration.
- **Port number - Protocol - Service:** If the port number is non-standard, it warrants further investigation. The lack of SSL in the Service info could also be an indicator that warrants further investigation.
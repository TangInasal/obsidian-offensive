**pcap to zeek**
convert pcap files to zeek for analysis
`zeek readpcap <traffic.pcap> <output/logs/directory>`


**zeek to RITA**
import zeek logs to RITA
`rita import --logs <logs/directory> --database <database_name>`

**view results**
view results in RITA
`rita view <database_name>`
![[Pasted image 20251224150841.png]]

**search bar**
to search, type `/` 
for help, type `/?`


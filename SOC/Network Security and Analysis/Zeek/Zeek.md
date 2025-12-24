**2 modes**
as a service, and packet investigator

**as service**
ZeekControl (needs sudo priv)
using zeek for network monitoring

`zeekctl status` - check status
`zeekctl start` - start zeek service
`zeekctl stop` - stop zeek service


**packet investigator**
zeek needs to process pcaps first before reading
zeek automatically creates log files in current directory

`zeek -C -r sample.pcap`
`-C` - ignore checksum errors
`-r` - pcap to read
`zeekctl` - ZeekControl module


**pcap to zeek**
convert pcap files to zeek for analysis
`zeek readpcap <traffic.pcap> <output/directory>`



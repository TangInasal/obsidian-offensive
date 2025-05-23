can run like tcpdump
**flags**
`-v` verbose
`-d` display packet data (payload)
`-e` display the link layer (TCP/IP/UDP/ICMP) headers.
`-X` display the full packet details in HEX
`-i` define a specific network interface to listen/sniff. Once you have multiple interfaces, you can choose a specific interface to sniff.

sniffing in verbose mode
`sudo snort -v -i eth0`

sniffing in data mode
`sudo snort -d -i eth0`

sniffing with data mode and header grabber
`sudo snort -d -e`

sniff in packet dump mode
`sudo snort -X`


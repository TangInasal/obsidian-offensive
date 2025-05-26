
`-r / --pcap-single=` - read a single PCAP file
`--pcap-list=` - read pcaps provided in command (space separated)
`--pcap-show` - Show pcap name on console during processing.

**investigating single pcap**
`sudo snort -c /etc/snort/snort.conf -q -r icmp-test.pcap -A console -n 10`
`-r` reading single pcap

**investigating multiple pcaps**
`sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console -n 10`
`--pcap-list="pcap1 pcap2"` reading multiple pcaps, separated with space
![[Pasted image 20250525121713.png]]

**investigating multiplepcapfiles wthpcapinfo**
`sudo snort -c /etc/snort/snort.conf -q --pcap-list="icmp-test.pcap http2.pcap" -A console --pcap-show`
`--pcap-list="pcap1 pcap2"` reading multiple pcaps, separated with space
`--pcap show`  shows which pcap file generated the alert
![[Pasted image 20250525121652.png]]


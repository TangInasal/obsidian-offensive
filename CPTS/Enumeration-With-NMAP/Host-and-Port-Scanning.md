
#### 6 different states for a scanned port we can obtain:

 - `open` - This indicates that the connection to the scanned port has been established. These connections can be **TCP connections**, **UDP datagrams** as well as **SCTP associations**.
 - `closed` -  When the port is shown as closed, the TCP protocol indicates that the packet we received back contains an `RST` flag. This scanning method can also be used to determine if our target is alive or not.
 - `filtered` - Either no response is returned from the target for the port or we get an error code from the target.
 - `unfiltered` - the port is accessible, but it cannot be determined whether it is open or closed.
 - `open|filtered` - When we dont get a response for a specific port. This indicates that a firewall or packet filter may protect the port.
 - `closed|filtered` - indicates that it was impossible to determine if the scanned port is closed or filtered by a firewall.
- 
---
## Discovering Open TCP Ports

#### Scanning Top 10 TCP Ports
```shell-session
udo nmap 10.129.2.28 --top-ports=10 
```
```output
PORT     STATE    SERVICE
21/tcp   closed   ftp
22/tcp   open     ssh
23/tcp   closed   telnet
25/tcp   open     smtp
80/tcp   open     http
110/tcp  open     pop3
139/tcp  filtered netbios-ssn
443/tcp  closed   https
445/tcp  filtered microsoft-ds
3389/tcp closed   ms-wbt-server
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)
```
#### UDP Port Scan
```shell-session
sudo nmap 10.129.2.28 -F -sU
```
```output
PORT     STATE         SERVICE
68/udp   open|filtered dhcpc
137/udp  open          netbios-ns
138/udp  open|filtered netbios-dgm
631/udp  open|filtered ipp
5353/udp open          zeroconf
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)
```
- `-F` - Scans top 100 ports.
- `-sU` - Performs a UDP scan.

#### Version scan
```shell-session
sudo nmap 10.129.2.28 -F -sV
```

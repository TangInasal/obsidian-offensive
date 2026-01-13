**NOTE:** It is always recommended to store every single scan. This can later be used for comparison, documentation, and reporting.

---
## Host Discovery
#### Scan Network Range
This scanning method works only if the firewalls of the hosts allow it.
```shell-session
 sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
```
```output
10.129.2.4
10.129.2.10
10.129.2.11
10.129.2.18
10.129.2.19
10.129.2.20
10.129.2.28
```
- `10.129.2.0/24` - Target network range.
- `-sn` - Disables port scanning.
- `-oA tnet` - Stores the results in all formats starting with the name 'tnet'.

#### Scan IP List
```sample-list
hosts.lst

10.129.2.4
10.129.2.10
10.129.2.11
10.129.2.18
10.129.2.19
10.129.2.20
10.129.2.28
```

```shell-session
sudo nmap -sn -oA tnet -iL hosts.lst | grep for | cut -d" " -f5
```
```output
10.129.2.18
10.129.2.19
10.129.2.20
```

- `-sn` - Disables port scanning.
- `-oA tnet` - Stores the results in all formats starting with the name 'tnet'.
- `-iL` - Performs defined scans against targets in provided 'hosts.lst' list.

we see that only 3 of 7 hosts are active. Remember, this may mean that the other hosts ignore the default **ICMP echo requests** because of their firewall configurations. Since `Nmap` does not receive a response, it marks those hosts as inactive.

#### Scan Multiple IPs
```shell-session
sudo nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20| grep for | cut -d" " -f5
```
```output
10.129.2.18
10.129.2.19
10.129.2.20
```
OR
```shell-session
sudo nmap -sn -oA tnet 10.129.2.18-20| grep for | cut -d" " -f5
```
```output
10.129.2.18
10.129.2.19
10.129.2.20
```

#### Scan Single IP

Check host if alive or not
```shell-session
sudo nmap 10.129.2.18 -sn -oA host 
```
```output
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-14 23:59 CEST
Nmap scan report for 10.129.2.18
Host is up (0.087s latency).
MAC Address: DE:AD:00:00:BE:EF
Nmap done: 1 IP address (1 host up) scanned in 0.11 seconds
```
OR with packet trace
```shell-session
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace 
```
```output
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-15 00:08 CEST
SENT (0.0074s) ARP who-has 10.129.2.18 tell 10.10.14.2
RCVD (0.0309s) ARP reply 10.129.2.18 is-at DE:AD:00:00:BE:EF
Nmap scan report for 10.129.2.18
Host is up (0.023s latency).
MAC Address: DE:AD:00:00:BE:EF
Nmap done: 1 IP address (1 host up) scanned in 0.05 seconds
```
OR with packet trace and disable arp ping
```shell-session
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace --disable-arp-ping 
```
```output
Starting Nmap 7.80 ( https://nmap.org ) at 2020-06-15 00:12 CEST
SENT (0.0107s) ICMP [10.10.14.2 > 10.129.2.18 Echo request (type=8/code=0) id=13607 seq=0] IP [ttl=255 id=23541 iplen=28 ]
RCVD (0.0152s) ICMP [10.129.2.18 > 10.10.14.2 Echo reply (type=0/code=0) id=13607 seq=0] IP [ttl=128 id=40622 iplen=28 ]
Nmap scan report for 10.129.2.18
Host is up (0.086s latency).
MAC Address: DE:AD:00:00:BE:EF
Nmap done: 1 IP address (1 host up) scanned in 0.11 seconds
```


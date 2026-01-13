#### Scan using ACK flag
You can also use `ACK` scan (`-sA`)
They cannot determine if the packet was new or established before
```
sudo nmap 10.129.2.28 -sA 
```
#### Scan by Using Decoys
```shell-session
sudo nmap 10.129.2.28 -p 80 -sS -Pn -n --disable-arp-ping -D RND:5
```
- `-D RND:5` - Generates five random IP addresses that indicates the source IP the connection comes from.

#### Testing Firewall Rule
```shell-session
sudo nmap 10.129.2.28 -n -Pn -p445 -O
```

#### Scan by Using Different Source IP
```shell-session
sudo nmap 10.129.2.28 -n -Pn -p 445 -O -S 10.129.2.200 -e tun0
```
- `-O` - Performs operation system detection scan.
- `-S` - Scans the target by using different source IP address.
- `10.129.2.200` - Specifies the source IP address.
- `-e tun0` - Sends all requests through the specified interface.

----
## DNS Proxying

`Nmap` still gives us a way to specify DNS servers ourselves (`--dns-server <ns>,<ns>`)
This method could be used if we are in a demilitarized zone (`DMZ`).
we can use `TCP port 53` as a source port (`--source-port`) for our scans
#### SYN-Scan From DNS Port
```shell-session
sudo nmap 10.129.2.28 -p50000 -sS -Pn -n --disable-arp-ping --packet-trace --source-port 53
```
```output
SENT (0.0482s) TCP 10.10.14.2:53 > 10.129.2.28:50000 S ttl=58 id=27470 iplen=44  seq=4003923435 win=1024 <mss 1460>
RCVD (0.0608s) TCP 10.129.2.28:50000 > 10.10.14.2:53 SA ttl=64 id=0 iplen=44  seq=540635485 win=64240 <mss 1460>
Nmap scan report for 10.129.2.28
Host is up (0.013s latency).

PORT      STATE SERVICE
50000/tcp open  ibm-db2
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)
```


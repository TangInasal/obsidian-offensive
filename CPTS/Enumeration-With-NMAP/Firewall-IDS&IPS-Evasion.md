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
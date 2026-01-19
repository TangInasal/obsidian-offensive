`Oracle Transparent Network Substrate` (`TNS`) server is a communication protocol that facilitates communication between Oracle databases and applications over networks.

## Footprinting the Service

#### Nmap
```shell-session
 sudo nmap -p1521 -sV 10.129.204.235 --open
```
```output
PORT     STATE SERVICE    VERSION
1521/tcp open  oracle-tns Oracle TNS listener 11.2.0.2.0 (unauthorized)
```

#### Nmap - SID Bruteforcing
There are various ways to enumerate, or guess SIDs. 
Therefore we can use tools like `nmap`, `hydra`, `odat`, and others.
```shell-session
sudo nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute
```
```output
PORT     STATE SERVICE    VERSION
1521/tcp open  oracle-tns Oracle TNS listener 11.2.0.2.0 (unauthorized)
| oracle-sid-brute: 
|_  XE
```
#### ODAT
We can use the `odat.py` tool to perform a variety of scans to enumerate and gather information about the Oracle database services and its components. 
Those scans can retrieve database names, versions, running processes, user accounts, vulnerabilities, misconfigurations, etc. 
Let us use the `all` option and try all modules of the `odat.py` tool.


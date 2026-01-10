**NOTE** : refer to [connecting to services](../Services/Connecting-to-Services) for login 

```
nmap -sC -sV -Pn -p- <rhost>
```
OR
```
nmap -sC -sV -Pn -p- <rhost> --min-rate=500
```


----
# Scanning Network Services
[Attacking Network Services](../Services/Attacking-Network-Services)
### Banner Grabbing

**netcat**
```
nc -nv <rhost> <rport>
```


Nmap will attempt to grab the banners
**NMAP**
```
nmap -sV --script=banner <rhost>
```

```
nmap -sV --script=banner -p21 10.10.10.0/24
```


#### SMB
Enumerating SMB with NMAP
Can also reveal OS version
```
nmap --script smb-os-discovery.nse -p445 <rhost>
```

Enumerating SMB service version
```shell-session
nmap -A -p445 <rhost>
```

Enumerating SMB Share
```shell-session
smbclient -N -L \\\\<rhost>
```
OR
```shell-session
d1ox@htb[/htb]$ smbclient -N -L \\\\10.129.42.253

	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	users           Disk      
	IPC$            IPC       IPC Service (gs-svcscan server (Samba, Ubuntu))
SMB1 disabled -- no workgroup available
```

**NOTE :** REFER TO [Attacking Network Services](../Services/Attacking-Network-Services#SMB)

#### SNMP 
**snmpwalk** (if we know the strings)
```shell-session
d1ox@htb[/htb]$ snmpwalk -v 2c -c public 10.129.42.253 1.3.6.1.2.1.1.5.0

iso.3.6.1.2.1.1.5.0 = STRING: "gs-svcscan"
```
OR
```shell-session
d1ox@htb[/htb]$ snmpwalk -v 2c -c private  10.129.42.253 

Timeout: No Response from 10.129.42.253
```


**NOTE** : refer to [connecting to services](../Services/Connecting-to-Services) for login 

```
nmap -sC -sV -Pn -p- <rhost>
```
OR
```
nmap -sC -sV -Pn -p- <rhost> --min-rate=500
```


----
# Attacking Network Services
### Banner Grabbing

**NETCAT**
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
smbclient -N -L \\\\10.129.42.253
```


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
```
nmap --script smb-os-discovery.nse -p445 <rhost>
```


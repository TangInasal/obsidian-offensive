Perform a full port scan first before proceding with service version detection
```shell-session
sudo nmap 10.129.2.28 -p- -v
```
## Service Version Detection
```shell-session
sudo nmap 10.129.2.28 -p- -sV
```
OR with specified ports
```shell-session
sudo nmap 10.129.2.28 -p<list of open ports> -sV
```
OR with --stats-every=5s --stats-every=1m 
```shell-session
sudo nmap 10.129.2.28 -p- -sV --stats-every=5s
```

## Banner Grabbing
```shell-session
sudo nmap 10.129.2.28 -p- -sV
```

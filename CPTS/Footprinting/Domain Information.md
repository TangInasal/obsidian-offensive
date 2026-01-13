## Online Presence
#### Finding subdomains thru SSL certificates
output as json format
```shell-session
curl -s https://crt.sh/\?q\=example.com\&output\=json | jq .
```
OR filtered by the unique subdomains.
```shell-session
curl -s https://crt.sh/\?q\=example.com\&output\=json | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u
```
OR save to subdomainlist
```shell-session
curl -s https://crt.sh/\?q\=example.com\&output\=json | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u >> subdomainlist
```

#### Company Hosted Servers
**Identify the hosts directly accessible from the Internet and not hosted by third-party providers**
```shell-session
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done
```
#### Running IP list thru Shodan
```shell-session
 for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f4 >> ip-addresses.txt;done
```
```shell-session
for i in $(cat ip-addresses.txt);do shodan host $i;done
```

#### DNS Records
```shell-session
dig any example.com
```

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


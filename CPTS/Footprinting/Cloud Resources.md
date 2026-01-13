#### Company Hosted Servers
```shell-session
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done
```

#### Google Search for AWS
``` dorks
intext:company inurl:amazonaws.com
```
#### Google Search for Azure
```dorks
intext:company inurl:blob.core.windows.net
```

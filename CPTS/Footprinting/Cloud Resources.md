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

Third-party providers such as [domain.glass](https://domain.glass/) can also tell us a lot about the company's infrastructure. We can also see that Cloudflare's security assessment status can classify as "Safe". This means we have already found a security measure that can be noted for the second layer (gateway).

Another very useful provider is [GrayHatWarfare](https://buckets.grayhatwarfare.com/). 
Discover AWS, Azure, and GCP cloud storage, and even sort and filter by file format. 
Therefore, once we have found them through Google, we can also search for them on GrayHatWarfare and passively discover what files are stored on the given cloud storage.



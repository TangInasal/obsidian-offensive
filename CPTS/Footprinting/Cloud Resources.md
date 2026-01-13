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

#### domain.glass
Third-party providers such as [domain.glass](https://domain.glass/) can also tell us a lot about the company's infrastructure. We can also see that Cloudflare's security assessment status can classify as "Safe". This means we have already found a security measure that can be noted for the second layer (gateway).

#### GrayHatWarfare
Another very useful provider is [GrayHatWarfare](https://buckets.grayhatwarfare.com/). 
Discover AWS, Azure, and GCP cloud storage, and even sort and filter by file format. 
Therefore, once we have found them through Google, we can also search for them on GrayHatWarfare and passively discover what files are stored on the given cloud storage.

**NOTE:** Many companies also use **abbreviations of the company name**, which are then used accordingly within the IT infrastructure. Such terms are also part of an excellent approach to discovering new cloud storage from the company. We can also search for files simultaneously to see the files that can be accessed at the same time.

#### Private and Public SSH Keys Leaked
Sometimes when employees are overworked or under high pressure, mistakes can be fatal for the entire company. These errors can even lead to SSH private keys being leaked, which anyone can download and log onto one or even more machines in the company without using a password.

![[Pasted image 20260113212418.png]]


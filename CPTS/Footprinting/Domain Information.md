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
- `A` records: We recognize the IP addresses that point to a specific (sub)domain through the A record. Here we only see one that we already know.
- `MX` records: The mail server records show us which mail server is responsible for managing the emails for the company. Since this is handled by google in our case, we should note this and skip it for now.
- `NS` records: These kinds of records show which name servers are used to resolve the FQDN to IP addresses. Most hosting providers use their own name servers, making it easier to identify the hosting provider.
- `TXT` records: this type of record often contains verification keys for different third-party providers and other security aspects of DNS, such as [SPF](https://datatracker.ietf.org/doc/html/rfc7208), [DMARC](https://datatracker.ietf.org/doc/html/rfc7489), and [DKIM](https://datatracker.ietf.org/doc/html/rfc6376), which are responsible for verifying and confirming the origin of the emails sent. Here we can already see some valuable information if we look closer at the results.

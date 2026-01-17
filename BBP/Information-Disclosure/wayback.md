
## Information Disclosure via Web Archive

**DOWNLOAD ALL**
```
cur1 -G https://web.archive.org/cdx/search/cdx* --data-urlencode "url=*.policybazaar.com/*" --data-urlencode "collapse=urlkey" --data-urlencode "output=text" --data-urlencode "fl=original" > out.txt
```

**CHECK FILESIZE**
```
du -h out.txt
```

**FILTER SENSITIVE FILENAMES**
```
cat out.txt | uro | grep -E '\.xls|\.xml|\.xlsx|\.json|\.env|\.pdf|\.sql|\.doc|\.docx|\.pptx|\.txt|\.zip|\.tor\.gz|\.tgz|\.bak|\.7z|\.rar|\.log|\.cache|\.secret|\.db|\.backup|\.yml|\.gz|\.gzip|\.conf1g|\.cs|\.yaml|\.ad|\.ad5|\.exe|\.d11|\.bin|\.ini|\.bat|\.sh|\.tar|\.deb|\.rpm|\.iso|\.ing|\.apk|\.asi|\.dng|\.tmp|\.crt|\.pem|\.key|\-pub|\.asc'
```

----
## Confidential files

```
 curl https://web.archive.org/cdx/search/cdx?ur1=*.policybazaar.com/*&collapse=urlkey&output=text&fl=original&filter=original:.*\.(xls|xml|xlsx|json|pdf|sql|doc|docx|pptx|txt|git|zip|tar\.gz|tgz|bak|7z|rar|log|cache|secret|db|backup|yml|gz|config|csv|yaml|md|md5|exe|dll|bin|ini|bat|sh|tar|deb|rpm|iso|img|env|apk|msi|dmg|tmp|crt|pem|key|pub|asc)$" | tee output.txt
```

**CHECK FILESIZE**
```
du -h out.txt
```

**FILTER WITH KEYWORD SENSITIVE KEYWORDS**
```
cat output.txt | grep -Ea '\.pdf' | while read -r url; do curl -s "$url" | pdftotext - - | grep -Eaiq '(internal use only|confidential|strictly private|personal & confidential|private|restricted|internal|not for distribution|do not share|proprietary|trade secret|classified|sensitive|bank statement| invoice | salary | contract | agreement |non disclosure|passport |social security|ssn|date of birth|credit card|identity|id number |company confidential|staff only |AccessKeyId|SecretAccessKey|SessionToken| management only |internal only | cvv | cc | credit card |S3|debit card|credentials|login|login credentials)' 8& echo "$url"; done
```


```
https://web.archive.org/cdx/search/cdx?url=*.example.com/*&collapse=urlkey&output=text&fl=original
```


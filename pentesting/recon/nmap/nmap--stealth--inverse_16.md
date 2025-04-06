   

# inverse

  

**INVERSE TCP SCAN** (FIN, NULL, XMAS)

NOTE: PREFFERED THAN SYN scan

EFFECTIVE to use on stateless firewalls and RFC 793 compliant firewalls

CANNOT be used for WINDOWS machines

PREFERRED to be execudet via PORT BY PORT

FIN Scan

nmap -sF 192.168.x.x

NULL Scan (no flags)

nmap -sN 192.168.x.x

XMAS Scan (all 3 flags)

nmap -sX 192.168.x.x

FIN Scan with reason:

nmap -sF 192.168.x.x --reason

FIN Scan with reason and scanning one port:

nmap -sF 192.168.x.x -p8080 --reason

GOLDEN RULE

![images/16-1.png](16-1.png)
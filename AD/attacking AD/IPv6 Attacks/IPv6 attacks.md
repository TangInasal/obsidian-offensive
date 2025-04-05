**IPv6 Attacks**

requirements:
Active Directory Certificate Servies - enabled (in AD)

TOOLS:
mitm6
ntlmrelayx

form of mitm attack/DNS spoofing
the attacker acts as the DNS for the host's ipv6
can authenticate attacker to the domain controller (thru LDAP or SMB)

step 1: the attacker spoofs ipv6 dns thru mitm6
step 2:the host sends ipv6 traffics to the attacker's spoofed dns
step 3: wait for the user to login to the host
step 4: the attacker recieves the signal (thru ntlm) from the host that it logged in.
step 5: the attacker LDAP relay to the Domain Controller with the NTLM it recieved
step 6: it automatically creates an account for us
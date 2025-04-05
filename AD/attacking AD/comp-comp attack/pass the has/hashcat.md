**NTLM hash cracking with hashcat**

NOTE: save hashes on a txt file
NTLM module - 1000

syntax:
```
hashcat -m 1000 <hashes.txt> <path/to/wordlist.txt> -O
```
![[Pasted image 20250402225916.png]]

NOTE: if password is BLANK, account is DISABLED
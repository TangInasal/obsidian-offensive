### Password hunt with impacket-secretsdump
**NOTE:** Must have KAPE output

## Pre requisites
Must have KAPE parsed hive outputs

Directory of artefacts:
```
/C/Windows/System32/config
```
```
DEFAULT       
DEFAULT.LOG2  
SAM.LOG1       
SECURITY     //u need this 
SECURITY.LOG2  
SOFTWARE.LOG1  
SYSTEM       //u need this
SYSTEM.LOG2
DEFAULT.LOG1  
SAM          //u need this
SAM.LOG2  
SECURITY.LOG1  
SOFTWARE       
SOFTWARE.LOG2  
SYSTEM.LOG1
```

### Impacket-secretsdump
```
impacket-secretsdump -sam SAM -security SECURITY -system SYSTEM LOCAL
```
```output
[*] Target system bootKey: 0x3a2999e73d3448fb21e14bbd9a9480d1
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:cf3a5525ee9414229e66279623ed5c58:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:02679f6b636628c0822c7f9836b84282:::
Werni:1002:aad3b435b51404eeaad3b435b51404ee:0fa16c6a581bf468c6a83510926b8358:::
svc_netupd:1003:aad3b435b51404eeaad3b435b51404ee:532303a6fa70b02c905f950b60d7da51:::
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] DPAPI_SYSTEM
dpapi_machinekey:0xb5eb284702c6192c55d1a64faaac43c2a28ae137
dpapi_userkey:0xb371dc89b1cdcaf5b6083d5e087a2c2af1d65b19
[*] NL$KM
 0000   EF 3D B7 8F 87 D7 55 B7  EF 83 72 02 BA 85 73 44   .=....U...r...sD
 0010   4A 1C 81 E5 03 DA 37 C2  D9 54 60 89 36 22 D1 75   J.....7..T`.6".u
 0020   C7 81 1E A1 F6 0C D9 EC  65 36 8E 58 BC A5 7C 1F   ........e6.X..|.
 0030   FE 1D 9C 45 86 F0 82 23  FD 47 60 FB B2 21 FC B8   ...E...#.G`..!..
NL$KM:ef3db78f87d755b7ef837202ba8573444a1c81e503da37c2d95460893622d175c7811ea1f60cd9ec65368e58bca57c1ffe1d9c4586f08223fd4760fbb221fcb8
[*] Cleaning up...
```

save user hash as `username_hash.txt`
**NOTE:**  save the 2nd half of the hash
```
echo "532303a6fa70b02c905f950b60d7da51" > svc_netupd_hash.txt 
```

### hashcat
crack user NTLM hash with hashcat
```
hashcat -m 1000 svc_netupd_hash.txt /usr/share/wordlists/rockyou.txt
```
OR with username
```
hashcat -m 1000 --username svc_netupd_hash.txt /usr/share/wordlists/rockyou.txt
```
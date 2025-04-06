<h2>USING METASPLOIT FOR SMB ENUM</h2>

SMB VERSION

payloads:

1. search smb
2. use (insert number)
3. type info for auxillary information
4. type options for available options


OPTIONS
RHOST: remote host
RHOSTS: plural hosts, you can use CICR notation (/24 to sweep range)
SMBDOmain: only fill if we knew these stuffs
SMBUser: nly fill if we knew these stuffs
SMBPasss: only fill if we knew these stuffs

THREADS:

========================================================================================================================

USAGE
set RHOST (ip address)
run

=====================================

<h2>smbclient</h2>
`smbclient -L \\\\192.168.x.x\\`
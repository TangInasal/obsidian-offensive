Simple Bash IOC Scanner

This was made to address issues of LOKI and THOR
Fenrir is a simple IOC scanner bash script. 
It allows scanning Linux/Unix/OSX systems for the following Indicators of Compromise (IOCs):

- Hashes
    MD5, SHA1 and SHA256 (using md5sum, sha1sum, sha -a 256)
- File Names
    string - checked for substring of the full path, e.g. "temp/p.exe" in "/var/temp/p.exe"
- Strings
    grep in files
- C2 Server
    checking for C2 server strings in 'lsof -i' and 'lsof -i -n' output
- Hot Time Frame
    using stat in different modes - define min and max epoch time stamp and get all files that have been created in between
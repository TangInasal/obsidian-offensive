   
#nmap


  

nmap scanning
scan all/aggressive scan (too noisy, not ideal for real-world pentest)
nmap -A 192.168.x.x

scan all ports
nmap -p- 192.168.x.x

scan specific ports
nmap -p 80,443,445 192.168.x.x

Threads (the more the threads, the faster the scan and noisier)
T1-T5

see more scan info
nmap -V 192.168.x.x
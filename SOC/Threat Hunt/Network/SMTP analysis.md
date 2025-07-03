go to mail server
check open ports and its process
`sudo netstat -lntp`

check running tech from PID
`ps -fax | grep <PID>`
![[Pasted image 20250703155127.png]]

check raw emails in the mail server
`cd /var/mail`
`ls -lh`
![[Pasted image 20250703155408.png]]

------------
<h2>email header analysis</h2>
check email header
`sudo less <filename>` 

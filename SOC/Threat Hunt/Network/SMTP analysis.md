**CASE: hunt for emails that use PHP mailer**

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
![[Pasted image 20250703155945.png]]

filter files with grep
`sudo grep "PHP" *`
OR
`sudo grep "keyword_here" *`
![[Pasted image 20250703160109.png]]

search all X-Mailer from all files
`sudo grep "X-Mailer:" *`
OR cleaner results and count each
`sudo grep "X-Mailer:" * | sort | uniq -c | sort -n`
![[Pasted image 20250703160407.png]]

check suspicious email contents and its FIRST 20 lines
`sudo cat <filename> | grep "X-Mailer:PHPMailer" -B 20`
![[Pasted image 20250703160901.png]]


check suspicious email contents and its NEXT 20 lines
`sudo cat <filename> | grep "X-Mailer:PHPMailer" -A 20`
![[Pasted image 20250703161210.png]]


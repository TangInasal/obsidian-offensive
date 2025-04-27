HTB Sherlocks

unzip all contents from zip file

1. **What is the name of the repository utilized by the Pen Tester within Forela that resulted in the compromise of his host?**
			1. go to /home/user/.bash_history
			2. look for git clone command
			3. ans: ![[Pasted image 20250427182720.png]]

2. **What is the name of the malicious function within the script ran by the Pen Tester?**
			1. go to repo link https://github.com/pttemplates/autoenum/
			2. check enum.sh
			3. check code functions
			4.  ![[Pasted image 20250427182649.png]]
3. **What is the password of the zip file downloaded within the malicious function?**
			1. check enum.sh code
			2. ![[Pasted image 20250427182754.png]]
			3. 	```echo "base64 part1 and part2" | base64 -d```
				

4. **What is the full URL of the file downloaded by the attacker?** 
			1. check enum.sh
			2. ![[Pasted image 20250427182941.png]]

5. **When did the attacker finally take out the real comments for the malicious function?**. 
			1. ```git clone https://github.com/pttemplates/autoenum/```
			2. ``git log --follow enum.sh``
			3. go to github 
			4. manually check all commits for changes
			5. find the right commit hash and look for it on the git logs hashes

6. **The attacker changed the URL to download the file, what was it before the change?**
			1. select e89644a
			2. ![[Pasted image 20250427183832.png]]

7.  **What is the MITRE technique ID utilized by the attacker to persist?**
			1. the attacker uses cronjob for persistence.
			2. ![[Pasted image 20250427184003.png]]
			3. ans:  T1053.003![[Pasted image 20250427184042.png]] 
	8. **What is the Mitre Att&ck ID for the technique relevant to the binary the attacker runs?**
			1. Resource hijacking
			2. T1496 ![[Pasted image 20250427184208.png]]
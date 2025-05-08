Your rule is only **as effective as your understanding of patterns you want to search** for

Every Yara requires 2 valid arguments
1. the file we created
2. name of file, directory, or PID for the rule
Every rule must have a `name` and `condition`
e.g: `yara myrule.yar directorytoscan`
NOTE: `.yar` is the standard file extension for ALL YARA RULES

---
**Rule Writing**
1. Create a file to scan
		`touch myfile`
2. Create a new file for yara
		`touch 1stYara.yar`
3. Open `1stYara.yar` using a text editor
4. paste this
```
	rule examplerule{
		condition: true
	}
```
this rule simply checks if the  file exists
if it doesnt see a file, it will print an error


![[Pasted image 20250508182814.png]]
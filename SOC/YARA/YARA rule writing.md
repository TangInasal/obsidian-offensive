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
		`touch somefile`
2. Create a new file for yara
		`touch 1stYara.yar`
3. Open `1stYara.yar` using a text editor
4. paste this
```
	rule fileexists{
		condition: true
	}
```
this rule simply checks if the  file exists
if it doesnt see a file, it will print an error

![[Pasted image 20250508184053.png]]


---
**YARA Conditions**


**Anatomy of Yara**
![[Pasted image 20250508215552.png]]


**Keywords**

1. Desc 
2. Meta
3. Strings
4. Conditions
5. Weight


 **Meta**
		reserve for descriptive information
		you can use `desc` short for description/to summarize what your rule checks for
		does not affect the rule, similar to `commenting` on code
**Strings**
		You can use this to search for `specific texts` or `hex` in file programs
```
rule hello_world_checker{
	strngs:
		$hello_world = "Hello World"
}
```
**Conditions**
		we NEED conditions to make the RULE VALID
```
rule hello_world_checker{
	strngs:
		$hello_world = "Hello World!"

	condition:
		$hello_world (calling the variable in strings)
}
```

this rule will ONLY MATCH WITH "Hello World"
this WILL NOT MATCH with "hello world" or "HELLO WORLD"
to solve: `any of them`
```
rule hello_world_checker{
	strngs:
		$hello_world = "Hello World!"
		$hello_world_lower = "hello world!"
		$hello_world_upper = "HELLO WORLD!"
		
	condition:
		any of them
}
```
this would match with 
"Hello World!"
"hello world!", and
"HELLO WORLD!"


**you can use regular operators from programming**
`<=` less than or equal to
`>=` more than or equal to
`!=` not equal to

```
rule hello_world_checker{
	strngs:
		$hello_world = "Hello World!"
		$hello_world_lower = "hello world!"
		$hello_world_upper = "HELLO WORLD!"
		
	condition:
		#hello_world <= 10
}
```

this will only 
1. Look for "Hello World" string
2. Only matches when there are LESS THAN OR EQUAL TO 10 occurrence of "Hello World"

**You can also use keywords such as**
1. and
2. not
3. or

**and**
this rule will check if the file contains "Hello World" and check if the file is < 10kb
the rule will only match if BOTH CONDITIONS ARE TRUE
```
rule hello_world_10kb{
	strings: 
		$hello_world = "Hello World"

		condition: 
			$hello_world and filesize < 10KB
}
```

****


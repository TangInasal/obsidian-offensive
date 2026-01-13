#### 3 different formats.
- Normal output (`-oN`) with the `.nmap` file extension
- Grepable output (`-oG`) with the `.gnmap` file extension
- XML output (`-oX`) with the `.xml` file extension

We can also specify the option (`-oA`) to save the results in all formats. 
```shell-session
sudo nmap 10.129.2.28 -p- -oA target
```

**Convert XML to HTML**
```shell-session
xsltproc target.xml -o target.html
```
![[Pasted image 20260113144222.png]]


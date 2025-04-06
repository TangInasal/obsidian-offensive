<h4>Net Users</h4>

syntax:
```
Get-NetUser
```
OR
users only:
```
Get-NetUser | select cn
```

![file:///tmp/.HZGD42/1.png](file:///tmp/.HZGD42/1.png)

<h4>admin accounts only</h4>
Get-NetUser | select useraccountcontrol
(look for 500 value)
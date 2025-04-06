**list computer count**

list out all the computers inside the network

syntax:
```
Get-NetComputer
```
OR with info
```
Get-NetComputer -FullData
```
OR just OS
```
Get-NetComputer -FullData | select OperatingSystems
```


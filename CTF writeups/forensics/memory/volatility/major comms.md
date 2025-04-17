<h3>windows</h3>
imageinfo:
```
python vol.py -f file.vmem windows.info
```

scan for process
```
python vol.py -f file.vmem windows.psscan
```

list out process
```
python vol.py -f file.vmem windows.pslist
```

filter with PPID only
```
python .\vol.py -f file.vmem windows.psscan | Select-String "PPID here"    
```
OR with --pid tag
```
python vol.py -f file.vmem windows.psscan --pid PID_here
```


show directories where process are aexecuted
```
python vol.py -f file.vmem windows.cmdline
```

filter directory where PPID is executed
```
python vol.py -f file.vmem windows.cmdline | Select-String "PPID here"
```
OR specify PID
```
python vol.py -f file.vmem windows.cmdline --pid PID_here
```

show handles (what type the process is executed - e.g file, directory... etc)
```
python vol.py -f file.vmem windows.handles
```


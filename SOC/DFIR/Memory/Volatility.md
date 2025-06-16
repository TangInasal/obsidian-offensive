<h3>windows</h3>
OS Information
```
python vol.py -f file.vmem windows.info
```

scan for process
```
python vol.py -f file.vmem windows.psscan
```


Process Information
```
python vol.py -f file.vmem windows.pslist
vol.py -f “/path/to/vmem” windows.pstree
```

filter with PPID only
```
python .\vol.py -f file.vmem windows.psscan | Select-String "PPID here"    
```
OR with --pid tag
```
python vol.py -f file.vmem windows.psscan --pid <PID
```

PROCdump
```
vol.py -f “/path/to/.vmem” -o “/path/to/dir” windows.dumpfiles ‑‑pid <PID
```

Memdump
```
vol.py -f “/path/to/.vmem” -o “/path/to/dir” windows.memmap ‑‑dump ‑‑pid <PID>
```

show directories where process are executed
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


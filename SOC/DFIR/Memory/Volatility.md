<h3>windows</h3>
OS Information
```
python vol.py -f file.vmem windows.info
```

scan for process
```
python vol.py -f file.vmem windows.psscan
```
`vol.py -f “-file.vmem” ‑‑profile <profile> pstree`
`vol.py -f “-file.vmem” ‑‑profile <profile> psxview`

Process Information
```
python vol.py -f file.vmem windows.pslist
vol.py -f “-file.vmem” ‑‑profile <profile> pstree
vol.py -f “-file.vmem” ‑‑profile <profile> psxview

```

filter with PPID only
```
python .\vol.py -f file.vmem windows.psscan | Select-String "PPID here"    
```
OR with --pid tag
```
python vol.py -f file.vmem windows.psscan --pid PID_here
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


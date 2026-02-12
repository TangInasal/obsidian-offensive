
`C:\Windows\System32\winevt\Logs`

## Tools:
- Event Viewer (GUI)
- Wevtutil.exe (cli)
- Get-WinEvent (powershell cmdlet)

## ez tools:
EvtxECmd.exe (parser)
```
EvtxECmd.exe -d \path\to\logs --csv \path\to\output --csvf samplelogs.csv --vss
```
`-d` specify directory of logs
`--csv \directory` specify csv output format and output directory
`--csvf` customize filename of the parsed csv file
`--vss` parse volume shadow 

### TimeLine explorer
right click to any column and select `column chooser`
scroll to right/left and drag `Map Description` on the top


---
## Chainsaw
It's like advanced grep for event logs

**Main Operators**
- Search
- Hunt
### Search
string search
```
chainsaw.exe search -s <string> -i C:\Windows\System32\winevt\logs -e <event id/type>
```
`-s` search for specific string
`-i` case insensitive
`-e` for event type or id you are looking for

```
chainsaw.exe search -r "string[a-zA-Z]" -i C:\Windows\System32\winevt\logs -e <event id/type>
```
`-r` regex and match string

```
chainsaw.exe search -s <string> -i C:\Windows\System32\winevt\logs -e <event id/type> -o output.txt
```
`-o` output file

---
### Hunt
hunt malicious/suspicious patterns via sigma rules

#### with built-in rules
hunt with built-in rules
```
chainsaw.exe hunt C:\Windows\System32\winevt\log
```

hunt for lateral movement with built-in rules
```
chainsaw.exe hunt C:\Windows\System32\winevt\log --lateral-all
```

#### with sigma rules
hunt with sigma rules
```
chainsaw.exe hunt C:\Users\Diox\Documents\ctf\HTB\sherlocks\EnduringEcho\C\Windows\System32\winevt\logs\ --sigma sigma\rules-threat-hunting\ --mapping mappings\sigma-event-logs-all.yml --skip-errors
```

hunt for lateral movement with sigma rules
```
chainsaw.exe hunt C:\Windows\System32\winevt\log --lateral-all --rules <path\to\sigma_rules> --mapping <path\to\sigma-mapping.yml>
```

hunt and save as csv
**NOTE: this could trigger windows defender:
```
chainsaw.exe hunt C:\Windows\System32\winevt\log --lateral-all --rules <path\to\sigma_rules> --mapping <path\to\sigma-mapping.yml> --csv
```

#### timeline explorer
save the output as csv
open the csv files on `timelineexplorer.exe`


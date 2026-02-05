
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
`-i` case INsensitive
`-e` for event type or id you are looking for

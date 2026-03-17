 **resources:** https://medium.com/@N1neKitsune/dfir-mastering-thor-lite-for-advanced-threat-detection-e86d4937a8af 
 https://www.eyehatemalwares.com/incident-response/thor-lite/
 https://drive.google.com/file/d/1I5U3Yr-JgBk6WWDstuxzZy-bFT3PUL2P/view
 
---
## main flags
`--soft` 
	- used for unstable/low spec systems (e.g 1 CPU core x 1024mb ram)
	- reduces CPU load to 70%
	- skips memory intensive checks
`-c percentage`
	- when CPU usage is more important
	- almost similar to `--soft` flag
	- para dili dakog kaon sa CPU
`-e D:\folder`
	- redirect output to folder
`--debug / -a Modulename`
	- Used to spot problems
	- use `-a Modulename` to run a single module (a.g -a ProcessCheck)
	- 

---
##### Adapting to System Conditions :
For systems under high load, the options `--nosoft` and `--nolowprio` allow Thor Lite to run at normal priority, making it easier to run alongside other applications.
``` windows-cmd
thor64-lite.exe --nolowprio --nosoft
```
##### Focus on Recent Modifications :
To examine recently modified files and logs, use the commands `--lookback 30`, targeting items changed in the last 30 days.
```windows
thor64-lite.exe --lookback 30
```
##### Managing System Impact :
To minimize the impact on the system during the scan, you can limit CPU usage to 30%.
```windows
thor64-lite.exe --cpulimit 30
```
#### Using Scan Templates
Thor Lite allows the application of custom scan templates. By default, it uses `thor.yml` in the `./config` folder. To use a different template, use the `-t` parameter:
```windows
thor.exe -t custom_scan.yml
```
#### Running the Scan and Reviewing Results
Initiate a full scan with on **Windows** all disks
```
.\thor64-lite.exe --allhds 
```

Initiate a full scan with on **Windows** :C  drive only
```windows
.\thor64-lite.exe --allhds --utc
```

Initiate a full scan with on **Linux** :
```
chmod +x thor-lite-linux-64
./thor-lite-linux-64 --alldrives --utc
```    

---
##### Risky Flags[](https://thor-manual.nextron-systems.com/en/latest/usage/scan.html#risky-flags "Link to this heading")
This list contains flags that should better be avoided unless you know exactly what you're doing.

| Parameter           | Description                                                                                                |
| ------------------- | ---------------------------------------------------------------------------------------------------------- |
| **--intense**       | long runtime, stability issues due to disabled resource control                                            |
| **--c2-in-memory**  | many false positives on user workstations (especially browser memory)                                      |
| **--alldrives**     | long runtime, stability issues due to scan on network drives or other remote file systems                  |
| **--mft**           | stability issues due to high memory usage                                                                  |
| **--dump-procs**    | stability issues, possibly high disk space usage <br>(free disk space checks are implemented but may fail) |
| **--full-registry** | longer runtime, low positive impact                                                                        |

---
##### Lesser Known But Useful Flags[](https://thor-manual.nextron-systems.com/en/latest/usage/scan.html#lesser-known-but-useful-flags "Link to this heading")
This list contains flags that are often used by analysts to tweak the scan in useful ways.

| Parameter                      | Description                                                                          |
| ------------------------------ | ------------------------------------------------------------------------------------ |
| **--max-reasons 0**            | Show all reasons that led to a certain score                                         |
| **--printshim**                | Print all available SHIM cache entries into the log                                  |
| **--utc**                      | Print all timestamps in UTC (helpful when creating timelines)                        |
| **--string-context num-chars** | Number of characters preceeding and following the string match to show in the output |

---
### Examples
##### Logging to a Network Share[](https://thor-manual.nextron-systems.com/en/latest/usage/scan.html#logging-to-a-network-share "Link to this heading")
Creates a plaintext log file on a share called "rep" on system "sys" if the user running the command has the respective access rights on the share.
```
thor64.exe --nohtml --nocsv -l \\sys\rep\%COMPUTERNAME%_thor.txt
```
#####  Logging to Syslog Server[](https://thor-manual.nextron-systems.com/en/latest/usage/scan.html#logging-to-syslog-server "Link to this heading")
Log to a remote syslog server only.
```
thor64.exe --nohtml --nocsv --nolog -s syslog.server.net
```
##### Scan a Single Directory[](https://thor-manual.nextron-systems.com/en/latest/usage/scan.html#scan-a-single-directory "Link to this heading")
```
thor64.exe -a Filescan -p C:\temp
```
##### Change the output directory[](https://thor-manual.nextron-systems.com/en/latest/usage/scan.html#change-the-output-directory "Link to this heading")
```
thor64.exe -e D:\
```
##### Only scan the last 7 days of (Windows) Event Logs[](https://thor-manual.nextron-systems.com/en/latest/usage/scan.html#only-scan-the-last-7-days-of-windows-event-logs "Link to this heading")
```
thor64.exe --lookback 7
```
By default the `--lookback` flag only applies to (Windows) Event Logs. 
To apply it to all modules, use the `--global-lookback` flag.



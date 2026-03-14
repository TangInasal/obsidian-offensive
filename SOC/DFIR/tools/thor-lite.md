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
Initiate a full scan with on **Windows** :c
```windows
.\thor64-lite.exe --allhds --utc
```

Initiate a full scan with on **Linux** :
```
chmod +x thor-lite-linux-64
./thor-lite-linux-64 --alldrives --utc
```    




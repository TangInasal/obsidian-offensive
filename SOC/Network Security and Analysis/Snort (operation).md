**Snort in IDS/IPS mode**

`-c` defining configuration file
`-T` testing the configuration file
`-N` disable logging
`-D` background mode

**ALERT MODS**
`-A` ALERT MODES
full - Full alert mode, providing all possible information about the alert. This one also is the **default mode**; once you use `-A` and don't specify any mode, snort uses this mode.
fast -  shows the alert message, timestamp, source and destination IP, along with port numbers.
console -  Provides fast style alerts on the console screen.
cmg - basic header details with payload in hex and text format.
none - disabling alerts.

**background mode**
`sudo snort -c /etc/snort/snort.conf -D -l -v -X`
`-c` path to config/rule file
`-D` background mode
`-l` logging mode
`-v` verbose
`-X` full packet dump

check the snort in background
`ps -ef | grep snort`


**IDS/IPS mode with parameter "-A"**



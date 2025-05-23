
You can use Snort as a sniffer and log the sniffed packets via logger mode. 
You only need to use the packet logger mode parameters, and Snort does the rest to accomplish this.

`-l` Logger mode, target **log and alert** output directory. Default output folder is **/var/log/snort**
The default action is to dump as tcpdump format in **/var/log/snort**
`-K ASCII` logs packets in ASCII - **human readable w/o using snort instance - snort can't read ASCII logs** 
`-r` reading option, read the dumped logs in snort
`-n` Specify the number of packets that will process/read. 
Snort will stop after reading the specified number of packets.

**saving logs in current directory**
`sudo snort -dev -l .`
`-dev` sniffer mode and log
`-l` logger mode
`.` save logs in current directory

**reading snort logs**
`sudo snort -r <logfile>`
`-r` read command

**filtering snort logs**
`sudo snort -r <logfile> icmp`
`sudo snort -r <logfile> 'udp and port 53`

**read 10 packets only**
 `snort -dvr logname.log -n 10`

**open snort log with tcpdump**
`sudo tcpdump -r <logfile> -ntc 10`



zeek generates logs according to traffic data
you will have logs for every connection
zeek logs in 7 categories
zeek logs are tab-separated ASCII files

**zeek logs in a nutshell**
`network` - network protocol logs
e.g: `dhcp.log, ssh.log, smb.log, etc`
`files` - file analysis results log
e.g: `files.log`
`NetControl`- network control and flow logs
eg: `netcontrol.log, netcontrol_drop.log`
`detection` - detection and indicator logs
e.g: `intel.log, notice.log, notice_alarm.log, signatures.log, traceroute.log`
`network observations` - network flow logs
e.g: `known_certs.log, known_hosts.log, etc`
`miscellaneous` - additional logs, 
`zeek diagnostic` - system messages, actions, and some statistics
e.g: `broker.log, capture_lost.log, stdout,log, etc.`


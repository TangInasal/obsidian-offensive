processes pcap and log files 

**NOTE:**
Best is to run the pcap file thru zeek first before processing it in Zui

Count by fields
`right click on the log/packet`
`click Count by fields`

count how many alerts
`alert | fuse | count() by event_type`

filter and count each dest port
`alert | count() by dest_port | fuse`

filter hosts only
`count() by host | fuse`

identify city
`_path=="conn"|cut geo.resp.country_code,geo.resp.region,geo.resp.city`

known patterns
`event_type="alert" or _path=="notice" or _path="signatures"`

sorting
`alert | sort alert.category=="Malware " | fuse`


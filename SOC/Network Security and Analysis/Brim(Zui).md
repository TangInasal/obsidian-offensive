processes pcap and log files 


identify city
`_path=="conn"|cut geo.resp.country_code,geo.resp.region,geo.resp.city`

known patterns
`event_type="alert" or _path=="notice" or _path="signatures"`

sorting
`alert | sort alert.category=="Malware " | fuse`


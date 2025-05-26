
**commands**
`cat dhcp.log | zeek-cut host_name` - get hostname
`cat dns.log | zeek-cut count query` - get all domains
`cat conn.log | zeek-cut duration` - get all connection duration
`cat conn.log | zeek-cut duration | sort -n` - sort duration short to longest
`cat signature.log | zeek-cut uid src_addr dst_addr` - get source and destination ip


**cheatsheet**
`cat file.log | cut -f 1` - cut the first field
`cat file.log | cut -c1` - cut the first column
`cat file.log | sort` - sort file alphabetically
`cat file.log | sort -n` - sort file numerically
`cat file.log | uniq` - remove duplicates
`cat file.log | sed -n '11p'` - print line 11
`cat file.log | sed -n '10,15p'` - - print lines 11-15

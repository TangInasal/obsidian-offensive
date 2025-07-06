**Hunting Unconstrained Delegation attack with security onion**
Event ID: `4624`

Open security onion
go to security data set

in kibana
`winlog.event_id: 4624`
look for the vulnerable computer
add as a filter
**NOTE: you can remove unnecessary columns
bare minimum columns:** `Time, _id`

expand row
look for `related.user`
toggle as column
look for `user.domain`
toggle as column
filter our value
you must have a lower event count/logs

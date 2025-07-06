**Hunt kerberoasting with Security Onion**
Kerberoasting event ID: `4769`

Go to KIbana
Go to security (under datasets)

Filtering
`winlog.event_id 4769`
OR if with account/service
`winlog.event_id 4769 AND <account/service-name>`


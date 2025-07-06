**FIND REGISTERING PRIVILEGE ATTEMPTS**

**NOTE: This could've been exploited by tools like
Rubeus or Mimikatz**

Event ID: `4611`

in kibana
query:
`winlog.event_id: 4611`
delete all filters

---
**FIND ADDING PRIVILEGE ATTEMPT**

**NOTE: If the tool like rubeus or mimikatz lacks privilege
the attacker will attempt to add privilege on the tools**

Event ID: `4673`

in kibana
query:
`winlog.event_id: 4673`
delete all filters


----
**FIND SID filtering event**

**NOTE: If you see this in a domain that
was NOT migrated from/to another, 
that's a BAD sign**

Event ID: `4675`

in kibana
query:
`winlog.event_id: 4675`
delete all filters


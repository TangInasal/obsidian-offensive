Windows Event Log analysis tool written in Rust that serves a similar purpose to Chainsaw but with a different focus. 
- Chainsaw is optimised for hunting and searching 
- Hayabusa excels at generating forensic timelines and provides more granular output formatting options. 
- It also uses Sigma rules and maintains its own extensive set of detection rules.

Hayabusa’s timeline output is particularly useful for building a chronological picture of attacker activity across multiple log sources. 
Load the CSV output into Timeline Explorer (part of Eric Zimmerman’s toolset) 
or a spreadsheet and you have a filterable, sortable view of every suspicious event correlated by timestamp.

The `metrics` command is useful for rapid triage, it gives you a count of detections by severity level so you immediately know whether you are dealing with a handful of alerts or hundreds.

### **When to use it:** 
- When you need a forensic timeline from Windows Event Logs
- or when you want structured CSV/JSON output for ingestion into other analysis tools.
- Many responders use both Chainsaw and Hayabusa as they have different rule sets and output formats that complement each other.

---
#### Generate a timeline from event logs
```
hayabusa csv-timeline -d /path/to/evtx/ -o timeline.csv
```
### Run threat hunting with all rules
```
hayabusa csv-timeline -d /path/to/evtx/ -o timeline.csv -p super-verbose
```
#### Generate a summary of findings by severity
```
hayabusa metrics -d /path/to/evtx/
```
#### Output a condensed timeline of critical and high severity events only
```
hayabusa csv-timeline -d /path/to/evtx/ -o critical.csv -l critical -l high
```


LOKI is an IoC scanner

4 methods of detection:
1. FIle name IoC check - Regex match on full file path/name
2. Yara rule check - Yara signature match on file data and process memory
3. Hash Check -   Checks for malicious hash
4. C2 back connect check - Compares process connection endpoints with C2 IOCs

Additional Checks: 
1. Regin filesystem check (via --reginfs)
2. Process anomaly check (based on [Sysforensics](http://goo.gl/P99QZQ)
3. SWF decompressed scan (new since version v0.8)
4. SAM dump check


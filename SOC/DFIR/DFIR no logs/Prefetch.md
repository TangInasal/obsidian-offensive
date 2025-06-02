Cached process for fast up startup.
**Filename:** Process.exe-HASH.pf
	eg: Chrome.exe-5349D2DF.pf

**Location:**
`C:\Windows\Prefetch`

NOTE: can be used even if the executable is deleted
show proof that the executable has been run


**Tool:**
WinPrefetchView
parse:
`PECmd.exe -q -d C:\Cases\Prefetch\ --csv "C:\Users\Diox\Desktop\dfir\CASES --csvf prefetch.csv"`

Timeline Explorer
sort timeline:
Click on the `RunTime` column to sort the timeline in either ascending or descending order. This helps in creating a proper timeline of events.


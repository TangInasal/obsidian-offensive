tool: [lnk-parser](https://code.google.com/archive/p/lnk-parser/)
cmd tool - point to a lnk file - generate a report

Make a report on all .lnk files
`C:\Tools\lnk-parser.exe -c -w C:\Users\Username\Desktop`

Import CSV
`$lnk = Import-Csv ./Report-filename.csv`
**NOTE:
IF error == "Icon Location (ASCII)" already present
remove "Icon Location" columns in spreadsheet**
ctrl+f ''icon location'
find all
select columns and delete

See all lnk filenames
`$lnk.Filename`
**NOTE: the '.lnk' file extension is not visible by default
so if file is named 'file.pdf.lnk, then the user will see it as ''file.pdf' **


Look for files ran with argument
`$lnk.{Arguments (UNICODE)}`
OR
look for the html version of the report
![[Pasted image 20250704135211.png]]


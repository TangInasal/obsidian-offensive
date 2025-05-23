Yara rule generator script
**NOTE**
always update yarGen before using
`yarGen.py --update`

Generate yara for the malicious file
`yarGen.py -m directory/to/file2 --excludegood -o directory/to/file2.yar`

**flags**
`-m`  is the path to file you want to generate the rules for
`--exclduegood` exclude all goodware strings 
(strings that can be found on legit softwares - decreases false positives)
`-o` location & name you want to output the yara rule

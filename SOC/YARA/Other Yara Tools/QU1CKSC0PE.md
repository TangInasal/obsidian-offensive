<H3>ALL IN ONE MALWARE ANALYSIS (STATIC AND DYNAMIC)</H3>

**RUN**
docker run -it --rm -v ~/www/:/data quickscope:latest 

**HELP**
docker run -it --rm -v ~/www/:/data quickscope:latest -h

**UPDATE**
docker run -it --rm -v ~/www/:/data quickscope:latest --db_update

**SCAN**
docker run -it --rm -v ~/www/:/data quickscope:latest --file <file/to/scan.exe> --analyze

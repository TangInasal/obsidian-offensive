`osqueryi` - check if osquery is installed

**basic usage**
1. enter OSQuery - `osqueryi`
2. show tables - `.tables`
3. show table schema/rows - . `.schema table_name`
4. show table contents from rows - `select column1, column2 from table_name;`
5. 

**help**
`.help` - show help options
`.tables` - shows all tables that can be queried
`.tables process` - shows tables associated with a process
`.tables user` - shows tables of users

**schema**
schema - knowledge of columns and types
`.schema table_name` - shows table name schema

schema (SQL queries) for users:
![[Pasted image 20250606212827.png]]

**SQL QUERIES**
`select column1, column2, column3 from table_name;`
e.g: 
`select uid, username, description from users;`


**Display mode**
`.mode` - show display modes
1. csv
2. column
3. line
4. list
5. pretty (dafault)



**programs**
`SELECT * from programs;`
OR
`SELECT * from programs LIMIT 1;`
![[Pasted image 20250606215653.png]]

select specific columns only
`select name, version, install_date from programs;`

count all programs
`select count(*) from programs;`

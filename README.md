# mysql-docs


### Changing database charset
1. backup the existing databse (optional)
2. check current charset using `SELECT default_character_set_name FROM information_schema.SCHEMATA
WHERE schema_name = "mecon";`
3. execute `ALTER DATABASE <dbname> CHARACTER SET utf8 COLLATE utf8_general_ci;`
it will change the charset of the database.
4. execute `SELECT CONCAT("ALTER TABLE ",TABLE_SCHEMA,".",TABLE_NAME," CHARACTER SET utf8 COLLATE utf8_general_ci;   ",
    "ALTER TABLE ",TABLE_SCHEMA,".",TABLE_NAME," CONVERT TO CHARACTER SET utf8 COLLATE utf8_general_ci;  ") 
    AS alter_sql
FROM information_schema.TABLES
WHERE TABLE_SCHEMA = <dbname>;`  
and copy the result and execute.  
it will change the charset of the whole tables
5. drop and recreate all routines manually. (please PR if you have any one-liner solution or query for this step)
6. reboot the database and done.

### Ugrading Version
`mysql_upgrade --skip-version-check --force -u root` 
http://blog.naver.com/PostView.nhn?blogId=bomyzzang&logNo=178666700

# mysql-docs


### Changing database charset
1. backup the existing databse (optional)
2. execute `ALTER DATABASE <dbname> CHARACTER SET utf8 COLLATE utf8_general_ci;`
it will change the charset of the database.
3. execute `SELECT CONCAT("ALTER TABLE ",TABLE_SCHEMA,".",TABLE_NAME," CHARACTER SET utf8 COLLATE utf8_general_ci;   ",
    "ALTER TABLE ",TABLE_SCHEMA,".",TABLE_NAME," CONVERT TO CHARACTER SET utf8 COLLATE utf8_general_ci;  ") 
    AS alter_sql
FROM information_schema.TABLES
WHERE TABLE_SCHEMA = <dbname>;`  
and copy the result and execute.  
it will change the charset of the whole tables
4. drop and recreate all routines manually. (please PR if you have any one-liner solution or query for this step)
5. reboot the database and done.

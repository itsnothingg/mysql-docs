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

### User password update
`ALTER USER user IDENTIFIED BY 'auth_string';`    
https://dev.mysql.com/doc/refman/8.0/en/set-password.html

### Installing ing mac (homebrew)
https://github.com/helloheesu/SecretlyGreatly/wiki/%EB%A7%A5%EC%97%90%EC%84%9C-mysql-%EC%84%A4%EC%B9%98-%ED%9B%84-%ED%99%98%EA%B2%BD%EC%84%A4%EC%A0%95%ED%95%98%EA%B8%B0

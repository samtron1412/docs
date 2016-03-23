[TOC]

# Overview
## Install
- http://dev.mysql.com/usingmysql/get_started.html
	+ WAMP, XAMPP, LAMP

[Archive](http://downloads.mysql.com/archives/community/)

## Terminology
### [Charset](http://dev.mysql.com/doc/refman/5.0/en/charset-general.html)
A **character set** is a set of symbols and encodings. A **collation** is a set of rules for comparing characters in a character set.

# Tutorial
## Pivot stored procedure


## Admin Command line
- Log in mysql localhost: `mysql -u<user name> -p<password>`
- Log in mysql remotely: `mysql -u<user name> -p<password> -h <host ip>`
- Run a sql file: at the MySQL command line `mysql>`
`mysql> source /home/sql_file.sql;`

`help contents`

`help <command name>`

### Databases
- Show databases: `SHOW DATABASES;`
- Create database: `CREATE DATABASE abc;`
- Select a database: `USE abc;`
- Export the database (windows command): `mysqldump -u<root_user> -p<password> <database name> -r abc.sql`
	+ Note that when your MySQL server is not set to UTF-8 you need to do mysqldump **--default-character-set=latin** (!) to get a correctly encoded dump.
	+ If you only want to dump the structure without data, use: `mysqldump -u<root_user> -p<password> --no-data <database name> -r abc.sql`
- Import an existing SQL dump (windows command):

		mysql -u<root_user> -p<password> --default-character-set=utf8 <database>
		mysql> SOURCE abc.sql

### Users and their privileges
- Show all users and host can access to user account: `SELECT user,host FROM mysql.user;`
	+ Host `%` mean user account can access anywhere.
- Create a user: `CREATE USER glider IDENTIFIED BY 'gliderinsky'`
- Update password: `UPDATE mysql.user SET Password=PASSWORD('new-password-here') WHERE User='user-name-here' AND Host='host-name-here';`
- Grant permission:
	+ Basic syntax: `GRANT <permission> ON <database.table> TO 'user'@'localhost';` <permission> maybe:
		*
	+ `GRANT USAGE ON *.* TO 'glider'@'localhost' IDENTIFIED BY 'gliderinsky';`
	+ `GRANT ALL PRIVILEGES ON abc.* TO 'glider'@'localhost';`
- Apply new privileges: `FLUSH PRIVILEGES`
- Show grants for an user: `SHOW GRANTS FOR 'user'@'localhost';`
- Remove privileges: `REVOKE ALL PRIVILEGES ON <database>.<table> FROM 'user'@'localhost';`
- Delete user(revoke usage on): `DROP USER 'user'@'localhost';`


### Table
- Quick view schema of table: `describe <table name>`

## Environment
- Install MySQL Workbench

## Five problems when training in RiverCraneVn
Each problem have:
- Values return: columns
- Which tables need query
- Condition of query
- Order data after query follow columns values

Tricks:
- Use **SELECT SQL_NO_CACHE id, name FROM customer;**
	+ **SQL_NO_CACHE**: The server does not use the query cache. It neither checks the query cache to see whether the result is already cached, nor does it cache the query result.
- Optimization
	+ [Cache](http://www.databasejournal.com/features/mysql/article.php/3110171/MySQLs-Query-Cache.htm)
	+ You can read about [optimizing queries and indexes](http://www.databasejournal.com/features/mysql/article.php/1382791/Optimizing-MySQL-Queries-and-Indexes.htm), optimizing by [improving the hardware, and tweaking the MySQL variables](http://www.databasejournal.com/features/mysql/article.php/1402311/Optimizing-MySQL-Hardware-and-the-Mysqld-Variables.htm), using the [slow query log](http://www.databasejournal.com/features/mysql/article.php/2013631/MySQLs-Over-looked-and-Under-worked-Slow-Query-Log.htm), and of course, there are other methods such as **replication**.
	+ **EXPLAIN**

### Number 1
- Use **SELECT, FROM, WHERE, ORDER BY**
- Use **CASE, WHEN, REGEXP**

		case
			when left(model_hyouji,1) regexp '[0-9]' then 0
			when left(model_hyouji,1) regexp '[a-z|A-Z]' then 1
			else 2
		end as prefix

- Maybe can use **IF(condition, true, false)**, e.g: IF(state IS NULL, 'N/A', state)

### Number 2
- First use of JOIN, INNER JOIN, LEFT/RIGHT JOIN, FULL OUTER JOIN
- **INNER JOIN/JOIN**: The **INNER JOIN** keyword selects all rows from both tables as long as there is a match between the columns in both tables.
- The **LEFT OUTER JOIN/LEFT JOIN** keyword returns all rows from the left table (table1), with the matching rows in the right table (table2). The result is **NULL** in the right side when there is no match.
- The **RIGHT OUTER JOIN/RIGHT JOIN** keyword returns all rows from the right table (table2), with the matching rows in the left table (table1). The result is NULL in the left side when there is no match.
- The **FULL OUTER JOIN/FULL JOIN** keyword returns all rows from the left table (table1) and from the right table (table2).
The FULL OUTER JOIN keyword combines the result of both LEFT and RIGHT joins.
- The **CROSS JOIN** keyword returns all rows where each row from the first table is combined with each row from the second table. Similar **SELECT * FROM tbl1, tbl2;** (Decarter)



## Transaction
- [Understanding Transaction Processing](http://www.brainbell.com/tutorials/MySQL/Understanding_Transaction_Processing.htm)
- [mysql docs](http://dev.mysql.com/doc/refman/5.7/en/commit.html)

# Command reference
## INSERT
	INSERT [LOW_PRIORITY | HIGH_PRIORITY] [IGNORE]
	[INTO] tbl_name [(col_name, ...)]
	{VALUES | VALUE} ({expr | DEFAULT},...),(...),...
    [ ON DUPLICATE KEY UPDATE
      col_name=expr
        [, col_name=expr] ... ]

	INSERT INTO tbl_name (col1,col2) VALUES(15,col1*2);

Insert multiple rows:

	INSERT INTO tbl_name (a,b,c) VALUES(1,2,3),(4,5,6),(7,8,9);



If INSERT inserts a row into a table tha has an `AUTO_INCREMENT` column, you can find the value used for that column by using the SQL `LAST_INSERT_ID()` function.

## REPLACE
Works excatly like INSERT, except that if an old row in the table has the same value as a new row for a PRIMARY KEY or a UNIQUE index, the old row is deleted before the new row is inserted.

	REPLACE [LOW_PRIORITY | DELAYED] [INTO] tbl_name [(col_name, ...)] {VALUES | VALUE} ({expr | DEFAULT}, ...), (...), ...


## DELETE
Single-table syntax:

	DELETE [LOW_PRIORITY] [QUICK] [IGNORE] FROM tbl_name
	    [WHERE where_condition]
	    [ORDER BY ...]
	    [LIMIT row_count]

Multiple-table syntax:

	DELETE [LOW_PRIORITY] [QUICK] [IGNORE]
	    tbl_name[.*] [, tbl_name[.*]] ...
	    FROM table_references
	    [WHERE where_condition]

For the single-table syntax, the DELETE statement deletes rows from tbl_name and returns a count of the number of deleted rows.

For the multiple-table syntax, DELETE deletes from each tbl_name the rows that satisfy the conditions. In this case, ORDER BY and LIMIT cannot be used.





## UPDATE
Single table syntax

	UPDATE [LOW_PRIORITY] [IGNORE] table_reference
	    SET col_name1={expr1|DEFAULT} [, col_name2={expr2|DEFAULT}] ...
	    [WHERE where_condition]
	    [ORDER BY ...]
	    [LIMIT row_count]

Multiple tables syntax

	UPDATE [LOW_PRIORITY] [IGNORE] table_references
	    SET col_name1={expr1|DEFAULT} [, col_name2={expr2|DEFAULT}] ...
	    [WHERE where_condition]


## ALTER
Change datatype of column

	ALTER TABLE tblName MODIFY colName newDataType;

Add new column

	ALTER TABLE tblName ADD COLUMN colName colDataType;

Syntax

	ALTER [ONLINE | OFFLINE] [IGNORE] TABLE tbl_name
	    [alter_specification [, alter_specification] ...]
	    [partition_options]

	alter_specification:
	    table_options
	  | ADD [COLUMN] col_name column_definition
	        [FIRST | AFTER col_name ]
	  | ADD [COLUMN] (col_name column_definition,...)
	  | ADD {INDEX|KEY} [index_name]
	        [index_type] (index_col_name,...) [index_option] ...
	  | ADD [CONSTRAINT [symbol]] PRIMARY KEY
	        [index_type] (index_col_name,...) [index_option] ...
	  | ADD [CONSTRAINT [symbol]]
	        UNIQUE [INDEX|KEY] [index_name]
	        [index_type] (index_col_name,...) [index_option] ...
	  | ADD FULLTEXT [INDEX|KEY] [index_name]
	        (index_col_name,...) [index_option] ...
	  | ADD SPATIAL [INDEX|KEY] [index_name]
	        (index_col_name,...) [index_option] ...
	  | ADD [CONSTRAINT [symbol]]
	        FOREIGN KEY [index_name] (index_col_name,...)
	        reference_definition
	  | ALTER [COLUMN] col_name {SET DEFAULT literal | DROP DEFAULT}
	  | CHANGE [COLUMN] old_col_name new_col_name column_definition
	        [FIRST|AFTER col_name]
	  | MODIFY [COLUMN] col_name column_definition
	        [FIRST | AFTER col_name]
	  | DROP [COLUMN] col_name
	  | DROP PRIMARY KEY
	  | DROP {INDEX|KEY} index_name
	  | DROP FOREIGN KEY fk_symbol
	  | DISABLE KEYS
	  | ENABLE KEYS
	  | RENAME [TO|AS] new_tbl_name
	  | ORDER BY col_name [, col_name] ...
	  | CONVERT TO CHARACTER SET charset_name [COLLATE collation_name]
	  | [DEFAULT] CHARACTER SET [=] charset_name [COLLATE [=] collation_name]
	  | DISCARD TABLESPACE
	  | IMPORT TABLESPACE
	  | ADD PARTITION (partition_definition)
	  | DROP PARTITION partition_names
	  | COALESCE PARTITION number
	  | REORGANIZE PARTITION [partition_names INTO (partition_definitions)]
	  | ANALYZE PARTITION {partition_names | ALL}
	  | CHECK PARTITION {partition_names | ALL}
	  | OPTIMIZE PARTITION {partition_names | ALL}
	  | REBUILD PARTITION {partition_names | ALL}
	  | REPAIR PARTITION {partition_names | ALL}
	  | PARTITION BY partitioning_expression
	  | REMOVE PARTITIONING

	index_col_name:
	    col_name [(length)] [ASC | DESC]

	index_type:
	    USING {BTREE | HASH}

	index_option:
	    KEY_BLOCK_SIZE [=] value
	  | index_type
	  | WITH PARSER parser_name

	table_options:
	    table_option [[,] table_option] ...  (see CREATE TABLE options)

	partition_options:
	    (see CREATE TABLE options)


## SHOW WARNINGS

## SHOW ERRORS


# Tips and Tricks
- [mysql Tips](https://dev.mysql.com/doc/refman/5.7/en/mysql-tips.html)
- [optimization Tips](http://dev.mysql.com/doc/refman/5.7/en/miscellaneous-optimization-tips.html)
- [mysqldump Tips](http://dev.mysql.com/doc/refman/5.7/en/mysqldump-tips.html)

## [Enable InnoDB](http://stackoverflow.com/questions/4757589/how-to-enable-innodb-in-mysql)


## Careful with update and delete query
- [discuss in stackoverflow](http://stackoverflow.com/questions/2173049/recovery-after-wrong-mysql-update-query)
- Backup before update, delete.
- Use explicit [transaction](http://dev.mysql.com/doc/refman/5.7/en/commit.html) for InnoDB.
-

## Cast to INT
[CAST function and operators](https://dev.mysql.com/doc/refman/5.0/en/cast-functions.html)
[Cast from VARCHAR to INT - StackOverflow](http://stackoverflow.com/questions/12126991/cast-from-varchar-to-int-mysql)

`SELECT CAST(PROD_CODE AS UNSIGNED) FROM PRODUCT`

## Delete All Data in a MySQL Table
### Delete and Truncate
There are two ways to delete all the data in a MySQL database table.

`TRUNCATE TABLE tablename;` This will delete all data in the table very quickly. In MySQL the table is actually dropped and recreated, hence the speed of the query. The number of deleted rows for MyISAM tables returned is zero; for INNODB it returns the actual number deleted.

`DELETE FROM tablename;` This also deletes all the data in the table, but is not as quick as using the "TRUNCATE TABLE" method. In MySQL >= 4.0 the number of rows deleted is returned; in MySQL 3.23 the number returned is always zero.

### Auto Increment Columns for MyISAM Tables
If you have an auto increment primary key column in your MyISAM table the result will be slightly different depending which delete method you use. When using the "TRUNCATE TABLE" method the auto increment seed **value will be reset back to 1**. When using the "DELETE FROM" method the auto increment seed will be **left as it was before** (eg if the auto increment field of last inserted record was 123 the next inserted record will be set to 124).

Note that this is **true for MySQL >= 4.0**; from my reading of the TRUNCATE manual page in **MySQL 3.23 TRUNCATE works just like DELETE which would mean the auto increment seed is not reset**. I do not currently have a 3.23 database set up to test it so cannot confirm this.

### Auto Increment Columns for INNODB Tables
For INNODB tables, whether you use the "TRUNCATE TABLE" or "DELETE FROM" methods, the auto increment field will not be reset. If you inserted 5 records into a new table, then deleted all records and inserted another record, the field would have a value of 6, regardless of which method you used.

**Update 17 Feb 2009**: I originally wrote this post when MySQL 4.0 was the current version. I've just tested the above now on an INNODB table using MySQL 5.0 and using TRUNCATE does reset the auto increment field back to the default. So either the behavior changed at some point or I was incorrect when making the above statement.

## [Log Files](http://www3.physnet.uni-hamburg.de/physnet/mysql/manual_Log_files.html)


## [Restore new password for root user](https://dev.mysql.com/doc/refman//5.5/en/resetting-permissions.html)
### Windows
1. Stop mysqld by xampp control panel or windows services
2. Create file `mysql-init.txt` with content:
		UPDATE mysql.user SET Password=PASSWORD('toor') WHERE User='root';
		FLUSH PRIVILEGES;
3. Run mysqld with command prompt: `mysqld --init-file="path_to_init_file"`
		`mysqld --init-file="D:\thaison\dev_server\xampp\mysql\bin\mysql-init.txt"`
4. Now root user have new password is `toor`.

### UNIX



## [REPLICATION](https://dev.mysql.com/doc/refman/5.0/en/replication-howto.html)
master: is database use to update other database
slave: databases is updated by master database

## [Reinstall MySQL on Linux](http://www.cyberciti.biz/faq/linux-completely-reinstall-mysql-server/)
1. Backup database and all config files
2. Erase/uninstall existing mysql server/client.
3. Delete all files data directory.
4. Delete all mysql config files.
5. Completely reinstall mysql server.
6. Restore config files and database.

### 1. Backup backup backup
Make a backup - it cannot be stressed enough how important it is to make a backup of your system before you do this. You need to backup

1. MySQL database data directory (e.g. `/var/lib/mysql/`).
2. MySQL databases using **mysqldump** command.
3. Mysql config files `/etc/my.cnf`, `/etc/logrotate.d/mysqld`, and other files.
4. Mysql log files (e.g. `/var/log/mysqld.log`).

In this example, I am backing up all important files on CentOS/RHEL 6.x based server:

	# mkdir /root/mysql-files/
	# tar zcvf /root/mysql-files/mysql.config-files.dd-mm-yyyy.tar.gz /etc/logrotate.d/mysqld /var/log/mysqld.log /etc/my.cnf /root/my.cnf /var/lib/mysql/

In this example, I am backing up all databases using a shell script called `mysql-backup.sh`:

```bash
#!/bin/sh
# mysql-backup.sh: Dump MySQL databases.
# Note: Test only on RHEL/CentOS/Debian/Ubuntu Linux.
# Author: nixCraft <www.cyberciti.biz> Under GPL v2.0+
# -----------------------------------------------------
NOW=$(date +"%d-%m-%Y")
BAK="/root/mysql-files/$NOW"

##################
## SET ME FIRST ##
##################
MUSER="root"
MPASS="YOUR-ROOT-PASSWORD-HERE"
MHOST="localhost"

MYSQL="$(which mysql)"
MYSQLDUMP="$(which mysqldump)"
GZIP="$(which gzip)"

if [ ! -d $BAK ]; then
  mkdir -p $BAK
else
 :
fi

DBS="$($MYSQL -u $MUSER -h $MHOST -p$MPASS -Bse 'show databases')"
echo -n "Dumping...${THISDB}..."
for db in $DBS
do
 echo -n "$db "
 FILE=$BAK/mysql-$db.$NOW-$(date +"%T").gz
 $MYSQLDUMP -u $MUSER -h $MHOST -p$MPASS $db | $GZIP -9 > $FILE
done
echo -n  "...Done @ ${BAK} directory."
echo ""
```

Run it as follows

	$ ./mysql-backup.sh

Sample outputs:

	Dumping......blog cyberciti mysql...Done @ /root/mysql-files/08-12-2013 directory.

Verify backups:

	# ls -l /root/mysql-files/08-12-2013

Sample outputs:

	-rw-r--r--. 1 root root  1836687 Dec  8 04:00 mysql-blog.08-12-2013-04:00:18.gz
	-rw-r--r--. 1 root root  7152648 Dec  8 04:00 mysql-cyberciti.08-12-2013-04:00:25.gz
	-rw-r--r--. 1 root root   135530 Dec  8 04:00 mysql-mysql.08-12-2013-04:00:41.gz

I suggest that you read our previous guide "[HowTo: Migrate / Move MySQL Database And Users To New Server](http://www.cyberciti.biz/tips/move-mysql-users-privileges-grants-from-one-host-to-new-host.html)" for more information.

### 2. Erase/Delete MySQL server

If you are using Debian/Ubuntu Linux type the following apt-get command:

	$ sudo apt-get purge mysql-server mysql-common mysql-client

Sample outputs:

	Reading package lists... Done
	Building dependency tree
	Reading state information... Done
	Package mysql-client is not installed, so not removed
	The following packages were automatically installed and are no longer required:
	  libnet-daemon-perl libdbi-perl libterm-readkey-perl mysql-server-core-5.5 mysql-client-core-5.5
	  libplrpc-perl
	Use 'apt-get autoremove' to remove them.
	The following packages will be REMOVED:
	  libdbd-mysql-perl* libmysqlclient18* mysql-client-5.5* mysql-common* mysql-server*
	  mysql-server-5.5*
	0 upgraded, 0 newly installed, 6 to remove and 2 not upgraded.
	After this operation, 67.3 MB disk space will be freed.
	Do you want to continue [Y/n]? y
	(Reading database ... 82128 files and directories currently installed.)
	Removing mysql-server ...
	Removing mysql-server-5.5 ...
	mysql stop/waiting
	Purging configuration files for mysql-server-5.5 ...
	Removing mysql-client-5.5 ...
	Removing libdbd-mysql-perl ...
	Removing libmysqlclient18 ...
	Purging configuration files for libmysqlclient18 ...
	Removing mysql-common ...
	Purging configuration files for mysql-common ...
	dpkg: warning: while removing mysql-common, directory '/etc/mysql' not empty so not removed.
	Processing triggers for man-db ...
	Processing triggers for ureadahead ...
	Processing triggers for libc-bin ...
	ldconfig deferred processing now taking place

Delete config/database/log files using rm command:

	$ sudo rm -rvfi /var/lib/mysql /etc/mysql/ /var/log/mysql*

If you are using CentOS/RHEL/Fedora/Red Hat/Scientific Linux type the following yum command to uninstall mysql:

	# yum remove mysql mysql-server

Sample outputs:

	Loaded plugins: product-id, rhnplugin, security, subscription-manager
	This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.
	This system is receiving updates from RHN Classic or RHN Satellite.
	Setting up Remove Process
	Resolving Dependencies
	--> Running transaction check
	---> Package mysql.x86_64 0:5.1.71-1.el6 will be erased
	---> Package mysql-server.x86_64 0:5.1.71-1.el6 will be erased
	--> Finished Dependency Resolution

	Dependencies Resolved

	======================================================================================================
	 Package                Arch             Version                Repository                       Size
	======================================================================================================
	Removing:
	 mysql                  x86_64           5.1.71-1.el6           @rhel-x86_64-server-6           2.4 M
	 mysql-server           x86_64           5.1.71-1.el6           @rhel-x86_64-server-6            25 M

	Transaction Summary
	======================================================================================================
	Remove        2 Package(s)

	Installed size: 27 M
	Is this ok [y/N]: y
	Downloading Packages:
	Running rpm_check_debug
	Running Transaction Test
	Transaction Test Succeeded
	Running Transaction
	  Erasing    : mysql-server-5.1.71-1.el6.x86_64                                                   1/2
	  Erasing    : mysql-5.1.71-1.el6.x86_64                                                          2/2
	  Verifying  : mysql-server-5.1.71-1.el6.x86_64                                                   1/2
	  Verifying  : mysql-5.1.71-1.el6.x86_64                                                          2/2

	Removed:
	  mysql.x86_64 0:5.1.71-1.el6                    mysql-server.x86_64 0:5.1.71-1.el6

	Complete!

Delete config/database/log files using rm command:

	# rm -rfvi /etc/my.cnf /var/lib/mysql/ /var/log/mysqld.log

### 3. Reinstall mysql database server

If you are using CentOS/RHEL/Fedora/Red Hat/Scientific Linux type the following yum command to install mysql:

	# yum install mysql mysql-server

If you are using Debian/Ubuntu Linux type the following apt-get command:

	$ sudo apt-get install mysql-client mysql-server mysql-common

### 4. Restore config files and databases

Restore all config files and databases as demonstrated in step #1. See how to restore a backup of a mysql database:

	$ gunzip mysql-blog.08-12-2013-04:00:18.gz
	$ mysql -u root -p mysql -e 'CREATE DATABASE blog;'
	$ mysql -u root -p blog < mysql-blog.08-12-2013-04\:00\:18

Restore mysql config file as follows:

	# tar xvf /root/mysql-files/mysql.config-files.dd-mm-yyyy.tar.gz -C /root/backups/
	# cp /root/backups/etc/my.cnf /etc
	# service mysqld restart

# Best Practices
- [1](http://code.tutsplus.com/tutorials/top-20-mysql-best-practices--net-7855)
- [2](http://www.onextrapixel.com/2013/08/02/20-tips-and-tricks-any-mysql-database-developer-should-consider/)
- [3](http://it.toolbox.com/blogs/unix-admin/mysql-tips-and-trick-58610)
- [4]()

# Troubleshoot
## SQL state [HY000]; error code [145]; Table 'xxx' is marked as crashed and should be repaired; nested exception is java.sql.SQLException
First, you need connect to mysql server and use database contain that table.

Then you use below command to check status of table: `CHECK TABLE <table_name>`

After that, you use command `REPAIR TABLE <table_name>` to repair this table.

**P/s**: change your table name to position of `<table_name>` at each command above.

## ERROR 1286 (42000): Unknown table engine 'INNODB'
When run command:

	mysql> show engine innodb status;

it will show error above and run command: `show engines;` you do not see InnoDB in list of engine.

Fix by stop mysqld remove file log of InnoDB `ib_logfile0 ib_logfile1` and restart mysqld.

Find file by command: `find / -name ib_logfile0` often locate at mysql folder.

## Effect of collation
Collation `xxx_unicode_ci` have rules for right sorting characters. But it have effect when you compare characters.

### Links:

	http://dev.mysql.com/doc/refman/5.0/en/charset-collation-effect.html

### Fix:
- Change to `utf8_bin`
- Change datatype not `char`.

## ERROR 1364: Field doesn't have a default values
This is caused by the `STRICT_TRANS_TABLES` SQL mode defined. Remove that mode and restart Mysql.

### [Link](http://www.noelherrick.com/blog/mysql-strict_all_tables-vs-strict_trans_tables)

`STRICT_ALL_TABLES`: avoid insert wrong values to database, check type of column but do not have transaction, when you use MyISAM, you got some records inserted and some not.

`STRICT_TRANS_TABLES`: like STRICT_ALL_TABLES but have transaction, use with InnoDB and no record inserted if have an error.

## [Best practice for clean mysql InnoDB storage engine](http://stackoverflow.com/questions/3927690/howto-clean-a-mysql-innodb-storage-engine)

To shrink `ibdata1` once and for all you must do the following:

1. Dump (e.g., with mysqldump) all databases into a .sql text file (SQLData.sql is used below)

2. Drop all databases (except for mysql and information_schema) CAVEAT : As a precaution, please run this script to make absolutely sure you have all user grants in place:

		mkdir /var/lib/mysql_grants
		cp /var/lib/mysql/mysql/* /var/lib/mysql_grants/.
		chown -R mysql:mysql /var/lib/mysql_grants

3. Login to mysql and run `SET GLOBAL innodb_fast_shutdown = 0;` (This will completely flush all remaining transactional changes from `ib_logfile0` and `ib_logfile1`)

4. Shutdown MySQL

5. Add the following lines to `/etc/my.cnf` (or my.ini on Windows)

		[mysqld]
		innodb_file_per_table
		innodb_flush_method=O_DIRECT
		innodb_log_file_size=1G
		innodb_buffer_pool_size=4G

	(Sidenote: Whatever your set for `innodb_buffer_pool_size`, make sure `innodb_log_file_size` is 25% of `innodb_buffer_pool_size`.

	Also: `innodb_flush_method=O_DIRECT` is not available on Windows)

6. Delete `ibdata*` and `ib_logfile*`, Optionally, you can remove all folders in `/var/lib/mysql`, except `/var/lib/mysql/mysql`.

7. Start MySQL (This will recreate `ibdata1` [10MB by default] and `ib_logfile0` and `ib_logfile1` at 1G each).

8. Import SQLData.sql

Now, ibdata1 will still grow but only contain table metadata because each InnoDB table will exist outside of ibdata1. ibdata1 will no longer contain InnoDB data and indexes for other tables.

For example, suppose you have an InnoDB table named mydb.mytable. If you look in /var/lib/mysql/mydb, you will see two files representing the table:

mytable.frm (Storage Engine Header)
mytable.ibd (Table Data and Indexes)

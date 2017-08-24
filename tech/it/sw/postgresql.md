[TOC]

# I - Tutorial
## Chapter 0 - Command and Use
**psql env**

- Create a new cluster or integrate an existing one into the postgresql-common architecture: **pg_createcluster**
- Completely remove a cluster: **pg_dropcluster**
- Control the server process of a cluster (start, stop, restart): **pg_ctlcluster**
- Show all database cluster: **pg_lsclusters**
- Show list user (role): **\du**
- List all databases: **\list**
- List all tables of current database: **\dt**
- Change password of role:
	+ `sudo -u postgres psql <db name>`
	+ `\password <role name>`
- Search role to know  commands work with database role
- 

## Chapter 1 - Getting started
### 1.1 - [Installation](http://www.postgresql.org/download/)
- [Wiki](https://wiki.postgresql.org/wiki/Main_Page)
- [Docs](http://www.postgresql.org/docs/)
- [Community](http://www.postgresql.org/community/)
- [Developer PostgreSQL](http://www.postgresql.org/developer/)
- Ubuntu:
	+ Use apt repository of postgresql
	+ Install postgresql and pgadmin3 (GUI)

### 1.2 - Architectural fundamentals
In database jargon, PostgreSQL uses a **client/server model**. A PostgreSQL session consists of the following cooperating *processes* (programs):

- A **server process**, which manages the database files, accepts connections to the database from client applications, and performs database actions on behalf of the clients. The database server program is called **postgres**.
- The **user's client** (frontend) application that wants to perform database operations. Client applications can be very diverse in nature: a client could be a *text-oriented tool*, a *graphical application*, a *web server* that accesses the database to display web pages, or a *specialized database maintenance tool*. Some client applications are supplied with the PostgreSQL distribution; most are developed by users.

The PostgreSQL server can handle *multiple concurrent connections* from clients. To achieve this it starts ("*forks*") a *new process for each connection*. From that point on, the client and the new server process communicate without intervention by the original postgres process. Thus, the *master server process is always running*, waiting for client connections, whereas client and associated server processes come and go.

### 1.3 - Creating a Database
	$ createdb mydb

Output maybe:

	createdb: command not found

it mean PostgreSQL was not installed properly.

	createdb: could not connect to database postgres: FATAL:  role "joe" does not exist

This will happen if the administrator has not created a PostgreSQL user account for you.

	createdb: database creation failed: ERROR:  permission denied to create database

If you have a user account but it does not have the privileges required to create a database, you will see this. Contact with admin to grant permisson for you.

Remove database:

	$ dropdb mydb

### 1.4 - Accessing a Database
Once you have created a database, you can access it by:

- Running the PostgreSQL interactive terminal program, called *psql*, which allows you to interactively enter, edit, and execute SQL commands.

- Using an existing *graphical frontend tool like pgAdmin* or an office suite with ODBC or JDBC support to create and manipulate a database. These possibilities are not covered in this tutorial.

- Writing a custom application, using one of the several available language bindings. These possibilities are discussed further in Part IV.

Start up **psql**

	$ psql mydb

If you do not supply the database name then it will default to your user account name. You'll see messages:

	psql (9.3.5)
	Type "help" for help.

	mydb=>

Last line can be

	mydb=#

it mean you are a database superuser.

## Chapter 2 - The SQL language

## Chapter 3 - Advanced features
View, Foreign keys, Transaction, Functions, etc.

# II - The SQL Language

# III - Server administration
## Chapter 17 - Server setup and Operation
### 17.1 - The PostgreSQL User Account
As with any *server daemon that is accessible to the outside world*, it is advisable to run PostgreSQL under a separate user account. This user account should only own the data that is managed by the server, and should not be shared with other daemons. (For example, using the user nobody is a bad idea.) It is not advisable to install executables owned by this user because compromised systems could then modify their own binaries.

To add a Unix user account to your system, look for a command *useradd* or *adduser*. The user name *postgres* is often used, and is assumed throughout this book, but you can use another name if you like.

### 17.2 - Creating a Database Cluster
Before you can do anything, you must *initialize a database storage area on disk*. We call this a **database cluster**. (SQL uses the term *catalog cluster*.) A database cluster is a *collection of databases that is managed by a single instance of a running database server*. After initialization, a database cluster will *contain a database named postgres*, which is meant as a default database for use by utilities, users and third party applications. The database server itself does not require the postgres database to exist, but many external utility programs assume it exists. Another database created within each cluster during initialization is called *template1*. As the name suggests, this will be used as a template for subsequently created databases; it should not be used for actual work. (See Chapter 21 for information about creating new databases within a cluster.)

In file system terms, a database cluster will be a *single directory under which all data will be stored*. We call this the **data directory** or **data area**. It is completely up to you where you choose to store your data. There is no default, although locations such as **/usr/local/pgsql/data** or **/var/lib/pgsql/data** are popular. To initialize a database cluster, use the command **initdb**, which is installed with PostgreSQL. The desired file system location of your database cluster is indicated by the **-D** option. You will find initdb under `/usr/lib/postgresql/x.y/bin/`.

	$ initdb -D /usr/local/pgsql/data

Note that you must execute this command while logged into the *PostgreSQL user account.*

**initdb** will attempt to create the directory you specify if it does not already exist. It is likely that it will not have the permission to do so (if you followed our advice and created an unprivileged account). In that case you should create the directory yourself (as root) and change the owner to be the PostgreSQL user. Here is how this might be done:

	root# mkdir /usr/local/pgsql/data
	root# chown postgres /usr/local/pgsql/data
	root# su postgres
	postgres$ initdb -D /usr/local/pgsql/data

**initdb** will refuse to run if the data directory looks like it has already been initialized.

Because the data directory contains all the data stored in the database, it is essential that it be secured from unauthorized access. **initdb** therefore revokes access permissions from everyone but the PostgreSQL user.

However, while the directory contents are secure, the default client authentication setup allows any local user to connect to the database and even become the database superuser. If you do not trust other local users, we recommend you use one of initdb's **-W**, **--pwprompt** or **--pwfile** options to assign a password to the database superuser. Also, specify **-A md5** or **-A password** so that the default trust authentication mode is not used; or modify the generated **pg_hba.conf** file after running initdb, but *before* you start the server for the first time. (Other reasonable approaches include using peer authentication or file system permissions to restrict connections. See *Chapter 19* for more information.)

See also `/usr/share/doc/postgresql-common/README.Debian.gz` for more information on the setup on Debian and Ubuntu.

	Please note that you can of course also use the upstream tools for creating clusters, such as initdb(1). However, please note that in this case you cannot expect *any* of above pg_* tools to work, since they use different configuration settings and file locations. If in doubt, then do *not* use initdb, but only pg_createcluster. Since merely installing postgresql-X.Y will already set up a default cluster which is ready to work, most people do not need to bother about initdb or pg_createcluster at all.

**Cluster management**

For managing clusters, the following commands are provided (each with its own
manual page):

	pg_createcluster  - Create a new cluster or integrate an existing one into the postgresql-common architecture.
	pg_dropcluster    - Completely remove a cluster.
	pg_ctlcluster     - Control the server process of a cluster (start, stop, restart).
	pg_lsclusters     - Show a list of all existing clusters and their status.
	pg_upgradecluster - Migrate a cluster from one major version to another one.

Please note that you can of course also use the upstream tools for
creating clusters, such as initdb(1). However, please note that in
this case you cannot expect *any* of above pg_* tools to work, since
they use different configuration settings (SSL, data directories,
etc.) and file locations (e. g.
/etc/postgresql/9.1/main/postgresql.conf). If in doubt, then do *not*
use initdb, but only pg_createcluster. Since merely installing
postgresql-X.Y will already set up a default cluster which is ready to
work, most people do not need to bother about initdb or
pg_createcluster at all.

	postgres$ pg_createcluster 9.3 data
	postgres$ pg_dropcluster 9.3 data


**Starting the PostgreSQL cluster**

Before anyone can access the database, you must start the database server. The database server program is called **postgres**. The **postgres** program must know where to find the data it is supposed to use. This is done with the **-D** option.

	$ sudo -u postgres /usr/lib/postgresql/9.3/bin/postgres -D /var/lib/postgresql/9.3/main/ -o "-c config_file=/etc/postgresql/9.3/main/postgresql.conf" start

Thus, the simplest way to start the server is:

	$ sudo -u postgres pg_ctlcluster 9.3 main start/stop/restart
	$ sudo -u postgres pg_ctlcluster 9.3 data start/stop/restart

Command behind will start/stop all cluster:

	$ sudo service postgresql start/stop









## Chapter 20 - Database Roles
PostgreSQL manages database access permissions using the concept of **roles**. A role can be thought of as either a *database user*, or a *group of database users*, depending on how the role is set up. Roles can own *database objects* (for example, tables) and can assign privileges on those objects to other roles to control who has access to which objects. Furthermore, it is possible to grant *membership* in a role to another role, thus allowing the member role to use privileges assigned to another role.

This chapter describes how to create and manage roles.

### 20.1 - Database Roles
Database roles are conceptually *completely separate from operating system users*. In practice it might be convenient to maintain a correspondence, but this is *not required*. Database roles are global across a database cluster installation (and not per individual database). To create a role use the **CREATE ROLE** SQL command:

	CREATE ROLE name;

To remove an existing role, use the analogous DROP ROLE command:

	DROP ROLE name;

For convenience, the programs **createuser** and **dropuser** are provided as wrappers around these SQL commands that can be called from the *shell command line*:

	createuser name
	dropuser name

To determine the set of existing roles, examine the **pg_roles** system catalog, for example:

	SELECT rolname FROM pg_roles;

The psql program's **\du** meta-command is also useful for listing the existing roles.

### 20.2 - Roles Attributes
A database role can have a number of attributes that define its privileges and interact with the client authentication system.

**login privilege**
Only roles that have the LOGIN attribute can be used as the initial role name for a database connection. A role with the LOGIN attribute can be considered the same as a "database user". To create a role with login privilege, use either:

	CREATE ROLE name LOGIN;
	CREATE USER name;

**superuser status**
A database superuser bypasses all permission checks, *except the right to log in or the right to initiate replication*. This is a dangerous privilege and should not be used carelessly; it is best to do most of your work as a role that is not a superuser. To create a new database superuser, use **CREATE ROLE name SUPERUSER**. You must do this as a role that is already a superuser. Creating a superuser will by default also grant permissions to initiate streaming replication. For increased security this can be disallowed using **CREATE ROLE name SUPERUSER NOREPLICATION**.

**database creation**

	CREATE ROLE name CREATEDB.

**role creation**

	CREATE ROLE name CREATEROLE

A role with CREATEROLE privilege can alter and drop other roles, too, as well as grant or revoke membership in them. However, to create, alter, drop, or change membership of a superuser role, superuser status is required; CREATEROLE is insufficient for that.

**initiating replication**
A role must explicitly be given permission to initiate streaming replication. A role used for streaming replication must always have LOGIN permission as well. To create such a role, use **CREATE ROLE name REPLICATION LOGIN**.

**password**

A role's attributes can be modified after creation with **ALTER ROLE**.

	ALTER ROLE name [ [ WITH ] option [ ... ] ]

	where option can be:

	      SUPERUSER | NOSUPERUSER
	    | CREATEDB | NOCREATEDB
	    | CREATEROLE | NOCREATEROLE
	    | CREATEUSER | NOCREATEUSER
	    | INHERIT | NOINHERIT
	    | LOGIN | NOLOGIN
	    | REPLICATION | NOREPLICATION
	    | CONNECTION LIMIT connlimit
	    | [ ENCRYPTED | UNENCRYPTED ] PASSWORD 'password'
	    | VALID UNTIL 'timestamp'

	ALTER ROLE name RENAME TO new_name

	ALTER ROLE name [ IN DATABASE database_name ] SET configuration_parameter { TO | = } { value | DEFAULT }
	ALTER ROLE name [ IN DATABASE database_name ] SET configuration_parameter FROM CURRENT
	ALTER ROLE name [ IN DATABASE database_name ] RESET configuration_parameter
	ALTER ROLE name [ IN DATABASE database_name ] RESET ALL

**Tip**: It is good practice to create a role that has the CREATEDB and CREATEROLE privileges, but is not a superuser, and then use this role for all routine management of databases and roles. This approach avoids the dangers of operating as a superuser for tasks that do not really require it.

### 20.3 - Role Membership
It is frequently convenient to group users together to ease management of privileges: that way, privileges can be granted to, or revoked from, a group as a whole. In PostgreSQL this is done by creating a role that represents the group, and then granting membership in the group role to individual user roles.

# IV - Client interfaces
libpq

# V - Server programming
Trigger, Procedural, etc/

# VI - Internals


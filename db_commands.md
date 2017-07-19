# MySQL DB Commands

## Create testdb: verifying replication

```
$ mysql -u root -p'root'
mysql> show status like 'wsrep%';
```

## Create an admin user

```
mysql> create user 'admin'@'%' identified by 'root';
mysql> grant all privileges on *.* to 'admin'@'%' with grant option;
mysql> flush privileges;
```

## Create a proxysql user

```
mysql> CREATE USER 'proxysqluser'@'%' IDENTIFIED BY 'root';
mysql> GRANT USAGE ON *.* TO 'proxysqluser'@'%';
mysql> FLUSH PRIVILEGES;
```

## Show MySQL Users

We only need the User table
```
mysql -u root -p
mysql> SELECT User, Host, Password FROM mysql.user;
mysql> SELECT User FROM mysql.user;
mysql> SELECT DISTINCT User FROM mysql.user;

## Create a proxysql monitor

```
mysql> CREATE USER 'proxysqlmonitor'@'%' IDENTIFIED BY 'root';
mysql> GRANT USAGE ON *.* TO 'proxysqlmonitor'@'%';
mysql> FLUSH PRIVILEGES;
```


## Create Database

```
mysql> CREATE DATABASE testdb;

mysql> USE testdb;
mysql> CREATE TABLE example (node_id INT PRIMARY KEY, node_name VARCHAR(30));
mysql> INSERT INTO testdb.example VALUES (1, 'sometext');
mysql> SELECT * FROM testdb.example;
```


## Create Table
```
mysql> create table table1 (a int not null auto_increment, primary key(a));

mysql> insert into table1 values (),(),(),(),();

mysql> select * from table1;
```



## Query size of mysql db

```
mysql> SELECT table_schema "systest", Round(Sum(data_length + index_length) / 1024 /1024, 1) "DB Size in MB"
    -> FROM information_schema.tables
    -> GROUP By table_schema;
;
```
## How to Get True Size of MySQL Database?

```
mysql> SHOW TABLE STATUS LIKE 'table_name';
mysql> SHOW TABLE STATUS LIKE 'sbtest1';
```

## Get a table count
	mysql> select count(*) from 'table_name';
	mysql> select count(*) from 'sbtest1;


## How to Back Up MySQL Databases From The Command Line

- Automated backups are important
1. Create a backup
	The mysqldump command is used to create textfile “dumps” of databases managed by MySQL.
	1.1. Single database
	```
		mysqldump database_name > database_name.sql
	```
	1.2. Multiple databases
	```
		mysqldump --databases database_one database_two > two_databases.sql
	```
	1.3. All databases
	```
		mysqldump --all-databases > all_databases.sql
	```

2. Restoring a backup
	database_name.sql: name of the backup file to be restored.
	database_name: name of the database you want to restore
```
mysql database_name < database_name.sql
```

Restore a single database from a dump of all databases
```
mysql --one-database database_name < all_databases.sql
```

3. Restoring Databases From cPanel Backups

4. Additonal

```bash
mysqldump -u [username] -p[password] [dbname] > [dbname].sql
```
## Install Sysbench Debian

	Make sure the system is updated. Then simply install Sysbench, and MySQL Server if you plan on running OLTP tests.

	$ apt-get update
	$ apt-get install -y sysbench
	$ apt-get install -y mysql-server
	$ sysbench --test=fileio --file-total-size=4G --file-num=64 prepare


## Install Sysbench CentOS
	
	- CentOS 7.1
	Install Sysbench 0.4.12 via YUM.
	It's available in the epel repo.

	$ yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
	$ yum install sysbench

	- CentOS 7.3

	Install Sysbench 0.5 via YUM
	You need to install the latest Percona repo to install Sysbench 0.5 if you use EPEL you will install version 0.4.12. Sysbench version 0.5 allows you to do LUA scripting and create multiple tables to run the OLTP test against.

	$ wget https://www.percona.com/redir/downloads/percona-release/redhat/latest/percona-release-0.1-4.noarch.rpm
	$ rpm -Uvh percona-release-0.1-4.noarch.rpm
	$ yum install sysbench

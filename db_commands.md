# MySQL DB Commands

## Create testdb: verifying replication

```
mysql -u root -p'root'
mysql> show status like 'wsrep%';
```

## Create an admin user

```
create user 'admin'@'%' identified by 'root';
grant all privileges on *.* to 'admin'@'%' with grant option;
flush privileges;
```

## Create a proxysql user

```
CREATE USER 'proxysqluser'@'%' IDENTIFIED BY 'root';
GRANT USAGE ON *.* TO 'proxysqluser'@'%';
FLUSH PRIVILEGES;
```

## Create a proxysql monitor

```
CREATE USER 'proxysqlmonitor'@'%' IDENTIFIED BY 'root';
GRANT USAGE ON *.* TO 'proxysqlmonitor'@'%';
FLUSH PRIVILEGES;
```


## Create Database

```
CREATE DATABASE testdb;

USE testdb;
CREATE TABLE example (node_id INT PRIMARY KEY, node_name VARCHAR(30));
INSERT INTO testdb.example VALUES (1, 'sometext');
SELECT * FROM testdb.example;
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

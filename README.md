# Hive-
Commands & concept used in Hive:

First Step : Always set the Hive Metastore to point your cluster, before creating a table

Database:

Create Database:   Command : Create database if not exists d1;
describe database: Command : describe database d1;
describe database with comment : create database if not exists d2 "this is the db"

Table:

Internal Table : Hive Metadata & actual data is stored
External Table : Hive Metadata alsone is maintained by Hive.

Create Table : Create Table if not exists table1(col1 string, col2 array(string), col3 string, col4 int) row format delimited terminated by ',' collection items terminated by ":" lines terminated by '\n' stored as textfile;

Create table with changing the location:  Create Table if not exists table1(col1 string, col2 array(string), col3 string, col4 int) row format delimited terminated by ',' collection items terminated by ":" lines terminated by '\n' stored as textfile location /user/itv000076/warehouse;

Describe tablename - shows the detailed level of table along with column names, structure and everything.

load data : Load data local inpath" pathname" into table table1;
Overwrite: Load data local inpath" pathname" overwrite table table1;


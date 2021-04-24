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

Difference between Internal & External Table: If a internal table is dropped, both Metadata of Hive and hdfs storage will be lost
                                              If an external table is dropped , we cant see in Hive, as it is lost, but the Hdfs storage will be present.

Create Table : Create Table if not exists table1(col1 string, col2 array(string), col3 string, col4 int) row format delimited terminated by ',' collection items terminated by ":" lines terminated by '\n' stored as textfile;

Create table with changing the location:  Create Table if not exists table1(col1 string, col2 array(string), col3 string, col4 int) row format delimited terminated by ',' collection items terminated by ":" lines terminated by '\n' stored as textfile location /user/itv000076/warehouse;

Describe tablename - shows the detailed level of table along with column names, structure and everything.

load data : Load data local inpath" pathname" into table table1;
Overwrite: Load data local inpath" pathname" overwrite table table1;


Insert data from one table to another table:
Insert into table table1 select col1, col2, col3 from table2

Alter table command: Alter table tab add columns( col1 string, col2 string);
                     Alter table change column( col2, col3);
                     Alter table replace columns( col1 string);
                    
 Alter table proprties also can be done.
 
 Sorting the data :
     Sort By : Sort by uses 2 reducers, and sorting is done within each reducer. SO, no full sorting is not done.
     Order By : orders in 1 reducer. SO performance is low
     distribute By: Distribute by distribute the data with no sorting is done. (advantage is avoids overlapping of teh data)
     Cluster by : is the short form of distribute by sort by. So, the data is distributed and sorted within the each reducer. Note: Here also, no complete sort is done.
     
Over all sort is done only by Order BY.

Partitioning:
types of Partitioning - Static & Dynamic Partitioning.

in the create table - add the partition by clause - as like this "Paritioned by"
after create the table - insert the data like below :
Insert data into partititoned table select column 1, column2 from 2nd table name where column name='HR'

For Dynamoc Partitioning, set the property as :
set hive.exec.dynamic.partition=true
set hive.dynamic.partition.mode=non strict

Difference between Static & Dynamic Partitioning: Static- will load the data manually based on column values.
                                                  Dynamic - Will load the data dynamically only based on column name itself.
                          
 Command to show the partitions: show partition tablename;
 
 To drop the partition, use ALter command
 Alter table table name drop partition (deptname='HR')
 
 To refresh the partition - we use msck repair table tablename
 
 Bucketing:
 
 Bucket can be created alone or along with Partition.
 Partition is a directory, while bucket is a file.
 
 Create table table1 ( col names) partitioned by (partition col name) clustered by( columns) into 4 bucket
 Number of reduce tasks will be equal to 4 buckets.
 
 Main key point of bucketing: If the data is unique, then we have to go with buckets without paritioning. Bucket s a file and total number of buckets can be controlled.
 Bucketed map joins are fastes joins.
 
 Difference between limit and tablesampling.
 Tablesampling can pick the data from each bucket.
 
 No_drop & Offline :
 Not to drop the table : alter table tablenaem enable no_drop;
 
 To safegaurd from querying the table : alter table tablename enable offline;
 
 Join :
 TO optimize the memory- choose the last table to be large table
 because in Hive by defautlt - first table will be buffered from memory and always last table will be streamed, so use the last table to be streamed.
 
 We can explicitly pass the stream table as like below :
 Select + STREAMTABLE= emp_tab
 
 Map joins :
 join is performed only on Maps.
 explicitly call in the command:
  Select + MapJOIN(emp_tab)
  
  Properties to be set for doing Bucketed Map Join:
  Bucketmapjoin=true
  sortmerge=true.
  bucketedmapjoin.sortmerge=true
  
  Index:
  create index i1 on table(tablename) as 'COMPACT' with deferred rebuild;
  
  Types of Index: COmpact & Bitmap
  both serve the same purpose - but index storage is different.
  In BitMap - its kind of digital.
  to identify which rows are present in which block
  
  
 
 

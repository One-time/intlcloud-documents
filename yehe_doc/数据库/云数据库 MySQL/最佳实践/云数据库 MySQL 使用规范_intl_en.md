
## Purpose
- To standardize the management and maintenance of TencentDB for MySQL to avoid unavailability and other issues caused by improper operations.
- To provide guidance for database developers on how to write SQL statements to ensure optimal performance of TencentDB for MySQL.

## Privileges Management Specifications
- Note that the SUPER, SHUTDOWN, and FILE privileges are restricted in TencentDB for MySQL to ensure the stability and security. Therefore, the following error may occur when you execute SET statements:  
```
#1227-Access denied;you need(at least one of)the SUPER privilege (s) for this operation
```     
Solution: you can modify parameters on the **Database Management** > **Parameter Settings** tab in the console rather than run SET statements.
- Grant privileges on demand. It is sufficient to grant general applications only the DML privileges (SELECT, UPDATE, INSERT, DELETE).
- Grant privileges to users of general application at the database level.
- Allow authorized users to access TencentDB for MySQL only from specific IPs or IP ranges. This can be achieved by configuring security groups in the console as instructed there. To set a security group for public network access, be sure to allow all the egress IPs involved.
- Use different accounts for management and development.

## Operation Specifications
### Notes
- Do not use weak passwords for enhanced instance security.
- Make sure that the CVM instance of the client and the TencentDB for MySQL instance are in the same region and under the same account when connecting to or logging in to databases over the private network.
- Make sure that the client's MySQL version is the same as that of the TencentDB for MySQL instance when locally parsing the binlogs downloaded from the console; otherwise, garbled characters will be displayed during parsing. It is recommended to use mysqlbinlog v3.4 or higher.
- Enclose the URL with quotation marks when downloading cold backup files to a CVM instance over the private network in the console; otherwise, a 404 error will occur.

### Suggestions
- Avoid performing online DDL operations during peak hours. You can use tools such as`pt-online-schema-change`.
- Avoid performing batch operations during peak hours.
- Avoid running an instance for multiple businesses so as to minimize the risk of mutual interference between businesses due to high coupling.
- Disable automatic transaction committing and develop a habit of using `begin;` for online operations, which can help minimize the risk of data loss caused by faulty operations. In case of a faulty operation, you can use the rollback feature of TencentDB for MySQL for data restoration (rollback to any point in time in the last 5 days is supported). For tables without cross-database and cross-table logic, you can use quick or instant rollback for even faster data restoration. The new table after rollback is named `original table name_bak`.
- Make an estimate of the resources required in advance and optimize the instances for promotional campaigns of your business. In case of a great demand for resources, contact your Tencent Cloud sales rep in a timely manner.


## Database and Table Design Specifications
### Notes
- Do not use MyISAM or MEMORY in MySQL v5.6 or higher as they are no longer supported. If MEMORY is required, you can use TencentDB for Redis or Memcached. If MyISAM databases are migrated to TencentDB for MySQL, MyISAM will be converted to InnoDB automatically.
- Create at least one index on the auto-increment column or create a composite index whose first column is the auto-increment column.
- Make sure that `row_format` is non-fixed.
- Make sure that each table has a primary key. Even if no column is suitable for use as the primary key, you still have to add a meaningless column as the primary key. According to MySQL 1NF, primary key values are saved on the standard InnoDB secondary index's leaf nodes. It is recommended to use a short auto-increment column as the primary key so as to reduce the disk capacity occupied by indexes and improve the efficiency. If `binlog_format` is row, deleting data in batches without the primary key can cause serious source-replica delay.
- Define fields as NOT NULL and set default values. NULL fields will cause unavailability of indexes, thus bringing problems to SQL development. NULL calculation can only be implemented based on IS NULL and IS NOT NULL.

### Suggestions
- Plan the resources used by databases reasonably based on business scenario analysis and estimation of data access (including database read/write QPS, TPS, and storage). You can also configure various Cloud Monitor metrics for TencentDB for MySQL in the console.
- Put the tables for the same type of businesses into one database when building databases and try not to mix and match. Do not perform cross-database correlation operations in programs, as doing so will affect subsequent quick rollbacks.
- Always use the utf8mb4 character set to minimize the risk of garbled characters. Some complex Chinese characters and emoji stickers can be displayed normally only in utf8mb4. If the character set is changed, the new character set will take effect only on tables created after the change. Therefore, it is recommended to select utf8mb4 as early as in the initialization of a new TencentDB for MySQL instance.
- Use the DECIMAL type to store decimal values. The FLOAT and DOUBLE types have insufficient precision, especially for businesses involving money where the DECIMAL type must be used.
- Do not use the TEXT or BLOB type to store a large quantity of text, binary data, images, files, and other contents in a database; instead, save such data as local disk files and only store their index information in the database.
- Avoid using foreign keys. It is recommended to implement the foreign key logic at the application layer. Foreign key and cascade update are not suitable for high-concurrence scenarios, because they may reduce the insertion performance and lead to deadlock in case of high concurrence.
- Reduce the coupling of business logic and data storage; use databases mainly for storing data and implement business logic at the application layer as much as possible; minimize the use of stored procedures, triggers, functions, events, views, and other advanced features due to their poor portability and scalability. If such objects exist in an instance, it is not recommended to set definer by default so as to avoid migration failures caused by inconsistency between migration account and definer.
- Do not use partitioned tables if you won't have a substantial business volume in the near future, because they are mainly used for archive management in the courier and ecommerce industries. Do not rely on partitioned tables for performance enhancement, unless over 80% of queries in your business involve the partitioning key.
- Purchase read-only instances to implement read/write separation at the database level for business scenarios with a high read load and low requirement for consistency (data delay within seconds is acceptable).

## Index Design Specifications
### Notes
- Do not create indexes on the columns that are updated frequently and have a lower selectivity. Record updates will change the B+ tree, so creating indexes on frequently updated fields may greatly reduce the database performance.
- Put the column with the highest selectivity on the far left when creating a composite index; for example, in `select xxx where a = x and b = x;`, if a and b are used together to create a composite index and a has a higher selectivity, then the composite index should be created as `idx_ab(a,b)`. If None-Equal To and Equal To conditions are used at the same time, the column with the Equal To condition must be put first; for example, in `where a xxx and b = xxx`, b must be placed on the far left even if a has a higher selectivity, because a will not be used in the query.

### Suggestions
- Use no more than 5 indexes in a single table and no more than 5 fields in a single index. Too many indexes may affect the filtering, occupy much more capacity, and consume more resources for management.
- Create indexes on the columns that are used for SQL filtering most frequently with a high cardinality value. It is meaningless to create indexes on a column not involved in SQL filtering. The higher the uniqueness of a field, the higher the cardinality value, and the better the index filtering result. Generally, an index column with a cardinality below 10% is considered an inefficient index, such as the gender field.
- Specify the index length when creating an index on the VARCHAR field. Do not index the entire column, because the VARCHAR column is often long, indexing the entire column will increase the maintenance costs, and specifying the index length can provide sufficient selectivity. You can use `count(distinct left(column name, index length))/count(\*)` to check index selectivity.
- Avoid using redundant indexes. If both index (a,b) and index (a) exist, (a) is considered a redundant index. If the query filtering is based on column a, the index (a,b) is sufficient.
- Use covering indexes reasonably to reduce IO overhead. In InnoDB, leaf nodes of a secondary index only save the values of their own keys and the primary key. If an SQL statement does not query such an index column or primary key, the query on the index will locate the corresponding primary key first and then locate the desired column based on the primary key. This is TABLE ACCESS BY INDEX ROWID, which will incur extra IO overhead. Covering indexes can be used to solve this problem; for example, in `select a,b from xxx where a = xxx`, if a is not the primary key, a composite index can be created on a and b columns to prevent the problem.

## SQL Statement Writing Specifications
### Notes
- Do not use LIMIT for UPDATE and DELETE operations, because LIMIT is random and may cause data errors; instead, you must use WHERE for such operations for exact match.
- Do not use `INSERT INTO t_xxx VALUES(xxx)`, and the column attributes to be inserted must be specified explicitly to prevent data errors caused by changes in the table structure.
- Pay attention to the following common reasons for invalid indexes in SQL statements:
 - Implicit type conversion; for example, if the type of index a is VARCHAR and the SQL statement is `where a = 1`, then VARCHAR is changed to INT.
 - Math calculations and functions are performed on the index columns; for example, date column is formatted using a function.
 - Columns on which a join operation is performed have different character sets.
 - Multiple columns have different sorting orders; for example, the index is (a,b), but the SQL statement is `order by a b desclike`.
 - When fuzzy queries are performed, some indexes can be queried for characters in the format of `xxx%`; however, in other cases, indexes will not be used.
 - NOT, !=, NOT IN, etc. are used in queries.
 
### Suggestions
- Ensure query on demand and reject `select *` to avoid the following problems:       
    - The covering index does not work and the problem of TABLE ACCESS BY INDEX ROWID occurs, which leads to extra IO overhead.      
    - Additional memory load; a large amount of cold data is imported to `innodb_buffer_pool_size` which may reduce the query hit rate.      
    - Additional overhead in network transfer.
- Avoid using large transactions. It is recommended to split a large transaction into multiple small ones to avoid source-replica delay.
- Commit transactions in the business code in a timely manner to avoid unnecessary lock waits.
- Minimize the use of join operations for multiple tables and do not perform join operations on big tables. When a join operation is performed on two tables, the smaller one must be used as the driving table, the columns to be joined must have the same character set, and all of them must have been indexed.
- Use LIMIT for paging optimization. The operation "LIMIT 80000, 10" is to filter out 80,010 records and then return the last 10 ones. This may cause a high load on the database. It is recommended to locate the first record before paging, such as `SELECT * FROM test WHERE id >= ( SELECT sql_no_cache id FROM test order by id LIMIT 80000,1 ) LIMIT 10 ;`.
- Avoid using an SQL statement with multi-level nested subqueries. The query optimizer prior to MySQL v5.5 can convert IN to EXISTS and does not go through the indexes. In this case, a large external table may result in poor performance.

>?
>- It is difficult to totally avoid the above problems. The solution is not to use the aforementioned conditions as the primary filtering conditions; instead, set them as the conditions secondary to the primary filtering conditions for indexes.
>- If a large number of full table scans are monitored, set the `log_queries_not_using_indexes` parameter in the console and download the slow logs for analysis later. Do not keep it enabled for too long so as to avoid a surge of slow logs.
>- Perform the required SQL audit before a business goes live. In daily OPS work, download slow logs regularly for targeted optimization.

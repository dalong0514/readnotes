12Advanced MySQL Administration

In this chapter, we cover some more advanced MySQL topics, including advanced privileges, security, and optimization.

Key topics covered in this chapter include

 ■ Understanding the privilege system in detail

 ■ Making your MySQL database secure

 ■ Getting more information about databases

 ■ Speeding things up with indexes

 ■ Optimizing your database

 ■ Backing up and recovering

 ■ Implementing replication

Understanding the Privilege System in DetailChapter 9,「Creating Your Web Database,」described the process of setting up users and granting them privileges. You saw how to do this with the GRANT command. If you’re going to administer a MySQL database, understanding exactly what GRANT does and how it works can be useful.

When you issue a GRANT statement, it affects tables in the special database called mysql. Privilege information is stored in seven tables in this database. Given this fact, when granting privileges on databases, you should be cautious about granting access to the mysql database.

You can look at what’s in the mysql database by logging in as an administrator and typing

USE mysql;

If you do this, you can then view the tables in this database as usual by typing

292

Chapter 12  Advanced MySQL Administration

SHOW TABLES;

Your results look something like this:

+-------------------------------+| Tables_in_mysql               |+-------------------------------+| columns_priv                  || db                            || event                         || func                          || general_log                   || help_category                 || help_keyword                  || help_relation                 || help_topic                    || host                          || innodb_index_stats            || innodb_table_stats            || ndb_binlog_index              || plugin                        || proc                          || procs_priv                    || proxies_priv                  || rds_configuration             || rds_global_status_history     || rds_global_status_history_old || rds_heartbeat2                || rds_history                   || rds_replication_status        || rds_sysinfo                   || servers                       || slave_master_info             || slave_relay_log_info          || slave_worker_info             || slow_log                      || tables_priv                   || time_zone                     || time_zone_leap_second         || time_zone_name                || time_zone_transition          || time_zone_transition_type     || user                          |+-------------------------------+36 rows in set (0.00 sec)

Each of these tables stores system information. Seven of them—user, host, db, tables_priv, columns_priv, proxies_priv, and procs_priv—store privilege information. They are 

Understanding the Privilege System in Detail

293

sometimes called grant tables. These tables vary in their specific function but all serve the same general function, which is to determine what users are and are not allowed to do. Each of them contains several types of fields. There are scope fields, which identify the user, host, and part of a database that the privilege refers to; and privilege fields, which identify which actions can be performed by that user in that scope. There are also security fields, which contain security-related information, and resource control columns, which constrain the number of resources that may be consumed.

The user table is used to decide whether a user can connect to the MySQL server at all and whether he or she has any administrator privileges. The host table was formerly used and is now obsolete, but it is still present in the mysql database. The db table determines which data-bases the user can access. The tables_priv table determines which tables within a database a user can use, the columns_priv table determines which columns within tables she has access to, the proxies_priv table determines which users can act as proxies or grant proxy privileges to others, and the procs_priv table determines which routines a user can execute.

The user TableThe user table contains details of global user privileges. It determines whether a user is allowed to connect to the MySQL server at all and whether she has any global-level privileges—that is, privileges that apply to every database in the system.

You can see the structure of this table by issuing a DESCRIBE user; statement. The schema for the user table is shown in Table 12.1.

Table 12.1  Schema of the user Table in the mysql DatabaseField

Type

Host

User

Password

Select_priv

Insert_priv

Update_priv

Delete_priv

Create_priv

Drop_priv

Reload_priv

Shutdown_priv

Process_priv

char(60)

char(16)

char(41)

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

294

Chapter 12  Advanced MySQL Administration

Field

File_priv

Grant_priv

References_priv

Index_priv

Alter_priv

Show_db_priv

Super_priv

Create_tmp_table_priv

Lock_tables_priv

Execute_priv

Repl_slave_priv

Repl_client_priv

Create_view_priv

Show_view_priv

Create_routine_priv

Alter_routine_priv

Create_user_priv

Event_priv

Trigger_priv

Create_tablespace_priv

ssl_type

ssl_cipher

x509_issuer

x509_subject

max_questions

max_updates

max_connections

max_user_connections

plugin

authentication_string

password_expired

Type

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y') 

enum('N','Y') 

enum('N','Y') 

enum('N','Y') 

enum('N','Y') 

enum('N','Y') 

enum('N','Y')

enum('N','Y')

enum('','ANY','X509','SPECIFIED')

blob

blob

blob 

int(11) unsigned

int(11) unsigned

int(11) unsigned

int(11) unsigned

char(64)

text

enum('N','Y')

Understanding the Privilege System in Detail

295

Most rows in this table correspond to a set of privileges for a User coming from a Host and logging in with the password. These are the scope fields for this table because they describe the scope of the privilege fields. The privilege fields end with _priv.

The privileges listed in this table (and the others to follow) correspond to the privileges granted using GRANT in Chapter 9. For example, Select_priv corresponds to the privilege to run a SELECT command.

If a user has a particular privilege, the value in that column will be Y. Conversely, if a user has not been granted that privilege, the value will be N.

All the privileges listed in the user table are global; that is, they apply to all the databases in the system (including the mysql database). Administrators will therefore have some Ys in there, but the majority of users should have all Ns. Normal users should have rights to appropriate  databases, not all tables.

The two other sets of fields in this table are the security fields and the resource control fields.

The security fields are ssl_type, ssl_cipher, x509_issuer, x509_subject, plugin,  authentication_string, and password_expired. The plugin field is NULL by default but may be set to contain an authentication plugin that will be used to authenticate a particular user account. The authentication_string may be used by plugins. The ssl_type and ssl_cipher fields are used if you have enabled SSL connections. 

The db TableMost of your average users’ privileges are stored in the db table.

The db table determines which users can access which databases from which hosts. The privileges listed in this table apply to whichever database is named in a particular row.

The schema of this table is shown in Table 12.2.

Table 12.2  Schema of the db Table in the mysql DatabaseField

Type

Host

Db

User

Select_priv

Insert_priv

Update_priv

Delete_priv

Create_priv

char(60)

char(64)

char(16)

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

296

Chapter 12  Advanced MySQL Administration

Field

Drop_priv

Grant_priv

References_priv

Index_priv

Alter_priv

Create_tmp_tables_priv

Lock_tables_priv

Create_view_priv

Show_view_priv

Create_routine_priv

Alter_routine_priv

Execute_priv

Event_priv

Trigger_priv

Type

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N’,'Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

enum('N','Y')

The tables_priv, columns_priv, and procs priv TablesThe tables_priv, columns_priv, procs_priv, and proxies_priv tables are used to store table-level privileges, column-level privileges, privileges regarding stored routines, and  proxy-related privileges, respectively. 

These tables have a slightly different structure than the user and db tables. The schemas for the tables_priv table, columns_priv table, procs_priv table, and proxies_priv table are shown in Tables 12.3, 12.4, 12.5, and 12.6, respectively.

Table 12.3  Schema of the tables_priv Table in the mysql DatabaseField

Type

Host

Db

User

Table_name

Grantor

Timestamp

char(60)

char(64)

char(16)

char(64)

char(77)

timestamp

Understanding the Privilege System in Detail

297

Table_priv

 set('Select', 'Insert', 'Update', 'Delete', 'Create', 'Drop', 

'Grant', 'References', 'Index', 'Alter', 'Create View', 'Show view',

'Trigger'))

Column_priv

set ('Select', 'Insert', 'Update', 'References')

Table 12.4  Schema of the columns_priv Table in the mysql Database

Field

Host

Db

User

Table_name

Column_name

Timestamp

Column_priv

Type

char(60)

char(64)

char(16)

char(64)

char(64)

timestamp

set('Select', 'Insert', 'Update', 'References')

Table 12.5  Schema of the procs_priv Table in the mysql Database

Field

Host

Db

User

Routine_name

Routine_type

Grantor

Proc_priv

Timestamp

Type

char(60)

char(64)

char(16)

char(64)

enum('FUNCTION', 'PROCEDURE')

char(77) 

set('Execute','Alter Routine','Grant')

timestamp

298

Chapter 12  Advanced MySQL Administration

Table 12.6  Schema of the proxies_priv Table in the mysql Database

Field

Host

User

Proxied_host

Proxied_user

With_grant

Grantor

Timestamp

Type

char(60)

char(16)

char(60)

char(16)

tinyint(1)

char(77) 

timestamp

The Grantor column in the tables_priv and procs_priv tables stores the name of the user who granted this privilege to this user. The Timestamp column in each of these tables stores the date and time when the privilege was granted. In the proxies_priv table, these columns are currently unused.

Access Control: How MySQL Uses the Grant TablesMySQL uses the grant tables to determine what a user is allowed to do in a two-stage process:

1.  Connection verification. Here, MySQL checks whether you are allowed to connect at all, 

based on information from the user table, as shown previously. This authentication is based on username, hostname, and password. If a username is blank, it matches all users. Hostnames can be specified with a wildcard character (%). This character can be used as the entire field (that is, % matches all hosts) or as part of a hostname (for example, %.example.com matches all hosts ending in .example.com). If the password field is blank, no password is required. Your system is more secure if you avoid having blank users, wildcards in hosts, and users without passwords. If the hostname is blank, it is effectively a wildcard, but with lower precedence than the % wildcard.

2.  Request verification. Each time you enter a request, after you have established a 

connection, MySQL checks whether you have the appropriate level of privileges to perform that request. The system begins by checking your global privileges (in the user table) and, if they are not sufficient, checks the db table. If you still don’t have sufficient privileges, MySQL will check the tables_priv table, and, if this is not enough, finally it will check the columns_priv table. If the operation uses stored routines, MySQL checks the procs_priv table instead of the tables_priv and columns_priv tables. If you are trying to proxy another user, or grant proxy privileges to a user, MySQL checks the proxies_priv table. 

Making Your MySQL Database Secure

299

Updating Privileges: When Do Changes Take Effect?The MySQL server automatically reads the grant tables when it is started and when you issue GRANT and REVOKE statements. However, now that you know where and how those privileges are stored, you can alter them manually. When you update them manually, the MySQL server will not notice that they have changed.

You need to point out to the server that a change has occurred, and you can do this in three ways. You can type

mysql> flush privileges;

at the MySQL prompt. (You need to be logged in as an administrator to use this command.) This is the most commonly used way of updating the privileges.

Alternatively, you can run either

> mysqladmin flush-privileges

or

> mysqladmin reload

from your operating system.

Finally, the MySQL server will reload the grant tables when it is restarted.

After this, global-level privileges will be checked the next time a user connects; database privileges will be checked when the next use statement is issued; and table- and column-level privileges will be checked on a user’s next request.

Making Your MySQL Database SecureSecurity is important, especially when you begin connecting your MySQL database to your website. The following sections explain a basic set of precautions you ought to take to protect your database. 

MySQL from the Operating System’s Point of ViewRunning the MySQL server (mysqld) as root is a bad idea if you are running a Unix-like  operating system. Doing this gives a MySQL user with a full set of privileges the right to read and write files anywhere in the operating system. This is an important point, easily overlooked, which was famously used to hack Apache’s website. (Fortunately, the crackers were「white hats」[good guys], and their only action was to tighten up security.)

Setting up a MySQL user specifically for the purpose of running mysqld is a good idea. In  addition, you can then make the directories (where the physical data is stored) accessible only by the MySQL user. In many installations, the server is set up to run as userid mysql, in the mysql group.

300

Chapter 12  Advanced MySQL Administration

You should also set up your MySQL server on an internal network, or behind your firewall. This way, you can prevent connections from unauthorized machines. Check to see whether you can connect from outside to your server on port number 3306. This is the default port MySQL runs on and should be closed on your firewall.

PasswordsMake sure that all your users have passwords (especially root!) and that they are well chosen and regularly changed, as with operating system passwords. One rule of thumb to remember here is that passwords that are or contain words from a dictionary are a bad idea. Combinations of letters, numbers, and symbols are best.

If you are going to store passwords in script files, make sure only the user whose password is stored can see that script. This is generally only relevant in shared hosting environments, which are less common these days. 

PHP scripts that are used to connect to the database need access to the password for that user. This can be done reasonably securely by putting the login and password in a file called, for example, dbconnect.php, that you then include when needed. This script can be carefully stored outside the web document tree and made accessible only to the appropriate user.

Remember that if you put these details in a file with .inc or some other extension in the web tree, you must be careful to check that your web server knows these files must be interpreted as PHP so that the details will not be viewed in plain text via a web browser. It’s better to avoid this situation altogether.

Don’t store passwords in plain text in your database. MySQL passwords are not stored that way, but commonly in web applications, you additionally want to store website members’ login names and passwords. You can encrypt passwords (one way) using MySQL’s password()  function. Remember that if you insert a password in this format when you run SELECT (to log in a user), you will need to use the same function again to check the password a user has typed.

You will use this functionality when you implement the projects in Part V,「Building Practical PHP and MySQL Projects.」

User PrivilegesKnowledge is power. Make sure that you understand MySQL’s privilege system and the conse-quences of granting particular privileges. Don’t grant more privileges to any user than she needs. You should check them by looking at the grant tables.

As a starting point, don't give access to the mysql database to any non-administrative user.

Don’t grant the PROCESS, FILE, SUPER, SHUTDOWN, and RELOAD privileges to any user other than an administrator unless absolutely necessary, and if you must, try to grant it only for the minimum time necessary. The PROCESS privilege can be used to see what other users are doing and typing, including their passwords. The FILE privilege can be used to read and write files to and from the operating system (including, say, /etc/password on a Unix system). The SUPER 

Getting More Information About Databases

301

privilege can be used to terminate other connections, modify system variables, and control replication. The RELOAD privilege is used to reload grant tables.

The GRANT privilege should also be granted with caution because it allows users to share their privileges with others.

Finally, and perhaps non-obviously, grant the ALTER option with caution. Users may use it to rename a table and hence subvert the privilege system.

Make sure that when you set up users, you grant them access only from the hosts that they will be connecting from. Avoid using wildcards in hostnames for similar reasons.

You can further increase security by using IPs rather than domain names in your host table. This way, you can avoid problems with compromised DNS. You can enforce this by starting the MySQL daemon (mysqld) with the --skip-name-resolve option, which means that all host column values must be either IP addresses or localhost.

You should also prevent non-administrative users from having access to the mysqladmin program on your web server. Because this program runs from the command line, access to it is an issue of operating system privilege.

Web IssuesConnecting your MySQL database to the web raises some special security issues.

It is a good idea to start by setting up a special user just for the purpose of web connections from a particular web application. This way, you can give the user the minimum privilege necessary and not grant, for example, DROP, ALTER, or CREATE privileges to that user. You might grant SELECT only on catalog tables and INSERT only on order tables. Again, this is an illus-tration of how to use the principle of least privilege.

You should always check all data coming in from a user. Even if your HTML form consists of select boxes and radio buttons, someone might alter the URL to try to crack your script. Checking the size of the incoming data is also worthwhile.

If users are typing in passwords or confidential data to be stored in your database, remember that it will be transmitted from the browser to the server in plain text unless you use Secure Sockets Layer (SSL). We discuss using SSL in more detail later in this book.

Getting More Information About DatabasesSo far, we’ve used SHOW and DESCRIBE to find out what tables are in the database and what columns are in them. In the following sections, we briefly look at other ways they can be used and at the use of the EXPLAIN statement to get more information about how a SELECT  operation is performed.

302

Chapter 12  Advanced MySQL Administration

Getting Information with SHOWPreviously, you used

mysql> SHOW TABLES;

to get a list of tables in the database.

The statement

mysql> SHOW DATABASES;

displays a list of available databases. You can then use the SHOW TABLES statement to see a list of tables in one of those databases:

mysql> SHOW TABLES FROM books;

When you use SHOW TABLES without specifying a database, it defaults to the one in use.

When you know what the tables are, you can get a list of the columns:

mysql> SHOW COLUMNS FROM Orders FROM books;

If you leave off the database name, the SHOW COLUMNS statement will default to the database currently in use. You can also use the table.column notation:

mysql> SHOW COLUMNS FROM books.Orders;

One other useful variation of the SHOW statement can be used to see what privileges a user has. For example, if you run

mysql> SHOW GRANTS FOR 'bookorama';you get the following output:

+--------------------------------------------------------------------------------+| Grants for bookorama@%                                                         |+--------------------------------------------------------------------------------+| GRANT USAGE ON *.* TO 'bookorama'@'%' IDENTIFIED BY PASSWORD '*1ECE648641438A28E1910D0D7403C5EE9E8B0A85' || GRANT SELECT, INSERT, UPDATE, DELETE ON `books`.* TO 'bookorama'@'%'   |+--------------------------------------------------------------------------------+2 rows in set (0.00 sec)

The GRANT statements shown are not necessarily the ones that were executed to give privileges to a particular user, but rather summary equivalent statements that would produce the user’s current level of privilege.

Many other variations of the SHOW statement can be used as well. In fact, there are over 30 vari-ations of the SHOW statement. Some of the more popular variations are shown in Table 12.7. For a complete list, see the MySQL Manual entry at http://dev.mysql.com/doc/refman/5.6/en/show.html. In all instances of [like_or_where] in the examples below, you can attempt to match a pattern using LIKE or an expression using WHERE.

Getting More Information About Databases

303

Table 12.7  SHOW Statement Syntax

Variation

Description

SHOW DATABASES [like_or_where]

Lists available databases.

SHOW TABLES [FROM database] [like_or_where]

Lists tables from the database currently in use, or from the database called database.

SHOW [FULL] COLUMNS FROM table [FROM  database] [like_or_where] 

SHOW INDEX FROM table [FROM database]

SHOW [GLOBAL | SESSION] STATUS [like_or_where]

SHOW [GLOBAL|SESSION] VARIABLES [like_or_where]

SHOW [FULL] PROCESSLIST

SHOW TABLE STATUS [FROM database] [like_or_where]

SHOW GRANTS FOR user 

SHOW PRIVILEGES

SHOW CREATE DATABASE

Lists all the columns in a particular table from the  database currently in use, or from the database  specified.

SHOW FIELDS is an alias for SHOW COLUMNS.

Shows details of all the indexes on a particular table from the database currently in use, or from the  database called database if specified. SHOW KEYS is an alias for SHOW INDEX.

Gives information about a number of system items, such as the number of threads running. The LIKE clause is used to match against the names of these items, so, for example, 'Thread%' matches the items 'Threads_cached',  'Threads_connected', 'Threads  created', and 'Threads running'.

Displays the names and values of the MySQL system variables, such as the version number.

Displays all the running processes in the system—that is, the queries that are currently being executed. Most users will see their own threads, but if they have the PROCESS privilege, they can see everybody’s  processes—including passwords if they are in queries. The queries are truncated to 100  characters by default. Using the optional keyword FULL displays the full  queries.

Displays information about each of the tables in the database currently being used, or the database called database if it is specified, optionally with a wildcard match. This information includes the table type and the time each table was last updated.

Shows the GRANT statements required to give the user specified in user his current level of privilege.

Shows the different privileges that the server sup-ports.

Shows a CREATE DATABASE statement that would  create the specified database.

304

Chapter 12  Advanced MySQL Administration

Variation

Description

SHOW CREATE TABLE tablename

SHOW [STORAGE] ENGINES

SHOW ENGINE

Shows a CREATE TABLE statement that would cre-ate the specified table.

Shows the storage engines that are available in this installation and which is the default. (We discuss  storage engines further in Chapter 13,「Advanced MySQL Programming.」)

There are a few variations, but most commonly used as SHOW ENGINE INNODB STATUS (formerly SHOW INNODB STATUS) which reports on the current state of the InnoDB engine.

SHOW WARNINGS [LIMIT [offset,] row_count]

Shows any errors, warnings, or notices generated by the last statement that was executed.

SHOW ERRORS [LIMIT [offset,] row_count]

Shows only the errors generated by the last state-ment that was executed.

Getting Information About Columns with DESCRIBEAs an alternative to the SHOW COLUMNS statement, you can use the DESCRIBE statement, which is similar to the DESCRIBE statement in Oracle (another RDBMS). The basic syntax for it is

DESCRIBE table [column];

This command gives information about all the columns in the table or a specific column if column is specified. You can use wildcards in the column name if you like.

Understanding How Queries Work with EXPLAINThe EXPLAIN statement can be used in two ways. First, you can use

EXPLAIN table;

This command gives similar output to DESCRIBE table or SHOW COLUMNS FROM table.

The second and more interesting way you can use EXPLAIN allows you to see exactly how MySQL evaluates a SELECT query. To use it this way, just put the word EXPLAIN in front of a SELECT statement.

You can use the EXPLAIN statement when you are trying to get a complex query to work and clearly haven’t got it quite right, or when a query is taking a lot longer to process than it should. If you are writing a complex query, you can check this in advance by running the EXPLAIN command before you actually run the query. With the output from this statement, you can rework your SQL to optimize it if necessary. It’s also a handy learning tool.

For example, try running the following query on the Book-O-Rama database:

Getting More Information About Databases

305

EXPLAINSELECT Customers.NameFROM Customers, Orders, Order_Items, BooksWHERE Customers.CustomerID = Orders.CustomerIDAND Orders.OrderID = Order_Items.OrderIDAND Order_Items.ISBN = Books.ISBNAND Books.Title LIKE '%Java%';

This query produces the following output. (Note that we are displaying this output vertically because the table rows are too wide to fit in this book. You can get this format by ending your query with \G instead of the semicolon.)

*************************** 1. row ***************************           id: 1  select_type: SIMPLE        table: Customers         type: ALLpossible_keys: PRIMARY          key: NULL      key_len: NULL          ref: NULL         rows: 4        Extra: NULL*************************** 2. row ***************************           id: 1  select_type: SIMPLE        table: Orders         type: refpossible_keys: PRIMARY,CustomerID          key: CustomerID      key_len: 4          ref: books.Customers.CustomerID         rows: 1        Extra: Using index*************************** 3. row ***************************           id: 1  select_type: SIMPLE        table: Order_Items         type: refpossible_keys: PRIMARY,ISBN          key: PRIMARY      key_len: 4          ref: books.Orders.OrderID         rows: 1        Extra: Using index*************************** 4. row ***************************           id: 1  select_type: SIMPLE

306

Chapter 12  Advanced MySQL Administration

        table: Books         type: ALLpossible_keys: PRIMARY          key: NULL      key_len: NULL          ref: NULL         rows: 4        Extra: Using where; Using join buffer (Block Nested Loop)4 rows in set (0.00 sec)

This output might look confusing at first, but it can be very useful. Let’s look at the columns in this table one by one.

The first column, id, gives the ID number of the SELECT statement within the query that this row refers to.

The column select_type explains the type of query being used. The set of values this column can have is shown in Table 12.8. 

Table 12.8  Possible Select Types as Shown in Output from EXPLAIN

Type

SIMPLE

PRIMARY

UNION

Description

Plain old SELECT, as in this example

Outer (first) query where subqueries and unions are used

Second or later query in a union

DEPENDENT UNION

Second or later query in a union, dependent on the primary query

UNION RESULT

The result of a UNION

SUBQUERY

Inner subquery

DEPENDENT SUBQUERY

Inner subquery, dependent on the primary query (that is, a correlated subquery)

DERIVED

Subquery used in FROM clause

MATERIALIZED

Materialized subquery

UNCACHEABLE SUBQUERY

A subquery whose result cannot be cached and must be reevaluated for each row

UNCACHEABLE UNION

The second or later select in a UNION that belongs to an  uncacheable subquery

The column table just lists the tables used to answer the query. Each row in the result gives more information about how that particular table is used in this query. In this case, you can see that the tables used are Orders, Order_Items, Customers, and Books. (You know this already by looking at the query.)

Getting More Information About Databases

307

The type column explains how the table is being used in joins in the query. The set of values this column can have is shown in Table 12.9. These values are listed in order from fastest to slowest in terms of query execution. The table gives you an idea of how many rows need to be read from each table to execute a query. 

Table 12.9  Possible Join Types as Shown in Output from EXPLAIN

Type

Description

const or system

eq_ref

fulltext

ref

The table is read from only once. This happens when the table has exactly one row. The type system is used when it is a system table, and the type const otherwise.

For every set of rows from the other tables in the join, you read one row from this table. This type is used when the join uses all the parts of the index on the table, and the index is UNIQUE or is the primary key.

A join has been performed using a fulltext index.

For every set of rows from the other tables in the join, you read a set of table rows that all match. This type is used when the join cannot choose a single row based on the join condition—that is, when only part of the key is used in the join, or if it is not UNIQUE or a primary key.

ref_or_null

This is like a ref query, but MySQL also looks for rows that are NULL. (This type is used mostly in subqueries.)

index_merge

A specific optimization, the Index Merge, has been used.

unique_subquery

This join type is used to replace ref for some IN subqueries where one unique row is returned.

index_subquery

This join type is similar to unique_subquery but is used for indexed nonunique subqueries.

range

index

ALL

For every set of rows from the other tables in the join, you read a set of table rows that fall into a particular range.

The entire index is scanned.

Every row in the table is scanned.

In the previous example, you can see that one of the tables is joined using eq_ref (Books), one is joined using ref (Order_Items), one is joined using index (Orders), and one (Customers) is joined using ALL—that is, by looking at every single row in the table. 

The rows column backs this up: It lists (roughly) the number of rows of each table that has to be scanned to perform the join. You can multiply these numbers together to get the total number of rows examined when a query is performed. You multiply these numbers because a join is like a product of rows in different tables. Check out Chapter 10,「Working with Your MySQL Database,」for details. Remember that this is the number of rows examined, not the number of rows returned, and that it is only an estimate; MySQL can’t know the exact number without performing the query.

308

Chapter 12  Advanced MySQL Administration

Obviously, the smaller you can make this number, the better. At present, you have a negligible amount of data in the database, but when the database starts to increase in size, this query would increase in execution time. We return to this matter shortly.

The possible_keys column lists, as you might expect, the keys that MySQL might use to join the table. 

The key column is either the key from the table MySQL actually used or NULL if no key was used. 

The key_len column indicates the length of the key used. You can use this number to tell whether only part of a key was used. The key length is relevant when you have keys that consist of more than one column. 

The ref column shows the columns used with the key to select rows from the table.

Finally, the Extra column tells you any other information about the way the join was performed. Some possible values you might see in this column are shown in Table 12.10. For a complete list of the more than 30 different possibilities, see the MySQL Manual at http://dev.mysql.com/doc/refman/5.6/en/explain-output.html#explain-extra-information.

Table 12.10  Some Possible Values for Extra Column as Shown in Output from EXPLAIN

Value

Distinct

Meaning

After the first matching row is found, MySQL stops trying to find rows.

Not exists

The query has been optimized to use LEFT JOIN.

Range checked for each record

For each row in the set of rows from the other tables in the join, MySQL tries to find the best index to use, if any.

Using filesort

Using index

Using join buffer

Using temporary

Using where

Two passes are required to sort the data. (This operation obviously takes twice as long.) 

All information from the table comes from the index; that is, the rows are not actually looked up.

Tables are read in portions, using the join buffer; then the rows are extracted from the buffer to complete the query.

A temporary table needs to be created to execute this query.

A WHERE clause is being used to select rows.

You can fix problems you spot in the output from EXPLAIN in several ways. First, you can check column types and make sure they are the same. This applies particularly to column widths. Indexes can’t be used to match columns if they have different widths. You can fix this problem by changing the types of columns to match or by building this in to your design from the start.

Optimizing Your Database

309

Second, you can tell the join optimizer to examine key distributions and therefore optimize joins more efficiently using an ANALYZE TABLE statement within the MySQL monitor:

ANALYZE TABLE Customers, Orders, Order_Items, Books;

Third, you might want to consider adding a new index to the table. If this query is a) slow and b) common, you should seriously consider this fix. If it’s a one-off query that you’ll never use again, such as an obscure report requested once, this technique may not be worth the effort because it may slow down other things. 

If the possible_keys column from an EXPLAIN contains some NULL values, you might be able to improve the performance of your query by adding an index to the table in question. If the column you are using in your WHERE clause is suitable for indexing, you can create a new index for it using ALTER TABLE like this:

ALTER TABLE ADD INDEX (column);

Finally, there are a couple of things to look out for in the Extra column. If you see Using temporary, it often means that you have different columns in your GROUP BY and ORDER BY columns. If you can restructure your query to avoid that it will help. If you see Using file-sort, it means that MySQL is making two passes: one to retrieve data, and the other to order the data (typically for an ORDER BY clause). In this case, consult the excellent (and long) article in the MySQL manual on how to optimize ORDER BY queries: http://dev.mysql.com/doc/refman/5.6/en/order-by-optimization.html.

Optimizing Your DatabaseIn addition to using the previous query optimization tips, you can do quite a few things to generally increase the performance of your MySQL database. 

Design OptimizationBasically, you want everything in your database to be as small as possible. You can achieve this result, in part, with a decent design that minimizes redundancy. You can also achieve it by using the smallest possible data type for columns. You should also minimize NULLs wherever possible and make your primary key as short as possible.

Avoid variable length columns if at all possible with MyISAM tables (such as VARCHAR, TEXT, and BLOB). If your tables have fixed-length fields, they will be faster to use but might take up a little more space. 

PermissionsIn addition to using the suggestions mentioned in the previous section on EXPLAIN, you can improve the speed of queries by simplifying your permissions. Earlier, we discussed the way that queries are checked with the permission system before being executed. The simpler this process is, the faster your query will run.

310

Chapter 12  Advanced MySQL Administration

Table OptimizationIf a table has been in use for a period of time, data can become fragmented as updates and dele-tions are processed. This fragmentation increases the time taken to find things in this table. You can fix this problem by using the statement

OPTIMIZE TABLE tablename;

Using IndexesYou should use indexes where required to speed up your queries. Keep them simple and don’t create indexes that are not being used by your queries. You can check which indexes are being used by running EXPLAIN, as shown previously. You should also minimize the length of primary keys.

Using Default ValuesWherever possible, you should use default values for columns and insert data only if it differs from the default. This way, you reduce the time taken to execute the INSERT statement.

Other TipsYou can make many other minor tweaks to improve performance in particular situations and address particular needs. The MySQL website offers a good set of additional tips. You can find it at http://www.mysql.com.

Backing Up Your MySQL DatabaseIn MySQL, there are several ways to do a backup. 

The first way is to lock the tables while you copy the physical files, using a LOCK TABLES command with the following syntax:

LOCK TABLES table lock_type [, table lock_type ...]

Each table should be the name of a table, and the lock type should be either READ or WRITE. For a backup, you only need a read lock. You need to execute a FLUSH TABLES; command to make sure any changes to your indexes have been written to disk before performing a backup.

Users and scripts can still run read-only queries while you make your backup. If you have a reasonable volume of queries that alter the database, such as customer orders, this solution is not practical.

The second, and superior, method is using the mysqldump command. Usage is from the  operating system command line, and is typically something such as

> mysqldump --all-databases > all.sql

Implementing Replication

311

This command dumps a set of all the SQL required to reconstruct the database to the file called all.sql.

If using InnoDB (the default engine), you can make an online backup, and even better keep track of where you were up to in the binary log. What this means is that if you are restoring your database from that backup, you will be able to reload the backup and then replay changes since the backup was made. You can do this with the following options:

> mysqldump --all-databases --single-transaction --flush-logs   --master-data=2 > all_databases.sql

The --single-transaction option does the backup while the database is still running (by acquiring a read lock). The --flush-logs and --master-data options flush the logs and then note the point in the log where the backup was made.

A third method is using the mysqlhotcopy script. You can invoke it with

> mysqlhotcopy database /path/for/backup

A final method of backup, which also has other advantages, is to maintain one or more replicated copies of the database. Replication is discussed later in this chapter.

Restoring Your MySQL DatabaseIf you need to restore your MySQL database, there are, again, a couple of approaches. 

If you used the first method from the preceding section for backup, you can copy the data files back into the same locations in a new MySQL installation.

If you used the second method for backup, there are a couple of steps. First, you need to run the queries in your dump file. This step reconstructs the database up to the point where you dumped that file. Second, you need to update the database to the point stored in the binary log. You can do this by running the command

> mysqlbinlog bin.[0-9]* | mysql

More information about the process of MySQL backup and recovery can be found at the MySQL website at http://www.mysql.com.

Implementing ReplicationReplication is a technology that allows you to have multiple database servers hosting the same data. This way, you can load share and improve system reliability; if one server goes down, the others can still be queried. Once set up, it can also be used for making backups.

The basic idea is to have a master server and add to it a number of slaves. Each of the slaves mirrors the master. When you initially set up the slaves, you copy over a snapshot of all the data on the master at that time. After that, slaves request updates from the master. The master 

312

Chapter 12  Advanced MySQL Administration

transmits details of the queries that have been executed from its binary log, and the slaves reapply them to the data.

The usual way of using this setup is to apply write queries to the master and read queries to the slaves. This is called read-write splitting and can be implemented using a tool such as MySQL Proxy, or in your application logic.

More complex architectures are possible, such as having multiple masters, but we will only consider the setup for the typical master-slave example.

You need to realize that slave data is generally not as up to date as on the master. This occurs in any distributed database. The difference between the master and slaves is sometimes referred to as slave lag.

To begin setting up a master and slave architecture, you need to make sure binary logging is enabled on the master. Enabling binary logging is discussed in Appendix A,「Installing Apache, PHP, and MySQL.」

You need to edit your my.ini or my.cnf file on both the master and slave servers. On the master, you need the following settings:

[mysqld]log-binserver-id=1

The first setting turns on binary logging (so you should already have this one; if not, add it in now). The second setting gives your master server a unique ID. Each of the slaves also needs an ID, so you need to add a similar line to the my.ini/my.cnf files on each of the slaves. Make sure the numbers are unique! For example, your first slave could have server-id=2; the next, server-id=3; and so on.

Setting Up the MasterOn the master, you need to create a user for slaves to use to connect. There is a special privilege level for slaves called REPLICATION SLAVE. Depending on how you plan to do the initial data transfer, you may need to temporarily grant some additional privileges.

In most cases, you will use a database snapshot to transfer the data, and in this case, only the special replication slave privilege is needed. If you decide to use the LOAD DATA FROM MASTER command to transfer data (you learn about it in the next section), this user will also need the RELOAD, SUPER, and SELECT privileges, but only for initial setup. As per the principle of least privilege, discussed in Chapter 9, you should revoke these other privileges after the system is up and running.

Create a user on the master. You can call it anything you like and give it any password you like, but you should make a note of the username and password you choose. In our example, we call this user rep_slave:

GRANT REPLICATION SLAVEON *.*

Implementing Replication

313

TO 'rep_slave'@'%' IDENTIFIED BY 'password';

Obviously, you should change the password to something else.

Performing the Initial Data TransferYou can transfer data from master to slave by taking a snapshot of the database at the current time. You can do this by using the procedures described for taking backups elsewhere in this chapter. You should first flush the tables with the following statement:

mysql> FLUSH TABLES WITH READ LOCK;

The reason for the read lock is that you need to record the place the server is up to in its binary log when the snapshot was taken. You can do this by executing this statement:

mysql> SHOW MASTER STATUS;

You should see output similar to the following from this statement:

+------------------+----------+--------------+------------------+| File             | Position | Binlog_Do_DB | Binlog_Ignore_DB |+------------------+----------+--------------+------------------+| mysql-bin.000001 |      107 |              |                  |+------------------+----------+--------------+------------------+

Note the File and Position; you will need this information to set up the slaves.

Now take your snapshot and unlock the tables with the following statement:

mysql> UNLOCK TABLES;

Setting Up the Slave or SlavesBegin by installing your data snapshot on the slave server.

Next, run the following queries on your slave:

change master tomaster-host='server',master-user='user',master-password='password',master-log-file='logfile',master-log-pos=logpos;start slave;

You need to fill in the data shown in italics. The server is the name of the master server. The user and password come from the GRANT statement you ran on the master server. The logfile and logpos come from the output of the SHOW MASTER STATUS statement you ran on the master server.

You should now be up and running.

314

Chapter 12  Advanced MySQL Administration

Further ReadingIn these chapters on MySQL, we have focused on the uses and parts of the system most relevant to web development and to linking MySQL with PHP. If you want to know more about MySQL administration, you can visit the MySQL website at http://www.mysql.com.

You might also want to consult Paul Dubois’ book MySQL (Fifth Edition), available from Addison-Wesley.

NextIn the next chapter,「Advanced MySQL Programming,」we look at some advanced features of MySQL that are useful when writing web applications, such as how to use the different storage engines, transactions, and stored procedures.


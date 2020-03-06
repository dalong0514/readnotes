9Creating Your Web Database

In this chapter, we explain how to set up a MySQL database for use on a website.

Key topics covered in this chapter include

 ■ Creating a database

 ■ Setting up users and privileges

 ■ Introducing the privilege system

 ■ Creating database tables

 ■ Creating indexes

 ■ Choosing column types in MySQL

In this chapter, we follow through with the Book-O-Rama online bookstore application discussed in the preceding chapter. As a reminder, here is the schema for the Book-O-Rama application:

Customers(CustomerID, Name, Address, City)

Orders(OrderID, CustomerID, Amount, Date)

Books(ISBN, Author, Title, Price)

Order_Items(OrderID, ISBN, Quantity) Book_Reviews(ISBN, Review)

Remember that each primary key is underlined and each foreign key is italic.

222

Chapter 9  Creating Your Web Database 

To use the material in this section, you must have access to MySQL. This usually means that you have completed the basic install of MySQL on your web server. This step includes

 ■ Installing the files

 ■ Setting up a user for MySQL to run as, if required on your OS

 ■ Setting up your path

 ■ Running mysql_install_db, if required on your OS

 ■ Setting the root password

 ■ Deleting the anonymous user and test database

 ■ Starting the MySQL server for the first time and setting it up to run automatically

If you’ve completed all these tasks, you can go right ahead and read this chapter. If you haven’t, you can find instructions on how to do these things in Appendix A,「Installing Apache, PHP, and MySQL.」

If you have problems at any point in this chapter, your MySQL system might not be set up correctly. If that is the case, refer to this list and Appendix A to make sure that your setup is correct.

You may be in a situation where you have access to MySQL on a machine that you do not administer, such as a web hosting service, a machine at your workplace, and so on.

If this is the case, to work through the examples or to create your own database, you need to have your administrator set up a user and database for you to work with and tell you the  username, password, and database name she has assigned to you. You can either skip the sections of this chapter that explain how to set up users and databases or read them to better explain what you need to your system administrator. As a typical user, you will not be able to execute the commands to create users and databases.

The examples in this chapter were built and tested with the latest MySQL 5.6 Community Edition version at the time of writing. Some earlier versions of MySQL have less functionality. You should install or upgrade to the most current stable release at the time of reading. You can download the current release from the MySQL site at http://www.mysql.com.

In this book, we interact with MySQL using a command-line client called the MySQL monitor, which comes with every MySQL installation. However, you can use other clients. If you are using MySQL in a hosted web environment, for example, system administrators will often provide the phpMyAdmin browser-based interface for you to use. Different graphic user  interface (GUI) clients obviously involve slightly different procedures from what we describe here, but you should be able to adapt these instructions fairly easily.

Using the MySQL MonitorIn the MySQL examples in this chapter and the next, each command ends with a semicolon (;). This tells MySQL to execute the command. If you leave off the semicolon, nothing will happen. This is a common problem for new users.

Logging In to MySQL

223

As a result of leaving off the semicolon, you can have new lines in the middle of a command. We used this scheme to make the examples easier to read. You can see where we have used this approach because MySQL provides a continuation symbol; it’s an arrow that looks like this:

mysql> grant select    ->

This symbol means MySQL expects more input. Until you type the semicolon, you get these characters each time you press Enter.

Another point to note is that SQL statements are not case sensitive, but database and table names can be (more on this topic later).

Logging In to MySQLTo log in to MySQL, go to a command-line interface on your machine and type the following:

mysql -h hostname -u username -p

The mysql command invokes the MySQL monitor, which is a command-line client that connects you to the MySQL server.

The -h switch specifies the host to which you want to connect—that is, the machine on which the MySQL server is running. If you’re running this command on the same machine as the MySQL server, you can leave out this switch and the hostname parameter. If not, you should replace the hostname parameter with the name of the machine where the MySQL server is running.

The -u switch specifies the username you want to connect as. If you do not specify, the default will be the username you are logged in to the operating system as.

If you have installed MySQL on your own machine or server, you need to log in as root and create the database we’ll use in this section. Assuming that you have a clean install, root is the only user you’ll have to begin with. If you are using MySQL on a machine administered by somebody else, use the username that person gave you.

The -p switch tells the server you want to connect using a password. You can leave it out if a password has not been set for the user you are logging in as.

If you are logging in as root and have not set a password for root, we strongly recommend that you visit Appendix A right now. Without a root password, your system is insecure.

You don’t need to include the password on this line. The MySQL server will ask you for it. In fact, it’s better if you don’t include it here. If you enter the password on the command line, it will appear as plain text on the screen and will be quite simple for other users to discover.

After you enter the previous command, you should get a response something like this:

Enter password: 

(If this command doesn’t work, verify that the MySQL server is running and the mysql command is somewhere in your path.)

224

Chapter 9  Creating Your Web Database 

You should then enter your password. If all goes well, you should see a response something like this:

Welcome to the MySQL monitor.  Commands end with ; or \g.Your MySQL connection id is 559Server version: 5.6.19-log MySQL Community Server (GPL)

Copyright (c) 2000, 2014, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or itsaffiliates. Other names may be trademarks of their respectiveowners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement. mysql>

On your own machine, if you don’t get a response similar to this, make sure that you have run mysql_install_db if required, you have set the root password, and you’ve typed it in correctly. If it isn’t your machine, make sure that you typed in the password correctly.

You should now be at a MySQL command prompt, ready to create the database. If you are using your own machine, follow the guidelines in the next section. If you are using  somebody else’s machine, these steps should already have been done for you. You can jump ahead to the「Using the Right Database」section. You might want to read the intervening sections for general background, but you cannot run the commands specified there. (Or at least you shouldn’t be able to.)

Creating Databases and UsersThe MySQL database system can support many different databases. You will generally have one database per application. In the Book-o-Rama example, the database will be called books.

Creating the database is the easiest part. At the MySQL command prompt, type

mysql> create database dbname;

You should substitute the name of the database you want to create for dbname. To begin  creating the Book-O-Rama example, create a database called books.

That’s it. You should see a response like this (the time to execute will likely be different):

Query OK, 1 row affected (0.0 sec)

This means everything has worked. If you don’t get this response, make sure that you typed the semicolon at the end of the line. A semicolon tells MySQL that you are finished, and it should actually execute the command.

Introducing MySQL’s Privilege System

225

Setting Up Users and PrivilegesA MySQL system can have many users. The root user should generally be used for  administration purposes only, for security reasons. For each user who needs to use the system, you need to set up an account and password. They do not need to be the same as usernames and passwords outside MySQL (for example, Unix usernames and passwords). The same  principle applies to root. Having different passwords for the system and for MySQL is a good idea, especially when it comes to the root password.

Setting up passwords for users isn’t compulsory, but we strongly recommend that you set up passwords for all the users you create. For the purposes of setting up a web database, it’s a good idea to set up at least one user per web application. You might ask,「Why would I want to do this?」The answer lies in privileges.

Introducing MySQL’s Privilege SystemOne of the best features of MySQL is that it supports a sophisticated privilege system. A privilege is the right to perform a particular action on a particular object and is associated with a  particular user. The concept is similar to file permissions. When you create a user within MySQL, you grant her a set of privileges to specify what she can and cannot do within the system.

Principle of Least PrivilegeThe principle of least privilege can be used to improve the security of any computer system. It’s a basic but important principle that is often overlooked. The principle is as follows:

A user (or process) should have the lowest level of privilege required to perform his assigned task.

It applies in MySQL as it does elsewhere. For example, to run queries from the Web, a user does not need all the privileges to which root has access. You should therefore create another user who has only the necessary privileges to access the database you just created.

User Setup: The CREATE USER and GRANT CommandsThe GRANT and REVOKE commands enable you to give rights to and take them away from MySQL users at these six levels of privilege:

 ■ Global

 ■ Database

 ■ Table

 ■ Column

 ■ Stored Routine

 ■ Proxy User

226

Chapter 9  Creating Your Web Database 

We will discuss the first four of these in this chapter. Stored routine privileges will be covered in the section on stored routines in Chapter 13,「Advanced MySQL Programming.」Proxy user privileges are not covered in this book as they are a much less common use case. Please refer to the MySQL manual for more information.

The CREATE USER command, unsurprisingly, creates a user. The general form of this command is as follows:

CREATE USER user_info IDENTIFIED BY [PASSWORD] password | IDENTIFIED WITH [auth_plugin] [AS auth_string]

The clauses in square brackets are optional. There are a number of placeholders in this syntax, too.

The user_info placeholder consists of a user_name, optionally followed by a hostname,  separated by an @ symbol, each in quotes, like the following: 'laura'@'localhost'.

The user_name should be the name you want the user to log in as in MySQL. Remember that it does not have to be the same as a system login name. The user_info in MySQL can also contain a hostname. You can use this to differentiate between, say, laura (interpreted as laura@localhost) and laura@somewhere.com. This capability is quite useful because users from different domains often have the same name. It also increases security because you can specify where users can connect from, and even which tables or databases they can access from a particular location.

The password placeholder should be the password you want the user to log in with. The usual rules for selecting passwords apply. We discuss security more later, but a password should not be easily guessable. This means that a password should not be a dictionary word or the same as the username. Ideally, it should contain a mixture of upper- and lowercase and nonalphabetic characters.

As an alternative to using passwords, since MySQL 5.5.7 you have been able to use an  authentication plugin. To use this, you would specify the alternate IDENTIFIED WITH [auth_plugin] syntax. We will not cover authentication plugins in this book, but you can read about them in the MySQL manual if you need this functionality. The GRANT command gives a user privileges. It will also create a user account if it does not yet exist, so skipping straight to GRANT can be used as a shortcut.

The general form of the GRANT command is

GRANT privileges [columns]ON itemTO user_info [IDENTIFIED BY password | IDENTIFIED WITH [auth_plugin] [AS auth_string]][REQUIRE ssl_options][WITH [GRANT OPTION | limit_options]  ]

Some of these clauses are the same as in the CREATE USER statement, and work exactly the same way. Let’s look at the new clauses introduced here.

The privileges clause should be a comma-separated list of privileges. MySQL has a defined set of such privileges, which are described in the next section.

Introducing MySQL’s Privilege System

227

The columns placeholder is optional. You can use it to specify privileges on a column-by-column basis. You can use a single column name or a comma-separated list of column names.

The item placeholder is the database or table to which the new privileges apply. You can grant privileges on all the databases by specifying *.* as the item. This is called granting global  privileges. You can also do this by specifying * alone if you are not using any particular  database. More commonly, you can specify all tables in a database as dbname.*, on a single table as dbname.tablename, or on specific columns by specifying dbname.tablename and some specific columns in the columns placeholder. These examples represent the three other levels of privilege available: database, table, and column, respectively. If you are using a specific database when you issue this command, tablename on its own will be interpreted as a table in the current database.

The REQUIRE clause allows you to specify that the user must connect via Secure Sockets Layer (SSL) and specify other SSL options. For more information on SSL connections to MySQL, refer to the MySQL manual.

The WITH GRANT OPTION option, if specified, allows the specified user to grant his or her own privileges to others.

You can instead specify the WITH clause as

MAX_QUERIES_PER_HOUR n

or

MAX_UPDATES_PER_HOUR n

or

MAX_CONNECTIONS_PER_HOUR n

or

MAX_USER_CONNECTIONS n

These clauses allow you to limit the number of queries, updates, connections per hour, or simultaneous connections a user may make. They can be useful for limiting individual user load on shared systems.

Privileges are stored in six system tables, in the database called mysql. These six tables are called mysql.user, mysql.db, mysql.host, mysql.tables_priv, mysql.columns_priv, and mysql.procs_priv. As an alternative to GRANT, you can alter these tables directly. We discuss exactly how these tables work and how you can alter them directly in Chapter 12,「Advanced MySQL Administration.」

Types and Levels of PrivilegesThree basic types of privileges exist in MySQL: privileges suitable for granting to regular users, privileges suitable for administrators, and a couple of special privileges. Any user can be granted any of these privileges, but it’s usually sensible to restrict the administrator type privileges to administrators, according to the principle of least privilege.

228

Chapter 9  Creating Your Web Database 

You should grant privileges to users only for the databases and tables they need to use. You should not grant access to the mysql database to anyone except an administrator. This is the place where all the users, passwords, and so on are stored. (We look at this database in Chapter 12.)

Privileges for regular users directly relate to specific types of SQL commands and whether a user is allowed to run them. We discuss these SQL commands in detail in the next chapter. For now, let’s look at a conceptual description of what they do. The basic user privileges are shown in Table 9.1. The items under the Applies To column are the objects to which privileges of this type can be granted.

Table 9.1  Privileges for Users

Privilege

SELECT

INSERT

UPDATE

DELETE

INDEX

ALTER

CREATE

Applies To

Description

Tables, columns

Allows users to select rows (records) from tables.

Tables, columns

Allows users to insert new rows into tables.

Tables, columns

Allows users to modify values in existing table rows.

Tables

Tables

Tables

Allows users to delete existing table rows.

Allows users to create and drop indexes on particular tables.

Allows users to alter the structure of existing tables by, for example, adding columns, renaming columns or tables, and changing data types of columns.

Databases, tables, indexes

Allows users to create new databases, tables, or indexes. If a particular database, table, or index is specified in a GRANT statement, they can only create that item, which means they will have to drop it first.

DROP

Databases, tables, views

EVENT

Databases

TRIGGER

Tables

CREATE VIEW

SHOW VIEW

Views

Views

PROXY

Everything

Allows users to drop (delete) databases, tables, or views.

Allows users to view, create, alter, and drop events in the Event Scheduler (not covered in this book).

Allows users to create, execute or drop triggers for the table named in the grant.

Allows users to create views.

Allows users to see the query that created a view.

Allows a user to impersonate another user, similar to su in Unix.

CREATE ROUTINE Stored routines

Allows users to create stored procedures and functions.

EXECUTE 

Stored routines

Allows users to run stored procedures and functions.

ALTER ROUTINE

Stored routines

Allows users to alter the definition of stored procedures and functions.

Introducing MySQL’s Privilege System

229

Most of the privileges for regular users are relatively harmless in terms of system security. The ALTER privilege can be used to work around the privilege system by renaming tables, but it is widely needed by users. Security is always a trade-off between usability and safety. You should make your own decision when it comes to ALTER, but it is often granted to users.

In addition to the privileges listed in Table 9.1, the GRANT privilege is granted with WITH GRANT OPTION rather than in the privileges list.

Table 9.2 shows the privileges suitable for use by administrative users.

Table 9.2  Privileges for Administrators

Privilege

Description

CREATE TABLESPACE

Allows an administrator to create, alter, or drop tablespaces.

CREATE USER

Allows an administrator to create users (as seen previously).

CREATE TEMPORARY TABLES Allows an administrator to use the keyword TEMPORARY in 

FILE

LOCK TABLES

PROCESS

RELOAD

REPLICATION CLIENT

REPLICATION SLAVE

SHOW DATABASES

SHUTDOWN

SUPER

a CREATE TABLE statement.

Allows data to be read into tables from files and vice versa.

Allows the explicit use of a LOCK TABLES statement.

Allows an administrator to view server processes belonging to all users.

Allows an administrator to reload grant tables and flush  privileges, hosts, logs, and tables.

Allows use of SHOW STATUS on replication masters and slaves. Replication is explained in Chapter 12.

Allows replication slave servers to connect to the master server. Replication is explained in Chapter 12.

Allows a list of all databases to be seen with a SHOW DATABASES statement. Without this privilege, users see only databases on which they have other privileges.

Allows an administrator to shut down the MySQL server.

Allows an administrator to kill threads belonging to any user.

You are able to grant these privileges to nonadministrators, but you should use extreme caution if you are considering doing so.

The FILE privilege is a special case. It is useful for users because loading data from files can save a lot of time re-entering data each time to get it into the database. However, file loading can be used to load any file that the MySQL server can see, including databases belonging to other users and, potentially, password files. Grant this privilege with caution or offer to load the data for the user.

230

Chapter 9  Creating Your Web Database 

Two special privileges also exist, and they are shown in Table 9.3.

Table 9.3  Special Privileges

Privilege

Description

ALL

USAGE

Grants all the privileges listed in Tables 9.1 and 9.2. You can also write ALL PRIVILEGES instead of ALL.

Grants no privileges. This privilege creates a user and allows him or her to log on, but it doesn’t allow the user to do anything. Usually, you will add more  privileges later. Using GRANT to create a user with USAGE privilege is equivalent to the CREATE USER statement.

The REVOKE CommandThe opposite of GRANT is REVOKE. You use it to take privileges away from a user. It is similar to GRANT in syntax:

REVOKE privileges [(columns)]ON itemFROM user_name

If you have given the WITH GRANT OPTION clause, you can revoke this (along with all other privileges) by adding

REVOKE ALL PRIVILEGES, GRANT OPTIONFROM user_name

Examples Using GRANT and REVOKETo set up an administrator, you can type

mysql> grant all    -> on *.*    -> to 'fred' identified by 'mnb123'    -> with grant option;

This command grants all privileges on all databases to a user called fred, connecting from any host, with the password mnb123 and allows him or her to pass on those privileges.

Chances are you don’t want this user in your system, so go ahead and revoke him or her:

mysql> revoke all privileges, grant option    -> from 'fred';

Now you can set up a regular user with no privileges:

mysql> grant usage    -> on books.*    -> to 'sally'@'localhost' identified by 'magic123';

Setting Up a User for the Web

231

After talking to Sally, you know a bit more about what she wants to do, so you can give her the appropriate privileges:

mysql> grant select, insert, update, delete, index, alter, create, drop    -> on books.*    -> to 'sally'@'localhost';

Note that you don’t need to specify Sally’s password to give her privileges.

If you decide that Sally has been up to something in the database, you might decide to reduce her privileges:

mysql> revoke alter, create, drop    -> on books.*    -> from 'sally'@'localhost';

And later, when she doesn’t need to use the database any more, you can revoke her privileges altogether:

mysql> revoke all    -> on books.*    -> from 'sally'@'localhost';

Setting Up a User for the WebYou need to set up a user for your PHP scripts to connect to MySQL. Again, you can apply the privilege of least principle: What should the scripts be able to do?

In most cases, they only need to run SELECT, INSERT, DELETE, and UPDATE queries. You can set up these privileges as follows:

mysql> grant select, insert, delete, update    -> on books.*    -> to 'bookorama' identified by 'bookorama123';

Obviously, for security reasons, you should choose a better password than the one shown here.

If you use a web hosting service, you usually get access to user-type privileges on a database the service creates for you. It typically gives you the same user_name and password for command-line use (setting up tables and so on) and for web script connections (querying the database). Using the same username and password for both is marginally less secure. You can set up a user with this level of privilege as follows:

mysql> grant select, insert, update, delete, index, alter, create, drop    -> on books.*    -> to 'bookorama' identified by 'bookorama123';

Go ahead and set up this second version of the user because you need to use it in the next section.

232

Chapter 9  Creating Your Web Database 

Note that in this case, we didn’t specify a hostname. You can add this here if you like. The value you add depends on where your PHP code is running. If it’s the same machine you can add ‘localhost’, if it’s a different machine then you’ll want to add the correct hostname or IP.

You can log out of the MySQL monitor by typing quit. You should log back in as your web user to test that everything is working correctly. If the GRANT statement that you ran was executed, but you are denied access when trying to log in, this usually means you have not deleted the anonymous users as part of the installation process. Log back in as root and consult Appendix A for instructions on how to delete the anonymous accounts. You should then be able to log in as the web user.

Using the Right DatabaseIf you’ve reached this stage, you should be logged in to a user-level MySQL account ready to test the sample code, either because you’ve just set it up or because your web server administrator has set it up for you.

The first step you need to take when you log in is to specify which database you want to use. You can do this by typing

mysql> use dbname;

where dbname is the name of your database.

Alternatively, you can avoid the use command by specifying the database when you log in, as follows:

mysql -D dbname -h hostname -u username -p

In this example, you can use the books database:

mysql> use books;

When you type this command, MySQL should give you a response such as

Database changed

If you don’t select a database before starting work, MySQL will give you an error message such as

ERROR 1046 (3D000): No Database Selected

Creating Database TablesThe next step in setting up the database is to actually create the tables. You can do this using the SQL command CREATE TABLE. The general form of a CREATE TABLE statement is

CREATE TABLE tablename(columns)

Creating Database Tables

233

NoteYou may be aware that MySQL offers more than one table type or storage engine. We  discuss the table types in Chapter 13. At present, all the tables in the database use the default  storage engine, which is now InnoDB as of MySQL 5.5.5.

You should replace the tablename placeholder with the name of the table you want to create and the columns placeholder with a comma-separated list of the columns in your table. Each column will have a name followed by a data type.

Here’s the Book-O-Rama schema again:

Customers(CustomerID, Name, Address, City)

Orders(OrderID, CustomerID, Amount, Date) Books(ISBN, Author, Title, Price) Order_Items(OrderID, ISBN, Quantity) Book_Reviews(ISBN, Review)

Listing 9.1 shows the SQL to create these tables, assuming you have already created the  database called books. You can find this SQL in the file chapter9/bookorama.sql.

You can run an existing SQL file through MySQL by typing

> mysql -h host -u bookorama -D books -p < bookorama.sql

(Remember to replace host with the name of your host and to specify the full path to the bookorama.sql file.)

Using file redirection is handy for this task because it means that you can edit your SQL in the text editor of your choice before executing it.

Listing 9.1  bookorama.sql—SQL to Create the Tables for Book-O-RamaCREATE TABLE Customers( CustomerID INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,  Name CHAR(50) NOT NULL,  Address CHAR(100) not null,  City CHAR(30) not null); CREATE TABLE Orders( OrderID INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,  CustomerID INT UNSIGNED NOT NULL,  Amount FLOAT(6,2),  Date DATE NOT NULL, 

234

Chapter 9  Creating Your Web Database 

  FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID));

CREATE TABLE Books(  ISBN CHAR(13) NOT NULL PRIMARY KEY,   Author CHAR(50),   Title CHAR(100),   Price FLOAT(4,2));

CREATE TABLE Order_Items( OrderID INT UNSIGNED NOT NULL,  ISBN CHAR(13) NOT NULL,  Quantity TINYINT UNSIGNED,

  PRIMARY KEY (OrderID, ISBN),  FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),  FOREIGN KEY (ISBN) REFERENCES Books(ISBN));

CREATE TABLE Book_Reviews(  ISBN CHAR(13) NOT NULL PRIMARY KEY,  Review TEXT,

  FOREIGN KEY (ISBN) REFERENCES Books(ISBN));

Each table is created by a separate CREATE TABLE statement. You can see that each table in the schema is created with the columns designed in the preceding chapter. Each column has a data type listed after its name, and some of the columns have other specifiers, too.

Understanding What the Other Keywords MeanNOT NULL means that all the rows in the table must have a value in this attribute. If it isn’t specified, the field can be blank (NULL).

AUTO_INCREMENT is a special MySQL feature you can use on integer columns. It means if you leave that field blank when inserting rows into the table, MySQL will automatically generate a unique identifier value. The value will be one greater than the maximum value in the column already. You can have only one of these in each table. Columns that specify AUTO_INCREMENT must be indexed.

PRIMARY KEY after a column name specifies that this column is the primary key for the table. Entries in this column have to be unique. MySQL automatically indexes this column. Where it is used with CustomerID in the Customers table in Listing 9.1, it appears with 

Creating Database Tables

235

AUTO_INCREMENT. The automatic index on the primary key takes care of the index required by AUTO_INCREMENT.

You can specify PRIMARY KEY after a column name only for single column primary keys. The PRIMARY KEY clause at the end of the Order_Items statement is an alternative form. We used it here because the primary key for this table consists of the two columns together. (This also creates an index based on the two columns together.)

You can also specify FOREIGN KEY at the end of the table definition, along with the name of the reference table and column. This constraint means that the specified column must have a matching value in the reference location. You can specify different semantics for what to do if the reference data is deleted. For example, ending this line with ON DELETE CASCADE would mean「if the reference row is deleted, delete corresponding rows here too」. In this case we have chosen to go with the default behavior which is RESTRICT. This means that you are unable to delete or update rows in the reference table without first making the appropriate changes in this table.

Note that the FOREIGN KEY specification will only have an effect if we are using a storage engine that supports foreign keys, such as the default, InnoDB. In older versions of MySQL, MyISAM was the default type, and it does not support foreign keys. We’ll talk more about the different storage engines in Chapter 13. 

UNSIGNED after an integer type means that it can have only a zero or positive value.

Understanding the Column TypesLet’s consider the first table as an example:

CREATE TABLE Customers( CustomerID INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,  Name CHAR(50) NOT NULL,  Address CHAR(100) not null,  City CHAR(30) not null); 

When creating any table, you need to make decisions about column types.

The Customers table has four columns as specified in the schema. The first one, CustomerID, is the primary key, which is specified directly. We decided this will be an integer (data type INT) and that these IDs should be UNISGNED , as we don’t plan on having negative CustomerIDs. We’ve also taken advantage of the AUTO_INCREMENT facility so that MySQL can manage them for us; it’s one less thing to worry about.

The other columns are all going to hold string type data. We chose the CHAR type for them. This type specifies fixed-width fields. The width is specified in the brackets, so, for example, Name can have up to 50 characters.

This data type will always allocate 50 characters of storage for the name, even if they’re not all used. MySQL will pad the data with spaces to make it the right size. The alternative is VARCHAR, 

236

Chapter 9  Creating Your Web Database 

which uses only the amount of storage required (plus one byte). There is a small trade-off: VARCHARs use less space on average, but CHARs are faster.

Note that all the columns are declared as NOT NULL. This is a minor optimization you can make wherever possible that also will make things run a bit faster. We address optimization in more detail in Chapter 12.

Some of the other CREATE statements have variations in syntax. Let’s look at the Orders table:

CREATE TABLE Orders( OrderID INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY,  CustomerID INT UNSIGNED NOT NULL,  Amount FLOAT(6,2),  Date DATE NOT NULL,   FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)); 

The Amount column is specified as a floating-point number of type FLOAT. With most  floating-point data types, you can specify the display width and the number of decimal places. In this case, the order amount will be in dollars, so we allowed a reasonably large order total (width 6) and two decimal places for the cents.

The Date column has the data type DATE.

This particular table specifies all columns, bar the amount, as NOT NULL. Why? When an order is entered into the database, you need to create it in Orders, add the items to Order_Items, and then work out the amount. You might not know the amount when the order is created, so you can allow for it to be NULL.

The Books table has some similar characteristics:

CREATE TABLE Books(  ISBN CHAR(13) NOT NULL PRIMARY KEY,   Author CHAR(50),   Title CHAR(100),   Price FLOAT(4,2)); 

In this case, you don’t need to generate the primary key because ISBNs are generated elsewhere. The other fields are left as NULL because a bookstore might know the ISBN of a book before it knows the Title, Author, or Price.

The Order_Items table demonstrates how to create multicolumn primary keys:

CREATE TABLE Order_Items( OrderID INT UNSIGNED NOT NULL,  ISBN CHAR(13) NOT NULL,  Quantity TINYINT UNSIGNED, 

Creating Database Tables

237

  PRIMARY KEY (OrderID, ISBN),  FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),  FOREIGN KEY (ISBN) REFERENCES Books(ISBN)); 

This table specifies the quantity of a particular book as a TINYINT UNSIGNED, which holds an integer between 0 and 255.

As mentioned previously, multicolumn primary keys need to be specified with a special primary key clause. This clause is used here.

Lastly, consider the Book_Reviews table:

CREATE TABLE Book_Reviews(  ISBN CHAR(13) NOT NULL PRIMARY KEY,  Review TEXT,

  FOREIGN KEY (ISBN) REFERENCES Books(ISBN)); 

This table uses a new data type, text, which we have not yet discussed. It is used for longer text, such as an article. There are a few variants on this, which we discuss later in this chapter.

To understand creating tables in more detail, let’s discuss column names and identifiers in general and then the data types we can choose for columns. First, though, let’s look at the  database we’ve created.

Looking at the Database with SHOW and DESCRIBELog in to the MySQL monitor and use the books database. You can view the tables in the data-base by typing

mysql> show tables;

MySQL then displays a list of all the tables in the database:

+-----------------+| Tables_in_books |+-----------------+| Book_Reviews    || Books           || Customers       || Order_Items     || Orders          |+-----------------+5 rows in set (0.01 sec) 

You can also use show to see a list of databases by typing

mysql> show databases;

238

Chapter 9  Creating Your Web Database 

If you do not have the SHOW DATABASES privilege, you will see listed only the databases on which you have privileges.

You can see more information about a particular table, for example, Books, using DESCRIBE:

mysql> describe books;

MySQL then displays the information you supplied when creating the database:

+--------+------------+------+-----+---------+-------+| Field  | Type       | Null | Key | Default | Extra |+--------+------------+------+-----+---------+-------+| ISBN   | char(13)   | NO   | PRI | NULL    |       || Author | char(50)   | YES  |     | NULL    |       || Title  | char(100)  | YES  |     | NULL    |       || Price  | float(4,2) | YES  |     | NULL    |       |+--------+------------+------+-----+---------+-------+4 rows in set (0.01 sec) 

These commands are useful to remind yourself of a column type or to navigate a database that you didn’t create.

Creating IndexesWe briefly mentioned indexes already, because designating primary keys creates indexes on those columns.

One common problem faced by new MySQL users is that they complain about poor performance from this database they have heard is lightning fast. This performance problem occurs because they have not created any indexes on their database. (It is possible to create tables with no primary keys or indexes.)

To begin with, the indexes that were created automatically for you will do. If you find that you are running many queries on a column that is not a key, you may want to add an index on that column to improve performance. You can do this with the CREATE INDEX statement. The general form of this statement is

CREATE [UNIQUE|FULLTEXT|SPATIAL] INDEX index_nameON table_name (index_column_name [(length)] [ASC|DESC], ...])

FULLTEXT indexes are for indexing text fields; we discuss their use in Chapter 13. SPATIAL indexes are for indexing spatial data, which is beyond the scope of this book.

UNIQUE indexes ensure that each value or combination of values in a multicolumn index must be unique. (This is the case for primary key indexes.)

The optional length field allows you to specify that only the first length characters of the field will be indexed. You can also specify that an index should be ascending (ASC) or  descending (DESC); the default is ascending.

Understanding MySQL Identifiers

239

Understanding MySQL IdentifiersMany kinds of identifiers are used in MySQL: databases, tables, columns, and indexes, which you’re already familiar with; aliases, which we cover in the next chapter; views and stored procedures, which we cover in Chapter 13; and a number of others.

Databases in MySQL map to directories in the underlying file structure, and tables map to one or more files. In older versions of MySQL, this mapping had a direct effect on the names you can give them, but now problematic characters are encoded.

However, this file system mapping also affects the case sensitivity of these names: If directory and filenames are case sensitive in your operating system, database and table names will be case sensitive (for example, in most varieties of Unix); otherwise, they won’t (for example, under Windows and OS X). Column names and alias names are not case sensitive, but you can’t use versions of different cases in the same SQL statement.

In addition—just to make matters more confusing—you can also affect case sensitivity of identifiers with the config setting lower_case_table_names.

In general, for maximum portability, it’s easiest to use lowercase for all identifiers.

As a side note, the location of the directory and files containing the data is wherever it was set in configuration. You can check the location on your system by using the mysqladmin facility as follows:

> mysqladmin -h host -u root -p variables

Then look for the datadir variable.

In general, identifiers can include all ASCII characters, and many Unicode characters. If you wish to include certain characters, your identifiers will need to be quoted. Quoted in this context means surrounded by backticks. The backtick character (`) may be mistaken for a single quote at first glance, but it is usually found below the tilde (~) on your keyboard.

The identifier rules are as follows:

 ■ Unquoted identifiers may contain ASCII letters (a-z and A-Z), digits (0-9), dollar signs, 

and underscores. They may also contain Unicode characters in the range U+0080 through U+FFFF.

 ■ If you put your identifier in quotes, it may contain anything in the ASCII range (U+0001 

through U+007F) and further Unicode characters from U+0080 through U+FFFF.

 ■ You may not ever use the NUL character (U+0000) or supplementary characters U+10000 

and up.

 ■ You may not have an identifier that consists solely of digits.

 ■ Database, table, and column names cannot end with a space.

240

Chapter 9  Creating Your Web Database 

A summary of possible identifiers is shown in Table 9.4.

Table 9.4  MySQL Identifiers

Type

Database

Table

Column

Index

Table alias

Column alias

Constraint

Trigger

View

Stored routine

Event

Tablespace

Server

Log file group

Compound statement label

Max Length

Case Sensitive?

64

64

64

64

256

256

64

64

64

64

64

64

64

64

16

OS dependent

OS/configuration dependent

No

No

OS dependent

No

No

OS dependent

OS dependent

No

No

Storage engine dependent

No

Yes

No

These rules are extremely open. You can even have reserved words and special characters of all kinds in identifiers. The only limitation is that if you use anything unusual like this, you have to quote it in backticks. For example,

create database `create database`;

Of course, you should apply common sense to all this freedom. Just because you can call a  database `create database` doesn’t that mean that you should. The same principle applies here as in any other kind of programming: Use meaningful identifiers.

Choosing Column Data TypesThe four basic column types in MySQL are numeric, date and time, string, and spatial. (We’ll discuss the first three of these within this book: spatial types are a special use case.) Within each of these categories are a large number of types. We summarize them here and go into more detail about the strengths and weaknesses of each in Chapter 12.

Choosing Column Data Types

241

Each of these three types come in various storage sizes. When you are choosing a column type, the principle is generally to choose the smallest type that your data will fit into.

For many data types, when you are creating a column of that type, you can specify the maximum display length. This is shown in the following tables of data types as M. If it’s optional for that type, it is shown in square brackets. The maximum value you can specify for M is 255.

Optional values throughout these descriptions are shown in square brackets.

Numeric TypesThe numeric types fall into the categories of integers, fixed-point numbers, floating-point numbers, and bit fields. For the floating-point numbers, you can specify the number of digits after the decimal place. This value is shown in this book as D. The maximum value you can specify for D is 30 or M-2 (that is, the maximum display length minus two—one character for a decimal point and one for the integral part of the number), whichever is lower.

For integer types, you can also specify whether you want them to be UNSIGNED, as shown in Listing 9.1.

For all numeric types, you can also specify the ZEROFILL attribute. When values from a ZEROFILL column are displayed, they are padded with leading zeros. If you specify a column as ZEROFILL, it will automatically also be UNSIGNED.

The integral types are shown in Table 9.5. Note that the ranges listed in this table show the signed range on one line and the unsigned range on the next.

Table 9.5 

Integral Data Types

Type

TINYINT[(M)]

SMALLINT[(M)]

Range

–127..128or 0..255

–32768..32767or 0..65535

MEDIUMINT[(M)] –8388608..

INT[(M)]

INTEGER[(M)]

BIGINT[(M)]

8388607or 0..16777215–231..231 –1or 0..232 –1

–263..263 –1or 0..264 –1

Storage (Bytes)

Description

1

2

3

4

8

Very small integers

Small integers

Medium-sized integers

Regular integers

Synonym for INT

Big integers

242

Chapter 9  Creating Your Web Database 

The floating-point types are shown in Table 9.6.

Table 9.6  Floating-Point Data Types

Type

Range

Storage (Bytes) Description

FLOAT(precision)

Depends on precision

Varies

4

8

FLOAT[(M,D)]

±1.175494351E-38±3.402823466E+38

DOUBLE[(M,D)]

±1.7976931348623157E+308±2.2250738585072014E-308

DOUBLEPRECISION[(M,D)] As above

REAL[(M,D)]

As above

The fixed-point data types are shown in Table 9.7.

Can be used to specify single or double precision floating-point numbers.

Single precision floating-point number. These numbers are equivalent to FLOAT(4) but with a  specified display width and number of decimal places.

Double precision  floating-point number. These numbers are equiv-alent to FLOAT(8) but with a  specified display width and number of deci-mal places.

Synonym for DOUBLE[(M, D)].

Synonym for DOUBLE[(M, D)].

Table 9.7  Fixed-Point Data Types

Type

DECIMAL[(M[,D])]

Range

Varies

NUMERIC[(M,D)]

DEC[(M,D)]

FIXED[(M,D)]

As above

As above

As above

Storage (Bytes)

Description

M+2

Fixed-point number—an exact value. The range depends on M, the display width.

Synonym for DECIMAL.

Synonym for DECIMAL.

Synonym for DECIMAL.

There is one additional numeric type: BIT(M). This allows storage of up to M bits, where M is between 1 and 64.

Choosing Column Data Types

243

Date and Time TypesMySQL supports a number of date and time types; they are shown in Table 9.8. With all these types, you can input data in either a string or numerical format. It is worth noting that a TIMESTAMP column in a particular row will be set to the date and time of the most recent  operation on that row if you don’t set it manually. This feature is useful for transaction recording.

Table 9.8  Date and Time Data Types

Type

DATE

TIME

DATETIME

TIMESTAMP[(M)]

YEAR[(2|4)]

Range

1000-01-019999-12-31

-838:59:59838:59:59

1000-01-0100:00:009999-12-3123:59:59

1970-01-0100:00:00

Sometime in 2037

70–69(1970–2069)1901–2155

Description

A date. Will be displayed as YYYY-MM-DD.

A time. Will be displayed as HH:MM:SS. Note that the range is much wider than you will probably ever want to use.

A date and time. Will be displayed as YYYY-MM-DD HH:MM:SS.

A timestamp, useful for transaction reporting.The display format depends on the value of M (see Table 9.9, which follows).The top of the range depends on the limit on Unix timestamps.

A year. You can specify two- or four-digit format. Each has a different range, as shown.

244

Chapter 9  Creating Your Web Database 

Table 9.9 shows the possible different display types for TIMESTAMP.

Table 9.9  TIMESTAMP Display Types

Type Specified

TIMESTAMP

TIMESTAMP(14)

TIMESTAMP(12)

TIMESTAMP(10)

TIMESTAMP(8)

TIMESTAMP(6)

TIMESTAMP(4)

TIMESTAMP(2)

Display

YYYYMMDDHHMMSS

YYYYMMDDHHMMSS

YYMMDDHHMMSS

YYMMDDHHMM

YYYYMMDD

YYMMDD

YYMM

YY

String TypesString types fall into four groups. First, there are plain old strings—that is, short pieces of text. These are the CHAR (fixed-length character) and VARCHAR (variable-length character) types. You can specify the width of each. Columns of type CHAR are padded with spaces to the maximum width regardless of the size of the data, whereas VARCHAR columns vary in width with the data. (Note that MySQL strips the trailing spaces from CHARs when they are retrieved and from VARCHARs when they are stored.) There is a space versus speed trade-off with these two types, which we discuss in more detail in Chapter 12.

Second, there are BINARY and VARBINARY types. These are strings of bytes rather than characters.

Third, there are TEXT and BLOB types. These types, which come in various sizes, are for longer text or binary data, respectively. BLOBs, or binary large objects, can hold anything you like—for example, image or sound data.

Because these column types can hold large amounts of data, they require some special  considerations. We discuss this issue in Chapter 12.

The fourth group has two special types: SET and ENUM. The SET type specifies that values in this column must come from a particular set of specified values. Column values can contain more than one value from the set. You can have a maximum of 64 things in the specified set.

ENUM is an enumeration. It is similar to SET, except that columns of this type can have only one of the specified values or NULL, and you can have a maximum of 65,535 things in the enumeration.

We summarized the string data types in Tables 9.10–9.13. Table 9.10 shows the plain string types.

Choosing Column Data Types

245

Table 9.10  Regular String Types

Type

Range

Description

CHAR(M) 

0 to 255 characters

CHAR

VARCHAR(M)

1 to 65,535 characters

Fixed-length string of length M, where M is between 0 and 255. 

Synonym for CHAR(1).

Same as above, except they are variable length.

Table 9.11 shows the BINARY and VARBINARY types.

Table 9.11  Binary String Types

Type

Range

Description

BINARY(M)

0 to 255 bytes

VARBINARY(M)

1 to 65,535 bytes

Fixed-length string of length M bytes, where M is between 0 and 255

Same as above, except they are variable length.

Table 9.12 shows the TEXT and BLOB types. The maximum length of a TEXT field in characters is the maximum size in bytes of files that could be stored in that field.

Table 9.12  TEXT and BLOB Types

Type

TINYBLOB

TINYTEXT

BLOB

TEXT

MEDIUMBLOB

MEDIUMTEXT

LONGBLOB

LONGTEXT

Maximum Length (Characters)28 –1 (that is, 255)

28 –1 (that is, 255)216 –1 (that is, 65,535)216 –1 (that is, 65,535)224 –1 (that is, 16,777,215)224 –1 (that is, 16,777,215)232 –1 (that is, 4,294,967,295)232 –1 (that is, 4,294,967,295)

Description

A tiny binary large object (BLOB) field

A tiny TEXT field

A normal-sized BLOB field

A normal-sized TEXT field

A medium-sized BLOB field

A medium-sized TEXT field

A long BLOB field

A long TEXT field

246

Chapter 9  Creating Your Web Database 

Table 9.13 shows the ENUM and SET types.

Table 9.13  ENUM and SET Types

Type

Maximum Values in Set

Description

ENUM('value1', 'value2',...)

65,535

SET('value1',

64

'value2',...)

Columns of this type can hold only one of the values listed or NULL.

Columns of this type can hold a set of the 

specified values or NULL.

Further ReadingFor more information, you can read about setting up a database in the MySQL online manual at http://www.mysql.com/.

NextNow that you know how to create users, databases, and tables, you can concentrate on inter-acting with the database. In the next chapter, we look at how to put data in the tables, how to update and delete it, and how to query the database.


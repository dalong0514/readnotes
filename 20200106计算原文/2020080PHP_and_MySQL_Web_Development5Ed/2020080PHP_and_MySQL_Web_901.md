10Working with Your MySQL Database

In this chapter, we discuss Structured Query Language (SQL) and its use in querying databases. You continue developing the Book-O-Rama database by learning how to insert, delete, and update data, and how to ask the database questions.

Key topics covered in this chapter include

 ■ What is SQL?

 ■ Inserting data into the database

 ■ Retrieving data from the database

 ■ Joining tables

 ■ Using subqueries

 ■ Updating records from the database

 ■ Altering tables after creation

 ■ Deleting records from the database

 ■ Dropping tables

We begin by describing what SQL is and why it’s a useful thing to understand.

If you haven’t set up the Book-O-Rama database, you need to do that before you can run the SQL queries in this chapter. Instructions for doing this are in Chapter 9,「Creating Your Web Database.」

What Is SQL?SQL stands for Structured Query Language. It’s the most standard language for accessing  relational database management systems (RDBMSs). SQL is used to store data to and retrieve it from a  database. It is used in database systems such as MySQL, Oracle, PostgreSQL, Sybase, and Microsoft SQL Server, among others.

248

Chapter 10  Working with Your MySQL Database 

There’s an ANSI standard for SQL, and database systems such as MySQL generally strive to implement this standard. There are some subtle differences between standard SQL and MySQL’s SQL. Some of these differences are planned to become standard in future versions of MySQL, and some are deliberate differences. We point out the more important ones as we go. A complete list of the differences between MySQL’s SQL and ANSI SQL in any given version can be found in the MySQL online manual. You can find this page at this URL and in many other locations: 

http://dev.mysql.com/doc/refman/5.6/en/compatibility.html.

You might have heard the terms Data Definition Language (DDL), used for defining databases, and Data Manipulation Language (DML), used for querying databases. SQL covers both of these bases. In Chapter 9, we looked at data definition (DDL) in SQL, so we’ve already been using it a little. You use DDL when you’re initially setting up a database.

You will use the DML aspects of SQL far more frequently because these are the parts that you use to store and retrieve data in a database.

Inserting Data into the DatabaseBefore you can do a lot with a database, you need to store some data in it. The way you most commonly do this is to use the SQL INSERT statement.

Recall that RDBMSs contain tables, which in turn contain rows of data organized into columns. Each row in a table normally describes some real-world object or relationship, and the column values for that row store information about the real-world object. You can use the INSERT  statement to put rows of data into the database.

The most common form of an INSERT statement is

INSERT [INTO] table [(column1, column2, column3,...)] VALUES(value1, value2, value3,...);

For example, to insert a record into Book-O-Rama’s Customers table, you could type

INSERT INTO Customers VALUES  (NULL, 'Julie Smith', '25 Oak Street', 'Airport West');

You can see that we’ve replaced table with the name of the actual table where we want to put the data and the values with specific values. The values in this example are all enclosed in quotation marks. Strings should always be enclosed in pairs of single or double quotation marks in MySQL. (We use both in this book.) Numbers and dates do not need quotes.

There are a few interesting things to note about the INSERT statement. The values specified here will be used to fill in the table columns in order. If you want to fill in only some of the columns, or if you want to specify them in a different order, you can list the specific columns in the columns part of the statement. For example,

INSERT INTO Customers (name, city) VALUES('Melissa Jones', 'Nar Nar Goon North');

Inserting Data into the Database

249

This approach is useful if you have only partial data about a particular record or if some fields in the record are optional. You can also achieve the same effect with the following syntax:

INSERT INTO CustomersSET Name = 'Michael Archer', Address = '12 Adderley Avenue', City = 'Leeton';

Also notice that we specified a NULL value for the CustomerID column when adding Julie Smith and ignored that column when adding the other customers. You might recall that when you set up the database, you created CustomerID as the primary key for the Customers table, so this might seem strange. However, you specified the field as AUTO_INCREMENT. This means that, if you insert a row with a NULL value or no value in this field, MySQL will generate the next number in the auto increment sequence and insert it for you automatically. This behavior is pretty useful.

You can also insert multiple rows into a table at once. Each row should be in its own set of parentheses, and each set of parentheses should be separated by a comma.

Only a few other variants are possible with INSERT. After the word INSERT, you can add LOW_PRIORITY, DELAYED, or HIGH_PRIORITY. The LOW_PRIORITY keyword means the system may wait and insert later when data is not being read from the table. The DELAYED keyword means that your inserted data will be buffered. If the server is busy, you can continue running queries rather than having to wait for this INSERT operation to complete. The HIGH_PRIORITY keyword only takes effect if you started mysqld with the --low-priority-updates option. It effectively cancels that option for the current query. If that option is not set, it has no effect.

Immediately after this, you can optionally specify IGNORE. This means that if you try to insert any rows that would cause a duplicate unique key, they will be silently ignored. Another alternative is to specify ON DUPLICATE KEY UPDATE expression at the end of the INSERT statement. This can be used to change the duplicate value using a normal UPDATE statement (covered later in this chapter).

We’ve put together some simple sample data to populate the database. This is just a series of simple INSERT statements that use the multirow insertion approach. This is shown in Listing 10.1.

Listing 10.1  book_insert.sql—SQL to Populate the Tables for Book-O-RamaUSE books;

INSERT INTO Customers VALUES  (1, 'Julie Smith', '25 Oak Street', 'Airport West'),  (2, 'Alan Wong', '1/47 Haines Avenue', 'Box Hill'),  (3, 'Michelle Arthur', '357 North Road', 'Yarraville');

INSERT INTO Books VALUES  ('0-672-31697-8', 'Michael Morgan',    'Java 2 for Professional Developers', 34.99),  ('0-672-31745-1', 'Thomas Down', 'Installing Debian GNU/Linux', 24.99),  ('0-672-31509-2', 'Pruitt, et al.', 'Teach Yourself GIMP in 24 Hours', 24.99),

250

Chapter 10  Working with Your MySQL Database 

  ('0-672-31769-9', 'Thomas Schenk',    'Caldera OpenLinux System Administration Unleashed', 49.99);

INSERT INTO Orders VALUES  (NULL, 3, 69.98, '2007-04-02'),  (NULL, 1, 49.99, '2007-04-15'),  (NULL, 2, 74.98, '2007-04-19'),  (NULL, 3, 24.99, '2007-05-01');

INSERT INTO Order_Items VALUES  (1, '0-672-31697-8', 2),  (2, '0-672-31769-9', 1),  (3, '0-672-31769-9', 1),  (3, '0-672-31509-2', 1),  (4, '0-672-31745-1', 3);

INSERT INTO Book_Reviews VALUES  ('0-672-31697-8', 'The Morgan book is clearly written and goes well beyond                     most of the basic Java books out there.'); 

You can run this script from the command line by piping it through MySQL as follows:

> mysql -h host -u bookorama -p books < /path/to/book_insert.sql

Retrieving Data from the DatabaseThe workhorse of SQL is the SELECT statement. It’s used to retrieve data from a database by selecting rows that match specified criteria from a table. There are a lot of options and different ways to use the SELECT statement.

The basic form of a SELECT is

SELECT [options] items[INTO file_details]FROM [tables][PARTITION partitions][ WHERE conditions ][ GROUP BY group_type ][ HAVING where_definition ][ ORDER BY order_type ][LIMIT limit_criteria ][PROCEDURE proc_name(arguments)][INTO destination][lock_options];

In the following sections, we describe each of the clauses of the statement. First, though, let’s look at a query without any of the optional clauses, one that selects some items from a 

Retrieving Data from the Database

251

particular table. Typically, these items are columns from the table. (They can also be the results of any MySQL expressions. We discuss some of the more useful ones in a later section.) This query lists the contents of the Name and City columns from the Customers table:

SELECT Name, CityFROM Customers;

This query has the following output, assuming that you’ve entered the sample data from Listing 10.1:

+-----------------+--------------+| Name            | City         |+-----------------+--------------+| Julie Smith     | Airport West || Alan Wong       | Box Hill     || Michelle Arthur | Yarraville   |+-----------------+--------------+3 rows in set (0.00 sec) 

As you can see, this table contains the items selected—Name and City—from the table  specified—Customers. This data is shown for all the rows in the Customers table.

You can specify as many columns as you like from a table by listing them after the SELECT keyword. You can also specify some other items. One useful item is the wildcard operator, *, which matches all the columns in the specified table or tables. For example, to retrieve all columns and all rows from the Order_Items table, you would use

SELECT *FROM Order_Items;

which gives the following output:

+---------+---------------+----------+| OrderID | ISBN          | Quantity |+---------+---------------+----------+|       1 | 0-672-31697-8 |        2 ||       2 | 0-672-31769-9 |        1 ||       3 | 0-672-31509-2 |        1 ||       3 | 0-672-31769-9 |        1 ||       4 | 0-672-31745-1 |        3 |+---------+---------------+----------+5 rows in set (0.01 sec) 

Retrieving Data with Specific CriteriaTo access a subset of the rows in a table, you need to specify some selection criteria. You can do this with a WHERE clause. For example,

SELECT *FROM OrdersWHERE CustomerID = 3;

252

Chapter 10  Working with Your MySQL Database 

selects all the columns from the Orders table, but only the rows with a CustomerID of 3. Here’s the output:

+---------+------------+--------+------------+| OrderID | CustomerID | Amount | Date       |+---------+------------+--------+------------+|       1 |          3 |  69.98 | 2007-04-02 ||       4 |          3 |  24.99 | 2007-05-01 |+---------+------------+--------+------------+2 rows in set (0.02 sec) 

The WHERE clause specifies the criteria used to select particular rows. In this case, we selected rows with a CustomerID of 3. The single equal sign is used to test equality; note that this is different from PHP, and you can easily become confused when you’re using them together.

In addition to equality, MySQL supports a full set of operators and regular expressions. The ones you will most commonly use in WHERE clauses are listed in Table 10.1. Note that this list is not complete; if you need something not listed here, check the MySQL manual.

Table 10.1  Useful Comparison Operators for WHERE Clauses

Operator

Name (If Applicable)

Example

Description

=

>

<

>=

<=

Equality

customerid = 3

Greater than

amount > 60.00

Less than

amount < 60.00

Greater than or equal to

Less than or equal to

amount >= 60.00

amount <= 60.00

!= or <>

Not equal

quantity != 0

Tests whether two values are equal

Tests whether one value is greater than another

Tests whether one value is less than another

Tests whether one value is greater than or equal to another

Tests whether one value is less than or equal to another

Tests whether two values are not equal

IS NOT NULL

n/a

IS NULL

n/a

BETWEEN

n/a

address is not null

Tests whether a field actually contains a value

address is null

Tests whether a field does not contain a value

amount between 0 and 60.00

Tests whether a value is greater than or equal to a minimum value and less than or equal to a  maximum value

Retrieving Data from the Database

253

IN

n/a

NOT IN

n/a

LIKE

Pattern match

city in ("Carlton", "Moe")

city not in ("Carlton", "Moe")

name like ("Fred %")

Tests whether a value is in a  particular set

Tests whether a value is not in a set

Checks whether a value matches a pattern using simple SQL  pattern matching

NOT LIKE

Pattern match

name not like ("Fred %")

Checks whether a value doesn’t match a pattern

REGEXP

Regular expression

name regexp

Checks whether a value matches a regular expression

The last three rows in the table refer to LIKE and REGEXP. They are both forms of pattern matching.

LIKE uses simple SQL pattern matching. Patterns can consist of regular text plus the % (percent) character to indicate a wildcard match to any number of characters and the _ (underscore) character to wildcard-match a single character.

The REGEXP keyword is used for regular expression matching. MySQL uses POSIX regular expressions. Instead of the keyword REGEXP, you can also use RLIKE, which is a synonym. The syntax for POSIX regular expressions is a little different from the PCRE regular expressions used in PHP. (PHP used to support POSIX-style regular expressions, but they have been deprecated.) Consult the MySQL manual for full details if needed.

You can test multiple criteria using the simple operators and the pattern matching syntax and combine them into more complex criteria with AND and OR. For example,

SELECT *FROM OrdersWHERE CustomerID = 3 OR CustomerID = 4;

Retrieving Data from Multiple TablesOften, to answer a question from the database, you need to use data from more than one table. For example, if you wanted to know which customers placed orders this month, you would need to look at the Customers table and the Orders table. If you also wanted to know what, specifically, they ordered, you would also need to look at the Order_Items table.

These items are in separate tables because they relate to separate real-world objects. This is one of the principles of good database design that we described in Chapter 8,「Designing Your Web Database.」

254

Chapter 10  Working with Your MySQL Database 

To put this information together in SQL, you must perform an operation called a join. This simply means joining two or more tables together to follow the relationships between the data. For example, if you want to see the orders that customer Julie Smith has placed, you will need to look at the Customers table to find Julie’s CustomerID and then at the Orders table for orders with that CustomerID.

Although joins are conceptually simple, they are one of the more subtle and complex parts of SQL. Several different types of joins are implemented in MySQL, and each is used for a different purpose.

Simple Two-Table JoinsLet’s begin by looking at some SQL for the query about Julie Smith we just discussed:

SELECT Orders.OrderID, Orders.Amount, Orders.DateFROM Customers, OrdersWHERE Customers.Name = 'Julie Smith' and Customers.CustomerID = Orders.CustomerID;

The output of this query is

+---------+--------+------------+| OrderID | Amount | Date       |+---------+--------+------------+|       2 |  49.99 | 2007-04-15 |+---------+--------+------------+1 row in set (0.02 sec)

There are a few things to notice here. First, because information from two tables is needed to answer this query, you must list both tables.

By listing two tables, you also specify a type of join, possibly without knowing it. The comma between the names of the tables is equivalent to typing INNER JOIN or CROSS JOIN. This is a type of join sometimes also referred to as a full join, or the Cartesian product of the tables. It means,「Take the tables listed, and make one big table. The big table should have a row for each possible combination of rows from each of the tables listed, whether that makes sense or not.」In other words, you get a table, which has every row from the customers table matched up with every row from the Orders table, regardless of whether a particular customer placed a particular order.

That brute-force approach doesn’t make a lot of sense in most cases. Often what you want is to see the rows that really do match—that is, the orders placed by a particular customer matched up with that customer.

You achieve this result by placing a join condition in the WHERE clause. This special type of conditional statement explains which attributes show the relationship between the two tables. In this case, the join condition is

Customers.CustomerID = Orders.CustomerID

which tells MySQL to put rows in the result table only if the CustomerID from the Customers table matches the CustomerID from the Orders table.

Retrieving Data from the Database

255

By adding this join condition to the query, you actually convert the join to a different type, called an equi-join.

Also notice the dot notation used to make it clear which table a particular column comes from; that is, Customers.CustomerID refers to the CustomerID column from the Customers table, and Orders.CustomerID refers to the CustomerID column from the Orders table.

This dot notation is required if the name of a column is ambiguous—that is, if it occurs in more than one table. As an extension, it can also be used to disambiguate column names from different databases. This example uses a table.column notation, but you can specify the  database with a database.table.column notation, for example, to test a condition such as

books.Orders.CustomerID = other_db.Orders.CustomerID

You can, however, use the dot notation for all column references in a query. Using this notation can be a good idea, particularly when your queries begin to become complex. MySQL doesn’t require it, but it does make your queries much more humanly readable and maintainable. Notice that we followed this convention in the rest of the previous query, for example, with the use of the condition

Customers.Name = 'Julie Smith'

The column Name occurs only in the table Customers, so we do not really need to specify what table it is from. MySQL will not be confused. For humans, though, the column Name on its own is vague, so it does make the meaning of the query clearer when you specify it as Customers.Name.

Joining More Than Two TablesJoining more than two tables is no more difficult than a two-table join. As a general rule, you need to join tables in pairs with join conditions. Think of it as following the relationships between the data from table to table to table.

For example, if you want to know which customers have ordered books on Java (perhaps so you can send them information about a new Java book), you need to trace these relationships through quite a few tables.

You need to find customers who have placed at least one order that included an Order_Item that is a book about Java. To get from the Customers table to the Orders table, you can use the CustomerID as shown previously. To get from the Orders table to the Order_Items table, you can use the OrderID. To get from the Order_Items table to the specific book in the Books table, you can use the ISBN. After making all those links, you can test for books with Java in the title and return the names of customers who bought any of those books.

Let’s look at a query that does all those things:

SELECT Customers.NameFROM Customers, Orders, Order_Items, BooksWHERE Customers.CustomerID = Orders.CustomerIDAND Orders.OrderID = Order_Items.OrderIDAND Order_Items.ISBN = Books.ISBNAND Books.Title LIKE '%Java%'; 

256

Chapter 10  Working with Your MySQL Database 

This query returns the following output:

+-----------------+| Name            |+-----------------+| Michelle Arthur |+-----------------+1 row in set (0.01 sec)

Notice that this example traces the data through four different tables, and to do this with an equi-join, you need three different join conditions. It is generally true that you need one join condition for each pair of tables that you want to join, and therefore a total of join conditions one less than the total number of tables you want to join. This rule of thumb can be useful for debugging queries that don’t quite work. Check off your join conditions and make sure you’ve followed the path all the way from what you know to what you want to know.

Finding Rows That Don’t MatchThe other main type of join that you will use in MySQL is the left join.

In the previous examples, notice that only the rows where a match was found between the tables were included. Sometimes you may specifically want the rows where there’s no match—for example, customers who have never placed an order or books that have never been ordered.

One way to answer this type of question in MySQL is to use a left join. This type of join matches up rows on a specified join condition between two tables. If no matching row exists in the right table, a row will be added to the result that contains NULL values in the right columns.

Let’s look at an example:

SELECT Customers.CustomerID, Customers.Name, Orders.OrderIDFROM Customers LEFT JOIN OrdersON Customers.CustomerID = Orders.CustomerID;

This SQL query uses a left join to join Customers with Orders. Notice that the left join uses a slightly different syntax for the join condition; in this case, the join condition goes in a special ON clause of the SQL statement.

The result of this query is

+------------+-----------------+---------+| CustomerID | Name            | OrderID |+------------+-----------------+---------+|          1 | Julie Smith     |       2 ||          2 | Alan Wong       |       3 ||          3 | Michelle Arthur |       1 ||          3 | Michelle Arthur |       4 |+------------+-----------------+---------+4 rows in set (0.00 sec)

Retrieving Data from the Database

257

This output shows only those customers who have non-NULL OrderIDs.

If you want to see only the customers who haven’t ordered anything, you can check for those NULLs in the primary key field of the right table (in this case, OrderID) because that should not be NULL in any real rows:

SELECT Customers.CustomerID, Customers.NameFROM Customers LEFT JOIN OrdersUSING (CustomerID)WHERE Orders.OrderID IS NULL;

In this case, the result is that no rows are returned, because all of our customers have placed an order.

Let’s add a new customer:

INSERT INTO Customers VALUES(NULL, 'George Napolitano', '177 Melbourne Road', 'Coburg');

If we then repeat the left join query, the result is

+------------+-------------------+| CustomerID | Name              |+------------+-------------------+|          4 | George Napolitano |+------------+-------------------+1 row in set (0.00 sec)

As you would expect, because George is a new customer, he is the only one who has not yet placed an order.

Also notice that this example uses a different syntax for the join condition. Left joins support either the ON syntax used in the first example or the USING syntax in the second example. Notice that the USING syntax doesn’t specify the table from which the join attribute comes; for this reason, the columns in the two tables must have the same name if you want to use USING.

You can also answer this type of question by using subqueries. We look at subqueries later in this chapter.

Using Other Names for Tables: AliasesBeing able to refer to tables by other names is often handy and occasionally essential. Other names for tables are called aliases. You can create them at the start of a query and then use them throughout. They are often handy as shorthand. Consider the huge query you saw earlier, rewritten with aliases:

SELECT C.NameFROM Customers AS C, Orders AS O, Order_Items AS OI, Books AS BWHERE C.CustomerID = O.CustomerIDAND O.OrderID = OI.OrderIDAND OI.ISBN = B.ISBNAND B.Title LIKE '%Java%'; 

258

Chapter 10  Working with Your MySQL Database 

As you declare the tables you are going to use, you add an AS clause to declare the alias for that table. You can also use aliases for columns; we return to this approach when we look at  aggregate functions shortly.

You need to use table aliases when you want to join a table to itself. This task sounds more difficult and esoteric than it is. It is useful, if, for example, you want to find rows in the same table that have values in common. If you want to find customers who live in the same city—perhaps to set up a reading group—you can give the same table (Customers) two different aliases:

SELECT C1.Name, C2.Name, C1.CityFROM Customers AS C1, Customers AS C2WHERE C1.City = C2.CityAND C1.Name != C2.Name;

What you are basically doing here is pretending that the table Customers is two different tables, C1 and C2, and performing a join on the City column. Notice that you also need the second condition, C1.Name != C2.Name; this is to avoid each customer coming up as a match to herself.

Summary of JoinsThe different types of joins we have described are summarized in Table 10.2. There are a few others, but these are the main ones you will use.

Table 10.2  Join Types in MySQL

Name

Description

Cartesian product

All combinations of all the rows in all the tables in the join. Used by specifying a comma between table names, and not specifying a WHERE clause.

Full join

Cross join

Inner join

Equi-join

Left join

Same as preceding.

Same as above. Can also be used by specifying the CROSS JOIN  keywords between the names of the tables being joined.

Semantically equivalent to the comma. Can also be specified using the INNER JOIN keywords. Without a WHERE condition, equivalent to a full join. Usually, you specify a WHERE condition as well to make this a true inner join.

Uses a conditional expression with = to match rows from the different tables in the join. In SQL, this is a join with a WHERE clause.

Tries to match rows across tables and fills in nonmatching rows with NULLs. Use in SQL with the LEFT JOIN keywords. Used for finding missing values. You can equivalently use RIGHT JOIN.

Retrieving Data from the Database

259

Retrieving Data in a Particular OrderIf you want to display rows retrieved by a query in a particular order, you can use the ORDER BY clause of the SELECT statement. This feature is handy for presenting output in a good human-readable format.

The ORDER BY clause sorts the rows on one or more of the columns listed in the SELECT clause. For example,

SELECT Name, AddressFROM CustomersORDER BY Name;

This query returns customer names and addresses in alphabetical order by name, like this:

+-------------------+--------------------+| Name              | Address            |+-------------------+--------------------+| Alan Wong         | 1/47 Haines Avenue || George Napolitano | 177 Melbourne Road || Julie Smith       | 25 Oak Street      || Michelle Arthur   | 357 North Road     |+-------------------+--------------------+4 rows in set (0.00 sec)

Notice that in this case, because the names are in firstname, lastname format, they are  alphabetically sorted on the first name. If you wanted to sort on last names, you would need to have them as two different fields.

The default ordering is ascending (a to z or numerically upward). You can specify this if you like by using the ASC keyword:

SELECT Name, AddressFROM CustomersORDER BY Name ASC;

You can also do it in the opposite order by using the DESC (descending) keyword:

SELECT Name, AddressFROM CustomersORDER BY Name DESC;

In addition, you can sort on more than one column. You can also use column aliases or even their position numbers (for example, 3 is the third column in the table) instead of names.

Grouping and Aggregating DataYou may often want to know how many rows fall into a particular set or the average value of some column—say, the average dollar value per order. MySQL has a set of aggregate functions that are useful for answering this type of query.

260

Chapter 10  Working with Your MySQL Database 

These aggregate functions can be applied to a table as a whole or to groups of data within a table. The most commonly used ones are listed in Table 10.3.

Table 10.3  Aggregate Functions in MySQL

Name

Description

AVG(column) 

Average of values in the specified column.

COUNT(items) 

If you specify a column, this will give you the number of non-NULL values in that column. If you add the word DISTINCT in front of the column name, you will get a count of the distinct values in that column only. If you specify COUNT(*), you will get a row count regardless of NULL values.

MIN(column)

MAX(column) 

STD(column)

Minimum of values in the specified column.

Maximum of values in the specified column.

Standard deviation of values in the specified column.

STDDEV(column)

Same as STD(column).

SUM(column) 

Sum of values in the specified column.

Let’s look at some examples, beginning with the one mentioned earlier. You can calculate the average total of an order like this:

SELECT AVG(Amount)FROM Orders;

The output is something like this:

+-------------+| AVG(Amount) |+-------------+|   54.985002 |+-------------+1 row in set (0.02 sec)

To get more detailed information, you can use the GROUP BY clause. It enables you to view the average order total by group—for example, by customer number. This information tells you which of your customers places the biggest orders:

SELECT CustomerID, AVG(Amount)FROM OrdersGROUP BY CustomerID;

When you use a GROUP BY clause with an aggregate function, it actually changes the behavior of the function. Instead of giving an average of the order amounts across the table, this query gives the average order amount for each customer (or, more specifically, for each CustomerID):

Retrieving Data from the Database

261

+------------+-------------+| CustomerID | AVG(Amount) |+------------+-------------+|          1 |   49.990002 ||          2 |   74.980003 ||          3 |   47.485002 |+------------+-------------+3 rows in set (0.00 sec)

Here’s one point to note when using grouping and aggregate functions: In ANSI SQL, if you use an aggregate function or GROUP BY clause, the only things that can appear in your SELECT clause are the aggregate function(s) and the columns named in the GROUP BY clause. Also, if you want to use a column in a GROUP BY clause, it must be listed in the SELECT clause.

MySQL actually gives you a bit more leeway here. It supports an extended syntax, which enables you to leave items out of the SELECT clause if you don’t actually want them.

In addition to grouping and aggregating data, you can actually test the result of an aggregate by using a HAVING clause. It comes straight after the GROUP BY clause and is like a WHERE that applies only to groups and aggregates.

To extend the previous example, if you want to know which customers have an average order total of more than $50, you can use the following query:

SELECT CustomerID, AVG(Amount)FROM OrdersGROUP BY CustomerIDHAVING AVG(Amount) > 50;

Note that the HAVING clause applies to the groups. This query returns the following output:

+------------+-------------+| CustomerID | AVG(Amount) |+------------+-------------+|          2 |   74.980003 |+------------+-------------+1 row in set (0.06 sec)

Choosing Which Rows to ReturnOne clause of the SELECT statement that can be particularly useful in Web applications is LIMIT. It is used to specify which rows from the output should be returned. This clause takes one or two parameters. If you provide one parameter, it specifies the number of rows to be returned. For example, the following query

SELECT NameFROM CustomersLIMIT 2;

262

Chapter 10  Working with Your MySQL Database 

produces this result:

+-------------+| Name        |+-------------+| Julie Smith || Alan Wong   |+-------------+2 rows in set (0.00 sec)

However, if you provide two parameters, the first one specifies the row number from which to start, and the second one specifies the number of rows to return. 

This query illustrates the second use of LIMIT:

SELECT NameFROM CustomersLIMIT 2,3;

This query can be read as,「Select name from customers, and then return 3 rows, starting from row 2 in the output.」Note that row numbers are zero indexed; that is, the first row in the output is row number zero. This feature is very useful for Web applications, such as when the customer is browsing through products in a catalog, and you want to show 10 items on each page. Note, however, that LIMIT is not part of ANSI SQL. It is a MySQL extension, so using it makes your SQL incompatible with many other RDBMSs.

Using SubqueriesA subquery is a query that is nested inside another query. Although most subquery functionality can be obtained with careful use of joins and temporary tables, subqueries are often easier to read and write.

Basic SubqueriesThe most common use of subqueries is to use the result of one query in a comparison in another query. For example, if you wanted to find the order in which the amount ordered was the largest of any of the orders, you could use the following query:

SELECT CustomerID, AmountFROM OrdersWHERE Amount = (SELECT MAX(Amount) FROM Orders);

This query gives the following results:

+------------+--------+| CustomerID | Amount |+------------+--------+|          2 |  74.98 |+------------+--------+1 row in set (0.03 sec)

Retrieving Data from the Database

263

In this case, a single value is returned from the subquery (the maximum amount) and then used for comparison in the outer query. This is a good example of subquery use because this particular query cannot be elegantly reproduced using joins in ANSI SQL.

The same output, however, produced by this join query:

SELECT CustomerID, AmountFROM OrdersORDER BY Amount DESCLIMIT 1;

Because it relies on LIMIT, this query is not compatible with most RDBMSs.

One of the main reasons that MySQL did not get subqueries for so long was that there is very little that you cannot do without them.

You can use subquery values in this way with all the normal comparison operators. Some special subquery comparison operators are also available and are detailed in the next section.

Subqueries and OperatorsThere are five special subquery operators. Four are used with regular subqueries, and one (EXISTS) is usually used only with correlated subqueries and is covered in the next section. The four regular subquery operators are shown in Table 10.4.

Table 10.4  Subquery Operators

Name

ANY

IN

SOME

ALL

Sample Syntax

Description

SELECT c1 FROM t1 WHERE c1 >ANY (SELECT c1 FROM t2);

Returns true if the comparison is true for any of the rows in the subquery 

SELECT c1 FROM t1WHERE c1 IN (SELECT c1 from t2);

Equivalent to =ANY

SELECT c1 FROM t1 WHERE c1 >SOME (SELECT c1 FROM t2);!

Alias for ANY; sometimes reads better to the human ear

SELECT c1 FROM t1 WHERE c1 >ALL (SELECT c1 from t2);

Returns true if the comparison is true for all of the rows in the subquery

Each of these operators can appear only after a comparison operator, except for IN, which has its comparison operator (=)「rolled in,」so to speak.

264

Chapter 10  Working with Your MySQL Database 

Correlated SubqueriesThere is a special type of subqueries known as correlated subqueries. In these, you can use items from the outer query in the inner query. For example,

SELECT ISBN, TitleFROM BooksWHERE NOT EXISTS(SELECT  * FROM Order_Items WHERE Order_Items.ISBN = Books.ISBN);

This query illustrates both the use of correlated subqueries and the use of the last special subquery operator, EXISTS. It retrieves any books that have never been ordered. Note that the inner query includes only the Order_Items table in the FROM list but refers to Books.ISBN. In other words, the inner query refers to data in the outer query. This is the definition of a correlated subquery: You are looking for inner rows that match (or in this case don’t match) the outer rows.

The EXISTS operator returns true if there are any matching rows in the subquery. Conversely, NOT EXISTS returns true if there are no matching rows in the subquery.

Row SubqueriesAll the subqueries so far have returned a single value, although in many cases this value is true or false (as with the preceding example using EXISTS). Row subqueries return an entire row, which can then be compared to entire rows in the outer query. This approach is generally used to look for rows in one table that also exist in another table. There is not a good example of this in the books database, but a generalized example of the syntax could be something like the following:

SELECT c1, c2, c3FROM t1WHERE (c1, c2, c3) IN (SELECT c1, c2, c3 FROM t2);

Using a Subquery as a Temporary TableYou can use a subquery in the FROM clause of an outer query. This approach effectively allows you to query the output of the subquery, treating it as a temporary table.

In its simplest form, this is something like

SELECT * FROM(SELECT CustomerID, Name FROM Customers WHERE City = 'Box Hill')AS box_hill_customers;

Note that we put the subquery in the FROM clause here. Immediately after the subquery’s closing parenthesis, you must give the results of the subquery an alias. You can then treat it like any other table in the outer query.

Altering Tables After Creation

265

Updating Records in the DatabaseIn addition to retrieving data from the database, you often want to change it. For example, you might want to increase the prices of books in the database. You can do this using an UPDATE statement.

The usual form of an UPDATE statement is

UPDATE [LOW_PRIORITY] [IGNORE] tablenameSET column1=expression1[,column2=expression2,...][WHERE condition][ORDER BY order_criteria][LIMIT number]

The basic idea is to update the table called tablename, setting each of the columns named to the appropriate expression. You can limit an UPDATE to particular rows with a WHERE clause and limit the total number of rows to affect with a LIMIT clause. ORDER BY is usually used only in conjunction with a LIMIT clause; for example, if you are going to update only the first 10 rows, you want to put them in some kind of order first. LOW_PRIORITY and IGNORE, if specified, work the same way as they do in an INSERT statement.

Let’s look at some examples. If you want to increase all the book prices by 10%, you can use an UPDATE statement without a WHERE clause:

UPDATE BooksSET Price = Price * 1.1;

If, on the other hand, you want to change a single row—say, to update a customer’s address—you can do it like this:

UPDATE CustomersSET Address = '250 Olsens Road'WHERE CustomerID = 4;

Altering Tables After CreationIn addition to updating rows, you might want to alter the structure of the tables within your database. For this purpose, you can use the flexible ALTER TABLE statement. The basic form of this statement is

ALTER TABLE [IGNORE] tablename alteration [, alteration ...]

Note that in ANSI SQL you can make only one alteration per ALTER TABLE statement, but MySQL allows you to make as many as you like. Each of the alteration clauses can be used to change different aspects of the table.

If the IGNORE clause is specified and you are trying to make an alteration that causes duplicate primary keys, the first one will go into the altered table and the rest will be deleted. If it is not specified (the default), the alteration will fail and be rolled back.

266

Chapter 10  Working with Your MySQL Database 

The most common alterations you can make with this statement are shown in Table 10.5.

Table 10.5  Possible Changes with the ALTER TABLE Statement

Syntax

Description

ADD [COLUMN] column_description [FIRST | AFTER column ] 

Adds a new column in the specified location (if not specified, then the column goes at the end). Note that column_description needs a name and a type, just as in a CREATE  statement. 

ADD [COLUMN] (column_description, column_description,...)

Adds one or more new columns at the end of the table.

ADD INDEX [index] (column,...)

ADD [CONSTRAINT [symbol]]PRIMARY KEY (column,...)

ADD UNIQUE [CONSTRAINT [symbol]] [index] (column,...)

Adds an index to the table on the specified column or columns.

Makes the specified column or columns the primary key of the table. The CONSTRAINT notation is for tables using foreign keys. See Chapter 13, 」Advanced MySQL Programming,」for more details.

Adds a unique index to the table on the specified column or columns. The CONSTRAINT notation is for tables using foreign keys. See Chapter 13 for more details.

ADD [CONSTRAINT [symbol]]

Adds a foreign key to a table. 

FOREIGN KEY [index] (index_col,...) [reference_definition]

ALTER [COLUMN] column[SET DEFAULTvalue | DROP DEFAULT]

CHANGE [COLUMN] column new_column description

MODIFY [COLUMN] column_description

See Chapter 13 for more details.

Adds or removes a default value for a particular column.

Changes the column called column so that it has the description listed. Note that this syntax can be used to change the name of a column because a column_description includes a name.

Similar to CHANGE. Can be used to change column types, not names.

DROP [COLUMN] column

Deletes the named column.

Altering Tables After Creation

267

DROP PRIMARY KEY

DROP INDEX index

DROP FOREIGN KEY key

DISABLE KEYS

ENABLE KEYS

Deletes the primary index (but not the column).

Deletes the named index.

Deletes the foreign key (but not the column).

Turns off index updating.

Turns on index updating.

RENAME [AS] new_table_name

Renames a table.

ORDER BY col_name

CONVERT TO CHARACTER SET cs COLLATE c

 [DEFAULT] CHARACTER SET csCOLLATE c

DISCARD TABLESPACE

IMPORT TABLESPACE

table_options

Re-creates the table with the rows in a particular order. (Note that after you begin changing the table, the rows will no longer be in order.)

Converts all text-based columns to the specified character set and collation.

Sets the default character set and collation.

Deletes the underlying tablespace file for an InnoDB table. (See Chapter 13 for more details on InnoDB.)

Re-creates the underlying tablespace file for an InnoDB table. (See Chapter 13 for more details on InnoDB.)

Allows you to reset the table options. Uses the same syntax as CREATE TABLE.

Let’s look at a few of the more common uses of ALTER TABLE.

You may frequently realize that you haven’t made a particular column「big enough」for the data it has to hold. For example, previously in the customers table, you allowed names to be 50 characters long. After you start getting some data, you might notice that some of the names are too long and are being truncated. You can fix this problem by changing the data type of the column so that it is 70 characters long instead:

ALTER TABLE CustomersMODIFY Name CHAR(70) NOT NULL;

Another common occurrence is the need to add a column. Imagine that a sales tax on books is introduced locally and that Book-O-Rama needs to add the amount of tax to the total order but keep track of it separately. You can add a Tax column to the Orders table as follows:

ALTER TABLE OrdersADD Tax FLOAT(6,2) AFTER Amount;

268

Chapter 10  Working with Your MySQL Database 

Getting rid of a column is another case that comes up frequently. You can delete the column you just added as follows:

ALTER TABLE OrdersDROP Tax;

Deleting Records from the DatabaseDeleting rows from the database is simple. You can do this using the DELETE statement, which generally looks like this:

DELETE [LOW_PRIORITY] [QUICK] [IGNORE] FROM table[WHERE condition][ORDER BY order_cols][LIMIT number]

If you write

DELETE FROM table;

on its own, all the rows in a table will be deleted, so be careful. Usually, you want to delete specific rows, and you can specify the ones you want to delete with a WHERE clause. You might do this, if, for example, a particular book were no longer available or if a particular customer hadn’t placed any orders for a long time and you wanted to do some housekeeping:

DELETE FROM CustomersWHERE CustomerID=5;

The LIMIT clause can be used to limit the maximum number of rows that are actually deleted. ORDER BY is usually used in conjunction with LIMIT.

LOW_PRIORITY and IGNORE work as they do elsewhere. QUICK may be faster on MyISAM tables.

Dropping TablesAt times, you may want to get rid of an entire table. You can do this with the DROP TABLE statement. This process is simple, and it looks like this:

DROP TABLE table;

This query deletes all the rows in the table and the table itself, so be careful using it.

Dropping a Whole DatabaseYou can go even further and eliminate an entire database with the DROP DATABASE statement, which looks like this:

DROP DATABASE database;

Next

269

This query deletes all the rows, all the tables, all the indexes, and the database itself, so it goes without saying that you should be somewhat careful using this statement.

Further ReadingIn this chapter, we provided an overview of the day-to-day SQL you will use when interacting with a MySQL database. In the next two chapters, we describe how to connect MySQL and PHP so that you can access your database from the Web. We also explore some advanced MySQL techniques.

If you want to know more about SQL, you can always fall back on the ANSI SQL standard for a little light reading. It’s available from http://www.ansi.org/.

For more details on the MySQL extensions to ANSI SQL, you can look at the MySQL website at http://www.mysql.com.

NextIn Chapter 11,「Accessing Your MySQL Database from the Web with PHP,」we cover how to make the Book-O-Rama database available over the web.

This page intentionally left blank 


13Advanced MySQL Programming

In this chapter, you learn about some more advanced MySQL topics, including table types, transactions, and stored procedures.

Key topics covered in this chapter include

 ■ The LOAD DATA INFILE statement

 ■ Storage engines

 ■ Transactions

 ■ Foreign keys

 ■ Stored procedures

The LOAD DATA INFILE StatementOne useful feature of MySQL that we have not yet discussed is the LOAD DATA INFILE  statement. You can use it to load table data in from a file. It executes very quickly.

This flexible command has many options, but typical usage is something like the following:

LOAD DATA INFILE "newbooks.txt" INTO TABLE books;

This line reads row data from the file newbooks.txt into the table books. (This assumes the books database is in use. You may also specify the database.table notation.) By default, data fields in the file must be separated by tabs and enclosed in single quotation marks, and each row must be separated by a newline (\n). Special characters must be escaped out with a slash (\). All these characteristics are configurable with the various options of the LOAD statement; see the MySQL manual for more details.

To use the LOAD DATA INFILE statement, a user must have the FILE privilege discussed in Chapter 9,「Creating Your Web Database.」

316

Chapter 13  Advanced MySQL Programming

Storage EnginesMySQL supports a number of different storage engines, sometimes also called table types. This means that you have a choice about the underlying implementation of the tables. Each table in your database can use a different storage engine, and you can easily convert between them.

You can choose a table type when you create a table by using

CREATE TABLE table TYPE=type ....

The commonly available table types are

 ■ InnoDB—This type is the default and is the storage engine you should use for most 

applications. These tables are transaction safe; that is, they provide COMMIT and ROLLBACK capabilities. InnoDB tables also support foreign keys. They have the best read-write performance, at least partly because they support row-level locking.

 ■ MyISAM—This type used to be the default in older versions of MySQL. It is based on 

the traditional ISAM type, which stands for Indexed Sequential Access Method, a standard method for storing records and files. MyISAM adds a number of advantages over the ISAM type. MyISAM tables can be compressed, and they support full text searching. They are not transaction safe and do not support foreign keys. They can outperform InnoDB on low-read or read-only applications, but because they use table-level locking, they do not perform as well as InnoDB on read-write applications.

 ■ MEMORY (previously known as HEAP)—Tables of this type are stored in memory, and their indexes are hashed. This makes MEMORY tables extremely fast, but, in the event of a crash, your data will be lost. These characteristics make MEMORY tables ideal for storing temporary or derived data for read-heavy applications. They support table-level locking so are not ideal for a write-heavy or mixed read-write workload. They cannot have BLOB or TEXT columns.

 ■ MERGE—These tables allow you to treat a collection of MyISAM tables as a single 

table for the purpose of querying. This way, you can work around maximum file size limitations on some operating systems.

 ■ ARCHIVE—These tables store large amounts of data but with a small footprint. Tables 

of this type support only INSERT and SELECT queries, not DELETE, UPDATE, or REPLACE. Additionally, indexes are not used.

 ■ CSV—These tables are stored on the server in a single file containing comma-separated 

values. The benefit of these types of tables only appears when you need to view or otherwise work with the data in an external spreadsheet application such as Microsoft Excel.

In most web applications, you will almost always use InnoDB tables.

You should always use InnoDB when transactions are important, such as for tables storing financial data or for situations in which INSERTs and SELECTs are being interleaved, such as online message boards or forums. You should also always use it when maintaining referential 

Transactions

317

integrity (via foreign keys) is important, which is the case in most applications that require a relational database.

You may choose to use MyISAM in some cases. The typical use of MyISAM is in a dataware-housing application, which is beyond the scope of this book. Also, at the time of writing, the full-text indexing support was more advanced in MyISAM than it was in InnoDB, but InnoDB is likely to catch up in the near future.

You can use MEMORY tables for temporary tables or to implement views, and MERGE tables if you need to deal with very large MyISAM tables.

You can change the type of a table after creation with an ALTER TABLE statement, as follows:

ALTER TABLE Orders ENGINE=innodb;ALTER TABLE  Order_Items ENGINE=innodb;

We will now spend some time focusing on the use of transactions and the way they are imple-mented in InnoDB tables.

TransactionsTransactions are mechanisms for ensuring database consistency, especially in the event of error or a server crash. In the following sections, you learn what transactions are and how to imple-ment them with InnoDB.

Understanding Transaction DefinitionsFirst, let’s define the term transaction. A transaction is a query or set of queries guaranteed either to be completely executed on the database or not executed at all. The database is therefore left in a consistent state whether or not the transaction completed.

To see why this capability might be important, consider a banking database. Imagine the  situation in which you want to transfer money from one account to another. This action involves removing the money from one account and placing it in another, which would involve at least two queries. It is vitally important that either these two queries are both executed or neither is executed. If you take the money out of one account and the power goes out before you put it into another account, what happens? Does the money just disappear?

You may have heard the expression ACID compliance. ACID is a way of describing four  requirements that transactions should satisfy:

 ■ Atomicity—A transaction should be atomic; that is, it should either be completely 

executed or not executed.

 ■ Consistency—A transaction should leave the database in a consistent state.

 ■ Isolation—Uncompleted transactions should not be visible to other users of the database; 

that is, until transactions are complete, they should remain isolated.

 ■ Durability—Once written to the database, a transaction should be permanent or durable.

318

Chapter 13  Advanced MySQL Programming

A transaction that has been permanently written to the database is said to be committed. A transaction that is not written to the database—so that the database is reset to the state it was in before the transaction began—is said to be rolled back.

Using Transactions with InnoDBBy default, MySQL runs in autocommit mode. This means that each statement you execute is immediately written to the database (committed). If you are using a transaction-safe table type, more than likely you don’t want this behavior.

To turn autocommit off in the current session, type

SET AUTOCOMMIT=0;

If autocommit is on, you need to begin a transaction with the statement

START TRANSACTION;

If it is off, you do not need this command because a transaction will be started automatically for you when you enter an SQL statement.

After you have finished entering the statements that make up a transaction, you can commit it to the database by simply typing

COMMIT;

If you have changed your mind, you can revert to the previous state of the database by typing

ROLLBACK;

Until you have committed a transaction, it will not be visible to other users or in other sessions.

Let’s look at an example. 

Open two connections to the books database. In one connection, add a new order record to the database:

INSERT INTO Orders VALUES (5, 2, 69.98, '2008-06-18');INSERT INTO  Order_Items VALUES (5, '0-672-31697-8', 1);

Now check that you can see the new order:

SELECT * FROM Orders WHERE OrderID=5;

You should see the order displayed:

+---------+------------+--------+------------+| OrderID | CustomerID | Amount | Date       |+---------+------------+--------+------------+|       5 |          2 |  69.98 | 2008-06-18 |+---------+------------+--------+------------+1 row in set (0.00 sec)

Foreign Keys

319

Leaving this connection open, go to your other connection and run the same SELECT query. You should not be able to see the order:

Empty set (0.00 sec)

(If you can see it, most likely you forgot to turn off autocommitting. Check this and that you created the table in question using InnoDB.) 

The reason you cannot see it is that the transaction has not yet been committed. (This is a good illustration of transaction isolation in action.)

Now go back to the first connection and commit the transaction:

COMMIT;

You should now be able to retrieve the row in your other connection.

Foreign KeysInnoDB also supports foreign keys. You may recall that we discussed the concept of foreign keys in Chapter 8,「Designing Your Web Database.」

Consider, for example, inserting a row into the order_items table. You need to include a valid orderid. Without foreign keys, you need to ensure the validity of the orderid you insert somewhere in your application logic. Using foreign keys, you can let the database do the  checking for you.

How do you set this up? As you may recall, we created the table initially using a foreign key, as follows:

CREATE TABLE Order_Items( OrderID INT UNSIGNED NOT NULL,  ISBN CHAR(13) NOT NULL,  Quantity TINYINT UNSIGNED,

  PRIMARY KEY (OrderID, ISBN),  FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),  FOREIGN KEY (ISBN) REFERENCES Books(ISBN));  We added the words REFERENCES Orders(OrderID) after OrderID. This means this column is a foreign key that must contain a value from the OrderID column in the Orders table.

To test the foreign key constraints, you can try to insert a row with an OrderID for which there is no matching row in the orders table:

INSERT INTO Order_Items VALUES (77, '0-672-31697-8', 7);

You should receive an error similar to

ERROR 1452 (23000): Cannot add or update a child row: a foreign key constraint fails (`books`.`Order_Items`, CONSTRAINT `Order_Items_ibfk_1` FOREIGN KEY (`OrderID`) REFERENCES `Orders` (`OrderID`))

320

Chapter 13  Advanced MySQL Programming

Stored ProceduresA stored procedure is a programmatic function that is created and stored within MySQL. It can consist of SQL statements and a number of special control structures. It can be useful when you want to perform the same function from different applications or platforms, or as a way of encapsulating functionality. Stored procedures in a database can be seen as analogous to an object-oriented approach in programming. They allow you to control the way data is accessed.

Let’s begin by looking at a simple example.

Basic ExampleListing 13.1 shows the declaration of a stored procedure.

Listing 13.1  basic_stored_procedure.sql—Declaring a Stored Procedure# Basic stored procedure example

DELIMITER //

CREATE PROCEDURE Total_Orders (OUT Total FLOAT)BEGIN SELECT SUM(Amount) INTO Total FROM Orders;END//

DELIMITER ;

Let’s go through this code line by line.

The first statement

DELIMITER //

changes the end-of-statement delimiter from the current value—typically a semicolon unless you have changed it previously—to a double forward slash. You do this so that you can use the semicolon delimiter within the stored procedure as you are entering the code for it without MySQL trying to execute the code as you go.

The next line

CREATE PROCEDURE Total_Orders (OUT Total FLOAT) 

creates the actual procedure. The name of this procedure is Total_Orders. It has a single parameter called Total, which is the value you are going to calculate. The word OUT indicates that this parameter is being passed out or returned.

Parameters can also be declared IN, meaning that a value is being passed into the procedure, or INOUT, meaning that a value is being passed in but can be changed by the procedure.

Stored Procedures

321

The word FLOAT indicates the type of the parameter. In this case, you return a total of all the orders in the Orders table. The type of the Orders column is FLOAT, so the type returned is also FLOAT. The acceptable data types map to the available column types.

If you want more than one parameter, you can provide a comma-separated list of parameters as you would in PHP.

The body of the procedure is enclosed within the BEGIN and END statements. They are  analogous to the curly braces within PHP ({}) because they delimit a statement block.

In the body, you simply run a SELECT statement. The only difference from normal is that you include the clause INTO Total to load the result of the query into the Total parameter.

After you have declared the procedure, you return the delimiter back to being a semicolon with the line

DELIMITER ;

After the procedure has been declared, you can call it using the CALL keyword, as follows:

CALL Total_Orders(@t);

This statement calls the total orders and passes in a variable to store the result. To see the result, you need to then look at the variable:

SELECT @t;

The result should be similar to

+--------------------+| @t                 |+--------------------+| 219.94000244140625 |+--------------------+1 row in set (0.00 sec)

In a way similar to creating a procedure, you can create a function. A function accepts input parameters (only) and returns a single value. 

The basic syntax for this task is almost the same. A sample function is shown in Listing 13.2.

Listing 13.2  basic_function.sql—Declaring a Stored Function# Basic syntax to create a function

DELIMITER //

CREATE FUNCTION Add_Tax (Price FLOAT) RETURNS FLOAT NO SQL  RETURN Price*1.1;

//

DELIMITER ;

322

Chapter 13  Advanced MySQL Programming

As you can see, this example uses the keyword FUNCTION instead of PROCEDURE. There are a couple of other differences.

Parameters do not need to be specified as IN or OUT because they are all IN, or input  parameters. After the parameter list, you can see the clause RETURNS FLOAT. It specifies the type of the return value. Again, this value can be any of the valid MySQL types.

After this you will see the keywords NO SQL. This is the characteristic of the function. Other things you might see in this location are

 ■ DETERMINISTIC or NOT DETERMINISTIC—a deterministic function will, given the same 

parameters, always return the same value.

 ■ NO SQL, CONTAINS SQL, READS SQL DATA, or MODIFIES SQL DATA indicates the 

contents of the function. In this case we have no SQL statements, so the function is NO SQL.

 ■ A comment in single quotes ' and '.

 ■ A language declaration: LANGUAGE SQL.

 ■ SQL SECURITY DEFINER or SQL SECURITY INVOKER defines whether to use the privilege 

level of the definer (declared in the function) or the invoker of the function.

We mention these characteristics here because when you are defining functions, if you have binary logging switched on, you will need to have one of DETERMINISTIC, NO SQL, or READS SQL DATA declared here. This is because functions that write data may be unsafe for recovery and replication, and therefore are not allowed. (You can read more about this in the MySQL manual.)

You return a value using the RETURN statement, much as you would in PHP.

Notice that this example does not use the BEGIN and END statements. You could use them, but they are not required. Just as in PHP, if a statement block contains only one statement, you do not need to mark the beginning and end of it.

Calling a function is somewhat different from calling a procedure. You can call a stored func-tion in the same way you would call a built-in function. For example,

SELECT Add_Tax(100);

This statement should return the following output:

+-------------+| Add_Tax(100) |+-------------+|         110 |+-------------+

After you have defined procedures and functions, you can view the code used to define them by using, for example,

SHOW CREATE PROCEDURE Total_Orders;

Stored Procedures

323

or

SHOW CREATE FUNCTION Add_Tax;

You can delete them with

DROP PROCEDURE Total_Orders;

or

DROP FUNCTION Add_Tax;

Stored procedures come with the ability to use control structures, variables, DECLARE handlers (like exceptions), and an important concept called cursors. We briefly look at each of these in the following sections.

Local VariablesYou can declare local variables within a BEGIN...END block by using a DECLARE statement. For example, you could alter the Add_Tax function to use a local variable to store the tax rate, as shown in Listing 13.3.

Listing 13.3 

 basic_function_with_variables.sql—Declaring a Stored Function with Variables

# Basic syntax to create a function DELIMITER // CREATE FUNCTION Add_Tax (Price FLOAT) RETURNS FLOAT NO SQLBEGIN  DECLARE Tax FLOAT DEFAULT 0.10;  RETURN Price*(1+Tax);END// DELIMITER ;

As you can see, you declare the variable using DECLARE, followed by the name of the  variable, followed by the type. The default clause is optional and specifies an initial value for the  variable.  You then use the variable as you would expect.

Cursors and Control StructuresLet’s consider a more complex example. For this example, you’ll write a stored procedure that works out which order was for the largest amount and returns the OrderID. (Obviously, you could calculate this amount easily enough with a single query, but this simple example illus-trates how to use cursors and control structures.) The code for this stored procedure is shown in Listing 13.4.

324

Chapter 13  Advanced MySQL Programming

Listing 13.4 

 control_structures_cursors.sql—Using Cursors and Loops to Process a Resultset

# Procedure to find the orderid with the largest amount# could be done with max, but just to illustrate stored procedure principles

DELIMITER //

CREATE PROCEDURE Largest_Order (OUT Largest_ID INT)BEGIN  DECLARE This_ID INT;  DECLARE This_Amount FLOAT;  DECLARE L_Amount FLOAT DEFAULT 0.0;  DECLARE L_ID INT;

  DECLARE Done INT DEFAULT 0;  DECLARE C1 CURSOR FOR SELECT OrderID, Amount FROM Orders;  DECLARE CONTINUE HANDLER FOR SQLSTATE '02000' SET Done = 1;

  OPEN C1;  REPEAT    FETCH C1 INTO This_ID, This_Amount;    IF NOT Done THEN      IF This_Amount > L_Amount THEN        SET L_Amount=This_Amount;        SET L_ID=This_ID;      END IF;    END IF;   UNTIL Done END REPEAT;  CLOSE C1;

  SET LARGEST_ID=L_ID;

END//

DELIMITER ;

This code uses control structures (both conditional and looping), cursors, and handlers. Let’s consider it line by line.

At the start of the procedure, you declare a number of local variables for use within the procedure. The variables This_ID and This_Amount store the values of OrderID and Amount in the current row. The variables L_Amount and L_ID are for storing the largest order amount and the corresponding ID. Because you will work out the largest amount by comparing each value to the current largest value, you initialize this variable to zero.

Stored Procedures

325

The next variable declared is Done, initialized to zero (false). This variable is your loop flag. When you run out of rows to look at, you set this variable to 1 (true).

The next thing is a cursor. A cursor is not dissimilar to an array; it retrieves a resultset for a query (such as returned by mysqli_query()) and allows you to process it a single line at a time (as you would with, for example, mysqli_fetch_row()). Consider this cursor:

DECLARE C1 CURSOR FOR SELECT OrderID, Amount FROM Orders;

This cursor is called C1. This is just a definition of what it will hold. The query will not be executed yet.

The line

DECLARE CONTINUE HANDLER FOR SQLSTATE '02000' SET Done = 1;

is called a declare handler. It is similar to an exception in stored procedures. Also available are continue handlers and exit handlers. Continue handlers, like the one shown, take the action specified and then continue execution of the procedure. Exit handlers exit from the nearest BEGIN...END block.

The next part of the declare handler specifies when the handler will be called. In this case, it will be called when SQLSTATE '02000' is reached. You may wonder what that means because it seems very cryptic. This means it will be called when no rows are found. You process a result-set row by row, and when you run out of rows to process, this handler will be called. You could also specify FOR NOT FOUND equivalently. Other options are SQLWARNING and SQLEXCEPTION.

The next line

OPEN C1;

actually runs the query. To obtain each row of data, you must run a FETCH statement. You do this in a REPEAT loop. In this case, the loop looks like this:

REPEAT...UNTIL DONE END REPEAT;

Note that the condition (UNTIL DONE) is not checked until the end. Stored procedures also support WHILE loops, of the form

WHILE condition DO...END WHILE;

There are also LOOP loops, of the form

LOOP...END LOOP

These loops have no built-in conditions but can be exited by means of a LEAVE; statement.

Note that there are no FOR loops.

326

Chapter 13  Advanced MySQL Programming

Continuing with the example, the next line of code fetches a row of data:

FETCH C1 INTO This_ID, This_Amount;

This line retrieves a row from the cursor query. The two attributes retrieved by the query are stored in the two specified local variables.

You check whether a row was retrieved and then compare the current loop amount with the largest stored amount, by means of two IF statements:

    IF NOT Done THEN      IF This_Amount > L_Amount THEN        SET L_Amount=This_Amount;        SET L_ID=This_ID;      END IF;    END IF;

Note that variable values are set by means of the SET statement.

In addition to IF...THEN, stored procedures also support an IF...THEN...ELSE construct with the following form:

IF condition THEN    ...    [ELSEIF condition THEN]    ...    [ELSE]    ...END IF

There is also a CASE statement, which has the following form:

CASE value    WHEN value THEN statement    [WHEN value THEN statement ...]    [ELSE statement]END CASE

Back to the example, after the loop has terminated, you have a little cleaning up to do:

CLOSE C1;SET LARGEST_ID=L_ID;

The CLOSE statement closes the cursor.

Finally, you set the OUT parameter to the value you have calculated. You cannot use the param-eter as a temporary variable, only to store the final value. (This usage is similar to some other programming languages, such as Ada.)

If you create this procedure as described here, you can call it as you did the other procedure:

CALL Largest_Order(@l);SELECT @l;

Triggers

327

You should get output similar to the following:

+------+| @l   |+------+| 3    |+------+1 row in set (0.00 sec)

You can check for yourself that the calculation is correct.

TriggersTriggers are a type of event-driven stored routine or callback, if you prefer. They are code associated with a particular table that is invoked when a particular action is taken on that table.

The basic form of a trigger is as follows:

CREATE TRIGGER trigger_name {BEFORE | AFTER} {INSERT | UPDATE | DELETE} ON table[order]FOR EACH ROWBEGIN   …END

The first line names the trigger to be created. The combination of the timing (BEFORE or AFTER) and the event that invokes the trigger (INSERT, UPDATE, or DELETE on the named table) specify when the code in the body of the trigger will run.

The optional order clause allows you to run more than one trigger on a particular time/event combination. The format of this clause is

{FOLLOWS | PRECEDES} other_trigger

The FOR EACH ROW clause means that the trigger is executed for each affected row in the  triggering query.

Let’s look at a simple example. This code is shown in Listing 13.5.

Listing 13.5 

 trigger.sql—When Deleting an Order, First Make Sure to Delete Each of the Items in That Order

# Trigger example

DELIMITER //

# delete order_items before order to avoid referential integrity errorCREATE TRIGGER Delete_Order_Items BEFORE DELETE ON Orders FOR EACH ROW

328

Chapter 13  Advanced MySQL Programming

BEGIN  DELETE FROM Order_Items WHERE OLD.OrderID = OrderID;END //

DELIMITER ;

This trigger is invoked when we try to delete an order. For an order containing Order_Items, this would normally cause a referential integrity error. In this case, we want to delete the Order_Items that are part of that order first.

You can see this is triggered before delete on orders. What the code does in the body is to delete each Order_Item with a matching OrderID. We use another special piece of syntax here: the OLD keyword. This means「use the value of this column before the invoking query runs.」There is also a NEW keyword.

To test the trigger, let's look at the data in the Order_Items table:

+---------+---------------+----------+| OrderID | ISBN          | Quantity |+---------+---------------+----------+|       1 | 0-672-31697-8 |        2 ||       2 | 0-672-31769-9 |        1 ||       3 | 0-672-31509-2 |        1 ||       3 | 0-672-31769-9 |        1 ||       4 | 0-672-31745-1 |        3 ||       5 | 0-672-31697-8 |        1 |+---------+---------------+----------+5 rows in set (0.00 sec)

Now, let's delete the order with OrderID 3:

DELETE FROM Orders WHERE OrderID=3;

On examining the Order_Items table, you should see that all the Order_Items with an OrderID of 3 have been deleted:

+---------+---------------+----------+| OrderID | ISBN          | Quantity |+---------+---------------+----------+|       1 | 0-672-31697-8 |        2 ||       2 | 0-672-31769-9 |        1 ||       4 | 0-672-31745-1 |        3 ||       5 | 0-672-31697-8 |        1 |+---------+---------------+----------+4 rows in set (0.00 sec)

This is a simple but useful example. 

Next

329

Other common uses of triggers are to reformat data, or to log an audit trail recording what changes were made, when, and by whom.

Further ReadingIn this chapter, we took a cook’s tour of the stored procedure and trigger functionality. You can find out more about stored procedures and triggers in the MySQL manual. 

For more information on LOAD DATA INFILE, the different storage engines, and stored proce-dures, also consult the MySQL manual.

If you want to find out more about transactions and database consistency, we recommend a good basic relational database text such as An Introduction to Database Systems by C. J. Date.

NextWe have now covered the fundamentals of PHP and MySQL. In Part III of this book,「Web Application Security,」we look at the security aspects of creating and running a web application.


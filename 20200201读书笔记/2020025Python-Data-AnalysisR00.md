# 2020025Python-Data-AnalysisR00

## 记忆时间

## 卡片

### 0101. 主题卡 ——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡 ——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡 ——

行动卡是能够指导自己的行动的卡。

### 0601. 数据信息卡 ——

### 0701. 任意卡 ——

最后还有一张任意卡，记录个人阅读感想。

## 前言

Governments, scientists, industry, and individuals have a growing need to learn from data Data analysis has gained popularity lately due to the hype around Data Science. Data analysis and Data Science attempt to extract information from data. For that purpose, we use techniques from statistics, machine learning, signal processing, natural language processing, and computer science.

This book starts as a tutorial on NumPy, SciPy, matplotlib, and pandas. These are open source Python packages useful for numerical work, data wrangling, and visualization. Combined, they can compete with MATLAB, Mathematica, and R. The second half of the book teaches more advanced topics such as signal processing, databases, text analysis, machine learning, interoperability, and performance tuning.

Chapter 1, Getting Started with Python Libraries, guides us to achieve a successful installation of the numerical Python software and set it up step by step. Also, we will create a small application.

Chapter 2, NumPy Arrays, introduces us to NumPy fundamentals and arrays. By the end of this chapter, we will have basic understanding of NumPy arrays and the associated functions.

Chapter 3, Statistics and Linear Algebra, gives a quick overview of linear algebra and statistical functions.

Chapter 4, pandas Primer, provides a tutorial on basic pandas functionality where we learn about pandas data structures and operations.

Chapter 5, Retrieving, Processing, and Storing Data, explains how to acquire data in various formats and how to clean raw data and store it.

Chapter 6, Data Visualization, teaches how to plot data with matplotlib.

Chapter 7, Signal Processing and Time Series, contains time series and signal processing examples using sunspot cycles data. The examples mostly use NumPy/SciPy, along with statsmodels in at least one example.

Chapter 8, Working with Databases, provides information about various databases (relational and NoSQL) and related APIs.

Chapter 9, Analyzing Textual Data and Social Media, analyzes texts for sentiment analysis and topics extraction. A small example is also given of network analysis.

Chapter 10, Predictive Analytics and Machine Learning, explains artificial intelligence with weather prediction as a running example and mostly uses scikit-learn. However, some machine learning algorithms are not covered by scikit-learn, so for those, we use other APIs.

Chapter 11, Environments Outside the Python Ecosystem and Cloud Computing, gives various examples on how to integrate existing code not written in Python. Also, setup in the Cloud will be demonstrated.

Chapter 12, Performance Tuning, Profiling, and Concurrency, gives hints on improving performance with profiling and Cythoning as key techniques. For multicore, distributed systems, we discuss the relevant frameworks too.

Appendix A, Key Concepts, serves as a glossary containing short descriptions of key concepts found throughout the book.

Appendix B, Useful Functions, gives an overview of functions used in the book. 

Appendix C, Online Resources, lists links to documentation, forums, articles, and other important information.

This book is for people with basic knowledge of Python and Mathematics who want to learn how to use Python software to analyze data. We try to keep things simple, but it's not possible to cover all the topics in great detail. It may be useful for you to refresh your knowledge of Mathematics via Khan Academy, Coursera, or Wikipedia. I would recommend the following books by Packt Publishing for further reading:

Building Machine Learning Systems with Python, Willi Richert and Luis Pedro Coelho (2013)

Learning Cython Programming, Philip Herron (2013)

Learning NumPy Array, Ivan Idris (2014)

Learning scikit-learn: Machine Learning in Python, Raúl Garreta and Guillermo Moncecchi (2013)

Learning SciPy for Numerical and Scientific Computing, Francisco J. Blanco-Silva (2013)

Matplotlib for Python Developers, Sandro Tosi (2009)

NumPy Beginner's Guide - Second Edition, Ivan Idris (2013)

NumPy Cookbook, Ivan Idris (2012)

Parallel Programming with Python, Jan Palach (2014)

Python Data Visualization Cookbook, Igor Milovanović (2013)

Python for Finance, Yuxing Yan (2014)

Python Text Processing with NLTK 2.0 Cookbook, Jacob Perkins (2010)

2『上面的书去收集。』——未完成

## 提炼汇总

8、如何使用 sqlite3。先建立连接，再建个「光标」，通过方法 c.execute() 创建一个新表，List the SQLite tables，写入数据，提取数据，丢弃数据；通过 pandas 连接数据库；如何新建一个 SQLAlchemy，并且通过 SQLAlchemy 来操作、访问数据库；Pony ORM is another Python ORM package；Storing data in Redis，Redis 的特点是快，数据存储结构类似于 Python 里的字典；Apache Cassandra，面向「行」的，即表里每行的数据可以有不同的列。

## 0701. Signal Processing and Time Series

In this chapter, the time series examples used annual sunspot cycles data. You learned that it's common to try to derive a relationship between a value and another data point or combination of data points a fixed number of periods in the past, in the same time series.

A moving average specifies a window of previously seen data, which is averaged each time the window slides forward by one period. In the pandas API, the rolling_ window() function provides the window functions functionality with different values of the win_type string parameter corresponding to different window functions.

Cointegration is similar to correlation and is a metric to define the relatedness of two time series. In regression setups, we frequently encounter the problem of overfitting. This issue arises when we have a perfect fit for a sample, which performs poorly when we introduce new data points. To evaluate a model, we can compute appropriate evaluation metrics.

Signal processing is a field of engineering and applied mathematics that analyzes analog and digital signals, corresponding to variables that vary with time. One of the categories of signal processing techniques is time series analysis. A time series is an ordered list of data points starting with the oldest measurements first. The data points are usually equidistant, for instance, consistent with daily or annual sampling. In time series analysis, the order of the values is important. It's common to try to derive a relation between a value and another data point or combination of data points a fixed number of periods in the past, in the same time series. The time series examples in this chapter use annual sunspot cycles data. This data is provided by the statsmodels package (an open source Python project). The examples use NumPy/SciPy, pandas, and also statsmodels.

1『原来 time series analysis 是 Signal processing 的一个种类。这章的数据来源于开源包 statsmodels。』

Moving averages are frequently used to analyze time series. A moving average specifies a window of data that is previously seen, which is averaged each time the window slides forward by one period; The different types of moving averages differ essentially in the weights used for averaging. The exponential moving average, for instance, has exponentially decreasing weights with time; This means that older values have less influence than newer values, which is sometimes desirable. The following code from the moving_average.py file in this book's code bundle plots the simple moving average for the 11- and 22-year sunspots cycles:

```py
import matplotlib.pyplot as plt 
import statsmodels.api as sm 
# from pandas.stats.moments import rolling_mean「rolling_mean has been removed in the new version」
import pandas as pd 

data_loader = sm.datasets.sunspots.load_pandas()
df = data_loader.data 
year_range = df["YEAR"].values

plt.plot(year_range, df["SUNACTIVITY"].values, label="Original")
# plt.plot(year_range, pd.rolling_mean(df, 11)["SUNACTIVITY"].values, label="SMA 11")「the style of old version」
plt.plot(year_range, df.rolling(window=11,center=False).mean()["SUNACTIVITY"].values, label="SMA 11")
plt.plot(year_range, df.rolling(window=22,center=False).mean()["SUNACTIVITY"].values, label="SMA 22")
plt.legend()
plt.show()
```

3『

`rolling_mean` 被取代的信息详见：

[v0.18.0 (March 13, 2016) — pandas 1.0.1 documentation](https://pandas.pydata.org/docs/whatsnew/v0.18.0.html?highlight=rolling_mean)

[pandas.core.window.rolling.Rolling.mean — pandas 1.0.1 documentation](https://pandas.pydata.org/docs/reference/api/pandas.core.window.rolling.Rolling.mean.html?highlight=rolling%20mean#pandas.core.window.rolling.Rolling.mean)

[pandas.DataFrame.rolling — pandas 1.0.1 documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.rolling.html?highlight=dataframe%20rolling#pandas.DataFrame.rolling)

[Python数据分析\_Pandas06_窗函数 - 简书](https://www.jianshu.com/p/f6e489de57f7)

[pandas中时间窗函数rolling的使用_CSDN博客](https://blog.csdn.net/wj1066/article/details/78853717)

』

## 0801. Working with Databases

Databases are an important tool for data analysis. Relational databases have been around since the 1970s. Recently, NoSQL databases have become a viable alternative.

We stored annual sunspots cycles data in different relational and NoSQL databases. The term relational here does not just pertain to relationships between tables; firstly, it has to do with the relationship between columns inside a table; secondly, it relates to connections between tables. The sqlite3 module in the standard Python distribution can be used to work with a SQLite database. We can give pandas a SQLite database connection or a SQLAlchemy connection.

SQLAlchemy is renowned for its ORM, based on a design pattern, where Python classes are mapped to database tables. The ORM pattern is a general architectural pattern applicable to other object-oriented programming languages. SQLAlchemy abstracts away the technical details of working with databases including writing SQL. MongoDB is a document-based store, which can hold a huge amount of data. In the in-memory mode, Redis is extremely fast, with writing and reading being almost equally fast. Redis is a key-value store that functions similarly to a Python dictionary. Apache Cassandra mixes features of key-value and traditional relational databases. It is column oriented and its columns are organized into families, which are the equivalent of tables in relational databases. Rows in Apache Cassandra are not tied to a particular set of columns.

1『关系型数据库的 2 个特征；各个数据库的特点。』

The next chapter, Chapter 9, Analyzing Textual Data and Social Media, describes analysis techniques for plain text data. Plain text data is found in many organizations and on the Internet. Generally, plain text data is very unstructured and requires a different approach than data that has been tabulated and cleaned. For the analysis, we will use NLTK — an open source Python package. NLTK is very comprehensive and comes with its own datasets.

If you work with data, sooner or later, you will come into contact with databases. This chapter introduces various databases (relational and NoSQL) and related APIs. A relational database is a database that has a collection of tables containing data organized by the relations between data items. A relationship can be set up between each row in the table and a row in another table. A relational database does not just pertain to relationships between tables; firstly, it has to do with the relationship between columns inside a table (obviously, columns within a table have to be related, for instance, a name column and an address column in a customer table); secondly, it relates to connections between tables.

NoSQL (Not Only SQL) databases are undergoing substantial growth in Big Data and web applications. NoSQL systems may in fact permit SQL-like query languages to be employed. The main theme of NoSQL databases is allowing data to be stored in a more flexible manner than the relational model permits. This may mean not having a database schema or a flexible database schema. Of course, the flexibility and speed may come at a price such as limited support for consistent transactions. NoSQL databases can store data using a dictionary style, in a column-oriented way, as documents, objects, graphs, tuples, or a combination thereof. The topics of this chapter are listed as follows:

1『非关系型数据库的主要特征是存储方式的弹性更大；灵活性和存储速度是负相关的；非关系型数据用「字典」存储。』

Lightweight access with sqlite3. SQLite is a very popular relational database. It's very lightweight and used by many applications, for instance, web browsers such as Mozilla Firefox. The sqlite3 module in the standard Python distribution can be used to work with a SQLite database. With sqlite3, we can either store the database in a file or keep it in RAM. For this example, we will do the latter. Import sqlite3 as follows:

    import sqlite3

A connection to the database is needed to proceed. If we wanted to store the database in a file, we would provide a filename. Instead, do the following:

The with statement is standard Python and relies on the presence of a  \_\_exit\_\_() method in a special context manager class. With this statement, we don't need to explicitly close the connection. The closing of the connection is done automatically by the context manager. After connecting to a database, we need a cursor. That's generally how it works with databases by the way. A database cursor is similar to a cursor in a text editor, in concept at least. We are required to close the cursor as well. Create the cursor as follows:

```
with sqlite3.connect(":memory:") as con:
    c = con.cursor()
```

1『这里的信息解释了 with 语句的由来，目前还是不太明白，mark 下；连接完数据库后先创建一个光标。』

We can now immediately create a table. Usually, you have to create a database first or have it created for you by a database specialist. In this chapter, you not only need to know Python, but SQL too. SQL is a specialized language for database querying and manipulating. We don't have enough space to describe SQL completely. However, basic SQL should be easy for you to pick up (for example, go through http://www.w3schools.com/sql/). To create a table, we pass a SQL string to the cursor as follows:

3『又见这个 SQL 的学习课程：[SQL Tutorial](https://www.w3schools.com/sql/)』

```
c.execute('''CREATE TABLE sensors 
                            (date text, city text, code text, sensor_id real, 
temperature real)''')

```

1『

我目前的理解，光标 c 其实是一个对象，所有对表格的操作都是通过这个对象里的方法来实现的，比如上面创建一个新的表。其实代码可以写成：

    c.execute('''CREATE TABLE sensors (date text, city text, code text, sensor_id real, temperature real)''')

传递参数进方法 c.execute()，这里有个疑问，创建表必须用 ''' 吗？因为后面传递进去的参数用的都是 " 。

』

This should create a table with several columns called sensors. In this string, text and real are data types corresponding to string and numerical values. We could trust the table creation to have worked properly. If something goes wrong, we will get an error. Listing the tables in a database is database dependent. There is usually a special table or set of tables containing metadata about user tables. List the SQLite tables as follows:

```
for table in c.execute("SELECT name FROM sqlite_master WHERE type = 'table'"):
    print("Table", table[0])
```

1『List the SQLite tables，这个操作到底是什么意思。』

Let's insert and query some random data as follows:

```
c.execute("INSERT INTO sensors VALUES ('2016-1105','Utrecht','Red',42,15.14)") 
c.execute("SELECT * FROM sensors") 
print(c.fetchone())
```

3『发现都是通过方法 c.execute() 实现对数据库的操作，上面一个是写入数据，一个是选择。后面的方法 fetchone()，表示返回单个的元组，也就是一条记录 (row)，如果没有结果 , 则返回 None；还有个方法 fetchall()，返回多个元组，即返回多条记录 (rows)，如果没有结果，则返回 ()。』

When we don't need a table anymore, we can drop it. This is dangerous, so you have to be absolutely sure you don't need the table. Once a table is dropped, it cannot be recovered unless it was backed up. Drop the table and show the number of tables after dropping it as follows:

```
con.execute("DROP TABLE sensors")

print("# of tables", c.execute("SELECT COUNT(*) FROM sqlite_master WHERE type = 'table'").fetchone()[0])
```

Accessing databases from pandas. We can give pandas a database connection such as the one in the previous example or a SQLAlchemy connection. We will cover the latter in the later sections of this chapter. We will load the statsmodels sunactivity data, just like in the previous chapter, Chapter 7, Signal Processing and Time Series:

1『第 7 章的这个数据待寻找。』

1) Create a list of tuples to form the pandas DataFrame. Contrary to the previous example, create a table without specifying data types. 2) The executemany() method executes multiple statements; in this case, we will be inserting records from a list of tuples. Insert all the rows into the table and show the row count as follows. 3) The rowcount attribute of the result of an execute() call gives the number of affected rows. This attribute is somewhat quirky and depends on your SQLite version. A SQL query, as shown in the previous code snippet, on the other hand is unambiguous. Delete the records where the number of events is more than 20. 4) If we hand the database connection to pandas, we can execute a query and return a pandas DataFrame with the read_sql() function. Select the records until 1732 as follows. 

```
rows = [tuple(x) for x in df.values]
con.execute("CREATE TABLE sunspots(year, sunactivity)")

con.executemany("INSERT INTO sunspots(year, sunactivity) VALUES (?, ?)", rows) 
c.execute("SELECT COUNT(*) FROM sunspots") 
print c.fetchone()

print("Deleted", con.execute("DELETE FROM sunspots where sunactivity > 20").rowcount, "rows")

print(read_sql("SELECT * FROM sunspots where year < 1732", con))
```

Refer to the panda_access.py file in this book's code bundle for the following code:

```
# 待补充
```

SQLAlchemy is renowned for its object-relational mapping (ORM) based on a design pattern, where Python classes are mapped to database tables. In practice, this means that an extra abstraction layer is added, so we use the SQLAlchemy API to talk to the database instead of issuing SQL commands. SQLAlchemy takes care of the details behind the scene. The drawback is that you have to learn the API and may have to pay a small performance penalty. In this section, you will learn how to set up SQLAlchemy, and populate and query databases with SQLAlchemy.

1『SQLAlchemy 是在 Python 和数据库间又搭建了一个「抽象层」，让我们可以通过 SQLAlchemy 的 API 来访问和操作数据库。』

SQLAlchemy requires us to define a superclass as follows:

```
from sqlalchemy.ext.declarative import declarative_base 
Base = declarative_base()
```

In this and the following sections, we will make use of a small database with two tables. The first table defines an observation station. The second table represents sensors in the stations. Each station has zero, one, or many sensors. A station is identified by an integer ID, which is automatically generated by the database. Also, a station is identified by a name, which is unique and mandatory.

A sensor has an integer ID as well. We keep track of the last value measured by the sensor. This value can have a multiplier related to it. The setup described in this section is expressed in the alchemy_entities.py file in this book's code bundle (you don't have to run this script, but it is used by another script):

Populating a database with SQLAlchemy. Creating the tables will be deferred to the next section. In this section, we will prepare a script, which will populate the database (you don't have to run this; it is used by a script in a later section). With a DBSession object, we can insert data into the tables. An engine is needed too, but creating the engine will also be deferred until the next section.

Querying the database with SQLAlchemy. An engine is created from a URI as follows. In this URI, we specified that we are using SQLite and the data is stored in the file demo.db. Create the station and sensor tables with the engine we just created.

Pony ORM is another Python ORM package. Pony ORM is written in pure Python and has automatic query optimization and a GUI database schema editor. It also supports automatic transaction management, automatic caching, and composite keys. Pony ORM uses Python generator expressions, which are translated in SQL. Install it as follows.

Dataset is a Python library, which is basically a wrapper around SQLAlchemy. It claims to be so easy to use that even lazy people like it. Create a table called books. Actually, the table in the database isn't created yet, since we haven't specified any columns. We only created a related object. The table schema is created automatically from calls to the insert() method. Give the insert() method dictionaries with book titles; These are all excellent books, of course! The read_sql() pandas function can query this table too; Load the sunspots data and show the first five rows as follows; We can easily show the tables in the database with the following line.

```
import dataset from pandas.io.sql 
import read_sql from pandas.io.sql 
import write_frame import statsmodels.api as sm

db = dataset.connect('sqlite:///:memory:')

table = db["books"] 
table.insert(dict(title="NumPy Beginner's Guide", author='Ivan Idris')) 
table.insert(dict(title="NumPy Cookbook", author='Ivan Idris')) 
table.insert(dict(title="Learning NumPy", author='Ivan Idris')) 
print(read_sql('SELECT * FROM books', db.executable.raw_connection()))

data_loader = sm.datasets.sunspots.load_pandas() 
df = data_loader.data 
write_frame(df, "sunspots", db.executable.raw_connection()) 
table = db['sunspots']

for row in table.find(_limit=5):
    print row

print("Tables", db.tables)
```

MongoDB (humongous) is a NoSQL document-oriented database. The documents are stored in the BSON format, which is JSON like.

Storing data in Redis. Redis (REmote DIctionary Server) is an in-memory, key-value database, written in C. In the in-memory mode, Redis is extremely fast, with writing and reading being almost equally fast. Redis follows the publish/subscribe model and uses Lua scripts as stored procedures. Publish/subscribe makes use of channels to which a client can subscribe in order to receive messages. 

```
import redis 
import statsmodels.api as sm 
import pandas as pd

r = redis.StrictRedis() 
data_loader = sm.datasets.sunspots.load_pandas()

df = data_loader.data 
data = df.T.to_json() 
r.set('sunspots', data) 
blob = r.get('sunspots') 
print(pd.read_json(blob))
```

Apache Cassandra mixes features of key-value and traditional relational databases. In a conventional relational database, the columns of a table are fixed. In Cassandra, however, rows within the same table can have different columns. Cassandra is therefore column oriented, since it allows a flexible schema for each row. Columns are organized in so-called column families, which are equivalent to tables in relational databases. Joins and subqueries are not possible with Cassandra. Please refer to http://wiki.apache.org/cassandra/ GettingStarted to get started.

1-3『

Cassandra 表里每行的数据可以有不同的列；安装 Cassandra 需要先安装 Java，1.7 以上的版本。

[Download](http://cassandra.apache.org/download/)

[Home - CASSANDRA - Apache Software Foundation](https://cwiki.apache.org/confluence/display/cassandra/)

』

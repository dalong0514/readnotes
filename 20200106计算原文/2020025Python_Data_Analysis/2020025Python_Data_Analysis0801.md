# 08 Working with Databases

If you work with data, sooner or later, you will come into contact with databases. This chapter introduces various databases (relational and NoSQL) and related APIs. A relational database is a database that has a collection of tables containing data organized by the relations between data items. A relationship can be set up between each row in the table and a row in another table. A relational database does not just pertain to relationships between tables; firstly, it has to do with the relationship between columns inside a table (obviously, columns within a table have to be related, for instance, a name column and an address column in a customer table); secondly, it relates to connections between tables.

NoSQL (Not Only SQL) databases are undergoing substantial growth in Big Data and web applications. NoSQL systems may in fact permit SQL-like query languages to be employed. The main theme of NoSQL databases is allowing data to be stored in a more flexible manner than the relational model permits. This may mean not having a database schema or a flexible database schema. Of course, the flexibility and speed may come at a price such as limited support for consistent transactions. NoSQL databases can store data using a dictionary style, in a column-oriented way, as documents, objects, graphs, tuples, or a combination thereof. The topics of this chapter are listed as follows:

## 01. Lightweight access with sqlite3

SQLite is a very popular relational database. It's very lightweight and used by many applications, for instance, web browsers such as Mozilla Firefox. The sqlite3 module in the standard Python distribution can be used to work with a SQLite database. With sqlite3, we can either store the database in a file or keep it in RAM. For this example, we will do the latter. Import sqlite3 as follows:

    import sqlite3

A connection to the database is needed to proceed. If we wanted to store the database in a file, we would provide a filename. Instead, do the following:

    with sqlite3.connect(":memory:") as con:

The with statement is standard Python and relies on the presence of a \__exit__() method in a special context manager class. With this statement, we don't need to explicitly close the connection. The closing of the connection is done automatically by the context manager. After connecting to a database, we need a cursor. That's generally how it works with databases by the way. A database cursor is similar to a cursor in a text editor, in concept at least. We are required to close the cursor as well. Create the cursor as follows:

    c = con.cursor()

We can now immediately create a table. Usually, you have to create a database first or have it created for you by a database specialist. In this chapter, you not only need to know Python, but SQL too. SQL is a specialized language for database querying and manipulating. We don't have enough space to describe SQL completely. However, basic SQL should be easy for you to pick up (for example, go through http://www. w3schools.com/sql/). To create a table, we pass a SQL string to the cursor as follows:

```
c.execute('''CREATE TABLE sensors 
                            (date text, city text, code text, sensor_id real, 
temperature real)''')

```

This should create a table with several columns called sensors. In this string, text and real are data types corresponding to string and numerical values. We could trust the table creation to have worked properly. If something goes wrong, we will get an error. Listing the tables in a database is database dependent. There is usually a special table or set of tables containing metadata about user tables. List the SQLite tables as follows:

```
for table in c.execute("SELECT name FROM sqlite_master WHERE type = 'table'"):
    print("Table", table[0])
```

As expected, we get the following output:

    Table sensors

Let's insert and query some random data as follows:

```
c.execute("INSERT INTO sensors VALUES ('2016-1105','Utrecht','Red',42,15.14)") 
c.execute("SELECT * FROM sensors") 
print(c.fetchone())
```

The record we inserted should be printed as follows:

    (u'2016-11-05', u'Utrecht', u'Red', 42.0, 15.14)

When we don't need a table anymore, we can drop it. This is dangerous, so you have to be absolutely sure you don't need the table. Once a table is dropped, it cannot be recovered unless it was backed up. Drop the table and show the number of tables after dropping it as follows:

```
con.execute("DROP TABLE sensors")

print("# of tables", c.execute("SELECT COUNT(*) FROM sqlite_master WHERE type = 'table'").fetchone()[0])
```

We get the following output:

    # of tables 0

Refer to the sqlite_demo.py file in this book's code bundle for the following code:

```
import sqlite3

with sqlite3.connect(":memory:") as con:
    c = con.cursor()
c.execute('''CREATE TABLE sensors (date text, city text, code text, sensor_id real,
temperature real)''')
for table in c.execute("SELECT name FROM sqlite_master WHERE type = 'table'"):
    print("Table", table[0])

c.execute("INSERT INTO sensors VALUES ('2020-02-07', 'HangZhou', '31000', 42.0, 15.14)")
c.execute("SELECT * FROM sensors")
print(c.fetchone())

con.execute("DROP TABLE sensors")
print("# of tables", c.execute("SELECT COUNT(*) FROM sqlite_master WHERE type = 'table'").fetchone()[0])

c.close(
```

## 02. Accessing databases from pandas

We can give pandas a database connection such as the one in the previous example or a SQLAlchemy connection. We will cover the latter in the later sections of this chapter. We will load the statsmodels sunactivity data, just like in the previous chapter, Chapter 7, Signal Processing and Time Series:

1『第 7 章的这个数据待寻找。』

1) Create a list of tuples to form the pandas DataFrame:

Contrary to the previous example, create a table without specifying data types:

2) The executemany() method executes multiple statements; in this case, we will be inserting records from a list of tuples. Insert all the rows into the table and show the row count as follows:

```
rows = [tuple(x) for x in df.values]
con.execute("CREATE TABLE sunspots(year, sunactivity)")

con.executemany("INSERT INTO sunspots(year, sunactivity) VALUES (?, ?)", rows) 
c.execute("SELECT COUNT(*) FROM sunspots") 
print c.fetchone()

print("Deleted", con.execute("DELETE FROM sunspots where sunactivity > 20").rowcount, "rows")

print(read_sql("SELECT * FROM sunspots where year < 1732", con))
```

The number of rows in the table is printed as follows:

    (309,)

3) The rowcount attribute of the result of an execute() call gives the number of affected rows. This attribute is somewhat quirky and depends on your SQLite version. A SQL query, as shown in the previous code snippet, on the other hand is unambiguous. Delete the records where the number of events is more than 20:

The following should be printed:

    Deleted 217 rows

4) If we hand the database connection to pandas, we can execute a query and return a pandas DataFrame with the read_sql() function. Select the records until 1732 as follows:

The end result is the following pandas DataFrame:

Refer to the panda_access.py file in this book's code bundle for the following code:

```
# 待补充
```

## 03. SQLAlchemy

SQLAlchemy is renowned for its object-relational mapping (ORM) based on a design pattern, where Python classes are mapped to database tables. In practice, this means that an extra abstraction layer is added, so we use the SQLAlchemy API to talk to the database instead of issuing SQL commands. SQLAlchemy takes care of the details behind the scene. The drawback is that you have to learn the API and may have to pay a small performance penalty. In this section, you will learn how to set up SQLAlchemy, and populate and query databases with SQLAlchemy.

### 1. Installing and setting up SQLAlchemy

The following is the command to install SQLAlchemy:

    $ pip install sqlalchemy

The latest version of SQLAlchemy at the time of writing was 0.9.6. The download page for SQLAlchemy is available at http://www.sqlalchemy.org/download.html with links to installers and code repositories. SQLAlchemy also has a support page available at http://www.sqlalchemy.org/support.html. After modifying the pkg_check.py script, we can display the modules of SQLAlchemy:

SQLAlchemy requires us to define a superclass as follows:

```
from sqlalchemy.ext.declarative import declarative_base 
Base = declarative_base()
```

In this and the following sections, we will make use of a small database with two tables. The first table defines an observation station. The second table represents sensors in the stations. Each station has zero, one, or many sensors. A station is identified by an integer ID, which is automatically generated by the database. Also, a station is identified by a name, which is unique and mandatory.

A sensor has an integer ID as well. We keep track of the last value measured by the sensor. This value can have a multiplier related to it. The setup described in this section is expressed in the alchemy_entities.py file in this book's code bundle (you don't have to run this script, but it is used by another script):

```
from sqlalchemy import Column, ForeignKey, Integer, String, Float 
from sqlalchemy.ext.declarative import declarative_base 
from sqlalchemy.orm import relationship 
from sqlalchemy import create_engine 
from sqlalchemy import UniqueConstraint

Base = declarative_base()

class Station(Base):
    __tablename__ = 'station' 
    id = Column(Integer, primary_key=True) 
    name = Column(String(14), nullable=False, unique=True)

    def __repr__(self):
        return "Id=%d name=%s" %(self.id, self.name)

class Sensor(Base):
    __tablename__ = 'sensor' id = Column(Integer, primary_key=True) 
    last = Column(Integer) 
    multiplier = Column(Float) 
    station_id = Column(Integer, ForeignKey('station.id')) 
    station = relationship(Station)

    def __repr__(self):
        return "Id=%d last=%d multiplier=%.1f station_id=%d"

%(self.id, self.last, self.multiplier, self.station_id)

if __name__ == "__main__":
    print("This script is used by another script. Run python alchemy_query.py")
```

### 2. Populating a database with SQLAlchemy

Creating the tables will be deferred to the next section. In this section, we will prepare a script, which will populate the database (you don't have to run this; it is used by a script in a later section). With a DBSession object, we can insert data into the tables. An engine is needed too, but creating the engine will also be deferred until the next section.

1.Create the DBSession object as follows:

```
Base.metadata.bind = engine

DBSession = sessionmaker(bind=engine) 
session = DBSession()
```

2.Let's create two stations:

```
de_bilt = Station(name='De Bilt') 
session.add(de_bilt) 
session.add(Station(name='Utrecht'))

session.commit() 
print("Station", de_bilt)

```

The rows are not inserted until we commit the session. The following is printed for the first station:

    Station Id=1 name=De Bilt

3.Similarly, insert a sensor record as follows:

```
temp_sensor = Sensor(last=20, multiplier=.1, station=de_bilt) 
session.add(temp_sensor) 
session.commit() 
print("Sensor", temp_sensor)
```

The sensor is in the first station; therefore, we get the following printout:

    Sensor Id=1 last=20 multiplier=0.1 station_id=1

The database population code can be found in the populate_db.py file in this book's code bundle (again you don't need to run this code; it's used by another script):

```
from sqlalchemy import create_engine 
from sqlalchemy.orm import sessionmaker

from alchemy_entities import Base, Sensor, Station

def populate(engine):
    Base.metadata.bind = engine
    
    DBSession = sessionmaker(bind=engine) 
    session = DBSession()

    de_bilt = Station(name='De Bilt') 
    session.add(de_bilt) 
    session.add(Station(name='Utrecht')) 
    session.commit() print "Station", de_bilt

    temp_sensor = Sensor(last=20, multiplier=.1, station=de_bilt) 
    session.add(temp_sensor) 
    session.commit() 
    print("Sensor", temp_sensor)

if __name__ == "__main__":

    print("This script is used by another script. Run python alchemy_query.py")
```

### 3. Querying the database with SQLAlchemy

An engine is created from a URI as follows:

    engine = create_engine('sqlite:///demo.db')

In this URI, we specified that we are using SQLite and the data is stored in the file demo.db. Create the station and sensor tables with the engine we just created:

    Base.metadata.create_all(engine)

For SQLAlchemy queries, we need a DBSession object again, as shown in the previous section. Select the first row in the station table:

    station = session.query(Station).first()

Select all the stations as follows:

    print("Query 1", session.query(Station).all())

The following will be the output:

    Query 1 [Id=1 name=De Bilt, Id=2 name=Utrecht]

Select all the sensors as follows:

    print("Query 2", session.query(Sensor).all())

The following will be the output:

    Query 2 [Id=1 last=20 multiplier=0.1 station_id=1]

Select the first sensor, which belongs to the first station:

    print("Query 3", session.query(Sensor).filter(Sensor.station == station).one())

The following will be the output:

    Query 3 Id=1 last=20 multiplier=0.1 station_id=1

We can again query with the pandas read_sql() method:

    print(read_sql("SELECT * FROM station", engine.raw_connection()))

You will get the following output:

Inspect the alchemy_query.py file in this book's code bundle:

```
from alchemy_entities import Base, Sensor, Station 
from populate_db import populate 
from sqlalchemy import create_engine 
from sqlalchemy.orm import sessionmaker 
import os 
from pandas.io.sql import read_sql

engine = create_engine('sqlite:///demo.db') 
Base.metadata.create_all(engine) 
populate(engine) 
Base.metadata.bind = engine
DBSession = sessionmaker() 
DBSession.bind = engine 
session = DBSession()

station = session.query(Station).first()

print("Query 1", session.query(Station).all() )
print("Query 2", session.query(Sensor).all() )
print("Query 3", session.query(Sensor).filter(Sensor.station == station).one() )
print(read_sql("SELECT * FROM station", engine.raw_connection()))

try:
    os.remove('demo.db') 
    print("Deleted demo.db" )
except OSError:
    pass
```

## 04. Pony ORM

Pony ORM is another Python ORM package. Pony ORM is written in pure Python and has automatic query optimization and a GUI database schema editor. It also supports automatic transaction management, automatic caching, and composite keys. Pony ORM uses Python generator expressions, which are translated in SQL. Install it as follows:

    $ sudo pip install pony
    $ pip freeze|grep pony pony==0.5.1

Import the packages we will need in this example. Refer to the pony_ride.py file in this book's code bundle:

```
from pony.orm import Database, db_session 
from pandas.io.sql import write_frame 
import statsmodels.api as sm
```

Create an in-memory SQLite database:

    db = Database('sqlite', ':memory:')

Load the sunspots data and write it to the database with the pandas write_frame() function:

```
with db_session:
    data_loader = sm.datasets.sunspots.load_pandas() 
    df = data_loader.data 
    write_frame(df, "sunspots", db.get_connection()) 
    print(db.select("count(*) FROM sunspots"))
```

The number of rows in the sunspots table is printed as follows:

    [309]

## 05. Dataset – databases for lazy people

Dataset is a Python library, which is basically a wrapper around SQLAlchemy. It claims to be so easy to use that even lazy people like it.

Install dataset as follows:

```
$ sudo pip install dataset 
$ pip freeze| grep dataset 
dataset==0.5.4
```

Create a SQLite in-memory database and connect to it:

```
import dataset 
db = dataset.connect('sqlite:///:memory:')
```

Create a table called books:

    table = db["books"]

Actually, the table in the database isn't created yet, since we haven't specified any columns. We only created a related object. The table schema is created automatically from calls to the insert() method. Give the insert() method dictionaries with book titles:

```
table.insert(dict(title="NumPy Beginner's Guide", author='Ivan Idris')) 
table.insert(dict(title="NumPy Cookbook", author='Ivan Idris')) 
table.insert(dict(title="Learning NumPy", author='Ivan Idris'))
```

These are all excellent books, of course! The read_sql() pandas function can query this table too:

```
print(read_sql('SELECT * FROM books', db.executable.raw_connection()))
```

The following is the output:

Load the sunspots data and show the first five rows as follows:

```
write_frame(df, "sunspots", db.executable.raw_connection()) 
table = db['sunspots']

for row in table.find(_limit=5):
    print row
```

The following will be printed:

```
OrderedDict([(u'YEAR', 1700.0), (u'SUNACTIVITY', 5.0)]) 
OrderedDict([(u'YEAR', 1701.0), (u'SUNACTIVITY', 11.0)]) 
OrderedDict([(u'YEAR', 1702.0), (u'SUNACTIVITY', 16.0)]) 
OrderedDict([(u'YEAR', 1703.0), (u'SUNACTIVITY', 23.0)]) 
OrderedDict([(u'YEAR', 1704.0), (u'SUNACTIVITY', 36.0)])
```

We can easily show the tables in the database with the following line:

    print("Tables", db.tables)

The following is the output of the preceding code:

    Tables [u'books', 'sunspots']

The following is the content of the dataset_demo.py file in this book's code bundle:

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

## 06. PyMongo and MongoDB

MongoDB (humongous) is a NoSQL document-oriented database. The documents are stored in the BSON format, which is JSON like. You can download a MongoDB distribution from http://www.mongodb.org/downloads. Installing should be just a matter of unpacking a compressed archive. The version at the time of writing was 2.6.3. In the bin directory of the distribution, we will find the mongod file, which starts the server.MongoDB expects to find a /data/db directory. This is the directory where data is stored. We can specify another directory from the command line as follows:

    $ mkdir /tmp/db

Start the database from the directory containing its binary executables:

    ./mongod --dbpath /tmp/db

We need to keep this process running to be able to query the database.

PyMongo is a Python driver for MongoDB. Install PyMongo as follows:

```
$ sudo pip install pymongo 
$ pip freeze|grep pymongo pymongo==2.7.1
```

Connect to the MongoDB test database:

```
from pymongo import MongoClient
client = MongoClient() 
db = client.test_database
```

Recall that we can create JSON from a pandas DataFrame. Create the JSON and store it in MongoDB:

```
data_loader = sm.datasets.sunspots.load_pandas() 
df = data_loader.data 
rows = json.loads(df.T.to_json()).values() 
db.sunspots.insert(rows)
```

Query the document we just created:

```
cursor = db['sunspots'].find({}) 
df = pd.DataFrame(list(cursor)) 
print df
```

This prints the entire pandas DataFrame. Refer to the mongo_demo.py file in this book's code bundle:

```
from pymongo import MongoClient 
import statsmodels.api as sm 
import json 
import pandas as pd

client = MongoClient() 
db = client.test_database

data_loader = sm.datasets.sunspots.load_pandas() 
df = data_loader.data 
rows = json.loads(df.T.to_json()).values() 
db.sunspots.insert(rows)

cursor = db['sunspots'].find({}) 
df = pd.DataFrame(list(cursor)) 
print df

db.drop_collection('sunspots')
```

## 07. Storing data in Redis

Redis (REmote DIctionary Server) is an in-memory, key-value database, written in C. In the in-memory mode, Redis is extremely fast, with writing and reading being almost equally fast. Redis follows the publish/subscribe model and uses Lua scripts as stored procedures. Publish/subscribe makes use of channels to which a client can subscribe in order to receive messages. The most recent Redis version at the time of writing was 2.8.12. Redis can be downloaded from the home page at http://redis. io/. After unpacking the Redis distribution, issue the following command to compile the code and create all the binaries:

    $ make

Run the server as follows:

    $ src/redis-server

Now let's install a Python driver:

```
$ sudo pip install redis
$ pip freeze|grep redis 
redis==2.10.1
```

It's pretty easy to use Redis when you realize it's a giant dictionary. However, Redis does have its limitations. Sometimes, it's just convenient to store a complex object as a JSON string (or other format). That's what we are going to do with a pandas DataFrame. Connect to Redis as follows:

    r = redis.StrictRedis()

Create a key-value pair with a JSON string:

    r.set('sunspots', data)

Retrieve the data with the following line:

    blob = r.get('sunspots')

The code is straightforward and given in the redis_demo.py file in this book's code bundle:

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

## 08. Apache Cassandra

Apache Cassandra mixes features of key-value and traditional relational databases. In a conventional relational database, the columns of a table are fixed. In Cassandra, however, rows within the same table can have different columns. Cassandra is therefore column oriented, since it allows a flexible schema for each row. Columns are organized in so-called column families, which are equivalent to tables in relational databases. Joins and subqueries are not possible with Cassandra. Cassandra can be downloaded from http://cassandra.apache.org/download/. The latest version at the time of writing was 2.0.9. Please refer to http://wiki.apache.org/cassandra/ GettingStarted to get started.

Run the server from the command line as follows:

    $ bin/cassandra –f

If you run the previous command, you may get the following error message:

    Cassandra 2.0 and later require Java 7 or later.

Java in this context is a high-level programming language such as Python. Java 7 refers to version 1.7 (it's a marketing ploy). If you have Java installed, you can check its version as follows:

    $ java –version 
    java version "1.7.0_60"

For most operating systems, except Mac OS X, you can download Java from http://www.oracle.com/technetwork/java/javase/downloads/index.html.

Instructions for installing Java on Mac are given at http://docs.oracle.com/javase/7/docs/webnotes/install/mac/macjdk.html. Since this is a Python book, we will not dwell too long on the details of installing Java. A quick web search should give you more than enough information.

Create the directories listed in conf/cassandra.yaml or tweak them as follows:

```
data_file_directories:
/tmp/lib/cassandra/data 
commitlog_directory: /tmp/lib/cassandra/commitlog 
saved_caches_directory: /tmp/lib/cassandra/saved_caches
```

The following commands make sense if you don't want to keep the data:

```
$ mkdir -p /tmp/lib/cassandra/data 
$ mkdir –p /tmp/lib/cassandra/commitlog 
$ mkdir –p /tmp/lib/cassandra/saved_caches
```

Install a Python driver with the following command:

```
$ sudo pip install cassandra-driver 
$ pip freeze|grep cassandra-driver 
cassandra-driver==2.0.2
```

You might get the following error message:

```
The required version of setuptools (>=0.9.6) is not available,

and can't be installed while this script is running. Please

install a more recent version first, using

'easy_install -U setuptools'.
```

This seems pretty self-explanatory.

Now it's time for the code. Connect to a cluster and create a session as follows:

```
cluster = Cluster() 
session = cluster.connect()
```

Cassandra has the concept of keyspace. A keyspace holds tables. Cassandra has its own query language called Cassandra Query Language (CQL). CQL is very similar to SQL. Create the keyspace and set the session to use it:

```
session.execute("CREATE KEYSPACE IF NOT EXISTS mykeyspace 
WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 1 };") 
session.set_keyspace('mykeyspace')
```

Now, create a table for the sunspots data:

```
session.execute("CREATE TABLE IF NOT EXISTS sunspots (year decimal PRIMARY KEY, sunactivity decimal);")
```

1.Create a statement that we will use in a loop to insert rows of the data as tuples:

```
query = SimpleStatement( "INSERT INTO sunspots (year, sunactivity) VALUES (%s, %s)",

consistency_level=ConsistencyLevel.QUORUM)
```

2.The following line inserts the data:

```
for row in rows:
    session.execute(query, row)
```

3.Get the count of the rows in the table:

    print session.execute("SELECT COUNT(*) FROM sunspots")

This prints the row count as follows:

    [Row(count=309)]

4.Drop the keyspace and shut down the cluster:

```
session.execute('DROP KEYSPACE mykeyspace') 
cluster.shutdown()
```

Refer to the cassandra_demo.py file in this book's code bundle:

```
from cassandra import ConsistencyLevel
from cassandra.cluster import Cluster 
from cassandra.query import SimpleStatement 
import statsmodels.api as sm

cluster = Cluster() 
session = cluster.connect() 
session.execute("CREATE KEYSPACE IF NOT EXISTS mykeyspace WITH REPLICATION = { 'class' : 'SimpleStrategy', 'replication_factor' : 1 };") 
session.set_keyspace('mykeyspace') 
session.execute("CREATE TABLE IF NOT EXISTS sunspots (year decimal PRIMARY KEY, sunactivity decimal);")

query = SimpleStatement("INSERT INTO sunspots (year, sunactivity) VALUES (%s, %s)", consistency_level=ConsistencyLevel.QUORUM)

data_loader = sm.datasets.sunspots.load_pandas() 
df = data_loader.data 
rows = [tuple(x) for x in df.values]

for row in rows:
    session.execute(query, row)

print(session.execute("SELECT COUNT(*) FROM sunspots"))

session.execute('DROP KEYSPACE mykeyspace') 
cluster.shutdown()
```

## Summary

We stored annual sunspots cycles data in different relational and NoSQL databases.

The term relational here does not just pertain to relationships between tables; firstly, it has to do with the relationship between columns inside a table; secondly, it relates to connections between tables.

The sqlite3 module in the standard Python distribution can be used to work with a SQLite database. We can give pandas a SQLite database connection or a SQLAlchemy connection.

SQLAlchemy is renowned for its ORM, based on a design pattern, where Python classes are mapped to database tables. The ORM pattern is a general architectural pattern applicable to other object-oriented programming languages. SQLAlchemy abstracts away the technical details of working with databases including writing SQL.

MongoDB is a document-based store, which can hold a huge amount of data.

In the in-memory mode, Redis is extremely fast, with writing and reading being almost equally fast. Redis is a key-value store that functions similarly to a Python dictionary.

Apache Cassandra mixes features of key-value and traditional relational databases. It is column oriented and its columns are organized into families, which are the equivalent of tables in relational databases. Rows in Apache Cassandra are not tied to a particular set of columns.

The next chapter, Chapter 9, Analyzing Textual Data and Social Media, describes analysis techniques for plain text data. Plain text data is found in many organizations and on the Internet. Generally, plain text data is very unstructured and requires a different approach than data that has been tabulated and cleaned. For the analysis, we will use NLTK—an open source Python package. NLTK is very comprehensive and comes with its own datasets.
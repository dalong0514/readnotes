# 05. pandas: Reading and Writing Data

Fabio Nelli1

(1)Rome, Italy

In the previous chapter, you became familiar with the pandas library and with the basic functiona lities that it provides for data analysis. You saw that dataframe and series are the heart of this library. These are the material on which to perform all data manipulations, calculations, and analysis.

In this chapter, you will see all of the tools provided by pandas for reading data stored in many types of media (such as files and databases). In parallel, you will also see how to write data structures directly on these formats, without worrying too much about the technologies used.

This chapter focuses on a series of I/O API functions that pandas provides to read and write data directly as datafram e objects. We start by looking at text files, then move gradually to more complex binary formats.

At the end of the chapter, you’ll also learn how to interface with all common databases, both SQL and NoSQL, including examples that show how to store data in a dataframe. At the same time, you learn how to read data contained in a database and retrieve them as a dataframe.

I/O API Tools

pandas is a library specialized for data analysis, so you expect that it is mainly focused on calculation and data processing. The processes of writing and reading data from/to external files can be considered part of data processing. In fact, you will see how, even at this stage, you can perform some operations in order to prepare the incoming data for manipulation.

Thus, this step is very important for data analysis and therefore a specific tool for this purpose must be present in the library pandas—a set of functions called I/O API. These functions are divided into two main categories: readers and writers.Readers

Writers

read_csv

to_csv

read_excel

to_excel

read_hdf

to_hdf

read_sql

to_sql

read_json

to_json

read_html

to_html

read_stata

to_stata

read_clipboard

to_clipboard

read_pickle

to_pickle

read_msgpack

to_msgpack (experimental)

read_gbq

to_gbq (experimental)

CSV and Textual Files

Everyone has become accustomed over the years to writing and reading files in text form. In particular, data are generally reported in tabular form. If the values in a row are separated by commas, you have the CSV (comma-separated values) format, which is perhaps the best-known and most popular format.

Other forms of tabular data can be separated by spaces or tabs and are typically contained in text files of various types (generally wi th the .txt extension).

This type of file is the most common source of data and is easier to transcribe and interpret. In this regard, pandas provides a set of functions specific for this type of file. read_csv

read_table

to_csv

Reading Data in CSV or Text Files

From experience, the most common operation of a person approaching data analysis is to read the data contained in a CSV file, or at least in a text file.

But before you start dealing with files, you need to import the following libraries.>>> import numpy as np

>>> import pandas as pd

In order to see how pandas handles this kind of data, we’ll start by creating a small CSV file in the working directory, as shown in Listing 5-1, and save it as ch05_01.csv .white,red,blue,green,animal

1,5,2,3,cat

2,7,8,5,dog

3,3,6,7,horse

2,2,8,3,duck

4,4,2,1,mouse

Listing 5-1ch05_01.csv

Since this file is comma-delimited, you can use th e read_csv() function to read its content and convert it to a dataframe object.>>> csvframe = pd.read_csv('ch05_01.csv')

>>> csvframe

white red blue green animal

0 1 5 2 3 cat

1 2 7 8 5 dog

2 3 3 6 7 horse

3 2 2 8 3 duck

4 4 4 2 1 mouse

As you can see, reading the data in a CSV file is rather trivial. CSV files are tabulated data in which the values on the same column are separated by commas. Since CSV files are considered text files, you can also use the read_table() fu nction, but specify the delimiter.>>> pd.read_table('ch05_01.csv',sep=',')

white red blue green animal

0 1 5 2 3 cat

1 2 7 8 5 dog

2 3 3 6 7 horse

3 2 2 8 3 duck

4 4 4 2 1 mouse

In this example, you can see that in the CSV file, headers that identify all the columns are in the first row. But this is not a general case; it often happens that the tabulated data begin directly in the first line (see Listing 5-2).1,5,2,3,cat

2,7,8,5,dog

3,3,6,7,horse

2,2,8,3,duck

4,4,2,1,mouse

>>> pd.read_csv('ch05_02.csv')

1 5 2 3 cat

0 2 7 8 5 dog

1 3 3 6 7 horse

2 2 2 8 3 duck

3 4 4 2 1 mouse

Listing 5-2ch05_02.csv

In this case, you could make sure that it is pandas that assigns the default names to the columns by setting the header opti on to None.>>> pd.read_csv('ch05_02.csv', header=None)

0 1 2 3 4

0 1 5 2 3 cat

1 2 7 8 5 dog

2 3 3 6 7 horse

3 2 2 8 3 duck

4 4 4 2 1 mouse

In addition, you can specify the names directly by assigning a list of labels to the names opt ion.>>> pd.read_csv('ch05_02.csv', names=['white','red','blue','green','animal'])

white red blue green animal

0 1 5 2 3 cat

1 2 7 8 5 dog

2 3 3 6 7 horse

3 2 2 8 3 duck

4 4 4 2 1 mouse

In more complex cases, in which you want to create a dataframe with a hierarchical structure by reading a CSV file, you can extend the functionality of the read_csv() fu nction by adding the index_col o ption, assigning all the columns to be converted into indexes.

To b etter understand this possibility, create a new CSV file with two columns to be used as indexes of the hierarchy. Then, save it in the working directory as ch05_03.csv (see Listing 5-3).color,status,item1,item2,item3

black,up,3,4,6

black,down,2,6,7

white,up,5,5,5

white,down,3,3,2

white,left,1,2,1

red,up,2,2,2

red,down,1,1,4

>>> pd.read_csv('ch05_03.csv', index_col=['color','status'])

item1 item2 item3

color status

black up 3 4 6

down 2 6 7

white up 5 5 5

down 3 3 2

left 1 2 1

red up 2 2 2

down 1 1 4

Listing 5-3ch05_03.csv

Using RegExp to Parse TXT Files

In other cases, it is possible that the files on which to parse the data do not show separators well defined as a comma or a semicolon. In these cases, the regular expressions come to our aid. In fact, you can specify a regexp within the read_table() f unction using the sep option.

To better understand regexp and understand how you can apply it as criteria for value separation, let’s start with a simple case. For example, suppose that your TXT file has values that are separated by spaces or tabs in an unpredictable order. In this case, you have to use the regexp, because that’s the only way to take into account both separator types. You can do that using the wildcard /s*. /s stands for the space or tab character (if you want to indicate a tab, you use /t), while the asterisk indicates that there may be multiple characters (see Table 5-1 for other common wildcards). That is, the values may be separated by more spaces or more tabs.Table 5-1 Metacharacters

.

Single character, except newline

\d

Digit

\D

Non-digit character

\s

Whitespace character

\S

Non-whitespace character

\n

New line character

\t

Tab character

\uxxxx

Unicode character specified by the hexadecimal number xxxx

Take for example an extreme case in which we have the values separated by tabs or spaces in a random order (see Listing 5-4).white red blue green

1 5 2 3

2 7 8 5

3 3 6 7

>>> pd.read_table('ch05_04.txt',sep='\s+', engine="python")

white red blue green

0 1 5 2 3

1 2 7 8 5

2 3 3 6 7

Listing 5-4ch05_04.txt

As you can see, the result is a perfect dataframe in which the values are perfectly ord ered.

Now you will see an example that may seem strange or unusual, but it is not as rare as it may seem. This example can be very helpful in understanding the high potential of a regexp. In fact, you might typically think of separators as special characters like commas, spaces, tabs, etc., but in reality you can consider separator characters like alphanumeric characters, or for example, integers such as 0.

In this example, you need to extract the numeric part from a TXT file, in which there is a sequence of characters with numerical values and the literal characters are completely fused.

Remember to set the header option to None whenever the column headings are not present in the TXT file (see Listing 5-5).000END123AAA122

001END124BBB321

002END125CCC333

>>> pd.read_table('ch05_05.txt', sep='\D+', header=None, engine="python")

0 1 2

0 0 123 122

1 1 124 321

2 2 125 333

Listing 5-5ch05_05.txt

Another f airly common event is to exclude lines from parsing. In fact you do not always want to include headers or unnecessary comments contained in a file (see Listing 5-6). With the skiprows option, you can exclude all the lines you want, just assigning an array containing the line numbers to not consider in parsing.

Pay attention when you are using this option. If you want to exclude the first five lines, you have to write skiprows = 5, but if you want to rule out the fifth line, you have to write skiprows = [5].########### LOG FILE ############

This file has been generated by automatic system

white,red,blue,green,animal

12-Feb-2015: Counting of animals inside the house

1,5,2,3,cat

2,7,8,5,dog

13-Feb-2015: Counting of animals outside the house

3,3,6,7,horse

2,2,8,3,duck

4,4,2,1,mouse

>>> pd.read_table('ch05_06.txt',sep=',',skiprows=[0,1,3,6])

white red blue green animal

0 1 5 2 3 cat

1 2 7 8 5 dog

2 3 3 6 7 horse

3 2 2 8 3 duck

4 4 4 2 1 mouse

Listing 5-6ch05_06.txt

Reading TXT Files Into Parts

When large files are processed, or when you are only interested in portions of these files, you often need to read the file into portions (chunks). This is both to apply any iterations and because we are not interested in parsing the entire file.

If, for example, you wanted to read only a portion of the file, you can explicitly specify the number of lines on which to parse. Thanks to the nrows and skiprows op tions, you can select the starting line n (n = SkipRows) and the lines to be read after it (nrows = i).>>> pd.read_csv('ch05_02.csv',skiprows=[2],nrows=3,header=None)

0 1 2 3 4

0 1 5 2 3 cat

1 2 7 8 5 dog

2 2 2 8 3 duck

Another interesting and fairly common operation is to split into portions that part of the text on which you want to parse. Then, for each portion a specific operation may be carried out, in order to obtain an iteration, portion by portion.

For example, you want to add the values in a column every three rows and then insert these sums in a series. This example is trivial and impractical but is very simple to understand, so once you have learned the underlying mechanism, you will be able to apply it in more complex cases.>>> out = pd.Series()

>>> i = 0

>>> pieces = pd.read_csv('ch05_01.csv',chunksize=3)

>>> for piece in pieces:

... out.set_value(i,piece['white'].sum())

... i = i + 1

...

0 6

dtype: int64

0 6

1 6

dtype: int64

>>> out

0 6

1 6

dtype: int64

Writing Data in CSV

In addition to reading the data contained in a file, it’s also common to write a data file produced by a calculation, or in general the data contained in a data structure.

For example, you might want to write the data contained in a dataframe to a CSV file. To do this writing process, you will use th e to_csv() function, which accepts as an argument the name of the file you generate (see Listing 5-7).>>> frame = pd.DataFrame(np.arange(16).reshape((4,4)),

index = ['red', 'blue', 'yellow', 'white'],

columns = ['ball', 'pen', 'pencil', 'paper'])

>>> frame.to_csv('ch05_07.csv')

If you open the new file called ch05_07.csv generated by the pandas library, you will see data as in Listing 5-7.,ball,pen,pencil,paper

0,1,2,3

4,5,6,7

8,9,10,11

12,13,14,15

Listing 5-7ch05_07.csv

As you can see from the previous example, when you write a dataframe to a file, indexes and columns are marked on the file by default. This default behavior can be changed by setting the two options index and header to False (see Listing 5-8).>>> frame.to_csv('ch05_07b.csv', index=False, header=False)

1,2,3

5,6,7

9,10,11

13,14,15

Listing 5-8ch05_07b.csv

One point to remember when writing files is that NaN values present in a data structure are shown as empty fields in the file (see Listing 5-9).>>> frame3 = pd.DataFrame([[6,np.nan,np.nan,6,np.nan],

... [np.nan,np.nan,np.nan,np.nan,np.nan],

... [np.nan,np.nan,np.nan,np.nan,np.nan],

... [20,np.nan,np.nan,20.0,np.nan],

... [19,np.nan,np.nan,19.0,np.nan]

... ],

... index=['blue','green','red','white','yellow'],

columns=['ball','mug','paper','pen','pencil'])

>>> frame3

ball mug paper pen pencil

blue 6.0 NaN NaN 6.0 NaN

green NaN NaN NaN NaN NaN

red NaN NaN NaN NaN NaN

white 20.0 NaN NaN 20.0 NaN

yellow 19.0 NaN NaN 19.0 NaN

>>> frame3.to_csv('ch05_08.csv')

,ball,mug,paper,pen,pencil

blue,6.0,,,6.0,

green,,,,,

red,,,,,

white,20.0,,,20.0,

yellow,19. 0,,,19.0,

Listing 5-9ch05_08.csv

However, you can replace this empty field with a value to your liking using the na_rep opt ion in the to_csv() function. Common values may be NULL, 0, or the same NaN (see Listing 5-10).>>> frame3.to_csv('ch05_09.csv', na_rep ='NaN')

,ball,mug,paper,pen,pencil

blue,6.0,NaN,NaN,6.0,NaN

green,NaN,NaN,NaN,NaN,NaN

red,NaN,NaN,NaN,NaN,NaN

white,20.0,NaN,NaN,20.0,NaN

yellow,19.0,NaN,NaN,19.0,NaN

Listing 5-10ch05_09.csv

Note

In the cases specified, dataframe has always been the subject of discussion since these are the data structures that are written to the file. But all these functions and options are also valid with regard to the series.

Reading and Writing HTML Files

pandas provides the corresponding pair of I/O API functions for the HTML format. read_html()

to_html()

These two functions can be very useful. You will appreciate the ability to convert complex dat a structures such as dataframes directly into HTML tables without having to hack a long listing in HTML, especially if you’re dealing with the Web.

The inverse operation can be very useful, because now the major source of data is just the web world. In fact, a lot of data on the Internet does not always have the form「ready to use,」that is packaged in some TXT or CSV file. Very often, however, the data are reported as part of the text of web pages. So also having available a function for reading could prove to be really useful.

This activity is so widespread that it is currently identified as web scraping . This process is becoming a fundamental part of the set of processes that will be integrated in the first part of data analysis: data mining and data preparation.

Note

Many websites have now adopted the HTML5 format, to avoid any issues of missing modules and error messages. I strongly recommend you install the module html5lib. Anaconda specified:

conda install html5lib

Writing Data in HTML

Now you learn how to convert a dataframe into an HTML table. The internal structure of the dataframe is automatically converted into nested tags <TH>, <TR>, and <TD> retaining any internal hierarchies. You do not need to know HTML to use this kind of function.

Because the data structures as the dataframe can be quite complex and large, it’s great to have a function like this when you need to develop web pages.

To better understand this potential, here’s an example. You can start by defining a simple dataframe.

Thanks to the to_html() func tion, you can directly convert the dataframe into an HTML table.>>> frame = pd.DataFrame(np.arange(4).reshape(2,2))

Since the I/O API functions are defined in the pandas data structures, you can call the to_html() function directly on the instance of the dataframe.>>> print(frame.to_html())

<table border="1" class="dataframe">

<thead>

<tr style="text-align: right;">

<th></th>

<th>0</th>

<th>1</th>

</tr>

</thead>

<tbody>

<tr>

<th>0</th>

<td> 0</td>

<td> 1</td>

</tr>

<tr>

<th>1</th>

<td> 2</td>

<td> 3</td>

</tr>

</tbody>

</table>

As you can see, the whole structure formed by the HTML tags needed to create an HTML table was generated correctly in order to respect the internal structure of the dataframe.

In the next example, you’ll see how the table appears automatically generated within an HTML file. In this regard, we create a dataframe a bit more complex than the previous one, where there are the labels of the indexes and column names.>>> frame = pd.DataFrame( np.random.random((4,4)),

... index = ['white','black','red','blue'],

... columns = ['up','down','right','left'])

>>> frame

up down right left

white 0.292434 0.457176 0.905139 0.737622

black 0.794233 0.949371 0.540191 0.367835

red 0.204529 0.981573 0.118329 0.761552

blue 0.628790 0.585922 0.039153 0.461598

Now you focus on writing an HTML page through the generation of a string. This is a simple and trivial example, but it is very useful to understand and to test the functionality of pandas directly on the web browser.

First of all we create a string that contains the code of the HTML page.>>> s = ['<HTML>']

>>> s.append('<HEAD><TITLE>My DataFrame</TITLE></HEAD>')

>>> s.append('<BODY>')

>>> s.append(frame.to_html())

>>> s.append('</BODY></HTML>')

>>> html = ".join(s)

Now that all the listing of the HTML page is contained within the html variable, you can write directly on the file that will be called myFrame.html:>>> html_file = open('myFrame.html','w')

>>> html_file.write(html)

>>> html_file.close()

Now in your working directory will be a new HTML file, my Frame.html. Double-click it to open it directly from the browser. An HTML table will appear in the upper left, as shown in Figure 5-1.

Figure 5-1The dataframe is shown as an HTML table in the web page

Reading Data from an HTML File

As you just saw, pandas can easily generate HTML tables starting from the dataframe. The opposite process is also possible; the functio n read_html () will perform a parsing an HTML page looking for an HTML table. If found, it will convert that table into an object dataframe ready to be used in our data analysis.

More precisely, the read_html() function returns a list of dataframes even if there is only one table. The source that will be parsed can be different types. For example, you may have to read an HTML file in any directory. For example you can parse the HTML file you created in the previous example:>>> web_frames = pd.read_html('myFrame.html')

>>> web_frames[0]

Unnamed: 0 up down right left

0 white 0.292434 0.457176 0.905139 0.737622

1 black 0.794233 0.949371 0.540191 0.367835

2 red 0.204529 0.981573 0.118329 0.761552

3 blue 0.628790 0.585922 0.039153 0.461598

As you can see, all of the tags that have nothing to do with HTML table are not considered absolutely. Furthermore web_frames is a list of dataframes, although in your case, the dataframe that you are extracting is only one. However, you can select the item in the list that you want to use, calling it in the classic way. In this case, the item is unique and therefore the index will be 0.

However, the mode most commonly used regarding the read_html() function is that of a direct parsing of an URL on the Web. In this way the web pages in the network are directly parsed with the extraction of the tables in them.

For example, now you will call a web page where there is an HTML table that shows a ranking list with some names and scores.>>> ranking = pd.read_html('https://www.meccanismocomplesso.org/en/meccanismo-complesso-sito-2/classifica-punteggio/')

>>> ranking[0]

Member points levels Unnamed: 3

0 1 BrunoOrsini 1075 NaN

1 2 Berserker 700 NaN

2 3 albertosallu 275 NaN

3 4 Mr.Y 180 NaN

4 5 Jon 170 NaN

5 6 michele sisi 120 NaN

6 7 STEFANO GUST 120 NaN

7 8 Davide Alois 105 NaN

8 9 Cecilia Lala 105 NaN

...

The same operation can be run on any web page that has one or more tables.

Reading Data from XML

In the list of I/O API functions, there is no specific tool regarding the XML (Extensible Markup Language) format. In fact, although it is not listed, this format is very important, because many structured data are available in XML format. This presents no problem, since Python has many other libraries (besides pandas) that manage the reading and writing of data in XML format.

One of these libraries is t he lxml library, which stands out for its excellent performance during the parsing of very large files. In this section you learn how to use this module for parsing XML files and how to integrate it with pandas to finally get the dataframe containing the requested data. For more information about this library, I highly recommend visiting the official website of lxml at http://lxml.de/index.html .

Take for example the XML file shown in Listing 5-11. Write down and save it with the name books.xml di rectly in your working directory.<?xml version="1.0"?>

<Catalog>

<Book id="ISBN9872122367564">

<Author>Ross, Mark</Author>

<Title>XML Cookbook</Title>

<Genre>Computer</Genre>

<Price>23.56</Price>

<PublishDate>2014-22-01</PublishDate>

</Book>

<Book id="ISBN9872122367564">

<Author>Bracket, Barbara</Author>

<Title>XML for Dummies</Title>

<Genre>Computer</Genre>

<Price>35.95</Price>

<PublishDate>2014-12-16</PublishDate>

</Book>

</Catalog>

Listing 5-11books.xml

In this e xample, you will take the data structure described in the XML file to convert it directly into a dataframe. The first thing to do is use the sub-module objectify of the lxml library, importing it in the following way.>>> from lxml import objectify

Now you can do the parser of the XML file with just the parse() function.>>> xml = objectify.parse('books.xml')

>>> xml

<lxml.etree._ElementTree object at 0x0000000009734E08>

You got an object tree, which is an internal data structure of the lxml module.

Look in more detail at this type of object. To navigate in this tree structure, so as to select element by element, you must first define the root. You can do this with th e getroot() function.>>> root = xml.getroot()

Now that the root of the structure has been defined, you can access the various nodes of the tree, each corresponding to the tag contained in the original XML file. The items will have the same name as the corresponding tags. So to select them, simply write the various separate tags with points, reflecting in a certain way the hierarchy of nodes in the tree.>>> root.Book.Author

'Ross, Mark'

>>> root.Book.PublishDate

'2014-22-01'

In this way you access nodes individually, but you can access various elements at the same time usi ng getchildren(). With this function, you’ll get all the child nodes of the reference element.>>> root.getchildren()

[<Element Book at 0x9c66688>, <Element Book at 0x9c66e08>]

With the tag attr ibute you get the name of the tag corresponding to the child node.>>> [child.tag for child in root.Book.getchildren()]

['Author', 'Title', 'Genre', 'Price', 'PublishDate']

While with the text att ribute you get the value contained between the corresponding tags.>>> [child.text for child in root.Book.getchildren()]

['Ross, Mark', 'XML Cookbook', 'Computer', '23.56', '2014-22-01']

However, regardless of the ability to move through t he lxml.etree tree structure, what you need is to convert it into a dataframe. Define the following function, which has the task of analyzing the contents of an eTree to fill a dataframe line by line.>>> def etree2df(root):

... column_names = []

... for i in range(0,len(root.getchildren()[0].getchildren())):

... column_names.append(root.getchildren()[0].getchildren()[i].tag)

... xml:frame = pd.DataFrame(columns=column_names)

... for j in range(0, len(root.getchildren())):

... obj = root.getchildren()[j].getchildren()

... texts = []

... for k in range(0, len(column_names)):

... texts.append(obj[k].text)

... row = dict(zip(column_names, texts))

... row_s = pd.Series(row)

... row_s.name = j

... xml:frame = xml:frame.append(row_s)

... return xml:frame

...

>>> etree2df(root)

Author Title Genre Price PublishDate

0 Ross, Mark XML Cookbook Computer 23.56 2014-22-01

1 Bracket, Barbara XML for Dummies Computer 35.95 2014-12-16

Reading and Writing Data on Microsoft Excel Files

In the previous section, you saw how the data can be easily read from CSV files. It is not uncommon, however, that there are data collected in tabular form in an Excel spreadsheet.

pandas provides specific functions for this type of format. You have seen that the I/O API provides two functions to this purpose: to_excel()

read_excel()

The read_excel() function can read Excel 2003 (.xls) files and Excel 2007 (.xlsx) files. This is possible thanks to the integration of the internal mo dule xlrd.

First, open an Excel file and enter the data as shown in Figure 5-2. Copy the data in sheet1 and sheet2. Then save it as ch05_data.xlsx.

Figure 5-2The two datasets in sheet1 and sheet2 of an Excel file

To read the data contained in the XLS file and convert it into a dataframe, you only have to use the read_excel() function .>>> pd.read_excel('ch05_data.xlsx')

white red green black

a 12 23 17 18

b 22 16 19 18

c 14 23 22 21

As you can see, by default, the returned dataframe is composed of the data tabulated in the first spreadsheets. If, however, you need to load the data in the second spreadsheet, you must then specify the name of the sheet or the number of the sheet (index) just as the second argument.>>> pd.read_excel('ch05_data.xlsx','Sheet2')

yellow purple blue orange

A 11 16 44 22

B 20 22 23 44

C 30 31 37 32

>>> pd.read_excel('ch05_data.xlsx',1)

yellow purple blue orange

A 11 16 44 22

B 20 22 23 44

C 30 31 37 32

The same applies for writing. To convert a dataframe into a spreadsheet on Excel, you have to write the following.>>> frame = pd.DataFrame(np.random.random((4,4)),

... index = ['exp1','exp2','exp3','exp4'],

... columns = ['Jan2015','Fab2015','Mar2015','Apr2005'])

>>> frame

Jan2015 Fab2015 Mar2015 Apr2005

exp1 0.030083 0.065339 0.960494 0.510847

exp2 0.531885 0.706945 0.964943 0.085642

exp3 0.981325 0.868894 0.947871 0.387600

exp4 0.832527 0.357885 0.538138 0.357990

>>> frame.to_excel('data2.xlsx')

In the wor king directory, you will find a new Excel file containing the data, as shown in Figure 5-3.

Figure 5-3The dataframe in the Excel file

JSON Data

JSON (JavaScript Object Notation) has become one of the most common standard formats, especially for the transmission of data on the Web. So it is normal to work with this data format if you want to use data on the Web.

The special feature of this format is its great flexibility, although its structure is far from being the one to which you are well accustomed, i.e., tabular.

In this section you will see how to use th e read_json() and to_json() functions to stay within the I/O API functions discussed in this chapter. But in the second part you will see another example in which you will have to deal with structured data in JSON format much more related to real cases.

In my opinion, a useful online application for checking the JSON format is JSONViewer, available at http://jsonviewer.stack.hu/ . This web application, once you enter or copy data in JSON format, allows you to see if the format you entered is valid. Moreover it displays the tree structure so that you can better understand its structure (see Figure 5-4).

Figure 5-4 JSONViewer

Let’s begin with the more useful case, that is, when you have a dataframe and you need to convert it into a JSON file. So, define a dataframe and then call the to_json() function on it, passing as an argument the name of the file that you want to create.>>> frame = pd.DataFrame(np.arange(16).reshape(4,4),

... index=['white','black','red','blue'],

... columns=['up','down','right','left'])

>>> frame.to_json('frame.json')

In the working directory, you will find a new JSON file (see Listing 5-12) containing the dataframe data translated into JSON format.{"up":{"white":0,"black":4,"red":8,"blue":12},"down":{"white":1,"black":5,"red":9,"blue":13},"right":{"white":2,"black":6,"red":10,"blue":14},"left":{"white":3,"black":7,"red":11,"blue":15}}

Listing 5-12 frame.json

The converse is possible, using the read_json() with the name of the file passed as an argument.>>> pd.read_json('frame.json')

down left right up

black 5 7 6 4

blue 13 15 14 12

red 9 11 10 8

white 1 3 2 0

The example you have seen is a fairly simple case in which the JSON data were in tabular form (since the file frame.json comes from a dataframe). Generally, however, the JSON files do not have a tabular structure. Thus, you will need to somehow convert the structure dict file into tabular form. This process is called normalizatio n.

The library pandas provides a function, called json_normalize(), that is able to convert a dict or a list in a table. First you have to import the function:>>> from pandas.io.json import json_normalize

Then you write a JSON file as described in Listing 5-13 with any text editor. Save it in the working directory as books.json.[{"writer": "Mark Ross",

"nationality": "USA",

"books": [

{"title": "XML Cookbook", "price": 23.56},

{"title": "Python Fundamentals", "price": 50.70},

{"title": "The NumPy library", "price": 12.30}

]

},

{"writer": "Barbara Bracket",

"nationality": "UK",

"books": [

{"title": "Java Enterprise", "price": 28.60},

{"title": "HTML5", "price": 31.35},

{"title": "Python for Dummies", "price": 28.00}

]

}]

Listing 5-13books.json

As you can see, the file structure is no longer tabular, but more complex. Then the approach with th e read_json() function is no longer valid. As you learn from this example, you can still get the data in tabular form from this structure. First you have to load the contents of the JSON file and convert it into a string.>>> import json

>>> file = open('books.json','r')

>>> text = file.read()

>>> text = json.loads(text)

Now you are ready to apply th e json_normalize() function. From a quick look at the contents of the data within the JSON file, for example, you might want to extract a table that contains all the books. Then write the books key as the second argument.>>> json_normalize(text,'books')

price title

0 23.56 XML Cookbook

1 50.70 Python Fundamentals

2 12.30 The NumPy library

3 28.60 Java Enterprise

4 31.35 HTML5

5 28.00 Python for Dummies

The function will read the contents of all the elements that have books as the key. All properties will be converted into nested column names while the corresponding values will fill the dataframe. For the indexes, the function assigns a sequence of increasing numbers.

However, you get a dataframe containing only some internal information. It would be useful to add the values of other keys on the same level. In this case you can add other columns by inserting a key list as the third argument of the function.>>> json_normalize(text,'books',['nationality','writer'])

price title nationality writer

0 23.56 XML Cookbook USA Mark Ross

1 50.70 Python Fundamentals USA Mark Ross

2 12.30 The NumPy library USA Mark Ross

3 28.60 Java Enterprise UK Barbara Bracket

4 31.35 HTML5 UK Barbara Bracket

5 28.00 Python for Dummies UK Barbara Bracket

Now as a result you get a dataframe from a starting tree structure.

The Format HDF5

So far you have seen how to write and read data in text format. When your data analysis involves large amounts of data, it is preferable to use them in binary format. There are several tools in Python to handle binary data. A library that is having some success in this area i s the HDF5 library.

The HDF term stands for hierarchical data format, and in fact this library is concerned with reading and writing HDF5 files containing a structure with nodes and the possibility to store multiple datasets.

This library, fully developed in C, however, has also interfaces with other types of languages like Python, MATLAB, and Java. It is very efficient, especially when using this format to save huge amounts of data. Compared to other formats that work more simply in binary, HDF5 supports compression in real time, thereby taking advantage of repetitive patterns in the data structure to compress the file size.

At present, the possible choices in Python are PyTables and h5py. These two forms differ in several aspects and therefore their choice depends very much on the needs of those who use it.

h5py provides a direct interface with the high-level APIs HDF5, while PyTables makes abstract many of the details of HDF5 to provide more flexible data containers, indexed tables, querying capabilities, and other media on the calculations.

pandas has a class-like dict call ed HDFStore, using PyTables to store pandas objects. So before working with the format HDF5, you must import the HDFStore class:>>> from pandas.io.pytables import HDFStore

Now you’re ready to store the data of a dataframe within an.h5 file. First, create a dataframe.>>> frame = pd.DataFrame(np.arange(16).reshape(4,4),

... index=['white','black','red','blue'],

... columns=['up','down','right','left'])

Now create a file HDF5 calling i t mydata.h5, then enter the data inside of the dataframe.>>> store = HDFStore('mydata.h5')

>>> store['obj1'] = frame

From here, you can guess how you can store multiple data structures within the same HDF5 file, specifying for each of them a label.

>>> frame

up down right left

white 0 0.5 1 1.5

black 2 2.5 3 3.5

red 4 4.5 5 5.5

blue 6 6.5 7 7.5

>>> store['obj2'] = frame

So with this type of format, you can store multiple data structures in a single file, represented by the store variable.>>> store

<class 'pandas.io.pytables.HDFStore'>

File path: mydata.h5

/obj1 frame (shape->[4,4])

Even the reverse process is very simple. Taking account of having an HDF5 file containing various data structures, objects inside can be called in the following way:>>> store['obj2']

up down right left

white 0 0.5 1 1.5

black 2 2.5 3 3.5

red 4 4.5 5 5.5

blue 6 6.5 7 7.5

Pickle—Python Object Serialization

The pickle module implements a powerful algorithm for serialization and deserialization of a data structure implemented in Python. Pickling is the process in which the hierarchy of an object is converted in to a stream of bytes.

This allows an object to be transmitted and stored, and then to be rebuilt by the receiver itself retaining all the original features.

In Python, the picking operation is carried out by the pickle module, but currently there is a module called cP ickle which is the result of an enormous amount of work optimizing the pickle module (written in C). This module can be in fact in many cases even 1,000 times faster than the pickle module. However, regardless of which module you do use, the interfaces of the two modules are almost the same.

Before moving to explicitly mention the I/O functions of pandas that operate on this format, let’s look in more detail at the cPickle module and see how to use it.

Serialize a Python Object with cPickle

The data format used by the pickle (or cPickle) module is specific to Python. By default, an ASCII representation is used to represent it, in order to be readable from the human point of view. Then, by opening a file with a text editor, you may be able to understand its contents. To use this module, you must first import it:>>> import pickle

Then create an object sufficiently complex to have an internal data structure, for example a dict object.>>> data = { 'color': ['white','red'], 'value': [5, 7]}

Now you will perform a serialization of the data object through the dumps() function of the cPickle module.>>> pickled_data = pickle.dumps(data)

Now, to see how it serialized the dict object, you need to look at the contents of the pickled_data variable.>>> print(pickled_data)

(dp1

S'color'

p2

(lp3

S'white'

p4

aS'red'

p5

asS'value'

p6

(lp7

I5

aI7

as.

Once you have serialized data, they can easily be written on a file or sent over a socket, pipe, etc.

After being transmitted, it is possible to reconstruct the serialized object (deserialization) with the loads() function of the cPickle module.>>> nframe = pickle.loads(pickled_data)

>>> nframe

{'color': ['white', 'red'], 'value': [5, 7]}

Pickling with pandas

When it comes to pickling (and unpickling) with the pandas library, everything is much easier. There is no need to import the cPickle module in the Python session and the whole operation is performed implicitly.

Also, the serialization format used by pandas is not completely in ASCII.>>> frame = pd.DataFrame(np.arange(16).reshape(4,4), index = ['up','down','left','right'])

>>> frame.to_pickle('frame.pkl')

There is a new file calle d frame.pkl in your working directory that contains all the information about the frame dataframe.

To open a PKL file and read the contents, simply use this command:>>> pd.read_pickle('frame.pkl')

0 1 2 3

up 0 1 2 3

down 4 5 6 7

left 8 9 10 11

right 12 13 14 15

As you can see, all the implications on the operation of pickling and unpickling are completely hidden from the pandas user, making the job as easy and understandable as possible, for those who must deal specifically with data analysis.

Note

When you use this format make sure that the file you open is safe. Indeed, the pickle format was not designed to be protected against erroneous and maliciously constructed data.

Interacting with Databases

In many applications, the data rarely come from text files, given that this is certainly not the most efficient way to store data.

The data are often stored in an SQL-based relational database, and also in many alternative NoSQL databases that have become very popular in recent times.

Loading data from SQL in a dataframe is sufficiently simple and pandas has some functions to simplify the process.

The pandas.io.sql m odule provides a unified interface independent of the DB, called sqlalchemy. Th is interface simplifies the connection mode, since regardless of the DB, the commands will always be the same. To make a connection you use the create_engine() function. With this feature you can configure all the properties necessary to use the driver, as a user, password, port, and database instance.

Here is a list of examples for the various types of databases:>>> from sqlalchemy import create_engine

For PostgreSQL:>>> engine = create_engine('postgresql://scott:tiger@localhost:5432/mydatabase')

For MySQL

>>> engine = create_engine('mysql+mysqldb://scott:tiger@localhost/foo')

For Oracle

>>> engine = create_engine('oracle://scott:tiger@127.0.0.1:1521/sidname')

For MSSQL

>>> engine = create_engine('mssql+pyodbc://mydsn')

For SQLite

>>> engine = create_engine('sqlite:///foo.db')

Loading and Writing Data with SQLite3

As a first example, you will use a SQLite database using the driver’s built-in Python sqlite3. SQL ite3 is a tool that implements a DBMS SQL in a very simple and lightweight way, so it can be incorporated in any application implemented with the Python language. In fact, this practical software allows you to create an embedded database in a single file.

This makes it the perfect tool for anyone who wants to have the functions of a database without having to install a real database. SQLite3 could be the right choice for anyone who wants to practice before going on to a real database, or for anyone who needs to use the functions of a database to collect data, but remaining within a single program, without having to interface with a database.

Create a dataframe that you will use to create a new table on the SQLite3 database.>>> frame = pd.DataFrame( np.arange(20).reshape(4,5),

... columns=['white','red','blue','black','green'])

>>> frame

white red blue black green

0 0 1 2 3 4

1 5 6 7 8 9

2 10 11 12 13 14

3 15 16 17 18 19

Now it’s time to implement the connection to the SQLite3 database.>>> engine = create_engine('sqlite:///foo.db')

Convert the dataframe in a table within the database.>>> frame.to_sql('colors',engine)

Instead, to read the database, you have to use the read_sql() fun ction with the name of the table and the engine.>>> pd.read_sql('colors',engine)

index white red blue black green

0 0 0 1 2 3 4

1 1 5 6 7 8 9

2 2 10 11 12 13 14

3 3 15 16 17 18 19

As you can see, even in this case, the writing operation on the database has become very simple thanks to the I/O APIs available in the pandas library.

Now you’ll see instead the same operations, but not using the I/O API. This can be useful to get an idea of how pandas proves to be an effective tool for reading and writing data to a database.

First, you must establish a connection to the DB and create a table by defining the corrected data types, so as to accommodate the data to be loaded.>>> import sqlite3

>>> query = """

... CREATE TABLE test

... (a VARCHAR(20), b VARCHAR(20),

... c REAL, d INTEGER

... );"""

>>> con = sqlite3.connect(':memory:')

>>> con.execute(query)

<sqlite3.Cursor object at 0x0000000009E7D730>

>>> con.commit()

Now you can enter data using the SQL INSERT statement.>>> data = [('white','up',1,3),

... ('black','down',2,8),

... ('green','up',4,4),

... ('red','down',5,5)]

>>> stmt = "INSERT INTO test VALUES(?,?,?,?)"

>>> con.executemany(stmt, data)

<sqlite3.Cursor object at 0x0000000009E7D8F0>

>>> con.commit()

Now that you’ve seen how to load the data on a table, it is time to see how to query the database to get the data you just recorded. This is possible using an SQL SELECT statement.>>> cursor = con.execute('select * from test')

>>> cursor

<sqlite3.Cursor object at 0x0000000009E7D730>

>>> rows = cursor.fetchall()

>>> rows

[(u'white', u'up', 1.0, 3), (u'black', u'down', 2.0, 8), (u'green', u'up', 4.0, 4), (u'red', 5.0, 5)]

You can pass the list of tuples to the constructor of the dataframe, and if you need the name of the columns, you can find them within the description attribute of the cursor.>>> cursor.description

(('a', None, None, None, None, None, None), ('b', None, None, None, None, None, None), ('c

one, None, None, None, None), ('d', None, None, None, None, None, None))

>>> pd.DataFrame(rows, columns=zip(*cursor.description)[0])

a b c d

0 white up 1 3

1 black down 2 8

2 green up 4 4

3 red down 5 5

As you can see, this approach is quite laborious.

Loading and Writing Data with PostgreSQL

From pandas 0.14, the PostgreSQL database is also supported. So double-check if the version on your PC corresponds to this version or greater.>>> pd.__version__

>>> '0.22.0'

To run this example, you must have installed on your system a Pos tgreSQL database. In my case I created a database called postgres, with postgres as the user and password as the password. Replace these values with the values corresponding to your system.

The first thing to do is install the psycopg2 library, which is designed to manage and handle the connection with the databases.

With Anaconda:conda install psycopg2

Or if you are using PyPi:pip install psycopg2

Now you can establish a connection with the database:>>> import psycopg2

>>> engine = create_engine('postgresql://postgres:password@localhost:5432/postgres')

Note

In this example, depending on how you installed the package on Windows, often you get the following error message:

from psycopg2._psycopg import BINARY, NUMBER, STRING, DATETIME, ROWID

ImportError: DLL load failed: The specified module could not be found.

This probably means you don’t have the PostgreSQL DLLs (libpq.dll in particular) in your PATH. Add one of the postgres\x.x\bin directories to your PATH and you should be able to connect from Python to your PostgreSQL installations.

Create a dataframe object:>>> frame = pd.DataFrame(np.random.random((4,4)),

index=['exp1','exp2','exp3','exp4'],

columns=['feb','mar','apr','may']);

Now we see how easily you can transfer this data to a table. With to_sql() you will record the data in a table c alled dataframe.>>> frame.to_sql('dataframe',engine)

pgAdmin III is a graphical application for managing PostgreSQL databases. It’s a very useful tool and is present on Linux and Windows. With this application, it is easy to see the table dataframe you just created (see Figure 5-5).

Figure 5-5The pgAdmin II I application is a perfect graphical DB manager for PostgreSQL

If you know the SQL language well, a more classic way to see the new created table and its contents is using a psql session.>>> psql -U postgres

In my case, I am connected to the postgres user; it may be different in your case. Once you’re connected to the database, perform an SQL query on the newly created table.postgres=# SELECT * FROM DATAFRAME;

index| feb | mar | apr | may

-----+-----------------+-----------------+-----------------+-----------------

exp1 |0.757871296789076|0.422582915331819|0.979085739226726|0.332288515791064

exp2 |0.124353978978927|0.273461421503087|0.049433776453223|0.0271413946693556

exp3 |0.538089036334938|0.097041417119426|0.905979807772598|0.123448718583967

exp4 |0.736585422687497|0.982331931474687|0.958014824504186|0.448063967996436

(4 righe)

Even the conversion of a table in a dataframe is a trivial operation. Even here there is a read_sql_table() function that reads directly on the database and returns a dataframe.>>> pd.read_sql_table('dataframe',engine)

index feb mar apr may

0 exp1 0.757871 0.422583 0.979086 0.332289

1 exp2 0.124354 0.273461 0.049434 0.027141

2 exp3 0.538089 0.097041 0.905980 0.123449

3 exp4 0.736585 0.982332 0.958015 0.448064

But when you want to read data in a database, the conversion of a whole and single table into a dataframe is not the most useful operation. In fact, those who work with relational databases prefer to use the SQL language to choose what data and in what form to export the data by inserting an SQL query.

The text of an SQL query can be integrated in the read_sql_query() func tion.>>> pd.read_sql_query('SELECT index,apr,may FROM DATAFRAME WHERE apr > 0.5',engine)

index apr may

0 exp1 0.979086 0.332289

1 exp3 0.905980 0.123449

2 exp4 0.958015 0.448064

Reading and Writing Data with a NoSQL Database: MongoDB

Among all the NoSQL data bases (BerkeleyDB, Tokyo Cabinet, and MongoDB), MongoDB is becoming the most widespread. Given its diffusion in many systems, it seems appropriate to consider the possibility of reading and writing data produced with the pandas library during data analysis.

First, if you have MongoDB installed on your PC, you can start the service to point to a given directory.mongod --dbpath C:\MongoDB_data

Now that the service is listening on port 27017, you can connect to this database using the official driver for MongoDB: pymongo.>>> import pymongo

>>> client = MongoClient('localhost',27017)

A single instance of MongoDB is able to support multiple databases at the same time. So now you need to point to a specific database.>>> db = client.mydatabase

>>> db

Database(MongoClient('localhost', 27017), u'mycollection')

In order to refer to this object, you can also use

>>> client['mydatabase']

Database(MongoClient('localhost', 27017), u'mydatabase')

Now that you have defined the database, you have to define the collection. The collection is a group of documents stored in MongoDB and can be considered the equivalent of the tables in an SQL database.>>> collection = db.mycollection

>>> db['mycollection']

Collection(Database(MongoClient('localhost', 27017), u'mydatabase'), u'mycollection')

>>> collection

Collection(Database(MongoClient('localhost', 27017), u'mydatabase'), u'mycollection')

Now it is the time to load the data in the collection. Create a DataFrame.

>>> frame = pd.DataFrame( np.arange(20).reshape(4,5),

... columns=['white','red','blue','black','green'])

>>> frame

white red blue black green

0 0 1 2 3 4

1 5 6 7 8 9

2 10 11 12 13 14

3 15 16 17 18 19

Before being added to a collection, it must be converted into a JSON format. The conversion process is not as direct as you might imagine; this is because you need to set the data to be recorded on DB in order to be re-extract as DataFrame as fairly and as simply as possible.>>> import json

>>> record = json.loads(frame.T.to_json()).values()

>>> record

[{u'blue': 7, u'green': 9, u'white': 5, u'black': 8, u'red': 6}, {u'blue': 2, u'green': 4, u'white':

0, u'black': 3, u'red': 1}, {u'blue': 17, u'green': 19, u'white': 15, u'black': 18, u'red': 16}, {u

'blue': 12, u'green': 14, u'white': 10, u'black': 13, u'red': 11}]

Now you are finally ready to insert a document in the collection, and you can do this with the insert() fu nction.

>>> collection.mydocument.insert(record)

[ObjectId('54fc3afb9bfbee47f4260357'), ObjectId('54fc3afb9bfbee47f4260358'), ObjectId('54fc3afb9bfbee47f4260359'), Obj ectId('54fc3afb9bfbee47f426035a')]

As you can see, you have an object for each line recorded. Now that the data has been loaded into the document within the MongoDB database, you can execute the reverse process, i.e., reading data in a document and then converting them to a dataframe.>>> cursor = collection['mydocument'].find()

>>> dataframe = (list(cursor))

>>> del dataframe['_id']

>>> dataframe

black blue green red white

0 8 7 9 6 5

1 3 2 4 1 0

2 18 17 19 16 15

3 13 12 14 11 10

You have removed the column containing the ID numbers for the internal reference of Mon goDB.

Conclusions

In this chapter, you saw how to use the features of the I/O API of the pandas library in order to read and write data to files and databases while preserving the structure of the dataframes. In particular, several modes of writing and reading data according to the type of format were illustrated.

In the last part of the chapter, you saw how to interface to the most popular models of databases to record and/or read data into it directly as a dataframe ready to be processed with the pandas tools.

In the next chapter, you’ll see the most advanced features of the library pandas. Complex instruments like the GroupBy and other forms of data processing are discussed in detail.

© Fabio Nelli 2018

Fabio NelliPython Data Analyticshttps://doi.org/10.1007/978-1-4842-3913-1_6

# 06. pandas in Depth: Data Manipulation

Fabio Nelli1

(1)Rome, Italy


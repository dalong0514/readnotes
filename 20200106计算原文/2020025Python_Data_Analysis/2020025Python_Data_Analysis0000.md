# Preface

"Data analysis is Python's killer app."

– Unknown

Data analysis has a rich history in the natural, biomedical, and social sciences. You may have heard of Big Data. Although, it's hard to give a precise definition of Big Data, we should be aware of its impact on data analysis efforts. Currently, we have the following trends associated with Big Data:

- The world's population continues to grow.

- More and more data is collected and stored.

- The number of transistors that can be put on a computer chip cannot grow indefinitely.

- Governments, scientists, industry, and individuals have a growing need to learn from data Data analysis has gained popularity lately due to the hype around Data Science. Data analysis and Data Science attempt to extract information from data. For that purpose, we use techniques from statistics, machine learning, signal processing, natural language processing, and computer science.

A mind map visualizing Python software that can be used for data analysis can be found at http://www.xmind.net/m/WvfC/. The first thing that we should notice is that the Python ecosystem is very mature. It includes famous packages such as NumPy, SciPy, and matplotlib. This should not come as a surprise since Python has been around since 1989. Python is easy to learn and use, less verbose than other programming languages, and very readable. Even if you don't know Python, you can pick up the basics within days, especially if you have experience in another programming language. To enjoy this book, you don't need more than the basics. There are plenty of books, courses, and online tutorials that teach Python.

## 01. What this book covers

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

Appendix B, Useful Functions, gives an overview of functions used in the book. Appendix C, Online Resources, lists links to documentation, forums, articles, and other important information.

## 02. What you need for this book

The code examples in this book should work on most modern operating systems. For all chapters, Python 2 and pip is required. To install Python, go to https://wiki.python.org/moin/BeginnersGuide/Download. To install pip, go to http://pip.readthedocs.org/en/latest/installing.html. Instructions to install software are given throughout the chapters. Most of the time, we need to run the following command with admin privileges:

    $ pip install <some software>

The following is a list of software used for the examples and versions used for testing purposes:

## 03. Who this book is for

This book is for people with basic knowledge of Python and Mathematics who want to learn how to use Python software to analyze data. We try to keep things simple, but it's not possible to cover all the topics in great detail. It may be useful for you to refresh your knowledge of Mathematics via Khan Academy, Coursera, or Wikipedia. I would recommend the following books by Packt Publishing for further reading:

- Building Machine Learning Systems with Python, Willi Richert and Luis Pedro Coelho (2013)

- Learning Cython Programming, Philip Herron (2013)

- Learning NumPy Array, Ivan Idris (2014)

- Learning scikit-learn: Machine Learning in Python, Raúl Garreta and Guillermo Moncecchi (2013)

- Learning SciPy for Numerical and Scientific Computing, Francisco J. Blanco-Silva (2013)

- Matplotlib for Python Developers, Sandro Tosi (2009)

- NumPy Beginner's Guide - Second Edition, Ivan Idris (2013)

- NumPy Cookbook, Ivan Idris (2012)

- Parallel Programming with Python, Jan Palach (2014)

- Python Data Visualization Cookbook, Igor Milovanović (2013)

- Python for Finance, Yuxing Yan (2014)

- Python Text Processing with NLTK 2.0 Cookbook, Jacob Perkins (2010)

## 04. Conventions

In this book, you will find a number of styles of text that distinguish between different kinds of information. Here are some examples of these styles, and an explanation of their meaning.

Code words in text, database table names, folder names, filenames, file extensions, pathnames, dummy URLs, user input, and Twitter handles are shown as follows: "Notice that numpysum() does not need a for loop."

A block of code is set as follows:

```
def pythonsum(n):
    a = range(n) 
    b = range(n) 
    c = []

for i in range(len(a)):
    a[i] = i ** 2
    b[i] = i ** 3

c.append(a[i] + b[i])

return c
```

Any command-line input or output is written as follows:

    $ yum install python-numpy

New terms and important words are shown in bold. Words that you see on the screen, in menus or dialog boxes for example, appear in the text like this: "Click on the Next button."

Warnings or important notes appear in a box like this.

Tips and tricks appear like this.

## 05. Customer support

Now that you are the proud owner of a Packt book, we have a number of things to help you to get the most from your purchase.

### 1. Downloading the example code

You can download the example code files for all Packt books you have purchased from your account at http://www.packtpub.com. If you purchased this book elsewhere, you can visit http://www.packtpub.com/support and register to have the files e-mailed directly to you.

[Support | Help Centre for all things Packt](https://www.packtpub.com/support)

### 2. Errata

Although we have taken every care to ensure the accuracy of our content, mistakes do happen. If you find a mistake in one of our books — maybe a mistake in the text or the code—we would be grateful if you would report this to us. By doing so, you can save other readers from frustration and help us improve subsequent versions of this book. If you find any errata, please report them by visiting http://www.packtpub.com/submit-errata, selecting your book, clicking on the errata submission form link, and entering the details of your errata. Once your errata are verified, your submission will be accepted and the errata will be uploaded on our website, or added to any list of existing errata, under the Errata section of that title. Any existing errata can be viewed by selecting your title from http://www.packtpub.com/support.

### 3. Questions

You can contact us at questions@packtpub.com if you are having a problem with any aspect of the book, and we will do our best to address it.



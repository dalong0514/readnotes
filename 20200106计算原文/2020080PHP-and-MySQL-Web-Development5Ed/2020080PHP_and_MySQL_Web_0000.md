Copyright © 2017 by Pearson Education, Inc.

## Introduction

Welcome to PHP and MySQL Web Development. Within its pages, you will find distilled knowledge from our experiences using PHP and MySQL, two of the most important and widely used web development tools around. Key topics covered in this introduction include:

 ■ Why you should read this book.

 ■ What you will be able to achieve using this book.

 ■ What PHP and MySQL are and why they’re great.

 ■ What’s changed in the latest versions of PHP and MySQL.

 ■ How this book is organized.

Let’s get started.

Note: Visit our website and register this book at informit.com/register for convenient access to any updates, downloads, or errata that might be available for this book.

### 1. Why You Should Read This Book

This book will teach you how to create interactive web applications from the simplest order form through to complex, secure web applications. What’s more, you’ll learn how to do it using open-source technologies.

This book is aimed at readers who already know at least the basics of HTML and have done some programming in a modern programming language before but have not necessarily programmed for the web or used a relational database. If you are a beginning programmer, you should still find this book useful, but digesting it might take a little longer. We’ve tried not to leave out any basic concepts, but we do cover them at speed. The typical readers of this book want to master PHP and MySQL for the purpose of building a large or commercial website. You might already be working in another web development language; if so, this book should get you up to speed quickly.

We wrote the first edition of this book because we were tired of finding PHP books that were basically function references. These books are useful, but they don’t help when your boss or client has said,「Go build me a shopping cart.」In this book, we have done our best to make every example useful. You can use many of the code samples directly in your website, and you can use many others with only minor modifications.

### 2. What You Will Learn from This Book

Reading this book will enable you to build real-world, dynamic web applications. If you’ve built websites using plain HTML, you realize the limitations of this approach. Static content from a pure HTML website is just that—static. It stays the same unless you physically update it. Your users can’t interact with the site in any meaningful fashion.

Using a language such as PHP and a database such as MySQL allows you to make your sites dynamic: to have them be customizable and contain real-time information.

We have deliberately focused this book on real-world applications, even in the introductory chapters. We begin by looking at simple systems and work our way through the various parts of PHP and MySQL.

We then discuss aspects of security and authentication as they relate to building a real-world website and show you how to implement these aspects in PHP and MySQL. We also introduce you to integrating front-end and back-end technologies by discussing JavaScript and the role it can play in your application development.

In the final part of this book, we describe how to approach real-world projects and take you through the design, planning, and building of the following projects:

 ■ User authentication and personalization

 ■ Web-based email

 ■ Social media integration

You should be able to use any of these projects as is, or you can modify them to suit your needs. We chose them because we believe they represent some the most common web  applications built by programmers. If your needs are different, this book should help you along the way to achieving your goals.

### 3. What Is PHP?

PHP is a server-side scripting language designed specifically for the web. Within an HTML page, you can embed PHP code that will be executed each time the page is visited. Your PHP code is interpreted at the web server and generates HTML or other output that the visitor will see.

PHP was conceived in 1994 and was originally the work of one man, Rasmus Lerdorf. It was adopted by other talented people and has gone through several major rewrites to bring us the broad, mature product we see today. According to Google’s Greg Michillie in May 2013, PHP ran more than three quarters of the world’s websites, and that number had grown to over 82% by July 2016.

PHP is an open-source project, which means you have access to the source code and have the freedom to use, alter, and redistribute it.

PHP originally stood for Personal Home Page but was changed in line with the GNU recursive naming convention (GNU = Gnu’s Not Unix) and now stands for PHP Hypertext Preprocessor.

The current major version of PHP is 7. This version saw a complete rewrite of the underlying Zend engine and some major improvements to the language. All of the code in this book has been tested and validated against the most recent release of PHP 7 at the time of writing, as well as the latest version in the PHP 5.6 family of releases, which is still officially supported.

The home page for PHP is available at http://www.php.net.

The home page for Zend Technologies is http://www.zend.com.

### 4. What Is MySQL?

MySQL (pronounced My-Ess-Que-Ell) is a very fast, robust, relational database management system (RDBMS). A database enables you to efficiently store, search, sort, and retrieve data. The MySQL server controls access to your data to ensure that multiple users can work with it concurrently, to provide fast access to it, and to ensure that only authorized users can obtain access. Hence, MySQL is a multiuser, multithreaded server. It uses Structured Query Language (SQL), the standard database query language. MySQL has been publicly available since 1996 but has a development history going back to 1979. It is the world’s most popular open-source database and has won the Linux Journal Readers’ Choice Award on a number of occasions.

MySQL is available under a dual licensing scheme. You can use it under an open-source license (the GPL) free as long as you are willing to meet the terms of that license. If you want to distribute a non-GPL application including MySQL, you can buy a commercial license instead.

### 5. Why Use PHP and MySQL?

When setting out to build a website, you could use many different products.

You need to choose the following:

 ■ Where to run your web servers: the cloud, virtual private servers, or actual hardware

 ■ An operating system

 ■ Web server software

 ■ A database management system or other datastore

 ■ A programming or scripting language

You may end up with a hybrid architecture with multiple datastores. Some of these choices are dependent on the others. For example, not all operating systems run on all hardware, not all web servers support all programming languages, and so on.

In this book, we do not pay much attention to hardware, operating systems, or web server software. We don’t need to. One of the best features of both PHP and MySQL is that they work with any major operating system and many of the minor ones.

The majority of PHP code can be written to be portable between operating systems and web servers. There are some PHP functions that specifically relate to the filesystem that are operating system dependent, but these are clearly marked as such in the manual and in this book.

Whatever hardware, operating system, and web server you choose, we believe you should seriously consider using PHP and MySQL.

### 6. Some of PHP’s Strengths

Some of PHP’s main competitors are Python, Ruby (on Rails or otherwise), Node.js, Perl, Microsoft .NET, and Java.

In comparison to these products, PHP has many strengths, including the following:

 ■ Performance

 ■ Scalability

 ■ Interfaces to many different database systems

 ■ Built-in libraries for many common web tasks

 ■ Low cost

 ■ Ease of learning and use

 ■ Strong object-oriented support

 ■ Portability

 ■ Flexibility of development approach

 ■ Availability of source code

 ■ Availability of support and documentation

A more detailed discussion of these strengths follows.

#### Performance

PHP is very fast. Using a single inexpensive server, you can serve millions of hits per day. It scales down to the smallest email form and up to sites such as Facebook and Etsy.

#### Scalability

PHP has what Rasmus Lerdorf frequently refers to as a「shared-nothing」architecture. This means that you can effectively and cheaply implement horizontal scaling with large numbers of commodity servers.

### Database Integration

PHP has native connections available to many database systems. In addition to MySQL, you can directly connect to PostgreSQL, Oracle, MongoDB, and MSSQL, among others. PHP 5 and PHP 7 also have a built-in SQL interface to flat files, called SQLite.

Using the Open Database Connectivity (ODBC) standard, you can connect to any database that provides an ODBC driver. This includes Microsoft products and many others.

In addition to native libraries, PHP comes with a database access abstraction layer called PHP Database Objects (PDOs), which allows consistent access and promotes secure coding practices.

#### Built-in Libraries

Because PHP was designed for use on the Web, it has many built-in functions for performing many useful web-related tasks. You can generate images on the fly, connect to web services and other network services, parse XML, send email, work with cookies, and generate PDF documents, all with just a few lines of code.

#### Cost

PHP is free. You can download the latest version at any time from http://www.php.net for no charge.

#### Ease of Learning PHP

The syntax of PHP is based on other programming languages, primarily C and Perl. If you already know C or Perl, or a C-like language such as C++ or Java, you will be productive using PHP almost immediately.

#### Object-Oriented Support

PHP version 5 had well-designed object-oriented features, which continued to be refined and improved in PHP version 7. If you learned to program in Java or C++, you will find the features (and generally the syntax) that you expect, such as inheritance, private and protected attributes and methods, abstract classes and methods, interfaces, constructors, and destructors. You will even find some less common features such as iterators and traits.

#### Portability

PHP is available for many different operating systems. You can write PHP code on free UNIX-like operating systems such as Linux and FreeBSD, commercial UNIX versions, OS X, or on different versions of Microsoft Windows.

Well-written code will usually work without modification on a different system running PHP.

### Flexibility of Development Approach

PHP allows you to implement simple tasks simply, and equally easily adapts to implementing large applications using a framework based on design patterns such as Model-View-Controller (MVC).

#### Source Code

You have access to PHP’s source code. With PHP, unlike commercial, closed-source products, if you want to modify something or add to the language, you are free to do so.

You do not need to wait for the manufacturer to release patches. You also don’t need to worry about the manufacturer going out of business or deciding to stop supporting a product.

### Availability of Support and Documentation

Zend Technologies ([Enterprise PHP | Zend by Perforce](https://www.zend.com/)), the company behind the engine that powers PHP, funds its PHP development by offering support and related software on a commercial basis.

The PHP documentation and community are mature and rich resources with a wealth of information to share.

### 7. Key Features of PHP 7

In December 2015, the long-awaited PHP 7 release was made available to the public. As mentioned in this introduction, the book covers both PHP 5.6 and PHP 7, which might lead you to ask「what happened to PHP 6?」The short answer is: there is no PHP 6 and never was for the general public. There was a development effort around a codebase that was referred to as「PHP 6」but it never came to fruition; there were many ambitious plans and subsequent complications that made it difficult for the team to continue to pursue. PHP 7 is not PHP 6 and doesn’t include the features and code from that development effort; PHP 7 is its own release with its own focus—specifically a focus on performance.

Under the hood, PHP 7 includes a refactor of the Zend Engine that powers it, which resulted in a significant performance boost to many web applications—sometimes upwards of 100%! While increased performance and decreased memory use were key to the release of PHP 7, so was backward-compatibility. In fact, relatively few backward-incompatible language changes were introduced. These are discussed contextually throughout this book so that the chapters remain usable with PHP 5.6 or PHP 7, as widespread adoption of PHP 7 has not yet occurred by commercial web-hosting providers.

### 8. Some of MySQL’s Strengths

MySQL’s main competitors in the relational database space are PostgreSQL, Microsoft SQL Server, and Oracle. There is also a growing trend in the web application world toward use of NoSQL/non-relational databases such as MongoDB. Let’s take a look at why MySQL is still a good choice in many cases.

MySQL has many strengths, including the following:

 ■ High performance

 ■ Low cost

 ■ Ease of configuration and learning

 ■ Portability

 ■ Availability of source code

 ■ Availability of support

A more detailed discussion of these strengths follows.

#### Performance

MySQL is undeniably fast. You can see the developers’ benchmark page at http://www.mysql.com/why-mysql/benchmarks/.

#### Low Cost

MySQL is available at no cost under an open-source license or at low cost under a commercial license. You need a license if you want to redistribute MySQL as part of an application and do not want to license your application under an open-source license. If you do not intend to distribute your application—typical for most web applications—or are working on free or open-source software, you do not need to buy a license.

#### Ease of Use

Most modern databases use SQL. If you have used another RDBMS, you should have no trouble adapting to this one. MySQL is also easier to set up and tune than many similar products.

#### Portability

MySQL can be used on many different UNIX systems as well as under Microsoft Windows.

#### Source Code

As with PHP, you can obtain and modify the source code for MySQL. This point is not important to most users most of the time, but it provides you with excellent peace of mind, ensuring future continuity and giving you options in an emergency.

In fact, there are now several forks and drop-in replacements for MySQL that you may consider using, including MariaDB, written by the original authors of MySQL, including Michael ‘Monty’ Widenius (https://mariadb.org).

#### Availability of Support

Not all open-source products have a parent company offering support, training, consulting, and certification, but you can get all of these benefits from Oracle (who acquired MySQL with their acquisition of Sun Microsystems, who had previously acquired the founding company, MySQL AB).

### 9. What Is New in MySQL (5.x)?

At the time of writing, the current version of MySQL was 5.7.

Features added to MySQL in the last few releases include:

 ■ A wide range of security improvements

 ■ FULLTEXT support for InnoDB tables

 ■ A NoSQL-style API for InnoDB

 ■ Partitioning support

 ■ Improvements to replication, including row-based replication and GTIDs

 ■ Thread pooling

 ■ Pluggable authentication

 ■ Multicore scalability

 ■ Better diagnostic tools

 ■ InnoDB as the default engine

 ■ IPv6 support

 ■ Plugin API

 ■ Event scheduling

 ■ Automated upgrades

Other changes include more ANSI standard compliance and performance improvements.

If you are still using an early 4.x version or a 3.x version of the MySQL server, you should know that the following features were added to various versions from 4.0:

 ■ Views

 ■ Stored procedures

 ■ Triggers and cursors

 ■ Subquery support

 ■ GIS types for storing geographical data

 ■ Improved support for internationalization

 ■ The transaction-safe storage engine InnoDB included as standard

 ■ The MySQL query cache, which greatly improves the speed of repetitive queries as often run by web applications

### 10. How Is This Book Organized?

This book is divided into five main parts:

Part I,「Using PHP,」provides an overview of the main parts of the PHP language with examples. Each example is a real-world example used in building an e-commerce site rather than「toy」code. We kick off this section with Chapter 1,「PHP Crash Course.」If you’ve already used PHP, you can whiz through this chapter. If you are new to PHP or new to programming, you might want to spend a little more time on it.

Part II,「Using MySQL,」discusses the concepts and design involved in using relational database systems such as MySQL, using SQL, connecting your MySQL database to the world with PHP, and advanced MySQL topics, such as security and optimization.

Part III,「Web Application Security,」covers some of the general issues involved in developing a web application using any language. We then discuss how you can use PHP and MySQL to authenticate your users and securely gather, transmit, and store data.

Part IV,「Advanced PHP Techniques,」offers detailed coverage of some of the major built-in functions in PHP. We have selected groups of functions that are likely to be useful when building a web application. You will learn about interaction with the server, interaction with the network, image generation, date and time manipulation, and session handling.

Part V,「Building Practical PHP and MySQL Projects,」is our favorite section. It deals with practical real-world issues such as managing large projects and debugging, and provides sample projects that demonstrate the power and versatility of PHP and MySQL.

### 11. Accessing the Free Web Edition

Your purchase of this book in any format includes access to the corresponding Web Edition, which provides several special features to help you learn:

 ■ The complete text of the book online

 ■ Interactive quizzes and exercises to test your understanding of the material

 ■ Bonus chapters not included in the print or e-book editions

 ■ Updates and corrections as they become available

The Web Edition can be viewed on all types of computers and mobile devices with any modern web browser that supports HTML5.

To get access to the Web Edition of PHP and MySQL Web Development, Fifth Edition all you need to do is register this book:

1.  Go to www.informit.com/register.

2.  Sign in or create a new account.

3.  Enter ISBN: 9780321833891.

4.  Answer the questions as proof of purchase.

The Web Edition will appear under the Digital Purchases tab on your Account page. Click the Launch link to access the product.

### Finally

We hope you enjoy this book and enjoy learning about PHP and MySQL as much as we did when we first began using these products. They are really a pleasure to use. Soon, you’ll be able to join the many thousands of web developers who use these robust, powerful tools to easily build dynamic, real-time web applications.

## Contents at a Glance

Introduction

### I: Using PHP

  1  PHP Crash Course  

  2  Storing and Retrieving Data  

  3  Using Arrays  

  4  String Manipulation and Regular Expressions  

  5  Reusing Code and Writing Functions  

  6  Object-Oriented PHP  

  7  Error and Exception Handling  

### II: Using MySQL

  8  Designing Your Web Database   

  9  Creating Your Web Database 
  
  10  Working with Your MySQL Database  

  11  Accessing Your MySQL Database from the Web with PHP  

  12  Advanced MySQL Administration  

  13  Advanced MySQL Programming  

### III: Web Application Security

  14  Web Application Security Risks

  15  Building a Secure Web Application

  16  Implementing Authentication Methods with PHP  

### IV: Advanced PHP Techniques

  17  Interacting with the File System and the Server

  18  Using Network and Protocol Functions 

  19  Managing the Date and Time 

  20  Internationalization and Localization 

  21  Generating Images 

  22  Using Session Control in PHP 

  23  Integrating JavaScript and PHP 

  24  Other Useful Features 

### V: Building Practical PHP and MySQL Projects

  25  Using PHP and MySQL for Large Projects

  26  Debugging and Logging 

  27  Building User Authentication and Personalization 

  28  Building a Web-Based Email Service with Laravel Part I  Web Edition

  29  Building a Web-Based Email Service with Laravel Part II  Web Edition

  30  Social Media Integration Sharing and Authentication  Web Edition

  31  Building a Shopping Cart  Web Edition

  VI: Appendix

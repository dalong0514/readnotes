## 记忆时间

英文第 5 版的出版时间：2016 年 9 月

## 卡片

### 0101. 主题卡 ——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡 —— `$_POST`、 `$_GET` 和 `$_REQUEST`

\$\_POST, \$\_GET, and \$\_REQUEST. One of the \$\_GET or \_POST arrays holds the details of all the form variables. Which array is used depends on whether the method used to submit the form was GET or POST, respectively. In addition, a combination of all data submitted via GET or POST is also available through \$_REQUEST.

If the form was submitted via the POST method, the data entered in the tireqty box will be stored in \$\_POST['tireqty']. If the form was submitted via GET, the data will be in \$_GET['tireqty']. In either case, the data will also be available in \$\_REQUEST['tireqty']. These arrays are some of the superglobal arrays. We will revisit the superglobals when we discuss variable scope later in this chapter.

### 0202. 术语卡 —— Variable Variables

Variable Variables. PHP provides one other type of variable: the variable variable. Variable variables enable you to change the name of a variable dynamically. As you can see, PHP allows a lot of freedom in this area. All languages enable you to change the value of a variable, but not many allow you to change the variable’s type, and even fewer allow you to change the variable’s name.  A variable variable works by using the value of one variable as the name of another. For example, you could set:

    $varname = 'tireqty';

You can then use \$\$varname in place of \$tireqty. For example, you can set the value of \$tireqty as follows:

    $$varname = 5;

This is equivalent to

    $tireqty = 5;

一个应用场景是与 for 循环结合。

you can combine variable variables with a for loop to iterate through a series of repetitive form fields. If, for example, you have form fields with names such as name1, name2, name3, and so on, you can process them like this:

```php
for ($i=1; $i <= $numnames; $i++) {  
    $temp= "name$i";  
    // 对 $$temp 操作，比如赋值、计算之类的，相当于对一系列 name1、name2、name3...操作
    echo htmlspecialchars($$temp).'<br />'; // or whatever processing you want to do
}
```

By dynamically creating the names of the variables, you can access each of the fields in turn. 

### 0203. 术语卡 —— RFCs

The fourth parameter can be used to send any additional valid email headers. Valid email headers are described in the document RFC822, which is available online if you want more details. (RFCs, or Requests for Comment, are the source of many Internet standards; we discuss them in Chapter 18「Using Network and Protocol Functions.」) 

### 0204. 术语卡 —— conversion specification

The %s in the format string is called a conversion specification. This one means「replace with a string.」In this case, it is replaced with \$total interpreted as a string. If the value stored in \$total was 12.4, both of these approaches would print it as 12.4. The advantage of printf() is that you can use a more useful conversion specification to specify that \$total is actually a floating-point number and that it should have two decimal places after the decimal point, as follows:

```php
printf ("Total amount of order is %.2f", $total);
```

Given this formatting, and 12.4 stored in \$total, this statement will print as 12.40. You can have multiple conversion specifications in the format string. If you have n conversion specifications, you will usually have n arguments after the format string. Each conversion speci-fication will be replaced by a reformatted argument in the order they are listed. 

```php
%[+]['padding_character][-][width][.precision]type
```

All conversion specifications start with a % symbol. If you actually want to print a % symbol, you need to use %%. The + sign is optional. By default, only numbers that are negative show a sign (in this case -). If you specify a sign here then positive values will be prefixed with the + sign and negative values will be prefixed with the - sign.

The padding\_character is optional. It is used to pad your variable to the width you have specified. An example would be to add leading zeros to a number like a counter. The default padding character is a space. If you are specifying a space or zero, you do not need to prefix it with the apostrophe ('). For any other padding character, you need to prefix it with an apostrophe.

The - symbol is optional. It specifies that the data in the field will be left-justified rather than right-justified, which is the default. The width specifier tells printf() how much room (in characters) to leave for the variable to be substituted in here. The precision specifier should begin with a decimal point. It should contain the number of places after the decimal point you would like displayed. The final part of the specification is a type code. A summary of these codes is shown in Table 4.3.

```php
printf ("Total amount of order is %2\$.2f (with shipping %1\$.2f) ",           
            $total_shipping, $total);
```

Just add the argument position in the list directly after the % sign, followed by an escaped \$ symbol; in this example, 2\$ means「replace with the second argument in the list.」This method can also be used to repeat arguments. Two alternative versions of these functions are called vprintf() and vsprintf(). These  variants accept two parameters: the format string and an array of the arguments rather than a variable number of parameters.

### 0301. 人名卡 —— Luke Welling

Luke Welling，本书的作者，PHP 以及 web 开发的大牛。

### 0401. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 书评

### 02

为了备战面试：我没有考上理想的研究院，就业的压力再一次摆在了我的面前。记得当初做毕业设计使用的 asp.net2.0 技术，发现网上已经开始使用 3.0+ 了。而且又在网上看到，说用 .net 做网站的程序员挣不了多少钱。再加上，我也不太喜欢 visual studio（我讨厌自动生成模板，就像《程序员修炼之道》中「邪恶的向导」所提到的一样）。这时，我想到了另一种语言 php（大学没接触 jsp 或是什么别的语言了）。那是距离我规定的找工作时间还有一个多月，我又一次拿出了这本书，开始从头看起。书的内容不用说自然是一本好书，从最简单的 php 标记开始讲起，然后的变量，逻辑，操作符，读写文件，使用数组，正则表达式，处理字符串，最后的面向对象的基本支持。讲完 php 后开始教授 mysql，然后是一些我认为的废话（电子商务与安全性），再然后的一些进阶的 php 知识，包括文件上传，网络函数，日期管理，创建图片，会话控制等，最后是一大堆的实例。因为时间的关系，我实现了购物车功能的那个实例（当时看到了 500 页）就急匆匆的开始投简历去了。

小小的打击： 记得当时面试 ZOL 时我还特意拿着这本书，面试官看我没有任何的工作经验，就把我叫到了一旁，问我：你虽然没有工作经验，但公司很喜欢你身上那种精神，你和另外两位已经进入了最后一轮面试。当时真没想到自己会这么幸运。我们三个人进入了一个小小的房间，面试官是 cto。在几个试探性的问题后，他看出了我的技术经验不足，从他的眼神中我看到，他想给我机会，但是我还不能达到他的目标。他看了我一眼，说：好吧，我问大家最后一个问题。如果我想用 mysql 降序排列一组数据，我该如何办？ 他手指指向我，让我第一个回答，显然这个问题对于另外两个人实在是太简单了。他希望通过我回答出这个问题，给我一次在这里工作的机会。我想了一下，说： 用 select top 然后跟。。。。他打断了我，并让另外两个人回答。显然我的答案是错的。就这样我的第一次面试失败了。出来后我翻遍了一整本书都没有找到为什么不能用 top（我把 mysql 和 sqlserver 记混了）。这件事情告诉我，学习任何技术一定要踏实，在去尝试新技术之前，应该熟练掌握已学习的知识。让他们变得更加的扎实！

遗忘： 我运气好，没经过太多波折就找到了一份工作，在那里干了二年三个月的时间。工作的压力让我淡忘了自己对 php 基础知识的不足。更多的时间拖入到跟框架有关的工作中，也没有在意自己的底子是不是扎实。那时候就想说，把工作任务先完成，书以后再学。就这样，两年的时间一下子就过去了。

重逢： 当我再次拿起他的时候，已经是我决定要离开第一家公司的时候。我希望可以去更加有发展的公司，但我也想起了第一次面试留给我的惨痛的经验教训。我现在应该把基础打牢！ 所以我再一次从书柜里面拿出了他。再一次从第一页开始读起，不管内容多么简单，我也认真的学习。虽然现在看来，后面的实例已经显得不那么实用，传授的知识也是很基础的，但是每当我翻开他的时候，看到的不仅仅是一个个知识点，更多的是当时学习 php 时的自己的模样。

### 03

[PHP 和 MySQL Web 应用开发核心技术（Core Web Application Development with PHP and MySQL）](https://book.douban.com/subject/1824542/)

上面这个链接的书名字叫《PHP 和 MySQL Web 应用开发核心技术》（以后我们简称「web 核心」），不管是名字还是书皮都跟这本书非常像，如果你都读过的话，会感觉里面的章节安排也是非常像的。我评论的这本书（以后简称「web 开发」，和「web 核心」区分开）由于被他的「圣经」光环所笼罩，所以当我拿到「web 核心」这本书的时候，感觉他其实就是在抄袭「web 开发」，不值得去阅读，但是当我有一次无意读了他其中的某些章节的时候，我感觉「web 核心」比「web 开发」更胜一筹，具体哪里更好，我现在已经无法细数了，现在只是留有印象：前者比后者讲的更清楚明白，项目开发中的经验讲的更多，新技术新思想也涉及的更多等等。

如果还要深入研究的话，上面两本书都不够，推荐下面这本书，PHP 5 权威编程：[PHP 5 权威编程](https://book.douban.com/subject/2981954/)。里面的代码优化和扩展开发部分对想深入学习的人非常有用！

2『以下载原文书籍「2020087Core_Web_Application_Development_with_」以及「2020090PHP5_Power_Programming」。』

### 06

《PHP 和 MySQL Web 开发》（SAMS）风格类似散文，精髓就是形散神不散，牢牢抓住「web 开发」的主旨，粗看前两篇（记得是 1-14 章）会让人感觉「东一榔头西一棒」，提了下显示动态内容，即刻就带到使用函数。这粗看让人觉得有些乱，但实际上这种写作风格却更好的体现了本书作者的思想，他把实践看的很重，所以几乎每篇每节都是围绕一个实例在做诠释，而因此本书的精髓则在后三篇。但正如上面一位老师说的，它没有详细的函数说明。

《PHP 与 MySQL 5 程序设计》（Apress）则是「说明文」，详细严谨的逐步解释每个概念，本书的读者能够了解并熟悉 php 和 mysql 技术中的各个细节，这非常适合刚入门的初学者，甚至你无需了解更多的相关内容（如 asp，c 语言）就能够看懂本书。而讲到的各个细节，则是说本书对函数做了大篇幅的说明，这是本书的一个特色。

## Preface

Welcome to PHP and MySQL Web Development. Within its pages, you will find distilled knowledge from our experiences using PHP and MySQL, two of the most important and widely used web development tools around. Key topics covered in this introduction include: 1) Why you should read this book. 2) What you will be able to achieve using this book. 3) What PHP and MySQL are and why they’re great. 4) What’s changed in the latest versions of PHP and MySQL. 5) How this book is organized.

Why You Should Read This Book. This book will teach you how to create interactive web applications from the simplest order form through to complex, secure web applications. What’s more, you’ll learn how to do it using open-source technologies. We wrote the first edition of this book because we were tired of finding PHP books that were basically function references. These books are useful, but they don’t help when your boss or client has said,「Go build me a shopping cart.」In this book, we have done our best to make every example useful. You can use many of the code samples directly in your website, and you can use many others with only minor modifications.

What You Will Learn from This Book. Reading this book will enable you to build real-world, dynamic web applications. If you’ve built websites using plain HTML, you realize the limitations of this approach. Static content from a pure HTML website is just that — static. It stays the same unless you physically update it. Your users can’t interact with the site in any meaningful fashion. Using a language such as PHP and a database such as MySQL allows you to make your sites dynamic: to have them be customizable and contain real-time information.

1『使用「PHP and a database」可以实现动态网页。』

We have deliberately focused this book on real-world applications, even in the introductory chapters. We begin by looking at simple systems and work our way through the various parts of PHP and MySQL. We then discuss aspects of security and authentication as they relate to building a real-world website and show you how to implement these aspects in PHP and MySQL. We also introduce you to integrating front-end and back-end technologies by discussing JavaScript and the role it can play in your application development.

1『前端和后端技术的英文名找到了，「front-end」和「back-end」。』

In the final part of this book, we describe how to approach real-world projects and take you through the design, planning, and building of the following projects: 1) User authentication and personalization. 2) Web-based email. 3) Social media integration.

You should be able to use any of these projects as is, or you can modify them to suit your needs. We chose them because we believe they represent some the most common web  applications built by programmers. If your needs are different, this book should help you along the way to achieving your goals.

What Is PHP? PHP is a server-side scripting language designed specifically for the web. Within an HTML page, you can embed PHP code that will be executed each time the page is visited. Your PHP code is interpreted at the web server and generates HTML or other output that the visitor will see.

1『 PHP 是服务端的脚本语言，其代码是在服务器端解释完成的，然后以 HTML 的格式返回给客户端，比如浏览器。PHP 是开源的。』

PHP was conceived in 1994 and was originally the work of one man, Rasmus Lerdorf. It was adopted by other talented people and has gone through several major rewrites to bring us the broad, mature product we see today. According to Google’s Greg Michillie in May 2013, PHP ran more than three quarters of the world’s websites, and that number had grown to over 82% by July 2016. PHP is an open-source project, which means you have access to the source code and have the freedom to use, alter, and redistribute it. PHP originally stood for Personal Home Page but was changed in line with the GNU recursive naming convention (GNU = Gnu’s Not Unix) and now stands for PHP Hypertext Preprocessor.

1『 PHP 起源于个人主页（personal home page）。』

The current major version of PHP is 7. This version saw a complete rewrite of the underlying Zend engine and some major improvements to the language. All of the code in this book has been tested and validated against the most recent release of PHP 7 at the time of writing, as well as the latest version in the PHP 5.6 family of releases, which is still officially supported.

What Is MySQL? MySQL (pronounced My-Ess-Que-Ell) is a very fast, robust, relational database management system (RDBMS). A database enables you to efficiently store, search, sort, and retrieve data. The MySQL server controls access to your data to ensure that multiple users can work with it concurrently, to provide fast access to it, and to ensure that only authorized users can obtain access. Hence, MySQL is a multiuser, multithreaded server. It uses Structured Query Language (SQL), the standard database query language. MySQL has been publicly available since 1996 but has a development history going back to 1979. It is the world’s most popular open-source database and has won the Linux Journal Readers’ Choice Award on a number of occasions.

1『数据库可以让我们非常有效的存储、搜索、排序和提取数据；数据能让很多人同访问数据，而且可以给访问的人设置不同的权限。』

Why Use PHP and MySQL? When setting out to build a website, you could use many different products. You need to choose the following: 1) Where to run your web servers: the cloud, virtual private servers, or actual hardware. 2) An operating system. 3) Web server software. 4) A database management system or other datastore. 5) A programming or scripting language.

You may end up with a hybrid architecture with multiple datastores. Some of these choices are dependent on the others. For example, not all operating systems run on all hardware, not all web servers support all programming languages, and so on. In this book, we do not pay much attention to hardware, operating systems, or web server software. We don’t need to. One of the best features of both PHP and MySQL is that they work with any major operating system and many of the minor ones.

The majority of PHP code can be written to be portable between operating systems and web servers. There are some PHP functions that specifically relate to the filesystem that are operating system dependent, but these are clearly marked as such in the manual and in this book. Whatever hardware, operating system, and web server you choose, we believe you should seriously consider using PHP and MySQL.

Some of PHP’s Strengths. Some of PHP’s main competitors are Python, Ruby (on Rails or otherwise), Node.js, Perl, Microsoft .NET, and Java. In comparison to these products, PHP has many strengths, including the following: 1) Performance. PHP is very fast. 2) Scalability. You can effectively and cheaply implement horizontal scaling with large numbers of commodity servers. 3) Database Integration. PHP has native connections available to many database systems. 4) Built-in Libraries. Because PHP was designed for use on the Web, it has many built-in functions for performing many useful web-related tasks. You can generate images on the fly, connect to web services and other network services, parse XML, send email, work with cookies, and generate PDF documents, all with just a few lines of code. 5) Cost. PHP is free. 6) Ease of Learning PHP. The syntax of PHP is based on other programming languages, primarily C and Perl. 7) Object-Oriented Support. 8) Portability. PHP is available for many different operating systems. 9) Flexibility of Development Approach. PHP allows you to implement simple tasks simply, and equally easily adapts to implementing large applications using a framework based on design patterns such as Model-View-Controller (MVC). 10) Source Code. 11) Availability of Support and Documentation. 

1『由于是针对 web 开发的语言，它内置的很多函数跟 web 相关，所以做这些任务就很方便，比如生成图片、连接网络服务、解析 XML、发送邮件、cookies 相关、生成 pdf 等；laravel 框架就是基于 MVC 的。』

Key Features of PHP 7. In December 2015, the long-awaited PHP 7 release was made available to the public. As mentioned in this introduction, the book covers both PHP 5.6 and PHP 7, which might lead you to ask「what happened to PHP 6?」The short answer is: there is no PHP 6 and never was for the general public. There was a development effort around a codebase that was referred to as「PHP 6」but it never came to fruition; there were many ambitious plans and subsequent complications that made it difficult for the team to continue to pursue. PHP 7 is not PHP 6 and doesn’t include the features and code from that development effort; PHP 7 is its own release with its own focus — specifically a focus on performance.

Under the hood, PHP 7 includes a refactor of the Zend Engine that powers it, which resulted in a significant performance boost to many web applications — sometimes upwards of 100%! While increased performance and decreased memory use were key to the release of PHP 7, so was backward-compatibility. In fact, relatively few backward-incompatible language changes were introduced. These are discussed contextually throughout this book so that the chapters remain usable with PHP 5.6 or PHP 7, as widespread adoption of PHP 7 has not yet occurred by commercial web-hosting providers.

1『 PHP6 没有实现，直接从 5.6 升级到了 7，7 对网页服务的性能提升很大。』

Some of MySQL’s Strengths. MySQL’s main competitors in the relational database space are PostgreSQL, Microsoft SQL Server, and Oracle. There is also a growing trend in the web application world toward use of NoSQL/non-relational databases such as MongoDB. Let’s take a look at why MySQL is still a good choice in many cases. MySQL has many strengths, including the following: 1) Performance. MySQL is undeniably fast. 2) Low Cost. 3) Ease of Use. 4) Portability. 5) Source Code. 6) Availability of Support. Not all open-source products have a parent company offering support, training, consulting, and certification, but you can get all of these benefits from Oracle.

1『非关系数据库的代表是 MongoDB；之前在书籍「2019025Learning_MySQL_and_MariaDB」里看到 MySQL 好像被谁收购了，怕会被限制商用，所以 Michael 开发了 MariaDB。』

How Is This Book Organized? This book is divided into five main parts:

Part I,「Using PHP」provides an overview of the main parts of the PHP language with examples. Each example is a real-world example used in building an e-commerce site rather than「toy」code. We kick off this section with Chapter 1,「PHP Crash Course.」If you’ve already used PHP, you can whiz through this chapter. If you are new to PHP or new to programming, you might want to spend a little more time on it.

Part II,「Using MySQL」discusses the concepts and design involved in using relational database systems such as MySQL, using SQL, connecting your MySQL database to the world with PHP, and advanced MySQL topics, such as security and optimization.

Part III,「Web Application Security」covers some of the general issues involved in developing a web application using any language. We then discuss how you can use PHP and MySQL to authenticate your users and securely gather, transmit, and store data.

Part IV,「Advanced PHP Techniques」offers detailed coverage of some of the major built-in functions in PHP. We have selected groups of functions that are likely to be useful when building a web application. You will learn about interaction with the server, interaction with the network, image generation, date and time manipulation, and session handling.

Part V,「Building Practical PHP and MySQL Projects」is our favorite section. It deals with practical real-world issues such as managing large projects and debugging, and provides sample projects that demonstrate the power and versatility of PHP and MySQL.

Finally. We hope you enjoy this book and enjoy learning about PHP and MySQL as much as we did when we first began using these products. They are really a pleasure to use. Soon, you’ll be able to join the many thousands of web developers who use these robust, powerful tools to easily build dynamic, real-time web applications.

## 01. PHP Crash Course

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

This chapter gives you a quick overview of PHP syntax and language constructs. In this book, you’ll learn how to use PHP by working through lots of real-world examples taken from our experiences building real websites. Often, programming textbooks teach basic syntax with very simple examples. We have chosen not to do that. We recognize that what you do is get something up and running, and understand how the language is used, instead of plowing through yet another syntax and function reference that’s no better than the online manual.

Try the examples. Type them in or download them from the website, change them, break them, and learn how to fix them again. This chapter begins with the example of an online product order form to show how  variables, operators, and expressions are used in PHP. It also covers variable types and operator  precedence. You will learn how to access form variables and manipulate them by working out the total and tax on a customer order. You will then develop the online order form example by using a PHP script to validate the input data. You’ll examine the concept of Boolean values and look at examples using if, else, the ?: operator, and the switch statement. Finally, you’ll explore looping by writing some PHP to generate repetitive HTML tables.

### 1.2 Creating a Sample Application: Bob’s Auto Parts

One of the most common applications of any server-side scripting language is processing HTML forms. You’ll start learning PHP by implementing an order form for Bob’s Auto Parts, a fictional spare parts company. Creating the Order FormBob’s. HTML programmer has set up an order form for the parts that Bob sells. This relatively simple order form, shown in Figure 1.1, is similar to many you have probably seen while surfing. Bob would like to be able to know what his customers ordered, work out the total prices of their orders, and determine how much sales tax is payable on the orders.

Notice that the form’s action is set to the name of the PHP script that will process the customer’s order. (You’ll write this script next.) In general, the value of the action attribute is the URL that will be loaded when the user clicks the Submit button. The data the user has typed in the form will be sent to this URL via the HTTP method specified in the method attribute, either get (appended to the end of the URL) or post (sent as a separate message).

    <form action="processorder.php" method="post">

Also note the names of the form fields: tireqty, oilqty, and sparkqty. You’ll use these names again in the PHP script. Because the names will be reused, it’s important to give your form fields meaningful names that you can easily remember when you begin writing the PHP script. Some HTML editors generate field names like field23 by default. They are difficult to remember. Your life as a PHP programmer will be easier if the names you use reflect the data typed into the field.

You should consider adopting a coding standard for field names so that all field names throughout your site use the same format. This way, you can more easily remember whether, for example, you abbreviated a word in a field name or put in underscores as spaces.

1『 form 即表单；又见这两种请求，get 和 post，get (appended to the end of the URL) or post (sent as a separate message)。』

3『

[\<tr> - HTML（超文本标记语言） | MDN](https://wiki.developer.mozilla.org/zh-CN/docs/Web/HTML/Element/tr)

源码里的 \<tr> 和 \<td> 元素，都是表格元素里的。\<tr> 元素定义表格中的行。 Those can be a mix of \<td> and \<th> elements. \<td> 元素定义了一个包含数据的表格单元格。

』

To process the form, you need to create the script mentioned in the action attribute of the form tag called processorder.php. Open your text editor and create this file. Then type in the following code:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Bob's Auto Parts - Order Results</title>
  </head>
  <body>
    <h1>Bob's Auto Parts</h1>
    <h2>Order Results</h2> 
  </body>
</html>
```

### 1.3 Embedding PHP in HTML

Under the \<h2> heading in your file, add the following lines:

    <?php  echo '<p>Order processed.</p>';?>

Save the file and load it in your browser by filling out Bob’s form and clicking the Submit Order button. You should see something similar to the output shown in Figure 1.2. Notice how the PHP code you wrote was embedded inside a normal-looking HTML file. Try viewing the source from your browser. You should see this code \<!DOCTYPE html>

None of the raw PHP is visible because the PHP interpreter has run through the script and replaced it with the output from the script. This means that from PHP you can produce clean HTML viewable with any browser; in other words, the user’s browser does not need to understand PHP. This example illustrates the concept of server-side scripting in a nutshell. The PHP has been interpreted and executed on the web server, as distinct from JavaScript and other client-side technologies interpreted and executed within a web browser on a user’s machine.

3『例子解释了服务端脚本的概念，浏览器不需要理解 PHP 这种服务端脚本，那么联想到，浏览器需要理解 JavaScript 这种客户端脚本。』

The code that you now have in this file consists of four types of text: 1) HTML. 2) PHP tags. 3) PHP statements. 4) Whitespace. You can also add comments. Most of the lines in the example are just plain HTML.

PHP Tags. The PHP code in the preceding example began with \<?php and ended with ?>. This is similar to all HTML tags because they all begin with a less than (\<) symbol and end with a greater than (>) symbol. These symbols (\<?php and ?>) are called PHP tags. They tell the web server where the PHP code starts and finishes. Any text between the tags is interpreted as PHP. Any text outside these tags is treated as normal HTML. The PHP tags allow you to escape from HTML.

There are actually two styles of PHP tags; each of the following fragments of code is equivalent:

 ■ XML style

    <?php echo '<p>Order processed.</p>'; ?>

This is the tag style that we use in this book; it is the preferred PHP tag style. The server administrator cannot turn it off, so you can guarantee it will be available on all servers, which is especially important if you are writing applications that may be used on different installations. This tag style can be used with Extensible Markup Language (XML) documents. In general, we recommend you use this tag style.

 ■ Short style

    <? echo '<p>Order processed.</p>'; ?>

This tag style is the simplest and follows the style of a Standard Generalized Markup Language (SGML) processing instruction. To use this type of tag — which is the shortest to type — you either need to enable the short_open_tag setting in your conﬁgﬁle or  compile PHP with short tags enabled. You can ﬁnd more information on how to use this tag style in Appendix A. The use of this style is not recommended for use in code you plan to distribute. It will not work in many environments as it is no longer enabled by default.

PHP Statements. You tell the PHP interpreter what to do by including PHP statements between your opening and closing tags. The preceding example used only one type of statement:

    echo '<p>Order processed.</p>';

As you have probably guessed, using the echo construct has a very simple result: It prints (or echoes) the string passed to it to the browser. In Figure 1.2, you can see the result is that the text Order processed. appears in the browser window. Notice that there is a semicolon at the end of the echo statement. Semicolons separate statements in PHP much like periods separate sentences in English. If you have programmed in C or Java before, you will be familiar with using the semicolon in this way. Leaving off the semicolon is a common syntax error that is easily made. However, it’s equally easy to find and to correct.

Whitespace. Spacing characters such as newlines (carriage returns), spaces, and tabs are known as whitespace. As you probably already know, browsers ignore whitespace in HTML, and so does the PHP engine. Consider these two HTML fragments:

These two snippets of HTML code produce identical output because they appear the same to the browser. However, you can and are encouraged to use whitespace sensibly in your HTML as an aid to humans — to enhance the readability of your HTML code. The same is true for PHP. You don’t need to have any whitespace between PHP statements, but it makes the code much easier to read if you put each statement on a separate line. For example,

    echo 'hello ';
    echo 'world';

and

    echo 'hello ';echo 'world';

are equivalent, but the first version is easier to read.

1『 HTML 和 PHP 都忽略 whitespace，whitespace 的概念：Spacing characters such as newlines (carriage returns), spaces, and tabs.』

Comments are exactly that: Comments in code act as notes to people reading the code. PHP supports C, C++, and shell script–style comments. The following is a C-style, multiline comment that might appear at the start of a PHP script:

```php
/* Author: Bob Smith   
Last modified: April 10   
This script processes the customer orders.
*/
```

Multiline comments should begin with a /* and end with */. As in C, multiline comments cannot be nested. You can also use single-line comments, either in the C++ style:

```php
echo '<p>Order processed.</p>'; // Start printing order
```

or in the shell script style:

```php
echo '<p>Order processed.</p>'; # Start printing order
```

With both of these styles, everything after the comment symbol (# or //) is a comment until you reach the end of the line or the ending PHP tag, whichever comes first. In the following line of code, the text before the closing tag, here is a comment, is part of a comment. The text after the closing tag, here is not, will be treated as HTML because it is outside the closing tag:

    // here is a comment ?> here is not

### 1.4 Adding Dynamic Content

So far, you haven’t used PHP to do anything you couldn’t have done with plain HTML. The main reason for using a server-side scripting language is to be able to provide dynamic content to a site’s users. This is an important application because content that changes according to users’ needs or over time will keep visitors coming back to a site. PHP allows you to do this easily. Let’s start with a simple example. Replace the PHP in processorder.php with the following code: 

You could also write this on one line, using the concatenation operator (.), as

```php
<?php  
echo "<p>Order processed at ".date('H:i, jS F Y')."</p>";?>
```

In this code, PHP’s built-in date() function tells the customer the date and time when his order was processed. This information will be different each time the script is run. The output of running the script on one occasion is shown in Figure 1.3.

Calling Functions. Look at the call to date(). This is the general form that function calls take. PHP has an  extensive library of functions you can use when developing web applications. Most of these functions need to have some data passed to them and return some data. Now look at the function call again:

    date('H:i, jS F')

Notice that it passes a string (text data) to the function inside a pair of parentheses. The element within the parentheses is called the function’s argument or parameter. Such  arguments are the input the function uses to output some specific results.

Using the date() Function. The date() function expects the argument you pass it to be a format string, representing the style of output you would like. Each letter in the string represents one part of the date and time. H is the hour in a 24-hour format with leading zeros where required, i is the minutes with a leading zero where required, j is the day of the month without a leading zero, S  represents the ordinal suffix (in this case th), and F is the full name of the month. Note: If date() gives you a warning about not having set the timezone, you should add the date.timezone setting to your php.ini file. More information on this can be found in the sample php.ini file in Appendix A. For a full list of formats supported by date(), see Chapter 19,「Managing the Date and Time.」

1『注意：第几天的 J 是小写的 j，之前敲的时候敲成大写的了；在 php.ini 可以改时区，默认的时区是不对的。』

Form Variables. Within your PHP script, you can access each form field as a PHP variable whose name relates to the name of the form field. You can recognize variable names in PHP because they all start with a dollar sign (\$). (Forgetting the dollar sign is a common programming error.)

Depending on your PHP version and setup, you can access the form data via variables in different ways.  In recent versions of PHP, all but one of these ways have been deprecated, so beware if you have used PHP in the past that this has changed. You may access the contents of the field tireqty in the following way:

    $_POST['tireqty']    

\$_POST is an array containing data submitted via an HTTP POST request — that is, the form method was set to POST. There are three of these arrays that may contain form data: 

\$\_POST, \$\_GET, and \$\_REQUEST. One of the \$\_GET or \_POST arrays holds the details of all the form variables. Which array is used depends on whether the method used to submit the form was GET or POST, respectively. In addition, a combination of all data submitted via GET or POST is also available through \$_REQUEST.

If the form was submitted via the POST method, the data entered in the tireqty box will be stored in \$\_POST['tireqty']. If the form was submitted via GET, the data will be in \$_GET['tireqty']. In either case, the data will also be available in \$\_REQUEST['tireqty']. These arrays are some of the superglobal arrays. We will revisit the superglobals when we discuss variable scope later in this chapter.

1『 \$\_POST、 \$\_GET 和 \$\_REQUEST 三个都是 superglobal（超级全局变量）。』

Let’s look at an example that creates easier-to-use copies of variables. To copy the value of one variable into another, you use the assignment operator, which in PHP is an equal sign (=). The following statement creates a new variable named \$tireqty and copies the contents of \$_POST['tireqty'] into the new variable:

    $tireqty = $_POST['tireqty'];

Place the following block of code at the start of the processing script. All other scripts in this book that handle data from a form contain a similar block at the start. Because this code will not produce any output, placing it above or below the \<html> and other HTML tags that start your page makes no difference. We generally place such blocks at the start of the script to make them easy to find.

```php
<?php  // create short variable names  
$tireqty = $_POST['tireqty'];  
$oilqty = $_POST['oilqty'];  
$sparkqty = $_POST['sparkqty'];
?>
```

1『所有从前端获取的数据，放到代码最前面的「容器」里，养成这个习惯。』

This code creates three new variables — \$tireqty, \$oilqty, and \$sparkqty — and sets them to contain the data sent via the POST method from the form. You can output the values of these variables to the browser by doing, for example:

    echo $tireqty.' tires<br />';

However, this approach is not recommended. At this stage, you have not checked the variable contents to make sure sensible data has been entered in each form field. Try entering deliberately wrong data and observe what happens. After you have read the rest of the chapter, you might want to try adding some data validation to this script.

Taking data directly from the user and outputting it to the browser like this is an extremely risky practice from a security perspective. We do not recommend this approach. You should filter input data. We will start to cover input filtering in Chapter 4,「String Manipulation and Regular Expressions,」and discuss security in depth in Chapter 14,「Web Application Security Risks.」

1『直接提取数据很不安全，超级不建议，提取前需要做验证。』

For now, it’s enough to know that you should echo out user data to the browser after passing it through a function called htmlspecialchars(). For example, in this case, we would do the following:

To make the script start doing something visible, add the following lines to the bottom of your PHP script:   

```php
<?php
echo '<p>Order processed at '.date('H:i, JS F Y').'</p>';;
echo '<p>your order is as follows: </p>';
echo htmlspecialchars($tireqty).' tires<br />';
echo htmlspecialchars($oilqty).' bottles of oil<br />';
echo htmlspecialchars($sparkqty).' spark plugs<br />';
?>   
```

1『 htmlspecialchars() 应该是 php 的一个库函数。』

If you now load this file in your browser, the script output should resemble what is shown in Figure 1.4. The actual values shown, of course, depend on what you typed into the form. The following sections describe a couple of interesting elements of this example.

String Concatenation. In the sample script, echo prints the value the user typed in each form field, followed by some explanatory text. If you look closely at the echo statements, you can see that the variable name and following text have a period (.) between them, such as this:

    echo htmlspecialchars($tireqty).' tires<br />';

This period is the string concatenation operator, which adds strings (pieces of text) together. You will often use it when sending output to the browser with echo. This way, you can avoid writing multiple echo commands. You can also place simple variables inside a double-quoted string to be echoed. (Arrays are somewhat more complicated, so we look at combining arrays and strings in Chapter 4.) Consider this example: 

```
$tireqty = htmlspecialchars($tireqty);  
echo "$tireqty tires<br />";
```

This is equivalent to the first statement shown in this section. Either format is valid, and which one you use is a matter of personal taste. This process, replacing a variable with its contents within a string, is known as interpolation. Note that interpolation is a feature of double-quoted strings only. You cannot place variable names inside a single-quoted string in this way. Running the following line of code:

    echo '$tireqty tires<br />';

1『嵌入变量可以生效的前提是用双引号包裹，以后还是都养成用双引号的习惯，对 json 数据也有好处，因为 json 格式里的属性值不支持单引号的。』

simply sends \$tireqty tires\<br /> to the browser. Within double quotation marks, the variable name is replaced with its value. Within single quotation marks, the variable name or any other text is sent unaltered.

Variables and Literals. The variables and strings concatenated together in each of the echo statements in the sample script are different types of things. Variables are symbols for data. The strings are data themselves. When we use a piece of raw data in a program like this, we call it a literal to distinguish it from a variable. \$tireqty is a variable, a symbol that represents the data the customer typed in. On the other hand, ' tires\<br />' is a literal. You can take it at face value. Well, almost. Remember the second example in the preceding section? PHP replaced the variable name \$tireqty in the string with the value stored in the variable.

Remember the two kinds of strings mentioned already: ones with double quotation marks and ones with single quotation marks. PHP tries to evaluate strings in double quotation marks, resulting in the behavior shown earlier. Single-quoted strings are treated as true literals.

1『如要想在字符串里直接输出变量的值，必须用双引号，解释器识别不了单引号里的变量。PHP 里双引号字符串和单引号字符串语义不一样。双引号字符串是 interpolated 的，即自动识别里面变量的值，下面讲的 Heredoc strings 也是。』

There is also a third way of specifying strings using the heredoc syntax (<<<), which will be familiar to Perl users. Heredoc syntax allows you to specify long strings tidily, by specifying an end marker that will be used to terminate the string. The following example creates a three-line string and echoes it:

```php
echo <<<theEnd  
line 1  
line 2 
line 3
theEnd
```

The token theEnd is entirely arbitrary. It just needs to be guaranteed not to appear in the text. To close a heredoc string, place a closing token at the start of a line. Heredoc strings are interpolated, like double-quoted strings.

1『 heredoc syntax 应用于有很多行的内容，可类比于双引号，前后的起始、终结标识符可以任意定，但必须保持一致，例子里给的 endEnd 可以作为以后默认使用的标识符。』

Understanding Identifiers. Identifiers are the names of variables. (The names of functions and classes are also identifiers; we look at functions and classes in Chapter 5「Reusing Code and Writing Functions,」and Chapter 6「Object-Oriented PHP.」) You need to be aware of the simple rules defining valid identifiers: 1) Identifiers can be of any length and can consist of letters, numbers, and underscores. 2) Identifiers cannot begin with a digit. 3) In PHP, identifiers are case sensitive. \$tireqty is not the same as \$TireQty. Trying to use them interchangeably is a common programming error. Function names are an exception to this rule: Their names can be used in any case. 4) A variable can have the same name as a function. This usage is confusing, however, and should be avoided. Also, you cannot create a function with the same name as another function.

1『识别码大小写敏感，但是函数名是个例外。』

You can declare and use your own variables in addition to the variables you are passed from the HTML form. One of the features of PHP is that it does not require you to declare variables before using them. A variable is created when you first assign a value to it. See the next section for details. You assign values to variables using the assignment operator (=) as you did when copying one variable’s value to another. On Bob’s site, you want to work out the total number of items ordered and the total amount payable. You can create two variables to store these numbers. To begin with, you need to initialize each of these variables to zero by adding these lines to the bottom of your PHP script. Each of these two lines creates a variable and assigns a literal value to it. You can also assign variable values to variables, as shown in this example:

```php
$totalqty = 0;
$totalamount = 0.00;

$totalqty = 0;
$totalamount = $totalqty;
```

### 1.6 Examining Variable Types

A variable’s type refers to the kind of data stored in it. PHP provides a set of data types. Different data can be stored in different data types. 

PHP’s Data Types. PHP supports the following basic data types: 1) Integer — Used for whole numbers. 2) Float (also called double)—Used for real numbers. 3) String — Used for strings of characters. 4) Boolean — Used for true or false values. 5) Array — Used to store multiple data items (see Chapter 3「Using Arrays」). 6) Object — Used for storing instances of classes (see Chapter 6).

Three special types are also available: NULL, resource, and callable. Variables that have not been given a value, have been unset, or have been given the specific value NULL are of type NULL.

Certain built-in functions (such as database functions) return variables that have the type resource. They represent external resources (such as database connections). You will almost certainly not directly manipulate a resource variable, but frequently they are returned by functions and must be passed as parameters to other functions.

3『原来在 laravel-admin 里看到的 resources 是一种特殊的数据类型，它可以用来表示外部资源，比如数据库连接，注意通常不会直接操作 resource variable，而是作为参数在各个函数间调用。』

Callables are essentially functions that are passed to other functions.

2『回调函数，去深挖一下。』

Type Strength. PHP is called a weakly typed or dynamically typed language. In most programming languages, variables can hold only one type of data, and that type must be declared before the variable can be used, as in C. In PHP, the type of a variable is determined by the value assigned to it. For example, when you created \$totalqty and \$totalamount, their initial types were  determined as follows:

1『 php 跟 JS、python 一样，动态语言，不要要提前声明变量的数据类型，用的时候直接赋值，它会根据被赋的值自己确定该变量所绑定的数据类型。』

Because you assigned 0, an integer, to \$totalqty, this is now an integer type variable. Similarly, \$totalamount is now of type float. Strangely enough, you could now add a line to your script as follows. The variable \$totalamount would then be of type string. PHP changes the variable type according to what is stored in it at any given time. This ability to change types transparently on the fly can be extremely useful. Remember PHP「automagically」knows what data type you put into your variable. It returns the data with the same data type when you retrieve it from the variable.

Type Casting. You can pretend that a variable or value is of a different type by using a type cast. This feature works identically to the way it works in C. You simply put the temporary type in parentheses in front of the variable you want to cast. For example, you could have declared the two variables from the preceding section using a cast:

```php
$totalqty = 0;
$totalamount = (float)$totalqty;
```

The second line means「Take the value stored in \$totalqty, interpret it as a float, and store it in \$totalamount.」The \$totalamount variable will be of type float. The cast variable does not change types, so \$totalqty remains of type integer.

1『 Type Casting 不会改变原来变量的数据类型。』

Variable Variables. PHP provides one other type of variable: the variable variable. Variable variables enable you to change the name of a variable dynamically. As you can see, PHP allows a lot of freedom in this area. All languages enable you to change the value of a variable, but not many allow you to change the variable’s type, and even fewer allow you to change the variable’s name.  A variable variable works by using the value of one variable as the name of another. For example, you could set:

    $varname = 'tireqty';

You can then use \$\$varname in place of \$tireqty. For example, you can set the value of \$tireqty as follows:

    $$varname = 5;

This is equivalent to

    $tireqty = 5;

This approach might seem somewhat obscure, but we’ll revisit its use later. Instead of having to list and use each form variable separately, you can use a loop and variable variable to process them all automatically. You can find an example illustrating this in the section on for loops later in this chapter.

1『应用场景在哪？目前知道了一个应用点，与 for 循环结合起来用，详见信息卡片。』

### 1.7 Declaring and Using Constants

As you saw previously, you can readily change the value stored in a variable. You can also declare constants. A constant stores a value just like a variable, but its value is set once and then cannot be changed elsewhere in the script. In the sample application, you might store the prices for each item on sale as a constant. You can define these constants using the define function:

```php
define('TIREPRICE', 100);
define('OILPRICE', 10);
define('SPARKPRICE', 4);
```

Notice that the names of the constants appear in uppercase. This convention, borrowed from C, makes it easy to distinguish between variables and constants at a glance. Following this convention is not required but will make your code easier to read and maintain.

One important difference between constants and variables is that when you refer to a constant, it does not have a dollar sign in front of it. If you want to use the value of a constant, use its name only. For example, to use one of the constants just created, you could type:

    echo TIREPRICE;

As well as the constants you define, PHP sets a large number of its own. An easy way to obtain an overview of them is to run the phpinfo() function:

    phpinfo();

This function provides a list of PHP’s predefined variables and constants, among other useful information. We will discuss some of them as we go along. One other difference between variables and constants is that constants can store only boolean, integer, float, or string data. These types are collectively known as scalar values.

### 1.8 Understanding Variable Scope

The term scope refers to the places within a script where a particular variable is visible. The six basic scope rules in PHP are as follows: 1) Built-in superglobal variables are visible everywhere within a script. 2) Constants, once declared, are always visible globally; that is, they can be used inside and outside functions. 3) Global variables declared in a script are visible throughout that script, but not inside functions. 4) Variables inside functions that are declared as global refer to the global variables of the same name. 5) Variables created inside functions and declared as static are invisible from outside the function but keep their value between one execution of the function and the next. (We explain this idea fully in Chapter 5.) 6) Variables created inside functions are local to the function and cease to exist when the function terminates.

The arrays \$\_GET and \$\_POST and some other special variables have their own scope rules. They are known as superglobals and can be seen everywhere, both inside and outside functions.

The complete list of superglobals is as follows: 1) \$GLOBALS—An array of all global variables (Like the global keyword, this allows you to access global variables inside a function—for example, as \$GLOBALS['myvariable'].) 2) \$\_SERVER—An array of server environment variables. 3) \$\_GET—An array of variables passed to the script via the GET method. 4) \$\_POST—An array of variables passed to the script via the POST method. 5) \$\_COOKIE—An array of cookie variables. 6) \$\_FILES—An array of variables related to file uploads. 7)  \$\_ENV—An array of environment variables. 8) \$\_REQUEST—An array of all user input including the contents of input including \$\_GET, \$\_POST, and \$\_COOKIE (but not including \$\_FILES). 9) \$\_SESSION—An array of session variables.

We come back to each of these superglobals throughout the book as they become relevant. We cover scope in more detail when we discuss functions and classes later in this chapter. For the time being, all the variables we use are global by default.

### 1.9 Using Operators

Operators are symbols that you can use to manipulate values and variables by performing an operation on them. You need to use some of these operators to work out the totals and tax on the customer’s order. We’ve already mentioned two operators: the assignment operator (=) and the string  concatenation operator (.). In the following sections, we describe the complete list.

In general, operators can take one, two, or three arguments, with the majority taking two. For example, the assignment operator takes two: the storage location on the left side of the = symbol and an expression on the right side. These arguments are called operands—that is, the things that are being operated upon.

#### 1.9.1 Arithmetic Operators

Arithmetic operators are straightforward; they are just the normal mathematical operators. PHP’s arithmetic operators are shown in Table 1.1.

You should note that arithmetic operators are usually applied to integers or doubles. If you apply them to strings, PHP will try to convert the string to a number. If it contains an e or an E, it will be read as being in scientific notation and converted to a float; otherwise, it will be converted to an integer. PHP will look for digits at the start of the string and use them as the value; if there are none, the value of the string will be zero.

#### 1.9.2 String Operators 

You’ve already seen and used the only string operator. You can use the string concatenation operator to add two strings and to generate and store a result much as you would use the addition operator to add two numbers:

#### 1.9.3 Assignment Operators

You’ve already seen the basic assignment operator (=). Always refer to this as the assignment operator and read it as「is set to.」For example,

Values Returned from Assignment. This technique enables you to form expressions such as:

    $b = 6 + ($a = 5);

This line sets the value of the \$b variable to 11. This behavior is generally true of assignments: The value of the whole assignment statement is the value that is assigned to the left operand. When working out the value of an expression, you can use parentheses to increase the  precedence of a subexpression, as shown here. This technique works exactly the same way as in mathematics.

Combined Assignment Operators. In addition to the simple assignment, there is a set of combined assignment operators. Each of them is a shorthand way of performing another operation on a variable and assigning the result back to that variable. For example,

    $a += 5;

This is equivalent to writing

    $a = $a + 5;

Combined assignment operators exist for each of the arithmetic operators and for the string concatenation operator. A summary of all the combined assignment operators and their effects is shown in Table 1.2.

Pre- and Post-Increment and Decrement. The pre- and post-increment (++) and decrement (--) operators are similar to the += and -= operators, but with a couple of twists. All the increment operators have two effects: They increment and assign a value. Consider the following:

```php
$a=4;
echo ++$a;
```

The second line uses the pre-increment operator, so called because the ++ appears before the \$a. This has the effect of first incrementing \$a by 1 and second, returning the incremented value. In this case, \$a is incremented to 5, and then the value 5 is returned and printed. The value of this whole expression is 5. (Notice that the actual value stored in \$a is changed: It is not just returning \$a + 1.) If the ++ is after the \$a, however, you are using the post-increment operator. It has a different effect. Consider the following:

```php
$a=4;
echo $a++;
```

In this case, the effects are reversed. That is, first, the value of \$a is returned and printed, and second, it is incremented. The value of this whole expression is 4. This is the value that will be printed. However, the value of \$a after this statement is executed is 5. As you can probably guess, the behavior is similar for the -- (decrement) operator. However, the value of \$a is decremented instead of being incremented.

Reference Operator. The reference operator (&, an ampersand) can be used in conjunction with assignment. Normally, when one variable is assigned to another, a copy is made of the first variable and stored elsewhere in memory. For example,

```php
$a = 5;
$b = $a;
```

These code lines make a second copy of the value in \$a and store it in \$b. If you subsequently change the value of \$a, \$b will not change:

```php
$a = 7; // $b will still be 5
```

You can avoid making a copy by using the reference operator. For example,

```
$a = 5;
$b = &$a;
$a = 7; // $a and $b are now both 7
```

References can be a bit tricky. Remember that a reference is like an alias rather than like a pointer. Both \$a and \$b point to the same piece of memory. You can change this by unsetting one of them as follows:

    unset($a);

Unsetting does not change the value of \$b (7) but does break the link between \$a and the value 7 stored in memory.

#### 1.9.4 Comparison Operators

The comparison operators compare two values. Expressions using these operators return either of the logical values true or false depending on the result of the comparison.

The Equal Operator. The equal comparison operator (==, two equal signs) enables you to test whether two values are equal. For example, you might use the expression to test whether the values stored in \$a and \$b are the same. The result returned by this  expression is true if they are equal or false if they are not. You might easily confuse == with =, the assignment operator. Using the wrong operator will work without giving an error but generally will not give you the result you wanted. In general, nonzero values evaluate to true and zero values to false. Say that you have initialized two variables as follows:

```php
$a = 5;$b = 7;
```

If you then test \$a = \$b, the result will be true. Why? The value of \$a = \$b is the value assigned to the left side, which in this case is 7. Because 7 is a nonzero value, the expression evaluates to true. If you intended to test \$a = = \$b, which evaluates to false, you have  introduced a logic error in your code that can be extremely difficult to find. Always check your use of these two operators and check that you have used the one you intended to use. Using the assignment operator rather than the equals comparison operator is an easy mistake to make, and you will probably make it many times in your programming career.

Other Comparison Operators. PHP also supports a number of other comparison operators. A summary of all the comparison operators is shown in Table 1.3. One to note is the identical operator (===), which returns true only if the two operands are both equal and of the same type. 

For example, 0\=='0' will be true, but 0==='0' will not because one zero is an integer and the other zero is a string.

#### 1.9.5 Logical Operators

The logical operators combine the results of logical conditions. For example, you might be interested in a case in which the value of a variable, \$a, is between 0 and 100. You would need to test both the conditions \$a >= 0 and \$a <= 100, using the AND operator, as follows:

    $a >= 0 && $a <=100

PHP supports logical AND, OR, XOR (exclusive or), and NOT. The set of logical operators and their use is summarized in Table 1.4. The and and or operators have lower precedence than the && and || operators. We cover precedence in more detail later in this chapter.

#### 1.9.6 Bitwise Operators

The bitwise operators enable you to treat an integer as the series of bits used to represent it. You probably will not find a lot of use for the bitwise operators in PHP, but a summary is shown in Table 1.5.

#### 1.9.7 Other Operators

In addition to the operators we have covered so far, you can use several others. The comma operator (,) separates function arguments and other lists of items. It is normally used incidentally. Two special operators, new and ->, are used to instantiate a class and access class members, respectively. They are covered in detail in Chapter 6. There are a few others that we discuss briefly here.

The Ternary Operator. The ternary operator (?:) takes the following form:

    condition ? value if true : value if false

The Execution Operator. The execution operator is really a pair of operators—a pair of backticks (``) in fact. The  backtick is not a single quotation mark; it is usually located on the same key as the ~ (tilde) symbol on your keyboard. PHP attempts to execute whatever is contained between the backticks as a command at the server’s command line. The value of the expression is the output of the command. For example, under Unix-like operating systems, you can use

```php
$out = `ls -la`;
echo '<pre>'.$out.'</pre>';
```

Or, equivalently on a Windows server, you can use

```php
$out = `dir c:`;
echo '<pre>'.$out.'</pre>';
```

Either version obtains a directory listing and stores it in \$out. It can then be echoed to the browser or dealt with in any other way. There are other ways of executing commands on the server. We cover them in Chapter 17「Interacting with the File System and the Server.」

Array Operators. There are a number of array operators. The array element operators ([]) enable you to access array elements. You can also use the => operator in some array contexts. These operators are covered in Chapter 3. You also have access to a number of other array operators. We cover them in detail in Chapter 3 as well, but we included them here in Table 1.6 for completeness.

You will notice that the array operators in Table 1.6 all have equivalent operators that work on scalar variables. As long as you remember that + performs addition on scalar types and union on arrays—even if you have no interest in the set arithmetic behind that behavior—the  behaviors should make sense. You cannot usefully compare arrays to scalar types.

The Type Operator. There is one type operator: instanceof. This operator is used in object-oriented programming, but we mention it here for completeness. (Object-oriented programming is covered in Chapter 6.) The instanceof operator allows you to check whether an object is an instance of a particular class, as in this example:

```php
class sampleClass{};
$myObject = new sampleClass();
if ($myObject instanceof sampleClass)  
    echo  "myObject is an instance of sampleClass";
```

### 1.10 Working Out the Form Totals

Now that you know how to use PHP’s operators, you are ready to work out the totals and tax on Bob’s order form. To do this, add the following code to the bottom of your PHP script:

```php
$totalqty = 0;
$totalqty = $tireqty + $oilqty + $sparkqty;
echo "<p>Items ordered: ".$totalqty."<br />";
$totalamount = 0.00;

define('TIREPRICE', 100);
define('OILPRICE', 10);
define('SPARKPRICE', 4);

$totalamount = $tireqty * TIREPRICE
                      + $oilqty * OILPRICE
                      + $sparkqty * SPARKPRICE;

echo "Subtotal: $".number_format($totalamount,2)."<br />";

$taxrate = 0.10;  // local sales tax is 10%
$totalamount = $totalamount * (1 + $taxrate);
echo "Total including tax: $".number_format($totalamount,2)."</p>";
```

As you can see, this piece of code uses several operators. It uses the addition (+) and  multiplication (*) operators to work out the amounts and the string concatenation operator (.) to set up the output to the browser.

It also uses the number\_format() function to format the totals as strings with two decimal places. This is a function from PHP’s Math library. If you look closely at the calculations, you might ask why the calculations were performed in the order they were. For example, consider this statement:

The total amount seems to be correct, but why were the multiplications performed before the additions? The answer lies in the precedence of the operators—that is, the order in which they are evaluated.

### 1.11 Understanding Precedence and Associativity

In general, operators have a set precedence, or order, in which they are evaluated. Operators also have associativity, which is the order in which operators of the same precedence are evaluated. This order is generally left to right (called left for short), right to left (called right for short), or not relevant. Table 1.7 shows operator precedence and associativity in PHP. In this table, operators with the lowest precedence are at the top, and precedence increases as you go down the table.

Table 1.7  Operator Precedence in PHP

Notice that we haven’t yet covered the operator with the highest precedence: plain old parentheses. The effect of using parentheses is to raise the precedence of whatever is contained within them. This is how you can deliberately manipulate or work around the precedence rules when you need to. Remember this part of the preceding example:

    $totalamount = $totalamount * (1 + $taxrate);

If you had written

    $totalamount = $totalamount * 1 + $taxrate;

the multiplication operation, having higher precedence than the addition operation, would be performed first, giving an incorrect result. By using the parentheses, you can force the subexpression 1 + \$taxrate to be evaluated first. You can use as many sets of parentheses as you like in an expression. The innermost set of parentheses is evaluated first. Also note one other operator in this table we have not yet covered: the print language construct, which is equivalent to echo. Both constructs generate output.

We generally use echo in this book, but you can use print if you find it more readable. Neither print nor echo is really a function, but both can be called as a function with parameters in parentheses. Both can also be treated as an operator: You simply place the string to work with after the keyword echo or print. Calling print as a function causes it to return a value (1). This capability might be useful if you want to generate output inside a more complex expression but does mean that print is marginally slower than echo.

### 1.12 Using Variable Handling Functions

Before we leave the world of variables and operators, let’s look at PHP’s variable handling functions. PHP provides a library of functions that enable you to manipulate and test variables in different ways.

#### 1.12.1 Testing and Setting Variable Types

Most of the variable functions are related to testing the type of function. The two most general are gettype() and settype(). They have the following function prototypes; that is, this is what arguments expect and what they return:

```php
string gettype(mixed var);
bool settype(mixed var, string type);
```

To use gettype(), you pass it a variable. It determines the type and returns a string containing the type name: bool, int, double (for floats, confusingly, for historical reasons), string, array, object, resource, or NULL. It returns unknown type if it is not one of the standard types.

To use settype(), you pass it a variable for which you want to change the type and a string containing the new type for that variable from the previous list.

Note: This book and the php.net documentation refer to the data type「mixed.」There is no such data type, but because PHP is so flexible with type handling, many functions can take many (or any) data types as an argument. Arguments for which many types are permitted are shown with the pseudo-type「mixed.」

You can use these functions as follows:

```php
$a = 56;
echo gettype($a) . '<br />';
settype($a, 'float');
echo gettype($a) . '<br />';
```

When gettype() is called the first time, the type of \$a is integer. After the call to settype(), the type is changed to float, which is reported as double. (Be aware of this difference.) PHP also provides some specific type-testing functions. Each takes a variable as an argument and returns either true or false. The functions are:

#### 1.12.2 Testing Variable Status

PHP has several functions for testing the status of a variable. The first is isset(), which has the following prototype:

    bool isset(mixed var[, mixed var[,...]])

This function takes a variable name as an argument and returns true if it exists and false otherwise. You can also pass in a comma-separated list of variables, and isset() will return true if all the variables are set. You can wipe a variable out of existence by using its companion function, unset(), which has the following prototype:

    void unset(mixed var[, mixed var[,...]])

This function gets rid of the variable it is passed. The empty() function checks to see whether a variable exists and has a nonempty, nonzero value; it returns true or false accordingly. It has the following prototype:

    bool empty(mixed var)

Let’s look at an example using these three functions. Try adding the following code to your script temporarily:

```php
echo 'isset($tireqty): ' . isset($tireqty).'<br />'; 
echo 'isset($nothere): ' . isset($nothere).'<br />';
echo 'empty($tireqty): ' . empty($tireqty).'<br />';
echo 'empty($nothere): ' . empty($nothere).'<br />';
```

The variable \$tireqty should return 1 (true) from isset() regardless of what value you entered in that form field and regardless of whether you entered a value at all. Whether it is empty() depends on what you entered in it. The variable \$nothere does not exist, so it generates a blank (false) result from isset() and a 1 (true) result from empty(). These functions are handy when you need to make sure that the user filled out the appropriate fields in the form.

#### 1.12.3 Reinterpreting Variables

You can achieve the equivalent of casting a variable by calling a function. The following three functions can be useful for this task:

```php
int intval(mixed var[, int base=10])
float floatval(mixed var)
string strval(mixed var)
```

Each accepts a variable as input and returns the variable’s value converted to the  appropriate type. The intval() function also allows you to specify the base for conversion when the  variable to be converted is a string. (This way, you can convert, for example, hexadecimal strings to integers.)

### 1.13 Making Decisions with Conditionals

Control structures are the structures within a language that allow you to control the flow of execution through a program or script. You can group them into conditional (or branching) structures and repetition structures (or loops). If you want to sensibly respond to your users’ input, your code needs to be able to make  decisions. The constructs that tell your program to make decisions are called conditionals.

#### 1.13.1 if Statements

You can use an if statement to make a decision. You should give the if statement a condition to use. If the condition is true, the following block of code will be executed. Conditions in if statements must be surrounded by parentheses ().

For example, if a visitor orders no tires, no bottles of oil, and no spark plugs from Bob, it is probably because she accidentally clicked the Submit Order button before she had finished filling out the form. Rather than telling the visitor「Order processed,」the page could give her a more useful message. When the visitor orders no items, you might like to say,「You did not order anything on the previous page!」You can do this easily by using the following if statement:

#### 1.13.2 Code Blocks

Often you may have more than one statement you want executed according to the actions of a conditional statement such as if. You can group a number of statements together as a block. To declare a block, you enclose it in curly braces:

```php
if ($totalqty == 0) {  
    echo '<p style="color:red">';  
    echo 'You did not order anything on the previous page!';  
    echo '</p>';}
```

The three lines enclosed in curly braces are now a block of code. When the condition is true, all three lines are executed. When the condition is false, all three lines are ignored.

Note: As already mentioned, PHP does not care how you lay out your code. However, you should indent your code for readability purposes. Indenting is used to enable you to see at a glance which lines will be executed only if conditions are met, which statements are grouped into blocks, and which statements are parts of loops or functions. In the previous examples, you can see that the statement depending on the if statement and the statements making up the block are indented.

#### 1.13.3 else Statements

You may often need to decide not only whether you want an action performed, but also which of a set of possible actions you want performed. An else statement allows you to define an alternative action to be taken when the condition in an if statement is false. Say you want to warn Bob’s customers when they do not order anything. On the other hand, if they do make an order, instead of a warning, you want to show them what they ordered. If you rearrange the code and add an else statement, you can display either a warning or a summary: 

You can build more complicated logical processes by nesting if statements within each other. In the following code, the summary will be displayed only if the condition \$totalqty == 0 is true, and each line in the summary will be displayed only if its own condition is met: 

#### 1.13.4 elseif Statements

For many of the decisions you make, you have more than two options. You can create a sequence of many options using the elseif statement, which is a combination of an else and an if statement. When you provide a sequence of conditions, the program can check each until it finds one that is true. 

Note that you are free to type elseif or else if—versions with or without a space are both correct.

1『原来 php 里 elseif 和 else if 都可以，python、JS 里都是 elseif。』

If you are going to write a cascading set of elseif statements, you should be aware that only one of the blocks or statements will be executed. It did not matter in this example because all the conditions were mutually exclusive; only one can be true at a time. If you write conditions in a way that more than one could be true at the same time, only the block or statement following the first true condition will be executed.

1『多个条件为真的情况，只执行第一个条件为真的语句。』

#### 1.13.5 switch Statements

The switch statement works in a similar way to the if statement, but it allows the condition to take more than two values. In an if statement, the condition can be either true or false. In a switch statement, the condition can take any number of different values, as long as it evaluates to a simple type (integer, string, or float). You need to provide a case statement to handle each value you want to react to and, optionally, a default case to handle any that you do not provide a specific case statement for.

```php
switch($find) {  
    case "a" :    
        echo "<p>Regular customer.</p>";    
        break;  
    case "b" :   
        echo "<p>Customer referred by TV advert.</p>";    
        break;  
    case "c" :    
        echo "<p>Customer referred by phone directory.</p>";    
        break;  
    case "d" :    
        echo "<p>Customer referred by word of mouth.</p>";    
        break;  
    default :    
        echo "<p>We do not know how this customer found us.</p>";    
        break;
    }
```

(Note that both of these examples assume you have extracted \$find from the \$\_POST array.)

The switch statement behaves somewhat differently from an if or elseif statement. An if statement affects only one statement unless you deliberately use curly braces to create a block of statements. A switch statement behaves in the opposite way. When a case statement in a switch is activated, PHP executes statements until it reaches a break statement. Without break statements, a switch would execute all the code following the case that was true. When a break statement is reached, the next line of code after the switch statement is executed.

#### 1.13.6 Comparing the Different Conditionals

If you are not familiar with the statements described in the preceding sections, you might be asking,「Which one is the best?」That is not really a question we can answer. There is nothing that you can do with one or more else, elseif, or switch statements that you cannot do with a set of if statements. You should try to use whichever conditional will be most readable in your situation. You will acquire a feel for which suits different situations as you gain experience.

### 1.14 Repeating Actions Through Iteration

One thing that computers have always been very good at is automating repetitive tasks. If you need something done the same way a number of times, you can use a loop to repeat some parts of your program.

Bob wants a table displaying the freight cost that will be added to a customer’s order. With the courier Bob uses, the cost of freight depends on the distance the parcel is being shipped. This cost can be worked out with a simple formula. You want the freight table to resemble the table in Figure 1.7.

Rather than requiring an easily bored human—who must be paid for his time—to type the HTML, having a cheap and tireless computer do it would be helpful. Loop statements tell PHP to execute a statement or block repeatedly.

#### 1.14.1 while Loops

The simplest kind of loop in PHP is the while loop. Like an if statement, it relies on a  condition. The difference between a while loop and an if statement is that an if statement executes the code that follows it only once if the condition is true. A while loop executes the block repeatedly for as long as the condition is true. You generally use a while loop when you don’t know how many iterations will be required to make the condition true. If you require a fixed number of iterations, consider using a for loop. The basic structure of a while loop is

    while( condition ) expression;

The following while loop will display the numbers from 1 to 5:

```php
$num = 1;
while ($num <= 5 ){  
    echo $num."<br />";  
    $num++;
}
```

At the beginning of each iteration, the condition is tested. If the condition is false, the block will not be executed and the loop will end. The next statement after the loop will then be executed. You can use a while loop to do something more useful, such as display the repetitive freight table in Figure 1.7. Listing 1.3 uses a while loop to generate the freight table.

#### 1.14.2 for and foreach Loops

The way that you used the while loops in the preceding section is very common. You set a counter to begin with. Before each iteration, you test the counter in a condition. And at the end of each iteration, you modify the counter. You can write this style of loop in a more compact form by using a for loop. The basic  structure of a for loop is

```
for( expression1; condition; expression2)  
    expression3;
```

1) expression1 is executed once at the start. Here, you usually set the initial value of a counter. 2) The condition expression is tested before each iteration. If the expression returns false, iteration stops. Here, you usually test the counter against a limit. 3) expression2 is executed at the end of each iteration. Here, you usually adjust the value of the counter. 4) expression3 is executed once per iteration. This expression is usually a block of code and contains the bulk of the loop code.
 
Both the while and for versions are functionally identical. The for loop is somewhat more compact, saving two lines. Both these loop types are equivalent; neither is better or worse than the other. In a given  situation, you can use whichever you find more intuitive.

As a side note, you can combine variable variables with a for loop to iterate through a series of repetitive form fields. If, for example, you have form fields with names such as name1, name2, name3, and so on, you can process them like this:

```php
for ($i=1; $i <= $numnames; $i++){  
    $temp= "name$i";  
    echo htmlspecialchars($$temp).'<br />'; // or whatever processing you want to do
}
```

By dynamically creating the names of the variables, you can access each of the fields in turn. As well as the for loop, there is a foreach loop, designed specifically for use with arrays. We discuss how to use it in Chapter 3.

#### 1.14.3 do...while Loops

The final loop type we describe behaves slightly differently. The general structure of a do...while statement is

    do  expression;while( condition );

A do...while loop differs from a while loop because the condition is tested at the end. This means that in a do...while loop, the statement or block within the loop is always executed at least once. Even if you consider this example in which the condition will be false at the start and can never become true, the loop will be executed once before checking the condition and ending:

```php
$num = 100;
do{  
    echo $num."<br />";
}while ($num < 1 ) ;
```

### 1.15 Breaking Out of a Control Structure or Script

If you want to stop executing a piece of code, you can choose from three approaches, depending on the effect you are trying to achieve. 1) If you want to stop executing a loop, you can use the break statement as previously discussed in the section on switch. If you use the break statement in a loop, execution of the script will continue at the next line of the script after the loop. 2) If you want to jump to the next loop iteration, you can instead use the continue statement. 3) If you want to finish executing the entire PHP script, you can use exit. This approach is typically useful when you are performing error checking. For example, you could modify the earlier example as follows:

```php
if($totalqty == 0){  
    echo "You did not order anything on the previous page!<br />";  
    exit;
}
```

1『找错的时候经常用 exit; 退出，结合函数 var_dump() 一起用。』 
 
### 1.16 Employing Alternative Control Structure Syntax

For all the control structures we have looked at, there is an alternative form of syntax. It consists of replacing the opening brace ({) with a colon (:) and the closing brace with a new keyword, which will be endif, endswitch, endwhile, endfor, or endforeach, depending on which control structure is being used. No alternative syntax is available for do...while loops. For example, the code

```php
if ($totalqty == 0) {  
    echo "You did not order anything on the previous page!<br />";  
    exit;
}
```

could be converted to this alternative syntax using the keywords if and endif:

```php
if ($totalqty == 0) :  
    echo "You did not order anything on the previous page!<br />";  
    exit;
endif;
```
 
### 1.17 Using declare

One other control structure in PHP, the declare structure, is not used as frequently in day-to-day coding as the other constructs. The general form of this control structure is as follows:

```php
declare (directive)
{
    // block
}
```

This structure is used to set execution directives for the block of code—that is, rules about how the following code is to be run. Currently, only two execution directives, ticks and encoding, have been implemented. You use ticks by inserting the directive ticks=n. It allows you to run a specific function every n lines of code inside the code block, which is principally useful for profiling and debugging. The encoding directive is used to set encoding for a particular script, as follows:

```
declare(encoding='UTF-8');
```

In this case, the declare statement may not be followed by a code block if you are using namespaces. We’ll talk about namespaces more later. The declare control structure is mentioned here only for completeness. We consider some examples showing how to use tick functions in Chapters 25「Using PHP and MySQL for Large Projects,」and 26「Debugging and Logging.」

## 02. Storing and Retrieving Data

Now that you know how to access and manipulate data entered in an HTML form, you can look at ways of storing that information for later use. In most cases, including the example from the previous chapter, you’ll want to store this data and load it later. In this case, you need to write customer orders to storage so that they can be filled later.

In this chapter, you learn how to write the customer’s order from the previous example to a file and read it back. You also learn why this isn’t always a good solution. When you have large numbers of orders, you should use a database management system such as MySQL instead.

Key topics covered in this chapter include: 1) Saving data for later. 2) Opening a file. 3) Creating and writing to a file. 4) Closing a file. 5) Reading from a file. 6) Locking files. 7) Deleting files. 8) Using other useful file functions. 9) Doing it a better way: using database management systems.

### 2.1 Saving Data for Later

You can store data in two basic ways: in flat files or in a database. A flat file can have many formats, but in general, when we refer to a flat file, we mean a simple text file. For this chapter’s example, you will write customer orders to a text file, one order per line.

Writing orders this way is very simple, but also limiting, as you’ll see later in this chapter. If you’re dealing with information of any reasonable volume, you’ll probably want to use a database instead. However, flat files have their uses, and in some situations you need to know how to use them.
 
### 2.2 Storing and Retrieving Bob’s Orders

In this chapter, you use a slightly modified version of the order form you looked at in the preceding chapter. Begin with this form and the PHP code you wrote to process the order data. We’ve modified the form to include a quick way to obtain the customer’s shipping address. You can see this modified form in Figure 2.1.

The form field for the shipping address is called address. This gives you a variable you can access as \$\_REQUEST['address'] or \$\_POST['address'] or \$\_GET['address'], depending on the form submission method. (See Chapter 1,「PHP Crash Course,」for details.) In this chapter, you write each order that comes in to the same file. Then you construct a web interface for Bob’s staff to view the orders that have been received.

### 2.3 Processing Files

Writing data to a file requires three steps: 1) Open the file. If the file doesn’t already exist, you need to create it. 2) Write the data to the file. 3) Close the file.

Similarly, reading data from a file takes three steps: 1) Open the file. If you cannot open the file (for example, if it doesn’t exist), you need to recognize this and exit gracefully. 2) Read data from the file. 3) Close the file. When you want to read data from a file, you have many choices about how much of the file to read at a time. We’ll describe some common choices in detail. For now, we’ll start at the beginning by opening a file.

### 2.4 Opening a File

To open a file in PHP, you use the fopen() function. When you open the file, you need to specify how you intend to use it. This is known as the file mode.

#### 2.4.1 Choosing File Modes

The operating system on the server needs to know what you want to do with a file that you are opening. It needs to know whether the file can be opened by another script while you have it open and whether you (or the script owner) have permission to use it in the requested way. Essentially, file modes give the operating system a mechanism to determine how to handle access requests from other people or scripts and a method to check that you have access and permission to a particular file.

You need to make three choices when opening a file: 1) You might want to open a file for reading only, for writing only, or for both reading and writing. 2) If writing to a file, you might want to overwrite any existing contents of a file or append new data to the end of the file. You also might like to terminate your program gracefully instead of overwriting a file if the file already exists. 3) If you are trying to write to a file on a system that differentiates between binary and text files, you might need to specify this fact. The fopen() function supports combinations of these three options.

#### 2.4.2 Using fopen() to Open a File

Assume that you want to write a customer order to Bob’s order file. You can open this file for writing with the following:

```php
$fp = fopen("$document_root/../orders/orders.txt", 'w');
```

When fopen() is called, it expects two, three, or four parameters. Usually, you use two, as shown in this code line.

The first parameter should be the file you want to open. You can specify a path to this file, as in the preceding code; here, the orders.txt file is in the orders directory. We used the PHP built-in variable \$\_SERVER['DOCUMENT_ROOT'] but, as with the cumbersome full names for form variables, we assigned a shorter name.

This variable points at the base of the document tree on your web server. This code line uses .. to mean「the parent directory of the document root directory.」This directory is outside the document tree, for security reasons. In this case, we do not want this file to be web acces-sible except through the interface that we provide. This path is called a relative path because it describes a position in the file system relative to the document root. As with the short names given form variables, you need the following line at the start of your script to copy the contents of the long-style variable to the short-style name.

```php
$document_root = $_SERVER['DOCUMENT_ROOT'];
```

You could also specify an absolute path to the file. This is the path from the root directory (/ on a Unix system and typically C:\ on a Windows system). On our Unix server, this path could be something like /data/orders. If no path is specified, the file will be created or looked for in the same directory as the script itself. The directory used will vary if you are running PHP through some kind of CGI wrapper and depends on your server configuration.

In a Unix environment, you use forward slashes (/) in directory paths. If you are using a Windows platform, you can use forward (/) or backslashes (\). If you use backslashes, they must be escaped (marked as a special character) for fopen() to understand them properly. To escape a character, you simply add an additional backslash in front of it, as shown in the following:

```php
$fp = fopen("$document_root\\..\\orders\\orders.txt", 'w');
```

Very few people use backslashes in paths within PHP because it means the code will work only in Windows environments. If you use forward slashes, you can often move your code between Windows and Unix machines without alteration.

The second fopen() parameter is the file mode, which should be a string. This string speci-fies what you want to do with the file. In this case, we are passing 'w' to fopen(); this means「open the file for writing.」A summary of file modes is shown in Table 2.1.

The right file mode to choose depends on how the system will be used. We used 'w' in this example which allows only one order to be stored in the file. Each time a new order is taken, it overwrites the previous order. This usage is probably not very sensible, so you would be better off specifying append mode (and binary mode, as recommended):

```php
$fp = fopen("$document_root/../orders/orders.txt", 'ab');
```

The third parameter of fopen() is optional. You can use it if you want to search the include\_path (set in your PHP configuration; see Appendix A,「Installing Apache, PHP, and MySQL」) for a file. If you want to do this, set this parameter to true. If you tell PHP to search the include\_path, you do not need to provide a directory name or path:

```php
$fp = fopen('orders.txt', 'ab', true);
```

The fourth parameter is also optional. The fopen() function allows filenames to be prefixed with a protocol (such as http://) and opened at a remote location. Some protocols allow for an extra parameter. We look at this use of the fopen() function in the next section of this chapter.

If fopen() opens the file successfully, a resource that is effectively a handle or pointer to the file is returned and should be stored in a variable—in this case, \$fp. You use this variable to access the file when you actually want to read from or write to it.

#### 2.4.3 Opening Files Through FTP or HTTP

In addition to opening local files for reading and writing, you can open files via FTP, HTTP, and other protocols using fopen(). You can disable this capability by turning off the allow\_url\_fopen directive in the php.ini file. If you have trouble opening remote files with fopen(), check your php.ini file.

If the filename you use begins with ftp://, a passive mode FTP connection will be opened to the server you specify and a pointer to the start of the file will be returned. If the filename you use begins with http://, an HTTP connection will be opened to the server you specify and a pointer to the response will be returned. Remember that the domain names in your URL are not case sensitive, but the path and file-name might be.

#### 2.4.4 Addressing Problems Opening Files

An error you might make is trying to open a file you don’t have permission to read from or write to. (This error occurs commonly on Unix-like operating systems, but you may also see it occasionally under Windows.) When you do, PHP gives you a warning similar to the one shown in Figure 2.2.

If you receive this error, you need to make sure that the user under which the script runs has permission to access the file you are trying to use. Depending on how your server is set up, the script might be running as the web server user or as the owner of the directory where the script is located.

On most systems, the script runs as the web server user. If your script is on a Unix system in the ~/public_html/chapter02/ directory, for example, you could create a group-writable directory in which to store the order by typing the following:

```
mkdir path/to/orders
chgrp apache path/to/orders
chmod 775 path/to/orders
```

1『

由于用的是 laravel 框架，第 2 步不需要，进入根目录 public 后：

```
mkdir orders
chmod 775 orders
```

』

You could also choose to change ownership of the file to the web server user. Some people will choose to make the file world-writable as a shortcut here, but bear in mind that directories and files that anybody can write to are dangerous. In particular, directories that are accessible directly from the Web should not be writable. For this reason, our orders directory is outside the document tree. We discuss security more in Chapter 15「Building a Secure Web Application.」

Incorrect permission setting is probably the most common thing that can go wrong when opening a file, but it’s not the only thing. If you can’t open the file, you really need to know this so that you don’t try to read data from or write data to it.

If the call to fopen() fails, the function will return false. It will also cause PHP to emit a warning\_level error (E\_WARNING). You can deal with the error in a more user-friendly way by suppressing PHP’s error message and giving your own:

```php
@$fp = fopen("$document_root/../orders/orders.txt", 'ab');
if (!$fp){  
    echo "<p><strong> Your order could not be processed at this time.  "       
        .Please try again later.</strong></p></body></html>";  
    exit;
}
```

The @ symbol in front of the call to fopen() tells PHP to suppress any errors resulting from the function call. Usually, it’s a good idea to know when things go wrong, but in this case we’re going to deal with that problem elsewhere. You can also write this line as follows:

```php
$fp = @fopen("$document_root/../orders/orders.txt", 'a');
```

1『 @ 的用法，处理错误的时候用，可以「压制」任何函数调用时的错误。』

Using this method tends to make it less obvious that you are using the error suppression operator, so it may make your code harder to debug.

Note: In general, use of the error suppression operator is not considered good style, so consider it a shortcut for now. The method described here is a simplistic way of dealing with errors. We look at a more elegant method for error handling in Chapter 7「Error and Exception Handling.」But one thing at a time.

The if statement tests the variable \$fp to see whether a valid file pointer was returned from the fopen() call; if not, it prints an error message and ends script execution.

### 2.6 Closing a File

After you’ve finished using a file, you need to close it. You should do this by using the fclose() function as follows:

```php
fclose($fp);
```

This function returns true if the file was successfully closed or false if it wasn’t. This process is much less likely to go wrong than opening a file in the first place, so in this case we’ve chosen not to test it. The complete listing for the final version of processorder.php is shown in Listing 2.2.

### 2.7 Reading from a File

Right now, Bob’s customers can leave their orders via the Web, but if Bob’s staff members want to look at the orders, they have to open the files themselves. Let’s create a web interface to let Bob’s staff read the files easily. The code for this interface is shown in Listing 2.3.

```php
<?php
    // create short variable name
    $document_root = $_SERVER['DOCUMENT_ROOT'];
?>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>Dalong's Auto Parts</h1>
    <h2>Customer Orders</h2>
    <?php
        @$fp = fopen('$document_root/../orders/orders.txt', 'rb');
        flock($fp, LOCK_SH);    // lock file for reading
        if (!$fp) {
            echo '<p><strong>No orders pending.<br />please try again later.
                    </strong></p>';
            exit;
        }
        while (!feof($fp)) {
            $order = fgets($fp);
            echo htmlspecialchars($order).'<br />>';
        }
        flock($fp, LOCK_UN);    // release read lock
        fclose($fp);
    ?>
</body>
</html>
```

This script follows the sequence we described earlier: open the file, read from the file, close the file. The output from this script using the data file from Listing 2.1 is shown in Figure 2.4.

#### 2.7.1 Opening a File for Reading: fopen()

Again, you open the file by using fopen(). In this case, you open the file for reading only, so you use the file mode 'rb':

```php
$fp = fopen("$document_root/../orders/orders.txt", 'rb');
```

#### 2.7.2 Knowing When to Stop: feof()

In this example, you use a while loop to read from the file until the end of the file is reached. The while loop tests for the end of the file using the feof() function:

```php
while (!feof($fp))
```

The feof() function takes a file handle as its single parameter. It returns true if the file pointer is at the end of the file. Although the name might seem strange, you can remember it easily if you know that feof stands for File End Of File. In this case (and generally when reading from a file), you read from the file until EOF is reached.

#### 2.7.3 Reading a Line at a Time: fgets(), fgetss(), and fgetcsv()

1『看到 fgetcsv() 就知道找到自己想要的知识点了，哈哈。（2020-04-21）』

In this example, you use the fgets() function to read from the file:

```php
$order= fgets($fp);
```

This function reads one line at a time from a file. In this case, it reads until it encounters a newline character (\n) or EOF. You can use many different functions to read from files. The fgets() function, for example, is useful when you’re dealing with files that contain plain text that you want to deal with in chunks.

An interesting variation on fgets() is fgetss(), which has the following prototype:

```php
string fgetss(resource fp[, int length[, string allowable_tags]]);
```

This function is similar to fgets() except that it strips out any PHP and HTML tags found in the string. If you want to leave in any particular tags, you can include them in the  allowable\_tags string. You would use fgetss() for safety when reading a file written by somebody else or one containing user input. Allowing unrestricted HTML code in the file could mess up your carefully planned formatting. Allowing unrestricted PHP or JavaScript could give a malicious user an opportunity to create a security problem.

The function fgetcsv() is another variation on fgets(). It has the following prototype:

```php
array fgetcsv ( resource fp, int length [, string delimiter              
                        [, string enclosure              
                        [, string escape]]])
```

This function breaks up lines of files when you have used a delimiting character, such as the tab character (as we suggested earlier) or a comma (as commonly used by spreadsheets and other applications). If you want to reconstruct the variables from the order separately rather than as a line of text, fgetcsv() allows you to do this simply. You call it in much the same way as you would call fgets(), but you pass it the delimiter you used to separate fields. For example,

```php
$order = fgetcsv($fp, 0, "\t");
```

1『参数 0 表示不限制长度。』

This code would retrieve a line from the file and break it up wherever a tab (\t) was encountered. The results are returned in an array (\$order in this code example). We cover arrays in more detail in Chapter 3. The length parameter should be greater than the length in characters of the longest line in the file you are trying to read, or 0 if you do not want to limit the line length. The enclosure parameter specifies what each field in a line is surrounded by. If not specified, it defaults to " (a double quotation mark).

#### 2.7.4 Reading the Whole File: readfile(), fpassthru(), file(), and file\_get\_contents()

Instead of reading from a file a line at a time, you can read the whole file in one go. Here are four different ways you can do this.

The first uses readfile(). You can replace almost the entire script you wrote previously with one line:

```
readfile("$document_root/../orders/orders.txt");
```

A call to the readfile() function opens the file, echoes the content to standard output (the browser), and then closes the file. The prototype for readfile() is:

```
int readfile(string filename, [bool use_include_path[, resource context]] );
```

The optional second parameter specifies whether PHP should look for the file in the include\_path and operates the same way as in fopen(). The optional context parameter is used only when files are opened remotely via, for example, HTTP; we cover such usage in more detail in Chapter 18. The function returns the total number of bytes read from the file.

1『通过网络协议 HTTP 打开文件，涉及到一个可选参数，去第 18 章看相关信息。』

Second, you can use fpassthru(). To do so, you need to open the file using fopen() first. You can then pass the file pointer as an argument to fpassthru(), which dumps the contents of the file from the pointer’s position onward to standard output. It closes the file when it is finished. You can use fpassthru() as follows:

```
$fp = fopen("$document_root/../orders/orders.txt", 'rb');
fpassthru($fp);
```

The function fpassthru() returns true if the read is successful and false otherwise.

The third option for reading the whole file is using the file() function. This function is  identical to readfile() except that instead of echoing the file to standard output, it turns it into an array. We cover this function in more detail when we look at arrays in Chapter 3. Just for reference, you would call it using：

```php
$filearray = file("$document_root/../orders/orders.txt");
```

This line reads the entire file into the array called \$filearray. Each line of the file is stored in a separate element of the array. Note that this function was not binary safe in older versions of PHP.

The fourth option is to use the file\_get\_contents() function. This function is identical to readfile() except that it returns the content of the file as a string instead of outputting it to the browser. 

#### 2.7.5 Reading a Character: fgetc()

Another option for file processing is to read a single character at a time from a file. You can do this by using the fgetc() function. It takes a file pointer as its only parameter and returns the next character in the file. You can replace the while loop in the original script with one that uses fgetc(), as follows:

```php
while (!feof($fp)){  
    $char = fgetc($fp);  
    if (!feof($fp))    
        echo ($char=="\n" ? "<br />": $char);  }
}
```

This code reads a single character at a time from the file using fgetc() and stores it in \$char, until the end of the file is reached. It then does a little processing to replace the text end-of-line characters (\n) with HTML line breaks (\<br />). 

This is just to clean up the formatting. If you try to output the file with newlines between records, the whole file will be printed on a single line. (Try it and see.) Web browsers do not render whitespace, such as newlines, so you need to replace them with HTML linebreaks (\<br />) instead. You can use the ternary operator to do this neatly.

A minor side effect of using fgetc() instead of fgets() is that fgetc() returns the EOF  character, whereas fgets() does not. You need to test feof() again after you’ve read the  character because you don’t want to echo the EOF to the browser. Reading a file character by character is not generally sensible or efficient unless for some reason you actually want to process it character by character.

#### 2.7.6 Reading an Arbitrary Length: fread()

The final way you can read from a file is to use the fread() function to read an arbitrary number of bytes from the file. This function has the following prototype:

```php
string fread(resource fp, int length);
```

It reads up to length bytes, to the end of the file or network packet, whichever comes first.

### 2.8 Using Other File Functions

Numerous other file functions are useful from time to time. Some that we have found handy are described next.

#### 2.8.1 Checking Whether a File Is There: file_exists()

If you want to check whether a file exists without actually opening it, you can use file_exists(), as follows:

```php
if (file_exists("$document_root/../orders/orders.txt")) {     
    echo 'There are orders waiting to be processed.';
} else {     
    echo 'There are currently no orders.';
}
```

#### 2.8.2 Determining How Big a File Is: filesize()

You can check the size of a file by using the filesize() function:

```php
echo filesize("$document_root/../orders/orders.txt");
```

It returns the size of a file in bytes and can be used in conjunction with fread() to read a whole file (or some fraction of the file) at a time. You can even replace the entire original script with the following:

```
$fp = fopen("$document_root/../orders/orders.txt", 'rb');
echo nl2br(fread( $fp, filesize("$document_root/../orders/orders.txt")));
fclose( $fp ); 
```

The nl2br() function converts the \n characters in the output to HTML line breaks (\<br />).

#### 2.8.3 Deleting a File: unlink()

If you want to delete the order file after the orders have been processed, you can do so by using unlink(). (There is no function called delete.) For example,

```php
unlink("$document_root/../orders/orders.txt");
```

This function returns false if the file could not be deleted. This situation typically occurs if the permissions on the file are insufficient or if the file does not exist.

#### 2.8.4 Navigating Inside a File: rewind(), fseek(), and ftell()

You can manipulate and discover the position of the file pointer inside a file by using rewind(), fseek(), and ftell(). The rewind() function resets the file pointer to the beginning of the file. The ftell()  function reports how far into the file the pointer is in bytes. For example, you can add the following lines to the bottom of the original script (before the fclose() command):

```php
echo 'Final position of the file pointer is '.(ftell($fp));
echo '<br />';rewind($fp);
echo 'After rewind, the position is '.(ftell($fp));
echo '<br />';
```

Figure 2.5  After reading the orders, the file pointer points to the end of the file, an offset of 198 bytes. The call to rewind sets it back to position 0, the start of the file

You can use the function fseek() to set the file pointer to some point within the file. Its prototype is

```php
int fseek ( resource fp, int offset [, int whence])
```

A call to fseek() sets the file pointer fp at a point starting from whence and moving offset bytes into the file. The optional whence parameter defaults to the value SEEK\_SET, which is effectively the start of the file. The other possible values are SEEK\_CUR (the current location of the file pointer) and SEEK\_END (the end of the file).

The rewind() function is equivalent to calling the fseek() function with an offset of zero. For example, you can use fseek() to find the middle record in a file or to perform a binary search. If you reach the level of complexity in a data file where you need to do these kinds of things, your life will be much easier if you use a built-for-purpose database.

Locking FilesImagine a situation in which two customers are trying to order a product at the same time. (This situation is not uncommon, especially when your website starts to get any kind of traffic volume.) What if one customer calls fopen() and begins writing, and then the other customer calls fopen() and also begins writing? What will be the final contents of the file? Will it be the first order followed by the second order, or vice versa? Will it be one order or the other?  Or will it be something less useful, such as the two orders interleaved somehow? The answer depends on your operating system but is often impossible to know.

To avoid problems like this, you can use file locking. You use this feature in PHP by using the flock() function. This function should be called after a file has been opened but before any data is read from or written to the file. The prototype for flock() is:

```php
bool flock (resource fp, int operation [, int &wouldblock])
```

You need to pass it a pointer to an open file and a constant representing the kind of lock you require. It returns true if the lock was successfully acquired and false if it was not. The optional third parameter will contain the value true if acquiring the lock would cause the current process to block (that is, have to wait). The possible values for operation are shown in Table 2.2. 1) LOCK_SH, Reading lock. The file can be shared with other readers. 2) LOCK_EX, Writing lock. This operation is exclusive; the file cannot be shared. 3) LOCK_UN, The existing lock is released. 4) LOCK_NB, Blocking is prevented while you are trying to acquire a lock. (Not  supported on Windows.)

If you are going to use flock(), you need to add it to all the scripts that use the file; otherwise, it is worthless.

Note that flock() does not work with NFS or other networked file systems. It also does not work with antique file systems that do not support locking, such as FAT. On some operating systems, it is implemented at the process level and does not work correctly if you are using a multithreaded server API. 

To use it with the order example, you can alter processorder.php as follows:

```php
@ $fp = fopen("$document_root/../orders/orders.txt", 'ab');

flock($fp, LOCK_EX);

if (!$fp) {      
    echo "<p><strong> Your order could not be processed at this time.            
                                    Please try again later.</strong></p></body></html>";      
    exit;   
}

fwrite($fp, $outputstring, strlen($outputstring));
flock($fp, LOCK_UN);    
fclose($fp);
```

You should also add locks to vieworders.php:

```php
@$fp = fopen("$document_root/../orders/orders.txt", 'rb');   
flock($fp, LOCK_SH); // lock file for reading   // read from file   
flock($fp, LOCK_UN); // release read lock   
fclose($fp);
```

The code is now more robust but still not perfect. What if two scripts tried to acquire a lock at the same time? This would result in a race condition, in which the processes compete for locks but it is uncertain which will succeed. Such a condition could cause more problems. You can do better by using a database.

1『数据库能满足多人同时读写的需求。』

### 2.9 A Better Way: Databases

So far, all the examples we have looked at use flat files. In Part II of this book, we look at how to use MySQL, a relational database management system (RDBMS), instead. You might ask,「Why would I bother?」

#### 2.9.1 Problems with Using Flat Files

There are a number of problems in working with flat files: 

1 When a file grows large, working with it can be very slow. 

2 Searching for a particular record or group of records in a flat file is difficult. If the records are in order, you can use some kind of binary search in conjunction with a fixed-width record to search on a key field. If you want to find patterns of information (for example, you want to find all the customers who live in Sometown), you would have to read in each record and check it individually.

3 Dealing with concurrent access can become problematic. You have seen how to lock files, but locking can cause the race condition we discussed earlier. It can also cause a bottleneck. With enough traffic on a site, a large group of users may be waiting for the file to be unlocked before they can place their order. If the wait is too long, people will go elsewhere to buy.

4 All the file processing you have seen so far deals with a file using sequential processing; that is, you start from the beginning of the file and read through to the end. Inserting records into or deleting records from the middle of the file (random access) can be difficult because you end up reading the whole file into memory, making the changes, and writing the whole file out again. With a large data file, having to go through all these steps becomes a significant overhead.

5 Beyond the limits offered by file permissions, there is no easy way of enforcing different levels of access to data.

#### 2.9.2 How RDBMSs Solve These Problems

Relational database management systems address all these issues: 1) RDBMSs can provide much faster access to data than flat files. And MySQL, the database system we use in this book, has some of the fastest benchmarks of any RDBMS. 2) RDBMSs can be easily queried to extract sets of data that fit certain criteria. 3) RDBMSs have built-in mechanisms for dealing with concurrent access so that you, as a programmer, don’t have to worry about it. 4) RDBMSs provide random access to your data. 5) RDBMSs have built-in privilege systems. MySQL has particular strengths in this area.

Probably the main reason for using an RDBMS is that all (or at least most) of the functionality that you want in a data storage system has already been implemented. Sure, you could write your own library of PHP functions, but why reinvent the wheel? In Part II of this book,「Using MySQL,」we discuss how relational databases work generally, and specifically how you can set up and use MySQL to create database-backed websites.

If you are building a simple system and don’t feel you need a full-featured database but want to avoid the locking and other issues associated with using a flat file, you may want to consider using PHP’s SQLite extension. This extension provides essentially an SQL interface to a flat file. In this book, we focus on using MySQL, but if you would like more information about SQLite, you can find it at http://sqlite.org/ and http://www.php.net/sqlite.

### 2.10 Further Reading

For more information on interacting with the file system, you can go straight to Chapter 17「Interacting with the File System and the Server.」In that part of the book, we talk about how to change permissions, ownership, and names of files; how to work with directories; and how to interact with the file system environment. You may also want to read through the file system section of the PHP online manual at http://www.php.net/filesystem.
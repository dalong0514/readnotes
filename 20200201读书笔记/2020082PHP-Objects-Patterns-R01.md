# 2020082PHP-Objects-Patterns-R01

PHP Objects, Patterns, and Practice

Copyright © 2016 by Matt Zandstra

## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

#### 01. 常识

#### 02. 反常识

#### 03. 知识来源

比如提出者，如何演化成型的；书或专栏具体出现的地方。

#### 04. 例子

### 0201. 术语卡 —— XP

Related topics also grew in prominence. Among them was eXtreme Programming (XP), championed by Kent Beck. XP is an approach to projects that encourages flexible, design-oriented, highly focused planning and execution. Prominent among XP’s principles is an insistence that testing is crucial to a project’s success. Tests should be automated, run often, and preferably designed before their target code is written.

XP also dictates that projects should be broken down into small (very small) iterations. Both code and requirements should be scrutinized at all times. Architecture and design should be a shared and constant issue, leading to the frequent revision of code.

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

#### 01. 出生日期

用一句话描述你对这个大牛的印象。

#### 02. 贡献及经历

#### 03. 论文及书籍

#### 04. 演讲汇总

找一个他的 TED 演讲，有的话。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

## 书评

### 01

每个段落先提出问题，给出实现，并讨论成效，对于 OO 入门有一定帮助，能够帮助开拓思路，对 OO 老鸟有参考价值，可以换换空气，让脑子清空一下，听听别人说什么，对开发新程序有一定作用。内容并不能说新颖，毕竟内容已经是 2007 的了，不过设计模式并不会随着技术的改进而有多少变化，毕竟理论层面上不会有什么改变的东西。

### 02

过程：花了一个月的时间把书中的主要部分，「面向对象」和「模式」部分。第三部分我只是选读了我认为比较有用的「单元测试」章节。翻译： 不错。没有咬文嚼字，通俗易懂，都是按照中国程序员对专属名词的普遍认识所翻译的。

内容部分——面向对象：在读面向对象部分时，我对本书还是抱有很大希望了，东西讲的比较深入，虽然有错误的地方，但是结构还是比较清晰。作者没有把读者当作是刚刚进入 php 世界的小孩子，而是认为读者有了一定的工作经验。所以在作者花了更多的精力来，讲解面向对象的高级特性，还为了给最重要的「模式」部分铺路，讲了一下「对象与设计」。

内容部分——模式： 我对第 7-11 章节还是比较满意的，作者没有太纠缠于任何一个复杂的设计模式，从一些原则开始讲起，譬如，「组合与继承」，「解耦」，「聚合」，「正交」等等。作者将这些零散而又重要的知识点一一呈现，并且细细讲清楚说明白，我还是觉得蛮受用的。一条「针对接口编程，而不是针对实现编程」贯彻始终。后面几个章节的各个小模式不管有用没用讲的也算是清晰（都画了 UML）。但是，个人认为最最恶心的第 12，13 章节让我彻底对这本书失望至极，如果说企业模式章节，是为了说明 MVC 结构的好，那我觉得还勉强说的过去，毕竟有对前面章节的一些知识点的升华，但是「数据库模式」章节，我就真的不能忍受了。一上来就搞了一个「数据库映射器」，我不知道该不该称其为模式。其作用是将数据库表中的行和列转换成项目中的数据结构，这么看感觉还是蛮有意义的，但是使用的方法比较复杂，最可气的是当你废了很大功夫搞懂之后，这一章的后半部分开始说这个方法有哪里哪里不好，我们应该把它细化，而使用的方法针对性很强，灵活性不高，感觉上只有「解耦和」这个作者的思想可以运用到实战中，书中提到的代码我看就算了吧。

都有更好的替代品：想获得面向对象的知识，可以看《php 手册》。想获得模式的知识，可以看《Head First 设计模式》。而第三部分「时间」的各个工具，我想也应该和 phpunit 一样有官方手册可以看吧。没有必要花时间在这本书上面。除非你已经很了解我上面提到的经典书籍里面的知识，想看看如何用 php 来实现模式的各个概念的，那就看看它吧。

### 04

读第一遍读到数据库模式，感觉吃不消了，所以跳过去直接读后面的实践部分。目前在读第二遍，希望这次能吃透作者讲的数据库模式。这绝对是一本每读一遍都会受益一便的好书，虽然书中讲的各种模式目前看来没有应用到工作中的机会，但是通过作者的讲解，你会看到这些模式一旦应用到项目中，会给整个代码的架构和质量带来多大的提升。

很久之前就想买一本介绍模式的书，看亚马逊的评论，有三个选择，四人帮的设计模式，head first desgin pattern 和这一本。如果你是 php 程序员，有一定的代码经验，想了解一下设计模式，这本书应该是你第一本入手的书。四人帮的设计模式应该是你的进阶书。而我个人来说不是那种中意类似看读学 XX 的读者，如果你是的话可能 head first design pattern 比较适合你。

该书的结构很清晰，作者行文也很流畅，虽然有个别语句可能读第一遍不很明白，但那很可能是你没有透彻理解当前的上下文，返回多读几遍便能了解作者的用意。翻译质量算很高的了。但是其中的错误（不知是印刷错误还是作者的错误还是译者的错误）有点多，我目前都有一个长长的列表，打算去官方勘误页面提交（不过貌似现在打不开...）

对象，模式和实践是本书的三个核心部分，有人说第三部分不是很必要，但是对于项目经验不是很丰富的程序员来说，第三部分绝对会对你项目开发流程的认识拓展很多，个人觉得是不能忽略的部分。对象部分对 php 对面向对象的支持和实现讲解的很透彻，不过重点是在实现，而不是设计，如果你需要面向对象设计方面的知识，这部分是远远不够的，但是对于 PHP 面向对象的实现，这部分应该是你需要读得唯一的东西了。

模式部分是本书的精华部分，我个人也在网上或视频教程中学过设计模式，但是还是感觉这本书对于模式的讲解最为透彻。包括项目中遇到的真实问题，可能的解决方案，每种解决方案的不足之处，引入设计模式，讲解模式的实现以及实现结果的优势和不足之处，实现的可能变种......等等方方面面。全面而透彻。

### 05

看到有人说这本书没有达到书名的目标，可能「深入」这个词让他产生的误解了吧，这本书更像一本实实在在的 PHP 进阶指南。本书全文分为三个方面：PHP 面向对象思想，PHP 设计模式，PHP 实践。这三个方面对于初级 PHP 工程师进阶来说都是很重要的内容。

PHP OOP，一般非直接通过 PHP 入门编程的童鞋对 OOP 都应该有一定的理解，这些内容对于 PHP 草根工程师更有帮助。此外，这一部分对 PHP 的一些 OOP 特性进行了阐述。

PHP 设计模式，这一块介绍了比较常用的设计模式，并且用 PHP 的语法进行了实现，对于对设计模式理解不到位的童鞋有帮助。此外，这一部分还涉及一些架构方面的内容，但是浅尝辄止，有兴趣的童鞋可以看一看《企业应用架构模式》一书。

PHP 实践，对于不了解的童鞋帮助很大，对于有所了解的童鞋帮助很小。这一块比较成体系的介绍了 PHP 开发的相关工具，仔细看一遍还是有一些收获的。不过，关于包管理一节用到的 PEAR 包未免太落后了，可以不用学，把精力用来学 Composer 是更优的选择。至于版本管理，SVN 已经落伍了，不过学习一下倒也无妨，本书下一版本已经把 SVN 换成 Git 了。

### 06

设计模式一直以来很难懂，之前遇到很大的瓶颈，买回来这本书，读起来基本一目十行，不是因为内容太简单，而是该做的我都已经做过了，只是在模式上认识还不够清晰，概念体系不完整，所以想看书补补，觉得这本书设计模式部分写的非常好。甚至这本书应该只保留对象和设计模式部分，其它都是多余的。推荐已经了解并且实践过的同行们都来一读，模式这种东西基本上不会发生太大改变，这本书里描述的也算是非常精准了。

至于其它部分，变化太快，比如工具中，phar 没有讲到，发展历程中，错误的预计了 php 的发展方向：php6 搁浅了，phpng（也就是 php7）将在 2015 年推出第一个版本。不过也无怪于作者，毕竟写这本书的时候鸟哥都没有在 github 上提交过 php 的源码。去掉这些多余的部分这本书简直可以堪称完美，或者保留发展历史，把展望去掉，太不好展望了，需要充分了解开源社区中风起云涌的变化。

### 07

这是最好的 PHP 的 OO 书之一，另外一本是 PHP in Action。PHP 架构中常用的设计模式不多，书中基本都谈到了。我觉得学习设计模式最好是和框架一起进行，一个是理论，一个是实践，而且流行的框架基本代表了设计的最新思想，设计模式没有好坏之分，所以有空都应该学学。

## Introduction

When I first conceived of this book, object-oriented design in PHP was an esoteric topic. The intervening years have not only seen the inexorable rise of PHP as an object-oriented language, but also the march of the framework. Frameworks are incredibly useful, of course. They manage the guts and the glue of many (perhaps, these days, most) web applications. What’s more, they often exemplify precisely the principles of design that this book explores. 

There is, though, a danger for developers here, as there is in all useful APIs. This is the fear that one might find oneself relegated to userland, forced to wait for remote gurus to fix bugs or add features at their whim. It’s a short step from this standpoint to a kind of exile in which one is left regarding the innards of a framework as advanced magic, and one’s own work as not much more than a minor adornment stuck up on top of a mighty unknowable infrastructure.

Although I’m an inveterate reinventor of wheels, the thrust of my argument is not that we should all throw away our frameworks and build MVC applications from scratch (at least not always). It is rather that, as developers, we should understand the problems that frameworks solve, and the strategies they use to solve them. We should be able to evaluate frameworks not only functionally but in terms of the design decisions their creators have made, and to judge the quality of their implementations. And yes, when the conditions are right, we should go ahead and build our own spare and focused applications, and, over time, compile our own libraries of reusable code.

1『秉持不要重新造轮子的原则，善用框架，但是要有一个概念，必须得清楚这个框架设计的初衷，它解决了什么问题，它用了什么策略。』

## 01. PHP: Design and Management

### 1. 逻辑脉络

一些面向编程的诉求；编程范式的发展。

### 2. 摘录及评论

I hope this book goes some way toward helping PHP developers apply design-oriented insights to their platforms and libraries, and provides some the conceptual tools needed when it’s time to go it alone. This is a book about object-oriented design and programming. It is also about tools for managing a PHP codebase from collaboration through to deployment.

These two themes address the same problem from different but complementary angles. The primary aim is to build systems that achieve their objectives and lend themselves well to collaborative development. A secondary goal lies in the aesthetics of software systems. As programmers, we build machines that have shape and action. We invest many hours of our working day, and many days of our lives, writing these shapes into being. We want the tools we build, whether individual classes and objects, software components, or end products, to form an elegant whole. The process of version control, testing, documentation, and build does more than support this objective: it is part of the shape we want to achieve. Just as we want clean and clever code, we want a codebase that is designed well for developers and users alike. The mechanics of sharing, reading, and deploying the project should be as important as the code itself.

In July 2004 PHP 5.0 was released. This version introduced a suite of radical enhancements. Perhaps first among these was radically improved support for object-oriented programming. This stimulated much interest in objects and design within the PHP community. In fact, this was an intensification of a process that began when version 4 first made object-oriented programming with PHP a serious reality.

1『2004 年发布的 PHP 5.0 增加了面向对象的编程特性。』

In this chapter, I look at some of the needs that coding with objects can address. I very briefly summarize some aspects of the evolution of patterns and related practices. I also outline the topics covered by this book. I will look at the following: 1) The evolution of disaster: A project goes bad. 2) Design and PHP: How object-oriented design techniques took root in the PHP community. 3) This book: Objects. Patterns. Practice.

### 01. The Problem

You add utility functions (such as database access code) to files that can be included from page to page, and before you know it you have a working web application. You are well on the road to ruin. You don’t realize this, of course, because your site looks fantastic. It performs well, your clients are happy, and your users are spending money. Trouble strikes when you go back to the code to begin a new phase. Now you have a larger team, some more users, a bigger budget. Yet, without warning, things begin to go wrong. It’s as if your project has been poisoned.

Your new programmer is struggling to understand code that is second nature to you, although perhaps a little byzantine in its twists and turns. She is taking longer than you expected to reach full strength as a team member. A simple change, estimated at a day, takes three days when you discover that you must update 20 or more web pages as a result.

One of your coders saves his version of a file over major changes you made to the same code some time earlier. The loss is not discovered for three days, by which time you have amended your own local copy. It takes a day to sort out the mess, holding up a third developer who was also working on the file.

Because of the application’s popularity, you need to shift the code to a new server. The project has to be installed by hand, and you discover that file paths, database names, and passwords are hard-coded into many source files. You halt work during the move because you don’t want to overwrite the configuration changes the migration requires. The estimated two hours becomes eight as it is revealed that someone did something clever involving the Apache module ModRewrite, and the application now requires this to operate properly.

You finally launch phase 2. All is well for a day and a half. The first bug report comes in as you are about to leave the office. The client phones minutes later to complain. Her report is similar to the first, but a little more scrutiny reveals that it is a different bug causing similar behavior. You remember the simple change back at the start of the phase that necessitated extensive modifications throughout the rest of the project.

You realize that not all of the required modifications are in place. This is either because they were omitted to start with or because the files in question were overwritten in merge collisions. You hurriedly make the modifications needed to fix the bugs. You’re in too much of a hurry to test the changes, but they are a simple matter of copy-and-paste, so what can go wrong?

The next morning you arrive at the office to find that a shopping basket module has been down all night. The last-minute changes you made omitted a leading quotation mark, rendering the code unusable. Of course, while you were asleep, potential customers in other time zones were wide awake and ready to spend money at your store. You fix the problem, mollify the client, and gather the team for another day’s firefighting.

This everyday tale of coding folk may seem a little over the top, but I have seen all these things happen over and over again. Many PHP projects start their life small and evolve into monsters. Because the presentation layer also contains application logic, duplication creeps in early as database queries, authentication checks, form processing, and more are copied from page to page. Every time a change is required to one of these blocks of code, it must be made everywhere that the code is found, or bugs will surely follow.

1『原因在于展示层常常也包含很多其他层的东西，比如软件的逻辑层、数据库请求等。还常常没有文档系统、测试系统。』

Lack of documentation makes the code hard to read, and lack of testing allows obscure bugs to go undiscovered until deployment. The changing nature of a client’s business often means that code evolves away from its original purpose until it is performing tasks for which it is fundamentally unsuited. Because such code has often evolved as a seething, intermingled lump, it is hard, if not impossible, to switch out and rewrite parts of it to suit the new purpose.

Now, none of this is bad news if you are a freelance PHP consultant. Assessing and fixing a system like this can fund expensive espresso drinks and DVD box sets for six months or more. More seriously, though, problems of this sort can mean the difference between a business’s success or failure.

### 02. PHP and Other Languages

PHP’s phenomenal popularity meant that its boundaries were tested early and hard. As you will see in the next chapter, PHP started life as a set of macros for managing personal home pages. With the advent of PHP 3 and, to a greater extent, PHP 4, the language rapidly became the successful power behind large enterprise websites. In many ways, however, the legacy of PHP’s beginnings carried through into script design and project management. In some quarters, PHP retained an unfair reputation as a hobbyist language, best suited for presentation tasks.

1『PHP 很多时候是拿来做展示层工作的。』

About this time (around the turn of the millennium), new ideas were gaining currency in other coding communities. An interest in object-oriented design galvanized the Java community. Since Java is an object-oriented language, you may think that this is a redundancy. Java provides a grain that is easier to work with than against, of course, but using classes and objects does not in itself determine a particular design approach.

The concept of the design pattern as a way of describing a problem, together with the essence of its solution, was first discussed in the 1970s. Perhaps aptly, the idea originated in the field of architecture, not computer science. By the early 1990s, object-oriented programmers were using the same technique to name and describe problems of software design. The seminal book on design patterns, Design Patterns: Elements of Reusable Object-Oriented Software (Addison-Wesley Professional, 1995) by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides (henceforth referred to in this book by their affectionate nickname, the Gang of Four), is still indispensable today. The patterns it contains are a required first step for anyone starting out in this field, which is why most of the patterns in this book are drawn from it.

1『面向对象的范式起源于建筑工程领域而非计算机；四人帮的书。』

2『已下载四人帮的原书「2019087Design-Patterns」。』

The Java language itself deployed many core patterns in its API but it wasn’t until the late 1990s that design patterns seeped into the consciousness of the coding community at large. Patterns quickly infected the computer sections of Main Street bookstores, and the first flame wars began on mailing lists and in forums. Whether you think that patterns are a powerful way of communicating craft knowledge or largely hot air (and, given the title of this book, you can probably guess where I stand on that issue), it is hard to deny that the emphasis on software design they have encouraged is beneficial in itself.

Related topics also grew in prominence. Among them was eXtreme Programming (XP), championed by Kent Beck. XP is an approach to projects that encourages flexible, design-oriented, highly focused planning and execution. Prominent among XP’s principles is an insistence that testing is crucial to a project’s success. Tests should be automated, run often, and preferably designed before their target code is written.

XP also dictates that projects should be broken down into small (very small) iterations. Both code and requirements should be scrutinized at all times. Architecture and design should be a shared and constant issue, leading to the frequent revision of code.

2『XP 做一张术语卡片。』

If XP was the militant wing of the design movement, then the moderate tendency is well represented by one of the best books about programming that I have ever read: The Pragmatic Programmer: From Journeyman to Master by Andrew Hunt and David Thomas (Addison-Wesley Professional, 1999).

1『The Pragmatic Programmer 的概念。』

XP was deemed a tad cultish by some, but it grew out of two decades of object-oriented practice at the highest level, and its principles were widely cannibalized. In particular, code revision, known as refactoring, was taken up as a powerful adjunct to patterns. Refactoring has evolved since the 1980s, but it was codified in Martin Fowler’s catalog of refactorings, Refactoring: Improving the Design of Existing Code (Addison-Wesley Professional), which was published in 1999 and defined the field.

2『上面的应该是一篇论文，去找下。』

Testing, too, became a hot issue with the rise to prominence of XP and patterns. The importance of automated tests was further underlined by the release of the powerful JUnit test platform, which became a key weapon in the Java programmer’s armory. A landmark article on the subject,「Test Infected: Programmers Love Writing Tests」by Kent Beck and Erich Gamma (http://junit.sourceforge.net/doc/testinfected/testing.htm), gives an excellent introduction to the topic and remains hugely influential.

2『上面是篇论文，已下载论文「2020014Test Infected: Programmers Love Writing Tests」存入 Zotero，并计划阅读存为本书的附件「2301Test-Infected」。』

PHP 4 was released at about this time, bringing with it improvements in efficiency and, crucially, enhanced support for objects. These enhancements made fully object-oriented projects a possibility. Programmers embraced this feature, somewhat to the surprise of Zend founders Zeev Suraski and Andi Gutmans, who had joined Rasmus Lerdorf to manage PHP development. As you shall see in the next chapter, PHP’s object support was by no means perfect. But with discipline and careful use of syntax, one could really begin to think in objects and PHP at the same time.

Nevertheless, design disasters such as the one depicted at the start of this chapter remained common. Design culture was some way off, and almost nonexistent in books about PHP. Online, however, the interest was clear. Leon Atkinson wrote a piece about PHP and patterns for Zend in 2001, and Harry Fuecks launched his journal at www.phppatterns.com (now defunct) in 2002. Pattern-based framework projects such as BinaryCloud began to emerge, as well as tools for automated testing and documentation.

The release of the first PHP 5 beta in 2003 ensured the future of PHP as a language for object-oriented programming. The Zend 2 Engine provided greatly improved object support. Equally important, it sent a signal that objects and object-oriented design were now central to the PHP project. Over the years, PHP 5 has continued to evolve and improve, incorporating important new features such as namespaces and closures. During this time, it has secured its reputation as the best choice for server-side web programming.

PHP 7, released in December 2015, represents a continuation of this trend. In particular it provides support for scalar and return type declarations — two features that many developers (together with previous editions of this book) have been clamoring for over the years. If you don’t know what that means or why it's important, read on!

1-2『PHP 7 的两个新特性很重要：support for scalar and return type declarations。PHP 7 发布的时间做一张信息卡片。』

### 03. About This Book

This book does not attempt to break new ground in the field of object-oriented design; in that respect, it perches precariously on the shoulders of giants. Instead, I examine, in the context of PHP, some well-established design principles and some key patterns (particularly those inscribed in Design Patterns, the classic Gang of Four book). Finally, I move beyond the strict limits of code to look at tools and techniques that can help to ensure the success of a project. Aside from this introduction and a brief conclusion, the book is divided into three main parts: objects, patterns, and practice.





ObjectsI begin Part 2 with a quick look at the history of PHP and objects, charting their shift from afterthought in PHP 3 to core feature in PHP 5.

You can still be an experienced and successful PHP programmer with little or no knowledge of objects. 

For this reason, I start from first principles to explain objects, classes, and inheritance. Even at this early stage, I look at some of the object enhancements that PHP 5 and PHP 7 introduced.

The basics established, I delve deeper into our topic, examining PHP’s more advanced object-oriented features. I also devote a chapter to the tools that PHP provides to help you work with objects and classes.It is not enough, however, to know how to declare a class, and to use it to instantiate an object. You must first choose the right participants for your system and decide the best ways for them to interact. These choices are much harder to describe and to learn than the bald facts about object tools and syntax. I finish Part 2 with an introduction to object-oriented design with PHP.

PatternsA pattern describes a problem in software design and provides the kernel of a solution.「Solution」here does not mean the kind of cut-and-paste code that you might find in a cookbook (excellent though cookbooks are as resources for the programmer). Instead, a design pattern describes an approach that can be taken to solve a problem. A sample implementation may be given, but it is less important than the concept that it serves to illustrate.


























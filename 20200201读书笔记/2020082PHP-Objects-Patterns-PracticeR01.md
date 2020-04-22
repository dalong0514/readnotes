# 2020082PHP-Objects-Patterns-PracticeR01

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

### 0202. 术语卡 —— PHP 本质的两块内容

In the Beginning: PHP/FI. The genesis of PHP as we know it today lies with two tools developed by Rasmus Lerdorf using Perl. PHP stood for Personal Homepage Tools. FI stood for Form Interpreter. Together, they comprised macros for sending SQL statements to databases, processing forms, and flow control. 

### 0203. 术语卡 ——继承

单纯拆分后的弊端：1）很多重复代码或者重复的形式；2）共有的部分要更新的话每个都得更新，容易忘。3）传参的时候类型检测不好实现了。「继承」是分割与合并之间的平衡把握。

The CD and book aspects of the ShopProduct class don’t work well together but can’t live apart, it seems. I want to work with books and CDs as a single type while providing a separate implementation for each format. I want to provide common functionality in one place to avoid duplication, but allow each format to handle some method calls differently. I need to use inheritance.

### 0301. 人名卡 ——

#### 01. 基本信息

PHP 的发明人。

#### 02. 贡献及书籍

### 0401. 金句卡——code to an interface, not an implementation

As you will see, object-oriented design often uses a method declaration as a kind of contract. The method demands certain inputs and, reciprocally, it promises to give you a particular type of data back. PHP 5 programmers were forced to rely on comments, convention, and manual type checking to maintain contracts of this kind in many cases. Developers and commentators often complained about this. Here is a quote from the previous edition of this book:

…there is still no commitment to provide support for hinted return types. This would allow you to declare in a method or function’s declaration the object type that it returns. This would then be enforced by the PHP engine. Hinted return types would further improve PHP’s support for pattern principles (principles such as「code to an interface, not an implementation」). I hope one day to revise this book to cover that feature!

I’m pleased to write that the day has come! PHP 7 introduced scalar type declarations (previously known as type hints) and return type declarations, and you’ll see them used plenty in this edition. PHP 7 also provided other nice-to-haves, including anonymous classes and some namespace enhancements.

### 0501. 任意卡——设置私有属性、保护属性的原则

As a general rule, err on the side of privacy. Make properties private or protected at first and relax your restriction only as needed. Many (if not most) methods in your classes will be public, but once again, if in doubt, lock it down. A method that provides local functionality for other methods in your class has no relevance to your class’s users. Make it private or protected.

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

很久之前就想买一本介绍模式的书，看亚马逊的评论，有三个选择，四人帮的设计模式，head first desgin pattern 和这一本。如果你是 php 程序员，有一定的代码经验，想了解一下设计模式，这本书应该是你第一本入手的书。四人帮的设计模式应该是你的进阶书。而我个人来说不是那种中意类似看图学 XX 的读者，如果你是的话可能 head first design pattern 比较适合你。

该书的结构很清晰，作者行文也很流畅，虽然有个别语句可能读第一遍不很明白，但那很可能是你没有透彻理解当前的上下文，返回多读几遍便能了解作者的用意。翻译质量算很高的了。但是其中的错误（不知是印刷错误还是作者的错误还是译者的错误）有点多，我目前都有一个长长的列表，打算去官方勘误页面提交（不过貌似现在打不开......）

对象，模式和实践是本书的三个核心部分，有人说第三部分不是很必要，但是对于项目经验不是很丰富的程序员来说，第三部分绝对会对你项目开发流程的认识拓展很多，个人觉得是不能忽略的部分。对象部分对 php 对面向对象的支持和实现讲解的很透彻，不过重点是在实现，而不是设计，如果你需要面向对象设计方面的知识，这部分是远远不够的，但是对于 PHP 面向对象的实现，这部分应该是你需要读得唯一的东西了。

模式部分是本书的精华部分，我个人也在网上或视频教程中学过设计模式，但是还是感觉这本书对于模式的讲解最为透彻。包括项目中遇到的真实问题，可能的解决方案，每种解决方案的不足之处，引入设计模式，讲解模式的实现以及实现结果的优势和不足之处，实现的可能变种......等等方方面面。全面而透彻。

### 05

看到有人说这本书没有达到书名的目标，可能「深入」这个词让他产生的误解了吧，这本书更像一本实实在在的 PHP 进阶指南。本书全文分为三个方面：PHP 面向对象思想，PHP 设计模式，PHP 实践。这三个方面对于初级 PHP 工程师进阶来说都是很重要的内容。

PHP OOP，一般非直接通过 PHP 入门编程的童鞋对 OOP 都应该有一定的理解，这些内容对于 PHP 草根工程师更有帮助。此外，这一部分对 PHP 的一些 OOP 特性进行了阐述。

PHP 设计模式，这一块介绍了比较常用的设计模式，并且用 PHP 的语法进行了实现，对于对设计模式理解不到位的童鞋有帮助。此外，这一部分还涉及一些架构方面的内容，但是浅尝辄止，有兴趣的童鞋可以看一看《企业应用架构模式》一书。

2『在书籍「2020104Laravel实战入门」里也推荐过这本书，已下载书籍「2020105企业应用架构模式」以及原书「2020105Patterns-of-Enterprise-Application-Architecture」，有空一定要去读下。（2020-03-12）』

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

## 0101. PHP: Design and Management

### 1. 逻辑脉络

一些面向编程的诉求；编程范式的发展。

### 2. 摘录及评论

I hope this book goes some way toward helping PHP developers apply design-oriented insights to their platforms and libraries, and provides some the conceptual tools needed when it’s time to go it alone. This is a book about object-oriented design and programming. It is also about tools for managing a PHP codebase from collaboration through to deployment.

These two themes address the same problem from different but complementary angles. The primary aim is to build systems that achieve their objectives and lend themselves well to collaborative development. A secondary goal lies in the aesthetics of software systems. 

As programmers, we build machines that have shape and action. We invest many hours of our working day, and many days of our lives, writing these shapes into being. We want the tools we build, whether individual classes and objects, software components, or end products, to form an elegant whole. The process of version control, testing, documentation, and build does more than support this objective: it is part of the shape we want to achieve. Just as we want clean and clever code, we want a codebase that is designed well for developers and users alike. The mechanics of sharing, reading, and deploying the project should be as important as the code itself.

1『编程两大主题：功能实现和代码简洁。』

In July 2004 PHP 5.0 was released. This version introduced a suite of radical enhancements. Perhaps first among these was radically improved support for object-oriented programming. This stimulated much interest in objects and design within the PHP community. In fact, this was an intensification of a process that began when version 4 first made object-oriented programming with PHP a serious reality.

1『2004 年发布的 PHP 5.0 增加了面向对象的编程特性。』

In this chapter, I look at some of the needs that coding with objects can address. I very briefly summarize some aspects of the evolution of patterns and related practices. I also outline the topics covered by this book. I will look at the following: 1) The evolution of disaster: A project goes bad. 2) Design and PHP: How object-oriented design techniques took root in the PHP community. 3) This book: Objects. Patterns. Practice.

### 01. The Problem

You add utility functions (such as database access code) to files that can be included from page to page, and before you know it you have a working web application. You are well on the road to ruin. You don’t realize this, of course, because your site looks fantastic. It performs well, your clients are happy, and your users are spending money. Trouble strikes when you go back to the code to begin a new phase. Now you have a larger team, some more users, a bigger budget. Yet, without warning, things begin to go wrong. It’s as if your project has been poisoned.

Your new programmer is struggling to understand code that is second nature to you, although perhaps a little byzantine in its twists and turns. She is taking longer than you expected to reach full strength as a team member. A simple change, estimated at a day, takes three days when you discover that you must update 20 or more web pages as a result.

One of your coders saves his version of a file over major changes you made to the same code some time earlier. The loss is not discovered for three days, by which time you have amended your own local copy. It takes a day to sort out the mess, holding up a third developer who was also working on the file.

Because of the application’s popularity, you need to shift the code to a new server. The project has to be installed by hand, and you discover that file paths, database names, and passwords are hard-coded into many source files. You halt work during the move because you don’t want to overwrite the configuration changes the migration requires. The estimated two hours becomes eight as it is revealed that someone did something clever involving the Apache module ModRewrite, and the application now requires this to operate properly.

1『迁移数据（migration）是个需要提前考虑的工作。』

You finally launch phase 2. All is well for a day and a half. The first bug report comes in as you are about to leave the office. The client phones minutes later to complain. Her report is similar to the first, but a little more scrutiny reveals that it is a different bug causing similar behavior. You remember the simple change back at the start of the phase that necessitated extensive modifications throughout the rest of the project.

You realize that not all of the required modifications are in place. This is either because they were omitted to start with or because the files in question were overwritten in merge collisions. You hurriedly make the modifications needed to fix the bugs. You’re in too much of a hurry to test the changes, but they are a simple matter of copy-and-paste, so what can go wrong?

The next morning you arrive at the office to find that a shopping basket module has been down all night. The last-minute changes you made omitted a leading quotation mark, rendering the code unusable. Of course, while you were asleep, potential customers in other time zones were wide awake and ready to spend money at your store. You fix the problem, mollify the client, and gather the team for another day’s firefighting.

This everyday tale of coding folk may seem a little over the top, but I have seen all these things happen over and over again. Many PHP projects start their life small and evolve into monsters. Because the presentation layer also contains application logic, duplication creeps in early as database queries, authentication checks, form processing, and more are copied from page to page. Every time a change is required to one of these blocks of code, it must be made everywhere that the code is found, or bugs will surely follow.

1『原因在于展示层常常也包含很多其他层的东西，比如软件的逻辑层、数据库请求、表单处理等等。还常常没有文档系统、测试系统。』

Lack of documentation makes the code hard to read, and lack of testing allows obscure bugs to go undiscovered until deployment. The changing nature of a client’s business often means that code evolves away from its original purpose until it is performing tasks for which it is fundamentally unsuited. Because such code has often evolved as a seething, intermingled lump, it is hard, if not impossible, to switch out and rewrite parts of it to suit the new purpose.

Now, none of this is bad news if you are a freelance PHP consultant. Assessing and fixing a system like this can fund expensive espresso drinks and DVD box sets for six months or more. More seriously, though, problems of this sort can mean the difference between a business’s success or failure.

### 02. PHP and Other Languages

PHP’s phenomenal popularity meant that its boundaries were tested early and hard. As you will see in the next chapter, PHP started life as a set of macros for managing personal home pages. With the advent of PHP 3 and, to a greater extent, PHP 4, the language rapidly became the successful power behind large enterprise websites. In many ways, however, the legacy of PHP’s beginnings carried through into script design and project management. In some quarters, PHP retained an unfair reputation as a hobbyist language, best suited for presentation tasks.

1『 PHP 很多时候是拿来做展示层工作的，应该是被低估了。』

About this time (around the turn of the millennium), new ideas were gaining currency in other coding communities. An interest in object-oriented design galvanized the Java community. Since Java is an object-oriented language, you may think that this is a redundancy. Java provides a grain that is easier to work with than against, of course, but using classes and objects does not in itself determine a particular design approach.

The concept of the design pattern as a way of describing a problem, together with the essence of its solution, was first discussed in the 1970s. Perhaps aptly, the idea originated in the field of architecture, not computer science. By the early 1990s, object-oriented programmers were using the same technique to name and describe problems of software design. The seminal book on design patterns, Design Patterns: Elements of Reusable Object-Oriented Software (Addison-Wesley Professional, 1995) by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides (henceforth referred to in this book by their affectionate nickname, the Gang of Four), is still indispensable today. The patterns it contains are a required first step for anyone starting out in this field, which is why most of the patterns in this book are drawn from it.

2『面向对象的范式起源于建筑工程领域而非计算机；已下载四人帮的原书「2019087Design-Patterns」。』

The Java language itself deployed many core patterns in its API but it wasn’t until the late 1990s that design patterns seeped into the consciousness of the coding community at large. Patterns quickly infected the computer sections of Main Street bookstores, and the first flame wars began on mailing lists and in forums. Whether you think that patterns are a powerful way of communicating craft knowledge or largely hot air (and, given the title of this book, you can probably guess where I stand on that issue), it is hard to deny that the emphasis on software design they have encouraged is beneficial in itself.

Related topics also grew in prominence. Among them was eXtreme Programming (XP), championed by Kent Beck. XP is an approach to projects that encourages flexible, design-oriented, highly focused planning and execution. Prominent among XP’s principles is an insistence that testing is crucial to a project’s success. Tests should be automated, run often, and preferably designed before their target code is written.

XP also dictates that projects should be broken down into small (very small) iterations. Both code and requirements should be scrutinized at all times. Architecture and design should be a shared and constant issue, leading to the frequent revision of code.

2『 XP 做一张术语卡片。』

If XP was the militant wing of the design movement, then the moderate tendency is well represented by one of the best books about programming that I have ever read: The Pragmatic Programmer: From Journeyman to Master by Andrew Hunt and David Thomas (Addison-Wesley Professional, 1999).

2『 2019 年出了新版，已下载原书「2020120The-Pragmatic-Programmer2Ed」，直觉上这本书一定要读；Martin Fowler 的《重构》2019 年也出了新版，已下载原书「2019030Refactoring2Ed」。』

XP was deemed a tad cultish by some, but it grew out of two decades of object-oriented practice at the highest level, and its principles were widely cannibalized. In particular, code revision, known as refactoring, was taken up as a powerful adjunct to patterns. Refactoring has evolved since the 1980s, but it was codified in Martin Fowler’s catalog of refactorings, Refactoring: Improving the Design of Existing Code (Addison-Wesley Professional), which was published in 1999 and defined the field.

2『上面的应该是一篇论文，去找下。』

Testing, too, became a hot issue with the rise to prominence of XP and patterns. The importance of automated tests was further underlined by the release of the powerful JUnit test platform, which became a key weapon in the Java programmer’s armory. A landmark article on the subject,「Test Infected: Programmers Love Writing Tests」by Kent Beck and Erich Gamma, gives an excellent introduction to the topic and remains hugely influential.

2『上面是篇论文，已下载论文「2020014Test Infected: Programmers Love Writing Tests」存入 Zotero。』

PHP 4 was released at about this time, bringing with it improvements in efficiency and, crucially, enhanced support for objects. These enhancements made fully object-oriented projects a possibility. Programmers embraced this feature, somewhat to the surprise of Zend founders Zeev Suraski and Andi Gutmans, who had joined Rasmus Lerdorf to manage PHP development. As you shall see in the next chapter, PHP’s object support was by no means perfect. But with discipline and careful use of syntax, one could really begin to think in objects and PHP at the same time.

Nevertheless, design disasters such as the one depicted at the start of this chapter remained common. Design culture was some way off, and almost nonexistent in books about PHP. Online, however, the interest was clear. Leon Atkinson wrote a piece about PHP and patterns for Zend in 2001, and Harry Fuecks launched his journal at www.phppatterns.com (now defunct) in 2002. Pattern-based framework projects such as BinaryCloud began to emerge, as well as tools for automated testing and documentation.

The release of the first PHP 5 beta in 2003 ensured the future of PHP as a language for object-oriented programming. The Zend 2 Engine provided greatly improved object support. Equally important, it sent a signal that objects and object-oriented design were now central to the PHP project. Over the years, PHP 5 has continued to evolve and improve, incorporating important new features such as namespaces and closures. During this time, it has secured its reputation as the best choice for server-side web programming.

PHP 7, released in December 2015, represents a continuation of this trend. In particular it provides support for scalar and return type declarations — two features that many developers (together with previous editions of this book) have been clamoring for over the years. If you don’t know what that means or why it's important, read on!

1-2『PHP 7 的两个新特性很重要：support for scalar and return type declarations。PHP 7 发布的时间做一张信息卡片。』

### 03. About This Book

Instead, I examine, in the context of PHP, some well-established design principles and some key patterns (particularly those inscribed in Design Patterns, the classic Gang of Four book). Finally, I move beyond the strict limits of code to look at tools and techniques that can help to ensure the success of a project. Aside from this introduction and a brief conclusion, the book is divided into three main parts: objects, patterns, and practice.

Objects. I begin Part 2 with a quick look at the history of PHP and objects, charting their shift from afterthought in PHP 3 to core feature in PHP 5. You can still be an experienced and successful PHP programmer with little or no knowledge of objects. For this reason, I start from first principles to explain objects, classes, and inheritance. Even at this early stage, I look at some of the object enhancements that PHP 5 and PHP 7 introduced.

1『基于类的面向对象，其基础内容是对象、类和继承。』

The basics established, I delve deeper into our topic, examining PHP’s more advanced object-oriented features. I also devote a chapter to the tools that PHP provides to help you work with objects and classes. It is not enough, however, to know how to declare a class, and to use it to instantiate an object. You must first choose the right participants for your system and decide the best ways for them to interact. These choices are much harder to describe and to learn than the bald facts about object tools and syntax. I finish Part 2 with an introduction to object-oriented design with PHP.

Patterns. A pattern describes a problem in software design and provides the kernel of a solution.「Solution」here does not mean the kind of cut-and-paste code that you might find in a cookbook (excellent though cookbooks are as resources for the programmer). Instead, a design pattern describes an approach that can be taken to solve a problem. A sample implementation may be given, but it is less important than the concept that it serves to illustrate. 

1『设计模式是用来解决问题的；模式是可复用的解决问题的套路。』

Part 3 begins by defining design patterns and describing their structure. I also look at some of the reasons behind their popularity. Patterns tend to promote and follow certain core design principles. An understanding of these can help in analyzing a pattern’s motivation, and can usefully be applied to all programming. I discuss some of these principles. I also examine the Unified Modeling Language (UML), a platform-independent way of describing classes and their interactions.

Although this book is not a pattern catalog, I examine some of the most famous and useful patterns. I describe the problem that each pattern addresses, analyze the solution, and present an implementation example in PHP.

Practice. Even a beautifully balanced architecture will fail if it is not managed correctly. In Part 4, I look at the tools available to help you create a framework that ensures the success of your project. If the rest of the book is about the practice of design and programming, Part 4 is about the practice of managing your code. The tools that I examine can form a support structure for a project, helping to track bugs as they occur, promoting collaboration among programmers, and providing ease of installation and clarity of code.

I have already discussed the power of the automated test. I kick off Part 4 with an introductory chapter that gives an overview of problems and solutions in this area. Many programmers are guilty of giving in to the impulse to do everything themselves. Composer, together with Packagist, its main repository, offers access to thousands of dependency managed packages that can be stitched into projects with ease. I look at the tradeoffs between implementing a feature yourself and deploying a Composer package. While I’m on the topic of Composer, I look at the installation mechanism that makes the deployment of a package as simple as a single command.

1『 Composer 是 PHP 的包管理工具，类似于 Python 的 pip；要学会在自己实现和用 composer 之间取得平衡。』

Code is about collaboration. This fact can be rewarding. It can also be a complete nightmare. Git is a version control system that enables many programmers to work together on the same codebase without overwriting one another’s work. It lets you grab snapshots of your project at any stage in development, see who has made which changes, and split the project into mergeable branches. Git will save your project one day.

When people and libraries collaborate, they often bring different conventions and styles to the party. While this is healthy, it can also undermine interoperability. Words like conform and comply give me the shivers, but it is undeniable that the creativity of the Internet is underpinned by standards. By obeying certain conventions, we are freed to play in an unimaginably vast sandbox. So, in a new chapter, I explore PHP standards, how they can help us, and how and why we should, yes, comply.

Two facts seem inevitable. First, bugs often recur in the same region of code, making some work days an exercise in déjà vu. Second, often improvements break as much as, or more than, they fix. Automated testing can address both of these issues, providing an early warning system for problems in your code. I introduce PHPUnit, a powerful implementation of the so-called xUnit test platform designed first for Smalltalk but ported now to many languages, notably Java. I look in particular at PHPUnit’s features and more generally at the benefits, and some of the costs, of testing.

Applications are messy. They may need files to be installed in nonstandard locations, or want to set up databases, or need to patch server configuration. In short, applications need stuff to be done during installation. Phing is a faithful port of a Java tool called Ant. Phing and Ant interpret a build file and process your source files in any way you tell them to. This usually means copying them from a source directory to various target locations around your system, but, as your needs get more complex, Phing scales effortlessly to meet them.

Some companies enforce development platforms — but in many cases teams end up running an array of different operating systems. Contractors arrive wielding PC laptops (hello Paul Tregoing, fifth edition tech editor), some team members evangelize endlessly for their favorite Linux distro (that’s me and my Fedora), and many hold out for yet another sexy-looking PowerBook (the coffee bar and meeting room use of which doesn’t at all make you look like just another node in a hipster Borg army). All of these will run a LAMP stack with varying degrees of ease. Ideally, though, developers should run their code in environments that closely resemble the ultimate production system. I examine Vagrant, an application which uses virtualization so that team members can keep their idiosyncratic development platforms but run project code on a production-like system.

Testing and build are all very well, but you have to install and run your tests, and keep on doing so in order to reap the benefits. It’s easy to become complacent and let things slide if you don’t automate your builds and tests. I look at some tools and techniques that are lumped together in the category「continuous integration」that will help you do just that.

What’s New in the Fifth Edition. PHP is a living language, and as such it’s under constant review and development. This new edition, too, has been reviewed and thoroughly updated to take account of changes and new opportunities. I cover new features such as anonymous classes, and the long-awaited scalar argument hints and return types. Examples use PHP 7 features where appropriate, so be aware that you will need to run code against the PHP 7 interpreter — or be ready to do some work to downgrade.

In previous editions, I included a chapter on the PEAR package repository. Composer and the Packagist repository are plainly now the standard for PHP development, and I have rewritten the chapter accordingly. It seems that I’ve switched my version control coverage for every other edition or so of this book. I’m glad to say that I’m sticking with Git this time round. I have, however, spent some more time looking at Git repositories like GitHub since these are increasingly used by developers.

I include a new chapter on the previously mentioned Vagrant. In another new chapter, I examine PHP Standards. Since I endorse the value of complying with a style guide, I have reworked every code example in the book to meet the PSR-1 and PSR-2 standards. This was a much bigger commitment than I realized, and tech editor Paul Tregoing has worked valiantly to keep me honest.

## 0102.  PHP and Objects

### 1. 逻辑脉络

PHP 各版本的特性，特别是面向对象在各个版本中的演化。

### 2. 摘录及评论

This short chapter placed objects in their context in the PHP language. The future for PHP is very much bound up with object-oriented design. In the next few chapters, I take a snapshot of PHP’s current support for object features, and introduce some design issues.

Objects were not always a key part of the PHP project. In fact, they were once described as an afterthought by PHP’s designers. As afterthoughts go, this one has proved remarkably resilient. In this chapter, I introduce this book’s coverage of objects by summarizing the development of PHP’s object-oriented features.

1『面向对象并非一直是 php 的核心，php 5 才成为其核心的。』

We will look at the following: 1) PHP/FI 2.0: PHP, but not as we know it. 3) PHP 3: Objects make their first appearance. 4) PHP 4: Object-oriented programming grows up. 5) PHP 5: Objects at the heart of the language. 6) PHP 7: Closing the gap.

### 01. The Accidental Success of PHP Objects

With PHP’s extensive object support and so many object-oriented PHP libraries and applications in circulation, the rise of the object in PHP may seem like the culmination of a natural and inevitable process. In fact, nothing could be further from the truth.

In the Beginning: PHP/FI. The genesis of PHP as we know it today lies with two tools developed by Rasmus Lerdorf using Perl. PHP stood for Personal Homepage Tools. FI stood for Form Interpreter. Together, they comprised macros for sending SQL statements to databases, processing forms, and flow control. These tools were rewritten in C and combined under the name PHP/FI 2.0. The language at this stage looked different from the syntax we recognize today, but not that different. There was support for variables, associative arrays, and functions. Objects, however, were not even on the horizon.

1『PHP 本质的东西，两大块，一是  Personal Homepage Tools，二是 Form Interpreter。Together, they comprised macros for sending SQL statements to databases, processing forms, and flow control. 』

Syntactic Sugar: PHP 3. In fact, even as PHP 3 was in the planning stage, objects were off the agenda. The principal architects of PHP 3 were Zeev Suraski and Andi Gutmans. PHP 3 was a complete rewrite of PHP/FI 2.0, but objects were not deemed a necessary part of the new syntax. According to Zeev Suraski, support for classes was added almost as an afterthought (on 27 August 1997, to be precise). Classes and objects were actually just another way to define and access associative arrays.

Of course, the addition of methods and inheritance made classes much more than glorified associative arrays, but there were still severe limitations on what you might do with your classes. In particular, you could not access a parent class’s overridden methods (don’t worry if you don’t know what this means yet; I will explain later). Another disadvantage that I will examine in the next section was the less than optimal way that objects were passed around in PHP scripts.

1『PHP3 继承的类里面的方法无法重构，即没法覆盖掉父类里同样名称的方法。另外一个缺点是「对象」的传递途径太少： the less than optimal way that objects were passed around in PHP scripts. 』

That objects were a marginal issue at this time is underlined by their lack of prominence in official documentation. The manual devoted one sentence and a code example to objects. The example did not illustrate inheritance or properties.

PHP 4 and the Quiet Revolution. If PHP 4 was yet another groundbreaking step for the language, most of the core changes took place beneath the surface. The Zend Engine (its name derived from Zeev and Andi) was written from scratch to power the language. The Zend Engine is one of the main components that drive PHP. Any PHP function you might care to call is in fact part of the high-level extensions layer. These do the busy work they were named for, like talking to database APIs or juggling strings for you. Beneath that, the Zend Engine manages memory, delegates control to other components, and translates the familiar PHP syntax you work with every day into runnable bytecode. It is the Zend Engine that we have to thank for core language features like classes.

1『 The Zend Engine 是 php 的核心组件，它在底层干了很多很多事。』

From our objective perspective, the fact that PHP 4 made it possible to override parent methods and access them from child classes was a major benefit. A major drawback remained, however. Assigning an object to a variable, passing it to a function, or returning it from a method resulted in a copy being made. Consider an assignment like this:

1『 php 4 在父类、子类上改进了很多，但还遗留一个大问题：对象的赋值并非绑定引用，而是赋值其值（又分配一块内存）。』

```php
$my_obj = new User('bob');
$other = $my_obj;
```

This resulted in the existence of two User objects rather than two references to the same User object. In most object-oriented languages, you would expect assignment by reference rather than by value. This means that you would pass and assign handles that point to objects rather than copy the objects themselves. The default pass-by-value behavior resulted in many obscure bugs as programmers unwittingly modified objects in one part of a script, expecting the changes to be seen via references elsewhere. Throughout this book, you will see many examples in which I maintain multiple references to the same object.

1『创建对象时，通过引用而非通过复制值，上面一段信息很重要。』

Luckily, there was a way of enforcing pass-by-reference, but it meant remembering to use a clumsy construction. Here’s how you would assign by reference:


```php
$other =& $my_obj;
// $other and $my_obj point to same object

// This enforces pass by reference:
function setSchool(& $school)    
    {  
    // $school is now a reference to not a copy of passed object    
    }

//And here is return by reference:
function & getSchool()    
    {        
    // returning a reference not a copy        
    return $this->school;    
    }

```

Although this worked fine, it was easy to forget to add the ampersand, and that meant it was all too easy for bugs to creep into object-oriented code. These were particularly hard to track down, because they rarely caused any reported errors, just plausible but broken behavior.

Coverage of syntax in general, and objects in particular, was extended in the PHP manual, and object-oriented coding began to bubble up to the mainstream. Objects in PHP were not uncontroversial (then, as now, no doubt), and threads like「Do I need objects?」were common flame-bait in mailing lists. Indeed, the Zend site played host to articles that encouraged object-oriented programming side-by-side with others that sounded a warning note. Pass-by-reference issues and controversy notwithstanding, many coders just got on and peppered their code with ampersand characters. Object-oriented PHP grew in popularity. Zeev Suraski wrote this in an article for DevX.com:

3『 [The Object-Oriented Evolution of PHP](http://www.devx.com/webdev/Article/10007) 』

One of the biggest twists in PHP’s history was that despite the very limited functionality, and despite a host of problems and limitations, object-oriented programming in PHP thrived and became the most popular paradigm for the growing numbers of off-the-shelf PHP applications. This trend, which was mostly unexpected, caught PHP in a suboptimal situation.  It became apparent that objects were not behaving like objects in other OO languages, and were instead behaving like [associative] arrays.

As noted in the previous chapter, interest in object-oriented design became obvious in sites and articles online. PHP’s official software repository, PEAR, itself embraced object-oriented programming. With hindsight, it’s easy to think of PHP’s adoption of object-oriented support as a reluctant capitulation to an inevitable force. It’s important to remember that, although object-oriented programming has been around since the 1960s, it really gained ground in the mid-1990s. Java, the great popularizer, was not released until 1995. A superset of C, a procedural language, C++ has been around since 1979. After a long evolution, it arguably made the leap to the big time during the 1990s. Perl 5 was released in 1994, another revolution within a formerly procedural language that made it possible for its users to think in objects (although some argue that Perl’s object-oriented support also felt like something of an afterthought). For a small procedural language, PHP developed its object support remarkably fast, showing a real responsiveness to the requirements of its users.

1『面向对象的概念是 1960 年代提出来的，但真正开始流行成主流是在 1990 年代中后期，java 是 1995 年发布，c++ 是 1990s 大改动（1979 年发布），Perl 5 是 1994 年发布，这些语言都是主流的面向对象语言。』

Change Embraced: PHP 5. PHP 5 represented an explicit endorsement of objects and object-oriented programming. That is not to say that objects were the only way to work with PHP (this book does not say that either, by the way). Objects were, however, recognized as a powerful and important means for developing enterprise systems, and PHP fully supported them in its core design.

1『之前 PHP 对面向对象很不情愿，PHP 5 开始拥抱面向对象。最重要的转变是从「复制对象」升级到了「传递引用」。除了这点，还有很多其他新特性，比如 private and protected methods and properties, the static keyword, namespaces, type hints (now called type declarations), and exceptions。PHP 是服役最长的版本，差不多 20 年。』

Arguably, one significant effect of the enhancements in PHP 5 was the adoption of the language by larger Internet companies. Both Yahoo! And Facebook, for example, started using PHP extensively within their platforms. With version 5, PHP became one of the standard languages for development and enterprise on the internet.

Objects had moved from afterthought to language driver. Perhaps the most important change was the default pass-by-reference behavior which replaced the evils of object copying. That was only the beginning, however. Throughout this book, and particularly in this part of it, we will encounter many more enhancements, including private and protected methods and properties, the static keyword, namespaces, type hints (now called type declarations), and exceptions. PHP 5 was around for a long time (about twelve years), and important new features were released incrementally.

PHP 5.3, for example, brought namespaces. These let you create a named scope for classes and functions, so that you are less likely to run into duplicate names as you include libraries and expand your system. They also rescue you from ugly but necessary naming conventions such as this:

```php
class megaquiz_util_Conf
{
}
```

Class names such as this are one way of preventing clashes between packages, but they can make for tortuous code. We have also seen support for closures, generators, traits, and late static bindings.

1『 php 竟然也支持闭包（closures）、迭代器（generators）、traits、静态绑定（static binding）。』

PHP 7: Closing the Gap. Programmers are a demanding lot. For many lovers of design patterns, there were two key features that PHP still lacked. These were scalar type declarations and enforced return types. With PHP 5 it was possible to enforce the type of an argument passed to a function or method, so long as you only needed to require an object, an array, or later, callable code. Scalar values (like integers, strings, and floats) could not be enforced at all. Furthermore, if you wanted to declare a method or a function’s return type, you were altogether out of luck.

1『PHP 7 最大的改进是：scalar type declarations and enforced return types. 』

As you will see, object-oriented design often uses a method declaration as a kind of contract. The method demands certain inputs and, reciprocally, it promises to give you a particular type of data back. PHP 5 programmers were forced to rely on comments, convention, and manual type checking to maintain contracts of this kind in many cases. Developers and commentators often complained about this. Here is a quote from the previous edition of this book:

…there is still no commitment to provide support for hinted return types. This would allow you to declare in a method or function’s declaration the object type that it returns. This would then be enforced by the PHP engine. Hinted return types would further improve PHP’s support for pattern principles (principles such as「code to an interface, not an implementation」). I hope one day to revise this book to cover that feature!

I’m pleased to write that the day has come! PHP 7 introduced scalar type declarations (previously known as type hints) and return type declarations, and you’ll see them used plenty in this edition. PHP 7 also provided other nice-to-haves, including anonymous classes and some namespace enhancements.

### 02. Advocacy and Agnosticism: The Object Debate

Objects and object-oriented design seem to stir passions on both sides of the enthusiasm divide. Many excellent programmers have produced excellent code for years without using objects, and PHP continues to be a superb platform for procedural web programming.

This book naturally displays an object-oriented bias throughout, a bias that reflects my object-infected outlook. Because this book is a celebration of objects, and an introduction to object-oriented design, it is inevitable that the emphasis is unashamedly object-oriented. Nothing in this book is intended, however, to suggest that objects are the one true path to coding success with PHP.

Whether a developer chose to work with PHP as an object-oriented language was once a matter of preference. This is still true to the extent that one can create perfectly acceptable working systems using functions and global code. Some great tools (e.g., WordPress) are still procedural in their underlying architecture (though even these may make extensive use of objects these days). It is, however, becoming increasingly hard to work as a PHP programmer without using and understanding PHP’s support for objects, not least because the third party libraries you are likely to rely upon in your projects will themselves likely be object-oriented.

1『很多地方看到这种观点：面向对象和面向 function，其实没有绝对的优劣，要看具体的应用场景。』

Still, as you read, it is worth bearing in mind the famous Perl motto,「There’s more than one way to do it.」This is especially true of smaller scripts, where quickly getting a working example up and running is more important than building a structure that will scale well into a larger system (scratch projects of this sort are often known as「spikes」).

Code is a flexible medium. The trick is to know when your quick proof of concept is becoming the root of a larger development, and to call a halt before lasting design decisions are made for you by the sheer weight of your code. Now that you have decided to take a design-oriented approach to your growing project, I hope that this book provides the help that you need to get started building object-oriented architectures.

## 0103. Object Basics

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

This chapter covered a lot of ground, taking a class from an empty implementation through to a fully featured inheritance hierarchy. You took in some design issues, particularly with regard to type and inheritance. You saw PHP’s support for visibility and explored some of its uses. In the next chapter, I will show you more of PHP’s object-oriented features.

Objects and classes lie at the heart of this book and, since the introduction of PHP 5 over a decade ago, they have lain at the heart of PHP, too. In this chapter, I lay down the groundwork for more in-depth coverage of objects and design by examining PHP’s core object-oriented features. If you are new to object-oriented programming, you should read this chapter carefully.

This chapter will cover the following topics: 1) Constructor methods: Automating the setup of your objects. 2) Classes and objects: Declaring classes and instantiating objects. 3) Primitive and class types: Why type matters. 4) Inheritance: Why we need inheritance and how to use it. 5) Visibility: Streamlining your object interfaces and protecting your methods and properties from meddling.

### 01. Classes and Objects

The first barrier to understanding object-oriented programming is the strange and wonderful relationship between the class and the object. For many people, it is this relationship that represents the first moment of revelation, the first flash of object-oriented excitement. So let’s not skimp on the fundamentals.

#### 1.1 A First Class

Classes are often described in terms of objects. This is interesting, because objects are often described in terms of classes. This circularity can make the first steps in object-oriented programming hard going. Because it’s classes that shape objects, we should begin by defining a class.

In short, a class is a code template used to generate one or more objects. You declare a class with the class keyword and an arbitrary class name. Class names can be any combination of numbers and letters, although they must not begin with a number. The code associated with a class must be enclosed within braces. Here I combine these elements to build a class:

```php
// listing 03.01

class ShopProduct
{    
    // class body
}
```

The ShopProduct class in the example is already a legal class, although it is not terribly useful yet. I have done something quite significant, however. I have defined a type; that is, I have created a category of data that I can use in my scripts. The power of this should become clearer as you work through the chapter.

#### 1.2 A First Object (or Two)

If a class is a template for generating objects, it follows that an object is data that has been structured according to the template defined in a class. An object is said to be an instance of its class. It is of the type defined by the class. I use the ShopProduct class as a mold for generating ShopProduct objects. To do this, I need the new operator. The new operator is used in conjunction with the name of a class, like this:

1『 php 里类实例化为对象，用 new 操作符。』

```php
// listing 03.02

$product1 = new ShopProduct();
$product2 = new ShopProduct();
```

The new operator is invoked with a class name as its only operand and returns an instance of that class; in our example, it generates a ShopProduct object.

I have used the ShopProduct class as a template to generate two ShopProduct objects. Although they are functionally identical (that is, empty), \$product1 and \$product2 are different objects of the same type generated from a single class. If you are still confused, try this analogy. Think of a class as a cast in a machine that makes plastic ducks. 

1『体现了对象三元素之一的「唯一标识性」，另外 2 个是状态和行为。』

Our objects are the ducks that this machine generates. The type of thing generated is determined by the mold from which it is pressed. The ducks look identical in every way, but they are distinct entities. In other words, they are different instances of the same type. The ducks may even have their own serial numbers to prove their identities. Every object that is created in a PHP script is also given its own unique identifier. (Note that the identifier is unique for the life of the object; that is, PHP reuses identifiers, even within a process).  I can demonstrate this by printing out the \$product1 and \$product2 objects:

```php
// listing 03.03

var_dump($product1);
var_dump($product2);
```

Executing these functions produces the following output:

```
object(popp\ch03\batch01\ShopProduct)#235 (0) {}
object(popp\ch03\batch01\ShopProduct)#234 (0) {}
```

Note: in ancient versions of php (up to version 5.1), you could print an object directly. this casted the object to a string containing the object’s iD. From php 5.2 onward, the language no longer supports this magic, and any attempt to treat an object as a string now causes an error unless a method named \_\_toString() is defined in the object’s class. I look at methods later in this chapter, and I cover \_\_toString() in Chapter 4「advanced Features.」

By passing the objects to var\_dump(), I extract useful information including, after the hash sign, each object’s internal identifier. In order to make these objects more interesting, I can amend the ShopProduct class to support special data fields called properties.

### 02. Setting Properties in a Class

Classes can define special variables called properties. A property, also known as a member variable, holds data that can vary from object to object. So in the case of ShopProduct objects, you may wish to manipulate title and price fields, for example.

A property in a class looks similar to a standard variable except that, in declaring a property, you must precede the property variable with a visibility keyword. This can be public, protected, or private, and it determines the scope from which the property can be accessed. 

Note: scope refers to the function or class context in which a variable has meaning (it refers in the same way to methods, which I will cover later in this chapter). so a variable defined in a function exists in local scope, and a variable defined outside of the function exists in global scope. as a rule of thumb, it is not possible to access data defined in a scope that is more local than the current one. so if you define a variable inside a function, you cannot later access it from outside that function. Objects are more permeable than this, in that some object variables can sometimes be accessed from other contexts. Which variables can be accessed and from what context is determined by the public, protected, and private keywords, as you shall see.

I will return to these keywords and the issue of visibility later in this chapter. For now, I will declare some properties using the public keyword:

```php
// listing 03.04

class ShopProduct{    
    public $title = "default product";    
    public $producerMainName = "main name";    
    public $producerFirstName = "first name";    
    public $price  = 0;
}
```

As you can see, I set up four properties, assigning a default value to each of them. Any objects I instantiate from the ShopProduct class will now be prepopulated with default data. The public keyword in each property declaration ensures that I can access the property from outside of the object context.

You can access property variables on an object-by-object basis using the characters '->' (the object operator) in conjunction with an object variable and property name, like this:

```php
// listing 03.05

$product1 = new ShopProduct();
print $product1->title;
```

    default product

Because the properties are defined as public, you can assign values to them just as you can read them, replacing any default value set in the class:

```php
// listing 03.06

$product1 = new ShopProduct();
$product2 = new ShopProduct();
$product1->title="My Antonia";
$product2->title="Catch 22";
```

By declaring and setting the \$title property in the ShopProduct class, I ensure that all ShopProduct objects have this property when first created. This means code that uses this class can work with ShopProduct objects based on that assumption. Because I can reset it, though, the value of \$title may vary from object to object.

Note: Code that uses a class, function, or method is often described as the class’s, function’s, or method’s client or as client code. You will see this term frequently in the coming chapters.

In fact, PHP does not force us to declare all our properties in the class. You could add properties dynamically to an object, like this:

```php
// listing 03.07

$product1->arbitraryAddition = "treehouse";
```

However, this method of assigning properties to objects is not considered good practice in object-oriented programming. Why is it bad practice to set properties dynamically? When you create a class you define a type. You inform the world that your class (and any object instantiated from it) consists of a particular set of fields and functions. If your ShopProduct class defines a \$title property, then any code that works with ShopProduct objects can proceed on the assumption that a \$title property will be available. There can be no guarantees about properties that have been dynamically set, though.

1『这不是跟 JS 一样，可以动态添加属性了嘛，赞。但作者却不建议，理由是不好控制。而且可能误加不想要的属性，比如属性名字打错了（后面有例子）。』

My objects are still cumbersome at this stage. When I need to work with an object’s properties, I must currently do so from outside the object. I reach in to set and get property information. Setting multiple properties on multiple objects will soon become a chore:

```php
// listing 03.08

$product1 = new ShopProduct();
$product1->title = "My Antonia";
$product1->producerMainName  = "Cather";
$product1->producerFirstName = "Willa";
$product1->price = 5.99;
```

I work once again with the ShopProduct class, overriding all the default property values one by one until I have set all product details. Now that I have set some data, I can also access it:

```php
// listing 03.09

print "author: {$product1->producerFirstName} "    
    . "{$product1->producerMainName}\n";
```

This outputs the following:

    author: Willa Cather

There are a number of problems with this approach to setting property values. Because PHP lets you set properties dynamically, you will not get warned if you misspell or forget a property name. For example, assume I want to type this line:

```php
$product1->producerMainName  = "Cather";
```

Unfortunately, I mistakenly type it like this:

```php
$product1->producerSecondName  = "Cather";
```

As far as the PHP engine is concerned, this code is perfectly legal, and I would not be warned. When I come to print the author’s name, though, I will get unexpected results.

Another problem is that my class is altogether too relaxed. I am not forced to set a title, a price, or producer names. Client code can be sure that these properties exist, but is likely to be confronted with default values as often as not. Ideally, I would like to encourage anyone who instantiates a ShopProduct object to set meaningful property values.

Finally, I have to jump through hoops to do something that I will probably want to do quite often. As we have seen, printing the full author name is a tiresome process. It would be nice to have the object handle such drudgery on my behalf. All of these problems can be addressed by giving the ShopProduct object its own set of functions that can be used to manipulate property data from within the object context.

1『对象里的成员方法，就是为了解决上面场景遇到的问题而生的，其可以在对象内部操作对象里的数据属性。数据属性声明为私有，在外面只能通过调用成员方法来操作对象里的数据属性，这就解决了在外面误改对象数据属性的可能性。』

### 03. Working with Methods

Just as properties allow your objects to store data, methods allow your objects to perform tasks. Methods are special functions declared within a class. As you might expect, a method declaration resembles a function declaration. The function keyword precedes a method name, followed by an optional list of argument variables in parentheses. The method body is enclosed by braces:

```php
public function myMethod($argument, $another)    
{        
    // ...    
}
```

Unlike functions, methods must be declared in the body of a class. They can also accept a number of qualifiers, including a visibility keyword. Like properties, methods can be declared public, protected, or private. By declaring a method public, you ensure that it can be invoked from outside of the current object. If you omit the visibility keyword in your method declaration, the method will be declared public implicitly. It is considered good practice, however, to declare visibility explicitly for all methods (I will return to method modifiers later in the chapter

```php
// listing 03.10

class ShopProduct
{

    public $title = "default product";    
    public $producerMainName = "main name";    
    public $producerFirstName = "first name";    
    public $price = 0;

    public function getProducer()    {        
    return $this->producerFirstName . " "            
        . $this->producerMainName;    
    }
}
```

In most circumstances, you will invoke a method using an object variable in conjunction with the object operator, ->, and the method name. You must use parentheses in your method call as you would if you were calling a function (even if you are not passing any arguments to the method):

I add the getProducer() method to the ShopProduct class. Notice that I declare getProducer() public, which means it can be called from outside the class. I introduce a feature in this method’s body. The \$this pseudo-variable is the mechanism by which a class can refer to an object instance. If you find this concept hard to swallow, try replacing \$this with the phrase「the current instance.」Consider the following statement:

    $this->producerFirstName

This translates to the following: the \$producerFirstName property of the current instance. So the getProducer() method combines and returns the \$producerFirstName and \$producerMainName properties, saving me from the chore of performing this task every time I need to quote the full producer name. This has improved the class a little. I am still stuck with a great deal of unwanted flexibility, though. 

I rely on the client coder to change a ShopProduct object’s properties from their default values. This is problematic in two ways. First, it takes five lines to properly initialize a ShopProduct object, and no coder will thank you for that. Second, I have no way of ensuring that any of the properties are set when a ShopProduct object is initialized. What I need is a method that is called automatically when an object is instantiated from a class.

#### 3.1 Creating a Constructor Method

A constructor method is invoked when an object is created. You can use it to set things up, ensuring that essential properties are assigned values and any necessary preliminary work is completed.

Note: in versions previous to php 5, a constructor method took on the name of the class that enclosed it. so the ShopProduct class would use a ShopProduct() method as its constructor. this no longer works in all circumstances and was deprecated as of php 7. Name your constructor method \_\_construct().

Note that the method name begins with two underscore characters. You will see this naming convention for many other special methods in PHP classes. Here I define a constructor for the ShopProduct class:

```php
// listing 03.12

class ShopProduct
{    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price = 0;

    public function __construct(        
        $title,        
        $firstName,        
        $mainName,        
        $price    ) {        
        $this->title = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName = $mainName;        
        $this->price = $price;    
        }

    public function getProducer()    {        
    return $this->producerFirstName . " "            
        . $this->producerMainName;    
    }
}
```

Once again, I gather functionality into the class, saving effort and duplication in the code that uses it. The \_\_construct() method is invoked when an object is created using the new operator:

Any arguments supplied are passed to the constructor. So in my example, I pass the title, the first name, the main name, and the product price to the constructor. The constructor method uses the pseudo-variable \$this to assign values to each of the object’s properties.

Note:  a ShopProduct object is now easier to instantiate and safer to use. instantiation and setup are completed in a single statement. any code that uses a ShopProduct object can be reasonably sure that all its properties are initialized.

This predictability is an important aspect of object-oriented programming. You should design your classes so that users of objects can be sure of their features. One way you can make an object safe is to render predictable the types of data it holds in its properties. One might ensure that a \$name property is always made up of character data, for example. But how can you achieve this if property data is passed in from outside the class? In the next section, I examine a mechanism you can use to enforce object types in method declarations.

1『传参的类型检验很重要。』

### 04. Arguments and Types

Type determines the way data can be managed in your scripts. You use the string type to display character data, for example, and manipulate such data with string functions. Integers are used in mathematical expressions, Booleans are used in test expressions, and so on. These categories are known as primitive types. On a higher level, though, a class defines a type. A ShopProduct object, therefore, belongs to the primitive type object, but it also belongs to the ShopProduct class type. In this section, I will look at types of both kinds in relation to class methods.

1『 primitive types 类比于 JS 里的 7 大基本语言类型。』

Method and function definitions do not necessarily require that an argument should be of a particular type. This is both a curse and a blessing. The fact that an argument can be of any type offers you flexibility. You can build methods that respond intelligently to different data types, tailoring functionality to changing circumstances. This flexibility can also cause ambiguity to creep into code when a method body expects an argument to hold one type but gets another.

#### 4.1 Primitive Types

PHP is a loosely typed language. This means that there is no necessity for a variable to be declared to hold a particular data type. The variable \$number could hold the value 2 and the string "two" within the same scope. In strongly typed languages, such as C or Java, you must declare the type of a variable before assigning a value to it, and, of course, the value must be of the specified type.

This does not mean that PHP has no concept of type. Every value that can be assigned to a variable has a type. You can determine the type of a variable’s value using one of PHP’s type-checking functions. Table 3-1  lists the primitive types recognized in PHP and their corresponding test functions. Each function accepts a variable or value and returns true if this argument is of the relevant type.

1『表里有检查类型的库函数，基本都是类型名字前面加了个 is\_ ，比如 is\_integer()。』

Checking the type of a variable can be particularly important when you work with method and function arguments.

Primitive Types Matter: An Example. You need to keep a close eye on type in your code. Here’s an example of one of the many type-related problems that you could encounter.

Imagine that you are extracting configuration settings from an XML file. The \<resolvedomains> XML element tells your application whether it should attempt to resolve IP addresses to domain names, a useful but relatively expensive process. Here is some sample XML:

```
<!-- listing 03.14 -->
<settings>    
    <resolvedomains>false</resolvedomains>
</settings>
```

The string "false" is extracted by your application and passed as a flag to a method called outputAddresses(), which displays IP address data. Here is outputAddresses():

```php
// listing 03.15

class AddressManager
{    
    private $addresses = ["209.131.36.159", "216.58.213.174"];

    public function outputAddresses($resolve)    {        
        foreach ($this->addresses as $address) {            
            print $address;            
            if ($resolve) {                
                print " (".gethostbyaddr($address).")";            
            }            
            print "\n";
        }    
    }
}
```

Of course, the AddressManager class could do with some improvement. It’s not very useful to hardcode IP addresses into a class, for example. Nevertheless, the outputAddresses() method loops through the \$addresses array property, printing each element. If the \$resolve argument variable itself resolves to true, the method outputs the domain name, as well as the IP address.

Here’s one approach that uses the settings XML configuration element in conjunction with the AddressManager class. See if you can spot how it is flawed:

```php
// listing 03.16

$settings = simplexml:load_file(__DIR__."/resolve.xml");
$manager = new AddressManager();
$manager->outputAddresses((string)$settings->resolvedomains);
```

The code fragment uses the SimpleXML API to acquire a value for the resolvedomains element. In this example, I know that this value is the text element "false", and I cast it to a string as the SimpleXML documentation suggests I should.

1『因为知道会误传参 "false"，做了相应的处理，如果不知道会误传何种类型呢？』

This code will not behave as you might expect. In passing the string "false" to the outputAddresses() method, I misunderstand the implicit assumption the method makes about the argument. The method is expecting a Boolean value (that is true or false). The string "false" will, in fact, resolve to true in a test. This is because PHP will helpfully cast a nonempty string value to the Boolean true for you in a test context. Consider this code:

```php
if ( "false" ) {    
    // ...
}
```

It is actually equivalent to this:

```php
if ( true ) {   
    // ...
 }
```

There are a number of approaches you might take to fix this. You could make the outputAddresses() method more forgiving, so that it recognizes a string and applies some basic rules to convert it to a Boolean equivalent:

```php
// listing 03.17

public function outputAddresses($resolve)    {        
if (is_string($resolve)) {            
$resolve =               
    (preg_match("/^(false|no|off)$/i", $resolve) ) ? false : true;        
    }        
    // ...    
}
```

There are good design reasons for avoiding an approach like this, however. Generally speaking, it is better to provide a clear and strict interface for a method or function than it is to offer a fuzzily forgiving one. Fuzzy and forgiving functions and methods can promote confusion and thereby breed bugs.

1『相比于对传入的参数先逻辑判断再进行处理，更好的方式是「提供一个清晰、严格的接口」。』

You could take another approach: Leave the outputAddresses() method as it is and include a comment containing clear instructions that the \$resolve argument should contain a Boolean value. This approach essentially tells the coder to read the small print or reap the consequences:

```php
/**     
* Outputs the list of addresses.     
* If $resolve is true then each address will be resolved     
* @param    $resolve    boolean    Resolve the address?     
*/    f

unction outputAddresses($resolve)    
{       
    // ...    
}
```

This is a reasonable approach, assuming your client coders are diligent readers of documentation.Finally, you could make outputAddresses() strict about the type of data it is prepared to find in the \$resolve argument. For primitive types like boolean, there was really only one way to do this prior to the release of PHP 7. You would have to write code to examine incoming data and take some kind of action if it does not match the required type:

```php
function outputAddresses($resolve)    
{        
    if (! is_bool($resolve)) {            
        // do something drastic        
    }        
    //...    
}
```

This approach can be used to force client code to provide the correct data type in the \$resolve argument or to issue a warning.

Note: in the next section,「taking the hint: Object types,」I will describe a much better way of constraining the type of arguments passed to methods and functions. Converting a string argument on the client’s behalf would be friendly but would probably present other problems. in providing a conversion mechanism, you second-guess the context and intent of the client. by enforcing the boolean data type, on the other hand, you leave the client to decide whether to map strings to boolean values and determine which word should map to true or false. the outputAddresses() method, meanwhile, concentrates on the task it is designed to perform. this emphasis on performing a specific task in deliberate ignorance of the wider context is an important principle in object-oriented programming, and I will return to it frequently throughout the book.

1『更好的实现方法在下节「taking the hint: Object types」里，心痒痒啊。』

In fact, your strategies for dealing with argument types will depend on the seriousness of any potential bugs on the one hand, and the benefits of flexibility on the other. PHP casts most primitive values for you, depending on context. Numbers in strings are converted to their integer or floating point equivalents when used in a mathematical expression, for example. So your code might be naturally forgiving of type errors. If you expect one of your method arguments to be an array, however, you may need to be more careful. Passing a nonarray value to one of PHP’s array functions will not produce a useful result and could cause a cascade of errors in your method.

1『一定要注意，不要把非数组的数据传入接受数组参数的函数里。』

It is likely, therefore, that you will strike a balance among testing for type, converting from one type to another, and relying on good, clear documentation (you should provide the documentation, whatever else you decide to do). 

However you address problems of this kind, you can be sure of one thing—type matters. The fact that PHP is loosely typed makes it all the more important. You cannot rely on a compiler to prevent type-related bugs; you must consider the potential impact of unexpected types when they find their way into your arguments. You cannot afford to trust client coders to read your thoughts, and you should always consider how your methods will deal with incoming garbage.

1『类型检验问题是 php 里是个大问题，同样为弱类型语言的 JS，应该也存在着相同的问题。』

#### 4.2 Taking the Hint: Object Types

Just as an argument variable can contain any primitive type, by default it can contain an object of any type. This flexibility has its uses, but can present problems in the context of a method definition. Imagine a method designed to work with a ShopProduct object:

```php
// listing 03.18

class ShopProductWriter
{    
    public function write($shopProduct)    {        
    $str  = $shopProduct->title . ": "            
        . $shopProduct->getProducer()            
        . " (" . $shopProduct->price . ")\n";        
    print $str;    }
}
```

You can test this class like this:

```php
// listing 03.19

$product1 = new ShopProduct("My Antonia", "Willa", "Cather", 5.99);
$writer = new ShopProductWriter();
$writer->write($product1);
```

This outputs the following:

    My Antonia: Willa Cather (5.99)

The ShopProductWriter class contains a single method, write(). The write() method accepts a ShopProduct object and uses its properties and methods to construct and print a summary string. I used the name of the argument variable, \$shopProduct, as a signal that the method expects a ShopProduct object, but I did not enforce this. That means I could be passed an unexpected object or primitive type and be none the wiser until I begin trying to work with the \$shopProduct argument. By that time, my code may already have acted on the assumption that it has been passed a genuine ShopProduct object.

Note: You might wonder why I didn't add the write() method directly to ShopProduct. the reason lies with areas of responsibility. the ShopProduct class is responsible for managing product data; the ShopProductWriter is responsible for writing it. You will begin to see why this division of labor can be useful as you read this chapter.

1『按业务（功能）划分代码。』

To address this problem, PHP 5 introduced class type declarations (known then as type hints). To add a class type declaration to a method argument, you simply place a class name in front of the method argument you need to constrain. So I can amend the write() method thus:

```php
// listing 03.20

    public function write(ShopProduct $shopProduct)    
    {        
        // ...    
    }
```

Now the write() method will only accept the \$shopProduct argument if it contains an object of type ShopProduct. This snippet tries to call write() with a dodgy object:

1『传递给函数的参数，如果类型不对是一个大问题。PHP 5 引入的 type hints 为此而生，在函数传递的参数前面直接指定类型。其他基本类型比如 string 之类的，不知道是否可以指定，待确认（2020-04-21）。回复：标量类型的声明指定是 PHP 7 新增的特性，下面正好有个例子。』

3『「2020121Full-Stack-Vuejs2-R01」

做路由的时候用到这个语法：

```php
Route::get('/listing/{listing}', function(ListingModel $listing) {
    $model = $listing->toArray();
    return view('app', [ 'model' => $model ]);
})
```

』

```php
// listing 03.21

class Wrong
{
}

$writer = new ShopProductWriter();
$writer->write(new Wrong());
```

Because the write() method contains a class type declaration, passing it a Wrong object causes a fatal error.

    TypeError: Argument 1 passed to ShopProductWriter::write() must be an instance of ShopProduct, instance of Wrong given, called in Runner.php on ...

This saves me from having to test the type of the argument before I work with it. It also makes the method signature much clearer for the client coder. She can see the requirements of the write() method at a glance. She does not have to worry about some obscure bug arising from a type error because the declaration is rigidly enforced.

Even though this automated type checking is a great way of preventing bugs, it is important to understand that type declarations are checked at runtime. This means that a class declaration will only report an error at the moment that an unwanted object is passed to the method. If a call to write() is buried in a conditional clause that only runs on Christmas morning, you may find yourself working the holiday if you haven’t checked your code carefully.

Armed with scalar type declarations, I can add some constraints to the ShopProduct class:

```php
// listing 03.22

class ShopProduct
{    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price = 0;

    public function __construct(        
    string $title,        
    string $firstName,        
    string $mainName,        
    float $price    
    ) {        
    $this->title = $title;        
    $this->producerFirstName = $firstName;        
    $this->producerMainName = $mainName;        
    $this->price = $price;    }

    // ...
}
```

With the constructor method shored up in this way, I can be sure that the \$title, \$firstName, \$mainName arguments will always contain string data, and that \$price will contain a float. I can demonstrate this by instantiating ShopProduct with the wrong information:

```php
// listing 03.23

// will fail
$product = new ShopProduct("title", "first", "main", []);
```

I attempt to instantiate a ShopProduct object. I pass three strings to the constructor, but I fail at the final hurdle by passing in an empty array instead of the required float. Thanks to type declarations, PHP won’t let me get away with that:

    TypeError: Argument 4 passed to ShopProduct::__construct() must be of the type float, array given, called in...

By default, PHP will implicitly cast arguments to the required type, where possible. This is an example of the tension between safety and flexibility we encountered earlier. The new implementation of the ShopProduct class, for example, will quietly turn a string into a float for us. So, this instantiation would not fail:

```php
// listing 03.24

$product = new ShopProduct("title", "first", "main", "4.22");
```

Behind the scenes, the string "4.22" becomes the float 4.22. So far, so useful. But think back to the problem we encountered with the AddressManager class. The string "false" was quietly resolving to the Boolean true. By default, this will still happen if I use a bool type declaration in the AddressManager::outputAddresses() method like this:

```php
// listing 03.25

    public function outputAddresses(bool $resolve)    
    {        
        // ...    
    }
```

Now consider a call that passes along a string like this:

```php
// listing 03.26

$manager->outputAddresses("false");
```

Because of implicit casting, it is functionally identical to one that passes the Boolean value true. You can make scalar type declarations strict, although only on a file by file basis. Here, I turn on strict type declarations and call outputAddresses() with a string once again:

```php
// listing 03.27

declare(strict_types=1);
$manager->outputAddresses("false");
```

1『原来可以自己指定是否采用严格模式。』

Because I declare strict typing, this call causes a TypeError to be thrown:

    TypeError: Argument 1 passed to AddressManager::outputAddresses() must be of the type boolean, string given, called in ...

Note:  a strict\_types declaration applies to the file from which a call is made, and not to the file in which a function or method is implemented. so it’s up to client code to enforce strictness.

You may need to make an argument optional, but nonetheless constrain its type if it is provided. You can do this by providing a default value:

```php
// listing 03.28

class ConfReader{

    public function getValues(array $default = null)    
    {        
        $values = [];

        // do something to get values
        // merge the provided defaults (it will always be an array)
        $values = array_merge($default, $values);        
        return $values;    
    }
}
```

In Table 3-2, I list the type declarations supported by PHP. 1) array. An array. Can default to null or an array. 2) int. An integer Can default to null or an integer. 3) float. A floating point number (a number with a decimal point). An integer will be accepted—even with strict mode enabled. Can default to null, a float, or an integer. 4) callable. Callable code (such as an anonymous function). Can default to null. 5) bool. A Boolean. Can default to null or a Boolean. 6) string. Character data. Can default to null or a string. 7) self. A reference to the containing class. 8) [a class type]. The type of a class or interface. Can default to null.

When I described class type declarations, I implied that types and classes are synonymous. There is a key difference between the two, however. When you define a class, you also define a type, but a type can describe an entire family of classes. The mechanism by which different classes can be grouped together under a type is called inheritance. I discuss inheritance in the next section.

### 05. Inheritance

Inheritance is the means by which one or more classes can be derived from a base class. A class that inherits from another is said to be a subclass of it. This relationship is often described in terms of parents and children. A child class is derived from and inherits characteristics from the parent. These characteristics consist of both properties and methods. The child class will typically add new functionality to that provided by its parent (also known as a superclass); for this reason, a child class is said to extend its parent. Before I dive into the syntax of inheritance, I’ll examine the problems it can help you to solve. 

#### 5.1 The Inheritance Problem

Look again at the ShopProduct class. At the moment, it is nicely generic. It can handle all sorts of products:

```php
// listing 03.29

$product1 = new ShopProduct("My Antonia", "Willa", "Cather", 5.99);
$product2 = new ShopProduct(    "Exile on Coldharbour Lane",    "The", "Alabama 3",    10.99);
print "author: " . $product1->getProducer() . "\n";
print "artist: " . $product2->getProducer() . "\n";
```

Here’s the output:

```
author: Willa Cather
artist: The Alabama 3
```

Separating the producer name into two parts works well with both books and CDs. I want to be able to sort on「Alabama 3」and「Cather」, not on「The」and「Willa」. Laziness is an excellent design strategy, so there is no need to worry about using ShopProduct for more than one kind of product at this stage.

If I add some new requirements to my example, however, things rapidly become more complicated. Imagine, for example, that you need to represent data specific to books and CDs. For CDs, you must store the total playing time; for books, the total number of pages. There could be any number of other differences, but this will serve to illustrate the issue.

How can I extend my example to accommodate these changes? Two options immediately present themselves. First, I could throw all the data into the ShopProduct class. Second, I could split ShopProduct into two separate classes. 

Let’s examine the first approach. Here, I combine CD- and book-related data in a single class:

```php
// listing 03.30

class ShopProduct{    
    public $numPages;    
    public $playLength;    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price;

    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float $price,        
        int $numPages = 0,        
        int $playLength = 0    ) {        
        $this->title = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName  = $mainName;        
        $this->price = $price;        
        $this->numPages = $numPages;        
        $this->playLength = $playLength;    
        }

    public function getNumberOfPages()    {        
        return $this->numPages;    
    }

    public function getPlayLength()    {        
        return $this->playLength;   
    }

    public function getProducer()    {        
        return $this->producerFirstName . " "            
            . $this->producerMainName;    
    }
}
```

I have provided method access to the \$numPages and \$playLength properties to illustrate the divergent forces at work here. An object instantiated from this class will include a redundant method and, for a CD, must be instantiated using an unnecessary constructor argument: a CD will store information and functionality relating to book pages, and a book will support play-length data. This is probably something you could live with right now. But what would happen if I added more product types, each with its own methods, and then added more methods for each type? Our class would become increasingly complex and hard to manage.

So forcing fields that don’t belong together into a single class leads to bloated objects with redundant properties and methods.

The problem doesn’t end with data, either. I run into difficulties with functionality as well. Consider a method that summarizes a product. The sales department has requested a clear summary line for use in invoices. They want me to include the playing time for CDs and a page count for books, so I will be forced to provide different implementations for each type. I could try using a flag to keep track of the object’s format. Here’s an example:

```php
// listing 03.31

public function getSummaryLine()    {        
    $base  = "{$this->title} ( {$this->producerMainName}, ";        
    $base .= "{$this->producerFirstName} )";        
    if ($this->type == 'book') {            
        $base .= ": page count - {$this->numPages}";        
    } elseif ($this->type == 'cd') {            
        $base .= ": playing time - {$this->playLength}";        
    }        
    return $base;    
}
```

In order to set the \$type property, I could test the \$numPages argument to the constructor. Still, once again, the ShopProduct class has become more complex than necessary. As I add more differences to my formats, or add new formats, these functional differences will become even harder to manage. Perhaps I should try another approach to this problem.

As ShopProduct is beginning to feel like two classes in one, I could accept this and create two types rather than one. Here’s how I might do it:

```php
// listing 03.32

class CdProduct{    
    public $playLength;    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price;

    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $playLength    
    ) {        
        $this->title             = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName  = $mainName;        
        $this->price             = $price;        
        $this->playLength        = $playLength;    
    }

    public function getPlayLength()    {        
        return $this->playLength;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": playing time - {$this->playLength}";        
        return $base;    
    }

    public function getProducer()    {        
    return $this->producerFirstName . " "            
        . $this->producerMainName;    
    }
}
```

```php
// listing 03.33

class BookProduct{    
    public $numPages;    
    public $title;    
    public $producerMainName;

    public $producerFirstName;    
    public $price;

    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $numPages    
    ) {        
        $this->title             = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName  = $mainName;        
        $this->price             = $price;        
        $this->numPages          = $numPages;    
    }

    public function getNumberOfPages()    {        
        return $this->numPages;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": page count - {$this->numPages}";        
        return $base;    
    }

    public function getProducer()    {        
        return $this->producerFirstName . " "            
            . $this->producerMainName;    
    }
}
```

I have addressed the complexity issue, but at a cost. I can now create a getSummaryLine() method for each format without having to test a flag. Neither class maintains fields or methods that are not relevant to it.

The cost lies in duplication. The getProducerName() method is exactly the same in each class. Each constructor sets a number of identical properties in the same way. This is another unpleasant odor you should train yourself to sniff out.

If I need the getProducer() methods to behave identically for each class, any changes I make to one implementation will need to be made for the other. Without care, the classes will soon slip out of synchronization. Even if I am confident that I can maintain the duplication, my worries are not over. I now have two types rather than one.

1『拆分后的弊端：1）很多重复代码或者重复的形式；2）共有的部分要更新的话每个都得更新，容易忘。3）传参的时候类型检测不好实现了。』

Remember the ShopProductWriter class? Its write() method is designed to work with a single type: ShopProduct. How can I amend this to work as before? I could remove the class type declaration from the method signature, but then I must trust to luck that write() is passed an object of the correct type. I could add my own type checking code to the body of the method:

```php
// listing 03.34

class ShopProductWriter{    
    public function write($shopProduct)    {        
        if (            
            ! ($shopProduct instanceof CdProduct)  &&            
            ! ($shopProduct instanceof BookProduct)        
        ) {            
            die("wrong type supplied");        
        }        
        $str  = "{$shopProduct->title}: "            
            . $shopProduct->getProducer()            
            . " ({$shopProduct->price})\n";        
        print $str;    
    }
}
```

Notice the instanceof operator in the example; instanceof resolves to true if the object in the left-hand operand is of the type represented by the right-hand operand.

Once again, I have been forced to include a new layer of complexity. Not only do I have to test the \$shopProduct argument against two types in the write() method, but I have to trust that each type will continue to support the same fields and methods as the other. It was all much neater when I simply demanded a single type because I could use a class type declaration and because I could be confident that the ShopProduct class supported a particular interface.

The CD and book aspects of the ShopProduct class don’t work well together but can’t live apart, it seems. I want to work with books and CDs as a single type while providing a separate implementation for each format. I want to provide common functionality in one place to avoid duplication, but allow each format to handle some method calls differently. I need to use inheritance.

1『为什么要发明「继承」特性，作者真的是把当时遇到问题的场景描述清楚了，很赞。任何新的好的特性都是为了解决某一个难题而创造出来的。「继承」是分割与合并之间的平衡把握。』

#### 5.2 Working with Inheritance

The first step in building an inheritance tree is to find the elements of the base class that don’t fit together or that need to be handled differently. I know that the getPlayLength() and getNumberOfPages() methods do not belong together. I also know that I need to create different implementations for the getSummaryLine() method. Let’s use these differences as the basis for two derived classes:

```php
// listing 03.35

class ShopProduct{    
    public $numPages;    
    public $playLength;    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price;    
    
    public function __construct(        
        string $title,
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $numPages = 0,        
        int    $playLength = 0    
    ) {        
        $this->title             = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName  = $mainName;        
        $this->price             = $price;        
        $this->numPages          = $numPages;        
        $this->playLength        = $playLength;    
    }

    public function getProducer()    {        
        return $this->producerFirstName . " "            
            . $this->producerMainName;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        return $base;    
    }
}
```

```php
// listing 03.36

class CdProduct extends ShopProduct{    
    public function getPlayLength()    {        
        return $this->playLength;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": playing time - {$this->playLength}";        
        return $base;    
    }
}
```

```php
// listing 03.37

class BookProduct extends ShopProduct{    
    public function getNumberOfPages() {        
        return $this->numPages;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": page count - {$this->numPages}";        
        return $base;    
    }
}
```

To create a child class, you must use the extends keyword in the class declaration. In the example, I created two new classes, BookProduct and CdProduct. Both extend the ShopProduct class.

Because the derived classes do not define constructors, the parent class’s constructor is automatically invoked when they are instantiated. The child classes inherit access to all the parent’s public and protected methods (though not to private methods or properties). This means that you can call the getProducer() method on an object instantiated from the CdProduct class, even though getProducer() is defined in the ShopProduct class:

```php
// listing 03.38

$product2 = new CdProduct(    
    "Exile on Coldharbour Lane",    
    "The",    
    "Alabama 3",    
    10.99,    
    0,    
    60.33
);
print "artist: {$product2->getProducer()}\n";
```

So both the child classes inherit the behavior of the common parent. You can treat a BookProduct object as if it were a ShopProduct object. You can pass a BookProduct or CdProduct object to the ShopProductWriter class’s write() method and all will work as expected.

Notice that both the CdProduct and BookProduct classes override the getSummaryLine() method, providing their own implementation. Derived classes can extend but also alter the functionality of their parents.

The super class’s implementation of this method might seem redundant because it is overridden by both its children. Nevertheless, it provides basic functionality that new child classes might use. The method’s presence also provides a guarantee to client code that all ShopProduct objects will provide a getSummaryLine() method. Later on you will see how it is possible to make this promise in a base class without providing any implementation at all. Each child ShopProduct class inherits its parent’s properties. Both BookProduct and CdProduct access the \$title property in their versions of getSummaryLine().

1『重载的好处比之前自己想象的要大很多，不仅仅是表层的覆盖。』

Inheritance can be a difficult concept to grasp at first. By defining a class that extends another, you ensure that an object instantiated from it is defined by the characteristics of first the child and then the parent class. Another way of thinking about this is in terms of searching. When I invoke \$product2->getProducer(), there is no such method to be found in the CdProduct class, and the invocation falls through to the default implementation in ShopProduct. When I invoke \$product2->getSummaryLine(), on the other hand, the getSummaryLine() method is found in CdProduct and invoked.

1『跟 JS 里的委托异曲同工，调用对象里的某个属性时，好不到就去它的原型对象里找，再找不到就去其原型对象的原型对象里去，直到找到根原型对象。』

The same is true of property accesses. When I access \$title in the BookProduct class’s getSummaryLine() method, the property is not found in the BookProduct class. It is acquired instead from the parent class, from ShopProduct. The \$title property applies equally to both subclasses, and therefore, it belongs in the superclass.

A quick look at the ShopProduct constructor, however, shows that I am still managing data in the base class that should be handled by its children. The BookProduct class should handle the \$numPages argument and property, and the CdProduct class should handle the \$playLength argument and property. To make this work, I will define constructor methods in each of the child classes.

#### 5.2.1 Constructors and Inheritance

When you define a constructor in a child class, you become responsible for passing any arguments on to the parent. If you fail to do this, you can end up with a partially constructed object. To invoke a method in a parent class, you must first find a way of referring to the class itself: a handle. 

PHP provides us with the parent keyword for this purpose. To refer to a method in the context of a class rather than an object, you use :: rather than ->:

```php
parent::__construct()
```

1『上面语句其实是个调用，里面要传入的参数，是父类里的基本属性。作者没写分号，之前没想到这点。』

The preceding means,「Invoke the \_\_construct() method of the parent class.」Here I amend my example so that each class handles only the data that is appropriate to it:

```php
// listing 03.39

class ShopProduct{    
    public $title;    
    public $producerMainName;    
    public $producerFirstName;    
    public $price;

    function __construct(        
        $title,        
        $firstName,        
        $mainName,        
        $price    
    ) {        
    $this->title             = $title;        
    $this->producerFirstName = $firstName;        
    $this->producerMainName  = $mainName;        
    $this->price             = $price;    
    }

    function getProducer()    {        
        return $this->producerFirstName . " "            
            . $this->producerMainName;    
    }

    function getSummaryLine()    {
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        r
        eturn $base;    
    }
}
```

```php
// listing 03.40

class BookProduct extends ShopProduct{    
    public $numPages;

    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $numPages    
    ) {        
        parent::__construct(            
            $title,            
            $firstName,            
            $mainName,            
            $price        
        );        
        $this->numPages = $numPages;    
    }

    public function getNumberOfPages()    {        
        return $this->numPages;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( $this->producerMainName, ";        
        $base .= "$this->producerFirstName )";        
        $base .= ": page count – {$this->numPages}";        
        return $base;    
    }
}
```

```php
// listing 03.41

class CdProduct extends ShopProduct{    
    public $playLength;

    public function __construct(        
        string $title,        
        string $firstName,
        string $mainName,        
        float  $price,        
        int    $playLength    
    ) {        
        parent::__construct(            
            $title,            
            $firstName,            
            $mainName,            
            $price        
    );        
    $this->playLength = $playLength;    
    }

    public function getPlayLength()    {        
        return $this->playLength;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": playing time - {$this->playLength}";        
        return $base;    
    }
}
```

Each child class invokes the constructor of its parent before setting its own properties. The base class now knows only about its own data. Child classes are generally specializations of their parents. As a rule of thumb, you should avoid giving parent classes any special knowledge about their children.

1『上面的方法，实现了父类里基本属性与子类的分离，子类只有通过构造函数才能访问到父类里的那些基本属性。』

Note: prior to php 5, constructors took on the name of the enclosing class. the new unified constructors use the name \_\_construct(). Using the old syntax, a call to a parent constructor would tie you to that particular class: parent::ShopProduct();. the old constructor syntax was deprecated in php 7.0 and should not be used.

#### 5.2.2 Invoking an Overridden Method

The parent keyword can be used with any method that overrides its counterpart in a parent class. When you override a method, you may not wish to obliterate the functionality of the parent, but rather to extend it. You can achieve this by calling the parent class’s method in the current object’s context. If you look again at the getSummaryLine() method implementations, you will see that they duplicate a lot of code. It would be better to use rather than reproduce the functionality already developed in the ShopProduct class:

```php
// listing 03.42

// ShopProduct class...

function getSummaryLine() {        
    $base  = "{$this->title} ( {$this->producerMainName}, ";        
    $base .= "{$this->producerFirstName} )";        
    return $base;    
}
`
// listing 03.43

// BookProduct class...

public function getSummaryLine() {        
    $base  = parent::getSummaryLine();        
    $base .= ": page count - $this->numPages";        
    return $base;    
}
```

I set up the core functionality for the getSummaryLine() method in the ShopProduct base class. Rather than reproduce this in the CdProduct and BookProduct subclasses, I simply call the parent method before proceeding to add more data to the summary string.

1『子类里的成员函数的重载也可以借鉴构造函数的思路，不用全部重载，父类里有的部分代码可以直接调用。』

Now that you have seen the basics of inheritance, I will reexamine property and method visibility in light of the full picture.

#### 5.3 Public, Private, and Protected: Managing Access to Your Classes

So far, I have declared all properties public. Public access is the default setting for methods and for properties if you use the old var keyword in your property declaration. Elements in your classes can be declared public, private, or protected: 1) Public properties and methods can be accessed from any context. 2) A private method or property can only be accessed from within the enclosing class. Even subclasses have no access. 3) A protected method or property can only be accessed from within either the enclosing class or from a subclass. No external code is granted access.

So how is this useful to us? Visibility keywords allow you to expose only those aspects of a class that are required by a client. This sets a clear interface for your object. By preventing a client from accessing certain properties, access control can also help prevent bugs in your code. Imagine, for example, that you want to allow ShopProduct objects to support a discount. You could add a \$discount property and a setDiscount() method:

```php
// listing 03.44

// ShopProduct class

public $discount = 0;
//...

public function setDiscount(int $num)    {        
    $this->discount = $num;    
}
```

Armed with a mechanism for setting a discount, you can create a getPrice() method that takes account of the discount that has been applied:

```php
public function getPrice()    {        
    return ($this->price - $this->discount);    
}
```

At this point, you have a problem. You only want to expose the adjusted price to the world, but a client can easily bypass the getPrice() method and access the \$price property:

```php
print "The price is {$product1->price}\n";
```

This will print the raw price and not the discount-adjusted price you wish to present. You can put a stop to this straight away by making the \$price property private. This will prevent direct access, forcing clients to use the getPrice() method. Any attempt from outside the ShopProduct class to access the \$price property will fail. As far as the wider world is concerned, this property has ceased to exist.

Setting properties to private can be an overzealous strategy. A private property cannot be accessed by a child class. Imagine that our business rules state that books alone should be ineligible for discounts. You could override the getPrice() method so that it returns the \$price property, applying no discount:

```php
// listing 03.45

// BookProduct

public function getPrice()    {        
    return $this->price;    
}
```

As the private \$price property is declared in the ShopProduct class and not BookProduct, the attempt to access it here will fail. The solution to this problem is to declare \$price protected, thereby granting access to descendant classes. Remember that a protected property or method cannot be accessed from outside the class hierarchy in which it was declared. It can only be accessed from within its originating class or from within children of the originating class.

As a general rule, err on the side of privacy. Make properties private or protected at first and relax your restriction only as needed. Many (if not most) methods in your classes will be public, but once again, if in doubt, lock it down. A method that provides local functionality for other methods in your class has no relevance to your class’s users. Make it private or protected.

1『以上是设置私有属性、保护属性的原则。』

#### 5.3.1 Accessor Methods

Even when client programmers need to work with values held by your class, it is often a good idea to deny direct access to properties, providing methods instead that relay the needed values. Such methods are known as accessors or getters and setters.

1『一个原则，通说对象的方法去访问属性值，不要直接访问，把「方法」作为接口。』

You have already seen one benefit afforded by accessor methods. You can use an accessor to filter a property value according to circumstances, as was illustrated by the getPrice() method. You can also use a setter method to enforce a property type. Type declarations can be used to constrain method arguments, but a property can contain data of any type. Remember the ShopProductWriter class that uses a ShopProduct object to output list data? I can develop this further, so that it writes any number of ShopProduct objects at one time:

```php
// listing 03.46

class ShopProductWriter{    
    public $products = [];
    
    public function addProduct(ShopProduct $shopProduct)    {        
        $this->products[] = $shopProduct;    
    }

    public function write()    {        
        $str =  "";        
        foreach ($this->products as $shopProduct) {            
        $str .= "{$shopProduct->title}: ";            
        $str .= $shopProduct->getProducer();            
        $str .= " ({$shopProduct->getPrice()})\n";        
        }        
    print $str;    
    }
}
```

The ShopProduct Writer class is now much more useful. It can hold many ShopProduct objects and write data for them all in one go. I must trust my client coders to respect the intentions of the class, though. Despite the fact that I have provided an addProduct() method, I have not prevented programmers from manipulating the \$products property directly. Not only could someone add the wrong kind of object to the \$products array property, but he could even overwrite the entire array and replace it with a primitive value. I can prevent this by making the \$products property private:

```php
class ShopProductWriter {    
    private $products = [];
    //...
```

It’s now impossible for external code to damage the \$products property. All access must be via the addProduct() method, and the class type declaration I use in the method declaration ensures that only ShopProduct objects can be added to the array property.

#### 5.3.2 The ShopProduct Classes

Let’s close this chapter by amending the ShopProduct class and its children to lock down access control:

```php
// listing 03.48

class ShopProduct{    
    private   $title;    
    private   $producerMainName;    
    private   $producerFirstName;    
    protected $price;    
    private   $discount = 0;

    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price    
    ) {        
        $this->title             = $title;        
        $this->producerFirstName = $firstName;        
        $this->producerMainName  = $mainName;        
        $this->price             = $price;    
    }

    public function getProducerFirstName()    {        
        return $this->producerFirstName;    
    }

    public function getProducerMainName()    {        
        return $this->producerMainName;    
    }

    public function setDiscount($num)    {        
        $this->discount = $num;   
    }

    public function getDiscount()    {        
        return $this->discount;    
    }

    public function getTitle()    {        
        return $this->title;    
    }

    public function getPrice()    {        
        return ($this->price - $this->discount);    
    }

    public function getProducer()    {        
        return $this->producerFirstName . ""           
            . $this->producerMainName;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";
        return $base;    
    }
}

// listing 03.49

class CdProduct extends ShopProduct{    
    private $playLength;    
    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $playLength    
    ) {        
    parent::__construct(            
        $title,            
        $firstName,            
        $mainName,            
        $price        
    );        
        $this->playLength = $playLength;    
    }

    public function getPlayLength()    {        
        return $this->playLength;    
    }

    public function getSummaryLine()    {        
        $base  = "{$this->title} ( {$this->producerMainName}, ";        
        $base .= "{$this->producerFirstName} )";        
        $base .= ": playing time - {$this->playLength}";        
        return $base;    
    }
}

// listing 03.50

class BookProduct extends ShopProduct{    
    private $numPages;
    public function __construct(        
        string $title,        
        string $firstName,        
        string $mainName,        
        float  $price,        
        int    $numPages    
    ) {
    parent::__construct(            
        $title,            
        $firstName,            
        $mainName,            
        $price        
    );        
        $this->numPages = $numPages;    
    }

    public function getNumberOfPages()    {        
        return $this->numPages;    
    }

    public function getSummaryLine()    {        
        $base  = parent::getSummaryLine();        
        $base .= ": page count - $this->numPages";        
        return $base;    
    }

    public function getPrice()    {        
        return $this->price;    
    }
}
```

There is nothing substantially new in this version of the ShopProduct family. All properties are either private or protected, and I added a number of accessor methods to round things off.

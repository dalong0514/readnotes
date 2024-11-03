## 记忆时间

## 卡片

### 0101. 主题卡 —— Packt 出版社书籍源码仓库

信息源自「2021065Test-Driven-Java-Development0000.md」

The code bundle for the book is also hosted on GitHub at https:/​/​github.​com/PacktPublishing/​Test-​Driven-​Java-​Development-​Second-​Edition. In case there's an update to the code, it will be updated on the existing GitHub repository.

We also have other code bundles from our rich catalog of books and videos available at https:/​/​github.​com/​PacktPublishing/​. Check them out!

2『

[PacktPublishing/Test-Driven-Java-Development-Second-Edition: Test-Driven Java Development – Second Edition, published by Packt](https://github.com/PacktPublishing/Test-Driven-Java-Development-Second-Edition)

已经 clone 原书代码作为本书的附件。（2021-04-24）

又挖到宝藏了，Packt 出版社的所有书籍源码仓库：[Packt](https://github.com/PacktPublishing/)。做一张主题卡片。—— 已完成

』

### 0102. 主题卡 —— Java 常用的开发工具和框架

信息源自「2021065Test-Driven-Java-Development0101.md」

The following topics will be covered in this chapter: 1) Git. 2) Virtual machines. 3) Build tools. 4) The integrated development environment. 5) Unit testing frameworks. 6) Hamcrest and AssertJ. 7) Code coverage tools. 8) Mocking frameworks. 9) User interface testing. 10) Behavior-driven development.

2『上面的 Java 开发工具和框架，做一张主题卡片。（2021-04-24）』—— 已完成

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

Test-Driven Java Development

Second Edition

Copyright © 2018 Packt Publishing

## About the authors

Alex Garcia is a Software Engineer at Schibsted. He started coding in C++ but later moved to Java. He is also interested in Groovy, Scala, and JavaScript. He is always eager to learn new things and that is why he has also worked as a System Administrator and Full Stack Engineer. He is a big fan of agile practices. He is always interested in learning new languages, paradigms, and frameworks. When the computer is turned off, he likes to walk around sunny Barcelona and play sports.

I enjoyed writing this book and I would like to thank those people who made this possible.

Thanks to the technical reviewers and staff at Packt Publishing for their valuable contributions. Thanks Viktor for sharing this experience with me. And finally, special thanks to my parents, my brother, and my girlfriend for being there whenever I need them.

Viktor Farcic is a Senior Consultant at CloudBees, a member of the Docker Captains group, and an author. His big passions are DevOps; microservices; continuous integration, delivery, and deployment; and test-driven development.

He often speaks at community gatherings and conferences. He published The DevOps Toolkit series and the Test-Driven Java Development book. His random thoughts and tutorials can be found at his blog, Technology Conversations.

I would like to thank a lot of people who have supported me during the writing of this book.

The people at Everis and Defe (companies I worked with earlier) provided all the support and encouragement I needed. The technical reviewers, Alvaro Garcia, Esko Luontola, Jeff Deskins, and Muhammad Ali, did a great job by constantly challenging my views, my assumptions, and the quality of the code featured throughout the examples. Alvaro provided even more help by writing the Legacy Code chapter. His experience and expertise in the subject were an invaluable help. The Packt Publishing team was very forthcoming, professional, and always available to provide guidance and support. Finally, I'd like to give a special thanks to my daughter, Sara, and wife, Eva. With weekdays at my job and nights and weekends dedicated to this book, they had to endure months without the support and love they deserve. This book is dedicated to my girls.

## Preface

Test-driven development has been around for a while and many people have still not adopted it. The reason behind this is that TDD is difficult to master. Even though the theory is very easy to grasp, it takes a lot of practice to become really proficient with it. The authors of this book have been practicing TDD for years and will try to pass on their experience to you. They are developers and believe that the best way to learn some coding practice is through code and constant practice. This book follows the same philosophy. We'll explain all the TDD concepts through exercises. This will be a journey through TDD best practices applied to Java development. At the end of it, you will earn a TDD black belt and have one more tool in your software craftsmanship tool belt.

### 01. Who this book is for

If you're an experienced Java developer and want to implement more effective methods of programming systems and applications, then this book is for you.

### 02. What this book covers

Chapter 1, Why Should I Care for Test-Driven Development? , spells out our goal of becoming a Java developer with a TDD black belt. In order to know where we're going, we'll have to discuss and find answers to some questions that will define our voyage.

Chapter 2, Tools, Frameworks, and Environments, will compare and set up all the tools, frameworks and environments that will be used throughout this book. Each of them will be accompanied with code that demonstrates their strengths and weaknesses.

Chapter 3, Red-Green-Refactor – From Failure Through Success until Perfection, will help us develop a Tic-Tac-Toe game using the red-green-refactor technique, which is the pillar of TDD. We'll write a test and see it fail; we'll write a code that implements that test, run all the tests, and see them succeed; and finally, we'll refactor the code and try to make it better.

Chapter 4, Unit Testing – Focusing on What You Do and Not on What Has Been Done, shows that to demonstrate the power of TDD applied to unit testing, we'll need to develop a remote-controlled ship. We'll learn what unit testing really is, how it differs from functional and integration tests, and how it can be combined with test-driven development.

Chapter 5, Design – If It's Not Testable, It's Not Designed Well, will help us develop a Connect 4 game without any tests and try to write tests at the end. This will give us insights into the difficulties we are facing when applications are not developed in a way that they can be tested easily.

Chapter 6, Mocking – Removing External Dependencies, shows how TDD is about speed. We want to quickly demonstrate some idea/concept. We'll continue developing our Tic-Tac-Toe game by adding MongoDB as our data storage. None of our tests will actually use MongoDB since all communications to it will be mocked.

Chapter 7, TDD and Functional Programming – A Perfect Match, dives into the functional programming paradigm and how TDD could be applied when programming in that way. We'll explore parts of the functional API provided by Java since version 8 and create readable and meaningful tests.

Chapter 8, BDD – Working Together with the Whole Team, discusses developing a book store application by using the BDD approach. We'll define the acceptance criteria in the BDD format, carry out the implementation of each feature separately, confirm that it is working correctly by running BDD scenarios, and if required, refactor the code to accomplish the desired level of quality.

Chapter 9, Refactoring Legacy Code – Making It Young Again, will help us refactor an existing application. The process will start with creation of test coverage for the existing code and from there on, we'll be able to start refactoring until both the tests and the code meet our expectations.

Chapter 10, Feature Toggles – Deploying Partially Done Features to Production, will show us how to develop a Fibonacci calculator and use feature toggles to hide functionalities that are not fully finished or that, for business reasons, should not yet be available to our users.

Chapter 11, Putting It All Together, will walk you through all the TDD best practices in detail and refresh the knowledge and experience you gained throughout this book.

Chapter 12, Leverage TDD by Implementing Continuous Delivery, explains how TDD and continuous delivery form a very powerful combination that leads to better and faster software deliveries. Some of the problems that companies are facing nowadays are illustrated with an example of a fictitious company. At the end, the speed of the development is increased and some of the pain points are mitigated by the implementation of an effective development pipeline based on automated tests and continuous delivery.

1『上面的第 7 章、12 章，是二版新增的。（2021-04-24）』

### 03. To get the most out of this book

The exercises in this book require readers to have a 64-bit computer. Installation instructions for all required software is provided throughout the book.

### 04. Download the example code files

You can download the example code files for this book from your account at www.packtpub.com. If you purchased this book elsewhere, you can visit www.packtpub.com/support and register to have the files emailed directly to you.

You can download the code files by following these steps:

1 Log in or register at www.packtpub.com.

2 Select the SUPPORT tab.

3 Click on Code Downloads & Errata.

4 Enter the name of the book in the Search box and follow the onscreen instructions.

Once the file is downloaded, please make sure that you unzip or extract the folder using the latest version of:

```
WinRAR/7-Zip for Windows

Zipeg/iZip/UnRarX for Mac

7-Zip/PeaZip for Linux
```

The code bundle for the book is also hosted on GitHub at https:/​/​github.​com/PacktPublishing/​Test-​Driven-​Java-​Development-​Second-​Edition. In case there's an update to the code, it will be updated on the existing GitHub repository.

We also have other code bundles from our rich catalog of books and videos available at https:/​/​github.​com/​PacktPublishing/​. Check them out!

2『

[PacktPublishing/Test-Driven-Java-Development-Second-Edition: Test-Driven Java Development – Second Edition, published by Packt](https://github.com/PacktPublishing/Test-Driven-Java-Development-Second-Edition)

已经 clone 原书代码作为本书的附件。（2021-04-24）

又挖到宝藏了，Packt 出版社的所有书籍源码仓库：[Packt](https://github.com/PacktPublishing/)。做一张主题卡片。—— 已完成

』

### 05. Download the color images

We also provide a PDF file that has color images of the screenshots/diagrams used in this book. You can download it here: https:/​/​www.​packtpub.​com/​sites/​default/​files/downloads/​TestDrivenJavaDevelopmentSecondEdition_​ColorImages.​pdf.
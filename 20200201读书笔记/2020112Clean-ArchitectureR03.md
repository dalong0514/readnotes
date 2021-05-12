## 记忆时间

## 目录

0701 SRP: The Single Responsibility Principle

0801 OCP: The Open-Closed Principle

0901 LSP: The Liskov Substitution Principle

1001 ISP: The Interface Segregation Principle

1101 DIP: The Dependency Inversion Principle

## Part III. Design Principles

Good software systems begin with clean code. On the one hand, if the bricks aren't well made, the architecture of the building doesn't matter much. On the other hand, you can make a substantial mess with well-made bricks. This is where the SOLID principles come in.

The SOLID principles tell us how to arrange our functions and data structures into classes, and how those classes should be interconnected. The use of the word「class」does not imply that these principles are applicable only to object-oriented software. A class is simply a coupled grouping of functions and data. Every software system has such groupings, whether they are called classes or not. The SOLID principles apply to those groupings.

The goal of the principles is the creation of mid-level software structures that: 1) Tolerate change, 2) Are easy to understand, and 3) Are the basis of components that can be used in many software systems.

The term「mid-level」refers to the fact that these principles are applied by programmers working at the module level. They are applied just above the level of the code and help to define the kinds of software structures used within modules and components.

Just as it is possible to create a substantial mess with well-made bricks, so it is also possible to create a system-wide mess with well-designed mid-level components. For this reason, once we have covered the SOLID principles, we will move on to their counterparts in the component world, and then to the principles of high-level architecture.

The history of the SOLID principles is long. I began to assemble them in the late 1980s while debating software design principles with others on USENET (an early kind of Facebook). Over the years, the principles have shifted and changed. Some were deleted. Others were merged. Still others were added. The final grouping stabilized in the early 2000s, although I presented them in a different order.

In 2004 or thereabouts, Michael Feathers sent me an email saying that if I rearranged the principles, their first words would spell the word SOLID — and thus the SOLID principles were born. The chapters that follow describe each principle more thoroughly. Here is the executive summary:

SRP: The Single Responsibility Principle. An active corollary to Conway's law: The best structure for a software system is heavily influenced by the social structure of the organization that uses it so that each software module has one, and only one, reason to change.

OCP: The Open-Closed Principle. Bertrand Meyer made this principle famous in the 1980s. The gist is that for software systems to be easy to change, they must be designed to allow the behavior of those systems to be changed by adding new code, rather than changing existing code.

LSP: The Liskov Substitution Principle. Barbara Liskov's famous definition of subtypes, from 1988. In short, this principle says that to build software systems from interchangeable parts, those parts must adhere to a contract that allows those parts to be substi-tuted one for another.

ISP: The Interface Segregation Principle. This principle advises software designers to avoid depending on things that they don't use.

DIP: The Dependency Inversion Principle. The code that implements high-level policy should not depend on the code that implements low-level details. Rather, details should depend on policies.

These principles have been described in detail in many different publications [1] over the years. The chapters that follow will focus on the architectural implications of these principles instead of repeating those detailed discussions. If you are not already familiar with these principles, what follows is insufficient to understand them in detail and you would be well advised to study them in the footnoted documents.

1 For example, Agile Software Development, Principles, Patterns, and Practices, Robert C. Martin, Prentice Hall, 2002, [ArticleS.UncleBob.PrinciplesOfOod](http://www.butunclebob.com/ArticleS.UncleBob.PrinciplesOfOod), and [SOLID (面向对象设计) - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/SOLID_(%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E8%AE%BE%E8%AE%A1)) (or just google SOLID).

通常来说，要想构建一个好的软件系统，应该从写整洁的代码开始做起。毕竟，如果建筑所使用的砖头质量不佳，那么架构所能起到的作用也会很有限。反之亦然，如果建筑的架构设计不佳，那么其所用的砖头质量再好也没有用。这就是 SOLD 设计原则所要解决的问题。

SOLID 原则的主要作用就是告诉我们如何将数据和函数组织成为类，以及如何将这些类链接起来成为程序。请注意，这里虽然用到了「类」这个词，但是并不意味着我们将要讨论的这些设计原则仅仅适用于面向对象编程。这里的类仅仅代表了一种数据和函数的分组，每个软件系都会有自己的分类系统，不管它们各自是不是将其称为「类」，事实上都是 SOLID 原则的适用领域。

一般情况下，我们为软件构建中层结构的主要目标如下：1）使软件可容忍被改动。2）使软件更容易被理解。3）构建可在多个软件系统中复用的组件。

我们在这里之所以会使用「中层」这个词，是因为这些设计原则主要适用于那些进行模块级编程的程序员。SOLID 原则应该直接紧贴于具体的代码逻辑之上，这些原则是用来帮助我们定义软件架构中的组件和模块的。当然了，正如用好砖也会盖歪楼一样，采用设计良好的中层组件并不能保证系统的整体架构运作良好。正因为如此，我们在讲完 SOLID 原则之后，还会再继续针对组件的设计原则进行更进一步的讨论，将其推进到高级软件架构部分。

SOLID 原则的历史已经很悠久了，早在 20 世纪 80 年代末期，我在 USENET 新闻组（该新闻组在当时就相当于今天的 Facebook）上和其他人论软件设计理念的时候，该设计原则就已经开始逐渐成型了。随着时间的推移，其中有一些原则得到了修改，有一些则被抛弃了，还有一些被合并了，另外也增加了ー些。它们的最终形态是在 2000 年左右形成的，只不过当时采用的是另外一个展现顺序。2004 年前后，Michael Feathers 的一封电子邮件提醒我：如果重新排列这些设计原则，那么它们的首字母可以排列成 SOLID 这就是 SOLD 原则诞生的故事。

在这一部分中，我们会逐章地详细讨论每个设计原则，下面先来做一个简单摘要。

SRP：单一职责原则。该设计原则是基于康威定律（Conway's Law) 的一个推论 —— 一个软件系统的最佳结构高度依赖于开发这个系统的组织的内部结构。这样，每个软件模块都有且只有一个需要被改变的理由。

OCP：开闭原则。该设计原则是由 Bertrand Meyer 在 20 世纪 80 年代大力推广的，其核心要素是：如果软件系统想要更容易被改变，那么其设计就必须允许新增代码来修改系統行为，而非只能靠修改原来的代码。

LSP：里氏替换原则。该设计原则是 Barbara Liskov 在 1988 年提出的一个著名的子类型定义。简单来说，这项原则的意思是如果想用可替换的组件来构建软件系统，那么这些组件就必须遵守同一个约定，以便让这些组件可以相互替换。

ISP：接口隔离原则。这项设计原则主要告诚软件设计师应该在设计中避免不必要的依赖。

DIP：依赖反转原则。该设计原则指出高层策略性的代码不应该依赖实现底层细节的代码，怡相反，那些实现底层细节的代码应该依赖高层策略性的代码。

这些年来，这些设计原则在很多不同的出版物中都有过详细描述。在接下来的章节中，我们将会主要关注这些原则在软件架构上的意义，而不再重复其细节信息。如果你对这些原则并不是特别了解，那么我建议你先通过脚注中的文档熟悉一下它们，否则接下来的章节可能有点难以理解。

## 0701. SRP: The Single Responsibility Principle

### Conclusion

The Single Responsibility Principle is about functions and classes — but it reappears in a different form at two more levels. At the level of components, it becomes the Common Closure Principle. At the architectural level, it becomes the Axis of Change responsible for the creation of Architectural Boundaries. We'll be studying all of these ideas in the chapters to come.

单一职责原则主要讨论的是函数和类之间的关系 —— 但是它在两个讨论层面上会以不同的形式出现。在组件层面，我们可以将其称为共同闭包原则（Common Closure Principle），在软件架构层面，它则是用于奠定架构边界的变更轴心（Axis of Change）。我们在接下来的章节中会深入学习这些。

### 00

Of all the SOLID principles, the Single Responsibility Principle (SRP) might be the least well understood. That's likely because it has a particularly inappropriate name. It is too easy for programmers to hear the name and then assume that it means that every module should do just one thing.

Make no mistake, there is a principle like that. A function should do one, and only one, thing. We use that principle when we are refactoring large functions into smaller functions; we use it at the lowest levels. But it is not one of the SOLID principles — it is not the SRP.

Historically, the SRP has been described this way: 

A module should have one, and only one, reason to change.

Software systems are changed to satisfy users and stakeholders; those users and stakeholders are the「reason to change」that the principle is talking about. Indeed, we can rephrase the principle to say this:

A module should be responsible to one, and only one, user or stakeholder.

Unfortunately, the words「user」and「stakeholder」aren't really the right words to use here. There will likely be more than one user or stakeholder who wants the system changed in the same way. Instead, we're really referring to a group — one or more people who require that change. We'll refer to that group as an actor. Thus the final version of the SRP is:

A module should be responsible to one, and only one, actor.

Now, what do we mean by the word「module」? The simplest definition is just a source file. Most of the time that definition works fine. Some languages and development environments, though, don't use source files to contain their code. In those cases a module is just a cohesive set of functions and data structures.

2『 SRP 定义的演化，做一张任意卡片。』——已完成

That word「cohesive」implies the SRP. Cohesion is the force that binds together the code responsible to a single actor. Perhaps the best way to understand this principle is by looking at the symptoms of violating it.

SRP 是 SOLID 五大设计原则中最容易被误解的一个。也许是名字的原因，很多程序员根据 SRP 这个名字想当然地认为这个原则就是指：每个模块都应该只做一件事。没错，后者的确也是一个设计原则，即确保一个函数只完成一个功能。我们在将大型函数重构成小函数时经常会用到这个原则，但这只是一个面向底层实现细节的设计原则，并不是 SRP 的全部。在历史上，我们曾经这样描述 SRP 这一设计原则：任何一个软件模块都应该有且仅有一个被修改的原因。

在现实环境中，软件系统为了满足用户和所有者的要求，必然要经常做出这样那样的修改。而该系统的用户或者所有者就是该设计原则中所指的「被修改的原因」。所以，我们也可以这样描述 SRP：任何一个软件模块都应该只对一个用户（User）或系统利益相关者（Stakeholder）负责。

不过，这里的「用户」和「系统利益相关者」在用词上也并不完全准确，它们很有可能指的是一个或多个用户和利益相关者，只要这些人希望对系统进行的变更是相似的，就可以归为一类个或多个有共同需求的人。在这里，我们将其称为行为者（actor）。所以，对于 SRP 的最终描述就变成了：任何一个软件模块都应该只对某一类行为者负责。

那么，上文中提到的「软件模块」究竟又是在指什么呢？大部分情況下，其最简单的定义就是指一个源代码文件。然而，有些编程语言和编程环境并不是用源代码文件来存储程序的。在这些情況下，「软件模块」指的就是一组紧密相关的函数和数据结构。在这里，「相关」这个词实际上就隐含了 SRP 这一原则。代码与数据就是靠着与某一类行为者的相关性被组合在一起的。或许，理解这个设计原则最好的办法就是让大家来看一些反面案例。

### 7.1 Symptom 1: Accidental Duplication

My favorite example is the Employee class from a payroll application. It has three methods: calculatePay(), reportHours(), and save() (Figure 7.1).

Figure 7.1  The Employee class

This class violates the SRP because those three methods are responsible to three very different actors.

The calculatePay() method is specified by the accounting department, which reports to the CFO.

The reportHours() method is specified and used by the human resources department, which reports to the COO.

The save() method is specified by the database administrators (DBAs), who report to the CTO.

By putting the source code for these three methods into a single Employee class, the developers have coupled each of these actors to the others. This coupling can cause the actions of the CFO's team to affect something that the COO's team depends on.

For example, suppose that the calculatePay() function and the reportHours() function share a common algorithm for calculating non-overtime hours. Suppose also that the developers, who are careful not to duplicate code, put that algorithm into a function named regularHours() (Figure 7.2).

Figure 7.2  Shared algorithm

Now suppose that the CFO's team decides that the way non-overtime hours are calculated needs to be tweaked. In contrast, the COO's team in HR does not want that particular tweak because they use non-overtime hours for a different purpose.

A developer is tasked to make the change, and sees the convenient regularHours() function called by the calculatePay() method. Unfortunately, that developer does not notice that the function is also called by the reportHours() function. The developer makes the required change and carefully tests it. The CFO's team validates that the new function works as desired, and the system is deployed.

Of course, the COO's team doesn't know that this is happening. The HR personnel continue to use the reports generated by the reportHours() function — but now they contain incorrect numbers. Eventually the problem is discovered, and the COO is livid because the bad data has cost his budget millions of dollars.

We've all seen things like this happen. These problems occur because we put code that different actors depend on into close proximity. The SRP says to separate the code that different actors depend on.

反面案例 1：重复的假象

这是我最喜欢举的一个例子：某个工资管理程序中的 Employee 类有三个函数 calculatepay() 、reporthours() 和 save()（见图 7.1)。

如你所见，这个类的三个函数分别对应的是三类非常不同的行为者，违反了 SRP 设计原则。calculatepay() 函数是由财务部门制定的，他们负责向 CFO 汇报。reporthours() 函数是由人力资源部门制定并使用的，他们负责向 COO 汇报。save()函数是由 DBA 制定的，他们负责向 CTO 汇报。

这三个函数被放在同一个源代码文件，即同一个 Employees 类中，程序员这样做实际上就等于使三类行为者的行为耦合在了一起，这有可能会导致 CFO 团队的命令影响到 COO 团队所依赖的功能。例如，calculatePay() 函数和 reportHours() 函数使用同样的逻辑来计算正常工作时数。程序员为了避免重复编码，通常会将该算法单独实现为一个名为 regularHours() 的函数（见图 7.2）。

接下来，假设 CFO 团队需要修改正常工作时数的计算方法，而 COO 领的 HR 团队不需要这个修改，因为他们对数据的用法是不同的。

这时候，负责这项修改的程序员会注意到 calculatePay() 函数调用了 regularHours() 函数，但可能不会注意到该函数会同时被 reportHours() 调用。于是，该程序员就这样按照要求进行了修改，同时 CFO 团队的成员验证了新算法工作正常。这项修改最终被成功部署上线了。

但是，COO 团队显然完全不知道这些事情的发生，HR 仍然在使用 reportHours() 产生的报表，随后就会发现他们的数据出错了！最终这个问题让 COO 十分愤怒，因为这些错误的数据给公司造成了几百万美元的损失。与此类似的事情我们肯定多多少少都经历过。这类问题发生的根源就是因为我们将不同行为者所依赖的代码强凑到了一起。对此，SRP 强调这类代码一定要被分开。

### 7.2 Symptom 2: Merges

It's not hard to imagine that merges will be common in source files that contain many different methods. This situation is especially likely if those methods are responsible to different actors.

For example, suppose that the CTO's team of DBAs decides that there should be a simple schema change to the Employee table of the database. Suppose also that the COO's team of HR clerks decides that they need a change in the format of the hours report.

Two different developers, possibly from two different teams, check out the Employee class and begin to make changes. Unfortunately their changes collide. The result is a merge. I probably don't need to tell you that merges are risky affairs. Our tools are pretty good nowadays, but no tool can deal with every merge case. In the end, there is always risk.

In our example, the merge puts both the CTO and the COO at risk. It's not inconceivable that the CFO could be affected as well. There are many other symptoms that we could investigate, but they all involve multiple people changing the same source file for different reasons.

Once again, the way to avoid this problem is to separate code that supports different actors.

反面案例 2：代码合并

一个拥有很多函数的源代码文件必然会经历很多次代码合并，该文件中的这些函数分别服务不同行为者的情况就更常见了。

例如，CTO 团队的 DBA 決定要对 Employee 数据库表结构进行简单修改。与此同时，COO 团队的 HR 需要修改工作时数报表的格式。这样一来，就很可能出现两个来自不同团队的程序员分别对 Employee 类进行修改的情况。不出意外的话，他们各自的修改一定会互相冲突，这就必须要进行代码合并。在这个例子中，这次代码合并不仅有可能让 CTO 和 COO 要求的功能出错，甚至连 CFO 原本正常的功能也可能受到影响。

事实上，这样的案例还有很多，我们就不ーー列举了。它们的一个共同点是，多人为了不同的目的修改了同一份源代码，这很容易造成问题的产生。而避免这种问题产生的方法就是将服务不同行为者的代码进行切分。

### 7.3 Solutions

There are many different solutions to this problem. Each moves the functions into different classes.

Perhaps the most obvious way to solve the problem is to separate the data from the functions. The three classes share access to EmployeeData, which is a simple data structure with no methods (Figure 7.3). Each class holds only the source code necessary for its particular function. The three classes are not allowed to know about each other. Thus any accidental duplication is avoided.

Figure 7.3 The three classes do not know about each other

The downside of this solution is that the developers now have three classes that they have to instantiate and track. A common solution to this dilemma is to use the Facade pattern (Figure 7.4).

Figure 7.4 The Facade pattern

The EmployeeFacade contains very little code. It is responsible for instantiating and delegating to the classes with the functions. Some developers prefer to keep the most important business rules closer to the data. This can be done by keeping the most important method in the original Employee class and then using that class as a Facade for the lesser functions (Figure 7.5).

Figure 7.5 The most important method is kept in the original Employee class and used as a Facade for the lesser functions

You might object to these solutions on the basis that every class would contain just one function. This is hardly the case. The number of functions required to calculate pay, generate a report, or save the data is likely to be large in each case. Each of those classes would have many private methods in them.

Each of the classes that contain such a family of methods is a scope. Outside of that scope, no one knows that the private members of the family exist.

我们有很多不同的方法可以用来解決上面的问题，每一种方法都需要将相关的函数划分成不同的类。其中，最简单直接的办法是将数据与函数分离，设计三个类共同使用一个不包括函数的、十分简单的 Employeedata 类（见图 7.3），每个类只包含与之相关的函数代码，互相不可见，这样就不存在互相依赖的情况了。这种解決方案的坏处在于：程序员现在需要在程序里处理三个类。另一种解決办法是使用 Facade 设计模式（见图 7.4）。

这样一来，EmployeeFacade 类所需要的代码量就很少了，它仅仅包含了初始化和调用三个具体实现类的函数。当然，也有些程序员更倾向于把最重要的业务逻辑与数据放在一起，那么我们也可以选择将最重要的函数保留在 Employee 类中，同时用这个类来调用其他没那么重要的函数（见图 7.5）。

图 7.5：将最重要的函数保留在 Employee 类中，同时调用其他两个没那么重要的类

读者也许会反对上面这些解决方案，因为看上去这里的每个类中都只有ー个函数。事实上并非如此，因为无论是计算工资、生成报表还是保存数据都是一个很复杂的过程，每个类都可能包含了许多私有函数总而言之，上面的每一个类都分別容纳了一组作用于相同作用域的函数，而在该作用域之外，它们各自的私有函数是互相不可见的。

## 0801. OCP: The Open-Closed Principle

### Conclusion

The OCP is one of the driving forces behind the architecture of systems. The goal is to make the system easy to extend without incurring a high impact of change. This goal is accomplished by partitioning the system into components, and arranging those components into a dependency hierarchy that protects higher-level components from changes in lower-level components.

OCP 是我们进行系统架构设计的主导原则，其主要目标是让系易于扩展，同时限制其每次被修改所影响的范围。实现方式是通过将系統划分为一系列组件，并且将这些组件间的依赖关系按层次结构进行组织，使得高阶组件不会因低阶组件被修改而受到影响。

### 8.0

The Open-Closed Principle (OCP) was coined in 1988 by Bertrand Meyer. [1] 

It says: A software artifact should be open for extension but closed for modification.

In other words, the behavior of a software artifact ought to be extendible, without having to modify that artifact.

This, of course, is the most fundamental reason that we study software architecture. Clearly, if simple extensions to the requirements force massive changes to the software, then the architects of that software system have engaged in a spectacular failure.

Most students of software design recognize the OCP as a principle that guides them in the design of classes and modules. But the principle takes on even greater significance when we consider the level of architectural components.

A thought experiment will make this clear.

1 Bertrand Meyer. Object Oriented Software Construction, Prentice Hall, 1988, p. 23.

开闭原则（OCP）是 Bertrand Meyer 在 1988 年提出的，该设计原则认为设计良好的计算机软件应该易于扩展，同时抗拒修改。换句话说，一个设计良好的计算机系统应该在不需要修改的前提下就可以轻易被扩展。

其实这也是我们研究软件架构的根本目的。如果对原始需求的小小延伸就需要对原有的软件系统进行大幅修改，那么这个系统的架构设计显然是失败的。尽管大部分软件设计师都已经认可了 OCP 是设计类与模块时的重要原则，但是在软件架构层面，这项原则的意义则更为重大。下面，让我们用一个思想实验来做一些说明。

### 8.1 A Thought Experiment

Imagine, for a moment, that we have a system that displays a financial summary on a web page. The data on the page is scrollable, and negative numbers are rendered in red.

Now imagine that the stakeholders ask that this same information be turned into a report to be printed on a black-and-white printer. The report should be properly paginated, with appropriate page headers, page footers, and column labels. Negative numbers should be surrounded by parentheses.

Clearly, some new code must be written. But how much old code will have to change?

A good software architecture would reduce the amount of changed code to the barest minimum. Ideally, zero.

How? By properly separating the things that change for different reasons (the Single Responsibility Principle), and then organizing the dependencies between those things properly (the Dependency Inversion Principle).

By applying the SRP, we might come up with the data-flow view shown in Figure 8.1. Some analysis procedure inspects the financial data and produces reportable data, which is then formatted appropriately by the two reporter processes.

Figure 8.1  Applying the SRP

The essential insight here is that generating the report involves two separate responsibilities: the calculation of the reported data, and the presentation of that data into a web- and printer-friendly form.

Having made this separation, we need to organize the source code dependencies to ensure that changes to one of those responsibilities do not cause changes in the other. Also, the new organization should ensure that the behavior can be extended without undo modification.

We accomplish this by partitioning the processes into classes, and separating those classes into components, as shown by the double lines in the diagram in Figure 8.2. In this figure, the component at the upper left is the Controller. At the upper right, we have the Interactor. At the lower right, there is the Database. Finally, at the lower left, there are four components that represent the Presenters and the Views.

Figure 8.2  Partitioning the processes into classes and separating the classes into components

Classes marked with `<I> `are interfaces; those marked with `<DS>` are data structures. Open arrowheads are using relationships. Closed arrowheads are implements or inheritance relationships.

The first thing to notice is that all the dependencies are source code dependencies. An arrow pointing from class A to class B means that the source code of class A mentions the name of class B, but class B mentions nothing about class A. Thus, in Figure 8.2, FinancialDataMapper knows about FinancialDataGateway through an implements relationship, but FinancialGateway knows nothing at all about FinancialDataMapper.

The next thing to notice is that each double line is crossed in one direction only. This means that all component relationships are unidirectional, as shown in the component graph in Figure 8.3. These arrows point toward the components that we want to protect from change.

1『想要高层不受底层变动的影响，底层必须依赖于高层。高层是接口类，底层是实现类。举例：B 是高层，A 是底层。谁调用 A 谁依赖于 A。B 直接调用 A 的话，B 依赖于 A，A 的变动会影响到 B。但如果把 A 的实现抽象出一个接口 I，B 调用 I 接口，A 调用 I 接口实现 I，那么 A 依赖于 I 就相当于 A 依赖于 B，A 的变动不会影响到 B，这就实现了依赖倒置。记住：空心箭头指向谁，谁是高层；实心箭头指向谁，调用谁。（2021-05-12）』

Figure 8.3  The component relationships are unidirectional

Let me say that again: If component A should be protected from changes in component B, then component B should depend on component A.

We want to protect the Controller from changes in the Presenters. We want to protect the Presenters from changes in the Views. We want to protect the Interactor from changes in — well, anything.

The Interactor is in the position that best conforms to the OCP. Changes to the Database, or the Controller, or the Presenters, or the Views, will have no impact on the Interactor.

Why should the Interactor hold such a privileged position? Because it contains the business rules. The Interactor contains the highest-level policies of the application. All the other components are dealing with peripheral concerns. The Interactor deals with the central concern.

Even though the Controller is peripheral to the Interactor, it is nevertheless central to the Presenters and Views. And while the Presenters might be peripheral to the Controller, they are central to the Views.

Notice how this creates a hierarchy of protection based on the notion of「level.」Interactors are the highest-level concept, so they are the most protected. Views are among the lowest-level concepts, so they are the least protected. Presenters are higher level than Views, but lower level than the Controller or the Interactor.

This is how the OCP works at the architectural level. Architects separate functionality based on how, why, and when it changes, and then organize that separated functionality into a hierarchy of components. Higher-level components in that hierarchy are protected from the changes made to lower-level components.

思想实验

假设我们现在要设计一个在 Web 页面上展示财务数据的系统，页面上的数据要可以滚动显示，其中负值应显示为红色。

接下来，该系统的所有者又要求同样的数据需要形成一个报表，该报表要能用黑白打印机打印，并且其报表格式要得到合理分页，每页都要包含页头、页尾及栏目名。同时，负值应该以括号表示。显然，我们需要增加一些代码来完成这个要求。但在这里我们更关注的问题是，满足新的要求需要更改多少旧代码。一个好的软件架构设计师会努力将旧代码的修改需求量降至最小，甚至为 0。

但该如何实现这一点呢？我们可以先将满足不同需求的代码分组（即 SRP），然后再来调整这些分组之间的依赖关系（即 DIP）。

利用 SRP，我们可以按图 8.1 中所展示的方式来处理数据流。即先用一段分析程序处理原始的财务数据，以形成报表的数据结构，最后再用两个不同的报表生成器来产生报表。这里的核心就是将应用生成报表的过程拆成两个不同的操作。即先计算出报表数据，再生成具体的展示报表（分别以网页及纸质的形式展示）。

接下来，我们就该修改其源代码之间的依赖关系了。这样做的目的是保证其中ー个操作被修改之后不会影响到另外一个操作。同时，我们所构建的新的组织形式应该保证该程序后续在行为上的扩展都无须修改现有代码。

在具体实现上，我们会将整个程序进程划分成一系列的类，然后再将这些类分割成不同的组件。下面，我们用图 8.2 中的那些双线框来具体描述一下个实现。在这个图中，左上角的组件是 Controller，右上角是 Interactor，右下角是 Database，左下角则有四个组件分别用于代表不同的 Presenter 和 View。

在图 8.2 中，用 `<I>` 标记的类代表接口，用 `<DS>` 标记的则代表数据结构；开放箭头指代的是使用关系，闭合箭头则指代了实现与继承关系。

首先，我们在图 8.2 中看到的所有依赖关系都是其源代码中存在的依赖关系。这里，从类 A 指向类 B 的箭头意味着 A 的源代码中涉及了 B，但是 B 的源代码中并不涉及 A。因此在图 8.2 中，FinancialDataMapper 在实现接口时需要知道 FinancialDataGateway 的实现，而 FinancialGateway 则完全不必知道 FinancialDataMapper 的实现。

其次，这里很重要的一点是这些双线框的边界都是单向跨越的。也就是说，上图中所有组件之间的关系都是单向依赖的，如图 8.3 所示，图中的箭头都指向那些我们不想经常更改的组件。让我们再来复述一下这里的设计原则：如果 A 组件不想被 B 组件上发生的修改所影响，那么就应该让 B 组件依赖于 A 组件。

所以现在的情况是，我们不想让发生在 Presenter 上的修改影响到 Controller，也不想让发生在 View 上的修改影响到 Presenter。而最关键的是，我们不想让任何修改影响到 Interactor。其中，Interactor 组件是整个系统中最符合 OCP 的。发生在 Database、Controller、Presenter 甚至 View 上的修改都不会影响到 interactor。

为什么 Interactor 会被放在这么重要的位置上呢？因为它是该程序的业务遇辑所在之处，Interactor 中包含了其最高层次的应用策略。其他组件都只是负责处理周边的辅助逻辑，只有 Interactor 才是核心组件。虽然 Controllers 组件只是 Interactor 的附属品，但它却是 Presenter 和 View 所服务的核心。同样的，虽然 Presenters 组件是 Controller 的附属品，但它却是 View 所服务的核心。

另外需要注意的是，这里利用「层级」这个概念创造了一系列不同的保护层级。譬如，Interactor 是最高层的抽象，所以它被保护得最严密，而 Presenteretview 的层级高，但比 Controller 和 Interactor 的层级低。

以上就是我们在软件架构层次上对 OCP 这一设计原则的应用。软件架构师可以根据相关函数被修改的原因、修改的方式及修改的时间来对其进行分组隔离，并将这些互相隔离的函数分组整理成组件结构，使得高阶组件不会因低阶组件被修改而受到影响。

### 8.2 Directional Control

If you recoiled in horror from the class design shown earlier, look again. Much of the complexity in that diagram was intended to make sure that the dependencies between the components pointed in the correct direction.

For example, the FinancialDataGateway interface between the FinancialReportGenerator and the FinancialDataMapper exists to invert the dependency that would otherwise have pointed from the Interactor component to the Database component. The same is true of the FinancialReportPresenter interface, and the two View interfaces.

依赖方向的控制

如果刚刚的类设计把你吓着了，别害怕！你刚刚在图表中所看到的复杂度是我们想要对组件之间的依赖方向进行控制而产生的。

例如，FinancialReportGenerator 和 FinancialDataMapper 之间的 FinancialDataGateway 接口是为了反转 Interactor 与 Database 之间的依赖关系而产生的。同样的，FinancialReportPresenter 接口与两个 view 接口之间也类似于这种情况。

### 8.3 Information Hiding

The FinancialReportRequester interface serves a different purpose. It is there to protect the FinancialReportController from knowing too much about the internals of the Interactor. If that interface were not there, then the Controller would have transitive dependencies on the FinancialEntities.

Transitive dependencies are a violation of the general principle that software entities should not depend on things they don't directly use. We'll encounter that principle again when we talk about the Interface Segregation Principle and the Common Reuse Principle.

So, even though our first priority is to protect the Interactor from changes to the Controller, we also want to protect the Controller from changes to the Interactor by hiding the internals of the Interactor.

信息隐藏

当然，FinancialReportRequester 接口的作用则完全不同，它的作用是保护 FinancialReportController。不过度依赖于 Interactor 的内部细节。如果没有这个接口，则 Controller 将会传递性地依赖于 FinancialEntities。这种传递性依赖违反了「软件系统不应该依赖其不直接使用的组件」这一基本原则。之后，我们会在讨论接口隔离原则和共同复用原则的时候再次提到这一点。所以，虽然我们的首要目的是为了让 interactor。屏蔽掉发生在 Controller 上的修改，但也需要通过隐藏 Interactor 内部细节的方法来让其屏掉来自 Controller 的依赖。

## 0901. LSP: The Liskov Substitution Principle

### Conclusion

The LSP can, and should, be extended to the level of architecture. A simple violation of substitutability, can cause a system's architecture to be polluted with a significant amount of extra mechanisms.

LSP 可以且应该被应用于软件架构层面，因为一旦违背了可替换性，该系统架构就不得不为此增添大量复杂的应对机制。

### 9.0

In 1988, Barbara Liskov wrote the following as a way of defining subtypes.

What is wanted here is something like the following substitution property: If  for each object o1 of  type S there is an object o2 of  type T such that for all  programs P defined in terms of  T, the behavior of  P is unchanged when o1 is  substituted for o2 then S is a subtype of  T. [1]

To understand this idea, which is known as the Liskov Substitution Principle (LSP), let's look at some examples.

1 Barbara Liskov, Data Abstraction and Hierarchy, SIGPLAN Notices 23, 5 (May 1988).

2『已下载论文「2021039Data Abstraction and Hierarchy」存入 Zotero。（2021-05-12）』

1988 年，Barbara Liskov 在描述如何定义子类型时写下了这样一段话：

这里需要的是一种可替换性：如果对于每个类型是 S 的对象 o1 都存在一个类型为 T 的对象 o2，能使操作类型的程序 P 在用 o2 替换 o1 时行为保持不变，我们就可以将 S 称为 T 的子类型。

为了让读者理解这段话中所体现的设计理念，也就是里氏替换原则（LSP），我们可以来看几个例子。

### 9.1 Guiding the Use of Inheritance

Imagine that we have a class named License, as shown in Figure 9.1. This class has a method named calcFee(), which is called by the Billing application. There are two「subtypes」of License: PersonalLicense and BusinessLicense. They use different algorithms to calculate the license fee.

Figure 9.1  License, and its derivatives, conform to LSP

This design conforms to the LSP because the behavior of the Billing application does not depend, in any way, on which of the two subtypes it uses. Both of the subtypes are substitutable for the License type.

继承的使用指导

假设我们有一个 License 类，其结构如图 9.1 所示。该类中有一个名为 calcFee() 的方法，该方法将由 Billing 应用程序来调用。而 License 类有两个子类型：PersonalLicense 与 BusinessLicense，这两个类会用不同的算法来计算授权费用。上述设计是符合 LSP 原则的，因为 Billing 应用程序的行为并不依赖于其使用的任何一个衍生类。也就是说，这两个衍生类的对象都是可以用来替换 License 类对象的。

### 9.2 The Square/Rectangle Problem

The canonical example of a violation of the LSP is the famed (or infamous, depending on your perspective) square/rectangle problem (Figure 9.2).

Figure 9.2  The infamous square/rectangle problem

In this example, Square is not a proper subtype of Rectangle because the height and width of the Rectangle are independently mutable; in contrast, the height and width of the Square must change together. Since the User believes it is communicating with a Rectangle, it could easily get confused. The following code shows why:

```java
Rectangle r = …
r.setW(5);
r.setH(2);
assert(r.area() == 10);
```

If the … code produced a Square, then the assertion would fail.

The only way to defend against this kind of LSP violation is to add mechanisms to the User (such as an if statement) that detects whether the Rectangle is, in fact, a Square. Since the behavior of the User depends on the types it uses, those types are not substitutable.

1『第一次纯看译文没弄清楚，看了原文才算明白。如果 new 了一个长方体对象，因为传进去的长和宽不一样，断言是错的。（2021-05-12）』

正方形 / 长方形问题

正方形 / 长方形问题是一个著名（或者说臭名远扬）的违反 LSP 的设计案例（该问题的结构如图 9.2 所示）。在这个案例中，Square 类并不是 Rectangle 类的子类型，因为 Rectangle 类的高和宽可以分别修改，而 Square 类的高和宽则必须一同修改。由于 User 类始终认为自己在操作 Rectangle 类，因此会带来一些混淆。例如在下面的代码中：

很显然，如果上述代码在 ...... 处返回的是 Square 类，则最后的这个 assertion 是不会成立的。如果想要防范这种违反 LSP 的行为，唯一的办法就是在 User 类中增加用于区分 Rectangle 和 Square 的检测逻辑（例如增加 if 语句）。但这样一来，User 类的行为又将依赖于它所使用的类，这两个类就不能互相替换了。

### 9.3 LSP and Architecture

In the early years of the object-oriented revolution, we thought of the LSP as a way to guide the use of inheritance, as shown in the previous sections. However, over the years the LSP has morphed into a broader principle of software design that pertains to interfaces and implementations.

The interfaces in question can be of many forms. We might have a Java-style interface, implemented by several classes. Or we might have several Ruby classes that share the same method signatures. Or we might have a set of services that all respond to the same REST interface.

In all of these situations, and more, the LSP is applicable because there are users who depend on well-defined interfaces, and on the substitutability of the implementations of those interfaces.

The best way to understand the LSP from an architectural viewpoint is to look at what happens to the architecture of a system when the principle is violated.

LSP 与软件架构

在面向对象这场编程革命兴起的早期，我们的普遍认知正如上文所说，认为 LSP 只不过是指导如何使用继承关系的一种方法，然而随着时间的推移，LSP 逐渐演变成了一种更广泛的、指导接口与其实现方式的设计原则。

这里提到的接口可以有多种形式  ——  可以是 Java 风格的接口，具有多个实现类；也可以像 Ruby 样，几个类共用一样的方法签名，甚至可以是几个服务响应同一个 REST 接口。

LSP 适用于上述所有的应用场景，因为这些场景中的用户都依赖于一种接口，并且都期待实现该接口的类之间能具有可替换性。想要从软件架构的角度来理解 LSP 的意义，最好的办法还是来看几个反面案例。

### 9.4 Example LSP Violation

Assume that we are building an aggregator for many taxi dispatch services. Customers use our website to find the most appropriate taxi to use, regardless of taxi company. Once the customer makes a decision, our system dispatches the chosen taxi by using a restful service.

Now assume that the URI for the restful dispatch service is part of the information contained in the driver database. Once our system has chosen a driver appropriate for the customer, it gets that URI from the driver record and then uses it to dispatch the driver.

Suppose Driver Bob has a dispatch URI that looks like this:

```java
purplecab.com/driver/Bob
```

Our system will append the dispatch information onto this URI and send it with a PUT, as follows:

```java
purplecab.com/driver/Bob
    /pickupAddress/24 Maple St.
    /pickupTime/153
    /destination/ORD
```

Clearly, this means that all the dispatch services, for all the different companies, must conform to the same REST interface. They must treat the pickupAddress, pickupTime, and destination fields identically.

Now suppose the Acme taxi company hired some programmers who didn't read the spec very carefully. They abbreviated the destination field to just dest. Acme is the largest taxi company in our area, and Acme's CEO's ex-wife is our CEO's new wife, and … Well, you get the picture. What would happen to the architecture of our system?

Obviously, we would need to add a special case. The dispatch request for any Acme driver would have to be constructed using a different set of rules from all the other drivers.

The simplest way to accomplish this goal would be to add an if statement to the module that constructed the dispatch command:

```java
if (driver.getDispatchUri().startsWith("acme.com"))…
```

But, of course, no architect worth his or her salt would allow such a construction to exist in the system. Putting the word「acme」into the code itself creates an opportunity for all kinds of horrible and mysterious errors, not to mention security breaches.

For example, what if Acme became even more successful and bought the Purple Taxi company. What if the merged company maintained the separate brands and the separate websites, but unified all of the original companies' systems? Would we have to add another if statement for「purple」?

Our architect would have to insulate the system from bugs like this by creating some kind of dispatch command creation module that was driven by a configuration database keyed by the dispatch URI. The configuration data might look something like this:

| URI | Dispatch Format |
| --- | --- | --- |
| Acme.com | /pickupAddress/%s/pickupTime/%s/dest/%s |
| `*.*` | /pickupAddress/%s/pickupTime/%s/destination/%s |

And so our architect has had to add a significant and complex mechanism to deal with the fact that the interfaces of the restful services are not all substitutable.

违反 LSP 的案例

设我们现在正在构建一个提供出租车调度服务的系统。在该系统中，用户可以通过访问我们的网站，从多个出租车公司内寻找最适合自己的出租车。当用户选定车子时，该系统会通过调用 restful 服务接口来调度这辆车。接下来，我们再假设该 restful 调度服务接口的 URI 被存储在司机数据库中。一旦该系统选中了最合适的出租车司机，它就会从司机数据库的记录中读取相应的 URI 信息，并通过调用这个 URI 来调度汽车。也就是说，如果司机 Bob 的记录中包含如下调度 URI：

那么，我们的系统就会将调度信息附加在这个 URI 上，并发送这样一个 PUT 请求：

很显然，这意着所有参与该调度服务的公司都必须遵守同样的 REST 接口，它们必须用同样的方式处理 pickupAddress、pickupTime 和 destination 字段。

接下来，我们再假设 Acme 出租车公司现在招聘的程序员由于没有仔细阅读上述接口定义，结果将 destination 字段缩写成了 dest。而 Acme 又是本地最大的出租车公司，另外，Acme CEO 的前妻不巧还是我们 CEO 的新欢。懂的！这会对系统的架构造成什么影响呢？

显然，我们需要为系统增加一类特殊用例，以应对 Acme 司机的调度请求。而这必须要用另外一套规则来构建。

最简单的做法当然是增加一条 if 语句：

然而很明显，任何一个称职的软件架构师都不会允许这样一条语句出现在自己的系统中。因为直接将「acme」这样的字串写入代码会留下各种各样神奇又可怕的错误隐患，甚至会导致安全问题。比如，Acme 也许会变得更加成功，最终收购了 Purple 出租车公司。然后，它们在保留了各自名字的同时却统一了彼此的计算机系統。在这种情况下，系统中难道还要再增加一条「purple」的特例吗？

软件架构师应该创建一个调度请求创建组件，并让该组件使用一个配置数据库来保存 URI 组装格式，这样的方式可以保护系统不受外界因素变化的影响。例如其配置信息可以如下：

但这样一来，软件架构师就需要通过增加一个复杂的组件来应对并不完全能实现互相替换的 restful 服务接口。

## 1001. ISP: The Interface Segregation Principle

### Conclusion

The lesson here is that depending on something that carries baggage that you don't need can cause you troubles that you didn't expect. We'll explore this idea in more detail when we discuss the Common Reuse Principle in Chapter 13,「Component Cohesion.」

本章所讨论的设计原则告诉我们：任何层次的软件设计如果依赖了它并不需要的东西，就会带来意料之外的麻烦。我们将会在第 13 章「组件聚合」中讨论共同复用原则的时候再来深入探讨更多相关的细节。

### 10.0

The Interface Segregation Principle (ISP) derives its name from the diagram shown in Figure 10.1.

Figure 10.1  The Interface Segregation Principle

In the situation illustrated in Figure 10.1, there are several users who use the operations of the OPS class. Let's assume that User1 uses only op1, User2 uses only op2, and User3 uses only op3.

Now imagine that OPS is a class written in a language like Java. Clearly, in that case, the source code of User1 will inadvertently depend on op2 and op3, even though it doesn't call them. This dependence means that a change to the source code of op2 in OPS will force User1 to be recompiled and redeployed, even though nothing that it cared about has actually changed.

This problem can be resolved by segregating the operations into interfaces as shown in Figure 10.2.

Again, if we imagine that this is implemented in a statically typed language like Java, then the source code of User1 will depend on U1Ops, and op1, but will not depend on OPS. Thus a change to OPS that User1 does not care about will not cause User1 to be recompiled and redeployed.

Figure 10.2  Segregated operations

在图 10.1 所描绘的应用中，有多个用户需要操作 OPS 类。现在，我们假设这里的 User1 只需要使用 op1，User2 只需要使用 op2，User3 只需要使用 op3。在这种情况下，如果 OPS 类是用 Java 编程语言编写的，那么很明显，User1 虽然不需要调用 op2、op3，但在源代码层次上也与它们形成依赖关系。这种依赖意味着我们对 OPS 代码中 op2 所做的任何修改，即使不会影响到 User1 的功能，也会导致它需要被重新编译和部署。这个问题可以通过将不同的操作隔离成接口来解决，具体如图 10.2 所示。

同样，我们也假设这个例子是用 Java 这种静态类型语言来实现的，那么现在 User1 的源代码会依赖于 U1Ops 和 op1，但不会依赖于 OPS。这样一来，我们之后对 OPS 做的修改只要不影响到 User1 的功能，就不需要重新编译和部 User1 了。

### 10.1 ISP and Language

Clearly, the previously given description depends critically on language type. Statically typed languages like Java force programmers to create declarations that users must import, or use, or otherwise include. It is these included declarations in source code that create the source code dependencies that force recompilation and redeployment.

In dynamically typed languages like Ruby and Python, such declarations don't exist in source code. Instead, they are inferred at runtime. Thus there are no source code dependencies to force recompilation and redeployment. This is the primary reason that dynamically typed languages create systems that are more flexible and less tightly coupled than statically typed languages.

This fact could lead you to conclude that the ISP is a language issue, rather than an architecture issue.

ISP 与编程语言

很明显，上述例子很大程度上也依赖于我们所采用的编程语言。对于 Java 这样的静态类型语言来说，它们需要程序员显式地 import、use 或者 include 其实现功能所需要的源代码。而正是这些语句带来了源代码之间的依赖关系，这也就导致了某些模块需要被重新编译和重新部。

而对于 Ruby 和 Python 这样的动态类型语言来说，源代码中就不存在这样的声明，它们所用对象的类型会在运行时被推演出来，所以也就不存在强制重新编译和重新部署的必要性。这就是动态类型语言要比静态类型语言更灵活、耦合度更松的原因当然，如果仅仅就这样说的话，读者可能会误以为 ISP 只是一个与编程语言的选择紧密相关的设计原则，而非软件架构问题，这就错了。

### 10.2 ISP and Architecture

If you take a step back and look at the root motivations of the ISP, you can see a deeper concern lurking there. In general, it is harmful to depend on modules that contain more than you need. This is obviously true for source code dependencies that can force unnecessary recompilation and redeployment — but it is also true at a much higher, architectural level.

Consider, for example, an architect working on a system, S. He wants to include a certain framework, F, into the system. Now suppose that the authors of F have bound it to a particular database, D. So S depends on F. which depends on D (Figure 10.3).

Figure 10.3  A problematic architecture

Now suppose that D contains features that F does not use and, therefore, that S does not care about. Changes to those features within D may well force the redeployment of F and, therefore, the redeployment of S. Even worse, a failure of one of the features within D may cause failures in F and S.

ISP 与软件架构

回顾一下 ISP 最初的成因：在一般情況下，任何层次的软件设计如果依赖于不需要的东西，都会是有害的。从源代码层次来说，这样的依赖关系会导致不必要的重新编译和重新部署，对更高层次的软件架构设计来说，问题也是类似的。

例如，我们假设某位软件架构师在设计系统 S 时，想要在该系統中引入某个框架 F。这时候，假设框架 F 的作者又将其捆绑在一个特定的数据库 D 上，那么就形成了 S 依赖于 F，F 又依赖于 D 的关系（参见图 10.3）。在这种情下，如果 D 中包含了 F 不需要的功能，那么这些功能同样也会是 S 不需要的。而我们对 D 中这些功能的修改将会导致 F 需要被重新部署，后者又会导致 S 的重新部署。更糟糕的是，D 中一个无关功能的错误也可能会导致 F 和 S 运行出错。
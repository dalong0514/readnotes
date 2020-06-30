PART II Patterns

# 0201. What Are Design Patterns? Why Use Them?

Most problems we encounter as programmers have been handled time and again by others in our community. Design patterns can provide us with the means to mine that wisdom. Once a pattern becomes a common currency, it enriches our language, making it easy to share design ideas and their consequences. Design patterns simply distill common problems, define tested solutions, and describe likely outcomes. 

Many books and articles focus on the details of computer languages, such as the available functions, classes and methods, and so on. Pattern catalogs concentrate instead on how you can move on from these basics (the「what」) to an understanding of the problems and potential solutions in your projects (the「why」and「how」).

In this chapter, I introduce you to design patterns and look at some of the reasons for their popularity. This chapter will cover the following: 1) Pattern basics: What are design patterns? 2) Pattern structure: What are the key elements of a design pattern? 3) Pattern benefits: Why are patterns worth your time?

## 1.1 What Are Design Patterns?

In the world of software, a pattern is a tangible manifestation of an organization’s tribal memory. [A pattern is] a solution to a problem in a context.

—The Gang of Four, Design Patterns: Elements of Reusable Object-Oriented Software

—Grady Booch in Core J2EE Patterns

在软件世界中，每个开发机构就像一个部落，而模式就是对部落的某种共同记忆的一种有形表现。

As these quotations imply, a design pattern is a problem analyzed with good practice for its solution explained. Problems tend to recur, and as web programmers we must solve them time and time again. How should we handle an incoming request? How can we translate this data into instructions for our system? How should we acquire data? Present results? Over time, we answer these questions with a greater or lesser degree of elegance and evolve an informal set of techniques that we use and reuse in our projects. These techniques are patterns of design.

正如上述引语所暗示的，设计模式便是分析过的问题和问题解决方案所阐释的优秀实践。同样的问题总是不断出现，而我们作为 Web 程序员必须一次又ー次地解决它们。比如如何处理一个请求？如何将请求数据转换成系统对应的指令？应该如何获得数据？又如何显示结果？随着时间流逝和经验积累，我们会或优雅或困难地回答这些问题，并总结出一些非正式的、可在项目中重复使用的解决方案，而这些解决方案便是设计模式。

Design patterns inscribe and formalize these problems and solutions, making hard-won experience available to the wider programming community. Patterns are (or should be) essentially bottom-up and not top-down. They are rooted in practice and not theory. That is not to say that there isn’t a strong theoretical element to design patterns (as we will see in the next chapter), but patterns are based on real-world techniques used by real programmers. Renowned pattern-hatcher Martin Fowler says that he discovers patterns, he does not invent them. For this reason, many patterns will engender a sense of déjà vu as you recognize techniques you have used yourself.

设计模式记录并规范化了这些问题及解决方案，使更广泛的开发社区可获得这些来之不易的经验。模式在本质上讲是（或者说应该是）自下而上而非自上而下的。它们来源于实践而不是空洞的理论。这并非指设计模式没有强有力的理论基础（你会在下一章中看到这些理论基础），但是模式是以真正的程序员使用的真实世界的技术为基础的的。著名的模式专家 Martin Fowler 便说他是在发现模式，而不是发明模式。正是因为这样的原因，许多模式都会给你造成似曾相识（a sense of deja）的感觉。

A catalog of patterns is not a cookbook. Recipes can be followed slavishly; code can be copied and slotted into a project with minor changes. You do not always need even to understand all the code used in a recipe. Design patterns inscribe approaches to particular problems. The details of implementation may vary enormously according to the wider context. This context might include the programming language you are using, the nature of your application, the size of your project, and the specifics of the problem.

Let’s say, for example, that your project requires that you create a templating system. Given the name of a template file, you must parse it and build a tree of objects to represent the tags you encounter.

You start off with a default parser that scans the text for trigger tokens. When it finds a match, it hands off responsibility for the hunt to another parser object, which is specialized for reading the internals of tags. This continues examining template data until it either fails, finishes, or finds another trigger. If it finds a trigger, it, too, must hand off responsibility to a specialist—perhaps an argument parser. Collectively, these components form what is known as a recursive descent parser.

So these are your participants: a MainParser, a TagParser, and an ArgumentParser. You create a ParserFactory class to create and return these objects. Of course, nothing is easy, and you’re informed late in the game that you must support more than one syntax in your templates. Now, you need to create a parallel set of parsers according to syntax: an OtherTagParser, an OtherArgumentParser, and so on.

一个模式目录并不是一本食谱。食谱中的配方可以直接遵循；具体的程序代码也可以只做很小改动便被复制和安置在一个项目中。你也不必理解使用的所有代码。设计模式只负责记录特定问题的解决方法，对于大范围的上下文环境，具体的实现细节可能差别甚大，而这些上下文环境包括所使用的编程语言、应用程序的性质、项目的大小及问题的细节等。比方说，如果项目要求创建一个模板系统。根据所给的模板文件名，你必须解析它并建立一个对象树来代表所遇到的标签。

首先我们需要一个可以扫描文本的默认解析器，用于触发标记。当解析器找到一个匹配的标签时，它把找到的标签传递给另一个专门读内部标签的解析器。解析器继续解析模板数据，一直到解析失败或者完成，或者找到另一个触发标记。如果找到了一个触发标记，也必须传递它给另一个专门的处理器一一可能是一个参数解析器。这些部件共同组成一个递归下降解析器。

因此我们将需要这些解析器：Mainparser（核心解析器）、Tagparser（标签解析器）和 Argumentparser（参数解析器）。我们可以创建 Parserfactory 类来创建并返回这些对象。当然，现实中并没有这么简单的事情。你总是会在事后才被告知必须在模板里面支持多种语法。现在，只能根据语法来创建一组相应的解析器：OtherTagParser 和 OtherArgumentParser 等。

This is your problem: you need to generate a different set of objects according to the circumstance, and you want this to be more or less transparent to other components in the system. It just so happens that the Gang of Four define the following problem in their book’s summary page for the pattern Abstract Factory,「Provide an interface for creating families of related or dependent objects without specifying their concrete classes.」That fits nicely. It is the nature of our problem that determines and shapes our use of this pattern. There is nothing cut and paste about the solution either, as you can see in Chapter 9, in which I cover Abstract Factory.

The very act of naming a pattern is valuable; it contributes to the kind of common vocabulary that has arisen naturally over the years in older crafts and professions. Such shorthand greatly aids collaborative design as alternative approaches and their various consequences are weighed and tested. When you discuss your alternative parser families, for example, you can simply tell colleagues that the system creates each set of objects using the Abstract Factory pattern. They will nod sagely, either immediately enlightened or making a mental note to look it up later. The point is that this bundle of concepts and consequences has a handle, which makes for a useful shorthand, as I’ll illustrate later in this chapter.

这时你的问题便是：需要根据不同的情况创建一组不同的对象，同时要这组对象在系统里相对于其他组件来说或多或少是透明的。这恰恰就是《设计模式》一书的摘要中为抽象工厂（Abstract Factory）模式所定义的问题：为一个相关或相依赖的对象家族提供统一的创建接口，并无需指定实体类。这和我们的问题十分符合。正是问题的本质决定和形成了我们对该模式的使用。没有任何对解决方案的剪切和粘贴，而在第 9 章中，你可以看到对于抽象工厂模式的详细介绍。

恰当地为一个模式命名是很有意义的，因为模式命名象征着长期的专业过程中自然形成的公认的词汇表。这样的简写名称大大促进了软件设计的合作，并且它们的结论是经过量化及测试的。比如当你讨论系列解析器时，你可以简单地告诉同事，系统会使用抽象工厂模式来创建每组相应的解析器。你的同事会明智地点头同意，无论立刻觉悟还是先记下稍后再查阅该模式的相关资料。也就是说，模式命名象征着一系列概念，这对于程序员间的交流非常有好处，这在本章后面会详细介绍。

Finally, it is illegal, according to international law, to write about patterns without quoting Christopher Alexander, an architecture academic whose work heavily influenced the original object-oriented pattern advocates. He states in A Pattern Language (Oxford University Press, 1977):

Each pattern describes a problem which occurs over and over again in our environment, and then describes the core of the solution to that problem, in such a way that you can use this solution a million times over, without ever doing it the same way twice.

最后，根据国际惯例，介绍模式时应当提及 Christopher Alexander。他是一个建筑学家，极大地影响了初期的面向对象模式。他在 A Pattern Language（牛津大学出版社，1977) 一书中写道：每个模式都描述着一种在我们的环境中一遍又一遍地出现的问题，并描述了对该问题的核心解决方策。以此方式你可以使用该方案上百万次，而从不需要重复做同样的事情。

2『做一张金句卡片。』——已完成

It is significant that this definition (which applies to architectural problems and solutions) begins with the problem and its wider setting, and then proceeds to a solution. There has been some criticism in recent years that design patterns have been overused, especially by inexperienced programmers. This is often a sign that solutions have been applied where the problem and context are not present. Patterns are more than a particular organization of classes and objects, cooperating in a particular way. Patterns are structured to define the conditions in which solutions should be applied and to discuss the effects of the solution.

In this book, I will focus on a particularly influential strand in the patterns field: the form described in Design Patterns: Elements of Reusable Object-Oriented Software by the Gang of Four (Addison-Wesley Professional, 1995). It concentrates on patterns in object-oriented software development and inscribes some of the classic patterns that are present in most modern object-oriented projects.

The Gang of Four book is important because it inscribes key patterns, but also because it describes the design principles that inform and motivate these patterns. We will look at some of these principles in the next chapter.

这个始于问题及其广泛的环境继而进入解决方案的定义（被应用于建筑问题及解决方案）意义重大。这几年有一些对设计模式被滥用的指责，特别是被没经验的程序员所使用时。解决方案被应用于并不符合的问题及上下文中通常是滥用的信号。模式是类和对象的一种特殊组织形式是以定义解决方案的应用条件并讨论其效果的形式来组织的。本书中，我们将关注模式领域中特别具有影响力的一部分，即 Erich Gamma、Richard Helm、Ralph Johnson 和 John Vlissidek 所著的《设计模式——可复用面向对象软件的基础》（Addison- Wesley 1995) 一书中所描述的模式。该书集中介绍了面向对象软件开发中的模式，并记录了一些在大多数现代面向对象项目中出现的传统模式。《设计模式》一书非常重要，不仅因为它记录了关键模式，而且因为它也描述了形成和推动这些模式的设计原则。在下一章中我们便会看到其中的一些原则。

 ■ Note: the patterns described by the gang of Four and in this book are really instances of a pattern language. a pattern language is a catalog of problems and solutions organized together so that they complement one another, forming an interrelated whole. there are pattern languages for other problem spaces, such as visual design and project management (and architecture, of course). When i discuss design patterns here, i refer to problems and solutions in object-oriented software development.

《设计模式》及本书中所描述的模式是模式语言的真实实例，这些模式便是组织在一起的问题和解决方策的一个目录，以使模式可相互补充而形成一个相互关联的整体。当然也存在其他问题的模式语言，如视觉设计和项目管理（当然还有建筑）。但在此我所讨论的设计模式都是针对面向对象软件开发的问题和解决方案的。

## 1.2 A Design Pattern Overview

At heart, a design pattern consists of four parts: the name, the problem, the solution, and the consequences.

### 1.2.1 Name

Names matter. They enrich the language of programmers; a few short words can stand in for quite complex problems and solutions. They must balance brevity and description. The Gang of Four claims,「Finding good names has been one of the hardest parts of developing our catalog.」

Martin Fowler agrees:「Pattern names are crucial, because part of the purpose of patterns is to create a vocabulary that allows developers to communicate more effectively」(Patterns of Enterprise Application Architecture, Addison-Wesley Professional, 2002).

In Patterns of Enterprise Application Architecture, Martin Fowler refines a database access pattern I first encountered in Core J2EE Patterns by Deepak Alur, Dan Malks, and John Crupi (Prentice Hall, 2001). Fowler defines two patterns that describe specializations of the older pattern. The logic of his approach is clearly correct (one of the new patterns models domain objects, while the other models database tables, a distinction that was vague in the earlier work). Nonetheless, it was hard to train myself to think in terms of the new patterns. I had been using the name of the original in design sessions and documents for so long that it had become part of my language.

在《企业应用架构模式》一书中，Martin Fowler 改进了一个我曾在《J2EE 核心模式》（Deepak Alur、Dan Malks 和 John Crupia 著，Prentice Hall, 2003）中了解到的数据库访问模式。他定义了两个新模式来描述旧模式的特例。显然他的逻辑是正确的：新模式之一，对领域对象（domain object）进行了建模；另一个新模式对数据库表进行了建模。这区分了之前模式中含糊不清的地方。但最初我很不习惯他所采用的新术语，因为我使用旧的命名方式已经很长时间了，以至于旧的命名已经成为我的语言中的一部分。

### 1.2.2 The Problem

No matter how elegant the solution (and some are very elegant indeed), the problem and its context are the grounds of a pattern. Recognizing a problem is harder than applying any one of the solutions in a pattern catalog. This is one reason that some pattern solutions can be misapplied or overused.

Patterns describe a problem space with great care. The problem is described in brief and then contextualized, often with a typical example and one or more diagrams. It is broken down into its specifics, its various manifestations. Any warning signs that might help in identifying the problem are described.

无论解决方案如何优雅（有些的确非常优雅），问题及问题发生的环境都是一个模式的基础。找出问题比使用模式目录中的解决方案更难。这正是某些模式的解决方案被误用或过度使用的原因之一。模式会小心谨慎地描述问题的空间（问题发生的条件和环境）。问题会被置于环境中简明扼要地描述，通常还会带有典型的范例及一个或多个图表。问题会被分解为不同细节和各种表现。同时任何可以帮助发现问题的警告标志都会在模式中被描述。

### 1.2.3 The Solution

The solution is summarized initially in conjunction with the problem. It is also described in detail, often using UML class and interaction diagrams. The pattern usually includes a code example.

Although code may be presented, the solution is never cut-and-paste. The pattern describes an approach to a problem. There may be hundreds of nuances in its implementation. Think about instructions for sowing a food crop. If you simply follow a set of steps blindly, you are likely to go hungry come harvest time. More useful would be a pattern-based approach that covers the various conditions that may apply. The basic solution to the problem (making your crop grow) will always be the same (prepare soil, plant seeds, irrigate, harvest crop), but the actual steps you take will depend on all sorts of factors, such as your soil type, your location, the orientation of your land, local pests, and so on.

Martin Fowler refers to solutions in patterns as「half-baked.」That is, the coder must take away the concept and finish it for himself.

解决方案最初是和问题放在一起的，并常用 UML 类图和交互图更详细地进行描述。而模式通常也包含一个代码范例。尽管代码也许是现成的，但解决方案从来不是简单的剪切及粘贴。模式描述了一个问题的解决方法，但在实现时可能会有上百种细微的差别。这就像农作物播种的操作，如果你简单地盲目遵循书本上的步骤，那么在收获季节很可能会挨饿。以模式为基础，但又能针对各种情况随机应变的方法会更实用。虽然问题的基本解决方案（使你的庄稼成长）总是相同的（播种、灌溉、收割），但是实际采用的步骤依赖于各种因素，如土壤类别、地理位置、土地的方位和当地的害虫等。于是 Martin Fowler 把模式中的解决方案称为「半成品」。换句话说，编码人员必须理解概念并自己来完成具体的实现。

### 1.2.4 Consequences

Every design decision you make will have wider consequences. This should include the satisfactory resolution of the problem in question, of course. A solution, once deployed, may be ideally suited to work with other patterns. There may also be dangers to watch for.

在设计代码的时候，你所做的每一个决定都会带来不同的结果。当然我们总是希望能得到令人满意的针对问题的解决方案。解决方案一旦被部署，理想情况下它也许会非常适合与其他模式一同工作，但也要留心是否会带来风险。

## 1.3 The Gang of Four Format

As I write, I have five pattern catalogs on the desk in front of me. A quick look at the patterns in each confirms that none of them use the same structure. Some are formal; some are fine-grained, with many subsections; and others are discursive.

There are a number of well-defined pattern structures, including the original form developed by Christopher Alexander (the Alexandrian form), and the narrative approach favored by the Portland Pattern Repository (the Portland form). Because the Gang of Four book is so influential, and because we will cover many of the patterns they describe, let’s examine a few of the sections they include in their patterns:

1. Intent: A brief statement of the pattern’s purpose. You should be able to see the point of the pattern at a glance.

2. Motivation: The problem described, often in terms of a typical situation. The anecdotal approach can help make the pattern easy to grasp.

3. Applicability: An examination of the different situations in which you might apply the pattern. While the motivation describes a typical problem, this section defines specific situations and weighs the merits of the solution in the context of each.

4. Structure/Interaction: These sections may contain UML class and interaction diagrams describing the relationships among classes and objects in the solution.

5. Implementation: This section looks at the details of the solution. It examines any issues that may come up when applying the technique and provides tips for deployment.

6. Sample Code: I always skip ahead to this section. I find that a simple code example often provides a way into a pattern. The example is often chopped down to the basics in order to lay the solution bare. It could be in any object-oriented language. Of course, in this book, it will always be PHP.

7. Known Uses: These describe real systems in which the pattern (problem, context, and solution) occurs. Some people say that for a pattern to be genuine, it must be found in at least three publicly available contexts. This is sometimes called the「rule of three.」

8. Related Patterns: Some patterns imply others. In applying one solution, you can create the context in which another becomes useful. This section examines these synergies. It may also discuss patterns that have similarities to the problem or the solution, as well as any antecedents (i.e., patterns defined elsewhere on which the current pattern builds).

编写本书时，在我桌上有 5 份模式目录。看一下每个目录的模式，便可发现每一个都使用不样的结构：其中一些比较正式；一些比较细致，有着许多的子分类；还有一些则比较松散。这些目录中有一些定义良好的模式结构，其中包括由 Christopher Alexander 原创的格式（Alexandrian 格式）和 Portland 模式库所钟爱的叙述性格式（Portland 格式）。不过因为《设计模式》书极具影响力，而且我们也会介绍该书所描述的很多模式，所以先研究一下该书所采用的模式结构。其主要组成部分如下所示。

1、意图：模式目的的简要概括。你应该一眼就能看出模式的要点。

2、动机；需要被解决的问题，通常根据一个典型的情况。叙述性的方式有助于使模式更容易被领会。

3、适用性：检验不同情况下你是否可以应用某模式。动机描述了一个典型问题，而适用性定义了特殊的情况，并衡量该解决方案在每种情况下的价值。

4、结构/交互：可能包含 UML 类图和交互图，用于描述解决方案中类和对象之间的关系。

5、实现：着眼于解决方案的细节，介绍了应用解决方案时可能发生的问题，并提供了部署的技巧。

6、示例代码：我总是先跳到这一部分。我发现简单的代码范例是理解模式的捷径。范例通常都会被简化以突出解决方案的核心内容。示例代码可以用任何一种面向对象语言编写，当然本书中使用的是 PHP。

7、已知应用：使用该模式（问题、上下文及解决方案）的真实系统。有些人会说一个模式要变得真实，它就必须出现在至少 3 个公开存在的真实系统中。这有时会被称为「三法则」（rule of three，意思是解决某个特定问题所采取的设计，一次出现是偶然现象，两次是巧合，3 次出现オ可称为一个模式）。

8、相关模式：一些模式意味着其他模式也要被采用。在使用某个设计模式时，可以创造出另一个模式适用的条件。这部分内容研究了可能存在的模式间的合作，也可能会讨论那些问题或解决方案中具有相似点的模式及任何需要预先使用的模式（当前模式可能以其他模式为基础）。

## 1.4 Why Use Design Patterns?

So what benefits can patterns bring? Given that a pattern is a problem defined and a solution described, the answer should be obvious. Patterns can help you to solve common problems. There is more to patterns, of course.

### 1.4.1 A Design Pattern Defines a Problem

How many times have you reached a stage in a project and found that there is no going forward? Chances are you must backtrack some way before starting out again. By defining common problems, patterns can help you to improve your design. Sometimes, the first step to a solution is recognizing that you have a problem.

有多少次在项目到了某个阶段时你发现无法继续？这时你很可能必须以某种方式返回而不是继续尝试前进。通过定义共性问题，模式能帮助你改进设计。有时找到解决方案的第一步便是认清你面对的问题。

### 1.4.2 A Design Pattern Defines a Solution

Having defined and recognized the problem (and made certain that it is the right problem), a pattern gives you access to a solution, together with an analysis of the consequences of its use. Although a pattern does not absolve you of the responsibility to consider the implications of a design decision, you can at least be certain that you are using a tried-and-tested technique.

在定义和识别当前存在的问题后，模式给你提供了解决方案及应用该方案所得结果的分析。尽管模式并不能代替你来作出决策，但至少能确认你使用的是一个可靠并经过测试的技术。

### 1.4.3 Design Patterns Are Language Independent

Patterns define objects and solutions in object-oriented terms. This means that many patterns apply equally in more than one language. When I first started using patterns, I read code examples in C++ and Smalltalk, and then deployed my solutions in Java. Others transfer with modifications to the pattern’s applicability or consequences, but remain valid. Either way, patterns can help you as you move between languages. Equally, an application that is built on good object-oriented design principles can be relatively easy to port between languages (although there are always issues that must be addressed).

模式以面向对象的方式来定义对象和解决方案。这意味着大多数模式可被直接应用于多种编程语言中。例如我第一次使用模式时阅读的是 C++和 Smalltalk 的代码范例，却在 Java 环境中部署我的解决方案。另一些模式针对不同语言可能有不同的适用性或效果，但总是可行的。无论是哪种情况，模式总可以在不同语言中给你帮助。同时，一个建立于优秀的面向对象设计原则之上的应用能被相对简单地在不同语言中移植（尽管总有些问题需要处理）。

### 1.4.4 Patterns Define a Vocabulary

By providing developers with names for techniques, patterns make communication richer. Imagine a design meeting. I have already described my Abstract Factory solution, and now I need to describe my strategy for managing the data the system compiles. I describe my plans to Bob:

Me: I’m thinking of using a Composite.

Bob: I don’t think you’ve thought that through.

Okay, Bob didn’t agree with me. He never does. But he knew what I was talking about, and therefore why my idea sucked. Let’s play that scene through again without a design vocabulary.

Me: I intend to use a tree of objects that share the same type. The type’s interface will provide methods for adding child objects of its own type. In this way, we can build up complex combinations of implementing objects at runtime.

Bob: Huh?

Patterns, or the techniques they describe, tend to interoperate. The Composite pattern lends itself to collaboration with the Visitor pattern, for example:

Me: And then we can use Visitors to summarize the data.

Bob: You’re missing the point.

Ignore Bob. I won’t describe the tortuous nonpattern version of this; I will cover Composite in Chapter 10 and Visitor in Chapter 11.

The point is that, without a pattern language, we would still use these techniques. They precede their naming and organization. If patterns did not exist, they would evolve on their own, anyway. Any tool that is used sufficiently will eventually acquire a name.

### 1.4.5 Patterns Are Tried and Tested

So if patterns document good practice, is naming the only truly original thing about pattern catalogs? In some senses, that would seem to be true. Patterns represent best practice in an object-oriented context. To some highly experienced programmers, this may seem an exercise in repackaging the obvious. To the rest of us, patterns provide access to problems and solutions we would otherwise have to discover the hard way.Patterns make design accessible. As pattern catalogs emerge for more and more specializations, even the highly experienced can find benefits as they move into new aspects of their fields. A GUI programmer can gain fast access to common problems and solutions in enterprise programming, for example. A web programmer can quickly chart strategies for avoiding the pitfalls that lurk in tablet and smart phone projects.

如果模式验证了高质量的实践，那么名称是否是模式目录仅有的真正原创的东西？从某种意义上说，好像是这样的。在面向对象的环境中，模式代表着最佳实践。对于一些经验非常丰富的程序员来说，这就像是再包装明显的最佳实践。对于我们而言，模式提供了发现问题和解决方案的途径，否则我们将不得不非常辛苦地去发掘。模式使我们更容易得到好的设计方案。当模式目录变得越来越专业化，即使经验丰富的程序员也会在进入新领域的时候从中受益。例如，图形用户界面程序员可以快速理解企业级开发中的常见问题和解决方案。Web 程序员能快速制定策略来避免 PDA 和智能手机项目的缺陷。

### 1.4.6 Patterns Are Designed for Collaboration

By their nature, patterns should be generative and composable. This means that you should be able to apply one pattern and thereby create conditions suitable for the application of another. In other words, in using a pattern you may find other doors opened for you.

Pattern catalogs are usually designed with this kind of collaboration in mind, and the potential for pattern composition is always documented in the pattern itself.

模式生来就是「可生成的」（generative）和「可组成的」（composable）。这意味着你能应用一个模式，并因此创建适合应用另一个模式的条件。换句话说，在使用某个模式时你也许会发现另一扇门为你敞开了，你可以同时使用其他模式。模式目录通常会关注于这类协作，而模式本身也会介绍潜在的模式组合。

### 1.4.7 Design Patterns Promote Good Design

Design patterns demonstrate and apply principles of object-oriented design. So, a study of design patterns can yield more than a specific solution in a context. You can come away with a new perspective on the ways that objects and classes can be combined to achieve an objective.

设计模式示范并应用了面向对象设计原则。因此设计模式能在一个具体环境中产生多个特定的解决方案，而你可以从一个新的角度来学习如何组合对象和类来达到目标。

### 1.4.8 Design Patterns are Used By Popular Frameworks

This book is primarily about designing from the ground up. The patterns and principles covered here should enable you to design your own core frameworks with the needs of your projects in mind. However, laziness is also a virtue, and you may wish to work with (or you may inherit code that already uses) a framework such as Zend, Laravel, or Symfony. A good understanding of core design patterns will help you as you engage with these framework APIs.

## 1.5 PHP and Design Patterns

There is little in this chapter that is specific to PHP, which is characteristic of our topic to some extent. Many patterns apply to many object-capable languages with few or no implementation issues.

This is not always the case, of course. Some enterprise patterns work well in languages in which an application process continues to run between server requests. PHP does not work that way. A new script execution is kicked off for every request. This means that some patterns need to be treated with more care. Front Controller, for example, often requires some serious initialization time. This is fine when the initialization takes place once at application startup, but it’s more of an issue when it must take place for every request. That is not to say that we can’t use the pattern; I have deployed it with very good results in the past. We must simply ensure that we take account of PHP-related issues when we discuss the pattern. PHP forms the context for all the patterns that this book examines.

I referred to object-capable languages earlier in this section. You could code in PHP without defining any classes at all. With a few notable exceptions, however, objects and object-oriented design lie at the heart of most PHP projects and libraries.

本章中只有很小一部分是专门针对 PHP 的，从某种程度上说它算是本章的一点特色。许多模式都可以应用于各种具有面向对象能力的语言，实现起来通常不会有什么问题。当然，并不总是这样。一些企业模式只有在服务器请求对应一个应用进程的情况下オ能很好地工作。PHP 并不能以那样的方式工作。在 PHP 中，每一个请求都会开始一个新的脚本执行。这意味着要更谨慎地对待一些模式。例如，前端控制器（Front Controller）模式通常需要较多的初始化时间。如果初始化仅在应用启动时发生一次，那么还没问题，但如果每次请求都需要初始化，就会导致问题。这并不是说我们不能使用该模式，因为我在以前成功地使用过该模式。我们必须确保在讨论模式的时候考虑到 PHP 相关的问题，因为 PHP 正是本书研究所有模式时的具体环境。

在本节开头我提到过「具有对象能力的语言」。你根本不必定义任何类就可编写 PHP 代码（但如果使用 PEAR，你将会使用到一些对象）。虽然本书几乎完全关注于用面向对象解决方案来解决编程问题，但并不是在鼓吹面向对象。模式和 PHP 能被有效地混合，而且它们也形成了本书的核心，另外它们也能与许多传统方式很好地共存。对此 PEAR 便是一个极好的证明。PEAR 包优雅地使用了设计模式，它们在本质上趋于面向对象。但这个特性使它们在过程式项目中更加实用（而非不实用）。因为 PEAR 包是自我封装的，并将它们自身的复杂性都隐藏在十分干净的接口下，所以它们能被轻松地嵌入任何类型的项目中。

## Summary

In this chapter, I introduced design patterns, showed you their structure (using the Gang of Four form), and suggested some reasons why you might want to use design patterns in your scripts.

It is important to remember that design patterns are not snap-on solutions that can be combined like components to build a project. They are suggested approaches to common problems. These solutions embody some key design principles. It is these that we will examine in the next chapter.

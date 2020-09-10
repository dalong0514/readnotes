# 2020082PHP-Objects-Patterns-PracticeR02

## 记忆时间

## 0201. What Are Design Patterns? Why Use Them?

In this chapter, I introduced design patterns, showed you their structure (using the Gang of Four form), and suggested some reasons why you might want to use design patterns in your scripts. It is important to remember that design patterns are not snap-on solutions that can be combined like components to build a project. They are suggested approaches to common problems. These solutions embody some key design principles. It is these that we will examine in the next chapter.

要记住，设计模式并非像组件那样能被合并来构建系统的固定解决方案。它们是解决一般性问题的通用方法。这些解决方案体现了一些关键的设计原则。

Most problems we encounter as programmers have been handled time and again by others in our community. Design patterns can provide us with the means to mine that wisdom. Once a pattern becomes a common currency, it enriches our language, making it easy to share design ideas and their consequences. Design patterns simply distill common problems, define tested solutions, and describe likely outcomes. 

Many books and articles focus on the details of computer languages, such as the available functions, classes and methods, and so on. Pattern catalogs concentrate instead on how you can move on from these basics (the「what」) to an understanding of the problems and potential solutions in your projects (the「why」and「how」).

In this chapter, I introduce you to design patterns and look at some of the reasons for their popularity. This chapter will cover the following: 1) Pattern basics: What are design patterns? 2) Pattern structure: What are the key elements of a design pattern? 3) Pattern benefits: Why are patterns worth your time?

### 1.1 What Are Design Patterns?

In the world of software, a pattern is a tangible manifestation of an organization’s tribal memory. [A pattern is] a solution to a problem in a context.

—The Gang of Four, Design Patterns: Elements of Reusable Object-Oriented Software

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

The very act of naming a pattern is valuable, it contributes to the kind of common vocabulary that has arisen naturally over the years in older crafts and professions. Such shorthand greatly aids collaborative design as alternative approaches and their various consequences are weighed and tested. When you discuss your alternative parser families, for example, you can simply tell colleagues that the system creates each set of objects using the Abstract Factory pattern. They will nod sagely, either immediately enlightened or making a mental note to look it up later. The point is that this bundle of concepts and consequences has a handle, which makes for a useful shorthand, as I’ll illustrate later in this chapter.

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

 ■ Note: the patterns described by the gang of Four and in this book are really instances of a pattern language. a pattern language is a catalog of problems and solutions organized together so that they complement one another, forming an interrelated whole. there are pattern languages for other problem spaces, such as visual design and project management (and architecture, of course). When I discuss design patterns here, I refer to problems and solutions in object-oriented software development.

《设计模式》及本书中所描述的模式是模式语言的真实实例，这些模式便是组织在一起的问题和解决方策的一个目录，以使模式可相互补充而形成一个相互关联的整体。当然也存在其他问题的模式语言，如视觉设计和项目管理（当然还有建筑）。但在此我所讨论的设计模式都是针对面向对象软件开发的问题和解决方案的。

### 1.2 A Design Pattern Overview

At heart, a design pattern consists of four parts: the name, the problem, the solution, and the consequences.

#### 1.2.1 Name

Names matter. They enrich the language of programmers; a few short words can stand in for quite complex problems and solutions. They must balance brevity and description. The Gang of Four claims,「Finding good names has been one of the hardest parts of developing our catalog.」

Martin Fowler agrees:「Pattern names are crucial, because part of the purpose of patterns is to create a vocabulary that allows developers to communicate more effectively」(Patterns of Enterprise Application Architecture, Addison-Wesley Professional, 2002).

In Patterns of Enterprise Application Architecture, Martin Fowler refines a database access pattern I first encountered in Core J2EE Patterns by Deepak Alur, Dan Malks, and John Crupi (Prentice Hall, 2001). Fowler defines two patterns that describe specializations of the older pattern. The logic of his approach is clearly correct (one of the new patterns models domain objects, while the other models database tables, a distinction that was vague in the earlier work). Nonetheless, it was hard to train myself to think in terms of the new patterns. I had been using the name of the original in design sessions and documents for so long that it had become part of my language.

2『已下载书籍「2020105企业应用架构模式 | 2020105Patterns-of-Enterprise-Application-Architecture」、「2020151J2EE核心模式 | 2020151Core-J2EE-Patterns」。』

在《企业应用架构模式》一书中，Martin Fowler 改进了一个我曾在《J2EE 核心模式》（Deepak Alur、Dan Malks 和 John Crupia 著，Prentice Hall, 2003）中了解到的数据库访问模式。他定义了两个新模式来描述旧模式的特例。显然他的逻辑是正确的：新模式之一，对领域对象（domain object）进行了建模；另一个新模式对数据库表进行了建模。这区分了之前模式中含糊不清的地方。但最初我很不习惯他所采用的新术语，因为我使用旧的命名方式已经很长时间了，以至于旧的命名已经成为我的语言中的一部分。

#### 1.2.2 The Problem

No matter how elegant the solution (and some are very elegant indeed), the problem and its context are the grounds of a pattern. Recognizing a problem is harder than applying any one of the solutions in a pattern catalog. This is one reason that some pattern solutions can be misapplied or overused.

Patterns describe a problem space with great care. The problem is described in brief and then contextualized, often with a typical example and one or more diagrams. It is broken down into its specifics, its various manifestations. Any warning signs that might help in identifying the problem are described.

无论解决方案如何优雅（有些的确非常优雅），问题及问题发生的环境都是一个模式的基础。找出问题比使用模式目录中的解决方案更难。这正是某些模式的解决方案被误用或过度使用的原因之一。模式会小心谨慎地描述问题的空间（问题发生的条件和环境）。问题会被置于环境中简明扼要地描述，通常还会带有典型的范例及一个或多个图表。问题会被分解为不同细节和各种表现。同时任何可以帮助发现问题的警告标志都会在模式中被描述。

#### 1.2.3 The Solution

The solution is summarized initially in conjunction with the problem. It is also described in detail, often using UML class and interaction diagrams. The pattern usually includes a code example.

Although code may be presented, the solution is never cut-and-paste. The pattern describes an approach to a problem. There may be hundreds of nuances in its implementation. Think about instructions for sowing a food crop. If you simply follow a set of steps blindly, you are likely to go hungry come harvest time. More useful would be a pattern-based approach that covers the various conditions that may apply. The basic solution to the problem (making your crop grow) will always be the same (prepare soil, plant seeds, irrigate, harvest crop), but the actual steps you take will depend on all sorts of factors, such as your soil type, your location, the orientation of your land, local pests, and so on.

Martin Fowler refers to solutions in patterns as「half-baked.」That is, the coder must take away the concept and finish it for himself.

1『设计模式中的解决方案是个半成品，此观点做一张任意卡片。』——已完成

解决方案最初是和问题放在一起的，并常用 UML 类图和交互图更详细地进行描述。而模式通常也包含一个代码范例。尽管代码也许是现成的，但解决方案从来不是简单的剪切及粘贴。模式描述了一个问题的解决方法，但在实现时可能会有上百种细微的差别。这就像农作物播种的操作，如果你简单地盲目遵循书本上的步骤，那么在收获季节很可能会挨饿。以模式为基础，但又能针对各种情况随机应变的方法会更实用。虽然问题的基本解决方案（使你的庄稼成长）总是相同的（播种、灌溉、收割），但是实际采用的步骤依赖于各种因素，如土壤类别、地理位置、土地的方位和当地的害虫等。于是 Martin Fowler 把模式中的解决方案称为「半成品」。换句话说，编码人员必须理解概念并自己来完成具体的实现。

#### 1.2.4 Consequences

Every design decision you make will have wider consequences. This should include the satisfactory resolution of the problem in question, of course. A solution, once deployed, may be ideally suited to work with other patterns. There may also be dangers to watch for.

在设计代码的时候，你所做的每一个决定都会带来不同的结果。当然我们总是希望能得到令人满意的针对问题的解决方案。解决方案一旦被部署，理想情况下它也许会非常适合与其他模式一同工作，但也要留心是否会带来风险。

### 1.3 The Gang of Four Format

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

2『设计模式结构（pattern structures）做一张术语卡片。』——已完成

编写本书时，在我桌上有 5 份模式目录。看一下每个目录的模式，便可发现每一个都使用不一样的结构：其中一些比较正式；一些比较细致，有着许多的子分类；还有一些则比较松散。这些目录中有一些定义良好的模式结构，其中包括由 Christopher Alexander 原创的格式（Alexandrian 格式）和 Portland 模式库所钟爱的叙述性格式（Portland 格式）。不过因为《设计模式》书极具影响力，而且我们也会介绍该书所描述的很多模式，所以先研究一下该书所采用的模式结构。其主要组成部分如下所示。

1、意图：模式目的的简要概括。你应该一眼就能看出模式的要点。

2、动机；需要被解决的问题，通常根据一个典型的情况。叙述性的方式有助于使模式更容易被领会。

3、适用性：检验不同情况下你是否可以应用某模式。动机描述了一个典型问题，而适用性定义了特殊的情况，并衡量该解决方案在每种情况下的价值。

4、结构/交互：可能包含 UML 类图和交互图，用于描述解决方案中类和对象之间的关系。

5、实现：着眼于解决方案的细节，介绍了应用解决方案时可能发生的问题，并提供了部署的技巧。

6、示例代码：我总是先跳到这一部分。我发现简单的代码范例是理解模式的捷径。范例通常都会被简化以突出解决方案的核心内容。示例代码可以用任何一种面向对象语言编写，当然本书中使用的是 PHP。

7、已知应用：使用该模式（问题、上下文及解决方案）的真实系统。有些人会说一个模式要变得真实，它就必须出现在至少 3 个公开存在的真实系统中。这有时会被称为「三法则」（rule of three，意思是解决某个特定问题所采取的设计，一次出现是偶然现象，两次是巧合，3 次出现才可称为一个模式）。

8、相关模式：一些模式意味着其他模式也要被采用。在使用某个设计模式时，可以创造出另一个模式适用的条件。这部分内容研究了可能存在的模式间的合作，也可能会讨论那些问题或解决方案中具有相似点的模式及任何需要预先使用的模式（当前模式可能以其他模式为基础）。

### 1.4 Why Use Design Patterns?

So what benefits can patterns bring? Given that a pattern is a problem defined and a solution described, the answer should be obvious. Patterns can help you to solve common problems. There is more to patterns, of course.

#### 1.4.1 A Design Pattern Defines a Problem

How many times have you reached a stage in a project and found that there is no going forward? Chances are you must backtrack some way before starting out again. By defining common problems, patterns can help you to improve your design. Sometimes, the first step to a solution is recognizing that you have a problem.

1『有时卡住的时候，可以尝试先退一步，为了后续跨出的更大更远。这里的退一步是指认清所遇问题的本质。（2020-07-17）』

有多少次在项目到了某个阶段时你发现无法继续？这时你很可能必须以某种方式返回而不是继续尝试前进。通过定义共性问题，模式能帮助你改进设计。有时找到解决方案的第一步便是认清你面对的问题。

#### 1.4.2 A Design Pattern Defines a Solution

Having defined and recognized the problem (and made certain that it is the right problem), a pattern gives you access to a solution, together with an analysis of the consequences of its use. Although a pattern does not absolve you of the responsibility to consider the implications of a design decision, you can at least be certain that you are using a tried-and-tested technique.

在定义和识别当前存在的问题后，模式给你提供了解决方案及应用该方案所得结果的分析。尽管模式并不能代替你来作出决策，但至少能确认你使用的是一个可靠并经过测试的技术。

#### 1.4.3 Design Patterns Are Language Independent

Patterns define objects and solutions in object-oriented terms. This means that many patterns apply equally in more than one language. When I first started using patterns, I read code examples in C++ and Smalltalk, and then deployed my solutions in Java. Others transfer with modifications to the pattern’s applicability or consequences, but remain valid. Either way, patterns can help you as you move between languages. Equally, an application that is built on good object-oriented design principles can be relatively easy to port between languages (although there are always issues that must be addressed).

模式以面向对象的方式来定义对象和解决方案。这意味着大多数模式可被直接应用于多种编程语言中。例如我第一次使用模式时阅读的是 C++和 Smalltalk 的代码范例，却在 Java 环境中部署我的解决方案。另一些模式针对不同语言可能有不同的适用性或效果，但总是可行的。无论是哪种情况，模式总可以在不同语言中给你帮助。同时，一个建立于优秀的面向对象设计原则之上的应用能被相对简单地在不同语言中移植（尽管总有些问题需要处理）。

#### 1.4.4 Patterns Define a Vocabulary

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

1『确实，任何一个好的技术只要足够好，到最后肯定会有一个大家都知道的名字。』

#### 1.4.5 Patterns Are Tried and Tested

So if patterns document good practice, is naming the only truly original thing about pattern catalogs? In some senses, that would seem to be true. Patterns represent best practice in an object-oriented context. To some highly experienced programmers, this may seem an exercise in repackaging the obvious. To the rest of us, patterns provide access to problems and solutions we would otherwise have to discover the hard way. Patterns make design accessible. As pattern catalogs emerge for more and more specializations, even the highly experienced can find benefits as they move into new aspects of their fields. A GUI programmer can gain fast access to common problems and solutions in enterprise programming, for example. A web programmer can quickly chart strategies for avoiding the pitfalls that lurk in tablet and smart phone projects.

如果模式验证了高质量的实践，那么名称是否是模式目录仅有的真正原创的东西？从某种意义上说，好像是这样的。在面向对象的环境中，模式代表着最佳实践。对于一些经验非常丰富的程序员来说，这就像是再包装明显的最佳实践。对于我们而言，模式提供了发现问题和解决方案的途径，否则我们将不得不非常辛苦地去发掘。模式使我们更容易得到好的设计方案。当模式目录变得越来越专业化，即使经验丰富的程序员也会在进入新领域的时候从中受益。例如，图形用户界面程序员可以快速理解企业级开发中的常见问题和解决方案。Web 程序员能快速制定策略来避免 PDA 和智能手机项目的缺陷。

#### 1.4.6 Patterns Are Designed for Collaboration

By their nature, patterns should be generative and composable. This means that you should be able to apply one pattern and thereby create conditions suitable for the application of another. In other words, in using a pattern you may find other doors opened for you.

Pattern catalogs are usually designed with this kind of collaboration in mind, and the potential for pattern composition is always documented in the pattern itself.

模式生来就是「可生成的」（generative）和「可组成的」（composable）。这意味着你能应用一个模式，并因此创建适合应用另一个模式的条件。换句话说，在使用某个模式时你也许会发现另一扇门为你敞开了，你可以同时使用其他模式。模式目录通常会关注于这类协作，而模式本身也会介绍潜在的模式组合。

#### 1.4.7 Design Patterns Promote Good Design

Design patterns demonstrate and apply principles of object-oriented design. So, a study of design patterns can yield more than a specific solution in a context. You can come away with a new perspective on the ways that objects and classes can be combined to achieve an objective.

设计模式示范并应用了面向对象设计原则。因此设计模式能在一个具体环境中产生多个特定的解决方案，而你可以从一个新的角度来学习如何组合对象和类来达到目标。

#### 1.4.8 Design Patterns are Used By Popular Frameworks

This book is primarily about designing from the ground up. The patterns and principles covered here should enable you to design your own core frameworks with the needs of your projects in mind. However, laziness is also a virtue, and you may wish to work with (or you may inherit code that already uses) a framework such as Zend, Laravel, or Symfony. A good understanding of core design patterns will help you as you engage with these framework APIs.

### 1.5 PHP and Design Patterns

There is little in this chapter that is specific to PHP, which is characteristic of our topic to some extent. Many patterns apply to many object-capable languages with few or no implementation issues.

This is not always the case, of course. Some enterprise patterns work well in languages in which an application process continues to run between server requests. PHP does not work that way. A new script execution is kicked off for every request. This means that some patterns need to be treated with more care. Front Controller, for example, often requires some serious initialization time. This is fine when the initialization takes place once at application startup, but it’s more of an issue when it must take place for every request. That is not to say that we can’t use the pattern; I have deployed it with very good results in the past. We must simply ensure that we take account of PHP-related issues when we discuss the pattern. PHP forms the context for all the patterns that this book examines.

I referred to object-capable languages earlier in this section. You could code in PHP without defining any classes at all. With a few notable exceptions, however, objects and object-oriented design lie at the heart of most PHP projects and libraries.

本章中只有很小一部分是专门针对 PHP 的，从某种程度上说它算是本章的一点特色。许多模式都可以应用于各种具有面向对象能力的语言，实现起来通常不会有什么问题。当然，并不总是这样。一些企业模式只有在服务器请求对应一个应用进程的情况下才能很好地工作。PHP 并不能以那样的方式工作。在 PHP 中，每一个请求都会开始一个新的脚本执行。这意味着要更谨慎地对待一些模式。例如，前端控制器（Front Controller）模式通常需要较多的初始化时间。如果初始化仅在应用启动时发生一次，那么还没问题，但如果每次请求都需要初始化，就会导致问题。这并不是说我们不能使用该模式，因为我在以前成功地使用过该模式。我们必须确保在讨论模式的时候考虑到 PHP 相关的问题，因为 PHP 正是本书研究所有模式时的具体环境。

在本节开头我提到过「具有对象能力的语言」。你根本不必定义任何类就可编写 PHP 代码（但如果使用 PEAR，你将会使用到一些对象）。虽然本书几乎完全关注于用面向对象解决方案来解决编程问题，但并不是在鼓吹面向对象。模式和 PHP 能被有效地混合，而且它们也形成了本书的核心，另外它们也能与许多传统方式很好地共存。对此 PEAR 便是一个极好的证明。PEAR 包优雅地使用了设计模式，它们在本质上趋于面向对象。但这个特性使它们在过程式项目中更加实用（而非不实用）。因为 PEAR 包是自我封装的，并将它们自身的复杂性都隐藏在十分干净的接口下，所以它们能被轻松地嵌入任何类型的项目中。

## 0202. Some Pattern Principles

In this chapter, I examined some of the principles that underp in many design patterns. I looked at the use of composition to enable object combination and recombination at runtime, resulting in more flexible structures than would be available using inheritance alone. I also introduced you to decoupling, the practice of extracting software components from their context to make them more generally applicable. Finally, I reviewed the importance of interface as a means of decoupling clients from the details of implementation. In the coming chapters, I will examine some design patterns in detail.

学习了一些设计模式背后的设计原则，讨论了在运行时使用组合来合并及再合并对象（这比单独使用继承的灵活性更高），介绍了解耦并提取组件来使它们更具适用性，回顾了接口（它将客户端代码与实现的具体细节相分离）的重要性。

Although design patterns simply describe solutions to problems, they tend to emphasize solutions that promote reusability and flexibility. To achieve this, they manifest some key object-oriented design principles. We will encounter some of them in this chapter and in more detail throughout the rest of the book.

This chapter will cover the following topics: 1) Composition: How to use object aggregation to achieve greater flexibility than you could with inheritance alone. 2) Decoupling: How to reduce dependency between elements in a system. 3) The power of the interface: Patterns and polymorphism. 4) Pattern categories: The types of patterns that this book will cover.

### 2.1 The Pattern Revelation

I first started working with objects in the Java language. As you might expect, it took a while before some concepts clicked. When it did happen, though, it happened very fast, almost with the force of revelation. The elegance of inheritance and encapsulation bowled me over. I could sense that this was a different way of defining and building systems. I got polymorphism, working with a type and switching implementations at runtime. It seemed to me that this understanding would solve most of my design problems, and help me design beautiful and elegant systems.

1『又见多态，可以替代条件语句的功能。working with a type and switching implementations at runtime. 』

All the books on my desk at the time focused on language features and the very many APIs available to the Java programmer. Beyond a brief definition of polymorphism, there was little attempt to examine design strategies. Language features alone do not engender object-oriented design. Although my projects fulfilled their functional requirements, the kind of design that inheritance, encapsulation and polymorphism had seemed to offer continued to elude me.

My inheritance hierarchies grew wider and deeper as I attempted to build a new class for every eventuality. The structure of my systems made it hard to convey messages from one tier to another without giving intermediate classes too much awareness of their surroundings, binding them into the application and making them unusable in new contexts.

It wasn’t until I discovered Design Patterns: Elements of Reusable Object-Oriented Software (Addison-Wesley Professional, 1995), otherwise known as the Gang of Four book, that I realized I had missed an entire design dimension. By that time, I had already discovered some of the core patterns for myself, but others contributed to a new way of thinking.

I found that I had over-privileged inheritance in my designs, trying to build too much functionality into my classes. But where else can functionality go in an object-oriented system?

I found the answer in composition. Software components can be defined at runtime by combining objects in flexible relationships. The Gang of Four boiled this down into a principle:「favor composition over inheritance.」The patterns described ways in which objects could be combined at runtime to achieve a level of flexibility impossible in an inheritance tree alone.

1『金子知识啊，组合替代继承。』

因为我努力地为每一个可能性建造新类，所以我的继承层次体系逐渐变得更广、更深。而在这样的系统结构中，如果中间类对于环境没有足够的了解，如果没有将它们绑定到具体应用中，如果没有使它们只可用于当前局部环境中，那么在系统的层级中传递信息将会变得十分困难。直到发现《设计模式》一书，我才意识到原来我没有完全理解什么是设计。虽然那时我自己也已经发现了一些核心模式，但是书中介绍的其他模式则提供了一种全新的思维方式。

我在设计中给了继承过多的特权，总是试图为我的类构建太多的功能。在面向对象系统里还有别的地方可以放置这些功能吗？我在组合模式中找到了答案。通过以灵活的关系来组合对象，组件能在运行时被定义。《设计模式》将这提炼成了一个原则：组合优于继承（favor composition over inheritance）。在该模式中，运行时组合对象所达到的灵活性非常高，而这在单独的继承树中是不可能达到的。

### 2.2 Composition and Inheritance

Inheritance is a powerful way of designing for changing circumstances or contexts. It can limit flexibility, however, especially when classes take on multiple responsibilities.

1『所以才会有单一职责原则，当类有太多职责的时候，就可以考虑使用多台来拆解。』

#### 2.2.1 The Problem

As you know, child classes inherit the methods and properties of their parents (as long as they are protected or public elements). You can use this fact to design child classes that provide specialized functionality.

Figure 8-1 presents a simple example using the UML. The abstract Lesson class in Figure 8-1 models a lesson in a college. It defines abstract cost() and chargeType() methods. The diagram shows two implementing classes, FixedPriceLesson and TimedPriceLesson, which provide distinct charging mechanisms for lessons.

Using this inheritance scheme, I can switch between lesson implementations. Client code will know only that it is dealing with a Lesson object, so the details of cost will be transparent.

What happens, though, if I introduce a new set of specializations? I need to handle lectures and seminars. Because these organize enrollment and lesson notes in different ways, they require separate classes. Now I have two forces that operate upon my design. I need to handle pricing strategies, and separate lectures and seminars.

Figure 8-2 shows a hierarchy that is clearly faulty. I can no longer use the inheritance tree to manage my pricing mechanisms without duplicating great swathes of functionality. The pricing strategies are mirrored across the Lecture and Seminar class families.

At this stage, I might consider using conditional statements in the Lesson super class, removing those unfortunate duplications. Essentially, I remove the pricing logic from the inheritance tree altogether, moving it up into the super class. This is the reverse of the usual refactoring, where you replace a conditional with polymorphism. Here is an amended Lesson class:

利用这种继承模式，我们可以在课程的实现之间切换。而客户端代码只知道它是在处理一个 Lesson 对象，因此费用的细节就会变得透明。可是如果引入一组新的特殊性，又会怎样呢？比如我们需要处理演讲和研讨会。因为演讲和研讨会会以不同的方式注册登记和教授课程，所以它们会要求独立的类。因此在设计上现在会有两个分支。我们需要处理不同的定价策略并区分演讲和研讨会。

图 8-2 的体系明显是有缺陷的。在该体系中，我们不得不大量重复开发功能，否则无法使用继承树来管理价格机制。定价策略在 Lecture 和 Seminar 类的子类中被重复实现。我们可能要考虑在父类 Lesson 中使用条件语句来移除那些不适宜的重复。我们是把定价逻辑从继承树中一并移除并迁移到父类中，但这与我们通常用多态替换条件的重构思想背道而驰。下面是一个修改过的 Lesson 类。

```php
<?php
// declare(strict_types=1);  // 显式声明类型检查为严格模式

// listing 0801

abstract class Lesson {
    protected $duration;
    const FIXED= 1;
    const TIMED = 2;
    private $costtype;

    public function __construct(int $duration, int $costtype = 1) {
        $this->duration = $duration;
        $this->costtype = $costtype;
    }

    public function cost(): int {
        switch ($this->costtype) {
            case self::TIMED:
                return (5 * $this->duration);
                break;
            case self::FIXED:
                return 30;
                break;
            default:
                $this->costtype = self::FIXED;
                return 30;
        }
    }

    public function chargeType(): string {
        switch ($this->costtype) {
            case self::TIMED:
                return "hourly rate";
                break;
            case self::FIXED:
                return "fixed rate";
                break;
            default:
                $this->costtype = self::FIXED;
                return "fixed rate";
        }
    }

    // more lesson methods...
}

class Lecture extends Lesson {
    // Lecture-specific implementions...
}

class Seminar extends Lesson {
    // Seminar-specific implementions...
}
```

Here’s how I might work with these classes:

```php
$lecture = new Lecture(5, Lesson::FIXED);
echo "{$lecture->cost()}({$lecture->chargeType()})\n";

$seminar = new Seminar(3, Seminar::TIMED);
echo "{$seminar->cost()}({$seminar->chargeType()})\n";
```

And here’s the output:

```
30 (fixed rate)
15 (hourly rate)
```

You can see the new class diagram in Figure 8-3. Inheritance hierarchy improved by removing cost calculations from subclasses.

I have made the class structure much more manageable, but at a cost. Using conditionals in this code is a retrograde step. Usually, you would try to replace a conditional statement with polymorphism. Here, I have done the opposite. As you can see, this has forced me to duplicate the conditional statement across the chargeType() and cost() methods. I seem doomed to duplicate code.

#### 2.2.2 Using Composition

I can use the Strategy pattern to compose my way out of trouble. Strategy is used to move a set of algorithms into a separate type. By moving cost calculations, I can simplify the Lesson type. You can see this in Figure 8-4.

Figure 8-4.  Moving algorithms into a separate type

I create an abstract class, CostStrategy, which defines the abstract methods, cost() and chargeType(). The cost() method requires an instance of Lesson, which it will use to generate cost data. I provide two implementations for CostStrategy. Lesson objects work only with the CostStrategy type, not a specific implementation, so I can add new cost algorithms at any time by subclassing CostStrategy. This would require no changes at all to any Lesson classes.

Here’s a simplified version of the new Lesson class illustrated in Figure 8-4:

```php
abstract class CostStrategy {
    abstract public function cost(Lesson $lesson): int;
    abstract public function chargeType(): string;
}

abstract class Lesson {
    private $duration;
    private $CostStrategy;

    public function __construct(int $duration, CostStrategy $strategy) {
        $this->duration = $duration;
        $this->CostStrategy = $strategy;
    }

    public function cost(): int {
        return $this->CostStrategy->cost($this);
    }

    public function chargeType(): string {
        return $this->CostStrategy->chargeType();
    }

    public function getDuration(): int {
        return $this->duration;
    }

    // more lesson methods...
}

class Lecture extends Lesson {
    // Lecture-specific implementions...
}

class Seminar extends Lesson {
    // Seminar-specific implementions...
}
```

The Lesson class requires a CostStrategy object, which it stores as a property. The Lesson::cost() method simply invokes CostStrategy::cost(). Equally, Lesson::chargeType() invokes CostStrategy::chargeType(). This explicit invocation of another object’s method in order to fulfill a request is known as delegation. In my example, the CostStrategy object is the delegate of Lesson. The Lesson class washes its hands of responsibility for cost calculations and passes on the task to a CostStrategy implementation. Here, it is caught in the act of delegation:

2『又见委托（delegation）。委托做一张术语卡片。』——已完成

这种显式调用另一个对象的方法来执行一个请求的方式便是所谓的「委托」。在我们的示例中，Coststrategy 对象便是 Lesson 的委托方。Lesson 类不再负责计费，而是把计费任务传给 CostStrategy 类。下面的代码执行了委托操作：

```php
    public function cost(): int {
        return $this->CostStrategy->cost($this);
    }
```

Here is the CostStrategy class, together with its implementing children:

```php
abstract class CostStrategy {
    abstract public function cost(Lesson $lesson): int;
    abstract public function chargeType(): string;
}

class TimedCostStrategy extends CostStrategy {
    function cost(Lesson $lesson):int {
        return ($lesson->getDuration() * 5);
    }

    function chargeType(): string {
        return "hourly rate";
    }
}

class FixedCostStrategy extends CostStrategy {
    function cost(Lesson $lesson): int {
        return 30;
    }

    function chargeType(): string {
        return "fixed rate";
    }
}
```

I can change the way that any Lesson object calculates cost by passing it a different CostStrategy object at runtime. This approach then makes for highly flexible code. Rather than building functionality into my code structures statically, I can combine and recombine objects dynamically:

```php
$lessons[] = new Seminar(4, new TimedCostStrategy);
$lessons[] = new Lecture(4, new FixedCostStrategy);

foreach ($lessons as $lesson) {
    print "lesson charge {$lesson->cost()}. \n";
    echo "Charge type: {$lesson->chargeType()}\n";
}
```

```
lesson charge 20. Charge type: hourly rate
lesson charge 30. Charge type: fixed rate
```

1『通过组合 Lesson 和 CostStrategy 实现，在运行时根据不同的条件实施不同的行为，即条件语句实现的功能。』

As you can see, one effect of this structure is that I have focused the responsibilities of my classes. CostStrategy objects are responsible solely for calculating cost, and Lesson objects manage lesson data. So, composition can make your code more flexible because objects can be combined to handle tasks dynamically in many more ways than you can anticipate in an inheritance hierarchy alone. There can be a penalty with regard to readability, though. Because composition tends to result in more types, with relationships that aren’t fixed with the same predictability as they are in inheritance relationships, it can be slightly harder to digest the relationships in a system.

组合使用对象比使用继承体系更灵活，因为组合可以以多种方式动态地处理任务，不过这可能导致代码的可读性下降。因为组合需要更多的对象类型，而这些类型的关系并不像在继承关系中那般有固定的可预见性，所以要理解系统中类和对象的关系会有些困难。

### 2.3 Decoupling

You saw in Chapter 6 that it makes sense to build independent components. A system with highly interdependent classes can be hard to maintain. A change in one location can require a cascade of related changes across the system.

#### 2.3.1 The Problem

Reusability is one of the key objectives of object-oriented design, and tight coupling is its enemy. You can diagnose tight coupling when you see that a change to one component of a system necessitates many changes elsewhere. You should aspire to create independent components, so that you can make changes without a domino effect of unintended consequences. When you alter a component, the extent to which it is independent is related to the likelihood that your changes will cause other parts of your system to fail.

重用性是面向对象设计的主要目标之一，而紧耦合（tight-coupling）便是它的敌人。当我们看到系统中一个组件的改变迫使系统其他许多地方也发生改变的时候，就可诊断为紧耦合了。为了能安全地做变动，我们总是期望创建能够独立存在的组件。在修改组件时，其独立程度会决定你的修改对系统中其他组件的影响程度，系统的其他组件甚至有可能会因此失败。

2『紧耦合，做一张术语卡片。』——已完成

You saw an example of tight coupling in Figure 8-2. Because the cost logic was mirrored across the Lecture and Seminar types, a change to TimedPriceLecture would necessitate a parallel change to the same logic in TimedPriceSeminar. By updating one class and not the other, I would break my system—without any warning from the PHP engine. My first solution, using a conditional statement, produced a similar dependency between the cost() and chargeType() methods.

By applying the Strategy pattern, I distilled my cost algorithms into the CostStrategy type, locating them behind a common interface and implementing each only once.

在图 8-2 中，我们看到过紧耦合的例子。因为费用计算逻辑在 Lecture 和 Seminar 类型中都存在，所以对 TimedPriceLecture 的一个改变将会迫使在 TimedPriceSeminar 中同样逻辑的相应变化。如果仅改动一个类而不改动其他类的代码，系统将无法正常工作，而且没有来自 PHP 引擎的任何警告。而我们的第一个解决方案（使用条件语句）在 cost() 和 chargeType() 方法之间生成了一个类似的依赖关系。通过应用策略模式，我们将费用算法提取为 CostStrategy 类型，将算法放置在共同接口后并且每个算法只需实现一次。

Coupling of another sort can occur when many classes in a system are embedded explicitly into a platform or environment. Let’s say that you are building a system that works with a MySQL database, for example. You might use methods such as mysqli::query() to speak to the database server.

Should you be required to deploy the system on a server that does not support MySQL, you could convert your entire project to use SQLite. You would be forced to make changes throughout your code, though, and face the prospect of maintaining two parallel versions of your application.

不过当系统中许多类都显式嵌入到一个平台或环境中时，其他类型的耦合仍时有发生。比如建立了一个基于 MySQL 数据库的系统。你可能会用一些诸如 mysql\_connect() 和 mysql\_query() 的函数来与数据库服务器交互。如果现在你被要求在不支持 MySQL 的服务器上部署系统，比如要把整个项目都转换成使用 SQLite，那么你可能被迫要改变整个代码，并且面临维护应用程序的两个并行版本的状况。

1『中文是老版书籍，看来数据库的连接方法都改了哦。』

The problem here is not the system’s dependency on an external platform. Such a dependency is inevitable. You need to work with code that speaks to a database. The problem comes when such code is scattered throughout a project. Talking to databases is not the primary responsibility of most classes in a system, so the best strategy is to extract such code and group it together behind a common interface. In this way, you promote the independence of your classes. At the same time, by concentrating your gateway code in one place, you make it much easier to switch to a new platform without disturbing your wider system. This process, the hiding of implementation behind a clean interface, is known as encapsulation. The Doctrine database library solves this problem with the DBAL (database abstraction layer) project. This provides a single point of access for multiple databases.

1『如何隔离与数据库交互的代码，这个思路太赞了。这里有提到「Doctrine database library 」这个工具，就是为了解决这个问题的，记得去了解下。突然想到有本 python 的英文书里（那个作者写了好几本书），也有提到这种在程序和数据库之间抽象出来的中间层。』

这里的问题不在于系统对外部平台的依赖。这样的依赖是无法避免的。我们确实需要使用与数据库交互的代码。但当这样的代码散布在整个项目中时，问题就来了。与数据库交互不是系统中大部分类的首要责任，因此最好的策略就是提取这样的代码并将其组合在公共接口后。这可以使类之间相互独立。同时，通过在一个地方集中你的「入口」代码，就能更轻松地切换到一个新的平台而不会影响到系统中更大的部分。这个把具体实现隐藏在一个干净的接口后面的过程，正是大家所知道的「封装」。

The DriverManager class provides a static method called getConnection() that accepts a parameters array. According to the makeup of this array, it returns a particular implementation of an interface called Doctrine\DBAL\Driver. You can see the class structure in Figure 8-5.

The DBAL package, then, lets you decouple your application code from the specifics of your database platform. You should be able to run a single system with MySQL, SQLite, MSSQL, and others without changing a line of code (apart from your configuring parameters, of course).

#### 2.3.2 Loosening Your Coupling

To handle database code flexibly, you should decouple the application logic from the specifics of the database platform it uses. You will see lots of opportunities for this kind of separation of components in your own projects.

Imagine, for example, that the Lesson system must incorporate a registration component to add new lessons to the system. As part of the registration procedure, an administrator should be notified when a lesson is added. The system’s users can’t agree whether this notification should be sent by mail or by text message. In fact, they’re so argumentative that you suspect they might want to switch to a new mode of communication in the future. What’s more, they want to be notified of all sorts of things, so that a change to the notification mode in one place will mean a similar alteration in many other places.

If you’ve hard-coded calls to a Mailer class or a Texter class, then your system is tightly coupled to a particular notification mode, just as it would be tightly coupled to a database platform by the use of a specialized database API. Here is some code that hides the implementation details of a notifier from the system that uses it:

为了灵活处理数据库代码，我们应该将应用逻辑从数据库平台的特殊性中解耦出来。在你自己的项目中，你会看到很多这种需要分离组件的情况。例如，课程系统中应包含注册组件，从而向系统中添加新课程。添加了新课程后，应该通知管理员，这是注册程序的一部分。对于应该通过邮件发送通知还是通过文本消息发送通知，系统用户的意见不一致。实际上，他们太挑别了，以至于你怀疑将来他们会想使用一种新的信息传达模式。此外，他们希望发生任何事情都会收到通知。所以，修改了通知模式的一处意味着要对多处做同样的修改。

如果已经硬编码了对 Mailer 类或 Texter 类的调用，那么系统就与特殊的通知模式紧密相关了。就像利用专门的数据库 API 时，系统就与某数据库平台紧密相关一样。下面的这些代码对使用通知程序的系统隐藏了通知程序的实现细节。

```php
class RegistrationMgr {
    function register(Lesson $lesson) {
        // do something with the lesson

        // now tell someone
        $notifier = Notifier::getNotifier();
        $notifier->inform("new lesson: cost({$lesson->cost()})");
    }
}

abstract class Notifier {
    public static function getNotifier(): Notifier {
        // acquire concrete class according to configuration or other logic
        if (rand(1, 2) === 1) {
            return new MailNotifier();
        } else {
            return new TextNotifier();
        }
    }
}

class MailNotifier extends Notifier {
    public function inform($message) {
        echo "MAIL notification: {$message}\n";
    }
}

class TextNotifier extends Notifier {
    public function inform($message) {
        echo "TEXT notification: {$message}\n";
    }
}
```

I create RegistrationMgr, a sample client for my Notifier classes. The Notifier class is abstract, but it does implement a static method, getNotifier(), which fetches a concrete Notifier object (TextNotifier or MailNotifier). In a real project, the choice of Notifier would be determined by a flexible mechanism, such as a configuration file. Here, I cheat and make the choice randomly. MailNotifier and TextNotifier do nothing more than print out the message they are passed along with an identifier to show which one has been called.

Notice how the knowledge of which concrete Notifier should be used has been focused in the Notifier::getNotifier() method. I could send notifier messages from a hundred different parts of my system, and a change in Notifier would only have to be made in that one method. Here is some code that calls the RegistrationMgr:

注意，具体应该使用哪个 Notifier 对象取决于 Notifier::getnotifier() 方法。我可以从系统的上百个不同部分发送消息，但只需在该方法中对 Notifier 进行一项修改即可。


```php
$mrg = new RegistrationMgr();
$mrg->register(new Seminar(4, new TimedCostStrategy));
$mrg->register(new Lecture(4, new FixedCostStrategy));
```

And here’s the output from a typical run:

```
TEXT notification: new lesson: cost (20)
MAIL notification: new lesson: cost (30)
```

Notice how similar the structure in Figure 8-6 is to that formed by the Doctrine components shown in Figure 8-5.

### 2.4 Code to an Interface, Not to an Implementation

This principle is one of the all-pervading themes of this book. You saw in Chapter 6 (and in the last section) that you can hide different implementations behind the common interface defined in a superclass. Client code can then require an object of the superclass’s type rather than that of an implementing class, unconcerned by the specific implementation it is actually getting.

Parallel conditional statements, like the ones I rooted out from Lesson::cost() and Lesson::chargeType(), are a common sign that polymorphism is needed. They make code hard to maintain because a change in one conditional expression necessitates a change in its siblings. Conditional statements are occasionally said to implement a「simulated inheritance.」

把不同的实现隐藏在父类所定义的共同接口下。然后客户端代码需要一个父类的对象而不是一个子类的对象，从而使客户端代码可以不用关心它实际得到的是哪个具体实现。我们在 Lesson::cost() 和 Lesson::cost() 中创建的并行条件语句，就是需要多态的常见标志。这样的条件语句使代码很难维护，因为条件表达式的改变必然要求与之对应的代码主体也随之改变，所以条件语句有时会被称作实现了一个「模拟继承」。

By placing the cost algorithms in separate classes that implement CostStrategy, I remove duplication. I also make it much easier should I need to add new cost strategies in the future.

From the perspective of client code, it is often a good idea to require abstract or general types in your methods’ parameters. By requiring more specific types, you could limit the flexibility of your code at runtime. Having said that, of course, the level of generality you choose in your argument hints is a matter of judgment. Make your choice too general, and your method may become less safe. If you require the specific functionality of a subtype, then accepting a differently equipped sibling into a method could be risky.

Still, make your choice of argument hint too restricted, and you lose the benefits of polymorphism. Take a look at this altered extract from the Lesson class:

而通过把计费算法放置在一个实现 CostStrategy 的独立的类中，我们可以移除重复代码，也可以使在未来加入新的计费策略变得更加容易。从客户端代码的角度看，类方法参数为抽象或通用类型通常都是不错的主意。如果参数对对象类型要求过于严格，就会限制代码在运行时的灵活性。

当然，如何使用参数类型提示来调整参数对象的「通用性」是需要仔细权衡的。选择过于通用，则会降低方法的安全性。而如果需要某个子类型的特有功能，那么方法接受另一个子类类型则可能会有风险。尽管如此，若参数的类型匹配限制过于严格，那么将无法得到多态带来的好处。下面是修改过的 Lesson 类里的一段代码。

```php
// listing 08.17    

public function __construct(int $duration, FixedCostStrategy $strategy)    {        
    $this->duration = $duration;        
    $this->costStrategy = $strategy;    
}
```

There are two issues arising from the design decision in this example. First, the Lesson object is now tied to a specific cost strategy, which closes down my ability to compose dynamic components. Second, the explicit reference to the FixedPriceStrategy class forces me to maintain that particular implementation.

By requiring a common interface, I can combine a Lesson object with any CostStrategy implementation:

```php
// listing 08.18    
public function __construct(int $duration, CostStrategy $strategy)    {        
    $this->duration = $duration;        
    $this->costStrategy = $strategy;    
}
```

1『 CostStrategy 只提供接口。』

I have, in other words, decoupled my Lesson class from the specifics of cost calculation. All that matters is the interface and the guarantee that the provided object will honor it. Of course, coding to an interface can often simply defer the question of how to instantiate your objects. 

When I say that a Lesson object can be combined with any CostStrategy interface at runtime, I beg the question,「But where does the CostStrategy object come from?」When you create an abstract superclass, there is always the issue of how its children should be instantiated. Which child do you choose and according to which condition? This subject forms a category of its own in the Gang of Four pattern catalog, and I will examine this further in the next chapter.

换句话说，我们把 Lesson 类从具体的费用计算中分离出来了。我们所做的就是提供接口并保证所提供的对象会实现接口。当然，面向接口编程无法回答如何实例化对象的问题。当我们说 Lesson 对象能在运行时与任何 Coststrategy 接口绑定时，我们回避了这么一个问题：「但是 coststrategy 对象从哪里来呢？」当创建一个抽象父类时，常会碰到如何实例化它的子类的问题。你会选择实例化哪个子类来对应相应的条件呢？这个主题在《设计模式》模式目录中形成了一个独立的类别，我们会在下章研究其中一些模式。

1『核心问题：当创建一个抽象父类时，常会碰到如何实例化它的子类的问题。你会选择实例化哪个子类来对应相应的条件呢？回复：在抽象父类和具体实例化子类之间再抽象出一个「中间类」，这个中间类专门负责实例化，具体实例化子类（包含实例化代码）继承这个中间类。（2020-07-03）』

### 2.5 The Concept that Varies

It’s easy to interpret a design decision once it has been made, but how do you decide where to start?

The Gang of Four recommend that you「encapsulate the concept that varies.」In terms of my lesson example, the varying concept is the cost algorithm. Not only is the cost calculation one of two possible strategies in the example, but it is obviously a candidate for expansion: special offers, overseas student rates, introductory discounts-all sorts of possibilities present themselves.

1『核心观点：封装变化。』

I quickly established that subclassing for this variation was inappropriate, and I resorted to a conditional statement. By bringing my variation into the same class, I underlined its suitability for encapsulation.

The Gang of Four recommend that you actively seek varying elements in your classes and assess their suitability for encapsulation in a new type. Each alternative in a suspect conditional may be extracted to form a class that extends a common abstract parent. This new type can then be used by the class or classes from which it was extracted. This has the following effects: 1) Promoting flexibility through composition. 2) Making inheritance hierarchies more compact and focused. 3) Focusing responsibility. 4) Reducing duplication.

我们发现为这个变化直接创建子类是不合适的，于是使用了条件语句。通过把变化的元素放入同一个类中，我们强调了封装的适用性。《设计模式》建议积极搜寻类中变化的元素，并评估它们是否适合用新类型来封装。根据一定条件，变化的元素（如计费算法）可被提取出来形成子类（如 TimedCostStrategy 和 FixedCostStrategy），而这些元素共同拥有一个抽象父类（Coststrategy）。而这个新类型（CostStrategy）能被其他类使用。这么做有以下好处：1）专注于职责。2）通过组合提高灵活性。3）使继承层级体系更紧凑和集中；4）减少重复。

So how do you spot variation? One sign is the misuse of inheritance. This might include inheritance deployed according to multiple forces at one time (e.g., lecture/seminar and fixed/timed cost). It might also include subclassing on an algorithm where the algorithm is incidental to the core responsibility of the type. The other sign of variation suitable for encapsulation is, as you have seen, a conditional expression.

1『发现「变化点」的两个信号：误用继承和条件语句。』

那么如何发现变化的元素呢？误用继承便是一个标志。误用的表现可能包括一次实现不同分支（lecture/seminar and fixed/timed cost）的继承；也可能包括子类化某个算法，而该算法对于该对象类型的核心职责是偶然的。当然，适合封装「变化元素」的另一个标志便是出现了条件表达式。

### 2.6 Patternitis

One problem for which there is no pattern is the unnecessary or inappropriate use of patterns. This has earned patterns a bad name in some quarters. Because pattern solutions are neat, it is tempting to apply them wherever you see a fit, whether they truly fulfill a need or not.

The eXtreme Programming (XP) methodology offers a couple of principles that might apply here. The first is,「You aren’t going to need it」(often abbreviated to YAGNI). This is generally applied to application features, but it also makes sense for patterns.

When I build large environments in PHP, I tend to split my application into layers, separating application logic from presentation and persistence layers. I use all sorts of core and enterprise patterns in conjunction with one another.

When I am asked to build a feedback form for a small business web site, however, I may simply use procedural code in a single page script. I do not need enormous amounts of flexibility; I won’t be building on the initial release. I don’t need to use patterns that address problems in larger systems. Instead, I apply the second XP principle:「Do the simplest thing that works.」

When you work with a pattern catalog, the structure and process of the solution are what stick in the mind, consolidated by the code example. Before applying a pattern, though, pay close attention to the problem, or「when to use it,」section, and then read up on the pattern’s consequences. In some contexts, the cure may be worse than the disease.

模式的一个问题便是不必要或不恰当地使用模式。这让模式在某些领域名声不佳。因为模式解决方案很棒，所以它会引诱你把模式应用在任何你认为合适的地方，无论它们是否真的适合用来达到目标。极限编程（XP, extreme Programming）提供了几个可以使用的相关原则。第一个是「你还不需要它」。这通常被应用在应用程序的功能上，但是对于模式来说也有意义。

当使用 PHP 开发较大的项目时，我会把应用程序分离到各个层中，把应用程序逻辑从表现层和持久化层中分离开来。我通常联合使用各种核心模式和企业模式。然而当为一个小型商务网站建立一个用户反馈表单时，我可能只在单一页面脚本中使用过程式代码。此时，不需要大量的灵活性，不需要以后基于最初版本进行大量扩展，也不需要使用那些在更庞大的系统中解决问题的模式，而是应用极限编程的第二个原则：用最简单的方式来完成任务。

当使用模式目录时，通过示例代码能巩固你脑中解决方案的结构和流程。然而在应用模式之前，要特别注意目录中「问题」或者「何时使用」那部分，并且熟读模式的效用。在某些情况下，错误的治疗会比疾病本身更糟。

### 2.7 The Patterns

This book is not a pattern catalog. Nevertheless, in the coming chapters, I will introduce a few of the key patterns in use at the moment, providing PHP implementations and discussing them in the broad context of PHP programming.

The patterns described will be drawn from key catalogs, including Design Patterns: Elements of Reusable Object-Oriented Software, Patterns of Enterprise Application Architecture by Martin Fowler (Addison-Wesley Professional, 2002) and Core J2EE Patterns: Best Practices and Design Strategies (Prentice Hall, 2001) by Alur, et al. I use the Gang of Four’s categorization as a starting point, dividing patterns into five categories, as follows.

被描述的模式将会从主要的模式目录，包括《设计模式》、《企业应用架构模式》和《J2EE 核心模式》中提取出来，我将以《设计模式》一书的分类为起点，将模式分为以下五类。

2『这三本模式相关的经典一定要去读，真香，哈哈。』

1. Patterns for Generating Objects. These patterns are concerned with the instantiation of objects. This is an important category given the principle,「Code to an interface.」If you are working with abstract parent classes in your design, then you must develop strategies for instantiating objects from concrete subclasses. It is these objects that will be passed around your system.

2. Patterns for Organizing Objects and Classes. These patterns help you to organize the compositional relationships of your objects. More simply, these patterns show how you combine objects and classes.

3. Task-Oriented Patterns. These patterns describe the mechanisms by which classes and objects cooperate to achieve objectives.

4. Enterprise Patterns. I look at some patterns that describe typical Internet programming problems and solutions. Drawn largely from Patterns of Enterprise Application Architecture and Core J2EE Patterns: Best Practices and Design Strategies, the patterns deal with presentation and application logic.

5. Database Patterns. An examination of patterns that help with storing and retrieving data, and with mapping objects to and from databases.

1『在使用生成对象模式时，运行时期间，如何根据特定的条件实现特定的子类实例化对象是关键点。』

1、用于生成对象的模式。这类模式关注对象的实例化。考虑到「面向接口编程」原则，这是一个重要的分类。如果在设计中使用抽象父类，那么我们必须考虑从具体子类实例化对象的策略。实例化得到的对象会在系统中被传递。

2、用于组织对象和类的模式。这类模式帮助我们组织对象的组成关系。更简单地说，就是这些模式教我们如何合并对象和类。

3、面向任务的模式。这类模式描述了如何让类和对象合作来达成特定目标。

4、企业模式。我们着眼于一些描述典型因特网编程问题和解决方案的模式。它们很大程度上来自于《企业应用架构模式》和《J2EE 核心模式》这两本书，用于处理表现逻辑及应用逻辑。

5、数据库模式。数据库存取数据及对象一数据库映射的相关模式。

## 0203. Generating Objects

This chapter covered some of the tricks that you can use to generate objects. I began by examining the Singleton pattern, which provides global access to a single instance. Next, I looked at the Factory Method pattern, which applies the principle of polymorphism to object generation. And I combined Factory Method with the Abstract Factory pattern to generate creator classes that instantiate sets of related objects. I also looked at the Prototype pattern and saw how object cloning can allow composition to be used in object generation. Finally, I examined two strategies for object creation: Service Locator and Dependency Injection.

本章介绍了一些用于生成对象的窍门，讨论了支持全局访问实例的单例模式，以及应用多态原则生成对象的工厂方法模式。之后，我们结合使用工厂方法模式和抽象工厂模式来生成一系列创建者类，用于实例化一组相关对象。最后，研究了原型模式，学习了如何使用对象克隆使对象组合可用于生成对象。

Creating objects is a messy business. So, many object-oriented designs deal with nice, clean abstract classes, taking advantage of the impressive flexibility afforded by polymorphism (the switching of concrete implementations at runtime). To achieve this flexibility, though, I must devise strategies for object generation. This is the topic I will look at in this chapter.

This chapter will cover the following patterns: 1) The Singleton pattern: A special class that generates one—and only one—object instance. 2) The Factory Method pattern: Building an inheritance hierarchy of creator classes. 3) The Abstract Factory pattern: Grouping the creation of functionally related products. 4) The Prototype pattern: Using clone to generate objects. 5) The Service Locator pattern: Asking your system for objects. 6) The Dependency Injection pattern: Letting your system give you objects.

单例模式：生成一个且只生成一个对象实例的特殊类；工厂方法模式：构建创建者类的继承层级。抽象工厂模式：功能相关产品的创建。原型模式：使用克隆来生成对象。

### 3.1 Problems and Solutions in Generating Objects

Object creation can be a weak point in object-oriented design. In the previous chapter, you saw the principle,「Code to an interface, not to an implementation.」To this end, you are encouraged to work with abstract supertypes in your classes. This makes code more flexible, allowing you to use objects instantiated from different concrete subclasses at runtime. This has the side effect that object instantiation is deferred.

对象创建有时会成为面向对象设计的一个薄弱环节。在前一章中，我们看到「针对接口编程，而不是针对实现编程」的原则。就此而言，鼓励在类中使用抽象的超类。这使代码更具灵活性，可以让你在运行时使用从不同的具体子类中实例化的对象。但这样做也有副作用，那就是对象实例化被推迟。

Here’s a class that accepts a name string and instantiates a particular object:

```php
<?php

abstract class Employee {
    protected $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    abstract public function fire();
}

class Minion extends Employee {
    public function fire()
    {
        echo "{$this->name}: I'll clear my desk\n";
    }
}

class NastyBoss {
    private $employees = [];

    public function addEmployee(string $employeeName) {
        $this->employees[] = new Minion($employeeName);
    }

    public function projectFail() {
        if (count($this->employees) > 0 ) {
            $emp = array_pop($this->employees);
            $emp->fire();
        }
    }
}

$boss = new NastyBoss();
$boss->addEmployee('harry');
$boss->addEmployee('bob');
$boss->addEmployee('mary');
$boss->projectFail();
```

```
mary: I'll clear my desk
```

As you can see, I define an abstract base class, Employee, with a downtrodden implementation, Minion. Given a name string, the NastyBoss::addEmployee() method instantiates a new Minion object. Whenever a NastyBoss object runs into trouble (via the NastyBoss::projectFails() method), it looks for a Minion to fire.

By instantiating a Minion object directly in the NastyBoss class, we limit flexibility. If a NastyBoss object could work with any instance of the Employee type, we could make our code amenable to variation at runtime as we add more Employee specializations. You should find the polymorphism in Figure 9-1 familiar.

如你所看到的，我们定义了一个抽象基类 Employee（雇员）以及一个受压迫员工的具体实现 Minion。NastyBoss::addEmployee() 方法通过接受的名字字符串来实例化新的 Minion。对象且 Nastyboss（苛刻的老板）对象遇到了麻烦（通过 NastyBoss::projectFails() 方法），它就会解雇一个 Minion。由于在 NastyBoss 类中直接实例化 Minion 对象，代码的灵活性受到了限制。如果 NastyBoss 对象可以使用 Employee 类的任何实例，那么代码在运行时就能应对更多特殊的 Employee。在图 9-1 中，应该可以找到你熟悉的多态。

Figure 9-1.  Working with an abstract type enables polymorphism

If the NastyBoss class does not instantiate a Minion object, where does it come from? Authors often duck out of this problem by constraining an argument type in a method declaration, and then conveniently omitting to show the instantiation in anything other than a test context:

如果 NastyBoss 类不实例化 Minion 对象，那么 Minion 对象从何而来？许多人通常在方法声明中限制参数类型来巧妙避开这个问题，然后除了在测试时实例化对象，在其他时候尽量避免提及。

1『抽象出一个状态类跟 NastyBoss 类组合起来呗，让 NastyBoss 调用状态类来实例化 Minion 对象。』

```php
<?php

abstract class Employee {
    protected $name;

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    abstract public function fire();
}

class Minion extends Employee {
    public function fire()
    {
        echo "{$this->name}: I'll clear my desk\n";
    }
}

class CluedUp extends Employee {
    public function fire() {
        echo "{$this->name}: I'll call my lawyer\n";
    }
}

class NastyBoss {
    private $employees = [];

    public function addEmployee(Employee $employee) {
        $this->employees[] = $employee;
    }

    public function projectFail() {
        if (count($this->employees) > 0 ) {
            $emp = array_pop($this->employees);
            $emp->fire();
        }
    }
}

$boss = new NastyBoss();
$boss->addEmployee(new Minion('harry'));
$boss->addEmployee(new CluedUp('bob'));
$boss->addEmployee(new Minion('mary'));
$boss->projectFail();
$boss->projectFail();
$boss->projectFail();
```

```
mary: I'll clear my desk
bob: I'll call my lawyer
harry: I'll clear my desk
```

Although this version of the NastyBoss class works with the Employee type, and therefore benefits from polymorphism, I still haven’t defined a strategy for object creation. Instantiating objects is a dirty business, but it has to be done. This chapter is about classes and objects that work with concrete classes, so that the rest of your classes do not have to.

If there is a principle to be found here, it is「delegate object instantiation.」I did this implicitly in the previous example by demanding that an Employee object be passed to the NastyBoss::addEmployee() method. I could, however, equally delegate to a separate class or method that takes responsibility for generating Employee objects. Here I add a static method to the Employee class that implements a strategy for object creation:

虽然这个版本的 NastyBoss 类能与 Employee 类型一起工作，而且也能从多态中获益，但我们仍旧没有定义创建对象的策略。实例化对象是一件麻烦事，但是我们又不得不去做。这一章讲的是使用具体类的类和对象。这样，不使用具体类的类和对象不一定非要实例化对象。如果说这里存在一个原则的话，那便是「把对象实例化的工作委托出来」。之前的示例已然隐含了这个原则，即要求将一个 Employee 对象传递给 NastyBoss::addEmployee() 方法。然而我们也可以委托一个独立的类或方法来生成 Employee 对象，其效果是一样的。下面给 Employee 类添加一个实现了对象创建策略的静态方法。

```php
abstract class Employee {
    protected $name;
    private static $types = ['Minion', 'CluedUp', 'WellConnected'];

    public static function recruit(string $name) {
        $num = rand(1, count(self::$types)) - 1;
        $class = __NAMESPACE__ . "\\" . self::$types[$num];
        return new $class($name);
    }

    public function __construct(string $name)
    {
        $this->name = $name;
    }

    abstract public function fire();
}

class Minion extends Employee {
    public function fire()
    {
        echo "{$this->name}: I'll clear my desk\n";
    }
}

class CluedUp extends Employee {
    public function fire() {
        echo "{$this->name}: I'll call my lawyer\n";
    }
}

class WellConnected extends Employee {
    public function fire() {
        echo "{$this->name}: I'll call my dad\n";
    }
}
```

As you can see, this takes a name string and uses it to instantiate a particular Employee subtype at random. I can now delegate the details of instantiation to the Employee class’s recruit() method:

```php
$boss = new NastyBoss();
$boss->addEmployee(Employee::recruit("harry"));
$boss->addEmployee(Employee::recruit("bob"));
$boss->addEmployee(Employee::recruit("mary"));
$boss->projectFail();
$boss->projectFail();
$boss->projectFail();
```

 ■ Note: I use the term「factory」frequently in this chapter. a factory is a class or method with responsibility for generating objects.
 
You saw a simple example of such a class in Chapter 4. I placed a static method in the ShopProduct class called getInstance(). 

getInstance() is responsible for generating the correct ShopProduct subclass based on a database query. The ShopProduct class, therefore, has a dual role. It defines the ShopProduct type, but it also acts as a factory for concrete ShopProduct objects:

```php
public static function getInstance(int $id, PDO $pdo): ShopProduct    {        
    $stmt = $pdo->prepare("select * from products where id=?");        
    $result = $stmt->execute([$id]);

    $row = $stmt->fetch();        
    if (empty($row)) {            
        return null;        
    }        
    if ($row['type'] == "book") {            
        // instantiate a BookProduct object        
    } elseif ($row['type'] == "cd") {            
        // instantiate a CdProduct object        
    } else {            
        // instantiate a ShopProduct object        
    }        
    $product->setId($row['id']);        
    $product->setDiscount($row['discount']);        
    return $product;    
}
```

The getInstance() method uses a large if/else statement to determine which subclass to instantiate. Conditionals like this are quite common in factory code. Although you should attempt to excise large conditional statements from your projects, doing so often has the effect of pushing the conditional back to the moment at which an object is generated. This is not generally a serious problem because you remove parallel conditionals from your code in pushing the decision-making back to this point. In this chapter, then, I will examine some of the key Gang of Four patterns for generating objects.

getinstance() 方法使用一系列 if/ese 语句来决定实例化哪个子类。像这样的条件语句在工厂代码中十分常见。尽管我们常尝试从项目中消除大量的条件语句，但生成对象确实需要使用这些条件语句。一般来说这不是一个严重问题，因为我们将代码中并行的条件语句转移到 getInstance() 来，由 getInstance() 来决定对象生成。在本章中，我们将研究一些用于生成对象的关键模式，它们来源于《设计模式》一书。

### 3.2 The Singleton Pattern

The global variable is one of the great bugbears of the object-oriented programmer. The reasons should be familiar to you by now. Global variables tie classes into their context, undermining encapsulation (see Chapter 6,「Objects and Design,」and Chapter 8,「Some Pattern Principles,」for more on this). A class that relies on global variables becomes impossible to pull out of one application and use in another, without first ensuring that the new application itself defines the same global variables.

1『全局变量破坏了封装，做一张任意卡片。』——已完成

全局变量是面向对象程序员遇到的引发 bug 的主要原因之一。这是因为全局变量将类捆绑于特定的环境，破坏了封装（参见第 6 章及第 8 章）。如果新的应用程序无法保证一开始就定义了相同的全局变量，那么一个依赖于全局变量的类就无法从一个应用程序中提取出来并应用到新应用程序中。

Although this is undesirable, the unprotected nature of global variables can be a greater problem. Once you start relying on global variables, it is perhaps just a matter of time before one of your libraries declares a global that clashes with another declared elsewhere. You have seen already that, if you are not using namespaces, PHP is vulnerable to class name clashes. But this is much worse. PHP will not warn you when globals collide. The first you will know about it is when your script begins to behave oddly. Worse still, you may not notice any issues at all in your development environment. By using globals, though, you potentially leave your users exposed to new and interesting conflicts when they attempt to deploy your library alongside others.

Globals remain a temptation, however. This is because there are times when the sin inherent in global access seems a price worth paying in order to give all of your classes access to an object.

As I hinted, namespaces provide some protection from this. You can at least scope variables to a package, which means that third-party libraries are less likely to clash with your own system. Even so, the risk of collision exists within the namespace itself.

尽管这并不是我们想要的，但全局变量不受保护的本质的确是个很大的问题。一旦开始依赖全局变量，那么某个类库中声明的全局变量和其他地方声明的全局变量迟早会发生冲突。我们已经看到过 PHP 易受到类名冲突的影响，但全局变量的冲突更加糟糕——PHP 并不会对全局变量冲突发出任何警告。你也许只是发现代码行为有些古怪。更糟的是，在开发环境中你也许根本发现不了任何问题。因此如果在类库中使用全局变量，用户可能在尝试将你的类库与其他类库一同部署时遇到冲突。

然而，全局变量仍是一个诱惑。因为有时我们为了使所有类都能访问某个对象，会不惜忍受全局访问的缺陷。我提到过，命名空间在一定程度上避免了命名冲突。你至少可以将变量的作用域定义在包中，这意味着第三方的库与你的系统产生冲突的可能性大大降低了。即便如此，命名空间内部还是存在命名冲突。

#### 3.2.1 The Problem

Well-designed systems generally pass object instances around via method calls. Each class retains its independence from the wider context, collaborating with other parts of the system via clear lines of communication. Sometimes, though, you find that this forces you to use some classes as conduits for objects that do not concern them, introducing dependencies in the name of good design.

1『作为对象间沟通的类 > 引入依赖关系，直觉上这个是个关键知识点，目前无法消化。（2020=07-18）』

经过良好设计的系统一般通过方法调用来传递对象实例。每个类都会与背景环境保持独立并通过清晰的通信方式来与系统中其他部分进行协作。有时你需要使用一些作为对象间沟通渠道的类，此时就不得不引入依赖关系。

Imagine a Preferences class that holds application-level information. We might use a Preferences object to store data such as DSN strings (Data Source Names hold table and user information about a database), URL roots, file paths, and so on. This is the sort of information that will vary from installation to installation. The object may also be used as a notice board, a central location for messages that could be set or retrieved by otherwise unrelated objects in a system.

Passing a Preferences object around from object to object may not always be a good idea. Many classes that do not otherwise use the object could be forced to accept it simply so that they could pass it on to the objects that they work with. This is just another kind of coupling.

假设有一个用于保存应用程序信息的 Preferences 类。我们可能会使用一个 Preferences 对象来保存诸如 DSN（用于保存数据库的表及用户信息）字符串，URL 根目录、文件路径等数据。这些信息在你每次部署程序时都可能会有所不同。该对象也可被用作一个「公告板」，它是可以被系统中其他无关对象设置和获取消息的中心。

但在对象中传递 Preferences 对象并不总是个好主意。你可以让原来并不使用 Preferences 对象的类强制性地接受 Preferences。对象，以便这些类能传递 Preferences 对象给其他对象。但这样做产生了另一种形式的耦合。

You also need to be sure that all objects in your system are working with the same Preferences object. You do not want objects setting values on one object, while others read from an entirely different one.

Let’s distill the forces in this problem: 1) A Preferences object should be available to any object in your system. 2) A Preferences object should not be stored in a global variable, which can be overwritten. 3) There should be no more than one Preferences object in play in the system. This means that object Y can set a property in the Preferences object, and object Z can retrieve the same property, without either one talking to the other directly (assuming both have access to the Preferences object).

我们还需要保证系统中的所有对象都使用同一个 Preferences 对象。我们不希望一些对象在一个 Preferences 对象上设值，而其他对象从另外一个完全不同的 Preferences 对象上读取数据。让我们提炼出这个问题的几个关键点：1）Preferences 对象应该可以被系统中的任何对象使用。2）Preferences 对象不应该被储存在会被覆写的全局变量中。3）系统中不应超过一个 Preferences 对象。也就是说，Y 对象可设置 Preferences 对象的一个属性，而 Z 对象不需要通过其他对象（假设 Y 和 Z 都可以访问 Preferences）对象就可以直接获得该属性的值。

#### 3.2.2 Implementation

To address this problem, I can start by asserting control over object instantiation. Here, I create a class that cannot be instantiated from outside of itself. That may sound difficult, but it’s simply a matter of defining a private constructor:

1『定义一个私有的构造函数，可以实现，创建一个不能从外部实例化的类。』

```php
<?php

class Preferences {
    private $props = [];

    private function __construct() {
        //
    }

    public function setProperty(string $key, string $val) {
        $this->props[$key] = $val;
    }

    public function getProperty(string $key): string {
        return $this->props[$key];
    }
}
```

Of course, at this point, the Preferences class is entirely unusable. I have taken access restriction to an absurd level. Because the constructor is declared private, no client code can instantiate an object from it. The setProperty() and getProperty() methods are therefore redundant. I can use a static method and a static property to mediate object instantiation:

```php
<?php

class Preferences {
    private $props = [];
    private static $instance;

    private function __construct() {
        //
    }

    public static function getInstance() {
        if (empty(self::$instance)) {
            self::$instance = new Preferences();
        }
        return self::$instance;
    }

    public function setProperty(string $key, string $val) {
        $this->props[$key] = $val;
    }

    public function getProperty(string $key): string {
        return $this->props[$key];
    }
}
```

The \$instance property is private and static, so it cannot be accessed from outside the class. The getInstance() method has access, though. Because getInstance() is public and static, it can be called via the class from anywhere in a script:

```php
// listing 09.12

$pref = Preferences::getInstance();
$pref->setProperty("name", "matt");
unset($pref);   // remove the reference
$pref2 = Preferences::getInstance();
$pref2->setProperty("name", "matt");
echo $pref2->getProperty("name") . "\n"; // demonstrate value is not lost
```

The output is the single value we added to the Preferences object initially, available through a separate access:

```
matt
```

A static method cannot access object properties because it is, by definition, invoked in a class and not an object context. It can, however, access a static property. When getInstance() is called, I check the Preferences::\$instance property. If it is empty, then I create an instance of the Preferences class and store it in the property. Then I return the instance to the calling code. Because the static getInstance() method is part of the Preferences class, I have no problem instantiating a Preferences object, even though the constructor is private.

静态方法不能访问普通的对象属性，因为根据静态的定义，它只能被类而不是对象调用。但静态方法可以访问一个静态属性。

#### 3.2.3 Consequences

So, how does the Singleton approach compare to using a global variable? First, the bad news. Both Singletons and global variables are prone to misuse. Because Singletons can be accessed from anywhere in a system, they can serve to create dependencies that can be hard to debug. Change a Singleton, and classes that use it may be affected. Dependencies are not a problem in themselves. After all, we create a dependency every time we declare that a method requires an argument of a particular type. The problem is that the global nature of the Singleton lets a programmer bypass the lines of communication defined by class interfaces. When a Singleton is used, the dependency is hidden away inside a method and not declared in its signature. This can make it harder to trace the relationships within a system. Singleton classes should therefore be deployed sparingly and with care.

Nevertheless, I think that moderate use of the Singleton pattern can improve the design of a system, saving you from horrible contortions as you pass objects unnecessarily around your system. Singletons represent an improvement over global variables in an object-oriented context. You cannot overwrite a Singleton with the wrong kind of data.

那么使用单例对象与使用全局变量相比，又如何呢？首先是坏的一面。单例和全局变量都可能被误用。因为单例在系统任何地方都可以被访问，所以它们可能会导致很难调试的依赖关系。如果改变一个单例，那么所有使用该单例的类可能都会受到影响。在这里，依赖本身并不是问题。毕竟，我们在每次声明一个有特定类型参数的方法时，也就创建了依赖关系。问题是，单例对象的全局化的性质会使程序员绕过类接口定义的通信线路。当单例被使用时，依赖便会被隐藏在方法内部，而并不会出现在方法声明中。这使得系统中的依赖关系更加难以追踪，因此需要谨慎小心地部署单例类。

然而，我认为适度地使用单例模式可以改进系统的设计。在系统中传递那些不必要的对象令人厌烦，而单例可以让你从中解放出来。在面向对象的开发环境中，单例模式是一种对于全局变量的改进。你无法用错误类型的数据覆写一个单例。这种保护在不支持命名空间的 PHP 版本里尤其重要。因为在 PHP 中命名冲突会在编译时被捕获，并使脚本停止运行。

### 3.3 Factory Method Pattern

Object-oriented design emphasizes the abstract class over the implementation. That is, it works with generalizations rather than specializations. The Factory Method pattern addresses the problem of how to create object instances when your code focuses on abstract types. The answer? Let specialist classes handle instantiation.

1『用特定的类来处理实例化。』

#### 3.3.1 The Problem

Imagine a personal organizer project that manages Appointment objects, among other object types. Your business group has forged a relationship with another company, and you must communicate appointment data to it using a format called BloggsCal. The business group warns you that you may face yet more formats as time wears on, though.

Staying at the level of interface alone, you can identify two participants right away. You need a data encoder that converts your Appointment objects into a proprietary format. Let’s call that class ApptEncoder. You need a manager class that will retrieve an encoder and maybe work with it to communicate with a third party. You might call that CommsManager. Using the terminology of the pattern, the CommsManager is the creator, and the ApptEncoder is the product. You can see this structure in Figure 9-3.

假设有一个关于个人事务管理的项目，其功能之一是管理 Appointment（预约）对象。我们的业务团队和另一个公司建立了关系，目前需要用一个叫做 BloggsCal 的格式来和他们交流预约相关的数据。但是业务团队提醒我们将来可能要面对更多的数据格式。在接口级别上，我们可以立即定义两个类。其一是需要一个数据编码器来把 Appointment 对象转换成一个专有的格式，将这个编码器命名为 Apptencoder 类；另外需要一个管理员类来获得编码器，并使用编码器与第三方进行通信，我们将这个管理类命名为 CommsManager 类。使用模式术语来描述的话，CommsManager 便是创建者（creator），而 ApptEncoder 是产品（product）你可以在图 9-3 中看到这个结构。

How do you get your hands on a real concrete ApptEncoder, though? You could demand that an ApptEncoder be passed to the CommsManager, but that simply defers your problem, and you want the buck to stop about here. Here I instantiate a BloggsApptEncoder object directly within the CommsManager class:

但是如何得到一个具体的 ApptEncoder 对象？我们可以要求传递 ApptEncoder 给 CommsManager，但这只是延缓了问题，而我们希望问题在此可以彻底解决。因此，先在 CommsManager 类中直接实例化 BloggsApptEncoder 对象。

```php
<?php

abstract class ApptEncoder {
    abstract public function encode(): string;
}

class BloggsApptEncoder extends ApptEncoder {
    public function encode(): string
    {
        return "Appointment data encoded in BloggsCal format\n";
    }
}

class MegaApptEncoder extends ApptEncoder {
    public function encode(): string
    {
        return "Appointment data encoded in MegaCal format\n";
    }
}

class CommsManager {
    public function getApptEncoder(): ApptEncoder {
        return new BloggsApptEncoder();
    }
}
```

The CommsManager class is responsible for generating BloggsApptEncoder objects. When the sands of corporate allegiance inevitably shift, and we are asked to convert our system to work with a new format called MegaCal, we can simply add a conditional into the CommsManager::getApptEncoder() method. This is the strategy we have used in the past, after all. Let’s build a new implementation of CommsManager that handles both BloggsCal and MegaCal formats:

CommsManager 类负责生成 BloggsApptEncoder 对象。当团队合作关系发生改变，而我们被要求转换系统来使用一个新的格式 MegaCal 时，可以只添加一个条件语句到 CommsManager::getApptEncoder() 方法。毕竟，这是我们以前用过的策略。下面来建立一个新的可以同时处理 BloggsCal 和 MegaCal格式的 CommsManager 的实现。

```php
class CommsManager {
    const BLOGGS = 1;
    const MEGA = 2;
    private $mode;

    public function __construct(int $mode)
    {
        $this->mode = $mode;
    }
     
    public function getApptEncoder(): ApptEncoder {
        switch ($this->mode) {
            case (self::BLOGGS):
                return new BloggsApptEncoder();
            default:
                return new MegaApptEncoder();
        }
        
    }
}

$man = new CommsManager(CommsManager::MEGA);
echo (get_class($man->getApptEncoder())) . "\n";
$man = new CommsManager(CommsManager::BLOGGS);
echo (get_class($man->getApptEncoder())) . "\n";
```

I use constant flags to define two modes in which the script might be run: MEGA and BLOGGS. I use a switch statement in the getApptEncoder() method to test the \$mode property and instantiate the appropriate implementation of ApptEncoder.

There is little wrong with this approach. Conditionals are sometimes considered examples of bad 「code smells,」but object creation often requires a conditional at some point. You should be less sanguine if you see duplicate conditionals creeping into your code. The CommsManager class provides functionality for communicating calendar data. Imagine that the protocols you work with require you to provide header and footer data to delineate each appointment. I can extend the previous example to support a getHeaderText() method:

这种方式仍有点小小的缺陷。通常情况下，创建对象的确需要指定条件，但有时候条件语句会被当做坏的「代码味道」的象征。如果重复的条件语句蔓延在代码中，我们不应该感到乐观。CommsManager 类已经能够提供交流日历数据的功能。但是，假设我们所使用的协议要求提供页眉和页脚数据来描述每次预约，情况又将如何呢？下面扩展之前的例子来支持 getHeaderText() 方法。

```php
class CommsManager {
    const BLOGGS = 1;
    const MEGA = 2;
    private $mode;

    public function __construct(int $mode)
    {
        $this->mode = $mode;
    }
     
    public function getApptEncoder(): ApptEncoder {
        switch ($this->mode) {
            case (self::BLOGGS):
                return new BloggsApptEncoder();
            default:
                return new MegaApptEncoder();
        }
        
    }

    public function getHeaderText(): string {
        switch ($this->mode) {
            case (self::BLOGGS):
                return "BloggsCal header\n";
            default:
                return "MegaCal header\n";
        }
        
    }
}
```

As you can see, the need to support header output has forced me to duplicate the protocol conditional test. This will become unwieldy as I add new protocols, especially if I also add a getFooterText() method. 

So, let’s summarize the problem so far: 1) I do not know until runtime the kind of object I need to produce (BloggsApptEncoder or MegaApptEncoder). 2) I need to be able to add new product types with relative ease (SyncML support is just a new business deal away!). 3) Each product type is associated with a context that requires other customized operations (e.g., getHeaderText(), getFooterText()).

Additionally, I am using conditional statements, and you have seen already that these are naturally replaceable by polymorphism. The Factory Method pattern enables you to use inheritance and polymorphism to encapsulate the creation of concrete products. In other words, you create a CommsManager subclass for each protocol, each one implementing the getApptEncoder() method.

之前已介绍过这些条件语句可以被多态代替，而工厂方法模式恰好能让我们用继承和多态来封装具体产品的创建。换句话说，我们要为每种协议创建 CommsManager 的一个子类，而每一个子类都要实现 getApptEncoder() 方法。

#### 3.3.2 Implementation

The Factory Method pattern splits creator classes from the products they are designed to generate. The creator is a factory class that defines a method for generating a product object. If no default implementation is provided, it is left to creator child classes to perform the instantiation. Typically, each creator subclass instantiates a parallel product child class. I can redesignate CommsManager as an abstract class. That way, I keep a flexible superclass and put all my protocol-specific code in the concrete subclasses. You can see this alteration in Figure 9-4.

Here’s some simplified code:

```php
<?php

abstract class ApptEncoder {
    abstract public function encode(): string;
}

class BloggsApptEncoder extends ApptEncoder {
    public function encode(): string
    {
        return "Appointment data encoded in BloggsCal format\n";
    }
}

class MegaApptEncoder extends ApptEncoder {
    public function encode(): string
    {
        return "Appointment data encoded in MegaCal format\n";
    }
}

abstract class CommsManager {
    abstract public function getHeaderText(): string;
    abstract public function getApptEncoder(): ApptEncoder;
    abstract public function getFooterText(): string;
}

class BloggsCommsManager extends CommsManager {
     
    public function getApptEncoder(): ApptEncoder {
        return new BloggsApptEncoder();
    }

    public function getHeaderText(): string {
        return "BloggsCal header\n";
    }

    public function getFooterText(): string {
        return "BloggsCal footer\n";
    }
}

$mgr = new BloggsCommsManager();
echo $mgr->getHeaderText();
echo $mgr->getApptEncoder()->encode();
echo $mgr->getFooterText();
```

So, when I am required to implement MegaCal, supporting it is simply a matter of writing a new implementation for my abstract classes. Figure 9-5 shows the MegaCal classes.

#### 3.3.3 Consequences

Notice that the creator classes mirror the product hierarchy. This is a common consequence of the Factory Method pattern and disliked by some as a special kind of code duplication. Another issue is the possibility that the pattern could encourage unnecessary subclassing. If your only reason for subclassing a creator is to deploy the Factory Method pattern, you may need to think again (that’s why I introduced the header and footer constraints to the example here).

1『对的，如果我只想创建 getApptEncoder 子类，目前的工厂模式额外创建了 getHeaderText 和 getFooterText 两个子类。』

I have focused only on appointments in my example. If I extend it somewhat to include to-do items and contacts, I face a new problem. I need a structure that will handle sets of related implementations at one time. The Factory Method pattern is often used with the Abstract Factory pattern, as you will see in the next section.

请注意我们的创建者类与产品的层次结构是非常相似的。这是使用工厂方法模式的常见结果，这形成了一种特殊的代码重复，因而被一些人所不喜欢。另一个问题是该模式可能会导致不必要的子类化。如果你为创建者类创建子类的原因只是为了实现工厂方法模式，那么最好再考虑下（这就是为什么在例子中引进页眉和页脚）。在示例中我们只关注「预约」功能。如果想扩展一下功能，使其能够处理「待办事宜」及联系人，那么将会遇到新问题。我们需要一个可以同时处理一组相关实现的架构。正如我们在下节中将看到的，工厂方法模式经常和抽象工厂模式一起使用。

### 3.4 Abstract Factory Pattern

In large applications, you may need factories that produce related sets of classes. The Abstract Factory pattern addresses this problem.

在大型应用中，我们很可能需要工厂来产生一组相关的类。抽象工厂模式可解决这个问题。

#### 3.4.1 The Problem

Let’s look again at the organizer example. I manage encoding in two formats, BloggsCal and MegaCal. I can grow this structure horizontally by adding more encoding formats, but how can I grow vertically, adding encoders for different types of PIM objects? In fact, I have been working toward this pattern already. In Figure 9-6, you can see the parallel families with which I will want to work. These are appointments (Appt), things to do (Ttd), and contacts (Contact).

再来看一下之前实现的个人事务管理的示例。我们以 BloggsCal 和 MegaCal 这两种格式管理编码。我们可以通过加入更多编码格式来使此结构「横向」增长，但如何通过给不同类型的 PM 对象加入编码器使它「纵向」增长呢？事实上，我们一直在应用该模式。在图 9-6 中，可以看到我们使用的相似的类层次结构，分别是预约（Appt）、待办事宜（Ttd）、和联系人（Contact）。

The BloggsCal classes are unrelated to one another by inheritance (although they could implement a common interface), but they are functionally parallel. If the system is currently working with BloggsTtdEncoder, it should also be working with BloggsContactEncoder. To see how I enforce this, you can begin with the interface, as I did with the Factory Method pattern (see Figure 9-7).

BloggsCal 的类与其他格式（如 MegaCal）互相没有关联（尽管它们实现了一个公共的接口），但它们的功能相似。所以如果系统目前正在使用 BloggsTtdEncoder，那么它应该也能使用 BloggsContactEncoder。看一下如何做到这一点。我们仍从接口开始着手，就如在工厂方法模式中所做的那样（见图 9-7)。

#### 3.4.2 Implementation

The abstract CommsManager class defines the interface for generating each of the three products (ApptEncoder, TtdEncoder, and ContactEncoder). You need to implement a concrete creator in order to actually generate the concrete products for a particular family. I illustrate that for the BloggsCal format in Figure 9-8.

CommsManager 抽象类定义了用于生成 3 个产品（ApptEncoder、TtdEncoder 和 ContactEncoder）的接口。我们需要先实现一个具体的创建者，然后才能创建一个特定类型的具体产品。图 9-8 创建了 BloggsCal 格式的创建者。

Here is a code version of CommsManager and BloggsCommsManager:

```php
abstract class CommsManager {
    abstract public function getHeaderText(): string;
    abstract public function getApptEncoder(): ApptEncoder;
    abstract public function getTtdEncoder(): getTtdEncoder;
    abstract public function getContactEncoder(): getContactEncoder;
    abstract public function getFooterText(): string;
}

class BloggsCommsManager extends CommsManager {
    
    public function getHeaderText(): string {
        return "BloggsCal header\n";
    }

    public function getApptEncoder(): ApptEncoder {
        return new BloggsApptEncoder();
    }

    public function getTtdEncoder(): TtEncoder {
        return new BloggsTtdEncoder();
    }

    public function getContactEncoder(): ContactEncoder {
        return new BloggsContactEncoder();
    }

    public function getFooterText(): string {
        return "BloggsCal footer\n";
    }
}
```

Notice that I use the Factory Method pattern in this example. getContactEncoder() is abstract in CommsManager and implemented in BloggsCommsManager. Design patterns tend to work together in this way, one pattern creating the context that lends itself to another. In Figure 9-9, I add support for the MegaCal format.

请注意，在这个例子中使用了工厂方法模式。getContactEncoder() 是 CommsManager 的抽象方法，并在 BloggsCommsManager 中被实现。设计模式间经常会这样协作：一个模式创建可以把它自己引入到另一个模式的上下文环境。在图 9-9 中，我们加入了对 MegaCal 格式的支持。

#### 3.4.3 Consequences

So, let’s look at what this pattern buys: 1) First, I decouple my system from the details of implementation. I can add or remove any number of encoding formats in my example without causing a knock-on effect. 2) I enforce the grouping of functionally related elements of my system. So, by using BloggsCommsManager, I am guaranteed that I will work only with BloggsCal-related classes. 3) Adding new products can be a pain. Not only do I have to create concrete implementations of the new product, but I also have to amend the abstract creator and every one of its concrete implementers in order to support it.

首先，将系统与实现的细节分离开来。我们可以在示例中添加或移除任意数目的编码格式而不会影响系统；对系统中功能相关的元素强制进行组合。因此，通过使用 BloggsCommsManager，可以确保只使用与 BloggsCal 相关的类；添加新产品将会令人苦恼。因为不仅要创建新产品的具体实现，而且为了支持它，我们必须修改抽象创建者和它的每一个具体实现。

Many implementations of the Abstract Factory pattern use the Factory Method pattern. This may be because most examples are written in Java or C++. PHP, however, does not have to enforce a return type for a method (though it now can), which affords us some flexibility that we might leverage. Rather than create separate methods for each Factory Method, you can create a single make() method that uses a flag argument to determine which object to return:

抽象工厂模式的许多实现都会使用工厂方法模式，这可能是因为大多数范例都是用 Java 或者 C++ 写的。但是 PHP 并不会强制规定方法的返回类型，这给了我们一些可能利用的灵活性。我们可以创建一个使用标志参数来决定返回什么对象的单一的 make() 方法，而不用给每个工厂方法创建独立的方法。

```php
interface Encoder {
    public function encode(): string;
}

abstract class CommsManager {
    const APPT = 1;
    const TTD = 2;
    const CONTACT =3;
    abstract public function getHeaderText(): string;
    abstract public function make(int $flag_int): Encoder;
    abstract public function getFooterText(): string;
}

class BloggsCommsManager extends CommsManager {
    
    public function getHeaderText(): string {
        return "BloggsCal header\n";
    }

    public function make(int $flag_int): Encoder {
        switch ($flag_int) {
            case self::APPT:
                return new BloggsApptEncoder();
            case self::CONTACT:
                return new BloggsContactEncoder();
            case self::TTD:
                return new BloggsTtdEncoder();
        }
    }

    public function getFooterText(): string {
        return "BloggsCal footer\n";
    }
}
```

As you can see, I have made the class interface more compact. I’ve done this at a considerable cost, though. In using a factory method, I define a clear interface and force all concrete factory objects to honor it. In using a single make() method, I must remember to support all product objects in all the concrete creators. I also introduce parallel conditionals, as each concrete creator must implement the same flag tests. A client class cannot be certain that concrete creators generate all the products because the internals of make() are a matter of choice in each case.

On the other hand, I can build more flexible creators. The base creator class can provide a make() method that guarantees a default implementation of each product family. Concrete children could then modify this behavior selectively. It would be up to implementing creator classes to call the default make() method after providing their own implementation. You will see another variation on the Abstract Factory pattern in the next section.

可以看出，类的接口变得更加紧凑。但是这样做也有一定代价。在使用工厂方法时，我们定义了一个清晰的接口并强制所有具体的工厂对象遵循它。而使用单一的 make() 方法，我们必须在所有的具体创建者中支持所有的产品对象。同时，我们也引入了平行条件，因为每个具体创建者都必须实现相同的标志检测（flag test）。客户类无法确定具体的创建者是否可以生成所有产品，因为 make() 方法的内部需要对每种情况都进行考虑并作出选择。另一方面，我们可以创建更灵活的创建者。创建者基类可以提供 make() 方法来保证每个产品家族有一个默认实现。具体子类可以选择性地改变这一行为。子类可以实现自己的 make() 方法并调用，由此决定生成何种对象。这些创建者子类可以自行决定是否在执行自己的 make() 方法后调用父类的 make() 方法。我们会在下一节中介绍抽象工厂模式的另一个变形。

### 3.5 Prototype

The emergence of parallel inheritance hierarchies can be a problem with the Factory Method pattern. This is a kind of coupling that makes some programmers uncomfortable. Every time you add a product family, you are forced to create an associated concrete creator (the BloggsCal encoders are matched by BloggsCommsManager, for example). In a system that grows fast enough to encompass many products, maintaining this kind of relationship can quickly become tiresome.

One way of avoiding this dependency is to use PHP’s clone keyword to duplicate existing concrete products. The concrete product classes themselves then become the basis of their own generation. This is the Prototype pattern. It enables you to replace inheritance with composition. This in turn promotes runtime flexibility and reduces the number of classes you must create.

平行继承层次的出现是工厂方法模式带来的一个问题。这是一种让一些程序员不舒服的耦合。每次添加产品家族时，你就被迫去创建一个相关的具体创建者（比如编码器 BloggsCal 和 BloggsCommsManager 匹配）。在一个快速增长的系统里会包含越来越多的产品，而维护这种关系便会很快令人厌烦。一个避免这种依赖的办法是使用 PHP 的 clone 关键词复制已存在的具体产品。然后，具体产品类本身便成为它们自己生成的基础。这便是原型模式。使用该模式我们可以用组合代替继承。这样的转变则促进了代码运行时的灵活性，并减少了必须创建的类。

#### 3.5.1 The Problem

Imagine a Civilization-style web game in which units operate on a grid of tiles. Each tile can represent sea, plains, or forests. The terrain type constrains the movement and combat abilities of units occupying the tile. You might have a TerrainFactory object that serves up Sea, Forest, and Plains objects. You decide that you will allow the user to choose among radically different environments, so the Sea object is an abstract superclass implemented by MarsSea and EarthSea. Forest and Plains objects are similarly implemented. The forces here lend themselves to the Abstract Factory pattern. You have distinct product hierarchies (Sea, Plains, Forests), with strong family relationships cutting across inheritance (Earth, Mars). Figure 9-10 presents a class diagram that shows how you might deploy the Abstract Factory and Factory Method patterns to work with these products.

假设有一款「文明」风格的网络游戏，可在区块组成的格子中操作战斗单元（unit）。每个区块分别代表海洋、平原和森林。地形的类别约束了占有区块的单元的移动和格斗能力。我们可以有一个 TerrainFactory 对象来提供 sea、Forest 和 Plains 对象，我们决定允许用户在完全不同的环境里选择，于是 sea 可能是 MarsSea 和 Earthsea 的抽象父类。Forest（森林）和 Plains（平原）对象也会有相似的实现。这里的分支便构成了抽象工厂模式。我们有截然不同的产品体系（sea、Plains、Forest），而这些产品家族间有超越继承的紧密联系，如 Earth（地球）和 Mars（火星），它们都同时存在海洋、森林和平原地形。图 9-10 所示的类图展示了如何对这些产品应用抽象工厂和工厂方法模式。

As you can see, I rely on inheritance to group the terrain family for the products that a factory will generate. This is a workable solution, but it requires a large inheritance hierarchy, and it is relatively inflexible. When you do not want parallel inheritance hierarchies, and when you need to maximize runtime flexibility, the Prototype pattern can be used in a powerful variation on the Abstract Factory pattern.

你可以看到，我们依赖继承来组合工厂生成的 terrain（地形）家族产品。这的确是一个可行的解决方案，但这需要有一个大型的继承体系，并且相对来说不那么灵活。当你不想要平行的继承体系而需要最大化运行时的灵活性时，可以使用抽象工厂模式的强大变形——原型模式。

#### 3.5.2 Implementation

When you work with the Abstract Factory/Factory Method patterns, you must decide, at some point, which concrete creator you wish to use, probably by checking some kind of preference flag. As you must do this anyway, why not simply create a factory class that stores concrete products, and then populate this during initialization? You can cut down on a couple of classes this way and, as you shall see, take advantage of other benefits. Here’s some simple code that uses the Prototype pattern in a factory:

当使用抽象工厂模式或工厂方法模式时，必须决定使用哪个具体的创建者，这很可能是通过检査配置的值来决定的。既然必须这样做，那为什么不简单地创建一个保存具体产品的工厂类，并在初始化时就加入这种做法呢？这样除了可以减少类的数量，还有其他好处。下面是在工厂中使用原型模式的简单代码：

```php
<?php

class Sea {
    //
}

class EarthSea extends Sea {
    //
}

class MarsSea extends Sea {
    //
}

class Plains {
    //
}

class EarthPlains extends Plains {
    //
}

class MarsPlains extends Plains {
    //
}

class Forest {
    //
}

class EarthForest extends Forest {
    //
}

class MarsForest extends Forest {
    //
}

class TerrainFactory {
    private $sea;
    private $plains;
    private $forest;

    public function __construct(Sea $sea, Plains $plains, Forest $forest) {
        $this->sea = $sea;
        $this->plains = $plains;
        $this->forest = $forest;
    }

    public function getSea(): Sea {
        return clone $this->sea;
    }

    public function getPlains(): Plains {
        return clone $this->plains;
    }

    public function getForest(): Forest {
        return clone $this->forest;
    }
}

$factory = new TerrainFactory(
    new EarthSea(),
    new EarthPlains(),
    new EarthForest()
);

print_r($factory->getSea());
print_r($factory->getPlains());
print_r($factory->getForest());
```

As you can see, I load up a concrete TerrainFactory with instances of product objects. When a client calls getSea(), I return a clone of the Sea object that I cached during initialization. This structure buys me additional flexibility. Want to play a game on a new planet with Earth-like seas and forests, but Mars-like plains? No need to write a new creator class—you can simply change the mix of classes you add to TerrainFactory:

```php
$factory = new TerrainFactory(
    new EarthSea(),
    new MarsPlains(),
    new EarthForest()
);
```

So the Prototype pattern allows you to take advantage of the flexibility afforded by composition. We get more than that, though. Because you are storing and cloning objects at runtime, you reproduce object state when you generate new products. Imagine that Sea objects have a \$navigability property. The property influences the amount of movement energy a sea tile saps from a vessel and can be set to adjust the difficulty level of a game:

```php
class Sea {
    private $navigability = 0;

    public function __construct(int $navigability) {
        $this->navigability = $navigability;
    }
}
```

Now when I initialize the TerrainFactory object, I can add a Sea object with a navigability modifier. This will then hold true for all Sea objects served by TerrainFactory:

```php
$factory = new TerrainFactory(
    new EarthSea(-1),
    new EarthPlains(),
    new EarthForest()
);
```

This flexibility is also apparent when the object you wish to generate is composed of other objects.

 ■ Note: I covered object cloning in Chapter 4. the clone keyword generates a shallow copy of any object to which it is applied. this means that the product object will have the same properties as the source. if any of the source’s properties are objects, then these will not be copied into the product. instead, the product will reference the same object properties. it is up to you to change this default and to customize object copying in any other way, by implementing a \_\_clone() method. this is called automatically when the clone keyword is used.

我们在第 4 章中介绍了对象克隆。clone 关健字能给应用的对象生成一个浅复制（shallow copy）。也就是说，产品对象会具有和源对象一样的属性。如果源对象的任何属性是对象，那么这些对象属性不会被直接复制到产品中，相反产品会引用同样的对象属性。通过实现  \_\_clone() 方法，可以改变克隆的默认行为，并定制对象复制的方式，而这在 clone 关健词被使用时会被自动调用。

Perhaps all Sea objects can contain Resource objects (FishResource, OilResource, etc.). According to a preference flag, we might give all Sea objects a FishResource by default. Remember that if your products reference other objects, you should implement a \_\_clone() method to ensure that you make a deep copy:

如果你想生成的对象是由其他对象组合而成的，以上代码显然颇具灵活性。假设所有的 Sea 对象都能包含 Resource 对象（FishResource、OilResource 等）。通过配置的值，可以给所有的 Sea 对象默认提供一个 FishResource 对象。要记住的是如果产品对象引用了其他对象，那么你应该实现  \_\_clone() 方法来保证你得到的是深复制（deep copy）。

```php
class Contained {
}

class Container {    

    public $contained;

    function __construct()    {        
        $this->contained = new Contained();    
    }

    function __clone()   {        
        // Ensure that cloned object holds a        
        // clone of self::$contained and not a reference to it        
        $this->contained = clone $this->contained;    
    }
}
```

### 3.6 Pushing to the Edge: Service Locator

I promised that this chapter would deal with the logic of object creation, doing away with the sneaky buck-passing of many object-oriented examples. Yet some patterns here have slyly dodged the decision-making part of object creation, if not the creation itself.

The Singleton pattern is not guilty. The logic for object creation is built-in and unambiguous. The Abstract Factory pattern groups the creation of product families into distinct concrete creators. How do we decide which concrete creator to use, though? The Prototype pattern presents us with a similar problem. Both these patterns handle the creation of objects, but they defer the decision as to which object or group of objects should be created.

我保证过这一章主要介绍如何创建对象，不会列举许多与面向对象无关的例子。然而本章的些模式很狡猾地避过了对象生成相关的决策过程，看起来似乎与对象生成无关一一如果并不是创建本身的话。单例模式不在此列，因为单例模式中的对象创建逻辑是内建并明确的。抽象工厂模式产品家族的创建则分布到了不同的具体创建者中。那么我们如何选择具体的创建者呢？原型模式把相似的问题呈现在我们面前。这两个模式都用于创建对象，但它们延缓了应该创建哪个对象或者哪组对象的决定。

The particular concrete creator that a system chooses is often decided according to the value of a configuration switch of some kind. This could be located in a database, a configuration file, or a server file (such as Apache’s directory-level configuration file, usually called .htaccess), or it could even be hard-coded as a PHP variable or property. Because PHP applications must be reconfigured for every request, you need script initialization to be as painless as possible. For this reason, I often opt to hard-code configuration flags in PHP code. This can be done by hand or by writing a script that autogenerates a class file. Here’s a crude class that includes a flag for calendar protocol types:

系统经常根据配置的值来决定选择哪个特定的具体创建者。而这些配置信息可以在数据库、配置文件或服务器文件中（如 Apache 服务器的配置文件通常是 htaccess），或者干脆以 PHP 变量或属性进行硬编码。因为 PHP 应用程序必须为每个请求重新配置，所以需要让脚本的初始化尽可能地简单。正因为此，我经常选择在 PHP 代码中通过硬编码来设定配置标志。这可以通过手写或者写一个自动生成类文件的脚本来完成。下面是一个包含日历协议类型的标记的类：

```php
class Settings {
    static $COMMSTYPE = 'Bloggs';
}

class AppConfig {
    private static $instance;
    private $commsManager;

    private function __construct() {
        // will run once only
        $this->init();
    }

    private function init() {
        switch (Settings::$COMMSTYPE) {
            case 'Mega':
                $this->commsManager = new MegaCommsManager();
               break;
            default:
               $this->commsManager = new BloggsCommsManager();
        }
    }

    public static function getInstance(): AppConfig {
        if (empty(self::$instance)) {
            self::$instance = new self();
        }
        return self::$instance;
    }

    public function getCommsManager(): CommsManager {
        return $this->commsManager;
    }
}
```

The AppConfig class is a standard Singleton. For that reason, I can get an AppConfig instance anywhere in the system, and I will always get the same one. The init() method is invoked by the class’s constructor and is therefore only run once in a process. It tests the Settings::\$COMMSTYPE property, instantiating a concrete CommsManager object according to its value. Now my script can get a CommsManager object and work with it without ever knowing about its concrete implementations or the concrete classes it generates:

AppConfig 类是一个标准的单例。因此，我们可以在系统中任何地方得到 AppConfig 实例，并且确保得到的一直是同一个实例。init() 方法会被类的构造方法调用，且因此在一个进程中只会运行一次。它检查 Settings::\$COMMSTYPE 属性，并根据该属性的值来实例化一个具体的 CommsManager 对象。现在我们的代码可以得到并使用一个 CommsManager 对象，而不需要知道它的具体实现或者它所生成的具体类。

```php
$commsMgr = AppConfig::getInstance()->getCommsManager();
$commsMgr->getApptEncoder()->encode();
```

Because AppConfig manages the work of finding and creating components for us, it is an instance of what’s known as the Service Locator pattern. It’s neat (and we’ll see it again in more detail in Chapter 12), but it does introduce a more benign dependency than direct instantiation. Any classes using its service must explicitly invoke this monolith, binding them to the wider system. For this reason, some prefer another approach.

### 3.7 Splendid Isolation: Dependency Injection

In the previous section, I used a flag and a conditional statement within a factory to determine which of two CommsManager classes to serve up. The solution was not as flexible as it might have been. The classes on offer were hard-coded within a single locator, with a choice of two components built-in to a conditional. That inflexibility was a facet of my demonstration code, though, rather than a problem with Service Locator, per se. I could have used any number of strategies to locate, instantiate, and return objects on behalf of client code. The real reason Service Locator is often treated with suspicion, however, is the fact that a component must explicitly invoke the locator. This feels a little, well, global. And object-oriented developers are rightly suspicious of all things global.

#### 3.7.1 The Problem

Whenever you use the new operator, you close down the possibility of polymorphism within that scope. Imagine a method that deploys a hard-coded BloggsApptEncoder object, for example:

```php
// listing 09.37

class AppointmentMaker {    
    public function makeAppointment()    {        
        $encoder = new BloggsApptEncoder();        
        return $encoder->encode();    
    }
}
```

This might work for our initial needs, but it will not allow any other ApptEncoder implementation to be switched in at runtime. That limits the ways in which the class can be used, and it makes the class harder to test. Much of this chapter addresses precisely this kind of inflexibility. But, as I pointed out in the previous section, I have skated over the fact that, even if we use the Prototype or Abstract Factory patterns, instantiation has to happen somewhere. Here again is a fragment of code that creates a Prototype object:

```php
// listing 09.32

$factory = new TerrainFactory(    
    new EarthSea(),    
    new EarthPlains(),    
    new EarthForest()
);
```

The Prototype TerrainFactory class called here is a step in the right direction—it demands generic types: Sea, Plains, and Forest. The class leaves it up to the client code to determine which implementations should be provided. But how is this done?

#### 3.7.2 Implementation

Much of our code calls out to factories. As we have seen, this model is known as the Service Locator pattern. A method delegates responsibility to a provider which it trusts to find and serve up an instance of the desired type. The Prototype example inverts this; it simply expects the instantiating code to provide implementations at call time. There’s no magic here—it’s simply a matter of requiring types in a constructor’s signature, instead of creating them directly within the method. A variation on this is to provide setter methods, so that clients can pass in objects before invoking a method that uses them.

So let’s fix up AppointmentMaker in this way:

```php
// listing 09.38

class AppointmentMaker2 {    

    private $encoder;

    public function __construct(ApptEncoder $encoder) {        
        $this->encoder = $encoder;    
    }
    
    public function makeAppointment()    {        
        return $this->encoder->encode();    
    }
}
```

AppointmentMaker2 has given up control—it no longer creates the BloggsApptEncoder, and we have gained flexibility. What about the logic for the actual creation of objects, though? Where do the dreaded new statements live? We need an assembler component to take on the job. Typically, this approach uses a configuration file to figure out which implementations should be instantiated. There are tools to help us with this, but this book is all about doing it ourselves, so let’s build a very naive implementation. I’ll start with a crude XML format which describes the relationships between classes in our system and the concrete types that should be passed to their constructors:

```html
<objects>    
    <class name="\popp\ch09\batch11\TerrainFactory">        
        <arg num="0" inst="\popp\ch09\batch11\EarthSea" />        
        <arg num="1" inst="\popp\ch09\batch11\MarsPlains" />        
        <arg num="2" inst="\popp\ch09\batch11\EarthForest" />    
    </class>

    <class name="\popp\ch09\batch14\AppointmentMaker2">        
        <arg num="0" inst="\popp\ch09\batch06\BloggsApptEncoder" />    
    </class>
</objects>
```

I’ve described two classes from this chapter: TerrainFactory and AppointmentMaker2. I want TerrainFactory to be instantiated with an EarthSea object, a MarsPlains object, and an EarthForest object. I would also like AppointmentMaker2 to be passed a BloggsApptEncoder object. Here’s a very simple assembler class that reads this configuration data and instantiates objects on demand:

```php
// listing 09.39

class ObjectAssembler {    

    private $components = [];

    public function __construct(string $conf)    {        
        $this->configure($conf);    
    }

    private function configure(string $conf)    {        
        $data = simplexml:load_file($conf);        
        foreach ($data->class as $class) {            
            $args = [];            
            $name = (string)$class['name'];           
            foreach ($class->arg as $arg) {                
                $argclass = (string)$arg['inst'];                
                $args[(int)$arg['num']] = $argclass;            
            }            
            ksort($args);            
            $this->components[$name] = function () use ($name, $args) {                
                $expandedargs = [];                
                foreach ($args as $arg) {                    
                    $expandedargs[] = new $arg();                
                }                
                $rclass = new \ReflectionClass($name);                
                return $rclass->newInstanceArgs($expandedargs);            
            };        
        }    
    }

    public function getComponent(string $class)    {        
        if (! isset($this->components[$class])) {            
            throw new \Exception("unknown component '$class'");        
        }        
        $ret = $this->components[$class]();        
        return $ret;    
    }
}
```

This is pretty crude, and it is a little dense at first reading, so let’s work through it briefly. Most of the real action takes place in configure(). The method accepts a path which is passed on from the constructor. It uses the simplexml extension to parse the configuration XML. In a real project, of course, we’d add more error handling here and throughout. For now, I’m pretty trusting of the XML I’m parsing. For every \<class> element, I extract the fully qualified class name and store it in the \$name variable. Then I acquire all the \<arg> subelements, all of which have their own class names. I store the arguments in an array named \$args, ordered according to the XML num argument. I pack all of this in an anonymous function which I store in the \$components property. This function, which instantiates a requested class and all its required objects, is only invoked when getComponent() is called with the correct class name. In this way the ObjectAssembler can maintain a pretty small footprint. Note the use of a closure here. The anonymous function has access to the \$name and \$args variables declared in the scope of its creation, thanks to the use keyword.

Of course, this is really toy code. In addition to improved error checking, a robust implementation would need to handle the possibility that the objects to be injected into a component might themselves require arguments. We might also want to address issues around caching. For example, should a contained object be instantiated for every call, or only once?

 ■ Note:  if you are considering building a Dependency injection assembler/container, you should look at a couple of options: pimple (notwithstanding its unpleasant name) and symfony Di. You can find out more about pimple at http://pimple.sensiolabs.org/; you can learn more about the symfony Di component at http://symfony.com/doc/current/components/dependency_injection/introduction.html.

Nevertheless, we can now maintain the flexibility of our components and handle instantiation dynamically. Let’s try out the ObjectAssembler:

```php
// listing 09.40$assembler = new ObjectAssembler("src/ch09/batch14/objects.xml");
$apptmaker = $assembler->getComponent("\\popp\\ch09\\batch14\\AppointmentMaker2");
$out = $apptmaker->makeAppointment();
print $out;
```

Once we have an ObjectAssembler, object acquisition takes up a single statement. The AppointmentMaker2 class is free of its previous hard-coded dependency on an ApptEncoder instance. A developer can now use the configuration file to control what classes are used at runtime, as well as to test AppointmentMaker2 in isolation from the wider system.

#### 3.7.3 Consequences

So, now we’ve seen two options for object creation. The AppConfig class was an instance of Service Locator (i.e., a class with the ability to find components or services on behalf of its client). Using dependency injection certainly makes for more elegant client code. The AppointmentMaker2 class is blissfully unaware of strategies for object creation. It simply does its job. This is the ideal for a class, of course. We want to design classes that can focus on their responsibilities, isolated as far as possible from the wider system. However, this purity does come at a price. The object assembler component hides a lot of magic. We must treat it as a black box and trust it to conjure up objects on our behalf. This is fine, so long as the magic works. Unexpected behavior can be hard to debug.

The Service Locator pattern, on the other hand, is simpler, though it embeds your components into a wider system. It is not the case that, used well, a Service Locator makes testing harder. Nor does it make a system inflexible. A Service Locator can be configured to serve up arbitrary components for testing or according to configuration. But a hard-coded call to a service locator makes a component dependent upon it. Because the call is made from within the body of a method, the relationship between the client and the target component (which is provided by the Service Locator) is also somewhat obscured. This relationship is made explicit in the Dependency Injection example because it is declared in the constructor method’s signature.

So, which approach should we choose? To some extent it’s a matter of preference. For my own part, I tend to prefer to start with the simplest solution, and then to refactor to greater complexity, if needed. For that reason, I usually opt for Service Locator. I can create a Registry class in a few lines of code, and increase its flexibility according to the requirements. My components are a little more knowing than I would like, but since I rarely move classes from one system to another, I have not suffered too much from the embedding effect. When I have moved a system-based class into a standalone library, I have not found it particularly hard to refactor the Service Locator dependency away.

Dependency Injection offers purity, but it requires another kind of embedding. You must buy in to the magic of the assembler. If you are already working within a framework which offers this functionality, there is no reason not to avail yourself of it. The Symfony  DependencyInjection component, for example, provides a hybrid solution of Service Locator (known as the「service container」) and Dependency Injection. The service container manages the instantiation of objects according to the configuration (or code, if you prefer) and provides a simple interface for clients to obtain those objects. The service container even allows the use of factories for object creation. On the other hand, if you are rolling your own, or using components from various frameworks, you may wish to keep things simple at the cost of some elegance.

## 0204. Patterns for Flexible Object Programming

In this chapter, I looked at a few of the ways that classes and objects can be organized in a system. In particular, I focused on the principle that composition can be used to engender flexibility where inheritance fails. In both the Composite and Decorator patterns, inheritance is used to promote composition and to define a common interface that provides guarantees for client code.

You also saw delegation used effectively in these patterns. Finally, I looked at the simple but powerful Facade pattern. Facade is one of those patterns that many people have been using for years without having a name to give it. Facade lets you provide a clean point of entry to a tier or subsystem. In PHP, the Facade pattern is also used to create object wrappers that encapsulate blocks of procedural code.

在本章中，我们研究了类和对象的几种组织方式，其中特别关注了使用组合以得到继承无法达到的灵活性。在组合模式和装饰模式中，使用继承是为了更好地组合对象，并为客户端代码提供统一的接口。我们也可以看到在这些模式中委托是如何被有效使用的。最后，我们研究了简单却强大的外观模式。外观模式是众多模式中一个被很多人运用了多年却没有得到命名的模式。外观模式可以为一个分层或一个子系统提供一个简洁的入口。在 PHP 中，外观模式也可用于创建封装过程式代码块的对象封装器。

With strategies for generating objects covered, we’re free now to look at some strategies for structuring classes and objects. I will focus in particular on the principle that composition provides greater flexibility than inheritance. The patterns I examine in this chapter are once again drawn from the Gang of Four catalog.

This chapter will cover a trio of patterns: 1) The Composite pattern: Composing structures in which groups of objects can be used as if they were individual objects. 2) The Decorator pattern: A flexible mechanism for combining objects at runtime to extend functionality. 3) The Facade pattern: Creating a simple interface to complex or variable systems.

### 4.1 Structuring Classes to Allow Flexible Objects

Way back in Chapter 4, I said that beginners often confuse objects and classes. This was only half true. In fact, most of the rest of us occasionally scratch our heads over UML class diagrams, attempting to reconcile the static inheritance structures they show with the dynamic object relationships their objects will enter into off the page.

Remember the pattern principle,「Favor composition over inheritance」? This principle distills this tension between the organization of classes and objects. In order to build flexibility into our projects, we structure our classes so that their objects can be composed into useful structures at runtime.

This is a common theme running through the first two patterns of this chapter. Inheritance is an important feature in both, but part of its importance lies in providing the mechanism by which composition can be used to represent structures and extend functionality.

在第 4 章中，我曾说过初学者常常对对象和类感到困惑。这也不全对。事实上，即使不是初学者，有时也会大伤脑筋，比如我们会尝试让 UML 类图中描述的静态继承结构与这些类的动态对象的关系保持一致，有时这个目标并不容易实现。你还记得「组合优于继承」这个模式原则吗？该原则体现了类和对象之间的组织弹性。为了使项目更具灵活性，我们需要将类按一定结构组织起来，以便它们的对象在代码运行时能被构建为有用的结构。这是本章前两个模式的共同主题。继承在这两个模式中很重要，但是组合所提供的描述结构及扩展功能的机制也很重要。

1『将类按一定的结构组织起来，便于它们的对象在运行时被构建成有用的结构。这个信息直觉上很重要，目前没吃透。（2020-09-04）』

### 4.2 The Composite Pattern

The Composite pattern is perhaps the most extreme example of inheritance deployed in the service of composition. It is a simple and yet breathtakingly elegant design. It is also fantastically useful. Be warned, though; it is so neat, you might be tempted to overuse this strategy.

The Composite pattern is a simple way of aggregating and then managing groups of similar objects so that an individual object is indistinguishable to a client from a collection of objects. The pattern is, in fact, very simple, but it is also often confusing. One reason for this is the similarity in structure of the classes in the pattern to the organization of its objects. Inheritance hierarchies are trees, beginning with the super class at the root, and branching out into specialized subclasses. The inheritance tree of classes laid down by the Composite pattern is designed to allow the easy generation and traversal of a tree of objects.

组合模式也许是将继承用于组合对象的最极端的例子。组合模式的设计思想简单而又非常优雅，并且非常实用。但要注意的是，因为这个模式很好用，你也许会经不起诱惑而过度使用它。组合模式可以很好地聚合和管理许多相似的对象，因而对客户端代码来说，一个独立对象和一个对象集合是没有差别的。虽然该模式实际上非常简单，但还是经常令人感到迷惑。其中一个原因就是模式中类的结构和对象的组织结构非常相似。组合模式中继承的层级结构是树型结构，由根部的基类开始，分支到各个不同的子类，在其继承树中可以轻松地生成枝叶，也可以很容易地遍历整个对象树中的对象。

If you are not already familiar with this pattern, you have every right to feel confused at this point. Let’s try an analogy to illustrate the way that single entities can be treated in the same way as collections of things. Given broadly irreducible ingredients such as cereals and meat (or soya if you prefer), we can make a food product—a sausage, for example. We then act on the result as a single entity. Just as we eat, cook, buy, or sell meat, we can eat, cook, buy, or sell the sausage that the meat in part composes. We might take the sausage and combine it with the other composite ingredients to make a pie, thereby rolling a composite into a larger composite. We behave in the same way to the collection as we do to the parts. The Composite pattern helps us to model this relationship between collections and components in our code.

如果你以前不熟悉这个模式，也许会感到有些困惑。让我们举例说明，单个物体有时可以被当成一个集合来看待。例如，用谷类和肉类（或者是你更加喜欢的大豆）可以制作一种食物香肠。然后我们将香肠当做单个物体来处理。就像我们可以食用、烹调、购买或者出售肉类一样，我们也可以食用、烹调、购买或者出售由肉类组成的香肠。我们也许会用香肠和其他组合成分来制作馅饼，从而将一个组合物合成一个更大的组合物。在这个例子中，我们处理组件的方式和处理集合的方式是一样的。组合模式有助于我们为集合和组件之间的关系建立模型。

1『

很佩服作者以及译者的表述能力，上面的这段信息算是把「组合模式」弄清楚了，再结合「王铮的设计模式专栏」里提到的，四人帮的原话：

Compose objects into tree structure to represent part-whole hierarchies. Composite lets client treat individual objects and compositions of objects uniformly.

将一组对象组织（Compose）成树形结构，以表示一种「部分 - 整体」的层次结构。组合让客户端（代指代码的使用者）可以统一单个对象和组合对象的处理逻辑。

』

#### 4.2.1 The Problem

Managing groups of objects can be quite a complex task, especially if the objects in question might also contain objects of their own. This kind of problem is very common in coding. Think of invoices, with line items that summarize additional products or services, or things-to-do lists with items that themselves contain multiple subtasks. In content management, we can’t move for trees of sections, pages, articles, or media components. Managing these structures from the outside can quickly become daunting.

Let’s return to a previous scenario. I am designing a system based on a game called Civilization. A player can move units around hundreds of tiles that make up a map. Individual counters can be grouped together to move, fight, and defend themselves as a unit. Here I define a couple of unit types:

管理一组对象是很复杂的，当对象中可能还包含着它们自己的对象时尤其如此。这类问题在开发中非常常见。比如发票中会包含描述产品或服务的条目，或者待办事宜列表会包含多个子任务。在 CMS（Content Management System，内容管理系统）中，我们无法离开页面、文章、多媒体组件等。从外部来管理这些结构相当困难。让我们回到之前虚构的一个场景，我们以一个叫做「文明」的游戏为基础设计一个系统。玩家可以在一个由大量区块所组成的地图上移动战斗单元。独立的单元可被组合起来一起移动、战斗和防守。我们先定义一些战斗单元的类型。

```php
// listing 10.01

abstract class Unit {    
    abstract public function bombardStrength(): int;
}

class Archer extends Unit {
    public function bombardStrength(): int {        
        return 4;    
    }
}

class LaserCannonUnit extends Unit {    
    public function bombardStrength(): int {        
        return 44;    
    }
}
```

The Unit class defines an abstract bombardStrength() method, which sets the attack strength of a unit bombarding an adjacent tile. I implement this in both the Archer and LaserCannonUnit classes. These classes would also contain information about movement and defensive capabilities, but I’ll keep things simple. I could define a separate class to group units together, like this:

```php
// listing 10.02

class Army {    
    private $units = [];

    public function addUnit(Unit $unit)    {        
        array_push($this->units, $unit);    
    }

    public function bombardStrength(): int    {        
    $ret = 0;        
    foreach ($this->units as $unit) {            
        $ret += $unit->bombardStrength();        
    }        
    return $ret;    
    }
}

// listing 10.03

$unit1 = new Archer();
$unit2 = new LaserCannonUnit();
$army = new Army();
$army->addUnit($unit1);
$army->addUnit($unit2);
print $army->bombardStrength();
```

The Army class has an addUnit() method that accepts a Unit object. Unit objects are stored in an array property called \$units. I calculate the combined strength of my army in the bombardStrength() method. This simply iterates through the aggregated Unit objects, calling the bombardStrength() method of  each one.

This model is perfectly acceptable, as long as the problem remains as simple as this. What happens, though, if I were to add some new requirements? Let’s say that an army should be able to combine with other armies. Each army should retain its own identity so that it can disentangle itself from the whole at a later date. The Arch Duke’s brave forces might share common cause today with General Soames’s assault upon the exposed flank of the enemy, but a domestic rebellion may send his army scurrying home at any time. For this reason, I can’t just decant the units from each army into a new force.

如果问题一直如此简单，那么这样的模型还是非常令人满意的。但是当我们加入一些新的需求，会发生什么呢？比如军队应该可以与其他军队进行合并。同时，每个军队都会有它自己的 ID，这样军队以后还能从整编中解散出来。比如今天大公爵（Archduke）和 Soames 将军的勇士们可能一起并肩作战，但是当国内发生叛乱时，公爵可能会在任何时候将它的军队调回。因此，我们不能仅支持将军队与军队合并，还要能够在必要的时候再把原来的军队抽离出来。我们可以修改 Army 类，使之可以像添加 Unit 对象一样添加 Army 对象

I could amend the Army class to accept Army objects as well as Unit objects:

```php
// listing 10.04

public function addArmy(Army $army) {        
    array_push($this->armies, $army);    
}
```

Then I’d need to amend the bombardStrength() method to iterate through all armies as well as units:

```php
// listing 10.05   

 public function bombardStrength(): int {        
    $ret = 0;        
    foreach ($this->units as $unit) {            
        $ret += $unit->bombardStrength();        
    }        
    foreach ($this->armies as $army) {            
        $ret += $army->bombardStrength();        
    }        
    return $ret;    
 }
```

This additional complexity is not too problematic at the moment. Remember, though, I would need to do something similar in methods like defensiveStrength(), movementRange(), and so on. My game is going to be richly featured. Already the business group is calling for troop carriers that can hold up to ten units to improve their movement range on certain terrains. Clearly, a troop carrier is similar to an army in that it groups units. It also has its own characteristics. I could further amend the Army class to handle TroopCarrier objects, but I know that there will be a need for still more unit groupings. It is clear that I need a more flexible model.

Let’s look again at the model I have been building. All the classes I created shared the need for a bombardStrength() method. In effect, a client does not need to distinguish between an army, a unit, or a troop carrier. They are functionally identical. They need to move, attack, and defend. Those objects that contain others need to provide methods for adding and removing them. These similarities lead us to an inevitable conclusion. Because container objects share an interface with the objects that they contain, they are naturally suited to share a type family.

此时，这个新的需求（即添加和抽取军队）还不算太复杂。但是记住，我们还需要对 defensiveStrength()、movementRange() 等方法做相似的修改。慢慢地，我们的游戏会变得越来越完善。现在客户提出了新要求：运兵船可以支持最多 10 个战斗单元以改进它们在某些地形上的活动范围。显然，运兵船与用于组合战斗单元的 Army 对象相似，但它也有一些自己的特性。虽然我们能够通过改进 Army 类来处理 TroopCarrier 对象，但是我们知道以后可能会有更多对部队进行组合的需求。显然，我们需要一个更灵活的模型。

让我们再回顾一下已经建立的这个模型。所有已创建的类都需要 bombardStrength() 方法。实际上，客户端代码并不需要去区分对象是 army、unit 还是 troop carrier 类型。就功能上说，它们都是相同的：它们都要移动、攻击和防御。这些包含其他对象的对象需要提供添加和移除其他对象的方法。这些相似性会给我们带来一个必然的结论：因为容器对象与它们包含的对象共享同一个接口，所以它们应该共享同一个类型家族。

#### 4.2.2 Implementation

The Composite pattern defines a single inheritance hierarchy that lays down two distinct sets of responsibilities. We have already seen both of these in our example. Classes in the pattern must support a common set of operations as their primary responsibility. For us, that means the bombardStrength() method. Classes must also support methods for adding and removing child objects.

组合模式定义了一个单根继承体系，使具有截然不同职责的集合可以并肩工作。在之前的例子中我们已看到以上两点。组合模式中的类必须支持一个共同的操作集，以将其作为它们的首要职责。对我们来说，bombardStrength() 方法便支持这样的操作。类同时必须拥有添加和删除子对象的方法。

Figure 10-1 shows a class diagram that illustrates the Composite pattern as applied to our problem.

As you can see, all the units in this model extend the Unit class. A client can be sure, then, that any Unit object will support the bombardStrength() method. So, an Army can be treated in exactly the same way as an Archer.

The Army and TroopCarrier classes are composites: they are designed to hold Unit objects. The Archer and LaserCannon classes are leaves, designed to support unit operations, but not to hold other Unit objects. There is actually an issue as to whether leaves should honor the same interface as composites, as they do in Figure 10-1. The diagram shows TroopCarrier and Army aggregating other units, even though the leaf classes are also bound to implement addUnit(). I will return to this question shortly. Here is the abstract Unit class:

可以看到，模型中的所有部队单位都扩展自 Unit 类。然后，客户端代码可以肯定任何 unit 对象都支持 bombardStrength() 方法，因此完全可以像处理 Archer 对象那样处理 Army 对象。Army 和 TroopCarrier 类都被设计为组合对象，用于包含 Unit 对象。Archer 和 LaserCannon 类则是局部对象 1，具有部队单位的操作功能，但不能包含其他 Unit 对象。这里有个问题，就是局部对象是否需要遵循与图 10-1 所示的组合对象同样的接口。图 10-1 中的 TroopCarrier 和 Army 实现了与其他作战单元的组合，而即使在局部类中，也实现了 addUnit() 方法。我们稍后将讨论这个问题。

1 也称为树叶对象。称为树叶是因为组合模式为树型结构，组合对象为枝干，单独存在的对象为树叶。树叶对象应该是最小单位，其中不能包含其他对象。一一译者注

1『悟了悟了，在组合模式里，「组合对象」是树干，单独存在的对象（叶子对象）是树叶，叶子对象是不能再包含其他对象的。（2020-09-10）』

```php
// listing 10.06

abstract class Unit {    
    abstract public function addUnit(Unit $unit);    
    abstract public function removeUnit(Unit $unit);    
    abstract public function bombardStrength(): int;
}
```

As you can see, I lay down the basic functionality for all Unit objects here. Now, let’s see how a composite object might implement these abstract methods:

```php
// listing 10.07

class Army extends Unit {    
    private $units = [];

    public function addUnit(Unit $unit) {        
        if (in_array($unit, $this->units, true)) {            
            return;        
        }
        $this->units[] = $unit;    
    }

    public function removeUnit(Unit $unit) {        
        $idx = array_search($unit, $this->units, true);        
        if (is_int($idx)) {            
            array_splice($this->units, $idx, 1, []);        
        }    
    }

    public function bombardStrength(): int {        
        $ret = 0;        
        foreach ($this->units as $unit) {            
            $ret += $unit->bombardStrength();        
        }        
        return $ret;    
    }
}
```

1『上面几个数组操作的函数值得借鉴，意外收获，哈哈。而且老版书中 removeUnit() 里是通过匿名函数实现的，新版的这个实现应该更好，不然作者不会做此更新的。（2020-09-05）回复：1）数组内没有该元素，增加进去。2）删除数组内的某个元素。这两个功能实现可以借鉴到其他地方去。（2020-09-10）』

The addUnit() method checks whether I have already added the same Unit object before storing it in the private \$units array property. removeUnit() uses a similar check to remove a given Unit object from the property.

Army objects, then, can store Units of any kind, including other Army objects, or leaves such as Archer or LaserCannonUnit. Because all units are guaranteed to support bombardStrength(), our Army::bombardStrength() method simply iterates through all the child Unit objects stored in the \$units property, calling the same method on each.

1『这里闻到了「多态」的味道，鸭子理论，因为这些类具有相同的行为 bombardStrength()，所以可以互相替换。（2020-09-10）』

One problematic aspect of the Composite pattern is the implementation of add and remove functionality. The classic pattern places add() and remove() methods in the abstract super class. This ensures that all classes in the pattern share a common interface. As you can see here, though, it also means that leaf classes must provide an implementation:

然后 Army 对象可保存任何类型的 Unit 对象，包括 Army 对象本身或者如 Archer 或 LaserCannonUnit 这样的局部对象。因为所有的部队单位都保证支持 bombardStrength() 方法，所以我们的 Army::bombardStrength() 方法只需遍历 Units 属性，调用每个 Unit 对象的 bombardStrength() 方法，就可以计算出整军队总的攻击强度。组合模式的一个问题是如何实现 add() 和 remove() 方法。一般的组合模式会在抽象超类中添加 add() 和 remove() 方法。这可以确保模式中的所有类都共享同一个接口，但这同时也意味着局部类必须也实现这些方法。

```php
// listing 10.08

class UnitException extends \Exception{}

// listing 10.09

class Archer extends Unit {    
    public function addUnit(Unit $unit) {        
        throw new UnitException(get_class($this) . " is a leaf");    
    }

    public function removeUnit(Unit $unit) {        
        throw new UnitException(get_class($this) . " is a leaf");    
    }

    public function bombardStrength(): int    {       
        return 4;    
    }
}
```

1『这种通过添加「异常」的处理方式，很多地方有看到，值得借鉴。（2020-09-10）』

I do not want to make it possible to add a Unit object to an Archer object, so I throw exceptions if addUnit() or removeUnit() are called. I will need to do this for all leaf objects, so I could perhaps improve my design by replacing the abstract addUnit()/removeUnit() methods in Unit with default implementations like the one in the preceding example:

```php
// listing 10.10

abstract class Unit { 
   
    public function addUnit(Unit $unit) {        
        throw new UnitException(get_class($this) . " is a leaf");    
    }

    public function removeUnit(Unit $unit) {        
        throw new UnitException(get_class($this) . " is a leaf");    
    }

    abstract public function bombardStrength(): int;
}

// listing 10.11

class Archer extends Unit {    
        public function bombardStrength(): int {        
            return 4;    
        }
}
```

This removes duplication in leaf classes, but has the drawback that a composite is not forced at compile time to provide an implementation of addUnit() and removeUnit(), which could cause problems down the line. I will look in more detail at some of the problems presented by the Composite pattern in the next section. Let’s end this section by examining some of its benefits:

这样做可以去除局部类中的重复代码，但是同时组合类不再需要强制性地实现 addUnit() 和  removeUnit() 方法了，这可能会带来问题。在下一节中，我们会深入讨论组合模式所带来的一些问题。现在先让我们回顾一下组合模式所带来的益处。

1. Flexibility: Because everything in the Composite pattern shares a common supertype, it is very easy to add new composite or leaf objects to the design without changing a program’s wider context.

2. Simplicity: A client using a Composite structure has a straightforward interface. There is no need for a client to distinguish between an object that is composed of others and a leaf object (except when adding new components). A call to Army::bombardStrength() may cause a cascade of delegated calls behind the scenes; but to the client, the process and result are exactly equivalent to those associated with calling Archer::bombardStrength().

3. Implicit reach: Objects in the Composite pattern are organized in a tree. Each composite holds references to its children. An operation on a particular part of the tree, therefore, can have a wide effect. We might remove a single Army object from its Army parent and add it to another. This simple act is wrought on one object, but it has the effect of changing the status of the Army object’s referenced Unit objects and of their own children.

4. Explicit reach: Tree structures are easy to traverse. They can be iterated in order to gain information or to perform transformations. We will look at a particularly powerful technique for this in the next chapter when we deal with the Visitor pattern.

1、灵活：因为组合模式中的一切类都共享了同一个父类型，所以可以轻松地在设计中添加新的组合对象或者局部对象，而无需大范围地修改代码。

2、简单：使用组合结构的客户端代码只需设计简单的接口。客户端代码没有必要区分一个对象是组合对象还是局部对象（除了添加新组件时）。客户端代码调用 Army::bombardStrength() 方法时也许会产生一些幕后的委托调用，但是对于客户端代码而言，无论是过程还是效果，都和调用 Army::bombardStrength() 方法是完全相同的。

3、隐式到达：组合模式中的对象通过树型结构组织。每个组合对象中都保存着对子对象的引用。因此对树中某部分的一个小操作可能会产生很大的影响。比如我们可能会将一个父 Army 对象的某个子 Army 对象删除，并将其添加到另外一个父 Army 对象上去。这个简单的动作看似只对子 Army 对象产生作用，但实际上却影响了子 Army 对象中所引用的 unit 对象及其子对象的状态。

4、显式到达：树型结构可轻松遍历。可以通过迭代树型结构来获取组合对象和局部对象的信息，或对组合对象和局部对象执行批量处理。在下一章中，我们在处理访问者模式时会看到一个与此相关的强大技术。

Often, you really see the benefit of a pattern only from the client’s perspective, so here are a couple of armies:

```php
// listing 10.12

// create an army
$main_army = new Army();

// add some units
$main_army->addUnit(new Archer());
$main_army->addUnit(new LaserCannonUnit());

// create a new army
$sub_army = new Army();

// add some units
$sub_army->addUnit(new Archer());
$sub_army->addUnit(new Archer());
$sub_army->addUnit(new Archer());

// add the second army to the first
$main_army->addUnit($sub_army);

// all the calculations handled behind the scenes
print "attacking with strength: {$main_army->bombardStrength()}\n";
```

I create a new Army object and add some primitive Unit objects. I repeat the process for a second Army object that I then add to the first. When I call Unit::bombardStrength() on the first Army object, all the complexity of the structure that I have built up is entirely hidden.

#### 4.2.3 Consequences

If you’re anything like me, you would have heard alarm bells ringing when you saw the code extract for the Archer class. Why do we put up with these redundant addUnit() and removeUnit() methods in leaf classes that do not need to support them? An answer of sorts lies in the transparency of the Unit type.

If a client is passed a Unit object, it knows that the addUnit() method will be present. The Composite pattern principle that primitive (leaf) classes have the same interface as composites is upheld. This does not actually help you much because you still do not know how safe you might be calling addUnit() on any Unit object you might come across.

If I move these add/remove methods down so that they are available only to composite classes, then passing a Unit object to a method leaves me with the problem that I do not know by default whether or not it supports addUnit(). Nevertheless, leaving booby-trapped methods lying around in leaf classes makes me uncomfortable. It adds no value and confuses a system’s design because the interface effectively lies about its own functionality.

你也许会像我一样，在看到 Archer 类的代码时就想起了警报——为什么我们要把 addUnit() 和 removeUnit() 这样的冗余方法加到并不需要它们的局部类中？答案在于 Unit 类型的透明性。客户端代码在得到一个 Unit 对象时，知道其中一定包含 addUnit() 方法。组合模式的原则便是局部类和组合类具有同样的接口。不过这未必能真正帮助我们，因为我们仍然不知道调用 Unit 对象的 addUnit() 方法是否安全。如果我们将 add / remove 方法降到下一级对象中，以便这些方法仅在组合类中使用，那么又会产生另一个问题——使用 Unit 对象时，我们并不知道该对象是否默认支持 addUnit() 方法。但是，将冗余的类方法留在局部类中让人感到不舒服。这样做毫无意义而且给系统设计带来歧义，因为接口应该关注于自己独有的功能。

You can split composite classes off into their own CompositeUnit subtype quite easily. First of all, I excise the add/remove behavior from Unit:

```php
// listing 10.13

abstract class Unit {    
    public function getComposite() {        
        return null;    
    }

    abstract public function bombardStrength(): int;
}
```

Notice the new getComposite() method. I will return to this in a little while. Now, I need a new abstract class to hold addUnit() and removeUnit(). I can even provide default implementations:

1『拥有 addUnit() 和 removeUnit() 方法的抽象类，这里指的是 CompositeUnit，即一个「接口」。（2020-09-10）』

注意一下新增的 getComposite() 方法，不过我们稍后再来看这个方法。现在我们需要个新的拥有 addUnit() 和 removeUnit() 方法的抽象类。我们甚至可以给这两个方法加上默认实现：

```php
// listing 10.14

abstract class CompositeUnit extends Unit {    
    private $units = [];

    public function getComposite(): CompositeUnit    {        
        return $this;    
    }

    public function addUnit(Unit $unit) {        
        if (in_array($unit, $this->units, true)) {            
            return;        
        }
        $this->units[] = $unit;    
    }
    
    public function removeUnit(Unit $unit) {        
        $idx = array_search($unit, $this->units, true);        
        if (is_int($idx)) {            
            array_splice($this->units, $idx, 1, []);        
        }    
    }

    public function getUnits(): array {       
        return $this->units;    
    }
}
```

The CompositeUnit class is declared abstract, even though it does not itself declare an abstract method. It does, however, extend Unit, and it does not implement the abstract bombardStrength() method. Army (and any other composite classes) can now extend CompositeUnit. The classes in my example are now organized as in Figure 10-2.

Figure 10-2.  Moving add/remove methods out of the base class

The annoying, useless implementations of add/remove methods in the leaf classes are gone, but the client must still check to see whether it has a CompositeUnit before it can use addUnit().

This is where the getComposite() method comes into its own. By default, this method returns a null value. Only in a CompositeUnit class does it return CompositeUnit. So if a call to this method returns an object, we should be able to call addUnit() on it. Here’s a client that uses this technique:

1『方法 getComposite() 是点睛之笔！（2020-09-10）』

因为 CompositeUnit 类继承自 Unit 类，并没有实现抽象的 bombardStrength() 方法，所以  CompositeUnit 类也被声明为抽象的，虽然它本身并没有抽象方法。Army 类（或任何其他组合类）现在可扩展 CompositeUnit 了，而我们示例中的类现在将以图 10-2 的形式来组织。虽然我们删除了局部类中冗余、烦人的 add / remove 方法，但客户端代码在使用 addUnit() 方法前却仍必须检查对象是否为一个 CompositeUnit 类型的对象。

这就是添加 getComposite() 方法的原因。该方法默认返回一个 null 值，它仅在 CompositeUnit 类中才返回 CompositeUnit 本身。所以如果该方法返回一个对象，那么便可以调用它的  addUnit() 方法。下面是使用这种思路的客户端代码：

```php
// listing 10.15

class UnitScript {    
    public static function joinExisting (Unit $newUnit, Unit $occupyingUnit): CompositeUnit {        
        $comp = $occupyingUnit->getComposite();        
        if (! is_null($comp)) {            
            $comp->addUnit($newUnit);        
        } else {        
            $comp = new Army();
            $comp->addUnit($occupyingUnit);            
            $comp->addUnit($newUnit);        
            }        
        return $comp;    
    }
}
```

The joinExisting() method accepts two Unit objects. The first is a newcomer to a tile, and the second is a prior occupier. If the second Unit is a CompositeUnit, then the first will attempt to join it. If not, then a new Army will be created to cover both units. I have no way of knowing at first whether the \$occupyingUnit argument contains a CompositeUnit. A call to getComposite() settles the matter, though. If getComposite() returns an object, I can add the new Unit object to it directly. If not, I create the new Army object and add both.

I could simplify this model further by having the Unit::getComposite() method return an Army object prepopulated with the current Unit. Or I could return to the previous model (which did not distinguish structurally between composite and leaf objects) and have Unit::addUnit() do the same thing: create an Army object and add both Unit objects to it. This is neat, but it presupposes that you know in advance the type of composite you would like to use to aggregate your units. Your business logic will determine the kinds of assumptions you can make when you design methods like getComposite() and addUnit().

These contortions are symptomatic of a drawback to the Composite pattern. Simplicity is achieved by ensuring that all classes are derived from a common base. The benefit of simplicity is sometimes bought at a cost to type safety. The more complex your model becomes, the more manual type checking you are likely to have to do. Let’s say that I have a Cavalry object. If the rules of the game state that you cannot put a horse on a troop carrier, I have no automatic way of enforcing this with the Composite pattern:

joinExisting() 方法有两个 Unit 对象参数。第一个参数是一个区块的新来者，第二个参数是之前的占据者。如果第二个 Unit 对象是一个 CompositeUnit 对象，那么第一个 Unit 对象被添加给它。但如果不是的话，方法将会创建一个新 Army 对象并将这两个对象添加到 Army 对象中。我们一开始并不知道 occupyingUnit 参数是否包含 CompositeUnit 对象，但是通过调  getComposite() 可以解决这个问题。若 getComposite() 返回对象，那么我们可以直接添加新的 Unit 对象。如果不是，那么我们创建一个新的 Army 象，并将两个 Unit 对象都添加给它。

我们还可以进一步简化该模型，让 Unit::getComposite() 方法返回一个添加当前 Unit 的 Army 对象。或者也可以返回前面的模型（即不从结构上区分组合或局部对象），并用 Unit::addUnit() 方法来做同样的事情：创建一个 Army 对象，并将两个 Unit 对象都添加给它。虽然这样代码很简洁，但是这假设你已经预先知道了部队单元所要聚合的组合类型。当你设计如  getComposite() 和 addUnit() 这样的方法时，业务逻辑将决定你所能做的假设。

而这正是组合模式缺陷的症状之一。简化的前提是使所有的类都继承同一个基类。简化的好处有时会以降低对象类型安全为代价。模型变得越复杂，你就不得不手动进行越多的类型检査。比如有一个 Cavalry（骑兵）对象，假设游戏规则规定不能将一匹马放到运兵船上，在组合模式中我们并没有自动化的方式来强制执行这个规则。

```php
// listing 10.16

class TroopCarrier extends CompositeUnit {    
    public function addUnit(Unit $unit) {        
        if ($unit instanceof Cavalry) {            
            throw new UnitException("Can't get a horse on the vehicle");        
        }        
        parent::addUnit($unit);    
    }

    public function bombardStrength(): int {        
        return 0;    
    }
}
```

I am forced to use the instanceof operator to test the type of the object passed to addUnit(). If you have too many special cases of this kind, the drawbacks of the pattern begin to outweigh its benefits. Composite works best when most of the components are interchangeable.

Another issue to bear in mind is the cost of some Composite operations. The Army::bombardStrength() method is typical in that it sets off a cascade of calls to the same method down the tree. For a large tree with lots of subarmies, a single call can cause an avalanche behind the scenes. bombardStrength() is not itself very expensive, but what would happen if some leaves performed a complex calculation to arrive at their return values? One way around this problem is to cache the result of a method call of this sort in the parent 

object, so that subsequent invocations are less expensive. You need to be careful, though, to ensure that the cached value does not grow stale. You should devise strategies to wipe any caches whenever any operations take place on the tree. This may require that you give child objects references to their parents.

这里我们不得不使用 instanceof 操作符来检査传给 addUnit() 方法的对象类型。特殊对象越来越多，组合模式开始渐渐显得弊大于利。在大部分局部对象可互换的情况下，组合模式才最适用。需要担心的另外一个问题是组合操作的成本。Army::bombardStrength() 方法便是典型的例子，该方法会逐级调用对象树中下级分支的方法。如果一个对象树中有大量子 Army 对象，一个简单的调用可能会导致系统崩溃。虽然 bombardStrength() 方法自身并不一定会带来多大的系统开销，但是如果一些局部对象为了获得返回值而执行一系列复杂的计算，那么会发生什么呢？解决问题的一个办法是在父级对象中缓存计算结果，这样可使接下来的调用减少系统开销。尽管如此，你还是需要小心地保证缓存值不会失效。因此你需要设计一个当对树进行操作时可移除过期缓存的策略，而这也许会要求你给子对象加上对父对象的引用。

1『确实，所以使用组合模式的前提是，树形对象结构。（2020-09-10）』

Finally, a note about persistence. The Composite pattern is elegant, but it doesn’t lend itself neatly to storage in a relational database. This is because, by default, you access the entire structure only through a cascade of references. To construct a Composite structure from a database in the natural way, you would have to make multiple expensive queries. You can get around this problem by assigning an ID to the whole tree, so that all components can be drawn from the database in one go. Having acquired all the objects, however, you would still have the task of recreating the parent/child references, which themselves would have to be stored in the database. This is not difficult, but it is somewhat messy.

Although Composites sit uneasily with relational databases, they lend themselves very well indeed to storage in XML. This is because XML elements are often themselves composed of trees of subelements.

Composite in SummarySo the Composite pattern is useful when you need to treat a collection of things in the same way as you would an individual, either because the collection is intrinsically like a component (armies and archers), or because the context gives the collection the same characteristics as the component (line items in an invoice). Composites are arranged in trees, so an operation on the whole can affect the parts, and data from the parts is transparently available via the whole. The Composite pattern makes such operations and queries transparent to the client. Trees are easy to traverse (as we shall see in the next chapter). It is easy to add new component types to Composite structures.

On the downside, Composites rely on the similarity of their parts. As soon as we introduce complex rules as to which composite object can hold which set of components, our code can become hard to manage. Composites do not lend themselves well to storage in relational databases, but are well suited to XML persistence.

最后，在对象持久化上需要注意一些地方。虽然组合模式是一个优雅的模式，但它并不能将自身轻松地存储到关系数据库里。这是因为在默认的情况下，你是通过级联引用来访问整个结构的。因此，按正常的途径从数据库构造一个组合结构，你将不得不使用多个昂贵的查询。我们可以通过给对象树中的每个节点赋于 ID 值来避免这个问题，于是所有组件都可从数据库中一次性取出。但是获得这些对象后，我们仍旧需要重建父子之间的引用关系，以便它们再保存回数据库虽然这不难，可并不优雅，甚至有些混乱。虽然组合模式难以使数据保存在关系型数据库中，但其数据却非常适合持久化为 XML。这是因为 XML 元素通常是由树型结构的子元素组合而成的。

### 4.3 The Decorator Pattern

While the Composite pattern helps us to create a flexible representation of aggregated components, the Decorator pattern uses a similar structure to help us to modify the functionality of concrete components. Once again, the key to this pattern lies in the importance of composition at runtime. Inheritance is a neat way of building on characteristics laid down by a parent class. This neatness can lead you to hard-code variation into your inheritance hierarchies, often causing inflexibility.

组合模式帮助我们聚合组件，而装饰模式则使用类似结构来帮助我们改变具体组件的功能。该模式同样体现了组合的重要性，但组合是在代码运行时实现的。继承是共享父类特性的一种简单的办法，但可能会使你将需要改变的特性硬编码到继承体系中，而这常会降低系统灵活性。

#### 4.3.1 The Problem

Building all your functionality into an inheritance structure can result in an explosion of classes in a system. Even worse, as you try to apply similar modifications to different branches of your inheritance tree, you are likely to see duplication emerge.

将所有功能建立在继承体系上会导致系统中的类「爆炸式」增多。更糟糕的是，当你尝试对继承树上不同的分支做相似的修改时，代码可能会产生重复。

Let’s return to our game. Here, I define a Tile class and a derived type:


```php
// listing 10.17

abstract class Tile {    
    abstract public function getWealthFactor(): int;
}

// listing 10.18

class Plains extends Tile {    
    private $wealthfactor = 2;

    public function getWealthFactor(): int {        
        return $this->wealthfactor;    
    }
}
```

A tile represents a square on which my units might be found. Each tile has certain characteristics. In this example, I have defined a getWealthFactor() method that affects the revenue a particular square might generate if owned by a player. As you can see, Plains objects have a wealth factor of 2. Obviously, tiles manage other data. They might also hold a reference to image information, so that the board can be drawn. Once again, I’ll keep things simple here.

I need to modify the behavior of the Plains object to handle the effects of natural resources and human abuse. I wish to model the occurrence of diamonds on the landscape, and the damage caused by pollution. One approach might be to inherit from the Plains object:

我们定义了ー个 tile 类。tile 表示部队单元所在的一个区域。每个 tile 对象都有明确的特征。在本例中，我们定义了一个 getWealthFactor() 方法，用于计算当某个特定区域被一个玩家所占有后的收益。如你所见，Plains（平原）对象的财富系数是 2。显然，tile 对象还管理其他数据。它们也许会有对图片的引用，用于在屏幕上绘图。这里我们还是先保持简单。我们还需要修改 Pains 对象的行为，用于处理一些自然资源和人类滥用的效果。我们希望为地表钻石的分布和污染造成的破坏建模。有一个办法是从 Pains 对象派生：

```php
// listing 10.19

class DiamondPlains extends Plains {    
    public function getWealthFactor(): int {        
        return parent::getWealthFactor() + 2;    
    }
}

// listing 10.20

class PollutedPlains extends Plains {    
    public function getWealthFactor(): int {        
        return parent::getWealthFactor() - 4;    
    }
}
```

I can now acquire a polluted tile very easily:

```php
// listing 10.21

$tile = new PollutedPlains();
print $tile->getWealthFactor();
```

You can see the class diagram for this example in Figure 10-3.

Figure 10-3.  Building variation into an inheritance tree

This structure is obviously inflexible. I can get plains with diamonds. I can get polluted plains. But can I get them both? Clearly not, unless I am willing to perpetrate the horror that is PollutedDiamondPlains. This situation can only get worse when I introduce the Forest class, which can also have diamonds and pollution.

This is an extreme example, of course, but the point is made. Relying entirely on inheritance to define your functionality can lead to a multiplicity of classes and a tendency toward duplication.

Let’s take a more commonplace example at this point. Serious web applications often have to perform a range of actions on a request before a task is initiated to form a response. You might need to authenticate the user, for example, and to log the request. Perhaps you should process the request to build a data structure from raw input. Finally, you must perform your core processing. You are presented with the same problem.

You can extend the functionality of a base ProcessRequest class with additional processing in a derived LogRequest class, in a StructureRequest class, and in an AuthenticateRequest class. You can see this class hierarchy in Figure 10-4.

Figure 10-4.  More hard-coded variations

What happens, though, when you need to perform logging and authentication, but not data preparation? Do you create a LogAndAuthenticateProcessor class? Clearly, it is time to find a more flexible solution.

关于这个问题，我们再举一个更真实的例子。真正的 Web 应用要在返回响应给用户之前执行一系列操作，例如验证用户及记录请求等。也许还需要将请求中的原始输入处理成某种数据结构。最后，还必须执行核心操作。此时我们遇到了同样的问题。在派生的 LogRequest 类、StructureRequest 类和 AuthenticateRequest 类中，我们可以对基类 ProcessRequest 类的功能进行扩展，并加上额外的处理。你可以在图 10-4 中看到该层级关系。但是当需要执行记录和验证，而不需要准备数据时，该怎么办？创建一个 LogAndAuthenticateProcessor 类？显然，我们必须找出一个更灵活的方案。

#### 4.3.2 Implementation

Rather than use only inheritance to solve the problem of varying functionality, the Decorator pattern uses composition and delegation. In essence, Decorator classes hold an instance of another class of their own type. A Decorator will implement an operation so that it calls the same operation on the object to which it has a reference before (or after) performing its own actions. In this way, it is possible to build a pipeline of Decorator objects at runtime.

1『装饰者模式，其实就是「组合优于继承」的一种具体实现方法。（2020-09-10）』

装饰模式使用组合和委托而不是只使用继承来解决功能变化的问题。实际上，Decorator 类会持有另外一个类的实例。Decorator 对象会实现与被调用对象的方法相对应的类方法。用这种办法可以在运行时创建一系列的 Decorator 对象。

Let’s rewrite our game example to illustrate this:

```php
abstract class Tile {    
    abstract public function getWealthFactor(): int;
}

class Plains extends Tile {    
    private $wealthfactor = 2;

    public function getWealthFactor(): int    {        
        return $this->wealthfactor;    
    }
}

// listing 10.22

abstract class TileDecorator extends Tile {    
    protected $tile;

    public function __construct(Tile $tile)    {        
        $this->tile = $tile;    
    }
}
```

Here, I have declared Tile and Plains classes as before, but I have also introduced a new class: TileDecorator. This does not implement getWealthFactor(), so it must be declared abstract. I define a constructor that requires a Tile object, which it stores in a property called \$tile. I make this property protected so that child classes can gain access to it. Now I’ll redefine the Pollution and Diamond classes:

1『子类继承一个抽象父类，如果该子类也是抽象类的话，就不需要实现抽象父类里的抽象方法了。（2020-09-10）』

```php
// listing 10.23

class DiamondDecorator extends TileDecorator {    
    public function getWealthFactor(): int {
        return $this->tile->getWealthFactor() + 2;    
    }
}

// listing 10.24

class PollutionDecorator extends TileDecorator {    
    public function getWealthFactor(): int {        
        return $this->tile->getWealthFactor() - 4;    
    }
}
```

Each of these classes extends TileDecorator. This means that they have a reference to a Tile object. When getWealthFactor() is invoked, each of these classes invokes the same method on its Tile reference before making its own adjustment. By using composition and delegation like this, you make it easy to combine objects at runtime. 

Because all the objects in the pattern extend Tile, the client does not need to know which combination it is working with. It can be sure that a getWealthFactor() method is available for any Tile object, whether it is decorating another behind the scenes or not:

这些类都扩展自 TileDecorator 类，这意味着它们拥有指向 Tile 对象的引用。当 getWealthFactor() 方法被调用时，这些类都会先调用所引用的 Tile 对象的 getWealthFactor() 方法，然后执行自己特有的操作。通过像这样使用组合和委托，可以在运行时轻松地合并对象。因为模式中所有的对象都扩展自 Tile，所以客户端代码并不需要知道内部是如何合并的。getWealthFactor() 方法在任何 Tile 对象中都是可用的，无论该对象是一个装饰器对象还是真正的 Tile 对象。

```php
// listing 10.25

$tile = new Plains();
print $tile->getWealthFactor(); // 2
```

Plains is a component. It simply returns 2:

```php
// listing 10.26

$tile = new DiamondDecorator(new Plains());
print $tile->getWealthFactor(); // 4
```

DiamondDecorator has a reference to a Plains object. It invokes getWealthFactor() before adding its own weighting of 2:

```php
// listing 10.27

$tile = new PollutionDecorator(new DiamondDecorator(new Plains()));
print $tile->getWealthFactor(); // 0
```

PollutionDecorator has a reference to a DiamondDecorator object, which has its own Tile reference.You can see the class diagram for this example in Figure 10-5.

Figure 10-5.  The Decorator pattern

This model is very extensible. You can add new decorators and components very easily. With lots of decorators, you can build very flexible structures at runtime. The component class, Plains in this case, can be significantly modified in many ways without the need to build the totality of the modifications into the class hierarchy. In plain English, this means you can have a polluted Plains object that has diamonds, without having to create a PollutedDiamondPlains object.

The Decorator pattern builds up pipelines that are very useful for creating filters. The java.io package makes great use of decorator classes. The client coder can combine decorator objects with core components to add filtering, buffering, compression, and so on to core methods like read(). My web request example can also be developed into a configurable pipeline. Here’s a simple implementation that uses the Decorator pattern:

这样的模型极具扩展性。我们可以非常轻松地添加新的装饰器或者新的组件。通过使用大量的装饰器，我们可以在运行时创建极为灵活的结构。本例中的组件类 Pains 的行为可以很方便地被改变，而不需要改动原来的类。通俗地说，这意味着不需要创建 PollutedDiamondPlains 对象，就可以构造一个拥有钻石并被污染的 Plains 对象。

饰模式所建立的管道对于创建过滤器非常有用。Java 的 IO 包便广泛使用了装饰器类。客户端程序员可将核心组件与装饰对象合并，从而对核心方法（如 read() 进行过滤、缓冲、压缩等操作。我们的 Web 请求示例也能被开发为一个具有可配置管道的模型。下面便是使用装饰模式的一个简单实现。

```php
// listing 10.28

class RequestHelper{}

// listing 10.29

abstract class ProcessRequest {    
    abstract public function process(RequestHelper $req);
}

// listing 10.30

class MainProcess extends ProcessRequest {    
    public function process(RequestHelper $req) {        
        print __CLASS__ . ": doing something useful with request\n";
    }
}

// listing 10.31

abstract class DecorateProcess extends ProcessRequest {    
    protected $processrequest;

    public function __construct(ProcessRequest $pr)    {        
    $this->processrequest = $pr;    
    }
}
```

As before, we define an abstract superclass (ProcessRequest), a concrete component (MainProcess), and an abstract decorator (DecorateProcess). MainProcess::process() does nothing but report that it has been called. DecorateProcess stores a ProcessRequest object on behalf of its children. Here are some simple concrete decorator classes:

```php
// listing 10.32

class LogRequest extends DecorateProcess {    
    public function process(RequestHelper $req) {        
        print __CLASS__ . ": logging request\n";        
        $this->processrequest->process($req);    
    }
}

// listing 10.33

class AuthenticateRequest extends DecorateProcess {    
    public function process(RequestHelper $req) {        
        print __CLASS__ . ": authenticating request\n";        
        $this->processrequest->process($req);    
    }
}

// listing 10.34

class StructureRequest extends DecorateProcess {    
    public function process(RequestHelper $req) {        
        print __CLASS__ . ": structuring request data\n";        
        $this->processrequest->process($req);    
    }
}
```

Each process() method outputs a message before calling the referenced ProcessRequest object’s own process() method. You can now combine objects instantiated from these classes at runtime to build filters that perform different actions on a request, and in different orders. Here’s some code to combine objects from all these concrete classes into a single filter:

装饰类的每个 process() 方法在调用引用的 ProcessRequest 对象的 process() 方法前输出条信息。现在我们可以在运行时合并这些类的初始对象，创建过滤器来对每一个请求按不同的顺序执行不同的操作。下面的代码将所有具体类的对象组合为一个过滤器。

```php
// listing 10.35

$process = new AuthenticateRequest(new StructureRequest(    
                                                            new LogRequest(        
                                                            new MainProcess()    
                                                            )));
$process->process(new RequestHelper());
```

This code gives the following output:

```
popp\ch10\batch07\
Authenticate
Request: authenticating request

popp\ch10\batch07\
StructureRequest: structuring request data

popp\ch10\batch07\
LogRequest: logging requestpopp

ch10\batch07\
MainProcess: doing something useful with request
```

■ Note: this example is, in fact, also an instance of an enterprise pattern called intercepting filter. intercepting filter is described in Core J2EE Patterns: Best Practices and Design Strategies (prentice hall, 2001) by alur et al.

#### 4.3.3 Consequences

Like the Composite pattern, Decorator can be confusing. It is important to remember that both composition and inheritance are coming into play at the same time. So LogRequest inherits its interface from ProcessRequest, but it is acting as a wrapper around another ProcessRequest object.

Because a decorator object forms a wrapper around a child object, it helps to keep the interface as sparse as possible. If you build a heavily featured base class, then decorators are forced to delegate to all public methods in their contained object. This can be done in the abstract decorator class, but it still introduces the kind of coupling that can lead to bugs.

1『装饰者模式中，装饰类一定要简单，里面的方法要少，可以用一个简单的抽象类来作为装饰类。（2020-09-10）』

Some programmers create decorators that do not share a common type with the objects they modify. As long as they fulfill the same interface as these objects, this strategy can work well. You get the benefit of being able to use the built-in interceptor methods to automate delegation (implementing \_\_call() to catch calls to nonexistent methods and invoking the same method on the child object automatically). However, by doing this, you also lose the safety afforded by class type checking. In our examples so far, client code can demand a Tile or a ProcessRequest object in its argument list and be certain of its interface, whether or not the object in question is heavily decorated.

和组合模式一样，裝饰模式有时也会令人困惑。一定要记住：组合和继承通常都是同时使用的。因此，LogRequest 是继承自 ProcessRequest 的，但是却表现为对另外一个 ProcessRequest 对象的封装。因为裝饰对象作为子对象的包装，所以保持基类中的方法尽可能少是很重要的。如果一个基类具有大量特性，那么装饰对象不得不为它们包装的对象的所有 public 方法加上委托。你可以用一个抽象的装饰类来实现，不过这仍旧会带来耦合，并可能导致 bug 的出现。

有些程序员创建的装饰类与其中拥有的对象并不共享相同的对象类型。只要这些装饰类提供相同的接口，这个策略也是可行的。使用 PHP 内建的拦截方法来实现自动委托，可以带来很多好处（如通过实现 \_\_call() 方法来捕捉装饰类中不存在的方法，并自动调用子对象对应的相同的方法）。但是，这样的话会丧失类型检査带来的安全性。就我们的例子来说，客户端代码要求传入的参数是一个 Tile 或 ProcessRequest 对象，并能确定该对象可以提供某些接口，无论传入的对象是否经过大量装饰。

### 4.4 The Facade Pattern

You may have had occasion to stitch third-party systems into your own projects in the past. Whether or not the code is object oriented, it will often be daunting, large, and complex. Your own code, too, may become a challenge to the client programmer who needs only to access a few features. The Facade pattern is a way of providing a simple, clear interface to complex systems.

可能你曾经有过在项目中集成第三方代码的经历。无论第三方代码是否面向对象，集成通常都是巨大而且复杂的工作，很容易让人畏缩。而对一个客户程序员来说，你的代码也可能是一个挑战，即使他可能仅需要访问很小一部分特性。外观模式可以为复杂系统创建一个简单、清晰的接口。

#### 4.4.1 The Problem

Systems tend to evolve large amounts of code that is really only useful within the system itself. Just as classes define clear public interfaces and hide their guts away from the rest of the world, so should well-designed systems. However, it is not always clear which parts of a system are designed to be used by client code and which are best hidden.

As you work with subsystems (like web forums or gallery applications), you may find yourself making calls deep into the logic of the code. If the subsystem code is subject to change over time, and your code interacts with it at many different points, you may find yourself with a serious maintenance problem as the subsystem evolves.

Similarly, when you build your own systems, it is a good idea to organize distinct parts into separate tiers. Typically, you may have a tier responsible for application logic, another for database interaction, another for presentation, and so on. You should aspire to keep these tiers as independent of one another as you can, so that a change in one area of your project will have minimal repercussions elsewhere. If code from one tier is tightly integrated into code from another, then this objective is hard to meet.

Here is some deliberately confusing procedural code that makes a song-and-dance routine of the simple process of getting log information from a file and turning it into object data:

在系统中总会逐渐形成大量仅在系统自身内部有用的代码。系统也应该像类那样，提供定义清晰的公共接口，并对外隐藏内部结构。但是，系统中哪部分应该设置为公开，哪部分设置为隐藏并不容易决定。当使用子系统（如 Web 论坛或者图库）的代码时，你也许会发现自己过于深入地调用子系统的逻辑代码。如果子系统代码总是在不断变化，而你的代码却又在许多不同地方与子系统代码交互，那么随着子系统的发展，你也许会发现维护代码变得非常困难。

类似地，当你创建自己的系统时，将不同的部分分层是很好的做法。例如，你可能会把系统分为应用逻辑层、数据库交互层和表现层等。你应该尽可能地使这些分层互相独立，以便项目中某一部分的修改尽量不影响到其他地方。如果某层中的代码与另一层的代码存在耦合的话，那么这个目标就很难达成了。下面是一些故意让人混淆的不着边际的程序代码，其功能只是从文件中获取 log 信息并将它转换为对象数据。

```php
// listing 10.36

function getProductFileLines($file) {    
    return file($file);
}

function getProductObjectFromId($id, $productname) {    
    // some kind of database lookup    
    return new Product($id, $productname);
}

function getNameFromLine($line) {    
    if (preg_match("/.*-(.*)\s\d+/", $line, $array)) {        
        return str_replace('_', ' ', $array[1]);    
    }    
    return '';
}

function getIDFromLine($line) {    
    if (preg_match("/^(\d{1,3})-/", $line, $array)) {        
        return $array[1];    
    }    
    return -1;
}

class Product {    
    public $id;    
    public $name;

    public function __construct($id, $name) {        
        $this->id = $id;        
        $this->name = $name;    
    }
}
```

Let’s imagine that the internals of this code are more complicated than they actually are, and that I am stuck with using it rather than rewriting it from scratch. For example, assume I have to turn a file that contains lines like these into an array of objects:

假设上面代码的内部其实是更复杂的，这样我们可以继续使用它们而非从头开始重写。我们的目的是将包含类似下面数据的文件转换为一个对象数组。而我们必须调用所有这些方法（注意为了简单起见，我们并不计算出价格的最终数字）：

```
234-ladies_jumper 55
532-gents_hat 44
```

To do so, I must call all of these functions (note that, for the sake of brevity, I don’t extract the final number, which represents a price):

```php
// listing 10.37

$lines = getProductFileLines(__DIR__ . '/test2.txt');
$objects = [];
foreach ($lines as $line) {    
    $id = getIDFromLine($line);    
    $name = getNameFromLine($line);    
    $objects[$id] = getProductObjectFromID($id, $name);
}
```

If I call these functions directly like this throughout my project, my code will become tightly wound into the subsystem it is using. This could cause problems if the subsystem changes, or if I decide to switch it out entirely. I really need to introduce a gateway between the system and the rest of our code.

如果在项目中像这样直接调用这些方法，那么我们的代码会和子系统紧紧地耦合在一起。当子系统变化时，或者我们决定将其与子系统完全断开时，代码就会出问题。可见，我们需要在这些子系统和代码中引入一个入口。

#### 4.4.2 Implementation

Here is a simple class that provides an interface to the procedural code you encountered in the previous section:

```php
// listing 10.38

class ProductFacade {    
    private $products = [];

    public function __construct(string $file) {        
        $this->file = $file;        
        $this->compile();    
    }

    private function compile() {        
        $lines = getProductFileLines($this->file);

        foreach ($lines as $line) {            
            $id = getIDFromLine($line);            
            $name = getNameFromLine($line);            
            $this->products[$id] = getProductObjectFromID($id, $name);        
        }    
    }

    public function getProducts(): array    {        
        return $this->products;    
    }

    public function getProduct(string $id): \Product {        
        if (isset($this->products[$id])) {            
            return $this->products[$id];        
        }        
        return null;    
    }
}
```

From the point of view of the client code, access to Product objects from a log file is much simplified:

```php
// listing 10.39

$facade = new ProductFacade(__DIR__ . '/test2.txt');
$object = $facade->getProduct("234");
```

1『门面模式，其实对面向对象编程范式中「封装性」的一个具体应用案例。』

#### 4.4.3 Consequences

A Facade is really a very simple concept. It is just a matter of creating a single point of entry for a tier or subsystem. This has a number of benefits. It helps to decouple distinct areas in a project from one another. It is useful and convenient for client coders to have access to simple methods that achieve clear ends. It reduces errors by focusing the use of a subsystem in one place; changes to the subsystem should cause failure in a predictable location. Errors are also minimized by Facade classes in complex subsystems where client code might otherwise use internal functions incorrectly.

Despite the simplicity of the Facade pattern, it is all too easy to forget to use it, especially if you are familiar with the subsystem you are working with. There is a balance to be struck, of course. On the one hand, the benefit of creating simple interfaces to complex systems should be clear. On the other hand, one could abstract systems with reckless abandon, and then abstract the abstractions. If you are making significant simplifications for the clear benefit of client code, and/or shielding it from systems that might change, then you are probably right to implement the Facade pattern.

外观模式是一个十分简单的概念，它只是为一个分层或一个子系统创建一个单一的入口。这会带来许多好处。首先，有助于分离项目中的不同部分。其次，对于客户端开发者来说，访问代码变得简洁，非常方便。另外，由于只在一个地方调用子系统，减少了出错的可能性，并因此可以预估子系统修改带来的问题所在。Facades 类还能使客户端代码避免不正确地使用子系统中复杂的内部方法，从而减少错误的发生。

尽管外观模式十分简单，但你很容易忘记它，特别是在你熟悉所使用的子系统时。这里存在着某种平衡。一方面，为复杂系统创建简单接口的好处是明显的；另一方面，你可能会过度抽象系统。总之，如果你想获得简洁的客户端访问代码，或者想把系统中的修改对客户端代码隐藏，那么你也许应该实现外观模式。

## 0205. Performing and Representing Tasks

In this chapter, I wrapped up my examination of the Gang of Four patterns, placing a strong emphasis on how to get things done. I began by showing you how to design a mini-language and build its engine with the Interpreter pattern.

In the Strategy pattern, you encountered another way of using composition to increase flexibility and reduce the need for repetitive subclassing. And with the Observer pattern, you learned how to solve the problem of notifying disparate and varying components about system events. You also revisited the Composite example; and with the Visitor pattern, learned how to pay a call on, and apply many operations to, every component in a tree. You even saw how the Command pattern can help you to build an extensible tiered system. Finally, you saved yourself a heap of checking for nulls with the Null Object pattern. In the next chapter, I will step further beyond the Gang of Four to examine some patterns specifically oriented toward enterprise programming.

在本章中，我们结了对《设计模式》一书中模式的研究。我们用解释器模式设计了一个迷你语言并创建了该语言的引擎；使用了策略模式（另一种使用组合的方式）来增加系统灵活性并减少对于重复子类的需要；使用了观察者模式解决了将系统事件通知到多个不同组件的问题；也重新回顾了组合模式的示例，并通过访问者模式学习了如何在对象树中访问每个节点元素，并对它们执行多种操作；最后看到了命令模式如何帮助我们建立一个具有扩展性的多层系统。在下一章中，我们会介绍《设计模式》ー书中未提及的一些模式，特别是面向企业应用的设计模式。

In this chapter, we get active. I look at patterns that help you to get things done, whether interpreting a mini-language or encapsulating an algorithm.

This chapter will walk you through several patterns: 1) The Interpreter pattern: Building a mini-language interpreter that can be used to create scriptable applications. 2) The Strategy pattern: Identifying algorithms in a system and encapsulating them into their own types. 3) The Observer pattern: Creating hooks for alerting disparate objects about system events. 4) The Visitor pattern: Applying an operation to all the nodes in a tree of objects. 5) The Command pattern: Creating command objects that can be saved and passed around. 6) The Null Object pattern: Using non-operational objects in place of null values.
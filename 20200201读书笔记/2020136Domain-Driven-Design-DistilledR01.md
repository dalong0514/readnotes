Copyright © 2016 Pearson Education, Inc.

## 记忆时间

## 0101. DDD for Me

You want to improve your craft and to increase your success on projects. You are eager to help your business compete at new heights using the software you create. You want to implement software that not only correctly models your business’s needs but also performs at scale using the most advanced software architectures. Learning Domain-Driven Design (DDD), and learning it quickly, can help you achieve all of this and more.

DDD is a set of tools that assist you in designing and implementing software that delivers high value, both strategically and tactically. Your organization can’t be the best at everything, so it had better choose carefully at what it must excel. The DDD strategic development tools help you and your team make the competitively best software design choices and integration decisions for your business. Your organization will benefit most from software models that explicitly reflect its core competencies. The DDD tactical development tools can help you and your team design useful software that accurately models the business’s unique operations. Your organization should benefit from the broad options to deploy its solutions in a variety of infrastructures, whether in house or in the cloud. With DDD, you and your team can be the ones to bring about the most effective software designs and implementations needed to succeed in today’s competitive business landscape.

DDD 同时提供了战略和战术上的建模工具，来帮助你设计和实现高价值的软件。你的组织无法在所有方面都出类拔萃，所以最好谨慎地识别其真正的优势所在。DDD 的战略设计工具可以帮助你和你的团队做出最有竟争力的软件设计选择和业务整合决策。你的组织将从这些明确反映其核心业务竟争力的软件模型中获得最大的收益。DDD 的战术实施工具可以帮助你和你的团队设计出实用的软件，它能对业务独一无二的运作方式进行精准地建模。你的组织可以有更多的选择，把解决方案部署到各种不同的基础设施中，不管这些基础设施是位于企业内部还是在公有云上，你的组织都会受益匪浅。借助 DDD，你的团队可以在当今竞争激烈的商业环境中持续地交付最有效的软件设计与实现。

In this book I have distilled DDD for you, with condensed treatment of both the strategic and tactical modeling tools. I understand the unique demands of software development and the challenges you face as you work to improve your craft in a fast-paced industry. You can’t always take months to read up on a subject like DDD, and yet you still want to put DDD to work as soon as possible.

I am the author of the best-selling book Implementing Domain-Driven Design [IDDD] , and I have also created and teach the three-day IDDD Workshop. And now I have also written this book to bring you DDD in an aggressively condensed form. It’s all part of my commitment to bringing DDD to every software development team, where it deserves to be. My goal, of course, includes bringing DDD to you.

### 1.1 Will DDD Hurt?

You may have heard that DDD is a complicated approach to software development. Complicated? It certainly is not complicated of necessity. Indeed, it is a set of advanced techniques to be used on complex software projects. Due to its power and how much you have to learn, without expert instruction it can be daunting to put DDD into practice on your own. You have probably also found that some of the other DDD books are many hundreds of pages long and far from easy to consume and apply. It required a lot of words for me to explain DDD in great detail in order to provide an exhaustive implementation reference on more than a dozen DDD topics and tools. That effort resulted in Implementing Domain-Driven Design [IDDD] . This new condensed book is provided to familiarize you with the most important parts of DDD as quickly and simply as possible. Why? Because some are overwhelmed by the larger texts and need a distilled guide to help them take the initial steps to adoption. I have found that those who use DDD revisit the literature about it several times. In fact, you might even conclude that you will never learn enough, and so you will use this book as a quick reference, and refer to others for more detail, a number of times as your craft is refined. Others have had trouble selling DDD to their colleagues and the all-important management team. This book will help you do that, not only by explaining DDD in a condensed format, but also by showing that tools are available to accelerate and manage its use.

Of course, it is not possible to teach you everything about DDD in this book, because I have purposely distilled the DDD techniques for you. For much more in-depth coverage, see my book Implementing Domain-Driven Design [IDDD] , and look into taking my three-day IDDD Workshop. The three-day intensive course, which I have delivered around the globe to a broad audience of hundreds of developers, helps get you up to speed with DDD rapidly. I also provide DDD training online at http://ForComprehension.com.

The good news is, DDD doesn’t have to hurt. Since you probably already deal with complexity on your projects, you can learn to use DDD to reduce the pain of winning over complexity.

### 1.2 Good, Bad, and Effective Design

Often people talk about good design and bad design. What kind of design do you do? Many software development teams don’t give design even a passing thought. Instead, they perform what I call “the task-board shuffle.” This is where the team has a list of development tasks, such as with a Scrum product backlog, and they move a sticky note from the “To Do” column of their board to the “In Progress” column. Coming up with the backlog item and performing “the task-board shuffle” constitutes the entirety of thoughtful insights, and the rest is left to coding heroics as programmers blast out the source. It rarely turns out as well as it could, and the cost to the business is usually the highest price paid for such nonexistent designs.

This often happens due to the pressure to deliver software releases on a relentless schedule, where management uses Scrum to primarily control timelines rather than allow for one of Scrum’s most important tenets: knowledge acquisition.

他们采用一种我称之为「任务板挪卡」的方法来代替设计。团队有个开发任务清单，比如 Scrum 产品待办列表，其中的任务被张贴在「任务板」上，然后他们可以将一张便利贴从「任务板」上的「待办」泳道移动到「进行中」泳道，这就是「任务板挪卡」。产品经理提出待办项（任务），然后来一次「任务板挪卡」，这便构成了关于设计的全部「真知灼见」，剩下的就交给程序员大神们去疯狂输出代码。很少有团队会这样做，如果真的这样做了，业务就会为这些不存在的设计付出最高昂的代价。这种情况常常是因为团队必须按照苛刻得近乎残忍的时间表去发布软件，管理层只会使用 Scrum 控制交付节奏，却对它最重要的信条之一：知识获取（Knowledge Acquisition），视而不见。

任务板挪卡是一种交接棒的协作模式。产品负责人在待办项列表中创建新的待办项，并更新列表中待办项的优先级。开发团队会依据优先级选取待办项，按照产品负责人的文档等需求描述完成相应的研发活动。上述过程中，业务人员与开发人员之间通过交互协作产生设计，这个动作很容易被忽略。优秀设计和有效设计并非由产品负责人或某个团队成员独立完成，而是通过他们之间不断的协作与交互，并在充分的知识获取后形成的。熟悉 Scrum 的读者会发现，Scrum 中的需求梳理与迭代计划会议一定程度上发挥了此类作用。但要注意，协作设计并非只局限在固定的会议中，也提倡在必要时随时随地进行。请参考《Scrum 精髓》[Essential Scrum] 获取更多的内容。——译注

Scrum 是一种用于开发创新产品和服务的敏捷方法。Scrum 的开发方法更加强调将软件开发作为一种不断认知学习的过程，鼓励团队成员与业务人员之间持续地通过协作来迭代交付可工作的软件，并以此快速地获取用户反馈。当然知识获取并非「免费」，所以我们期望开发团队与业务人员之间通过一系列的设计研讨，并引入高效的协作工具（如 DDD 工具箱）帮助团队更加紧密和有效地进行知识传递与分享。关于 Scrum 中的需求梳理和迭代计划的更多介绍请参考《Scrum 精髓》[Essential Scrum] ——译注

2『去下载书籍「Essential Scrum」。』——未完成

When I consult or teach at individual businesses, I generally find the same situations. Software projects are in peril, and entire teams are hired to keep systems up and running, patching code and data daily. The following are some of the insidious problems that I find, and interestingly ones that DDD can readily help teams avoid. I start with the higher-level business problems and move to the more technical ones:

在我独立进行咨询和培训的经历中，经常会遇到相同的情境。软件项目如履薄冰，所有团队成员都在努力地维护着系统稳定，每天面对着代码和数据打补丁。以下是我发现的些潜在问题，有趣的是，DDD 可以帮助团队轻而易举地避免其中的一部分问题。我先从高层次的业务问题开始，然后再讨论技术相关的问题。

1. Software development is considered a cost center rather than a profit center. Generally this is because the business views computers and software as necessary nuisances rather than sources of strategic advantage. (Unfortunately there may not be a cure for this if the business culture is firmly fixed.)

2. Developers are too wrapped up with technology and trying to solve problems using technology rather than careful thought and design. This leads developers to constantly chase after new “shiny objects,” which are the latest fads in technology.

3. The database is given too much priority, and most discussions about the solutions center around the database and a data model rather than business processes and operations.

4. Developers don’t give proper emphasis to naming objects and operations according to the business purpose that they fill. This leads to a large chasm between the mental model that the business owns and the software that developers deliver.

5. The previous problem is generally a result of poor collaboration with the business. Often the business stakeholders spend too much time in isolated work producing specifications that nobody uses, or that are only partly consumed by developers.

6. Project estimates are in high demand, and very frequently producing them can add significant time and effort, resulting in the delay of software deliverables. Developers use the “task-board shuffle” rather than thoughtful design. They produce a Big Ball of Mud (discussed in the following chapters) rather than appropriately segregating models according to business drivers.

7. Developers house business logic in user interface components and persistence components. Also, developers often perform persistence operations in the middle of business logic.

8. There are broken, slow, and locking database queries that block users from performing time-sensitive business operations.

9. There are wrong abstractions, where developers attempt to address all current and imagined future needs by overly generalizing solutions rather than addressing actual concrete business needs.

10. There are strongly coupled services, where an operation is performed in one service, and that service calls directly to another service to cause a balancing operation. This coupling often leads to broken business processes and unreconciled data, not to mention systems that are very difficult to maintain.

2『上面的十大问题，总结一下做一张任意卡片。』——已完成

1、软件开发被视为成本中心而非利润中心。这通常是因为从业务的视角来看计算机和软件技术是必要的消耗而不是战略优势的重要来源。（不幸的是，在根深蒂固的商业文化下，这种观念不太可能被转变）

2、开发人员热衷于技术并通过技术手段解决问题，而不是深入思考和设计，这会导致他们孜孜不倦地追逐技术上的新潮流。

3、过于重视数据库，大多数解决方案的讨论都是围绕数据库和数据模型，而不是业务流程和运作方式。

4、对于根据业务目标命名的对象和操作，开发人员没有给予应有的重视，这导致他们交付的软件和业务所拥有的心智模型之间产生巨大的分歧。

5、上面的问题一般是业务协作不顺畅而导致的。业务干系人常常浪费大把时间闭门造车以实现各种无人问津的需求，或者只有一小部分能被开发人员采用。

6、频繁而又要求精准的项目估算会占用大量的时间和精力，导致软件交付延期。开发人员使用「任务板挪卡」而非考虑周详的设计导致他们造出了一个个「大泥球」（接下来的章节将会讨论），而不是业务驱动下恰当的分离模型。

7、开发人员在用户界面和持久层组件中构建业务逻辑。此外，开发人员也经常会在业务逻辑当中执行持久化操作。

8、数据库查询会时常出现中断、延退、死锁等问题，阻碍用户执行时间敏感型的业务操作。

9、项目中存在错误的抽象级别，表现为开发人员试图借助过度概括的方案满足所有当下以及臆想出来的未来需求，而不是解决实际而又具体的业务诉求。

10、在紧耦合服务群中，当一个服务执行操作时，该服务直接调用另一个服务并引发个对等操作。这种耦合会经常破坏业务流程和未达成一致的数据，更别提这样的系统会有多难维护了。

This all seems to happen in the spirit of “no design yields lower-cost software.” And all too often it is simply a matter of businesses and the software developers not knowing that there is a much better alternative. “Software is eating the world” [WSJ] , and it should matter to you that software can also eat your profits, or feed your profits a banquet.

It’s important to understand that the imagined economy of No Design is a fallacy that has cleverly fooled those who apply the pressure to produce software without thoughtful design. That’s because design still flows from the brains of the individual developers through their fingertips as they wrangle with the code, without any input from others, including the business. I think that this quote sums up the situation well:

Questions about whether design is necessary or affordable are quite beside the point: design is inevitable. The alternative to good design is bad design, not no design at all.

——Book Design: A Practical Introduction by Douglas Martin

这一切都似乎发生在「设计无法带来低成本的软件」的观念下。而这时常是出于商业上的简单考虑，软件开发人员并不知道还有其他更好的选择。软件正在蚕食整个世界 WSJ，对你而言重要的是，软件不但可以蚕食你的利润，也可以提供一场利润盛宴。你一定要明白，臆想出来的「不做设计能省钱」的观念简直是一个谬论，它已经巧妙地愚弄了那些不思考周详设计而只会对软件交付施压的人们。这是因为设计仍然会从每个开发人员的脑海流淌到在键盘上不断敲打着代码的指尖之中，这些设计并不需要来自其他地方的输入，包括业务。

以下这句话可以很好地总结这种现象：关于设计是否必要或是否负担得起的问题根本都没有问到点上：设计是不可或缺的。除了优秀设计就是糟糕设计，根本不存在「不做设计」一说。

不做设计并不能节约成本，而过度设计也会造成浪费，所以我们提倡适度的设计。Martin Fowler 认为敏捷开发不是轻视设计只注重实践和重构，而是鼓励演进式的设计（Evolutionary Design）。优秀设计与有效设计是在持续的重构和迭代过程中产生的，每一次的设计优化都是从最大限度地满足客户的功能性需求和非功能性需求角度出发，以拥抱变化的心态来应对变幻莫测的需求。——译注

1『演化思维无处不在，这里有两个关键词「功能性需求」和「非功能性需求」。』

Although Mr. Martin’s comments are not specifically about software design, they are still applicable to our craft, where there is no substitute for thoughtful design. In the situation just described, if you have five software developers working on the project, No Design will actually produce an amalgamation of five different designs in one. That is, you get a blend of five different made-up business language interpretations that are developed without the benefit of the real Domain Experts.

尽管 Martin 先生的评论并非专门针对软件设计，但这同样适用于我们的技艺，考虑周详的设计同样无可取代。在刚才的情景中，如果一个项目由五名开发人员参与，那么「不做设计」将会产生五种不同的设计。也就是说，在没有任何真正领域专家的协助下，你开发出来的软件将会混杂着五种不同的、虚构出来的、对业务语言的诠释。

The bottom line: we model whether we acknowledge modeling or not. This can be likened to how roads are developed. Some ancient roads started out as cart paths that were eventually molded into well-worn trails. They took unexplained turns and made forks that served only a few who had rudimentary needs. At some point these pathways were smoothed and then paved for the comfort of the increasing number of travelers who used them. These makeshift thoroughfares aren’t traveled today because they were well designed, but because they exist. Few of our contemporaries can understand why traveling one of these is so uncomfortable and inconvenient. Modern roads are planned and designed according to careful studies of population, environment, and predictable flow. Both kinds of roads are modeled. One model employed minimal, base intellect. The other model exploited maximum cognition. Software can be modeled from either perspective.

事实上：无论承认与否，我们都是在构建模型。这就好比修建道路。一些历史悠久的道路最开始是跑马车的，经过岁月的碾压最终变得年久失修。为了满足少数人的需要，它们被加入了不明所以的转弯和岔路，并被改造得迁回曲折。在某个时刻，它们会被铲平并且会被重新建设，为的是让越来越多的旅客感到舒适。这些将就湊合的道路到现在还有人路过，不是因为它们设计良好，而仅仅是因为它们存在着而己。如今很少有人能够了解行走在这些道路上别扭不堪的原因。而现代道路都会依据人口、环境以及可预测的流量来规划和设计。两种类型的道路都会被建模。一种模型只是做了最基本、最简单的思考，另种则最大程度地发挥了聪明才智。软件建模也可以从这两种角度出发。

If you are afraid that producing software with thoughtful design is expensive, think of how much more expensive it’s going to be to live with or even fix a bad design. This is especially so when we are talking about software that needs to distinguish your organization from all others and yield considerable competitive advantages.

A word closely related to good is effective, and it possibly more accurately states what we should strive for in software design: effective design. Effective design meets the needs of the business organization to the extent that it can distinguish itself from its competition by means of software. Effective design forces the organization to understand what it must excel at and is used to guide the creation of the correct software model.

2『有效设计，做一张术语卡片。』——已完成

如果你担心周详的设计会带来高昂的软件开发成本，那么设想一下，将来为了维护甚至修缮一套糟糕设计的软件就需要付出更为昂贵的代价。当我们把软件作为你的公司与其他公司之间的差异，并依靠它带来可观的竞争优势时，尤其如此。

有效（Efective）一词和优秀（Good）意义相近，它能更准确地表达我们应该在软件设计中努力追求的目标：「有效设计」（Effective Design）。有效设计可以满足商业组织希望借助软件超越竟争者的诉求。它可以驱动企业去思考哪些核心业务必须成为其竞争力，还可以指引构建正确软件模型的方向。

In Scrum, knowledge acquisition is done through experimentation and collaborative learning and is referred to as “buying information” [Essential Scrum] . Knowledge is never free, but in this book I do provide ways for you to accelerate how you come by it.

Just in case you still doubt that effective design matters, don’t forget the insights of someone who seems to have understood its importance:

Most people make the mistake of thinking design is what it looks like. People think it’s this veneer—that the designers are handed this box and told, “Make it look good!” That’s not what we think design is. It’s not just what it looks like and feels like. Design is how it works.

——Steve Jobs

In software, effective design matters, most. Given the single alternative, I recommend effective design.

Scrum 中的知识获取是通过不断的试验及协作学习完成的，这被称为「知识付费」（Essential Scrum）。知识水远都不是免费的，但在本书中，我将提供一些方法帮你更快地获取它们。如果你对有效设计的影响仍心存疑虑，别忘了那位曾洞察其重要性的人：绝大部分人错误地认为设计只关乎外观。人们只理解了表象一一将这个金子递给设计师，告诉他们：「把它变得好看一些！」这不是我们对设计的理解。设计并不仅仅是感观，设计也是产品的工作方式。——Steve Jobs

「设计，是让生活变得完美的艺术。」这是乔布斯的产品设计理念。对他而言，有效设计首先意味着「简洁」的产品（开箱即用）、「简洁」的战略（产品的专注）和「简洁」的沟通（高效的沟通）。其次有效设计允许不完美。任何产品都始于不完美，只有通过不断试错与修正的送代才可能逐步趋于完美在软件设计中，我们也可以借鉴这些理念：有效设计是简洁而非冗余，它也需要不断地演进与优化才能趋于完美。——译注

### 1.3 Strategic Design

We begin with the all-important strategic design. You really cannot apply tactical design in an effective way unless you begin with strategic design. Strategic design is used like broad brushstrokes prior to getting into the details of implementation. It highlights what is strategically important to your business, how to divide up the work by importance, and how to best integrate as needed.

First you will learn how to segregate your domain models using the strategic design pattern called Bounded Contexts. Hand in glove, you will see how to develop a Ubiquitous Language as your domain model within an explicitly Bounded Context.

我们先从最为重要的战略设计谈起。不以战略设计开始，战术设计将无法被有效实施。在展开具体实现细节之前，需要优先完成宏观层面的战略设计。它强调的是业务战略上的重点，如何按重要性分配工作，以及如何进行最佳整合。

首先，你需要学会运用名为限界上下文（Bounded Contex）的战略设计模式来分离领域模型。紧接着，你会了解如何使用在明确的限界上下文中发展一套领域模型的通用语言（Ubiquitous Language）。

You will learn about the importance of engaging with not only developers but also Domain Experts as you develop your model’s Ubiquitous Language. You will see how a team of both software developers and Domain Experts collaborate. This is a vital combination of smart and motivated people who are needed for DDD to produce the best results. The language you develop together through collaboration will become ubiquitous, pervasive, throughout the team’s spoken communication and software model.

As you advance further into strategic design, you will learn about Subdomains and how these can help you deal with the unbounded complexity of legacy systems, and how to improve your results on greenfield projects. You will also see how to integrate multiple Bounded Contexts using a technique called Context Mapping. Context Maps define both team relationships and technical mechanisms that exist between two integrating Bounded Contexts.

通过本书，大家将会了解到，在发展模型通用语言的过程中开发人员和领域专家的参与同样重要。也将看到团队中的软件开发人员与领域专家是如何协作的。这是一个由一群聪明而又上进的人们组成的重要组合，他们需要借助 DDD 来达成最佳效果。通过协作而产生的语言会变得统一、流行、并遍布于团队的日常口头交流和软件模型之中。

当进一步深入到战略设计中时，将会学到子域（Subdomain），并了解如何通过它处理遗留系统中无边界的复杂性，以及如何改进新项目上的成果。还会了解如何通过名为上下文映射（Context Mapping）的技术来集成多个限界上下文。上下文映射图（Context map）同时定义了两个进行集成的限界上下文之间的团队间关系及技术实现方式。

### 1.4 Tactical Design

After I have given you a sound foundation with strategic design, you will discover DDD’s most prominent tactical design tools. Tactical design is like using a thin brush to paint the fine details of your domain model. One of the more important tools is used to aggregate entities and value objects together into a right-sized cluster. It’s the Aggregate pattern.

DDD is all about modeling your domain in the most explicit way possible. Using Domain Events will help you both to model explicitly and to share what has occurred within your model with the systems that need to know about it. The interested parties might be your own local Bounded Context and other remote Bounded Contexts.

在打好战略设计的基础之后，将会发现 DDD 最为突出的莫过于战术层面的设计工具。战术设计犹如使用一把精小的画笔在领域模型上描绘着每个细枝末节。其中一个比较重要的工具被用来将若干实体和值对象以恰当的大小聚集在一起。这就是聚合（Aggregate）模式。

DDD 就是以最明确而又可行的方式对领域进行建模。使用领域事件（Domain Events）既可以让你明确地建立模型，也可把模型内部发生的事情分享给需要知道这一切的系统。这些相关的系统可能是你自己的本地限界上下文和其他的远程限界上下文。

### 1.5 The Learning Process and Refining Knowledge

DDD teaches a way of thinking to help you and your team refine knowledge as you learn about your business’s core competencies. This learning process is a matter of discovery through group conversation and experimentation. By questioning the status quo and challenging your assumptions about your software model, you will learn much, and this all-important knowledge acquisition will spread across the whole team. This is a critical investment in your business and team. The goal should be not only to learn and refine, but to learn and refine as quickly as possible. There are additional tools to help with those goals that can be found in Chapter 7 , “Acceleration and Management Tools .”

DDD 为我们带来了一种全新的思维方式，这种思维方式可以帮助你和你的团队在理解业务核心竟争力的同时提炼知识。学习过程是小组讨论与试验的一系列探索。通过不断地质疑现状与挑战软件模型的假设，你可以学到更多的知识，而且这些非常重要的知识将在传播中惠及整个团队。这是业务和团队所需要付出的关键投资。我们的目标不应该只是学习和提炼，而是以尽可能快的速度学习和提炼。第 7 章中将会提供很多额外的方法和工具来帮助实现这一目标。

Let’s Get Started! Even in a condensed presentation, there’s plenty to learn about DDD. So let’s get started with Chapter 2 , “Strategic Design with Bounded Contexts and the Ubiquitous Language .”

## 0201. Strategic Design with Bounded Contexts and the Ubiquitous Language

In summary you have learned: 1) Some of the major pitfalls of putting too much into one model and creating a Big Ball of Mud. 2) The application of DDD strategic design. 3) The use of Bounded Context and Ubiquitous Language. 4) How to challenge your assumptions and unify mental models. 5) How to develop a Ubiquitous Language. 6) About the architectural components found inside a Bounded Context. 6) That DDD is not too difficult to put into practice yourself! For a more in-depth treatment of Bounded Contexts , see Chapter 2 of Implementing Domain-Driven Design [IDDD] .

What are these things called Bounded Contexts ? What’s the Ubiquitous Language ? In short, DDD is primarily about modeling a Ubiquitous Language in an explicitly Bounded Context. While true, that probably wasn’t the most helpful description that I could provide. Let me break this down for you.

2『上面对 DDD 下了一个简洁的定义，做一张术语卡片。』——已完成

First, a Bounded Context is a semantic contextual boundary. This means that within the boundary each component of the software model has a specific meaning and does specific things. The components inside a Bounded Context are context specific and semantically motivated. That’s simple enough.

When you are just getting started in your software modeling efforts, your Bounded Context is somewhat conceptual. You could think of it as part of your problem space. However, as your model starts to take on deeper meaning and clarity, your Bounded Context will quickly transition to your solution space , with your software model being reflected as project source code. (The problem space and solution space are better explained in the box.) Remember that a Bounded Context is where a model is implemented, and you will have separate software artifacts for each Bounded Context.

首先，限界上下文是语义和语境上的边界。这意味着边界内的每个代表软件模型的组件都有着特定的含义并处理特定的事务。限界上下文中的这些组件有特定的上下文语境和语义理据。这确实很简单。如果刚刚开始投入到软件建模中，限界上下文多少是有些概念化的。你可以将它理解为问题空间（Problem Space）的一部分。然而，随着软件模型开始呈现出更深层次以及更清断的含义时，限界上下文将会被迅速转换到解决方案空间（Solution Space）中，同时软件模型将通过项目的源代码来体现（下面这段文字可以更好地解释问题空间和解决方案空间）。请记住，模型是在限界上下文中实现的，你也将会为每个限界上下文开发出不同的软件。

2『 Bounded Context，做一张术语卡片。』——已完成

『

What Is a Problem Space and a Solution Space?

Your problem space is where you perform high-level strategic analysis and design steps within the constraints of a given project. You can use simple diagrams as you discuss the high-level project drivers and note important goals and risks. In practice, Context Maps work very well in the problem space. Note too that Bounded Contexts may be used in problem space discussions, when needed, but are also closely associated with your solution space.

Your solution space is where you actually implement the solution that your problem space discussions identify as your Core Domain. When the Bounded Context is being developed as a key strategic initiative of your organization, it’s called the Core Domain. You develop your solution in the Bounded Context as code, both main source and test source. You will also produce code in your solution space that supports integration with other Bounded Contexts .

什么是问题空间和解决方案空间？问题空间是在给定项目的约束条件下进行高级战略分析与设计各个步骤的地方。你可以使用简单的图表来展示讨论中高级的项目驱动因素，并记录关键目标与风险。在实践中，上下文映射图可以在问题空间中工作得很好。同时还要注意，限界上下文不仅可以在需要时用于问题空间的讨论，也与你的解决方案空间密切相关。

解决方案空间就是真正实施解决方案的地方，这些解决方案在问题空间讨论中被识别为核心域（Core Domain）1。当限界上下文被当作组织的关键战略举措进行开发时，即被称为核心域。你将主要通过源代码和测试代码来实现限界上下文中的解决方案，也会在解決方案空间中编写代码，来支撑与其他限界上下文之间的集成。

1 核心域的识别是一个持续的精练过程，把一堆混杂在一起的组件分离，以某种形式提炼出最重要的内容，这种形式也将使核心域更具价值。一个严峻的现实是，我们不可能对所有的设计部分投入同等的资源进行优化，如同 MVP (Minimum Viable Product）产品原则所提倡的那样，产品研发需要聚焦在最小化可行产品上，不断获取用户反馈，并在这个最小化可行产品上持续快速选代，从而获得一个稳定的核心产品。在有限的资源下，为了使领域模型成为最有价值的资产，我们必须有效地梳理出模型的真正核心并完全根据这个核心来实现软件服务，这也是核心域的战略价值所在。一一译注

』

The software model inside the context boundary reflects a language that is developed by the team working in the Bounded Context and is spoken by every member of the team that creates the software model that functions within that Bounded Context. The language is called the Ubiquitous Language because it is both spoken among the team members and implemented in the software model. Thus, it is necessary that the Ubiquitous Language be rigorous—strict, exact, stringent, and tight. In the diagram, the boxes inside the Bounded Context represent the concepts of the model, which may be implemented as classes. When the Bounded Context is being developed as a key strategic initiative of your organization, it’s called the Core Domain.

1-2『这里算是解释了核心域的概念，一个限界上下文被组织当作关键战略进行开发时，那么它就成为了一个核心域。』

团队在限界上下文中发展了一种语言用于表达其边界内的软件模型，这一语言由在该界上下文中开发软件模型的每个团队成员所使用。它之所以被称之为通用语言（Ubiquitous Language）2，是因为团队成员间交流用的是它，软件模型实现的也是它。因此，通用语言必须严谨、精确，并且紧湊。上图中，限界上下文中的方框所表示的概念模型可以用类来实现。当限界上下文被当作组织的关键战略举措进行开发时，即被称之为核心域。

2 在《实例化需求》[Specification] 一书中译作統一语言，也是一种常见的译法。一一译注

When compared with all the software your organization uses, a Core Domain is a software model that ranks among the most important, because it is a means to achieve greatness. A Core Domain is developed to distinguish your organization competitively from all others. At the very least it addresses a major line of business. Your organization can’t excel at everything and shouldn’t even try. So you choose wisely what should be part of your Core Domain and what should not. This is the primary value proposition of DDD, and you want to invest appropriately by committing your best resources to a Core Domain.

When someone on the team uses expressions from the Ubiquitous Language , everyone on the team understands what is meant with precision and constraints. The expression is ubiquitous within the team, as is all language used by the team that defines the software model being developed.

When you consider language in a software model, think of the various nations that make up Europe. Within one of the countries across this space, the official language of each country is clear. Within the boundaries of those nations—for example, Germany, France, and Italy—the official languages are certain. As you cross a boundary, the official language changes. The same goes for Asia, where Japanese is spoken in Japan, and the languages spoken in China and Korea are clearly different across the national boundaries. You can think of Bounded Contexts in much the same way, as being language boundaries. In the case of DDD, the languages are those spoken by the team that owns the software model, and a notable written form of the language is the software model’s source code.

1『欧洲各个国家语言的例子，值得细品。获得的启示，数据流里，每个外专业的任务领域，应该就是一个限界上下文，很明显，一个给排水设计人员是不懂暖通的专业知识的。（2020-08-04）』

与组织使用的所有其他软件相比，核心域是其中最重要的软件模型，因为它是组织取得巨大成就的手段。发展核心域可以使你的组织在与其他组织的竞争中脱颗而出。至少，它标明了组织的业务主航道。你的组织无法在所有领域都出类拔萃，也无须如此。因此你需要做出明智的选择，哪些是核心域，而哪些不是。这是 DDD 的首要价值主张，同时你也期望通过恰当的投资把最好的资源投入到核心域中。当团队中有人使用通用语言进行交流时，其他人都可以明白他表达的准确含义和约束条件。通用语言和开发软件模型中使用的其他语言一样，在团队中无处不在。

当你思考软件模型中的语言时，想一想组成欧洲的各个国家：整个欧洲大陆中的任何一个国家，使用的官方语言都是明确的。在这些国家的边境内，如德国、法国和意大利，官方语言是确定的。当你越过边境时，官方语言也会改变。同样的情况也适用于亚洲：被界线分开的日本、韩国和中国都使用着自己的语言。限界上下文也是如此。在 DDD 中通用语言就是软件模型团队日常交流时使用的语言，而软件模型的源代码就是这种语言的书面表达方式。

1-2『限界上下文中的通用语言，上面的欧洲各个国家的隐喻很贴切，通用语言做一张术语卡片。』——已完成

『

Bounded Contexts, Teams, and Source Code Repositories

There should be one team assigned to work on one Bounded Context. There should also be a separate source code repository for each Bounded Context. It is possible that one team could work on multiple Bounded Contexts , but multiple teams should not work on a single Bounded Context. Cleanly separate the source code and database schema for each Bounded Context in the same way that you separate the Ubiquitous Language. Keep acceptance tests and unit tests together with the main source code.

It is especially important to be clear that one team works on a single Bounded Context. This completely eliminates the chances of any unwelcome surprises that arise when another team makes a change to your source code. Your team owns the source code and the database and defines the official interfaces through which your Bounded Context must be used. It’s a benefit of using DDD.

一个团队应该在一个限界上下文中工作。每个限界上下文应该拥有一个独立的源代码仓库 1。一个团队可能工作在多个限界上下文中，但是多个团队不应该在同一个限界上下文中共事。我们应该采用和分离通用语言同样的方式，干净地把不同限界上下文的源代码和数据库模式隔离开。并且，将同一个限界上下文中的验收测试、单元测试和主要源代码存放在一起。尤其重要的是，要明确一个团队只在单一的限界上下文中工作。别给其他团队留下任何机会去修改你的源代码，从而引发意外。2 你的团队控制着源代码和数据库并定义了官方接口，必须通过这些接口才可以调用限界上下文。这是使用 DDD 所能带来的好处之一。

1『上面的「一个限界上下文中只能有一个团队」，这个观点很认可，做一张任意卡片。』——已完成

1 传统软件开发方式里，一个产品往往由多个组件团队共同开发，组件代码分别存放在不同的代码仓库，只有负责的团队拥有组件代码仓库的所有权。由于使用了这种代码仓库的划分方法，大量的集成将会发生在组件与组件之间，同时也会产生大量的跨团队的交流和代码访问。一种常见的场景是，在开发初期新的功能往往无法集成并正常运作，更不可能完成阶段性验收，只有等到开发的后期才能获得一个可以运行的产品。而书中提及的独立代码仓库将遵循限界上下文进行划分，上下文内使用统一的通用语言进行交流，并尽可能由一个团队对领域模型进行维护。两种代码仓库的划分方式的最大区别在于，限界上下文内的领域模型往往具有独立的业务价值，可以独立地提供服务。而传统的组件式代码仓库经常会存在相互间的紧耦合关系，无法独立地提供服务。本书译者所著的《代码管理核心技术及实践》一书中也谈到了类似的案例，介绍了一个团队是如何从组件代码仓库转换到领域代码仓库的。一一译注 

2 这并不是绝对的。事实上，很多上下文的代码仓库是开放的，并接受其他团队提交的代码。甚至，很多独角兽企业（如 Google 和 Facebook）在代码仓库上惊人一致地选择了单一仓库（monoreme）进行代码管理，即整个组织所有的产品代码放在唯一一个超大的代码仓库中。这些代码并不是铁板一块，它依然可以被分成多个服务甚至多个产品，由多个团队独立地构建、测试和维护。单一仓库和开放仓库一样更注重的是代码共有制带来的协作效率。代码共有制不会造成混乱，原因在于它们拥有完善的机制和工具对所有提交的代码进行准入控制和验证，而这些仓库的贡献者也对编写代码有着严格的自我要求。所以并不是要杜绝其他团队对代码仓库进行修改，而是要让这些修改可以预期且可以控制，这必须采取些适合团队的实践和工具来实现，例如频繁交流（如结对编程）、代码走查（如 Pull Request）和自动化验证（如契约测试）等。这些实践和手段往往由上下文映射关系决定，如共享内核关系就可以采用 Pull Request 的实践，而客户一供应商关系则可以采用契约测试的实践。关于映射关系的讨论请参考本书第 4 章的内容。——译注

』

In human languages, terminology evolves over time, and across national boundaries the same or similar words take on nuances of meaning. Think of the differences between Spanish words used in Spain and those same words used in Colombia, where even the pronunciation changes. There is clearly Spain’s Spanish and Colombia’s Spanish. So too with software model languages. It’s possible that people from other teams would have a different meaning for the same terminology, because their business knowledge is within a different context; they are developing a different Bounded Context. Any components outside the context are not expected to adhere to the same definitions. In fact, they are probably different, either slightly or vastly, from the components that your team models. That’s fine.

在人类的语言中，词汇随时间的推移不断发展并跨越国界，相同或相似的词汇在意义上有着细做的差别。比如，同一个西班牙语词汇在西班牙和哥伦比亚代表不一样的含义有些甚至发音也不同。西班牙式的西班牙语与哥伦比亚式的西班牙语有着明显的区别。软件模型的语言也是如此。来自其他团队的成员可能对于同一术语有着不同的理解，这正是因为他们业务知识的上下文不同，他们在开发一个不同的限界上下文。别指望上下文之外的任何组件会遵循相同的定义。事实上，这些组件与你的模型组件之间可能存在着差异，或细做或巨大，这很正常。

To understand one big reason to use Bounded Contexts , let’s consider a common problem with software designs. Often teams don’t know when to stop piling more and more concepts into their domain models. The model may start out small and manageable......

But then the team adds more concepts, and more, and still more. This soon results in a big problem. Not only are there too many concepts, but the language of the model becomes blurred, because when you think about it there are actually multiple languages in one large, confusing, unbounded model.

为了更好地理解使用限界上下文的重要原因，让我们来思考软件设计中的一个常见问题。通常，团队并不清楚应该何时停止向领域模型中注入越来越多的概念。或许刚开始时这个模型很小也能被管理…...然而随着团队不断地注入更多概念，很快便出现了一个大麻烦。不仅概念太多，而且模型中的语言也变得模糊不清，因为在你思考它时，会发现在这个巨大的、混乱的、漫无边际的模型中实际存在着多种语言。

Due to this fault, teams will often turn a brand-new software product into what is called a Big Ball of Mud. To be sure, a Big Ball of Mud is not something to be proud of. It’s a monolith, and worse. This is where a system has multiple tangled models without explicit boundaries. It probably also requires multiple teams to work on it, which is very problematic. Furthermore, various unrelated concepts are blown out over many modules and interconnected with conflicting elements. If this project has tests, it probably takes a very long time to run them, and so the tests may be bypassed at especially important times.

因为这样或那样的错误，团队常常会将全新的软件产品变成一个所谓的大泥球（Big Ball of Mud）。当然，大泥球并不值得骄做。它是一个庞然大物，而且会变得更糟。这个系统由多个没有明确边界并纠缠在一起的模型组成。更为严重的是，它可能还会要求多个团队在其中工作。此外，各种毫不相干的概念充斥在众多的模块中，并与自相矛盾的元素相互关联。如果这个项目有测试，运行它们可能需要很长的时间，而这些测试可能会在非常重要的时刻被忽略。

It’s the product of trying to do too much, with too many people, in the wrong place. Any attempt to develop and speak a Ubiquitous Language will result in a fractured and ill-defined dialect that will soon be abandoned. The language wouldn’t even be as well conceived as Esperanto. It’s just a mess, like a Big Ball of Mud.

这是一个在错误的领域投入过多人力并尝试去做太多事情的产物。任何发展和使用通用语言的努力都将会产生一种支离破碎而又定义不明的方言，并很快被弃用。这种语言甚至不如世界语 1。它只是一个如同大泥球般的烂推子。

1 语言不仅仅只是起到交流的作用，更蕴含了使用该语言的背景、民族历史和发展历程。曾经风靡一时的世界语，正是因为脱离了一个共同的情境而无法真正普及。发展通用语言，是希望读者基于一定的业务上下文的情境不断地优化和建立统一的语言。一一译注

1『此处颇有感触。世界语之所以被抛弃，就是它想做「万用模型」，模型只能在「范围」与「精度」间取平衡，要万用的话其精度必定很差，这模型也就没啥用了。DDD 里的通用语言也是一个道理，它必定依托于一个特定的限界上下文（业务场景）。（2020-08-04）』

### 2.1 Domain Experts and Business Drivers

There may be strong, or at least subtle, hints communicated by business stakeholders that could have been used to help the technical team make better modeling choices. Thus, a Big Ball of Mud is often the result of unbridled effort made by a team of software developers who don’t listen to the business experts.

The business’s department or work group divisions can provide a good indication of where model boundaries should exist. You will tend to find at least one business expert per business function. Lately there is a trend toward grouping people by project, while business divisions or even functional groups under a management hierarchy seem to be less popular. Even in the face of newer business models you will still find that projects are organized according to business drivers and under an area of expertise. You may need to think of division or function in those terms.

业务干系人传递出的暗示会帮助技术团队做出更好的建模选择，这些暗示或许强烈或许非常微妙。而大泥球往往是由于软件开发人员无视业务专家的建议，一意孤行的结果。业务部门或工作组织的划分可以很好地标明模型边界的位置。你将倾向于为每个业务功能寻找至少一位业务专家。近来有一种按项目划分团队的趋势，而那些在管理层之下的业务部门，甚至是职能组织都似乎不那么受欢迎。即使在较新的商业模式下，你仍会发现项目是根据业务驱动并被专业领域组织起来的，你需要从这些角度考虑部门和职能。

1『项目是根据业务驱动的。』

You can determine that this kind of segregation is needed when you consider that each business function likely has different definitions for the same term. Consider the concept named “policy” and how the meaning differs across the various insurance business functions. You can easily imagine that a policy in underwriting is vastly different from a policy in claims and a policy in inspections. See the box for more details.

The policy in each of these business areas exists for different reasons. There is no escaping this fact, and no amount of mental gymnastics changes this.

当你意识到不同业务领域对同一术语可能有不同的定义时，就可以确定这种分离是必要的。考虑一下保单（Policy）的概念，以及其在不同的保险业务领域中不同的含义。可以很容易地想象出，保单在承保中的含义与理赔、审核中的含义有很大的不同。更多的细节可以参考下一页的描述。每个业务领域中的保单因不同原因而存在。这是无法回避的事实，即便花费再多的力气、绞尽脑汁也无济于事。

『

Differences in Policies by Function

Policy in Underwriting: In the area of expertise that is focused on underwriting, a policy is created based on the evaluation of the risks of the insured entity. For example, when working in underwriting for property insurance, the underwriters would assess the risks associated with a given property in order to calculate the premium for the policy to cover the property asset.

Policy in Inspections: Again, if we are working in the property insurance field, the insurance organization will likely have an inspections area of expertise that is responsible for inspecting a property that is to be insured. The underwriters are somewhat dependent on the information found during inspections, but only from the standpoint that the property is in the condition asserted by the insured. Assuming that a property will be insured, the inspection details—photos and notes—are associated with a policy in the inspections area, and its data can be referenced by underwriting to negotiate the final premium cost in the underwriting area.

Policy in Claims: A policy in the claims area of expertise tracks the request for payment by the insured based on the terms of the policy created by the underwriting area. The claims policy will need to make some references to the underwriting policy but will be focused on, for example, damages to the insured property and reviews performed by the claims personnel to determine the payment, if any, that should be made.

承保保单：专门从事承保的业务领域中，保单会基于对被保险实体进行的风险评估而创建。例如，在承保财产保险时，保险公司将对给定的财产进行相关风险评估，以便计算承保财产保单的保费。

审核保单：同样，如果我们从事于财产保险领城，保险公司将很有可能下设一个专门负责审核的业务部门，该部门负责审核需要投保的财产。承保部门一定程度上依赖于在审核过程中发现的信息，但仅从财产状况与被保险人声明是否一致的这一点出发。假设有一笔财产正在投保，审核的细节包括照片和文档，这些都与审核环节的保单相关，而在承保环节商定最终保费时，这些信息都会被参考。

理赔保单：理赔中的保单是根据承保环节制订的保险条款，来跟踪投保人理赔的赔付请求进度。索赔保单需要参考承保保单，但会着重确认被保险财产的损害情况和理赔员所审查的材料是否一致，以确定是否应支付保险费，如果是，则究成赔付。

』

If you try to merge all three of these policy types into a single policy for all three business groups, you will certainly have problems. This would become even more problematic if the already-overloaded policy had to support a fourth and fifth business concept in the future. Nobody wins.

On the other hand, DDD emphasizes embracing such differences by segregating the differing types into different Bounded Contexts. Admit that there are different languages, and function accordingly. Are there three meanings for policy? Then there are three Bounded Contexts , each with its own policy, with each policy having its own unique qualities. There’s no need to name these UnderwritingPolicy , ClaimsPolicy , or InspectionsPolicy . The name of the Bounded Context takes care of that scoping. The name is simply Policy in all three Bounded Contexts.

如果你尝试将这三种保单类型合并成一个适合所有业务职能领域的单一保单概念，背定会出问题。如果这个已经超负荷的保单不得不继续承担第四、第五个业务概念，情况会变得更糟。最终没有赢家。

1『所以说嘛，用界限分割上下文很重要，不能混合在一起（建模），必须先划分在其各自的上下文中，然后在每个上线文中分别建模。这里体现了郑烨一直说的「分离关注点」。』

相反，DDD 强调将这些不同的概念类型分离到不同的限界上下文中，以此来拥抱这些差异，并且承认存在不同的通用语言和与之对应的职能。这里确实存在三种不同的保单定义，此处有三个界限上下文，它们都有各自的保单，每个保单都是独一无二的。没有必要把这些保单命名为承保保单、理赔保单或是审核保单，因为限界上下文的名称就可以区分它们。在这三个限界上下文中我们只需要一个简单的名称：保单。

『

Another Example: What Is a Flight?

In the airline industry, a “flight” can have multiple meanings. There is a flight that is defined as a single takeoff and landing, where the aircraft is flown from one airport to another. There is a different kind of flight that is defined in terms of aircraft maintenance. And there is yet another flight that is defined in terms of passenger ticketing, either nonstop or one-stop. Because each of these uses of “flight” is clearly understood only by its context, each should be modeled in a separate Bounded Context. To model all three of these in the same Bounded Context would lead to a confusing tangle.

航空业中的「飞行」有很多含义。其中ー个是，飞机从一个机场飞到另一个机场的单次起降。飞机维修领城则有另一种不同的定义。还有一种是客票领域的定义，可以是直达也可以是中转。这几种「飞行」概念只有通过各自的上下文才能被清晣地解释，并且应该在被分离的限界上下文中建模。在同一个限界上下文中为这三种概念建模会导致混乱。

』

### 2.2 Case Study

To make the reason to use Bounded Contexts more concrete, let me illustrate with a sample domain model. In this case we are working on a Scrum-based agile project management application. So, a central or core concept is Product, which represents the software that is to be built and that will be refined over perhaps years of development. The Product has Backlog Items, Releases, and Sprints. Each Backlog Item has a number of Tasks, and each Task can have a collection of Estimation Log Entries. Releases have Scheduled Backlog Items and Sprints have Committed Backlog Items. So far, so good. We have identified the core concepts of our domain model, and the language is focused and intact.

为了让使用限界上下文的原因更加具体，我将以一个领域模型为例。在此案例中，我们正在开发一个基于 Scrum 的敏捷项目管理应用。因此，核心概念是产品（Product），它代表了将要被开发的软件，并且在未来数年的研发中将会被持续改进。产品由待办项（Backlog Item）、发布（Release）和冲刺（Sprint）组成。每个待办项都包含一些任务（Task），每个任务都拥有一个估算记录条目（Estimation LogEntry）集合。发布中包含计划好的待办项（Scheduled Backlog Item），冲刺中包含已提交的待办项（Committed Backlog Item）。目前为止，一切顺利。我们已经确定了领域模型的核心概念，通用语言也是专注且完整的。

“Oh, yeah,” say the team members, “we also need our users. And we want to facilitate collaborative discussions within the product team. Let’s represent each subscribing organization as a Tenant. Within Tenants we will allow the registration of any number of Users, and Users will have Permissions. And let’s add a concept called Discussion to represent one of the collaborative tools that we will support.”

团队成员说，「我们也需要产品的用户。我们希望促进产品团队内的协作讨论。让我们用租户（Tenant）来表示每个订购了产品的组织，在每个租户中，我们将允许任意数量的用户（User）注册，同时他们还将拥有一些权限（Permission）。让我们增加个讨论（Discussion）的概念，来代表我们即将支持的一种协作工具。」

Then the team members add, “Well, there are also other collaboration tools. Discussions belong within Forums and Discussions have Posts. Also we want to support Shared Calendars.”

随后有成员补充：「嗯，还有其他的协作工具。讨论应该属于论坛（Forum），而且还应该包括讨论帖（Post）。此外，我们还希望支持共享日历（Shared Calendar）。」

They continue: “And don’t forget that we need a way for Tenants to make Payments. We will also sell tiered support plans, so we need a way to track support incidences. Both Support and Payments should be managed under an Account.”

他们继续说道：「别忘了我们还需要一种方式让租户完成支付（Payment）。我们将会销售支持计划（Support Plan）的套餐，为此还需要一种跟踪支持事件（Incident）的方法无论是支持（Support）还是支付都应该在账户（Account）下进行管理。

And still more concepts emerge: “Every Scrum-based Product has a specific Team that works on the product. Teams are composed of a single Product Owner and a number of Team Members. But how can we address Human Resource Utilization concerns? Hmmm, what if we modeled the Schedules of Team Members along with their utilization and availability?”

随后会涌现出更多的概念：「每个基于 Scrum 运作的产品都有一个特定团队（Team）团队。由一位产品负责人（Product Owner）和一些团队成员（Team Member）组成。但我们如何解决人力资源利用率（Human Resource Utilization）的问题呢？嗯，如果我们为团队成员建立日程（Schedule），以及利用率（Utilization）和可用性（Availability）的模型，会怎么样？

“You know what else?” they ask. “Shared Calendars should not be limited to bland Calendar Entries. We should be able to identify specific kinds of Calendar Entries, such as Reminders, Team Milestones, Planning and Retrospective Meetings, and Target Dates.”

Hang on a minute! Do you see the trap that the team is falling into? Look at how far they have strayed from the original core concepts of Product, Backlog Items, Releases, and Sprints. The language is no longer purely about Scrum; it has become fractured and confused.

「你知道还有什么吗？」团队成员说，「共享日历不应仅限于保存日常的日历条目（Calendar Entry）。它还应该可以保存一些特殊的条目，比如提醒（Reminder）、团队里程碑（Team Milestone）、计划会议（Planning Meeting）和回顾会议（Retrospective Meeting），还有交付日期（Target Date）。等一下！你有没有发现团队正在落入一种陷阱？他们已经偏离了最初的核心概念：产品（Product）、待办项（Backlog Item）、发布（Release）和冲刺（Sprint）。通用语言已经不再纯粹地与 Scrum 相关，它已经变得支离破碎并令人困惑。

Don’t be fooled by the somewhat limited number of named concepts. For every named element, we might expect to have two or three more concepts to support those that quickly popped into mind. The team is already well on its way to delivering a Big Ball of Mud and the project has barely started.

不要因为命名概念过少而疑惑。对于每一个命名元素而言，我们都可能情不自禁地在脑海中闪现两个、三个或更多可以支撑它的概念。而此时项目才刚刚起步，团队就已经滑向大泥球的深渊 1。

1 事实上，开发人员更加擅长在设计过程中不断地抽象对于客观世界的观察。如果这些概念被全盘接受，无形中就会形成过度设计的领域模型。因此在设计过程中，开发人员需要不断地向业务人员确认上下文的核心和必要概念，及时抑制过度设计的冲动。如果无法除那些不必要或不属于核心域的概念，在不的将来就会造就一批低价值的功能，而这些功能对于产品研发而言就是巨大的浪费。一一译注

1『抑制住过渡设计。采用战略设计中的「限界上下文」和「通用语言」可以避免过渡设计，只关注核心领域功能。』

### 2.3 Fundamental Strategic Design Needed

What tools are available with DDD to help us avoid such pitfalls? You need at least two fundamental strategic design tools. One is the Bounded Context and the other is the Ubiquitous Language. Employing a Bounded Context forces us to answer the question “What is core?” The Bounded Context should hold closely all concepts that are core to the strategic initiative and push out all others. The concepts that remain are part of the team’s Ubiquitous Language. You will see how DDD works to avoid the design of monolithic applications.

DDD 中有哪些工具可以帮助我们避免这些陷阱？你至少需要两种基本的战略设计工具，限界上下文和通用语言。采用限界上下文会迫使我们回答「什么是核心？」的问题。它应紧紧地抓住战略举措中所有的核心概念，并排除其他概念，剩下的都应该是团队通用语言的一部分。你将看到 DDD 如何避免单体应用设计的产生。

『

Testing Benefits

Because Bounded Contexts are not monolithic, other benefits are experienced when they are used. One such benefit is that tests will be focused on one model and thus be fewer in number and will run more quickly. Although this isn’t the primary motivation to use Bounded Contexts , it sure pays off in other ways.

1『哈哈，妙哉妙哉，限界上下文无意中让测试更好写。』

限界上下文并非庞然大物，使用它们却可以收益良多。其中之一就是测试会聚焦于一个模型中，这样测试的数量会更少，执行更快。虽然这并非是使用限界上下文的主要动机，但确实是意外的收获。

』

Literally, some concepts will be in context and be clearly included in the team’s language.

And other concepts will be out of context. The concepts that survive this stringent application of core-only filtering are part of the Ubiquitous Language of the team that owns the Bounded Context.

从字面上看，有些概念属于限界上下文，并被清晰地包含在团队的通用语言中。而其他的概念将会在限界上下文之外。只有经过「仅限核心」的严格过滤之后保留下来的概念，才能成为拥有限界上下文的团队的通用语言的一部分。

Take Note: The concepts that survive this stringent application of core-only filtering are part of the Ubiquitous Language of the team that owns the Bounded Context. The boundary emphasizes the rigor inside.

注意：只有经过「仅限核心」的严格过滤之后保留下来的概念，才能成为拥有限界上下文的团队的通用语言的一部分。限界上下文的边界强调其内部的严谨性。

So, how do we know what is core? This is where we have to bring together two vital groups of individuals into one cohesive, collaborative team: Domain Experts and software developers.

The Domain Experts will naturally be more focused on business concerns. Their thoughts will be centered on their vision of how the business works. In the domain of Scrum, count on the Domain Expert being a Scrum Master who thoroughly understands how Scrum is executed on a project.

然而，我们该如何确定核心？为此，我们必须将两个重要的群体一一领域专家（Domain xper）和软件开发人员，整合成一个有凝聚力的协作团队。领城专家自然会更加关注业务问题。他们的想法会集中在组织如何运作的愿景上。Scrum 的业务领域中，我们期望领域专家是一位 Scrum Master 1，他完全了解如何在项目中实施 Scrum。

1 Scrum Master，是组成 Scrum 团队的三个角色之一，也是 Scrum 团队的敏捷教练。请参考《Scrum 精髓》[Essential Scrum]，——译注

『

Product Owner or Domain Expert?

You may wonder what the difference is between a Scrum product owner and a DDD Domain Expert. Well, in some cases they might be one and the same, that is, one person capable of filling both roles. Yet it should not be surprising that a product owner is typically more focused on managing and prioritizing the product backlog and seeing to it that the conceptual and technical continuity of the project is maintained. This doesn’t mean, however, that the product owner is naturally an expert in the business’s core competency in which you are working. Make sure that you have a true Domain Expert on the team, and don’t substitute a product owner without the necessary know-how instead.

你可能会疑惑，Scum 中的产品负责人与 DDD 中的领域专家之间的区别是什么。在某些情况下，他们可能是同一个人，也就是说，一个人承担两个角色。产品负责人常常更加关注管理和产品待办项的优先级排序，并时刻留意着项目的概念和技术是否保持着连续性，这一点也不足为奇。但这并不意味着产品负责人天生就是领城内的业务核心竟争力方面的专家。我们要确保团队中有真正的领城专家，还要避免让缺乏必要专业技能的产品负责人代替领域专家。

』

In your particular business, you also have Domain Experts. It’s not a job title but rather describes those who are primarily focused on the business. It’s their mental model that we start with to form the foundation of the team’s Ubiquitous Language.

On the other hand, developers are focused on software development. As depicted here, developers can become consumed by programming languages and technologies. Yet developers working in a DDD project need to carefully resist the urge to be so technically centered that they cannot accept the business focus of the core strategic initiative. Rather, the developers should reject any uncalled-for terseness and be able to embrace the Ubiquitous Language that is gradually developed by the team inside their particular Bounded Context.

2『精辟啊， It’s their mental model that we start with to form the foundation of the team’s Ubiquitous Language. 做一张金句卡片。』——已完成

在特定的业务领域中，你还是需要领域专家的。这不仅是一个职称，而是形容那些主要专注于业务的人。领域专家的心智模型将会成为团队通用语言的坚实基础。另一方面，开发人员专注于软件开发。如图所示，开发人员将精力花费在编程语言与技术研究中。然而，在 DDD 项目的实施过程中，开发人员需要尽量克制这种「以技术为中心」的冲动，以防无法接受以业务为中心的核心战略举措。相反开发人员应当抛弃任何多余的技术洁癖 1，并拥抱团队在特定限界上下文中逐步发展的通用语言。

1 在此过程中，开发人员会不由自主地进入「编码实现」的惯性思维模式，比如：这个概念应该设计怎样的关系型数据表，把这个概念设计成一个 REST 资源怎么样，这个概念需要使用一个抽象类来实现方便未来的扩展，等等。这些是过往的经验、对某种技术的偏好或者组织规范的要求而导致的，一点也不奇怪。但需要注意的是，我们在进行战略设计时，一定要暂时搁置这些关于实现的技术细节。一方面，这时通用语言（概念和需求）依然在发展过程中，我们会不断地质疑并修正它们，过早地思考针对这些概念和需求的实现没有任何意义。另一方面，如果在现阶段的讨论中就提及这样一些专业的技术术语，只会对领域专家造成干扰，浪费掉和他们协作的宝贵时间。不用着急，我们会在战术设计阶段再来考虑这些关于实现的细节问题。——译注

『

Focus on Business Complexity, Not Technical Complexity

You are using DDD because the business model complexity is high. We never want to make the domain model more complex than it should be. Still, you are using DDD because the business model is more complex than the technical aspects of the project. That’s why the developers have to dig into the business model with Domain Experts !

之所以会采用 DDD，是因为业务模型的高度复杂。我们从未想过让领城模型比其更复杂。不过，也正是因为业务模型比项目的技术特性更加复杂，我们才会使用 DDD。这也是开发人员必须与领域专家一起深入钻研业务模型的原因。

』

Both developers and Domain Experts should reject any tendency to allow documents to rule over conversation. The best Ubiquitous Language will be developed by a collaborative feedback loop that drives out the combined mental model of the team. Open conversation, exploration, and challenges to your current knowledge base result in deeper insights about the Core Domain.

开发人员和领域专家都应该拒绝任何以文档为主要交流手段的倾向。最佳的通用语言是通过协作反馈循环而发展出来的，从中可以促成团队形成共同的心智模型。对当前知识领域的开放式讨论、探索和质疑都会深化团队对于核心城的认知。

### 2.4 Challenge and Unify

Now back to the question “What is core?” Using the previously out-of-control and ever-expanding model, let’s challenge and unify!

现在让我们回到之前的问题：「什么是核心？」就之前已然失控并无限扩展的业务模型而言，我们要对它提出质疑并将其统一。

One very simple challenge is to ask whether each of the large-model concepts adheres to the Ubiquitous Language of Scrum. Well, do they? For example, Tenant , User , and Permission have nothing to do with Scrum. These concepts should be factored out of our Scrum software model.

一个非常简单的质疑是，每个大型模型的概念是否都符合 Scrum 通用语言的要求？真的如此吗？例如，Tenant、User 和 Permission 都与 Scrum 无关。这些概念都应该从 Scrum 的软件模型中剥离出去。

Tenant, User, and Permission should be replaced by Team, ProductOwner, and TeamMember. A ProductOwner and a TeamMember are actually Users in a Tenancy , but with ProductOwner and TeamMember we adhere to the Ubiquitous Language of Scrum. They are naturally the terms we use when we have conversations about Scrum products and the work a team does with them.

Tenant、User 和 Permission 应该被 Team、ProductOwner 和 TeamMember 取代。虽然 ProductOwner 和 TeamMember 实际上是一个 Tenant 中的 User，但使用它们更符合 Scrum 的通用语言。当讨论 Scrum 的产品和团队任务时，它们是我们脱口而出的术语。

Are SupportPlans and Payments really part of Scrum project management? The answer here is clearly “no.” True, both SupportPlans and Payments will be managed under a Tenant’s Account, but these are not part of our core Scrum language. They are out of context and are removed from this model.

SupportPlans 和 Payments 真的是 Scrum 项目管理的一部分吗？答案显然是「不」，的确，它们都将在 Tenant 的 Account 下进行管理，但并不是 Scrum 的核心通用语言。它们脱离了 Scrum 上下文，将会从模型中移除。

What about introducing Human Resource Utilization concerns? It’s probably useful to someone, but it’s not going to be directly used by TeamMember Volunteers who will work on BacklogItemTasks. It’s out of context.

引入人力资源利用率（Human Resource Utilization）的概念会有什么问题吗？对于某些人而言它可能有用，但它并不会被那些负责 BacklogItemTasks 的 Team Member Volunteer 直接使用。它不属于 Scrum 上下文。

After the addition of the Team, ProductOwner, and TeamMember, the modelers realized that they were missing a core concept to allow TeamMembers to work on Tasks. In Scrum this is known as a Volunteer. So, the Volunteer concept is in context and was included in the language of the core model.

在添加团队、产品负责人和团队成员后，建模者意识到他们遗漏了一个核心的概念，当缺少这个概念时，TeamMember 将无法自愿认领 Task。这就是 Scrum 中的 Volunteer。因此，Volunteer 的概念属于 Scum 上下文，并包含在核心模型的通用语言中。

Even though calendar-based Milestones, Retrospectives, and the like are in context, the team would prefer to save those modeling efforts for a later sprint. They are in context, but for now they are out of scope.

尽管日历中的 Milestones、Retrospectives 等类似的概念都属于 Scrum 上下文，但团队更愿意将为其建模的工作留给接下来的冲刺。它们属于这个上下文，但目前已经超出了交付范围。

Finally, the modelers want to make sure that they account for the fact that threaded Discussions will be part of the core model. So they model a Discussion. This means that Discussion is part of the team’s Ubiquitous Language, and thus inside the Bounded Context.

最后，建模者希望确保考虑到的主题 Discussion 概念也将成为核心模型的一部分。为此，他们构建了一个 Discussion 模型。这意味着 Discussion 是团队通用语言的部分，并属于核心限界上下文。

These linguistic challenges have resulted in a much cleaner and clearer model of the Ubiquitous Language. Yet how will the Scrum model fulfill needed Discussions? It would certainly require a lot of ancillary software component support to make it work, so it seems inappropriate to model it inside our Scrum Bounded Context. In fact, the full Collaboration suite is out of context. The Discussion will be supported by integrating with another Bounded Context —the Collaboration Context.

对于这些语言的质疑使得通用语言的模型越来越清晰。然而，Scrum 模型将如何实现必要的讨论（Discussion）？这里肯定需要许多辅助的软件组件的支持，直接在 Scrum 限界上下文中对其建模似乎是不合适的。事实上，整套协作（Collaboration）的概念都不属于 Scrum 上下文。讨论将通过与另外一个限界上下文，协作上下文的集成获得支持。

After that walk-through, we’re left with a much smaller actual Core Domain. Of course the Core Domain will grow. We already know that Planning, Retrospectives, Milestones, and related calendar-based models must be developed in time. Still, the model will grow only as new concepts adhere to the Ubiquitous Language of Scrum.

在这次练习之后，我们将会留下一个小巧却实际得多的核心域。当然，核心域将会持续扩展。我们已经知道必须尽快开发 Planning、Retrospectives、Milestones 以及其他基于日历的模型。尽管如此，只有当新的概念符合 Scrum 的通用语言时，才会扩展核心。

And what about all the other modeling concepts that have been removed from the Core Domain? It’s quite possible that several of the other concepts, if not all, will be composed into their own respective Bounded Contexts, each adhering to its own Ubiquitous Language. Later you will see how we integrate with them using Context Mapping.

那么，我们该如何从核心域中分离出其他的建模概念呢？其他的几个概念，即便不是全部，都有很大的可能被放到不同的限界上下文中，并且都要遵循各自的通用语言。稍后你将了解我们是如何通过上下文映射来集成它们的。

### 2.5 Developing a Ubiquitous Language

So how do you actually go about developing a Ubiquitous Language within your team as you put into practice one of the chief tools provided by DDD? Is your Ubiquitous Language formed from a set of well-known nouns? Nouns are important, but often software developers put too much emphasis on the nouns within a domain model, forgetting that spoken language is composed of far more than nouns alone. True, we have mainly focused on nouns within our previous sample Bounded Contexts to this point, but that’s because we were interested in another aspect of DDD, that of constraining a Core Domain down to essential model elements.

当你将 DDD 的主要工具之一付诸实践时，是如何在团队中发展通用语言的呢？这些通用语言是由一系列通俗易懂的名词所组成的吗？名词固然很重要，但开发人员在领域模型中往往过于强调名词，而忘记了名词只是口头语言中很小的一部分。诚然，目前为止，在之前的限界上下文示例中我们主要关注的是名词，那是因为当时我们对 DDD 的另一个方面感兴趣，即将核心域限制在最基本的模型元素范围内。

『

Accelerate Your Discovery

You may want to try a few Event Storming sessions as you work on your scenarios. These can help you to quickly understand which scenarios you should be working on, and how they should be prioritized. Likewise, developing concrete scenarios will give you a better idea of the direction that you should take in your Event Storming sessions. They are two tools that work well together. I explain the use of Event Storming in Chapter 7 , “Acceleration and Management Tools .”

在一些场景上工作时，你或许想尝试几次事件风暴（Event Storming）的讨论。这些讨论可以帮助你快速地理解应该投入到哪些场景中，以及如何对这些场景进行优先级排序。同样，创建具体场景将会给你的事件风暴讨论方向带来一些更好的思路。这两种工具能够很好地配合。第 7 章中会介绍事件风暴的用法。（两个工具：事件风暴和创建具体场景。）

』

Don’t limit your Core Domain to nouns alone. Rather, consider expressing your Core Domain as a set of concrete scenarios about what the domain model is supposed to do. When I say “scenarios” I don’t mean use cases or user stories, such as is common in software projects. I literally mean scenarios in terms of how the domain model should work—what the various components do. This can be accomplished in the most thorough way only by collaborating as a team of both Domain Experts and developers.

我们不要将核心域局限在名词上。相反，应当使用一组具体场景来表达核心域，这些场景描述了领域模型应该做的事情。当提及「场景」时，并不是指用例或用户故事这些软件项目中常见的概念。本书所定义的场景，其真正含义是领域模型该如何工作，各种组件该做什么 1。只有领域专家和开发人员组成通力协作的团队，才有可能最大限度地完成这些场景。

1 正如前文所引用的：「绝大部分的人错误地认为设计只关乎外观。人们只理解了表象一一将这个盒子递给设计师，告诉他们：把它变得好看一些！这不是我们对设计的理解。设计并不仅仅是感观，设计也是产品的工作方式。」我们不仅需要认识到设计对于产品重要性，更需要体会通过设计改变产品的内在运作方式可以有效地改善用户的体验。我们对于「场景」的描述，也期望团队不仅仅只是观察到它的表象，更是希望通过不断地协作认知更加清晰地描绘出「场景」背后的运作逻辑。——译注

Here’s an example of a scenario that fits with the Ubiquitous Language of Scrum:

Allow each backlog item to be committed to a sprint. The backlog item may be committed only if it is already scheduled for release. If it is already committed to a different sprint, it must be uncommitted first. When the commit completes, notify interested parties.

Notice that this is not just a scenario about how humans use Scrum on a project. We are not talking about human procedures. Rather, this scenario is a description of how the very real software model components are used to support the management of a Scrum-based project.

下面是一个符合 Scrum 通用语言的场景示例：允许将每一个待办项提交到某个冲刺中。只有待办项位于发布计划中时才能进行提交。对于已经提交过的待办项如果想再次提交到另外一个冲刺中，需要先将其回收。提交完成时，通知相关方取消提交的冲刺与准备提交的冲刺。

请注意，这并不只是一个关于如何在真实的项目中使用 Scrum 的场景。我们不是在讨论人类如何运作 Scrum 的流程，而是描述了如何使用真实的软件模型来支持基于 Scrum 运作的项目管理。

The previous scenario is not a perfectly stated one, and a perk of using DDD is that we are constantly on the lookout for ways to improve the model. Yet this is a decent start. We hear nouns spoken, but our scenario doesn’t limit us to nouns. We also hear verbs and adverbs, and other kinds of grammar. You also hear that there are constraints—conditions that must be met before the scenario can be completed to its successful end. The most important benefit and empowering feature is that you can actually have conversations about how the domain model works—its design.

上述场景的示例陈述得并不完美，而使用 DDD 的额外收获在于我们一直在寻找改进模型的方法。这是一个不错的开端。我们在场景中听到了各种词汇，其中不仅仅有名词，也有动词和副词，还有其他的类型的词。你也会听到一些约束条件，这些约束条件必须在场景顺利完成前得到满足。使用 DDD 带来的最大收获和赋予你的最大能力在于可以真正地通过对话了解领域模型是如何工作的，即它的设计。

We can even draw simple pictures and diagrams. It’s all about doing whatever is needed to communicate well on the team. One word of warning is appropriate here. Be careful about the time spent in your domain-modeling efforts when it comes to keeping documents with written scenarios and drawings and diagrams up-to-date over the long haul. Those things are not the domain model. Rather, they are just tools to help you develop a domain model. In the end the code is the model and the model is the code. Ceremony is for distinguished observances, like weddings, not domain models. This doesn’t mean that you forgo any efforts to freshen scenarios, but only do so as long as it is helpful rather than burdensome.

我们甚至可以绘制一些简单的图画和图表。这些方式都是为了帮助团队进行良好的沟通。这里适当地提醒一句，当心你在建模工作中对文字场景、图画、图表这些文档长期保持同步花费过长的时间。2 这些文档并不是领域模型。相反，它们只是帮助你开发领域模型的工具。模型终将与代码融为一体。只有像婚礼这样的重要活动才需要仪式，而领域模型并不需要这些仪式。这并非意味着你不需要为更新场景付出努力，而是应该在正确的时候做正确的事。

 2 请回忆敏捷宣言，「工作的软件高于详尽的文档」。文档只是一种工具，对于用户而言并不能产生价值，所以在产品的研发过程中，利用轻量级的文档（例如 Wiki）去记录一些关键信息和共识足以。一一译注

What would you do to improve a part of the Ubiquitous Language in our previous example? Think about it for just a minute. What’s missing? Before too long you probably wish for an understanding of who does the committing of backlog items to a sprint. Let’s add the who and see what happens:

The product owner commits each backlog item to a sprint . . .

对于之前的示例，你会做些什么来完善这部分通用语言？思考ー下，有什么遗漏吗？很快你会恍然大悟：谁将会把待办项提交到冲刺中？让我们加上谁，看看会发生什么：产品负责人提交每个待办项到一个冲刺中......

You will find in many cases that you should name each persona involved in the scenario and give some distinguishing attribute to other concepts such as to the backlog item and sprint. This will help to make your scenario more concrete and less like a set of statements about acceptance criteria. Still, in this particular case there isn’t a strong reason to name the product owner or further describe the backlog item and sprint involved. In this case all product owners, backlog items, and sprints will work the same way whether or not they have a concrete persona or identity. In cases where giving names or other distinguishing identities to concepts in the scenario helps, use them:

The product owner Isabel commits the View User Profile backlog item to the Deliver User Profiles sprint . . .

你将发现在多数情况下你需要给场景中的每个人物命名，并赋予他们一些和待办项冲刺等这些其他概念有区别的属性。这有助于将场景描述得更加有血有肉，而不只是一堆验收标准的陈述。然而，在这种特殊的情境下，很难找到一个强有力的理由去写清楚产品负责人的名字，或进一步描述涉及的待办项与冲刺。此时，无论是否拥有一个具体的人物角色或身份，所有的产品负责人、待办项和冲刺都会遵循相同的业务规则。如果需要给场景中的概念提供名字或有区别的身份，请这样做：产品负责人 Isabel 提交查看用户设置待办项到交付用户设置冲刺中......

Now let’s pause for a moment. It’s not that the product owner is the sole individual responsible for deciding that a backlog item will be committed to a sprint. Scrum teams wouldn’t like that very much, because they would be committed to delivering software within some time frame that they had no say in determining. Still, for our software model it may be most practical for a single person to have the responsibility to carry out this particular action on the model. So in this case we have stated that it’s the product owner role that does this. Even so, the nature of Scrum teams forces the question “Is there anything that must be done by the remainder of the team to enable the product owner to perform the commitment?”

这里并不是说产品负责人是唯一可以决定将待办项提交到冲刺中的人。Scrum 团队也不会喜欢这样，因为这要求团队承诺在一段时间内交付软件，同时他们却对决定没有任何发言权。尽管如此，对于我们软件模型交付而言，最切合实际的方式仍旧是让一个人负责在模型上执行这个特殊的动作。就这个例子来说，我们主张由产品负责人担任这一角色并执行这一动作。即便如此，Scrum 团队的天性一定会让他们抛出这样的问题：「团队里的其他成员还要做些什么，才能让产品负责人执行提交动作？」

Do you see what has happened? By challenging the current model with the who question, we have been led to an opportunity for deeper insight into the model. Perhaps we should require at least some team consensus that a backlog item can be committed before actually allowing the product owner to carry out the commit operation. This could lead to the following refined scenario:

The product owner commits a backlog item to a sprint. The backlog item may be committed only if it is already scheduled for release, and if a quorum of team members have approved commitment . . .

你看到这里发生的一切了吗？通过使用谁这个问题不断地质疑当前的模型，我们得到一个深入理解模型的机会。在允许产品负责人执行提交动作之前，也许我们至少需要对这一个待办项是否可以被提交达成一些团队共识。这会将场景优化成下面这样：产品负责人提交待办项到冲刺中。只有待办项位于发布计划中时才能进行提交，而且需要赞成承诺的团队成员达到法定人数…...

OK, now we have a refined Ubiquitous Language , because we have identified a new model concept called a quorum. We decided that there must be a quorum of team members who agree that a backlog item should be committed, and there must be a way for them to approve commitment. This has now introduced a new modeling concept and some idea that the user interface will have to facilitate these team interactions. Do you see the innovation unfolding?

There is another who missing from the model. Which one? Our opening scenario concluded: When the commit completes, notify interested parties.

很好，现在的我们的通用语言变得更加准确，这是因为我们识别出了一个新的模型概念，叫作法定人数（Quorum）。我们决定，只有待办项得到法定人数的团队成员同意后才能被提交，并且必须要有一种赞成（Approve）承诺的方法。我们现在引入了一个新的建模概念和一些有助于团队交流的用户界面的新想法。你是否看到了创新？我们还遗漏了模型中的另一个谁。之前的场景是这样结尾的：当待办项的提交完成后，需要通知相关方。

Who or what are the interested parties? This question and challenge further lead to modeling insights. Who needs to know when a backlog item has been committed to a sprint? Actually one important model element is the sprint itself. The sprint needs to track total sprint commitment, and what effort is already required to deliver all the sprint’s tasks. However you decide to design the sprint to track that, the important point now is for the sprint to be notified when a backlog item is committed to it:

If it is already committed to a different sprint, it must be uncommitted first. When the commitment completes, notify the sprint from which it was uncommitted and the sprint to which it is now committed.

相关方是何人何物？这个疑问将引导我们进一步思考这些建模。当提交待办项到冲刺中时，谁会需要知道？实际上，一个重要的模型元素是冲刺本身。冲刺需要跟踪其中承诺的待办项总数，以及交付所有冲刺任务所需要投入的工作量。不管怎样，你决定冲刺要设计成可以跟踪这些信息，此时设计的重点是在待办项提交到冲刺时通知它：对于已经提交过的待办项想再次提交到另外一个冲刺中，那么需要先将其回收。提交完成后时，需要通知相关方（相关的冲刺）。

Now we have a fairly decent domain scenario. This concluding sentence has also led us to an understanding that the backlog item and the sprint may not necessarily be aware of commitment at the same time. We need to ask the business to be certain, but it sounds like a great place to introduce eventual consistency. You will see why that is important and how it is accomplished in Chapter 5 , “Tactical Design with Aggregates .”

The refined scenario in its entirety looks like this:

The product owner commits a backlog item to a sprint. The backlog item may be committed only if it is already scheduled for release, and if a quorum of team members have approved commitment. If it is already committed to a different sprint, it must be uncommitted first. When the commitment completes, notify the sprint from which it was uncommitted and the sprint to which it is now committed.

1『上面的信息是提炼后的领域场景，需要反复读，一定要有能力将自己的业务逻辑提炼成类似的场景描述。』

现在我们有了一个相当不错的领域场景。结尾的这句话令我们了解到，待办项与冲刺可能不需要在同一时间知晓待办项的提交状态。我们需要询问业务来确定，但这听起来像是引入最终一致性（Eventual Consistency）的好去处。在第 5 章中，你将会明白为什么最终一致性非常重要，以及如何达成它。

优化后的完整场景如下所示：产品负责人提交待办项到冲刺中。只有待办项位于发布计划中时才能进行提交，而且需要赞成承诺的团队成员达到法定人数。如果待办项已经提交到另外一个冲刺中，那么需要先将其回收。当待办项的提交完成后时，需要通知相关方（相关的冲刺）。

How would a software model actually work in practice? You can well imagine a very innovative user interface supporting this software model. As a Scrum team is participating in a sprint planning session, team members use their smartphones or other mobile devices to add their approval to each backlog item as it is discussed and agreed upon to work on during the next sprint. The consensus of the quorum of team members approving each of the backlog items gives the product owner the ability to commit all of the approved backlog items to the sprint.

实际的软件模型是如何工作的？你可以设想用一个非常有创意的用户界面来支撑这个软件模型。当 Scrum 团队正在进行一场冲刺计划会议时，团队成员们在讨论每个待办项时，会借助智能手机或其他移动设备投出他们的赞成票，这些待办项已被讨论并同意在下一个冲刺中完成。赞成每个待办项的团队成员达到法定人数后，产品负责人才能将所有赞成通过的待办项提交到冲刺中。

#### 2.5.1 Putting Scenarios to Work

You may be wondering how you can make the transition from a written scenario to some sort of artifact that can be used to validate your domain model against the team’s specifications. There is a technique named Specification by Example [Specification] that can be used; it’s also called Behavior-Driven Development [BDD] . What you are trying to achieve with this approach is to collaboratively develop and refine a Ubiquitous Language , model with a shared understanding, and determine whether your model adheres to your specifications. You will do this by creating acceptance tests. Here is how we might restate the preceding scenario as an executable specification:

你可能想知道如何把书面场景转换成某种可以用来验证领域模型是否符合团队需求说明的产出物。可以采用一种被称为实例化需求「Specification」的技术，它也被称为行为驱动开发 [BDD] 1。你期望通过这种方法达到这些效果：协作发展并完善通用语言、团队共识建模，以及确定模型是否符合需求说明的要求。我们可以通过创建验收测试 [2] 来达到这些效果。下面是将之前的场景重新表述为可执行的需求说明之后的例子：

1 Behavior Driven Development，行为驱动开发是一种敏捷软件开发方法，它鼓励软件项目中的开发者测试和业务人员之间的协作，包括验收测试和客户测试驱动等实践。实例化需求（Specification by Example, SBE）也是一种用于定义软件产品的需求和面向业务的功能测试的协作方法，它和行为驱动开发表达的是同样的概念，采用的也是同样的实践。实例化需求的介绍请参考同名书籍《实例化需求》[Specification]。——译注

2『已下载书籍「2020156实例化需求 | 2020156Specification-by-Example」。敏捷开发的相关知识首选去看之前下载的书籍「2020139Scrum敏捷软件开发」和「2020140用户故事与敏捷方法」。』

2 验收测试通常指面向业务（用户）的（功能）测试，因此它还承载着衔接需求说明和测试代码的职责。验收测试最好使用业务人员、开发人员、测试人员都能理解的「语言」来描述，尽可能避免需求理解的偏差。在敏捷开发方法中，我们推崇使用用户故事中的验收条件来描述需求，它采用自然语言和「假如 / 当 / 那么」（Given/When/Then）的固定格式。这里验收测试的场景和用户故事中的验收条件几乎一模样。这些场景使用一种简单的编程语言 Gherkin 编写，它是行为驱动开发框架 Cucumber 的一部分。这些场景中的每一行语句都可以被 Cucumber 框架映射成支撑代码来执行。它支持包括中文在内的 60 种自然语言，这里的代码我们也使用了它支持的中文保留字来实现。一一译注

```
Scenario: The product owner commits a backlog item to a sprint

Given a backlog item that is scheduled for release

And the product owner of the backlog item

And a sprint for commitment

And a quorum of team approval for commitment

When the product owner commits the backlog item to the sprint

Then the backlog item is committed to the sprint

And the backlog item committed event is created

场景：产品负责人提交待办项到冲刺中

假知，待办项已经为发布排期

并且，有待办项的产品负责人

并且，有需要承诺的冲刺

并且，有法定数量的团队成员赞成承诺

当，产品负责人提交待办项到冲刺中

那么，待办项被提交到冲刺中

并且，待办项已提交的事件被创建
```

With a scenario written in this form, you can create some backing code and use a tool to execute this specification. Even without a tool, you may find that this form of scenario authoring with its given/when/then approach works better than the previous scenario authoring example. Yet executing your specifications as a means of validating the domain model may be hard to resist. I comment on this further in Chapter 7 , “Acceleration and Management Tools .”

You don’t have to use this form of executable specification in order to validate your domain model against your scenarios. You can use a unit testing framework to accomplish much the same thing, where you create acceptance tests (not unit tests) that validate your domain model:

1『绝妙啊，用单元测试来验证领域模型，一石二鸟，因为自己本来就要写单元测试的，果然软件开发里的几个最佳实践都是串起来的：重构、单元测试、领域模型、设计原则、设计模式......』

通过这种形式编写的场景，你可以实现一些支撑代码，并使用工具来执行该需求说明。即便没有工具，你也会发现这种「假如 / 当 / 那么」（Given/When/Then）的场景编写方式比之前的例子要好。然而，可执行的需求说明作为验证领域模型的方法着实让人难以抗拒 1。后面的第 7 章中，会对其进一步点评。你并非一定要使用这种形式的可执行需求说明来验证场景与领域模型是否一致。你也可以使用单元测试框架来达成同样的目标，通过它创建验收测试（不是单元测试）来验证领域模型：

1 这里要提醒读者，行为驱动开发是一组实践方法，Cucumber 等框架只是实践行为驱动开发的可选工具中的一种。通过 Cucumber 框架刻意追求验收测试的自动化是一种狭义的认知。行为驱动开发框架不是自动化测试的银弹，不要期望它能轻易自动地解决你在场景验收中的所有问题。验收测试意味着对系统功能进行完整的端到端的测试，这样的测试牵涉到从数据库到用户界面的方方面面，实施自动化的成本特别高。在具体的实施过程中，需要根据产品 / 项目的实际情况,比如资金、人力资源、时间、组织架构等，合理选择投入的方式与切入点。我们建议学习并理解测试金字塔，来帮助你构建更合理的自动化则试体系。——译注

1『测试金字塔相关的知识，目前的认知就是多些底部的单元测试。（2020-08-05）』

```js
/*

The product owner commits a backlog item to a sprint.

The backlog item may be committed only if it is already scheduled for release, and if a quorum of team members

have approved commitment. When the commitment completes,

notify the sprint to which it is now committed.

*/

[Test]

public void ShouldCommitBacklogItemToSprint()

{

// Given

var backlogItem = BacklogItemScheduledForRelease();
var productOwner = ProductOwnerOf(backlogItem);
var sprint = SprintForCommitment();
var quorum = QuorumOfTeamApproval(backlogItem, sprint);

// When

backlogItem.CommitTo(sprint, productOwner, quorum);

// Then

Assert.IsTrue(backlogItem.IsCommitted());

var backlogItemCommitted =
    backlogItem.Events.OfType<BacklogItemCommitted>().SingleOrDefault();

Assert.IsNotNull(backlogItemCommitted);

}
```

This unit-test-based approach to acceptance testing accomplishes the same goal as the executable specification. The advantage here may be the ability to write this kind of scenario validation more rapidly but at the cost of some readability. Still, most Domain Experts should be able to follow this code with some help from the developer. When using this approach it would probably work best to maintain the document form of the scenario associated with the validation code in comments, as seen in this example.

Whichever approach you decide on, both will generally be used in a red-green (fail-pass) fashion, where your specification will first fail when run, because there is no implementation of domain model concepts yet to be validated. You stepwise refine your domain model through a series of red results until you fully support your specification and the validations pass (you see all green). These acceptance tests will be directly associated with your Bounded Context and kept in its source code repository.

这种基于单元测试的验收测试方法实现的目标与可执行的需求说明相同。其优势在于可以更快完成这种场景验证的编写，但会牺牲一定的可读性。尽管如此，大部分的领域专家都应能在开发人员的协助下读懂这些代码 1。如本例所示，使用这种方法时，在验证代码的注释中维护文档形式的相关场景可能效果更好。

1 理想很丰满现实却骨感：极少有业务人员愿意编写甚至是阅读这种的验收测试「代码」。即便是使用行为驱动开发框架编写的场景也很难激起业务人员的阅读兴趣。而且，也不是所有的验收测试或场景都能自动化。所以，最现实的一种解决方法就是，业务人员按照自己的喜好选择工具，按照验收条件的格式编写需求说明，团队选出最值得做自动化的那些，由开发人员和测试人员将它们「翻译」成自动化测试脚本。这些测试脚本由开发人员和测试人员维护，根据场景的变化来更新测试脚本，这样才能做到像实例化需求提倡的那样让业务人员编写的需求说明持续地「执行」验证。因此，这种情况下对技术人员更友好的单元测试反而比 Cucumber 这样的框架更受欢迎。

无论你决定采用哪种，这两种方法通常都会遵循红一绿（失败一通过）的形式 1，需求说明首先会运行失败，这是因为待验证的领域模型尚未实现。通过一系列的验证失败（红色），逐步完善领域模型，直到完全支持需求说明并通过验证（全绿）。这些验收测试将会直接与你的限界上下文相关，并保存在限界上下文的源代码库中。

1 此处所提及的红一绿（失败一通过）的形式正是测试驱动开发（Test Driven Development, TDD）所提倡的软件实现方式。测试驱动开发是敏捷开发中的一项核心实践和技术，也是一种设计方法论。它的基本思路就是通过测试来推动整个开发的进行，但测试驱动开发并不只是单纯的测试工作，而是把需求分析、设计、质量控实例化的过程。实际上行为驱动开发也是对测试驱动开发的响应，只不过测试驱动开发多发生在开发人员编写代码时，而行为驱动开发从更早的需求梳理阶段就开始了，参与其中的除了开发人员还有业务人员和测试。关于测试驱动开发的内容请参考 Kent Beck 所著的《测试驱动开发》——译注

1『测试驱动开发和行为测试开发的区别，做一张任意卡片。』——已完成

#### 2.5.2 What about the Long Haul?

Now you may be wondering how we should support the Ubiquitous Language once the innovation has ceased and maintenance sets in. Actually, some of the best learning, or knowledge acquisition, takes place over a long period of time, even during what some might refer to as “maintenance.” It is a mistake for teams to take the view that innovation ends when maintenance begins.

Perhaps the worst thing that could happen is for the label “maintenance phase” to be attached to a Core Domain. A continuous learning process is not a phase at all. The Ubiquitous Language that was developed early on must continue to thrive as years pass. True, it may eventually be less significant, but probably not for quite a while. It is all part of your organization’s commitment to a core initiative. If this long-term commitment cannot be made, is this model that you are working on today truly a strategic differentiator, a Core Domain ?

现在，你可能会关心，一旦创新停滞并进入维护期后 2，我们该如何继续维持通用语言？事实上，最佳的学习方式，即知识获取，将在一段很长的时间持续发生，甚至发生在所谓的「维护期」。团队如果认为创新在维护开始时就结束了，这本身就是一个错误。

最糟糕的情况可能是给核心域贴上「维护阶段」的标签。持续学习的过程根本不是图个阶段。早期发展的通用语言必定随着岁月的流逝而不断成长。确实，它终将可能不那么重要，但这也需要相当长的一段时间。它是组织对于核心举措的全部承诺。如果不能做出长期承诺，那么今天你所开发的模型真的是组织的战略差异性所在，即核心域吗？

2 对于一个产品而言，创新贯穿了整个生命周期，从探索到拓展，再到维护，乃至退出，每个阶段都需要持续创新。我们不能将创新局限在新的功能和新的服务上。同时，商业模式、用户体验以及质量改善也都可以是创新的发力点。当产品进入了稳定期或是维护期时，我们需要在现有的高价值业务流程上延伸出新的创新，有时是入口创新，如近几年很多成功的产品，都从 PC 端转向了移动端，但核心的用户体验或是业务场景还是以原有的为主。有时候是模式创新，如 Microsoft 从多年的 Office 私有化服务最终转向了公有云的商业模式，并一举获得了巨大的成功。——译注

### 2.6 Architecture

There is another question that you may have wondered about. What’s inside a Bounded Context? Using this Ports and Adapters [IDDD] architecture diagram, you can see that a Bounded Context is composed of more than a domain model.

These layers are common in a Bounded Context: Input Adapters , such as user interface controllers, REST endpoints, and message listeners; Application Services that orchestrate use cases and manage transactions; the domain model that we’ve been focusing on; and Output Adapters such as persistence management and message senders. There is much to be said about the various layers in this architecture, and it is too elaborate to state in this distilled book. See Chapter 4 of Implementing Domain-Driven Design [IDDD] for an exhaustive discussion.

1『这里的框架图直觉上非常非常重要。在限界上下文这个框架里可以包含多个层级的模型：1）输入适配器。2）应用层服务。3）领域模型。4）输出适配器。』

还有一个你可能想了解的问题。限界上下文内会有什么？当使用端ロ (Port）和适配器（Adapters）[IDDD] 1 的架构图时，你会发现限界上下文的组成绝不仅仅只是一个领域模型。

1 这种架构也称为六边形架构，最早由 Alistair Cockburn 提出。和传统的「数据一应用一展现」的「自下而上」的三层应用架构不同，端口和适配器的「应用一端口一适配器」是「由内向外」的三层架构。它将核心业务逻辑（应用层或领域层）和外层的 API 接口（端口层）以及外部各种具体实现的依赖（适配器层，如各种前端界面、数据库、第三服务、消息机制等）解耦开。通过依赖注入等手段让架构更具灵活性和可扩展性的同时，也让团队把更多的精力聚焦在核心的应用层（领域模型）上。Robert C. Martin 提出的整洁架构（Clean Architecture）也是此架构的变种。请参考《实现领域驱动设计》IDDD 第 4 章的详细介绍。一一译注

『

Technology-Free Domain Model

Although there will be technology scattered throughout your architecture, the domain model should be free of technology. For one thing, that’s why transactions are managed by the application services and not by the domain model.

虽然在整个架构体系中遍布着各种技术，但领域模型本身与技术无关。这就是为什么事务是由应用服务管理，而不是由领域模型来管理的原因。

』

Ports and Adapters can be used as a foundational architecture, but it’s not the only one that can be used along with DDD. Along with Ports and Adapters, you can use DDD with any of these architectures or architecture patterns (and others), mixing and matching them as needed:

1. Event-Driven Architecture; Event Sourcing [IDDD]. Note that Event Sourcing is discussed in this book in Chapter 6 , “Tactical Design with Domain Events .”

2. Command Query Responsibility Segregation (CQRS) [IDDD] .

3. Reactive and Actor Model; see Reactive Messaging Patterns with the Actor Model [Reactive] , which also elaborates on the use of the Actor model with DDD.

4. Representational State Transfer (REST) [IDDD] .

5. Service-Oriented Architecture (SOA) [IDDD] .

6. Microservices are explained in Building Microservices [Microservices] as essentially equivalent to DDD Bounded Contexts , so both the book you are reading and Implementing Domain-Driven Design [IDDD] discuss the development of microservices from that perspective.

7. Cloud computing is supported in much the same way as microservices, such that anything you read in this book, in Implementing Domain-Driven Design [IDDD] , and in Reactive Messaging Patterns with the Actor Model [Reactive] is applicable.

我们可以使用端口和适配器作为一种基础架构，但这不是在 DDD 中唯一可用的架构。除了端口和适配器，你可以在 DDD 中使用任何架构，或架构模型（或是其他），并可以根据需要进行匹配或是混合使用。1）事件驱动架构，事件溯源「IDDD」。在本书第 6 章中将会讨论事件溯源。2）命令和查询职责分离（CQRS）[IDDD] 1。3）响应式架构和 Actor 模型 2：参阅《响应式架构：消息模式 Actor 实现与 Scala、Akka 应用集成》[Reactive]，它说明了如何结合 DDD 运用 Actor 模型。4）具象状态传输（REST）[IDDD] 3。4）面向服务的架构（SOA）[IDDD] 4。5）《微服务设计》[Microservices] 一书中解释了微服务本质上等同于 DDD 中的限界上下文，所以本书和《实现领域驱动设计》[IDDD] 都是从这个视角讨论微服务开发的。6）云计算和微服务以一样的方式得到支持，同样的内容可以在本书、《实现领域驱动设计》以及《响应式架构：消息模式 Actor 实现与 Scala、Akka 应用集成》中读到 5。

1 命令与查询职责分离（Command Query Responsibility Segregation, CQRS）和传统的 CRUD 模式不一样，它把同一个模型的无副作用查询操作和改变状态的修改操作（通常称为命令）分开。两部分可以分别在不同的模块和服务实现，可以分别部署到不同的硬件或基础设施上，甚至可以使用完全不同的数据存储方式。例如，改变状态的命令经常会采用事件溯源来实现。这种架构特别适合需要高性能且查询和命令的扩展性有不同要求的应用（或者服务），它们可以根据自己的需要分别采用不同的方式进行扩展。当然，随之而来的是架构复杂性的增加，在使用之前需要谨慎地权衡，选择合适的服务或模块应用这种架构。——译注

2 在 Actor 模型中，每个 Actor 都可以被看成是一致性边界和一个独立的业务单元，可以和 DDD 中的聚合概念完美对接。——译注

3 具象状态传递（Representational State Transfer, REST）是 2000 年 Roy Fielding 博士在他的博士论文中提出来的一种软件架构风格。REST 围绕资源这个核心概念定义了一套标准的方法，而这套方法正好和 HTTP 的动词以及状态码匹配。随着互联网的发展，REST 几乎成了 API 定义以及微服务通信的事实标准。REST 会在 DDD 的上下文映射中得到应用。但需要注意的是，REST 并不是真正意义上的标准，对它的理解和实现可谓百花齐放。在使用这种风格之前，请参考 Richardson Maturity Model 和一些公开的 API 设计范例（如 Github API），来了解 REST 的最佳实践。此外，REST 也不是唯一的选择，还有 gRPC 和 graphQL 这样的替代方案（就像 REST 替代 SOAP 一样）。一一译注

4 面向服务的架构（Service Oriented Architecture, SOA）是一个组件模型，它将应用程序的不同功能单元（称为服务）通过这些服务之间定义良好的接口和契约联系起来。我们经常会看见 SOA 和微服务的比较，但实际上微服务和 SOA 一脉相承，可以认为是 SOA 的一种特定的现代的实现。微服务相对于 SOA 更注重对独立业务单元的拆分来形成清晰的边界，并采用轻量级的通信机制，以一种更加松耦合的方式进行集成，来提供更好的扩展性和灵活性。同时，借助 Devops 和云平台的东风，微服务可以由单个独立的小团队开发、部署和运维。因此，微服务已经成为现代分布式系统的首选架构，也成了遗留架构首选的演进和重构方向。微服务强调的服务边界和 DDD 提倡的限界上下文可谓不谋而合，因此，DDD 方法在在微服务的设计和拆分中得到了广泛的应用。——译注

5 充分利用云计算优势构建和运行的应用被称为云原生（Cloud Native）应用，企业需要借助构建和运行云原生应用和服务的平台，来自动执行并集成 Devops、持续交付、微服务和容器等概念。微服务、事件湖源、CORS 以及 Actor 模型这些架构都可以完美地契合云原生应用和平台。而 Amazon 加入 CNCF  (Cloud Native Computing Foundation）之后，三大云平台供应商（Google、Microsoft 和 Amazon）齐齐聚首，推进了云原生的标准化和最佳实践的普及。一一译注

Another comment on microservices is in order. Some consider a microservice to be much smaller than a DDD Bounded Context. Using that definition, a microservice models only one concept and manages one narrow type of data. An example of such a microservice is a Product and another is a BacklogItem. If this is the granularity that you consider a worthy microservice, understand that both the Product microservice and the BacklogItem microservice will still be in the same larger, logical Bounded Context. The two small microservice components have only different deployment units, which may also have an impact on how they interact (see Context Mapping ). Linguistically they are still within the same Scrum-based contextual and semantic boundary.

另一种关于微服务的解释也很恰当。有些人认为其实微服务要比 DDD 的限界上下文要小得多。按照这种定义，一个微服务模型只包含一个概念，并只用管理一种小类型的数据。例如，产品是一个微服务，待办项是另外一个。如果你认为这样粒度的微服务很有价值，那么你需要理解产品微服务和待办项微服务仍将存在于同一个更大的逻辑限界上下文中。1 即使这两个小型的微服务组件之间的区别仅仅是部署单元不一样，这也会影响它们的交互方式（参考上下文映射）。从语言学上来说，它们仍位于同一个基于 Scrum 的语境和语义边界之内。

2 经常会有一些有关于微服务粒度的讨论，也会有人质疑某个微服务太大或是太小，在这里我们希望重中的观点是，微服务的边界（粒度）是一个设计决策，而没有一个标准答案。因此，我们鼓励对微服务划分的质疑，也鼓励针对划分的探讨。但微服务划分归根结底是架构设计，因此，你需要着重从以下几点展开思考：首先是现有架构间的依赖关系，其次是业务上的可扩展性，再次是团队目前的人员能力，最后则是在实现过程中可能遇到的风险与挑战。这些划分的依据往往也是我们在 DDD 中对上下文和子域进行划分时需要考虑的问题。一一译注

## 0301. Strategic Design with Subdomains

In summary you have learned: 1) What Subdomains are and how they are used, both in the problem space and in the solution space. 2) The difference between a Core Domain , a Supporting Subdomain , and a Generic Subdomain. 3) How you can make use of Subdomains while reasoning about integration with a Big Ball of Mud legacy system. 4) The importance of aligning your DDD Bounded Context one-to-one with a single Subdomain. 5) How you should segregate a Supporting Subdomain model from your Core Domain model using a DDD Module when it is impractical to separate the two in different Bounded Contexts. For exhaustive coverage of Subdomains , see Chapter 2 of Implementing Domain-Driven Design [IDDD] .

When you work on a DDD project, there are always multiple Bounded Contexts in play. One of the Bounded Contexts will be the Core Domain , and there will also be various Subdomains in other Bounded Contexts. In the previous chapter you saw the importance of dividing different models by their specific Ubiquitous Language and forming multiple Bounded Contexts. There are six Bounded Contexts and six Subdomains in the preceding diagram. Because DDD strategic design was used, the teams achieved the most optimal modeling composition: one Subdomain per Bounded Context , and one Bounded Context per Subdomain. In other words, the Agile Project Management Core is both one clean Bounded Context and one clean Subdomain. In some situations, there may be multiple Subdomains in one Bounded Context , but that doesn’t achieve the most optimal modeling outcome.

DDD 项目中总会碰到很多限界上下文（Bouded Contexts）。这些上下文中一定有一个将成为核心域（Core Domain），而其他的限界上下文之中也会存在许多不同的子域（Sub Domain）。第 2 章中，你已经了解了通过特定的通用语言来划分不同模型，并形成多个限界上下文的重要性。上图中有六个限界上下文与六个子城。正是因为采用了 DDD 的战略设计，团队方能实现最佳的建模成果：限界上下文与子域之间一一对应。换句话说，敏捷项目管理核心即一个清晰的限界上下文，也是一个清晰的子域。在某些情况下，一个限界上下文中有可能存在多个子域，但这并非是最理想的建模结果。

### 3.1 What Is a Subdomain?

Simply stated, a Subdomain is a sub-part of your overall business domain. You can think of a Subdomain as representing a single, logical domain model. Most business domains are usually too large and complex to reason about as a whole, so we generally concern ourselves only with the Subdomains that we must use within a single project. Subdomains can be used to logically break up your whole business domain so that you can understand your problem space on a large, complex project.

Another way to think of a Subdomain is that it is a clear area of expertise, assuming that it is responsible for providing a solution to a core area of your business. This implies that the particular Subdomain will have one or more Domain Experts who understand very well the aspects of the business that a specific Subdomain facilitates. The Subdomain also has greater or lesser strategic significance to your business.

If DDD had been used to develop it, the Subdomain would have been implemented as a clean Bounded Context. The Domain Experts who specialize in that particular area of the business would have been members of the team that developed the Bounded Context. Although using DDD to develop a clean Bounded Context is the optimal choice, sometimes we can only wish that had been the case.

简单地说，子域是整个业务领域的一部分。你可以认为子域代表的是一个单一的、有逻辑的领域模型。大多数的业务领域都过于庞大和复杂，难以作为整体来分析，因此我们一般只关心那些必须在单个项目中涉及的子域。子域可以用来逻辑地拆分整个业务领域，这样才能理解存在于大型复杂项目中的问题空间。

也可以认为子域是一个明确的专业领域，假设它负责为核心业务提供解决方案。这意味着特定的子域将会有一位或多位领域专家领衔，他们非常了解由这些特定子域促成的业务的方方面面。对你的业务而言，子域也有或多或少的战略意义。

如果通过 DDD 来创建子域，它将会被实现成一个清晰的限界上下文。特定业务的领域专家将会成为共建限界上下文团队中的一员。虽然使用 DDD 来建立一个清晰的限界上下文是最佳选择，但有时这只是我们一厢情愿的想法。

### 3.2 Types of Subdomains

There are three primary types of Subdomains within a project:

1. Core Domain: This is where you are making a strategic investment in a single, well-defined domain model, committing significant resources for carefully crafting your Ubiquitous Language in an explicit Bounded Context. This is very high on your organization’s list of projects because it will distinguish it from all competitors. Since your organization can’t be distinguished in everything that it does, your Core Domain demarcates where it must excel. Achieving the level of deep learning and understanding required to make such a determination requires commitment, collaboration, and experimentation. It’s where the organization needs to invest most liberally in software. I provide the means to accelerate and manage such projects efficiently and effectively later in this book.

2. Supporting Subdomain: This is a modeling situation that calls for custom development, because an off-the-shelf solution doesn’t exist. However, you will still not make the kind of investment that you have made for your Core Domain. You may want to consider outsourcing this kind of Bounded Context to avoid mistaking it for something strategically distinguishing, and thus investing heavily in it. This is still an important software model, because your Core Domain cannot be successful without it.

3. Generic Subdomain: This kind of solution may be available for purchase off the shelf but may also be outsourced or even developed in house by a team that doesn’t have the kind of elite developers that you assign to your Core Domain or even a lesser Supporting Subdomain. Be careful not to mistake a Generic Subdomain for a Core Domain. You don’t want to make that kind of investment here.

When discussing a project where DDD is being employed, we are most likely discussing a Core Domain.

1、核心域（Sub Domain）：它是一个唯一的、定义明确的领域模型，要对它进行战略投资，并在一个明确的限界上下文中投入大量资源去精心打磨通用语言。它是组织中最重要的项目，因为这将是你与其他竟争者的区别所在。正是因为你的组织无法在所有领域都出类拔萃，所以必须把核心域打造成组织的核心竟争力。做出这样的决定需要对核心域进行深入的学习与理解，而这需要承诺、协作与试验。这是组织最需要在软件中倾斜其投资的方向。后面的章节中会提供加速与高效管理这些项目的方法。

2、支撑子域（Supporting Subdomain）：这类建模场景提倡的是「定制开发」，因为找不到现成的解决方案。对它的投入无论如何也达不到与核心域相同的程度。也许会考虑使用外包的方式实现此类限界上下文，以避免因错误地认为其具有战略意义而进行巨额的投资。这类软件模型仍旧非常重要，核心域的成功离不开它。

3、通用子域（Generic Subdomain）：通用子域的解決方案可以采购现成的，也可以采用外包的方式，抑或是由内部团队实现，但我们不用为其分配与核心域同样优质的研发资源，甚至都不如支撑子域。请注意不要把通用子域误认为是核心域。我们并不希望对其投资过甚。当讨论一个正在实施 DDD 的项目时，最有可能讨论的是核心域。

1 子域的划分，不仅仅涉及实现方式、投资规模，同时还会影响组织的架构、流程。因此，合理的子域划分，以及每个子域恰当的定位，是产品得以顺利发展的重要因素。因此我们需要更好地理解这三种子域的定位。核心域是产品独特的竞争力，它是产品之所以存在的根本。因此在产品的初期，没有经过市场的验证之前，我们需要遵循 MVP (Minimum Viable Product）的原则，快速地迭代以获取市场的反馈，一旦产品被市场证明，合理的重构即需要被发生。支撑子域不需要过度地考虑可扩展性和兼容性，可重用性并非其技术着力的方向，可替代性才是，这也要求我们需要对于支撑子域有着明确的契约规范和业务约束条件。通用子域内的业务规则相对明确，在很多产品和业务上下文中保持高度的重合度，因此我们需要通过快速的采购获取，我们对其定制化要求较低，而稳定性和兼容性则要求较高。——译注

### 3.3 Dealing with Complexity

Some of the system boundaries within a business domain will very likely be legacy systems, perhaps those that your organization has created or those that have been purchased through software licensing. At this point you may not be able to do much about improving those legacy systems, but you still need to reason about them when they have an impact on your Core Domain project. To do so, use Subdomains as a tool for discussing your problem space.

业务领域中的某些系统边界将非常可能是遗留系统，它们也许是由你的组织构建的，也许是通过购买软件许可的方式获得的。此时，可能无法对这些遗留系统进行任何改造，但当它们对核心域产生影响时，就需要我们认真对待。为此，子域可以作为讨论问题空间。

Unfortunately, but true all the same, some legacy systems are so counter to the DDD way of designing with Bounded Contexts that you might even refer to them as unbounded legacy systems. That’s because such a legacy system is what I’ve already referred to as a Big Ball of Mud. In reality the one system is full of multiple tangled models that should have been separately designed and implemented but were jumbled together into one very complex and intertwined mess.

不幸的是，事与愿违，有些遗留系统与强调限界上下文的 DDD 设计方式大相径庭，甚至可以称之为无边界（mounded）遗留系统。这样的遗留系统正是我提到的「大泥球」。事实上，「大泥球」内充满了多个错综复杂的模型，这些模型本应被分别设计并实现，但当它们纠缠在一起时，整个系统会乱成一团。

1『上图的子域分别为：账户子域、订单子域、目录子域、发票子域和物流子域。』

Stated another way, when we are discussing a legacy system there are probably some, even many, logical domain models that exist inside that one legacy system. Think of each of those logical domain models as a Subdomain. In the diagram, each logical Subdomain in the unbounded legacy monolithic Big Ball of Mud is marked off by a dashed box. There are five logical models or Subdomains. Treating the logical Subdomains as such helps us grapple with the complexity of large systems. This makes a lot of sense because it allows us to treat the problem space as if it had been developed using DDD and multiple Bounded Contexts.

The legacy system seems less monolithic and muddy if we imagine separate Ubiquitous Languages , at least for the sake of understanding how we must integrate with it. Thinking about and discussing such legacy systems using Subdomains helps us cope with the harsh realities of a large entangled model. And as we reason using this tool, we can determine the Subdomains that are more valuable to the business and necessary for our project, and those that can be relegated to lesser status.

With that in mind, you can even show the Core Domain that you are working on, or are about to work on, right in the same simple diagram. This will help you understand the associations and dependencies between Subdomains. But I will save the details of that discussion for Context Mapping.

换言之，当我们在讨论某个遗留系统时，其中可能会包含一些甚至许多逻辑领域模型。我们将每个逻辑域模型当成一个子域对待。上图中，无边界遗留单体大泥球中，每个逻辑子城都已经被虚线框标记出来。共有五个逻辑模型或子域。这样处理逻辑子域的方式有助于我们应对大型系统的复杂性。这很有意义，因为我们可以像使用 DDD 和多个限界上下文应对问题空间一样，为其提供解决方案。

如果使用分开的通用语言思考，可能遗留系统就不会成为单体大泥球，这至少也可以帮助我们理解如何与它进行集成。使用子域来思考和讨论此类遗留系统有助于我们应对大型错综复杂模型的残酷现实。当使用这类工具时，我们可以明确那些对业务更有价值、对项目更重要的子域，而其他子域可以降低到次要位置。考虑到这一点，甚至可以通过同样的简单图表展示团队准备或正在构建的核心域。这帮助你了解子域间的关联与依赖。更多的细节内容将留到上下文映射（Context Mapping）中介绍。

When using DDD, a Bounded Context should align one-to-one (1:1) with a single Subdomain. That is, when using DDD, if there is one Bounded Context , there is, as a goal, one Subdomain model in that Bounded Context. It may not always be possible or practical to achieve, but where possible it is important to design in that way. This will keep your Bounded Contexts clean and focused on the core strategic initiative.

1『明确掉了，一个限界上下文对应于一个子域模型。』

If you must create a second model in the same Bounded Context (within your Core Domain ), you should segregate the secondary model from your Core Domain using a completely separate Module [IDDD] . (A DDD Module is basically a package in Scala and Java, and a namespace in F# and C#.) This makes a clear linguistic statement that one model is core and the other is merely supporting. This particular use of segregating a Subdomain is one that you would employ in your solution space.

当使用 DDD 时，限界上下文应该与子域一一对应（1:1）。也就是说，如果存在一个限界上下文，那么它的目标就应该是对应且只对应一个子域模型。想要始终做到这一点很难，但在可能的前提下，尽量以这种方式去建模很重要。这样可以使限界上下文清晰并且始终专注于核心战略举措。

如果必须在同一个限界上下文（核心域）中创建第二个模型，应该使用一个完全独立模块，将该模型从核心域中分离出来 [IDDD]（DDD 的模块基本上等同于 Scala 和 Java 中的包，或者是 F# 和 C# 的命名空间）。DDD 通过清晰的语言声明了一个模型是核心，而另一个只是它的支撑。我们可以在解决方案空间中使用分离子域这种特殊方法。

## 0401. Strategic Design with Context Mapping

In summary, you have learned: 1) About the various kinds of Context Mapping relationships, such as Partnership , Customer-Supplier , and Anticorruption Layer. 2) How to use Context Mapping integration with RPC, with RESTful HTTP, and with messaging. 3) How Domain Events work with messaging. 4) A foundation on which you can build your Context Mapping experience. For thorough coverage of Context Maps , see Chapter 3 of Implementing Domain-Driven Design [IDDD].

In previous chapters you learned that in addition to the Core Domain , there are multiple Bounded Contexts associated with every DDD project. All concepts that didn’t belong in the Agile Project Management Context —the Core Domain —were moved to one of several other Bounded Contexts.

在前面的章节中，已经了解到除了核心域（Sub Domain）之外，每个 DDD 项目还关联着多个限界上下文。所有不属于敏捷项目管理上下文（即核心域）的概念都会被迁移到其他某个限界上下文之中。

You also learned that the Agile Project Management Core Domain would have to integrate with other Bounded Contexts. That integration is known in DDD as Context Mapping. You can see in the previous Context Map that Discussion exists in both Bounded Contexts. Recall that this is because the Collaboration Context is the source of the Discussion , and that the Agile Project Management Context is the consumer of the Discussion .

还了解到，敏捷项目管理核心域必须和其他限界上下文进行集成。这种集成关系在 DDD 中称为上下文映射（Context Mapping）。你可以在上面的上下文映射图（Context Map）中看到，Discussion 同时存在于两个限界上下文（Bounded Context）之中。回忆一下这是因为协作上下文是 Discussion 的来源，而敏捷项目管理上下文是 Discussion 的消费者。

A Context Mapping is highlighted in this diagram by the line inside the dashed box. (The dashed box is not part of the Context Mapping but is used only to highlight the line.) It’s actually this line between the two Bounded Contexts that represents a Context Mapping. In other words, the line indicates that the two Bounded Contexts are mapped in some way. There will be some inter-team dynamic between the two Bounded Contexts as well as some integration.

上图中，上下文映射用虚线框里的线段表示（虚线框不是上下文映射的一部分，只是用于强调中间的线段）。实际上，连接两个限界上下文之间的这条线段就代表了上下文映射。换句话说，这条线段表示这两个限界上下文之间存在着某种形式的映射，包括两个限界上下文之间的集成关系以及团队间的动态关系。

Considering that in two different Bounded Contexts there are two Ubiquitous Languages , this line represents the translation that exists between the two languages. By way of illustration, imagine that two teams need to work together, but they work across national boundaries and don’t speak the same language. Either the teams would need an interpreter, or one or both teams would have to learn a great deal about the other’s language. Finding an interpreter would be less work for both teams, but it could be expensive in various ways. For example, imagine the extra time needed for one team to talk to the interpreter, and then for the interpreter to relay the statements to the other team. It works fine for the first few moments but then becomes cumbersome. Still, the teams might find this a better solution than learning and embracing a foreign language and constantly switching between languages. And, of course, this describes the relationship only between two teams. What if there are a few other teams involved? Similarly, the same trade-offs would exist when translating one Ubiquitous Language into another, or in some other way adapting to another Ubiquitous Language.

考虑到两个不同的限界上下文中存在着两种通用语言（Ubiquitous Language），这条线段也代表着两种语言之间的转译过程。挙个例子，假设有两个团队需要一起工作，但他们位于不同的国家，讲不同的语言。为了解决沟通问题，要么在两个团队间设置一名翻译要么其中一个团或者全部两个团队需要熟练掌握对方的语言。找一名翻译更容易一些，但各方面的开销会显著增加。例如，想一想下面这个场景中所消耗的额外时间：一个团队需要先和翻译沟通，然后由翻译转述给另一个团队。这样做刚开始可能还行，但过一段时间就变成了麻烦。尽管如此，相比学习和接受一门外语并在两者之间来回切换，这些团队可能会认为请翻译是一个更好的解决方案。这还只是涉及两个团队的关系，如果还有更多其他团队参与进来又会怎么样？类似地，将一种通用语言翻译成另一种时，或者以其他某种方式适应另一种通用语言时，也要做出同样的权衡。

When we talk about Context Mapping , what is of interest to us is what kind of inter-team relationship and integration is represented by the line between any two Bounded Contexts. Well-defined boundaries and contracts between them support controlled changes over time. There are several kinds of Context Mappings , both team and technical, that can be represented by the line. In some cases both an inter-team relationship and an integration mapping will be blended.

当我们谈论上下文映射时，我们感兴趣的是连接任意两个限界上下文之间的这条线段究竟代表的是哪种类型的团队间关系和集成关系。它们之间定义清晰的边界和契约可以随着时间发生可控的变化。这条线段表示各种各样的上下文映射，包括团队间的和技术上的在某些情况下，团队间关系和集成映射会被混合在一起。

### 4.1 Kinds of Mappings

What relationships and integrations can be represented by the Context Mapping line? I will introduce them to you now.

#### 4.1.1 Partnership

A Partnership relationship exists between two teams. Each team is responsible for one Bounded Context. They create a Partnership to align the two teams with a dependent set of goals. It is said that the two teams will succeed or fail together. Since they are so closely aligned, they will meet frequently to synchronize schedules and dependent work, and they will have to use continuous integration to keep their integrations in harmony. The synchronization is represented by the thick mapping line between the two teams. The thick line indicates the level of commitment required, which is quite high.

It can be challenging to maintain a Partnership over the long term, so many teams that enter a Partnership may do best to set limits on the term of the relationship. The Partnership should last only as long as it provides an advantage, and it should be remapped to a different relationship when the advantage is trumped by the drain of commitment.

合作关系（Partnership）关系存在于两个团队之间。每个团队各自负责一个限界上下文。两个团队通过互相依赖的一套目标联合起来形成合作关系。一损俱损，一荣俱荣。由于相互之间的联系非常紧密，他们经常会面对同步日程安排和相互关联的工作，他们还必须使用持续集成 [1] 对保持集成工作协调一致。两个团队之间的一致步调使用粗的映射线段表示。粗线段表示两个团队彼此需要高度承诺。

保持长期的合作关系很有挑战性，因此许多进入合作关系的团队可能会尽最大努力为这种关系设置一个期限。只有在能发挥彼此优势时才维持合作关系，而随着承诺的消失，这些优势会不复存在，而这种合作关系应该被重新映射成另外的一种关系。

1 Martin Fowler 对持续集成的定义是：持续集成是一种软件开发实践，即团队开发成员经常集成他们的工作，通常每个成员每天至少集成一次，也就意味着每天可能会发生多次集成。每次集成都通过自动化的构建（包括编译、发布、自动化测试）来验证，从而尽快地发现集成错误。许多团队发现这个过程可以大大减少集成的问题，让团队能够更快地开发内聚的软件。这里介绍的上下文映射本质就是一种集成关系，因此持续集成的实践活动对几乎所有的上下文映射关系而言都是不可或缺的。一一译注

#### 4.1.2 Shared Kernel

A Shared Kernel , depicted on page 54 by the intersection of the two Bounded Contexts , describes the relationship between two (or more) teams that share a small but common model. The teams must agree on what model elements they are to share. It’s possible that only one of the teams will maintain the code, build, and test for what is shared. A Shared Kernel is often very difficult to conceive in the first place, and difficult to maintain, because you must have open communication between teams and constant agreement on what constitutes the model to be shared. Still, it is possible to be successful if all involved are committed to the idea that the kernel is better than going Separate Ways (see the later section).

共享内核（Shared Kernel）用上图中两个限界上下文的交集表示，它描述了这样一种关系：两个（或更多）团队之间共享着一个小规模但却通用的模型。团队必须就要共享的模型元素达成一致。有可能它们当中只有一个团队会维护、构建及测试共享模型的代码。共事内核通常一开始很难理解，也很难维护，这是因为团队之间的沟通必须完全开放，而且他们必须就共享模型的构成不断地达成一致 [1]。但是，只要所有参与者都认同共享内核比各行其道 [2]（参见后面的小节）的方式更好，就有可能获得成功。

1 共享内核常见的一种方式就是将通用模块通过二进制依赖（如 JAR 包或者链接库）的方式共享给所有上下文使用。正如书中所说，持续地就修改进行开放式沟通并达成一致是很困难的，效率也很低。但蓬勃发展的开源软件社区却给我们做出了表率。大部分的开源软件都以二进制库的形式发布，开发者们也很难有直接面对面的沟通机会，但它们的发展和演进一点也不慢。开源软件开发者们会使用各种约定和相应实践进行沟通协作，使用 Github 的拉取请求（Pull Request）来审查代码并接受贡献，或是使用长期支持版本（Long Term Support, LTS）保持固定发布节奏给下游预留升级时间，又或是使用语义化版本（Semantic Version）向下游宣告破坏性修改。因此，越来越多的企业向开源社区学习，搭建基础设施和平台，建立企业的「内源」（内部开源）社区来开鼓励开发团队更高效地进行跨团队的协作。在译者所著的《代码管理核心技术及实践》中有关于「内源」社区的介绍。——译注

2 Separate Ways，借鉴了《领域驱动设计》中的译法，和《实现领域驱动》（IDDD 中的译法「另谋他路」同义。——译注

#### 4.1.3 Customer-Supplier

A Customer-Supplier describes a relationship between two Bounded Contexts and respective teams, where the Supplier is upstream (the U in the diagram) and the Customer is downstream (the D in the diagram). The Supplier holds sway in this relationship because it must provide what the Customer needs. It’s up to the Customer to plan with the Supplier to meet various expectations, but in the end the Supplier determines what the Customer will get and when. This is a very typical and practical relationship between teams, even within the same organization, as long as corporate culture does not allow the Supplier to be completely autonomous and unresponsive to the real needs of Customers.

客户一供应商（Customer-Supplier）描述的是两个限界上下文之间和两个独立团队之间的一种关系：供应商位于上游（图中的 U），客户位于下游（图中的 D）。支配这种关系的是供应商，因为它必须提供客户需要的东西。客户需要与供应商共同制订规划来满足各种预期，但最终却是由供应商来决定客户获得的是什么以及何时获得 [1]。即便是来自于同一个组织的团队，只要企业文化不允许供应商完全自治或无视客户的实际需求，客户一供应商关系也是一种非常典型且现实的关系。

1 和共享内核的映射关系一样，保持客户和供应商之间持续开放的沟通也很重要，持续沟通才能保障供应商按照客户的预期提供集成所需的接口。存在这种集成关系的团队常常会采用一种被称为消费者驱动契约（Consumer Driven Contract, CDC）的实践，通过契约测试来保证上游（生产者或供应商）和下游（消费者或客户）之间的协作。而利用一些工具（如 Pact），客户可以在进行测试时，将对供应商接口的期望记录下来，并将其变成供应商的接口测试，作为供应商持续集成流水线的一部分持续地进行验证。这样供应商可以随时了解自己提供的接口实现是否满足了客户期望。关于消费者驱动契的和契的测试的介绍请参考《微服务设计》第 7 章。关于 Pact 的使用请参考官方文档，一一译注

#### 4.1.4 Conformist

A Conformist relationship exists when there are upstream and downstream teams, and the upstream team has no motivation to support the specific needs of the downstream team. For various reasons the downstream team cannot sustain an effort to translate the Ubiquitous Language of the upstream model to fit its specific needs, so the team conforms to the upstream model as is. A team will often become a Conformist , for example, when integrating with a very large and complex model that is well established. Example: Consider the need to conform to the Amazon.com model when integrating as one of Amazon’s affiliate sellers.

跟随者（Conformist）[1] 关系存在于上游团队和下游团队之间，上游团队没有任何动机满足下游团队 [2] 的具体需求。由于各种原因，下游团队也无法投入资源去翻译上游模型的通用语言来适应自己的特定需求，因此只能顺应上游的模型。例如，当一个团队需要与一个非常庞大复杂的模型集成，而且这个模型已经非常成熟时，团队往往会成为它的跟随者 [3]。例子：在作为亚马逊联盟的卖家进行集成时就需要考虑遵循 Amazon.com 的模型。

1 此处借鉴了《领域驱动设计》中的译法，和《实现领域驱动》中的「遵奉者」同义一一译注

2 很多成对的词语可以表示这种下游依赖上游的类似关系，如：「客户」和「供应商」、「客户端」和「服务端」、「消费」和「生产」，「订阅」和「发布」。这些词语绝大部分情况下在本书中会成对地出现。但有时词语对并不完全「对称」，比如「上游」和「消费」，读者可以结合当时语境理解。 ——译注

3 这种关系对跟随者来说是一把双刃剑。跟随者一方面可以借助上游的生态圈快速地获得用户和流量。而另一方面，跟随者也要严格地遵循上游制订的「游戏规则」，而破坏规则将使自己处于非常被动的境地比如，在国内的移动开发中，无论是 iOS 或是 Android，开发者都特别热衷于实现「动态化」方案，在应用中动态下发和执行代码。这样的方式会使用未公开的隐藏接口，甚至是操作系统的漏洞。一旦这些漏洞和接口被修复或关闭（Apple 和 Google 已经开始这样做了），这些方案将完全失效。无论是出于何种原因（比如快速修复线上问题的 Hotfix），采用这种映射关系将自己的核心域作为上游规则「漏洞」的附庸，实在是不明智的选择。——译注

#### 4.1.5 Anticorruption Layer

An Anticorruption Layer is the most defensive Context Mapping relationship, where the downstream team creates a translation layer between its Ubiquitous Language (model) and the Ubiquitous Language (model) that is upstream to it. The layer isolates the downstream model from the upstream model and translates between the two. Thus, this is also an approach to integration.

Whenever possible, you should try to create an Anticorruption Layer between your downstream model and an upstream integration model, so that you can produce model concepts on your side of the integration that specifically fit your business needs and that keep you completely isolated from foreign concepts. Yet, just like hiring a translator to act between two teams speaking different languages, the cost could be too high in various ways for some cases.

防腐层（Anticorruption Layer）是最具防御性的上下文映射关系，下游团队在其通用语言（模型）和位于它上游的通用语言（模型）之间创建了一个翻译层。防腐层隔离了下游模型与上游模型，并完成两者之间的翻译。所以，这也是一种集成的方式。

但凡有可能，你就应该尝试在下游模型和上游集成模型之间创建一个防腐层，这样才可以在你这端的集成中创造出特别适合业务需求的模型概念，并将外部概念完全地隔离。然而，就像为两个讲不同语言的团队雇佣翻译来解决沟通问题一样，在某些情况下各方面的成本会水涨船高。

1 防腐层可以说是最常见的一种阻止外部技术偏好或领域模型侵入的设计模式。几乎没有什么向题是一个防腐层解决不了的。API 网关就是一种防腐层的具体实现。例如，AWS API Gateway 有一项重要的功能就是要对一些服务端点的请求和响应进行转换，我们可以将外部 REST API 返回的数据通过 AWS API Gateway 重新映射，变成我们期望的符合业务模型的事件或者响应数据。另外，在对遗留单块系统进行拆分时，防腐层也发挥着巨大的作用。有一种对付单块系统的重构方式叫作「抽象分支」（Branch by Abstraction），其中从要拆分的模块中提取出的抽象层就发挥着防腐层的作用，在重构的过程中抵挡着未拆分部分对重构工作的腐蚀。这种修者模式的具体介绍，请参考《服务拆分与架构演进》。一一译注

1『又看到这个观点，软件开发过程中，几乎所有的问题都是可以通过抽象出一层中间层来解决。』

#### 4.1.6 Open Host Service

An Open Host Service defines a protocol or interface that gives access to your Bounded Context as a set of services. The protocol is “open” so that all who need to integrate with your Bounded Context can use it with relative ease. The services offered by the application programming interface (API) are well documented and a pleasure to use. Even if you were Team 2 in this diagram and could not take time to create an isolating Anticorruption Layer for your side of the integration, it would be much more tolerable to be a Conformist to this model than many legacy systems you may encounter. We might say that the language of the Open Host Service is much easier to consume than that of other types of systems.

开放式主机服务（Open Host Service）[1] 会定义一套协议或接口，让限界上下文可以被当作一组服务访问。该协议是「开放的」，所有需要与限界上下文进行集成的客户端都可以相对轻松地使用它。通过应用程序編程接口（API）提供的服务都有详细的文档，用起来也很舒服。即使是处在类似图中团队 2 的位置，也没有时间在这端的集成中创建隔离用的防腐层，和许多可能遇到的遗留系统相比，作为团队 1 模型的跟随者更容易被接受。可以说开放主机服务的语言比其他类型的系统语言更易用。

1 REST 服务就是一种最常见的开放主机服务实例。实现开放主机服务相对来说是一种成本较高的集成方式。它的 API 要提供给许多下游上下文使用，这就要求接口实现要做到足够的兼容性、可伸缩性、健壮性。同时，开放主机服务还要提供易用的文档，因此通常会和已发布语言一起使用，采用主流协议来定义 API，这是一种特别适合快速扩张形成生态的方式，我们看到 API 已经变成了主流互联网公司的标配，帮助它们牢牢地把持着自己的生态圈和开发者社区。我们也观察到一些传统的大型企业也在利用 API 和服务化治理整合内部资源，请参考《数字化企业的 API 架构治理》。一一译注

#### 4.1.5 Published Language

A Published Language , illustrated in the image at the bottom of page 57 , is a well-documented information exchange language enabling simple consumption and translation by any number of consuming Bounded Contexts. Consumers who both read and write can translate from and into the shared language with confidence that their integrations are correct. Such a Published Language can be defined with XML Schema, JSON Schema, or a more optimal wire format, such as Protobuf or Avro. Often an Open Host Service serves and consumes a Published Language , which provides the best integration experience for third parties. This combination makes the translations between two Ubiquitous Languages very convenient.

上图中展示的已发布语言（Published Language）是一种有着丰富文档的信息交换语言，可以被许多消费方的限界上下文简单地使用和翻译。需要读写信息的消费者们可以把共享语言翻译成自己的语言，反之亦然，而在此过程中它们对集成的正确性充满信心。这种已发布语言可以用 XML Schema、JSON Schema 或更佳的序列化格式定义，比如 Protobuf 或 Avro。通常，同时提供和使用己发布语言的开放主机服务可以为第三方提供最佳的集成体验。这种结合使得两种通用语言之间的转译非常方便。

1 Protocol Buffers，简称 Protobuf，是 Google 开源的数据交换标准，用于定义数据传输和持久化的报文格式。Avro 是 Apache Hadoop 的一个子项目，是一种远程过程调用和数据序列化框架。除了书中提到的这两种新的序列化协议，另一种新的「查询语言」GraphQL 也在逐渐流行起来。它由 Facebook 开源具备类型安全、内省、文档生成和可预测响应等优势，非常适合对数据有不同要求的各种客户端。有兴趣的读者可以参考其中文网站。——译注

#### 4.1.5 Separate Ways

Separate Ways describes a situation where integration with one or more Bounded Contexts will not produce significant payoff through the consumption of various Ubiquitous Languages. Perhaps the functionality that you seek is not fully provided by any one Ubiquitous Language. In this case produce your own specialized solution in your Bounded Context and forget integrating for this special case.

各行其道（Separate Way）[1] 描述了一种情况，使用各种通用语言来与一个或多个限界上下文集成这样的方式不能产生显著的回报。也许你所寻求的功能并不能由任何一种通用语言提供。在这种情况下，只能在限界上下文中创造属于自己的特殊解决方案，并放弃针对这种特殊情况的集成。

1 各行其道意味着两个上下文之间根本没有关系，不需要控制，也不需要承诺。在一个复杂的模型中定存在着许多上下文，而大部分上下文之间应该是没有直接依赖关系的。例如，第 3 章中的一个关于子域的例子里，账户子域（上下文）和物流子域（上下文）之间就没有直接联系。如果任何两个上下文之间都有直接联系，整个模型就要走向另一个极端：大泥球。两个上下文之间没有任何依赖，自由地独立演进，这应该是我们最希望的。因此，在可能的情况下，我们应该把两个上下文分开，让它们各行其道。——译注

#### 4.1.5 Big Ball of Mud

You already learned plenty about Big Ball of Mud in the previous chapters, but I am going to reinforce the serious problems you will experience when you must work in or integrate with one. Creating your own Big Ball of Mud should be avoided like the plague.

在第 3 章中，已经学到了很多关于大泥球（Big Ball of Mud）的知识，但这里要强调在处理大泥球或者要和它进行集成时可能面临的严重问题。制造大泥球这种事应该人人避之唯恐不及。

Just in case that’s not enough warning, here’s what happens over time when you are responsible for creating a Big Ball of Mud: 1) A growing number of Aggregates cross-contaminate because of unwarranted connections and dependencies. 2) Maintaining one part of the Big Ball of Mud causes ripples across the model, which leads to “whack-a-mole” issues. 3) Only tribal knowledge and heroics—speaking all languages at once—save the system from complete collapse.

假如这还不够让你警醒，下面描述的是如何一步一步把系统推向大泥球深渊：1）越来越多的聚合因为不合理的关联和依赖而交叉污染。2）对大泥球的一部分进行维护就会牵一发而动全身，解决问题就像在「打地鼠」。3）只剩下「部落知识」和「个人英雄主义」，唯有同时「讲」出所有语言的极个别「超人」方能扶大厦之将倾 [1]。

The problem is that there are already many Big Balls of Mud out there in the wide world of software systems, and the number will no doubt grow every month. Even if you are able to avoid creating a Big Ball of Mud by employing DDD techniques, you may still need to integrate with one or more. If you must integrate with one or more, try to create an Anticorruption Layer against each legacy system in order to protect your own model from the cruft that would otherwise pollute your model with the incomprehensible morass. Whatever you do, don’t speak that language!

问题是，大泥球已经遍布于世界上的软件系统中，这个数量还铁定会逐月增长。即使可以通过采用 DDD 技术避免创建自己的大泥球，仍可能不得不与它们集成。如果必须与个或多个这样的大泥球系统集成，请尝试针对每个这样的遗留系统创建一个防腐层，保护自己的模型免受污染，否则会陷入难以理解的泥潭。不管怎样，别「讲」这种语言！

1 Tribal Knowledge，是指一种仅存在于某个部落中的信息或知识，这些知识不为外界所知，没有正式记录，只能口口相传。当系统发展到这个大泥球程度，可以想象，参与到其中的每个团队甚至每个人都有着自己对模型的理解和定义，就像一个个坐井观天的小「部落」一样讲着只有自己能懂的语言。只有极个别充满「个人英雄主义」的架构师能够理解不同小团队或个人的不同语言，苦苦地支撑着脆弱的系统。如果这少数几个架构师失去了坚持下去的勇气或者离开了团队（这很可能会发生），整个系统将完全无法维护，很快会落得重写的结局。最差的情况是，团队连重写的勇气都没有，只能默默地祈祷系统可以荀延残喘。——译注

### 4.2 Making Good Use of Context Mapping

1『中文版书里的这张图可以好好看下。画了 3 个常用的协议：远程过程调用（RPC）、RESTful 以及消息机制。』

You may be wondering what specific kind of interface would be supplied to allow you to integrate with a given Bounded Context. That depends on what the team that owns the Bounded Context provides. It could be RPC via SOAP, or RESTful interfaces with resources, or it could be a messaging interface using queues or Publish-Subscribe. In the least favorable of situations you may be forced to use database or file system integration, but let’s hope that doesn’t happen. Database integration really should be avoided, and if you are forced to integrate that way, you really should be sure to isolate your consuming model by means of an Anticorruption Layer.

Let’s take a look at three of the more trustworthy integration types. We will move from the least robust to the most robust integration approaches. First we will look at RPC, followed by RESTful HTTP, and then messaging.

你可能想知道提供什么样的特定接口才能和指定的限界上下文进行集成。这取决于负责这个限界上下文的团队提供的是什么。它可以是基于 SOAP 的 RPC，也可以是基于资源的 RESTFUL 接口，抑或是使用队列或发布订阅的消息机制。最不济你会被迫使用数据库或文件系统进行集成，让我们祈祷这种情况不会发生。基于数据库的集成方式是一定要避免的 [1]，如果不得不以这种方式进行集成，请务必通过防腐层来隔离要去集成和适配的模型。我们来看看三种更可靠的集成类型。我们将按照健壮性逐步加强的方式介绍这三种集成方式。首先我们介绍的是 RPC，接下来是 RESTful HTTP，最后是消息机制。

1 共享数据库的集成方式看起来简单直接，实现起来很快。因此，它曾经是一种颇受欢迎的集成选择。然而，随着它暴露的问题越来越多，现在已经变成了一种反模式。首先，它是单点故障和性能瓶颈的源头此外，它违背了「高内聚、低耦合」的设计原则。多个消费方上下文和一种具体的数据库技术实现（如关系型数据库）紧密地耦合在了一起，对数据库的任何调整将会导致霰弹式修改。而消费方上下文也受到数据库内部细节和技术选型的干扰。选择这种方式的结果就是所有消费方上下文最后都会骑虎难下不敢做出任何修改。——译注

#### 4.2.1 RPC with SOAP

Remote Procedure Calls, or RPC, can work in a number of ways. One popular way to use RPC is via the Simple Object Access Protocol, or SOAP. The idea behind RPC with SOAP is to make using services from another system look like a simple, local procedure or method invocation. Still, the SOAP request must travel over the network, reach the remote system, perform successfully, and return results over the network. This carries the potential for complete network failure, or at least latency that is unanticipated when first implementing the integration. Additionally, RPC over SOAP also implies strong coupling between a client Bounded Context and the Bounded Context providing the service.

远程过程调用（Remote Procedure Call, RPC）能以多种方式工作。一种流行的方式是通过简单对象访问协议（Simple Object Access Protocol, SOAP）使用 RPC [1]。基于 SOAP 的 RPC 背后的思路是让调用另一个系统的服务如同调用一个本地过程或方法那样简单。然而，SOAP 请求必须通过网络传播才能抵达远程系统，成功执行并再次通过网络返回结果。在开始实施这种集成方式时就要承受网络彻底瘫痪的风险，或者至少要承受意外的网络延迟。另外，基于 SOAP 的 RPC 还意味着客户端限界上下文和提供服务的服界上下文之间存在着紧耦合。

1 SOAP 这种 RPC 方法有些历史了，现在提起 RPC 我们更可能想到的是 gRPC 和 Thrift。相较于 SOAP 这些现代的 RPC 机制能更友好地支持更多的编程语言，对使用者的侵入性更低。它们采用了比 XML 效率更高的数据序列化格式和现代的传输协议（如 HTTP/2），能够有效地降低延迟。因此，如果选择 RPC 作为集成方式，应该考虑采用这些现代的 RPC 机制。一一译注

The main problem with RPC, using SOAP or another approach, is that it can lack robustness. If there is a problem with the network or a problem with the system hosting the SOAP API, your seemingly simple procedure call will fail entirely, giving only error results. Don’t be fooled by the seeming ease of use.

RPC 的主要问题是，无论是使用 SOAP 或是其他方法，它都缺乏健壮性。如果网络出现问题或者托管 SOAP API 的系统出现问题，那么看似简单的过程调用将完全失败，只会留下错误的结果。不要被看似易用的表面所迷惑。

When RPC works—and it mostly works—it can be a very useful way to integrate. If you can influence the design of the service Bounded Context , it would be in your best interests if there is a well-designed API that provides an Open Host Service with a Published Language. Either way, your client Bounded Context can be designed with an Anticorruption Layer to isolate your model from unwanted outside influences.

当 RPC 有效时一一大部分时间它都是有效的——它是一种非常实用的集成方式。当我们可以影响服务端限界上下文的设计时，如果它有一个设计良好的 API 使用已发布语言来提供开放主机服务，那就最好不过了。不管怎样，客户端限界上下文都可以设计一层防腐层，将模型与多余的外部影响隔离开来。

#### 4.2.2 RESTful HTTP

Integration using RESTful HTTP focuses attention on the resources that are exchanged between Bounded Contexts , as well as the four primary operations: POST, GET, PUT, and DELETE. Many find that the REST approach to integration works well because it helps them define good APIs for distributed computing. It’s difficult to argue against this claim given the success of the Internet and Web.

使用 RESTful HTTP 的集成将注意力集中在限界上下文之间交换的资源上，还有相关的四个主要操作：POST、GET、PUT 和 DELETE。许多人发现采用 REST 方式进行集成效果很好，因为它可以帮助他们定义出非常适合分布式计算的 API。互联网的成功让这一点不可辩驳。

There is a very certain way of thinking when you use RESTful HTTP. I won’t get into the details in this book, but you should look into it before trying to employ REST. The book REST in Practice [RiP] is a good place to start.

A service Bounded Context that sports a REST interface should provide an Open Host Service and a Published Language. Resources deserve to be defined as a Published Language , and combined with your REST URIs they will form a natural Open Host Service.

使用 RESTful HTTP 是一种非常固定的思维方式。在本书里不会详细展开，但应该在尝试之前仔细研究 REST。《REST 实战》[RiP] 这本书是一个不错的开始。支持 REST 接口的服务端限界上下文应该提供开放主机服务和已发布语言。资源理应被定义成已发布语言，而且当它们与你的 REST URI 结合在一起之后，将形成天然的开放主机服务。

2『已下载书籍「2020157REST实战 | 2020157REST-in-Practice」。』

RESTful HTTP will tend to fail for many of the same reasons that RPC does—network and service provider failures, or unanticipated latency. However, RESTful HTTP is based on the premise of the Internet, and who can find fault with the track record of the Web when it comes to reliability, scalability, and overall success?

造成 RESTful HTTP 失败的原因通常和许多造成 RPC 失败的原因一样一一网络或服务提供商故障，还有意外延迟。在没有网络的前提下，RESTful HTTP 无法运作，但谁又能通过跟踪这期间的日志记录来发现导致失败的原因，从而达成保证其成功的可靠性、可伸缩性以及完整性的目标呢？

A common mistake made when using REST is to design resources that directly reflect the Aggregates in the domain model. Doing this forces every client into a Conformist relationship, where if the model changes shape the resources will also. So you don’t want to do that. Instead, resources should be designed synthetically to follow client-driven use cases. By “synthetic” I mean that to the client the resources provided must have the shape and composition of what they need, not what the actual domain model looks like. Sometimes the model will look just like what the client needs. But what the client needs is what drives the design of the resources, and not the model’s current composition.

使用 REST 常犯的设计错误是直接把模型中的聚合暴露成资源。服务端模型一旦发生变化，资源也会随之一起改变，这样会把跟随者关系强加给每个客户端。所以你不会想这样做。相反，应该根据客户端驱动的用例设计出「合成」的资源。「合成」，是指对客户端来说，服务端提供出来的资源必须具有它们所需要的样子和组成，而不是直接给出实际的领域模型。有时候模型看起来就像客户端需要的东西。但客户端真正所需要的是驱动资源模型的设计，而不只是保持模型的皮囊。

#### 4.2.3 Messaging

When using asynchronous messaging to integrate, much can be accomplished by a client Bounded Context subscribing to the Domain Events published by your own or another Bounded Context. Using messaging is one of the most robust forms of integration because you remove much of the temporal coupling associated with blocking forms such as RPC and REST. Since you already anticipate the latency of message exchange, you tend to build more robust systems because you never expect immediate results.

在使用异步消息机制进行集成时，很多工作都是通过客户端限界上下文订阅由它自己或另一个限界上下文发布的领域事件（Domain Events）来完成的。使用消息机制是最健壮的集成方法之一，因为可以消除那些和阻塞（同步）形式（如 RPC 和 REST）有关的暂时性耦合。如果可以提前预见到消息交换会产生延迟，就可以构建出更健壮的系统，因为你从未期望结果会即时发生。

『

Going Asynchronous with REST

It’s possible to accomplish asynchronous messaging using REST-based polling of a sequentially growing set of resources. Using background processing, a client would continuously poll for a service Atom feed resource that provides an ever-increasing set of Domain Events. This is a safe approach to maintaining asynchronous operations between a service and clients, while supplying up-to-date events that continue to occur in the service. If the service becomes unavailable for some reason, clients will simply retry on normal intervals, or back off with retry, until the feed resource is available again.

This approach is discussed in detail in Implementing Domain-Driven Design [IDDD].

可以基于 REST 对有序增长的资源集合进行轮询达到异步消息机制的效果。客户端可以在后台进程中持续轮询一个 Atom Feed [1] 资源服务，该资源提供了一个持续增长的领域事件集合。这是一种维持服务和客户端之间异步操作的安全方法，同时还能提供服务中持发生的最新事件。如果服务因某些原因而无法使用，则客户端将简单地在固定时间间隔之后重试，或以退避算法进行重试 [2]，直到资源再次可用。在《实现领域駆动设计》中译细讨论了这种方法。

1 Atom 是工程任务组（ITEF）发布的标准规范，用于表示提要（Feed）格式和用于編辑 Web 资源的协议如 Weblog、在线日志、Wiki 以及类似内容。——译注

2 Backof，是一种重试机制，发送者会在再次重试之前等待一个随机时间，这样可以避免多个发送者按相同时间间隔重试产生的冲突。这个等待时间的随机范一般会采用一种策略和算法来计算，常见的种实现是指数退避算法。——译注

Avoid Integration Train Wrecks

When a client Bounded Context (C1) integrates with a service Bounded Context (S1), C1 should usually not be making a synchronous, blocking request to S1 as a direct result of handling a request made to it. That is, while some other client (C0) makes a blocking request to C1, don’t allow C1 to make a blocking request to S1. Doing so has a very high potential for causing an integration train wreck between C0, C1, and S1. This can be avoided by using asynchronous messaging.

如果客户端限界上下文（C1) 和服务端限界上下文（S1) 集成，C1 在处理其他客户端发给它的请求时，通常不应该将发给 S1 的同步阻塞请求作为这种处理的直接结果。也就是说，当其他某个客户端（C0) 向 C1 发起阻塞请求时，不允许 C1 向 S1 发起另一个阻塞请求。因为这样的做法很可能导致 C0、C1 和 S1 之间发生「集成火车事故」。你可以使用异步消息机制来避免这种事故 [2]。


2 当 C1 向 S1 发起同步阻塞请求并等待其返回作为处理结果来响应 C0 的请求时，它们三者之间就形成了暂时性耦合。C0 的请求是否能成功，返回的是快是慢，取决于 S1 和 C1 以及它们之间的连接（通常是网络连接）。一旦 S1 发生问题，C1 和 C0 就会像相邻的火车车厢一样受到牵连。更糟的是，C0 和 C1 还可能因为阻塞影响可用性。而使用异步消息机制之后，C0 和 C1 首先从设计上就要考虑消息延迟和网络故障导致的失败，自身的健壮性更强。当它们触发命令（发布一条消息）之后，三者之间再无瓜葛，S1 的失敗影响范围就能降到最小。这样就能避免集成火车事故。一一译注

』

Typically an Aggregate in one Bounded Context publishes a Domain Event , which could be consumed by any number of interested parties. When a subscribing Bounded Context receives the Domain Event , some action will be taken based on its type and value. Normally it will cause a new Aggregate to be created or an existing Aggregate to be modified in the consuming Bounded Context.

通常情况下，领域事件由限界上下文中的聚合（aggregate）发布，许多对它感兴趣的订阅方限界上下文都可以消费。当订阅方限界上下文收到领域事件时，将依据其类型和值进行一些操作。一般它会导致在消费方限界上下文中新聚合的创建或者现有聚合的修改。

『

Are Domain Event Consumers Conformists?

You may be wondering how Domain Events can be consumed by another Bounded Context and not force that consuming Bounded Context into a Conformist relationship. As recommended in Implementing Domain-Driven Design [IDDD] , and specifically in Chapter 13, “Integrating Bounded Contexts,” consumers should not use the event types (e.g., classes) of an event publisher. Rather, they should depend only on the schema of the events, that is, their Published Language. This generally means that if the events are published as JSON, or perhaps a more economical object format, the consumer should consume the events by parsing them to obtain their data attributes.

你可能想知道领域事件如何被另一个服界上下文消费，而不会强迫这个消费方限界上下文变成跟随者。正如《实现领域驱动设计》中（特别是在第 13 章中）所建议的那样，消费者不应该使用事件发布者定义的事件类型（比如，类）。相反，他们只应该依赖事件的格式，即它们的已发布语言。这通常意味着，如果事件以 JSON 格式或者更高效的对象格式发布，那么消者应通过解析它们获取其数据属性来消该事件。

』

Of course, the foregoing assumes that a subscribing Bounded Context can always benefit from unsolicited happenings in the publishing Bounded Context. Sometimes, however, a client Bounded Context will need to proactively send a Command Message to a service Bounded Context to force some action. In such cases the client Bounded Context will still receive any outcome as a published Domain Event.

当然，上述内容假定订阅方限界上下文总是可以从被动接受的发布方限界上下文事件上获益。然而，有时候客户端限界上下文需要主动发送命令消息给服务端限界上下文来强制执行一些操作。这种情况下，客户端限界上下文依然会收到作为结果被发布出来的领域事件。

In all cases of using messaging for integration, the quality of the overall solution will depend heavily on the quality of the chosen messaging mechanism. The messaging mechanism should support At-Least-Once Delivery [Reactive] to ensure that all messages will be received eventually. This also means that the subscribing Bounded Context must be implemented as an Idempotent Receiver [Reactive] .

在使用消息进行集成的所有用例中，整体解决方案的质量很大程度上将取决于所选消息机制的质量。消息机制应支持至少ー次投递 [Reactive] 来保证所有消息最终都会被收到这也意味着订阅方限界上下文必须实现成幂等接收者（Idempotent Receiver) [Reactive]。

At-Least-Once Delivery [Reactive] is a messaging pattern where the messaging mechanism will periodically redeliver a given message. This will be done in cases of message loss, slow-reacting or downed receivers, and receivers failing to acknowledge receipt. Because of this messaging mechanism design, it is possible for the message to be delivered more than once even though the sender sends it only once. Still, that needn’t be a problem when the receiver is designed to deal with this.

至少ー次投递 [Reactive] 是一种消息机制的模式，这种模式下消息机制将周期性地重发指定消息。在消息丢失、接收者响应不及时，或者宕机以及接收者应答回执发送失败的情况下会发生重发。由于消息机制的这种设计，即使发送者只发送了一次，消息也可能被多次投递。但是，如果接收者的设计可以处理这种情况，那就不是问题。

Whenever a message could be delivered more than once, the receiver should be designed to deal correctly with this situation. Idempotent Receiver [Reactive] describes how the receiver of a request performs an operation in such a way that it produces the same result even if it is performed multiple times. Thus, if the same message is received multiple times, the receiver will deal with it in a safe manner. This can mean that the receiver uses de-duplication and ignores the repeated message, or safely reapplies the operation with the exact same results that the previous delivery caused.

Due to the fact that messaging mechanisms always introduce asynchronous Request-Response [Reactive] communications, some amount of latency is both common and expected. Requests for service should (almost) never block until the service is fulfilled. Thus, designing with messaging in mind means that you will always plan for at least some latency, which will make your overall solution much more robust from the outset.

只要消息可以多次投递，接收方的设计就应该正确处理这种情况。幂等接收者（Reactive）描述了请求的接收者执行操作的一种方式，即使多次执行这些操作也能产生相同的结果。因此，即使多次收到相同的消息，接收者也可以妥善处理。这可能意味着接收方要么使用消息去重功能来忽略重复的消息，要么妥善地重新应用该操作，使其结果与之前处理收到的消息所产生的结果完全一致。

因为消息机制总是采用异步的请求响应 [Reactive] 通信方式，所以有一些延迟是正常的，也是可以预见的。服务请求应该（几乎）不会阻塞，直到服务完成。因此，设计时把消息机制放在心上意味着你至少需要时刻准备着处理一些延退，这将使你的整体解决方案从一开始就更加健壮。

### 4.3 An Example in Context Mapping

Returning to an example discussed in Chapter 2 , “Strategic Design with Bounded Contexts and the Ubiquitous Language ,” a question arises about the location of the official Policy type. Remember that there are three different Policy types in three different Bounded Contexts. So, where does the “policy of record” live in the insurance enterprise? It’s possible that it belongs to the underwriting division since that is where it originates. For the sake of this example, let’s say it does belong to the underwriting division. So how do the other Bounded Contexts learn about its existence?

到第 2 章中讨论过的例子，有关正式 Policy 类型的位置问题凸显了出来。请记住出现在三个不同的限界上下文中的三种 Policy 类型是有区别的。那么，保单记录（Record of Policy）在保险企业中的位置应该在哪儿呢？它可能属于承保分部，因为那是它的来源。作为示例，我们假设它属于承保分部。那么其他限界上下文如何感知它的存在呢？

When a component of type Policy is issued in the Underwriting Context , it could publish a Domain Event named PolicyIssued . Provided through a messaging subscription, any other Bounded Context may react to that Domain Event , which could include creating a corresponding Policy component in the subscribing Bounded Context.

当承保上下文中「出立」（issue）了ー个 Policy 类型的组件时，可以同时发布一个名为 PolicyIssued 的领域事件。这个领域事件通过消息订阅提供出去，任何其他服界上下文都可能会对它做出响应，包括在订阅方限界上下文中创建对应的 Policy 组件。

The PolicyIssued Domain Event would contain the identity of the official Policy. Here it’s policyId . Any components created in a subscribing Bounded Context would retain that identity for traceability back to the originating Underwriting Context. In this example the identity is saved as issuedPolicyId . If there is a need for more Policy data than the PolicyIssued Domain Event provided, the subscribing Bounded Context can always query back on the Underwriting Context for more information. Here the subscribing Bounded Context uses the issuedPolicyId to perform a query on the Underwriting Context.

PolicyIssued 领域事件会包含正式 Policy 的唯一标识符。这里就是 policyId，订阅方限界上下文中创建的任何组件都将保留该标识符，用来回溯到原始的承保上下文在这个例子中，标识符被保存为 issuedPolicyId。如果 PolicyIssued 领域事件还要提供更多的 Policy 数据，订阅方限界上下文可以始终反向查询承保上下文来获得更多信息。这里订阅方限界上下文使用 issuedPolicyId 在承保上下文中进行查询。

『

Enrichment versus Query-Back Trade-offs

Sometimes there is an advantage to enriching Domain Events with enough data to satisfy the needs of all consumers. Sometimes there is an advantage to keeping Domain Events thin and allowing for querying back when consumers need more data. The first choice, enrichment, allows for greater autonomy of dependent consumers. If autonomy is your driving requirement, consider enrichment.

On the other hand, it is difficult to predict every piece of data that all consumers will ever need in Domain Events , and there may be too much enrichment if you provide it all. For example, it may be a poor security choice to greatly enrich Domain Events. If that is the case, designing thin Domain Events and a rich query model with security for consumers to request from may be the choice you need.

Sometimes circumstances will call for a balanced blend of both approaches.

在增强事件与反向查询之间的权衡。有时，填充足够多的数据增强领域事件来满足所有消费者的需求是有好处的。而有些时候，保持轻量的领域事件并让消费者在需要更多数据时进行查询会更有利。第一种选择，即增强事件，将给予从属消费者更多自治权。如果自治是你的驱动要素，请选择增强事件数据的方式。另一方面，很难预料到所有消费者需要在领域事件中获取的每一条数据，而且如果全部提供，可能会丰富过了头。例如，在领域事件中填充数据可能是一个糟糕的安全性决策。如果是这种情况，设计轻量的领域事件和一个可以让消费者请求的安全且丰富的查询模型可能才是正确的选择。而有些时候，需要视情况平衡地混合使用两种方法。

1 请参考《实现领域驱动设计》D 附录 A 中的「增强事件」小节。一一译注

』

And how might the query back on the Underwriting Context work? You could design a RESTful Open Host Service and Published Language on the Underwriting Context. A simple HTTP GET with the issuedPolicyId would retrieve the IssuedPolicyData .

那么又该如何向承保上下文进行查询呢？你可以在承保上下文中设计 RESTful 开放主机服务和已发布语言。一次带 issuedPolicyId 的简单 HTTP GET 请求就能取回 IssuedpolicyData.

You’re probably wondering about the data details of the Policy-Issued Domain Event. I will provide Domain Event design details in Chapter 6 , “Tactical Design with Domain Events .”

Are you curious about what happened to the Agile Project Management Context example? Straying from that to the insurance business domain allowed you to examine DDD with multiple examples. That should have helped you grasp DDD even better. Don’t worry, we will return to the Agile Project Management Context in the next chapter.

你是不是对敏捷项目管理上下文的例子感到好奇？这里我们切换到保险业务领域，可以让你利用多个例子来研究 DDD，从而帮助你更好地掌握 DDD。别着急，我们将在下一章回到敏捷项目管理上下文上来。
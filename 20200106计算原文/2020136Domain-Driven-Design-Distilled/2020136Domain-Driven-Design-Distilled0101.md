# 0101. DDD for Me

You want to improve your craft and to increase your success on projects. You are eager to help your business compete at new heights using the software you create. You want to implement software that not only correctly models your business’s needs but also performs at scale using the most advanced software architectures. Learning Domain-Driven Design (DDD), and learning it quickly, can help you achieve all of this and more.

DDD is a set of tools that assist you in designing and implementing software that delivers high value, both strategically and tactically. Your organization can’t be the best at everything, so it had better choose carefully at what it must excel. The DDD strategic development tools help you and your team make the competitively best software design choices and integration decisions for your business. Your organization will benefit most from software models that explicitly reflect its core competencies. The DDD tactical development tools can help you and your team design useful software that accurately models the business’s unique operations. Your organization should benefit from the broad options to deploy its solutions in a variety of infrastructures, whether in house or in the cloud. With DDD, you and your team can be the ones to bring about the most effective software designs and implementations needed to succeed in today’s competitive business landscape.

DDD 同时提供了战略和战术上的建模工具，来帮助你设计和实现高价值的软件。你的组织无法在所有方面都出类拔萃，所以最好谨慎地识别其真正的优势所在。DDD 的战略设计工具可以帮助你和你的团队做出最有竟争力的软件设计选择和业务整合决策。你的组织将从这些明确反映其核心业务竟争力的软件模型中获得最大的收益。DDD 的战术实施工具可以帮助你和你的团队设计出实用的软件，它能对业务独一无二的运作方式进行精准地建模。你的组织可以有更多的选择，把解决方案部署到各种不同的基础设施中，不管这些基础设施是位于企业内部还是在公有云上，你的组织都会受益匪浅。借助 DDD，你的团队可以在当今竞争激烈的商业环境中持续地交付最有效的软件设计与实现。

In this book I have distilled DDD for you, with condensed treatment of both the strategic and tactical modeling tools. I understand the unique demands of software development and the challenges you face as you work to improve your craft in a fast-paced industry. You can’t always take months to read up on a subject like DDD, and yet you still want to put DDD to work as soon as possible.

I am the author of the best-selling book Implementing Domain-Driven Design [IDDD] , and I have also created and teach the three-day IDDD Workshop. And now I have also written this book to bring you DDD in an aggressively condensed form. It’s all part of my commitment to bringing DDD to every software development team, where it deserves to be. My goal, of course, includes bringing DDD to you.

## 1.1 Will DDD Hurt?

You may have heard that DDD is a complicated approach to software development. Complicated? It certainly is not complicated of necessity. Indeed, it is a set of advanced techniques to be used on complex software projects. Due to its power and how much you have to learn, without expert instruction it can be daunting to put DDD into practice on your own. You have probably also found that some of the other DDD books are many hundreds of pages long and far from easy to consume and apply. It required a lot of words for me to explain DDD in great detail in order to provide an exhaustive implementation reference on more than a dozen DDD topics and tools. That effort resulted in Implementing Domain-Driven Design [IDDD] . This new condensed book is provided to familiarize you with the most important parts of DDD as quickly and simply as possible. Why? Because some are overwhelmed by the larger texts and need a distilled guide to help them take the initial steps to adoption. I have found that those who use DDD revisit the literature about it several times. In fact, you might even conclude that you will never learn enough, and so you will use this book as a quick reference, and refer to others for more detail, a number of times as your craft is refined. Others have had trouble selling DDD to their colleagues and the all-important management team. This book will help you do that, not only by explaining DDD in a condensed format, but also by showing that tools are available to accelerate and manage its use.

Of course, it is not possible to teach you everything about DDD in this book, because I have purposely distilled the DDD techniques for you. For much more in-depth coverage, see my book Implementing Domain-Driven Design [IDDD] , and look into taking my three-day IDDD Workshop. The three-day intensive course, which I have delivered around the globe to a broad audience of hundreds of developers, helps get you up to speed with DDD rapidly. I also provide DDD training online at http://ForComprehension.com.

The good news is, DDD doesn’t have to hurt. Since you probably already deal with complexity on your projects, you can learn to use DDD to reduce the pain of winning over complexity.

## 1.2 Good, Bad, and Effective Design

Often people talk about good design and bad design. What kind of design do you do? Many software development teams don’t give design even a passing thought. Instead, they perform what I call “the task-board shuffle.” This is where the team has a list of development tasks, such as with a Scrum product backlog, and they move a sticky note from the “To Do” column of their board to the “In Progress” column. Coming up with the backlog item and performing “the task-board shuffle” constitutes the entirety of thoughtful insights, and the rest is left to coding heroics as programmers blast out the source. It rarely turns out as well as it could, and the cost to the business is usually the highest price paid for such nonexistent designs.

This often happens due to the pressure to deliver software releases on a relentless schedule, where management uses Scrum to primarily control timelines rather than allow for one of Scrum’s most important tenets: knowledge acquisition.

他们采用一种我称之为「任务板挪卡」的方法来代替设计。团队有个开发任务清单，比如 Scrum 产品待办列表，其中的任务被张贴在「任务板」上，然后他们可以将一张便利贴从「任务板」上的「待办」泳道移动到「进行中」泳道，这就是「任务板挪卡」。产品经理提出待办项（任务），然后来一次「任务板挪卡」，这便构成了关于设计的全部「真知灼见」，剩下的就交给程序员大神们去疯狂输出代码。很少有团队会这样做，如果真的这样做了，业务就会为这些不存在的设计付出最高昂的代价。这种情况常常是因为团队必须按照苛刻得近乎残忍的时间表去发布软件，管理层只会使用 Scrum 控制交付节奏，却对它最重要的信条之一：知识获取（Knowledge Acquisition），视而不见。

任务板挪卡是一种交接棒的协作模式。产品负责人在待办项列表中创建新的待办项，并更新列表中待办项的优先级。开发团队会依据优先级选取待办项，按照产品负责人的文档等需求描述完成相应的研发活动。上述过程中，业务人员与开发人员之间通过交互协作产生设计，这个动作很容易被忽略。优秀设计和有效设计并非由产品负责人或某个团队成员独立完成，而是通过他们之间不断的协作与交互，并在充分的知识获取后形成的。熟悉 Scrum 的读者会发现，Scrum 中的需求梳理与迭代计划会议一定程度上发挥了此类作用。但要注意，协作设计并非只局限在固定的会议中，也提倡在必要时随时随地进行。请参考《Scrum 精髓》【Essential Scrum】获取更多的内容。——译注

Scrum 是一种用于开发创新产品和服务的敏捷方法，请参考《Scrum 精髓》【Essential Scrum] ——译注 

Scrum 的开发方法更加强调将软件开发作为一种不断认知学习的过程，鼓励团队成员与业务人员之间持续地通过协作来迭代交付可工作的软件，并以此快速地获取用户反馈。当然知识获取并非「免费」，所以我们期望开发团队与业务人员之间通过一系列的设计研讨，并引入高效的协作工具（如 DDD 工具箱）帮助团队更加紧密和有效地进行知识传递与分享。关于 Scrum 中的需求梳理和迭代计划的更多介绍请参考《Scrum 精髓》【Essential Scrum】——译注

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

2『上面的十大问题，总结一下做一张任意卡片。』

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

这一切都似乎发生在「设计无法带来低成本的软件」的观念下。而这时常是出于商业上的简单考虑，软件开发人员并不知道还有其他更好的选择。软件正在蚕食整个世界 WSJ，对你而言重要的是，软件不但可以蚕食你的利润，也可以提供一场利润盛宴。你一定要明白，臆想出来的「不做设计能省钱」的观念简直是一个谬论，它已经巧妙地愚弄了那些不思考周详设计而只会对软件交付施压的人们。这是因为设计仍然会从每个开发人员的脑海流淌到在键盘上不断敲打着代码的指尖之中，这些设计并不需要来自其他地方的输入，包括业务。以下这句话可以很好地总结这种现象：关于设计是否必要或是否负担得起的问题根本都没有问到点上：设计是不可或缺的。除了优秀设计就是糟糕设计，根本不存在「不做设计」一说。

不做设计并不能节约成本，而过度设计也会造成浪费，所以我们提倡适度的设计。Martin Fowler 认为敏捷开发不是轻视设计只注重实践和重构，而是鼓励演进式的设计（Evolutionary Design）。优秀设计与有效设计是在持续的重构和迭代过程中产生的，每一次的设计优化都是从最大限度地满足客户的功能性需求和非功能性需求角度出发，以拥抱变化的心态来应对变幻莫测的需求。——译注

Although Mr. Martin’s comments are not specifically about software design, they are still applicable to our craft, where there is no substitute for thoughtful design. In the situation just described, if you have five software developers working on the project, No Design will actually produce an amalgamation of five different designs in one. That is, you get a blend of five different made-up business language interpretations that are developed without the benefit of the real Domain Experts.

尽管 Martin 先生的评论并非专门针对软件设计，但这同样适用于我们的技艺，考虑周详的设计同样无可取代。在刚才的情景中，如果一个项目由五名开发人员参与，那么「不做设计」将会产生五种不同的设计。也就是说，在没有任何真正领域专家的协助下，你开发出来的软件将会混杂着五种不同的、虚构出来的、对业务语言的诠释。

The bottom line: we model whether we acknowledge modeling or not. This can be likened to how roads are developed. Some ancient roads started out as cart paths that were eventually molded into well-worn trails. They took unexplained turns and made forks that served only a few who had rudimentary needs. At some point these pathways were smoothed and then paved for the comfort of the increasing number of travelers who used them. These makeshift thoroughfares aren’t traveled today because they were well designed, but because they exist. Few of our contemporaries can understand why traveling one of these is so uncomfortable and inconvenient. Modern roads are planned and designed according to careful studies of population, environment, and predictable flow. Both kinds of roads are modeled. One model employed minimal, base intellect. The other model exploited maximum cognition. Software can be modeled from either perspective.

事实上：无论承认与否，我们都是在构建模型。这就好比修建道路。一些历史悠久的道路最开始是跑马车的，经过岁月的碾压最终变得年久失修。为了满足少数人的需要，它们被加入了不明所以的转弯和岔路，并被改造得迁回曲折。在某个时刻，它们会被铲平并且会被重新建设，为的是让越来越多的旅客感到舒适。这些将就湊合的道路到现在还有人路过，不是因为它们设计良好，而仅仅是因为它们存在着而己。如今很少有人能够了解行走在这些道路上别扭不堪的原因。而现代道路都会依据人口、环境以及可预测的流量来规划和设计。两种类型的道路都会被建模。一种模型只是做了最基本、最简单的思考，另种则最大程度地发挥了聪明才智。软件建模也可以从这两种角度出发。

If you are afraid that producing software with thoughtful design is expensive, think of how much more expensive it’s going to be to live with or even fix a bad design. This is especially so when we are talking about software that needs to distinguish your organization from all others and yield considerable competitive advantages.

A word closely related to good is effective, and it possibly more accurately states what we should strive for in software design: effective design. Effective design meets the needs of the business organization to the extent that it can distinguish itself from its competition by means of software. Effective design forces the organization to understand what it must excel at and is used to guide the creation of the correct software model.

如果你担心周详的设计会带来高昂的软件开发成本，那么设想一下，将来为了维护甚至修缮一套糟糕设计的软件就需要付出更为昂贵的代价。当我们把软件作为你的公司与其他公司之间的差异，并依靠它带来可观的竞争优势时，尤其如此。

有效（Efective）一词和优秀（Good）意义相近，它能更准确地表达我们应该在软件设计中努力追求的目标：「有效设计」（Effective Design）。有效设计可以满足商业组织希望借助软件超越竟争者的诉求。它可以驱动企业去思考哪些核心业务必须成为其竞争力，还可以指引构建正确软件模型的方向。

In Scrum, knowledge acquisition is done through experimentation and collaborative learning and is referred to as “buying information” [Essential Scrum] . Knowledge is never free, but in this book I do provide ways for you to accelerate how you come by it.

Just in case you still doubt that effective design matters, don’t forget the insights of someone who seems to have understood its importance:

Most people make the mistake of thinking design is what it looks like. People think it’s this veneer—that the designers are handed this box and told, “Make it look good!” That’s not what we think design is. It’s not just what it looks like and feels like. Design is how it works.

——Steve Jobs

In software, effective design matters, most. Given the single alternative, I recommend effective design.

Scrum 中的知识获取是通过不断的试验及协作学习完成的，这被称为「知识付费」（Essential Scrum）。知识水远都不是免费的，但在本书中，我将提供一些方法帮你更快地获取它们。如果你对有效设计的影响仍心存疑虑，别忘了那位曾洞察其重要性的人：绝大部分人错误地认为设计只关乎外观。人们只理解了表象一一将这个金子递给设计师，告诉他们：「把它变得好看一些！」这不是我们对设计的理解。设计并不仅仅是感观，设计也是产品的工作方式。——Steve Jobs

「设计，是让生活变得完美的艺术。」这是乔布斯的产品设计理念。对他而言，有效设计首先意味着「简洁」的产品（开箱即用）、「简洁」的战略（产品的专注）和「简洁」的沟通（高效的沟通）。其次有效设计允许不完美。任何产品都始于不完美，只有通过不断试错与修正的送代才可能逐步趋于完美在软件设计中，我们也可以借鉴这些理念：有效设计是简洁而非冗余，它也需要不断地演进与优化才能趋于完美。——译注

![](./res/2020001.png)

## 1.3 Strategic Design

We begin with the all-important strategic design. You really cannot apply tactical design in an effective way unless you begin with strategic design. Strategic design is used like broad brushstrokes prior to getting into the details of implementation. It highlights what is strategically important to your business, how to divide up the work by importance, and how to best integrate as needed.

First you will learn how to segregate your domain models using the strategic design pattern called Bounded Contexts. Hand in glove, you will see how to develop a Ubiquitous Language as your domain model within an explicitly Bounded Context.

我们先从最为重要的战略设计谈起。不以战略设计开始，战术设计将无法被有效实施在展开具体实现细节之前，需要优先完成宏观层面的战略设计。它强调的是业务战略上的重点，如何按重要性分配工作，以及如何进行最佳整合。

首先，你需要学会运用名为限界上下文（Bounded Contex）的战略设计模式来分离领域模型。紧接着，你会了解如何使用在明确的限界上下文中发展一套领域模型的通用语言（Ubiquitous Language）。

You will learn about the importance of engaging with not only developers but also Domain Experts as you develop your model’s Ubiquitous Language. You will see how a team of both software developers and Domain Experts collaborate. This is a vital combination of smart and motivated people who are needed for DDD to produce the best results. The language you develop together through collaboration will become ubiquitous, pervasive, throughout the team’s spoken communication and software model.

As you advance further into strategic design, you will learn about Subdomains and how these can help you deal with the unbounded complexity of legacy systems, and how to improve your results on greenfield projects. You will also see how to integrate multiple Bounded Contexts using a technique called Context Mapping. Context Maps define both team relationships and technical mechanisms that exist between two integrating Bounded Contexts.

通过本书，大家将会了解到，在发展模型通用语言的过程中开发人员和领域专家的参与同样重要。也将看到团队中的软件开发人员与领域专家是如何协作的。这是一个由一群聪明而又上进的人们组成的重要组合，他们需要借助 DDD 来达成最佳效果。通过协作而产生的语言会变得统一、流行、并遍布于团队的日常口头交流和软件模型之中。

当进一步深入到战略设计中时，将会学到子域（Subdomain），并了解如何通过它处理遗留系统中无边界的复杂性，以及如何改进新项目上的成果。还会了解如何通过名为上下文映射（Context Mapin）的技术来集成多个限界上下文。上下文映射图（Context map）同时定义了两个进行集成的限界上下文之间的团队间关系及技术实现方式。

## 1.4 Tactical Design

After I have given you a sound foundation with strategic design, you will discover DDD’s most prominent tactical design tools. Tactical design is like using a thin brush to paint the fine details of your domain model. One of the more important tools is used to aggregate entities and value objects together into a right-sized cluster. It’s the Aggregate pattern.

![](./res/2020002.png)

DDD is all about modeling your domain in the most explicit way possible. Using Domain Events will help you both to model explicitly and to share what has occurred within your model with the systems that need to know about it. The interested parties might be your own local Bounded Context and other remote Bounded Contexts.

在打好战略设计的基础之后，将会发现 DDD 最为突出的莫过于战术层面的设计工具。战术设计犹如使用一把精小的画笔在领域模型上描绘着每个细枝末节。其中一个比较重要的工具被用来将若干实体和值对象以恰当的大小聚集在一起。这就是聚合（Aggregate）模式。

DDD 就是以最明确而又可行的方式对领域进行建模。使用领域事件（Domain Events）既可以让你明确地建立模型，也可把模型内部发生的事情分享给需要知道这一切的系统。这些相关的系统可能是你自己的本地限界上下文和其他的远程限界上下文。

## 1.5 The Learning Process and Refining Knowledge

DDD teaches a way of thinking to help you and your team refine knowledge as you learn about your business’s core competencies. This learning process is a matter of discovery through group conversation and experimentation. By questioning the status quo and challenging your assumptions about your software model, you will learn much, and this all-important knowledge acquisition will spread across the whole team. This is a critical investment in your business and team. The goal should be not only to learn and refine, but to learn and refine as quickly as possible. There are additional tools to help with those goals that can be found in Chapter 7 , “Acceleration and Management Tools .”

DDD 为我们带来了一种全新的思维方式，这种思维方式可以帮助你和你的团队在理解业务核心竟争力的同时提炼知识。学习过程是小组讨论与试验的一系列探索。通过不断地质疑现状与挑战软件模型的假设，你可以学到更多的知识，而且这些非常重要的知识将在传播中惠及整个团队。这是业务和团队所需要付出的关键投资。我们的目标不应该只是学习和提炼，而是以尽可能快的速度学习和提炼。第 7 章中将会提供很多额外的方法和工具来帮助实现这一目标。

Let’s Get Started! Even in a condensed presentation, there’s plenty to learn about DDD. So let’s get started with Chapter 2 , “Strategic Design with Bounded Contexts and the Ubiquitous Language .”
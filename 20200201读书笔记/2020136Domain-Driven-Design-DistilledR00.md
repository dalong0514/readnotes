# 2020136Domain-Driven-Design-DistilledR00

Copyright © 2016 Pearson Education, Inc.

## 记忆时间

## 卡片

### 0101. 主题卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——三种学习模式

听者、视者和触者。

But why? Every person has a learning style. There are a number of learning styles, but three of the most discussed are auditory, visual, and tactile styles. The auditory learners learn by hearing and listening. The visual learners learn by reading or seeing imagery. The tactile learners learn by doing something that involves touching. It’s interesting that each learning style is heavily favored by the individual to the extent that he or she can sometimes have trouble with other types of learning. For example, tactile learners likely remember what they have done but may have problems remembering what was said during the process. With model building, you would think that visual and tactile learners would have a huge advantage over the auditory learners, because model building seems to mostly involve visual and tactile stimulation. However, that might not always hold true, especially if a team of model builders uses audible communication in their building process. In other words, model building holds out the possibility to accommodate the learning style of the vast majority of individuals.

### 0202. 术语卡——Strategic Design

We begin with the all-important strategic design. You really cannot apply tactical design in an effective way unless you begin with strategic design. Strategic design is used like broad brushstrokes prior to getting into the details of implementation. It highlights what is strategically important to your business, how to divide up the work by importance, and how to best integrate as needed.

First you will learn how to segregate your domain models using the strategic design pattern called Bounded Contexts. Hand in glove, you will see how to develop a Ubiquitous Language as your domain model within an explicitly Bounded Context.

You will learn about the importance of engaging with not only developers but also Domain Experts as you develop your model’s Ubiquitous Language. You will see how a team of both software developers and Domain Experts collaborate. This is a vital combination of smart and motivated people who are needed for DDD to produce the best results. The language you develop together through collaboration will become ubiquitous, pervasive, throughout the team’s spoken communication and software model.

As you advance further into strategic design, you will learn about Subdomains and how these can help you deal with the unbounded complexity of legacy systems, and how to improve your results on greenfield projects. You will also see how to integrate multiple Bounded Contexts using a technique called Context Mapping. Context Maps define both team relationships and technical mechanisms that exist between two integrating Bounded Contexts.

### 0203. 术语卡——Tactical Design

After I have given you a sound foundation with strategic design, you will discover DDD’s most prominent tactical design tools. Tactical design is like using a thin brush to paint the fine details of your domain model. One of the more important tools is used to aggregate entities and value objects together into a right-sized cluster. It’s the Aggregate pattern.

DDD is all about modeling your domain in the most explicit way possible. Using Domain Events will help you both to model explicitly and to share what has occurred within your model with the systems that need to know about it. The interested parties might be your own local Bounded Context and other remote Bounded Contexts.

### 0204. 术语卡——限界上下文（Bounded Contexts）

First, a Bounded Context is a semantic contextual boundary. This means that within the boundary each component of the software model has a specific meaning and does specific things. The components inside a Bounded Context are context specific and semantically motivated. That’s simple enough.

When you are just getting started in your software modeling efforts, your Bounded Context is somewhat conceptual. You could think of it as part of your problem space. However, as your model starts to take on deeper meaning and clarity, your Bounded Context will quickly transition to your solution space , with your software model being reflected as project source code. (The problem space and solution space are better explained in the box.) Remember that a Bounded Context is where a model is implemented, and you will have separate software artifacts for each Bounded Context.

首先，限界上下文是语义和语境上的边界。这意味着边界内的每个代表软件模型的组件都有着特定的含义并处理特定的事务。限界上下文中的这些组件有特定的上下文语境和语义理据。这确实很简单。如果刚刚开始投入到软件建模中，限界上下文多少是有些概念化的。你可以将它理解为问题空间（Problem Space）的一部分。然而，随着软件模型开始呈现出更深层次以及更清断的含义时，限界上下文将会被迅速转换到解决方案空间（Solution Space）中，同时软件模型将通过项目的源代码来体现（下面这段文字可以更好地解释问题空间和解决方案空间）。请记住，模型是在限界上下文中实现的，你也将会为每个限界上下文开发出不同的软件。

What Is a Problem Space and a Solution Space?

Your problem space is where you perform high-level strategic analysis and design steps within the constraints of a given project. You can use simple diagrams as you discuss the high-level project drivers and note important goals and risks. In practice, Context Maps work very well in the problem space. Note too that Bounded Contexts may be used in problem space discussions, when needed, but are also closely associated with your solution space.

Your solution space is where you actually implement the solution that your problem space discussions identify as your Core Domain. When the Bounded Context is being developed as a key strategic initiative of your organization, it’s called the Core Domain. You develop your solution in the Bounded Context as code, both main source and test source. You will also produce code in your solution space that supports integration with other Bounded Contexts .

什么是问题空间和解决方案空间？问题空间是在给定项目的约束条件下进行高级战略分析与设计各个步骤的地方。你可以使用简单的图表来展示讨论中高级的项目驱动因素，并记录关键目标与风险。在实践中，上下文映射图可以在问题空间中工作得很好。同时还要注意，限界上下文不仅可以在需要时用于问题空间的讨论，也与你的解决方案空间密切相关。

解决方案空间就是真正实施解决方案的地方，这些解决方案在问題空间讨论中被识别为核心域（Core Domain）。当限界上下文被当作组织的关键战略举措进行开发时，即被称为核心域。你将主要通过源代码和测试代码来实现限界上下文中的解决方案，也会在解決方案空间中编写代码，来支撑与其他限界上下文之间的集成。

1 核心域的识别是一个持续的精练过程，把一堆混杂在一起的组件分离，以某种形式提炼出最重要的内容，这种形式也将使核心域更具价值。一个严峻的现实是，我们不可能对所有的设计部分投入同等的资源进行优化，如同 MVP (Minimum Viable Product）产品原则所提倡的那样，产品研发需要聚焦在最小化可行产品上，不断获取用户反馈，并在这个最小化可行产品上持续快速选代，从而获得一个稳定的核心产品。在有限的资源下，为了使领域模型成为最有价值的资产，我们必须有效地梳理出模型的真正核心并完全根据这个核心来实现软件服务，这也是核心域的战略价值所在。一一译注

### 0206. 术语卡——通用语言（Ubiquitous Language）

The software model inside the context boundary reflects a language that is developed by the team working in the Bounded Context and is spoken by every member of the team that creates the software model that functions within that Bounded Context. The language is called the Ubiquitous Language because it is both spoken among the team members and implemented in the software model. Thus, it is necessary that the Ubiquitous Language be rigorous—strict, exact, stringent, and tight. In the diagram, the boxes inside the Bounded Context represent the concepts of the model, which may be implemented as classes. When the Bounded Context is being developed as a key strategic initiative of your organization, it’s called the Core Domain.

团队在限界上下文中发展了一种语言用于表达其边界内的软件模型，这一语言由在该界上下文中开发软件模型的每个团队成员所使用。它之所以被称之为通用语言（Ubiquitous Language）2，是因为团队成员间交流用的是它，软件模型实现的也是它。因此，通用语言必须严谨、精确，并且紧湊。上图中，限界上下文中的方框所表示的概念模型可以用类来实现。当限界上下文被当作组织的关键战略举措进行开发时，即被称之为核心域。

2 在《实例化需求》[Specification] 一书中译作統一语言，也是一种常见的译法。一一译注

When compared with all the software your organization uses, a Core Domain is a software model that ranks among the most important, because it is a means to achieve greatness. A Core Domain is developed to distinguish your organization competitively from all others. At the very least it addresses a major line of business. Your organization can’t excel at everything and shouldn’t even try. So you choose wisely what should be part of your Core Domain and what should not. This is the primary value proposition of DDD, and you want to invest appropriately by committing your best resources to a Core Domain.

When someone on the team uses expressions from the Ubiquitous Language , everyone on the team understands what is meant with precision and constraints. The expression is ubiquitous within the team, as is all language used by the team that defines the software model being developed.

When you consider language in a software model, think of the various nations that make up Europe. Within one of the countries across this space, the official language of each country is clear. Within the boundaries of those nations—for example, Germany, France, and Italy—the official languages are certain. As you cross a boundary, the official language changes. The same goes for Asia, where Japanese is spoken in Japan, and the languages spoken in China and Korea are clearly different across the national boundaries. You can think of Bounded Contexts in much the same way, as being language boundaries. In the case of DDD, the languages are those spoken by the team that owns the software model, and a notable written form of the language is the software model’s source code.

与组织使用的所有其他软件相比，核心域是其中最重要的软件模型，因为它是组织取得巨大成就的手段。发展核心域可以使你的组织在与其他组织的竞争中脱颗而出。至少，它标明了组织的业务主航道。你的组织无法在所有领域都出类拔萃，也无须如此。因此你需要做出明智的选择，哪些是核心域，而哪些不是。这是 DDD 的首要价值主张，同时你也期望通过恰当的投资把最好的资源投入到核心域中。当团队中有人使用通用语言进行交流时，其他人都可以明白他表达的准确含义和约束条件。通用语言和开发软件模型中使用的其他语言一样，在团队中无处不在。

当你思考软件模型中的语言时，想一想组成欧洲的各个国家：整个欧洲大陆中的任何一个国家，使用的官方语言都是明确的。在这些国家的边境内，如德国、法国和意大利，官方语言是确定的。当你越过边境时，官方语言也会改变。同样的情况也适用于亚洲：被界线分开的日本、韩国和中国都使用着自己的语言。限界上下文也是如此。在 DDD 中通用语言就是软件模型团队日常交流时使用的语言，而软件模型的源代码就是这种语言的书面表达方式。

### 0207. 术语卡——子域（Subdomain）

Simply stated, a Subdomain is a sub-part of your overall business domain. You can think of a Subdomain as representing a single, logical domain model. Most business domains are usually too large and complex to reason about as a whole, so we generally concern ourselves only with the Subdomains that we must use within a single project. Subdomains can be used to logically break up your whole business domain so that you can understand your problem space on a large, complex project.

Another way to think of a Subdomain is that it is a clear area of expertise, assuming that it is responsible for providing a solution to a core area of your business. This implies that the particular Subdomain will have one or more Domain Experts who understand very well the aspects of the business that a specific Subdomain facilitates. The Subdomain also has greater or lesser strategic significance to your business.

If DDD had been used to develop it, the Subdomain would have been implemented as a clean Bounded Context. The Domain Experts who specialize in that particular area of the business would have been members of the team that developed the Bounded Context. Although using DDD to develop a clean Bounded Context is the optimal choice, sometimes we can only wish that had been the case.

简单地说，子域是整个业务领域的一部分。你可以认为子域代表的是一个单一的、有逻辑的领域模型。大多数的业务领域都过于庞大和复杂，难以作为整体来分析，因此我们般只关心那些必须在单个项目中涉及的子域。子域可以用来逻辑地拆分整个业务领域，这样才能理解存在于大型复杂项目中的问题空间。

也可以认为子域是一个明确的专业领域，假设它负责为核心业务提供解决方案。这意味着特定的子城将会有一位或多位领域专家领衔，他们非常了解由这些特定子域促成的业务的方方面面。对你的业务而言，子域也有或多或少的战略意义。

如果通过 DDD 来创建子域，它将会被实现成一个清晰的限界上下文。特定业务的领域专家将会成为共建限界上下文团队中的一员。虽然使用 DDD 来建立一个清晰的限界上下文是最佳选择，但有时这只是我们一厢情愿的想法。

### 0207. 术语卡——上下文映射（Context Mapping）

### 0205. 术语卡——领域对象

### 0207. 术语卡——代码走查（如 Pull Request）

### 0301. 人名卡——Vaughn Vernon

沃恩·弗农（Vaughn Vernon），DDD 的布道者，著作《IDDD》以及本书《DDD精粹》。

注：Google 上搜 Vaughn Vernon 可以获取不少有价值的信息，比如他的演讲视频。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 任意卡——本书的内容框架

领域驱动设计（DDD）是时下软件设计领域中的热门话题，它通过指导我们构建领域模型，来表达丰富的软件功能需求，并由此实现可以满足用户真正需要的软件。然而在实践过程中，由于不同的角色对于 DDD 的核心概念和主要工具的理解不同，常常会造成协作上的不一致。为了帮助和指导面向对象的开发人员、系统分析人员和设计人员更加合理地组织工作，各有侧重、有条不紊地进行复杂系统的开发，并有效地建立丰富而实用的领域模型，本书的作者 Vaughn Vernon 将自己近年来在领域驱动设计领域的理解进一步提炼，并将本书以精粹的形式呈现给广大的读者。本书的内容包括：DDD 对于广大读者的意义、从战略层面进行设计、从战术层面进行设计，以及相关的辅助工具。当然，仅仅通过此书的阅读无法深入地掌握领域驱动设计的精髓，无论你是什么经验水平或角色，请阅读本书并在项目中实践 DDD。并在这之后，再重读此书，看看你从项目的经历中学到了什么。反复这样的循环，你将会获益匪浅。

### 0502. 任意卡——软件开发过程中的十大问题

1、软件开发被视为成本中心而非利润中心。

2、开发人员热衷于技术并通过技术手段解决问题，而非深入思考和设计。

3、过于重视数据库，大多数解决方案的讨论都是围绕这数据库和数据模型，而非业务流程和运作方式。

4、开发人员对领域对象不够重视。

5、业务协作不顺畅，业务干系人员常浪费时间闭门造车，实现各种无人问津的需求。

6、频繁而又要求精准的项目估算会占有大量时间和精力。

7、开发人员在用户界面和持久层组件中构建业务逻辑。

8、数据库查询会时常出现中断、延退、死锁等问题。

9、项目中存在着错误的抽象级别。

10、紧耦合服务群。

### 0503. 任意卡——团队应该在一个限界上下文中工作

Bounded Contexts, Teams, and Source Code Repositories

There should be one team assigned to work on one Bounded Context. There should also be a separate source code repository for each Bounded Context. It is possible that one team could work on multiple Bounded Contexts , but multiple teams should not work on a single Bounded Context. Cleanly separate the source code and database schema for each Bounded Context in the same way that you separate the Ubiquitous Language. Keep acceptance tests and unit tests together with the main source code.

It is especially important to be clear that one team works on a single Bounded Context. This completely eliminates the chances of any unwelcome surprises that arise when another team makes a change to your source code. Your team owns the source code and the database and defines the official interfaces through which your Bounded Context must be used. It’s a benefit of using DDD.

一个团队应该在一个限界上下文中工作。每个限界上下文应该拥有一个独立的源代码仓库 1。一个团队可能工作在多个限界上下文中，但是多个团队不应该在同一个限界上下文中共事。我们应该采用和分离通用语言同样的方式，千净地把不同限界上下文的源代码和数据库模式隔离开。并且，将同一个限界上下文中的验收測试、单元測试和主要源代码存放在一起。尤其重要的是，要明确一个团队只在单一的限界上下文中工作。别给其他团队留下任何机会去修改你的源代码，从而引发意外。2 你的团队控制着源代码和数据库并定义了官方接口，必须通过这些接口才可以调用限界上下文。这是使用DDD 所能带来的好处之一。

1 传统软件开发方式里，一个产品往往由多个组件团队共同开发，组件代码分别存放在不同的代码仓库，只有负责的团队拥有组件代码仓库的所有权。由于使用了这种代码仓库的划分方法，大量的集成将会发生在组件与组件之间，同时也会产生大量的跨团队的交流和代码访问。一种常见的场景是，在开发初期新的功能往往无法集成并正常运作，更不可能完成阶段性验收，只有等到开发的后期才能获得一个可以运行的产品。而书中提及的独立代码仓库将遵循限界上下文进行划分，上下文内使用统一的通用语言进行交流，并尽可能由一个团队对领域模型进行维护。两种代码仓库的划分方式的最大区别在于，限界上下文内的领域模型往往具有独立的业务价值，可以独立地提供服务。而传统的组件式代码仓库经常会存在相互间的紧耦合关系，无法独立地提供服务。本书译者所著的《代码管理核心技术及实践》一书中也谈到了类似的案例，介绍了一个团队是如何从组件代码仓库转换到领域代码仓库的。一一译注 

2 这并不是绝对的。事实上，很多上下文的代码仓库是开放的，并接受其他团队提交的代码。甚至，很多独角兽企业（如 Google 和 Facebook）在代码仓库上惊人一致地选择了单一仓库（monoreme）进行代码管理，即整个组织所有的产品代码放在唯一一个超大的代码仓库中。这些代码并不是铁板一块，它依然可以被分成多个服务甚至多个产品，由多个团队独立地构建、测试和维护。单一仓库和开放仓库一样更注重的是代码共有制带来的协作效率。代码共有制不会造成混乱，原因在于它们拥有完善的机制和工具对所有提交的代码进行准入控制和验证，而这些仓库的贡献者也对编写代码有着严格的自我要求。所以并不是要杜绝其他团队对代码仓库进行修改，而是要让这些修改可以预期且可以控制，这必须采取些适合团队的实践和工具来实现，例如频繁交流（如结对编程）、代码走查（如 Pull Request）和自动化验证（如契约测试）等。这些实践和手段往往由上下文映射关系决定，如共享内核关系就可以采用 Pull Request 的实践，而客户一供应商关系则可以采用契约测试的实践。关于映射关系的讨论请参考本书第 4 章的内容。——译注

### 0504. 任意卡——避免过渡设计

抑制住过渡设计。采用战略设计中的「限界上下文」和「通用语言」可以避免过渡设计，只关注核心领域功能。

What tools are available with DDD to help us avoid such pitfalls? You need at least two fundamental strategic design tools. One is the Bounded Context and the other is the Ubiquitous Language. Employing a Bounded Context forces us to answer the question “What is core?” The Bounded Context should hold closely all concepts that are core to the strategic initiative and push out all others. The concepts that remain are part of the team’s Ubiquitous Language. You will see how DDD works to avoid the design of monolithic applications.

DDD 中有哪些工具可以帮助我们避免这些陷阱？你至少需要两种基本的战略设计工具，限界上下文和通用语言。采用限界上下文会迫使我们回答「什么是核心？」的问题。它应紧紧地抓住战略举措中所有的核心概念，并排除其他概念，剩下的都应该是团队通用语言的一部分。你将看到 DD 如何避免单体应用设计的产生。

### 0505. 任意卡——三大类子域

There are three primary types of Subdomains within a project:

1. Core Domain: This is where you are making a strategic investment in a single, well-defined domain model, committing significant resources for carefully crafting your Ubiquitous Language in an explicit Bounded Context. This is very high on your organization’s list of projects because it will distinguish it from all competitors. Since your organization can’t be distinguished in everything that it does, your Core Domain demarcates where it must excel. Achieving the level of deep learning and understanding required to make such a determination requires commitment, collaboration, and experimentation. It’s where the organization needs to invest most liberally in software. I provide the means to accelerate and manage such projects efficiently and effectively later in this book.

2. Supporting Subdomain: This is a modeling situation that calls for custom development, because an off-the-shelf solution doesn’t exist. However, you will still not make the kind of investment that you have made for your Core Domain. You may want to consider outsourcing this kind of Bounded Context to avoid mistaking it for something strategically distinguishing, and thus investing heavily in it. This is still an important software model, because your Core Domain cannot be successful without it.

3. Generic Subdomain: This kind of solution may be available for purchase off the shelf but may also be outsourced or even developed in house by a team that doesn’t have the kind of elite developers that you assign to your Core Domain or even a lesser Supporting Subdomain. Be careful not to mistake a Generic Subdomain for a Core Domain. You don’t want to make that kind of investment here.

When discussing a project where DDD is being employed, we are most likely discussing a Core Domain.

1、核心域（Sub Domain）：它是一个唯一的、定义明确的领域模型，要对它进行战略投资，并在一个明确的限界上下文中投入大量资源去精心打磨通用语言。它是组织中最重要的项目，因为这将是你与其他竟争者的区别所在。正是因为你的组织无法在所有领域都出类拔萃，所以必须把核心域打造成组织的核心竟争力。做出这样的决定需要对核心域进行深入的学习与理解，而这需要承诺、协作与试验。这是组织最需要在软件中倾斜其投资的方向。后面的章节中会提供加速与高效管理这些项目的方法。

2、支撑子域（Supporting Subdomain）：这类建模场景提倡的是「定制开发」，因为找不到现成的解决方案。对它的投入无论如何也达不到与核心域相同的程度。也许会考虑使用外包的方式实现此类限界上下文，以避免因错误地认为其具有战略意义而进行巨额的投资。这类软件模型仍旧非常重要，核心域的成功离不开它。

3、通用子域（Generic Subdomain）：通用子域的解決方案可以采购现成的，也可以采用外包的方式，抑或是由内部团队实现，但我们不用为其分配与核心域同样优质的研发资源，甚至都不如支撑子域。请注意不要把通用子域误认为是核心域。我们并不希望对其投资过甚。当讨论一个正在实施 DDD 的项目时，最有可能讨论的是核心域。

1 子域的划分，不仅仅涉及实现方式、投资规模，同时还会影响组织的架构、流程。因此，合理的子域划分，以及每个子域恰当的定位，是产品得以顺利发展的重要因素。因此我们需要更好地理解这三种子域的定位。核心域是产品独特的竞争力，它是产品之所以存在的根本。因此在产品的初期，没有经过市场的验证之前，我们需要遵循 MVP (Minimum Viable Product）的原则，快速地迭代以获取市场的反馈，一旦产品被市场证明，合理的重构即需要被发生。支撑子域不需要过度地考虑可扩展性和兼容性，可重用性并非其技术着力的方向，可替代性才是，这也要求我们需要对于支撑子域有着明确的契约规范和业务约束条件。通用子域内的业务规则相对明确，在很多产品和业务上下文中保持高度的重合度，因此我们需要通过快速的采购获取，我们对其定制化要求较低，而稳定性和兼容性则要求较高。——译注

## 译者序

2003 年，Eric Evans 的《领域驱动设计》出版，第一次总结了这种软件设计和建模方法。这种方法让团队在质疑中发展出对复杂问题的统一认识，再利用战略设计和战术设计的各种手段，如同庖丁解牛般地分解并映射成各种构造块，最后信手拈来地运用各种设计模式将这些构造块一一化解。领域驱动设计在国外的技术社区一直是受到热捧、不断演化的软件设计方法。在 Eric 的著作面世十年之后，另一位 DDD 社区的领军人物 Vaughn Vernon 撰写了《实现领域驱动设计》。在这本著作中，Vaughn 用一个连贯完整的实例，将领域驱动设计的所有概念和模式串连在一起，并将这些内容落地到了实例的代码之中。另外，他还在这部著作中总结了这十年来 DDD 社区涌现的一些新的架构风格和模式，如事件溯源和 CQRS、REST 风格的架构、事件驱动的架构、六边形架构，等等。

但这十几年间，在国内技术社区，领域驱动设计却像被遗忘在角落的宝藏等待着人们去发掘。当越来越复杂的业务场景开始频繁涌现，当工程实践和基础设施发展成熟，我们重新将视线汇聚在如何达成有效设计、将复杂的业务分而治之，我们发现这种设计方法仿佛早就看透了一切。当宝藏上的灰尘被拂去，领域驱动设计再次发出璀璨夺目的光芒，为我们指明应对软件系统复杂性的前进方向。

重新焕发青春活力的领域驱动设计得到了许多新的团队和架构师的青睞。他们首先就会去阅读这两部略微晦涩的著作，期望能快速地学习和掌握这种方法，但很快就会发现这并不轻松。首先，这两部著作要求读者具备一定的软件开发技术背景。在领域驱动设计的实践中，业务领域的专家在团队中扮演关键角色，他们往往没有软件开发的技术背景。两位软件巨匠在著作中详细阐述技术概念和实现代码时并没有照顾他们的感受。其次，这两部著作缺少对实际项目建模过程的描写。我们读到的内容多是概念的阐述和与之对应的实例及代码，对于建模实操的过程和工具着墨不多。而这些 Magic Move 却是很多团队实施领域驱动设计时迫切需要指导的关键步骤。最后，两部著作的内容包罗万象，读者容易被繁杂的知识淹没。两部著作中的一些概念和模式（如值对象、实体、工厂和仓储）早已深入人心。而另一部分模式和架构（如事件溯源和 CQRS）则要求架构经验尚浅的读者通过项目实践或扩展阅读才能深入理解。

作为《实现领域驱动设计》一书的作者，Vaughn 也意识到了这些问题，因此编写了这本「精粹版」。他将领域驱动设计的知识进行了提炼，保留了子域、限界上下文、上下文映射、聚合、领域事件这些核心概念，分别用一个章节进行了阐述。在最后一章，作者将他过去在一些团队中实践领域驱动设计时行之有效的具体操作方法（如风靡 DDD 社区的事件风暴工作坊）和工具进行了总结。本书的内容更侧重于高层次的战略设计，关于战术设计的内容偏少，尤其是代码在内容中的比重极低，完全不影响非技术背景的读者阅读。如果你想开始在团队中尝试领域驱动设计，对于团队（包括业务领域的专家）来说，本书的内容可以作为指导手册，让他们快速地进入状态，达到可以参与事件风暴工作坊的要求。我们建议读者们在阅读本书之后亲自组织并实施一次事件风暴工作坊，这是作者推荐的融合视觉、听觉和触觉三种学习方式的「知识获取」实践，是威力无穷的领域建模形式。在开发团队完成建模并最终需要落实到代码时，读者可以将本书作为「武林秘籍」的目录，结合前两部著作和本书参考文献中引用的其他专著一起阅读。

本书中，作者毫不掩饰地表达了对一些架构模式和具体实践的偏好。这些特色鲜明的观点之中，有些符合社区的普遍认知，如事件驱动的响应式架构、单元测试、事件风暴；有些却是对争议性话题的个人理解，如作者对于建模设计的工作量估算的看法。我们要牢记一点，没有「银弹」可以精确地匹配我们的产品和团队，或者完美地解决我们要面对的可题。任何工具和实践都有约束条件。读者们在采用这些工具和实践时，不妨仔细思考作者运用它们的上下文及其体现出的原则，结合自己的实际情况对工具和实践进行持续改进，避免出现教条主义错误。

## About the Author

Vaughn Vernon is a veteran software craftsman and thought leader in simplifying software design and implementation. He is the author of the best-selling books Implementing Domain-Driven Design and Reactive Messaging Patterns with the Actor Model, also published by Addison-Wesley. He has taught his IDDD Workshop around the globe to hundreds of software developers. Vaughn is a frequent speaker at industry conferences. He is most interested in distributed computing, messaging, and in particular with the Actor model. Vaughn specializes in consulting around Domain-Driven Design and DDD using the Actor model with Scala and Akka. You can keep up with Vaughn’s latest work by reading his blog at www.VaughnVernon.co and by following him on his Twitter account @VaughnVernon.

2『做一张人名卡片。』

## Preface

Why is model building such a fun and rewarding activity? Ever since I was a kid I have loved to build models. At that time I mostly built models of cars and airplanes. I am not sure where LEGO was in those days. Still, LEGO has been a big part of my son’s life since he was very young. It is so fascinating to conceive and build models with those small bricks. It’s easy to come up with basic models, and it seems you can extend your ideas almost endlessly. You can probably relate to some kind of youthful model building.

Models occur in so many situations in life. If you enjoy playing board games, you are using models. It might be a model of real estate and property owners, or models of islands and survivors, or models of territories and building activities, and who knows what all. Similarly, video games are models. Perhaps they model a fantasy world with fanciful characters playing fantastic roles. A deck of cards and related games model power. We use models all the time and probably so often that we don’t give most models a well-deserved acknowledgment. Models are just part of our lives.

But why? Every person has a learning style. There are a number of learning styles, but three of the most discussed are auditory, visual, and tactile styles. The auditory learners learn by hearing and listening. The visual learners learn by reading or seeing imagery. The tactile learners learn by doing something that involves touching. It’s interesting that each learning style is heavily favored by the individual to the extent that he or she can sometimes have trouble with other types of learning. For example, tactile learners likely remember what they have done but may have problems remembering what was said during the process. With model building, you would think that visual and tactile learners would have a huge advantage over the auditory learners, because model building seems to mostly involve visual and tactile stimulation. However, that might not always hold true, especially if a team of model builders uses audible communication in their building process. In other words, model building holds out the possibility to accommodate the learning style of the vast majority of individuals.

With our natural affinity to learning through model building, why would we not naturally desire to model the software that ever increasingly assists and influences our lives? In fact, to model software appears to be, well, human. And model software we should. It seems to me that humans should be elite software model builders.

从建模中学习的能力是人类与生俱来的，为何不利用它去构建已经给生活带来巨大帮助和影响的软件模型呢？事实上，软件模型需要人类去实现，也应该由人类去完成。我认为，人类本应该是优秀的软件模型构建者。

It is my strong desire to help you be as human as you can possibly be by modeling software using some of the best software modeling tools available. These tools are packaged under the name “Domain-Driven Design,” or DDD. This toolbox, actually a set of patterns, was first codified by Eric Evans in the book Domain-Driven Design: Tackling Complexity in the Heart of Software [DDD] . It is my vision to bring DDD to everyone possible. To make my point, if I must say that I want to bring DDD to the masses, then so be it. That is where DDD deserves to be, and DDD is the toolbox that model-oriented humans deserve to use to create their most advanced software models. With this book, I am determined to make learning and using DDD as simple and easy as possible and to bring that to the broadest conceivable audience.

我强烈期望能够帮助你使用最好的建模工具来实现软件。这些工具已被打包成「领域驱动设计」工具箱，或称之为 DDD 工具箱。该工具箱实际上是一套模式，在 Eric Evans 所著的《领域驱动设计：软件核心复杂性应对之道》一书中首次提出。我期望将 DDD 带给每一个人。如果必须表达我的观点，我想说的是，让我把 DDD 介绍给大家吧！DDD 也本该如此，它是面向模型设计的人们用于构建卓越软件模型的工具箱。本书中，我会尽可能地简化 DDD 的学习和使用，并将其带给每一位读者。

For auditory learners, DDD holds out the prospect of learning through the team communication of building a model based on the development of a Ubiquitous Language. For visual and tactile learners, the process of using DDD tools is very visual and hands-on as your team models both strategically and tactically. This is especially true when drawing Context Maps and modeling the business process using Event Storming. Thus, I believe that DDD can support everyone who wants to learn and achieve greatness through model building.

1『出现了 2 个关键词，绘制上下文映射图、用事件暴风建模。』

对于听觉学习者而言，DDD 通过团队的沟通来构建基于通用语言的开发模型，并以此创造学习的契机。对于视觉和触觉学习者来说，在团队进行战略和战术建模时使用 DDD 其过程高度视觉化并非常注重实操。绘制上下文映射图并使用事件风暴构建业务流程时尤为如此。因此，我相信 DDD 可以帮助到每一位期待通过模型构建来学习并且希望获得伟大成就的人。

### Who Is This Book For?

This book is for everyone interested in learning the most important DDD aspects and tools and in learning quickly. The most common readers are software architects and software developers who will put DDD into practice on projects. Very often, software developers quickly discover the beauty of DDD and are keenly attracted to its powerful tooling. Even so, I have made the subject understandable for executives, domain experts, managers, business analysts, information architects, and testers alike. There’s really no limit to those in the information technology (IT) industry and research and development (R&D) environments who can benefit from reading this book.

3『忘记在哪里看到过（好像是「科学」杂志的一篇文章），把人员分成了 IT 和 R&D 两大类，待确认。（2020-07-29）』

If you are a consultant and you are working with a client to whom you have recommended the use of DDD, provide this book as a way to bring the major stakeholders up to speed quickly. If you have developers—perhaps junior or midlevel or even senior—working on your project who are unfamiliar with DDD but need to use it very soon, make sure that they read this book. By reading this book, at minimum, all the project stakeholders and developers will have the vocabulary and understand the primary DDD tools being used. This will enable them to share things meaningfully as they move the project forward.

Whatever your experience level and role, read this book and then practice DDD on a project. Afterward, reread this book and see what you can learn from your experiences and where you can improve in the future.

### What This Book Covers

The first chapter, “DDD for Me,” explains what DDD can do for you and your organization and provides a more detailed overview of what you will learn and why it’s important.

Chapter 2 , “Strategic Design with Bounded Contexts and the Ubiquitous Language ,” introduces DDD strategic design and teaches the cornerstones of DDD, Bounded Contexts and the Ubiquitous Language. 

Chapter 3 , “Strategic Design with Subdomains ,” explains Subdomains and how you can use them to deal with the complexity of integrating with existing legacy systems as you model your new applications. 

Chapter 4 , “Strategic Design with Context Mapping ,” teaches the variety of ways that teams work together strategically and ways that their software can integrate. This is called Context Mapping.

Chapter 5 , “Tactical Design with Aggregates ,” switches your attention to tactical modeling with Aggregates. An important and powerful tactical modeling tool to be used with Aggregates is Domain Events , which is the subject of Chapter 6 , “Tactical Design with Domain Events .”

Finally, in Chapter 7 , “Acceleration and Management Tools ,” the book highlights some project acceleration and project management tools that can help teams establish and maintain their cadence. These two topics are seldom if ever discussed in other DDD sources and are sorely needed by those who are determined to put DDD into practice.
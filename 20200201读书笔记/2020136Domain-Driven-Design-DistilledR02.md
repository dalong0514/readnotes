# 2020136Domain-Driven-Design-DistilledR02

Copyright © 2016 Pearson Education, Inc.

## 记忆时间

## 0501. Tactical Design with Aggregates

In this chapter you learned: 1) What the Aggregate pattern is and why you should use it. 2) The importance of designing with a consistency boundary in mind. 3) About the various parts of an Aggregate. 4) The four rules of thumb of effective Aggregate design. 5) How you can model an Aggregate ’s unique identity. 6) The importance of Aggregate attributes and how to prevent creating an Anemic Domain Model. 7) How to model behavior on an Aggregate. 8) To always adhere to the Ubiquitous Language within a Bounded Context. 9) The importance of selecting the proper level of abstraction for your designs. 10) A technique for right-sizing your Aggregate compositions, and how that includes designing for testability. For a more in-depth treatment of Entities , Value Objects , and Aggregates , see Chapters 5 , 6 , and 10 of Implementing Domain-Driven Design [IDDD] .

总结：1）什么是聚合模式以及为什么应该使用它。2）设计时牢记在一致性边界的重要性。3）一个聚合的不同组成部分。4）有效聚合设计的四条经验法则。5）如何对聚合的唯一标识符进行建模。6）聚合属性的重要性以及如何避免创建贫血领域模型。7）如何对聚合的行为进行建模。8）在限界上下文中始终遵循通用语言。9）为你的设计选择适当抽象级别的重要性。10）一种让聚合大小适中的技术，以及它如何蕴含着可测试性的设计。

So far I have discussed strategic design with Bounded Contexts, Subdomains, and Context Maps. Here you see two Bounded Contexts, the Core Domain named Agile Project Management Context and a Supporting Subdomain that provides collaboration tools through Context Mapping integration.

But what about the concepts that live inside a Bounded Context ? I’ve touched on these, but I will next cover them in more detail. They are likely the Aggregates in your model.

目前为止，我们讨论的都是使用限界上下文（Bounded Conter）、子域（Sub Domain)和上下文映射图（Context Map）的战略设计。这里你看到的是两个限界上下文，名为敏捷项目管理上下文的核心域（Core Domain）和提供协作工具的支撑子域（Supporting Subdomain），它们使用上下文映射（Context Mapping）集成在一起。但是那些包含在限界上下文之中的概念又是什么呢？接下来，将详细地阐述这些之前曾经提及的概念。它们很可能就是你模型中的聚合（Aggregate）。

### 5.1 Why Used

Each of the circled concepts that you see inside these two Bounded Contexts is an Aggregate. The one concept not circled—Discussion —is modeled as a Value Object. Even so, we are focused on Aggregates in this chapter, and we will take a closer look at how to model Product, BacklogItem, Release, and Sprint.

这两个限界上下文中你看到的每一个被圈起来的概念都是一个聚合。只有一个概念 Discussionー一没有被圈起来，它被作为一个值对象（Value object）进行建模。尽管如此，本章我们将重点放在聚合上，并将仔细研究如何对 Product、BacklogItem、Release 和 Sprint 进行建模。

『

What Is an Entity?

An Entity models an individual thing. Each Entity has a unique identity in that you can distinguish its individuality from among all other Entities of the same or a different type. Many times, perhaps even most times, an Entity will be mutable; that is, its state will change over time. Still, an Entity is not of necessity mutable and may be immutable. The main thing that separates an Entity from other modeling tools is its uniqueness—its individuality.

See Implementing Domain-Driven Design [IDDD] for an exhaustive treatment of Entities.

一个实体模型就是一个独立的事物。每个实体都拥有一个唯一的标识符，可以将它的个体性和所有其他类型相同或者不同的实体区分开。许多时候，也许应该说绝大多时侯，实体是可变的。也就是说，它的状态会随着时间发生变化。不过，一个实体不一定必须是可变的，它也可能是不可变的。将实体与其他建模工具区分开的主要因素是它的唯一性一一即它的个体性。请参阅《实现领域驱动设计》中更多对实体的译尽阐述。

』

What is an Aggregate? Two are represented here. Each Aggregate is composed of one or more Entities, where one Entity is called the Aggregate Root. Aggregates may also have Value Objects composed on them. As you see here, Value Objects are used inside both Aggregates.

聚合是什么？这里展示了两个聚合。它们都是由一个或多个实体组成，其中一个实体被称为聚合根（Aggregate Rool）。聚合的组成还可能包括值对象。就像这里看到的，两个聚合中都用到了值对象。

『

What Is a Value Object?

A Value Object, or simply a Value, models an immutable conceptual whole. Within the model the Value is just that, a value. Unlike an Entity, it does not have a unique identity, and equivalence is determined by comparing the attributes encapsulated by the Value type. Furthermore, a Value Object is not a thing but is often used to describe, quantify, or measure an Entity.

See Implementing Domain-Driven Design [IDDD] for detailed coverage of Value Objects.

一个值对象，或者更简单地说，值（Value），是对一个不变的概念整体所建立的模型。在这个模型中，值就真的只有一个值。和实体不一样，它没有唯一标识符，而是由值类型封的属性对比来决定相等性。此外，一个值对象不是事物而是常常被用来描述、量化或者测量一个实体。请参阅《实现领域驱动设计》来获得更多对值对象的译细介绍。

』

The Root Entity of each Aggregate owns all the other elements clustered inside it. The name of the Root Entity is the Aggregate’s conceptual name. You should choose a name that properly describes the conceptual whole that the Aggregate models.

1『根实体的名称就是聚合概念上的名称，跟聚合取名时就先找出其跟实体。』

每个聚合的根实体（Root Entity）控制着所有聚集在其中的其他元素。根实体的名称就是聚合概念上的名称。你应该选择一个名称来恰当地描述聚合模型概念上的完整性。

Each Aggregate forms a transactional consistency boundary. This means that within a single Aggregate, all composed parts must be consistent, according to business rules, when the controlling transaction is committed to the database. This doesn’t necessarily mean that you are not supposed to compose other elements within an Aggregate that don’t need to be consistent after a transaction. After all, an Aggregate also models a conceptual whole. But you should be first and foremost concerned with transactional consistency. The outer boundary drawn around Aggregate Type 1 and Aggregate Type 2 represents a separate transaction that will be in control of atomically persisting each object cluster.

每个聚合都会形成保证事务一致性的边界。这意味着在一个单独的聚合中，在控制被提交给数据库的事务时，它的所有组成部分必须根据业务规则保持一致。这并非意味着你不应该把那些事务完成之后不一致的元素组合到聚合中。毕竟，一个聚合也要建立概念上完整的模型。但是，你应该首先关心事务一致性。围绕在 Aggregate Type1（聚合类型 1）和 Aggregate Type2（聚合类型 2）外面的边界分别代表着独立的事务边界，掌管着每个对象集的原子级持久化。

『

Broader Meaning of Transaction

To some degree, the use of transactions in your application is an implementation detail. For example, a typical use would have an Application Service [IDDD] controlling the atomic database transaction on behalf of the domain model. Under a different architecture, such as the Actor model [Reactive] where each Aggregate is implemented as an actor, transactions could be handled using Event Sourcing (see the next chapter) with a database that doesn’t support atomic transactions. Either way, what I mean by “transaction” is how modifications to an Aggregate are isolated and how business invariants—the rules to which the software must always adhere—are guaranteed to be consistent following each business operation. Whether this requirement is controlled by an atomic database transaction or by some other means, the Aggregate’s state, or its representation by means of Event Sourcing, must be safely and correctly transitioned and maintained at all times.

1『上面的信息目前无法消化吸收。（2020-08-21）』

某种程度上，在应用程序中使用事务是一个实现细节。例如，一种典型的实现会包括一个代表领域模型来控制原子级数据库事务的应用服务 [IDDD]。在其他不同的架构中，例如在 Actor 模型 [Reactive] 中，每个聚合都作为 Actor 实现，而事务可以使用事件溯源（Event Sourcing）（见第 6 章）来处理，即便数据库不支持原子级事务。不管怎样，我所说的「事务」就是如何隔离对聚合的修改，以及如何保证业务不变性（即软件必须始终遵守的规则）在每一次业务操作中都保持致。无论是通过原子级的数据库事务还是其他方法来控制需求，聚合的状态或者它通过事件溯源方法表现出的形式，必须始终安全和正确地进行转移和维护。

』

The reasons for the transactional boundary are business motivated, because it is the business that determines what a valid state of the cluster should be at any given time. In other words, if the Aggregate was not stored in a whole and valid state, the business operation that was performed would be considered incorrect according to business rules.

事务边界由商业动机决定，因为任何时候都是业务来决定对象集的有效状态应该是什么。换句话说，如果聚合没有保存在一个完整有效的状态中，那么根据业务规则所执行的业务操作会被认为是错误的。

To think about this in a different way, consider this. Although two Aggregates are represented here, only one of the two should be committed in a single transaction. That’s a general rule of Aggregate design: modify and commit only one Aggregate instance in one transaction. That’s why you see only the instance of Aggregate Type 1 within a transaction. We will look at the other rules of Aggregate design soon.

我们换个角度来思考。虽然这里呈现了两个聚合，但在单次事务中只能对其中之一完成提交。这是聚合设计的一条普遍规则：只能在一次事务中修改一个聚合实例并提交。这就是为什么你只能在本次事务中看到 Aggregate Type 1 的实例。很快我们将讨论其他的聚合设计规则。

Any other Aggregate will be modified and committed in a separate transaction. That’s why an Aggregate is said to be a transactional consistency boundary. So, you design your Aggregate compositions in a way that allows for transactional consistency and success. As seen here, an instance of Aggregate Type 2 is controlled under a separate transaction from the instance of Aggregate Type 1.

其他聚合将在另一次独立事务中修改并提交。这就是聚合被认为是事务一致性的边界的原因。所以，你可以按照能让事务保持一致性和提交成功的方式来设计你的聚合组成部分。就像这里看到的一样，Aggregate Type 2 实例和 Aggregate Type 1 实例分别在各自的事务中进行控制。

Since instances of these two Aggregates are designed to be modified in separate transactions, how do we get the instance of Aggregate Type 2 updated based on changes made to the instance of Aggregate Type 1, to which our domain model must react? That’s a good question; we will consider the answer to it a bit later in this chapter.

1『关键知识点，聚合 2 依赖于聚合 1，聚合 1 更新后如何确保聚合 2 跟着更新，领域模型需要实现这个。』

The main point to remember from this section is that business rules are the drivers for determining what must be whole, complete, and consistent at the end of a single transaction.

由于这两个聚合的实例被设计成在各自的事务中进行修改，我们如何根据 Aggregate Type 1 实例上发生的变化来更新 Aggregate Type 2  实例？领域模型必须对这些变化做出响应。我们将在本章稍后考虑这个问题的答案。本节中要记住的重点是，业务规则才是驱动力，最终決定在单次事务完成提交后，哪些对象必须是完整、完全和一致的驱动力。

### 5.2 Aggregate Rules of Thumb

Let’s next consider the four basic rules of Aggregate design:

1. Protect business invariants inside Aggregate boundaries.

2. Design small Aggregates.

3. Reference other Aggregates by identity only.

4. Update other Aggregates using eventual consistency.

1『聚合里的不变性，是有业务决定的；一致性边界就是聚合边界；标识符（类比于数据库表的主键）作为独一无二的外部引用。』

Of course, these rules are not necessarily strictly enforced by any “DDD police.” They are meant as sound guidance such that when thoughtfully applied, they will help you design Aggregates that work effectively. That being the case, we will now dig into each of these rules to see how they should be applied wherever possible.

接下来我们要思考的是聚合设计的四条基本规则：1）在聚合边界内保护业务规则不变性。2）聚合要设计得小巧。3）只能通过标识符引用其他聚合。4）使用最终一致性更新其他聚合。当然，这些规则不会由任何「DDD 警察」来强制执行。它们只是适当的指导，当经过深思熟虑被应用之后，它们将帮助你设计出能有效工作的聚合。既然是这样，现在我们要仔细钻研每一条规则，看看它们应该如何运用在合适的地方。

在作者的《实现领域驱动设计》第 10 章「聚合」中也有提到设计聚合时要遵循的四条原则，它们是：1）一致性边界之内建模真正的不变条件。2）设计小聚合。3）通过唯一标识引用其他聚合。4）在边界之外使用最终一致性。本书中提出的四条原则看起来似乎和它们一样，但描述却更加鲜明准确。在第 1 条规则中作者直接点明了不变性乃是由业务决定，在第 3 条规则中作者强调将标识符作为独一无二的外部引用，在第 1 条和第 4 条中作者更是指出了一致性边界就是聚合边界。这些原则是作者在完成《实现领域驱动设计》之后，经过不断实践再次修正和精练的成果。一一译注

Rule 1: Protect Business Invariants inside Aggregate Boundaries

Rule 1 means that the business should ultimately determine Aggregate compositions based on what must be consistent when a transaction is committed. In the example on page 81, Product is designed such that at the end of a transaction all composed ProductBacklogItem instances must be accounted for and consistent with the Product root. Also, Sprint is designed such that at the end of a transaction all composed CommittedBacklogItem instances must be accounted for and consistent with the Sprint root.

规则一的意思是聚合的组成部分应该由业务最终决定，而且要以那些在一次事务提交中必须保持一致的内容为基础。在上面的例子中，Product 被设计成在事务完成提交时，所有组成它的 ProductBacklogItem 都必须由它负责并和根 Product 保持一致。同样的，Sprint 被设计成在事务完成提交时，所有组成它的 CommittedBacklogItem 都必须由它负责并和根 Sprint 保持一致。

Rule 1 becomes clearer with another example. Here’s the BacklogItem Aggregate. There is a business rule that states, “When all Task instances have hoursRemaining of zero, the BacklogItem status must be set to DONE.” Thus, at the end of a transaction this very specific business invariant must be met. The business requires it.

规则一在另一个例子中更加明确。这是 BacklogItem 聚合的例子，其中包含着这样一条业务规则：「当所有 Task 实例的 hoursRemaining 都为零时，BacklogItem 的状态必须设置为 DONE。」因此，当事务完成提交时，这项特定的业务不变性规则必须要满足。这是业务要求的。

Rule 2: Design Small Aggregates

This rule highlights that the memory footprint and transactional scope of each Aggregate should be relatively small. In the preceding diagram the Aggregate that is represented is not small. Here, Product literally contains a potentially very large collection of BacklogItem instances, a large collection of Release instances, and a large collection of Sprint instances. Over time, these collections could grow to be quite large, with thousands of BacklogItem instances and probably hundreds of Release and Sprint instances. This design approach is generally a very poor choice.

这条规则强调，每个聚合的内存占用空间和事务包含范围应该相对较小。前面图例中展示的聚合并不算小。这里的 Product 确实可能包含大量的 BacklogItem 实例集合大量的 Release 实例集合，还有大量的 Sprint 实例集合。随着时间推移，这些集合可能会变得非常庞大，并且发展为数千个 BacklogItem 实例以及数百个 Release 和 Sprint 实例。这种设计思路通常是非常糟糕的选择。

However, if we break up the Product Aggregate to form four separate Aggregates, this is what we get: a small Product Aggregate, a small BacklogItem Aggregate, a small Release Aggregate, and a small Sprint Aggregate. These load quickly, take less memory, and are faster to garbage collect. Perhaps most importantly, these Aggregates will have transactional success much more frequently than the previous large-cluster Product Aggregate.

Following this rule has the added benefit that each Aggregate will be easier to work on, because each associated task can be managed by a single developer. This also means that the Aggregate will be easier to test.

Another thing to keep in mind when designing Aggregates is the Single Responsibility Principle (SRP). If your Aggregate is trying to do too many things, it is not following SRP, and this will likely be telling in its size. Ask yourself, for example, whether your Product is a very focused implementation of a Scrum product, or if it is also trying to be other things. What is the reason to change Product : to make it a better Scrum product, or to manage backlog items, releases, and sprints? You should change Product only in order to make it a better Scrum product.

可是，当我们把 Product 聚合拆分成四个独立的聚合之后，我们将会得到：一个小型 Product 聚合、一个小型 BacklogItem 聚合、一个小型 Release 聚合和一个小型 Sprint 聚合。这些模型加载快、内存占用少，并且垃圾回收也更迅速。而且也许更重要的是，这些聚合相比之前大块的 Product 聚合能获得更高的事务成功率。

遵守这条规则还可以带来另一个好处：每个聚合可以更容易地实现，因为每个关联到它的任务都可以由一个开发者掌控。这也意味着聚合更容易测试。在设计聚合时还需要记住的是单一职责原则（Single Responsibility Principle, SRP）。如果你的聚合想做的事情太多，就违反了 SRP，这由它的大小就可以判断出来。比如，问问自己，Product 是一个非常专注于 Scrum 产品的实现，还是它需要兼顾其他事情。

Product 发生变化的原因是什么：是为了让它变成更好的 Scrum 产品，还是为了管理待办事项、发布和冲刺？Product 的变化仅仅是为了实现更好的 Scrum 产品，这才应该是你的答案。

Rule 3: Reference Other Aggregates by Identity Only

Now that we’ve broken up the large-cluster Product into four smaller Aggregates, how should each reference the others where needed? Here we follow Rule 3, “Reference other Aggregates by identity only.” In this example we see that BacklogItem, Release, and Sprint all reference Product by holding a ProductId. This helps keep Aggregates small and prevents reaching out to modify multiple Aggregates in the same transaction.

This further helps keep the Aggregate design small and efficient, making for lower memory requirements and quicker loading from a persistence store. It also helps enforce the rule not to modify other Aggregate instances within the same transaction. With only identities of other Aggregates, there is no easy way to obtain a direct object reference to them.

Another benefit to using reference by identity only is that your Aggregates can be easily stored in just about any kind of persistence mechanism, such as relational database, document database, key-value store, and data grids/fabrics. This means that you have options to use a MySQL relational table, a JSON-based store such as PostgreSQL or MongoDB, GemFire/Geode, Coherence, and GigaSpaces.

现在，我们已经把大块的 Product 拆分成了四个更小的聚合，它们又如何在需要时引用其他的聚合呢？这里我们要遵守规则三：「只能通过标识符引用其他聚合」，在这个例子里，我们看到 BacklogItem、Release 和 Sprint 全都通过持有一个 ProductId 来引用 Product。这能帮助保持聚合不会变大，并防止在同一次事务中画蛇添足地修改多个聚合。

这能进一步帮助保持聚合设计得小巧又高效，从而降低内存需求，并提升持久化存储中加载的速度。它还有助于强化不要在同一次事务中修改其他聚合实例的規则。在只拥有其他聚合标识符的情况下，获取它们的直接对象引用没那么容易。

仅使用标识符引用还有一个好处，就是聚合可以使用任何类型的持久化机制轻松地存储，包括关系型数据库、文档数据库、键值型存储以及数据网格 / 结构。这意味着你可以选择 MYSQL 关系型数据库表、PostgreSQL 或者 MongoDB 这样基于 JSON 的存储，GemFire/Geode、Coherence、还有 Gigaspaces。

Apache Geode 是 Apache 顶级项目，由 Gemfire 开源而来，是集中间件、缓存、消息队列、事件处理引、NoSQL 数据库于一身的分布式内存数据处理平台它的介绍请参考《大中型企业的天网：Apache Geode》一文。——译注

Oracle Coherence 是 Oracle 的内存中数据网格解决方案。更多内容请参考 Coherence 文档。Gigaspaces XAP 是一种在虚拟化和分布式环境中可自动扩展的高端应用服务器，可为事务型和分析型应用提供一个高性能、可扩展、高可靠性的运行平台。更多内容请参考 Gigaspaces 官方网站。一一译注

Rule 4: Update Other Aggregates Using Eventual Consistency

Here a BacklogItem is committed to a Sprint. Both the BacklogItem and the Sprint must react to this. It is first the BacklogItem that knows it has been committed to a Sprint. This is managed in one transaction, when the state of the BacklogItem is modified to contain the SprintId of the Sprint to which it is committed. So, how do we ensure that the Sprint is also updated with the BacklogItemId of the newly committed BacklogItem?

例子里 BacklogItem 被提交到 Sprint 中。BacklogItem 和 Sprint 都要对此做出响应。首先 BacklogItem 知道它被提交到 Sprint 中，这是在一次事务中管理的，这次事务中 BacklogItem 的状态被修改，修改之后的状态会包含它被提交到的那个 Sprint 的 SprinteId。那么，我们如何确保 Sprint 的更新也包括了新提交的 BacklogItem 的 BacklogItemId 呢？

As part of the BacklogItem Aggregate’s transaction, it publishes a Domain Event named BacklogItemCommitted. The BacklogItem transaction completes and its state is persisted along with the BacklogItemCommitted Domain Event. When the BacklogItemCommitted makes its way to a local subscriber, a transaction is started and the state of the Sprint is modified to hold the BacklogItemId of the committed BacklogItem. The Sprint holds the BacklogItemId inside a new CommittedBacklogItem Entity.

作为 BacklogItem 聚合事务的一部分，名为 BacklogItemCommitted 的领域事件将被发布出来。BacklogItem 事务结束之后，它的状态和领域事件 BacklogItemCommitted 一起完成了持久化。当将 BacklogItemCommitted 传递到本地的订阅者那里时，一个新的事务会被触发，而 Sprint 的状态会被修改，并且持有提交给它的 BacklogItem 的 BacklogItemId。Sprint 会在一个新的 CommittedBacklogItem 实体中保存 BacklogItemId。

1『上面的过程，即使看了中文后还是无法消化。（2020-08-22）』

Recall now what you learned in Chapter 4, “Strategic Design with Context Mapping.” Domain Events are published by an Aggregate and subscribed to by an interested Bounded Context. The messaging mechanism delivers the Domain Events to interested parties by means of subscriptions. The interested Bounded Context can be the same one from which the Domain Event was published, or it could be different Bounded Contexts.

1『消息机制通过发布或订阅的方式，将领域事件传递给其他限界上下文。』

回忆一下你在第 4 章中学到的内容，领域事件由一个聚合发布并由感兴趣的限界上下文订阅。消息机制通过发布 / 订阅的方式把领域事件传递给感兴趣的限界上下文。感兴趣的限界上下文可能和发布领域事件的限界上下文是同一个，也有可能是另外一个。

It’s just that in the case of the BacklogItem Aggregate and the Sprint Aggregate, the publisher and subscriber are in the same Bounded Context. You don’t absolutely need to use a full-blown messaging middleware product for this case, but it’s easy to do so since you already use it for publishing to other Bounded Contexts.

就 BacklogItem 聚合和 Sprint 聚合这个例子而言，发布者和订阅者位于同一个限界上下文中。这种情况下，没有必要使用重量级的消息中间件，但如果已经使用了这样的中间件来发布消息给其他限界上下文，也可以利用它轻松地实现消息发布。

『

If Eventual Consistency Seems Scary

There is nothing incredibly difficult about using eventual consistency. Still, until you can gain some experience, you may be concerned about using it. If so, you should still partition your model into Aggregates according to business-defined transactional boundaries. However, there is nothing preventing you from committing modifications to two or more Aggregates in a single atomic database transaction. You might choose to use this approach in cases that you know will succeed but use eventual consistency for all others. This will allow you to get used to the techniques without taking too big an initial step. Just understand that this is not the primary way that Aggregates are meant to be used, and you may experience transactional failures as a result.

运用最终一致性并非特别地困难。尽管如此，如果你没有任何经验，可能会使用它有些疑虑。即使这样，你依然需要根据业务定义的事务边界来将模型划分成不同的聚合。然而，没有什么能够阻止你在一次原子数据库事务中提交对两个甚至更多聚合的修改。你可以在事务一定能提交成功的场景中使用这种方式而在其他场景中使用最终一致性方法。这可以让你逐步地适应最终一致性技术，而不会刚开始就把步子迈得太大。只是要理解这并非是使用聚合的主流方式，并且你最终可能会遇到事务失败。

』

### 5.3 Modeling Aggregates

There are a few hooks waiting for you as you work on your domain model, implementing your Aggregates. One big, nasty hook is the Anemic Domain Model [IDDD]. This is where you are using an object-oriented domain model, and all of your Aggregates have only public accessors (getters and setters) but no real business behavior. This tends to happen when there is a technical rather than business focus during modeling. Designing an Anemic Domain Model requires you to take on all the overhead of a domain model without realizing any of its benefits. Don’t take the bait!

2『上面算是解释了贫血模型的概念：除了公有访问器之外，没有包含任何真正意义上的业务行为。贫血做一张术语卡片。』

Also watch out for leaking business logic into the Application Services above your domain model. It can happen undetected, just like physical anemia. Delegating business logic from services to helper/utility classes isn’t going to work out well either. Service utilities always exhibit an identity crisis and can never keep their stories straight. Place your business logic in your domain model, or suffer bugs sponsored by an Anemic Domain Model.

1『贫血模型能带来哪些问题？回复：因为将业务的逻辑行为也放到服务层，最终导致服务越来越臃肿。（2020-08-22）』

当你在领域模型上展开工作并实现聚合时，有一些诱惑在等待着你。贫血领域模型（Anemic Domain Model）就是一个令人讨厌的巨大诱惑。如果你正在使用面向对象的领域模型，而这些模型除了公有访问器（Getter 和 Setter）之外没有包含任何真正的业务行为，那就是这种模型了。如果在建模过程中过于注重技术而忽略了业务就会造成这种结果。你需要承担领域模型中的所有的开销来设计贫血模型，但从中却获益甚少。所以不要上当！

同时也要注意别把领域模型中的业务逻辑放到上层的应用服务中。这可能在不经意中就发生了，就像生理贫血一样，也不容易检查出来。将服务中的业务逻辑委托给帮助 / 工具类也不会有什么改善。服务工具类往往会显现出身份认同危机，也永远无法保持业务逻辑的连续性。请把业务逻辑放在领域模型之中。不然就要忍受贫血领域模型带来的问题。

1 在使用一些 MVC 框架时我们常常会掉进贫血模型的陷阱。MVC 框架常常会使用 ORM 来将关系型数据库的查询和操作结果直接映射成对象（有的框架甚至就把这些对象称为实体，更增加了迷惑性），这些对象一般只包含 Getter 和 Setter。而真正的业务逻辑和这些所谓的「实体」脱离，被放在另外一些被称为服务的对象里。这些服务一般会负责调用 ORM 加载对象，执行操作改变对象状态，最后进行持久化存储。本来应该和这些实体有着内聚性的业务逻辑完全被置于独立的服务中，最终导致服务越来越臃肿的同时，把这些 ORM 映射的对象变成了贫血领域模型，实际上 ORM 只是一种资源库（Repository）的具体实现方式，它不属于领域模型的一部分，它映射出来的对象也不能简单地直接当作领域模型中的聚合和实体。这种错误的做法显然缺失了领域模型这个关键的层次。领域模型应该由持久化的对象转换而来，并承担被错放在服务中的那些业务逻辑。一一译注

1『上面的注释信息量蛮大的，需反复品味。』

1『请教戴强后，仓库层（资源库 Repository），是逻辑层和 Model 间的过渡层。』

『

What about Functional Programming?

When using functional programming, the rules change considerably. While an Anemic Domain Model is a bad idea when using object-oriented programming, it is somewhat the norm when applying functional programming. That’s because functional programming promotes the separation of data and behavior. Your data is designed as immutable data structures or record types, and your behavior is implemented as pure functions that operate on the immutable records of specific types. Rather than modifying the data that functions receive as arguments, the functions return new values. These new values may be the new state of an Aggregate or a Domain Event that represents a transition in an Aggregate ’s state.

1『贫血模型，用函数式编程范式时竟然是推荐的，长见识了。做一张任意卡片。』

I have largely addressed the object-oriented approach in this chapter because it is still the most widely used and well understood. Yet if you are employing a functional language and approach to DDD, be aware that some of this guidance is not applicable or is at least subject to overriding rules.

当使用函数式程范式时，规则会发生明显的变化：尽管贫血领域模型在使用面向对象编程范式时不是一个好主意，但在使用函数式程范式时却可能成为规范标准。这是因为函数式编程范式宣扬的是数据和行为的分离。你的数据要设计成不变的数据结构或者记录类型，而你的行为将被设计成操作特定类型不变记录的纯函数。函敏将返回新的值，而不是直接修改其作为参数接收的数据。这些新的值可能就是聚合的新状态，或者是表示一次聚合状态转换的领域事件。本章中我还是主要着眼于面向对象方法，因为这种方法仍然应用得最广泛也被理解得更透彻。但如果你正在使用函数式编程语言并准备引入 DDD，注意这指南中有些规则并不适用，或者至少要重新定义才可以遵从。

』

Next I’m going to show you some of the technical components you will need to implement a basic Aggregate design. I assume you are using Scala, C#, Java, or another object-oriented programming language. The following examples are in C# but are very understandable by Scala, F#, Java, Ruby, Python, and other programmers alike.

The first thing you must do is create a class for your Aggregate Root Entity. Here is a UML (Unified Modeling Language) representation of the Product Root Entity. Included is also the Product class in C#, which extends a base class named Entity. This base class just takes care of standard Entity kinds of things. See Implementing Domain-Driven Design [IDDD] for exhaustive discussions on both Entity and Aggregate design and implementation.

第一件必须做的事情是为聚合根实体创建一个类。上面图例中有 Product 根实体的 UML（统一建模语言）类图。还包括了用 C# 定义的 Product 类，这个类继承了名为 Entity 的基类。基类仅仅负责那些标准的和实体类型有关的事情。请参阅《实现领域驱动设计》中关于实体和聚合设计实现的详细讨论。

Every Aggregate Root Entity must have a globally unique identity. A Product in the Agile Project Management Context actually has two forms of globally unique identity. The TenantId scopes the Root Entity inside a given subscriber organization. (Every organization that subscribes to the offered services is known as a tenant and thus has a unique identity for that.) The second identity, which is also globally unique, is the ProductId. This second identity sets the Product apart from all others within the same tenant. Also included is the C# code that declares the two identities inside Product.

每一个聚合根实体都必须拥有全局唯一的标识符。敏捷项目管理上下文中的 Product 实际上拥有两种形式的全局唯一标识符。TenantId 将根实体的范围限制在订购了产品的指定组织之内。每个订购了服务的组织都被称为租户，因此要具有代表它的唯一标识符。第二个标识符也是全局唯一的，即 ProductId，它将 Product 与同一租户内的所有其他类型实例区分开来。图中还包括了 Product 中声明两个标识符的 C# 代码。

『

Use of Value Objects

Here, both TenantId and ProductId are modeled as immutable Value Objects.

』

Next you capture any intrinsic attributes or fields that are necessary for finding the Aggregate. In the case of Product, there are both description and name. Users can search one or both of these to find each Product. I also provide the C# code that declares these two intrinsic attributes.

接下来要记录在查找聚合时必须用到的内在属性或者字段。在 Product 这个场景里 description 和 name 就是这样的属性。用户可以通过搜索其中的一个属性或者搜索全部两个属性来找到每一个 Product。我还提供了声明这两个内在属性的 C# 代码。

Of course, you can add simple behavior such as read accessors (getters) for intrinsic attributes. In C# this would probably be done using public property getters. However, you may not want to expose setters as public. Without public setters, how do property/attribute values change? When using an object-oriented approach (C#, Scala, and Java), you change internal state using behavioral methods. If using a functional approach (F#, Scala, and Clojure), the functions will return new values that are different from the values passed as arguments.

当然，你可以给内在属性添加简单行为，比如 Getters。在 C 中使用公有属性 Getter 就能做到。然而，你可能不想将 Setter 暴露成公有的。如果没有公有的 Setter，怎样改变属性的值呢？当使用面向对象（C#、Scala 以及 Java）方法时，会使用行为方法来改变内部状态。如果使用函数式（F#、Scala 以及 Clojure）方法，函数将返回新的值，这些值和作为参数传入的值不同。

You should be on a mission to fight the Anemic Domain Model [IDDD]. If you expose public setter methods, it could quickly lead to anemia, because the logic for setting values on Product would be implemented outside the model. Think hard before doing this, and keep this warning in mind.

你应当承担对抗贫血顿域模型的责任。如果暴露了公有 setter 方法，用来设置 Product 的值的逻辑可能会在模型之外实现，这样很快会导致模型贫血。谨记这条警告三思而后行。

Finally, you add in any complex behavior. Here we’ve got four new methods: PlanBacklogItem(), PlannedProductBacklogItem(), ScheduleRelease(), and ScheduleSprint(). The C# code for each of these methods should be added to the class.

Remember, when using DDD, we are always modeling a Ubiquitous Language inside a Bounded Context. Thus, all parts of the Product Aggregate are modeled per the Ubiquitous Language. You don’t just make up these composed parts. Everything shows harmony between Domain Experts and developers of your close-knit team.

记住，运用 DDD 时，我们总是在一个限界上下文的范围内用通用语言进行建模。因此，Product 聚合的所有部分都是按照通用语言来建模的。这些组成部分都不是凭空想象出来的，这一切都体现出领域专家与开发人员的合作无间。

#### 5.3.1 Choose Your Abstractions Carefully

An effective software model is always based on a set of abstractions that address the business’s way of doing things. There is, however, the need to choose the appropriate level of abstraction for each concept being modeled.

If you follow the direction of your Ubiquitous Language, you will generally create the proper abstractions. It’s much easier to model the abstractions correctly because it is the Domain Experts who convey at least the genesis of your modeling language. Still, sometimes software developers who are overzealous for solving the wrong problems will try to force in abstractions that are, well, too abstract.

有效的软件模型总是建立在一套对业务行为方式的抽象之上。所以，为每个建模中的概念选择适当的抽象級别是非常有必要的。如果沿着通用语言的方向，你通常会建立合理的抽象。因为建模语言起码最初是由领域专家表达出来的，所以抽象建模会简单一些。尽管如此，有时候软件开发人员会过度热心于解决错误的问题，他们会建立过高的抽象级别。

For example, in the Agile Project Management Context we are dealing with Scrum. It makes sense to model Product, BacklogItem, Release, and Sprint concepts that we’ve been discussing. Even so, what if the software developers were less concerned about modeling the Ubiquitous Language of Scrum, and more interested in modeling a solution to all current and future Scrum concepts?

If this angle were pursued, the developers would probably come up with abstractions such as ScrumElement and ScrumElementContainer. A ScrumElement could fill the current need for Product and Backlog-Item, and ScrumElementContainer could represent the obviously more explicit concepts of Release and Sprint. The ScrumElement would have a typeName property, and it would be set to "Product" or "BacklogItem" in appropriate cases. We could design the same kind of typeName property for ScrumElementContainer and allow the values "Release" or "Sprint" to be set on it.

以我们正在处理的 Scrum 的敏捷项目管理上下文为例。对已经讨论过的 Product、BacklogItem、Release 以及 Sprint 这些概念所进行的建模当然合乎情理。即便如此，如果软件开发人员关心的不是在 Scrum 的通用语言中建模，而是对所有现在和未来的 Scrum 概念的建模更有兴趣呢？

如果沿着这个方向继续前进，开发人员很可能提出 ScrumElement 和 ScrumElementContainer 这样的抽象概念。 ScrumElement 可以满足当前对 Product 和 BacklogItem 的要求，而 ScrumElementContainer 也可以表示 Release 和 Sprint 概念，这些当前的概念显然更具象。ScrumElement 可以包含一个 typeName 属性，它可以在不同的场景中被适当地设置成「Product」或者「BacklogItem」。我们也可以为 ScrumElementContainer 设计类似的 typeName 属性，并允许将它的值设置为「Release」或者「Sprint」。

Do you see the problems with this approach? There are more than a few, but consider the following:

1. The language of the software model does not match the mental model of the Domain Experts.

2. The level of abstraction is too high, and you will get into deep trouble when you start to model the details of each of the individual types.

3. This will lead to creating special cases in each of the classes and likely result in a complex class hierarchy with general approaches to explicit problems.

4. You will have much more code than you need, because you are trying to solve an unsolvable problem that should not matter in the first place.

5. Often the language of the wrong abstractions will find its way even into the user interface, which will cause confusion for users.

6. You will waste considerable time and money.

7. You will never be able to address all future needs up front, which means if new Scrum concepts are ever added in the future, your existing model will prove to be a failure in foreseeing those needs.

你发现该方法的问题了吗？这里面的问题不少，但请主要思考以下几点：1）软件模型的语言无法匹配领域专家的心智模型。2）抽象级别过高，当你开始对每个独立概念类型进行建模时会陷入大麻烦。3）这会导致每个类中都有特殊情况产生，并且可能造成使用通用方法去解决具体问题的复杂的类层次结构。4）因为试图要先去解决无关紧要的无解问题，你将会编写比实际需要多得多的代码。错误抽象的语言会殃及用户界面，并且将给用户带来困扰。会浪费大量时间和金钱。5）永远无法预先满足未来所有的需求，这意味着未来如果增加新的 Scrum 概念，现有模型对这些需求的预判会被证明是失败的。

Following such a path may seem strange to some, but this incorrect level of abstractions is used often in technically inspired implementations.

Don’t get taken in by this alluring, highly abstract implementation trap. Model the Ubiquitous Language explicitly according to the mental model of the Domain Experts that is refined by your team. By modeling what the business needs today, you will save a considerable amount of time, budget, code, and embarrassment. More still, you will do the business a great service by modeling an accurate and useful Bounded Context that reflects an effective design.

这样的思路看起来有些奇怪，但由技术启发的实现中常常出现这种不正确的抽象级别。不要被这个诱人的、实现高度抽象的陷阱所吸引，而要根据团队精练过的领域专家的心智模型，脚踏实地地对通用语言进行建模。通过对当下的业务需求进行建模，你将省去大量的时间、预算和代码，并且避免了不必要的麻烦。更重要的是，你将通过建立能体现有效设计的准确且实用的限界上下文模型来为业务提供有效的服务。

#### 5.3.2 Right-Sizing Aggregates

You may be wondering how you can determine the boundaries of Aggregates and prevent the design of large clusters, while still maintaining consistency boundaries that will protect true business invariants. Here I have provided a worthy design approach. If you have already created large-cluster Aggregates, you can use this approach to refactor into smaller ones, but I am not going to start from that perspective.

你可能在思考如何确定聚合的边界并避免出现臃肿的设计，同时还要维持并保证真实业务不变性规则的一致性边界。在这里我提供了一个有价值的设计方法。如果你已经创建出了臃肿的聚合，你可以使用这种方法将它重构得更小巧，但我会从另一个角度来介绍这个方法。

Consider these design steps that will help you reach consistency boundary goals:

1. Put your first focus on the second rule of Aggregate design, “Design small Aggregates. ” Start by creating every Aggregate with just one Entity, which will serve as the Aggregate Root. Don’t even dare to place two Entities in a single boundary. That opportunity will come soon enough. Populate each of the Entities with the fields/attributes/properties that you believe are most closely associated with the single Root Entity. One big hint here is to define every field/attribute/property that is required to identify and find the Aggregate, as well as any additional intrinsic fields/attributes/properties that are required for the Aggregate to be constructed and left in a valid initial state.

2. Now place your focus on the first rule of Aggregate design, “Protect business invariants inside Aggregate boundaries.” You have already asserted by the previous step that at a minimum all the intrinsic fields/attributes must be up-to-date when the single-Entity Aggregate is persisted. But now you need to look at each of your Aggregates one at a time. As you do so for Aggregate A1, ask the Domain Experts if any other Aggregates you have defined must be updated in reaction to changes made to Aggregate A1. Make a list of each of the Aggregates and their consistency rules, which will indicate the time frames for all reaction-based updates. In other words, “Aggregate A1” would be the heading of one list, and other Aggregate types would be listed under A1 if they will be updated in reaction to A1 updates.

3. Now ask the Domain Experts how much time may elapse until each of the reaction-based updates may take place. This will lead to two kinds of specifications: (a) immediately, and (b) within N seconds/minutes/hours/days. One possible way to find the correct business threshold is by presenting an exaggerated time frame (such as weeks or months) that is obviously unacceptable. This will likely cause business experts to respond with an acceptable time frame.

4. For each of the immediate time frames (3a), you should strongly consider composing those two Entities within the same Aggregate boundary. That means, for example, that Aggregate A1 and Aggregate A2 will actually be composed into a new Aggregate A[1,2]. Now Aggregates A1 and A2 as they were previously defined will no longer exist. There is only Aggregate A[1,2].

5. For each of the reacting Aggregates that can be updated following a given elapsed time (3b), you will update these using the fourth rule of Aggregate design, “Update other Aggregates using eventual consistency.”

思考下面这些可以帮助你达到一致性边界目标的设计步骤。

1、将重点先放在聚合设计的规则二上：「聚合要设计得小巧」。每个聚合一开始创建时只允许包含一个实体，并且它将作为聚合根。千万不要尝试在边界内放入两个实体。这样的机会很快就会出现。用你认为和单个聚合根关联最紧密的字段 / 属性填充每个实体。这里有一个重要的技巧是定义出每个用来识别和查找聚合的字段 / 属性，以及任何其他用于构造聚合并使之处于有效初始状态的内在属性。

2、现在将重点放在聚合设计的规则一上：「聚合边界内保护业务不变性规则」。在上ー步中，已经声明了至少在单个实体持久化时所有内在字段 / 属性必须是最新的。但是现在需要一个一个地检查每个聚合。在检查聚合 A1 时，问问领域专家需不需要更新其他己定义的聚合，来响应聚合 A1 发生的改变。为每个聚合和它的一致性规则制作一个清单，还要记录所有这些基于响应的更新的时间范围。换句话说，「聚合 A1」作为清单的标题，如果其他的聚合类型也需要更新来响应 A1 的变化，就把它们罗列在 A1 之下。

3、现在询问领域专家，每个基于响应的更新可以等待多长时间。答案会是两种：a）即时发生；b）在 n 秒/分/小时/天之内发生。一种可行的寻找正确的业务阈值的方法是，先抛出一个夸张到显然无法接受的时间范围（比如几周或几个月）。业务专家很可能会据此提出一个可接受的时间范围作为回应。

4、对每一个即时发生的时间范围（3a），应该坚定地考虑把这两个实体合并到同一个聚合的边界之内。例如，聚合 A1 和聚合 A2 实际上将合并成一个新的聚合 A[1, 2]。现在之前定义的聚合 A1 和聚合 A2 将不复存在。只剩下唯一的聚合 A[1, 2]。

5、对于每一个在给定等待时间（3b）内更新的响应聚合，将使用聚合设计的规则四来更新它们：「利用最终一致性更新其他聚合」。

In this figure our focus is on modeling Aggregate A1. Note from the A1 list of consistency rules that A2 has an immediate time frame, while C14 has an eventual (30 seconds) time frame. As a result, A1 and A2 are modeled into a single Aggregate A[1,2]. During runtime Aggregate A[1,2] publishes a Domain Event that causes Aggregate C14 to be updated eventually.

Be careful that the business doesn’t insist that every Aggregate fall within the 3a specification (immediate consistency). It can be an especially strong tendency when many in the design session are influenced by database design and data modeling. Those stakeholders will have a very transaction-centered point of view. However, it is very unlikely that the business really needs immediate consistency in every case. To change this thinking you will probably have to spend time proving how transactions will fail due to concurrent updates by multiple users across different composed parts of the (now) large-cluster Aggregates. Furthermore, you can point out how much memory overhead there is with such large-cluster designs. Obviously these kinds of problems are what we are trying to avoid in the first place.

这张图中的焦点是聚合 A1 的建模。注意，在 A1 的一致性规则清单中，A2 的时间范围是即时发生，而 C14 的时间范围是最终发生（30 秒）。因此，A1 和 A2 被建模成单个聚合 A[1, 2]。在运行时聚合 A[1, 2] 会发布领域事件，将导致聚合 C14 最终得到更新。

请注意，业务并不会强求每个聚合都符合 3a 标准（即时一致性）。当大部分设计活动受到数据库设计和数据建模的影响时，即时一致性可能成为一种非常强烈的趋势。这些干系人有着强烈的以事务为中心的观点。然而，业务很可能并不是在任何情况下都真的需要即时一致性。要改变这种想法，可能需要花时间证明，事务是如何因为多个用户在（现在还是）臃肿聚合的不同组成部分中并发更新而失败。此外，你可以指出这种臃肿设计会带来多少内存开销。显然，这些问题才是我们要优先避免的。

This exercise indicates that eventual consistency is business driven, not technically driven. Of course, you will have to find a way to technically cause eventual updates between multiple Aggregates, as discussed in the previous chapter on Context Mapping. Even so, it is only the business that can determine the acceptable time frame for updates to occur between various Entities. Some are immediate, or transactional, which means they must be managed by the same Aggregate. Some are eventual, which means they may be managed through Domain Events and messaging, for example. Considering what the business would have to do if it ran its operations only by means of paper systems can provide some worthwhile insights into how various domain-driven operations should work within a software model of the business operations.

这个练习表明最终一致性是由业务驱动的，而不是由技术驱动的。当然，你必须找到一种方法在多个聚合之间完成技术上的最终更新，就像第 4 章中关于上下文映射的讨论一样。即便如此，只有业务才能决定发生在各种实体之间的更新的可接受时间范围。有些时间范围是即时或事务性的，这意味着它们必须由同一个聚合管理。而有些时间范围是最终一致的，这意味着它们可以通过领域事件和消息机制进行管理。假定业务只能通过纸制系统才可以完成操作，这样能激发一些有价值的思考，思考各种领域驱动的操作如何在业务操作的软件模型中工作。

#### 5.3.3 Testable Units

You should also design your Aggregates to be a sound encapsulation for unit testing. Complex Aggregates are hard to test. Following the previous design guidance will help you model testable Aggregates.

Unit testing is different from validating business specifications (acceptance tests) as discussed in Chapter 2, “Strategic Design with Bounded Contexts and the Ubiquitous Language,” and Chapter 7, “Acceleration and Management Tools.” Development of the unit tests will follow the creation of scenario specification acceptance tests. What we are concerned with here is testing that the Aggregate correctly does what it is supposed to do. You want to push on all the operations to ensure the correctness, quality, and stability of your Aggregates. You can use a unit testing framework for this, and there is much literature available on how to effectively unit test. These unit tests will be directly associated with your Bounded Context and kept with its source code repository.

还应该将聚合封装设计得合理，让它们更适合单元测试。复杂的聚合将难以测试。遵循之前的规则指南将帮助你建立可测试的聚合模型。单元测试和第 2 章以及第 7 章中讨论的业务需求的验证（验收测试）不同。单元测试的开发紧跟在场景需求验收测试创建之后。这里我们关心的是，测试聚合是否正确地做到了它应该做的事情。你希望推进所有活动来确保聚合的正确性、高质量和稳定性。为此可以使用单元测试框架，还可以参考很多关于如何有效进行单元测试的文献。这些单元测试和限界上下文息息相关，并且保存在限界上下文的源代码仓库之中。

## 0601. Tactical Design with Domain Events

In this chapter you learned: 1) How to create and name your Domain Events. 2) The importance of defining and implementing a standard Domain Event interface. 3) That naming your Domain Events well is especially important. 4) How to define the properties of your Domain Events. 5) That some Domain Events may be caused by commands, while others may happen due to the detection of some other changing state, such as a date or time. 6) How to save your Domain Events to an event store. 7) How to publish your Domain Events after they are saved. 8) About Event Sourcing and how your Domain Events can be stored and used to represent the state of your Aggregates.

For a thorough treatment of Domain Events and integration, see Chapters 8 and 13 of Implementing Domain-Driven Design [IDDD].

1『这一章书讲如何对领域事件建模的，可以配合 IDDD 的第 8 章和第 13 章来看。』

总结：1）如何创建和命名领域事件。2）定义和实现标准领域事件接口的重要性。3）合理地命名领域事件非常重要。4）如何定义领域事件的属性。5）一些领域事件可能是由命令引起的，而另一些事件可能由其他变化的状态引起，比如日期和时间。6）如何把领域事件保存到事件存储中。7）在领域事件保存后如何发布它们。8）事件溯源的相关内容，以及领域事件如何存储和使用才能表示聚合的状态。

You’ve already seen a bit in previous chapters about how Domain Events are used. A Domain Event is a record of some business-significant occurrence in a Bounded Context. By now you know that Domain Events are a very important tool for strategic design. Still, often during tactical design Domain Events are conceptualized and become a part of your Core Domain.

在前面的章节中已经学到了一些领域事件（Domain Event）的用法。领域事件是一条记录，记录着在限界上下文（Bounded Context）中发生的对业务产生重要影响的事情。目前为止，我们已经了解到领域事件是非常重要的战略设计工具。然而，领域事件往往会在战术设计的过程中被概念化并演变成核心域的组成部分。

To see the full power that results from using Domain Events, consider the concept of causal consistency. A business domain provides causal consistency if its operations that are causally related—one operation causes another—are seen by every dependent node of a distributed system in the same order [Causal]. This means that causally related operations must occur in a specific order, and thus one thing cannot happen unless another thing happens before it. Perhaps this means that one Aggregate cannot be created or modified until it is clear that a specific operation occurred to another Aggregate :

1. Sue posts a message saying, “I lost my wallet!”.

2. Gary says in reply, “That’s terrible!”.

3. Sue posts a message saying, “Don’t worry, I found my wallet!”.

4. Gary replies, “That’s great!”.

我们通过因果一致性的概念来展现运用领域事件所产生的全部威力。如果业务领域中存在因果关系的操作一一即一个操作会由另一个操作引起一一在分布式系统的每个独立节点中它们被观察到的发生顺序都是一样的，这就是业务领域提供的因果一致性 [Casual]。这意味着存在因果关系的操作必须按照特定的顺序发生，而且，如果前一个操作没有发生，那么后面的操作就不能发生。也许这就说明了，只有在一个聚合上明确地发生了特定操作的情况下，另一个聚合才能被创建或者修改：

If these messages were replicated on distributed nodes, but not in a causal order, it could appear that Gary said, “That’s great!” to the message “I lost my wallet!” The message “That’s great!” is not directly or causally related to “I lost my wallet!” and that’s definitely not what Gary wants Sue or anyone else to read. Thus, if causality is not achieved in the proper way, the overall domain would be wrong or at least misleading. This sort of causal, linearized system architecture can be readily achieved through the creation and publication of correctly ordered Domain Events.

如果这些消息被复制到多个分布式节点，却没有按照因果顺序排列，就可能会变成 Gray 对消息「我的钱包丢了！」回复「那就好！」。「那就好！」这条消息和「我的钱包丢了！」之间不存在直接关系或因果关系，这也不是 Gary 想让 Sue 或者其他人获得的消息。因此，如果因果关系没有以正确的方式实现，整个领域就会完全错误，或者至少会产生误会。这种因果的线性系统架构可以通过创建并发布顺序正确的领域事件来轻松地实现。

From tactical design efforts Domain Events become a reality in your domain model and can as a result be published and consumed in your own Bounded Context and by others. It’s a very powerful way to inform interested listeners of important occurrences that have taken place. Now you will learn how to model Domain Events and use them in your Bounded Contexts.

由于战术设计的不懈努力，领域事件在领域模型中落实，并且可以在自己的或者其他限界上下文中被发布和消费。这是一种非常有效的方式，它将已发生的重要事件告知感兴趣的监听器。接下来将学习如何建立领域事件模型以及如何在限界上下文中使用它们。

### 6.1 Designing, Implementing, and Using Domain Events

The following guides you through the steps needed to effectively design and implement Domain Events in your Bounded Context. Following this, you will also see examples of how Domain Events are used.

This C# code might be considered the minimum interface that every Domain Event should support. You generally want to convey the date and time when your Domain Event occurred, so that’s provided by the OccurredOn property. This detail is not an absolute necessity, but it is often useful. So your Domain Event types would likely implement this interface.

You must show care in how you name your Domain Event types. The words you use should reflect your model’s Ubiquitous Language. These words will form a bridge between the happenings in your model and the outside world. It’s vital that you communicate your happenings well.

这段 C# 代码可以被认为是每个领域事件都必须支持的最小接口。一般都要表达领域事件发生的日期和时间，所以这些信息由属性 OccurredOn 来提供。这个细节信息不是绝对必要的，但通常很实用。因此领域事件类型很有可能会实现这个接口。必须重视领域事件类型的命名。使用的词语应该体现出模型的通用语言（Ubiquitous Language）。这些词语将形成连接模型中所发生的事情和外部世界的桥梁。就所发生的事情进行充分的沟通至关重要。

Your Domain Event type names should be a statement of a past occurrence, that is, a verb in the past tense. Here are some examples from the Agile Project Management Context : ProductCreated, for instance, states that a Scrum product was created at some past time. Other Domain Events are ReleaseScheduled, SprintScheduled, BacklogItemPlanned, and BacklogItemCommitted. Each of the names clearly and concisely states what happened in your Core Domain.

1『大赞，领域事件命名很有讲究的，首先命令要能反映出这个领域事件是做什么的，要能反映出这个模型的通用语言（最好领域专家来起名）；其次，命令要以过去式来命令，比如 ProductCreated 这种。』

1-2『对领域事件建模的整个思路。1）先命名好领域事件（类名）。2）通过找领域服务来倒推出领域事件模型中所包含的属性（类里面的属性）。领域事件是一个结果，通过这个结果去追溯是什么动作导致的这个结果，这个「动作」即领域服务，接着去看领域服务模型里的属性，将这些属性照搬到领域事件中去。作者的例子里，领域事件是橙色的卡片，领域服务是蓝色卡片，聚合是黄色卡片。做一张任意卡片。』——已完成

领域事件类型的名称应该是对过去发生的事情的陈述，即动词的过去式。这里有一些敏捷项目管理上下文中的例子：例如 ProductCreated 表明在过去的某个时间一个 Scrum Product 被创建了。其他领域事件有 ReleaseScheduled、SprintScheduled、BacklogItemPlanned 和 BacklogItemCommitted。每个名称都清晰简洁地呈现了在核心域（Core Domain 中发生的事情）。

It’s a combination of the Domain Event’s name and its properties that fully conveys the record of what happened in the domain model. But what properties should a Domain Event hold?

Ask yourself, “What is the application stimulus that causes the Domain Event to be published?” In the case of ProductCreated there is a command that causes it (a command is just the object form of a method/action request). The command is named CreateProduct. So you can say that ProductCreated is the result of a CreateProduct command.

领域事件的名称和属性组合在一起才能完整记录领域模型中发生的事情。但领域事件应该包含哪些属性呢？问问你自己：「是什么应用的刺激导致领域事件被发布出来？」在 ProductCreated 的例子中，它是由一个命令引起的（命令就是一个方法 / 动作请求的对象形态)。这个命令被命名为 CreateProduct。所以可以说 ProductCreated 就是命令 CreateProduct 的结果。

The CreateProduct command has a number of properties: 1) the tenantId that identifies the subscribing tenant, 2) the productId that identifies the unique Product being created, the 3) Product name, and 4) the Product description. Each of these properties is essential to creating a Product.

Therefore, the ProductCreated Domain Event should hold all the properties that were provided with the command that caused it to be created: 1) tenantId, 2) productId, 3) name, and 4) description. This will fully and accurately inform all subscribers what happened in the model; that is, a Product was created, it was for the tenant identified with the tenantId, the Product was uniquely identified with productId, and the Product had the name and description assigned to it.

因此，领域事件 ProductCreated 必须包含导致 Product 被创建出来的那条命令提供的所有属性：1) tenantId, 2) productId, 3) name, and 4) description，它会完整精准地将模型中发生的事情通知给所有订阅者：即，一个 Product 被创建了，它是为 tenantId 代表的租户创建的，Product 通过 productId 被唯一标识，而且 name 和 description 被赋值给了 Product。

These five examples give you a good idea of the properties that should be included with the various Domain Events published by the Agile Project Management Context. For instance, when a BacklogItem is committed to a Sprint, the BacklogItemCommitted Domain Event is instantiated and published. This Domain Event contains the tenantId, the backlogItemId of the BacklogItem that was committed, and the sprintId of the Sprint to which it was committed.

As described in Chapter 4, “Strategic Design with Context Mapping,” there are times when a Domain Event can be enriched with additional data. This can be especially helpful to consumers that don’t want to query back on your Bounded Context to obtain additional data that they need. Even so, you must be careful not to fill up a Domain Event with so much data that it loses its meaning. For example, consider the problem with BacklogItemCommitted holding the entire state of the BacklogItem. According to this Domain Event, what actually happened? All the extra data may make it unclear, unless you require the consumer to have a deep understanding of your BacklogItem element. Also, consider using BacklogItemUpdated with the full state of the BacklogItem, as opposed to providing BacklogItemCommitted. What happened to the BacklogItem is very unclear, because the consumer would have to compare the latest BacklogItemUpdated to the previous BacklogItemUpdated in order to understand what actually occurred to the BacklogItem.

这五个例子很好地展示了，由敏捷项目管理上下文发布的各种不同的领域事件，应该包含哪些属性。例如，当一个 BacklogItem 被提交到 Sprint 中，领域事件 BacklogItemCommitted 被初始化并发布出来。这个领域事件包含了 tenantId，代表被提交的 BacklogItem 的 backlogItemId，以及代表它被提交的 Sprint 的 sprintId。

正如第 4 章中所述，有时可以使用额外的属性来增强领域事件。某些消费者不想在限界上下文中通过查询来获取他们需要的额外数据，对于这些消费者来说，用额外属性增强过的事件会很方便。即便如此，也必须特别小心，以避免把太多的数据塞给领域事件，从而导致它失去了本来的意义。例如，思考一下包含完整 BacklogItem 状态的 BacklogItemCommitted 所带来的问题。按照这个领域事件的定义，实际发生了什么？所有额外的数据都可能对此含义产生误导，除非消费者对 BacklogItem 元素有着深刻的理解。此外，再想一想使用包含 BacklogItem 完整状态的 BacklogItemUpdated 代替 BacklogItemCommitted。这个名字对 BacklogItem 上发生的事情的描述是模糊的，因为消费者不得不对比最新的 BacklogItemUpdated 和前一个 BacklogItemUpdated 才能理解究竟发生了什么。

To make the proper use of Domain Events clearer, let’s walk through one scenario. The product owner commits a BacklogItem to a Sprint. The command itself causes the BacklogItem and the Sprint to be loaded. Then the command is executed on the BacklogItem Aggregate. This causes the state of the BacklogItem to be modified, and then the BacklogItemCommitted Domain Event is published as an outcome.

为了令我们更清楚地理解正确使用领域事件的方法，看看这样一个场景。产品负责人向 Sprint 提交了一个 BacklogItem。这个命令自己会加载 BacklogItem 和 Sprint，然后会在聚合 BacklogItem 上执行。这导致 BacklogItem 的状态被修改，随后领域事件 BacklogItemCommitted 被作为结果发布出来。

It’s important that the modified Aggregate and the Domain Event be saved together in the same transaction. If you are using an object-relational mapping tool, you would save the Aggregate to one table and the Domain Event to an event store table, and then commit the transaction. If you are using Event Sourcing, the state of the Aggregate is fully represented by the Domain Events themselves. I discuss Event Sourcing in the next section of this chapter. Either way, persisting the Domain Event in the event store preserves its causal ordering relative to what has happened across the domain model.

1『修改后的聚合和领域事件必须同时保存。做一张任意卡片。』——已完成

在同一次事务中同时保存修改过的聚合和领域事件非常关键。如果你使用的是对象关系映射工具，可以把聚合保存在一张表里，并且把领域事件保存在另一张事件存储表中然后提交事务。如果你使用的是事件溯源（Event Sourcing），聚合的状态可以完全由领域事件自己表达。我将在本章下一节讨论事件溯源。无论使用哪种方式，在事件存储中对领域事件进行持久化都会保留它们之间的因果顺序，这些顺序和在领域模型中发生的事件相关。

Once your Domain Event is saved to the event store, it can be published to any interested parties. This might be within your own Bounded Context and to external Bounded Contexts. This is your way of telling the world that something noteworthy has occurred in your Core Domain.

Note that just saving the Domain Event in its causal order doesn’t guarantee that it will arrive at other distributed nodes in the same order. Thus, it is also the responsibility of the consuming Bounded Context to recognize proper causality. It might be the Domain Event type itself that can indicate causality, or it may be metadata associated with the Domain Event, such as a sequence or causal identifier. The sequence or causal identifier would indicate what caused this Domain Event, and if the cause was not yet seen, the consumer must wait to apply the newly arrived event until its cause arrives. In some cases it is possible to ignore latent Domain Events that have already been superseded by the actions associated with a later one; in this case causality has a dismissible impact.

一旦领域事件被保存到了事件存储中，它就可以发布给任何对它感兴趣的订阅方。这可能发生在自己的限界上下文中也可能发生在外部的限界上下文中。这是你向世界宣告的方式，宣告在你的核心域中发生了一些值得关注的事件事情。

注意，只是按照因果顺序保存领域事件并不能保证这些事件会以同样的顺序到达其他的分布式节点。因此，识别出正确因果关系的重任就落到了消费事件的限界上下文肩上。因果关系可以由领域事件类型本身表明，或者由和领域事件关联在一起的元数据表示，比如一个序列标识符或者因果标识符。序列标识符或者因果标识符可以表示导致领域事件发生的原因事件，如果原因事件尚未出现，消费者必须等它到达后才能处理先前到达的（结果）事件。某些情况下，可以忽略潜在的领域事件，这些事件已经被后续事件的关联动作取代，这种情况下因果关系具有可消除的影响。

One more point about what can cause a Domain Event is noteworthy. Although often it is a user-based command emitted by the user interface that causes an event to occur, sometimes Domain Events can be caused by a different source. This might be from a timer that expires, such as at the end of the business day or the end of a week, month, or year. In cases like this it won’t be a command that causes the event, because the ending of some time period is a matter of fact. You can’t reject the fact that some time frame has expired, and if the business cares about this fact, the time expiration is modeled as a Domain Event, and not as a command.

What is more, such an expiring time frame will generally have a descriptive name that will become part of the Ubiquitous Language. For example, “Fiscal Year Ended” may be an important event that your business needs to react to. Furthermore, 4:00 p.m. (16:00) on Wall Street is known as “Markets Closed” and not just as 4:00 p.m. Therefore, you have a name for that particular time-based Domain Event.

A command is different from a Domain Event in that a command can be rejected as inappropriate in some cases, such as due to supply and availability of some resources (product, funds, etc.), or another kind of business-level validation. So, a command may be rejected, but a Domain Event is a matter of history and cannot logically be denied. Even so, in response to a time-based Domain Event it could be that the application will need to generate one or more commands in order to ask the application to carry out some set of actions.

关于导致领域事件的原因还有一点值得注意。尽管事件通常都是用户在用户界面发起的命令导致的，但有时领域事件可能由其他原因引起。这些原因可能是快要到期的计时器比如营业日结束或者一周、一月、一年的结尾。这种情况下，导致事件发生的原因不是命令，因为某个时间段的结束是一个事实。你不能抗拒时间范围到期的事实，而且如果业务关注了这个事实，时间到期会被建模成领域事件而不是命令。

而且，这样一个会到期的时间范围通常会有一个描述性的名称，这个名称会成为通用语言的一部分。例如，「财年截止」（Fiscal Year End）可能是业务需要响应的一个重要事件。又比如，华尔街的下午 4 点（16 点整）并不是简单的下午 4 点，而被认为是「收盘」。因此，基于时间的特殊领域事件应该拥有合适的名称。

命令和领域事件的不同在于，某些情况下不恰当的命令可以被拒绝，比如某些资源（产品、资金等）的供应和可用性或者其他业务层面的验证导致的情况。所以，命令可能被拒绝，而领域事件是历史事实，必须无条件地接受。尽管如此，为了响应基于时间的领域事件，应用可能需要生成一条或多条命令，来执行一些动作。

### 6.2 Event Sourcing

Event Sourcing can be described as persisting all Domain Events that have occurred for an Aggregate instance as a record of what changed about that Aggregate instance. Rather than persisting the Aggregate state as a whole, you store all the individual Domain Events that have happened to it. Let’s step through how this is supported.

All of the Domain Events that have occurred for one Aggregate instance, ordered as they originally occurred, make up its event stream. The event stream begins with the first Domain Event that ever occurred for the Aggregate instance and continues until the last Domain Event that occurred. As new Domain Events occur for a given Aggregate instance, they are appended to the end of its event stream. Reapplying the event stream to the Aggregate allows its state to be reconstituted from persistence back into memory. In other words, when using Event Sourcing, an Aggregate that was removed from memory for any reason is reconstituted entirely from its event stream.

In the preceding diagram, the first Domain Event to occur was BacklogItemPlanned; the next was BacklogItemStoryDefined; and the event that just occurred is BacklogItemCommitted. The full event stream is currently composed of those three events, and they follow the order described and seen in the diagram.

Each of the Domain Events that occurs for a given Aggregate instance is caused by a command, just as described previously. In the preceding diagram, it is the CommitBacklogItemToSprint command that has just been handled, and this has caused the BacklogItemCommitted Domain Event to occur.

事件溯源（Event Sourcing）可以描述为，对所有发生在聚合实例上的领域事件进行持久化，把它们当作对聚合实例变化的记录。你存储的是发生在聚合上的所有独立事件，而不是把聚合状态作为一个整体进行持久化。一个聚合实例上发生的所有领域事件，按照它们原本发生的顺序，组成了该实例的事件流。事件流从聚合实例上发生的第一个领域事件开始，到最近发生的领域事件结束。当指定的聚合实例上发生了新的领域事件时，这些事件被追加到该实例事件流的末尾。在聚合上重新应用事件流，可以让它的状态从持久化存储中被重建到内存中。换句话说，使用事件溯源时，出于任何原因从内存中移除的聚合将依据它的事件流完整地进行重建。

在上图中，最先发生的领域事件是 BacklogItemPlanned，接下来是 BacklogItemStoryDefined，而最近刚刚发生的是 BacklogItemCommitted。完整的事件流现在由这三个事件组成，它们按照图中呈现的顺序排列。和之前描述的一样，每个发生在指定聚合实例上的领域事件都是由命令引起的。在上图中，刚刚被处理的命令是 CommitBacklogItemToSprint，并且由此导致事件 BacklogItemCommitted 发生。

The event store is just a sequential storage collection or table where all Domain Events are appended. Because the event store is append-only, it makes the storage mechanism extremely fast, so you can plan on a Core Domain that uses Event Sourcing to have very high throughput, low latency, and be capable of high scalability.

事件存储就是一个顺序存储集合或者一张表，所有领域事件都被追加到其中。由于事件存储只允许追加记录，从而使得存储进程非常快，所以可以规划在核心域上使用事件溯源，来达到高吞吐量、低延迟和高伸缩性。

『

Performance Conscious

If one of your primary concerns is performance, you will appreciate knowing about caching and snapshots. First of all, your highest-performing Aggregates will be those that are cached in memory, where there is no need to reconstitute them from storage each time they are used. Using the Actor model with actors as Aggregates [Reactive] is one of the easier ways to keep your Aggregates’ state cached.

Another tool at your disposal is snapshots, where the load time of your Aggregates that have been evicted from memory can be reconstituted optimally without reloading every Domain Event from an event stream. This translates to maintaining a snapshot of some incremental state of your Aggregate (object, actor, or record) in the database. Snapshots are discussed in more detail in Implementing Domain-Driven Design [IDDD] and in Reactive Messaging Patterns with the Actor Model [Reactive].

如果关注的重点之一是性能，就需要了解缓存和快照的知识。首先，性能最好的是那些缓存在内存中的聚合，每次用到它们时不需要从存储中进行重建。使用 Actor 作为聚合的 Actor 模型 [Reactive] 是一种更为简便的保持缓存聚合状态的方法。可以使用的另外一种工具是快照 [1]，从内存中释放的聚合能够以最优方式进行重建，而不需要加载事件流中的每个领域事件，这样可以节省加载时间。这将转变成在数据库中对聚合（对象、Actor 或记录）的一些增量状态的快照进行維护。快照在《实现领域驱动设计》和《响应式架构：消息模式 Actor 实现与 Scala、Aka 应用集成》中有更详细的讨论。

1『原来作者的那本「Actor」的书籍是跟快照等概念相关的。』

1 Snapshot，是事件溯源必须支持的一种机制。如果每次读取聚合实例时，都要从头至尾将所有事件依次「重播」一遍，这样产生的性能开销可想而知，尤其事件数量特别多的时候。随着系统規模的扩大和时间的推移，这显然是无法避免的。而快照可以在某个时间点将聚合实例的完整状态进行持久化，之后的读取只需要在这次保存下来的最新状态上「重播」之后发生的事件，这样可以极大地提升性能。一一译注

2『一直对「持久化」这个概念没有一个具体的认知，去搜索一下相关知识。』——未完成

』

One of the greatest advantages of using Event Sourcing is that it saves a record of everything that has ever happened in your Core Domain, at the individual occurrence level. This can be very helpful to your business for many reasons, ones that you can imagine today, such as compliance and analytics, and ones that you won’t realize until later. There are also technical advantages. For example, software developers can use event streams to examine usage trends and to debug their source code.

You can find coverage of Event Sourcing techniques in Implementing Domain-Driven Design [IDDD]. Also, when you use Event Sourcing you are almost certainly obligated to use CQRS. You can also find discussions of this topic in Implementing Domain-Driven Design [IDDD].

使用事件溯源最大的优势之一就是它在独立事件这个级别保存了核心域中发生的一切。这会从各个方面对业务产生非常大的帮助，有一些现在就能想象得到，比如合规性检查和数据分析，还有一些将来才会意识到。它还有一些技术上的优势，例如，软件开发人员可以利用事件流检查使用趋势或者调试源码。在《实现领域驱动设计》中可以找到关于事件溯源技术的内容。另外，当使用事件溯源时，几乎一定会同时使用 CQRS。相关主题的讨论也可以在《实现领域驱动设计》中找到。

## 0701. Acceleration and Management Tools

In summary, in this chapter you learned: 1) About Event Storming, how it can be used, and how to perform sessions with your team, all with a view to accelerating your modeling efforts. 2) About other tools that can be used along with Event Storming. 3) How to use DDD on a project and how to manage estimates and the time you need with Domain Experts. For an exhaustive reference covering the implementation of DDD on projects, see Implementing Domain-Driven Design [IDDD].

When using DDD we are on a quest for deep learning about how the business works, and then to model software based on the extent of our learning. It’s really a process of learning, experimenting, challenging, learning more, and modeling again. We need to crunch and distill knowledge in great quantities and produce a design that is effective in meeting the strategic needs of an organization. The challenge is that we have to learn quickly. In a fast-paced industry we are usually working against time, because time matters, and time generally drives many of our decisions, possibly even more than it should. If we don’t deliver on time and within budget, no matter what we have achieved with the software, we seem to have failed. And everyone is counting on us to succeed in every way.

Some have made efforts to convince management that most project time estimations are valueless and that they cannot be successfully used. I am not sure how those efforts are working out in the large, but every client with whom I work is still being pressured to deliver within very specific time frames, which forces timeboxing into the design/implementation process. At best it’s a constant struggle between software development and management.

Unfortunately, one common response to this negative pressure is to try to economize and shorten timelines by eliminating design. Recall from the first chapter that design is inevitable, and that either you will do poorly as a result of bad design, or you will succeed by delivering with an effective design, and possibly even with a good design. So, what you should attempt to do is meet the demands of time squarely and design in an accelerated way, using approaches that will help you deliver the very best design possible within the limits of time that you face.

To that end I provide some very useful design acceleration and project management tools in this chapter. First I discuss Event Storming and then conclude with a way to leverage the artifacts produced by that collaboration process to create estimates that are meaningful and, best of all, attainable.

当使用 DDD 时，我们的任务是深入学习业务如何运作，然后基于学习的范围建立软件模型。这实际上是一个学习、试验、质疑、再学习和重建模型的过程。我们要从大量学到的内容中研磨和提炼知识，并创造出能有效满足组织战略需要的设计。我们面临的挑战是如何快速地学习。在快节奏的行业中，我们在和时间赛跑，因为时间很关键，并且往往促使我们做出许多决定，有些决定甚至超出了我们的能力范围。如果不能按时、按预算交付，无论我们的软件可以达到什么样的高度，我们都会失败，但每个人都希望我们在各个方面取得成功。

有些人试图说服管理层，大多数项目的时间估算没有价值也不能成功地被采用。我不确定这些尝试在大型项目中的效果，但和我共事的每个客户仍然承受着在给定时间范围内完成交付的压力，这会迫使时间盒变成设计实施的瀑布流程。即使在最乐观的情况下，这也会变成软件开发人员和管理层之间的拉锯战。

不幸的是，应付这种负面压力的一种普遍手段是，牺牲设计来节省时间和缩短周期。第 1 章我们就说过，无论是因为糟糕的设计而挣扎，还是因为交出了有效甚至优秀的设计而成功，设计都是不可或缺的。所以，我们应该尝试不打折扣地满足时间要求，并加速设计，这要运用一些方法，这些方法能够帮你在面对时间限制时交出最佳设计。

为此，我将在本章提供一些非常实用的加速设计和项目管理的工具。首先会讨论事件风暴（Event Storming），然后总结一种方法，该方法利用协作过程中的产出物来做出有意义的估算，最重要的一点是，这些估算是可以达成的。

### 7.1 Event Storming

Event Storming is a rapid design technique that is meant to engage both Domain Experts and developers in a fast-paced learning process. It is focused on the business and business process rather than on nouns and data.

Prior to learning Event Storming I used a technique that I called event-driven modeling. It usually involved conversations, concrete scenarios, and event-centric modeling using very lightweight UML. The UML-specific steps could be achieved on a whiteboard alone and could also be captured in a tool. However, as you probably know, few business people are informed and proficient in even a minimalistic use of UML. So, this left most of the modeling part of the exercise to me or another developer who understood the basics of UML. It was a very useful approach, but there had to be a way to get business experts more directly involved in the process. That probably meant leaving out UML in favor of a more engaging tool.

事件风暴是一种快速的设计技术，让领域专家和开发人员都可以参与到这个快节奏的学习过程中。它聚焦于业务和业务流程，而非名词概念和数据。

在学习事件风暴之前，我使用过一种被我称为事件驱动建模的技术。它通常涉及对话和具体的场景，还会用到非常轻量的 UML，并以事件为中心的方式建模。UML 的相关步骤可以只用白板完成，也可以使用工具记录。然而，你可能已经意识到，很少有业务人员能了解或精通哪怕是最简化的 UML。所以，练习中建模部分的大多数工作就留给了我和另外一位有些 UML 基础的开发人员。这是一种非常有用的方法，但必须想办法让业务专家直接参与整个过程。这很可能意味着要放弃 UML，转投另一种更具吸引力的工具。

I first learned about Event Storming years ago from Alberto Brandolini [Ziobrando], who had also experimented with another form of event-driven modeling. On one occasion, being short on time, Alberto decided that he should ditch the UML and use sticky notes instead. This was the birth of an approach to rapid learning and software design that got everybody in the room very directly involved in the process. Here are some of its advantages:

1. It is a very tactile approach. Everyone gets a pad of sticky notes and a pen and is responsible for contributing to the learning and design sessions. Both business people and developers stand on equal ground as they learn together. Everyone provides input to the Ubiquitous Language.

2. It focuses everyone on events and the business process rather than on classes and the database.

3. It is a very visual approach, which dismisses code from the experimentation and puts everyone on a level footing with the design process.

4. It is very fast and very cheap to perform. You can literally storm out a new Core Domain in rough format in a matter of hours rather than weeks. If you write something on a sticky note that you later decide doesn’t work, you wad up the sticky note and throw it away. It costs you only a penny or two for that mistake, and no one is going to resist the opportunity to refine due to effort already invested.

5. Your team will have breakthroughs in understanding. Period. It happens every time. Some will come to the session thinking that they have a pretty good understanding of the specific core business model, but no matter, they always leave with a greater understanding and even new insights about the business process.

6. Everybody learns something. Whether you are a Domain Expert or a software developer, you will walk away from the sessions with a crisp, clear understanding of the model at hand. This is different from achieving breakthroughs and is important in its own right. In many projects, at least some project members, and possibly many, do not understand what they are working on until it is too late and the damage is already in the code. Storming out a model helps everyone clear up misunderstandings and move forward with a unified direction and purpose.

7. This implies that you are also identifying problems in both the model and in understanding as early and quickly as possible. Iron out misunderstandings and leverage the outcome as new insights. Everybody in the room benefits.

8. You can use Event Storming for both big-picture and design-level modeling. Doing big-picture storming will be less precise, while design-level storming will lead you toward certain software artifacts.

9. It is unnecessary to limit the storming sessions to one. You can start off with a two-hour storming session, then take a break. Sleep on your accomplishments and return the next day to spend another hour or two to expand and refine. If you do this for two hours a day for three or four days, you will gain a deep understanding of your Core Domain and integrations with your surrounding Subdomains.

几年前，我是在 Alberto Brandolini [Ziobrando] 那第一次学习到事件风暴，他也曾经试验过其他形式的事件驱动建模方法。一次偶然的机会，因为时间所剩无几，Alberto 决定放弃 UML 转而使用便利贴。一种能让房间里所有人都直接参与其中的快速学习和进行软件设计的方法由此而诞生。下面是该方法的一些优点：

1、这是一种有很强参与感的方法。每个人都拿着一叠便利贴和马克笔，随时可以加入学习和设计的讨论中。业务人员和开发人员在平等的基础上共同学习。每个人都使用通用语言提出建议。

2、它令每个人都聚焦于事件和业务流程，而不是类和数据库。

3、这是一种高度视觉化的方法，消除了试验过程中的代码，让每个人平等地参与到设计过程中。

4、它实施起来非常快，投入成本也很低。只需花几个小时，而不用数周，就差不多可以通过头脑风暴得出粗略形式的核心域模型。如果后来发现写在便利贴上的内容不对，把它揉成一团扔掉即可。这样的错误只会花费几分钱且谁也不会因为担心浪费己经投入的精力而拒绝改善设计的机会。

5、你的团队成员无一例外地会取得对业务理解的突破。有些成员在加入讨论之前认为他们已经非常了解特定的核心业务，但是无论怎样，他们都会带着对业务流程更深入的认知甚至新颖的见解离开。

6、每个人都能学到东西。无论是业务专家还是软件开发人员，都会带着对现有模型新鲜且清晰的理解离开讨论。这不同于业务理解上取得的突破，对于模型本身的理解也很重要。在许多项目中，一部分甚至大多数项目成员根本不了解他们的工作内容，直到代码出现问题，才发现为时己晚。快速产出模型能帮助每个人消除误解，朝着统一的方向和目标前进。

7、这意味着你已经尽早、尽快地在模型和认知中识别出了问题，扫除误解并将结论作为新的见解善加利用。屋子里的每个人都将受益匪浅。

8、宏观（big-picture）的建模和设计级别（design-level）的建模都可以使用事件风暴。宏观的事件风暴不追求细节，而设计级别的事件风暴会引导你完成一些特定的软件产出物。

9、不必强求一次风暴讨论就能解决所有问题。可以先从一次两小时左右的风暴讨论开始，然后休息。枕着前一天的成果入睡，第二天再花上一两个小时来扩展和完善。如果每天两小时，连续做上三四天，你将会深入地理解核心域以及它和周边子域之间的集成。

Here is a list of the people, mindset, and supplies you will need to storm out a model:

1. Having the right people is essential, which means the Domain Expert(s) and developers who are to work on the model. Everyone is going to have some of the questions and some of the answers. In order to support each other, they all need to be in the same room during the modeling sessions.

2. Everyone should come with an open mind that is free of strict judgment. The biggest mistake I see during Event Storming sessions is people trying to be too correct too soon. You should rather be fully determined to create far too many events. More events is better than fewer events, because that’s what will make you learn the most. There is time to refine later, and refinement is fast and cheap.

3.  Have on hand an assortment of colors of sticky notes, and plenty of them. At a minimum you need these colors: orange, purple/red, light blue, pale yellow, lilac, and pink. You may find that other colors (such as green; see later examples) come in handy. The sticky note dimensions can be square (3 inches by 3 inches, or 7.62 cm by 7.62 cm) rather than the wider variety that are rectangular. You don’t need to write much on the sticky note; usually just a few words will do. Consider getting the extra-sticky variety. You don’t want your sticky notes falling on the floor.

4. Provide one black marker pen for each person, which will enable handwriting to show up bold and clear. Fine-tip markers are best.

5. Find a wide wall where you can model. Width is more important than height, but your modeling surface should be approximately one meter/yard high. Width should be practically unlimited, but something in the range of 10 meters/yards should be considered a minimum. In lieu of such a wall being available, you can always use a long conference table or the floor. The problem with a table is that it will ultimately limit your modeling space. The problem with the floor is that it might not be accessible to everyone on the team. A wall is best.

6. Obtain a long roll of paper, such as can often be found at art stores, teaching supply stores, and even at Ikea stores. The paper should be to the dimensions described previously, with at least 10 meters/yards in width and 1 meter/yard in height. Hang the paper on the wall using strong tape. Some may decide to forgo the paper and just work on whiteboards. This may work for a while, but the sticky notes tend to lose adhesion over time on whiteboards, especially if they are pulled up and restuck in different locations. Stickies adhere longer when they are applied to paper. If you intend to model for brief periods of time over three or four days, rather than in one long session, longevity of stickiness is important.

1、邀请合适的人员是最基本的要求，领域专家和开发人员都要在模型上工作。每个人都会提出问题，也能给出问题的答案。为了互相支持，他们全部都要在同一个房间里参与建模讨论。

2、每个成员都应该以开放包容的心态参与。我在事件风暴讨论中观察到的最大问题就是，人们总是苛刻地追求正确和速度。创建事件的时候别犹豫，多多益善，因为你可以从中学到更多的东西，将来还有时间既快速又经济地完善这些事件。

3、手边要有各种颜色的便利贴，永远不要嫌多。你至少需要这几种颜色：橘色、紫红色、浅蓝色、淡黄色、浅紫色和粉红色。你会发现其他颜色（比如绿色，后面的例子会用到）的便利贴也能派上用场。便利贴的尺寸应该是正方形（边长 7.62m）而不是那种更常见的矩形。便利贴上不需要写太多字，通常只用写几个词语。要考虑选一些贴得更牢的便利贴，你不会想看到便利贴散落在地上。

4、每个人都需要一支黑色马克笔，用它写的字清楚醒目。粗字笔效果最好。

5、找一面可以用来建模的宽墙。墙的宽度比高度更重要，但你用来建模的墙面至少需要 1m 的高度。墙面宽度最好没有限制，10m 左右的宽度应该是最低要求。通常可以使用长的会议桌或者地板来代替这样的可用墙面。会议桌的问题是它始终会限制你的施展空间，而地板的问题在于团队中未必所有成员都能轻松地够得着。所以，墙是最好的选择。

6、准备一大卷白纸，通常可以在美术用品店、文具/教具店买到，甚至可以在宜家买到。白纸的尺寸应该和前面提到的墙面一样，宽 10m，高 1m，使用强力胶带将白纸贴在墙上。有些人选择使用白板代替白纸，这样虽然可以工作一段时间，但是白板上的便利贴会慢慢失去黏性，特别是反复地在不同位置上揭开又重贴之后白纸上的便利贴会贴得更久，如果你的建模活动打算进行大概三四天，而不是在几个小时的会议内结東，那么便利贴粘贴的寿命至关重要。

Given the basic supplies and having the right people participating in the session, you are ready to begin. Consider each of the steps, one by one.

#### 01

Storm out the business process by creating a series of Domain Events on sticky notes. The most popular color to use for Domain Events is orange. Using orange makes the Domain Events stand out most prominently on the modeling surface.

通过创建一系列写在便利贴上的领域事件，快速梳理出业务流程。最流行的代表领域事件的便利贴颜色是橘色。橘色让建模平面上的领域事件最显眼突出。下面是在创建领域事件时应该遵守的一些基本规则。

The following are some basic guidelines that should be employed as you create your Domain Events:

1. Creating Domain Events first should emphasize that we have our first and primary focus on the business process, not on the data and its structure. It may take your team 10 to 15 minutes to warm up to this, but follow the steps just as I outline them here. Don’t be tempted to jump ahead.

2. Write the name of each Domain Event on a sticky note. The name, as you learned in the previous chapter, should be a verb stated in the past tense. For example, an event may be named ProductCreated, and another may be named BacklogItemCommitted. (You can certainly break these names into multiple lines on the sticky notes.) If you are doing big-picture storming and you think that these names are too precise for the participants, use other names.

3. Place the sticky notes on your modeling surface in time order, that is, from left to right in the order in which each event occurs in the domain. You start with the first Domain Events to the far left of your modeling surface and then move gradually to the right. Sometimes you won’t have a good understanding of the time order, in which case you should just put the corresponding Domain Events somewhere in the model. Figure out the “when” part, which will probably become obvious, later.

4. A Domain Event that happens in parallel with another according to your business process can be located under the Domain Event that happens at the same time. So, you use vertical space to represent parallel processing.

5. As you go through this part of the storming session, you are going to find trouble spots in your existing or new business process. Clearly mark these with a purple/red sticky note and some text that explains why it’s a problem. You need to invest time at such points to learn more.

6. Sometimes the outcome of a Domain Event is a Process that needs to run. This could be a single step or multiple complex steps. Each Domain Event that causes a Proces s to be executed should be captured and named on a lilac sticky note. Draw a line with an arrowhead from the Domain Event to the named Process (lilac sticky note). Model a fine-grained Domain Event only if it is important to your Core Domain. Most likely a user registration process is a necessity but probably not considered a core feature of your application. Model the registration process as one single coarse-grained event, UserRegistered, and move on. Put your concentrated efforts into more important events.

1、在创建领域事件时要强调我们优先和主要关注的是业务流程，而不是数据及其结构。这可能要花费 10-15 分钟才能让团队适应，但是请按照我这里列出的步骤慢慢来，别着急略过任何步骤。

2、把每个领域事件的名称写在一张便利贴上。在前面的章节中已提到，事件的名称应该是动词的过去式。例如，可以命名某个事件为 Productcreated 而命名另一个事件为 Backlogitemcommitted（当然可以把这些名称分成几行写在便利贴上）。如果正在进行的是宏观的事件风暴，并且你认为这些名称对参与者来说过于细致，请使用其他名称。

3、把这些写好事件的便利贴按照时间顺序摆放在建模平面上，即按照每个事件在领域中发生的先后顺序从左到右排列。从建模平面上最左边的、最先发生的领域事件开始，逐步地向右推进。有时可能没有搞清楚确切的时间顺序那就把领域事件放在平面的其他地方。对于它「何时发生」的这个问题，可能稍后才会变得清晰。

4、按照业务流程，有些领域事件会和其他事件并行发生，可以把这些事件摆放在同时发生的领域事件的下方。这样，就可以使用纵向的空间来表示并行处理。

5、在风暴讨论的这个步骤中，会在已有的或新的业务流程中发现问题点。将它们清楚地记录在紫/红色的便利贴上，并用一段文字解释为什么它是一个问题点。你需要在这些问题点上投入更多的时间来学习。

6、有时领域事件将导致一个需要执行的流程（Process）。流程可以是一个单独步骤，也可以是多个复杂步骤。由每个领域事件导致执行的流程都应该被命名并记录在浅紫色的便利贴上。请从领域事件开始绘制一条带箭头的连线最终指向这个命名流程（浅紫色便利贴）。只用对那些核心域中非常重要的细粒度领域事件进行建模。用户注册的流程或许是必需的，但可能不会被视为应用程序的核心功能。应该将注册流程创建成一个粗粒度的事件 UserRegistered，然后继续建模。把精力集中于需要解决的更重要的问题。

If you think you have exhausted all possible important Domain Events, it may be time to take a break and come back to the modeling session later. Returning to the modeling surface a day later will no doubt cause you to find missing concepts and to refine or toss out superficial ones that you previously considered important. Even so, at some point you will have identified most of the Domain Events that are of greatest importance. At that time you should move on to the next step.

如果你认为己经穷尽了所有可能的重要领域事件，那么可以休息一下，稍后再回到建模的讨论中。一天之后再次回到建模平面前，你将可以找到之前缺失的一些概念，还可以改进或抛弃那些之前认为重要但现在却发现无关紧要的概念。即便如此，在某个时刻，你将识别出大部分最重要的领域事件。这时你应该继续下一步。

#### 02

Create the Commands that cause each Domain Event. Sometimes a Domain Event will be the outcome of a happening in another system, and it will flow into your system as a result. Still, often a Command will be the outcome of some user gesture, and that Command, when carried out, will cause a Domain Event. The Command should be stated in the imperative, such as CreateProduct and CommitBacklogItem. These are some basic guidelines:

创建导致每个领域事件发生的命令。有时，领域事件由其他系统中所发生的事情引发，作为结果流入系统中。但是，命令（Command）通常是某个用户操作的结果，而且命令的执行将导致领域事件的发生。命令应该被描述成指令式的，比如 CreateProduct 和 CommitBacklogItem。下面是一些基本指南：

1. On the light blue sticky notes, write the name of the Command that causes each corresponding Domain Event. For example, if you have a Domain Event named BacklogItemCommitted, the corresponding Command that causes that event is named CommitBacklogItem.

2. Place the light blue sticky note of the Command just to the left of the Domain Event that it causes. They are associated in pairs: Command/Event, Command/Event, Command/Event, and so on. Remember that some Domain Events will occur because of time limits being reached and so may not have a corresponding Command that explicitly causes them.

3. If there is a specific user role that performs an action, and it is important to specify, you can place a small, bright yellow sticky note on the lower left corner of the light blue Command with a stick figure and the name of the role. In the above figure, “Product Owner” would be the role that performs the Command.

4. Sometimes a Command will cause a Process to be run. This could be a single step or multiple complex steps. Each Command that causes a Process to be executed should be captured and named on a lilac sticky note. Draw a line with an arrowhead from the Command to the named Process (lilac sticky note). The Process will actually cause one or more Commands and subsequent Domain Events, and if you know what those are now, create sticky notes for them and show them emitting from the Process.

5. Continue to move from left to right in time order just as you did when first creating each of the Domain Events.

6. It is possible that creating Commands will cause you to think about Domain Events (as above when discovering lilac Processes, or other ones) that you didn’t previously envision. Go ahead and address this discovery by placing the newly discovered Domain Event on the modeling surface along with its corresponding Command.

7. You may also find that there is only one Command that causes multiple Domain Events. That’s fine; model the one Command and place it to the left of the multiple Domain Events that it causes.

1、在浅蓝色便利贴上，写下导致每个领域事件发生的对应命令的名称。例如，如果有一个名为 BacklogItemCommitted 的领域事件，导致该事件发生的对应命令的名称是 CommitBacklogItem。

2、把代表命令的浅蓝色便利贴紧挨着摆放在由它引起的领域事件的左边。它们被成对地关联在一起：命令 / 事件、命令 / 事件、命令 / 事件，一对接一对。记住有些领域事件是由即将到达的时间期限引起的，因此不存在对应的显式命令导致它发生。

3、如果存在一个执行动作的特定用户角色，并且这一点很重要，可以在浅蓝色命令的左下角贴上一张亮黄色的小便利贴，画上一个简笔小人并写上角色的名称。上图的示例中，「产品负责人」就是执行这个命令的角色。

4、有时命令将会导致流程的执行。流程可以是一个单独步骤，也可以是多个复杂步骤。每个命令导致执行的流程都应该被命名并记录在浅紫色的便利贴上。从命令开始绘制一条带箭头的连线，最后指向这个命名流程（浅紫色便利贴）。实际上，流程将触发一个或更多的命令以及这些命令后续的领域事件，如果现在你就知道这些内容，请用便利贴表示它们，并标明它们是由该流程触发的。

5、按照从左到右的时间顺序继续处理下一个命令 / 事件对，和先前创建领域事件时一样。

6、创建命令很有可能让你想到一些之前没有预料到的领域事件（比如上面发现的浅紫色流程或者其他事件）。继续把新发现的领域事件和它对应的命令摆放在建模平面上，记录下这些新的发现。

7、你还会发现一个命令可能导致多个领域事件发生。这很正常。创建一个命令把它摆放在那些由它引起的所有领域事件的左边。

Once you have all of the Commands associated with the Domain Events that they cause, you are ready to move on to the next step.

#### 03

Associate the Entity/Aggregate on which the Command is executed and that produces the Domain Event outcome. This is the data holder where Commands are executed and Domain Events are emitted. Entity relationship diagrams are often the first and most popular step in today’s IT world, but it is a big mistake to start here. Business people don’t understand them well, and they can shut down conversations quickly. In fact, this step has been relegated to third place in Event Storming, because we are more focused on the business process than on the data. Even so, we do need to think about data at some point, and that point is now. At this stage, business experts will likely understand that the data comes into play. Here are some guidelines for modeling the Aggregates :

把命令和领域事件通过实体 / 聚合 [1] 关联起来，命令在实体 / 聚合上执行并产生领域事件的结果。实体就是命令执行和领域事件触发的数据载体。在如今的 IT 世界中，绘制实体关系图通常是最流行的第一个步骤，但以此为起点却大错特错。业务人员并不了解这些关系图，很快就会失去沟通的兴趣。事实上，这个步骤已经在事件风暴中被推迟到了第三步，因为我们更关注业务流程而非数据。即便如此，我们确实需要在某个时候考虑数据，现在是时候了。在这个阶段，业务专家可能会理解数据在模型中扮演的角色。下面是一些建立聚合模型的指南：

1 在这个步骤中，虽然引用了 DDD 中的两个概念「实体」和「聚合」，但它们所表达的含义和《领域驱动设计》一书中的这两个概念的含义有所不同。Eric 在书中强调，「实体」是对业务对象的抽象属于解决方案。「聚合」由一个或一组实体所组成，也属于解決方案。而当下，我们的团队还处于对业务问题域的分析和理解过程中，因此译者建议读者将该步骤中的「实体」看成客观的业务对象；将「聚合」看成一个拥有生命周期的状态机，并由一个或一组业务对象所组成。——译注

1. If the business people don’t like the word Aggregate, or if it confuses them in any way, you should use another name. Usually they can understand Entity, or you could just call it Data. The important thing is that the sticky allows the team to communicate clearly about the concept that it represents. Use the pale yellow sticky notes for all Aggregates and write the name of an Aggregate on each sticky note. This is a noun, such as Product or BacklogItem. You will do this for each Aggregate in your model.

2. Place the Aggregate sticky note behind and slightly above the Command and Domain Event pairs. In other words, you should be able to read the noun written on the Aggregate sticky note, but the Command and Domain Event pairs should adhere to the lower part of the Aggregate sticky to indicate that they are associated. If you really want to put a little space between the stickies that’s fine, but just be clear which Commands and Domain Events belong to which Aggregate.

3. As you move across your business process timeline, you will probably find that Aggregates are repeatedly used. Don’t rearrange your timeline in order to move all Command/Event pairs under a single Aggregate sticky note. Rather, create the same Aggregate noun on multiple sticky notes and place them repeatedly on the timeline where the corresponding Command/Event pairs occur. The main point is to model the business process; the business process occurs over time.

4. It’s possible that as you think about the data associated with various actions, you may discover new Domain Events. Don’t ignore these. Rather, place the newly discovered Domain Events along with the corresponding Commands and Aggregates on the modeling surface. You may also discover that some of the Aggregates are too complex, and you need to break these into a managed Process (lilac sticky). Don’t ignore these opportunities.

1、如果业务人员不喜欢聚合这个词，或者这个词以任何形式干扰了他们，就应该使用其他名称。通常他们可以理解实体，或者干脆称之为数据。重要的是，团队可以利用便利贴清楚地沟通它们代表的概念。使用淡黄色便利贴表示所有聚合，把每个聚合的名称都写在便利贴上。这个名称是一个名词，比如 Product 或 Backlogitem。模型中的每个聚合都要完成这一步。把命令和领域事件便利贴一起贴在聚合便利贴上，聚合便利贴稍微靠上和其他两张便利贴错开一些。换句话说，你应该能看到聚合便利贴上的名词，而命令和领域事件便利贴应该分别贴在聚合便利贴的左下角和右下角，这样表明它们是关联在一起的。如果想让这些便利贴之间多错开一些距离也没有问题，但是要清楚地表示哪些命令和领域事件是属于哪个聚合的。

2、沿着业务流程的时间线移动，你很可能会发现一个聚合被反复地使用。不用调整时间线让所有命令 / 事件对都贴在同一张聚合便利贴上，而应该用多张便利贴，都写上同一个聚合的名字，分别贴在时间线上对应命令 / 事件对出现的地方。我们的重点是对业务流程建模，而业务流程是按时间发生的。

3、当你思考和各种操作相关的数据时，可能会发现新的领域事件。不要忽视这些事件，而应该将新发现的领域事件和对应的命令和聚合记录下来，放在建模平面上。你还可能会发现某些聚合过于复杂，需要将它们拆分成一个托管的流程（浅紫色便利贴）[1]。不要放过任何改善的机会。

1 就和前面步骤中发现的登录流程一样，它包含很多领域事件和命令，复杂但不属于核心域，使用没紫色便利贴表示就可以。——译注

Once you have completed this part of the design stage, you are approaching some of the extra steps that you can perform if you choose to. Also understand that if you are using Event Sourcing, as described in the previous chapter, you have already come a long way toward understanding your Core Domain implementation, because there is a large overlap in Event Storming and Event Sourcing. Of course, the closer your storming is to the big picture, the further it potentially is from actual implementation. Still, you can use this same technique to reach a design-level view. In my experience teams tend to move in and out of big-picture and design-level within the same sessions. In the end your need to learn certain details will drive you beyond the big picture to reach a design-level model where it is essential.

设计阶段进行这一步后，还可以选择执行一些额外的步骤。还要理解一点，如果使用的是第 6 章中提到的事件溯源，你对核心域实现的理解己经迈进了一大步，因为事件风暴和事件溯源中存在大量的重叠内容。当然，事件风暴越宏观，它离真实的实现就越远。不过，也可以使用同样的技术来完成设计级别的建模。根据我的经验，团队倾向于在同一次事件风暴的讨论中，不断切换宏观和设计级别的视角。最后，对某些细节理解和学习的追求会驱使你超越大局观，接近最基本的设计级别的模型。

Draw boundaries and lines with arrows to show flow on your modeling surface. You have very likely discovered that there are multiple models in play, and Domain Events that flow between models, in your Event Storming sessions. Here’s how to deal with that:

在建模平面上画出边界和表示事件流动的箭头连线。在事件风暴的讨论中，很可能已经发现了多个模型和在这些模型之间流动的领域事件。下面是处理这些模型和事件方法：

1. In summary, you will very likely find boundaries under the following conditions: departmental divisions, when different business people have conflicting definitions for the same term, or when a concept is important but not really part of the Core Domain.

2. You can use your black marker pens to draw on the paper modeling surface. Show context and other boundaries. Use solid lines for Bounded Contexts and dashed lines for Subdomains. Obviously drawing boundaries on the paper is permanent, so be sure you understand this level of detail before wading in. If you want to start by bounding models with less permanence, use the pink stickies to mark general areas and withhold drawing boundaries with permanent markers until your confidence justifies it.

3. Place the pink sticky notes inside various boundaries and put the name that applies inside the boundary on those sticky notes. This names your Bounded Contexts.

4. Draw lines with arrowheads to show the direction of Domain Events flowing between Bounded Contexts. This is an easy way to communicate how some Domain Events arrive in your system without being caused by a Command in your Bounded Context.

1、简要地说，你非常有可能在下面这些条件满足时发现边界：部门分界出现时、不同业务人员对相同术语的定义出现冲突时，或者非常重要但不属于核心域的某个概念出现时。

2、可以用黑色马克笔在建模平面的白纸上绘制边界。要把上下文边界和其他类型的边界区分开。使用实线表示限界上下文边界，使用虚线表示子域边界。显然，绘制在纸上的边界是永久性的，所以请在动笔前确保你对这层细节的理解是准确的。如果你想先把模型围起来并且还可以方便地调整边界，请使用粉红色的便利贴标出大概区域，不要用永久性马克笔绘制边界，直到你具备了判断边界是否准确的信心。

3、把粉红色便利贴摆在不同的区域边界内，并在这些便利贴上写上代表该区域内容的名字。这就是在给限界上下文命名。

4、绘制箭头连线来表示领域事件在限界上下文之间的流动方向。这是一种交流领域事件如何抵达系统的简单方法，这些领域事件并非由限界上下文中的命令引起。

Any other details about these steps should be intuitively obvious. Just use boundaries and lines to communicate.

#### 05

Identify the various views that your users will need to carry out their actions, and important roles for various users.

1. You won’t necessarily need to show every view that your user interface will provide, or any at all for that matter. If you decide to show any views, they should be those that are significant and require some special care in creating. These view artifacts can be represented by green sticky notes on the modeling surface. If it helps, draw a quick mockup (or wireframe) of the user interface views that are most important.

2. You can also use bright yellow sticky notes to represent various important user roles. Again, show these only if you need to communicate something of significance about the user’s interaction with the system, or something that the system does for a specific role of user.

It could well be that the fourth and fifth steps are all the extras you will need to incorporate with your Event Storming exercises.

识别用户执行操作所需的各种視图（views），以及不同用户的关键角色。

1、不一定展示用户界面提供的所有视图，或者根本不需要展示任何视图。你觉得需要展示的任何视图都应该是非常重要的并且在创建时需要特别留意。这些视图产出物可以用建模平面上的绿色便利贴表示。请绘制那些最重要的用户界面视图的快速原型（或者线框图），如果这样做有帮助的话。

2、你还可以使用亮黄色便利贴来表示各种不同的重要用户角色。再次重申，只有当关于用户和系统交互的重要事项，或者系统针对用户的特定角色要完成的事情需要交流时，才需要展示这些内容。

#### Other Tools

Of course this doesn’t prevent you from experimenting, such as placing other drawings on your modeling surface and trying other modeling steps in your Event Storming session. Remember, this is about learning and communicating a design. Use whatever tools you need to model as a close-knit team. Just be careful to reject ceremony, because that’s going to cost a lot. Here are some other ideas:

Introduce high-level executable specifications that follow the given/when/then approach. These are also known as acceptance tests. You can read more about this in the book Specification by Example by Gojko Adzic [Specification], and I provide an example in Chapter 2, “Strategic Design with Bounded Contexts and the Ubiquitous Language.” Just be careful not to go overboard with these, where they become all-consuming and take precedence over the actual domain model. I estimate that it requires somewhere in the range of 15% to 25% more time and effort to use and maintain executable specifications instead of common unit-testing-based approaches (also demonstrated in Chapter 2 ), and it is easy to get caught up in keeping the specifications relevant to the current business direction as the model changes over time.

Try Impact Mapping [Impact Mapping] to make sure the software you are designing is a Core Domain and not some less important model. This is a technique also defined by Gojko Adzic.

Look into User Story Mapping by Jeff Patton [User Story Mapping]. This is used to place your focus on the Core Domain and understand what software features you should be investing in.

The previous three add-on tools have a large overlap with the DDD philosophy and would be quite suitable to introduce into any DDD project. All of them are meant to be used in a highly accelerated project, are low ceremony, and are very cheap to use.

2『已下载书籍「2020156实例化需求 | 2020156Specification-by-Example」、「Impact Mapping」、「User Story Mapping」。』

当然，这并不妨碍你进行试验，比如在建模平面上加入其他图形，并在事件风暴讨论中尝试其他建模步骤。请记住，这是关于设计的学习和沟通的过程，可以使用任何必要的工具将团队拧成一股绳来进行建模。只是要小心抵制仪式化，因为这会浪费很多资源。下面是其他的一些创意。

引入按照「假如/当/那么」（Given/When/Then）的格式编写的可执行的高级需求说明，也被称为验收测试。你可以在 Gojko Adzic 的《实例化需求》一书中读到更多相关的内容，我在第 2 章中提供了一个例子。请注意，不要过度使用这种方法，别让它们消耗了全部精力，或是让它们显得比实际的领域模型还要重要。我做过估算，使用和维护可执行的需求说明来代替常见的基于单元测试的方法（在第 2 章中也有描述），需要花费 15%-25% 的额外时间和精力，还要在模型不断变化的同时保持需求说明和当前业务方向一致，这很容易就陷入困境。

试试影响力地图 1，确保你设计的软件是核心域，而不是一些不太重要的模型。这也是 Gojko Adzic 创造的方法。参考 Jeff Patton 的用户故事地图 2，可以通过这种方法将重点放在核心域，并搞清楚应该将资源投入哪些软件特性。

上面这三种补充工具有很大一部分和 DDD 的思想重叠，而且非常适合引进到任何采用 DDD 的项目上。所有这些工具都可以在全力加速的项目中使用，它们不是那么的仪式化，而且实施成本很低。

### 7.2 Managing DDD on an Agile Project

I previously mentioned that there has been a movement around what is called No Estimates. This is an approach that rejects typical estimation approaches such as story points or task hours. It focuses on delivering value over controlling cost, and not estimating any task that would likely require only a few months to complete. I don’t dismiss this approach. Yet, at the time of writing this, the clients I work with are still required to provide estimates and to timebox tasks, such as programming effort needed to implement even fine-grained features. If No Estimates works for you and your project situation, use it.

I am also aware that some in the DDD community have basically defined their own process or process execution framework for using DDD and performing with it on a project. This may work well and be effective when it is accepted by a given team, but it can be more difficult to get buy-in from organizations that have already invested in an agile execution framework, such as Scrum.

前面我曾提到过周围正在发生的名为拒绝估算（No Estimates) 的运动。这种方法拒绝采用常见的估算形式，比如故事点或者工时。它关注价值的交付更胜于关注成本的控制，对于即使只需要几个月完成的任务都不做估算。我不反对这种做法。然而，在撰写本书时我合作的客户仍然需要提供估算并限制任务时间，比如实现同等的细粒度功能所需的编程工作量。如果拒绝估算适合你和你的项目，那就接受它。

我还了解到，DDD 社区中的一些人为了在项目中实施 DDD，定义了他们自己的基本流程或流程实施框架。当这些流程或框架被某个团队接受时，可能会有效并运转良好。但是，在那些已经把资源投入敏捷实施框架（例如 Scrum）的组织里，这些流程或框架要获得支持可能会更加困难。

No Estimates，最早源于 Twitter 上个 Hashtag（话题）「#NoEstimates」。最初，一些开发者在这个话题下讨论估算的替代方法，这些讨论后来逐步扩大到博客和行业会议中，变成了一场运动。它并非全盘否定估算的效果，而是强调持续改进，不断地思考有哪些手段可以协助或者改善敏捷实践中的估算活动让团队能够更聚焦于交付价值。拒绝估算的实践者会先推动限制可用的估算点数（比如只允许 1 点、2 点和 3 点，甚至只允许 1 点），继而推动团队将故事和任务拆解成更小的可交付的任务。当任务足够小交付足够快时，就不再需要估算了。他们通过这种方法让团队更关注交付价值而不是浪费精力去做不准确的无意义的估算。——译注

Martin Fowler 关于估算的总结恰到好处：「估算本身并无好坏之分…...任何关于估算用法的争论，都要遵从于敏捷的原则，即针对特定的上下文，决定该采用什么样的方法。」请参考《估算的目的》一文。——译注

I have observed that recently Scrum has come under considerable criticism. While I don’t take sides in this criticism, I will openly state that often or even most times Scrum is being misused. I have already mentioned the tendency for teams to “design” using what I call “the task-board shuffle.” It’s just not the way Scrum was meant to be used on a software project. And, to repeat myself again, knowledge acquisition is both a Scrum tenet and a major goal of DDD but is largely ignored in exchange for relentless delivery with Scrum. Even so, Scrum is still heavily used in our industry, and I doubt that it will be displaced anytime soon.

Therefore, what I will do here is to show you how you can make DDD work in a Scrum-based project. The techniques I show you should be equally applicable with other agile project approaches, such as when using Kanban. There is nothing here that is exclusive to Scrum, although some of the guidance is stated in terms of Scrum. And since many of you will already be familiar with Scrum by putting it into practice in some form, most of my guidance here will be regarding the domain model and learning, experimenting, and designing with DDD. You will need to look elsewhere for general guidance on using Scrum, Kanban, or another agile approach.

Where I use the term task or task board, this should be compatible with agile in general, and even Kanban. Where I use the term sprint, I will also try to include the words iteration for agile in general and WIP (work in progress) as a reference to Kanban. It may not always be a perfect fit, as I am not trying to define an actual process here. I hope you will simply benefit from the ideas and find a way to apply them appropriately in your specific agile execution framework.

我注意到最近 Scrum 饱受批评。虽然我不持任何立场，但我会公开声明 Scrum 经常被误用，甚至在大部分时间内都被误用。我经提到过一些团队使用我称之为「任务板挪卡」的方法来进行「设计」的作风。这本来就不是 Scrum 应该在软件项目中的正确使用方式。而且，我再次重申，知识获取（Knowledge Acquisition）既是 Scrum 的宗旨，也是 DDD 的主要目标之一，但是在 Scum 的实施中却在很大程度上被牺牲了，用来交换无止境的交付。即便如此，Scrum 在我们这个行业内仍然会被大量使用，对它很快就会日薄西山的说法我表示怀疑。

因此，我将在这里展示如何在基于 Scrum 运作的项目中运用 DDD。我向你展示的技术应该同样适用于其他敏捷项目方法，比如看板方法。这里没有什么是 Scrum 独有的，尽管些指南是用 Scrum 术语来表述的。鉴于大多数读者都通过某种形式的实践熟悉了 Scrum，所以大部分指南都是关于领域模型，以及使用 DDD 进行学习、试验和设计的。你需要在别处寻找使用 Scrum、看板方法或其他敏捷方法的概要指南。

在这里我将使用术语任务（Task）或任务板（Task Board），这些术语应该与通用敏捷方法甚至是看板方法兼容。在这里我会使用术语冲刺，也会尝试使用通用敏捷方法中的选代（Iteration）一词，在涉及看板方法时我会使用 WIP 这些术语并不总是能完美地契合，因为我并不想在这里尝试定义一个实际的流程。我希望你可以从这些想法中受益，并找到一种方式在特定的敏捷实施框架中恰当地应用这些想法。

Working in Process 的编写，在制品进行中的工作，来源于制造业。此处特指在软件研发工作流中的正在进行的开发任务，并通过对其管理来持续优化产品交付流程。——译注

#### 7.2.1 First Things First

One of the most important means to successfully employing DDD on a project is to hire good people. There is simply no replacement for good people, and above-average developers for that matter. DDD is an advanced philosophy and technique for developing software, and it calls for above-average developers, even very good developers, to put it to use. Never underestimate the importance of hiring the right people with the right skills and self-motivation.

在项目中成功应用 DDD 的最重要的手段之一就是聘请优秀的员工。在这方面，优秀人才和中上水平的开发人员根本无法替代。DDD 是开发软件的先进理念和技术，中上水平的乃至是非常优秀的开发人员能运用好它。雇用技能匹配和自我激励的合适人选的重要性永远不能低估。

#### 7.2.2 Use SWOT Analysis

In case you are unfamiliar with SWOT analysis [SWOT], it stands for Strengths, Weaknesses, Opportunities, and Threats. SWOT analysis is a way for you to think about your project in very specific ways, gaining maximum knowledge as early as possible. Here are the basic ideas behind what you are looking to identify on a project: 1) Strengths: characteristics of the business or project that give it an advantage over others. 2) Weaknesses: characteristics that place the business or project at a disadvantage relative to others. 3) Opportunities: elements that the project could exploit to its advantage. 4) Threats: elements in the environment that could cause trouble for the business or project.

At any time on any Scrum or other agile project you should feel free and inclined to use SWOT analysis to determine your project’s current situation:

1. Draw a large matrix with four quadrants.

2. Going back to the sticky notes, choose a different color for each of the four SWOT quadrants.

3. Now, identity the Strengths of your project, the Weaknesses of your project, the Opportunities on your project, and the Threats to your project.

4. Write these on the sticky notes and place them in the matrix within the appropriate quadrant.

5. Use these SWOT characteristics of the project (we are particularly thinking domain model here) to plan what you are going to do about them. The next steps you take to promote the good areas and mitigate the troublesome areas could be critical to your success.

You will have the opportunity to place these actions on the task board as you perform project planning, as discussed later.

#### 7.2.3 Modeling Spikes and Modeling Debt

Does it surprise you to learn that you can have modeling spikes and modeling debt to pay on a DDD project?

One of the best things you can do at the inception of a project is to use Event Storming. This and related modeling experiments would constitute a modeling spike. You will have to “buy” knowledge about your Scrum product, and sometimes the payment is a spike, and a spike during project inception is almost certain. Still, I have already shown you how using Event Storming can greatly reduce the cost of necessary investment.

For certain, you can’t expect to model your domain perfectly from the start, even if you think in terms of the inception of your project as having a valuable modeling spike. You won’t even be perfect as you use Event Storming. For one thing, business and our understanding of it change over time, and so will your domain model.

Furthermore, if you intend to timebox your modeling efforts as tasks on a task board, expect to incur some modeling debt during each sprint (or iteration, or WIP). You simply won’t have time to carry out every desired modeling task to perfection when you are timeboxed. For one thing, you will start a design and realize after experimentation that the design you have does not fit the business needs as well as you expected. Yet the time limit that you are under will require you to move on.

The worst thing you could do now is to just forget everything that you learned from the modeling efforts that called out for a different, improved design. Rather, make a note that this needs to go into a later sprint (or iteration, WIP). This can be brought to your retrospective meeting 1 and turned in as a new task at your next sprint planning meeting (or iteration planning meeting, or added to the Kanban queue).

看到 DDD 项目中出现建模 Spike，甚至还有建模债务要偿还，你是不是有些惊讶？项目启动阶段最好的选择之一就是事件风暴。它与其他相关的建模试验将共同形成一次建模 Spike。你必须「购买」关于 Scrum 产品的知识，有时「支付方式」就是建模 Spike，项目启动阶段几乎都需要 Spike。不过，我已经展示了使用事件风暴可以大大降低必要的投资成本。

毫无疑问，即便将有价值的建模 Spike 视为项目的启动，也别指望一开始就可以完美地建立领域模型。甚至使用事件风暴之后，建模也不会那么完美。首先，业务和我们对它的理解会随着时间而改变，领域模型也会随之变化。此外，如果打算将建模工作当作任务，在任务板上管理它，并限定其完成时间，则可能会在每个冲刺（或迭代，或 WIP）中产生一些建模债务。当有时间限制时，根本没有足够的时间去尽善尽美地完成所有想要的建模任务。首先，将从设计开始，并在试验后意识到这些设计既不符合业务需求也不符合自己的预期。然而，却迫于时间限制的压力停下未完成的设计继续其他任务。

Spike 一词来源于极限编程（Extreme Programming），它通过一系列的探索活动获取必要的知识，以降低技术方法的风险、更好地理解业务需求或提高用户故事估算的可靠性。这些探索活动包括研究、设计、调查和原型等。——译注

Modeling Debt，建模债务是类比技术债务（Technical Debt）的提法。技术债务是编程及软件工程中的一个比喻，指开发人员为了加速软件开发采取的短视而非最佳的方案，虽然眼前看起来可以得到好处，但必须在未来偿还。作者认为建模也是这样的，会因为时间压力而妥协并产生债务，而这些债务需要记录下来并及时偿还。更多关于技术债务的内容请参考《「鱼变慢」还是「技术债」：适合国人口味的比喻》一文。——译注

项目启动阶段是指在产品或项目启动初期，业务和技术人员通过高密度、深度协作互动的一系列工作坊，对项目范围、技术实现以及需求优先级达成初步一致的理解的过程，以便于快速进入后期项目交付。它也是一个将想法（ldea）变为计划（Plan）的过程。我们也希望读者可以将事件风暴引入这个过程中，以一种快速的设计技术，让领域专家和开发人员都可以参与到这个快节奏的学习过程中。——译注

In Kanban you can actually have retrospectives every day, so don’t wait for long to present the need to improve the model.

#### 7.2.4 Identifying Tasks and Estimating Effort

Event Storming is a tool that can be used at any time, not just during project inception. As you work in an Event Storming session, you will naturally create a number of artifacts. Each of the Domain Events, Commands, and Aggregates that you storm out in your paper model can be used as estimation units. How so?

事件风暴可以在任何时间使用，并不会被局限在项目启动阶段中。在事件风暴中的工作会自然而然地创造出大量产出物。在纸面模型中创造出的每个领域事件、命令和聚合，都可以当作估算单元。该如何做呢？

One of the easiest and most accurate ways to estimate is by using a metrics-based approach. As you see here, create a simple table with estimation units for each component type that you will need to implement. This will take the guesswork out of estimates and provide science around the process of creating estimations of effort. Here is how the table works:

1. Create one column for Component Type to describe the specific kind of component for which the estimation units are defined.

2. Create three other columns, one each for Easy, Moderate, and Complex. These columns will reflect the estimation unit, which is in hours or fractions of hours, for the specific unit type.

3. Now create one row for each component type in your architecture. Shown are Domain Event, Command, and Aggregate types. However, don’t limit yourself to those. Create a row for the various user interface components, services, persistence, Domain Event serializers and deserializers, and so on. Feel free to create a row for every single kind of artifact that you will create in source code. (If, for example, you normally create a Domain Event serializer and deserializer along with each Domain Event as a composite step, assign an estimation value to Domain Events that reflects the creation of all of those components together in each column.)

4. Now fill in the hours or fraction of an hour needed for each level of complexity: easy, moderate, and complex. These estimates not only include the time needed for implementation but may also include further design and testing efforts. Make these accurate, and be realistic.

5. When you know the backlog item tasks (WIP) that you will work on, obtain a metric for each of the tasks and identify it clearly. You might use a spreadsheet for this.

6. Add up all the estimation units for all components in the current sprint (iteration or WIP), and this becomes your total estimation.

最简单和最准确的估算方式之一是，使用基于度量指标的方法。正如在这里所看到的创建一张包含估算单元的简单表格，每种需要实现的组件类型都对应着一个估算单元。这将去除估算中的猜测部分，并为工作量估算的过程提供科学依据。以下是该表格的工作原理。

1、第一列代表组件类型（Component Type），描述了特定的组件种类，每一个种类都定义了估算单元。

2、其他三列分别代表简单（Easy）、适中（Moderate）和复杂（Complex）。这些列将代表特定单元类型的估算单元，表示为以小时为单位的整数或分数。

3、现在为架构中出现的每一种组件类型添加一行。这里只展示了领域事件、命令和聚合这几种类型。但是，不要局限于这些类型。各种用户界面组件、服务、持久化操作、领域事件的序列化器和反序列化器等都可以添加一行。源代码中创建的每种特殊的产出物类型都可以添加一行（例如，如果通常在一个复合步骤里创建领域事件以及它的序列化器和反序列化器，在每一列中给这些领域事件分配的估算值要能体现出所有这些组件是一起创建的）。

4、现在，填入每一种复杂级别（简单、适中和复杂）所需要的小时数（整数或者分数）。这些估算不仅包括实现所需的时间，还要包括进一步的设计和测试的工作量。这些数字要做到既精确又真实。

5、当你知道接下来要处理的待办项任务（WIP）时，找到每项任务对应的指标并明确地识别出来。这里电子表格可以派上用场。

6、将当前冲刺（代或 WIP）中所有组件的估算单元相加，就能得到总的估算。

As you execute each sprint (iteration or WIP), tune your metrics to reflect the hours or fractions of hours that were actually required.

If you are using Scrum and you have come to detest hour estimates, understand that this approach is much more forgiving and also much more accurate. As you learn your cadence, you will fine-tune your estimation metrics to be more accurate and realistic. It might require a few sprints to get it right. Also realize that as time and experience progress, you will probably either tune your numbers lower or use the Easy or Moderate columns more readily.

If you are using Kanban and you think that estimates are completely fallacious and unnecessary, ask yourself a question: How do I know how to determine an accurate WIP in the first place in order to correctly limit our work queue? Regardless of what you may think, you are still estimating the effort involved and hoping that it is correct. Why not add a little science to the process and use this simple and accurate estimation approach?

当执行每个冲刺（迭代或 WIP）时，根据实际完成需要的小时数（整数或分数）来调整这些指标。如果正在使用 Scrum 而且已经厌倦了以小时为单位的估算，请理解这种方法会更加宽容，也更加精确。在找到节奏之后，会调整估算度量指标，使其更加准确，更加符合实际。这可能需要几个冲刺来找感觉。还需要意识到，随着时间的推移和经验的增长，可能要调低估算的数字或者更多地使用简单或适中这两列。

如果正在使用看板方法，并且认为估算完全不可靠也没有必要，那么请问自己一个问题：怎样才能先确定精确的 WIP 来正确地限制我们的工作队列？不管你怎么想，你仍然在估算涉及的工作量，并寄希望于它是正确的。为什么不让流程变得更科学一点，使用这种简单而准确的估算方法呢？

相信大部分读者，特别是拥有敏捷（包括 Scrum）软件开发方法实践经验的读者，更熟悉的是使用故事点数来做估算，而不是这里的小时数。要准确地做出对完成故事所需小时数的估算是很困难的，因为影响这个数字的因素实在太多，未知的风险、模棱两可的需求和开发者的经验都会对其产生影响。而故事点数反映的是故事的复杂度。这里作者提出的这种方法也许能在他经历的一些案例中奏效。作者也在他的 Twitter 中提到，这种方法实际上是 #NoEstimates 中定义的「预测」（Forecast）而不是「估算」（Estimate），是「基于参考数据的分析结果对未来事件做出的预判和计算」。「预测」也好「估算」也罢，每一种估算方法都有它使用的场景。读者应该根据自己希望借助估算达成的目标和项目的实际情况选择适合自己的估算方式并持续改进。但是，作者这里对完成每个任务的真实时间的持续记录是非常值得推荐的实践。即便要做出估算，基于过往真实数据的推测总要好过拍脑袋。——译注

『

A Comment on Accuracy

This approach works. On one large corporate program the organization demanded estimates for a large and complex project within the overall program. Two teams were assigned to this task. First there was a team of high-cost consultants who worked with Fortune 500 companies to estimate and manage projects. They were accountants and had doctorates and were outfitted with everything that would both intimidate and give them the clear advantage. The second team of architects and developers was empowered with this metrics-based estimation process. The project was in the \$20 million range, and in the end when both estimates came in, they were within approximately \$200,000 of each other (the technical team’s being the slightly lower estimate). Not bad for techies.

You should be able to get within 20% accuracy on long-term estimates, and much better on shorter-term estimates, such as for sprints, iterations, and WIP queues.

这种方法是有效的。在一个大型公司计划中，该组织要求对整个计划中的个大型复杂项目进行估算。这个任务被分配给了两个团队。第一个团队由费用昂贵的顾问组成，他们有着与财富 500 强公司合作的估算和项目管理经验。这个团队里都是会计师和博士，还拥有能带来优势的震撼配置。第二个团队则是架构师和开发人员，他们使用这种基于度量指标的评估流程。该项目的规模在 2000 万美元左右，最终两个团队做出的估算结果只相差约 20 万美元（技术团队的估算略低）。技术人员做得还不赖。

』


### 7.3 Timeboxed Modeling

Now that you have estimates for each component type, you can base your tasks directly off of those components. You might choose to keep each component as a single task with a number of hours or fraction thereof, or you might choose to break your tasks down a bit further. However, I suggest being careful with breaking tasks down to be too fine-grained, so as not to make the task board overly complex. As shown previously, it might even be best to combine all of the Commands and all of the Domain Events used by a single Aggregate into a single task.

现在已经得到了每种组件类型的估算，可以直接将任务建立在这些组件之上。可以选择将每个花费数小时的组件直接保留为单个任务，也可以选择将这些任务进一步分解。但是，我建议分解任务时要小心，别把任务分解得太细，以免任务板变得过于复杂。如前所述，甚至可以将单个聚合使用的所有命令和领域事件合并为一个任务。

#### 7.3.1 How to Implement

Even with artifacts identified by Event Storming, you will not necessarily have all the knowledge you need to work on a specific domain scenario, story, and use case. If more is needed, be sure to include time for further knowledge acquisition in your estimates. But time for what? Recall that in Chapter 2 I introduced you to creating concrete scenarios around your domain model. This can be one of the best ways to acquire knowledge about your Core Domain, beyond what you can get out of Event Storming. Concrete scenarios and Event Storming are two tools that should be used together. Here’s how it works:

即使有了在事件风暴中识别的产出物，也不一定掌握了完成关于特定领域场景、故事和用例的工作所需的全部知识。如果需要更多知识，请确保在估算中包含了更深入的知识获取所需的时间。时间怎么安排？回忆ー下，在第 2 章中，我介绍了围绕领域模型创建具体场景的方法。除了通过事件风暴获得知识，这可能是获取核心域知识的最佳途径之一。具体场景和事件风暴这两种工具应该一起使用。下面是具体的方法。

1. Perform a quick session of Event Storming, perhaps just for an hour or so. You will almost certainly discover that you need to develop more concrete scenarios around some of your quick modeling discoveries.

2. Partner with a Domain Expert to discuss one or more concrete scenarios that need to be refined. This identifies how the software model will be used. Again, these are not just procedures but should be stated with the goal of identifying actual domain model elements (e.g., objects), how the elements collaborate, and how they interact with users. (Refer to Chapter 2 as needed.)

3. Create a set of acceptance tests (or executable specifications) that exercise each of the scenarios. (Refer to Chapter 2 as needed.)

4. Create the components to allow the tests/specifications to execute. Iterate (briefly and quickly) as you refine the tests/specifications and the components until they do what your Domain Expert expects.

5. Very likely some of the iteration (brief and quick) will cause you to consider other scenarios, create additional tests/specifications, and refine existing and create new components.

1、开展一次快速的事件风暴讨论，可能只需要 1 小时左右。你几乎肯定会发现，你需要围绕着快速建模的发现来发展更多的具体场景。

2、和领域专家一起讨论一个或多个需要完善的具体场景。这将识别软件模型的使用方式。再次强调，这不仅是流程描述，而且还应该以识别真实的领域模型元素（例如对象）、元素协作方式以及用户交互方式为目标来进行陈述（需要时请参阅第 2 章）。

3、创建一组验收测试（或可执行的需求说明）来验证每个场景（需要时请参阅第 2 章）。

4、创建让这些测试 / 需求可以执行的组件。持续（短平快的）迭代来优化测试 / 需求说明和组件，直到达到领域专家的期望。

5、很可能某些（短平快的）迭代会激发你对其他场景的思考，创建额外的测试 / 需求，完善现有组件并创建新组件。

Continue this until you have acquired all the knowledge necessary to meet a limited business objective, or until your timebox expires. If you haven’t reached the desired point, make sure to incur modeling debt so that this can be addressed in the (ideally near) future.

Yet how much time will you need from Domain Experts?

持续下去直到获得能满足限定业务目标所需的全部知识，或抵达了时间盒的期限。如果还没有达到预期的目标，一定要记录下这些建模债务，这样可以在将来（越快越好）解决这个问题。然而需要占用多少领域专家的时间呢？

#### 7.3.2 Interacting with Domain Experts

One of the major challenges of employing DDD is getting time with Domain Experts, and without overdoing it. Many times those who are Domain Experts on a project will have loads of other responsibilities, hours of meetings, and possibly travel. With such potential absences from the modeling environment, it can be difficult to find enough time with them. So, we had better make the time we use count and limit it to just what is necessary. Unless you make modeling sessions fun and efficient, you stand a good chance of losing their help at just the wrong time. If they find it valuable, enlightening, and rewarding, you will likely establish the strong partnership that you will need.

运用 DDD 的主要挑战之一是，合理地协调领域专家的时间。很多时候，项目中的领域专家还承担着大量其他工作，他们要参加大大小小的会议，还有可能出差。他们缺席建模活动的可能性很大，因此很难协调出足够的时间和他们交流。所以，我们最好合理控制时间，将其限制在必要的范围内。除非能让建模讨论有趣又高效，否则很可能因为时间安排错误而失去他们的支持。如果他们觉得这些讨论有价值、有启发、有回报，那么你很可能会和他们建立起所需要的强有力的伙伴关系。

So the first questions to answer are “When do we need time with Domain Experts ? What tasks do they need to help us perform?”

1. Always include Domain Experts in Event Storming activities. Developers will always have a lot of questions, and Domain Experts will have the answers. Make sure they are in the Event Storming sessions together.

2. You will need Domain Experts’ input on discussions and the creation of model scenarios. See Chapter 2 for examples.

3. Domain Experts will be needed to review tests to verify model correctness. This assumes that the developers have already made a conscientious effort to adhere to the Ubiquitous Language and to use quality, realistic test data.

4. You will need Domain Experts to refine the Ubiquitous Language and its Aggregate names, Commands, and Domain Events, which are determined by the entire team. Ambiguities are resolved through review, questions, and discussion. Even so, Event Storming sessions should have already resolved most of the questions about the Ubiquitous Language.

所以，首先要回答的几个问题是：我们什么时候需要领域专家？他们需要帮助我们完成哪些任务？

1、一定要邀请领域专家参加事件风暴活动。开发人员总是会遇到很多问题，而领域专家有他们想要的答案。确保他们共同参与事件风暴讨论。

2、在讨论和创建模型场景时需要领域专家的意见。请参考第 2 章中的示例。

3、需要领域专家来评审验证模型正确性的测试。假定开发人员已经尽职尽责地遵循了通用语言，并使用了高质量的真实的测试数据。

4、需要领域专家来完善通用语言以及聚合名称、命令和领域事件，这些都应该由团队一起决定。通过评审、质疑和讨论来消除歧义。即便如此，事件风暴讨论应该已经解决了关于通用语言的大部分问题。

So, now that you know what you will need from Domain Experts, how much time should you require of them for each of these responsibilities?

1. Event Storming sessions should be limited to a few hours (two or three) each. You may need to hold sessions on consecutive days, such as for three or four days.

2. Block out generous amounts of time for scenario discussion and refinement, but try to maximize the time for each scenario. You should be able to discuss and iterate on one scenario over perhaps 10 to 20 minutes of time.

3. For tests, you will need some time with Domain Experts to review what you have written. But don’t expect them to sit there as you write the code. Maybe they will, and that’s a bonus, but don’t expect it. Accurate models require less time to review and verify. Don’t underestimate the ability of Domain Experts to read through a test with your help. They can do it, especially if the test data is realistic. Your tests should allow the Domain Expert to understand and verify around one test every one to two minutes, or thereabouts.

4. During test reviews, Domain Experts can provide input on Aggregates, Commands, and Domain Events, and perhaps other artifacts, as to how they adhere to the Ubiquitous Language. This can be accomplished in brief amounts of time.

This guidance should help you use just the right amount of time with Domain Experts, and to limit the amount of time that you need to spend with them.

现在已经知道了需要从领域专家那里得到的东西，那么这些工作需要占用他们多少时间呢？

1、每次事件风暴讨论应限制在几个小时（两三个小时）以内。你可以连续几天都进行讨论，比如三天或四天。

2、别用大块的时间讨论和细化场景，但尽量最大化利用每个场景的讨论时间。大概 10-20 分钟的时间，就能够完成一个场景的讨论和迭代。

3、需要一些时间和领域专家一起评审自己写的测试，但是别指望他们坐下来看着你写代码。也许他们会这样做，这是惊喜，但别抱任何幻想。模型越精确，检査和验证花费的时间就越少。不要低估领域专家阅读测试的能力。在你的帮助下，他们能做到这一点，特别是当使用真实测试数据时。测试应该让领域专家在一两分钟之内理解并验证。

4、在测试评审过程中，领域专家可以就聚合、命令和领域事件以及其他可能的产出物遵循通用语言的方式提出意见。这可以在短时间内完成。

上面这份指南应该可以帮助你和领域专家协调恰当的时间，并把他们需要被占用的时间限制在合理范围内。
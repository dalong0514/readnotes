## 记忆时间

## 卡片

### 0101. 主题卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——CQRS 

CQRS stands for Command Query Responsibility Segregation. It's a pattern that I first heard described by Greg Young. At its heart is the notion that you can use a different model to update information than the model you use to read information. For some situations, this separation can be valuable, but beware that for most systems CQRS adds risky complexity.

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。

#### 01. 基本信息

用一句话描述你对这个大牛的印象。

#### 02. 贡献及著作

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 目录

20200801Anemic-Domain-Model.md

20200802Domain-Driven-Design.md

20200803DDD-Aggregate.md

20200804Bounded-Context.md

20200805CQRS.md

20200806Currency-As-Value.md

20200807Contextual-Validation.md

20200808Customer-Loyalty-Software.md

## 20200801Anemic-Domain-Model.md

25 November 2003

This is one of those anti-patterns that's been around for quite a long time, yet seems to be having a particular spurt at the moment. I was chatting with Eric Evans on this, and we've both noticed they seem to be getting more popular. As great boosters of a proper Domain Model, this is not a good thing.

The basic symptom of an Anemic Domain Model is that at first blush it looks like the real thing. There are objects, many named after the nouns in the domain space, and these objects are connected with the rich relationships and structure that true domain models have. The catch comes when you look at the behavior, and you realize that there is hardly any behavior on these objects, making them little more than bags of getters and setters. Indeed often these models come with design rules that say that you are not to put any domain logic in the the domain objects. Instead there are a set of service objects which capture all the domain logic, carrying out all the computation and updating the model objects with the results. These services live on top of the domain model and use the domain model for data.

1『上面是老马对贫血模型症状的阐述。』

The fundamental horror of this anti-pattern is that it's so contrary to the basic idea of object-oriented design; which is to combine data and process together. The anemic domain model is really just a procedural style design, exactly the kind of thing that object bigots like me (and Eric) have been fighting since our early days in Smalltalk. What's worse, many people think that anemic objects are real objects, and thus completely miss the point of what object-oriented design is all about.

Now object-oriented purism is all very well, but I realize that I need more fundamental arguments against this anemia. In essence the problem with anemic domain models is that they incur all of the costs of a domain model, without yielding any of the benefits. The primary cost is the awkwardness of mapping to a database, which typically results in a whole layer of O/R mapping. This is worthwhile if you use the powerful OO techniques to organize complex logic. By pulling all the behavior out into services, however, you essentially end up with Transaction Scripts, and thus lose the advantages that the domain model can bring. As I discussed in P of EAA, Domain Models aren't always the best tool.

1『 P of EAA 是老马的书籍「Patterns of Enterprise Application Architecture」。』

It's also worth emphasizing that putting behavior into the domain objects should not contradict the solid approach of using layering to separate domain logic from such things as persistence and presentation responsibilities. The logic that should be in a domain object is domain logic - validations, calculations, business rules - whatever you like to call it. (There are cases when you make an argument for putting data source or presentation logic in a domain object, but that's orthogonal to my view of anemia.)

One source of confusion in all this is that many OO experts do recommend putting a layer of procedural services on top of a domain model, to form a Service Layer. But this isn't an argument to make the domain model void of behavior, indeed service layer advocates use a service layer in conjunction with a behaviorally rich domain model.

Eric Evans's excellent book Domain Driven Design has the following to say about these layers.

Application Layer [his name for Service Layer]: Defines the jobs the software is supposed to do and directs the expressive domain objects to work out problems. The tasks this layer is responsible for are meaningful to the business or necessary for interaction with the application layers of other systems. This layer is kept thin. It does not contain business rules or knowledge, but only coordinates tasks and delegates work to collaborations of domain objects in the next layer down. It does not have state reflecting the business situation, but it can have state that reflects the progress of a task for the user or the program.

Domain Layer (or Model Layer): Responsible for representing concepts of the business, information about the business situation, and business rules. State that reflects the business situation is controlled and used here, even though the technical details of storing it are delegated to the infrastructure. This layer is the heart of business software.

The key point here is that the Service Layer is thin - all the key logic lies in the domain layer. He reiterates this point in his service pattern:

1『充血模型，即模型模型的基本特点是，服务层很单薄，数据和行为都放到领域层了。』

Now, the more common mistake is to give up too easily on fitting the behavior into an appropriate object, gradually slipping toward procedural programming.

I don't know why this anti-pattern is so common. I suspect it's due to many people who haven't really worked with a proper domain model, particularly if they come from a data background. Some technologies encourage it; such as J2EE's Entity Beans which is one of the reasons I prefer POJO domain models.

In general, the more behavior you find in the services, the more likely you are to be robbing yourself of the benefits of a domain model. If all your logic is in services, you've robbed yourself blind.

## 20200802Domain-Driven-Design.md

Domain-Driven Design is an approach to software development that centers the development on programming a domain model that has a rich understanding of the processes and rules of a domain. The name comes from a 2003 book by Eric Evans that describes the approach through a catalog of patterns. Since then a community of practitioners have further developed the ideas, spawning various other books and training courses. The approach is particularly suited to complex domains, where a lot of often-messy logic needs to be organized.

Eric Evans's 2003 book is an essential read for serious software developers

The idea that software systems need to be based on a well-developed model of a domain has been around for at least as long as I've been in the industry. I learned much of this thinking from Jim Odell, who developed this style of thinking with data modeling, information engineering, and object-oriented analysis. Representing the underlying domain was a key part of much work in the database and object-oriented communities throughout the 1980s and 1990s.

Eric Evans's great contribution to this, through his book, was developing a vocabulary to talk about this approach, identifying key conceptual elements that went beyond the various modeling notations that dominated the discussion at the time. At the heart of this was the idea that to develop software for a complex domain, we need to build Ubiquitous Language that embeds domain terminology into the software systems that we build. While many folks talked about developing such models, they were often only done on paper, and usually expected to be done up-front. DDD stresses doing them in software, and evolving them during the life of the software product. Eric is a strong proponent of Extreme Programming and sees Domain-Driven Design as a natural component of an extreme programming approach - a view shared by most XP practitioners I know.

The book introduced the notion of classifying objects into Entities, Value Objects, and Service Objects - what I call the Evans Classification and identifying the concept of Aggregates. I found these filled an important gap in thinking about objects which eluded both programming languages and diagrammatic notations. A particularly important part of DDD is the notion of Strategic Design - how to organize large domains into a network of Bounded Contexts. Up that point, I'd not seen anyone tackle this issue in any compelling way.

Although Eric's background is rooted in the Object-Oriented community, the core notions of Domain-Driven Design are conceptual, and thus apply well with any programming approach - a fact that's especially true of the strategic design aspects.

## 20200803DDD-Aggregate.md

Aggregate is a pattern in Domain-Driven Design. A DDD aggregate is a cluster of domain objects that can be treated as a single unit. An example may be an order and its line-items, these will be separate objects, but it's useful to treat the order (together with its line items) as a single aggregate.

An aggregate will have one of its component objects be the aggregate root. Any references from outside the aggregate should only go to the aggregate root. The root can thus ensure the integrity of the aggregate as a whole.

Aggregates are the basic element of transfer of data storage - you request to load or save whole aggregates. Transactions should not cross aggregate boundaries.

DDD Aggregates are sometimes confused with collection classes (lists, maps, etc). DDD aggregates are domain concepts (order, clinic visit, playlist), while collections are generic. An aggregate will often contain mutliple collections, together with simple fields. The term "aggregate" is a common one, and is used in various different contexts (e.g. UML), in which case it does not refer to the same concept as a DDD aggregate.

## 20200804Bounded-Context.md

Bounded Context is a central pattern in Domain-Driven Design. It is the focus of DDD's strategic design section which is all about dealing with large models and teams. DDD deals with large models by dividing them into different Bounded Contexts and being explicit about their interrelationships.

DDD is about designing software based on models of the underlying domain. A model acts as a Ubiquitous Language to help communication between software developers and domain experts. It also acts as the conceptual foundation for the design of the software itself - how it's broken down into objects or functions. To be effective, a model needs to be unified - that is to be internally consistent so that there are no contradictions within it.

1『通用统一语言是开发人员和领域专家，知识的交集部分。』

As you try to model a larger domain, it gets progressively harder to build a single unified model. Different groups of people will use subtly different vocabularies in different parts of a large organization. The precision of modeling rapidly runs into this, often leading to a lot of confusion. Typically this confusion focuses on the central concepts of the domain. Early in my career I worked with a electricity utility - here the word "meter" meant subtly different things to different parts of the organization: was it the connection between the grid and a location, the grid and a customer, the physical meter itself (which could be replaced if faulty). These subtle polysemes could be smoothed over in conversation but not in the precise world of computers. Time and time again I see this confusion recur with polysemes like "Customer" and "Product".

In those younger days we were advised to build a unified model of the entire business, but DDD recognizes that we've learned that "total unification of the domain model for a large system will not be feasible or cost-effective" [1]. So instead DDD divides up a large system into Bounded Contexts, each of which can have a unified model - essentially a way of structuring Multiple Canonical Models.

Bounded Contexts have both unrelated concepts (such as a support ticket only existing in a customer support context) but also share concepts (such as products and customers). Different contexts may have completely different models of common concepts with mechanisms to map between these polysemic concepts for integration. Several DDD patterns explore alternative relationships between contexts.

Various factors draw boundaries between contexts. Usually the dominant one is human culture, since models act as Ubiquitous Language, you need a different model when the language changes. You also find multiple contexts within the same domain context, such as the separation between in-memory and relational database models in a single application. This boundary is set by the different way we represent models.

DDD's strategic design goes on to describe a variety of ways that you have relationships between Bounded Contexts. It's usually worthwhile to depict these using a context map.

### Further Reading

The canonical source for DDD is Eric Evans's book. It isn't the easiest read in the software literature, but it's one of those books that amply repays a substantial investment. Bounded Context opens part IV (Strategic Design).

Vaughn Vernon's Implementing Domain-Driven Design focuses on strategic design from the outset. Chapter 2 talks in detail about how a domain is divided into Bounded Contexts and Chapter 3 is the best source on drawing context maps.

I love software books that are both old and still-relevant. One of my favorite such books is William Kent's Data and Reality. I still remember his short description of the polyseme of Oil Wells.

Eric Evans describes how an explicit use of a bounded context can allow teams to graft new functionality in legacy systems using a bubble context. The example illustrates how related Bounded Contexts have similar yet distinct models and how you can map between them.

## 20200805CQRS.md

CQRS stands for Command Query Responsibility Segregation. It's a pattern that I first heard described by Greg Young. At its heart is the notion that you can use a different model to update information than the model you use to read information. For some situations, this separation can be valuable, but beware that for most systems CQRS adds risky complexity.

2『 CQRS，做一张术语卡片。』——已完成

The mainstream approach people use for interacting with an information system is to treat it as a CRUD datastore. By this I mean that we have mental model of some record structure where we can create new records, read records, update existing records, and delete records when we're done with them. In the simplest case, our interactions are all about storing and retrieving these records.

As our needs become more sophisticated we steadily move away from that model. We may want to look at the information in a different way to the record store, perhaps collapsing multiple records into one, or forming virtual records by combining information for different places. On the update side we may find validation rules that only allow certain combinations of data to be stored, or may even infer data to be stored that's different from that we provide.

As this occurs we begin to see multiple representations of information. When users interact with the information they use various presentations of this information, each of which is a different representation. Developers typically build their own conceptual model which they use to manipulate the core elements of the model. If you're using a Domain Model, then this is usually the conceptual representation of the domain. You typically also make the persistent storage as close to the conceptual model as you can.

This structure of multiple layers of representation can get quite complicated, but when people do this they still resolve it down to a single conceptual representation which acts as a conceptual integration point between all the presentations.

The change that CQRS introduces is to split that conceptual model into separate models for update and display, which it refers to as Command and Query respectively following the vocabulary of Command Query Separation. The rationale is that for many problems, particularly in more complicated domains, having the same conceptual model for commands and queries leads to a more complex model that does neither well.

By separate models we most commonly mean different object models, probably running in different logical processes, perhaps on separate hardware. A web example would see a user looking at a web page that's rendered using the query model. If they initiate a change that change is routed to the separate command model for processing, the resulting change is communicated to the query model to render the updated state.

There's room for considerable variation here. The in-memory models may share the same database, in which case the database acts as the communication between the two models. However they may also use separate databases, effectively making the query-side's database into a real-time Reporting Database. In this case there needs to be some communication mechanism between the two models or their databases.

The two models might not be separate object models, it could be that the same objects have different interfaces for their command side and their query side, rather like views in relational databases. But usually when I hear of CQRS, they are clearly separate models.

CQRS naturally fits with some other architectural patterns.

1. As we move away from a single representation that we interact with via CRUD, we can easily move to a task-based UI.

2. CQRS fits well with event-based programming models. It's common to see CQRS system split into separate services communicating with Event Collaboration. This allows these services to easily take advantage of Event Sourcing.

3. Having separate models raises questions about how hard to keep those models consistent, which raises the likelihood of using eventual consistency.

4. For many domains, much of the logic is needed when you're updating, so it may make sense to use EagerReadDerivation to simplify your query-side models.

5. If the write model generates events for all updates, you can structure read models as EventPosters, allowing them to be MemoryImages and thus avoiding a lot of database interactions.

6. CQRS is suited to complex domains, the kind that also benefit from Domain-Driven Design.

### When to use it

Like any pattern, CQRS is useful in some places, but not in others. Many systems do fit a CRUD mental model, and so should be done in that style. CQRS is a significant mental leap for all concerned, so shouldn't be tackled unless the benefit is worth the jump. While I have come across successful uses of CQRS, so far the majority of cases I've run into have not been so good, with CQRS seen as a significant force for getting a software system into serious difficulties.

In particular CQRS should only be used on specific portions of a system (a BoundedContext in DDD lingo) and not the system as a whole. In this way of thinking, each Bounded Context needs its own decisions on how it should be modeled.

So far I see benefits in two directions. Firstly is that a few complex domains may be easier to tackle by using CQRS. I must stress, however, that such suitability for CQRS is very much the minority case. Usually there's enough overlap between the command and query sides that sharing a model is easier. Using CQRS on a domain that doesn't match it will add complexity, thus reducing productivity and increasing risk.

The other main benefit is in handling high performance applications. CQRS allows you to separate the load from reads and writes allowing you to scale each independently. If your application sees a big disparity between reads and writes this is very handy. Even without that, you can apply different optimization strategies to the two sides. An example of this is using different database access techniques for read and update.

If your domain isn't suited to CQRS, but you have demanding queries that add complexity or performance problems, remember that you can still use a ReportingDatabase. CQRS uses a separate model for all queries. With a reporting database you still use your main system for most queries, but offload the more demanding ones to the reporting database.

Despite these benefits, you should be very cautious about using CQRS. Many information systems fit well with the notion of an information base that is updated in the same way that it's read, adding CQRS to such a system can add significant complexity. I've certainly seen cases where it's made a significant drag on productivity, adding an unwarranted amount of risk to the project, even in the hands of a capable team. So while CQRS is a pattern that's good to have in the toolbox, beware that it is difficult to use well and you can easily chop off important bits if you mishandle it.

### Further Reading

Greg Young was the first person I heard talking about this approach - this is the summary from him that I like best.

Udi Dahan is another advocate of CQRS, he has a detailed description of the technique.

There is an active mailing list to discuss the approach.

## 20200806Currency-As-Value.md

There are many common examples of Value Object, my favorite is Money - and one closely linked to Money is currency.

For many systems currency works well as a value, the key part you need is the internationally recognized currency code (such as USD for US Dollars).

However I was once involved with a system where it got a bit more interesting. If my memory serves me correctly, one of the things they wanted from their currency was a 'pip value'. On their UI they had nudge buttons to nudge the currencies up and down in value. Each currency had its own pip value, and this pip value could change. It didn't change often, but it did change. This violates a very useful rule of value objects - that they are immutable.

The solution we did was to have two currency classes. One was a value object, it held the currency code and maybe a couple of other immutable things. The second was a reference object (I think we called them something like CurrencyValue and CurrencyReference). The value object was passed around most of the time, but some methods in the value object, such as pip value, delegated to the reference object - which was mostly static data. The reference objects were held in a lookup table indexed by the currency code (that's not the only way to do it.)

This bi-semantic behavior is unusual - it's the only time I've seen it. Certainly most systems can get away with a simple value object for currency.

## 20200807Contextual-Validation.md

In my writing endeavors, I've long intended to write a chunk of material on validation. It's an area that leads to a lot of confusion and it would be good to get some solid description of some of the techniques that work well. However life is full of things to write about, rather more than time allows.

Some recent readings made me think about saying a few preliminary things on the topic. One common thing I see people do is to develop validation routines for objects. These routines come in various ways, they may be in the object or external, they may return a boolean or throw an exception to indicate failure. But one thing that I think constantly trips people up is when they think object validity on a context independent way such as an isValid method implies.

I think it's much more useful to think of validation as something that's bound to a context - typically an action that you want to do. Is this order valid to be filled, is this customer valid to check in to the hotel. So rather than have methods like isValid have methods like isValidForCheckIn.

One of the consequences of this is that saving an object to a database is itself an action. Thinking about it that way raises some important questions. Often when people talk about a context-free validity, they mean it in terms of saving to a database. But the various validity checks that make this up should be interrogated with the question "should failing this test prevent saving?"

In About Face Alan Cooper advocated that we shouldn't let our ideas of valid states prevent a user from entering (and saving) incomplete information. I was reminded by this a few days ago when reading a draft of a book that Jimmy Nilsson is working on. He stated a principle that you should always be able to save an object, even if it has errors in it. While I'm not convinced that this should be an absolute rule, I do think people tend to prevent saving more than they ought. Thinking about the context for validation may help prevent that.

## 20200808Customer-Loyalty-Software.md

I was in the Calgary office last week and had a good chat with John Kordyback, one of our most trusted technical leads. He's worked on, and dug into, a number of travel loyalty software systems (frequent flyer/sleeper etc) and we talked about the nature of these kinds of things and how to think about them in a more fruitful manner.

The core of of a loyalty system is a system to keep track of points (or miles). This should allow customers to see their points and also for the company to manage the unredeemed points. Although it seems that most people don't see it this way, this is essentially an accounting system, just switching points for dollars. John's observation was that repeatedly he runs into what people see as difficult problems that are much easier to deal with once you put accounting spectacles on.

An example of this is dealing with ad-hoc changes. However good your automated rules processing is, there always cases when something odd happens and you have to intervene manually. The result for many systems is and ad hoc change to totals that is error prone and unaudited. With an accounting frame of mind, however, you look at these changes as accounting adjustments and the patterns for this are well understood.

A notable difference between a loyalty program and most accounting systems is that a loyalty program is more about managing liabilities rather than managing assets. Hence there's more focus on things like risk management, as well as common themes like taxes and revenue reporting.

Many loyalty systems have multiple kinds of points, such as such as regular miles and elite qualifying miles. This is a common point of complexity. If you use an accounting viewpoint, however, you can track these easily as multiple currencies.

An interesting twist on this is potential points. If I book a flight for next month, the airline needs to know that there are miles I will earn when I fly next month (potential miles). These potential miles affect their liabilities. However it's only when I fly that they turn into real miles. Again accounting thinking can help here, we can use multiple currencies again, or use an accounts payable notion. The mechanisms are there and well understood, we just have to apply the model to the situation.

We fleshed this out in practice where we also found it really helpful to use TestDrivenDevelopment. A group of people spent a couple of weeks trying to sort out potential miles with planned design, but the core issue was cracked in a couple of days with TDD. The crucial part of this was focusing on examples to make the problem concrete.

The accounting analogy also applies, although partly less directly, to deciding how to award miles for activity. Any program has activity rules that need to be very flexible and need to cope with constant changes to the loyalty program. We can look at this as following the model of domain events triggering accounting entries through using Agreement Dispatchers. This is a pattern John and I have used lots of times and works well to these kinds of changing rules. Essentially we have agreements that represent the overall program rules for a class of participant. Each agreement consists of a set of posting rules keyed by the type of event and a date range. When an domain event occurs (a hotel stay) we look up the agreement dispatcher for the customer, and use the event to look up the right posting rule. We then run the posting rule to create the appropriate accounting entries to represent the miles for the event. The time dating of the events allow us to change posting rules over time but still be able to handle old events and correctly do automated processing of adjustments. (Some day I'll finish writing up these patterns, but what I have on the web is hopefully enough to give you some ideas.)

The second aspect of a loyalty system is tracking the customer experience. Since the accounting requires the system to record the customer's activity, the loyalty system acts as a natural base to learn from the customer's interactions with the company. Much of this is data mining - looking for patterns in customer behavior which can lead to new products and promotions. You can also use this activity history to assess the success of promotions - if you offer a mileage bonus for flying a route what is the response like?

Like me, John is a strong proponent of using ReportingDatabases, and this is a good fit for this kind of problem. The accounting side needs a very different set of data structures and uses regular updates as activities occur. The customer experience analysis is all read only, so you can use less normalized structures with regular, but not necessarily real time, feeds from the accounting side.

Taking it further, it seems reasonable to completely decouple the accounting and customer experience systems. They are both usually lodged together as a single customer loyalty system because they track the same events. Yet since they differ so much on the inside it may make more sense to treat them as two separate systems that feed off the same event stream (the accounting side would probably generate some events for the customer experience side too).

One of the habits of customer experience tracking is frequent changes to the system to support new kinds of analysis. We speculated that we could try an approach that had a single stored event log of customer activity, and plug in relatively independent 'miners' that would transform selected information from the log into more particular data structures to do different kinds of analysis. The miners could be relatively independent of each other and thus easier to build.

As you can see, our discussion did shift from looking at John's experiences to some of our joint speculations about how a system like this could be built in the future. What's clear to us is that there is a lot of room for exploring new ideas in this space that could introduce a new set of abstractions that would lead to systems that can provide better support to this business activity. More and more attention is being paid to this these days, so this seems like a fruitful territory for us to work in.
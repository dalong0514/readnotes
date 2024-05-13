Copyright © 2016 Pearson Education, Inc.

领域驱动设计（DDD）是时下软件设计领域中的热门话题，它通过指导我们构建领域模型，来表达丰富的软件功能需求，并由此实现可以满足用户真正需要的软件。然而在实践过程中，由于不同的角色对于 DDD 的核心概念和主要工具的理解不同，常常会造成协作上的不一致。为了帮助和指导面向对象的开发人员、系统分析人员和设计人员更加合理地组织工作，各有侧重、有条不紊地进行复杂系统的开发，并有效地建立丰富而实用的领域模型，本书的作者 Vaughn Vernon 将自己近年来在领域驱动设计领域的理解进一步提炼，并将本书以精粹的形式呈现给广大的读者。本书的内容包括：DDD 对于广大读者的意义、从战略层面进行设计、从战术层面进行设计，以及相关的辅助工具。当然，仅仅通过此书的阅读无法深入地掌握领域驱动设计的精髓，无论你是什么经验水平或角色，请阅读本书并在项目中实践 DDD。并在这之后，再重读此书，看看你从项目的经历中学到了什么。反复这样的循环，你将会获益匪浅。

1『总结了本书的四大内容：1）DDD 的意义。2）战略层进行设计。3）战术层进行设计。4）相关的辅助工具。』

## 译者序

2003 年，Eric Evans 的《领域驱动设计》出版，第一次总结了这种软件设计和建模方法。这种方法让团队在质疑中发展出对复杂问题的统一认识，再利用战略设计和战术设计的各种手段，如同庖丁解牛般地分解并映射成各种构造块，最后信手拈来地运用各种设计模式将这些构造块一一化解。领域驱动设计在国外的技术社区一直是受到热捧、不断演化的软件设计方法。在 Eric 的著作面世十年之后，另一位 DDD 社区的领军人物 Vaughn Vernon 撰写了《实现领域驱动设计》。在这本著作中，Vaughn 用一个连贯完整的实例，将领域驱动设计的所有概念和模式串连在一起，并将这些内容落地到了实例的代码之中。另外，他还在这部著作中总结了这十年来 DDD 社区涌现的一些新的架构风格和模式，如事件溯源和 CQRS、REST 风格的架构、事件驱动的架构、六边形架构，等等。

但这十几年间，在国内技术社区，领域驱动设计却像被遗忘在角落的宝藏等待着人们去发掘。当越来越复杂的业务场景开始频繁涌现，当工程实践和基础设施发展成熟，我们重新将视线汇聚在如何达成有效设计、将复杂的业务分而治之，我们发现这种设计方法仿佛早就看透了一切。当宝藏上的灰尘被拂去，领域驱动设计再次发出璀璨夺目的光芒，为我们指明应对软件系统复杂性的前进方向。

重新焕发青春活力的领域驱动设计得到了许多新的团队和架构师的青睞。他们首先就会去阅读这两部略微晦涩的著作，期望能快速地学习和掌握这种方法，但很快就会发现这并不轻松。首先，这两部著作要求读者具备一定的软件开发技术背景。在领域驱动设计的实践中，业务领域的专家在团队中扮演关键角色，他们往往没有软件开发的技术背景。两位软件巨匠在著作中详细阐述技术概念和实现代码时并没有照顾他们的感受。其次，这两部著作缺少对实际项目建模过程的描写。我们读到的内容多是概念的阐述和与之对应的实例及代码，对于建模实操的过程和工具着墨不多。而这些 Magic Move 却是很多团队实施领域驱动设计时迫切需要指导的关键步骤。最后，两部著作的内容包罗万象，读者容易被繁杂的知识淹没。两部著作中的一些概念和模式（如值对象、实体、工厂和仓储）早已深入人心。而另一部分模式和架构（如事件溯源和 CQRS）则要求架构经验尚浅的读者通过项目实践或扩展阅读才能深入理解。

作为《实现领域驱动设计》一书的作者，Vaughn 也意识到了这些问题，因此编写了这本「精粹版」。他将领域驱动设计的知识进行了提炼，保留了子域、限界上下文、上下文映射、聚合、领域事件这些核心概念，分别用一个章节进行了阐述。在最后一章，作者将他过去在一些团队中实践领域驱动设计时行之有效的具体操作方法（如风靡 DDD 社区的事件风暴工作坊）和工具进行了总结。本书的内容更侧重于高层次的战略设计，关于战术设计的内容偏少，尤其是代码在内容中的比重极低，完全不影响非技术背景的读者阅读。如果你想开始在团队中尝试领域驱动设计，对于团队（包括业务领域的专家）来说，本书的内容可以作为指导手册，让他们快速地进入状态，达到可以参与事件风暴工作坊的要求。我们建议读者们在阅读本书之后亲自组织并实施一次事件风暴工作坊，这是作者推荐的融合视觉、听觉和触觉三种学习方式的「知识获取」实践，是威力无穷的领域建模形式。在开发团队完成建模并最终需要落实到代码时，读者可以将本书作为「武林秘籍」的目录，结合前两部著作和本书参考文献中引用的其他专著一起阅读。

本书中，作者毫不掩饰地表达了对一些架构模式和具体实践的偏好。这些特色鲜明的观点之中，有些符合社区的普遍认知，如事件驱动的响应式架构、单元测试、事件风暴；有些却是对争议性话题的个人理解，如作者对于建模设计的工作量估算的看法。我们要牢记一点，没有「银弹」可以精确地匹配我们的产品和团队，或者完美地解决我们要面对的可题。任何工具和实践都有约束条件。读者们在采用这些工具和实践时，不妨仔细思考作者运用它们的上下文及其体现出的原则，结合自己的实际情况对工具和实践进行持续改进，避免出现教条主义错误。

我和同事笪磊结对完成了对本书的翻译。我们一人擅长技术，一人则擅长管理，翻译的过程也是我们默契配合、实践「发展通用语言」的「知识获取」过程。我们也将个人对关键内容的理解补充记录在译注中。我们力求翻译内容的准确和译注的质量，但受限于个人经验和知识水平，难免出现偏差甚至错误，还请各位读者斧正。

本书翻译工作于 2017 年末启动，两个月后初稿完成并进入了审校阶段。这期间正值农历戌成年春节，我们的投入离不开家人们的理解和支持，谢谢她们。我们还要感谢提出宝贵意见的审校者：肖然、刘传湘、王威、朱傲、黄雨清、王林波。他们过去几年都活跃在国内 DDD 社区，也帮助过许多团队运用领域驱动设计方法和事件风暴工作坊来实施架构设计和系统改造。他们过硬的理论知识和丰富的实践经验让本书的翻译增色不少。最后我们还要感谢专业和严谨的编辑张春雨和刘佳禾，本书也凝聚着你们的心血。

## Preface

Why is model building such a fun and rewarding activity? Ever since I was a kid I have loved to build models. At that time I mostly built models of cars and airplanes. I am not sure where LEGO was in those days. Still, LEGO has been a big part of my son’s life since he was very young. It is so fascinating to conceive and build models with those small bricks. It’s easy to come up with basic models, and it seems you can extend your ideas almost endlessly. You can probably relate to some kind of youthful model building.

Models occur in so many situations in life. If you enjoy playing board games, you are using models. It might be a model of real estate and property owners, or models of islands and survivors, or models of territories and building activities, and who knows what all. Similarly, video games are models. Perhaps they model a fantasy world with fanciful characters playing fantastic roles. A deck of cards and related games model power. We use models all the time and probably so often that we don’t give most models a well-deserved acknowledgment. Models are just part of our lives.

But why? Every person has a learning style. There are a number of learning styles, but three of the most discussed are auditory, visual, and tactile styles. The auditory learners learn by hearing and listening. The visual learners learn by reading or seeing imagery. The tactile learners learn by doing something that involves touching. It’s interesting that each learning style is heavily favored by the individual to the extent that he or she can sometimes have trouble with other types of learning. For example, tactile learners likely remember what they have done but may have problems remembering what was said during the process. With model building, you would think that visual and tactile learners would have a huge advantage over the auditory learners, because model building seems to mostly involve visual and tactile stimulation. However, that might not always hold true, especially if a team of model builders uses audible communication in their building process. In other words, model building holds out the possibility to accommodate the learning style of the vast majority of individuals.

With our natural affinity to learning through model building, why would we not naturally desire to model the software that ever increasingly assists and influences our lives? In fact, to model software appears to be, well, human. And model software we should. It seems to me that humans should be elite software model builders.

从建模中学习的能力是人类与生俱来的，为何不利用它去构建已经给生活带来巨大帮助和影响的软件模型呢？事实上，软件模型需要人类去实现，也应该由人类去完成。我认为，人类本应该是优秀的软件模型构建者。

It is my strong desire to help you be as human as you can possibly be by modeling software using some of the best software modeling tools available. These tools are packaged under the name “Domain-Driven Design,” or DDD. This toolbox, actually a set of patterns, was first codified by Eric Evans in the book Domain-Driven Design: Tackling Complexity in the Heart of Software [DDD] . It is my vision to bring DDD to everyone possible. To make my point, if I must say that I want to bring DDD to the masses, then so be it. That is where DDD deserves to be, and DDD is the toolbox that model-oriented humans deserve to use to create their most advanced software models. With this book, I am determined to make learning and using DDD as simple and easy as possible and to bring that to the broadest conceivable audience.

我强烈期望能够帮助你使用最好的建模工具来实现软件。这些工具已被打包成「领域驱动设计」工具箱，或称之为 DDD 工具箱。该工具箱实际上是一套模式，在 Eric Evans 所著的《领域驱动设计：软件核心复杂性应对之道》一书中首次提出。我期望将 DDD 带给每一个人。如果必须表达我的观点，我想说的是，让我把 DDD 介绍给大家吧！DDD 也本该如此，它是面向模型设计的人们用于构建卓越软件模型的工具箱。本书中，我会尽可能地简化 DDD 的学习和使用，并将其带给每一位读者。

For auditory learners, DDD holds out the prospect of learning through the team communication of building a model based on the development of a Ubiquitous Language. For visual and tactile learners, the process of using DDD tools is very visual and hands-on as your team models both strategically and tactically. This is especially true when drawing Context Maps and modeling the business process using Event Storming. Thus, I believe that DDD can support everyone who wants to learn and achieve greatness through model building.

对于听觉学习者而言，DDD 通过团队的沟通来构建基于通用语言的开发模型，并以此创造学习的契机。对于视觉和触觉学习者来说，在团队进行战略和战术建模时使用 DDD 其过程高度视觉化并非常注重实操。绘制上下文映射图并使用事件风暴构建业务流程时尤为如此。因此，我相信 DDD 可以帮助到每一位期待通过模型构建来学习并且希望获得伟大成就的人。

### Who Is This Book For?

This book is for everyone interested in learning the most important DDD aspects and tools and in learning quickly. The most common readers are software architects and software developers who will put DDD into practice on projects. Very often, software developers quickly discover the beauty of DDD and are keenly attracted to its powerful tooling. Even so, I have made the subject understandable for executives, domain experts, managers, business analysts, information architects, and testers alike. There’s really no limit to those in the information technology (IT) industry and research and development (R&D) environments who can benefit from reading this book.

If you are a consultant and you are working with a client to whom you have recommended the use of DDD, provide this book as a way to bring the major stakeholders up to speed quickly. If you have developers—perhaps junior or midlevel or even senior—working on your project who are unfamiliar with DDD but need to use it very soon, make sure that they read this book. By reading this book, at minimum, all the project stakeholders and developers will have the vocabulary and understand the primary DDD tools being used. This will enable them to share things meaningfully as they move the project forward.

Whatever your experience level and role, read this book and then practice DDD on a project. Afterward, reread this book and see what you can learn from your experiences and where you can improve in the future.

### What This Book Covers

The first chapter, “DDD for Me,” explains what DDD can do for you and your organization and provides a more detailed overview of what you will learn and why it’s important.

Chapter 2 , “Strategic Design with Bounded Contexts and the Ubiquitous Language ,” introduces DDD strategic design and teaches the cornerstones of DDD, Bounded Contexts and the Ubiquitous Language. Chapter 3 , “Strategic Design with Subdomains ,” explains Subdomains and how you can use them to deal with the complexity of integrating with existing legacy systems as you model your new applications. Chapter 4 , “Strategic Design with Context Mapping ,” teaches the variety of ways that teams work together strategically and ways that their software can integrate. This is called Context Mapping.

Chapter 5 , “Tactical Design with Aggregates ,” switches your attention to tactical modeling with Aggregates. An important and powerful tactical modeling tool to be used with Aggregates is Domain Events , which is the subject of Chapter 6 , “Tactical Design with Domain Events .”

Finally, in Chapter 7 , “Acceleration and Management Tools ,” the book highlights some project acceleration and project management tools that can help teams establish and maintain their cadence. These two topics are seldom if ever discussed in other DDD sources and are sorely needed by those who are determined to put DDD into practice.

### Conventions

There are only a few conventions to keep in mind while reading. All of the DDD tools that I discuss are printed in italics. For example, you will read about Bounded Contexts and Domain Events. Another convention is that any source code is presented in a monospaced Courier font. Acronyms and abbreviations for works listed in the References on pages 136 -137 appear in square brackets throughout the chapters.

Even so, what this book emphasizes most, and what your brain should like a lot, is visual learning through lots of diagrams and figures. You will notice that there are no figure numbers in the book, because I didn’t want to distract you with so many of those. In every case the figures and diagrams precede the text that discusses them, which means that the graphic visuals introduce thoughts as you work your way through the book. That means that when you are reading text, you can count on referring back to the previous figure or diagram for visual support.

## Acknowledgments

This is now my third book within the esteemed Addison-Wesley label. It’s also my third time working with my editor, Chris Guzikowski, and developmental editor, Chris Zahn, and I am happy to say that the third time has been as much a charm as the first two. Thanks again for choosing to publish my books.

As always, a book cannot be successfully written and published without critical feedback. This time I turned to a number of DDD practitioners who don’t necessarily teach or write about it but are nonetheless working on projects while helping others use the powerful toolbox. I felt that this kind of practitioner was crucial to make sure this aggressively distilled material said exactly what is necessary and in just the right way. It’s kind of like, if you want me to talk for 60 minutes, give me 5 minutes to prepare; if you want me to talk for 5 minutes, give me a few hours to prepare.

In alphabetical order by last name, those who helped me the most were Jérémie Chassaing, Brian Dunlap, Yuji Kiriki, Tom Stockton, Tormod J. Varhaugvik, Daniel Westheide, and Philip Windley. Thanks much!

## About the Author

Vaughn Vernon is a veteran software craftsman and thought leader in simplifying software design and implementation. He is the author of the best-selling books Implementing Domain-Driven Design and Reactive Messaging Patterns with the Actor Model, also published by Addison-Wesley. He has taught his IDDD Workshop around the globe to hundreds of software developers. Vaughn is a frequent speaker at industry conferences. He is most interested in distributed computing, messaging, and in particular with the Actor model. Vaughn specializes in consulting around Domain-Driven Design and DDD using the Actor model with Scala and Akka. You can keep up with Vaughn’s latest work by reading his blog at www.VaughnVernon.co and by following him on his Twitter account @VaughnVernon.

2『做一张人名卡片。』

## Contents

Chapter 1 DDD for Me

Chapter 2 Strategic Design with Bounded Contexts and the Ubiquitous Language

Chapter 3 Strategic Design with Subdomains

Chapter 4 Strategic Design with Context Mapping

Chapter 5 Tactical Design with Aggregates

Chapter 6 Tactical Design with Domain Events

Chapter 7 Acceleration and Management Tools
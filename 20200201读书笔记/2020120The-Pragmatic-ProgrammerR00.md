Copyright © 2020 Pearson Education, Inc. 2Ed

## 记忆时间

## 卡片

### 0101. 主题卡 —— 

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡 —— 

根据反常识，再补充三个证据 —— 就产生三张术语卡。

### 0202. 术语卡 —— 

### 0203. 术语卡 —— 

### 0301. 人名卡 —— 

根据这些证据和案例，找出源头和提出术语的人是谁 —— 产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 —— 

最后根据他写的非常震撼的话语 —— 产生一张金句卡。

### 0501. 任意卡 —— 

最后还有一张任意卡，记录个人阅读感想。

Copyright © 2020 Pearson Education, Inc.

内容简介：《程序员修炼之道》之所以在全球范围内广泛传播，被一代代开发者奉为圭臬，盖因它可以创造出真正的价值：或编写出更好的软件，或探究出编程的本质，而所有收获均不依赖于特定语言、框架和方法。时隔 20 年的新版，经过全面的重新选材、组织和编写，覆盖哲学、方法、工具、设计、解耦、并发、重构、需求、团队等务实话题的最佳实践及重大陷阱，以及易于改造、复用的架构技术。本书极具洞察力与趣味性，适合从初学者到架构师的各阶层读者潜心研读或增广见闻。

## Foreword

I remember when Dave and Andy first tweeted about the new edition of this book. It was big news. I watched as the coding community responded with excitement. My feed buzzed with anticipation. After twenty years, The Pragmatic Programmer is just as relevant today as it was back then.

It says a lot that a book with such history had such a reaction. I had the privilege of reading an unreleased copy to write this foreword, and I understood why it created such a stir. While it's a technical book, calling it that does it a disservice. Technical books often intimidate. They're stuffed with big words, obscure terms, convoluted examples that, unintentionally, make you feel stupid. The more experienced the author, the easier it is to forget what it's like to learn new concepts, to be a beginner.

Despite their decades of programming experience, Dave and Andy have conquered the difficult challenge of writing with the same excitement of people who've just learned these lessons. They don't talk down to you. They don't assume you are an expert. They don't even assume you've read the first edition. They take you as you are—programmers who just want to be better. They spend the pages of this book helping you get there, one actionable step at a time.

To be fair, they'd already done this before. The original release was full of tangible examples, new ideas, and practical tips to build your coding muscles and develop your coding brain that still apply today. But this updated edition makes two improvements on the book.

1『重点来了，2 大改进。』

The first is the obvious one: it removes some of the older references, the out-of-date examples, and replaces them with fresh, modern content. You won't find examples of loop invariants or build machines. Dave and Andy have taken their powerful content and made sure the lessons still come through, free of the distractions of old examples. It dusts off old ideas like DRY (don't repeat yourself) and gives them a fresh coat of paint, really making them shine.

But the second is what makes this release truly exciting. After writing the first edition, they had the chance to reflect on what they were trying to say, what they wanted their readers to take away, and how it was being received. They got feedback on those lessons. They saw what stuck, what needed refining, what was misunderstood. In the twenty years that this book has made its way through the hands and hearts of programmers all over the world, Dave and Andy have studied this response and formulated new ideas, new concepts.

They've learned the importance of agency and recognized that developers have arguably more agency than most other professionals. They start this book with the simple but profound message:「it's your life.」It reminds us of our own power in our code base, in our jobs, in our careers. It sets the tone for everything else in the book—that it's more than just another technical book filled with code examples.

What makes it truly stand out among the shelves of technical books is that it understands what it means to be a programmer. Programming is about trying to make the future less painful. It's about making things easier for our teammates. It's about getting things wrong and being able to bounce back. It's about forming good habits. It's about understanding your toolset. Coding is just part of the world of being a programmer, and this book explores that world.

I spend a lot of time thinking about the coding journey. I didn't grow up coding; I didn't study it in college. I didn't spend my teenage years tinkering with tech. I entered the coding world in my mid-twenties and had to learn what it meant to be a programmer. This community is very different from others I'd been a part of. There is a unique dedication to learning and practicality that is both refreshing and intimidating.

For me, it really does feel like entering a new world. A new town, at least. I had to get to know the neighbors, pick my grocery store, find the best coffee shops. It took a while to get the lay of the land, to find the most efficient routes, to avoid the streets with the heaviest traffic, to know when traffic was likely to hit. The weather is different, I needed a new wardrobe.

The first few weeks, even months, in a new town can be scary. Wouldn't it be wonderful to have a friendly, knowledgeable neighbor who'd been living there a while? Who can give you a tour, show you those coffee shops? Someone who'd been there long enough to know the culture, understand the pulse of the town, so you not only feel at home, but become a contributing member as well? Dave and Andy are those neighbors.

As a relative newcomer, it's easy to be overwhelmed not by the act of programming but the process of becoming a programmer. There is an entire mindset shift that needs to happen—a change in habits, behaviors, and expectations. The process of becoming a better programmer doesn't just happen because you know how to code; it must be met with intention and deliberate practice. This book is a guide to becoming a better programmer efficiently.

But make no mistake—it doesn't tell you how programming should be. It's not philosophical or judgmental in that way. It tells you, plain and simple, what a Pragmatic Programmer is—how they operate, and how they approach code. They leave it up to you to decide if you want to be one. If you feel it's not for you, they won't hold it against you. But if you decide it is, they're your friendly neighbors, there to show you the way.

— Saron Yitbarek | Founder & CEO of CodeNewbie | Host of Command Line Heroes

我还记得 Dave 和 Andy 第一次在推特上谈论这本书的新版的那一刻 —— 这可是一条大新闻。在编程社区，所见之处都是对这条大新闻兴奋的回应，人们的期待塞满了我的信息流。二十年过去了，《程序员修炼之道》这本书的地位不逊于当年。

承载这样一段历史的一本书，能引起这样的反响，本身就说明了很多问题。为了写这篇序，我有幸在尚未出版前阅读了本书，读后我就明白了它为什么会引起这么大的轰动。本来，一本书被冠以技术图书之名，给人的印象应该是不太好的。因为技术图书常常令人生畏 —— 充斥着深奥的词汇、晦涩的术语和令人费解的例子，不经意间就会让你觉得自己很愚蠢。而且，作者越有经验，就越容易忘记初学者在学习新概念时的感觉。

Dave 和 Andy 的作品，却能透出那种只有刚刚学到这些课程的人才会有的兴奋感，尽管他们已有几十年的编程经验，却战胜了写出这种感觉的挑战。他们不会居高临下地指指点点，不会假定你是个专家，甚至不认为你已读过本书第一版，仅仅把你当成想要变得更好的程序员而已。他们不惜用整本书的篇幅来帮助你达到目标，一步一个脚印。

公平地说，在这方面，他们在过往已经成绩斐然。最初的本书第一版，包含了许多具体的例子、新想法和实用的技巧，可以帮助你修炼编程所需的「肌肉」和「大脑」，这些东西到今天仍然适用。但是，这次在新版图书中，又有了两项改进。

第一项显而易见：删除了一些较老的引用内容和过时的例子，增补了大量新鲜、现代的内容。循环不变式或构建机这样的例子已经看不到了。Dave 和 Andy 保留了第一版书中的重要内容，以确保相应的课程依然有效，而且读者也不必受旧示例的干扰。对于像 DRY（不要重复自己）这样的旧思想，上面的灰尘已被掸去，并且涂上了一层新油漆 —— 这样做真的让其熠熠生辉。

而第二项，才是这次新版图书发布真正令人兴奋的地方。在写完本书第一版后，他们有机会思考自己想要说什么，想让读者获得什么，以及读者是如何接受这些信息的。他们得到了这些课程的反馈，也看到了读者在哪里被卡住、有什么需要改进，以及哪些内容被误解。在这本书通过全世界程序员的双手和心灵传播的二十年间，Dave 和 Andy 研究了这些回应，并且形成了新的想法和理念。

他们认识到自主权的重要性，并且意识到，相比大多数其他专业人员，开发者或许更能为自己做主。他们以简单而深刻的启示开始这本书：「人生是你的。」这唤起了我们自己的力量，它就蕴含在我们的代码库、工作和职业生涯中。这也为本书的其他内容定下了基调 —— 它不仅仅是又一本充满代码示例的技术图书。

这本书必定会在摆满各种技术图书的书架上脱颖而出，因为它理解身为一名程序员到底意味着什么。编程关涉诸事 —— 尽量减少未来的痛苦，让队友更轻松，做错事情后能够重新振作起来，养成良好的习惯，以及理解工具集。编程只是程序员世界的一部分，而这本书探索了整个世界。

我在思考编码之旅上花了很多时间。我不是从小就开始接触编程的，大学里也没学过编程课。可以说，我的青少年时光并没有花在「摆弄」科技上，直到二十来岁的时候才进入了编程的世界，因而亟须想明白一件事情：成为一名程序员意味着什么。编程社区与我曾经身处的其他社区非常不同。其独特之处在于，人们无不醉心于学习和实践，这既令人生畏，又让人耳目一新。

这对我来说，真像进入一个全新的世界。就算去到一个新城镇，也有必要了解邻居、挑选杂货店、找到最好的咖啡店。我花了一段时间来了解地形，找到了最有效的路线，避开了交通最繁忙的街道，并且知道了什么时候交通可能会出问题。等到天气变化，我又要去置办应季的新衣。

来到一个新城镇的头几周，甚至是头几个月，可能会很害怕。如果有一个已经在这里住了一段时间的邻居，而且他知识渊博又友好，那不是再好不过的事情吗？谁能带你四处参观，谁能领你去那些咖啡店？当然是一个在当地待了足够长时间的，了解当地文化、当地脉搏的人。这样你不仅有家的感觉，还能成为一个同样有贡献的成员。Dave 和 Andy 就是这样的邻居。

一个准新人，更容易对成为程序员的过程，而不是对编程的行为不知所措。因此，必须对整个心态做一次切换 —— 改变习惯、行为和期望。仅仅知道如何编程，并不会让你成为一名更好的程序员，在这个过程中必须经历有意识和深思熟虑的实践。好在现在有了这本书，可以有效地指导你成为更好的程序员。

但不要搞错了 —— 这本书不会告诉你编程应该是怎样的，它并没有使用那种哲学或审判的方式，它只是简单、明了地告诉你，什么是务实的程序员 —— 他们如何操作、如何处理代码。作者让你自己决定是否想成为其中的一员。如果你觉得不适合，也没有人会怪罪你。但如果你决定成为其中的一员，作者就是你的友好邻居，会陪伴左右、为你指路。

Saron Yitbarek

CodeNewbie 创始人及 CEOCommand Line Heroes 主办者

## Preface to the Second Edition

Back in the 1990s, we worked with companies whose projects were having problems. We found ourselves saying the same things to each: maybe you should test that before you ship it; why does the code only build on Mary's machine? Why didn't anyone ask the users?

To save time with new clients, we started jotting down notes. And those notes became The Pragmatic Programmer. To our surprise the book seemed to strike a chord, and it has continued to be popular these last 20 years. But 20 years is many lifetimes in terms of software. Take a developer from 1999 and drop them into a team today, and they'd struggle in this strange new world. But the world of the 1990s is equally foreign to today's developer. The book's references to things such as CORBA, CASE tools, and indexed loops were at best quaint and more likely confusing.

At the same time, 20 years has had no impact whatsoever on common sense. Technology may have changed, but people haven't. Practices and approaches that were a good idea then remain a good idea now. Those aspects of the book aged well.

So when it came time to create this 20th Anniversary Edition, we had to make a decision. We could go through and update the technologies we reference and call it a day. Or we could reexamine the assumptions behind the practices we recommended in the light of an additional two decades' worth of experience. In the end, we did both. 

As a result, this book is something of a Ship of Theseus.[1] Roughly one-third of the topics in the book are brand new. Of the rest, the majority have been rewritten, either partially or totally. Our intent was to make things clearer, more relevant, and hopefully somewhat timeless.

We made some difficult decisions. We dropped the Resources appendix, both because it would be impossible to keep up-to-date and because it's easier to search for what you want. We reorganized and rewrote topics to do with concurrency, given the current abundance of parallel hardware and the dearth of good ways of dealing with it. We added content to reflect changing attitudes and environments, from the agile movement which we helped launch, to the rising acceptance of functional programming idioms and the growing need to consider privacy and security.

Interestingly, though, there was considerably less debate between us on the content of this edition than there was when we wrote the first. We both felt that the stuff that was important was easier to identify. Anyway, this book is the result. Please enjoy it. Maybe adopt some new practices. Maybe decide that some of the stuff we suggest is wrong. Get involved in your craft. Give us feedback. But, most important, remember to make it fun.

在 20 世纪 90 年代，我们在与一些项目存在问题的公司合作时，发现总是在对每个人说同样的话：也许你应该在发布之前先测试一下。为什么代码只能在 Mary 的机器上构建？为什么没有人问一下用户呢？

为了节省与新客户打交道的时间，我们开始做笔记。这些笔记最终变成了《程序员修炼之道》这本书。令人惊讶的是，这本书似乎引起了大家的共鸣，在过去的二十年间，这本书一直很受欢迎。

但是二十年对于软件领域来说已经过了好几代。如果一个开发者从 1999 年直接穿越到今天的团队中，面对这个陌生的新世界一定会备感挣扎。但 20 世纪 90 年代的世界对今天的开发者来说同样陌生。书中所引用的 CORBA、CASE 工具，以及索引、循环这些东西，放在今天，充其量不过略显古雅有趣，而更多的会给人带来困扰。

与此同时，二十年对常识没有丝毫影响。技术可能改变了，但人没有。实践和方法中的闪光点，在今天看来光芒依旧。在这些方面，本书保鲜如初。

所以，当我们要出版这本二十周年纪念版的时候，必须做出抉择 —— 是回顾和更新前一版中引用的技术后就大功告成，还是充分借鉴这平添的二十年丰富经验，重新审视前一版所推崇的实践背后的种种假设。

最终，我们两者都做了。

因此，这本书有点像忒修斯之船。书中大约三分之一的主题是全新的，而其余的大部分都被部分或全部重写了。我们的目的是，让内容变得更清晰、更贴切，并在某种程度上不受时间的影响。

我们做了一些艰难的决定。删除了参考资料附录，这样做既因为它无法持续更新，也因为当你有此需要时很容易就能搜索获得。我们重新组织了与并发有关的主题，这是因为考虑到当前有着大量的并行硬件，却缺乏处理并行的好方法。我们还添加了一些内容来反映不断变化的认知和环境，从我们帮助发起的敏捷运动，到对函数式编程语境的日益接受，再到对隐私和安全性方面日益增长的需求。

然而有趣的是，我们之间关于版本内容的争论比写第一个版本时要少得多。重要的东西更容易辨别，这已是我们的共识。

无论如何，这本书最后就是这个样子了，请享用吧。你也许可以从中吸取一些新的做法，也许会觉得我们建议的某些东西是错的，不妨把它们都带到你的工作中去，然后给我们反馈。

但是，最重要的是，记住过程要开心。

### 01. How the Book Is Organized

This book is written as a collection of short topics. Each topic is self-contained, and addresses a particular theme. You'll find numerous cross references, which help put each topic in context. Feel free to read the topics in any order—this isn't a book you need to read front-to-back.

Occasionally you'll come across a box labeled Tip nn (such as Tip 1, Care About Your Craft). As well as emphasizing points in the text, we feel the tips have a life of their own—we live by them daily. You'll find a summary of all the tips on a pull-out card inside the back cover.

We've included exercises and challenges where appropriate. Exercises normally have relatively straightforward answers, while the challenges are more open-ended. To give you an idea of our thinking, we've included our answers to the exercises in an appendix, but very few have a single correct solution. The challenges might form the basis of group discussions or essay work in advanced programming courses.

There's also a short bibliography listing the books and articles we explicitly reference.

这本书是如何组织的

这本书是许多短小主题的合集。每一个主题都针对特定的话题而独立成章。你会发现大量的交叉引用，这有助于把各个主题连贯起来。你可以以任意次序随意阅读这些主题 —— 这不是一本需要从头到尾阅读的书。

偶尔你会看到一个写有提示 n 的框起来的标签块（比如位于第 XVII 页的提示 1：关注你的技艺）。这些提示不仅是文中的重点，在我们眼里也是一条条生命 —— 我们每天都赖以为生。

我们已尽可能适时地在书中加入了练习和挑战。练习通常有相对简单的答案，而挑战则更加开放。为了让你理解我们的思维方式，在附录里我们列出了这些练习的答案，但是拥有唯一正确答案的问题并不多。挑战或许能用于高级编程课程中的小组讨论，或许能作为论文写作的基础。

本书还有一个简短的参考文献，列出了我们明确引用的图书和文章。

### 02. What's in a Name?

Scattered throughout the book you'll find various bits of jargon—either perfectly good English words that have been corrupted to mean something technical, or horrendous made-up words that have been assigned meanings by computer scientists with a grudge against the language. The first time we use each of these jargon words, we try to define it, or at least give a hint to its meaning. However, we're sure that some have fallen through the cracks, and others, such as object and relational database, are in common enough usage that adding a definition would be boring. If you do come across a term you haven't seen before, please don't just skip over it. Take time to look it up, perhaps on the web, or maybe in a computer science textbook. And, if you get a chance, drop us an email and complain, so we can add a definition to the next edition.

Having said all this, we decided to get revenge against the computer scientists. Sometimes, there are perfectly good jargon words for concepts, words that we've decided to ignore. Why? Because the existing jargon is normally restricted to a particular problem domain, or to a particular phase of development.

However, one of the basic philosophies of this book is that most of the techniques we're recommending are universal: modularity applies to code, designs, documentation, and team organization, for instance. When we wanted to use the conventional jargon word in a broader context, it got confusing—we couldn't seem to overcome the baggage the original term brought with it. When this happened, we contributed to the decline of the language by inventing our own terms.

1『关键知识：modularity applies to code, designs, documentation, and team organization. 』

名字有什么含义

「我用一个词，」矮胖子相当傲慢地说，「总是同我想要说的恰如其分的，既不重，也不轻。」

—— 路易斯·卡罗《爱丽丝镜中奇遇》

在整本书中，你会发现各种各样的行话 —— 要么原本是完好的英语单词，却被曲解为技术词，要么是一些可怕的合成词，由那些对语言充满怨恨的计算机科学家赋予其意义。当我们第一次使用这些行话时，会尝试定义它们，或者至少对其含义给出解释。当然，肯定还有漏网之鱼，而且像对象和关系型数据库这种已被广泛使用的，再下一次定义就有点画蛇添足了。如果你遇到一个以前没见过的术语，请不要跳过它，不妨花点时间去查一下，可以在网上查，也可以在计算机科学的课本上查。如果有机会还可以给我们发邮件投诉，这样我们就可以在本书下一版中增加一个定义。

既然话已至此，我们决定报复一下计算机科学家。有时候，明明有一些非常好的术语，对某个概念表达得很好，但我们却决定不使用这些术语。为什么？因为现有的术语通常局限于特定的问题领域，或者特定的开发阶段。而本书的基本哲学之一就是，我们推荐的大多数技术都是通用的：例如模块化，它就能同时适用于代码、设计、文档和团队组织。当某个传统术语被拿来在更广泛的场景下使用时，却会造成困惑 —— 我们似乎无法摆脱该术语从最初就开始背负的历史包袱。当这种情况发生时，我们只好发明自己的术语，助纣为虐地让语言继续堕落。

### 03. Source Code and Other Resources

Most of the code shown in this book is extracted from compilable source files, available for download from our website.[2] There you'll also find links to resources we find useful, along with updates to the book and news of other Pragmatic Programmer developments.

[1] If, over the years, every component of a ship is replaced as it fails, is the resulting vessel the same ship?

[2] https://pragprog.com/titles/tpp20

### 04. Send Us Feedback

We'd appreciate hearing from you. Email us at

ppbook@pragprog.com.

## From the Preface to the First Edition

This book will help you become a better programmer. You could be a lone developer, a member of a large project team, or a consultant working with many clients at once. It doesn't matter; this book will help you, as an individual, to do better work. This book isn't theoretical—we concentrate on practical topics, on using your experience to make more informed decisions. The word pragmatic comes from the Latin pragmaticus—「skilled in business」—which in turn is derived from the Greek πραγματικός, meaning「fit for use.」

This is a book about doing.

Programming is a craft. At its simplest, it comes down to getting a computer to do what you want it to do (or what your user wants it to do). As a programmer, you are part listener, part advisor, part interpreter, and part dictator. You try to capture elusive requirements and find a way of expressing them so that a mere machine can do them justice. You try to document your work so that others can understand it, and you try to engineer your work so that others can build on it. What's more, you try to do all this against the relentless ticking of the project clock. You work small miracles every day.

It's a difficult job.

There are many people offering you help. Tool vendors tout the miracles their products perform. Methodology gurus promise that their techniques guarantee results. Everyone claims that their programming language is the best, and every operating system is the answer to all conceivable ills.

Of course, none of this is true. There are no easy answers. There is no best solution, be it a tool, a language, or an operating system. There can only be systems that are more appropriate in a particular set of circumstances.

This is where pragmatism comes in. You shouldn't be wedded to any particular technology, but have a broad enough background and experience base to allow you to choose good solutions in particular situations. Your background stems from an understanding of the basic principles of computer science, and your experience comes from a wide range of practical projects.

Theory and practice combine to make you strong. You adjust your approach to suit the current circumstances and environment. You judge the relative importance of all the factors affecting a project and use your experience to produce appropriate solutions. And you do this continuously as the work progresses. Pragmatic Programmers get the job done, and do it well.

本书将帮助你成为更好的程序员。

不论你是独立开发者，还是大型项目团队的一员，或是同时与许多客户共事的顾问，都无所谓。本书旨在告诉你，作为个体如何更好地完成工作。这本书不是理论书 —— 我们专注于实践的话题，利用经验来做出更明智的决定。务实（Pragmatic）这个词来自拉丁语 pragmaticus ——「精通业务」，该词又来源于希腊语 πραγματικός，意思是「适合使用」。

这是一本关于实干的书。

编程是一门技艺。简单地说，就是让计算机做你想让它做的事情（或是你的用户想让它做的事情）。作为一名程序员，你既在倾听，又在献策；既是传译，又行独裁；你试图捕获难以捉摸的需求，并找到一种表达它们的方式，以便仅靠一台机器就可以从容应付。你试着把工作记录成文档，以便他人理解；你试着将工作工程化，这样别人就能在其上有所建树；更重要的是，你试图在项目时钟的滴答声中完成所有这些工作。你每天都在创造小小的奇迹。

编程是一项艰难的工作。

想帮你的人可不少 —— 工具供应商在吹嘘他们家产品所创造出的奇迹，方法论大师承诺他们的技术可以为结果做出保证，每个人都声称他们用的编程语言是最好的，每个操作系统都自诩包治百病。

当然，这些都不是真的，哪有什么简单的答案。没有最好的解决方案，无论是工具、语言还是操作系统；只在特定的环境下才有所谓更合适的系统。

这就让务实主义有了用武之地。你不应该拘泥于任何特定的技术，而应该拥有足够广泛的背景和经验基础，以便在特定的情况下选择合适的解决方案。你的背景来自对计算机科学基本原理的理解，而你的经验来自广泛的实际项目。理论结合实践会让你变得强大。

调整方法去适应当前的情况和环境。对所有影响项目因素的相对重要性做出判断，并通过经验找到适当的解决方案。随着工作的进展，你要不断地这样做。务实的程序员不仅把工作做完，并且做得很好。

### 01. Who Should Read This Book?

This book is aimed at people who want to become more effective and more productive programmers. Perhaps you feel frustrated that you don't seem to be achieving your potential. Perhaps you look at colleagues who seem to be using tools to make themselves more productive than you. Maybe your current job uses older technologies, and you want to know how newer ideas can be applied to what you do.

We don't pretend to have all (or even most) of the answers, nor are all of our ideas applicable in all situations. All we can say is that if you follow our approach, you'll gain experience rapidly, your productivity will increase, and you'll have a better understanding of the entire development process. And you'll write better software.

谁应该读这本书

本书的目标读者是那些希望成为更高效、多产的程序员的人。也许你现在感到沮丧，因为似乎没能发挥自己的潜力；也许你已经注意到，有些同事似乎正在利用工具让自己的效率比你更高；也许你在现在的工作中使用的是较老的技术，你想知道如何为工作引入新的想法。

我们不会假装拥有所有（或是绝大部分）的答案，也不会假装我们的每个想法都适用于所有情况。我们只能说，如果你遵循我们的方法，你将快速获得经验、提高生产力，并且更好地理解整个开发过程。最终，你会写出更好的软件。

### 02. What Makes a Pragmatic Programmer? 

Each developer is unique, with individual strengths and weaknesses, preferences and dislikes. Over time, each will craft their own personal environment. That environment will reflect the programmer's individuality just as forcefully as his or her hobbies, clothing, or haircut. However, if you're a Pragmatic Programmer, you'll share many of the following characteristics: 

1 Early adopter/fast adapter. You have an instinct for technologies and techniques, and you love trying things out. When given something new, you can grasp it quickly and integrate it with the rest of your knowledge. Your confidence is born of experience.

2 Inquisitive. You tend to ask questions. That's neat—how did you do that? Did you have problems with that library? What's this quantum computing I've heard about? How are symbolic links implemented? You are a pack rat for little facts, each of which may affect some decision years from now.

3 Critical thinker. You rarely take things as given without first getting the facts. When colleagues say「because that's the way it's done,」or a vendor promises the solution to all your problems, you smell a challenge.

4 Realistic. You try to understand the underlying nature of each problem you face. This realism gives you a good feel for how difficult things are, and how long things will take. Deeply understanding that a process should be difficult or will take a while to complete gives you the stamina to keep at it.

5 Jack of all trades. You try hard to be familiar with a broad range of technologies and environments, and you work to keep abreast of new developments. Although your current job may require you to be a specialist, you will always be able to move on to new areas and new challenges.

We've left the most basic characteristics until last. All Pragmatic Programmers share them. They're basic enough to state as tips: 

Tip 1: Care About Your Craft. 

We feel that there is no point in developing software unless you care about doing it well.

Tip 2: Think! About Your Work.

In order to be a Pragmatic Programmer, we're challenging you to think about what you're doing while you're doing it. This isn't a one-time audit of current practices—it's an ongoing critical appraisal of every decision you make, every day, and on every project. Never run on auto-pilot. Constantly be thinking, critiquing your work in real time. The old IBM corporate motto, THINK! , is the Pragmatic Programmer's mantra.

If this sounds like hard work to you, then you're exhibiting the realistic characteristic. This is going to take up some of your valuable time—time that is probably already under tremendous pressure. The reward is a more active involvement with a job you love, a feeling of mastery over an increasing range of subjects, and pleasure in a feeling of continuous improvement. Over the long term, your time investment will be repaid as you and your team become more efficient, write code that's easier to maintain, and spend less time in meetings.

是什么造就了务实的程序员

每个开发人员都是独特的，有各自的优势和劣势，以及偏好和厌恶的东西。诚如随着时间的推移，每个人都将打造自己的个人环境。这种环境将像程序员的爱好、衣服或发型一样，能强烈地反映出他或她的个性。然而，作为务实的程序员，你们会共有许多如下特征：

早期的采纳者 / 快速的适配者

你对技术和技巧有一种直觉，喜欢尝试。当接触到新东西时，你可以很快地掌握它们，并把它们与其他的知识结合起来。你的信心来自经验。

好奇

你倾向于问问题。这真不错 —— 你怎么做到的？你对那个库有意见吗？总在听人说起的量子计算到底是什么？符号链接是怎么实现的？你热衷于收集各种细微的事实，坚信它们会影响自己多年后的决策。

批判性的思考者

你在没有得到证实前很少接受既定的现实。当同事们说「因为就该这么做」，或者供应商承诺会解决所有的问题时，你会闻到挑战的味道。

现实主义

你试图理解所面临的每个问题的本质。这种现实主义让你对事情有多困难、需要用多长时间有一个很好的感知。一个过程应该很难，或是需要点时间才能完成，对这些的深刻理解，给了你坚持下去的毅力。

多面手

你努力熟悉各种技术和环境，并努力跟上新的进展。虽然目前的工作可能要求你在某个专门领域成为行家，但你总是能够进入新的领域，迎接新的挑战。

我们把最基本的特征留到最后。所有务实的程序员都有这个特征。它足够基本，完全可以作为提示来加以声明。

提示 1 关注你的技艺

我们觉得，如果你不关心怎么把软件开发好，那么软件开发领域就再也没什么好谈的事情了。

提示 2 思考！思考你的工作

为了成为一名务实的程序员，我们要求你在做事的时候，思考一下自己正在做什么。这不是对当前实践做的一次性审计 —— 而是对每天里每一个项目所做的每一个决定进行的批判性评估。不要用自动辅助驾驶系统偷懒，而是要不断地思考，即时地批判自己的工作。IBM 公司的座右铭「思考！」，实属每个务实程序员的真言。

如果你觉得这听起来很困难，那么你就表现出了现实主义的特征。这会占用你一些宝贵的时间 —— 可能是已经处于巨大压力之下的时间。当然会有回报，你能更积极地投入喜欢的工作，对越来越多的学科有掌控感，对不断进步产生愉悦感。从长期来看，时间投资将得到回报，因为你和你的团队将变得更高效，能编写出更容易维护的代码，并且在会议上花的时间更少。

### 03. Individual Pragmatists, Large Teams

Some people feel that there is no room for individuality on large teams or complex projects.「Software is an engineering discipline,」they say,「that breaks down if individual team members make decisions for themselves.」

We strongly disagree.

There should be engineering in software construction. However, this doesn't preclude individual craftsmanship. Think about the large cathedrals built in Europe during the Middle Ages. Each took thousands of person-years of effort, spread over many decades. Lessons learned were passed down to the next set of builders, who advanced the state of structural engineering with their accomplishments. But the carpenters, stonecutters, carvers, and glass workers were all craftspeople, interpreting the engineering requirements to produce a whole that transcended the purely mechanical side of the construction. It was their belief in their individual contributions that sustained the projects: We who cut mere stones must always be envisioning cathedrals.

Within the overall structure of a project there is always room for individuality and craftsmanship. This is particularly true given the current state of software engineering. One hundred years from now, our engineering may seem as archaic as the techniques used by medieval cathedral builders seem to today's civil engineers, while our craftsmanship will still be honored.

务实的个体，大型的团队

有些人认为在大型团队或复杂的项目中没有个性的空间。「软件是一门工程学科，」他们说，「如果团队成员个体自行其是，软件就会崩溃。」

我们强烈反对这种看法。

诚然，软件构造有工程的成分。然而，这并不妨碍个体的技艺。想想中世纪在欧洲建造的大教堂，每一座都需要数千人年的努力，时间跨度长达几十年。从中吸取的经验教训被传递给下一代的建造者，最终一代代累积的造诣推动了结构工程的发展。而木匠、石匠、雕刻师和玻璃工人都是手工艺人 —— 通过吃透工程要求，其创造所体现出的整体水准，已远超建筑中纯机械的部分。正是他们对个人贡献的信念支撑着这些项目：我们，采集的只是石头，却必须始终展望着未来的大教堂。

在一个项目的整体结构中，总有个性和技艺的空间。考虑到软件工程的当前状态，这一点尤为正确。今天的土木工程师，很难接受中世纪大教堂建造者使用的技术 —— 百年后我们的工程看上去也一样古老，而我们的技艺仍将受到尊重。

### 04. It's a Continuous Process

A tourist visiting England's Eton College asked the gardener how he got the lawns so perfect.「That's easy,」he replied,「You just brush off the dew every morning, mow them every other day, and roll them once a week.」

「Is that all?」asked the tourist.「Absolutely,」replied the gardener.「Do that for 500 years and you'll have a nice lawn, too.」

Great lawns need small amounts of daily care, and so do great programmers. Management consultants like to drop the word kaizen in conversations.「Kaizen」is a Japanese term that captures the concept of continuously making many small improvements. It was considered to be one of the main reasons for the dramatic gains in productivity and quality in Japanese manufacturing and was widely copied throughout the world.

Kaizen applies to individuals, too. Every day, work to refine the skills you have and to add new tools to your repertoire. Unlike the Eton lawns, you'll start seeing results in a matter of days.

Over the years, you'll be amazed at how your experience has blossomed and how your skills have grown.

这是一个连续的过程

一位游客在参观英格兰伊顿公学时，询问园丁是如何把草坪修剪得如此完美的。「那很简单，」园丁回答说，「你只要每天早上拂去露水，隔天修剪一次，一周再滚压一次就行了。」

「就是这些吗？」游客问。「就这些，」园丁回答，「这样做上五百年，你也会有一片漂亮的草坪。」

伟大的草坪需要每天的点滴护理，伟大的程序员也是如此。管理顾问喜欢在谈话中抛出「改善」（Kaizen）这个词。「改善」是一个日语术语，意思是不断地做出许多小的改进。这被认为是日本制造业生产率和质量大幅提高的主要原因之一，并被全世界广泛效仿。改善也适用于个人。每一天都要努力打磨你的技能，并往技能库里添加新的工具。与伊顿草坪不同，你会在几天内就看到效果。几年下来，你会对成果惊讶不已 —— 经验业已开花结果，技能早就茁壮成长。

## Praise for the second edition of The Pragmatic Programmer

Some say that with The Pragmatic Programmer, Andy and Dave captured lightning in a bottle; that it's unlikely anyone will soon write a book that can move an entire industry as it did. Sometimes, though, lightning does strike twice, and this book is proof. The updated content ensures that it will stay at the top of「best books in software development」lists for another 20 years, right where it belongs.

— VM (Vicky) Brasseur | Director of Open Source Strategy, Juniper Networks

If you want your software to be easy to modernize and maintain, keep a copy of The Pragmatic Programmer close. It's filled with practical advice, both technical and professional, that will serve you and your projects well for years to come.

— Andrea Goulet | CEO, Corgibytes; Founder, LegacyCode.Rocks

The Pragmatic Programmer is the one book I can point to that completely dislodged the existing trajectory of my career in software and pointed me in the direction of success. Reading it opened my mind to the possibilities of being a craftsman, not just a cog in a big machine. One of the most significant books in my life.

— Obie Fernandez | Author, The Rails Way 

First-time readers can look forward to an enthralling induction into the modern world of software practice, a world that the first edition played a major role in shaping. Readers of the first edition will rediscover here the insights and practical wisdom that made the book so significant in the first place, expertly curated and updated, along with much that's new.

— David A. Black | Author, The Well-Grounded Rubyist

I have an old paper copy of the original Pragmatic Programmer on my bookshelf. It has been read and re-read and a long time ago it changed everything about how I approached my job as a programmer. In the new edition everything and nothing has changed: I now read it on my iPad and the code examples use modern programming languages—but the underlying concepts, ideas, and attitudes are timeless and universally applicable. Twenty years later, the book is as relevant as ever. It makes me happy to know that current and future developers will have the same opportunity to learn from Andy and Dave's profound insights as I did back in the day.

— Sandy Mamoli | Agile coach, author of How Self-Selection Lets People Excel Twenty years ago, the first edition of The Pragmatic

Programmer completely changed the trajectory of my career. This new edition could do the same for yours.

— Mike Cohn | Author of Succeeding with Agile, Agile Estimating and Planning, and User Stories Applied 

这样的赞美一直不绝于耳：通过撰写一本书来推动整个行业，是 Andy 和 Dave 用《程序员修炼之道：从小工到专家》完成的一大壮举，无人可以超越。然而，有时两次闪电的确会击中同一个地方，这部名著的再版即为明证。其令人震撼的内容更新，足以确保自身在未来二十年里继续雄踞「精选软件开发图书」榜单之首，此可谓实至名归。

—— VM（Vicky）Brasseur 瞻博网络开源战略总监

如果想让自己的软件既领先于时代又易于维护，就在手边摆放一本《程序员修炼之道：通向务实的最高境界（第 2 版）》。本书充满实用建议，有技术方面的，也有专业方面的，无不能让你和你的项目受益多年。

—— Andrea GouletCorgibytes 公司 CEOLegacyCode.Rocks 创始人

可以说，《程序员修炼之道》完全改变了我的职业轨迹，为我指明了软件领域的成功方向。正是这本书，开阔了我的视野，让我意识到自己不仅仅是庞大机器上的一枚齿轮，有朝一日也能藉由修炼成为匠师。它是我生命中最重要的一本书。

—— Obie Fernandez《Rails 之道》作者

初读此书的读者，在见识到那个软件开发实践的新世界时，立刻充满期待。而第一版图书，对塑造这样一个迷人的现代世界，的确厥功至伟。现在，第一版的读者将有机会在新版中重温旧梦，再次接受洞察力和实践智慧的洗礼，而《程序员修炼之道》当初正因此被奉为圭臬。更重要的是，经由两位专家亲手组织与更新的再版图书，业已因富含新知而重焕青春。

—— David A.Black《Ruby 程序员修炼之道》作者

旧版的《程序员修炼之道》一直驻留在我的书架上。从很久以前它改变我作为一个程序员的工作方式那一刻起，我读了又读。在这个全新的版本中，一切似乎都已改变，而一切又仿佛还在那里。虽然我们现在换用 iPad 阅读新版，其代码示例也改由现代编程语言实现 —— 但是蕴藏其中的概念、思想和态度，亘古不变且通行宇宙。二十年过去，这本书的价值从未折损。现在乃至将来的开发人员，都有机会从 Andy 和 Dave 的深刻洞见中获益，正如当年的我一样，这让人备感欣慰。

—— Sandy Mamoli 敏捷教练 How Self-Selection Lets People Excel 作者

二十年前，《程序员修炼之道》的第一版彻底颠覆了我的技术生涯。这次的新版，也将对你有此影响。

—— Mike Cohn《Scrum 敏捷软件开发》《敏捷估计与规划》《用户故事与敏捷方法》作者
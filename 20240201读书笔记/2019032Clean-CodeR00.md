## 记忆时间

原书出版时间：2008 年。

## 卡片

### 0101. 主题卡 ——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡 ——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 数据信息卡 ——

### 0601. 任意卡 ——

最后还有一张任意卡，记录个人阅读感想。

## Robert C. Martin Series

The mission of this series is to improve the state of the art of software craftsmanship. The books in this series are technical, pragmatic, and substantial. The authors are highly experienced craftsmen and professionals dedicated to writing about what actually works in practice, as opposed to what might work in theory. You will read about what the author has done, not what he thinks you should do. If the book is about programming, there will be lots of code. If the book is about managing, there will be lots of case studies from real projects.

These are the books that all serious practitioners will have on their bookshelves. These are the books that will be remembered for making a difference and for guiding professionals to become true craftsman.

Managing Agile Projects 

Sanjiv Augustine

Agile Estimating and Planning 

Mike Cohn

Working Effectively with Legacy Code 

Michael C. Feathers

Agile Java™: Crafting Code with Test-Driven Development 

Jeff Langr

Agile Principles, Patterns, and Practices in C# 

Robert C. Martin and Micah Martin

Agile Software Development: Principles, Patterns, and Practices 

Robert C. Martin

Clean Code: A Handbook of Agile Software Craftsmanship 

Robert C. Martin

UML For Java™ Programmers 

Robert C. Martin

Fit for Developing Software: Framework for Integrated Tests 

Rick Mugridge and Ward Cunningham

Agile Software Development with SCRUM 

Ken Schwaber and Mike Beedle

Extreme Software Engineering: A Hands on Approach 

Daniel H. Steinberg and Daniel W. Palmer

For more information, visit informit.com/martinseries

## 内容提要

软件质量，不但依赖于架构及项目管理，而且与代码质量紧密相关。这一点，无论是敏捷开发流派还是传统开发流派，都不得不承认。

本书提出一种观念：代码质量与其整洁度成正比。干净的代码，既在质量上较为可靠，也为后期维护、升级奠定了良好基础。作为编程领域的佼佼者，本书作者给出了一系列行之有效的整洁代码操作实践。这些实践在本书中体现为一条条规则（或称「启示」），并辅以来自现实项目的正、反两面的范例。只要遵循这些规则，就能编写出干净的代码，从而有效提升代码质量。

本书阅读对象为一切有志于改善代码质量的程序员及技术经理。书中介绍的规则均来自作者多年的实践经验，涵盖从命名到重构的多个编程方面，虽为一「家」之言，然诚有可资借鉴的价值。

## Foreword

One of our favorite candies here in Denmark is Ga-Jol, whose strong licorice vapors are a perfect complement to our damp and often chilly weather. Part of the charm of Ga-Jol to us Danes is the wise or witty sayings printed on the flap of every box top. I bought a two-pack of the delicacy this morning and found that it bore this old Danish saw:

Ærlighed i små ting er ikke nogen lille ting .

「Honesty in small things is not a small thing.」It was a good omen consistent with what I already wanted to say here. Small things matter. This is a book about humble concerns whose value is nonetheless far from small.

God is in the details , said the architect Ludwig mies van der Rohe. This quote recalls contemporary arguments about the role of architecture in software development, and particularly in the Agile world. Bob and I occasionally find ourselves passionately engaged in this dialogue. And yes, mies van der Rohe was attentive to utility and to the timeless forms of building that underlie great architecture. On the other hand, he also personally selected every doorknob for every house he designed. Why? Because small things matter.

In our ongoing「debate」on TDD, Bob and I have discovered that we agree that software architecture has an important place in development, though we likely have different visions of exactly what that means. Such quibbles are relatively unimportant, however, because we can accept for granted that responsible professionals give some time to thinking and planning at the outset of a project. The late-1990s notions of design driven only by the tests and the code are long gone. Yet attentiveness to detail is an even more critical foundation of professionalism than is any grand vision. First, it is through practice in the small that professionals gain proficiency and trust for practice in the large. Second, the smallest bit of sloppy construction, of the door that does not close tightly or the slightly crooked tile on the floor, or even the messy desk, completely dispels the charm of the larger whole. That is what clean code is about.

Still, architecture is just one metaphor for software development, and in particular for that part of software that delivers the initial product in the same sense that an architect delivers a pristine building. In these days of Scrum and Agile, the focus is on quickly bringing product to market. We want the factory running at top speed to produce software. These are human factories: thinking, feeling coders who are working from a product backlog or user story to create product . The manufacturing metaphor looms ever strong in such thinking. The production aspects of Japanese auto manufacturing, of an assembly-line world, inspire much of Scrum.

Yet even in the auto industry, the bulk of the work lies not in manufacturing but in maintenance — or its avoidance. In software, 80% or more of what we do is quaintly called「maintenance」: the act of repair. Rather than embracing the typical Western focus on producing good software, we should be thinking more like home repairmen in the building industry, or auto mechanics in the automotive field. What does Japanese management have to say about that ?

In about 1951, a quality approach called Total Productive Maintenance (TPM) came on the Japanese scene. Its focus is on maintenance rather than on production. One of the major pillars of TPM is the set of so-called 5S principles. 5S is a set of disciplines — and here I use the term「discipline」instructively. These 5S principles are in fact at the foundations of Lean — another buzzword on the Western scene, and an increasingly prominent buzzword in software circles. These principles are not an option. As Uncle Bob relates in his front matter, good software practice requires such discipline: focus, presence of mind, and thinking. It is not always just about doing, about pushing the factory equipment to produce at the optimal velocity. The 5S philosophy comprises these concepts:

1 Seiri , or organization (think「sort」in English). Knowing where things are — using approaches such as suitable naming — is crucial. You think naming identifiers isn't important? Read on in the following chapters.

2 Seiton , or tidiness (think「systematize」in English). There is an old American saying: A place for everything, and everything in its place . A piece of code should be where you expect to find it — and, if not, you should re-factor to get it there.

3 Seiso , or cleaning (think「shine」in English): Keep the workplace free of hanging wires, grease, scraps, and waste. What do the authors here say about littering your code with comments and commented-out code lines that capture history or wishes for the future? Get rid of them.

4 Seiketsu , or standardization: The group agrees about how to keep the workplace clean. Do you think this book says anything about having a consistent coding style and set of practices within the group? Where do those standards come from? Read on.

5 Shutsuke , or discipline ( self -discipline). This means having the discipline to follow the practices and to frequently reflect on one's work and be willing to change.

If you take up the challenge — yes, the challenge — of reading and applying this book, you'll come to understand and appreciate the last point. Here, we are finally driving to the roots of responsible professionalism in a profession that should be concerned with the life cycle of a product. As we maintain automobiles and other machines under TPM, breakdown maintenance — waiting for bugs to surface — is the exception. Instead, we go up a level: inspect the machines every day and fix wearing parts before they break, or do the equivalent of the proverbial 10,000-mile oil change to forestall wear and tear. In code, refactor mercilessly. You can improve yet one level further, as the TPM movement innovated over 50 years ago: build machines that are more maintainable in the first place. Making your code readable is as important as making it executable. The ultimate practice, introduced in TPM circles around 1960, is to focus on introducing entire new machines or replacing old ones. As Fred Brooks admonishes us, we should probably re-do major software chunks from scratch every seven years or so to sweep away creeping cruft. Perhaps we should update Brooks' time constant to an order of weeks, days or hours instead of years. That's where detail lies.

There is great power in detail, yet there is something humble and profound about this approach to life, as we might stereotypically expect from any approach that claims Japanese roots. But this is not only an Eastern outlook on life; English and American folk wisdom are full of such admonishments. The Seiton quote from above flowed from the pen of an Ohio minister who literally viewed neatness「as a remedy for every degree of evil.」How about Seiso? Cleanliness is next to godliness . As beautiful as a house is, a messy desk robs it of its splendor. How about Shutsuke in these small matters? He who is faithful in little is faithful in much . How about being eager to re-factor at the responsible time, strengthening one's position for subsequent「big」decisions, rather than putting it off? A stitch in time saves nine . The early bird catches the worm. Don't put off until tomorrow what you can do today. (Such was the original sense of the phrase「the last responsible moment」in Lean until it fell into the hands of software consultants.) How about calibrating the place of small, individual efforts in a grand whole? Mighty oaks from little acorns grow. Or how about integrating simple preventive work into everyday life? An ounce of prevention is worth a pound of cure. An apple a day keeps the doctor away. Clean code honors the deep roots of wisdom beneath our broader culture, or our culture as it once was, or should be, and can be with attentiveness to detail.

Even in the grand architectural literature we find saws that hark back to these supposed details. Think of mies van der Rohe's doorknobs. That's seiri . That's being attentive to every variable name. You should name a variable using the same care with which you name a first-born child.

As every homeowner knows, such care and ongoing refinement never come to an end. The architect Christopher Alexander — father of patterns and pattern languages — views every act of design itself as a small, local act of repair. And he views the craftsmanship of fine structure to be the sole purview of the architect; the larger forms can be left to patterns and their application by the inhabitants. Design is ever ongoing not only as we add a new room to a house, but as we are attentive to repainting, replacing worn carpets, or upgrading the kitchen sink. Most arts echo analogous sentiments. In our search for others who ascribe God's home as being in the details, we find ourselves in the good company of the 19th century French author Gustav Flaubert. The French poet Paul Valery advises us that a poem is never done and bears continual rework, and to stop working on it is abandonment. Such preoccupation with detail is common to all endeavors of excellence. So maybe there is little new here, but in reading this book you will be challenged to take up good disciplines that you long ago surrendered to apathy or a desire for spontaneity and just「responding to change.」

Unfortunately, we usually don't view such concerns as key cornerstones of the art of programming. We abandon our code early, not because it is done, but because our value system focuses more on outward appearance than on the substance of what we deliver. This inattentiveness costs us in the end: A bad penny always shows up . Research, neither in industry nor in academia, humbles itself to the lowly station of keeping code clean. Back in my days working in the Bell Labs Software Production Research organization ( Production , indeed!) we had some back-of-the-envelope findings that suggested that consistent indentation style was one of the most statistically significant indicators of low bug density. We want it to be that architecture or programming language or some other high notion should be the cause of quality; as people whose supposed professionalism owes to the mastery of tools and lofty design methods, we feel insulted by the value that those factory-floor machines, the coders, add through the simple consistent application of an indentation style. To quote my own book of 17 years ago, such style distinguishes excellence from mere competence. The Japanese worldview understands the crucial value of the everyday worker and, more so, of the systems of development that owe to the simple, everyday actions of those workers. Quality is the result of a million selfless acts of care — not just of any great method that descends from the heavens. That these acts are simple doesn't mean that they are simplistic, and it hardly means that they are easy. They are nonetheless the fabric of greatness and, more so, of beauty, in any human endeavor. To ignore them is not yet to be fully human.

Of course, I am still an advocate of thinking at broader scope, and particularly of the value of architectural approaches rooted in deep domain knowledge and software usability. The book isn't about that — or, at least, it isn't obviously about that. This book has a subtler message whose profoundness should not be underappreciated. It fits with the current saw of the really code-based people like Peter Sommerlad, Kevlin Henney and Giovanni Asproni.「The code is the design」and「Simple code」are their mantras. While we must take care to remember that the interface is the program, and that its structures have much to say about our program structure, it is crucial to continuously adopt the humble stance that the design lives in the code. And while rework in the manufacturing metaphor leads to cost, rework in design leads to value. We should view our code as the beautiful articulation of noble efforts of design — design as a process, not a static endpoint. It's in the code that the architectural metrics of coupling and cohesion play out. If you listen to Larry Constantine describe coupling and cohesion, he speaks in terms of code — not lofty abstract concepts that one might find in UML. Richard Gabriel advises us in his essay,「Abstraction Descant」that abstraction is evil. Code is anti-evil, and clean code is perhaps divine.

Going back to my little box of Ga-Jol, I think it's important to note that the Danish wisdom advises us not just to pay attention to small things, but also to be honest in small things. This means being honest to the code, honest to our colleagues about the state of our code and, most of all, being honest with ourselves about our code. Did we Do our Best to「leave the campground cleaner than we found it」? Did we re-factor our code before checking in? These are not peripheral concerns but concerns that lie squarely in the center of Agile values. It is a recommended practice in Scrum that re-factoring be part of the concept of「Done.」Neither architecture nor clean code insist on perfection, only on honesty and doing the best we can. To err is human; to forgive, divine. In Scrum, we make everything visible. We air our dirty laundry. We are honest about the state of our code because code is never perfect. We become more fully human, more worthy of the divine, and closer to that greatness in the details.

In our profession, we desperately need all the help we can get. If a clean shop floor reduces accidents, and well-organized shop tools increase productivity, then I'm all for them. As for this book, it is the best pragmatic application of Lean principles to software I have ever seen in print. I expected no less from this practical little group of thinking individuals that has been striving together for years not only to become better, but also to gift their knowledge to the industry in works such as you now find in your hands. It leaves the world a little better than I found it before Uncle Bob sent me the manuscript.

Having completed this exercise in lofty insights, I am off to clean my desk.

James O. Coplien Mørdrup, Denmark

序言

乐嚼（Ga-Jol）是在丹麦最受欢迎的糖果品种之一，它浓郁的甘草味道，完美地弥补了此地潮湿且时常寒冷的天气。对于我们这些丹麦人，乐嚼的妙处还在于包装盒顶上印制的哲言慧语。今早我买了一包两件装，在其包装盒上发现这句丹麦谚语：

「小处诚实非小事。」这句话正好是我想在这里说的。以小见大。本书写到了一些价值殊胜的小主题。

神在细节之中，建筑师 Ludwig mies van der Rohe（路徳维希·密斯·范·徳·罗）如是说。这句话引发了有关软件开发、特别是敏捷软件开发中架构所处地位的若干争论。鲍勃（Bob）2 和我时常发现自己沉湎于此类对话中。没错，Ludwig mies van der Rohe 的确专注于效用和基于宏伟架构之上的永恒建筑形式。然而，他也为自己设计的每所房屋挑选每个门把手。为什么？因为小处见大。

就 TDD 话题展开目前仍在继续的「辩论」时，鲍勃和我认识到，我们均同意软件架构在开发中占据重要地位，但就其确切意义而言，我们之间还有分歧。然而，这种矛与盾孰利的讨论相对而言并不重要，因为在项目开始之时，我们理所当然应该让专业人士投入些许时间去思考及规划。20 世纪 90 年代末期有关仅以测试和代码驱动设计的概念已一去不返。相对于任何宏伟愿景，对细节的关注甚至是更为关键的专业性基础。首先，开发者通过小型实践获得可用于大型实践的技能和信用度。其次，宏大建筑中最细小的部分，比如关不紧的门、有点儿没铺平的地板，甚至是凌乱的桌面，都会将整个大局的魅力毁灭殆尽。这就是整洁代码之所系。

架构只是软件开发用到的借喻之一，主要用在那种等同于建筑师交付毛坯房一般交付初始软件产品的场合。在 Scrum 和敏捷（Agile）的日子里，人们关注的是快速将产品推向市场。我们要求工厂全速运转、生产软件。这就是人类工厂：懂思考、会感受的编码人，他们由产品备忘或用户故事开始创造产品。来自制造业的借喻在这种场合大行其道。例如，Scrum 就从装配线式的日本汽车生产方式中获益良多。

1 译注：20 世纪中期著名现代建筑大师，乗承「少即是多」的建筑设计哲学，缔造了玻璃幕墙等现代建筑结构。

2 译注：本书主要作者 Robert C. Martin 绰号 Uncle Bob，这里的「鲍勃」及后文的「鲍勃大叔」就是指 Robert C. Martin。

3 译注：Test Driven Development，测试驱动开发。

即便是在汽车工业里，大量工作也并不在于生产而在于维护 —— 或避免维护。对于软件而言，百分之八十或更多的工作量集中在我们美其名曰「维护」的事情上：其实就是修修补补。与其接受西方关于制造好软件的传统看法，不如将其看作建筑工业中的房屋修理工，或者汽车领域的汽修工。日本式管理对于这种事怎么说的呢？

大约在 1951 年，一种名为「全员生产维护」（Total Productive Maintenance, TPM）的质量保证手段在日本出现。它关注维护甚于关注生产。TPM 的主要支柱之一是所谓的 5S 原则体系。5S 是一套规程，用「规程」这个词，是为了读者便于理解。5S 原则其实是精益（Lean）西方视野中的一个时髦词，也是在软件领域渐领风骚的时耄词 一一 的基石所在。正如鲍勃大叔（Uncle Bob）在前言中写到的，良好的软件实践遵循这些规程：专注、镇定和思考。这并非总只有关实作，有关推动工厂设备以最高速度运转。5S 哲学包括以下概念：

1、整理（Seiri），或谓组织「想想英语中的 sort（分类、排序）一词」。搞清楚事物之所在通过恰当地命名之类的手段一至关重要。觉得命名标识无关紧要？读读后面的章节吧。

2、整顿（Seiton），或谓整齐「想想英文中的 systematize（系统化）一词」。有句美国老话说：物皆有其位，而后物尽归其位（A place for everything, and everything in its place）。每段代码都该在你希望它所在的地方 一一 如果不在那里，就需要重构了。

3、清楚（Seiso），或谓清洁「想想英文中的 shine（锃亮）一词」。清理工作地的拉线、油污和边角废料。对于那种四处遗弃的带注释的代码及反映过往或期望的无注释代码，本书作者怎么说的来着？除之而后快。

4、清洁（Seiketsu），或谓标准化。有关如何保持工作地清洁的组内共识。本书有没有提到在开发组内使用一贯的代码风格和实践手段？这些标准从哪里来？读读看。

5、身美（Shitsuke），或谓纪律（自律）。在实践中贯彻规程，并时时体现于个人工作上，而且要乐于改进。

如果你接受挑战 —— 没错，就是挑战，阅读并应用本书，你就会理解和赞赏上述最后一条。我们最终是在驶向一种负责任的专业精神之根源所在，这种专业性隶属于一个关注产品生命周期的专业领域。在我们遵循 TPM 来维护机动车和其他机械时，停机维护 ー一 等待缺陷显现出来 一一 并不常见。我们更上一层楼：每天检査机械，在磨损机件停止工作之前就换它，或者按常例每 1000 英里（约 16093km）就更换润滑油、防止磨损和开裂。对于代码，应无情地做重构。还可以更进一步，就像 TPM 运动在 50 多年前的创新：一开始就打造更易维护的机械。写出可读的代码，重要程度不亚于写出可执行的代码。1960 年左右，围绕 TPM 引入的终极实践（ultimate practice），关注用全新机械替代旧机械。诚如 Fred Brooks 所言，我们或许应该每 7 年就重做一次软件的主要模块，清理慢陈腐的代码。也许我们该把重构周期从以年计缩短到以周、以天甚至以小时计。那便是细节所在了。

译注：这些概念最初出现于日本，5 个概念的日文罗马字拼音首字母正好都是 S，所以这里也保留了日文罗马字拼音写法。中译本以日文汉字直接译出，读者留意，不可直接对应其中文意思。

译注：中文意为「素养、教养」。

细节中自有天地，而在生活中应用此类手段时也有微言大义，就像我们一成不变地对那些源自日本的做法寄予厚望一般。这并非只是东方的生活观；英美民间也遍是这类警句。

上引「整顿」（Seiton）二字就曾出现在某位俄亥俄州牧师的笔下，他把齐整看作是「荡涤种种罪恶之良方」。「清楚」（Seiso）又如何呢？整洁近乎虔诚（Cleanliness is next to godliness）张脏乱的桌子足以夺去一所丽宅的光彩。老话怎么说「身美」（Shitsuke）的？守小节者不亏大节（He who is faithful in little is faithful in much）。对于时时准备在恰当时机做重构，为未来的「大」决定夯实基础，而不是置诸脑后，有什么说法吗？及时一针省九针（A stitch in time saves nine）。早起的鸟儿有虫吃（The early bird catches the worm）。日事日毕（Don' t put off until tomorrow what you can do today）。在精益实践落入软件咨询师之手前，这就是其所谓「最后时机」的本义所在。摆正单项工作在整体中的位置呢？巨木生于树（Mighty oaks from little acorns grow）。如何在日常生活中做好简单的防备性工作呢？防病好过治病（An ounce of prevention is worth a pound of cure）。一天一苹果，医生远离我（An apple a day keeps the doctor away）。整洁代码以其对细节的关注，荣耀了深埋于我们现有、或曾有、或该有的壮丽文化之下的智慧根源。

即便是在宏伟的建筑作品中，我们也听到关注细节的回响。想想 Ludwig mies van der Rohe 的门把手吧。那正是整理（sei）。认真对待每个变量名。你当用为自己第一个孩子命名般的谨慎来给变量命名。

正如每位房主所知，此类照料和修葺永无止。建筑师 Christopher Alexander 模式与模式语言之父一把每个设计动作看作是较小的局部修复动作。他认为，设计良好结构才是建筑师的本职所在，而更大的建筑形态则当留给模式及居住者搬进的家私来完成。设计始终在持续进行，不只是在新建一个房间时，也在我们重新粉刷墙面、更换旧地毯或者换厨房水槽时。大多数艺术门类也持类似主张。在寻找其他推祟细节的人时，我们发现，19 世纪法国作家 Gustav Flaubert（古斯塔夫·福楼拜）名列其中。法国诗人 Paul Valery（保尔·瓦雷里）认为，每首诗歌都无写完之时，得持续重写，直至放弃为止。全心倾注于细节，屡见于追求卓越的行为之中。虽然这无甚新意，但阅读本书对读者仍是一种挑战，你要重拾久已弃置脑后的良好规则，自发自主，「响应改变」。

不幸的是，我们往往见不到人们把对细节的关注当作编程艺术的基础要件。我们过早地放弃了在代码上的工作，并不是因为它业已完成，而是因为我们的价值体系关注外在表现甚于关注要交付之物的本质。疏忽最终结出了恶果：坏东西一再出现。无论是在行业里还是学术领域，研究者都很重视代码的整洁问题。

供职于贝尔软件生产研究实验室（Bell Labs Software Production Research）—— 没错，就是生产！时，我们有些不太严密的发现，认为前后一致的缩进风格明显标志了较低的缺陷率。我们原指望将质量归因于架构、编程语言或者其他高级概念；我们的专业能力归功于对工具的掌握和各种高高在上的设计方法，至于那些安置于厂区的机器，那些编码者，他们居然通过简单地保持一致缩进风格创造了价值，这简直是一种侮辱。我在 17 年前就在书中写过，这种风格远不止是一种单纯的能力那么简单。日本式的世界观深知日常工作者的价值，而且，还深知工作者简单的日常行为所锻造的开发系统的价值。质量是上百万次全心投入的结果 一一 而非仅归功于任何来自天堂的伟大方法。这些行为简单却不简陋，也不意味着简易。相反，它们是人力所能达的不仅伟大而且美丽的造物。忽略它们，就不成其为完整的人。

当然，我仍然提倡放宽思路，也推祟根植于深厚领域知识和软件可用性的各种架构手法的价值。但本书与此无关一至少，没有明显关系。本书精妙之处，其意义之深远，不该无人赏识。它正与 Peter Sommerlad、Kevlin Henny 及 Giovanni Asproni：等真正写代码的人现今所持的观念相吻合。他们鼓吹「代码即设计」和「简单代码」。我们要谨记，界面就是程序，而且其结构也极大地反映出程序结构，但也理应始终谦逊地承认设计存在于代码中，这至关紧要。制造上的返工导致成本上升，但重做设计却创造出价值。我们应当视代码为设计 一一 作为过程而非终点的设计这种高尚行为的漂亮体现。耦合与内聚的架构韵律在代码中脉动。Larry Constantine 以代码的形式 一一 而不是用 UML 那种高高在上的抽象概念 —— 来描述耦合与内聚。Richard Garbriel 在「Abstraction Descant」（抽象刍议）一文中告诉我们，抽象即恶。代码除恶，而整洁的代码则大抵是圣洁的。

回到我那个小小的乐嚼包装盒，我想要重点提一下，那句丹麦谚语不只是教我们重视小处，更教我们小处要诚实。这意味着对代码诚实、对同僚坦承代码现状，最重要的是在代码问题上不自欺。是否已尽全「把露营地清理得比来时还干净」？签入代码前是否做重构？这可不是皮毛小事，它正高卧于敏捷价值的正中位置。Scrum 有一种建议的实践，主张重构是「完成」（Done）概念的一部分。无论是架构还是代码都不强求完美，只求竭诚尽力而已。人孰无过，神亦容之（To err is human; to forgive, divine）。在 Scrum 中，我们使一切可见。我们晾出脏衣服。我们坦承代码状态，因为它永不完美。我们日渐成为完整的人，配得起神的眷顾，也越来越接近细节中的伟大之处。

在自己的专业领域中，我们亟需能得到的一切帮助。假使干净的地板能减少事故发生，假使归置到位的工具能提升生产力，我也会倾力做到。至于本书，在我看过的有关将精益原则应用于软件的印刷品中，是最具实用性的。那班求索者多年来并肩奋斗，不但是为求一己之进步，更将他们的知识通过和你手上正在做的事一般的工作贡献给这个行业。看过鲍勃大叔寄来的原稿之后，我发现，世界竟略有改善了。

对高瞻远瞩的练习业已结束，我要去清理自己的书桌了。

## Introduction

Which door represents your code? Which door represents your team or your company? Why are we in that room? Is this just a normal code review or have we found a stream of horrible problems shortly after going live? Are we debugging in a panic, poring over code that we thought worked? Are customers leaving in droves and managers breathing down our necks? How can we make sure we wind up behind the right door when the going gets tough? The answer is: craftsmanship .

There are two parts to learning craftsmanship: knowledge and work. You must gain the knowledge of principles, patterns, practices, and heuristics that a craftsman knows, and you must also grind that knowledge into your fingers, eyes, and gut by working hard and practicing.

I can teach you the physics of riding a bicycle. Indeed, the classical mathematics is relatively straightforward. Gravity, friction, angular momentum, center of mass, and so forth, can be demonstrated with less than a page full of equations. Given those formulae I could prove to you that bicycle riding is practical and give you all the knowledge you needed to make it work. And you'd still fall down the first time you climbed on that bike.

Coding is no different. We could write down all the「feel good」principles of clean code and then trust you to do the work (in other words, let you fall down when you get on the bike), but then what kind of teachers would that make us, and what kind of student would that make you?

No. That's not the way this book is going to work.

Learning to write clean code is hard work . It requires more than just the knowledge of principles and patterns. You must sweat over it. You must practice it yourself, and watch yourself fail. You must watch others practice it and fail. You must see them stumble and retrace their steps. You must see them agonize over decisions and see the price they pay for making those decisions the wrong way.

Be prepared to work hard while reading this book. This is not a「feel good」book that you can read on an airplane and finish before you land. This book will make you work, and work hard . What kind of work will you be doing? You'll be reading code — lots of code. And you will be challenged to think about what's right about that code and what's wrong with it. You'll be asked to follow along as we take modules apart and put them back together again. This will take time and effort; but we think it will be worth it.

We have divided this book into three parts. The first several chapters describe the principles, patterns, and practices of writing clean code. There is quite a bit of code in these chapters, and they will be challenging to read. They'll prepare you for the second section to come. If you put the book down after reading the first section, good luck to you!

The second part of the book is the harder work. It consists of several case studies of ever-increasing complexity. Each case study is an exercise in cleaning up some code — of transforming code that has some problems into code that has fewer problems. The detail in this section is intense . You will have to flip back and forth between the narrative and the code listings. You will have to analyze and understand the code we are working with and walk through our reasoning for making each change we make. Set aside some time because this should take you days .

The third part of this book is the payoff. It is a single chapter containing a list of heuristics and smells gathered while creating the case studies. As we walked through and cleaned up the code in the case studies, we documented every reason for our actions as a heuristic or smell. We tried to understand our own reactions to the code we were reading and changing, and worked hard to capture why we felt what we felt and did what we did. The result is a knowledge base that desribes the way we think when we write, read, and clean code.

This knowledge base is of limited value if you don't do the work of carefully reading through the case studies in the second part of this book. In those case studies we have carefully annotated each change we made with forward references to the heuristics. These forward references appear in square brackets like this: [H22]. This lets you see the context in which those heuristics were applied and written! It is not the heuristics themselves that are so valuable, it is the relationship between those heuristics and the discrete decisions we made while cleaning up the code in the case studies .

To further help you with those relationships, we have placed a cross-reference at the end of the book that shows the page number for every forward reference. You can use it to look up each place where a certain heuristic was applied.

If you read the first and third sections and skip over the case studies, then you will have read yet another「feel good」book about writing good software. But if you take the time to work through the case studies, following every tiny step, every minute decision — if you put yourself in our place, and force yourself to think along the same paths that we thought, then you will gain a much richer understanding of those principles, patterns, practices, and heuristics. They won't be「feel good」knowledge any more. They'll have been ground into your gut, fingers, and heart. They'll have become part of you in the same way that a bicycle becomes an extension of your will when you have mastered how to ride it.

前言

你的代码在哪道门后面？你的团队或公司在哪道门后面？为什么会在那里？只是一次普通的代码复査，还是产品面世后オ发现一连串严重问题？我们是否在战战兢兢地调试自己之前错以为没问题的代码？客户是否在流失？经理们是否把我们盯得如芒刺在背？当事态变得严重起来，如何保证我们在那道正确的门后做补救工作？答案是：技艺（craftsmanship）。

习艺之要有二：知和行。你应当习得有关原则、模式和实践的知识，穷尽应知之事，并且要对其了如指掌，通过刻苦实践掌握它。

我可以教你骑自行车的物理学原理。实际上，经典数学的表达方式相对而言确实简洁明了。重力、摩擦力、角动量、质心等，用一页写满方程式的纸就能说明白。有了这些方程式，我可以为你证明出骑车完全可行，而且还可以告诉你骑车所需的全部知识。即便如此，你在初次骑车时还是会跌倒在地。

编码亦同此理。我们可以写下整洁代码的所有「感觉良好」的原则，放手让你去干（换言之，让你从自行车上摔下来）。那样的话，我们算是哪门子老师？而你又会成为怎样的学生呢？

不！本书可不会这么做。

学写整洁代码很难。它可不止于要求你掌握原则和模式。你得在这上面花工夫。你须自行实践，且体验自己的失败。你须观察他人的实践与失败。你须看看别人是怎样蹒跚学步，再转头研究他们的路数。你须看看别人是如何绞尽脑汁做出决策，又是如何为错误决策付出代价。

阅读本书要多用心思。这可不是那种降落前就能读完的「感觉不错」的飞机书。本书要让你用功，而且是非常用功。如何用功？阅读代码一大量代码。而且你要去琢磨某段代码好在什么地方、坏在什么地方。在我们分解，而后组合模块时，你得亦步亦趋地跟上。这得花些工夫，不过值得一试。

本书大致可分为 3 个部分。前几章介绍编写整洁代码的原则、模式和实践。这部分有相当多的示例代码，读起来颇具挑战性。读完这几章，就为阅读第 2 部分做好了准备。如果你就此止步，只能祝你好运啦！

第 2 部分最需要花工夫。这部分包括几个复杂性不断增加的案例研究。每个案例都清理些代码把有问题的代码转化为问题少一些的代码。这部分极为详细。你的思维要在讲解和代码段之间跳来跳去。你得分析和理解那些代码，琢磨每次修改的来龙去脉。

你付出的劳动将在第 3 部分得到回报。这部分只有一章，列出从上述案例研究中得到的启示和灵感。在遍览和清理案例中的代码时，我们把每个操作理由记录为一种启示或灵感。我们尝试去理解自己对阅读和修改代码的反应，尽力了解为什么会有这样的感受、为什么会如此行事。结果得到了一套描述在编写、阅读、清理代码时思维方式的知识库。

如果你在阅读第 2 部分的案例研究时没有好好用功，那么这套知识库对你来说可能所值无几。在这些案例研究中，每次修改都仔细注明了相关启示的标号。这些标号用方括号标出，如：[H22]。由此你可以看到这些启示在何种环境下被应用和编写。启示本身不值钱，启示与案例研究中清理代码的具体决策之间的关系才有价值。

如果你跳过案例研究部分，只阅读了第 1 部分和第 3 部分，那就不过是又看了一本关于写出好软件的「感觉不错」的书。但如果你肯花时间琢磨那些案例，亦步亦趋 一一 站在作者的角度，迫使自己以作者的思维路径考虑问题，就能更深刻地理解这些原则、模式、实践和启示。这样的话，就像一个熟练地掌握了骑车的技术后，自行车就如同其身体的延伸部分那样；对你来说，本书所介绍的整洁代码的原则、模式、实践和启示就成为了本身具有的技艺，而不再是「感觉不错」的知识。

## Acknowledgments

Thank you to my two artists, Jeniffer Kohnke and Angela Brooks. Jennifer is responsible for the stunning and creative pictures at the start of each chapter and also for the portraits of Kent Beck, Ward Cunningham, Bjarne Stroustrup, Ron Jeffries, Grady Booch, Dave Thomas, Michael Feathers, and myself.

Angela is responsible for the clever pictures that adorn the innards of each chapter. She has done quite a few pictures for me over the years, including many of the inside pictures in Agile Software Develpment: Principles, Patterns, and Practices . She is also my firstborn in whom I am well pleased.

A special thanks goes out to my reviewers Bob Bogetti, George Bullock, Jeffrey Overbey, and especially Matt Heusser. They were brutal. They were cruel. They were relentless. They pushed me hard to make necessary improvements.

Thanks to my publisher, Chris Guzikowski, for his support, encouragement, and jovial countenance. Thanks also to the editorial staff at Pearson, including Raina Chrobak for keeping me honest and punctual.

Thanks to Micah Martin, and all the guys at 8th Light ( www.8thlight.com ) for their reviews and encouragement.

Thanks to all the Object Mentors, past, present, and future, including: Bob Koss, Michael Feathers, Michael Hill, Erik Meade, Jeff Langr, Pascal Roy, David Farber, Brett Schuchert, Dean Wampler, Tim Ottinger, Dave Thomas, James Grenning, Brian Button, Ron Jeffries, Lowell Lindstrom, Angelique Martin, Cindy Sprague, Libby Ottinger, Joleen Craig, Janice Brown, Susan Rosso, et al.

Thanks to Jim Newkirk, my friend and business partner, who taught me more than I think he realizes. Thanks to Kent Beck, Martin Fowler, Ward Cunningham, Bjarne Stroustrup, Grady Booch, and all my other mentors, compatriots, and foils. Thanks to John Vlissides for being there when it counted. Thanks to the guys at Zebra for allowing me to rant on about how long a function should be.

And, finally, thank you for reading these thank yous.

## On the Cover

The image on the cover is M104: The Sombrero Galaxy. M104 is located in Virgo and is just under 30 million light-years from us. At it's core is a supermassive black hole weighing in at about a billion solar masses.

Does the image remind you of the explosion of the Klingon power moon Praxis ? I vividly remember the scene in Star Trek VI that showed an equatorial ring of debris flying away from that explosion. Since that scene, the equatorial ring has been a common artifact in sci-fi movie explosions. It was even added to the explosion of Alderaan in later editions of the first Star Wars movie.

What caused this ring to form around M104? Why does it have such a huge central bulge and such a bright and tiny nucleus? It looks to me as though the central black hole lost its cool and blew a 30,000 light-year hole in the middle of the galaxy. Woe befell any civilizations that might have been in the path of that cosmic disruption.

Supermassive black holes swallow whole stars for lunch, converting a sizeable fraction of their mass to energy. E = MC 2 is leverage enough, but when M is a stellar mass: Look out! How many stars fell headlong into that maw before the monster was satiated? Could the size of the central void be a hint?

The image of M104 on the cover is a combination of the famous visible light photograph from Hubble (right), and the recent infrared image from the Spitzer orbiting observatory (below, right). It's the infrared image that clearly shows us the ring nature of the galaxy. In visible light we only see the front edge of the ring in silhouette. The central bulge obscures the rest of the ring.

But in the infrared, the hot particles in the ring shine through the central bulge. The two images combined give us a view we've not seen before and imply that long ago it was a raging inferno of activity.

Cover image: © Spitzer Space Telescope

## 代码猴子与童子军军规

2007 年 3 月，我在 SD West 2007 技术大会上聆听了 Robert C. Martin（鲍勃大叔）的主题演讲「Craftsmanship and the Problem of Productivity: Secrets for Going Fast without Making a Mess」，一身体闲打扮的鲍勃大叔，以一曲嘲笑低水平编码者的 Code Monkey（代码猴子）开场。

是的，我们就是一群代码猴子，上蹿下跳，自以为领略了编程的真谛。可惜，当我们抓着几个酸桃子，得意洋洋坐到树枝上，却对自己造成的混乱熟视无睹。那堆「可以运行」的乱麻程序，就在我们的眼皮底下慢慢腐坏。

从听到那场以 TDD 为主题的演讲之后，我就一直关注鲍勃大叔，还有他在 TDD 和整洁代码方面的言论。去年，人民邮电出版社计算机分社拿一本书给我看，封面上赫然写着 Robert C. Martin 的大名。看完原书序和前言，我已经按捺不住，接下了翻译此书的任务。这本书名为 Clean Code，乃是 Object Mentor（鲍勃大叔开办的技术咨询和培训公司）一干大牛在编程方面的经验累积。按鲍勃大叔的话来说，就是「Object Mentor 整洁代码派」的说明。

正如 Coplien 在序中所言，宏大建筑中最细小的部分，比如关不紧的门、有点儿没铺平的地板，甚至是凌乱的桌面，都会将整个大局的魅力毁灭殆尽。这就是整洁代码之所系。Coplien 列举了许多谚语，证明整洁的价值，中国也有修身齐家治国平天下之语。整洁代码的重要性毋庯置疑，问题是如何写出真正整洁的代码。

本书既是整洁代码的定义，亦是如何写出整洁代码的指南。鲍勃大叔认为，「写整洁代码，需要遵循大量的小技巧，贯彻刻苦习得的整洁感」。这种「代码感就是关键所在…… 它不仅让我们看到代码的优劣，还予我们以借戒规之化劣为优的攻略。」作者阐述了在命名、函数、注释、代码格式、对象和数据结构、错误处理、边界问题、单元测试、类、系统、并发编程等方面如何做到整洁的经验与最佳实践。长期遵照这些经验编写代码，所谓「代码感」也就自然而然滋生出来。更有价值的部分是鲍勃大叔本人对 3 个 Java 项目的剖析与改进过程的实操记录。通过这多达 3 章的重构记录，鲍勃大叔充分地证明了童子军军规在编程领域同样适用：离开时要比发现时更整洁。为了向读者呈现代码的原始状态，这部分代码及本书其他部分的绝大多数代码注释都不做翻译。如果读者有任何疑问，可通过邮件与我沟通（cleancode.cn@gmail.com）。

接触开发技术十多年以来，特别是从事 IT 技术媒体工作六年以来，我见过许多对于代码整洁性缺乏足够重视的开发者。不算过分地说，这是职业素养与基本功的双重缺陷。我翻译 The Elements of C# Style（中译版《C# 编程风格》）和本书，实在也是希望在这方面看到开发者重视度和实际应用的提升。

在本书的结束语中，鲍勃大叔提到别人给他的一条腕带，上面的字样是 Test Obsessed（沉迷测试）。鲍勃大叔「发现自己无法取下腕带。不仅是因为腕带很紧，而且那也是条精神上的紧箍咒。… 它一直提醒我，我做了写出整洁代码的承诺。」有了这条腕带，代码猴子成了模范童子军。我想，每位开发者都需要这样一条腕带吧？
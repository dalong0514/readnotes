## 记忆时间

## 卡片

### 0001. 反常识卡 —— 硬件既是硬的也是软的

常识：硬件，如晶体管，是物理的实体对象，硬的，怎么会是软的呢。

反常识：硬件既是硬的也是软的。

信息源自「Hardware Is Ephemeral」

Steven Connor, professor of modern literature and theory at Birkbeck, University of London, credits the French philosopher Michel Serres, now a Professor of French at Stanford, with developing a subtle and beautiful theory of「the hard and the soft.」Serres' thesis, according to Connor, is woven throughout his prolific writings, many of which have not been translated into English. Connor comments that it is difficult to quote Serres, so I will quote Connor instead:

[T] he contrast between the hard and the soft refers to this distinction between the domain of nature, the object of attention of what we call the「hard sciences,」and the domain of culture. The hard means the given, as opposed to the made. It means the physical, as opposed to the conceptual. It means hardware as opposed to software. It means object as opposed to idea, form as opposed to information, world as opposed to word. (Connor, 2009)

Connor finds allusions in Serres' writings to an astonishing array of oppositions between hard and soft, including body and language, science and humanities, things and signs, physical and conceptual, object and idea, form and information, physics and language, a stone and a ghost, motors and information theory, the manual and the digital, sound and meaning, bridge and hyphen, energy and information, flesh and word, the real and the virtual, forces and codes, solids and geometry, objective and subjective, war and religion, a book and a story, or sound and music.

But Serres does not succumb to Platonicity, requiring a sharp delineation between the hard and the soft. Quite the contrary. According to Connor,

Serres's principal effort is to allow his reader to grasp [the] intermixture [of the hard and the soft.] … The hard can always evaporate into the soft, the soft calcify into the hard. (Connor, 2009)

In Serres' own words (translated from the French by Connor),

Hard things display a soft side; material, of course, they engram and programme themselves like software. There is software [logiciel] in the hardware [matériel]. (Serres, 2003, p. 73)

We then find the more subtle oppositions between the hard and the soft, such as wax and wax, nature and nature, ropes and ropes, or mathematics and mathematics. Each of these, depending on its role and use, can be either hard or soft.「Hardness in softness and softness in hardness,」according to Serres.

Following Serres, the three-word summary of this chapter would need to be「hardware and hardware.」Hardware is both hard and soft. I will argue that for an engineer who works with digital technology, hardware is merely an ephemeral expression of an idea, lasting longer than a spoken word, which vanishes from the room in a few milliseconds, but still ephemeral, in the grand scheme. The ideas articulated by the hardware, in contrast, although undoubtably mutating and evolving, can last a long time indeed. These ideas are expressed using layers of paradigms that shape and constrain the ideas in ways that even the designer of the hardware is not aware of.

In the rest of this chapter, I outline the layers of modeling used specifically for computer hardware. With apologies to the reader, I confess that the rest of this chapter is a bit of a nerd storm. If you are an impatient reader, or you have no interest in hardware, and you are willing to grant my basic thesis, then please feel free to skip reading the rest of this chapter.

My basic thesis is that the hardware of modern computers is far too complex to design directly. Layers of abstraction are essential, and except for the bottom layer, semiconductor physics, none of these layers is given to us by nature. They are all human constructions, paradigms in Kuhn's sense that frame our thinking about hardware design.

Moreover, I claim that these paradigms, despite having no physical form, are more durable than the hardware. Paradigm shifts are difficult for humans. They can also be quite costly because changes in technology paradigms can mean significant retooling. Software that supports design, such as hardware description languages and their compilers, may have to be redesigned with significant paradigm shifts. Even manufacturing plants may have to change.

Nevertheless, the layering of paradigms makes paradigm shifts easier than they would otherwise be. The design of a microprocessor, for example, often does not need to change when moving to a new semiconductor technology. The emphasis of this chapter is on how this layering of paradigms enables creativity and technological advances. In chapter 6 , I will explain how technological advances trigger paradigm shifts.

If you persist in reading this chapter, my primary goal is to show a reader with little or no prior exposure to electronics how the basic operations of an application such as Wikipedia are realized by transistors operating as switches. This explanation cannot be given all at once. It has to be built up in layers. Otherwise, the complexity is simply too much for the human brain. But starting from an abstraction of a single transistor as a switch, we quickly get to abstractions that when realized in a chip require thousands, millions, and billions of transistors. My goal is to show how these layered abstractions enable such scaling up.

史蒂文·康纳是伦敦大学伯克贝克学院现代文学和理论专业的教授，他认为斯坦福大学的法语教授、法国哲学家米歇尔·塞尔创立了一套精妙而漂亮的「硬和软」的理论。据康纳所说，塞尔的论题贯穿于他的多部作品之中，其中许多作品尚未被翻译成英文。康纳评论说，要引用塞尔的原文是有点儿难度的，所以我在这里就引用了康纳的一段文字：

「硬」和「软」的对比指的是自然领域和文化领域的区别，自然领域是我们所说的「硬科学」关注的对象。硬指的是给予的，而不是制造的。它指的是物质上的，而不是概念上的。它指的是硬件而不是软件。它指的是对象而不是想法，是形式而不是信息，是物理世界而不是文字。（康纳，2009）

康纳在塞尔的著作中发现了一系列令人吃惊的硬和软的经典对立情形，包括身体与语言、科学与人文、事物与符号、物理的与概念的、对象与想法、形式与信息、物理与语言、石头与鬼魂、发动机与信息论、手册与数字、声音与意义、桥梁与连字符、能量与信息、肉体与文字、真实与虚拟、力量与代码、立方体与几何学、客观与主观、战争与宗教、一本书与一个故事以及声音与音乐等等。

然而，塞尔并未屈从于柏拉图主义，那需要在硬和软之间有一个清晰的界限。恰恰相反，康纳表示：

塞尔的主要成就是，允许他的读者领悟（硬和软）是可以相互转换的…… 硬的总是能蒸发成软的，而软的也常常可以钙化为硬的。（康纳，2009 年）

塞尔在自己的著作中提道（康纳翻译自法语）：

硬的东西常常显示出软的一面；当然，材料本身就像软件一样可以被记忆和编程。硬件（法语 matériel）中有软件（法语 logiciel）。（塞尔，2003:73）

然后，我们又在硬和软之间发现了更为微妙的对立关系，例如，蜡和蜡、自然和自然、绳子和绳子，或者数学和数学。根据作用和用途的不同，上述例子中的每一方既可以是硬的，也可以是软的。按照塞尔的观点，「硬中有软，软中有硬」。

在塞尔的观点之后，我想简要地概括一下本章的内容 ——「硬件和硬件」，意思是硬件既是硬的也是软的。我要说的是，对于一个从事数字技术工作的工程师来说，硬件仅仅是一种思想的短暂表达，它的持续时间也许只稍稍长过一个几毫秒内就会从房间里消失的口语表达词语，但在宏大的计划中仍然是短暂的。相比之下，硬件所表达的思想，尽管总是处在不断的变化和演变之中，但确实可以持续很长的时间。这些思想是通过分层的范式来表达的。这些范式以设计者都不知道的方式形成和约束着这些思想。

2『硬件既是硬的也是软的，做一张反常识卡片。（2021-10-24）』—— 已完成

在本章的其余部分，我将概要阐述专门用于计算机硬件的建模层。感到抱歉的是，我承认本章后续内容会像一场技术呆子的头脑风暴。如果你是个急性子或者对硬件不感兴趣，并且同意我的基本论点，那么请直接跳过这部分内容。

我的基本论点是，现代计算机的硬件过于复杂，根本无法直接进行设计。因此，抽象层是必不可少的，除了最低层的半导体物理层之外，所有其他的层都不是大自然赋予我们的。它们都是人类构建的，是库恩所指意义上构建我们对硬件设计的思路的范式。

此外，我还想表明，尽管这些范式没有物理形式，却比硬件本身的生命力更持久。范式的转换对人类来说是一件十分困难的事情。它们也可能会有很高的代价，因为技术范式的转换可能意味着重大的重组。用以支持设计的软件，例如硬件描述语言及其编译器，可能必须被重新设计并进行重大的范式转换，甚至就连制造工厂也可能不得不进行改变。

尽管如此，范式的分层使得范式的转换比其他情况下的转换要更容易。例如，微处理器的设计在转向一种新的半导体技术时，通常不需要进行改变。本章的重点在于这种范式的分层是如何激发创造力和推动技术进步的。在第 6 章，我将进一步解释技术进步是如何引发范式转换的。

如果你坚持阅读本章的内容，那么我可以先告诉你我的主要目标是，向那些很少或根本没有接触过电子技术的读者展示诸如维基百科这样的一个应用程序是如何以晶体管为开关实现基本操作的。关于这个过程的解释不可能一下子就给出来，它必须是分层的。否则，人类大脑就要应对过于复杂的事物了。但是，从把单个晶体管抽象为一个开关开始，我们很快就得到了在芯片中实现时需要的成千上万、数百万和数十亿个晶体管的抽象。我的目标是向读者展示这些分层的抽象是如何实现这种扩展的。

### 0101. 主题卡 —— 技术发展的本质是建立在人类构造的模型之上

信息源自「0501 Software Endures」

Following Brooks, I would argue that the essential difficulties in writing this book center on how to weave an accessible story around highly technical topics. The technology I have at my disposal has probably removed nearly all of the accidental complexities around this task. I have a QWERTY keyboard, and I can touch type quite fast. I have excellent, free, open-source word processing software ( ).

When I can't recall what exactly it is that Fred Brooks said in his silver bullet paper, I just go to Google and search for「silver bullet,」and I quickly have the paper right in front of me. The only remaining difficulties are the essential ones that follow from the possibly quite controversial cases that I'm trying to make, including the one here, that technology development is a fundamentally creative human activity driven by culture and aesthetics and built on models that are human fabrications much more than discovered natural laws. Only the difficulty of making this case makes writing this book difficult.

The engineered systems that help me, my laptop computer, , Wikipedia, and Google, are human constructions of astonishing complexity. The engineers responsible for them relied on tools that also removed many of the accidental complexities, enabling them to focus on the essential complexities. Jimmy Wales and Larry Sanger, who created Wikipedia, did not write their programs in binary or even assembly language. In fact, they used several additional layers of models.

The next layer above ISAs and assembly language is the programming language. In late 1953, John W. Backus at IBM started a project to develop an easier language for expressing programs, particularly those extensively using mathematical expressions. The result of this project was Fortran, a language that endures to this day, with the latest update to the language occurring in 2008.

除了布鲁克斯所说的复杂性，我认为撰写本书的主要困难在于如何围绕非常技术化的主题来编织一个读者易理解的故事。我所掌握的技术可能已经消除了围绕这项任务的几乎所有的偶然复杂性。我有一个 QWERTY 键盘（全键盘），而且我打字相当快。

我还有优秀、免费且开源的文字处理软件（LATEX）。

当我记不起布鲁克斯在他的《银弹》论文中到底说了什么时，我就会去谷歌搜索「银弹」，很快这篇论文就呈现在我面前了。剩下的唯一困难就是一些本质性的困难了。这些困难来自我试图提出的一些可能颇有争议的问题，包括这里所说的一个问题，技术发展本质上是一种由文化和美学驱动的创造性的人类活动，它建立在人类构造的模型之上，而非被发现的自然法则的模型之上。仅是提出这个问题的困难就已经使得本书的写作变得非常有难度了。

1-2『上面的观点贯穿整本书：技术发展的本质是建立在人类构造的模型之上而非建立在人类发现的自然法则模型之上的。做一张主题卡片。（2021-10-25）』—— 已完成

帮助我写这本书的工程系统包括我的笔记本电脑、LATEX 排版软件、维基百科和谷歌，它们都是人类构建的复杂得惊人的系统。负责这些系统的工程师依赖于同样消除了许多偶然复杂性的那些工具，从而使他们能够专注于本质复杂性。创建维基百科的吉米·威尔士和拉里·桑格并没有用二进制甚至汇编语言编写他们的程序。事实上，他们使用了另外几个模型层。

指令集体系架构和汇编语言之上的一层是编程语言。1953 年年末，在 IBM 工作的约翰·W. 巴克斯启动了一个项目，开发了一种更简单的语言来表达程序，特别是那些广泛使用数学表达式的程序。这个项目的结果是产生了 Fortran 语言，它是一种一直沿用至今的语言。它的最新版本出现于 2008 年。

### 0201. 术语卡 —— 工艺

信息源自「0601 Evolution and Revolution」

工艺指的是人类创造以前不存在的人工制品的技能。但是，常态工程的工艺与创新有着明显的不同。一个出色的网页会让用户产生互动的乐趣，但它并不一定具有创新性，而且几乎肯定不构成一项发明，这与常态科学并不追求新奇性的道理是一样的：

2『这里看到了对工艺的定义，跟自己的本行业相关了，做一张术语卡片。（2021-10-24）』—— 已完成

常态科学不以新奇的事实或理论为目标。而且，当取得成功的时候，也根本找不出任何新奇的东西。（库恩，1962：52）

工艺、美学对工程任务能否成功的影响与创新一样大，甚至是更大。苹果手机成功的一个主要因素无疑是其充满美学的外观设计，这都要归功于乔纳森·伊夫。令人感到惊讶的是，苹果公司居然设法为这一设计申请了专利，并将其标榜为一项发明。该专利包含一个声明，全文是「如图所示和描述的便携式显示装置的外观设计」（赤名等人，2012）。在我看来，这是一个令人讨厌的声明，它有悖于任何关于发明的合理概念。美国专利和商标局应该为批准该项专利的行为感到羞愧。

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 数据信息卡 —— 各种「淘汰」编程语言的特色

信息源自「0501 Software Endures」

A graveyard language that takes the opposite approach is COBOL, after「common business-oriented language.」COBOL was designed in 1959 based on an earlier language developed by Grace Hopper, shown in figure 5.5 . Hopper was an early proponent of high-level programming languages that were portable, meaning that they could be compiled to execute on a variety of machines, even machines with different instruction set architectures.

COBOL was intended to have a syntax more like English than like mathematics, so it tends to replace symbol operators with words. For example, instead of the APL assignment statement x ← y, in COBOL you would say MOVE y TO x . For many years, COBOL was widely used for business applications such as banking, but today few new programs are written in COBOL.

COBOL and APL represent extremes in an exploration of programming paradigms. COBOL is verbose, using English-language words, with the idea that programs would be more readable by business people. APL is concise, cryptic, and requiring special keyboards. Both succumbed to the Darwinian competition of paradigms, dinosaurs that were once successful but are now largely extinct.

Many more languages are in the graveyard, including Algol, Pascal, PL/I, SNOBOL, Smalltalk, and Prolog. Each of these has interesting ideas and an interesting story. Algol introduced many features present in most modern imperative programming languages, including Java, C, C++, and C#. Pascal introduced the idea of compiling first into a virtual machine language (called byte code) and then executing that program in a program that simulates the virtual machine. This is a centerpiece of the widely used Java language today. SNOBOL, developed at Bell Labs by David Farber, Ralph Griswold, and Ivan Polonsky in the 1960s, introduced high-level manipulation of text, including parsing and pattern matching, a centerpiece of the widely used JavaScript language today, among others. Smalltalk was one of the earliest object-oriented languages, providing a way of structuring programs that is widely used today. Prolog is a「logic programming」language that elegantly expresses rule-based queries over structured data.

Figure 5.5 Rear Admiral Grace Hopper, 1906-1992. Hopper was an early proponent of portable programming languages and pioneered a style of programming where programs read more like English-language sentences than like mathematical expressions. [Image courtesy of the United States Navy.]

Each of these languages encodes a paradigm, a way of thinking about computation. These languages did not die the way Kuhn's scientific paradigms die. No crisis was created by anomalous observations that exposed discrepancies between the paradigm and the natural world. Rather, these languages either mutated into new species of languages (as in ALGOL and Pascal) or progressed toward extinction in a Darwinian competition of survival of the fittest or the most promiscuous (as in APL and COBOL).

已被淘汰的 COBOL（common business-oriented language，面向商业的通用语言）语言采用了与 APL 截然相反的方法。COBOL 是在 1959 年格蕾丝·霍珀（见图 5.5）早期开发的语言基础上设计出来的。霍珀是可移植高级编程语言的早期支持者，这意味着这些编程语言可以被编译到各种机器上执行，甚至是具有不同指令集体系架构的机器上。

COBOL 的语法更像英语而非数学，因为它倾向于用单词代替符号运算符。例如，与 APL 赋值语句 x ← y 不同，在 COBOL 中，你可以写成「MOVE y TO x」。多年来，COBOL 被广泛应用于银行等商业领域。但现在很少有新的程序是用 COBOL 编写的。

图 5.5 格蕾丝·霍珀（1906—1992），美国前海军少将。霍珀是可移植编程语言的早期支持者，她开创的一种编程风格，使程序读起来更像英语句子而不是数学表达式。（该图片由美国海军提供。）

COBOL 和 APL 代表了探索编程范式的两个极端。COBOL 是冗长的，它使用英语单词编写程序，其思想是使得这种程序更易于被商业人士阅读。APL 则简洁、隐秘且需要特殊的键盘。当然，它们都屈从于达尔文式的范式竞争。正如恐龙这一曾经生机勃勃的物种，现在已经全部灭绝了。

还有许多已经被淘汰的语言，包括 Algol、Pascal、PL/I、SNOBOL、Smalltalk 和 Prolog。它们中的每一个都包含了有趣的想法和奇妙的故事。Algol 引入了包括 Java、C、C++ 和 C# 等大多数现代命令式编程语言中的许多特性。Pascal 引入了这样一种思想：首先将一个程序编译成虚拟机语言（它们被称为字节码），然后在模拟该虚拟机的程序中执行这个程序。这是当今广泛使用的 Java 语言的精髓。SNOBOL 是由大卫·法伯、拉尔夫·格里斯沃尔德和伊万·波隆斯基于 20 世纪 60 年代在贝尔实验室开发的。SNOBOL 引入了对文本的高级操作机制，包括解析和模式匹配等，而这正是当今广泛使用的 JavaScript 语言的核心。

Smalltalk 是最早的面向对象的语言之一，它提供了一种当今广泛运用的结构化程序设计方法。Prolog 是一种「逻辑编程」语言，它可以优雅地表达结构化数据中的基于规则的查询。

2『各种「淘汰」编程语言的特色，做做一张信息数据卡片。（2021-10-25）』—— 已完成

这些语言中的每一种都编码了一种范式 —— 一种关于计算的思维方式。这些语言范式并没有像库恩所说的科学范式那样消亡了。那些暴露了范式与自然界之间差异的反常的观察并没有造成危机。相反，这些语言要么变异成新的语言物种（如 Algol 和 Pascal 语言），要么在适者生存与混杂式达尔文竞争中渐渐走向灭绝（如 APL 和 COBOL）。

### 0601. 任意卡 —— 新范式的胜利是因为坚守老范式的那些科学家最终死去了

信息源自「0201 Inventing Laws of Nature」

范式经常会发生改变。库恩的科学范式变化相对较少，但这些变化可能会对科学界造成相当大的破坏。在《科学革命的结构》一书中，库恩引用了马克斯·普朗克的话：

一个新的科学真理并不是通过说服对手并让他们看到真理之光而获得胜利的，而是因为它的对手最终会死去，而熟悉它的新一代人会成长起来。

1-2-3『上面的这段话，在 N 多个地方看到过，新范式的胜利是因为坚守老范式的那些科学家最终死去了。做一张任意卡片。（2021-10-24）』—— 已完成

同样的事情也发生在技术范式上。让我们来看看有多少现代科技让老化的大脑根本无法领悟。我们的孩子当然能够很快接受老年人无法理解的技术真理。事实上，我认为当今技术进步的步伐更多地受到人类无法吸收新范式的限制，而非技术本身存在的任何限制。

库恩对那些曾经持有的范式被后来更好的范式取代的科学家说出了以下的慷慨之词：

…… 总的来说，那些曾经流行的自然观与今天流行的自然观相比，无论在科学性还是人文性方面都毫不逊色。

…… 如果这些过时的信念可以被称为神话，那么可以用同样的方法制造神话，并以同样的理由坚持这些神话，而这些理由现在导致了科学知识的产生。

我们应该同样慷慨地对待那些生活在过时的技术范式时代的人，而不应把他们当作卢德派分子或恐龙。我会对我的孩子们说：「别担心，有一天你也会变成恐龙的。」

### 0602. 任意卡 —— JavaScript、jQuery 和 CSS 在网页生成中各自的作用

信息源自「0501 Software Endures」

The web page of figure 5.6 is constructed using three distinct languages, JavaScript, HTML, and CSS, and one dialect, jQuery, each idiosyncratic and designed largely by a single creative individual. This is perhaps not as culturally rich and diverse as, say, Jerusalem, but it is most certainly not just dispassionate, objective, soul-less technology. It has every element of human subjectivity and invention pervading it. And millions of people today use this particular combination of technologies to design sophisticated web pages.

Of course, we could create a web page like that in figure 5.6 using HTML alone, but there are good reasons for using this combination of technologies. Using JavaScript enables the web page to dynamically update the contents of the page, making it interact with the user. Using CSS separates visual presentation design elements from logical structure and functionality, modularizing the design better. Using jQuery mitigates the accidental complexity associated with the fact that web pages can take a long time (relative to computer speeds) to load from a server and provides convenient access to elements of the page.

Although these languages and dialects each originated with a single individual, all are now thriving open-source communities with hundreds of contributors. They have evolved into a form of collective wisdom, like Wikipedia, rather than individual wisdom, like the Encyclopedia Britannica.

图 5.6 所示的网页是由三种不同的语言（JavaScript、HTML 和 CSS）以及另外一种方言 jQuery 构建的。每一种语言都非常独特，主要由一个有创造力的人设计。也许它不像耶路撒冷那般具有丰富多样的文化，但也绝不只是一种冷静、客观、无灵魂的技术。它有着人类的主体性并充满了创造性。今天，数以百万计的人使用这种特殊的技术组合来设计复杂的网页。

当然，我们可以单独使用 HTML 创建一个如图 5.6 所示的网页页面，但是也有充分的理由使用这种技术组合。使用 JavaScript 语言可以使网页动态地更新页面内容，使其能够与用户进行交互。使用 CSS 能够将视觉上的设计元素从逻辑结构和功能中分离出来，这也会使设计实现更好的模块化。由于从服务器加载网页可能需要很长的时间（与计算机的运行速度有关），所以使用 jQuery 语言可以减少这个长时间过程所带来的偶然复杂性，并提供对页面元素的便捷访问。

2『 JavaScript、jQuery 和 CSS 在网页生成中各自的作用，做一张任意卡片。（2021-10-26）』—— 已完成

虽然这些语言和方言最初都源于个人，但它们有成千上万的贡献者，这使得它们今天能够在开源社区中蓬勃发展。它们已经演变成一种集体智慧的形式，就像维基百科，而不是像《不列颠百科全书》那样的个体智慧。

## 推荐序

科学技术是人类文明进步的产物，是人类社会的重要构成，其源自人类的生产创造和社会文化，又对人类社会发展产生持久而深远的影响。自以天文学、物理学为代表的近代科学技术诞生以来，科学技术在近几个世纪里持续加速发展，传统领域不断突破、科技创新方兴未艾，人类社会已经迈入一个科技大繁荣的新时代。放眼国际，科技创新与发展水平现已成为衡量发达国家综合国力与核心竞争力的重要方面，提升科技实力也已成为建设世界强国的核心战略。

以自然科学为核心的科学技术主要聚焦于客观的物理世界，致力于未知客观规律的发现以及新事物的发明与创造，但实际上，其发展水平也与社会人文、科技文化等诸多方面密切相关。在一个特定的历史阶段、一个特定的社会形态中，科技群体开展科学与工程创新的水平本质上会受到群体内所形成的科技价值、模式、文化及生态等因素的影响。对人文与科技、科学与工程、发现与发明、发明与设计、价值与价格、内涵与形式、开放与封闭、人类与技术等这些二元关系的正确认知以及辩证统一会在很大程度上决定科技创新的质量与高度。当然，科技文化与生态的形成和演进是一个较为缓慢的过程，其前提是营造益于激发创新创造的科技哲学与文化氛围，形成聚焦价值引领、激励原始创新的科技文化生态。

富有思想性的优秀科技哲学类著作将有益于引导科技界进行深入思考，有益于从根本上促进科技的创新，而爱德华教授的这本书恰好就是这样的一部上乘之作。在书中，爱德华教授将知识与技术是由独立于人类存在且被人类发现的柏拉图理想所构成的观点与人类创造而不是发现知识与技术的观点对立起来，进而以作为现代科技发展新引擎的数字技术为主要贯穿内容，重点对模型世界与物理世界、科学领域与工程领域的一系列论题进行了深入生动的辨析。爱德华教授强调工程学同样是一门极具创造性和智慧性的学科，二者相辅相成、不可偏废。显然，将科学与工程进行辩证统一、融合发展才能真正推动科技的协同创新与产业繁荣，而自主科技体系的建立也必然需要兼顾这两个方面。爱德华教授强调，模型与范式（即公认的模型或模式）可以激发创造力，技术范式较科学范式的演化更为频繁且通常是变革式的，技术进步的速度取决于人类对新范式的理解和接受程度。显然，这一论断进一步强调了制约工程学与科学演化的根本在于范式及范式的转换，就有如思维对知识、元模型对具体模型的影响。当今以半导体物理学为载体的数字技术飞跃发展，其关键便在于形成了独特且层次分明的范式体系。换言之，要想从根本上推动科技发展，就必须发现、创造和培育优秀的、层次化的范式。

基于对信息及软硬件技术内涵与特点的分析，爱德华教授进一步强调了人类与技术之间的互补与共生关系。他认为，物理世界中存在着不确定性和连续性，而数字技术是离散和不完备的，因此，数字技术真正的力量还是要源于其与人类的伙伴关系，但其发展还存在诸多障碍。关于近年来的人工智能浪潮，爱德华教授认为「智能」与「自主」只是对计算机的拟人化，其本质上有一定的不合理性，且在当前的技术体系下也不够实际。人类与计算机要实现的是共生，而非由计算机复制并替代人类。书中提到的另一个重要主题是专业化，这是科学与工程在演进过程中呈现出的一个共同趋势。但爱德华教授强调，过度的专业化会使人们对越来越细小的事物关注得越来越多，甚至是「对一无所知的事情了如指掌」（书中原文），但这样必然会让人们丢掉大的知识体系与背景，从而形成支离破碎且阻碍科技发展的范式与生态。学科过度细分、技术过度细分、领域过度细分，但凡这些过度的细分都会造成更多难以融合融通的专业「竖井」，其必然会对我们的高质量人才培养、科技创新、产业推进等形成阻碍。因此，如何在专业化发展的过程中推动交叉与融合，实现二者的平衡与优化将会对一个国家或地区的科技发展产生巨大影响，这一点非常值得我们深思。

可以看出，爱德华教授对制约科技创新发展的本质问题进行了深刻的哲学思考，本书则是从科技与哲学、文化相融合的角度撰写的一部见解独到、思想深邃又诙谐易读的经典科技哲学著作。通过阅读本书，我相信广大读者一定能够获得丰富的科技哲理启发以及有效的思维认知提升，它必然会对读者日常的教育、科研工作乃至生活都产生潜在而积极的影响。同时，我建议读者对书中给出的观点进行开放式的思考与探讨，这对于拓展读者的专业思维、提升读者的专业素养必将是极为有益的。正如作者所言，物理世界的不确定性和模型的不完备性必然使得人类社会的科技创新永无止境，这也必然为人类的创造力提供无限空间。因此，我们应该以数字技术的发展为借鉴和支撑，通过认知、模型、范式的不断优化和发展来更好地探索物理世界中的未知，并辩证运用人文与科技、科学与工程的互相支撑来更好地开展创新与创造工作。

中国工程院院士

2020.7

© 2017 Massachusetts Institute of Technology

This book is dedicated to my muse, Rhonda Righter, with thanks for many dinnertime conversations that shaped my thinking.

## Preface

### 01. What This Book Is About

When I was young, my father wanted me to become a lawyer or get an MBA and take over the family business. Engineers were the people who worked for him. The brightest young minds, at least those of white Anglo-Saxon stock in the United States, went to law school, business school, or medical school. Today, engineering schools are much harder to get into, but that was not true when I was going to college. Yes, my father was profoundly disappointed in me when I double majored in Computer Science and what Yale called「Engineering and Applied Science.」I made it worse when I went to MIT for graduate school in engineering and then went to work as an engineer at Bell Labs, and worse still when I went to Berkeley for a PhD and then became a professor. This book is perhaps my last-ditch attempt to justify those decisions.

When I started writing the book, I really didn't know who my target audience would be. As it has turned out, this book is targeted toward readers who are either literate technologists or numerate humanists. I'm not sure how many such people there are, but I'm convinced there must be a few. I hope you are one of them.

This book is my attempt to explain why the process of creating technology, a process that we call engineering, is a deeply creative process, and how this explains why it has become so hot and competitive, making geeks out of the brightest young minds. The book is about the culture of technology, about both its power and its limitations, and about how the real power of technology stems from its partnership with humans. I like to think of the book as a popular philosophy of technology, but I doubt it will be very popular, and I am not sure I have the qualifications to write about philosophy. So really, the only guarantee I can make is that it is about technology and the engineers who create technology. And even then, it is limited to the part of technology that I understand best, specifically, the digital and information technology revolutions.

This book is not about the artistry and creativity that is unleashed by using technology as a medium. For that topic, I recommend the wonderful book by Virginia Heffernan, Magic and Loss (Heffernan, 2016). Heffernan claims that「the Internet is a massive and collaborative work of realist art,」but she is referring to the content of the Internet. In my book, I claim that Internet technology itself , and all of digital technology that shores it up, is a massive and collaborative creative work, even if not an artistic work.

Digital technology as a medium for this latter sort of creativity has enormous potential, well beyond what has been accomplished to date. In the first part of this book, I explain exactly why this technology has been so transformative and liberating. I study how engineers use models and abstractions to build inventive artificial worlds and give us incredible capabilities, such as the ability to carry around in our pockets everything humans have ever published.

But this is not to say that digital technology has no limitations. Pursuing a yin and yang balance, in the second part of the book, I attempt to counter a runaway enthusiasm among some thought leaders about digital technology and computation. Driven by the immense potential of computers, this enthusiasm has led to unjustified beliefs that go as far as to assert that everything in the physical world is in fact a computation, in exactly the same sense as in modern computers. Everything, including such complex phenomena as human cognition and such unfamiliar objects as quasars, is software operating on digital data. I will argue that the evidence for such conclusions is weak and the likelihood is remote that nature has limited itself to only processes that conform with today's notion of digital computation. And I will show that this digital hypothesis cannot be tested empirically, and therefore can never be construed as a scientific theory. Because the likelihood is remote, the evidence is weak, and the hypothesis is untestable, these conclusions are an act of faith. My argument here will likely get me into trouble because I'm swimming against a considerable current.

Also bucking much current thought, I argue that the goal of artificial intelligence to reproduce human cognitive functions in computers is misguided, is unlikely to succeed, and vastly underestimates the potential of computers. Instead, technology is coevolving with humans, augmenting our own cognitive and physical capabilities, all the while enabling us to nurture, evolve, and propagate the technology. We are seeing the emergence of symbiotic coevolution, where the complementarity between humans and machines dominates over their competition.

But most of the book is very much swimming with the current, upbeat about the enormous potential of technology to improve our lives. But more than just utilitarian, one of my main messages is that engineering is a deeply creative and intellectual discipline, every bit as interesting and rewarding as the arts and sciences. In areas where the technology is less mature, the creative contributions reflect the personalities, aesthetics, and idiosyncrasies of the creators. In areas that are more mature, the work can become deeply technical and opaque to outsiders. This happens in all disciplines, so this is hardly surprising.

Like the sciences, engineering is built around accepted paradigms that provide frameworks for thought. Also like the sciences, engineering is punctuated by paradigm shifts, to use the words of Thomas Kuhn (Kuhn, 1962). Unlike the sciences, however, the paradigm shifts are frequent, even relentless. I argue, in fact, that the pace of technological progress in our current culture is more limited by our human inability to assimilate new paradigms than by any physical limitations of the technology. I attempt in this book to explain why this is.

Like the arts, the evolution of the field of engineering is governed by culture, language, and cross-germination of ideas. Also like the arts, success or failure is often determined by intangible and inexplicable forces, such as fashion and culture. And in an observation that may take many readers by surprise, also like the arts, the creative media used to engineer new artifacts and systems today, particularly digital media, have become astonishingly versatile and expressive. In my opinion, this latter property, the versatility and expressiveness of digital media, accounts for the attractiveness of the field to bright young minds, more even than the lucrative job prospects.

Engineering is a broad field, encompassing everything from water supply systems to social networking software. Any individual, myself included, cannot have more than a superficial understanding of more than a few of its subdisciplines. My arguments in this book, therefore, are based on my experience with electronics, electrical engineering, and computer science. These arguments apply to digital and information technologies and may or may not apply to other technologies such as bridges and chemical plants. Nevertheless, I do know from experience that digital technologies have invaded nearly all other engineering disciplines. Modern chemical plants, for example, include substantial computer control and therefore become instances of cyber physical systems, discussed in chapter 6 . Such systems are most certainly subject to the potential, vagaries, and limitations of digital technology that I point out in this book.

I do not assume of the reader any particular technical background. In some sections of the book, I do dive more deeply than I probably should into technical topics that are near and dear to my heart, but I promise the reader that every such indulgence is short, and hopefully skipping the technical details will not seriously undermine the message. Please persist. The nerd storm will pass quickly.

I do assume a numerate reader. Against all advice, I have even included 12 equations in the book. They are not complicated equations. High school math and science is more than sufficient to fully understand them, but even then full understanding is not needed to get the message. My publisher has used this argument against me, saying that if it is true, I should remove them. But I like them. I have confidence that there are more numerate readers than there used to be. I have assured the publisher that, counting my friends and family, a few dozen book sales are assured.

The title of this book comes from the wonderful book by Nassim Nicholas Taleb, The Black Swan (Taleb, 2010), who titled a section of the prologue「Plato and the Nerd.」Taleb talks about「Platonicity」as「the desire to cut reality into crisp shapes.」Taleb laments the ensuing specialization and points out that such specialization blinds us to extraordinary events, which he calls「black swans.」Following Taleb, a theme of my book is that technical disciplines are also vulnerable to excessive specialization; each speciality unwittingly adopts paradigms that turn the speciality into a slow-moving culture that resists rather than promotes innovation.

But more fundamentally, the title puts into opposition the notion that knowledge, and hence technology, consists of Platonic Ideals that exist independent of humans and is discovered by humans, and an opposing notion that humans create rather than discover knowledge and technology. The nerd in the title is a creative force, subjective and even quirky, and not an objective miner of preexisting truths.

I hope that through this book, I can change the public discourse so young people are more inclined to consider a career in engineering, and not just because of the job prospects. I am convinced that engineering is fundamentally a creative discipline, and the technical drudgery that prejudices many people is no more drudgery than found in any other creative discipline. Yes, hard work is required, but as a reward for that hard work, you can change the world.

主要内容

当我年轻的时候，我的父亲想让我将来成为一名律师，或者获得工商管理学硕士学位并接管家族企业，而工程师是那些正在为他干活的人。最聪明的年轻人，至少是那些美国盎格鲁 - 撒克逊白人的后裔，读的是法学院、商学院或医学院。和过去相比，现在要考入工程学院的难度很大，在我读大学的时候情况却并非如此。当我主修耶鲁大学的「计算机科学」和「工程与应用科学」双学士学位的时候，父亲对我感到非常失望。继而我去麻省理工学院攻读工程硕士学位，然后成为贝尔试验室的一名工程师，最后又去伯克利大学攻读博士学位，并成为一名大学教授。我的一次次决定让我的父亲愈感失望。这本书也许是我为那些决定进行辩护的最后一次尝试吧。

当我开始写作本书时，我实际上并不清楚我的读者受众都会有谁。但随着本书的完成，我确信本书是以有人文社科底蕴的技术专家或者懂技术的人文主义者为读者对象的。我不确定这样的人能有多少，但我深信肯定会有一些。我希望你就是其中的一员。

本书试图解释为什么创造技术的过程，即我们称为工程的过程，是一个非常有创造性的过程，并希望向读者解释为什么这个学科变得如此火热和有竞争力，以至能够让一些极客从最聪明的年轻人当中脱颖而出。本书将向读者介绍技术文化、技术的力量与局限性以及技术的真正力量等，是如何通过与人类的伙伴关系发挥出来的。我倾向于把这本书视为一种受欢迎的技术哲学读物，但我怀疑它是否会受到读者的欢迎，而且我也不确定我是否具备撰写一部哲学类图书的水平。但是，我唯一可以保证的是，这是一本关于技术和创造技术的工程师的著作。即便如此，本书也无法做到包罗万象，仅限于我最了解的技术部分，特别是数字和信息技术革命。

本书讨论的不是如何以技术为媒介来释放艺术性和创造性。如果读者想要了解这方面的内容，那么我推荐阅读维吉尼亚·赫弗南于 2016 年出版的《魔法与迷失》（Magic and Loss）一书。赫弗南声称「互联网是现实主义艺术大规模协同工作的产物」，但她所指的主要是互联网的内容。在我的书中，我认为互联网技术本身，以及支撑它的所有数字技术，都是一项大规模协同的创造性工作，即使其并非艺术性工作。

数字技术作为后来出现的一种富有创造力的媒介，有着巨大的潜力，并且远远超过迄今为止其他技术领域所取得的成就。在本书的第一部分，我将详尽地解释为什么这项技术具有如此彻底的变革力和释放性。我研究了工程师是如何创造性地使用模型和抽象来构建人工世界，并给予我们难以置信的能力。例如，将迄今为止人类出版过的所有图书全部装入口袋的能力。

但这并不意味着数字技术就没有它的局限性。为了从正反两方面阐释数字技术的发展，我在本书的第二部分试图反驳一些所谓思想领袖对数字技术和计算的狂热痴迷。在计算机技术巨大潜力的驱动下，这种狂热导致了一些不合理的信念。这些信念甚至断言，物理世界中的一切实际上都是一种计算，其在本质上与现代计算机的运算过程是完全相同的。一切事物，包括诸如人类认知等复杂现象以及诸如星体等我们所不熟悉的事物，都不过是在数字数据上运行的软件。

我认为，支撑这些结论的证据是薄弱的，大自然仅将自身局限于符合当今数字计算概念的过程的可能性相当渺茫。我将证明，这一数字假说并不能得到实证验证，因此也就永远不能被解释为一种科学理论。由于其可能性非常渺茫，证据极弱，而且假设又是不可验证的，所以得出的结论不过是一些无根据的猜想罢了。我在这里的论点可能会给我带来一些麻烦，因为我正逆流而行，与大多数人的观点相左。

的确，我的观点与当前的许多观点都不同，我认为人工智能在计算机上复制人类认知功能的目标是一种误导，其是不大可能获得成功的，并且还在很大程度上低估了计算机科学的潜能。相反，我认为，技术正在与人类共同进化，正在拓展我们的认知和自身能力，所有这些也使得我们能够培育、发展和传播技术。我们已经看到，人类与机器之间存在的互补性正在促进人类与机器共生、共同进化。

然而，本书的大部分内容都与现实情况相吻合，比如，技术的巨大潜力将改善我们的生活，这是人类对技术发展所持有的乐观态度。除了强调技术已对人类生活产生的积极影响，我在本书中要表达的主要观点之一在于，工程学是一门极具创造性和智识性的学科，它同艺术和自然科学一样是有趣和有价值的。在技术不那么成熟的领域中，创造性的贡献更多地体现了创造者的个性、审美和特质。在更为成熟的领域，这些工作可能会变得极为技术化，且令非专业人士觉得有些晦涩难懂。然而，我们必须承认，这种情形在所有学科中都会出现，所以不足为奇。

与科学一样，工程学是建立在被广泛认可的范式之上的，是指导行动的思想框架。工程学与科学相似，用托马斯·库恩（1962）的话来说，工程学的发展也会不时地为范式的转换所打断。然而，与科学不同的是，工程学中范式的转换是频繁的，甚至是变革式的。事实上，我认为，在我们目前的文化中，技术进步的速度主要是受到人类无法理解新范式的制约，而并非技术自身发展的限制。我希望本书能够清楚地阐释其中的原因。

与艺术一样，工程学领域的发展也会受到文化、语言和思想交叉萌发的制约。也和艺术一样，工程学的成功或失败往往决定于无形和不可解释的力量，比如时尚和文化。就这一点而言，工程学的发展几乎和艺术是相同的。仍然像艺术一样，一个新的发现可能会让诸多读者感到惊讶不已。今天用来设计新的手工艺品和系统的创意媒体，尤其是数字媒体，其广泛的用途和丰富的表现力真是令人惊讶。在我看来，数字媒体的多功能性和强大的表现力足以解释为什么该领域对优秀的年轻人具有这么大的吸引力。这种巨大的吸引力甚至超过了高收入就业前景所具有的吸引力。

工程学是一个很宽广的领域，它从供水系统到社交网络软件，包罗万象。任何人，包括我自己在内，对工程学诸多子学科的理解都还是比较肤浅的。因此，本书的观点主要基于我在电子、电气工程和计算机科学方面的有限经验。这些观点适用于数字和信息技术，也可能适用于其他技术，如桥梁以及化工厂等等。尽管如此，根据我的经验，数字技术已经渗透到几乎所有的工程学科中。例如，现代化的工厂大部分是由计算机控制和管理的，从而也就成为信息物理系统（CPS）的实例。本书的第 6 章对该内容进行了详细的阐述。这类系统无疑受到我在本书中所指出的数字技术的潜力、多变性和局限性的制约。

我首先假定读者是没有任何特定技术背景的。但在本书的某些章节中，我也的确是较为深入地讨论了一些我所关注的技术主题。但是，我向读者保证，每一个这样的讨论都不会过度深入。当然，我也希望我所略掉的这些技术细节不会严重破坏我所要传递的信息。但凡遇到这样的技术主题，请读者保持耐心并坚持下去。请相信，类似这种技术呆子式的头脑风暴会很快过去的。

我的确假设您是一位了解计算机技术的读者。在据理力争之后，我在本书中只保留了 12 个方程。实际上，要理解这些并非复杂的方程，高中水平的数学和科学知识就足够了，即使不能完全理解，读者也能从中获取应有的信息。我的出版商用这个理由反驳我，说如果这是真的，我就应该将其全部删除。但是我更希望予以保留，我坚信，现在了解计算技术的读者比以前会更多。我已经向出版商保证，算上我的朋友和家人，本书几十册的销量还是可以保证的。

本书书名的灵感来自纳西姆·尼古拉斯·塔勒布精彩的著作《黑天鹅》。塔勒布给书的序言的一个部分取名为「柏拉图与愚人」。塔勒布把「柏拉图主义」形容为「将现实切割为清晰形状的愿望」。塔勒布哀叹随后的专业化发展趋势，并指出这种专业化使我们对那些不寻常的事件视而不见，他将不寻常的事件称为「黑天鹅」。围绕塔勒布的思想，本书的一个主题会阐明技术学科也容易受到过度专业化的影响；每个专业都在不知不觉地采用某些范式，这些范式将这个专业转化为一种缓慢发展的文化，其结果是阻碍了而不是促进了技术的创新。

此外，本书的书名从根本上反对这样的认知，即技术是由独立于人类的柏拉图式的理想构成的，并且技术是由人类发现的。这一观点刚好与认为人类创造而不是发现知识和技术的观念背道而驰。书名中的技术呆子象征着一种主观甚至是奇特的创造性力量，而不是客观真理的一个发现者。

我希望本书可以改变公众对工程学的某些偏见，进而鼓励年轻人更倾向于选择工程学方面的职业，而不只是根据某种工作的前景来进行规划。我确信，工程学从根本上说是一门创造性的学科，而让许多人产生偏见的技术苦差事并不比任何其他创造性学科中的工作更为辛苦和乏味。是的，努力工作是我们必需坚持的职业操守，但是，你在工程学上的努力付出是一定会有回报的，那就是，你可以改变这个世界。

### 02. Overview of the Chapters

Some readers like to be told what they will be told before they are told it. Putting aside the problematic self-referentiality, for those readers, I provide here a brief overview of the book. But honestly, I recommend skipping this and going directly to chapter 1 . The story told in this book cannot be accurately summarized in a few paragraphs, and any such summary will necessarily make the book seem more dense than it is. Nevertheless, for those who really need it, here is my summary.

Popular perception of technology and engineering is often one of a dispassionate field dominated by logic and trading in colorless facts and truths. In chapter 1 , I explore the idea of facts and truths in technology, showing that these are not just discovered but more often invented or designed. Rather than being built on timeless Platonic Ideals, technology is built on ideas that are more fluid and sometimes quirky. The notion of truth becomes more subjective; collective wisdom becomes better than individual wisdom; a narrative about how facts evolve becomes more interesting than the facts themselves; facts and truths may be wrong; and it can cost billions to show that facts are true. I then develop the idea that engineering and science, disciplines rooted in facts and truths, are complementary and overlapping, leveraging each others' methodologies. In this chapter, I try to understand the cultural phenomenon that engineering has been considered the「kid sister」of science.

In chapter 2 , I focus on the relationship between discovery and invention. A key theme of this chapter is that models are invented not discovered, and it is the usefulness of models, not their truth, that gives them value. Note that the usefulness of a model need not be a practical, utilitarian sort of usefulness. A model may be useful simply because it explains or predicts observations, even if the phenomena observed have no practical application.

Models are useful to scientists when they are faithful to the natural system being studied, whereas models are useful to engineers when a physical realization can be constructed that is faithful to the model. These uses are complementary and, in fact, are often applied in combination.

Chapter 2 is heavily influenced by Kuhn (1962). But Kuhn focused on science, not engineering. The engineering use of models results in more room for creativity in the construction of models because it is not necessary for the models to be faithful to some preexisting natural system. But the use of models can also slow technological change because models are built on paradigms that frame our thinking and therefore limit our thinking. Models can also get quite sophisticated, forcing increased specialization, which can also slow change by impeding communication across specializations.

In chapter 3 , I dive into exactly how the engineering use of models enables creativity. I do this by illustrating the role that models have played in the development of digital technology, where models are stacked many layers deep, with the design of each layer affecting the designs both above and below it. Digital technology has, through this multiplicity of layers, mostly removed any meaningful physical constraints from a broad class of engineered systems. Each layer of models conforms with an established paradigm, a way of modeling and abstracting an engineered design. Innovation, therefore, is less limited by the physics of the technology than by our imagination and ability to assimilate new paradigms.

I argue that paradigms play a central role in digital technology because without them, no human could possibly comprehend the complexity of the systems we routinely build today. But these paradigms are human constructions, governed by culture and language. In many cases, the paradigms that have emerged are idiosyncratic, reflecting the personality and aesthetics of their creators.

A notable feature of digital technology is that paradigms are layered one on top of another. Semiconductor physics gives us the ability to make transistors, which we can use as electrically controlled switches that have two distinct states:「on」and「off.」This enables a digital abstraction that turns out to be just the first of many layers, building up eventually to the programming languages that enable us to build databases, machine learning systems, web servers, and so on. Each of these layers forms through coalescing of competing paradigms.

In chapter 4 , I explore the layered paradigms that make up much of today's digital technology hardware. I show that the physical substance of the hardware is not durable, but the paradigms are. The hardware is routinely discarded every few years as it wears out and becomes obsolete, but the principles on which the hardware is designed, with all their warts and idiosyncrasies, persist for decades.

In chapter 5 , I explore the layered paradigms that make up much of today's information technology. These paradigms define how we construct software, and software, it turns out, endures much better than hardware. Paradigms, like human culture, change slowly, particularly compared with the speed with which technology changes. Although Kuhn's scientific paradigms are strictly human constructions, the paradigms of software are encoded in the software. In an orgy of self-referentiality, software builds its own scaffolding. The self-scaffolding of software makes it much more durable than hardware, despite its ephemeral nonsubstantive existence. It could even outlast humans.

Chapter 6 explores the structure of technology revolutions, with a particular focus on digital technology. This chapter is also heavily influenced by Kuhn, but it strives to identify how technology revolutions differ from scientific revolutions. One key difference is that technology paradigms appear and disappear much more rapidly probably because, compared with scientific paradigms, they are relatively unconstrained by the physical world and are layered one upon another many layers deep. Like scientific paradigms, new technology paradigms do not necessarily replace old ones. They may instead overlay the old ones, building new platforms on top of existing platforms. The ability to do this depends on the transitivity of models explored in the three previous chapters. Unlike scientific paradigms, the crises that trigger new technology paradigms do not arise so much from the discovery of anomalies but from increasing complexity and technology-driven opportunity.

To balance the enthusiasm, the next few chapters look at what we cannot do with digital technology, at least not today. This requires explaining three classic concepts that emerged in the 20th century: Shannon's information theory, the Church-Turing thesis, and Gödel's incompleteness of formal models. In the later chapters, I consider the concept of determinism and examine how we can build models that embrace uncertainty using the notion of probability. Along the way, I need to confront another paradigm that emerged in 20th century called digital physics and a view that human cognition is software.

This part of the story begins in chapter 7 , where I examine the concept of information — what it is and how to measure it. In this chapter, I introduce Claude Shannon's way of measuring information and show that his notion of information often cannot be represented digitally. I define an「information-processing machine」more broadly than what can be realized using software and computers, as they exist today.

In chapter 8 , I explain what software cannot do. I point out that the number of information-processing functions is vastly larger than the number of possible computer programs. I introduce Alan Turing's undecidability result, which shows that useful information-processing functions exist that are not realizable by software on today's computers. But it does not follow that if a function is not realizable by software, then it is not realizable by any machine.

I caution against getting carried away by enthusiasm, marveling at what has already been accomplished with software, and caution against predicting that natural phenomena such as cognition and understanding are realizable in software. Here, I am forced to confront a belief that some people call「digital physics」: that the physical world is somehow software or equivalent to software. I argue that this idea is unlikely to be either true or useful as a way of understanding the physical world, at least in its more extreme forms, and I show that this thesis is not falsifiable and therefore not scientific.

In chapter 9 , I go beyond the countable world of computing and argue that computers are not universal machines and their real power comes from their partnership with humans. I explain the notion of a continuum, a concept that is out of reach for software and rejected by digital physics but seemingly essential for modeling the physical world. I examine the fundamental limitations of formal models that underlie the world of software, and I argue that the partnership and coevolution of humans and computers is much more powerful than either alone. In this chapter, I explain Kurt Gödel's famous incompleteness theorems, which impose fundamental limits on any modeling formalism that is capable of self-reference. We need to be humble, but we also need to recognize the as yet vast unexplored potential that still waits for us to catch up.

In chapter 10 , I consider determinism, a property of software and many mathematical models of nature. I argue that determinism is a property of models not of the physical world. But it is an extremely valuable property, one that has historically delivered considerable payoffs in engineering and science. However, determinism also has its limits. Even deterministic models may not be usefully predictive because of chaos and complexity. Also, families of deterministic models that embrace both discrete and continuous behaviors are incomplete. There are unavoidable holes where determinism breaks down, and deterministic models have their limitations. In many cases, nondeterministic models are simpler and better reflect what we do not know. Nondeterministic models, used explicitly and judiciously, play an essential role in engineering.

In chapter 11 , I finally confront the meaning of randomness and its measure, probability, which quantifies the likelihood of nondeterministic events. I argue that probability is fundamentally a model of uncertainty about something and not directly a model of that something. It models what we do not know. I examine the long-standing debate between the frequentists and the Bayesians, coming down solidly on the side of the Bayesians. I show that the philosophical difficulties presented by randomness vanish when using models in the engineering sense rather the scientific sense and when interpreting probability in the Bayesian sense. In this chapter, I also reconsider continuums and argue that probabilistic models over continuums reinforce the conclusion that digital physics is extremely unlikely. As a consequence, we should demand incontrovertible evidence for digital physics before accepting it.

In the final chapter, I tie things together by examining the epistemic role that models have in technology and the relationship between models and the physical systems they ultimately model. I leverage the previous arguments in the book: At least with digital technology, so many layers of abstraction exist between the models and the physical reality that the connection between the two becomes tenuous indeed. Moreover, the self-scaffolding that software paradigms have, described in chapter 5 , allows these models to stand on their own, almost but not completely independent of physical reality. I argue that this does not lead to a Cartesian mind-body dualism, but it does emphasize the need to insist, with great determination and discipline, on separating the map from the territory. Models are best viewed as having a separate reality from the physical world, despite existing in the physical world.

The most expressive modeling paradigms are capable of self-reference, which enables them to build their own scaffolding but also makes them necessarily incomplete. This incompleteness is fundamentally what enables creativity and ensures that what we can accomplish with technology is limitless. So what holds us back? In this final chapter, I consider both the obstacles to progress and the threats that technology, when misapplied, can have on society.

内容概述

有些读者喜欢在读一本书之前去了解书的大致内容。抛开有问题的自指性，对于这样的读者，我在这里特地给出了本书的简要概述。但是，坦率地说，我建议读者跳过这部分内容，直接从第 1 章开始阅读。因为本书所要讲述的内容是无法用几个段落来准确概括的。任何类似的内容摘要都必然会使本书看起来比它实际的内容更为晦涩难懂。然而，对于那些真的需要内容提要的读者而言，以下便是我对本书内容的简要总结。

人们对技术和工程的普遍看法往往是这样的：这是一个缺少激情的领域，它由逻辑和枯燥乏味的事实与真理主导。在第 1 章，我探讨了技术中的事实和真理的概念，我认为这些事实和真理并不只是被人类发现的，实际上更多是被人类发明或设计出来的。技术不是建立在永恒的柏拉图式的理想之上的，而是建立在更灵活多变且有时更为离奇的构思之上的。真理的概念变得更具主观性；集体的智慧比个人的智慧更加完善；关于事实演变的描述要比事实本身更为有趣；事实和真理可能都是错误的。然而，要想证明一个事实为真，有时可能会花费数十亿美元的巨资。因此，我在这里提出这样的观点：工程学和科学都是建立在事实和真理基础之上的学科，二者相辅相成、相互重叠，且相互利用彼此的方法。在这一章中，我试图理解工程学一直以来被视作科学的「胞妹」的文化现象。

第 2 章的内容主要是研究发现与发明之间的关系。该章的一个重要主题是，模型是被发明的，而不是被发现的。正是模型的有用性，而不是它们的真实性，赋予了它们价值。请读者注意，模型的有用性并不一定是一种实用的、功用的有用性。一个模型可能仅仅是因为解释或预测了观测结果就成为有用的模型，即使其所观测到的现象并没有实际的应用价值。

当模型与正在被研究的自然系统相符时，该模型对科学家而言就是有用的。而当符合该模型的物理实现总是能被构建时，该模型对工程师而言才是有用的。实际上，这些用途是相互补充的，且常常被组合使用。

本书第 2 章的内容深受库恩（1962）思想的影响。但是，库恩关注的是科学，而不是工程学。模型的工程应用给模型的构建带来更大的创造性空间，因为这些模型无须与某些已存在的自然系统保持高度一致。但是，另一方面，模型的使用会减缓技术的变革，这是因为模型建立在使我们思想条框化的范式之上，会对我们的思维造成限制。模型也可能变得相当复杂，从而导致更加专业化的发展。当然，模型也会因为不顺畅的跨专业融通而发展缓慢。

在第 3 章，我深入探讨了模型的工程应用是如何激活创造力的。我会通过说明模型在数字技术发展中所起的作用来进行讨论。在数字技术中，模型被层层叠加起来，每一层的设计都会影响其上、下相邻层的设计。通过这种多重的分层，数字技术已经从广泛的工程化系统中基本上消除了任何有意义的物理约束。每一层模型都与一个已建立的范式相符合，这是一种建模和抽象工程化设计的方法。因此，创新并不会受到技术物理学的制约，而会受到我们的想象力和吸收新范式的能力的影响。

我认为范式在数字技术中起着核心作用，因为如果没有它们，人类就不可能理解我们今天用常规方法所构建的系统的复杂性。但这些范式属于人类构造的范畴，会受到文化和语言的支配。在许多情况下，已经出现的范式会显得有些不同寻常，这是因为它们还呈现了创造者的个性和审美标准。

数字技术的一个显著特点是，这些范式是层叠的。半导体物理学赋予我们制造晶体管的能力，我们可以使用晶体管作为电子控制开关，其只具有两种截然不同的状态：「导通」和「截止」。这使得作为诸多分层中第一层的数字抽象成为可能，最终建立起使我们能够构建数据库、机器学习系统、网络服务器等的编程语言。这些层中的每一层都是通过聚结一组相互竞争的范式形成的。

在第 4 章，我探讨了构成当今大多数数字技术硬件的层次化范式。我将说明硬件的物理实体并非长久不变，但范式却可以长久存在。这些硬件通常每隔几年就会被丢弃，因为它们已经被严重损耗，或者因为过时而被淘汰了。然而，硬件的设计原理以及它们所有的缺陷和特性仍会持续几十年。

在第 5 章，我将探讨构成当今大部分信息技术的层次化范式。这些范式界定了我们是如何构造软件的。事实证明，软件比硬件的生命力要持久得多。范式就像人类的文化，变化缓慢，特别是当它与技术的变化速度相比时，就更是如此了。虽然从严格的意义上说，库恩的科学范式是人类构建的结果，但软件的范式会被编码在软件之中。在自我参照的狂欢中，软件会构建自己的「脚手架」。尽管软件是一种短暂的非实体性存在，但是软件的自我支撑使得它的生命力要比硬件更为持久。可以说，软件的寿命甚至可能超过人类的寿命。

第 6 章探讨了技术革命的结构，并特别聚焦于数字技术。这一章的内容同样深受库恩的影响，但主要是致力于找出技术革命与科学革命的不同之处。我认为，其中一个关键性的不同点就是，相较于科学范式的变化，技术范式的出现和消失的速度要快得多。这可能是因为，技术范式相对而言不受物理世界的限制，而且是深度层叠的。与科学范式一样，新的技术范式并不一定必须取代旧范式。相反，它们可能会覆盖旧的平台，在现有平台的基础上构建出新的平台。能否做到这一点取决于我在前三章中所探讨的模型的传递性。与科学范式不同的是，触发新技术范式的那些危机并非来自一场现象的发现，而是来自日益增长的复杂性和技术驱动的新机遇。

为了不让读者对数字技术的发展过于感到乐观，接下来的几章将会探讨什么是我们不能用数字技术来解决的，至少目前如此。这就需要我先向读者解释一下 20 世纪出现的三个经典概念：香农的信息理论，丘奇 — 图灵论题，以及哥德尔关于形式化模型的不完备性。在后面的章节，我将考虑继续探讨决定论的概念，并进一步论述我们如何利用概率的概念来建立非确定性的模型。在探讨该问题的过程中，我需要面对 20 世纪出现的被称为数字物理学的另一个范式，以及人类认知就是软件的观点。

这一部分内容是从第 7 章开始的，在本章，我分析了信息的概念 —— 信息是什么，以及如何测量信息。在这一章，我介绍了克劳德·香农的信息测量方法，并指出通常无法用数字化的方式表达他的信息概念。我定义了一个比现在用软件和计算机所能实现的用途更为宽泛的「信息处理机」。

在第 8 章我会解释软件功能的局限性。我认为，信息处理函数的数量远远大于可能的计算机程序的数量。在这一章，我介绍了艾伦·图灵的不可判定性研究结果，该结果表明存在一些有用的但当今计算机上的软件所不能实现的信息处理函数。但这并不意味着，一个函数如果不能通过软件实现，它就不能通过其他任何机器来实现。

我希望大家不要被这种热情冲昏头脑，不要对软件已经取得的成就感到惊讶，也不要预言诸如认知和理解等自然现象在软件中是可以实现的。在这里，我不得不面对被一些人称为「数字物理学」的信念，即物理世界在某种程度上就是软件或相当于软件。我认为，作为理解物理世界的一种方式，这种想法不太可能是正确或有用的，至少在更极端的方式下如此，而且我认为这一论题是不可证伪的，因此也就是不科学的。

在第 9 章中所探讨的内容超越了可数的计算世界。我会阐明，计算机不是通用机器，且它们真正的力量源于它们与人类的伙伴关系。在这一章，我解释了连续统的概念。这个概念超出了软件的范畴且为数字物理学所排斥，但其似乎对物理世界的建模又必不可少。我分析了作为软件世界基础的形式化模型的局限性，同时我认为人类和计算机的共同进化与伙伴关系要比二者之一都更强大。在本章，我还解释了库尔特·哥德尔著名的不完备性定理，其对任何具有自我参照能力的建模形式化方法设定了一些基本的限制。我们应该秉持谦逊的态度，但我们也需要认识到仍有巨大的开发潜力等待我们去发掘。

在第 10 章，我们讨论了决定论、软件的性质以及许多自然界的数学模型。我认为，确定性是模型的一种属性，而不是物理世界的属性。但它是一种极为宝贵的属性，在历史上为工程学和科学都带来了可观的回报。然而，决定论也有其局限性。由于混沌和复杂性，即便确定性的模型也可能无法被有效地预测。同时，包含离散功能和连续行为的确定性模型家族目前仍不完善。因此，我认为，决定论被瓦解是不可避免的，确定性模型有其明显的局限性。在许多情况下，非确定性模型更为简单，也能够更好地反映出我们所不知道的东西。如果非确定性模型能被明智而审慎地使用，那么它将在工程学中起到至关重要的作用。

在第 11 章，我最终将面对随机性的含义及其度量，即概率，其量化了非确定性事件的可能性。我认为，从根本上讲，概率是一种关于事物不确定性的模型，而非事物的直接模型。它建模了我们所不了解的东西。在本章，我分析了频率学派和贝叶斯学派存在已久的争论，并会坚定地支持贝叶斯学派。我认为，在使用工程学而不是科学意义上的模型，以及使用贝叶斯意义上的概率做出解释时，随机性所带来的哲学困扰就会骤然消失。在这一章，我还重新考虑了连续统问题，并阐明连续统上的概率模型进一步强化了「数字物理学是极不可能的」这一结论。因此，在接受数字物理学之前，我们必须为其找到无可辩驳的证据。

在最后一章，我通过分析模型在技术中的认知作用，以及模型与它们最终建模的物理系统之间的关系，将所有这一切都联系在一起。我运用了本书前面内容中的论点：至少在数字技术中，模型和物理现实之间存在着许多抽象层，两者之间的联系的确变得非常脆弱。但是，如第 5 章所述，软件范式所具有的自支撑能力允许这些模型独立存在，允许它们几乎但并非完全独立于物理现实。我认为，这不会导致笛卡儿的身心二元论，但它确实强调了以极大的决心和约束坚持将地图与地域进行区分的必要性。尽管模型存在于物理世界之中，但最好将其视为与物理世界相分离的现实。

最具表现力的建模范式能够自我参照，这使得它们能够不断地构建支撑自身的「脚手架」，但同时必然使得它们是不完备的。从根本上讲，正是这种不完备性激发了创造力，并确保我们能够运用技术完成的事情是无限的。那么到底是什么因素阻碍了我们呢？在本章，我既分析了进步过程中存在的障碍，同时也指出技术应用不当可能给社会带来的威胁。

### 03. Acknowledgments

The author gratefully acknowledges contributions and helpful suggestions from Christopher Brooks, Malik Ghallab, Thomas Henzinger, Madeline Johnson, Hokeun Kim, Gil Lederman, Marten Lohstroh, Dave Messerschmitt, Mehrdad Niknami, Rodion Rathbone, Rhonda Righter, Bernhard Rumpe, Naresh Shanbhag, Joseph Sifakis, Marjan Sirjani, Kimball Strong, David J. Stump, and Eli Yablonovitch. I would also like to thank three anonymous reviewers commissioned by the publisher who were extremely helpful. Several of these people disagreed with major points that I make in the book, and they thereby helped me to understand where my arguments needed to be strengthened or reworked. All remaining errors and opinions that I have stubbornly stuck to are entirely my own, not those of these contributors.

Most especially, however, I would like to thank two very special people who played a major role in the development of this book. The first is Heather Levien, who, unlike me, really knows how to write and without whom this book would be a disorganized pile of random ideas. The second is my mom, Kitty Fassett, a professional musician with an aversion for mathematics but a true intellectual and also a great writer. Without her help, this book would be unreadable to nonspecialists. She was my guinea pig, telling me each place where a nonspecialist might get lost.

I also thank the staff at MIT Press and Heather Jefferson for her superb copy editing. In addition, I thank the many unwitting contributors who have offered their thoughts through largely anonymous media such as Wikipedia and the contributors who have generously posted images online that I can (and have) reused because of their choice of creative commons licenses.

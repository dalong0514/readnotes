Copyright © 1998 by W. D. Hillis.

Hillis, W. Daniel.

The pattern on the stone : the simple ideas that make computers work / W. Daniel Hillis. — 1st ed.

书名：丹尼尔·希利斯讲计算机

出版时间：2021 年 1 月

## PREFACE: MAGIC IN THE STONE

I etch a pattern of geometric shapes onto a stone. To the uninitiated, the shapes look mysterious and complex, but I know that when arranged correctly they will give the stone a special power, enabling it to respond to incantations in a language no human being has ever spoken. I will ask the stone questions in this language, and it will answer by showing me a vision: a world created by my spell, a world imagined within the pattern on the stone.

A few hundred years ago in my native New England, an accurate description of my occupation would have gotten me burned at the stake. Yet my work involves no witchcraft; I design and program computers. The stone is a wafer of silicon, and the incantations are software. The patterns etched on the chip and the programs that instruct the computer may look complicated and mysterious, but they are generated according to a few basic principles that are easily explained.

Computers are the most complex objects we human beings have ever created, but in a fundamental sense they are remarkably simple. Working with teams of only a few dozen people, I have designed and built computers containing billions of active parts. The wiring diagram of one of these machines, if it were ever to be drawn, would fill all the books in a good-sized public library, and nobody would have the patience to scan the whole of it. Fortunately, such a diagram is unnecessary, because of the regularity of a computer's design. Computers are built up in a hierarchy of parts, with each part repeated many times over. All you need to understand a computer is an understanding of this hierarchy.

Another principle that makes computers easy to understand is the nature of the interactions among the parts. These interactions are simple and well-defined. They are also usually one-directional, so that the actions of the computer can be sorted neatly into causes and effects, making the inner workings of a computer more comprehensible than, say, the inner workings of an automobile engine or a radio. A computer has a lot more parts than a car or a radio does, but it's much simpler in the way the parts work together. A computer is not dependent so much on technology as on ideas.

Moreover, the ideas have almost nothing to do with the electronics out of which computers are built. Present-day computers are built of transistors and wires, but they could just as well be built, according to the same principles, from valves and water pipes, or from sticks and strings. The principles are the essence of what makes a computer compute. One of the most remarkable things about computers is that their essential nature transcends technology. That nature is what this book is about.

This is the book I wish I had read when I first started learning about the field of computing. Unlike most books on computers — which are either about how to use them or about the technology out of which they're built (ROM, RAM, disk drives, and so on) — this is a book about ideas . It explains, or at least introduces, most of the important ideas in the field of computer science, including Boolean logic, finite-state machines, programming languages, compilers and interpreters, Turing universality, information theory, algorithms and algorithmic complexity, heuristics, uncomutable functions, parallel computing, quantum computing, neural networks, machine learning, and self-organizing systems. Anyone interested enough in computers to be reading this book will probably have encountered many of these ideas before, but outside of a formal education in computer science there are few opportunities to see how they all fit together. This book makes the connections — all the way from simple physical processes like the closing of a switch to the learning and adaptation exhibited by self-organizing parallel computers.

A few general themes underlie an exposition of the nature of computers: the first is the principle of functional abstraction , which leads to the aforementioned hierarchy of causes and effects. The structure of the computer is an example of the application of this principle — over and over again, at many levels. Computers are understandable because you can focus on what is happening at one level of the hierarchy without worrying about the details of what goes on at the lower levels. Functional abstraction is what decouples the ideas from the technology.

The second unifying theme is the principle of the universal computer  — the idea that there is really only one kind of computer, or, more precisely, that all kinds of computers are alike in what they can and cannot do. As near as we can tell, any computing device, whether it's built of transistors, sticks and strings, or neurons, can be simulated by a universal computer. This is a remarkable hypothesis: as I will explain, it suggests that making a computer think like a brain is just a matter of programming it correctly.

The third theme in this book, which won't be fully addressed until the last chapter, is in some sense the antithesis of the first. There may be an entirely new way of designing and programming computers — a way not based on the standard methods of engineering. This would be exciting, because the way we normally design systems begins to break down when the systems become too complicated. The very principles that enable us to design computers lead ultimately to a certain fragility and inefficiency. This weakness has nothing to do with any fundamental limitations of information-processing machines — it's a limitation of the hierarchical method of design. But what if instead we were to use a design process analogous to biological evolution — that is, a process in which the behaviors of the system emerge from the accumulation of many simple interactions, without any「top-down」control? A computing device designed by such an evolutionary process might exhibit some of the robustness and flexibility of a biological organism — at least, that's the hope. This approach is not yet well understood, and it may turn out to be impractical. It is the topic of my current research.

In an explanation of the nature of computers, there are some fundamentals that have to be dealt with before we can move on to the good stuff. The first two chapters introduce the fundamentals: Boolean logic, bits, and finite-state machines. The payoff is that by the end of chapter 3 you'll understand how computers work, top to bottom. This sets the stage for the exciting ideas about universal computing machines, which begin in chapter 4 .

The philosopher Gregory Bateson once defined information as「the difference that makes a difference.」Another way of saying this is that information is in the distinctions we choose to make significant. In a primitive electrical calculator, say, information is indicated by light bulbs that go on or off depending on whether a current is flowing or not. The voltage of the signal doesn't matter, nor does the direction of current flow. All that matters is that a wire carries one of two possible signals, one of which causes a bulb to light. The distinction that we choose to make significant — the difference that makes a difference, in Bateson's phrase — is between current flowing and not flowing. Bateson's definition is a good one, but the phrase has always meant something more to me. In my lifetime of four decades, the world has been transformed. Most of the changes we've seen in business, politics, science, and philosophy in that time have been caused by, or enabled by, developments in information technology. A lot of things are different in the world today, but the difference that has made the difference has been computers.

These days, computers are popularly thought of as multimedia devices, capable of incorporating and combining all previous forms of media — text, graphics, moving pictures, sound. I think this point of view leads to an underestimation of the computer's potential. It is certainly true that a computer can incorporate and manipulate all other media, but the true power of the computer is that it is capable of manipulating not just the expression of ideas but also the ideas themselves. The amazing thing to me is not that a computer can hold the contents of all the books in a library but that it can notice relationships between the concepts described in the books — not that it can display a picture of a bird in flight or a galaxy spinning but that it can imagine and predict the consequences of the physical laws that create these wonders. The computer is not just an advanced calculator or camera or paintbrush; rather, it is a device that accelerates and extends our processes of thought. It is an imagination machine, which starts with the ideas we put into it and takes them farther than we ever could have taken them on our own.

## 再版前言 —— 计算机背后不曾改变的基本原理

本书初版问世很久之后，我的出版商惊讶地发现：它在当下仍然很受欢迎。这也是我有机会为本书写再版前言的原因。本书已被翻译为十几种语言，至今仍有众多读者。自本书问世以来，计算机技术及应用发生了天翻地覆的变化。不过本书并不着眼于计算机的具体技术及应用，而是关注计算机背后不曾改变的基本原理，这也是本书能持续热卖的关键所在。

我必须承认，令我感到诧异的不是在数字革命之初就已存在的那些关于计算机科学的原理如今依然很重要，而是迄今为止，几乎没有新的原理补充进来。10 多年过去了，虽然计算机技术及应用以及编程技术都取得了巨大进步，对社会产生的影响也远远超出了预言家的预期，但计算机背后的工作原理，即本书所阐述的关于计算机的概念，仍没有改变。我本来想利用再版的机会增添一些新内容，但令我感到吃惊的是，并无新的基本原理可供补充。

在目前的版本中，我选择性地删除了一些无须再费笔墨解释的概念。不过，这并非意味着这些内容是错误的。例如，在一个每天都享受云并行计算服务的读者看来，并行计算方面的内容并无新意。真正令人费解的是，为何 20 世纪有如此多的专家都坚信，并行计算机永远不会被投入使用。此外，如今的你们可能会对本书中有关人工智能的观点有所抵触，因为目前你们与智能机器相处得十分融洽。事实上，20 世纪时许多人对智能计算机的概念感到惶恐不安，比如，当计算机第一次击败人类国际象棋冠军时，许多人感到很沮丧。然而，过了不到 20 年，当计算机在一项流行的益智电视节目中再次击败人类冠军时，更多人开始为计算机鼓劲加油。从那时起，人们普遍将计算机视为助手而非威胁。

除了修订拼写错误之外，我尽可能地保持了本书初版的原汁原味，不去刻意提高文字的感性程度，实际上，感性是一种不断变化的浮动目标。与其紧跟必将过时的当下潮流，还不如让作品定格在某一时刻更为有趣。同时，本书写成于计算机科学发展历程中的一个特殊时期，虽然那时计算机已经显示出了足以改变我们生活的潜力，但这一切很大程度上还未实现。那时的计算机非常简单，以至于我对自己设计的计算机的每个晶体管和所编写的每行代码都了如指掌。不过，正如本书最后一章预期的那样，我们现在到达了一个临界点，即计算机系统的复杂度已经超出了任何人所能完全理解和掌握的程度。

关于未来的发展，本书提出了两个可能的方向。第一个是量子计算，正如书中所述，它具有巨大的潜力，但目前并无可行的实现方式。当我写下这句话时，现实情况仍是如此。从理论和技术方面来说，量子计算取得了巨大突破，但它们中的任何一个的计算速度都比不上传统计算机。正如本书初版所述，量子计算仍是「一个值得关注的领域」。本书预测的第二个可能方向是，计算机能像生物进化过程那样实现自我设计。目前，这个方向已经显现出了隐约的曙光，不过在很大程度上，它只是一个未实现的可能方案。目前，我们还缺乏相关理论来说明这个过程如何才能成为现实。我对未来发现这些新原理持乐观态度，期待能够在本书的后续版本中继续讨论。

## 前言 —— 石头中的魔术

在一块石头上，我蚀刻了一系列几何图案，在外行看来，这些图案显得神秘而又复杂，但我清楚地知道，只要布局正确，这些图案就会赋予这块石头一种特殊的能力，即对人类从未说过的一种咒语做出回应。如果我用这种语言提问，石头便会应答：这是一个我用符咒创造的世界，一个在石头图案中想象的世界。

如果我在几百年前的老家新英格兰说出自己从事的职业，可能会被当作巫师送上火刑柱。实际上，我的工作和巫术没有任何关系，我从事的是计算机设计和编程，而上文提到的石头是硅晶片，符咒是软件程序。虽然蚀刻在芯片上的几何图案和指示计算机工作的程序看起来复杂且神秘，但根据一些基本的生成原理，我们很容易将其解释清楚。

虽然计算机是人类有史以来最复杂的人造物，但从基本原理上来说，它们又十分简单，仅有数十人的团队就能设计并制造出包含数十亿个零部件的各类计算机。如果将其中一台计算机的线路图在纸上画出来，那么所用的纸张便能塞满一座大型公共图书馆，没有人会有耐心将其浏览一遍。幸运的是，计算机的设计具有规律性，没有必要将线路图看一遍。计算机是由不同层次的部件构建起来的，而每一层次的部件都会被重复多次。只要理解了这些层次结构，你就能读懂计算机。

还有一个使计算机易于理解的原理，那就是其各部件之间交互作用的本质。这些交互作用很简单，而且定义明确，通常具有单向性，可以准确地排列成一系列因果关系，这使计算机内部的运行原理比汽车发动机或者收音机的运行原理更容易理解。虽然相比于汽车和收音机，计算机拥有更多零部件，但这些部件协同工作的方式非常简单。计算机更多依据的是概念，而非技术。

这些概念与组成计算机的电子元件没有任何关系。现代计算机由晶体管和电路组成，不过，根据同样的原理，计算机也可以由阀门和管道，或者棍棒和绳索搭建起来。这些原理是计算机能够进行计算的根本所在。计算机最引人称道的一点是，其本质远胜于技术，而本书就旨在介绍计算机的本质。

我多么希望在刚开始学习计算机这门学科时就能读到这样一本书。大多数计算机类书籍不是介绍计算机的使用方法，便是介绍具体的创造技术，比如只读存储器（ROM）、随机存储器（RAM）、磁盘驱动器等。这本书讨论的重点是「概念」，而且会介绍计算机科学领域的大多数重要概念，包括布尔逻辑、有限状态机、编程语言、编译程序和解释程序、图灵准则、信息论、算法及其复杂度、启发式方法、不可计算的函数、并行计算、量子计算、神经网络、机器学习和自组织系统等。对计算机感兴趣的读者可能已经听说过其中的许多概念，但对于非计算机专业出身的人来说，很难明白这些概念是如何结合在一起的。本书将会介绍这些关联 —— 从类似开关的闭合等简单的物理过程开始，一直深入到自组织并行计算机所呈现出来的学习和自适应能力。

计算机的本质基于几条基本原则。第一条原则是功能抽象原理（functional abstraction），它奠定了前文提到的因果关系层次结构。计算机的结构就是这一原理的应用范例，即许多层次结构能够被不断重复。计算机之所以易于理解，是因为你可以专注于某一层次结构发生的情况，而不必担心较低层次结构上发生的细节。功能抽象原理是使概念与技术脱离的关键。

第二条原则是通用计算机原理（universal computer），即所有的计算机都属于同一种类型，更确切地说，所有类型的计算机在能做和不能做哪些事上是相似的。我们也可以这样说，一台通用计算机能够模拟所有类型的计算机，无论其组成材料是晶体管、棍棒、绳索，还是神经元。这是一个非常重要的假设，它表明，制造一台能像大脑一样思考的计算机只是一个进行正确编程的问题，我将在后面详细解释这一点。

从某种意义上来说，第三条原则是第一条原则的对立面，我将在最后一章展开详述。也许存在一种全新的计算机设计和编程方式，它并不基于标准的工程设计方式。这一设想令人感到无比兴奋，因为当系统过于复杂时，常规的系统设计方式将不再有效。实际上，第一条原则会导致系统带有一定程度的脆弱性和低效性。这个缺点与信息处理器的基础性缺陷没有关系，而是层次设计方式的一个缺陷。那么，如果我们采用一种与生物进化相似的设计过程，情况会如何呢？在这个设计过程中，系统行为源自很多简单交互作用的累积，而非「自上而下」的控制。通过这种进化过程设计出来的计算机可能具有生物体的某些健壮性和适应性。至少，这是一种希望。我们还未完全参透这一设计方式，它也可能会被证明行不通。这是目前我研究的一个课题。

为了全面了解计算机的本质，我们需要先掌握一些基本知识，再研究深层次的内容。本书前两章将介绍以下基本内容：布尔逻辑、二进制和有限状态机。在读完第 3 章时，你便能自上而下地理解计算机的工作原理。这也为理解第 4 章的内容奠定了基础，第 4 章将介绍有关通用计算机的有趣概念。

哲学家格雷戈里·贝特森（Gregory Bateson）曾将信息定义为「非同小可的差异」。换句话说，信息存在于我们选择用来表示意义的差异之中。例如，在原始的电子计算器中，信息是以电流流通与否造成的灯的开启和关闭来表示的，而信号的电压和电流方向则无关紧要。这其中起关键作用的是一根能够传输两种可能的信号的线路，其中一种信号是让灯亮起。在这里，产生关键作用的差异之处，也就是贝特森所说的「非同小可的差异」，就是电流的流通与否。贝特森给出的定义很明确，这个定义于我而言有着更为丰富的含义。在短短几十年间，世界发生了翻天覆地的变化。信息技术的发展引发或者促成了我们在商业、政治、科学和哲学领域所目睹的许多变革。当今世界，许多事情已异于往昔，而这一非同小可的变化皆源自计算机。

人们普遍认为，计算机是一种能够融合文本、图像、动画、声音等所有已有形式的多媒体设备。然而我认为，这一观点低估了计算机的潜力。计算机当然能够综合处理各种形式的媒体，但其真正的威力是它不仅能处理概念的表示形式，而且能处理概念本身。计算机最令我震惊的地方不在于它能够储存图书馆中所有书籍的内容，而在于它能够识别并总结出书中所述的各种概念之间的关系；不在于它能展示出飞鸟或者星系自旋的图像，而在于它能猜想并预测出创造了这些奇迹的物理定律将会产生的结果。计算机不只是一台先进的计算器，或一架高级的照相机，或一支具有神奇功能的画笔，它更是一种能够加速和扩展思维过程的工具。计算机是一架富有想象力的机器，它从我们输入的概念演变为人类从未抵达的情境。
## 0501. Software Endures

· · · in which I argue that the layers of paradigms for software are so deep that the physical world largely becomes irrelevant; that software reflects the personalities and idiosyncrasies of its creators; that software endures much better than hardware in no small part because it encodes its own layered paradigms; and that connected machines in server farms dream.

0501 软件的持久力

在这一章，我会讨论软件的范式层次如此之深，以至物理世界在很大程度上变得无关紧要了；软件反映了其创造者的个性和特质；软件在很大程度上要比硬件耐久，这是因为它编码了自己的分层范式；在服务器群组之梦中连接的机器。

### 5.1 Self-Scaffolding

In principle, engineers who wish to write programs could set individual bits in the program memory to get the hardware to do their bidding. In practice, this would be mind-numbingly tedious. A typical program might consist of, say, 10 million bits stored in program memory. That's a lot of zeros and ones. No human could write those zeros and ones without making many, many errors.

The bit patterns that constitute a program are called machine code . They are meant for the machine to read, not for the human designer to write. So how do they get written? How does a human designer build a program like a word processor or a system like Wikipedia? Here's where the next stack of abstractions comes into play, those focused on software.

A modern computer program will typically consist of hundreds or thousands of「modules」or「packages,」each of which consists of dozens or hundreds of「classes,」each of which has dozens or hundreds of「methods,」each of which has dozens or hundreds of lines of code. The lines of code are written in a programming language that is translated by a compiler into machine code (often indirectly, first translating into another language, then another language, then to machine code). These layers of design are essential to being able to form any sort of understanding of the behavior of the program.

Way back in 1972, Edsger Dijkstra, a Dutch computer scientist, then a mathematics professor at the Eindhoven University of Technology in The Netherlands, described software as a「hierarchical system,」which he defined by analogy,

We understand walls in terms of bricks, bricks in terms of crystals, crystals in terms of molecules, etc. (Dijkstra, 1972)

He then observed that the number of levels in such hierarchical abstractions is small unless the「ratio between the largest and the smallest grain」is large. The number of molecules in a wall is very large, and yet Dijkstra gives us only four layers.

For the structure of programs, the ratio between a bit of machine code and a program may easily be in the millions. However, in addition, there is layering in the temporal behavior of a program. An individual line of code may execute in a few nanoseconds, whereas the overall function of the program may span hours, days, or months. Dijkstra comments on this ratio:

I do not know of any other technology covering a ratio of 10 10 or more: the computer, by virtue of its fantastic speed, seems to be the first to provide us with an environment where highly hierarchical artifacts are both possible and necessary. (Dijkstra, 1972)

To assess Dijkstra's「ratio between the largest and the smallest grain」for software, we need to combine three effects. A computer program may have a million lines of code and get translated into a few million bits of machine code. The machine code is executed on a chip that has billions of transistors, each acting as a switch. And these switches are switching billions of times per second. If the smallest grain is the switching of a transistor and the largest is the computer program, then the ratio is at least 10 24 or

1,000,000,000,000,000,000,000,000.

This number is large for something made by humans. Hence, by the time we get to software, we are quite distant from the physical world.

At this point, it ceases to be useful to think of software as a physical phenomenon. It is instead what Hal Abelson and Gerry Sussman call「procedural epistemology」in their introductory computer science book, Structure and Interpretation of Computer Programs (Abelson and Sussman, 1996). Software becomes an abstract medium for human creativity and craftsmanship and starts to more closely resemble Searle's cognitive phenomena than the physical phenomena out of which it originates. Software becomes a medium for human expression, not just technical, but also cultural, literary, and artistic. It is of course ultimately realized in the physical world by electrons sloshing around. In words that Connor calls「startlingly sacramental,」Serres invokes the Bible when talking about the coalescence of the soft model of software and hard matter that it runs on:

Et verbum caro factum est . (Serres, 2001, p. 78)

And the word was made flesh.

With such a huge difference in scale of the largest and smallest grain sizes, layers of modeling become essential. Unlike the scientific effort that Searle criticizes to explain preexisting sociological phenomena such as money in terms of neurophysiology, our enterprise here is engineering not science. We only need to explain the phenomena we construct, not ones given to us by nature. As humans, we construct software and all the layers below, down to the transistors. It is much easier to explain a phenomenon that we have constructed in terms of a lower level phenomenon that we have also constructed, particularly because the lower level phenomenon was constructed in part to support the upper level one.

Each layer of modeling is governed by a paradigm. A programming language, for example, is such a paradigm. It shapes the programmer's thinking and provides the framework for procedural epistemology. The programming language is a human invention and often reflects the creativity and idiosyncrasies of its inventors.

As a paradigm, a programming language has an interesting property. Specifically, the language can be used, and often is used, to encode its own paradigm. Specifically, a program is translated into a lower level language, such as machine code, by a compiler. Assuming that the machine code is well defined, the compiler encodes the meaning of the programming language and hence encodes its paradigm. But the compiler can usually be written in the very language that it compiles! In fact, it is a common litmus test for a language to be deemed worthy that it be able to encode its own compiler. According to Wikipedia, at least the following languages have compilers written in their own language: BASIC, ALGOL, C, D, Pascal, PL/I, Factor, Haskell, Modula-2, Oberon, OCaml, Common Lisp, Scheme, Go, Java, Rust, Python, Scala, Nim, and Eiffel.

This kind of self-scaffolding of paradigms, I believe, is unique to software among other technologies. It seems to approach Searle's description of sociological phenomena, where「the concept that names the phenomenon is itself a constituent of the phenomenon.」And it pervades software from the lowest to the highest layer. At the lowest layer, a microprocessor includes a「boot loader,」a tiny built-in program that is executed when the microprocessor is first powered up. The term「boot loader」is a reference to bootstrapping, a term that, according to Wikipedia,

· · · appears to have originated in the early 19th century United States (particularly in the phrase「pull oneself over a fence by one's bootstraps」), to mean an absurdly impossible action · · · [retrieved April 30, 2016]

At a much higher layer in software, I quoted earlier the Wikipedia page on Wikipedia, itself a form of self-scaffolding. At intermediate levels, to reboot an operating system, something all of us have done, is also a reference to bootstrapping. The operating system uses its own services to start the operating system itself.

In the rest of this chapter, I will explain a few of the layers of modeling that we commonly use in software technology. I hope these explanations will be somewhat less nerdy than the hardware layers of the previous chapter in part because they are more idiosyncratic. I will describe these layers not as facts about the world but as inventions by humans. But I again apologize in advance for the brief nerd storms that I have been unable to keep out of this book. As in the previous chapter, I will progress from lower layers to the upper ones.

5.1 自我支撑

编写程序的工程师原则上可以在程序存储器中设置单独的比特位，以使硬件能够执行他们的命令。在实践中，这是一件极其乏味的工作。一个典型的程序可能是程序存储器中的 1 000 万个比特位，那是很多很多的「0」和「1」。没有人能够在不犯很多很多错误的情况下写出这些「0」和「1」。

构成程序的比特模式被称为机器码。它们是供机器读取的，而不是让设计人员来编写的。那么它们又是怎么被编写出来的呢？设计人员是如何构建出一个文字处理器或维基百科这样的系统的？这就是下一组堆叠的抽象要发挥作用的地方了，它们聚焦于软件。

现代计算机程序通常由成百上千或成千上万个「模块」或「包」组成，其中每个「包」有数十或成百上千个「类」，每个「类」又有几十或成百上千个「方法」，而每个「方法」则有数十行或成百上千行代码。代码行是用某种编程语言编写的，并由编译器将其翻译成机器码（首先转换为另一种语言，然后再转换为机器码，这些转换通常是间接的）。设计中的这些层次对于能够从任何层理解程序的行为都是至关重要的。

早在 1972 年荷兰计算机科学家艾兹格·迪杰斯特拉在荷兰埃因霍芬理工大学任数学教授时，他就把软件描述为「分层系统」，并以下面的类比定义这个系统：

我们通过砖块来了解墙壁，通过晶体来了解砖块，通过分子来了解晶体。（迪杰斯特拉，1972）

然后，他注意到，除非「最大粒度与最小粒度之间的比率」较大，否则这种分层系统中的层数会很少。墙壁中的分子数量巨大，但是迪杰斯特拉只为我们给出了 4 个分层。

对于程序的结构而言，机器码的一个比特与一个程序之间的比率可能很容易就达到数百万。此外，程序的时间行为也是分层的。单行代码可以在几纳秒内完成执行，而程序的总体功能可能需要几个小时、几天或几个月。迪杰斯特拉对这一比率做了如下评论：

我不知道还有没有其他技术能具有 1010

或更大的比率：计算机以其惊人的速度，似乎是第一个为我们提供了一种环境，在这里高度分层的人工制品成为可能的和必要的。（迪杰斯特拉，1972）

为了评估迪杰斯特拉关于软件的「最大和最小粒度之间的比率」，我们需要综合考量三个因素。一个计算机程序可能包括 100 万行代码，并被翻译成几百万条机器码。机器码是在一个芯片上被执行的，该芯片上有数十亿个晶体管，每个晶体管充当一个开关。这些开关每秒切换数十亿次。如果最小粒度是晶体管的开关切换，最大的是计算机程序，那么它们之间的比率至少是 1024

或者下面这个数字：

1 000 000 000 000 000 000 000 000

这个数字对于人类制造的东西而言实在是太大了。因此，当我们开始接触软件的时候，我们实际上已经远离了物理世界。

此时，再把软件视为一种物理现象已经没用了。哈罗德·阿贝尔森和杰伊·萨斯曼在其计算机科学的入门书《计算机程序的构造和解释》中将软件称为「程序认识论」（阿贝尔森和萨斯曼，1996）。软件成为人类施展创造力和技能的一个抽象媒介，它更接近约翰·塞尔的认知现象，而不是作为其起源的物理现象。软件成为人类表达思想的媒介，不仅体现在技术上，还表现在文化、文学和艺术等方面。当然，它最终是通过物理世界的电子流动实现的。在康纳所说的「令人有些震惊的神圣感」中，当谈到软件的软模型和它所运行的硬物质的结合时，米歇尔·塞尔引用了《圣经》中的话：

道成了肉身。（米歇尔·塞尔，2001:78）

由于最大和最小粒度在规模上的巨大差异，分层建模就变得至关重要了。我们致力于工程而不是科学，与塞尔批评的从神经生理学角度解释诸如金钱等先前存在的社会学现象的科学努力不同，我们在这里要关注的是工程而不是科学，我们只需要解释我们所构造的现象，而不是大自然赋予我们的那些现象。作为人类，我们构建软件及其下面的所有层，直到晶体管。用我们构造的一个较低层的现象来解释我们构造的现象要容易得多，特别是因为较低层的现象部分地是为了支持较高层的现象而构造的。

建模的每一层都会受到一个范式的支配。例如，编程语言就是这样一种范式。它塑造了程序员的思维，并为程序认识论提供了框架。编程语言是人类的发明，它通常反映了发明者的创造力和特质。

作为一种范式，编程语言具有一个有趣的特性。具体来说，编程语言可以而且经常被用来编码它自己的范式。例如，程序被编译器翻译成较低级别的语言，例如机器码。假设机器码是定义良好的，编译器就会对编程语言的含义进行编码，从而对其范式进行编码。但是编译器通常可以用它所编译的语言编写！事实上，一种语言能否对自己的编译器进行编码，是一种常见的试金石。根据维基百科，至少以下语言的编译器是用其本身编写的，包括 BASIC、ALGOL、C、D、Pascal、PL/I、Factor、Haskell、Modula-2、Oberon、OCaml、Common Lisp、Scheme、Go、Java、Rust、Python、Scala、Nim 以及 Eiffel。

我相信，这种范式的自我支撑是软件所特有的。这似乎接近塞尔对社会学现象的描述，「命名现象的概念本身就是现象的组成部分」。从最低层到最高层，软件都是如此。在最低层，微处理器包括了一个「引导加载程序」，这是一个很小的内置程序，该程序在微处理器第一次启动时被执行。「引导加载程序」一词指的是自引导（也称自举），在维基百科中有如下说明。

…… 这个词似乎起源于 19 世纪初的美国（特别是在「通过拽自己靴子上的鞋带，把自己提起来越过栅栏」这样的句子），指的是一个荒谬的不可能的行为……（2016 年 4 月 30 日检索）

站在软件的更高层次，我在前面引用了维基百科上的维基百科页面，它本身就是一种自我支撑的形式。在中间层次上，重新启动操作系统，这是我们所有人都做过的事情，也是指自引导。操作系统使用自己的服务启动操作系统本身。

在本章的其余部分，我将解释我们通常在软件技术中使用的建模层。我希望这些解释不会比前一章对硬件建模层的解释更乏味，部分原因是它们更为特殊。我不把这些层描述为关于世界的事实，而是把它们视为人类的发明。这部分也许还会涉及一些技术呆子式的头脑风暴。真是抱歉，为了让读者更好地理解这些内容，我不得不如此。和前一章一样，我将先从较低的层开始解释，逐步到更高的层次。

### 5.2 Instruction Set Architectures

Fred Brooks, working at IBM in the 1960s, is credited with developing the idea of an instruction set architecture (ISA), which abstracts what the hardware in a computer does. When a computer executes a program, it executes a sequence of instructions. An instruction may, for example, compare two numbers. Another instruction may specify which instruction to execute next based on the outcome of the comparison. The set of instructions that a computer can execute is called, not surprisingly, its「instruction set.」Before Brooks, every distinct model of computer had a different instruction set.

In the 1960s, IBM was developing a family of computers called the System/360 family. One of the goals of the System/360 project was to produce a diverse product line of computers that could all execute the same programs. That is, once you had a bit pattern to put into the instruction memory, that same bit pattern would work on an entry-level computer and on a more advanced, more expensive model. This means that multiple distinct hardware designs all need to interpret programs, stored as bit patterns, in the same way. The hardware could vary by executing programs faster or slower or by providing more or less memory, but the basic functionality of the program should be the same on all instances of the hardware.

To accomplish this, Brooks proposed a standardized「architecture,」a specification that defines a fixed instruction set and the bit pattern encoding each instruction. The resulting instruction set architecture is called the IBM System/360 ISA.

It's worth an aside to understand how different Fred Brook's world of computers was compared with ours today. A typical IBM 360, the model 25, could be rented for $5,330 a month or purchased for $253,000 in 1968 (equivalent to about $35,800 and $1.7 million in 2016). The model 25 was aimed at users of「small and medium sized computers」(IBM, 1968). In its largest configuration, its main memory contained 48,000 bytes (each byte is 8 bits). By contrast, the main memory on the laptop I am using to write this book has about 16 billion bytes, and the purchase price was about $2,000.

Despite the enormous differences in cost and scale, Brooks' basic idea of an ISA persists almost unchanged to this day. The ISA used in the laptop on which I am typing this text is called the「x86」instruction set. It was originally introduced in 1978 in the Intel 8086 microprocessor, about 10 years after the IBM 360 first appeared. A variant of the 8086 called the Intel 8088 was used in the first IBM PC, introduced in 1981, shown in figure 5.1 .

The x86 ISA grew over time, but it grew in a「backward compatible」way, meaning that an Intel 80186, 80286, 80386, 80486, and many other microprocessors could all execute programs that were written for the 8086. The Haswell processors shown in figure 3.2 are also x86 processors.

Figure 5.1

Original IBM Personal Computer, model 5150. [Image licensed under CC BY-SA 3.0 by Ruben de Rijcke. From https://commons.wikimedia.org/w/index.php?curid=9561543 .]

The astonishing persistence of the x86 ISA is a real testament to the power of Brooks' idea. Ironically, the hardware becomes transient, disposable after a few years, and the software endures for decades. Even the word「endure」underscores the irony because this word originates from the old French usage, where「dure」means「hard,」and to build a「durable」building, one builds it out of hard material such as stone. Yet in computing, software endures much better than hardware.

Let me illustrate how an ISA abstracts the hardware. Suppose, for example, that one of the tasks for the machine whose hardware is depicted in figure 4.6 is to compare two numbers. If the numbers are equal, then it should branch to a different part of the program. If the numbers are unequal, then it should continue executing the sequence of instructions that it is currently executing. This might be part of the search function on Wikipedia, for example, or a search for the occurrence of a word in a text.

Figure 5.2 shows a small segment of a program for an x86 machine. In the figure, each box represents an instruction. The machine executes the instructions one after the other, from top to bottom. The grey boxes represent arbitrary, unspecified instructions. Two specific instructions are shown. The first is

cmp      eax, ebx

This instruction compares the contents of two registers named「eax」and「ebx.」These two registers contain 32-bit numbers; prior to executing this instruction, the program has presumably loaded these registers to contain the numbers representing the characters we are searching for. For example, the characters「Plat」can be loaded into a 32-bit register, assuming that each character is encoded with 8 bits.

Figure 5.2

Small fragment of x86 assembly code.

The previous instruction is written in assembly language, a textual specification that has to be translated into machine code. The machine code for this instruction is

0011010111010100

The text in the figure is translated into this binary representation by a program called an「assembler.」The「cmp」word is called a「mnemonic」because it is easier to remember than「0011010111010100.」

If I may digress briefly, I would like to comment on the culture of programmers. In the 1960s and 1970s, the memory in computers was much smaller than it is today. At that time, it was advantageous to represent an instruction with the mnemonic「cmp」rather than「compare」because「cmp」requires only 24 bits to store, whereas「compare」requires 56. Today, memory is plentiful, but engineers still feel compelled to use short cryptic mnemonics rather than complete words. They will write「fun」rather than「function,」「len」rather than「length,」and「buf」rather than「buffer.」I personally find this an amusing (and sometimes annoying) cultural relic.

The other instruction explicitly shown in figure 5.2 is

je       label

The mnemonic「je」stands for「jump if equal,」and the argument「label」tells the assembler where in the program to jump to if the registers compared by the previous instruction are equal.

There are aspects of this design that seem quite arbitrary, besides the cosmetic choice of mnemonics. For example, why did the designers of the x86 instruction set choose to first compare and then jump in two separate instructions? Why didn't they combine these into a single instruction, such as

je       eax, ebx, label

They could have done this, but it would have complicated the hardware design because now a single instruction needs to encode four things: the「jump if equal」command, the two registers to compare, and the destination address. The engineering problem that the designers of the x86 architecture were solving straddled two levels of abstraction: the hardware design at the digital machine level, as in figure 4.6 , and the instruction set that would be used to specify programs. The phenomenon of assembly language and the lower level phenomenon of the computer hardware affect each other with bidirectional causality.

Engineers who work at these levels are called「computer architects.」There is a long and rich history of architectures, most of which have not survived in the marketplace, and some of which operate in very different ways. So-called「dataflow computers,」for example, don't even specify programs as sequences of instructions (Arvind et al., 1991). Today, a small handful of instruction set architectures dominate (x86, ARM, SPARC, MIPS, RISC-V, and few others).

Although a computer architect operates at a level quite separated from the「sciences of the natural,」ample opportunity exists to use the scientific method to optimize computer architectures. Hennessy and Patterson (1990) revolutionized the field of computer architecture by advocating in their textbook a「quantitative approach,」which amounted to systematic use of experiments. A computer architect can form a hypothesis that a particular choice of instruction set design will improve performance and then design experiments to measure the performance on actual programs. This could be done using programs found「in the wild,」but these days it is done instead with standardized benchmark suites. The programs in such a suite are idealized models of real programs that attempt to capture their essential features.

The concept of an instruction set architecture brings us safely across the boundary from hardware to software. It is now possible to build applications by writing textual programs. But doing so in assembly language is not a good idea. The programs are too difficult to understand at such a low level of abstraction. To bring up the level of abstraction, computer scientists invented programming languages.

5.2 指令集体系架构

早在 20 世纪 60 年代，在 IBM（国际商业机器公司）工作的小弗雷德里克·布鲁克斯就创建了指令集体系架构（ISA）的概念。该架构对计算机硬件的功能进行了抽象。当计算机执行一个程序时，它执行一系列指令。例如，一条指令可能对两个数进行比较，另一条指令则可以根据比较的结果指定下一步要执行的指令。毫无疑问，一台计算机可以执行的一系列指令被称为它的「指令集」。在布鲁克斯之前，每一种不同的计算机模型都有不同的指令集。

在 20 世纪 60 年代，IBM 开发了一个名为 System/360 的计算机系列产品。System/360 项目的目标之一是生产能够执行相同程序的各种计算机产品线。也就是说，一旦你有一个可以放入指令存储器的比特模式，那么，同样的比特模式在入门级计算机、更高级更昂贵的计算机上都能运行。这意味着多种不同的硬件设计都需要以相同的方式解释存储为比特模式的程序。硬件可能因执行程序的快或慢、提供存储器的多或少而有所不同，但是在硬件的所有实例上，程序的基本功能都应该是相同的。

为了实现这一点，布鲁克斯提出了一个标准化的「体系结构」，它是一种定义了一个固定指令集和编码每条指令的比特模式的规范。之后产生的指令集体系结构被称为 IBM System/360 ISA。

值得一提的是，布鲁克斯的计算机世界与我们今天的相比有很大的不同，大家非常有必要知道这一点。作为典型的 IBM 360 系列计算机，model 25 在 1968 年可以以每月 5 330 美元的价格被租用，或以 25.3 万美元的价格被购买（相当于 2016 年的 3.58 万美元和 170 万美元）。model 25 的目标客户是「中小型计算机」用户（IBM，1968）。在其最大配置中，主存包含 4.8 万个字节（每个字节是 8 比特）。相比之下，我用来撰写这本书的笔记本电脑的主存大约有 160 亿个字节，这台电脑的售价约为 2 000 美元。

尽管在成本和规模上存在着巨大的差异，但布鲁克斯有关指令集体系架构的基本思想一直沿用至今。我正在输入当前内容的笔记本电脑使用的指令集体系结构被称为「x86」指令集。它最初是在 1978 年英特尔的 8086 型微处理器中被引入的，大约比 IBM 360 计算机的问世晚了 10 年。英特尔公司在 1981 年推出的第一台 IBM PC 中使用了 8086 型微处理器的一个变体 —— 英特尔 8088（如图 5.1 所示）。

图 5.1 IBM 最早的个人电脑，型号 5150。（图片由鲁本·德·里克提供，并获得 CC BY-SA 3.0 授权。图片来自 https://commons.wikimedia.org/w/index.php?curid=9561543。）

x86 指令集的规模随着时间的推移而不断增长，但它是以「向后兼容」的方式增长的。这意味着英特尔 80186、80286、80386、80486 和许多其他微处理器都可以执行为 8086 编写的程序。图 3.2 所示的 Haswell 系列处理器也是 x86 处理器。

x86 指令集体系架构惊人的生命力强有力地证明了布鲁克斯的想法的威力。具有讽刺意味的是，硬件的生命力变得短暂，用几年就得更换，而软件却可以持续使用几十年。甚至连「endure」这个词也凸显了讽刺意味，因为这个词源于古法语用法，「dure」的意思是「坚硬」（hard），而要建造一座「耐久的」建筑，就得使用石头等坚硬的材料。然而，在计算机领域，软件要比硬件耐久得多。

下面，我来说明指令集体系架构是如何抽象硬件的。举例来说，假设硬件如图 4.6 所示的机器的任务之一是比较两个数。如果这两个数相等，那么它应该跳转到程序的另一部分。如果不相等，则应继续执行当前正在执行的指令序列。例如，这可能就是维基百科搜索功能的一部分，或者是搜索文本中出现的一个单词的功能部分。

图 5.2 给出了 x86 计算机程序中的一个小片段。在图中，每个框代表一条指令。机器从上到下依次执行这些指令。灰色框表示任意的、未指定的指令。图中给出两个具体指令，其中的第一条是：

cmp eax, ebx

该指令比较两个寄存器「eax」和「ebx」的内容。这两个寄存器中存放了 32 位数；在执行这条指令之前，程序大概已经加载了这些寄存器，以包含表示我们正在搜索的字符的数字。例如，可以将字符串「Plat」加载到 32 位寄存器中，假设每个字符都采用 8 位编码。

图 5.2 x86 汇编代码的小片段

上面的指令是用汇编语言编写的，这是一种专业的文本规范，必须被翻译成机器码。这条指令的机器码为：

0011010111010100

图中的文本被称为「汇编器」的程序转换成这种二进制表示形式。

「cmp」这个词被称为「助记符」，因为它比「0011010111010100」更容易被记住。

请允许我稍稍拓展一下，我想谈谈程序员的文化。在 20 世纪 60 年代和 70 年代，计算机的存储器要比现在小得多。在当时，使用助记符「cmp」要比「compare」更有优势，因为存储「cmp」只需要 24 比特，而「compare」需要 56 比特。今天，计算机的存储容量大幅增加，但工程师仍然觉得必须使用简短而神秘的助记符而不是完整的单词。他们更愿意写「fun」、「len」和「buf」，而不是完整的「function」、「length」和「buffer」。我个人认为这是一个有趣（有时又有点儿令人讨厌）的文化遗产。

图 5.2 中明确给出的另一条指令是：

j e label

助记符「je」表示「如果相等就跳转」，参数「label」告诉汇编器，如果前一条指令所比较的寄存器是相等的，则程序要跳转到程序的哪个位置。

除了这种注重形式的助记符选择，这种设计还有一些方面看起来相当随意。例如，为什么 x86 指令集的设计者会选择在两条指令中进行先比较再跳转的操作呢？为什么他们不把这两步合并成一条指令呢？例如下面的指令：

j e eax, ebx, label

他们本来可以这样做，但是这会使硬件设计变得复杂，因为现在一条指令需要编码 4 种东西：「jump if equal」（如果相等就跳转）命令、要比较的两个寄存器以及目标地址。x86 架构的设计者要解决的工程问题跨着两个抽象层：数字机器层的硬件设计（如图 4.6 所示）和用于设计程序的指令集。汇编语言现象和计算机硬件底层现象受双向因果关系支配而相互影响。

工作在这些层的工程师被称为「计算机架构师」。计算机体系架构有着悠久而丰富的历史，其中大多数都没有在市场上留存下来，而其中的一些则以非常不同的方式运行着。例如，所谓「数据流计算机」甚至不把程序表示为指令序列（阿尔温德等，1991）。今天，只有少数指令集体系架构占据着主导地位（包括 x86、ARM、SPARC、MIPS、RISC-V 以及少数其他架构）。

尽管计算机架构师工作在一个与「自然科学」完全分离的层次上，但他们仍有大量的机会利用科学方法来优化计算机体系结构。亨尼西和帕特森（1990）在他们的教科书中开创性地提倡一种「定量方法」，即系统地使用实验，从而在计算机体系架构领域掀起了一场革命。

计算机架构师可以建立一种假设，即特定的指令集设计选择将提高计算机的性能，然后设计不同的实验来测量实际程序的性能。这可以通过一些非常规的测试程序完成，但是现在它是用标准化的基准测试套件来完成的。这种套件中的程序是真实程序的理想化模型，它们试图呈现这些真实程序的基本特性。

指令集体系架构的概念使我们安全地跨越了从硬件到软件的界限。现在，我们就可以通过编写文本程序来构建应用程序。但用汇编语言来构建应用程序并不是一个好主意。在这么低的抽象层上，要理解这些程序是非常困难的。为了提高抽象的层次，计算机科学家发明了编程语言。

### 5.3 Programming Languages

Fred Brooks, crediting Aristotle, in a famous paper titled No Silver Bullet—Essence and Accidents of Software Engineering , made a distinction between accidental complexity and essential complexity (Brooks, 1987). Essential complexity, Brooks argues, is the complexity inherent in the problem that we are asking the software to solve. Accidental complexity arises from the difficulties that「today attend [software] production but are not inherent.」

If I were asked to write this book using a keyboard with only two keys labeled「0」and「1,」I could, in principle, do so. The computer, after all, stores this entire book as a sequence of zeros and ones. But it would be difficult to write a book this way. The reality is that this book is difficult enough to write without having to deal with such accidental complexities.

Following Brooks, I would argue that the essential difficulties in writing this book center on how to weave an accessible story around highly technical topics. The technology I have at my disposal has probably removed nearly all of the accidental complexities around this task. I have a QWERTY keyboard, and I can touch type quite fast. I have excellent, free, open-source word processing software ( ).

When I can't recall what exactly it is that Fred Brooks said in his silver bullet paper, I just go to Google and search for「silver bullet,」and I quickly have the paper right in front of me. The only remaining difficulties are the essential ones that follow from the possibly quite controversial cases that I'm trying to make, including the one here, that technology development is a fundamentally creative human activity driven by culture and aesthetics and built on models that are human fabrications much more than discovered natural laws. Only the difficulty of making this case makes writing this book difficult.

The engineered systems that help me, my laptop computer, , Wikipedia, and Google, are human constructions of astonishing complexity. The engineers responsible for them relied on tools that also removed many of the accidental complexities, enabling them to focus on the essential complexities. Jimmy Wales and Larry Sanger, who created Wikipedia, did not write their programs in binary or even assembly language. In fact, they used several additional layers of models.

The next layer above ISAs and assembly language is the programming language. In late 1953, John W. Backus at IBM started a project to develop an easier language for expressing programs, particularly those extensively using mathematical expressions. The result of this project was Fortran, a language that endures to this day, with the latest update to the language occurring in 2008.

In Backus' time,「Fortran」was written「FORTRAN.」In fact, most everything was written using only capital letters because if you restrict the alphabet to only capital letters, then each letter can be encoded with fewer bits, saving memory. Like the curt mnemonics of assembly code, the use「all caps」became a bit of a cultural relic. My late colleague Chittoor Ramamoorthy, a charming man who went by「Ram」and contributed a great deal to the field of computer architecture, persisted until his death in 2016 in using only capital letters in all his communications, seemingly oblivious to the cultural shift where the use of all caps became yelling.

Figure 5.3 shows a single Fortran statement on a punched card. In the 1950s and 1960s, punched cards were both a storage medium (a stack of cards was a record of the program) and a data entry mechanism. This card reveals one of the key innovations of the Fortran language, which is the use of symbolic variable names rather than memory addresses to refer to numeric quantities that the program is to manipulate. Specifically, the Fortran statement on the card is

Z(1) = Y + W(1)

Figure 5.3

Punched card containing one Fortran statement. [Image licensed under CC BY-SA 2.5 by Arnold Reinhold, via Wikimedia Commons. From https://commons.wikimedia.org/wiki/File:FortranCardPROJ039.agr.jpg .]

Here, Y refers to a value that has presumably been previously assigned, perhaps using a Fortran statement such as

Y = 42

Z(1) and W(1) refer to the first values in arrays named Z and W . 1 Writing code this way removes the accidental complexity of having to decide where in memory these variables are to be located, choosing registers to temporarily store the values, giving instructions for loading the values from memory into registers, and finally giving the instruction to perform the add. The latter style is what would be required in assembly code.

A Fortran program is translated into assembly code (or directly into machine code) by a compiler. The compiler is responsible for deciding which registers are used for what and where in memory values are stored. Designing good compilers is quite an art, with many opportunities for optimization and experimentation.

But designing good programming languages is more subjective. Programming languages can develop fervent, almost religious followings. Followers of so-called「functional programming,」for example, are notorious for their zeal, advocating languages such as Haskell, named after logician Haskell Curry, and SML, Standard ML. SML is a descendant of ML (MetaLanguage), developed by Robin Milner, a prolific computer scientist and one of my personal heroes who did most of his work at the University of Edinburgh in Scotland and at Cambridge in England. These languages have an elegant mathematical way of specifying computation. Programs can be quite aesthetically pleasing, succinctly stating intent without over-specifying how the intent is to be realized. Nevertheless, among the pantheon of languages, pure functional languages have a small, albeit devoted following.

Much like natural language, programming languages shape the thinking of a programmer. As I mentioned earlier, Abelson and Sussman talk about computing as a「procedural epistemology」:

the study of the structure of knowledge from an imperative point of view, as opposed to the more declarative point of view taken by classical mathematical subjects. (Abelson and Sussman, 1996)

A program is imperative in the sense that it tells a computer what to do, as opposed to a mathematical equation, which tells what is. But there are many ways to tell a computer what to do.

A direct way to tell a computer what to do is to tell it how to do it. Computer scientists call a program「imperative」if it specifies a sequence of commands, giving a step-by-step procedure, a recipe that the computer is to follow. An imperative program directly represents knowledge as procedure, and like all knowledge, it is surely shaped by language. Most of the widely used programming languages, including Fortran, are imperative languages.

The functional languages, in contrast to imperative languages, adopt the declarative style of mathematics. In an imperative language, for example, the pair of statements

x = 1;

x = 42;

means to first assign the value 1 to variable x and then to change the value of the variable x to 42. 2 In a declarative language, these two statements are contradictory and will be rejected by a compiler. In a declarative language, the = operator has a different meaning. A statement x = 1 does not assign a value to a variable at a particular point in a procedure but rather declares that the symbol x   means 1, not at a point in a procedure but always. The order in which such statements are given is irrelevant. In a declarative language, the two statements above are contradictory because x can't mean 1 and also mean 42. Their declarative style is distinctly different from the procedural, step-by-step style of imperative programs. It is perhaps ironic that despite claiming that software constitutes a「procedural epistemology」and「the study of the structure of knowledge from an imperative point of view,」Abelson and Sussman's book uses throughout a dialect of Lisp, a functional language originally developed by John McCarthy in the 1950s. Although a Lisp program tells a computer what to do (and hence is imperative in the broader sense of the word), it is a declarative language at its core.

Purely functional languages have been less successful than imperative languages, having only a small but devoted following. As Kuhn says,

As in political revolutions, so in paradigm choice—there is no standard higher than the assent of the relevant community. (Kuhn, 1962, p. 94)

Kuhn talks about scientific paradigms being incommensurable. They can be irreconcilable accounts of reality, where one paradigm cannot be understood or judged through the conceptual framework and terminology of the other. At their most basic level, programming languages are not incommensurable because they are all (today) essentially equivalent to Turing machines, which have an imperative flavor, and to Church's lambda calculus, which has a declarative flavor (see chapter 8 ). But programmers are usually not using these languages at such an elemental level, and when bundled with the libraries, tools, patterns, and idioms that accompany a language, they arguably do become incommensurable paradigms. Kuhn continues,

To be accepted as a paradigm, a theory must seem better than its competitors, but it need not, and in fact never does, explain all the facts with which it can be confronted. (Kuhn, 1962, p. 18)

Programming languages do not exist to explain facts but rather to realize algorithms. Any language will realize some algorithms better than others. This may help explain the cacophony of languages that prevail today. If you can indulge me, dear reader, I would like to explore that cacophony.

Wikipedia is realized by an open-source program called MediaWiki, which is written in the PHP programming language. The first version of MediaWiki was created in 2001 by Magnus Manske, then a student at the University of Cologne. His program was later named MediaWiki, a permutation of the name of its biggest user, the Wikimedia Foundation, which runs Wikipedia. As with a lot of open-source software, many people have contributed to MediaWiki since Manske's original design.

Why did Manske use PHP to program MediaWiki? PHP was originally created in 1994 by Rasmus Lerdorf, a Danish-Canadian programmer who worked at Yahoo. PHP is a「scripting language」specifically designed for building web pages. A scripting language is a programming language intended for specifying short scripts that automate tasks that would otherwise be performed by a human. Notice the layers of culture rather than just technology behind all this: scripting language, wiki, open source, web page. These things did not exist three decades ago, and they are much less new technologies than they are new cultures.

The acronym「PHP」originally stood for Personal Home Page, but according to the current developers, PHP now stands for「PHP: Hypertext Preprocessor.」The new name makes PHP a「backronym,」which is an acronym where the words are chosen to match the letters rather than vice versa. Moreover, the backronym is self-referential or recursive because the「P」stands for「PHP.」Recursion is one of the central tenets of computer science, one of the basic concepts taught in every introductory computer science class. So computer scientists like to pun with recursion.

The use of recursive acronyms was popularized by Richard Stallman with GNU, which stands for「GNU's not Unix!」Choosing a recursive backronym for PHP was, I suspect, a bow to Stallman. GNU is a collection of software that Stallman intended to eventually replace Unix, an operating system originally developed in the 1970s at Bell Labs by Ken Thompson, Dennis Ritchie, and others.

Richard Stallman ( figure 5.4 ) is one of the most influential individuals today in the world of software. Stallman is responsible for a great deal of software that is used worldwide for many purposes. He is also one of the most interesting characters in the story of software. Stallman's GNU project was, in part, a revolt against corporate America. He has spent much of his effort in recent years campaigning against all sorts of encumbrances on software, including software patents, digital rights management, software license agreements, nondisclosure agreements, activation keys, copy restriction, and binary executables that do not include the source code.

Figure 5.4

Richard Stallman in Vietnam. [Copyright by Richard Stallman, released under「CC-ND,」 https://stallman.org/photos/ .]

In 1985, Stallman launched the Free Software Foundation, which is committed to freeing software. Note my odd use of words; I didn't say it was committed to「free software,」which could be easily misunderstood as software that does not cost money. The cost of the software is irrelevant; Stallman uses「free」as in「freedom.」In fact, I'm convinced that Stallman anthropomorphizes software, and that his commitment is to freeing the software so the software can go wherever it likes and do whatever it likes, rather than freeing the humans that use software. The latter model, which is better represented by the Berkeley open-source software movement, allows humans to do whatever they like with open-source software. Stallman's model, however, constrains the humans to ensure that they never enslave the software. The copyright notice on GNU software, called the GNU General Public License (GPL), specifically requires that any uses and modifications of GPL'd software preserve the same open rights as the original. This style of copyright is sometimes called a「copyleft」presumably because of seemingly left-leaning politics compared with the right-wing corporate-dominated copyright.

I'm hoping that you can see that the world of software constitutes a diversity of cultures and a literature with parody, social commentary, language, and politics all playing a role, along with technology.

But I digress. My topic in this section is programming languages. Returning to PHP, the language used to create MediaWiki, Lerdorf did not intend PHP to be a new programming language. In an audio interview, Lerdorf noted,

I don't know how to stop it, there was never any intent to write a programming language · · · I have absolutely no idea how to write a programming language, I just kept adding the next logical step on the way. (Lerdorf, 2003)

It is not uncommon for major software artifacts to come about this way. They start as small, personal projects, and they grow organically. Lerdorf quipped,「I really don't like programming. I built this tool to program less so that I could just reuse code.」With this style of design, the personality and aesthetics of the original authors have a huge impact on the end product.

Besides PHP, several of the most widely used programming languages today, C, C++, C#, and Java, share many essential features with Fortran and with each other. Even so, crossing denominations is rare. A C++ programmer will fight any request to write a Java program and vice versa, often with dogmatic arguments of faith and aesthetics.

In his 1987 Silver Bullet article, Brooks argued that programming languages had advanced sufficiently to have removed nearly all the accidental complexity in programming. The remaining essential complexity, he said, accounted for what has become known as Brooks' law,

Adding manpower to a late software project makes it later.

Brooks first articulated this law in his 1975 book, The Mythical Man Month (Brooks, 1975), which is often credited for launching the field called「software engineering.」Brooks once quipped that his book is called「The Bible of Software Engineering」because「everybody quotes it, some people read it, and a few people go by it.」

But I believe that Brooks vastly underestimated the complexity of systems that were to come, and programming languages alone do not provide an appropriate level of modeling. Many modern software systems consist of millions of lines of code, vastly more than any human can comprehend at the level of the programming language. Instead, programs have to be designed and understood as compositions of subprograms, much the way hardware at the digital machine level abstracts the low-level logic gates.

If you study computer science today, you will likely learn to use only a small number of programming languages, maybe even only one. In my opinion, a software engineer who has mastered only one language is about as well educated as a medieval monk who has studied exactly one book. There is a great deal to be learned from even studying the extensive graveyard of programming languages that have faded from memory.

The following, for example, is a short program in the programming language APL, which I used in a class that I took at Yale in 1978:

x [ ← 5?10]

APL, which stands for A Programming Language, was developed by Kenneth Iverson in the late 1960s. Iverson received the Turing Award in 1979 for this work. At Yale, an entire computer room was equipped with special terminals that had keyboards that could make the characters in the previous program, such as and ←.

Iverson wanted a language that would concisely specify mathematical operations on entire arrays of data all at once. I can explain the prior program if you can tolerate a short but intense nerd storm. The inner expression 5?10 means, in APL, to create an array with five elements consisting of random numbers in the range 1 to 10 with no repetitions. For example, evaluating this expression in APL might yield the array [9,4,3,8,1]. The expression x ← 5?10 means that this array should become the value of the variable x. The operator represented by the symbol takes the array that is now the value of x, sorts it, and returns indices that can be used to retrieve the values in the array in numerical order. The construct x[ · · · ] then uses that array of indices to retrieve the values. So here is a sequence of evaluations that yields a result:

x [ x ← 5?10]

x [ x ← [9, 4, 3, 8, 1]]

x [ [9, 4, 3, 8, 1]]

x [[5, 3, 2, 4, 1]]

[1, 3, 4, 8, 9]

So this program generates an array with five random numbers and then sorts the array so that you get the numbers in increasing order. As you can see, APL programs can be quite cryptic, but they tend to be concise.

A graveyard language that takes the opposite approach is COBOL, after「common business-oriented language.」COBOL was designed in 1959 based on an earlier language developed by Grace Hopper, shown in figure 5.5 . Hopper was an early proponent of high-level programming languages that were portable, meaning that they could be compiled to execute on a variety of machines, even machines with different instruction set architectures.

COBOL was intended to have a syntax more like English than like mathematics, so it tends to replace symbol operators with words. For example, instead of the APL assignment statement x ← y, in COBOL you would say MOVE y TO x . For many years, COBOL was widely used for business applications such as banking, but today few new programs are written in COBOL.

COBOL and APL represent extremes in an exploration of programming paradigms. COBOL is verbose, using English-language words, with the idea that programs would be more readable by business people. APL is concise, cryptic, and requiring special keyboards. Both succumbed to the Darwinian competition of paradigms, dinosaurs that were once successful but are now largely extinct.

Many more languages are in the graveyard, including Algol, Pascal, PL/I, SNOBOL, Smalltalk, and Prolog. Each of these has interesting ideas and an interesting story. Algol introduced many features present in most modern imperative programming languages, including Java, C, C++, and C#. Pascal introduced the idea of compiling first into a virtual machine language (called byte code) and then executing that program in a program that simulates the virtual machine. This is a centerpiece of the widely used Java language today. SNOBOL, developed at Bell Labs by David Farber, Ralph Griswold, and Ivan Polonsky in the 1960s, introduced high-level manipulation of text, including parsing and pattern matching, a centerpiece of the widely used JavaScript language today, among others. Smalltalk was one of the earliest object-oriented languages, providing a way of structuring programs that is widely used today. Prolog is a「logic programming」language that elegantly expresses rule-based queries over structured data.

Figure 5.5

Rear Admiral Grace Hopper, 1906-1992. Hopper was an early proponent of portable programming languages and pioneered a style of programming where programs read more like English-language sentences than like mathematical expressions. [Image courtesy of the United States Navy.]

Each of these languages encodes a paradigm, a way of thinking about computation. These languages did not die the way Kuhn's scientific paradigms die. No crisis was created by anomalous observations that exposed discrepancies between the paradigm and the natural world. Rather, these languages either mutated into new species of languages (as in ALGOL and Pascal) or progressed toward extinction in a Darwinian competition of survival of the fittest or the most promiscuous (as in APL and COBOL).

5.3 编程语言

小弗雷德里克·布鲁克斯信奉亚里士多德的理念，他在著名的论文《没有银弹：思考软件工程中的根本和次要问题》（以下简称《银弹》）中对偶然复杂性和本质复杂性进行了区分（布鲁克斯，1987）。布鲁克斯认为，本质复杂性是我们要求软件解决的问题所固有的复杂性。偶然复杂性源于「当今伴随（软件）生产而出现的非固有的」各种困难。

如果要求我只能用带有「0」和「1」两个键的键盘来撰写这本书，那么原则上我是可以这样做的。毕竟，计算机会将整本书存储为 0 和 1 的序列。但是，用这种方式写一本书肯定特别困难。事实上，在无须处理这种偶然复杂性的情况下，这本书本身就已经很难写了。

除了布鲁克斯所说的复杂性，我认为撰写本书的主要困难在于如何围绕非常技术化的主题来编织一个读者易理解的故事。我所掌握的技术可能已经消除了围绕这项任务的几乎所有的偶然复杂性。我有一个 QWERTY 键盘（全键盘），而且我打字相当快。

我还有优秀、免费且开源的文字处理软件（LATEX）。

当我记不起布鲁克斯在他的《银弹》论文中到底说了什么时，我就会去谷歌搜索「银弹」，很快这篇论文就呈现在我面前了。剩下的唯一困难就是一些本质性的困难了。这些困难来自我试图提出的一些可能颇有争议的问题，包括这里所说的一个问题，技术发展本质上是一种由文化和美学驱动的创造性的人类活动，它建立在人类构造的模型之上，而非被发现的自然法则的模型之上。仅是提出这个问题的困难就已经使得本书的写作变得非常有难度了。

帮助我写这本书的工程系统包括我的笔记本电脑、LATEX 排版软件、维基百科和谷歌，它们都是人类构建的复杂得惊人的系统。负责这些系统的工程师依赖于同样消除了许多偶然复杂性的那些工具，从而使他们能够专注于本质复杂性。创建维基百科的吉米·威尔士和拉里·桑格并没有用二进制甚至汇编语言编写他们的程序。事实上，他们使用了另外几个模型层。

指令集体系架构和汇编语言之上的一层是编程语言。1953 年年末，在 IBM 工作的约翰·W. 巴克斯启动了一个项目，开发了一种更简单的语言来表达程序，特别是那些广泛使用数学表达式的程序。这个项目的结果是产生了 Fortran 语言，它是一种一直沿用至今的语言。它的最新版本出现于 2008 年。

在巴克斯的时代，「Fortran」会被写成「FORTRAN」。事实上，大多数文本都是用大写字母写出的，因为如果把字母表限制为只用大写字母，每个字母就可以用更少的比特位来编码，从而节省存储器，就像汇编代码的简略助记符一样。字母「全部大写」也成了一种文化遗产。我的同事奇图尔·拉马莫西（Chittoor Ramamoorthy）生前是个很有魅力的人，常被称为「Ram」，他为计算机体系结构做出了很大的贡献。在 2016 年去世之前，他在所有的通信中一直坚持只使用大写字母，似乎并没有注意到这种文化的转变 —— 全部使用大写字母已经变得像一种大喊大叫了。

图 5.3 给出了打孔卡片上的一个 Fortran 语句。在 20 世纪 50 年代和 60 年代，打孔卡片既是一种存储介质（一叠卡片记录一个程序），也是一种数据输入机制。图中的这张卡片揭示了 Fortran 语言的一个关键性创新 —— 使用符号变量名而不是内存地址来指代程序要操作的数字量。具体来说，卡片上的 Fortran 语句是：

Z(1)=Y+W(1)

在这里，Y 指的是一个之前可能已经被赋值的值，可能使用了如下的 Fortran 语句：

Y=42

图 5.3 包含一个 Fortran 语句的打孔卡片。（阿诺德·雷因霍尔德通过维基共享资源供图，并获得 CC BY-SA 2.5 授权。图片来自 https://commons.wikimedia.org/wiki/File：FortranCardPROJ039.agr.jpg。）

Z (1) 和 W (1) 分别是名为 Z 和 W 的数组中的第一个值，通过这种方式编写代码可以消除这样一些偶然复杂性：必须确定内存中这些变量的位置，选择寄存器临时存储这些值，给出将这些值从内存加载到寄存器的指令，以及最后给出执行加法操作的指令。后一种风格是汇编代码中所需要的。

Fortran 程序经由编译器转换为汇编代码（或直接转换为机器码）。编译器负责决定哪些寄存器用于存储什么，以及这些值存放在内存中的什么位置。好的编译器的设计是一门艺术，其中有很多优化和实验的机会。

但是，好的编程语言的设计更具有主观性特点。编程语言可以激发热情，甚至培养出虔诚的追随者。例如，所谓「函数式编程」的追随者曾因其热情而有些声名狼藉。他们推崇使用 Haskell（以逻辑学家哈斯凯尔·加里的名字命名）和 SML（标准 ML）等语言。SML 语言源于 ML（元语言），而 ML 是由罗宾·米尔纳开发的。米尔纳本人既是一位成果丰硕的计算机科学家，也是我心目中的一个英雄。他的大部分工作是在苏格兰爱丁堡大学和英国剑桥大学完成的。

这些语言使用一种优雅的数学方法来指定计算。这样的程序非常美观，简洁地陈述意图而不过分指定如何实现意图。尽管如此，在计算机语言的万神殿中，函数式语言只有一小部分忠实的追随者。

就像自然语言那样，编程语言塑造了程序员的思维。正如我在前面提到的，阿贝尔森和萨斯曼将计算作为一种「程序认识论」：

从命令式的观点研究知识的结构，而不是古典数学学科所采取的更具陈述性的观点。（阿贝尔森和萨斯曼，1996）

程序是命令式的，因为它告诉计算机要做什么，这与说明这是什么的数学方程相反。

但是，告诉计算机做什么的方法有很多。

告诉计算机做什么的直接方法是告诉它该如何去做。如果一个程序给定一个命令序列，并给出计算机所需遵循的逐步执行过程，计算机科学家就将其称为「命令式」程序。命令式程序直接将知识表示为程序式的过程，就像所有知识一样，它肯定是由语言塑造的。大多数被广泛使用的编程语言，包括 Fortran 语言在内，都是命令式语言。

与命令式语言不同，函数式语言采用数学的声明式风格。例如，如下是命令式语言中的两条语句：

x=1

x=

42

其意味着，首先将值 1 赋给变量 x，然后将变量 x 的值更改为 42。在声明式语言里，这两条语句是矛盾的，并会被编译器拒绝。在声明式语言里，操作符「=」具有不同的含义。语句 x=1 不会在程序中的特定点给变量赋值，而是声明符号 x 表示 1，不是在某个点，而是始终。这与所给定的这种语句顺序是无关的。在声明式语言里，上述两个语句是矛盾的，因为 x 的值不能既表示 1，又表示 42。显然，它们的声明式风格与命令式程序的过程式、逐步式风格有着明显的不同。带有些许讽刺意味的是，尽管阿贝尔森和萨斯曼声称软件构成了一种「程序认识论」以及「从命令式的角度研究知识的结构」，但他们的书自始至终都在使用一种 Lisp 方言，这是一种最初由约翰·麦卡锡在 20 世纪 50 年代开发的函数式语言。虽然 Lisp 程序告诉计算机要做什么（因此从广义上理解也是命令式的），但它本质上是一种声明式语言。

函数式语言远远不如命令式语言成功，只有少数狂热的追随者。正如库恩说的那样：

对范式的选择也如政治革命一样 —— 没有什么标准能比得到相关团体的赞同更高了。（库恩，1962:94）

库恩认为科学范式之间是不可通约的。它们可以是对现实不可调和的描述，其中一种范式不能用另一种范式的概念框架和术语进行理解或判断。在最基本的层面上，编程语言并非不可通约，因为它们（如今）在本质上都等同于具有命令式风格的图灵机器以及丘奇具有声明式风格的 λ 演算（参见第 8 章）。但是程序员通常不会在这样一个基本层次上使用这些语言。当这些基本的编程语言与伴随一种语言的库、工具、模式和惯用用法捆绑在一起的时候，它们可能会成为不可通约的范式。库恩继续指出：

一种理论要被接受成为一种范式，它必须看起来比与它竞争的范式更好，但它不需要，而且事实上也永远不会解释它所能面对的所有事实。（库恩，1962：18）

编程语言的存在并不是为了解释事实，而是为了实现算法。任何语言都能比其他语言更好地实现一些算法。理解这一点可能有助于解释当今盛行的各种语言之间的不相容之处。亲爱的读者，请允许我探究一下这些不和谐的声音。

维基百科是基于一个名为 MediaWiki 的开源程序实现的，它是用 PHP 编程语言编写的。MediaWiki 的第一个版本由马格努斯·曼斯奇于 2001 年创建，当时他还是科隆大学的学生。他的程序后来被命名为 MediaWiki，这是它的最大用户、运行维基百科的维基媒体（Wikimedia）基金会的名字的变体。和许多开源软件一样，从曼斯奇的最初设计开始，有很多人对 MediaWiki 的发展做出了贡献。

为什么曼斯奇要使用 PHP 来编写 MediaWiki？PHP 最初是由在雅虎工作的加拿大籍丹麦程序员拉斯马斯·勒德尔夫于 1994 年创建的。PHP 是一种专门为构建网页而设计的「脚本语言」。脚本语言是一种用于编写短脚本的编程语言。这些脚本可以自动执行原本由人来执行的任务。就脚本语言、维基百科、开源和网页这一切而言，我们需要关注的不仅仅是技术层面，更要关注其背后的文化层面。这些东西在 30 年前并不存在，因此，与其说它们是新技术，不如说它们是新文化。

缩略词「PHP」最初代表的是个人主页（Personal Home Page），但在当今的开发人员中，PHP 现在代表「超级文本预处理器（HypertextPreprocessor）」。新名称使 PHP 成为「逆向首字母缩略词」，一个根据字母选择匹配单词而非相反的缩略词。此外，逆向首字母缩略语是自引用或递归的，因为字母「P」代表「PHP」。递归是计算机科学的核心原理之一，是计算机科学导论课中教授的基本概念之一。所以计算机科学家通常喜欢用递归来进行双关表达。

递归缩略词的使用是由理查德·斯托曼在 GNU（一款自由的操作系统）中推广的，其代表「GNU 不是 Unix！」我怀疑，为 PHP 选择一个递归的逆向首字母缩略词就是在向斯托曼致敬。GNU 是斯托曼打算最终取代 Unix 的一个软件集。如我们所知，Unix 最初是由肯·汤普逊、丹尼斯·里奇等人于 20 世纪 70 年代在贝尔实验室开发的一种操作系统。

理查德·斯托曼（图 5.4）是当今软件界最具影响力的人物之一。斯托曼领导了在世界各地被用于许多用途的大量软件的开发工作。他也是软件开发历史上最有趣的人物之一。斯托曼的 GNU 计划（也称革奴计划）在一定程度上是对美国企业界的反抗。最近几年，他花了大量精力反对软件上的各种权限障碍，包括软件专利、数字版权管理、软件许可协议、保密协议、激活密钥、复制限制和不包含源代码的二进制可执行文件等。

图 5.4 理查德·斯托曼在越南。（照片版权归理查德·斯托曼所有，照片经「CC-ND」许可发布，来自网站 https://stallman. org/photos/。）

1985 年，斯托曼成立了自由软件基金会，该基金会致力于推广自由软件。请注意这一用词，似乎有种很奇怪的感觉。我没有说它致力于「免费软件」，这很容易被误认为是免费的软件。软件的成本无关紧要。斯托曼在这里所用的 free 指的是「自由（freedom）」的意思。事实上，我确信斯托曼将软件进行了拟人化，他的承诺是给予软件自由，这样软件就可以去它想去的任何地方，做它想做的任何事，而不是给予使用软件的人以自由。以伯克利开源软件运动为代表的后一种模式，允许人们可以对开源软件为所欲为。然而，斯托曼的模式是限制人类的行为，其目的是确保人类永远不会奴役软件。GNU 软件的版权声明也被称为 GNU 通用公共许可证（GPL），特别要求对 GPL 软件的任何使用和修改都要保留与原始软件相同的开放权利。这种形式的版权（copyright）有时被称为「copyleft」。这大概是因为与偏右（right）企业主导的版权相比，其政治立场似乎是偏左（left）的。

我希望你能够看到软件的世界构成了文化上的多样性，也构成了一种文学，模仿、社会评论、语言和政治都与技术一起发挥作用。

不好意思，我又跑题了。本节的主题是编程语言。让我们还是继续 PHP 的话题 —— 用于创建 MediaWiki 的语言。勒德尔夫并不打算将 PHP 视为一种新的编程语言。勒德尔夫在一次音频采访中指出：

我不知道该怎么阻止它，我从来没有想过要写一种编程语言…… 我完全不知道怎么写一个程序语言，我只是在这个过程中不断地添加下一个逻辑步骤。（勒德尔夫，2003）

主要的软件产品都是以这种方式出现的，这并不稀奇。它们总是从个人的小项目开始，然后逐渐发展起来。勒德尔夫打趣道：「我真的不喜欢编程。我创建这个工具是为了少编程，这样我就可以重用代码了。」在这种设计风格下，原作者的个性和审美就对最终产品产生了巨大的影响。

除了 PHP 之外，目前使用最广泛的几种编程语言，如 C，C++，C# 和 Java，都与 Fortran 以及彼此之间共享许多基本特性。即便如此，它们也很难兼容。一个 C++ 程序员会拒绝编写 Java 程序，反之亦然。每种语言的程序员都常常带有某种信念和审美的教条性观点。

布鲁克斯在 1987 年发表的《银弹》一文中指出，编程语言已经取得了长足的进步，几乎消除了编程中所有的偶然复杂性。他说，剩下的本质复杂性解释了所谓的布鲁克斯定律，即向一个延迟的软件项目增加人力会使其进一步延迟。

布鲁克斯在他 1975 年出版的《人月神话》一书中首次阐明了这一定律。这本书通常被认为开启了一个被称为「软件工程」的领域。布鲁克斯曾经开玩笑说，他的书被称为「软件工程的圣经」，因为「每个人都引用这本书，有些人认真阅读它，还有一些人遵从它」。

但是，我相信布鲁克斯大大低估了即将到来的系统的复杂程度，而编程语言本身并不能提供一个合适的建模级别。许多现代软件系统具有数百万行代码，这远远超出任何人类可在编程语言的层次上理解的范围。因此，每个程序都必须被当作子程序的组合来设计和理解，这在很大程度上类似于数字机器层次的硬件抽象低层逻辑门的方式。

如果你今天学习计算机科学，那么你可能只学会使用少数几种编程语言，甚至可能只学会使用一种。在我看来，一个只掌握了一种编程语言的软件工程师，和一个只学过一本经书的中世纪僧侣差不多。其实，我们甚至可以从许多已经被淘汰的编程语言中学到许多知识。

例如，以下是以编程语言 APL 编写的一个短程序，1978 年我在耶鲁大学学习的一门课中就用过这个程序：

x

[x

← 5?10]

APL 是一种编程语言（A Programming Language）的首字母缩略词，这一语言是肯尼思·艾弗森在 20 世纪 60 年代末开发的。1979 年，艾弗森因这项工作获得了图灵奖。在耶鲁大学，整个计算机机房都配备了带有特殊键盘的终端，可以输入上述程序中的字符，如和←。

艾弗森想要设计一种能够一次指定对整个数据数组进行数学运算的语言。如果你还能忍受短暂却有些强烈的技术呆子头脑风暴，请允许我在这里解释一下上面的程序。在 APL 中，内部表达式 5?10 表示要创建一个包括 5 个元素的数组，这些元素由 1 到 10 之间没有重复的随机数构成。例如，在 APL 语言中，这个表达式可能会产生数组 [9，4，3，8，1]。表达式 x

← 5?10 表示这个数组应该成为变量 x

的值。由符号表示的运算符获取当前是 x

的值的数组，对其进行排序，并返回可用于按数字顺序检索数组中的值的索引。随后，结构 x

[…] 使用该数组的索引来检索这些值。如下是由此产生的一系列结果：

x

[x

← 5?10]

x

[x

← [9, 4, 3, 8, 1]]

x

[[9, 4, 3, 8, 1]]

x

[[5, 3, 2, 4, 1]]

[1, 3, 4, 8, 9]

由此，这个程序生成了一个包含 5 个随机数的数组，然后对数组进行排序，这样就可以按递增顺序得到这些数。正如你看到的，APL 程序可能看起来相当晦涩，但是它们往往又非常简洁。

已被淘汰的 COBOL（common business-oriented language，面向商业的通用语言）语言采用了与 APL 截然相反的方法。COBOL 是在 1959 年格蕾丝·霍珀（见图 5.5）早期开发的语言基础上设计出来的。霍珀是可移植高级编程语言的早期支持者，这意味着这些编程语言可以被编译到各种机器上执行，甚至是具有不同指令集体系架构的机器上。

COBOL 的语法更像英语而非数学，因为它倾向于用单词代替符号运算符。例如，与 APL 赋值语句 x

← y

不同，在 COBOL 中，你可以写成「MOVE yTO x

」。多年来，COBOL 被广泛应用于银行等商业领域。但现在很少有新的程序是用 COBOL 编写的。

图 5.5 格蕾丝·霍珀（1906—1992），美国前海军少将。霍珀是可移植编程语言的早期支持者，她开创的一种编程风格，使程序读起来更像英语句子而不是数学表达式。（该图片由美国海军提供。）

COBOL 和 APL 代表了探索编程范式的两个极端。COBOL 是冗长的，它使用英语单词编写程序，其思想是使得这种程序更易于被商业人士阅读。APL 则简洁、隐秘且需要特殊的键盘。当然，它们都屈从于达尔文式的范式竞争。正如恐龙这一曾经生机勃勃的物种，现在已经全部灭绝了。

还有许多已经被淘汰的语言，包括 Algol、Pascal、PL/I、SNOBOL、Smalltalk 和 Prolog。它们中的每一个都包含了有趣的想法和奇妙的故事。Algol 引入了包括 Java、C、C++ 和 C# 等大多数现代命令式编程语言中的许多特性。Pascal 引入了这样一种思想：首先将一个程序编译成虚拟机语言（它们被称为字节码），然后在模拟该虚拟机的程序中执行这个程序。这是当今广泛使用的 Java 语言的精髓。SNOBOL 是由大卫·法伯、拉尔夫·格里斯沃尔德和伊万·波隆斯基于 20 世纪 60 年代在贝尔实验室开发的。SNOBOL 引入了对文本的高级操作机制，包括解析和模式匹配等，而这正是当今广泛使用的 JavaScript 语言的核心。

Smalltalk 是最早的面向对象的语言之一，它提供了一种当今广泛运用的结构化程序设计方法。Prolog 是一种「逻辑编程」语言，它可以优雅地表达结构化数据中的基于规则的查询。

这些语言中的每一种都编码了一种范式 —— 一种关于计算的思维方式。这些语言范式并没有像库恩所说的科学范式那样消亡了。那些暴露了范式与自然界之间差异的反常的观察并没有造成危机。相反，这些语言要么变异成新的语言物种（如 Algol 和 Pascal 语言），要么在适者生存与混杂式达尔文竞争中渐渐走向灭绝（如 APL 和 COBOL）。

### 5.4 Operating Systems

Today, the word「operating system」means, to most people, one of three things: Apple's OS X, Microsoft's Windows, or Linux. Linux was originally developed in the early 1990s by Linus Torvalds, a Finnish (and later American) software engineer. Linux has become one of the most successful open-source software projects ever, with thousands of contributors and widespread adoption. Linux, like OS X, is based on the Unix operating system originally developed in the 1970s at Bell Labs by Ken Thompson and Dennis Ritchie, with contributions from many others. These three systems, OS X, Windows, and Linux, are the survivors of promiscuous evolution and competition over decades. Today, we should add iOS from Apple and Android from Google, operating systems designed specifically for smartphones and tablet computers.

I could write a great deal about operating systems, but instead I would just like to focus on how an operating system encodes one or more paradigms. A key feature of all these operating systems is the file system. In the hardware of a computer, various forms of memory store sequences of bytes, where each byte is a sequence of eight bits. The laptop computer on which I am writing this book has 16 gigabytes of volatile memory (memory that forgets its contents when you turn off the power) and one terabyte of nonvolatile memory. 3 The nonvolatile memory is sometimes called the「hard disk,」although these days it is more likely to be implemented using a type of semiconductor memory called a flash memory rather than the older spinning magnetic disk memory. As far as the hardware is concerned, the contents of the hard disk is just a sequence of a trillion bytes. The hardware can retrieve or update any single byte.

But a list of a trillion bytes, by itself, is not a useful way to organize information. Early operating system designers, such as Thompson and Ritchie, built into the operating system a way of encoding onto these disks a notion of a「file.」A file is a subset of the eight trillion bytes that forms a logical unit, and a file system supports assigning a name to the file and organizing files into hierarchical directories, which are also named. With the advent of graphical user interfaces, these directories acquired the metaphor of a「folder,」even though, for physical-world folders, folders that contain folders are rather awkward.

My key observation is that nothing in the computer hardware provides the notion of a file and the organization of files into directories. The software embodied in the operating system provides this notion.

The software that realizes the file system is quite clever. It does not even require that the contents of a file be contiguous in memory; the bytes of a file may be scattered all over the disk. The operating system software keeps track of which bytes belong to which file and what directory the file is logically contained in.

Once you have a file system to work with, you no longer need to worry about how your data is stored on a disk. You access the file as a single conceptual unit.

5.4 操作系统

今天，对大多数人来说，「操作系统」一词意味着如下三者之一：苹果的 OS X、微软的 Windows 或 Linux。Linux 最初是由芬兰（后来加入美国国籍）软件工程师林纳斯·托瓦兹于 20 世纪 90 年代初开发的，现已经成为有史以来最成功的开源软件项目之一，有着成千上万的贡献者并被广泛使用。和 OSX 一样，Linux 也是基于 Unix 的操作系统。Unix 操作系统最初是由贝尔实验室的肯·汤普森和丹尼斯·里奇于 20 世纪 70 年代开发的，也有其他许多人为之做出了很多贡献。OS X、Windows 和 Linux 这三个系统是几十年来混杂进化和竞争的幸存者。今天，我们还应该加上苹果的 iOS 系统和谷歌的 Android 系统，它们是专门为智能手机和平板电脑设计的操作系统。

我可以写很多有关操作系统的文章，但我只想聚焦于一个操作系统会如何编码一个或多个范式。所有这些操作系统的一个关键特征是文件系统。在计算机的硬件中，各种形式的存储器存储字节序列，其中每个字节都是一个 8 比特的序列。我正用来撰写这本书的笔记本电脑有 16GB 的易失性存储器（当你关闭电源时就会忘记所有内容的存储器），以及 1TB 的非易失性存储器。非易失性存储器有时被称为「硬盘」，虽然现在它更有可能使用一种被称为闪存的半导体存储器，而不是老式的旋转磁盘存储器。就硬件而言，硬盘的内容只是 1 万亿字节的序列。硬件可以检索或更新任何一个字节。

但是，一个 1 万亿字节的列表本身并不是一种组织信息的有效方式。早期操作系统的设计者，如汤普森和里奇等，在操作系统中内置了一种将「文件」的概念编码在这些磁盘上的方法。文件是构成逻辑单元的 8 万亿字节的子集，文件系统支持为文件指定名称并将文件组织到层次化的目录中，这些目录也是被命名的。随着图形用户界面的出现，这些目录已被形象地称为「文件夹」。当然，在物理世界中，一个文件夹中又包含许多文件夹会令人相当尴尬。

我的主要观察是，计算机硬件中没有提供文件的概念以及将文件组织到目录中的方法，而以操作系统呈现的软件提供了这个概念。

实现文件系统的软件相当聪明，它甚至不要求文件的内容在存储器中是连续性的。从而，文件的字节可以散布在整个磁盘上。操作系统软件能够跟踪哪些字节属于哪个文件，以及该文件在逻辑上包含在哪个目录中。

一旦有了要使用的文件系统，你就不用再担心数据是如何存储在磁盘上的了。你可以将该文件作为一个概念单元来访问。

### 5.5 Libraries, Languages, and Dialects

Millions of lines of code get translated into millions of zeros and ones that coerce billions of transistors to regulate the sloshing of who-knows-how-many electrons. This is starting to sound like Carl Sagan, whose signature lines involving「billions and billions」frequented his PBS television series Cosmos: A Personal Voyage in the 1980s. Sagan was talking about stars and galaxies and often emphasized the incomprehensible range of possibilities, including extraterrestrial life, that such numbers imply.

Digital technology seems to have hit a threshold where the possibilities are limited more by the human imagination than by physical constraints imposed on us by the world. What can be accomplished by software far exceeds what we accomplish today, even without further technological improvements. Software has become a digital medium for creativity. I will explore this issue in more detail in chapter 6 , and what we cannot do with software in chapter 8 , but for now let's just focus on how to manage the vastness of the possibilities.

Modern programming languages do, as Brooks claimed, mitigate a great deal of accidental complexity, but not enough to build really interesting systems like Wikipedia. Just as digital machine designs are augmented with standard cell and IP libraries, languages are augmented with component libraries and entire subsystems. As of this writing (August 2016), the Java language, Standard Edition version 8, has 4,240 software components built in for use by software designers. A software engineer will use these components in much the same way that a hardware engineer will use standard cells or an architect premanufactured components such as windows and doors.

Such a library of components becomes like a rich vocabulary, jazzing up the expressiveness of the language. Computer scientists do not usually consider such a library to be part of the language but rather something living and evolving apart from the language. But the library could well have far greater impact on the productivity and creativity of designers than the language. The mechanisms and conventions by which components in the library interact become, in effect, at least a dialect and sometimes even a new language. It is difficult to read a program if you are not familiar with the components it is using, even if you are fluent in its language.

Consider another widely used programming language for web applications, JavaScript, originally developed in 10 days in May 1995 by Brendan Eich. At the time, Eich was working for Netscape, one of the first companies to try to capitalize on the World Wide Web. Netscape was founded as Mosaic Communications Corporation in 1994 by Jim Clark and Marc Andreessen but eventually lost the browser wars to Microsoft and disappeared. Netscape's browser eventually morphed into the widely used, open-source, community-developed Firefox browser.

JavaScript, unlike PHP, is designed to run in the browser rather than in the server. This means that if you access a web page from your laptop or smartphone, and the web page includes a JavaScript program, that program runs on your laptop computer or your smartphone not on the server computer hosting the web page. Many of the web pages you visit routinely include a JavaScript program. Like PHP, the design of the JavaScript language exhibits interesting idiosyncrasies that reflect personal aesthetic decisions made by the original author.

The vast majority of the most widely used websites make extensive use of JavaScript. However, it is difficult to design beautiful and sophisticated web pages with JavaScript alone. Web designers leverage an ecosystem with thousands of「modules」available to designers. Many of these are open-source modules collectively developed by the community, much the way a Wikipedia page is collectively developed.

One widely used JavaScript module for creating sophisticated web pages is jQuery, originally created by John Resig. If you are fluent in JavaScript but do not know anything about the jQuery module, then programs that use it will be unreadable to you. Indulge me to illustrate this.

The JavaScript language, unlike most other programming languages, allows variable names to begin with the dollar sign character, $. The jQuery module defines a single global variable that it calls simply $. That is, the name of the variable is a single character, the dollar sign. This variable gets widely used in programs. To those unfamiliar with this idiom, the program looks cryptic, as a text written in the cyrillic alphabet looks to an English speaker. But the dialect is much richer than implied by just this idiom. Consider the following short JavaScript program:

$(document).ready(function(){

$("#target").text("Hello World");

});

If you are fluent in the JavaScript language but unfamiliar with the jQuery module and the modules provided by today's browsers, then this program is completely unreadable. It makes as much sense as the following does to someone fluent in English 4 :

Twas brillig, and the slithy toves

Did gyre and gimble in the wabe

Like this poem, the JavaScript program's verse is vaguely familiar but oddly incomprehensible to the JavaScript programmer.

I will spare you the details, but the prior JavaScript program can be used together with an HTML file and a style sheet to create the rather trivial web page shown in figure 5.6 . HTML, for HyperText Markup Language, is a completely different language, originally developed in 1980 by Tim Berners-Lee, creator of the World Wide Web, while he was a contractor at CERN, the European Organization for Nuclear Research (the acronym comes from the French name). The HTML that works with the previous JavaScript program to define the web page in figure 5.6 is as follows:

Figure 5.6

Web page using three languages and one dialect to specify.

<!DOCTYPE html>

<html>

<body>

<div id="target"></div>

</body>

</html>

Notice the idiosyncratic use of symbols < , > , and / , which were borrowed by Berners-Lee from a documentation format being used internally at CERN at the time.

HTML is universally used today to specify the contents of web pages, along with yet another language called CSS, for Cascading Style Sheets, first proposed in 1994 by Håkon Wium Lie, who was working with Berners-Lee at CERN. To use the previous JavaScript program, HTML is used to define the web page layout, and CSS is used to define the styles used to render the page. For example, if we include the following CSS code:

#target {

color: red;

}

then the text「Hello World」will be rendered in red. Notice that the syntax of CSS is quite different from HTML, which is quite different from JavaScript.

The web page of figure 5.6 is constructed using three distinct languages, JavaScript, HTML, and CSS, and one dialect, jQuery, each idiosyncratic and designed largely by a single creative individual. This is perhaps not as culturally rich and diverse as, say, Jerusalem, but it is most certainly not just dispassionate, objective, soul-less technology. It has every element of human subjectivity and invention pervading it. And millions of people today use this particular combination of technologies to design sophisticated web pages.

Of course, we could create a web page like that in figure 5.6 using HTML alone, but there are good reasons for using this combination of technologies. Using JavaScript enables the web page to dynamically update the contents of the page, making it interact with the user. Using CSS separates visual presentation design elements from logical structure and functionality, modularizing the design better. Using jQuery mitigates the accidental complexity associated with the fact that web pages can take a long time (relative to computer speeds) to load from a server and provides convenient access to elements of the page.

Although these languages and dialects each originated with a single individual, all are now thriving open-source communities with hundreds of contributors. They have evolved into a form of collective wisdom, like Wikipedia, rather than individual wisdom, like the Encyclopedia Britannica.

The culture of these communities should make an interesting subject of study for a cultural anthropologist. Resig, for example, first introduced jQuery to the web development community at a conference called a BarCamp in 2006 in New York City. BarCamps might be characterized as the anarchists' conference, in that nobody and everybody organizes the conference. Unlike most professional conferences, which will have a prepublished agenda with all events and presentations defined by an organizing committee, BarCamp participants self-organize using the web, whiteboards, and Post-It notes.

The license history of jQuery also reflects an ongoing passionate debate about the nature of open-source software. It was originally released using a GPL-style license as promoted by Stallman (specifically the Creative Commons CC BY-SA 2.5 license) but was later released under a less restrictive Berkeley-style license called the MIT license.

But I digress again (it is hard to avoid… the background stories are really quite interesting). Let's return to the subject of how to manage the vastness of possibilities that software offers. Software technologies emerge chaotically in a Darwinian ecosystem of ideas. Like a real Darwinian ecosystem, not everyone will agree on what makes one idea more「fit」than another idea, and survival depends more on the ability to propagate than on technical fitness. Promiscuity, personality, money, and culture have enormous, incomprehensible effects.

One approach to understanding this problem is the anthropologists' approach, which is to study the culture as it emerges and attempt to extract wisdom from that study. Just as an anthropologist might use the evolution of natural language as a key part of that study, a software anthropologist might use the evolution of programming languages, with idioms, dialects, and clichés.

One pioneering software anthropology effort was carried out by Erich Gamma, Richard Helm, Ralph Johnson, and John Vlissides in their book on design patterns (Gamma et al., 1994). Widely known as the「gang of four,」these authors attempt to categorize a variety of widely used patterns and idioms in software construction. They credit Christopher Alexander, architect, for inspiring their approach. Alexander proposed a pattern language for buildings and cities, and they translated this approach to software. In a testament to the difficulty of this task, in their preface, the gang of four state:

A word of warning and encouragement: Don't worry if you don't understand this book completely on the first reading. We didn't understand it all on the first writing!

I probably should have included a similar statement in the preface to my book.

The cultural nature of software may help explain why software endures better than hardware. Culture changes much more slowly than technology. The fact that software encodes its own paradigms can also contribute to its durability. For example, although APL is an extinct language, it is easy to find a web page that, using a similar HTML, JavaScript, and CSS combination, presents you with a customized APL keyboard and evaluates any APL programs that you type in.

The cacophony of languages that prevail today is reminiscent of immature scientific fields. Kuhn describes the scientific study of electricity in the first half of the eighteenth century before it acquired its first universally accepted paradigm:

During that period there were almost as many views about the nature of electricity as there were important electrical experimenters, men like Hauksbee, Gray, Desaguliers, Du Fay, Nollett, Watson, Franklin, and others. (Kuhn, 1962, p. 14)

But even at that time, Kuhn says, these competing paradigms shared a common metaparadigm:

All their numerous concepts of electricity had something in common— they were partially derived from one or another version of the mechanico-corpuscular philosophy that guided all scientific research of the day. (Kuhn, 1962, p. 14)

The languages used in web technology today, PHP, JavaScript, jQuery, CSS, and HTML, all have a common「mechanico-corpuscular」core, specifically the Turing-Church notion of computation, considered in chapter 8 .

5.5 库、语言和方言

数百万行代码被转换成数百万个 0 和 1，又迫使数十亿的晶体管去调节多得无法计数的流动电子。这听起来很像卡尔·萨根的标志性台词。20 世纪 80 年代美国公共广播公司播出的电视连续剧《卡尔·萨根的宇宙》中，他标志性的台词总是涉及「数十亿」这样巨大数字。萨根经常会在谈到恒星和星系时，强调这些巨大的数字所暗示的不可思议的可能性范畴，其中包括外星生命。

数字技术似乎已经达到了一个极限，其未来的可能性更多地受到人类想象力的限制，而不是自然世界强加给我们的物理约束。即使没有进一步的技术改进，软件所能完成的事情也远远超出我们今天所能完成的。软件已经成为激发创造力的数字媒介。我将在第 6 章更详细地探讨这个问题，并在第 8 章讨论软件的局限性，但现在还是让我们集中讨论如何管理这些巨大的可能性吧。

正如布鲁克斯所言，现代编程语言确实极大地降低了偶然复杂性，但还不足以构建像维基百科般有趣的系统。就像用标准元件和 IP 库增强数字机器一样，组件库和整个子系统也增强了语言。在撰写本书之时（2016 年 8 月），Java 语言标准版第 8 版中已经有 4 240 个软件组件可供软件设计人员使用。软件工程师使用这些组件的方式与硬件工程师使用标准元件，或者建筑师使用预制组件（如窗、门等）的方式非常相似。

这样一个组件库就像一个丰富的词汇表，可以大大提高语言的表现力。计算机科学家通常并不将这样的库当作语言的一部分，而是认为它们是与语言分离存在且不断发展的。但是，组件库对计算机设计人员的生产力和创造力所产生的影响要比语言的大很多。实际上，库中组件相互交互的机制和约定，至少差不多已成为一种方言，有时甚至成为一种新的语言。如果你不熟悉一个程序所使用的那些组件，那么，你即使精通它的语言，也很难读懂它。

我们来考虑另一种被广泛使用的万维网应用编程语言 ——JavaScript。该语言最初是由布兰登·艾奇于 1995 年 5 月在 10 天之内开发的。当时，艾奇正在为美国网景公司工作，该公司是最早尝试利用万维网的公司之一。该公司由吉姆·克拉克和马克·安德森于 1994 年创立，原名为马赛克通信公司（Mosaic Communications Corporation）。该公司最终在激烈的网络大战中输给了微软，之后就销声匿迹了。网景公司的浏览器最终演变成后来被广泛使用的、开源且由社区开发的火狐浏览器。

JavaScript 与 PHP 不同，它被设计成在浏览器中运行，而不是在服务器中运行。这意味着，如果用笔记本或智能手机访问一个网页，而该页面包含一个 JavaScript 程序的话，那么该程序是在你的笔记本电脑或智能手机上运行的，而不是在托管该网页的服务器上运行的。你经常访问的许多网页都会包含一个 JavaScript 程序。与 PHP 语言一样，JavaScript 语言的设计同样表现出一些有趣的特性。这些特性反映了原作者的个人审美风格。

绝大多数使用最广泛的网站都在使用 JavaScript 语言。然而，仅使用 JavaScript 语言是很难设计出美观又复杂的网页的。实际上，网页设计人员利用一个包含了数千个可供设计人员使用的「模块」的生态系统。其中许多都是社区集体开发的开源模块，就像维基百科页面是由集体开发的一样。

一个广泛用于创建复杂网页的 JavaScript 模块是 jQuery，它最初由约翰·瑞森创建。如果你精通 JavaScript 语言却对 jQuery 模块一无所知，那么你将无法理解使用 jQuery 模块的程序。请允许我在这里简要地说明一下。

与其他大多数编程语言不同，JavaScript 语言允许变量名以美元符号 $ 开头。jQuery 模块定义了一个简单称为 $ 的全局变量。也就是说，该变量的名称是单个字符，即美元符号。这个变量在程序中被广泛使用。对于那些不熟悉这个习语的人来说，这个程序看上去很神秘，就像一个说英语的人见到用西里尔字母写的文本一样。但方言比这个习语所蕴含的内容要丰富得多。我们来看看以下这个简短的 JavaScript 程序：

$(document).ready(function(){

$("#target").text("Hel

l

o World");    });

如果你精通 JavaScript 语言，但一点儿也不熟悉 jQuery 模块以及当今浏览器所提供的模块，那么你是完全读不懂这个程序的。那种感觉就像某个精通英语的人读到了下面这段话一样：

怪兽，烤晚餐肉时辰粘柔的三不像怪兽（Twas brillig, and the slithy toves），

围着日晷草坪转悠钻地洞（Did gyre and gimble in the wabe）。

就像上面这首诗一样，这段 JavaScript 程序的诗对于 JavaScript 程序员来说是似曾相识却难以理解的。

我就不在这里花时间谈论细节了，但是上面的 JavaScript 程序可以与一个 HTML 文件和样式表一起使用，以创建图 5.6 所示的非常简单的网页。HTML 是英语 HyperText Markup Language 的首字母缩略词，意思是超文本标记语言，这是一种完全不同的语言，它是由万维网的创始人蒂姆·伯纳斯·李于 1980 年开发的，当时他是欧洲核子研究组织（CERN，该缩略语源自该组织的法语名称）的承包商。与上面给出的 JavaScript 程序一起用来定义图 5.6 所示网页的 HTML 代码如下所示：

图 5.6 使用三种语言和一种方言规定的网页。

<!DOCTYPE html>

<html>  <body>   <div id="tar

g

et"></div>  </body>  </html>

注意符号 <、> 和 / 的特殊用法，这些符号是伯纳斯·李从当时欧洲核子研究组织内部使用的文档格式中借用来的。

今天，HTML 普遍用于描述网页的内容，另外还有一种被称为 CSS 的语言，用于制作样式层叠表（Cascading Style Sheets）。该语言是 1994 年由哈肯·维姆莱首次提出的，他当时与伯纳斯·李一起在欧洲核子研究组织工作。为了使用如前所述的 JavaScript 语言，得先使用 HTML 定义网页的布局，CSS 则用于定义该页面的样式。例如，如果我们包含以下 CSS 代码：

#target {

color:

red;   }

那么文本「Hello world」将显示为红色。请注意，CSS 的语法与 HTML 的非常不同，后者与 JavaScript 的语法也有很大的不同。

图 5.6 所示的网页是由三种不同的语言（JavaScript、HTML 和 CSS）以及另外一种方言 jQuery 构建的。每一种语言都非常独特，主要由一个有创造力的人设计。也许它不像耶路撒冷那般具有丰富多样的文化，但也绝不只是一种冷静、客观、无灵魂的技术。它有着人类的主体性并充满了创造性。今天，数以百万计的人使用这种特殊的技术组合来设计复杂的网页。

当然，我们可以单独使用 HTML 创建一个如图 5.6 所示的网页页面，但是也有充分的理由使用这种技术组合。使用 JavaScript 语言可以使网页动态地更新页面内容，使其能够与用户进行交互。使用 CSS 能够将视觉上的设计元素从逻辑结构和功能中分离出来，这也会使设计实现更好的模块化。由于从服务器加载网页可能需要很长的时间（与计算机的运行速度有关），所以使用 jQuery 语言可以减少这个长时间过程所带来的偶然复杂性，并提供对页面元素的便捷访问。

虽然这些语言和方言最初都源于个人，但它们有成千上万的贡献者，这使得它们今天能够在开源社区中蓬勃发展。它们已经演变成一种集体智慧的形式，就像维基百科，而不是像《不列颠百科全书》那样的个体智慧。

这些社区的文化应该能够成为文化人类学家研究的有趣课题。例如，2006 年在纽约召开的一次名为「BarCamp」的会议上，瑞森首次在万维网开发社区介绍了 jQuery。BarCamp 会议具有无政府主义者聚会的特征，没有人组织这个会议，但所有人都参与组织。与大多数专业会议不同的是，这类会议有一个预先公布的议程，由一个组织委员会安排所有的活动和演讲，BarCamp 的与会者使用网络、白板和便利贴自行组织会议。

jQuery 获得许可的历史也反映了一场关于开源软件本质的激烈争论。它最初使用斯托曼倡导的 GPL 风格许可进行发布（特别是知识共享 CC BY-SA2.5 许可），但后来才在限制更少的伯克利式（Berkeley-style）许可下发布，该许可也被称作 MIT 许可。

非常抱歉，我似乎又离题了（实际上这有些难以避免，因为这些背景故事真的很有趣）。让我们回到如何管理软件所提供的巨大可能性这一主题上吧。在达尔文思想生态中，软件技术的出现有些混乱。就如同一个真正的达尔文生态系统一样，并不是每个人都同意是某些因素让一个想法比另一个更「适合」，生存更依赖于传播能力而不是技术的适合程度。混杂、个性、资本以及文化等都有着不可思议的巨大影响。

有一种人类学家的方法可以帮助我们理解这个问题，换言之，在文化出现时就对其进行研究，并试图从中汲取智慧。正如人类学家可能将自然语言的演化作为这项研究的关键部分一样，软件人类学家可能会使用编程语言的演化，包括各种习语、方言和陈词滥调。

埃里克·伽玛、理查德·赫尔姆、拉尔夫·约翰逊和约翰·威利斯迪斯在他们共同撰写的《设计模式：可复用面向对象软件的基础》一书中进行了软件人类学的一项开创性工作（伽玛等人，1994）。他们被业内人士称为「四人组」。他们试图对软件构造中广泛使用的各种模式和习语进行分类。他们声称是建筑师克里斯托弗·亚历山大启发了他们的方法。建筑师亚历山大提出了一种关于建筑物和城市设计的模式语言。他们将亚历山大的这种方法转换至软件方面。为了证明这项任务的艰巨性，在该书的序言中，四位作者就这项任务的艰巨性做出如下陈述：

给你一个警告和鼓励：如果你在第一次阅读时发现不能完全理解这本书，那么，请不要担心。因为我们在第一次写的时候也没有完全理解！

我也许应该在我这本书的前言里加上类似的陈述。

软件的文化特性可能有助于解释为什么软件比硬件具有更耐久的生命力。文化的变迁远比技术的发展要缓慢得多。软件编码其自身的范式这一事实也有助于它的耐久性。例如，虽然 APL 是一种已被淘汰的编程语言，但是很容易找到一个使用类似于 HTML、JavaScript 和 CSS 组合的网页，这样的网页能为你提供一个定制的 APL 键盘，并能够处理你所输入的任何 APL 程序。

当今这些编程语言的不和谐现象让人想起了不成熟的科学领域。库恩描述了 18 世纪上半叶对电的科学研究，那时尚未形成第一个普遍被接受的范式：

在那个时期，关于电的本质的观点与当时开展电的实验的重要人员一样多，如霍克斯比、格雷、德萨吉利埃、杜菲、诺莱、沃森、富兰克林等人。（库恩，1962:14）

但即使在那个时候，库恩也认为，这些相互竞争的范式有一个共同的元范式：

这些范式对电的所有概念都有某些共同之处 —— 它们都部分地源于当时指导所有科学研究的机械粒子哲学的一个或另一个版本。（库恩，1962:14）

现在网络技术中使用的语言，如 PHP、JavaScript、jQuery、CSS 和 HTML 等，都有一个共同的「机械粒子」核心，特别是我们要在第 8 章中讨论的丘奇 — 图灵计算概念。

### 5.6 The Cloud

So far we have been talking about individual computers and the software that runs on them. But many of the most interesting uses of computers today are far too big for a single computer to handle. These applications run on computers housed in「server farms,」large facilities that can consume up to tens of megawatts of electricity. It is hard to get exact numbers, but various estimates indicate that, as of this writing (2016), Microsoft, Google, and Amazon have on the order of a million servers each in their data centers. Many companies operate perhaps an order of magnitude fewer servers, including Facebook, Yahoo, HP, IBM, eBay, Intel, Rackspace, and Akamai. Each server may contain tens of「cores,」individual computers that share certain resources among them, such as memory and network interfaces.

Taken together, this means that there are single software-based services, such as Facebook and Google search, that are running simultaneously on as many as millions of individual computers. These applications make extensive use of PHP, JavaScript, and more general-purpose programming languages like Java, discussed in the previous sections. But they overlay on these languages yet higher level paradigms to handle the distribution of tasks and data across many machines. Languages with curious names such as Pig Latin and frameworks such as ZooKeeper, Sqoop, and Oozie encode the design styles of these paradigms.

For example, Apache Hadoop is an open-source framework that has at its core a distributed file system for spreading data across servers and a realization of a pattern called MapReduce for delegating to servers chunks of a data processing operation. MapReduce was invented in 2004 (and patented) by Jeffrey Dean and Sanjay Ghemawat of Google, although as usual for inventions, the actual novelty is in dispute. MapReduce is strikingly similar to patterns that had existed previously in older software for distributed computing such as MPI (the Message Passing Interface) and database systems.

Hadoop forms an ecosystem of patterns and tools for the design of multiserver applications. Like many of its competitors, Hadoop assumes that hardware failures are common because with millions of servers failure will occur. Hardware gets virtualized so that applications can move from machine to machine with minimal disruption. An application may even move from one machine to another machine of an entirely different type, emphasizing the disconnect between the software and the physics of the hardware.

Server applications are often called on to handle truly vast amounts of data, much more than any single computer could handle at once. Consider Google search, for example, which returns in less than a second the results of searching billions of web pages and handles on the order of 40,000 searches per second (Pappas, 2016). How does Google do that? Storing the contents of the web on a computer and searching it each time a query comes in clearly will not work. There is just too much data.

The key to a web search is collecting and indexing the data ahead of time. A major part of the work of Google's servers is not actually responding to search requests but rather reading, indexing, and sorting web pages ahead of time and creating a massive distributed data structure. A「web crawler」finds a website, collects the words on it, and follows the links to other websites, all the while keeping track of link relationships between web pages. The collected data, including statistical features such as word proximity, word ordering, frequency of links, and link associations, are used to build a「memory」of the web that allows for quick recall.

In his book Turing's Cathedral , George Dyson draws a thought-provoking analogy:

The behavior of a search engine, when not actively conducting a search, resembles the activity of a dreaming brain. Associations made while「awake」are retraced and reinforced, while memories gathered while「awake」are replicated and moved around.

· · ·

In 1950, Turing asked us to「consider the question, ‘Can machines think?' 」Machines will dream first. (Dyson, 2012, p. 311)

Indeed, the human brain apparently uses sleep and dreaming to organize information. Does this mean that Google's million-server machines are a nascent intelligence in the process of building some form of cognition by organizing information about the world? I defer this difficult question until chapter 9 , where I confront the idea of a digital psyche.

There is quite a bit of sophistication (and secrecy) about how a search works exactly. But one thing is sure: when you perform a Google search, it is not a single computer that replies. Instead, your search is routed through a string of servers depending on the keywords and language patterns in the search so that the search query goes to where the organized data resides. No single server can store and access more than a tiny fraction of the「knowledge」that the servers build while dreaming, so no single computer can reasonably respond to an arbitrary search. The server that first sees your query will be random, based on which servers are available, but after that the query will be forwarded to servers based on keywords and patterns in your search.

Let's consider how much data is involved. First, the amount of data is constantly increasing. The content in the web grows, of course, but more interestingly (and disturbingly, like Orwell's Big Brother), a search engine will watch your every move and use correlations with your previous searches, your location, and even a learned model of your preferences to improve the search results (and to improve the likelihood that advertisements presented to you will be relevant to you). When you read and shop online, you are being read back. The data gathered gets fed into the dream machine to be organized.

It is hard to get solid numbers, but some 2016 estimates suggest that Google may be storing on the order of exabytes of data. One exabyte is 10 18 or

1,000,000,000,000,000,000.

That's a lot of data, and potentially all of it can be used to build models of the world, using, for example, the machine learning techniques considered in chapter 11 .

The web and users of the web provide a wealth of data for these servers to learn from, but that is not the only source. Software providers are systematically trying to shift all of our computing activity from our personal computers to servers in「the cloud.」This changes the business model of software from product to service but, more important, gives the software vendors more direct access to your data, to data about your use of their software, and to data about you.

Even legacy data is being uploaded to these servers. Printed material such as books and journals are being steadily digitized to be added to the online arsenal of information. In 2002, Google started a project to scan every book ever published. Dyson's description of this project is quite extraordinary:

At the time of my visit, my hosts [at Google] had just begun a project to digitize all the books in the world. Objections were immediately raised, not by the books' authors, who were mostly long dead, but by book lovers who feared that the books might somehow lose their souls. Others objected that copyright would be infringed. Books are strings of code. But they have mysterious properties like strings of DNA. Somehow the author captures a fragment of the universe, unravels it into a one-dimensional sequence, squeezes it through a keyhole, and hopes that a three-dimensional vision emerges in the reader's mind. The translation is never exact. In their combination of mortal, physical embodiment with immortal, disembodied knowledge, books have a life of their own. Are we scanning the books and leaving behind the souls? Or are we scanning the souls and leaving behind the books?

「We are not scanning all those books to be read by people,」an engineer revealed to me after lunch.「We are scanning them to be read by an [artificial intelligence].」(Dyson, 2012, p. 312)

Why stop at books? In 2006, Google bought YouTube for $1.6 billion. Because YouTube is a video-sharing website, it provides a truly vast arsenal of data about the world. In 2014, YouTube said that 300 hours of new videos were uploaded to the site each minute, on average. Although the technology for extracting useful information from video and images lags behind that for extracting information from text, we can be sure that the technology will improve. The machines will start to dream in color. As data from sensors comes online, for example, from connected cars, thermostats, and the whole Internet of Things world, what more can the machines learn? I examine this question in the next chapter.

5.6 云

到目前为止，我们一直都在谈论个人计算机及其运行的软件。然而，当今计算机有很多非常有趣的应用，这些应用远远超出一台计算机的处理能力。这些应用程序运行在「服务器集群」上，这些大型设施可以消耗高达几十兆瓦的电力。尽管很难得到确切的数据，但截至 2016 年我撰写这本书的时候，各种估计表明，微软、谷歌和亚马逊的数据中心大约有 100 万台服务器。许多公司运行的服务器数量可能要少一个数量级，例如脸书、雅虎、惠普、IBM、易贝、英特尔、Rackspace（一家全球领先的托管服务器及云计算提供商）和阿卡迈等。但是，每个服务器可能包含数十个「核」，即它们是共享诸如存储器和网络接口的一组独立的计算机。

总而言之，这意味着基于单个软件的一组服务（如脸书和谷歌搜索）能够同时运行在数百万台个人计算机上。这些应用程序普遍使用了 PHP、JavaScript 以及诸如 Java 等更为通用的编程语言，相关的这些内容已在前面的章节中讨论过。但是，它们覆盖了这些语言，并使用了更高层次的范式来处理任务和数据在许多机器上的分布。一些有着奇怪名字（如 Pig Latin）和框架（如 ZooKeeper、Sqoop 和 Oozie）的语言编码了这些范式的设计风格。

例如，Apache Hadoop 是一个开源框架，其核心是一个分布式文件系统，用于在服务器之间传输数据，同时，其实现了一个被称为 MapReduce 的模式，用于将一组数据处理操作的块委托给服务器。MapReduce 模式是由谷歌公司的杰弗里·迪安和桑贾伊·马沃特于 2004 年发明的（并获得了专利）。尽管与普通的发明一样，但其实际的新颖性仍然是具有争议的。MapReduce 与之前用于分布式计算的旧软件，如 MPI（消息传递接口），以及数据库系统中的模式惊人地相似。

Hadoop 形成了设计多服务器应用程序的模式和工具的生态系统。与它的诸多竞争对手一样，Hadoop 也假定硬件故障很常见，因为数以百万计的服务器中肯定会发生故障。由于硬件被虚拟化了，所以应用程序就可以从一台机器迁移到另一台机器，且会尽管少地影响程序执行。一个应用程序甚至可以从一台机器迁移到另一台类型完全不同的机器上，这实际上强调了软件与硬件之间的分离。

服务器应用程序经常被调用来处理真正的大规模数据，它们的能力要远远超过任何单台计算机一次可处理的数据量。以谷歌搜索引擎为例，它在不到 1 秒的时间内就可以返回对数十亿个网页的搜索结果，并以每秒 4 万次的速度进行处理（帕帕斯，2016）。那么，谷歌是如何做到这一点的呢？将网络内容存储在计算机上，并在查询请求每次到来时进行搜索，这种办法显然是不够的。这是因为要处理的数据实在是太多了。

网络搜索的关键是提前收集和索引数据。事实上，谷歌服务器的主要工作并不是真的去响应搜索请求，而是提前读取网页并进行索引和排序，同时创建一个庞大的分布式数据结构。一个「网络爬虫」找到一个网站，收集该网站上的关键词，并跟踪到其他网站的链接，同时跟踪网页之间的链接关系。收集到的数据包括了诸如单词接近度、单词排序、连接频率以及链接关联性等统计特性，它们被用来构建一个允许快速访问的网络「存储器」。

乔治·戴森在他所著的《图灵的大教堂》一书中，做了一个发人深省的类比：

在不主动进行搜索时，搜索引擎的行为就类似于做梦时大脑的活动。「清醒」时所产生的联想会被不断地追溯和强化，而「清醒」时收集的记忆会被复制和移动。

……

1950 年，图灵就让我们「思考这样一个问题，‘机器能思考吗'」，机器得先会做梦。（戴森，2012:311）

事实上，人类的大脑显然是通过睡眠和做梦来组织信息的。这是否意味着谷歌的百万台服务器是一种新生的智能，它们正在通过组织有关世界的信息来构建某种形式的认知？我把这个棘手的问题留到第 9 章再讨论，第 9 章将会涉及数字心灵的概念。

一次搜索到底是如何工作的，关于这一点还是有点儿复杂（和神秘）的。但有一件事是可以肯定的：当你使用谷歌进行搜索时，给出响应的肯定不是一台计算机。相反，你的搜索将根据搜索中的关键字和语言模式通过一连串服务器进行路由，这样搜索查询就可以到达有组织的数据所在的位置。没有任何一台服务器能够存储和访问服务器在做梦时所建立「知识」的哪怕是一小部分，因此，可以说没有一台计算机能够对任意的搜索做出合理的响应。首先接收到你的查询请求的服务器将是随机的，这主要取决于哪些服务器可用，但在此之后，这条查询请求将被基于你所搜索的关键字和模式转发到其他服务器上。

让我们来考虑一下到底会涉及多少数据。首先，数据量在不断增加。当然，网络上的内容不断增长，但更有趣（且更令人不安，就像奥威尔的哥哥那样）的是，搜索引擎将会关注你的一举一动，并使用与你之前搜索过的内容、你当前所在位置的关联性，甚至你的偏好的学习模型来改善搜索结果（同时，提高向你推送和你有关的广告的可能性）。当你在网上阅读和购物时，你的一举一动都被记录下来。这些被收集的数据会被输入将要被组织在一起做梦的机器中。

虽然很难得到确切的数据，但 2016 年的一些评估表明，谷歌可能存储了艾字节级的数据。1 艾字节是 1018

字节或

1 000 000 000 000 000 000。

这是规模巨大的数据，而且很可能所有的数据都可被用来构建世界的模型，例如，使用第 11 章提到的机器学习技术。

网络和网络用户提供了丰富的数据供这些服务器学习，但这并不是唯一的来源。软件提供商正在系统地尝试将我们所有的计算活动从我们的个人计算机迁移到「云」中的服务器上。这将改变软件从产品转为服务的业务模型，但更为重要的是，软件供应商可以更直接地访问你的数据、关于你使用其软件的数据以及关于你的数据。

甚至所有的遗留数据也都被上传到这些服务器上。诸如书籍和期刊等的印刷材料正在稳步走向数字化，从而可以被加入在线的信息库。2002 年，谷歌公司开始了一个扫描所有已出版图书的宏大项目。戴森对这个项目的描述非常特别：

在我访问的那段时间，我的雇主（在谷歌的）刚刚开始了一个将世界上所有书数字化的项目。反对的声音立即就出现了。反对之声不是来自那些早已辞世的书籍作者，而是来自广大的书迷。他们提出了强烈的反对意见，担心一旦数字化就会使这些书失去灵魂。还有一些人则说这会侵犯书的版权。书不过是一串代码，但是它们带有某些神秘的特性，就像基因序列一样。书的作者以某种方式捕捉到了宇宙的一个片段，并将其展开成一个一维的序列，然后把它挤进一个钥匙孔并希望在读者的脑海中呈现出一个三维的景象。当然，这种转换从来都不是百分百准确的。书籍将平凡的有形化身与不朽的无形知识结合在一起，从而拥有了它们自己的生命。我们是要扫描书本，并将其灵魂留下吗？或者我们是要扫描灵魂而把书本抛于脑后？

「我们扫描所有这些书，并不是让人们去阅读。」一位工程师在午餐后对我说，「我们扫描它们是为了让人工智能来阅读的。」（戴森，2012:312）

为什么止步于书籍？谷歌公司是不会仅仅满足于扫描图书的。2006 年，谷歌公司以 16 亿美元的巨资收购了 YouTube。如我们所知，YouTube 是一个视频分享网站，它提供了关于世界的海量数据。2014 年，YouTube 声称平均每分钟会有时长 300 小时的新视频上传到其网站。虽然从视频和图像中提取有用信息的技术落后于从文本中提取信息的技术，但我们可以肯定，该类技术将会得到改进。机器将开始做彩色的梦。随着在线获取传感器数据，例如来自联网汽车、恒温器以及整个物联网世界的数据技术的发展，机器还将学到什么呢？我将在下一章讨论这个问题。

__________

1 Fortran makes extensive use of arrays as a way to manage memory. For example, an array W with four integers might be declared and then initialized with the statements

INTEGER, DIMENSION(4) :: W

W = (/ 42, 43, 44, 45 /)

After these statements are executed, the value of W(1) is the integer 42, the value of W(2) is the integer 43, and so on.

2 Among computer scientists, the number 42 is popular to use in examples because of Douglas Adams' Hitchhiker's Guide to the Galaxy , a 1978 BBC radio comedy series that later became a「trilogy」of five books. In that story, a special computer called Deep Thought is built to answer the「ultimate question of life, the universe, and everything.」The computer takes 7.5 million years to compute and check the answer, which turns out to be 42. The computer reports that the answer seems meaningless because the beings who programmed it never actually knew what the question was.

3 Sixteen gigabytes is about 16 billion bytes, and a terabyte is about one trillion bytes.

4 From Through the Looking-Glass, and What Alice Found There , a novel by Lewis Carroll, 1871.

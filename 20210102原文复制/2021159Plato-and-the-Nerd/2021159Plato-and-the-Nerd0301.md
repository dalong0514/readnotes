## 0301. Models of Models of Models of Models of Things

· · · in which I argue that in engineering, models are stacked many layers deep, with the design of each layer affecting the designs both above and below it; and that the engineering use of models enables creativity because the layering of models distances designers from the physical constraints of the realization. Digital technology, particularly, has, in effect, mostly removed any meaningful physical constraints from a broad class of engineered systems. Innovation, therefore, is less limited by the physics of the technology than it is by our human imagination and ability to assimilate new paradigms.

0301 事物之模型之模型之模型

我认为：1）工程中的模型是深度层叠的，并且每一层的设计都会影响上、下相邻两层的设计；2）而且模型的工程运用能激活创造性，这是因为模型的分层使设计者能够摆脱现实的物理约束。实际上，特别是数字技术已经在很大程度上消除了一大类工程系统中任何有意义的物理约束。因此，可以说，人类的想象力和吸收新范式的能力是限制创新的因素，而不是技术本身的因素。

### 3.1 Technological Tapestries

Consider the engineer's question,「Can I make a thing for this model?」Suppose that the answer is「yes」for a broad class of models. For example, technology today gives us the ability to make networks of electrically controlled switches, where closing one switch can cause another switch to open or close. A semiconductor chip is such a network, where the switches are realized as transistors and the network consists of wires that connect the transistors. The medium in which such a network is crafted is the silicon and metal of semiconductors, a physical medium.

Once the answer to the question is「yes, we can make the thing」for networks of switches, then networks of switches become a medium for making models. This medium has its own paradigm, much like Kuhn's scientific paradigms. Just as a scientist uses a paradigm to construct a model of a thing, so does an engineer. The paradigm gives the conceptual framework within which to understand the model.

So what can we build with networks of switches? The network of switches paradigm is quite an expressive one. With just two states for each switch, on and off, it might not seem so expressive, but it turns out that we can interconnect such switches to perform logic functions corresponding to natural language words such as「and,」「or,」and「not.」We can interconnect those logic functions to compare and manipulate strings of bits that represent text and to perform arithmetic on numbers represented in binary. In fact, networks of switches are capable of enormously rich manipulation of any information that is representable as sequences of zeros and ones. It is no accident that transistors functioning as binary switches are the linchpins of information technology.

Once we have the ability to perform arithmetic, we open up the possibility of using another paradigm for design, namely, arithmetic expressions. This paradigm is distinctly different from the network of switches paradigm, but models in the arithmetic expression paradigm are implementable as models in the network of switches paradigm. So if an engineer has a model consisting of arithmetic operations on binary numbers and again asks the question,「Can I make a thing for this model,」then again the answer is「yes.」To realize the「thing,」however, the arithmetic model needs to be first translated into a network of switches model, which then in turn is translated into a silicon chip. Arithmetic expressions become a virtual medium, not directly physical, but translatable into something physical through one level of indirection. This is my first example of transitive models.

It turns out that we can do much more with networks of switches. We can make memory, which stores binary patterns. For example, a bank balance of $256 can be represented by the binary pattern 0000000100000000. There are 16 bits in this representation. It is possible to design a network of 96 switches that can store this number indefinitely. If a customer deposits $16, representable by the binary number 0000000000010000, then a network of switches can add the two numbers, getting 0000000100010000, the binary representation for the number 272. It can then update the memory with the new balance. We can start to see the glimmer of how a computer banking system can emerge from networks of switches.

But thinking about a computer banking system as a network of switches is not practical. For one thing, the number of switches actually required will be vastly more than I've indicated above, and the operations that need to be performed are vastly more complex. A bank will not hire an engineer to wire together transistors, which realize the switches, to make a computer banking system. Instead, the bank will hire an engineer who will write software that will be translated by a computer into a binary pattern that will control a machine that is ultimately composed of a network of transistors. This engineer need not know anything about how to craft a transistor, nor how to perform binary arithmetic using networks of switches, nor how to organize networks of switches to make memories.

In fact, there are many layers of models between the bank engineer and the physical realization. The bank application, a computer program represented as a sequence of letters, numbers, and punctuation, is in fact a model of a model, which in turn is a model of another model, which in turn is yet another model of a model, until ultimately we get down to a model of a thing. Each of these layers of modeling has a paradigm, and each paradigm is a human invention. Only the lowest level physics is given to us by nature.

In this chapter, I will attempt to articulate why such layering of paradigms is so powerful and how the layers turn paradigms into a creative medium that other engineers can use to realize their models. You may come at this with the preconception that these layers of paradigms will be dry, fact-laden technologies, intricate and boring at the same time. But they are not. They are shaped by what is physically possible, but particularly with digital technology, it turns out that so much is possible that they are much more shaped by the personalities and idiosyncrasies of the engineers who create them.

Educators all too often belie the personality of the technology. They present technology as Platonic facts about the world that must be mastered. This is how the educators learned about it. But the creators of the technology did not learn it that way. They invented it, and like literature and art, their inventions reflect the predilections of the creators and the (technological) culture in which they lived. The culture in which they lived was, in turn, defined by the inventions of others. Technology is not a collection of Platonic truths that have always been lurking in the background, waiting to be discovered, but is rather a rich sociological tapestry of ideas created by human inventors. It is shaped by those humans, and had a different set of humans created it, including more women, for example, the technology would unquestionably be different.

I will defer many details to the next two chapters, where I attempt to capture the paradigms and cultures that have manifested in hardware and software technology. In this chapter, I keep a high-level view.

3.1 技术的分层

让我们先来看一看工程师给出的一个问题：「我可以为这个模型做点儿什么吗？」假定对于一大类模型来说，该答案是「是的」。例如，今天的技术使我们能够构造电气控制的开关网络。在这个网络中，闭合一个开关会导致另一个开关断开或闭合。半导体芯片就是这样的网络，其中的开关就是晶体管，网络是由连接这些晶体管的线路组成的。制作该类网络的介质是硅金属半导体，它是一种物理介质。

一旦这个问题的答案是「是的，我们可以」，那么开关网络就变成了构造模型的媒介。就如同库恩的科学范式一样，这种媒介也有它自己的范式。正如科学家使用范式来构建事物的模型一样，工程师也使用范式来构建事物的模型。范式提供了理解模型的概念框架。

那么，我们可以建立什么样的开关网络呢？开关网络的范式是颇具表达力的。每个开关只有两种状态 —— 开（导通）和关（截止），它看起来不那么有表达力，但事实证明，我们可以将这些开关连接起来，以执行与自然语言相对应的逻辑功能，例如「与」、「或」和「非」。我们可以将这些逻辑功能互联起来，以比较和操作表示文本的位串，并对二进制表示的数字执行算术运算。事实上，开关网络能够对任何可以表示为 0、1 序列的信息进行极其丰富的操作。作为二进制开关的晶体管能成为信息技术的关键，这并非偶然。

一旦我们拥有了执行算术运算的能力，我们就有可能开启另一种设计范式 —— 算术表达式。这一范式与开关网络的范式有着明显的不同，但算术表达式范式中的模型与开关网络范式中的模型一样具有可实现性。因此，如果一个工程师有一个由二进制数的算术运算组成的模型，并且再次回到这个问题 ——「我可以为这个模型做点儿什么吗？」，那么答案依然会是「是的」。然而，要实现「做点儿什么」的愿望，首先需要将算术模型转换为一个开关网络模型，然后将其转换为硅芯片。由此，算术表达式就变成了一种虚拟的媒介，它并非直接就是物理的，但可以通过一个间接层转换到某个物理介质。这是我要解释的第一个传递性模型的例子。

事实证明，我们可以用开关网络做更多的事情。我们可以用它创建存储器，存储二进制模式。例如，256 美元的银行余额可以用二进制模式 0000000100000000 来表示。这种二进制表示法共有 16 位。我们可以设计一个由 96 个开关组成的网络，其可以存储银行无限多的数据。如果客户存入账户 16 美元，该数据可以用二进制模式 0000000000010000 来表示，随后，开关网络可以将这两个数进行相加，并得到一个二进制数 0000000100010000，这个二进制数表示十进制数 272。然后，它可以用新的银行余额更新存储器。我们可以看到计算机银行系统是如何从开关网络中慢慢浮现而出的。

但是，把计算机银行系统看作一个开关网络是不现实的想法。首先，它实际所需的开关数量比我前面给出的例子要多得多，同时，所需执行的操作也要复杂得多。银行不会雇用一名工程师来连接实现开关功能的晶体管，以构建一个计算机银行系统。相反，银行会聘请一名工程师编写软件，这些软件将被计算机翻译为二进制模式，从而控制最终由晶体管构成的机器。这位工程师不需要知道如何制造一个晶体管，也不需要知道如何使用开关网络进行二进制运算，更不需要知道如何组织开关网络来制造一块存储器。

事实上，在银行系统的工程师和最终的计算机银行系统之间有许多模型层次。银行的应用，一个由字母、数字和标点符号组成的计算机程序，实际上是另一个模型的模型，另一个模型又是第三个模型的模型，以此类推，直到我们最终向下到达某个事物的模型。每个建模层次都有一个范式，而且每个范式都是由人类发明的。只有最低层的物理实体是大自然给予我们的。

在本章中，我试图阐明为什么分层的范式会如此强大，以及这些层次如何将范式转化为其他工程师可以用来实现其模型的创造性媒介。此时，你可能会带有成见地认为，这些范式层是枯燥的和充满事实的技术，同时也是复杂的和无聊的。然而，事实并非如此。它们是由物理上的可能性塑造的，尤其是有了数字技术之后，事实证明，它们更可能带有缔造者（工程师）的个性和气质的深深印迹。

教育工作者往往不承认技术的个性。他们把技术描述为人们必须掌握的关于世界的柏拉图式的事实。这就是教育家学习它的方式。但是，技术的创造者并不是以这种方式来学习的。他们发明了技术，就像文学和艺术是被发明的一样。他们的发明反映了创造者的个人偏好，以及他们所处的（技术）文化环境。反过来，他们所处的文化环境又为其他人的发明所定义。技术不是一直潜伏在幕后等待被发现的柏拉图式真理的集合，而是由人类发明家创造的丰富的社会学思想的结晶。它是由这些人塑造的，并且是由一群不同的人创造出来的，其中包括很多女性。因此，技术无疑会有所不同。

我将把许多细节推到接下来的两章中进行阐述。在这两章中，我将尝试捕捉在硬件和软件技术中表现出来的范式和文化。而在本章中，我主要是给出一个高层次的观点。

### 3.2 Complexity Simplified

Engineering of simple systems, like Edison's lightbulb, can be carried out with a prototype-and-test approach. But this approach breaks down as systems get more complex. With more complex systems, the use of models becomes much more important.

Complexity is a difficult concept to pin down. Roughly speaking, something is complex when it strains our human minds to comprehend it. Complexity is therefore a relation between an artifact or a concept and a human observer.

One source of complexity is large numbers of parts. The human brain has difficulty keeping in mind simultaneously more than a few distinct components. In the early days of the telephone network, for example, extensive human studies conducted by Bell Labs determined that people could reliably keep seven numbers in short-term memory but not more. So telephone numbers were constructed with seven digits.

Computers have no such difficulty. They can easily keep billions of numbers「in mind」simultaneously. Computers, therefore, become both a source of complexity for us (we can't understand what they are doing with all those numbers) and a way to help us manage complexity (we delegate to them our memory).

Consider the horse model shown being 3D printed in figure 2.3 . The virtual prototype shown in figure 2.5 has more than 23,000 triangular facets. Each facet is specified by nine numbers, so the STL file that defines the virtual prototype contains more than 207,000 numbers represented by more than 46 million bits. Yet my laptop computer generates from these numbers the graphic image shown in the figure, complete with simulated lighting, in less than one second. I can interactively rotate that graphical image to examine all sides of the horse with no noticeable delay for the computer to re-render and re-simulate the lighting at each angle. The rendering of the image requires millions of arithmetic computations on the numbers that represent the vertices of the 23,000 triangles.

It is harder to design a complex system using Edison's prototype-and-test approach because there are so many more possible configurations to try. Nevertheless, prototypes and tests on those prototypes continue to play a major role in engineering today. A modern prototype of an electrical device is shown in figure 3.1 and reported in Choi et al. (2001). This is a transistor of a type called a FinFET, invented at Berkeley by Jeff Bokor, Tsu-Jae King, Chenming Hu, and their students. The prototype shown in the figure, made in 2001, uses the same principles as the field-effect transistor (FET) patented by Julius Lilienfeld (Lilienfeld, 1930).

The innovation in this transistor is its structure, which is more vertical than its predecessors in integrated circuits. Its vertical structure enables many more of these transistors to be packed into a given area of a silicon chip.

I would like to emphasize the dimensions indicated in the figure. The「fin」on the FinFET is 20 nanometers wide. There are one billion nanometers in a meter, so this is quite small indeed.

Figure 3.1 Prototype of a modern transistor. [Courtesy of Tsu-Jae King-Liu.]

Consider the implications of being able to realize a transistor that is so small. A modest sized silicon chip is about one centimeter squared. How many 20-nm squares fit in one centimeter squared? Shall I pause for you to do the calculation?

Pause.

OK, hopefully you got the same answer I did, which is 2.5 × 10 11 , or 250 billion! This is a square centimeter:

It is hard to imagine fitting 250 billion distinct human-made objects into the space above.

As of 2017, nobody has made a chip with 250 billion transistors (yet), in part, because a chip includes many other things besides transistors, such as wires to connect the transistors. Also, each transistor needs some space around it to separate it from neighboring transistors. So how many transistors can a chip have in practice?

Intel makes a family of microprocessor chips that they call their Haswell line using 22-nm FinFETs. You may have such a chip in your computer. Figure 3.2 shows a portion of a silicon wafer containing several such chips. A「fab」is a high-tech factory that produces such wafers and then cuts them into individual chips and packages them for inclusion in a computer. Each chip in the figure occupies 1.77 centimeters squared, nearly twice as big as the square shown above, and has 1.4 billion transistors (Shimpi, 2013). This is far fewer than 250 billion, but it is still a large number. [1]

Much writing about such technology, including what I've written above, has a breathless enthusiasm about the big numbers. But most of us actually have quite a bit of difficulty assigning any meaning to such numbers because they are so much bigger than anything we encounter in daily life. In fact, the point I want to make is that the human brain is incapable of comprehending any design that has 1.4 billion individual components, each with a potentially different function, despite the fact that the human brain has some 100 billion neurons, each of which does more than a transistor!

Each transistor can function as an electronic switch. It has a control input that either turns the switch on or turns it off. It can turn on and off billions of times per second. Billions of transistors switching billions of times per second creates unimaginable potential complexity.

Figure 3.2 Photo of a silicon wafer with several Intel Haswell microprocessor chips. The pin on top is for scale. [Photo by Intel Free Press (Flickr: Haswell Chip), released under a CC BY 2.0 license, via Wikimedia Commons.]

How can we design anything using this technology? Can we use Edison's prototype-and-test style of experimentation? Bokor, King, and Hu probably did some prototyping and testing before getting a single FinFET to work. Even so, it was much harder for them than for Edison simply because of the dimensions involved. It is extremely difficult to sculpt a physical structure 20 nm wide. You can't do this with a hammer and chisel. As a consequence, they would have had to make much more use of models than Edison did.

But more to the point, if you want to design a system based on a silicon chip, would you start your design by assembling and interconnecting transistors? Consider, for example, the system I am using to write this book. I'm using a software package called that converts text that I type into a formatted book that can be distributed electronically or printed. Suppose I want to design such a system. Should I start with a bagful of transistors and start connecting them in various ways to see what they do? Most certainly not.

is an interesting story. It provides me, a book author, with a paradigm for modeling a book. I construct a model of my book in a text editor that contains annotations such as \footnote{Footnote contents} to create a footnote, such as this one. [2] I then run a program to convert the text model into a PDF file, another model of pages to be printed. was created by Leslie Lamport in the early 1980s, when he was at SRI International. Lamport is an astonishingly prolific and influential computer scientist who received the 2013 Turing Award, sometimes called the Nobel Prize of computer science, for his work on distributed software systems. stands for「Lamport's 」and is built on top of , designed in the late 1970s by Donald Knuth from Stanford University, another Turing Award winner. Knuth is most well known for his monumental multi-volume work The Art of Computer Programming , an encyclopedic compendium of algorithms and principles of programming. Vikram Chandra, in his wonderful book about the aesthetics of software, Geek Sublime , said,

If ever there was a person who fluently spoke the native idiom of machines, it is Knuth, computing's great living sage. (Chandra, 2014)

In an article called「Literate Programming,」Knuth argued that software is a literature where code can be written as much to communicate with other human beings as to tell the computer what to do:

Let us change our traditional attitude to the construction of programs: Instead of imagining that our main task is to instruct a computer what to do, let us concentrate rather on explaining to human beings what we want a computer to do. (Knuth, 1984, emphasis in the original)

Knuth created TeX over about 10 years starting in the late 1970s because he found the typography of phototypesetting systems of the day ugly. Today, thousands of people have contributed to and , primarily through a system of packages that support an astonishing variety of document preparation needs. It is a thriving, open-source community where nearly all software is free. Almost as if in homage to Knuth, the code gets read and improved by others. The typography that TeX produces, in my opinion, is better than any commercial word processor that I have encountered. In chapter 5 , I will have much more to say about the human expressiveness of software.

[1] The particular chip shown in figure 3.2 is a「quad-core + GPU」version of the Haswell product, meaning that each chip actually contains five computers, four「cores」that execute your programs and one「graphics processing unit」that manages the rendering of graphics and text on a screen. The GPU is also a computer, albeit a rather specialized one. If you squint at the figure, you can see the dies for each chip, the rectangular repeating pattern. Within each die, you can see four identical patterns; these are the four cores. The GPU is above the four cores. The rest of the chip is probably mostly memory. As of this writing (August 2016), the largest Haswell chip has 5.56 billion transistors, is about 6.6 centimeters squared, and has 18 cores.

[2] Footnote contents

3.2 简化的复杂性

简单系统的工程，如爱迪生的灯泡，可以用一种原型 — 测试的方法来实现。但随着系统变得越来越复杂，这种方法可能会失效。对于更为复杂的系统，模型的使用变得越发重要。

复杂性是一个很难被界定的概念。粗略地说，当一件事迫使我们绞尽脑汁去思考才能理解时，它就是复杂的。因此，复杂性是一种人工制品或一个概念与观察者之间的关系。

复杂性的一个来源是大量的组件。人类的大脑很难同时记住几个不同的组件。例如，在电话网络发展的早期，贝尔实验室对人类的记忆能力进行了大量研究。研究结果表明，人类在短时间内可以可靠地记住 7 个数字，但不能再多了。

所以电话号码是由 7 位数组成的。

计算机没有这样的困难。它们可以很容易同时「记住」数十亿个数字。因此，计算机对我们人类来说既是复杂性的来源（我们无法理解它们在用这些数字做什么），也是帮助我们管理复杂性的一种方法（我们将自己的记忆托付给它们）。

以图 2.3 中 3D 打印的马的模型为例，图 2.5 所示的虚拟模型共有超过 23 000 个三角形平面。每个平面都由 9 个数字指定，因此，定义虚拟模型的 STL 文件中包含了由 4 600 万比特表示的超过 207 000 个数字。然而，我的笔记本电脑可以用这些数字生成图中的图形，并在不到 1 秒钟的时间内完成模拟光线。我还可以在没有明显延迟的情况下交互式旋转该图形，以便计算机重新渲染和重新模拟每个角度的光线。该图像的渲染需要对代表 23 000 个三角形顶点的数字进行数百万次的算术运算。

使用爱迪生的原型 — 测试法设计一个复杂的系统比较困难，因为有太多可能的配置可供尝试。尽管如此，针对原型的这些原型 — 测试方法在今天的工程中仍然扮演着重要的角色。图 3.1 所示的是崔伊等人（2001）报道的电子元件现代原型。这是一种被称为鳍式场效应管（FinFET）的晶体管，是由杰夫·博科尔、金智杰、胡正明和他们的学生在伯克利大学发明的。图中所示的原型是在 2001 年制造的，其原理与朱利叶斯·利林菲尔德申请的场效应晶体管专利具有相同的原理（利林菲尔德，1930）。

这种晶体管的创新之处在于其结构，它比以前的集成电路更加立体。它的垂直结构使得更多的晶体管可以被封装到一个硅芯片的特定区域。

我要强调一下图中所示的几个尺寸大小。鳍式场效应晶体管上的「鳍」的宽度是 20 纳米。我们知道，1 米有 10 亿个纳米，所以这确实是相当小的。

图 3.1 一个现代晶体管的原型。（金智杰供图，致谢。）

让我们来思考一下实现如此小的晶体管的意义。一个中等规模的硅芯片的面积约为 1 平方厘米。想想看，1 平方厘米的硅芯片上能有多少个 20 纳米的小方块呢？我要不要先停下来，等你计算一下呢？

我先暂停一会儿。

好吧，希望你得到的答案和我的一样，那就是 2.5×1011，也就是 2 500 亿！下面这个小方块的面积就是 1 平方厘米：

要把 2 500 亿个不同的人造对象装进上面的空间，这的确令人难以想象。

在 2016 年之前，还没有人制造出拥有 2 500 亿个晶体管的芯片，部分原因是除了晶体管之外，芯片中还包括许多其他的东西，例如连接晶体管的线路。此外，任何两个晶体管之间都需要一定的距离和空间。那么，一个芯片实际上能有多少个晶体管呢？

英特尔公司使用 22 纳米的鳍式场效应晶体管制造了一系列的微处理器芯片，并将它们命名为 Haswell 系列芯片。你的电脑里可能就有这样的一块芯片。图 3.2 给出了包含多个此类芯片的硅芯片的一部分。作为高科技工厂，「晶圆厂」生产这种晶圆，然后将其切割成单个芯片，并将它们安装在计算机中。图中每个芯片的面积是 1.77 平方厘米，几乎是如上所示正方形的两倍，且具有 14 亿个晶体管（辛皮，2013）。这远远少于如前所述的 2 500 亿，但是仍然是一个庞大的数字。图 3.2 这是一张带有多个英特尔 Haswell 微处理器芯片的硅片照片。通过上面的别针可以感受其大小。[照片由英特尔免费媒体（雅虎网络相册：Haswell 芯片）发布，已获得维基共享资源 2.0 授权。]

很多关于这类技术的文章，包括我在上面所写的，都对大的数字有着令人窒息的热情，因为它们比我们在日常生活中遇到的任何东西都要大得多。但实际上，我们大多数人很难给这些庞大的数字赋予任何意义。事实上，我想说明的一点是，尽管人类的大脑有大约 1 000 亿个神经元，且每个神经元的功能都比一个晶体管更复杂，但人类的大脑还是无法理解任何由 14 亿个功能都可能不同的单个组件构成的设计！

每个晶体管都可以作为一个电子开关。它有一个控制输入，可以使得开关导通或截止。它可以在每秒钟开关数十亿次。数十亿计的晶体管以每秒数十亿次的速度进行开关，其结果就是产生了难以想象的潜在复杂性。

我们如何才能利用这项技术设计任何东西呢？我们可以使用爱迪生的原型 — 测试实验风格吗？博科尔、金智杰以及胡正明很可能在成功设计鳍式场效应晶体管之前，的确做了一些原型 — 测试的实验。即便如此，仅仅因为所涉及的尺度，他们的实验也比爱迪生的要困难得多。要雕刻一个 20 纳米的物理结构是非常困难的，你不能用锤子和凿子来做到这一点。因此，与爱迪生相比，他们不得不更多地使用模型。

但是更重要的是，如果你想设计一个基于硅芯片的系统，你会从晶体管的组装和连接开始吗？

例如，我们来看看我用来编写本书的系统。我使用了一个名为 LATEX 的软件包，它能够把我输入的文本转换成可电子分发或打印的格式化书籍。假设我想设计这样一个系统，那么，我是否应该从一堆晶体管开始，以各种方式把它们连接起来，再看看它们能做些什么？肯定不会是这样的。

LATEX 是一个有趣的软件。它为我（一本书的作者）提供了建模图书的范式。我在文本编辑器中构造了我的书的模型，其中包含诸如用 \ footnote {脚注内容} 的注释创建一个脚注。然后，我会运行一个 LATEX 程序，将文本模式的内容转换为一个 PDF 文件 —— 待打印文件的另一种页面模式。LATEX 软件是莱斯利·兰波特 20 世纪 80 年代初在斯坦福国际研究院工作时开发的。兰波特是一位多产且有影响力的计算机科学家。他因在分布式软件系统方面的突出贡献获得 2013 年的图灵奖（有时也被称为诺贝尔计算机科学奖）。LATEX 是「Lamport 的 TEX」的缩写，它以斯坦福大学的另一位图灵奖得主高德纳于 20 世纪 70 年代末设计的 TEX 排版系统为基础。高德纳因他不朽的多卷型巨著《计算机程序设计艺术》而声名显赫。这是一本关于算法和编程原理的百科全书。维克拉姆·钱德拉在他的关于软件美学的著作《极客写作：代码与小说之美》（Geek Sublime）一书中写道：

如果有一个人能流利地说出机器里的方言，那么这个人一定是高德纳 —— 计算机领域的活佛。（钱德拉，2014)

在一篇名为「文学编程」的文章中，高德纳认为，软件是一种文学，在这种文学中，编写的代码不仅可以告诉计算机该做什么，还能用来与他人进行交流：

让我们改变一下我们对构建程序的传统态度：与其设想我们的主要任务是指导计算机去做什么，不如让我们集中精力向人类

解释我们想让计算机做什么。（高德纳，1984）

从 20 世纪 70 年代末开始，高德纳花了大约 10 年创建了 TEX 排版系统，因为他发现当时的照相排字系统的排版实在太难看了。今天，成千上万人已经为 TEX 和 LATEX 软件做出了贡献，主要是通过一个支持各种文档准备需求的软件包系统。它是一个蓬勃发展的开源社区，几乎所有的软件都是免费的。人们阅读并改进其中的代码，这几乎就像是在向高德纳致敬。在我看来，TEX 软件生成的字体比我遇到的任何商业文字处理器的都要好。在第 5 章，我将更多地谈及有关软件的人类表达的内容。

### 3.3 Transitivity of Models

A word processing system, such as the one I'm using to write this book, runs on a microprocessor like that in figure 3.2 , which uses transistors based on the prototype in figure 3.1 . Many levels of modeling exist between the physics of silicon and the word processor. Even more layers can be found between the physics and a system like Wikipedia. Like a pencil, no individual person knows how to make such a system. The fact that such systems exist, however, is a direct consequence of human ingenuity and creativity. Each layer of modeling allows individuals to contribute to the design without knowledge of or concern for how the layers of modeling they are using came about and without knowledge of how the layers of modeling they are creating will be used by other designers.

A few of the layers involved in the construction of a system such as Wikipedia are shown in figure 3.3 . My friend and colleague Alberto Sangiovanni-Vincentelli calls these layers「platforms」(Sangiovanni-Vincentelli, 2007), an apt term because each platform forms a substrate for construction of the models above it. Some of the models above it define platforms for further construction. Sangiovanni-Vincentelli points out that the platforms give designers「freedom from choice.」Below a platform there are many possibilities, offering more choices than any human designer can handle. Above the platform, there are fewer choices to be made. You can design more systems by creating a network of transistors than you can using logic gates (explained in chapter 4 ), for example. But when logic gates provide a suitable platform, the design job becomes much easier if you use logic gates rather than networks of transistors.

Occasionally, one encounters the use of such layers of abstraction in science. But compared with engineering, it is relatively rare, and depth of the layering is much more shallow. Scientists wish to construct models of physical reality, and models of models of physical reality become more suspect simply because they are further from the physical reality.

Figure 3.3 Layers of paradigms.

An example from science where layering of models has been successful is the gas laws developed at the end of the eighteenth century. These laws relate pressure, temperature, volume, and mass of a gas, including Boyle's law, Charles' law, Gay-Lussac's law, and Avogadro's law. These models describe phenomena that are ultimately due to the motion of large numbers of molecules in a gas, but they do not describe the phenomena in terms of the individual molecules. For example, Boyle's law states that at a fixed temperature, the pressure of a gas is inversely proportional to the volume it occupies. So, for example, if you reduce the volume (compress the gas), then pressure will increase. These are useful models of models, where the lower level model is of randomly moving molecules colliding with one another and with the surface of the enclosure.

In biology, arguably the most complex of the natural sciences, some researchers have argued that only through such layering can natural biological systems become comprehensible. Fisher et al. (2011), for example, propose the layers shown in figure 3.4 「to tame complexity of living systems.」They explicitly propose these layers in analogy to computer hardware systems, even naming some of the layers accordingly, such as「bio-logic gates.」The question marks in the figure, however, reveal that this approach is not mature. Biology appears less able to exploit the transitivity of models, compared with engineering, at least so far.

I believe this limitation is quite fundamental. Science cannot benefit as much as engineering from the layering of modeling paradigms. The root of the reason, which I explore more fully in the subsequent chapters, is that engineers build systems to match models rather than models to match systems.

Figure 3.4 Layers of abstraction proposed by Fisher et al. (2011) for synthetic biology.

Even without layering, many phenomena in our physical world (maybe even most phenomena) defy scientific modeling. John Searle has written extensively about the inability of scientific models to address cognitive and social phenomena, for example, even though those phenomena are clearly physical. Recall his claim that「the methods of the natural sciences have not given the kind of payoff in the study of human behavior that they have in physics and chemistry」(Searle, 1984, p. 71). His explanation, to my understanding, is a form of failure of transitivity of models. As an illustrative example, he looks at our inability to predict wars and revolutions in terms of lower level physical phenomena:

Whatever else wars and revolutions are, they involve lots of molecule movements. But that has the consequence that any strict law about wars and revolutions would have to match perfectly with the laws about molecule movements. (Searle, 1984, p. 75)

He points out that we have no laws (in the sense of physical laws) about the occurrence of wars and revolutions, although, ultimately,「wars and revolutions, like everything else, consist of molecule movements.」

It is not that higher level phenomena cannot be explained in terms molecule movements. Some can. Searle cites Boyle's law and Charles' law, which can be shown consistent with models of molecule movements. The relationship is relatively simple and the models become predictive. But not so with wars and revolutions. Wars and revolutions are so distant from molecule movements that no such relationship makes sense.

Searle argues that such relationships are impossible not just difficult. His reason is quite deep and thought provoking. To make his case, he asks us to consider the concept of「money,」which as he points out is「whatever people use and think of as money」(Searle, 1984, p. 78). The fact that this concept is self-referential is a key part of Searle's argument, in that「the concept that names the phenomenon is itself a constituent of the phenomenon.」Money can take the form of printed paper, gold coins, or (today) bits stored in a computer and displayed as numbers on a screen. An attempt to explain money as a neurophysiological phenomenon, Searle says, gets tripped up by the many forms that money can take. As we see money in these various forms, the stimulus on the visual cortex will be completely different. Searle asks how these completely different stimuli could have the same effect on the brain:

[F]rom the fact that money can have an indefinite range of physical forms it follows that it can have an indefinite range of stimulus effects on our nervous systems. But since it can have an indefinite range of stimulus patterns on our visual systems, it would … be a miracle if they all produced exactly the same neurophysiological effect on the brain. (Searle, 1984, p. 80)

So the concept of money must be more than a neurophysiological effect, Searle claims.

[T] here can't be any systematic connections between the physical and the social or mental properties of the phenomenon. (Searle, 1984, p. 78)

The same argument seems to apply to effects that are quite unlike the sociological concept of money, such as face recognition. We recognize our mother's face in a black-and-white picture of her taken before we were born, for example, despite enormous differences in the physical structure of the face and the material nature of a black-and-white photo versus a real face. It seems that Searle would have to conclude that this too is not a neurophysiological effect. But I suspect it is. The human brain has evolved to categorize visual stimuli into discrete bins despite huge variability in the stimulus.

I'm an engineer, not a philosopher, and not a neuroscientist. I can't credibly reject or defend Searle's argument, but frankly I don't need it to reach essentially the same conclusion. I am perfectly willing to accept that nobody will ever establish any meaningful connection between the physical stimulus to the visual system and the sociological concept of money. Even if we could construct the layers of epiphenomena, [3] their relationships would be so complex, or there would be so many layers, that nothing meaningful could ever arise from their connections. The phenomena at the higher levels are emergent phenomena , in that they comprise the lower level phenomena but have their own identity and properties. In later chapters, I will examine the fundamental limits of modeling that make such connections improbable even if the concept of money really is a neurophysiological effect.

But perhaps more interesting, even for some phenomena where we know exactly how to explain how they arise from physical effects, it is not useful to do so. In chapter 5 , I argue that, although software is ultimately electrons sloshing around in silicon, there are so many layers of modeling between the physics and the software that the connection to the physical is practically meaningless.

I claim that a high-level technology such as Wikipedia has little (and declining) meaningful connection with the underlying physical phenomena in semiconductor physics that make it all work. For digital technology, we can in fact trace the connection from Wikipedia all the way down to semiconductor physics. I will do this for you in chapters 4 and 5 . But in doing so, I will show you that there are so many levels of indirection that what happens at the higher level has little meaningful connection with what happens at the lower levels.

Engineers have an advantage over scientists when dealing with layers of models. Natural biological systems and wars and revolutions are givens in our world. Engineered systems are not. For engineered systems, the goal is not to explain them in terms of lower level phenomena. The goal instead is to design them using lower level phenomena. This different goal makes it much easier to exploit the transitivity of models.

Consider synthetic biology, which is concerned with designing artificial biological systems. This field is less focused on explaining naturally occurring systems and more focused on leveraging natural biological pathways to synthesize new systems. In synthetic biology, researchers have embraced layered abstractions to great effect. Endy (2005), for example, argues for using predefined functional modules to create biological systems. Indeed, an engineering discipline such as synthetic biology can more readily use layered abstractions because the models need only to model the systems being created. The bioengineers choose the systems to be modeled, and they choose them in part because they can model them. To be effective, scientific models need to model the systems given to us by nature, which are much more numerous. And we can't choose those. They are given.

In the next two chapters, I will elaborate on the layers in figure 3.3 , with an emphasis on understanding how they came about and with the goal of showing that the specific design of such layers is the creative work of humans, not a collection of God-given facts. But first I would like to spend a little time thinking about how to decide which layer to focus on for any given task.

[3] An epiphenomenon is a phenomenon that can be completely explained in terms of more fundamental phenomena.

3.3 模型的传递性

一个文字处理系统，就像我在写作本书时使用的一样，运行在图 3.2 所示的微处理器上，其使用基于图 3.1 所示原型的晶体管。

在硅物质和文字处理器之间存在着许多建模层次。在物理和维基百科这样的系统之间可以找到更多的层次。就像铅笔一样，没有人知道如何制作这样一个系统。然而，这种系统的存在的确是人类伟大智慧和创造力的直接结果。每个建模层都允许个人对设计做出贡献，而无须了解或关心他们正在使用的建模层是如何产生的，也无须知道他们正在创建的建模层将如何被其他设计人员使用。

图 3.3 给出了构建一个系统（例如维基百科）所涉及的几个层次。我的朋友兼同事阿尔贝托·圣乔瓦尼 — 温琴泰利称这些层次为「平台」（圣乔瓦尼 — 温琴泰利，2007）。这是一个恰当的术语，因为每个平台构成了构造上层模型的基础。上面的一些模型又定义了用于进一步构造的平台。圣乔瓦尼 — 温琴泰利指出，这些平台给了设计人员「选择的自由」。每个平台下面都存在很多种可能性，这些可能性提供的选择比任何设计人员所能处理的都要多。而在平台之上，可做出的选择很少。例如，与使用逻辑门相比，你可以通过创建一个晶体管网络设计更多的系统（将在第 4 章中做出解释）。但是，当逻辑门提供了一个合适的平台时，如果你使用逻辑门而不是晶体管网络，设计工作就会变得容易很多。

图 3.3 范式的分层。

人们偶尔会在科学中遇到这种抽象分层的使用。但与工程相比，科学中的这种情况还是比较少见的，而且也不会出现那么多的层次。科学家希望构建物理现实的模型，然而，物理现实的模型的模型会仅仅因为其离物理现实更远而变得更加令人怀疑。

18 世纪末发展起来的气体定律是模型成功分层的科学的例子。这些定律与气体的压力、温度、体积和质量有关。它们包括玻意耳定律、查理定律、盖 — 吕萨克定律和阿伏伽德罗定律。这些模型描述了最终由气体中大量分子的运动所导致的现象，但它们并没有从单个分子的角度描述这些现象。例如，玻意耳定律指出，在不变的温度下，气体的压力与它所占的体积成反比。因此，如果你要减小气体的体积（压缩气体），气体的压力就会增加。这些都是非常有用的模型的模型，其中较低层次是随机移动的分子之间的相互碰撞以及与外壳表面碰撞的模型。

可以说，生物学是最复杂的自然科学学科。一些研究人员认为，只有通过这样的分层才能使自然生物系统变得容易理解。例如，费希尔等人在 2011 年提出了如图 3.4 所示的层次「以征服生命系统的复杂性」。他们类比计算机硬件系统的分层而明确提出了这些层，甚至相应地命名了其中的一些层，如「生物逻辑门」。然而，图中的问号显示这种方法还不成熟。至少到目前为止，生物学似乎比工程更难利用模型的传递性。

我相信这个限制是非常基础的。科学不能像工程那样从建模范式的分层中获益。原因在于，工程师构建系统来匹配模型，而不是构造模型来匹配系统。我将在后面的章节对此进行更全面的讨论。

图 3.4 费希尔等（2011）为合成生物学提出的抽象层次。

即使没有分层，我们物理世界中的许多现象（甚至也许是大多数现象）也不适合于科学建模。例如，约翰·塞尔写了大量关于科学模型无法处理认知和社会现象的文章，尽管这些现象显然属于物理现象。我们回顾一下他的观点，「自然科学的方法在研究人类行为时并没有像在物理学和化学中那样带来回报」（塞尔，1984:71）。据我的理解，他的解释是模型传递性失败的一种形式。作为一个例证，他从较低层次的物理现象来看待我们无法预测战争和革命的现象：

不管是什么样的战争和革命，它们都会涉及大量的分子运动。其结果是，任何有关战争和革命发生的铁律都必须与分子运动的规律完全一致。（塞尔，1984:75)

他指出，我们没有关于战争和革命发生的规律（从物理规律意义上讲）。尽管最终「战争和革命，和其他一切事物一样，都是由分子运动组成的」。

这并不是说更高层次的现象不能用分子运动来解释。有些现象是可以的。塞尔引用了玻意耳定律和查理定律，这两个定律与分子运动的模型是一致的。这种关系相对简单，而且模型具有预测性。但是，战争和革命并非如此。战争和革命距离分子运动是如此遥远，以至没有任何关联是有意义的。

塞尔认为建立这种关联不仅是困难的，也是不可能的。他给出的理由既深刻又发人深省。为了证明他的观点，他让我们思考一下「货币」这个概念。正如他指出的那样，「货币就是人们所使用和认为是货币的东西」（塞尔，1984:78）。这个概念是自我参照的这一事实，是塞尔观点的关键所在。原因在于，「命名现象的概念本身就是这个现象的组成部分」。货币可以有不同的形式，如纸币、金币或（今天）存储在电脑中并以数字形式显示在屏幕上的比特位。塞尔说，试图将货币解释为一种神经生理学现象的尝试为货币的多种形式所羁绊。因为，当我们看到这些不同形式的货币时，视觉皮层上的刺激会完全不同。塞尔提出问题 —— 这些完全不同的刺激是如何对大脑产生同样的影响的：

从货币可以有范围不定的物理形式这一事实来看，它可以对我们的神经系统产生范围不定的刺激作用。但是，由于它可以给我们的视觉系统带来一种范围不定的刺激模式，如果它们都能对我们的大脑产生完全相同的神经生理效应，那么它会…… 是个奇迹。（塞尔，1984:80）

因此，塞尔认为，货币的概念对我们的大脑不会仅仅是一种神经生理效应。

这种现象的物质和社会或者精神属性之间不可能有任何系统的联系。（塞尔，1984:78）

同样的观点似乎也适用于与货币这一社会学概念截然不同的现象，如人脸识别。例如，我们能够在一张我们出生以前拍摄的黑白照片中认出自己母亲的脸，尽管那时黑白照片上母亲的面容与现在有很大的差异。塞尔似乎必须得出这样的结论 —— 这也不是一种神经生理效应。但是，我怀疑它是。尽管刺激有很大的可变性，但人类大脑已经进化到将视觉刺激归类为不相关联的类别了。

我是工程师，不是哲学家，更不是神经学家。我不能言之凿凿地拒绝或支持塞尔的观点，但坦率地讲，我并不需要它得出本质上相同的结论。我完全愿意接受这一点 —— 没有人会在视觉系统的生理刺激和货币的社会学概念之间建立任何有意义的联系。即使我们能构建出副现象的层次，它们之间的关系也会特别复杂，或者会有很多层次，以至从它们的联系中也不会产生任何有意义的东西。较高层次的现象是涌现现象，它们包含了较低层次的现象，但又有其自身的特征和属性。在后面的章节中，我将探讨建模的基本限制。即便货币的概念确实是一种神经生理学效应，这些限制也会使这种联系变得不可能。

这也许是更为有趣的事实，即使我们清楚地知道如何解释产生于物理效应的一些现象，这样做本身也没什么意义。在第 5 章，我会谈到，尽管软件最终是在硅材料中流动的电子，但是物理效应和软件之间存在着太多的建模层。实际上，这已经使得它们之间的联系变得毫无意义了。

我认为，像维基百科这样的高端技术，与使其运转的半导体物理学中的潜在物理现象几乎没有（而且正在减少）什么有意义的联系。对于数字技术，我们实际上可以将这种关系从维基百科一直追溯到半导体物理学。我将在第 4 章和第 5 章中探究这些问题。但在这个过程中，我将向大家展示，较高层次与较低层次的模型之间存在着许多间接层次，以至高层次上发生的事情与低层次上发生的事情几乎没有什么有意义的联系。

在处理模型的分层时，工程师比科学家有优势。自然生物系统以及战争与革命都是我们的世界赋予的，而工程系统不是。就工程系统而言，工程师的目标不是用较低层次的现象解释它们，而是用较低层次的现象设计它们。这个不同的目标使得利用模型的传递性变得更加容易。

以合成生物学为例，它与设计人工生物系统有关。这一领域较少关注解释自然产生的系统，而更侧重于利用自然生物途径来合成新的系统。在合成生物学中，研究人员采用了分层的抽象概念，并获得了很大的成效。例如，恩迪（2005）主张使用预设的功能模块创建生物系统。实际上，像合成生物学这样的工程学科，可以更容易地使用分层抽象，因为模型只需要对正在创建的系统建模。生物工程师选择要建模的系统，而且他们选择系统的部分依据是他们可以建模这些系统。为了提高效率，科学模型就需要对大自然赋予我们的众多系统进行建模。而且，我们不能选择这些系统，它们是大自然赋予我们的。

在接下来的两章中，我将详细介绍图 3.3 中的这些层，重点在于理解它们是如何产生的，而且我的目的在于说明这些层是人类的创造性工作，而不是上帝给予的事实的集合。但是，我首先还是想先花一点儿时间来思考，对任何给定的任务，如何确定应该关注哪个层。

### 3.4 Reductionism

At the lowest level, a word processor and Wikipedia are electrons sloshing around in silicon and metal, and the programs that make up Wikipedia are models of models of models of · · · models of electrons sloshing around in silicon and metal. It is tempting to fall into a reductionist trap and say that Wikipedia is「nothing but」electrons sloshing around in silicon, but this would grossly misrepresent reality.

A reductionist perspective explains a system at any level of modeling in terms of the level below it. For example, we could explain how a Wikipedia search uses operators in a programming language that compare text, which are realized by comparisons between binary representations of text in machine code, which uses a compare instruction in an instruction set architecture, which is implemented by microarchitecture with an arithmetic logic unit (ALU) that can do comparison, which is made up of logic gates that implement the comparison, which gates are interconnections of transistors, which transistors are three-dimensional structures of doped silicon. This is a terrible explanation of the search function of Wikipedia.

One of the implications of reductionism is that an epiphenomenon has no effect on the phenomena that explain it. The epiphenomena of temperature and pressure of a gas, for example, can be explained in terms of the underlying molecule movements, but molecule movements would exist unchanged even if we had no concepts of temperature and pressure. But this implication is patently false for the layers of figure 3.3 . Only the lowest foundation of these layers, electrons moving an electric field, is given to us by nature. Every other layer is constructed by humankind, often distinctly with an eye toward servicing better the layer above. It is perfectly valid to explain the operation of a logic gate in terms of its role in the design of digital machines and the design of digital machines in terms of the software they are expected to execute. The design of each layer is affected by the layers below and above it.

In the sciences of the natural, if scientists were to use such layers, it would be a teleological leap of faith to claim that higher levels of the stack affect lower ones. How could the existence of a biologic gates abstraction in figure 3.4 affect nature's realization of signaling pathways? In contrast, in the stack of figure 3.3 , it is not farfetched to claim that transistors are pretty good switches to enable Wikipedia.

In fact, designers of physics-based electronics are constantly trying to improve transistors to make them more like ideal switches. Fundamentally, a transistor is not a switch. It is an amplifier. But engineers tune the design of transistors to make them more like switches. For example, when a transistor is off, it is desirable that little current leak through it. This will reduce energy consumption, making it possible to pack more transistors into a small space without generating excessive heat that could melt the silicon. Hence, engineers will tweak the design of the physical structure to reduce leakage. They do this so that Wikipedia can work better. Teleological explanations in this case are perfectly reasonable.

The resemblance, therefore, between the stack of models in figure 3.3 and the one in figure 3.4 is superficial at best. I come back to the point I made in section 2.3 , which is that in science, the value of a model lies in how well its properties match those of the target, whereas in engineering, the value of the target lies in how well its properties match those of the model. If our model of a transistor is a switch, then the most valuable transistors are the ones that most perfectly behave like ideal switches.

With sufficient positivist dogmatic determination, we could still insist on a reductionist approach. Once we are given transistors by the physical electronics engineers, gates by the VLSI design software, a microarchitecture by Intel, an instruction set architecture by Intel, a Java compiler by Oracle, and a library of Java components by the Eclipse Foundation, then we could explain how Wikipedia works in terms of these foundations.

But this is too nerdy even for me. First, these foundations aren't static, so our laboriously constructed explanation could only be valid at an instant. But more important, it vastly understates what Wikipedia really is. At the higher layers of abstraction properties emerge that are difficult if not impossible to explain in terms of the lower level abstractions. An enormous part of the value of Wikipedia lies in its essence as a partnership between technology and culture. I admit a genuine aesthetic delight when I encounter a particularly well-written Wikipedia page and a sense of frustration and gloom when I find a more poorly written page or one that too clearly reflects the views of too few people. A well-written Wikipedia page is difficult to explain in terms of sloshing electrons.

Technology alone does not create a phenomenon such as Wikipedia. Any reductionist explanation of the phenomenon would be naive. In later chapters, I will argue that the failure of reductionism is fundamental and unavoidable in complex technology.

Notice that our layering need not stop at the top of figure 3.3 . The software in Wikipedia is created within the modeling paradigms at the top of the figure, but in large part that technology is molded to support a sociological layer above it. But I am a nerd, and I don't understand people, so I won't try to extend my analysis to those sociological levels. I will leave that to the social scientists.

In the next chapter, I will focus on hardware technologies. I point out that hardware does not last nearly as long as the models of the same hardware. Models and the paradigms on which they are based, despite having no material form, are more durable than the things they model, despite those being physical. I focus on digital technology because as we move up from the physical layer (silicon chips), we quickly get extremely expressive media capable of realizing enormously complex and intricate models. The expressiveness of these media unleashes the creativity of humans, enabling the emergence of such transformative technologies as Wikipedia.

In chapter 5 , I focus on software technologies. Here, I point out that software encodes the paradigms on which it is constructed. This self-scaffolding enables the bootstrapping of truly innovative artifacts, ones that can profoundly affect human culture. In later chapters, I will explain what software cannot do. The door remains open to further creativity.

3.4 还原论

在最低层次上，文字处理器和维基百科都是在硅材料和金属中流动的电子，而构成维基百科的程序是硅材料和金属中流动的电子的模型的模型的模型的模型…… 人们很容易落入还原论的陷阱，于是认为维基百科「除了」是电子在材料硅中流动外什么都不是，但这会极大地歪曲事实。

对于任何建模层的系统，还原论的观点是用其下面的一层来进行解释的。例如，我们可以解释，维基百科的搜索功能是如何使用编程语言中比较文本的操作符的，这些操作符通过比较机器码中的文本二进制表示来实现，机器码使用了某个指令集体系架构中的一条比较指令，指令集体系架构由带有一个可以执行比较操作的算术逻辑单元（ALU）的微体系结构实现，该逻辑单元由实现比较功能的一组逻辑门构成，这些逻辑门是互连的一组晶体管，而晶体管是三维结构的掺杂硅。显然，这是对维基百科搜索功能的一个糟糕解释。

还原论蕴含的一个含义是，一种副现象对解释它的现象没有任何影响。例如，气体的温度和压力的副现象可以用潜在的分子运动来解释，但是，即便我们不了解温度和压力的概念，分子运动也不会发生改变。然而，对于图 3.3 所示的这些层来说，这一含义显然是错误的。只有这些层的最低层，即移动电场的电子，是自然界赋予我们的。其他的每一层都是由人类构建的，而且其目的通常是更好地服务于上层。以逻辑门在数字机器设计中的作用来解释逻辑门的操作，以及用数字机器所要执行的软件来解释数字机器的设计，都是非常有效的，因为每一层的设计都要受到其下面以及上面层的影响。

在自然科学中，如果科学家想要使用这样的层，那么声称栈中更高的层影响其中较低的层将是一次信念的目的论飞跃。图 3.4 中生物门的存在如何影响自然界的信号通路的实现？相比之下，如果认为图 3.3 的栈中，晶体管是启动维基百科的很好的开关，这样的观点就不会让人觉得牵强了。

事实上，基于物理电子学的设计者一直在努力改进晶体管，使其更像理想的开关。从根本上讲，晶体管并不是开关，而是一个放大器。然而，工程师们对晶体管的设计进行了不断调整，使它们更像开关。例如，当晶体管处于截止状态时，通过它的泄漏电流应该非常小。这样可以减少能耗，这使得将更多的晶体管封装到一个小空间而不产生可能融化硅材料的过多热量成为可能。因此，工程师将会调整物理结构的设计，以减少电流的泄漏。他们这样做是为了让维基百科更好地运行。在这种情况下，有目的论的解释是完全合理的。

因此，图 3.3 与图 3.4 所示模型栈的相似之处充其量只是表面的。

我现在要重申一下我在 2.3 节提出的观点 —— 在科学中，模型的价值取决于它的特性与目标物属性的匹配程度，而在工程中，目标物的价值在于它的属性与模型特性的匹配程度。如果我们的晶体管模型是一个开关，那么最有价值的晶体管会是那些表现得最像理想开关的晶体管。

尽管我们有着坚持实证主义教条的决心，但是我们仍然可以坚持一种还原论的方法。一旦我们得到了物理电子工程师设计的一些晶体管、超大规模集成电路软件设计的一些逻辑门、英特尔设计的微体系结构以及指令集体系架构、甲骨文开发的 Java 编译器、Eclipse 基金会的 Java 组件库，我们就可以用这些基础来解释维基百科是如何工作的。

但是，这些解释对我来说太过于呆子气了。首先，这些基础并不是静态的，所以我们费力构建的解释只会在瞬间有效。而更重要的是，这种解释大大低估了维基百科存在的真正意义。在抽象的更高层次，出现了一些很难（如果不是不可能的话）用较低层次的抽象来解释的属性。从本质上说，维基百科使技术和文化达成一种伙伴关系。这在很大程度上就是维基百科的价值所在。我承认，当我看到一个写得特别好的维基百科页面时，我确实感到一种真正的审美上的愉悦；而当我看到一个写得很糟糕的页面，或者过于清晰地反映太少人的观点的页面时，我会感到非常沮丧和郁闷。一个写得好的维基百科页面很难用流动的电子来解释。

技术本身并不能创造出像维基百科这样的现象。对该类现象进行任何简化的解释都是幼稚的。在后面的章节中，我将说明，还原论的失败是复杂技术中不可避免的基本问题。

请注意，我们的分层不需要止步于在图 3.3 所示的顶部层次。

维基百科中的软件是在该图顶部的建模范式中被创建的。但在很大程度上，技术是为了支撑其上的社会学层次才被建模的。我只是个技术呆子，我不了解人，所以我不会试图把我的分析扩展到那些社会学层次。我把这个任务留给社会科学家。

在下一章，我将重点介绍硬件技术。我认为，硬件的生命力并没有该硬件的模型那么持久。尽管没有物质的形式，但是模型和它们所基于的范式比它们所建模的事物具有更持久的生命力。我之所以关注数字技术，是因为当我们从物理层（硅芯片）开始向上时，我们很快就会得到极具表现力的媒介，其可以实现极其复杂的模型。这些媒介的表现力释放了人类的创造力，并促成了像维基百科这样的变革性技术的出现。

在第 5 章，我将聚焦于软件技术。在这里，我需要指出，软件对构建它的范式进行编码。这种自我支撑能激发真正的创新力，并创造出那些能够对人类文化产生深远影响的真正的创新产品。在后面的章节，我将阐释软件的局限性。进一步创新的大门依然敞开着。

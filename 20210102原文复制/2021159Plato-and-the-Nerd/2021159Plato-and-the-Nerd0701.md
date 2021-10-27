## 0701. Information

· · · in which I examine the concept of information, what it is and how to measure it; and in which I introduce Claude Shannon's way of measuring information and show that information cannot always be represented digitally.

0701 信息

在本章，我会研究信息的概念，信息是什么以及如何度量信息；我还会介绍克劳德·香农度量信息的方法，并说明信息并非总是可以用数字方式来表示的。

### 7.1 Pessimism Becomes Optimism

In chapter 2 , I emphasized the importance of keeping distinctly separate in our minds the model and the thing being modeled. Unfortunately, this is really hard to do. Because so much of our thought process is structured around models, we have an enormous backdrop of unknown knowns. But a failure to make this separation inevitably leads us to invalid conclusions.

Engineers choose their models and then seek physical realizations that are faithful to those models. For this task, we need models that we can understand. Although we have developed, over centuries, a huge arsenal of models and ways of building models, I will show that the number of possible models in this arsenal is tiny compared with the number of models possible in theory. There is no end to the possible engineering innovations.

A scientist, in contrast to an engineer, tries to find or invent a model (which can take the form of a「law of nature」) to match a given physical object or process. A timeless goal in science has been to find a small number of such models that can somehow「explain」everything in the universe. In some sense, whereas an engineer strives to grow the number of relevant models (those for which we can build a faithful physical realization), the scientist tries to shrink the number of relevant models (those needed to explain the natural world).

Unfortunately for science, this timeless goal is unachievable. We already know that nature is capable of creating processes that are at least as sophisticated as software on computers because humans and our computers, after all, exist in the natural world. In chapter 8 , I will review Alan Turing's classic result that it is impossible, in general, to tell what a program will do merely by looking at the program. This finding alone crushes the optimism that any small set of rules can explain everything in the universe because it shows that we have no way to explain the behaviors of some programs that exist in the universe. All we have are the programs themselves.

The situation for science is exacerbated by the fact that mathematical models, which are not exactly the same as computational models and form the bedrock of scientific explanations of the natural world, are incomplete in a similar manner to software, as I will explain in chapter 9 . Kurt Gödel's classic incompleteness theorems show that any system of mathematical models that is potentially rich enough to explain the natural world will be either inconsistent or incomplete.「Inconsistent」means that it has statements that can be shown to be both true and false.「Incomplete」means that it has statements that cannot be shown to be true and cannot be shown to be false.

The goal of an engineer is not to explain the natural world but rather to create artifacts and processes that have never before existed in that natural world. Engineers need only to explain the systems they design, not the systems given to them by nature (at least not as their primary task). They build physical systems to match their models rather than the other way around. If the modeling toolkit is rich and expressive enough, and if the space of physical systems is vastly larger than the modeling toolkit, then there is plenty of room for innovation.

Engineering, of course, requires science. As we try to synthesize new physical realizations from our models, we will learn more about nature as we try to understand how the physical realizations deviate from the predictions of the model. Engineering, therefore, can provide a set of guideposts for science by exposing phenomena that nature has not happened to expose.

The transistor is a good example of this reversal, where engineering drives science. I know of no natural occurrence of a transistor that has ever been found. But the engineering effort to create an electrically controllable switch has led to a much deeper scientific understanding of how electricity behaves in materials. That scientific understanding has in turn enabled better engineering models, bootstrapping a process of progress that cannot occur by just passively observing systems that nature happens to give us. The limitations exposed by Turing and Gödel do not impede this progress. Instead, they simply assert that this process will never be complete. There will always be room for more progress.

So far in this book, I have argued that digital technology and computation provide a rich medium for such creative work. But like the scientist, the engineer is subject to fundamental limitations of both computation and mathematical models. For engineers, these limitations do not undermine any timeless mission. Engineers have the luxury that they can try to avoid systems they cannot explain. Software engineers, for example, usually try to write programs that will exhibit behaviors they can explain, avoiding programs that Turing showed are inexplicable. But to avoid them, they need to understand the limitations of their modeling toolkit. Thus, in contrast to the previous chapters in this book, in the next few chapters I will explain what software and mathematical models cannot do.

I focus on digital technology and computation, which are fundamentally about processing information. But what is information? Only with a clear notion of information can we understand what can and cannot be done with digital technology. Hence, information is the subject of the rest of this chapter.

7.1 悲观主义变成乐观主义

在第 2 章，我强调了在我们的头脑中清楚地区分模型和被建模事物的重要性。然而，不幸的是，这真的很难做到。因为我们的思维过程有很多是围绕着模型的，所以我们有一个巨大的未知的背景。但是，这种分离的失败将不可避免地导致我们得出无效的结论。

工程师选择他们的模型，然后寻找符合这些模型的物理实现。我们需要能够完全理解这项任务所需的模型。尽管几个世纪以来，我们已经开发了一个巨大的模型库以及大量构建模型的方法，但是，我将向大家说明，这个库中可能的模型数量与理论上可能的模型数量相比是微不足道的。换言之，可能的工程创新是永无止境的。

与工程师不同的是，科学家试图找到或发明一个模型（可能是「自然法则」的形式）来匹配一个特定的物理对象或过程。科学领域的一个永恒目标就是找到少量这样的模型，以某种方式去「解释」宇宙中的一切事物。从某种意义上讲，工程师努力拓展相关模型的数量（那些我们可以为之建立一个可靠物理实现的模型），而科学家则试图减少相关模型的数量（那些需要用来解释自然世界的模型）。

不幸的是，对于科学来说，这个永恒的目标是无法实现的。我们已经知道，大自然能够创造出至少和计算机软件一样复杂的过程，因为人类和我们的计算机毕竟都存在于自然界中。在第 8 章，我将回顾艾伦·图灵的经典发现，一般来说，仅通过阅读程序是不可能判断出程序的功能的。这一发现本身就粉碎了一种盲目的乐观情绪 —— 任何一个小规则集都可以解释宇宙中的一切事物，因为它表明我们根本无法解释宇宙中存在的某些程序的行为。我们只是拥有程序本身罢了。

正如我将在第 9 章中解释的那样，数学模型与计算模型不完全相同，它们构成了科学解释大自然的基石，然而它们与软件一样是不完备的。这一事实恶化了科学的处境。库尔特·歌德尔经典的不完备性定理表明，任何能够解释自然世界的数学模型系统，无论它多么充分，都要么是不相容的，要么是不完备的。「不相容」意味着它的命题既可以被证明为真，也可以被证明为假。「不完备」是指它的命题既不能被证明为真也不能被证明为假。

工程师的目标不是解释自然世界，而是创造自然世界中从未存在过的人工制品和过程。工程师只需要解释他们所设计的系统，而不是自然界中存在的系统（至少这不是他们的首要任务）。他们建立物理系统来匹配他们的模型，而不是反过来。如果建模所需的工具足够丰富和具有表现力，并且物理系统的空间比建模工具集大得多，就有足够的空间进行创新。

当然，工程是需要科学的。当我们试图从模型中合成新的物理实现时，我们就会更多地了解自然，因为我们会试图理解物理实现是如何偏离模型的预测的。因此可以这么说，工程可以通过揭示自然未解之现象，为科学提供一套指南。

晶体管正是上面所说的工程反向推动科学发展的一个很好的例子。据我所知，我们还没有发现过晶体管的自然现象。但是，创造一种电控开关的工程努力，已经使人们对电流在材料中的行为方式有了更深入的科学理解。这种科学理解反过来使得构建更好的工程模型成为可能，并引导了这一过程，而这一过程不可能仅仅通过被动地观察大自然赋予我们的系统来实现。图灵和哥德尔揭示的局限性并不妨碍这一过程。相反，他们只是断言这个过程永远不会完成。进步的空间永远很大。

到目前为止，在本书中，我已经论证了数字技术和计算为这种创造性的工作提供丰富媒介的观点。但是，和科学家一样，工程师也受到计算和数学模型的根本限制。对工程师来说，这些限制不会削弱他们永恒的使命。工程师一直都有一个优势，那就是他们可以避开他们无法解释的系统。例如，软件工程师通常会尝试编写能够展示他们可以解释的行为的程序，而避开图灵所展示的那些无法解释的程序。但如果要避免这些程序，工程师就需要了解建模工具集自身的局限性。因此，与本书的前几章相比，在接下来的几章中，我将解释软件和数学模型不能做什么。

我关注的是数字技术和计算，它们基本上都是关于信息处理的。但是，信息到底是什么呢？只有明确了解信息的概念，我们才能理解数字技术能做什么，不能做什么。因此，信息是本章后续内容的主题。

### 7.2 Information-Processing Machines

A computer program is a model. Ultimately, it models electrons sloshing around in silicon and metal. But as I've pointed out, there are so many levels of abstraction between software as a model and semiconductor physics that viewing software as a model of electrons sloshing is not useful. In fact, software is more usefully viewed like mathematics. It is a formal model, existing in its own self-scaffolded world. Like mathematics, it is a powerful model. We can do a lot with software.

But we can't do everything. In fact, I will show you in chapter 8 that despite the incredible power of software, we can do almost nothing with it, in the sense that no matter how much we do with it, there are vastly many more things we cannot do with it.

Many futurists and technology enthusiasts exaggerate the capabilities of software. To pick on one, in his book Tools for Thought , Howard Rheingold states,

The digital computer is based on a theoretical discovery known as「the universal machine,」which is not actually a tangible device but a mathematical description of a machine capable of simulating the actions of any other machine. Once you have created a general-purpose machine that can imitate any other machine, the future development of the tool depends only on what tasks you can think to do with it. (Rheingold, 2000, p. 15)

Rheingold draws the same conclusion that I do, that technological progress is limited by humans rather than by technology but for the wrong reason. Rheingold actually misrepresents the history of computing. There is no universal machine, mathematical or otherwise. What he is actually referring to is known as the「universal Turing machine,」which is capable of simulating any Turing machine, not any machine. There are machines that are not Turing machines, like my dishwasher, for example.

But wait, I'm sure that Rheingold would object now that my dishwasher is not an information-processing machine, and his book is about information-processing machines. Dirty dishes are not a form of information (or maybe they are; see section 8.4 in the next chapter). So what is an information-processing machine?

The first question we have to answer, the one I focus on in the rest of this chapter, is, what is information? Merriam-Webster has several definitions, but to me the most relevant to software is:

2 b: the attribute inherent in and communicated by one of two or more alternative sequences or arrangements of something (as nucleotides in DNA or binary digits in a computer program) that produce specific effects.

The key in this definition is「one of two or more alternative sequences or arrangements.」Information is the resolution of alternatives. When there are two alternatives, for example, a transistor can be on or off or a coin can yield heads or tails,「information」is the determination of one of the alternatives.

With a little thought, I hope you can see that this is consistent with an intuitive notion of information. If, for example, I don't know whether my colleague Fred is married to Sue, then there are two「alternative arrangements.」If you tell me that Fred is married to Sue, then I have received information from you in the sense that what you have conveyed to me resolves these alternatives. Notice that it is still information, even if you lied to me. You have conveyed a resolution to the alternatives, and whether that resolution is true is a separate issue.

Merriam-Webster also gives the following definition:

2 d: a quantitative measure of the content of information; specifically: a numerical quantity that measures the uncertainty in the outcome of an experiment to be performed.

Measuring information is a relatively recent development, usually credited to Claude Shannon. In 1948, while working at the storied Bell Labs, Shannon published a paper called「A Mathematical Theory of Communication」in the Bell System Technical Journal . This paper launched the field of information theory (Shannon, 1948). In this paper, Shannon used probability theory (about which I will say more in chapter 11 ) to come up with a measure of the amount of information contained in a sequence of bits and the amount of information that can be conveyed over an imperfect communication channel. Solomon Golomb, who was hugely influential in subsequent development of coding and information theory, and to whom I owe the「drilling through the map」metaphor, remarked that Shannon's influence cannot be overstated:「It's like saying how much influence the inventor of the alphabet has had on literature」(Horgan, 1992).

Suppose, by the first definition from Merriam-Webster, that there are exactly two「alternative arrangements」for something. Fred is either married or not. A coin toss can yield heads or tails. Then once we have resolved these alternatives, we have received one bit of information, exactly representable by one binary digit, 0 or 1. Can information always be represented by bits?

Note that the physical world rarely gives us exactly two alternative arrangements for anything. A coin toss could result in the coin falling into a pond, sinking to the bottom, and embedding in the mud in a vertical position, with neither heads nor tails being up. Even in Fred's case, Fred may be married to Sue, in that there are papers filed with the local courthouse, but living with Joe and wishing that his state allowed him to be married to Joe. Marriage is a model of a social structure, and only the model can have a binary choice between exactly two arrangements. The physical world is messier. We need to be careful to keep the map (the legal institution of marriage) distinct from the territory (Fred's actual situation).

Nevertheless, Shannon measured information in bits. As it turns out, this measure only works well when the alternative arrangements are discrete and finite, or when attempting to communicate over an imperfect channel. Suppose that instead of telling me whether Fred is married (one bit of information), you tell me the temperature in the room right now. How many bits of information have you conveyed? This question is impossible to answer without making many more assumptions. How much do I already know about the temperature in the room? Is the number of possible temperatures finite? Perhaps I only care about the temperature within a degree or so. Then the number of possible messages you will convey to me is certainly finite. But have you really conveyed the temperature? Does the temperature itself in the room entail information? Could it have an infinite number of possible values?

These are all difficult questions. Even when the number of alternative arrangements is finite, the amount of information conveyed by resolving the alternatives is not always obvious. Shannon noticed that the amount of information conveyed depends not only on the number of alternatives but also on the likelihood of the alternatives. I will next explain how Shannon measured information in units of bits when the number of alternatives is finite.

7.2 信息处理机

计算机程序是一个模型，它最终模拟了在硅材料和金属中流动的电子。但是，正如我指出的那样，在作为模型的软件以及半导体物理学之间有很多抽象层，所以仅仅把软件看作电子流动的模型是没有用的。事实上，将软件视为数学更有用。它是一个形式化的模型，存在于它自己构建的世界中。就像数学一样，它是一个强大的模型。我们可以用软件做很多事情。

但是，软件并不是什么事都能做到。事实上，我将在第 8 章向读者展示，尽管软件有着不可思议的力量，但我们几乎不能用它做任何事情。从这个意义上说，虽然我们已经用软件做了多少事情，但是还是有很多事情我们不能用软件来做。

许多未来学家和技术爱好者夸大了软件的实际能力。举个例子，霍华德·莱因戈尔德在他的《思考的工具》一书中写道：

数字计算机以一个被称为「通用机器」的理论发现为基础，它实际上并不是一种有形的设备，而是一种能够模拟其他任何机器动作的机器的数学描述。一旦你创造出一种可以模仿任何其他机器的通用机器，这个通用工具的未来发展就只取决于你想用它来执行什么任务。（莱因戈尔德，2000:15）

莱因戈尔德得出的结论和我的一样，即技术进步受到人类的限制，而不是技术的限制，但其原因是错误的。实际上，莱因戈尔德歪曲了计算的演进历史。根本就没有什么通用机器，无论是数学的还是其他的。他实际上指的是所谓的「通用图灵机」，它能够模拟图灵机，而不是任何其他机器。有些机器不是图灵机，例如我的洗碗机之类的机器。

但是，请稍等一下。我敢肯定莱因戈尔德现在会反对说，我的洗碗机并不是一台信息处理机，而他的书是关于信息处理机的。弄脏的盘子不是一种信息的形式（或者它们可能是，详见 8.4 节）。那么到底什么是信息处理机呢？

我们要回答第一个问题，也就是我要在本章剩余部分重点关注的一个问题 —— 什么是信息。《韦氏大词典》给出了好几个定义，但对我来说，下面这个与软件最为相关：

2 b：由产生特定效果的事物（如 DNA 中的核苷酸或计算机程序中的二进制数）的两个或多个可选序列或选项之一所固有以及表示的属性。

这个定义的关键是「两个或多个可选序列或选项中的一个」。信息是对一组可选项进行选定的解决方案。当有两种选择的时候，例如，晶体管可以导通或截至，或者硬币可以是正面或背面朝上，而「信息」是对其中一种选项的确定。

让我们稍加思考，我希望读者能明白，这与信息的直观概念是一致的。例如，如果我不知道我的同事弗雷德和苏结婚了没有，我就会有两种「可选选项」。如果你告诉我弗雷德和苏结婚了，那么我从你那里得到信息，你向我传达的信息给出这些选项的解决方案。请注意，即使你对我撒了谎，那也是信息，因为你已经就这些选项传递了一个解决方案，而这个解决方案是否正确则是另一回事。

《韦氏大词典》还给出以下定义：

2 d：是对信息量的定量度量；具体而言，是度量待进行实验的结果中不确定性的一个数字量。

度量信息是一个相对较新的发展领域，通常被认为是由克劳德·香农率先创建的。1948 年，香农在著名的贝尔实验室工作时，在《贝尔系统技术期刊》上发表了一篇名为「通信的数学理论」的论文。这篇论文开创了信息论的研究领域（香农，1948）。在论文中，香农基于概率论（我将在第 11 章更详细地介绍这个理论）提出了一种测度方法，其可以度量一个比特序列中所包含的信息量以及在非理想通信信道上能够传输的信息量。所罗门·格伦布对编码和信息论后来的发展有着巨大影响，我也感谢他「在地图上钻孔」的隐喻。格伦布评论说，香农的影响巨大，怎么强调也不为过，「就好比字母表的发明者对文学产生的巨大影响一样」（霍根，1992）。

假设根据《韦氏大词典》的第一个定义，对某物有两种「可选选项」。就上面的例子来说，弗雷德要么结婚要么不结婚。也就是说抛出一枚硬币要么正面朝上要么背面朝上。然而，一旦我们解决了这些选择，我们就收到 1 比特的信息，完全可以用一个二进制数来表示，0 或者 1。那么问题在于，信息总是能用比特来表示的吗？

请注意，物理世界很少恰巧给我们提供任何东西的两种可选选项。抛硬币可能导致硬币掉进池塘里，然后沉到水底，并且垂直地埋入淤泥里，那么抛硬币的结果就既不是正面朝上也不是背面朝上了。即使在弗雷德的例子中，也会出现不同的结果。弗雷德可能会和苏结婚，因为有他向当地法院提交的文件，但是他目前正和乔住在一起并希望他所在的州能够允许他与乔结婚。婚姻是一种社会结构的模式，只有这种模式才能在两种安排之间进行二元选择。物理世界则更加混乱。我们需要谨慎地将地图（例如婚姻的法律制度）与地域（弗雷德的实际情况）区分开来。

尽管如此，香农还是以比特为单位来度量信息。事实证明，只有当可选选项是离散的和有限的，或者试图通过非理想信道进行通信时，这种度量才能很好地被实施。假设你没有告诉我弗雷德是否结婚（1 比特的信息），而是告诉我房间现在的温度，那么你到底传达了多少信息呢？如果不做更多的假设，这个问题是不能被回答的。关于房间的温度我已经知道多少了？房间的可能温度是有限的吗？也许我只关心 1 摄氏度左右的温度。那么，你能传递给我的信息数量肯定是有限的。但是，你真的传递了有关温度的信息吗？房间的温度本身是否蕴含着信息呢？它会有无限多个可能的值吗？

这些都是很难回答的问题。即使可选选项的数量是有限的，解决可选选项的方案所传递的信息量也并不总是显而易见的。香农注意到，传递的信息量不仅取决于可选选项的数量，还取决于这些选项的可能性。在接下来的内容中，我将解释当可选选项的数量有限时，香农会如何以比特为单位度量信息。

### 7.3 Measuring Information

Suppose that we have an unfair coin that almost always comes up heads. Then observing a head does not convey much information. Most outcomes are heads, so you will not be surprised to see heads. Suppose that we toss the coin 20 times and get the following outcomes:

HH HT HH HH HH TH HH HH HH HH

where「H」represents heads and「T」represents tails. We can code this sequence of outcomes using binary digits 0 and 1 as follows:

This encodes the outcomes using 20 bits. It is a quite literal encoding, using a 1 to represent H and a 0 to represent T. However, because tails is much less likely than heads, there are relatively few tails, so Shannon noticed that this sequence can be encoded with fewer than 20 bits by using a less literal encoding. For example, suppose that we group the coin tosses in pairs, as above, and encode pairs of results according to the following table:

In other words, when we get two heads in a row, we will represent that fact with a single bit, 0, rather than two bits, 11. If we get TT, then we will represent that with three ones in a row, 111. These codes are carefully chosen so that any sequence of bits can be unambiguously decoded into a sequence of coin tosses. For example, 010 represents HHTH, four outcomes.

The previous sequence of coin tosses can now be represented as follows:

The more likely「HH」pairs are encoded efficiently with just one bit, whereas the less likely sequences require more bits. This encoding requires only 13 bits rather than the direct encoding, which requires 20. Shannon noticed that if heads are much more likely than tails, then most of the time this alternative encoding will require fewer bits than the direct encoding. So the amount of information in 20 unfair coin tosses is usually less than 20 bits, Shannon observed.

Shannon also noticed that ordinary English-language text could also be encoded more efficiently. A great deal of redundant information is found in a sequence of letters and spaces. If I text you a message saying,「i lv u,」I'm pretty sure you will understand it.

Note that during World War II, Shannon worked on coding schemes for secret communications, including codes used by Roosevelt and Churchill for trans-Atlantic conferences. His cryptography work no doubt lay the groundwork for information theory because it made it clear to Shannon that a message could be encoded in many ways. Some ways would result in a more efficient encoding (fewer bits), and some would be difficult to read if you didn't know the code. If you don't know the code given in the earlier table, then the sequence 0110000100000 is hard to interpret as HHHTHHHHHHTHHHHHHHHH. For most of us, it is hard even if we do know the code, unlike「i lv u,」which requires no explicit listing of the code.

Our encoding may not always work well, however. For example, suppose we get a sequence of 20 tails in a row. The prior encoding will require 30 bits instead of the 20 that the direct encoding requires because each pair TT will be encoded by three bits, 111. This is unlikely, but it is still possible. Using probability, which I will talk about in chapter 11 , we can estimate how unlikely this is. If the coin tosses are all independent (they do not influence one another), and on average 1 in 10 tosses comes up tails, then the probability of 20 tails in a row is 10 −20 . In chapter 11 , I will discuss what this really means, but for this example it simply means that if you repeat the experiment of tossing 20 coins 10 20 times (100 quintillion times), on average, you can expect one occurrence of 20 tails in a row. This outcome is very rare indeed. In fact, we can also use probability to show that most outcomes will require fewer than 20 bits. But I will spare you that nerd storm.

Based on earlier work by Hartley (1928), Shannon used this observation to come up with a quantitative measure of the amount of information conveyed by observing a single coin toss. According to Shannon, if our unfair coin comes up heads, then when we observe this fact, we get − log 2 (0.9) ≈ 0.15 bits of information. Here, 0.9 is the probability of heads, indicating that 9 out of 10 tosses yield heads, on average.

Because heads are much more likely than tails, we can take this as a measure of our surprise or what we have learned, or, in short, information. When we observe heads, we get 0.15 bits of information, much less than one bit. We are not surprised. The information in observing an outcome of tails is − log 2 (0.1) ≈ 3.32 bits, where 0.1 is the probability of tails. We are much more surprised when we see tails. So seeing tails conveys more information, 3.32 bits, than seeing heads, 0.15 bits.

If instead the coin were fair, then the probability of T would be 0.5, meaning that, on average, half of all coin tosses yield T. The Shannon information in observing T is therefore − log 2 (0.5) = 1 bit of information. For a fair coin, every toss gives us one bit of information. It is more surprising than seeing H for the unfair coin and less surprising than seeing T for the unfair coin.

Why the logarithm? This seems kind of arbitrary, a rabbit pulled out of a hat. But a logarithm has a nice property, which is that for any two numbers a and b , log 2 ( ab ) = log 2 ( a ) + log 2 ( b ). Logarithms turn multiplication into addition. Consider a pair of unfair coin tosses that turn out to be TH, tails followed by heads. How much information is in that result? Well, we get 3.32 bits from the T and 0.15 bits from the H, so the pair presumably conveys the sum or 3.47 bits of information. When you receive a sequence of unrelated messages, the information conveyed is the sum of the information in each of the messages (we assume each coin toss has no effect on the outcome of the next coin toss).

Suppose that we toss two coins simultaneously and observe TH. What is the information content in that? To apply Shannon's theory, we need to determine the probability of TH. If the coin tosses are independent (one does not affect the other), then the probability of TH is the product of the probabilities for T and H, or 0.1 × 0.9 = 0.09. This probability is slightly less than 0.1, indicating that slightly fewer than 1 in 10 times tossing two coins we will see TH. So the Shannon information conveyed by observing TH is − log 2 (0.09) ≈ 3.47. Because a logarithm turns a product into a sum, this is the same as the sum of the information we get from each coin toss, − log 2 (0.1 × 0.9) = − log 2 (0.1) − log 2 (0.9). This is why Shannon used a logarithm. It makes the information content in two identical coins tossed simultaneously the same as the information content in two sequential tosses of the same coin.

The logarithm base 2 was used by Shannon so that the information measure would be in units of bits. If you use the natural logarithm instead, then the information measure has units of「nats.」If you use base 10, then it has units of decimal digits. In all cases, however, it measures information.

You might ask why there is the annoying minus sign everywhere. There are two reasons. One is that probabilities are always less than one, [1] and the logarithm of a number less than one is negative. We would prefer a positive number to quantify information, and the minus sign gives us that. The second and more important reason is that the quantity of information should increase as the event gets more rare. Without the minus sign, it would decrease, and the relationship between information and rarity would be backward.

If on average 1 in 10 coin tosses yields tails, then Shannon said that the average information in a single coin toss is

Equation (64) is just the average of these two information quantities, weighted by their probability, and hence it is the average information in one coin toss. This means that each coin toss conveys about 0.47 bits of information rather than one bit of information, on average. In theory, therefore, we may be able to come up with an encoding that will represent 20 coin tosses with only 20 × 0.47 = 9.38 bits, on average. Shannon showed, in fact, that we cannot do any better, so 9.38 bits per 20 coin tosses is the limit. No encoding scheme will do better than this, on average, so the average amount of information in 20 unfair coin tosses is 9.38 bits.

Equation (64) represents what Shannon called the「entropy」in a coin toss. Shannon chose the term「entropy」for this because the mathematical structure of his formula resembles the formula that had previously been used for a concept called「entropy」in thermodynamics. In a profile of Shannon, Horgan writes:

The great mathematician and computer theoretician John von Neumann persuaded Shannon to use the word entropy. The fact that no one knows what entropy really is, von Neumann argued, would give Shannon an edge in debates over information theory. (Horgan, 1992)

Thermodynamics studies the macroscopic properties of materials (especially gasses) in terms of the microscopic properties (especially molecules in motion). The notion of entropy originated in 1870 with the work of physicist Ludwig Boltzmann in Austria, James Clerk Maxwell in Scotland, and Josiah Willard Gibbs in the United States. Entropy is the central concept in the second law of thermodynamics. That law asserts that the entropy in the universe (or in any isolated system within the universe) tends to increase. To Boltzmann, Maxwell, and Gibbs, entropy was a measure of randomness or disorder in a physical system. Physical systems tend inexorably toward greater randomness, where eventually all outcomes are equally likely.

Specifically, Boltzmann and his contemporaries modeled the degree of randomness (entropy) in a macroscopic system (e.g., a volume of gas) as

where M is the number of possible states of the microscopic system (a collection of gas molecules) that are consistent with the observed macroscopic properties of the system (like the temperature and pressure of the gas). The constant k is a scaling constant called the Boltzmann constant. If each of the M states is equally likely, then the probability of each state is 1 /M , and this becomes − k log(1/ M ), which is similar to Shannon's entropy.

At least two significant differences can be found between Boltzmann's entropy and Shannon's. One is the constant multiplier k , which simply changes the units with which we are expressing entropy. Shannon used bits as his units, [2] whereas Boltzmann used joules per degree kelvin (energy per temperature). Because temperature is actually energy, Boltzmann's entropy is dimensionless. Dimensionless quantities do not generally measure something in the physical world, but they can be useful when making comparisons. Boltzmann's entropy allows us to compare the entropy in two scenarios, and the second law of thermodynamics is all about comparing entropies. Entropy at one point in time is higher than entropy at an earlier time. The law assigns little meaning to the actual numbers, only to their relative magnitudes. An exception is that when the entropy is zero, there is a distinct physical meaning. For the entropy to be zero, we need M = 1, which means that there is only one possible state. For an ideal gas, this occurs exactly at a temperature called absolute zero, approximately −460° F or −273° C, where all motion stops.

A second difference between Boltzmann's entropy and Shannon's concerns the notion of the「number of possible states.」In Shannon's model, this notion is well defined because the very notion of the number of possible states is part of the model. When considering a coin toss, Shannon did not consider the unlikely possibility that the coin would land on its edge in the mud, yielding neither heads nor tails. Instead, the「coin toss」is just a physical metaphor for a model where there are exactly two possible outcomes. The notion of probabilities for these outcomes, a notion I consider in more depth in chapter 11 , is also part of the model and hence is well defined.

In Boltzmann's case, however, what is the「number of possible states」of a physical gas? This is well defined at absolute zero but more difficult to pin down at achievable temperatures. Boltzmann assumed each molecule in the gas had a physical position and velocity and the state of the molecule was captured by these numbers. How many possible values are there for the position and velocity of a molecule? In Boltzmann's time, there was no physics that would bound the number of possibilities for these numbers to a finite set. The more recent development of quantum mechanics changes the situation. At least for a closed system with well-defined boundary conditions, quantum mechanics does yield a finite number of states. But for all but the tiniest systems, the number of states is enormous. Moreover, precisely defining the boundary conditions is treacherous and risks confusing the map with the territory. Despite these considerable subtleties, many people have associated Boltzmann's entropy with Shannon's quite closely and concluded that the world is digital. I will examine this question in the next chapter.

But sticking to Shannon's self-contained and well-defined notion of entropy, which exists entirely in the world of models, entropy is a good measure of the uncertainty, randomness, or disorder in a system. If the coin is fair (heads and tails are equally likely), then the entropy is 1 bit, so no encoding scheme can do better than the direct encoding, on average. This is the highest level of uncertainty, randomness, or disorder that a coin-toss system can have. At the other extreme, if the coin is extremely unfair, and you only ever get heads, then the entropy is zero. No information at all is conveyed by observing a coin toss. Certainty is high, there is no randomness, and the coin-toss system is perfectly ordered. The result of a coin toss can be encoded with no bits at all because we already know the outcome.

Shannon's quantification of information content and his choice to express this quantification in bits had an enormous impact on communication theory, computer science, and even philosophy. But it is easy to forget that the theory I've described here applies much more readily to scenarios where the alternative arrangements are finite and distinct. What happens if the alternative arrangements offer an infinite number of possibilities? For example, what if the position of each molecule in Boltzmann's gas can be any point in a volume of space? This set of alternative arrangements is not finite. A direct adaptation of Shannon's entropy to scenarios with a continuous range of possible outcomes has to be interpreted more carefully. I do that in the next section.

I apologize in advance that the next section is a bit more technical. The short story, should you wish to skip to the next chapter, is that information cannot always be represented as binary data. Hence, there is a notion of information that is out of reach for computers.

[1] Probabilities are less than one because we can say「one out of ten coin tosses comes up tails」(probability 1 / 10 = 0.1), but we would not say「eleven out of ten coin tosses comes up tails」(probability 11 / 10 = 1.1).

[2] In fact, the standard term for Shannon's units is shannons, in his honor, but many people continue to use bits.

7.3 度量信息

假设我们有一枚硬币，其几乎总是不公正地正面朝上。那么通过观察硬币正面朝上的情况并不能获得更多的信息。因为大多数结果都是正面朝上，所以当你看到正面朝上时，你根本不会感到惊讶。假设我们掷硬币 20 次，并得到如下结果：

HH HT HH HH HH TH HH HH HH HH

其中「H」代表硬币正面朝上，「T」代表硬币背面朝上。那么我们就可以使用二进制数 0 和 1 对这个结果序列进行编码，如下所示：

其使用 20 个比特对结果进行编码，而且是一种直接编码方式，用 1 表示 H，0 表示 T。但是，由于出现背面朝上的可能性要比出现正面朝上的可能性小得多，所以香农注意到，通过使用较少的直接编码，就可以用不到 20 个比特编码这个序列。例如，假设我们将掷硬币的结果进行成对编组，如上面的序列所示，并根据下表对结果进行编码：

换句话说，当我们在一个序列中连续得到两次正面朝上时，我们将用一个比特 0 来表示，而不是两个比特 11。如果我们得到的结果是 TT，那么我们就用连续的三个 1 来表示，即 111。这些编码是经过精心挑选的，以便任何比特序列都能被明确地解码成掷硬币的序列。例如，010 代表 HHTH 四个结果。

由此，之前掷硬币的编码序列现在可以表示为如下形式：

更可能经常出现的「HH」对只需要一个比特就能够编码，而那些不太可能出现的序列则需要更多的比特来编码。这种编码只需要 13 个比特，而不是直接编码所需的 20 个比特。香农注意到这一现象，如果硬币正面朝上的可能性比背面朝上大得多，那么在大多数情况下，这种替代编码比直接编码所需的比特会更少。因此，香农观察到，掷 20 次非均匀硬币的信息量通常小于 20 个比特。

香农还注意到，普通的英文文本也可以被更为有效地编码。因为一系列字母和空格中存在大量的冗余信息。如果我发一条「i lv u」的英文短信给你，我相信你会理解的。

请注意，在第二次世界大战期间，香农致力于制定保密通信的编码方案，包括罗斯福和丘吉尔在跨大西洋会议上使用的编码。毫无疑问，他的密码学工作为信息论奠定了基础。因为它让香农明白，一个信息可以用多种方式编码，其中有些方法一定会使用更有效的编码（也就是使用更少的比特），而如果你不知道编码的规则，那么有些方法会很难读懂。如果你不懂前面表格中给出的编码规则，那么序列 0110000100000 就很难解释为 HHHTHHHHHHTHHHHHHHHH。对于我们大多数人来说，即使我们知道这样的编码规则，也很难理解一长串序列代码所表达的意思。毕竟不像「i lv u」这样的英文信息，它不需要显式的编码规则列表。

然而，我们所采用的编码可能并不总是有效的。例如，假设我们得到了一组 20 个背面全部朝上的序列，那么，采用之前的编码方案将需要 30 比特，而不是直接编码时所需的 20 比特，因为每个 TT 对将由 111 这三个比特进行编码。当然，出现这种情况的可能性比较小，但仍然是有可能的。我将在第 11 章讨论概率的问题。利用概率，我们就可以估计出这种情况会有多么不可能。如果掷硬币的结果都是独立的（这些结果互不影响），并且平均每掷 10 次就有 1 次背面朝上，那么连续出现 20 次背面朝上的概率是 10-20

。在第 11 章，我将继续讨论这到底意味着什么。然而，对于这个例子来说，它只是意味着，如果你重复掷 20 枚硬币 1020 次（100 乘以百万的三次方，即 1 亿兆次或 1 垓次）的实验，那么平均来说，你可以预期连续出现一组 20 个背面朝上。这样的结果确实非常罕见。事实上，我们也可以用概率来证明，大多数结果需要的比特数都小于 20。当然，我不会把你带入一场技术呆子的头脑风暴。

基于哈特利（1928）早期的工作，香农利用这一观察得出一个通过观察掷一次硬币所传递的信息量的量化度量方法。根据香农的说法，如果这枚非均匀的硬币正面朝上，那么当我们观察到这个事实时，我们得到了 - log 2 (0.9)≈0.15 比特的信息。这里，0.9 是硬币正面朝上的概率，表示每掷 10 次平均就会有 9 次正面朝上。因为正面朝上的可能性远远大于背面朝上，所以我们可以用这一点衡量我们的惊讶程度，或者我们学到的东西，或者简单地说，就是我们获得的信息。当我们看到正面朝上时，我们得到 0.15 比特的信息，远远少于 1 比特。但是，我们并不感到惊讶。我们在观察背面朝上的结果时得到的信息是 - log2 (0.1)≈3.32 比特，其中 0.1 是硬币背面朝上的概率。当我们看到背面朝上时，我们会更加惊讶。因此，看到硬币背面朝上所传递的信息是 3.32 比特，比看到正面朝上时的 0.15 比特信息要更多。

相反，如果硬币是均匀的，那么 T（背面朝上）的概率会是 0.5。这意味着，平均来说，掷硬币的所有结果中会有一半是背面朝上。此时，观察 T 的香农信息是 - log2 (0.5)=1 比特的信息。因此，对于一枚均匀的硬币而言，每次掷硬币都能给我们 1 比特的信息。这比看到非均匀硬币的结果 H 更令人惊讶，而比看到其出现结果 T 更不令人惊讶。

那为什么要用对数来表示呢？这看起来似乎有些随意，就好像是从帽子里拽出的一只兔子。但是，对数有一个很好的性质，对于任意两个数字 a 和 b 来说，log2(ab)=log2(a)+ log2(b)。对数的这个性质可以把乘法变成加法。假设掷硬币的一个结果对是 TH，即先是背面朝上，再是正面朝上。这样的结果中包含了多少信息呢？一起来看一下，我们从 T 的结果中得到 3.32 比特，从 H 的结果中得到 0.15 比特，所以这个结果对大概传递了两者之和或者 3.47 比特的信息。当你收到一系列不相关的消息时，其所传递的信息是每条消息的和（我们假设每次掷硬币对下一次掷硬币的结果没有影响）。

假设我们同时掷两枚硬币，观察到的结果是 TH。那其中的信息量是多少呢？要应用香农的理论，我们就需要确定 TH 的概率。如果掷硬币是独立的（一个不影响另一个），则 TH 的概率是 T 的概率和 H 的概率的乘积，或者 0.1×0.9=0.09。这个概率略小于 0.1，表明每掷两枚硬币 10 次，我们看到的 TH 的次数略小于 1。由此，通过观察 TH 所传递的香农信息就为 - log2 (0.09)≈3.47。由于对数可以将乘积转化为和，这就等于每次掷硬币得到的信息之和，即 - log2 (0.1×0.9)=-log2 (0.1)-log 2 (0.9)。这就是香农使用对数的原因。它使同时掷两枚相同硬币的信息量与连续两次掷同一枚硬币的信息量相同。

香农使用了以 2 为基数的对数，这样一来信息度量就会以比特为单位。如果你使用的是自然对数，那么信息度量的单位是「纳特（nat）」。如果你以 10 作为基数，那么信息度量就以十进制数为单位。然而，在所有的情况下，这都是在度量信息。

你可能会问，为什么到处都是这个讨厌的负号呢？有两个原因可以解释这个问题。第一个原因在于，概率总是小于 1，小于 1 的对数都是负数。我们总是倾向于用一个正数来量化信息，而在一个负数前边加上负号可以得到一个正数。第二个也是更为重要的原因是，随着事件越来越少，信息量应该增加。如果没有前边的负号，信息量就会减少，而信息和稀缺性之间的关系会发生退化。

如果平均每掷 10 次硬币就会有 1 次背面朝上，那么香农认为，每次掷硬币的平均信息量是如下数值：

-0.9log2(0.9) - 0.1log2(0.1) ≈ 0.47（比特）（64）

方程（64）就是这两个信息量的平均值，是它们概率的加权值，因此，它就是投掷一次硬币的平均信息。这意味着，每掷一次硬币平均传递的信息是 0.47 比特，而不是 1 比特。因此，从理论上讲，我们能够提出一种编码，它将代表掷硬币 20 次且其平均只有 20×0.47=9.38 比特的信息。香农证明，事实上，我们不能做得更好了，所以每掷 20 次硬币，其信息的极限是 9.38 比特。一般来说，没有比这更好的编码方案了，所以掷 20 次非均匀硬币的平均信息量是 9.38 比特。

方程（64）代表了香农在掷硬币时所说的「熵」。香农之所以选择「熵」这个术语，是因为其公式的数学结构类似于先前在热力学中被用于「熵」这一概念的公式。在一篇关于香农的简介中，霍根写道：

伟大的数学家和计算机理论家约翰·冯·诺依曼说服香农使用「熵」这个词。冯·诺依曼认为，没有人知道熵到底是什么，这一事实将使香农在信息论的争论中获得优势。（霍根，1992）

热力学从微观性质（尤其是运动中的分子）的角度研究物质（尤其是气体）的宏观性质。1870 年，奥地利物理学家路德维希·玻尔兹曼、苏格兰物理学家的詹姆斯·克拉克·麦克斯韦以及美国物理学家约西亚·威拉德·吉布斯共同提出了「熵」的概念。熵是热力学第二定律中的核心概念。该定律断言，宇宙（或宇宙中任何孤立系统）的熵都趋于增加。对玻尔兹曼、麦克斯韦和吉布斯来说，熵是一种对物理系统中随机性或无序性的度量。物理系统不可避免地趋向于更大的随机性，这样一来，最终所有的结果都是均等的。

具体而言，玻尔兹曼和他的同辈学者将宏观系统（例如气体的体积）中的随机程度（熵）建模为如下的公式：

S=klog(M)（32）

公式中，M 是微观系统（气体分子的集合）的可能状态数，其与观察到的宏观系统属性（如气体的温度和压力）一致。常数 k 是一个比例常数，被称为玻尔兹曼常数。如果 M

种状态中每一个的可能性都是相同的，那么每种状态的概率就都是 1/M，此时公式可以变成 - klog（1/M），和香农的熵相似。

玻尔兹曼的熵和香农的熵至少有两个显著的区别。一个是常数系数 k

，它简单地改变了我们表示熵的单位。香农使用比特作为单位，而玻尔兹曼使用焦耳 / 开尔文（能量 / 温度）。因为温度实际上是能量，玻尔兹曼的熵是无量纲的。无量纲的量通常不能用于度量物理世界中的某些事物，但它们在进行比较时是有用的。玻尔兹曼的熵让我们可以比较两种情况下的熵，而热力学的第二定律就是在比较熵，某一时刻的熵大于前一时刻的熵。这一定律对实际的数字没有什么意义，只对它们的相对大小有意义。其中有一个例外，当熵为零时，就会有一个明显的物理意义。要使熵为零，我们需要令 M

=1，这意味着只有一个可能的状态。对于理想气体而言，这恰恰发生在绝对零度的温度下，大约是 - 460 ℉或 - 273℃，此时所有的运动都会停止。

玻尔兹曼熵和香农熵的第二个区别在于「可能的状态数」这一概念。在香农的模型中，这个概念被定义得很好，因为可能的状态数这一概念是模型的一部分。在考虑掷硬币的时候，香农并没有考虑硬币垂直落到淤泥里的情况，也就是既非正面又非背面的可能性。相反，「掷硬币」只是对一种模型的物理隐喻，这种模型有两种可能的结果。我会在第 11 章更深入地探讨这些结果的概率概念。概率这个概念也是模型的一部分，因此也得到了很好的定义。

然而，在玻尔兹曼的例子中，物理气体的「可能状态数」是多少？在绝对零度的状态下，这可以被很好地界定，但在可达到的温度下则很难被确定。玻尔兹曼假设气体中的每个分子都有一个物理位置和速度，分子的状态可由这些数字反映出来。那么，分子的物理位置和速度有多少可能的值呢？在玻尔兹曼时代，物理学还不能把这些数字的可能性的数量限定为一个有限的集合。量子力学的最新发展改变了这种情况。至少对一个有明显边界的封闭系统，量子力学确实能产生有限数量的状态。但是，除了这些最小系统，所有系统的状态数都是巨大的。此外，精确地定义这些边界条件是不可靠的，且具有混淆地图与地域的风险。尽管有如此多的微妙之处，许多人还是把玻尔兹曼熵和香农熵紧密地联系在一起，并得出世界是数字化的这一结论。我将在下一章讨论这个问题。

但是，我们确实应该坚持香农自包含且定义良好的熵的概念，这一概念完全存在于模型世界之中，是衡量系统中不确定性、随机性或无序性的好方法。如果硬币是均匀的（出现正面和背面的可能性相等），那么熵是 1 比特，所以平均来说，没有任何编码方案能比直接编码的方案更好。这表示了掷硬币系统可能具有的最高程度的不确定性、随机性或无序性。在另一个极端中，如果硬币是非均匀的，你得到的结果永远只是正面朝上，那么熵是零。由此，通过观察掷硬币的过程根本无法传递任何信息。结果具有很高的确定性，而没有随机性，换言之，这个掷硬币系统是理想有序的。这样的掷硬币结果完全可以不使用比特进行编码，因为我们已经知道结果了。

香农对信息量的量化以及选择用比特来表达这种量化，对通信理论、计算机科学乃至哲学都产生了巨大的影响。但是，人们很容易忘记，我在这里描述的理论更适用于那些具有有限且明确可选选项的情形。如果可选选项提供了无限的可能性，那么会发生什么？例如，如果玻尔兹曼气体中每个分子的位置可以是出现在一定空间中的任意点，情况会怎样呢？这组可选选项的数量不是有限的。所以，当我们直接将香农熵用于那些可能的结果为连续范围的情形时，我们必须更加谨慎地加以解释。我会在下一节的讨论中这样做。

在这里，我想先表示一下我的歉意，因为下一节的内容会涉及不少技术性问题。如果你想跳过这些内容直接到下一章，那么我在这里简要地说明一下，信息并非总能表示为二进制的数据。因此，有一种信息的概念是计算机无法触及的。

### 7.4 Continuous Information

Equation (64) gives the entropy of a random experiment (an unfair coin toss) that has exactly two possible outcomes, one with probability 0.1 and one with probability 0.9. Shannon showed that this entropy can be interpreted as the minimum number of bits required to encode an outcome of the experiment, on average. Equation (64) states that roughly half a bit (0.47 bits) is required to encode each outcome of the unfair coin toss. Equivalently, on average, each bit in a sequence of bits can encode the results of roughly two coin tosses. This requires clever encoding of a sequence of outcomes of the experiment, but with such encoding, it quantifies the amount of information gleaned from observing each coin toss, about half a bit, on average.

A fair coin, in contrast, has an entropy with value 1, so on average one bit is needed to encode each outcome. In this case, no clever coding is needed because we can just encode heads with 1 and tails with 0. Every coin toss yields one bit of information.

Formula (64) is a sum of two quantities, each of the form − p log 2 ( p ), where p is the probability of one of the two outcomes, and the negative of the logarithm quantifies the amount of information in that outcome. The more rare the outcome, the more information it carries. It is easy to generalize this idea to a random experiment with more than two possible outcomes, such as the toss of a pair of dice. The sum in (64) will simply have one term of the form − p log 2 ( p ) for each possible outcome with probability p.

But what if we have a random experiment that can have an infinite number of possible outcomes? Suppose, for example, that some variable is equally likely to have any real-numbered value between − a and a for some positive real number a . What is the entropy of this random experiment, and how many bits are required to encode an outcome?

The formula for entropy is easy to adapt, where the summation of terms of the form − p log 2 ( p ) in equation (64) is replaced with an integration over a continuous range of possible values. Specifically, the entropy of a continuous random experiment is given by the formula

H ( X ) represents the entropy of a random experiment that we name X . Bear with me.

The form of equation (16) is similar to equation (64). An integral, after all, is just a sum over a continuum of an infinite number of values (I will return to the idea of a continuum in chapter 9 ). The integration is a sum over the set Ω of all possible values x that the experiment might yield. Each term being summed by the integral has a form similar to that of the terms in equation (64), − p log 2 ( p ), except that probabilities p have been replaced with probability densities f ( x ). The term f ( x ) is the probability density at x , where x is one of the possible outcomes of the experiment. A probability density, just like a probability, reveals the relative likelihood that the experiment will yield certain outcomes. I will talk about probability densities more carefully in chapter 11 , but loosely, if for two possible outcomes x and y we have that f ( x ) > f ( y ), then the experiment is more likely to yield an outcome in the vicinity of x than in the vicinity of y . The phrase「in the vicinity」reflects that this is a probability density not a probability.

The continuous entropy of equation (16), like the discrete entropy of equation (64), represents the average amount of information obtained by observing outcomes of the experiment. Like discrete entropy, outcomes that are more rare (values of x where f ( x ) is lower) carry more information than values that are more likely. It is no longer correct, however, to interpret this entropy as specifying the average number of bits required to encode an outcome of the experiment. In fact, every outcome will require an infinite number of bits to encode. An outcome of a continuous random value is not representable exactly with binary numbers, unlike a discrete random value.

Consider a simple example, a random experiment that can yield any real number between − a and a . Assume that every value in that range is equally likely. For this experiment, the probability density f is plotted in figure 7.1 for the particular case where a = 4. The plot shows that outside the range between − a and a , f ( x ) = 0, indicating that those values have zero probability, whereas inside that range, f ( x ) = 1 / 8, indicating that all values inside the range are equally likely.

The probability density function indicates the relative likelihoods of outcomes of the experiment. An area under the plot, like the shaded area in the figure, indicates the probability that the experiment will yield an outcome inside a range. The area of the shaded rectangle in the figure is 1 × 1 / 8 = 1 / 8, which indicates that the probability of an outcome between 1 and 2 is one eighth. This indicates that one in eight outcomes will lie in this range.

The total area under the plot for any probability density f is required to add up to one because that total area indicates the probability of any outcome, and the experiment must yield some outcome. In the figure, the total area under the plot for f is a rectangle with width 8 and height 1 / 8, so as required, the area under f is 8 × 1 / 8 = 1.

For the probability density function of figure 7.1 , the entropy H ( X ) in equation (16) is easy to calculate. An integral is just finding the area under a curve, and the「curve」in this case is not curvy. It is a rectangle. Without boring you with the details,

Figure 7.1 Probability density function for a uniform continuous random experiment.

with the uniform probability density of figure 7.1 , the entropy becomes

If we were to erroneously interpret this as the number of bits required to encode an outcome of X , then we would conclude that three bits are sufficient. But this should worry us. How could three bits distinguish between an infinite number of possible outcomes?

A discrete entropy as in equation (64) is always zero or positive. It cannot be negative. A probability p is always between zero and one, and the logarithm of a number between zero and one is always negative, so − p log 2 ( p ) is always nonnegative. A sum of nonnegative numbers is always nonnegative.

For the continuous random experiment, the situation is a bit different. The entropy H ( X ) can be positive or negative. Suppose, for example, that X has a probability density function similar to figure 7.1 , but instead of a = 4, it has a = 1 / 4. Then when x is in the range −1 / 4 to 1 / 4, the density must be f ( x ) = 2. It has to be 2 because the total area under f must be 1. But now you can verify from equation (8) that H ( X ) = − log 2 (2) = −1. The entropy is negative! This further underscores that continuous entropy does not represent the number of bits required to encode an outcome. How could we encode the outcome of an experiment using a negative number of bits?

When a continuous entropy is negative, this should not be interpreted as meaning that negative information is conveyed by an observation of the experiment. In fact, infinite information (in bits) is conveyed. It should instead be interpreted to mean that an experiment with negative entropy conveys less information than one with positive entropy. Indeed, when a = 4, there are more possible values for x than when a = 1 / 4, so a (perfect) observation in the first scenario conveys more information than a (perfect) observation in the second. But neither bundle of information can be encoded using bits.

There is an interesting special case when an experiment has only one possible outcome, for example, a coin toss that always yields heads because both sides of the coin are heads. In the discrete case, the entropy is zero. The sum in equation (64) will have only one term, − p log 2 ( p ), where p = 1. But the logarithm of 1 is 0, so an experiment with only one possible outcome has entropy equal to zero. It requires zero bits to encode because we already know the answer. This makes sense.

What if we have a continuous experiment where there happens to be only exactly one possible outcome? In other words, the experiment is not actually random, like our coin with two heads. Suppose, for example, we have a continuous experiment that happens to always yield x = 0. To model this, we can use the probability density function of figure 7.1 and let a become arbitrarily close to zero. As a gets small, the height 1 / 2 a of f ( x ) in the range − a to a gets large to ensure that the area under f remains 1. As a approaches zero, f ( x ) approaches infinity for − a ≤ x ≤ a . As a consequence, as a approaches zero, H ( X ) = − log 2 (1 / 2 a ) approaches minus infinity.

So for a continuous random experiment, an entropy of minus infinity indicates that no information is conveyed by a measurement. This is different from a discrete random experiment, where an entropy of zero indicates that no information is conveyed. The difference between zero and minus infinity is huge so confusing the two forms of entropy will yield drastically erroneous conclusions. If we insist on trying to compare these two forms of entropy, then we need to acknowledge that there is an infinite offset between them. It takes infinitely more bits to encode the continuous outcome than the discrete one.

What does it mean when the continuous entropy is zero? Not much. It just means that there is more information than if the entropy had been negative and less information than if the entropy had been positive. You can verify that if a = 1 / 2 in figure 7.1 , then H ( X ) = 0.

Why does each outcome of the continuous experiment require an infinite number of bits to encode? I will fully address this subtle question in the next chapter. The short answer is that there are vastly more possible outcomes than there are finite bit sequences. There are just not enough finite bit sequences to assign a unique bit sequence to each possible outcome. This will become clear in the next chapter, but for now I ask you to take my word for it so that I can explain a truly remarkable insight, due to Shannon.

In the same 1948 paper, Shannon observed the rather obvious fact that any noisy observation of an experiment yields less information than a perfect observation.「Noise」is a term that engineers use for extraneous factors that creep into measurements so that the measurements are imperfect. Noise is unavoidable in any measurement of the physical world.

But Shannon's truly remarkable observation was that a noisy observation of a continuous-valued experiment yields much less information, and that the information it yields can be represented with a finite number of bits. Although outcomes of the experiment contain information that requires an infinite number of bits to represent, any noisy observation only reveals a finite number of bits. Thus, all measurements of the physical world can be encoded with binary digits, assuming all measurements are noisy.

But this does not imply that the physical world can be encoded with binary digits. That would be confusing the map for the territory. It may be true that a physical system can be encoded with bits, although I personally doubt it (see section 8.4 on digital physics in the next chapter), but it is not finite entropy that makes it true. Continuous entropy is finite even though its continuous variable cannot be encoded with a finite number of bits.

Shannon's result that a noisy measurement reveals a finite number of bits of information is known as the「channel capacity theorem.」Shannon was considering communication problems, where a quantity known at one point in space is to be conveyed via an imperfect communication channel to another point in space. One of his central results is that any channel that adds noise can only convey a finite amount of information, measured in bits, for each observation of the output of the channel. The output of the channel is a noisy observation of the input to the channel. [3]

So how much information is conveyed by a noisy measurement? Consider the experiment X with probability density function as shown in figure 7.1 and entropy H ( X ) as given in equation (16). Let Y represent a noisy measurement of X . Let x represent a particular outcome of experiment X and y represent a particular measurement of that outcome. Because the measurement is noisy, it is likely that y is close to x but not exactly equal to x . The measurement y tells us something about an outcome x but not everything. So how much does it tell us?

If we have a model for the measurement noise, then given some specific measurement y , we can come up with a probability density function that represents the relative likelihoods of values x that could have yielded the measurement y . This new probability density is called a「conditional probability density」because it is a valid probability density for x only once we have a measurement y .

Suppose we know that our measurement apparatus adds noise no bigger than 1 / 2. This means that given a measurement y , it must be true that x is within the range y − 1 / 2 to y + 1 / 2. Suppose further that we have the measurement y = 1.5 right in the middle of the grey region in figure 7.1 . We can conclude that the actual value of x is equally likely to be anywhere in the grey region, in the range from 1 to 2. It cannot be anywhere else because the measurement apparatus does not add noise larger than 1 / 2.

Armed with this knowledge, once we observe y = 1.5, the actual value of x is still random (it is not known), but now it is equally likely to be anywhere in the grey region. We have gained information because without the measurement, it was equally likely to be anywhere from −4 to 4. Now we know that it is equally likely to be in the range from 1 to 2. We have significantly narrowed the range.

How much information have we gained? Intuitively, the grey region is one eighth of the total possible region for x . Hence, our measurement tells us that the actual value for x is in one of eight possible equally sized regions. We can distinguish eight regions using three bits because three bits have eight distinguishable patterns: 000, 001, 010, 011, 100, 101, 110, and 111. So it seems we have gained three bits of information. Shannon shows us that we actually gain slightly more than three bits of information, on average, because measurements that are close to the edge of the region, near −4 or 4, will yield more information than measurements in the middle of the region under this noise model. For example, if our measurement happens to be y = 4.5, then the only possible value for x is 4, so with this (extremely unlikely) measurement, we have gained a huge amount of information. We have achieved certainty.

How did Shannon determine the information conveyed by a noisy measurement? Once a measurement is taken, we have a new conditional probability density function for X . Figure 7.2 shows the conditional probability density given a measurement y = 1.5 and noise limited to ±1 / 2. We can use that new density in equation (16) to calculate the entropy. Let's call this entropy H ( X | Y ), which we read as「the entropy remaining in X given a measurement Y .」Shannon's channel capacity theorem then tells us that the information yielded by a measurement is, on average,

H ( X ) is the information we would gain with a perfect observation, and H ( X | Y ) is the information that is not revealed by the experiment. In other words, H ( X | Y ) is the remaining randomness after the measurement. The truly astonishing thing about this theorem is that for a wide range of models of measurement noise, the difference H ( X ) − H ( X | Y ) represents information that can be encoded with a finite number of bits, even if the original outcome x of experiment X cannot be encoded with a finite number of bits. The information revealed by the experiment, in bits, is finite, although the information in the actual system, in bits, is infinite. In forming the difference H ( X ) − H ( X | Y ), both quantities have an infinite offset compared with discrete entropy, but the offsets cancel, and the difference becomes a discrete entropy. This insight is truly remarkable.

For our particular example, where a = 4, we have determined that H ( X ) = 3. Calculating H ( X | Y ) precisely is a bit tedious, so I will spare you the details, but our intuition holds up, and H ( X | Y ) turns out to be slightly less than 0. Hence, C in equation (4) turns out to be slightly larger than 3, indicating that our measurement reveals slightly more than 3 bits of information on average.

It is now worth considering some special cases. Suppose the measurement is perfect. In this case, H ( X | Y ) is minus infinity because once a measurement is taken, there is no remaining randomness in X . Hence, C is infinite regardless of the value of H ( X ) (as long as H ( X ) is not also minus infinity). As a consequence, a perfect observation of a continuous random experiment yields an infinite number of bits of information .

Figure 7.2 Conditional probability density function (dashed line) given a measurement y = 1.5.

Suppose that our experimental apparatus is hopeless, and a measurement yields no information about X . In this case, H ( X | Y ) = H ( X ) because the randomness after observation is the same as before. Hence, C = 0. A hopelessly bad measurement yields zero bits of information about X .

It is also easy to see that H ( X ) − H ( X | Y ) cannot be negative because the randomness (the uncertainty) H ( X | Y ) after measurement cannot be more than the randomness (uncertainty) H ( X ) before measurement. Hence, making a measurement never reveals a negative number of bits of information.

In short, an outcome of a continuous random experiment has information, but that information cannot be encoded in a finite number of bits. A noisy observation of the outcome of continuous random experiment, however, can be encoded with a finite number of bits. That number is given by the Shannon channel capacity theorem, equation (4). So the question arises whether the physical world presents scenarios where variables can have values in a continuous range. There is real risk here of confusing the map and the territory, so I defer this question to a more careful analysis in the next chapter.

As I argued in chapter 2 , in an engineering use of models, we seek physical realizations that match a model. Models that represent information digitally are extremely useful, and thanks to the digital technology outlined in chapters 4 and 5 , we know how to make physical systems that are faithful to this digital representation of information. In the scientific use of models, in contrast, we seek models that match the physical world. In this use, the assumption that all information is digital and can be represented in bits is questionable (see section 8.4 in the next chapter). This assumption is demonstrably untrue if continuous quantities exist in nature.

In chapter 11 , I will examine the meaning of probability, which underlies Shannon's notion of information. Fundamentally, probability is a measure of uncertainty, the lack of information. The entropy in a system quantifies exactly how much information we lack about the system. Put another way, entropy quantifies how much information can potentially be gained by observing the system. But there are two distinct and incomparable measures, discrete and continuous entropy. Only discrete entropy measures information in bits.

In the next chapter, we will look at machines whose sole purpose is to process digital information. I will argue that even if we restrict our attention to the digital world, leaving out my dishwasher, software is still limited. It cannot perform most information-processing functions.

[3] Any text on digital communication will cover this topic of channel capacity, including one that I coauthored (Barry et al., 2004, p. 123).

7.4 连续信息

方程（64）给出了一次随机实验（非均匀硬币的一次投掷）所产生的熵，它有两种可能的结果：一种的概率是 0.1，另一种的概率是 0.9。香农证明，这个熵可以被理解为对实验结果进行编码所需的最小比特数。方程（64）表明，对每次投掷非均匀硬币所产生结果的编码大约需要半个比特（0.47 比特）。同样，平均而言，一个比特序列中的每个比特都可以编码大约两次掷硬币所产生的结果。当然，这需要对该试验的结果序列进行合理的编码，但是如果我们进行了这样的编码，就量化了从观察每一次掷硬币所收集到的信息量，平均约为 0.5 比特。

相较而言，一枚均匀硬币的熵值为 1，因此，每个结果平均需要 1 个比特来进行编码。在这种情况下，就不需要复杂的编码，因为我们可以将正面朝上的情况编码为 1，背面朝上的情况编码为 0。每次掷硬币都会产生 1 比特的信息。

方程（64）是两个量的总和，每一个的形式都是 - p

log2(p

)，其中 p

是两种结果之一的概率，而对数的负数量化了该结果中的信息量。结果越是罕见，其携带的信息越多。这一想法很容易被推广到具有两个以上可能结果的随机实验中，例如掷一对骰子。对于每一个概率为 p

的可能结果，方程（64）中的和将只相应地包含一个形式为 - p

log2(p

) 的项。

但是，如果我们拥有的是一个有着无数可能结果的随机实验呢？例如，假设 a 是某个正实数，且某个变量在 - a

和 a

之间等可能地取任何实数值，那么这个随机实验的熵是多少？编码一个结构又需要多少比特？

熵的公式很容易被改造，方程（64）中形式为 - p

log2(p

) 的项的和被替换为一个连续的可能值范围上的积分。具体而言，连续随机实验的熵可由下式计算：

其中，H

(X

) 表示名为 X

的随机实验的熵。请你耐心读如下解释。

方程（16）的形式与方程（64）的类似。毕竟，积分只是一个对无限多个值的连续统的求和（我将在第 9 章回到连续统的概念）。该积分对实验可能产生的所有可能值 x

的集合 Ω 求和。用积分求和的每个项的形式与方程（64）中的项相似，即 - p

log2(p

)，只是概率 p

已被概率密度 f

(x

) 取代。f

(x

) 是在 x

处的概率密度，x

是实验的可能结果之一。概率密度，就像概率一样，揭示了实验将产生某些结果的相对可能性。我将在第 11 章更详细地讨论概率密度问题。简要地讲，如果对于 x

和 y

两种可能的结果，我们有 f

(x

)>f

(y

)，那么实验更有可能在 x

附近产生结果，而不是在 y

附近。「在附近」这个短语反映了这是一个概率密度，而不是一个概率。

方程（16）的连续熵与方程（64）的离散熵一样，表示通过观测实验结果所获得的平均信息量。与离散熵一样，比较少见的结果［f

(x

) 较小的 x

取值］比更有可能出现的结果携带更多的信息。然而，将这个熵解释为对实验结果进行编码所需的平均比特数已不再合适。事实上，每个结果都需要无限多的比特来编码。与离散随机值不同，连续随机值的结果并不能用二进制数精确表示。

我们来看一个简单的例子。一个随机实验，可以产生 - a

和 a

之间的任意实数。假设在这个范围内，每个值的可能性都是相等的。在这个实验中，对于 a

=4 的特定情形，图 7.1 给出了其概率密度 f

。由图可知，在 - a

到 a

的范围之外，f

(x

)=0，表示这些值的概率为零。

然而，在该范围之内，f

(x

)=1/8，表明所有值出现的可能性都是相同的。

概率密度函数表示实验结果的相对概率。该图下面的区域，例如图中的阴影区域，表示实验在一定范围内产生结果的概率。图中矩形阴影的面积为 1×1/8=1/8，表明一个结果位于 1 和 2 之间的概率为 1/8。这也表明，1/8 的结果将处于这一范围。

对于任何概率密度 f

，图下方的面积总和必须为 1，因为这个总面积表示任何结果的概率，而且，实验必定会产生某个结果。在图中，f

的图下总面积是一个宽度为 8、高度为 1/8 的矩形，因此，按照如上要求，f

以下的面积为 8×1/8=1。

图 7.1 均匀连续随机实验的概率密度函数。

对于图 7.1 中的概率密度函数，方程（16）中的熵 H

(X

) 很容易被计算出来。积分只是求曲线下的面积，这里，「曲线」并不是曲线，而是一个矩形。好了，我不会在此过多地解释细节。就图 7.1 的均匀概率密度而言，此时的熵可由下式来计算：

H(X)

=- log2(1/2a

)=log2(2a

)=3（8）

如果我们错误地将其解释为编码一个 X

的结果所需的比特数，那么我们会得出 3 个比特就已足够的结论。但是，这会让我们产生疑问。3 个比特如何区分无限多的可能结果？

方程（64）中的离散熵总是为零或正数，而不可能是负数。概率 p

总是在 0 到 1 之间，而 0 到 1 之间的数的对数总是负的，所以 - p

log2(p

) 总是非负的。非负数之和总是非负的。

对于连续随机实验，情况有些不同。熵 H

(X

) 可以为正，也可以为负。例如，假设 X

有一个类似于图 7.1 的概率密度函数，但 a

不是 4，而是 1/4。那么当 x

在 - 1/4 到 1/4 的范围时，其概率密度必须是 f

(x

)=2。它必须等于 2，因为 f

下面的总面积必须是 1。但是现在你可以从方程（8）中验证 H

(X

)=-log2 (2)=-1。熵是负的！这进一步强调了连续熵并不代表编码一个结果所需的比特数。我们如何用负的比特数来编码一个实验的结果？

当连续熵为负时，不应将其理解为通过一个实验的观测结果传递了负信息。事实上，是传递了无限信息（以比特为单位）。相反，应该将其解释为负熵实验比正熵实验传递的信息更少。实际上，当 a

=4 时，x

的可能取值要比 a

=1/4 时更多，因此第一种情形中的（理想的）观测结果比第二种情形中的（理想的）观测结果传递的信息更多。但这两组信息都不能用比特进行编码。

有一个有趣的特殊情况，即一个实验只有一种可能的结果，例如，一个硬币的两面都有头像时，掷这个硬币后总会是正面朝上。在离散式的随机情况下，其熵为零。方程（64）中的和只包含一个求和项，即 - p

log2(p

)，其中 p

=1。但是 1 的对数是 0，所以只有一种可能结果的实验的熵等于零。对它的编码需要零比特，因为我们已经知道结果了。这是很有意义的。

如果我们有一个连续的实验且其碰巧只有一个可能的结果呢？换句话说，这个实验并不是随机的，就像硬币的两面都是头像。例如，假设我们有一个连续的实验，其结果碰巧总是 x

=0。为了对其进行建模，我们可以使用图 7.1 中的概率密度函数并令 a

无限趋近零。当 a

变小时，f

(x

) 在 - a

到 a

范围内的高度 1/2a

会变大，以确保 f

下的面积为 1。当 a

趋于 0 时，对于 - a

≤ x

≤ a

，f

(x

) 趋于无穷大。因此，当 a

趋于 0 时，H

(X

)=-log2(1/2a

) 会趋于负无穷大。

因此，对于连续随机实验，一个负无穷大的熵表示测量没有传递任何信息。这与离散随机实验的结果不同。在离散随机实验中，熵为零表示没有任何信息被传递。零和负无穷大之间的差别是巨大的，所以混淆这两种形式的熵会产生严重错误的结论。如果我们坚持比较这两种形式的熵，那么我们需要承认它们之间存在着无限的偏差。与离散结果相比，编码连续结果所需的比特要多得多。

连续熵为零是什么意思呢？它并没有太多的含义。它只是意味着，比熵为负时的信息更多，比熵为正时的信息更少。可以验证，如果图 7.1 所示的 a

=1/2，那么 H

(X

)=0。

为什么连续实验的每个结果都需要无限多的比特进行编码？我将在下一章详细讨论这个问题。在这里我先做一个简短的回答，因为可能出现的结果会比有限的比特序列多得多。因此，没有足够的有限比特序列能够为每个可能的结果分配一个唯一的比特序列。在下一章中，这个问题会变得非常清楚。但现在请你相信我所说的，以便我能继续解释一个由香农提出的很了不起的见解。

在 1948 年发表的那篇论文中，香农观察到一个相当明显的事实，即由一个实验的任何带噪声观测所产生的信息都要少于理想观测所产生的信息。「噪声」是工程师们使用的一个术语，用来指那些混入测量并使得测量结果变得不理想的外部因素。在对物理世界的任何测量中，噪声都是不可避免的。

但是，香农的观察中真正值得注意的是，对一个连续数值实验的带噪声观测所产生的信息要少得多，而且，它产生的信息可以用有限数量的比特来表示。虽然实验的结果包含了需要用无限个比特来表示的信息，但任何有噪声的观测结果都只会揭示有限的比特数。因此，假设物理世界中的所有测量都是带噪声的，那么物理世界中的所有测量值都可以用二进制数进行编码。

但是，这并不意味着物理世界可以用二进制数来编码。这样做一定会将地图与地域混为一谈。物理系统可以用比特进行编码，这可能是真的，尽管我个人对此表示怀疑（见下一章 8.4 节），但并不是有限熵使其为真。连续熵是有限的，即使它的连续变量不能用有限数量的比特进行编码。

香农的结论是，一个有噪声的测量揭示了有限数量的信息比特，这被称为「信道容量定理」。香农当时在考虑某些通信问题，其中将空间某一点上已知的量通过一个非理想信道传送到空间中的另一点。他的主要结果之一是，对于任何增加了噪声的信道，对于该信道输出的每一次观测只能传递有限数量的信息，以比特为单位。信道的输出是对信道输入的一个有噪声的测量。那么，一个有噪声的测量能传递多少信息呢？假设实验 X

，其概率密度函数如图 7.1 所示，熵 H

(X

) 如方程（16）所示。设 Y

是对 X

的有噪声测量，x

代表实验 X

的一个特定结果，y

代表对该结果的一个特定测量。因为测量是有噪声的，所以 y

很可能接近 x

，但不完全等于 x

。测量 y

告诉我们一些关于结果 x

的信息，但并不完全。那么，它告诉了我们多少信息呢？

如果我们拥有一个用于测量噪声的模型，然后给出一些具体的测量 y

，我们就可以得出一个概率密度函数，其表示产生测量 y

的一组 x

值的相对可能性。这种新的概率密度被称为「条件概率密度」，这是因为，仅当我们有一个测量 y

时，该概率密度才是 x

的有效概率密度。

假设我们知道我们的测量仪器所引入的噪声不超过 1/2。这意味着，给定一个测量 y

，x

在 y

-1/2 到 y

+1/2 的范围之内必定成立。

进一步假设我们的测量 y

=1.5，即图 7.1 灰色区域的中间位置。那么，我们可以得出结论，x

的实际值在 1 到 2 的范围内，其在灰色区域的任何地方的可能性都是相同的。它不可能在其他任何地方，因为测量仪器不会引入大于 1/2 的噪声。

基于这些知识，一旦我们观测到 y

=1.5，且 x

的实际值仍然是随机的（它是未知的），那么它现在在灰色区域任何地方出现的可能性就是相同的。我们已经得到一些信息，因为如果没有测量，它出现在 - 4 到 4 之间任何位置的可能性都是相等的。现在我们知道它在 1 到 2 之间任何位置出现的可能性也是相同的。当然，我们已经大大地缩小了范围。

那我们得到了多少信息呢？直观上，灰色区域是 x

的全部可能区域的 1/8。因此，这些测量告诉我们，x

的实际值会落入 8 个可能的等大小区域中的一个。我们可以使用 3 个比特来区分 8 个区域，因为 3 个比特共有 8 个可区分的模式：000、001、010、011、100、101、110 和 111。看来我们已经获得了 3 比特的信息。香农告诉我们，我们实际上获得了平均略多于 3 比特的信息。因为在这个噪声模型下，靠近区域边缘的测量，接近 - 4 或 4，要比区域中部的测量产生更多的信息。例如，如果我们的测量恰好是 y

=4.5，那么 x

的唯一可能值是 4，因此，通过这种（极不可能的）测量，我们已经获得了巨大的信息量。我们获得了确定性。

香农如何确定一个有噪声的测量所传递的信息呢？一旦测量完成，我们就会有一个 X

的新的条件概率密度函数。图 7.2 给出给定测量为 y

=1.5 且噪声限制为 ±1/2 的条件概率密度。我们可以用方程（16）中的新密度来计算熵。让我们把这个熵称为 H

(X

|Y

)，也就是「给定一个测量 Y

的条件下，X

中剩余的熵」。那么，香农的信道容量定理告诉我们，一次测量所得到的平均信息可由下式计算：

C=H(X)

- H(X|Y)

（4）

H

(X

) 是我们通过一次理想的测量得到的信息，而 H

( X

|Y

) 是实验未揭示的信息。换句话说，H

( X

|Y

) 是测量后剩下的随机性。关于这个定理真正令人惊讶的是，对于许多测量噪声的模型而言，差值 H

( X

) - H

( X

|Y

) 所表示的信息可以用有限的比特进行编码，即使实验 X

的原始结果 x

不能用有限的比特编码。实验所揭示的信息是用有限比特表示的，尽管实际系统中的信息需要用无限的比特来表示。在形成差值 H

( X

) - H

( X

|Y

) 时，这两个量与离散熵相比都有无限的偏移量，但是偏移量被抵消了，差值就变成了离散熵。这是一个非常了不起的见解。

对于我们给出的特定示例，其中 a

=4，我们已经确定了 H

( X

)=3。精确地计算 H

( X

|Y

) 确实有些乏味，所以我就不再赘述了，但是我们的直觉是站得住脚的，H

( X

|Y

) 的结果略小于 0。因此，方程（4）中 C

的值略大于 3，这表明我们的测量平均揭示了略多于 3 比特的信息。

现在，有必要考虑一些特殊情况。假设测量是理想的。在这种情况下，H

( X

|Y

) 是负无穷大，因为一旦进行了测量，X

中就没有剩余的随机性了。因此，无论 H

( X

) 的值是多少，C

都是无限的［只要 H

( X

) 不是负无穷大］。结果是，对一个连续的随机实验进行理想的测量会产生无限比特的信息。

图 7.2 有条件的概率密度函数（虚线），给定一个测量 y=1.5。

假设我们的实验仪器非常糟糕，而且一次测量也不会产生任何有关 X

的信息。在这种情况下，H

( X

|Y

)=H

( X

)，因为测量后的随机性与之前的相同。因此，C

=0。一个极其糟糕的测量会产生关于 X

的零比特信息。

由于测量后剩余的随机性（不确定性）H

( X

|Y

) 不可能大于测量前的随机性（不确定性）H

( X

)，我们很容易就看出 H

( X

) - H

( X

|Y

) 不可能为负。因此，进行测量永远不会得出负的信息比特数。

简而言之，一个连续随机实验的结果是有信息量的，但这些信息不能用有限数量的比特进行编码。然而，对连续随机实验结果的有噪声观测可以用有限数量的比特进行编码。香农的信道容量定理，即方程（4），给出了这个数量。由此，问题出现了，物理世界是否呈现了变量可以在一个连续的范围内取值的情形。这里确实存在混淆地图和地域的风险，所以我把这个问题推后到下一章。到时候，我会进行详细的分析。

正如我在第 2 章中论述的，在模型的工程应用中，我们寻求与模型匹配的物理实现。以数字化方式表示信息的模型是非常有用的。基于第 4 章和第 5 章中阐述的数字技术，我们知道了如何构建高度符合于这种数字化信息表示的物理系统。相比之下，在模型的科学应用中，我们寻求的是与物理世界相匹配的模型。在这种使用过程中，假定所有信息都是数字化的并且可以用比特来表示，这样的假设是有问题的（见下一章的 8.4 节）。如果自然界中存在连续的数，那么这个假设显然是不正确的。

在第 11 章，我将研究概率的意义，它是香农所指信息概念的基础。从根本上讲，概率是衡量不确定性，即信息的缺乏程度的一种度量。系统中的熵精确地量化了我们缺少多少关于系统的信息。换句话说，熵量化了通过观测系统可能潜在地获得的信息量。但是，这里存在着两种截然不同、无法比拟的度量，即离散熵和连续熵。只有离散熵可以用比特来度量信息。

在下一章中，我们将研究那些以处理数字信息为唯一目标的机器。我想说的是，即使我们把全部的焦点都限定于数字世界，不考虑我的洗碗机，软件仍然有其局限性。软件不能执行大多数的信息处理功能。

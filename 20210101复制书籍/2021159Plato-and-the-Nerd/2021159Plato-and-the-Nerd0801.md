## 0801. The Limits of Software

· · · in which I explain what software cannot do and show that the number of information-processing functions is vastly larger than the number of possible computer programs; and in which I explain the Church-Turing thesis, which shows that there are useful information-processing functions that are not realizable by software. But it does not follow that if a function is not realizable by software, then it is not realizable by any machine. Here, I am forced to confront the paradigm of「digital physics,」which argues that the physical world itself is somehow software or equivalent to software.

0801 软件的局限性

在本章，我会阐释：1）软件不能做什么，并说明信息处理功能的数量远远大于可能的计算机程序的数量；2）此外，我还解释了丘奇-图灵论题，它表明有一些有用的信息处理功能是软件无法实现的。但这并不是说，一个功能如果不能通过软件实现，它就不能由任何机器来实现。在这里，我将不得不面对「数字物理学」的范式，它认为物理世界本身在某种程度上就是软件或等价于软件。

### 8.1 Universal Machines?

Computers are information-processing machines. The previous chapter studied what information is and how to measure it. I showed that information is not necessarily representable digitally, at least in theory. In practice, the inevitability of measurement noise and the possibility that the physical world is digital may lead to the conclusion that information in the physical world can always be represented digitally. If we go a step further and assume that all transformations of information in the physical world are performed in essentially the same way as in computers, then it is impossible in principle to do more than what can be done by software. This conclusion, if it were true, would be quite remarkable because it turns out that software can do little compared with what we can imagine is possible. In this chapter, I will explain the limits of software and why I believe that we can (and do) do things that software cannot.

The set of all computer programs, each of which is a model, is actually a tiny set. The size of that set is the same as the smallest of all the infinite sets that Georg Cantor identified in the late 1800s. Cantor, a Russian-German mathematician, showed that some infinite sets are vastly larger than other infinite sets.

It is difficult to reason about size when talking about infinity. In fact, Cantor spent 12 years attempting to prove that all infinite sets have the same size (Smullyan, 1992, p. 219). He failed! In the process, he developed a remarkable insight that I will use to show how much smaller the set of all computer programs is compared with the set of functions that we might be interested in implementing on computers. Consequently, although we can do an extraordinary amount with software, it's nothing compared with what is possible if we do not limit ourselves to this smallest of infinite sets.

There is, however, a potential caveat that I am forced to confront. Since the development of information theory and the theory of computing, a branch of thought has emerged that some people call「digital physics.」Digital physics postulates that nature does not and cannot have a continuous range of possibilities. Some of the stronger forms of digital physics postulate that going beyond what software can do in principle is physically impossible. In practice, however, going beyond what software can do is clearly possible today and in the foreseeable future. Software cannot realize my dishwasher, for example. Nevertheless, I will conclude the chapter with a discussion of digital physics.

For now, let's put aside the question of whether the physical world is digital and just consider information-processing functions where the inputs are binary numbers and the outputs are binary numbers. In fact, let's consider an even smaller set of functions, those whose input is a finite binary number and whose output is just a single zero or one rather than a sequence of zeros and ones. Such functions are called「decision functions」because for each particular input, say 010101, the function will say either YES (1) or NO (0). The function makes a decision.

In the 1930s, the young English computer scientist Alan Turing defined the set of「effectively computable」functions to be those decision functions that can be computed algorithmically (in a step-by-step fashion) using a machine that is now called a Turing machine. [1] In principle, a Turing machine is realizable by a modern computer that has a sufficient amount of memory. Independently of Turing, in 1936, Alonzo Church, an American mathematician, came up with a different model than the Turing machine that yields exactly the same set of effectively computable functions. The fact that two different models result in the same set of effectively computable functions suggests that there is something special about this particular set of functions.

There are many possible Turing machines, each of which may compute a different decision function. In Turing's formulation, each such machine can be encoded by a finite sequence of bits, much the way machine code encodes a computer program as a finite sequence of bits (see chapter 5 ). For example, the sequence 000111 might represent a Turing machine that computes a particular decision function. Turing showed that there is a「universal Turing machine,」a Turing machine that can implement any other Turing machine. For example, if 000111 encodes a Turing machine, and we would like to know what decision that machine makes for the input 010101, then we can concatenate the bits specifying the machine code and the input to get 000111010101. Providing that combined bit pattern as the input to a universal Turing machine yields the answer that the machine 000111 would have given. So the bit pattern 000111 encodes the program, and the universal Turing machine is the computer that executes the program. So a「universal」Turing machine is simply a programmable Turing machine where the program can encode any other Turing machine.

The effectively computable functions constitute the set of decision functions that can be realized by a universal Turing machine. What is now called the Church-Turing thesis states that any function that a human can compute using a systematic, step-by-step process, given enough pencil and paper and enough time, is one of the effectively computable functions.

Given enough memory and time, any modern computer can also compute any effectively computable function. So any modern computer is a universal Turing machine, except that it may run out of memory. But memory has become so cheap and plentiful that this caveat carries little weight.

The question remains whether a modern computer can do more than compute effectively computable functions. Many people, including Rheingold quoted in chapter 7 , mistake the Turing-Church thesis to state that it cannot. In fact, Rheingold goes further to state that no machine can do more than compute effectively computable functions. Turing and Church considered only machines that operate on digital data, and only machines that compute algorithmically, via a step-by-step process. We routinely build machines that satisfy neither of these properties, such as my dishwasher.

A universal Turing machine implements algorithms , step-by-step processes, where each step changes the state of the machine discretely. The word「algorithm」comes from the name of the Persian mathematician, astronomer, and geographer, Muhammad ibn Musa al-Khwarizmi (780—850), who was instrumental in the spread of the arabic system of numerals that we all use today. An algorithm is a step-by-step calculation procedure, a recipe. The notion of an algorithm is central to computer science, but it is important to recognize that an algorithm is a model of what a machine does. In a modern computer, what is really happening is electrons sloshing around.

The notion of a step, a discrete operation that takes a calculation toward its conclusion, is an abstraction. Most processes in the physical world do not proceed in a sequence of discrete steps. [2] Even a human walking, from which we get the concept of「steps,」is not actually discrete because each step evolves as continuous motions that begin with leaning forward and lifting a leg. But the digital machine abstraction considered in chapter 4 abstracts the underlying continuous physical processes in semiconductors as a discrete sequence of steps. An algorithm is an abstraction that ignores the messy continuous-world details of the computer. In this abstraction, a step does not take time, and there is no notion of being halfway through a step. A step occurs atomically , meaning indivisibly and instantaneously.

A second important feature of an algorithm is that it reaches a conclusion. That is, it halts, giving a final answer. The purpose for an algorithm is to determine that answer. An algorithm that realizes a decision function must halt, giving the answer 0 or 1. If it does not halt, then it does not realize the decision function.

To compute an effectively computable function, the program executing on a universal Turing machine must halt to deliver the final answer. Modern computers routinely run programs that are not designed to halt, such as the operating system (see section 5.4 ). These programs do occasionally halt, but we describe such halting as a「crash,」making it quite clear that this was not intended. A program that does not halt does not realize an effectively computable function. Nevertheless, even an operating system is a composition of Turing computations, chunks of computation that are each algorithmic, digital, and halting.

An operating system implements interactive behavior, which is quite different from implementing a decision function. Peter Wegner, a computer science professor at Brown University, has written extensively arguing that interactive programs can do more than algorithms (Wegner, 1997). An interactive program does not have access to all of its input when it starts executing. Input may be provided by the program's environment while the program is running, and the program can provide outputs to the environment before it halts (if it halts at all). Hence, the program becomes able to probe the environment, providing stimulus to the environment, watching its reaction (which will be provided as input), and adapting its own behavior accordingly. Turing's model included no such interaction. In his model, the input is unaffected by the output, so no dialogue with the environment is considered in the model. But still, every interactive program is a composition of algorithmic, digital, and halting chunks.

Nevertheless, if an interactive program is interacting with the physical world (i.e., the program is part of a cyberphysical system; see chapter 6 ), then the timing of the actions of the program will affect the overall behavior of the system. Such a program is clearly not a Turing computation because Turing's model includes no notion of time. The timing of the program's actions must be considered part of its「output」because the timing affects the behavior of the system. But Turing's model includes no notion of time, so the behavior is not expressible within his model. For such interactive programs, Wegner was clearly correct that they are not algorithmic.

An interactive program may be interacting with another interactive program. These two programs may even be executing on the same machine if the machine is capable of multitasking, [3] as most modern computers are. Such a pair of programs is said to be concurrent . Again, the timing of actions may affect the overall behavior, so Turing's model requires some extension to include such systems.

Robin Milner, who appeared in chapter 5 as the author of the ML programming language, in his Turing Award lecture in 1975, observed that concurrent programs cannot be modeled simply as functions from inputs to outputs, as (halting) Turing machines can be. Their chunks can be modeled as such functions but not their overall behavior.

So Wegner and Milner argue that modern computers can do things that a universal Turing machine cannot do, at least when a program is viewed holistically. Their arguments continue to be debated, but even if you accept them, modern computers, even if you endow them with unbounded memory, are still not universal machines. They still cannot do many things. In fact, I will show that there are vastly more things that a computer cannot do than things a computer can do. The reason is quite simple: the number of possible computer programs is much smaller than the number of things we might want to do. This is true even if we limit ourselves to implementing decision functions and much more obviously true if we consider functions where timing matters. Even in the limited case of decision functions, there are vastly more decision functions that neither a computer nor a Turing machine can compute than decision functions they can compute. Decision functions that cannot be realized by software on a computer are said to be「undecidable.」

[1] Later, like Claude Shannon, Alan Turing worked on cryptography during World War II. Turing played a central role in intercepting German communications that were encrypted using a machine called the Enigma. Turing led a troubled life, including being prosecuted for homosexual acts in 1952, which were illegal in the United Kingdom at the time. In 1954, he took his own life at age 41. In his few short years, however, he transformed the landscape of computing. The highest honor in computer science, the Turing Award, is named after him.

[2] If you accept a strong form of digital physics (see section 8.4 ), then every process in the physical world does, in fact, proceed in a sequence of discrete steps. But for most purposes, at the macroscale at which we interact with the physical world, this does not provide a useful model of physical processes.

[3] Multitasking means that the computer executes several programs at once rather than completing one program before executing the next one. Without multitasking, a computer could only ever execute at most one nonhalting program. The word「multitasking」has even spread into the vernacular to refer to humans simultaneously handling more than one task.

8.1 通用机器？

计算机是处理信息的机器。我在前一章探究了什么是信息以及如何度量信息。并且，我已说明信息不一定是数字形式的，至少理论上如此。在实践中，测量噪声的不可避免性以及物理世界是数字化的可能性，可能会导致这样的结论：物理世界中的信息总是可以用数字表示。如果我们更进一步，假设物理世界中的所有信息转换基本上都是以与计算机相同的方式进行的，那么原则上我们不可能做比软件所能做的更多工作。如果这个结论为真，那么它就是相当了不起的，因为它表明，软件可以做的事情远远少于我们可以想象的。在本章中，我将解释软件的局限性，以及为什么我相信我们可以（且一定可以）做软件不能做的事情。

所有计算机程序的集合实际上是一个很小的集合，其中每个程序都是一个模型。该集合的大小与 19 世纪末格奥尔格·康托尔给出的所有无限集合中最小的集合相同。俄罗斯裔德国数学家康托尔指出，有些无限集合比其他无限集合大得多。

当谈论无穷大时，我们很难推断出它的大小。事实上，康托尔花费了 12 年的时间，试图证明所有无限集合都具有相同的大小（斯穆里安，1992:219）。但是，最终他还是失败了！在这个过程中，他发展出了非凡的洞察力。我将用它来说明所有计算机程序的集合与我们可能感兴趣的在计算机上实现的功能集合相比要小得多。因此，虽然我们可以用软件做大量的事情，但是，如果我们不把自己限制在无限集合中的这个最小集合，那么其与可能的事情相比会是微不足道的。

然而，我不得不面对一个潜在的警示。随着信息论和计算理论的发展，出现了一个思想流派，一些人将其称为「数字物理学」。数字物理学假定，自然界没有也不可能存在一个连续的可能性区间。一些更强大的数字物理形式则假定，物理在原则上不可能超越软件所能做的事情。然而，在实践中，超越软件的能力在今天和可预见的将来显然会是可能的。例如，软件无法实现我的洗碗机。尽管如此，我将以对数字物理学的讨论来结束这一章。

现在，让我们抛开物理世界是否是数字化的这一问题，只考虑输入和输出都是二进制数的信息处理函数。实际上，让我们来考虑一个更小的函数集合，这些函数的输入是有限的二进制数，输出仅是一个 0 或 1，而不是一个 0 和 1 的序列。这样的函数被称为「决策函数」，因为对于每一个特定的输入，如 010101，函数都会得出是（1）或否（0）的结果。函数以这种方式做出决策。

20 世纪 30 年代，年轻的英国计算机科学家艾伦·图灵定义了一组「可有效计算」的函数，也就是那些可以使用今天被称为图灵机的机器进行算法计算（以逐步计算的方式）的决策函数。原则上，图灵机是可以用内存足够大的现代计算机来实现的。1936 年，美国数学家阿隆佐·丘奇提出了一个不同于图灵机的模型，它并不依赖于图灵机，可是，它产生了完全相同的有效计算函数集合。这实在令人感到惊奇。两个不同的模型得出相同的有效计算函数集合，这一事实表明，这组特定的函数肯定有一些特殊之处。

可能的图灵机有许多，每一个都可以计算一个不同的决策函数。在图灵的形式化表述中，每一台这样的机器都可以用有限的比特序列进行编码，就像机器码将计算机程序编码成一个有限的比特序列一样（见第 5 章）。例如，序列 000111 可能表示一个计算特定决策函数的图灵机。图灵证明了存在一个「通用图灵机」，一个可以实现任何其他图灵机的图灵机。例如，如果 000111 编码了一台图灵机，并且我们想知道该图灵机会对输入 010101 做出什么决策，那么我们可以将表示机器码的比特和输入连接起来，得到一个编码 000111010101。将这个组合的比特模式作为通用图灵机的输入，就能得到图灵机 000111 计算出的答案。所以说，比特模式 000111 是对程序的编码，而通用图灵机则是执行该程序的计算机。因此，「通用」图灵机只是一个可编程的图灵机，其中的程序可以编码任何其他的图灵机。

可有效计算函数构成了可由通用图灵机实现的决策函数集合。现在被称为丘奇 - 图灵论题的理论指出，给定足够的铅笔、纸以及足够的时间，任何一个可以由人类使用系统、逐步的过程来计算的函数，就都是可有效计算的函数之一。

只要有足够的内存和时间，任何现代计算机都可以计算任何的可有效计算函数。因此，任何现代计算机都可以被视为通用图灵机，除了会耗尽内存。但是，现在内存已经变得如此廉价和充足，所以这个警告几乎没有什么分量。

问题是，除了计算可有效计算函数之外，现代计算机是否还能做更多的事情。许多人，包括第 7 章引用的莱因戈尔德，都错误地认为丘奇 - 图灵论题是不可能成立的。事实上，莱因戈尔德进一步指出，除了计算那些可有效计算的函数，没有任何机器可以做其他更多的事情。图灵和丘奇只考虑了操作数字数据的机器，也只考虑通过逐步的过程来执行算法计算的机器。实际上，我们通常构建的机器大都不能满足这些特性，例如我家的洗碗机。

通用图灵机可以实现一组算法，一组逐步执行的过程，其中的每一步都离散式地改变机器的状态。「算法」一词来自波斯数学家、天文学家和地理学家穆罕默德·伊本·穆萨·花剌子米（约 780—850）的名字。他在我们今天仍在使用的阿拉伯数字系统的传播中发挥了重要作用。一个算法是一个逐步的计算过程，就像一个配方。算法的概念是计算机科学的核心，但重要的是要认识到，算法是机器所做事情的模型。在现代计算机中，真正发生的是电子的流动。

步骤的概念是一种抽象，是一个通过计算得出结论的离散操作。在物理世界中，大多数过程并不是按照一系列离散步骤进行的。我们从人类的行走中得到「步骤」的概念，即使如此，行走本身实际上也不是离散的，因为每一步都是从身体前倾和抬腿开始的连续动作发展而来的。但是，我们在第 4 章讨论的数字机器将半导体中基本的连续物理过程抽象为一个离散的步骤序列。算法是一种抽象，它忽略了计算机那混乱的连续世界的细节。在这个抽象中，一个步骤不需要花费时间，也没有行至步骤中途的概念。一个步骤的出现是原子的，意思是它是不可分割且瞬间发生的。

算法的第二个重要特征在于，它能得出结论。也就是说，它会终止，并给出一个最终的答案。算法的目的是确定这个答案。实现决策函数的算法必须能够终止，并给出答案 0 或 1。如果它不能终止，就不能实现决策功能。

为了计算一个有效可计算的函数，在通用图灵机上执行的程序必须能够终止，以提供最终的答案。现代计算机通常运行的是那些并非被设计为要终止的程序，例如操作系统（见 5.4 节）。这些程序偶尔会停止，但是，我们将这种停止描述为「崩溃」，以明确表示这不是有意的设计。不会终止的程序不能实现一个有效可计算的函数。然而，即使是一个操作系统，也是由一组图灵计算组成的，图灵计算是一个算法式的、数字化的和会终止的计算块。

操作系统实现交互行为，这与实现决策函数的情况非常不同。布朗大学的计算机科学教授彼得·韦格纳写了大量文章，认为交互式程序可以做的不仅仅是算法（韦格纳，1997）。交互式程序在开始执行时不能访问它的所有输入。当程序运行时，其输入可以由程序所处的环境提供，同时，程序可以在终止之前向环境提供输出（如果完全终止）。因此，程序能够探测环境，为环境提供激励，观察环境的反应（将这些反应作为输入），并相应地调整自己的行为。图灵的模型不包括这样的交互。在该模型中，输入不受输出的影响，因此模型中并不考虑与环境的交互。但是，每个交互式程序都是由算法式的、数字化的和会终止的块组成的。

然而，如果一个交互式程序是在和物理世界进行交互（即该程序是一个信息物理系统的一部分，请参阅第 6 章），那么该程序的动作的定时时间将影响系统的整体行为。这样的程序显然不是图灵计算，因为图灵的模型并未包含时间的概念。程序动作的定时必须被认为是其「输出」的一部分，因为定时会影响系统的行为。但是，图灵的模型不包含时间的概念，因此相应的行为在其模型中是无法表达的。对于这样的交互式程序，韦格纳已经说得很清楚，它们并不是算法型的。

一个交互式程序可以与另一个交互式程序交互。如果机器具有多任务处理能力，就像大多数现代计算机一样，那么这两个程序甚至可以在同一台机器上被执行。这样的一对程序被称为并发。再一次，动作的定时可能会影响整个系统的行为，所以图灵的模型需要一些扩展才能涵盖这样的系统。

我在第 5 章提到了罗宾·米尔纳，ML 编程语言的作者。他在 1975 年的图灵奖演讲中指出，并发程序不能像（会终止的）图灵机那样被简单地建模为从输入到输出的函数。它们的模块可以建模为这样的函数，但是它们的总体行为则不能。

因此，韦格纳和米尔纳认为，现代计算机可以做通用图灵机不能做的事情，至少从整体上看待一个程序的时候是这样的。他们的论点在学界引起长久的争论。但是，即使你接受了现代计算机，即使你赋予它们无限的内存，它们也不是通用的机器，它们仍然不能做许多事情。事实上，我要展示的是，计算机不能做的事情远比它们能做的事多得多。原因很简单，可能的计算机程序的数量远远小于我们可能想做的事情的数量。即使我们将自己局限于执行决策函数，这也是正确的，如果我们考虑具有定时属性的函数，这就更显而易见了。而且即使是在限定为决策函数的情形下，计算机和图灵机都不能计算的决策函数依然比它们可以计算的决策函数要多很多。计算机上软件不能实现的决策函数是「不可判定的」。

### 8.2 Undecidability

Recall that a decision function takes as input a finite binary integer, such as 010101, and produces a binary result, 0 or 1. I can prove to you that no computer can realize all decision functions even if the computer has unbounded memory. Because a modern computer, given enough memory, can do anything that a Turing machine can do, Turing's universal machines are also unable to realize all decision functions.

In fact, almost all decision functions are undecidable, or, equivalently, almost all decision functions are not effectively computable. But it is a logic error to conclude from this that no machine can realize these functions or other functions beyond decision functions. To draw that conclusion requires accepting a strong form of digital physics.

I can give you a rather simple proof. First, let's assume that we have a modern computer with an unbounded amount of memory. This hypothetical computer can implement any function that a universal Turing machine can implement.

You might already be objecting. Unbounded memory? Any computer will eventually run out of memory, so actually it will not be able to do everything that a universal Turing machine can do. But even if the computer does have unbounded memory, it is still not a universal machine. Specifically, this hypothetical computer cannot realize all decision functions. To show this, I will use a variant of a clever argument that Cantor used that is called「diagonalization.」

To show that not all decision functions can be implemented by our unbounded-memory computer, I just have to find one decision function that is not implemented by any program for that computer. In section 8.3 , we will see that there are many more than one decision function that cannot be implemented by any program, but we only need one to show that our unbounded-memory computer is not a universal machine.

First, note that I can create a list of all the possible inputs to our decision functions:

0

1

00

01

10

11

000

001

· · ·

Each input is a finite sequence of bits. This list will get very long. Infinite in fact. But hopefully you can see that every possible input, every possible finite bit sequence, will be somewhere on this list.

Every program for any modern computer is represented as a sequence of zeros and ones. As a consequence, every program will also be somewhere on this list. Not all elements of the list are valid programs, but every valid program must be on the list.

Some of these valid programs produce as output just one number, 0 or 1, for each possible input. Let's call those programs「decision programs.」Every decision program is on the list. Clearly, every decision program realizes a decision function, but not every decision function has such a program.

Let's call the first decision program on the list P 1 , the second P 2 , and so on. We see now that we can assign a name of the form P n for every decision program, where n is an integer. Each of these programs yields a decision for each of the inputs in the previous list. For example, it might be that program P 1 yields the following outputs:

P 1 (0) = 0

P 1 (1) = 0

P 1 (00) = 1

P 1 (01) = 1

· · ·

I can now find a decision function that is not implemented by any decision program. This is a contrarian function, so I will call it C . The decision function C yields the following decisions for each input:

C (0) = ¬ P 1 (0)

C (1) = ¬ P 2 (1)

C (00) = ¬ P 3 (00)

C (01) = ¬ P 4 (01)

· · ·

where the symbol ¬ is logical negation. It converts a 0 to a 1 and vice versa, like the NOT gate in chapter 4 . So if P 1 (0) = 0, then ¬ P 1 (0) = 1.

This function is contrarian because for each possible input, it yields the opposite of what one of the decision programs yields. Notice now that C is different from every decision program. It is different from P 1 because its output differs from P 1 for input 0, it is different from P 2 because its output differs from P 2 for input 1, and so on. So the decision function C is not implemented by any computer program. Hence, not all decision functions can be implemented by our infinite memory computer. Our proof is concluded.

Notice that C resembles the functions that a computer can realize, in that its input is a sequence of bits and its output is one bit. It seems that a computer should be able to realize C , but I have just shown that it can't.

The「effectively computable」functions are exactly those decision functions that are realized by one of the decision programs P n in the list. It is quite a remarkable fact that for any modern computer, regardless of its particular machine code structure, the set of effectively computable functions is essentially the same. Any computer that can realize all the effectively computable functions is said to be Turing complete . Any modern computer, if we extend it to have unbounded memory, is Turing complete. The decision function C is not an effectively computable function, or, equivalently, C is undecidable . There is no computer program that can make the decisions that C makes.

You might be protesting that C is not a useful decision function. It's just a cute corner case, an academic exercise. I have two rebuttals. First, I will show in the next section that there are vastly more functions like C than there are effectively computable functions. Second, many useful decision functions are known to be undecidable. Turing gave one: Turing's useful function takes as input a binary encoding for a Turing machine concatenated with an input string and returns 0 if the Turing machine halts and 1 if it does not. A Turing machine that does not halt just keeps executing forever without ever giving a final answer. Turing's useful function solves the so-called halting problem , telling us whether a program will halt for a particular input. This is clearly something that could be useful to know. Turing showed that this function is undecidable.

It is surprisingly easy to show that the halting problem is undecidable. If you will again indulge me a brief nerd storm, the proof is another diagonalization argument, as shown earlier. First, assume we have a computer program called H that solves the halting problem. If H were to exist, then it would be given two inputs: a binary encoding B of a program and a binary encoding I of an input to that program. All that H has to do is return 0 if B halts for input I and return 1 otherwise. It must return these values after a finite number of steps. We can't wait forever for H or its answer would be useless.

Because B and I can be concatenated into a single input bit sequence, H is a decision program. Let's write the concatenated input BI , and let's write H ( BI ) to mean「execute program H on input BI .」For H to actually solve the halting problem, it must itself halt for any input. Given any input BI (or at least any input BI where B is a valid program), it must return 0 or 1.

Because B and I are both sequences of bits, if H exists, then we should certainly be able to evaluate H ( BB ), and it should return 0 if B halts with input B , and 1 otherwise. Now recall that every program is encoded as a bit sequence, and every bit sequence is in the list of bit sequences 0, 1, 00, 01, 10, 11, 000, · · · . The list must contain every program that, given input BB for any valid program B , halts and returns 0 or 1. Let's call the first such program on the list F 1 , the second one F 2 , and so on. We can now show that H must be different from every one of these F n programs, and hence H cannot be a program that halts and returns 0 or 1 for every input BB . It cannot solve the halting problem.

For each F n on the list, we construct a new program T n , a rather annoying program like the contrarian program C shown earlier. It uses F n as a subprogram, but it does not itself implement an effectively computable function. It fails to halt for some inputs. Specifically, given a valid program B , the first thing T n does is evaluate F n ( BB ). By assumption, F n ( BB ) always halts and returns 0 or 1. If F n ( BB ) returns 1, then T n ( P ) returns 0. Otherwise, and here is where T n gets annoying, T n loops forever and never returns anything. It fails to halt. In pseudocode, [4]   T n looks like this:

if   ( F n ( BB ) == 1) {

return 0

}  else {

loop forever

}

We can now show that none of the F n in the list solves the halting problem or, equivalently, that the function that F n implements is different from the function that H implements for every n = 1, 2, · · · . To do this, suppose we evaluate the annoying function T n on its own binary encoding. That is, we evaluate T n ( T n ). Does this halt? If it does, then H ( T n T n ) should return 0; otherwise it should return 1. What does F n ( T n T n ) return? Well, we don't know because F n is just some arbitrary program realizing an effectively computable function. But we do know that F n ( T n T n ) halts and returns something.

Suppose that F n ( T n T n ) returns 1. Then T n halts and returns 0, so H ( T n T n ) = 0. So in this case, F n is not the same as H . They return different values. Suppose instead that F n ( T n T n ) returns 0. Then T n annoyingly does not halt, so H ( T n T n ) = 1. So again F n is not the same as H .

Because H is different from F n for all n , H is not on the list of programs that return 0 or 1 for any input BB . Hence, H cannot be a program that solves the halting problem. Whew. Survived another nerd storm.

A direct consequence of the undecidability of the halting problem is that in any programming language, there will be valid programs where we can't tell what the program will do just by looking at the program. We cannot tell whether the program will ever halt and give an answer.

The philosophical consequences are profound. Programs and their executions on computers exist in the physical world. So Turing has shown us that there are physical processes that we cannot fully「explain.」A full explanation of some physical process should, it seems, tells us why it exhibits some behavior. But Turing showed us there are processes for which we cannot even tell whether they will exhibit some behavior, much less why.

A fundamental theme of this book is that we must insist on keeping separate in our minds the map and the territory. Any「explanation」of the physical world or of what a computer does is a map. It is a model. A computer program is a model of its own execution. Turing showed us that this model can never fully explain the thing it models. A program does not fully explain its own execution because you cannot tell what it will do just by looking at the program. The world is what it is, and every model, every explanation, every map, and every program we construct is a human invention distinct from the thing that it models. The set of all maps is incomplete, in that there are properties of the physical world that cannot be mapped.

Nothing that I have said should be construed to undermine the value of models or maps. It leaves open the question of whether programs, as models, can describe all processes, even if we now know that they cannot explain all processes. The question remains whether our hypothetical unbounded-memory computer is a universal machine. If you define 「computation」to mean exactly those decision functions that are effectively computable , then our unbounded-memory computer can realize all「computations.」But this argument is circular. We have defined「universal」to mean「it does everything that it does.」This is why the Church-Turing thesis is called a thesis and not a theorem. It simply states that the effectively computable functions are the ones we can compute with an (idealized) computer. Nothing about this thesis says that there is no machine that can realize C . All we have shown is that a computer , as defined by the digital technology of chapters 4 and 5 , cannot realize more than a small subset of decision functions.

It turns out to be a surprisingly controversial topic whether there could be a machine to realize functions like C . A whole community has emerged that looks at what some people call「hypercomputation」or「super-Turing computation」that specifies (mostly hypothetical) machines that compute functions that are not effectively computable. For example, Blum et al. (1989) describe a hypothetical machine that is similar to an ordinary computer except that it operates on real numbers rather than digital data. But its execution is still algorithmic, so many of the same questions and answers carry over from Turing machines, such as the question of whether a program ever halts.

Martin Davis, an American mathematician whose PhD thesis advisor was Alonzo Church, vocally debunks the very idea of hypercomputation, except possibly as a pure theory exercise (Davis, 2006). Even his arguments, however, are set squarely in the framework of algorithmic operations on finite bit sequences. He ignores timing, for example, presumably assuming that timing is irrelevant, and he assumes that input and output are discrete. He observes, for example, of any machine that produces a non-Turing-computable infinite sequence of natural numbers (which can be encoded as finite bit sequences),「no matter how long this goes on, we will see only a finite number of these outputs」(Davis, 2006). This assumes the outputs are rendered to the observer as a list (which is discrete) of natural numbers (also discrete). Is this the only way to present a result of a computation? It is the way computers present results, but what about other machines? My dishwasher does not present its results as a list of numbers.

Ultimately, I believe that any conclusion that no machine can realize functions like C is an act of faith, a position I will defend more strongly in the next chapter. Like many acts of faith, this one requires ignoring evidence against it. Clearly, computers are not universal machines because they can't do what my dishwasher does. Surely my dishwasher is a machine, albeit not an information-processing machine. In fact, it is a cyberphysical system because it includes a computer working in concert with mechanical and hydraulic systems. A dishwasher that presents clean dishes as a list of numbers won't sell well. But actually, even the resistors and inductors considered in chapter 2 , as modeled by Ohm's and Faraday's laws, are not realizable by computers because they do not operate on binary data and do not operate algorithmically.

Nevertheless, many authors, not just Rheingold and Davis, subscribe to this faith of universal computation. In fact, it's a powerful religion these days, with many believers. Turing and many others since have conjectured that even the human brain, and hence human cognition, is realizable by a universal Turing machine. As I will show in the next chapter, I cannot prove this conjecture false, but I believe it is extraordinarily unlikely. This faith of universal computation can only be true if a strong form of digital physics is true, and even then it will not lead to useful models.

Turing himself actually described a hypothetical machine that can realize C . He called it an「oracle machine」and assumed it would not be implementable. I can explain a simple version of it. Assume infinite memory. Technically, this assumption is stronger than the assumption of unbounded memory that we made for the universal Turing machine because「unbounded」means that we have all the memory we need, whereas「infinite」means that we can actually store an infinite list of bits. Even so, this new machine will prove not to be a Turing machine.

Suppose that the infinite memory initially contains a table of all the outputs that C produces for each input. This memory is like an oracle, all knowing. That is, the first entry in the table has one bit with value ¬ P 1 (0), which gives us C (0); the second entry has value ¬ P 2 (1), which gives us C (1); and so on. Now, given any input, such as 010101, the machine simply goes down the table until it finds the entry matching this input and produces the corresponding output C (010101). For any input, this procedure can be accomplished in a finite number of steps, so this machine will always produce an output eventually. It realizes the decision function C . In fact, just by providing a different initial table, this hypothetical machine can realize all decision functions, so it's much more「universal」than a universal Turing machine.

I have already pointed out, but it bears repeating, that Turing never intended the word「universal」in「universal Turing machine」to mean that these machines could do everything. Turing's machine is universal in the sense that its program, which defines the function it computes, is part of the input to the machine. A nonuniversal Turing machine, by contrast, is not programmable. It computes exactly one function, and that function is built into it. So Turing's「universal」means simply that the machine can be programmed to compute any effectively computable function. It is a mistake to reinterpret「universal」to mean that it can do everything.

In what sense is this oracle machine not a Turing machine? The key issue is the memory containing the table. Turing did not include in his description of a universal Turing machine the ability to initialize an infinite memory. Modern computers also do not have this capability. But does this mean that no machine can do this?

To conclude that there cannot be such a machine, I would have to assume that it is physically impossible to construct something that「remembers」any infinite sequence of bits. Is it? Only by accepting digital physics can I conclude that this is impossible.

Suppose I want to remember the number π. A binary encoding requires an infinite number of bits. Suppose that I can cut a steel rod so that its length is exactly π  meters. In 1799, a platinum bar was placed in the National Archives in Paris and became, for many years, the standard definition of one meter of length. So it is not so far fetched to use the length of a rod for memorizing a value. Haven't I just made a memory that stores an infinite number of bits of information?

Of course, I will run into a number of practical physical problems with this memory. The length of the rod will vary with temperature (and with passing gravitational waves, apparently), and I would need a clear and precise specification of what「one meter」is to interpret the length of the bar as「π meters.」Measuring the length precisely will be difficult or even impossible due to quantum mechanical uncertainty laws. And if there is any noise at all in the measurement process, then Shannon's channel capacity theorem from the previous chapter, equation (4), shows that the information conveyed by a measurement contains only a finite number of bits.

But just because I can't measure the length doesn't mean that the rod doesn't have a length. Moreover, even if the length of the rod changes over time, as it does so, if it progresses fluidly from one length to another, then the length at each instant will have some dependence on the lengths at prior instants. Isn't such dependence a form of memory? If the length changes fluidly from one value to another, then at least some of the intermediate lengths would require an infinite number of bits to be represented precisely under any units of length, be they meters, inches, furlongs, or any arbitrary unit.

The form of the information is not in bits. Where are the bits? But then again, where are the bits in a computer? A key premise in the concept of information is that the form in which it is stored is not important. This is why information can be conveyed and copied. The idea of conveying and copying information depends on the assumption that the recipient has the same information as the originator, although the physical form of the information is obviously distinct in the recipient. Modern computer memories store bits electrically or magnetically, using the techniques of chapter 4 to abstract the messy physics into digital models. When information is conveyed from one computer to another, the form of storage can change, for example, from electrical charges to magnetic polarization. When designing computer memories, engineers have no need to assume that the underlying physics is discrete. So what is wrong with the means by which my rod stores the number π? Nothing. If I insist that the form be as a list of bits, then I've already assumed the conclusion, that such a memory is not possible.

An astute reader can use many remaining problems to challenge my position. Suppose, for example, that you require that in order for something to be deemed to be「information,」it must be possible to convey or copy it. Then we run into a fundamental problem. Shannon's channel capacity theorem, equation (4), tells us that if there is any noise in the channel over which the information is conveyed or copied, then only a finite number of bits of information gets through. With this observation, you could define「information」to only include things that can be represented with a finite number of bits. This requires rejecting the use of continuous entropy ( section 7.4 ) as a measure of information.

I am a teacher. I know quite a lot about a few things. I think what I know is「information.」But I also know that I routinely fail to convey this information to my students. Some of it gets through, but not all of it. I am privileged to work with extremely smart students, and many of them creatively misunderstand what I am trying to convey and come up with insights that I never had. And sometimes they fail to convey those insights to me. But this does not make what I know and what they know any less「information.」It is still information even if it is not conveyed.

So I believe there is plenty of room for doubt that a universal Turing machine is a universal information-processing machine. This is probably a minority opinion today, and I will try to defend it better in the next section. The root of my doubt lies in the mathematical notion of cardinality of infinite sets. The fact is that the set of all computer programs is a small infinite set. In fact, the size of this set is equal to the size of the smallest infinite sets that mathematicians know about. Much bigger infinite sets exist. To assume that all the machines we can make are limited to this smallest of infinite sets, I have to assume digital physics. To assume that all machines that nature can make (or has made) are also so limited, I have to reject the existence of anything continuous in nature. This requires accepting one of the stronger forms of digital physics. I will now try to explain just how unlikely this limitation is by examining the notion of cardinality. I will then directly confront the idea of digital physics in section 8.4 . In chapter 11 , I will explain why it is that when some hypothesis is unlikely to be true, we must demand much stronger evidence before accepting the hypothesis than if the hypothesis is a priori likely to be true.

[4] Programmers use「pseudocode」to refer to a sketch of a program that is not written in any particular programming language. Its purpose is to communicate intent to other humans.

8.2 不可判定性

我们回顾一下，一个决策函数以有限的二进制整数（如 010101）作为输入，并产生一个二进制结果 0 或 1。我可以向你证明，即使可以拥有无限的内存，也没有一台计算机能够实现所有的决策函数。因为只要有足够的内存，现代计算机就可以做图灵机能做的任何事情，所以，图灵的通用机器也无法实现所有的决策函数。

事实上，几乎所有的决策函数都是不可判定的，或者几乎所有的决策函数都不是有效可计算的。但是，由此得出，没有任何机器能够实现这些函数或决策函数之外的其他函数这一结论，却是逻辑错误的。要得出这样的结论，就需要接受一种强大的数字物理学形式。

我可以给你一个很简单的证明。首先，假设我们拥有一台内存无限大的现代计算机。这台假想的计算机可以实现通用图灵机所能实现的任何函数。

你可能已经开始反对我的观点了。有无限大的内存吗？任何计算机最终都会耗尽内存的，难道不是吗？所以实际上计算机将无法完成通用图灵机所能完成的一切。但是，即使计算机的确拥有无限大的内存，它也不会是一台通用机器。具体而言，这台假想的计算机并不能实现所有的决策函数。为了证明这一点，我将使用一个被康托尔使用的、称作「对角化」的巧妙变量的变体。

为了证明并非所有决策函数都可以由我们那具有无限内存的计算机来实现，我只需要找到一个不能被任何计算机上的计算机程序实现的决策函数即可。在 8.3 节中，我们将看到有许多决策函数不能被任何程序实现，但我们只需要一个来表明拥有无限内存的计算机并不是一台通用机器。

首先，请注意，我可以为我们的决策函数创建一个所有可能输入的列表：

01

00

01

10

11

000

001

…

每个输入都是一个有限的比特序列。这个列表会很长。实际上，它将是无限的。但是，我希望你能看到，每一个可能的输入以及每一个可能的有限比特序列，都会出现在这个列表的某个位置上。

任一现代计算机上的任何程序都可被表示成一个 0 和 1 的序列。因此，每个程序也将出现在这个列表的某个位置上。并不是这个列表中的所有元素都会是有效的程序，但是，每个有效的程序都一定会在列表中。

其中一些有效的程序对于每个可能的输入只会产生一个数字，0 或 1。

让我们把这些程序称为「决策程序」。每个决策程序都在列表上。显然，每个决策程序都实现了一个决策函数，但并不是每个决策函数都会有这样一个程序。

让我们将列表上的第一个决策程序称为 P1 ，第二个称为 P2，以此类推。现在我们可以为每个决策程序分配 Pn 形式的名称，其中 n为整数。这些程序中的每一个都会为前面列表中的每个输入生成一个决策。例如，程序 P1 可能产生以下输出：

P1(0)=0

P1(1)=0

P1(00)=1

P1(01)=1

…

现在，我可以找到一个没有被任何决策程序实现的决策函数。这是一个反向函数（contrarian function），所以我称它为 C。决策函数 C 为每个输入产生以下决策：

C(0)=¬P1(0)

C(1)=¬P2(10)

C(00)=¬P3(00)

C(01)=¬P4(01)

…

其中符号 ¬ 是逻辑否定。它将 0 转换为 1，反之亦然，就像第 4 章中的非门。由此，如果 P1(0)=0，那么 ¬P1(0)=1。

这个函数是反向的，因为对于每个可能的输入，它所产生的结果都与决策程序的结果相反。现在请读者们注意，C 与每一个决策程序都是不同的。它不同于 P1，因为输入为 0 时它的输出与 P1 不同，输入为 00 时它的输出与 P2 不同，以此类推。因此，决策函数 C 不是由任何计算机程序实现的。由此我们可以得出，并不是所有的决策函数都可以由我们拥有无限内存的计算机来实现。好了，我们的证明到此结束。

请注意，C 类似于计算机可以实现的函数，因为它的输入是一个比特序列，输出是一个比特。这让人感觉似乎计算机应该能够实现函数 C，但是我刚刚证明了它不能。

「可有效计算」函数正是由列表中的那些决策程序 Pn 实现的决策函数。对于任何现代计算机来说，无论其特定的机器码结构如何，可有效计算函数的集合都是相同的，这是一个非常值得注意的事实。任何能够实现所有有效计算函数的计算机都是图灵完备的。任何现代计算机，如果我们把它们扩展到拥有无限内存的话，它们就都是图灵完备的。决策函数 C 不是一个可有效计算函数，换言之，C 是不可判定的。没有任何计算机程序可以做出 C 所做的决策。

你可能会提出不同的观点，认为 C 不是一个有用的决策函数。它不过是一个有趣的例外，一个学术探讨而已。但是，我可以提出两条反驳意见。首先，我将在下一节做出说明，像 C 这样的函数要比可有效计算函数多得多；其次，许多有用的决策函数已知是不可判定的。图灵给出一个例子，图灵的有用函数将图灵机的二进制编码与输入字符串连在一起，如果图灵机停机，就返回 0，否则，返回 1。一台不停机的图灵机会永远执行，而不会给出最终的答案。图灵的这个有用函数解决了所谓停机问题，其告诉我们一个程序是否会因为一个特定的输入终止。这显然是非常有用的。图灵证明了这个函数是不可判定的。

要证明停机问题是不可判定的，实际上非常容易。如果你还有耐心的话，我想再进行一场简短的技术呆子头脑风暴，该证明如同之前所示的，是另一个对角化的论点。首先，假设我们有一个名为 H 的计算机程序，它可以解决停机问题。如果 H 存在，那么它会有两个输入：程序的二进制编码 B 和程序输入的二进制编码 I。

H 要做的是，如果输入为 I 时 B 会终止，返回 0，否则返回 1。它必须在有限的步骤之后返回这些值。我们不能永远地等待 H ，如果是这样的话，H 的答案就是没有用的。

因为 B 和 I 可以连接成一个输入比特序列，所以 H 是一个决策程序。我们将连在一起的输入记为 BI，并用 H（BI）表示「在输入 BI 上执行程序 H」。为了让 H 能够真正解决停机问题，它对任何输入都必须能够自己终止。给定任何输入 BI（或者至少是 B 为一个有效程序的任何输入 BI），它必须返回 0 或 1。

因为 B 和 I 都是比特序列，如果程序 H 存在，那么我们肯定能够计算 H（BB）。如果输入 B 以后 B 终止了，那么 H（BB）应该返回 0，否则返回 1。现在我们回顾一下之前的内容，每个程序都被编码为一个比特序列，每个比特序列都在比特序列 0,00,01,10,11,000,… 的列表中。列表必须包含每一个程序，对任何有效程序 B 输入 BB 时，该程序将终止，并返回 0 或 1。我们将列表上的第一个这样的程序称为 F1，第二个称为 F2，以此类推。我们现在可以证明，H 必须不同于所有这些 Fn 程序中的任何一个，因此 H 就不可能是对于每个输入 BB 都会终止并返回 0 或 1 的一个程序。因此，我们还是不能解决停机问题。

对于列表中的每个 Fn，我们构造了一个新的程序 Tn，就像前面给出的反向程序 C 一样，这是一个非常烦人的程序。它将 Fn 作为一个子程序，但它本身并没有实现一个有效可计算的函数。对于某些输入，这个程序不能终止。具体来说，给定一个有效的程序 B，Tn 要做的第一件事就是计算 Fn（BB）。根据假设，Fn（BB）程序总是能够终止并返回 0 或 1。如果 Fn（BB）返回 1，则 Tn（P）返回 0。否则，Tn 就会永远循环且不返回任何结果，这也是 Tn 让人恼火的地方。它不会终止。Tn 的伪代码看上去是这样的：

现在我们可以证明，列表中的 Fn 都是不能解决停机问题的程序，换言之，对于每一个 n=1,2,…，Fn 实现的函数与 H 实现的函数是不同的。为此，假设我们在 Tn 自己的二进制编码上进行 Tn 计算，也就是说，我们计算 Tn（Tn），它能终止吗？如果可以，那么 H（TnTn）应该返回 0，否则它应该返回 1。那么，Fn（TnTn）会返回什么呢？我们还不知道，因为 Fn 只是实现了一个可有效计算函数的任意程序。但是，我们的确知道 Fn（TnTn）会终止并返回某种结果。

假设 Fn（TnTn）返回 1，之后 Tn 终止并返回 0，由此，H（TnTn）=0。在这种情况下，Fn 和 H 是不同的，它们返回不同的值。相反，假设 Fn（TnTn）返回 0，那么 Tn 不会终止，所以 H（TnTn）=1。所以，我重申一遍，Fn 不同于 H。

因为对于所有的 n，H 与 Fn 都不相同，所以 H 并不在对于任何输入 BB 都能返回 0 或 1 的程序列表之中。因此，H 不可能是一个解决停机问题的程序。哇，我们躲过了另一场技术呆子的头脑风暴。

停机问题的不可判定性导致的一个直接后果就是，在任何编程语言中都会存在一些有效的程序，而我们不能仅通过查看程序就知道程序要做什么。我们也无法判断程序是否会终止，并给出最终的答案。

停机问题的哲学意义是深远的。程序及其在计算机上的执行存在于物理世界中。所以，图灵告诉我们，物理世界里存在着一些我们无法完全「解释」的物理过程。对某个物理过程的充分解释似乎应该能够告诉我们为什么它会表现出某种行为。但是，图灵也给我们展示了一些物理过程，对于这些物理过程而言，我们甚至不知道它们是否会表现出某种行为，更不用说为什么会是这样。

本书的一个基本主题是 —— 我们必须在头脑中坚持把地图和地域这两个概念区分开。对物理世界或计算机所做事情的「解释」都不过是一张地图。地图是一个模型，计算机程序是其自身执行的一个模型。图灵向我们展示了这个模型永远不能完全解释它所建模的事物。程序不能完全解释它自己的执行，因为你不能仅仅通过查看程序就知道它要做什么。世界就是它本来的样子，然而，我们所构建的每一个模型、每一种解释、每一张地图，以及每一个程序都是人类的发明，它们不同于它们所建模的事物。所有地图的集合也是不完整的，因为物理世界的某些属性无法被映射出来。

我所说的一切都不应被解读为要破坏模型或地图的价值。但这仍然留下一个悬而未决的问题 —— 程序作为模型是否能够描述所有的过程，即使我们现在知道它们不能解释所有的过程。问题在于，我们假设的拥有无限内存的计算机是否就是通用机器。如果你定义的「计算」精确地指那些可有效计算的决策函数，我们那些拥有无限内存的计算机就可以实现所有的「计算」。但是，这个论点就变成了一个循环。我们已经把「通用」定义为「它做它所做的一切」。这就是丘奇 - 图灵论题只能被称为论题而非定理的原因。该论题简单地说明，可有效计算函数是我们可以用一台（理想的）计算机计算的函数。这一论题并没有说不存在可以实现函数 C 的机器。我们需要说明的是，正如在第 4 章和第 5 章中数字技术所定义的那样，一台计算机只能实现一个小的决策函数子集。

是否存在一台能够实现类似 C 这样的函数的机器，这成了一个令人惊讶的争议性话题。后来，出现了一个关注所谓「超计算」或「超图灵计算」的群体，「超计算」或「超图灵计算」旨在研究（大多是假设的）计算非可有效计算函数的机器。例如，布卢姆等（1989）描述了一台与普通计算机相似的假想机器，只不过它操作的是实数而非上述数字数据。但是，它的执行仍然是算法式的，由此，也就从图灵机中延续了许多相同的问题和答案，例如一个程序是否会终止的问题。

马丁·戴维斯是一位美国数学家，他的博士论文导师是阿隆佐·丘奇。马丁非正式地揭示过超计算的思想，但是，那很可能只是一次纯粹的理论尝试（戴维斯，2006）。然而，即使是他的论点，也是在有限比特序列上的算法式操作框架中建立起来的。例如，他忽略了定时的问题，并假定计算与定时是不相关的，以及输入和输出是离散的。例如，他观察到，任何产生非图灵可计算的无限自然数序列（可以编码为有限比特序列）的机器，「无论其运行多长时间，我们只会看到有限数量的输出」（戴维斯，2006）。这假设呈现给观察者的输出是自然数（是离散的）的列表（是离散的）。这是表示计算结果的唯一方法吗？如果这是计算机呈现结果的方式，那么其他机器呢？我的洗碗机就不会以一个数字列表的方式给出计算结果。

最终，我认为，有关没有机器能够实现类似于 C 的函数的任何结论都是一种具有信念的行动，我将在下一章更加坚定地捍卫这一立场。就像许多具有信念的行动一样，这需要忽略反对它的证据。很明显，计算机并不是通用机器，因为它们不能做我的洗碗机能做的事情。当然，我的洗碗机虽然不是一台信息处理机，但它是一台机器。事实上，它是一个信息物理系统，因为它包括了一台与机械液压系统协同工作的计算机。用一个数字列表显示干净盘子的洗碗机并不会卖得更好，效果才是主要的。但实际上，即使是第 2 章提及的由欧姆定律和法拉第定律建模的电阻和电感，也不可能通过计算机来实现，因为它们操作的不是二进制数据，也不是以算法的方式运作。

尽管如此，除了莱因戈尔德和戴维斯，还有许多人认同这一通用计算的信念。事实上，这现在是一个十分强大的信念，并且拥有众多的追随者。图灵和其他许多人都推测，甚至是人类的大脑以及人类的认知，也可以通过通用图灵机来实现。正如我将会在下一章说明的，我不能证明这个猜想是错误的，但我认为这是极其不可能的。只有在一种强大的数字物理学形式成立时，这种通用计算的信念才会成立，即使这样，它也不会产生有用的模型。

实际上，图灵自己描述了一台可以实现函数 C 的假想机器。他将其称为「预言机」（也译为谕示机），并假设是无法实现的。这里，我可以简单地解释一下。假设它有无限的内存，从技术角度讲，这个假设比我们为通用图灵机建立的无边界内存的假设要更为强大，因为「无边界」内存意味着我们拥有我们需要的所有内存，而「无限的」意味着我们实际上可以存储无限的比特列表。即使如此，这台新机器也被证明不是图灵机。

假设该无限的内存中最初包含一个由函数 C 对每个输入所生成的所有输出的表。这个内存就像一个神谕，知晓一切。也就是说，表中的第一个条目为 1 个比特，它的值为 ¬P1(0)，给出了 C（0）；第二项的值为 ¬P2(00)，给出了 C（00），以此类推。现在，给定任何输入，如 010101，机器只需要沿着表查找与该输入匹配的条目，并生成相应的输出 C（010101）即可。对于任何输入，这个过程都可以在有限的步骤内完成，所以这台机器最终总会产生一个输出，它实现了决策函数 C。事实上，只要提供一个不同的初始表，这个假想的机器就可以实现所有的决策函数，因此它比通用图灵机要更为「通用」。

之前我已经阐明，但在这里还需要重申一下，图灵从未期望「通用图灵机」中的「通用」一词是指这些机器可以做任何事情。图灵的机器是通用的，因为定义了它所计算的函数的程序是机器输入的一部分。相比之下，非通用图灵机是不可编程的，它只计算一个函数，并且该函数是被内置到机器中的。所以图灵的「通用」意味着机器可以被编程用来计算任何的可有效计算函数。如果将「通用」解释为无所不能，就大错特错了。

那么，到底从何种意义上说，这台预言机不是图灵机呢？关键问题要看包含了这张表的内存。图灵对通用图灵机的描述不包括初始化无限内存的能力。当然，现代计算机也没有这种能力。但是，这是否意味着没有一台机器可以做到这一点呢？

要得出不可能存在这样一台机器的结论，我就必须假设，从物理上不可能构建一个能够「记住」任何无限比特序列的事物。是这样吗？只有接受数字物理学，我才能得出这是不可能的这一结论。

假设我想要记住 π 这个数字。在二进制编码中，这需要无数的比特。假设我可以切割一根钢条，使它的长度正好是 π 米。1799 年，一根白金杆被放置在巴黎的国家档案馆中，多年来，它已成为一米这一长度单位的标准定义。因此，可以这么说，用杆的长度来记忆一个值并不是遥不可及的事情。我刚刚不就建立了一个存储无限信息比特的内存吗？

当然，这个内存会让我遇到一些实际的物理问题。金属杆的长度会随温度的变化（显然，以及重力波的通过）而发生改变。我需要一个「一米」表示什么的清晰和精确规格来解释杆的长度为「π

米」。由于量子力学的不确定性定律，想要精确地测量长度将是非常困难甚至是不可能的。如果测量过程中存在任何噪声，那么根据上一章香农的信道容量定理，即方程（4），测量所传递的信息仅包含有限的比特数。

但是，不能仅仅因为我不能测量长度，就说其意味着这个杆没有长度。此外，即使杆的长度随着时间的推移会发生变化，如果它从一个长度连续地变为另一个长度，那么每个时刻的长度也在一定程度上依赖于前一时刻的长度。那么这种依赖不是记忆的一种形式吗？如果长度从一个值连续地变化到另一个值，那么至少有一些中间长度将要求在任何长度单位下精确地表示无限数量的比特，无论长度单位是米、英寸、弗隆还是其他任意单位。

这种信息并不以比特的形式来表示。那么比特用在哪里呢？换言之，计算机中的比特在哪里？信息概念的一个关键前提是，信息的存储形式并不重要。这就是为什么信息可以被传递和复制。尽管信息的物理形式在接收者那里是明显不同的，但传递和复制信息的想法取决于这样一种假设，即接收者与发出者拥有相同的信息。现代计算机的存储器以电荷或磁能的方式存储比特，利用第 4 章的技术将那些无序的物理现象抽象为清晰的数字模型。

当信息从一台计算机传送到另一台计算机时，信息的存储形式可能会发生改变，例如从电荷变成磁极化。在设计计算机存储器时，工程师无须假设底层的物理过程是离散的。那么，是我用金属杆存储数字 π 的方法出了什么问题吗？什么问题都没有。如果我坚持其形式就是一个比特列表，那么我已经假定了这样一个结论 —— 这样的信息存储是不可能的。

一位敏锐的读者可以利用许多悬而未决的问题来挑战我的立场。例如，如果你要求让某物被认为是「信息」，那么我们必须能够传递或复制它。这样，我们就得面对一个根本性的问题。香农的信道容量定理，即方程（4）告诉我们，如果在传输或复制信息的信道中存在任何噪声，那么只有有限比特数量的信息能够通过。基于这个观察，你可以将「信息」定义为仅包括可以用有限比特来表示的事物。这要求不能使用连续熵（第 7.4 节）作为信息的度量。

我是一名教师，对一些事物也有相当的了解。我认为我知道什么是「信息」。但是我也知道，我常常不能将这些信息传递给我的学生。部分信息被传递了，但并不是全部信息。我很有幸能够与非常聪明的学生一起工作。他们中的许多人创造性地误解了我想要传递的信息，并提出我从未有过的见解。有时候，他们也没能把这些见解全部传递给我。但是，这并不能减少我所知道的和他们所知道的「信息」。即便信息没有被传递出去，它们也是信息。

因此，我相信，通用图灵机是通用的信息处理机这一说法是非常值得商榷的。今天，这可能只是少数人的观点，我将在下一章更好地为之辩护。我质疑的根源在于无限集合的势（也称基数）这一数学概念。事实上，由所有计算机程序组成的集合是一个很小的无限集合。实际上，这个集合的大小等于数学家们所知道的最小无限集合的大小。当然，存在着更大的无限集合。为了假设我们可以制造的所有机器都局限于这些无限集合中的最小集合，我必须对数字物理学做出假设。为了假设自然界所能制造（或已经制造）的所有机器也是非常有限的，我不得不排除自然界中任何连续的事物的存在。这就需要接受一种更强大的数字物理学形式。现在我将通过研究势的概念来解释这种限制是多么不可能。然后，我将在 8.4 节直接探讨数字物理学的概念。在第 11 章中，我将解释为什么当某些假设不太可能成立的时候，在接受该假设之前，我们必须具有比该假设可能先验成立的还要更强有力的证据。

### 8.3 Cardinality

A mathematician uses the term「cardinality」for the size of a set. [5] A set with two items, for example, has cardinality two. This rather trivial concept becomes interesting only when we consider sets that have an infinite number of items, such as the set of all computer programs.

In the previous section, I showed that there is at least one decision function that is not implementable by any computer program. Using Cantor's results, we can show more strongly that an infinite number of decision functions are not realizable by any computer program. Even more strongly, we can show that vastly more decision functions cannot be realized than decision functions that can be realized by a computer program.

This result depends on Cantor's observation that not all infinite sets have the same size. To put this in intuitive terms, consider the set of all nonnegative integers, N = {0, 1, 2, 3, · · · }. The symbol N is shorthand for this entire infinite set of integers.

There are clearly a lot of them, an infinite number, in fact, as indicated by the ellipsis「· · · ,」which can be read「and so on.」This set is called the set of「natural numbers」presumably because someone thought that negative and fractional numbers were somehow unnatural.

Consider now the set of all「real numbers,」commonly given the symbol ℝ. [6] This set includes all the elements of ℕ but also many more numbers. It includes negative numbers, fractions, and irrational numbers (numbers such as π that cannot be represented using fractions). Clearly ℝ is a bigger set than ℕ . But how much bigger?

First, we need to be clear on what we mean by the size of an infinite set. In Cantor's notion of the sizes of infinite sets, two infinite sets A and B are said to have the same size if we can define a one-to-one correspondence between the elements of the sets. A one-to-one correspondence means that for every element of A , we can assign a unique element of B to be its partner. For example, consider the set ℕ and another set = {−1, −2, −3, · · · }. We can establish a one-to-one correspondence as follows:

Each and every element of one set has a unique partner in the other set. So Cantor's observation is that we can declare these two sets to have the same size.

Interestingly, we can also establish a one-to-one correspondence between the set ℕ and a subset of itself containing only even integers, = {0, 2, 4, 6, · · · }:

Every element of both sets is represented, so these two sets also have the same size, although the second set omits half the elements of the first. This oddity is a property of infinite sets. They have the same size as many of their own subsets.

Cantor denoted the size of the set ℕ by the symbol ℵ 0 , where ℵ is the first letter of the Hebrew alphabet, aleph. The subscript 0 indicates that this is the size of the smallest known infinite sets. Mathematicians pronounce ℵ 0 「aleph null.」

Interestingly, many sets have size ℵ 0 , including the natural numbers ℕ , the integers, and even the rational numbers. The set of binary sequences listed in the previous section, let's call it = {0, 1, 00, 01, 10, 11, 000, · · · }, also has size ℵ 0 .

Hopefully, you can see how to establish a one-to-one correspondence between this set and ℕ .

A set with size ℵ 0 is called a「countably infinite set」because there is a one-to-one correspondence with the set of counting numbers {1, 2, 3, 4, · · · }. Hence, we can「count」the elements of the set, although we will eventually tire of doing so because of its infinite size.

For any set with size ℵ 0 , every infinite subset of that set also has size ℵ 0 . Consequently, the size of the set of all computer programs is also ℵ 0 . This is because every computer program is in the set , and an infinite number of such programs is possible.

Now things get really interesting. Cantor, to whom I owe the diagonalization arguments in the previous section, showed that there are infinite sets with vastly bigger size than ℵ 0 . In particular, Cantor showed that the set ℝ of real numbers has no one-to-one correspondence with ℕ . He used a diagonal argument similar to what I used in the previous section. Mathematicians say that the set ℝ is「uncountable.」Moreover, there are even bigger infinite sets, such as the set of all functions that map real numbers into real numbers.

There are many uncountable sets besides ℝ . In fact, the set of decision functions from the previous section is also uncountable. It has the same size as ℝ . To show this, we can establish a one-to-one correspondence between the set of real numbers and the set of decision functions. We could do that here, but I'll spare you that nerd storm and ask you to take my word for it.

As with ℕ , a proper subset of ℝ may have the same size as ℝ . For example, the size of the set of real numbers between zero and one is the same.

An uncountable set is strictly larger than a set with size ℵ 0 . In light of this result, it is not surprising that not all decision functions can be realized by computer programs, even though decision functions only involve binary digits. The set of decision functions is uncountable, and the set of computer programs is countable and therefore much smaller. If more decision functions than the decidable ones are realizable, then computers are not universal information-processing machines.

Now notice that any machine that deals with real numbers will also not be realizable by computer programs. Hence, to consider computers to be universal information-processing machines, we have to exclude real numbers from our notion of「information.」This rather drastic step goes against almost all tradition in mathematics, science, and engineering. We should not accept this step lightly.

Recall from the previous chapter that information can be measured in bits if the number of alternative arrangements being distinguished is finite. That is, information in bits selects from a finite set. Finite sets are even smaller than countable sets. If a random (unknown) quantity has an uncountable number of possible outcomes, for example, the variable can take on any real value between zero and one, then Shannon's results actually show that the outcome cannot be represented with a finite number of bits. This is now obvious. Because there are only countably many finite bit sequences, it cannot be possible to use bit sequences to distinguish values from an uncountable set. There just aren't enough bit sequences.

The total number of possible computer programs is ℵ 0 . The total number of decision functions is bigger, but how much bigger? If it's only slightly bigger, then maybe we haven't lost much by limiting ourselves to what digital computers can do. But it isn't only slightly bigger. It is actually vastly bigger.

First, notice that if we add one element to a countably infinite set, the set does not get any larger. For example, suppose we add the element −1 to ℕ to get the set {−1, 0, 1, 2, 3, · · · }. The resulting set has the same size as ℕ , as we can see by this correspondence:

The correspondence includes all elements of both sets.

By the same reasoning, if we add any finite number of elements to a countably infinite set, the size of the set does not change. What if we add a countably infinite number of elements? Suppose, for example, that we add to ℕ all the elements of = {−1, −2, −3, · · · }. The combined set is the set of all integers, often written . The combined set again has the same size as ℕ ! This correspondence again includes all elements of both sets:

Intuitively, it would seem that we have doubled the size of the set, but actually we haven't changed the size at all. Thus, an uncountable set is more than twice as large as ℵ 0 . But it's even much bigger than that.

The set of rational numbers, it turns out, is also countably infinite. A rational number r is any number that can be written as the ratio of two integers n and d (i.e., as n/d ). To make it easier to find the correspondence, let's restrict ourselves to only positive n and d . We can then form a table that includes every possible rational number as follows:

The ellipsis · · · means simply to continue the pattern horizontally and vertically forever. This table has more entries than there are rational numbers because there are some redundancies. For example, the diagonal elements, 1 / 1, 2 / 2, 3 / 3, and so on, all represent the same rational number 1. But every positive rational number is somewhere in the table.

We can establish a one-to-one correspondence between the entries in this table and ℕ by traversing the table as shown by the arrows below:

If you now follow the arrows in the table, you can see how to「count」the rational numbers, hitting every single rational number in a well-defined order. Following the path of the arrows and eliminating any redundancies as you go, you can establish a correspondence between the set of all positive rational numbers and the set ℕ . Just start at the upper left and associate 1/1 with the natural number 0. Follow the first arrow and associate 2/1 with the natural number 1. Follow the second arrow and associate 1/2 with the natural number 2. Continuing like this, we can associate every positive rational number with a unique natural number. We can then show that the set of all rational numbers, positive and negative, is also countable, using the same trick we used to show that is countable.

A square array like the table above, if it is finite, is equal in size to the square of the number of rows and columns. Ignoring the ellipsis · · · in the table above, there are three rows and three columns, for a total of nine entries, the square of three. Letting the table grow, which is what is implied by the ellipsis, the size of the table will become n 2 , where n is the number of rows and columns. As the table grows to infinity, the number of rows and columns will become ℵ 0 , suggesting that the size of the table should be . However, because the entries in the table are countable, . Thus, intuitively, the size of ℝ and the size of the set of decision functions is larger than the square of ℵ 0 . Put another way, an uncountable set is not only bigger than two infinite sets with size ℵ 0 combined, but it is bigger than the combination of a countably infinite number of countably infinite sets! In fact, it's bigger than any finite power of ℵ 0 . Hence, the set of decision functions really is vastly bigger than ℵ 0 , and there are even bigger sets that are vastly bigger than the set of decision functions.

An obvious question arises: is there any set whose size lies between ℵ 0 and the set of decision functions? Mathematicians usually assume that no such set exists. This hypothesis is called the「continuum hypothesis.」It is unproven and in fact cannot be proven. It must be assumed. In 1939, the Austrian-American mathematician Kurt Gödel proved that the continuum hypothesis cannot be disproved using the accepted axioms of set theory. [7] In 1963, the American mathematician Paul Cohen proved that the continuum hypothesis also cannot be proved from these same axioms. The continuum hypothesis is therefore independent of the axioms of set theory. But regardless of whether we assume the continuum hypothesis, it remains true that any uncountable set has vastly more elements than any countable set.

The proof I gave above that computers cannot solve all decision functions offered just one counterexample, a single decision function C that could not be implemented by any program. The same argument proves that no countable set of programs can realize all decision functions. So this shows that the size of the set of decision functions is strictly larger than the set of programs. The set of decision functions is uncountable and therefore vastly larger than the set of decision functions that can be computed by any computer.

Turing's result, that decision functions exist that are not effectively computable, is one of several results emerging around the same time that crushed the optimism of the previous century. [8] In the face of such results, particularly when viewed through the lens of cardinality, I have to conclude that it is extremely improbable that every interesting information-processing machine is somehow a piece of software. To believe something so improbable in the face of such weak evidence requires a great deal of faith. In chapter 11 , I will show how to systematically use evidence to update our beliefs (using Bayesian reasoning) and why an improbable hypothesis demands stronger evidence.

Fortunately, engineers are not limited to working with software. As described in chapter 6 , cyberphysical systems form a partnership between software and other nonsoftware physical systems. These combined machines offer a vast and largely unexplored landscape for creative designers and inventors. Even more interesting, the partnership between computers and humans has vastly more potential than either alone, as I will argue in the next chapter.

[5] I recommend the wonderfully readable book on this subject by Raymond Smullyan called Satan, Cantor & Infinity (Smullyan, 1992). I first learned from this book that Cantor was trying to show that all infinite sets have the same size when he discovered that they did not.

[6] Although the concept of real numbers is quite old, appearing in the ancient Greek work of Archimedes and Eudoxus, who was a student of Plato's, the modern formalization of the concept is relatively recent, dating to the nineteenth-century work of Weierstrass and Dedekind. It is actually quite a subtle concept. According to Penrose (1989),「to the ancient Greeks, and to Eudoxos in particular, ‘real' numbers were things to be extracted from the geometry of physical space. Now we prefer to think of the real numbers as logically more primitive than geometry.」

[7] Specifically, using the axioms of Zermelo-Fraenkel set theory, from which much of mathematics can be derived.

[8] For a wonderful account of this optimism and its downfall, see Kline (1980).

8.3 势

数学家使用术语「势」表示集合的大小。例如，一个包含两个元素的集合的势为 2。只有当我们考虑有无限个元素的集合时，例如所有计算机程序的集合，这个如此微不足道的概念才会变得有趣。

在上一节的内容中，我向读者阐明至少存在一个决策函数是任何计算机程序都无法实现的。利用康托尔的研究结果，我们可以更有力地证明有无数的决策函数是不能由任何计算机程序来实现的。我们还可以更强有力地证明，不能用计算机程序实现的决策函数要远多于可实现的决策函数。

这个结果主要依赖于康托尔的观察 —— 并非所有无限集合的大小都是相同的。我们用直观的方法表达他的观点，考虑所有的非负整数集合，N={0,1,2,3,…}。符号 N 是这些整数的无限集合的缩写。很明显，这个集合里的整数有很多，实际上是无穷多的。正如集合里的省略号所表示的，其可被读作「等等」。这个集合被称为「自然数」集合，大概是因为有人认为负数和分数有些不太自然吧。

现在我们来考虑所有「实数」的集合，通常它的符号记为 R。这个集合包含 N 的所有元素，但也包含更多的数字。它包括负数、分数和无理数（指不能用分数表示的数字，如 π）。显然，R 是一个比 N 更大的集合。但它到底大了多少呢？

首先，我们需要弄清楚无限集合的大小是什么意思。在康托尔关于无限集合大小的概念中，如果我们可以在 A 和 B 两个无限集合的元素之间定义一个一一对应的关系，则称这两个无限集合 A 和 B 具有相同的大小。一一对应的关系意味着，对于 A 中的每一个元素，我们可以在 B 中指定一个唯一的元素作为它的对应伙伴。例如，考虑集合 N 和另一个集合 M={-1，-2，-3，…}。我们可以建立起一个一一对应的关系，如下所示：

一个集合的每一个元素在另一个集合中都有唯一的伙伴。康托尔的观点认为，如果是这样的话，我们就可以宣称这两个集合具有相同的大小。

有趣的是，我们还可以在集合 N 和它自身的偶整数子集 E={0, 2,4, 6,…} 之间建立起一一对应关系：

尽管第二个集合省略了第一个集合的一半元素，但这两个集合的每个元素都一一对应，因此这两个集合有相同的大小。这种奇异性是无限集合的一个性质。它们的大小与它们自己的许多子集相同。

康托尔用符号 ℵ0 表示集合 N 的大小，其中ℵ是希伯来字母表的第一个字母 aleph。下标 0 表示这是已知的最小无限集的大小。数学家将 ℵ0 读为「alephnull」。

有趣的是，许多集合大小都为 ℵ0，包括自然数 N、整数，甚至有理数。上一节列出的二进制序列的集合，我们称为 B={0, 1, 00, 01,10, 11, 000, …}，其大小也为 ℵ0。希望你能明白如何在这个集合和 N 之间建立一个一一对应关系。

一个大小为 ℵ0 的集合被称为「可数无限集合」，因为它与计数数字 {1, 2, 3, 4, …} 的集合是一一对应的。因此，我们可以对集合里的元素进行「计数」，当然，我们最终会因为它的无限规模而厌倦这样做。

对于任何大小为 ℵ0 的集合，该集合的每个无限子集合的大小也为 ℵ0。因此，所有计算机程序集合的大小都是 ℵ0。这是因为每个计算机程序都在集合 B 中，而这样的程序可能是无限的。

现在事情变得越来越有趣了。我在上一节借鉴了康托尔的对角化方法，他指出存在无数个比 ℵ0 大得多的集合。康托尔还特别证明了实数集合 R 与自然数集合 N 之间不存在一一对应关系。他使用了一个对角参数，类似于我在上一节中所使用的。数学家都说，集合合 R 是「不可数的」。此外，还有更大的无限集合，比如将实数映射到实数的函数集合。

除了 R，还有许多不可数的集合。实际上，上一节讨论的决策函数集合也是不可数的，它的大小和 R 一样。为了证明这一点，我们可以在实数集合和决策函数集合之间建立起一一对应关系。

与集合 N 一样，集合 R 的真子集可能与 R 具有相同的大小。例如，与 0 到 1 之间的实数集合的大小就是相同的。

一个不可数集合严格大于大小为 ℵ0 的集合。由这一结果可知，并不是所有的决策函数都可以由计算机程序来实现，尽管决策函数只涉及二进制数。因为决策函数的集合是不可数的，而计算机程序的集合是可数的，所以后者要小得多。如果决策函数比可判定的函数多，计算机就不是通用的信息处理机。

现在请大家注意，计算机程序也不能实现任何处理实数的机器。因此，如果我们想要将计算机看作通用的信息处理机，那么，我们必须从我们的「信息」概念中排除实数。这一处理方式实在太过激进了，可以说几乎违背离了数学、科学以及工程领域的所有传统。我们不能轻率地接受这一处理方式。

我们简要回顾一下前一章的内容。如果被区分的可选项的数量是有限的，就可以用比特来度量信息。也就是说，以比特度量的信息是从一个有限集合中被选择出来的。有限集合甚至比可数集合还要小。如果一个随机（未知）量的可能结果是不可数的，例如，这个变量可以取 0 到 1 之间的任何实数，那么，香农的结论实际上表明，这个结果不能用有限数量的比特来表示，这一点现在已经非常明显。由于只有一些可数的有限比特序列，所以不能用这些比特序列从不可数的集合中区分一组值，因为确实没有足够的比特序列。

如前所述，可能的计算机程序的总数为ℵ0

。决策函数的总数更大，但是究竟大了多少呢？如果它只是稍微大了一些，那么我们也许并没有因为限制数字计算机能做什么而损失太多。但实际上不只是稍微大了一些，它要大很多。

首先，请注意，如果我们向可数无限集合添加一个元素，该集合不会变得更大。例如，假设我们将元素 - 1 添加到集合 N，并得到一个集合 {-1，0，1，2，3，…}。那么，所得到的集合与 N 具有相同的大小，正如我们从如下对应关系中看到的：

两个集合的所有元素都一一对应。

通过同样的推理过程，如果我们在可数无限集合中添加任意有限数量的元素，那么集合的大小是不会改变的。如果我们添加可数无限数量的元素呢？假设我们将 M={-1, -2, -3, …} 的所有元素添加到集合 N 中，新的组合集合就是所有整数的集合，常记为 Z。然而，组合集合 Z 的大小与 N 的大小仍然是相同的！这种一一对应的关系同样涵盖了两个集合中的所有元素：

直观上看，我们似乎已经把集合的大小增加了一倍，但实际上，我们根本没有改变它的大小。因此，一个不可数集合的大小肯定是ℵ0

的两倍以上。但它甚至比那还要大得多。

实际上，有理数集合也是可数无限的集合。有理数 r 是可以写成两个整数 n 和 d（例如，n/d）之比的任何数。为了更容易找到这种对应关系，我们将 n 和 d 限定为正数。然后我们可以构造一个包含所有可能的有理数的表，如下所示：

此处的省略号指的是在水平、垂直方向上一直延续这个模式。这个表包含了比有理数更多的条目，因为有一些是冗余的。例如，对角线元素，1/1、2/2、3/3 等等，都表示相同的有理数 1。但是，每个正有理数都会在这张表中的某个地方。

以下图中箭头所示的顺序遍历这张表，我们就可以建立表中条目与集合 N 之间的一一对应关系：

如果你现在沿着表中箭头的路径进行观察，就可以看到如何对有理数进行「计数」，并按照定义良好的顺序命中每个有理数。沿着箭头的路径并在前进的过程中消除任何冗余，就可以在所有正有理数集合和集合 N 之间建立起元素的一一对应关系。从左上角开始，将 1/1 与自然数 0 进行关联。沿着第一个箭头，将 2/1 与自然数 1 关联起来。沿着第二个箭头，将 1/2 与自然数 2 相关联。继续下去，我们就可以把每个正有理数和一个唯一的自然数关联起来。然后，用我们证明集合 Z 是可数的相同方法，我们就可以证明所有有理数的集合，包括正的和负的，也都是可数的。

一个与上面的表类似的正方形阵列，如果它是有限的，那么它的大小等于行数或列数的平方。如果我们忽略上表中省略号省略的部分，表中有 3 行 3 列，共有 9 个条目，是 3 列的平方。让这张表不断增长，也就是省略号所表示的，表的大小将变成 n2，其中 n 是行数和列数。当表增长到无穷大时，行数和列数将变成 ℵ0，这意味着表的大小应该是 ℵ20。

但是，由于表中的条目是可数的，所以 ℵ20=ℵ0。因此，直观地看，集合 R 的大小和决策函数集合的大小都大于 ℵ0 的平方。换句话说，一个不可数集合不仅大于两个大小为 ℵ0 的无限集合的总和，而且大于一个可数无限数量的可数无限集合的组合！事实上，它比 ℵ0 的任何有限次幂都要大。因此，决策函数的集合实际上远远大于 ℵ0，而且存在比决策函数集合大得多的更大集合。

一个显而易见的问题出现了：是否存在一个大小介于 ℵ0 和决策函数集合之间的集合呢？数学家通常假设不存在这样的集合。这个假设被称为「连续统假设」，它是未经证明的，事实上也无法被证明。它必须是被假设的。1939 年，奥地利裔美国数学家库尔特·哥德尔证明了连续统假说不能用集合论中的公理来证伪。1963 年，美国数学家保罗·寇恩证明，连续统假说也不能以这些公理加以证明。因此，连续统假说与集合论公理无关。但不管我们是否假设连续统假说，任何不可数集合都比任何可数集合拥有更多的元素，这是一个不争的事实。

我在上面给出的关于计算机不能解决所有决策函数的证明只是给出一个反例，一个不能被任何程序实现的决策函数 C。同样的论据证明，没有一个可数的机器集合能够实现所有的决策函数。这表明，决策函数集合的大小严格大于任何可数集合。决策函数集合是不可数的，因此远大于可被任何计算机计算的决策函数集合。

图灵的结论 —— 存在无法有效计算的决策函数，是几个同时出现的研究结论之一，这些结论粉碎了前一个世纪的乐观情绪。面对这样的结果，尤其是从势的角度来看，我不得不得出结论，从某种程度上讲，每台有趣的信息处理机都不可能是一种软件。然而，面对如此微弱的证据，我们需要极大的信心才能相信这样的结论。

### 8.4 Digital Physics?

Digital physics postulates that nature does not and cannot have a continuous range of possibilities, the total number of possible states that any system can have (including the entire universe) is finite, and physical systems are essentially equivalent to software. Digital physics is a paradigm shift, in the sense of Kuhn, and I hope I am not just one of those opponents who must eventually die so the paradigm can become universally accepted.

If it is true, then the postulate has severe consequences. It means that many of our most cherished ideas of the physical world are wrong, including that space is a three-dimensional continuum and time progresses fluidly from one instant to the next. It means that Newton's laws and Einstein's relativity are are both wrong because both depend on time and space continuums. Of course, as stated by Box and Draper (1987), all models are wrong, but some are useful. By this principle, digital physics must also be wrong. It is a model, a map, not a territory.

For most purposes, digital physics is unlikely to be as useful as models that admit continuity in the physical world. Even if it is finite, the number of states of all but the most tiny systems will be enormous compared with what digital technology can manage today and in the foreseeable future. Nevertheless, the idea of digital physics provokes deep questions about modeling from scientific, engineering, and philosophical perspectives.

From the engineering perspective, digital physics postulates that everything that is possible to make, in principle, can be made with software. It means that dishwashers are, in fact, information-processing machines. It means that the human mind and all of its cognitive functions are, in principle, realizable in software (I will return to this question in section 9.3 in the next chapter). It means that no machine can accomplish what software cannot do, such as computing undecidable functions or working with real numbers. Hence, it is pointless to try to build such machines.

From the scientific perspective, digital physics postulates that nature is extremely constrained, operating within a tiny subset of mechanisms that might have been possible. This tiny subset includes almost none of the physical theories that humans have developed over centuries.

From a philosophical perspective, if the number of states of the universe is finite, then it must be true that (1) the universe must eventually find itself in a state that it has been in before; (2) the universe can only change state a finite number of times in infinite time, so it must effectively stop changing; or (3) time must end. I find all of these possibilities profoundly disturbing.

Perhaps even more disturbing is that it may be impossible to disprove digital physics. Specifically, if we assume that all measurements of the physical world are noisy, then the Shannon channel capacity theorem, equation (4), states that every measurement will convey only a finite number of bits of information. Therefore, any measurement that attempts to show that the number of states of some system is infinite will fail. Hence, by Popper's philosophy of science, digital physics is not scientific because it is not falsifiable. Digital physics becomes a faith.

Digital physics strikes me as far fetched, but most of modern physics is. Most of physics in the universe operates in regimes where our human senses and the intuitions built through them are useless. Our senses and our experience on earth do not give us much intuition to use in understanding black holes and quarks. So by now we should be used to counterintuitive theories. But there is one aspect of digital physics that makes it highly improbable and, hence, extremely surprising. It constrains the universe to operating within a countable and, worse, a finite system. Given that almost all of our deepest and best understanding of the world has come from powerful models of continuums and infinities, for example, Newton's and Leibniz's calculus, to conclude that nature has no need for anything infinite gives pause. It seems like a throwback to preenlightenment days. At a minimum, we should insist on incontrovertible evidence before accepting this. Although the evidence today looks weak to me, quite a consensus has formed among physicists supporting this hypothesis, so the evidence must not look weak to them. In chapter 11 , I will explain exactly what I mean by「evidence,」but for now let's just examine what digital physics means and why it is so improbable.

Digital physics has several variants, some of which are bizarre. The variants can be put in order from weakest to strongest as follows:

In its weakest form (fewest assumptions), digital physics asserts that the number of possible states of any system in nature with finite energy and volume is finite. If this is the case, then the state of any such system can be completely encoded with a finite number of bits.

A slightly stronger form asserts that the physical world is essentially informational. Every process is an information transformation, and every object in the world is essentially a bundle of information. Digital physics further asserts that information can be measured in bits.

In a stronger form, digital physics assumes that every physical process is essentially a computation, representable in principle as software. This requires that processes in nature be algorithmic, proceeding as step-by-step operations.

In a still stronger form, digital physics assumes that the physical world is essentially a computer.

In the strongest form that I have seen, digital physics asserts that the physical world is a simulation carried out by a computer.

In my opinion, these philosophies are confusing the map with the territory. Are they talking about models of reality or about reality? [9]

A supporter of at least the weaker forms of digital physics was the Mexico-born Israeli-American theoretical physicist Jacob Bekenstein, who was a professor at the Ben-Gurion University and then the Hebrew University in Israel until his unexpected death in 2015. Bekenstein and his colleagues developed what is now called the「Bekenstein bound,」an upper limit on the entropy that can be contained within a given finite volume of space that has a finite amount of energy (see Freiberger [2014] for a short readable summary). If we assume that the form of entropy that Bekenstein considered is discrete entropy, explained in the previous chapter, then the Bekenstein bound shows that the amount of information, measured in bits, that can be stored in a given volume of space is limited. Equivalently, the bound shows that anything occupying a given volume of space can be completely described, down to the quantum level, with a finite number of bits. I will call this the「digital interpretation of Bekenstein's bound.」Under this interpretation, the first form of digital physics listed previously follows immediately. An alternative nondigital interpretation of the Bekenstein bound using continuous entropy appears to be consistent with Bekenstein's original formulation (Bekenstein, 1973), but this is not the interpretation adopted by most physicists today.

So under the digital interpretation, how many bits can we store in a given space? James Redford, who also claims that modern physics proves the existence of God, in a 2012 paper uses the Bekenstein bound to calculate the number of bits required to encode a human being (Redford, 2012, p. 126). He concludes that an adult human male can be encoded in 2 × 10 45 bits. My laptop's hard disk can store one terabyte, or 10 12 bytes, or roughly 10 13 bits. So I would need 10 32 such laptops to store this many bits. This is 10 32 :

100,000,000,000,000,000,000,000,000,000,000.

If Moore's law continues unabated and we assume it applies to memory storage devices, then in only about 130 years, we may have a computer with this much memory. Such is the power of Moore's law, which predicts a doubling of the number of transistors on a chip every two years.

Although the digital interpretation of Bekenstein's bound seems to be widely accepted among physicists today, I remain stoically skeptical, an admittedly lonely position. I do not doubt Bekenstein's result that entropy in a volume of space is limited and finite. What I doubt is that Bekenstein's entropy is discrete entropy, and hence represents information that can be encoded in bits. Bekenstein's arguments seem to work just as well using continuous entropy, explained in section 7.4 of the previous chapter. It is a mistake to give a digital interpretation to continuous entropy. The continuous entropy in a system does not tell us how many bits it takes to encode that system, although it does quantify information content. If we are using continuous entropy, the system cannot be encoded with a finite number of bits. The system nevertheless has information, and its information content can be compared with the information content in other continuous systems.

Ludwig Boltzmann and his contemporaries defined the thermodynamic entropy in a macroscopic system, such as a volume of gas, by the formula k log( M ), equation (32) on page 133 . In the usual explanations, M is the number of states that the microscopic system, consisting of the individual molecules in the gas, can be in such that the macroscopic state (volume, pressure, mass, and temperature) are as observed. The scaling constant k is called the Boltzmann constant, and it simply changes the units that we are using to measure entropy. This explanation assumes that the M states are all equally likely and that the number of such states is finite . To interpret this as equivalent to bits in discrete entropy, we have to assume that molecules can only have a finite number M of possible states. This assumption is a form of digital physics. Hence, to interpret thermodynamic entropy as a measure of information in bits, we have to first assume that digital physics is true. To then use the Bekenstein bound to prove digital physics is a logic error. There may be other reasons that the number of states is finite, but the reason cannot be that the entropy is finite.

The error here is subtle but important. Boltzmann couldn't have known how many possible states the microsystem could have that were consistent with an observed macrostate. Boltzmann wanted to model the state of a molecule by its position and velocity (or momentum). In Boltzmann's time, these would have been continuous random quantities, so the entropy should be more properly interpreted as continuous entropy. Today, the number of possible states is understood to be determined by quantum mechanics, which had not been developed in Boltzmann's day. In an alternative explanation, M is a stand-in for relative degrees of freedom. It was common in classical thermodynamics, before quantum mechanics, to replace M with a number proportional to the number of molecules in the volume of gas being considered. In this case, the entropy has an arbitrary offset, but as long as the same offset is used for any two entropies, it remains valid to compare entropies. But the absolute value of the entropy loses any physical meaning.

After Boltzmann, formulas for entropy have been improved by physicists to take into account more knowledge of the underlying physics, including quantum effects, and thereby acquire more direct physical meaning. An example is the so-called Sackur-Tetrode equation for the entropy in an ideal gas, derived in the early 1900s, which has both classical and quantum mechanical aspects. I will spare you the details, but Wikipedia provides a starting point if you are interested. This equation, however, must be a continuous entropy measure, not discrete entropy, because it does not constrain the entropy to be positive, and it sets the entropy at minus infinity when the temperature gets to absolute zero. A physicist would likely tell you that the equation becomes invalid at low temperatures, where the approximations used to derive the equation are no longer accurate. This may be true, but if this is a continuous entropy, then it is a mistake to read it as a number of bits of information at any temperature. This landscape underscores the difficulty in keeping straight whether a discussion of entropy is talking about discrete or continuous entropy. The two are not comparable.

If in fact a physical system has an infinite number of possible states consistent with the observations, and if the probability density function for these states is known, then in fact we can define a continuous entropy for the system, and the number does have physical meaning, as shown in section 7.4 of the previous chapter. This entropy quantifies information content, just like discrete entropy, but the information cannot be encoded in bits. An infinite number of bits would be required, just as an infinite number of bits is required to encode a real number, even though the number is finite. If, further, the probability density function is uniform, as depicted in figure 7.1 , then the form of expression for continuous entropy will be exactly k log 2 ( M ), where M now is simply the height of the probability density function. So Boltzmann's formulation works fine even if the number of states is not finite, as long as all the states are equally likely.

Entropy is the central concept in the second law of thermodynamics, which states that entropy increases in any system (or at least does not decrease). So the second law of thermodynamics is all about comparing entropies, and not at all about their absolute values, so it is completely unaffected by whether we interpret entropy as a measure of information in bits. It is even unaffected by the arbitrary offset that results if we do not know the probability density function for the states. The second law of thermodynamics works just as well with continuous entropy as with discrete entropy. To give a digital interpretation to entropy, to measure it in units of bits, we need to assume that the number of possible states of a molecule is finite . We have to assume digital physics.

Too many physicists seem to assume that the word「entropy」automatically means discrete entropy. Seth Lloyd, a professor of mechanical engineering and physics at MIT, in his 2006 book Programming the Universe , does this repeatedly. He says about the second law,

It states that each physical system contains a certain number of bits of information—both invisible information (or entropy) and visible information—and that the physical dynamics that process and transform that information never decrease that total number of bits. (Lloyd, 2006)

But the second law works absolutely unmodified if the underlying random processes are continuous, in which case the information is not representable in bits. Other principles in physics may result in bits, and Lloyd argues strongly that quantum mechanics does this. However, a physical system can have a finite entropy and still not be representable in bits if that finite entropy is a continuous entropy.

Lloyd defines entropy digitally, saying,「entropy is a measure of the number of bits of unavailable information registered by the atoms and molecules that make up the world.」And「the quantity called entropy is proportional to the number of bits required to describe the way atoms are jiggling.」But continuous entropy is still entropy, and it is not a measure in bits. Lloyd then makes an extraordinary claim that「as the statistical mechanicians of the late nineteenth century showed, the world is made up of bits.」Those statistical mechanicians, Boltzmann and his contemporaries, had never heard of bits, and their theories work fine with continuous entropy.

Lloyd has other reasons for assuming that the physical world is digital. In Programming the Universe , he argues that the universe is in fact a type of computer known as a「quantum computer.」Although the relationship between quantum computers and Turing computation is far from trivial, Lloyd's position is strongly in favor of digital physics at least to the level that everything in the world is digital. However, it is highly misleading to claim that a finite entropy implies that the world is digital.

Quantum computers are based on quantum mechanics, which emerged well after the work of the statistical mechanicians of the late nineteenth century. Quantum mechanics replaces the notions of position and momentum, which those mechanicians would have used, with a「wave function,」which relates position and momentum probabilistically. The wave function involves continuous variables and has an offset in space, effectively a position. Is the number of possible offsets of the wave function finite?

Digital physics rests on a principle that for any physical system with well-defined boundary conditions, only a finite number of wave functions that constitute the system are possible. But how to model these boundary conditions is quite subtle. If we are talking about a chamber of gas, as Boltzmann was, then aren't the walls of the chamber properly modeled as wave functions interacting with those of the gas molecules? If so, then the enclosure must be considered part of the system rather than a boundary condition, but so must the environment around the enclosure, and the environment around that. If we assume that ultimately the universe is finite in extent and age, then we eventually get well-defined boundary conditions. But it boggles my mind to rely on the finite scale of the universe to describe behaviors at the subatomic scale where quantum mechanics applies. Even the tiniest approximations or the use of statistical arguments in any calculations that span such a range of values would invalidate the conclusions, and entropy calculations are rife with approximations. But the physicists know more about this than I do, so I will have to take their word for it. Ultimately, the conclusion that the number of states is actually finite seems to depend on models that I do not understand, have not been validated experimentally, and cannot be falsified.

Shannon did show that if an observation of a continuous variable is imperfect (it is noisy), then the information conveyed by the observation can be measured in bits and is finite. This is the channel capacity theorem, equation (4) in the previous chapter. However, the quantity of information observed is not equal to the entropy in that continuous variable, which is finite but not measured in bits. The entropy of a continuous variable is a continuous entropy. The fact that a noisy observation of a continuous random variable conveys only a finite number of bits is a consequence of the relative entropy before and after observation. This was Shannon's most profound observation. He showed that the information capacity of any noisy communication channel is finite and measurable in bits.

Nevertheless, perhaps digital physics can be salvaged by assuming that observations are always noisy and the information conveyed is all the information that is relevant. Shannon did not show that the information contained in the variable is finite, only that the information conveyed is finite. In fact, the information contained would require an infinite number of bits to encode. Shannon showed that it is not possible to perfectly reconstruct the value of a continuous variable from a noisy observation. To salvage digital physics, we could assume that any information that fails to be conveyed by a noisy observation is not relevant information. This is equivalent to assuming digital physics. We have to assume digital physics to prove digital physics.

This question of information conveyed versus information contained is a deep and difficult question. Is it possible for a physical system to have information that is not externally observable at all but is nonetheless essential to the system? I briefly addressed this question in section 8.2 , where I lamented that, as a teacher, I am unable to convey all the information I carry in my brain. I will return to this question when I consider the human brain and cognition in chapter 9 , but ultimately, I believe that even information that is not conveyed is still relevant.

The way Bekenstein developed his bound is an interesting story. He worked with physicist Stephen Hawking on a problem that black holes seem to defy the second law of thermodynamics by swallowing up entropy. To salvage the second law of thermodynamics, Bekenstein and Hawking associated the surface area of the event horizon of a black hole with entropy. Nobody before Bekenstein and Hawking had thought that a surface area of anything had anything to do with entropy, but this association resolved the problem, saving the second law.

The bound also depends on the theory of quantum gravity, an effort to reconcile quantum mechanics with Einstein's general theory of relativity. Neither this nor equating surface area with entropy is without controversy, and neither has had any experimental observation. For me, accepting Bekenstein's bound requires a great deal of faith in physics that is difficult if not impossible to fully understand and may be beyond the reach of experimental observation. Even Hawking, one of the most widely recognized and respected physicists today, expresses doubt, pointing out that the digital interpretation of the bound is inconsistent with most of modern physics. Hawking notes that continuums are required in both time and space for the bedrock of quantum mechanics, the Schrödinger equation, resulting in「an infinite density of information which is not allowed」(Hawking, 2002). Unless you assume that the number of possible states is finite, the Bekenstein bound talks about continuous entropy, not entropy in bits, and the contradiction evaporates.

At this time, there is no experimental confirmation of a digital and quantized nature of the universe, both needed for digital physics. Experiments in progress are looking for such confirmation. One is the Fermilab Holometer near Chicago that is intended to be the world's most sensitive laser interferometer, more sensitive than LIGO (see chapter 1 ). According to Wikipedia, the principal investigator on this project, Craig Hogan, states,

We're trying to detect the smallest unit in the universe. This is really great fun, a sort of old-fashioned physics experiment where you don't know what the result will be. [Wikipedia page on Holometer, Retrieved May 24, 2016]

The experiment started collecting data in August 2014, and as of August 2016 has no major results yet. Worse, even if it gets results, if there is any noise at all in the measurements, then Shannon's channel capacity theorem tells us that the measurements can only convey a finite number of bits of information, even if the underlying system has an infinite number of bits of information.

I am not a physicist, so you should take my skepticism with a grain of salt, but I have to say I would be extraordinarily surprised if digital physics is valid. It reads more like a cult than a science to me. If it is valid, then nature has its hands tied indeed. For some reason, nature has restricted itself to operating within only a finite number of possibilities. Why would nature do that? Although my skepticism seems to be a minority opinion, I am not entirely alone.

Sir Roger Penrose, an English physicist, mathematician, and philosopher, in his controversial book The Emperor's New Mind , states,

The belief seems to be widespread that, indeed,「everything is a digital computer.」It is my intention, in this book, to try to show why, and perhaps how, this need not be the case. (Penrose, 1989, p. 30)

Penrose goes on to argue that consciousness, a naturally occurring process in the physical world, is not only not a computation but is not even explainable using the known laws of physics.

Gualtiero Piccinini, a philosopher at the University of Missouri, observes,

· · · from the point of view of strict mathematical description, the thesis that everything is a computing system · · · cannot be supported. (Piccinini, 2007)

Piccinini, like me, defends this idea using the notion of cardinality. There just aren't enough possible computations to encompass the richness of the physical world.

Digital physics cannot be disproved, assuming all measurements have noise, so this issue may never be resolved. It will probably always remain a matter of faith. My faith is that nature is more likely to be richer in possibilities than poorer. The tiny cardinality of a digital universe just seems too small to me.

[9] The existence of a reality independent of humans is not a universally accepted truth. Philosophers call this assumption「realism,」and for the purposes of this argument, it is a position I will adopt.

8.4 数字物理学？

数字物理学假定，自然界中不存在也不可能存在一组可能性的连续范围，任何系统（包括整个宇宙在内）所拥有的可能状态总数是有限的，并且物理系统在本质上等同于软件。从库恩的观点来看，数字物理学是一种范式转换。我希望我自己不是那些为了让这种范式得到普遍接受而必须最终死去的反对者之一。

如果这是真的，那么这个假设会产生严重的后果。这意味着我们对物理世界的许多最令人珍视的想法都是错误的，包括空间是一个三维连续统，时间从一个瞬间流动到另一个瞬间，等等。这意味着牛顿的那些定律以及爱因斯坦的相对论都是错误的，因为它们都依赖于时间和空间的连续性。当然，正如博克斯和德雷珀（1987）所述，所有的模型都是错误的，但也有一些是有用的。根据这一原则，数字物理学也必定是错误的。因为它是一个模型，是一张地图，而不是真正的地域。

在大多数情况下，数字物理学不太可能像接纳物理世界连续性的模型那样有用。即使假设物理世界的状态是有限的，所有系统（除了最微小的系统）的状态数量都远远超过数字技术在目前以及可预见的未来所能管理的状态数量。尽管如此，数字物理学的概念还是从科学、工程和哲学的角度引发了关于建模的深层次问题。

从工程学的角度来看，数字物理学假定一切可能被制造的东西原则上都可以用软件来实现。这其实就等于说，洗碗机实际上就是信息处理机。这意味着，人类的心智及其所有认知功能原则上都可以在软件中实现（我将在下一章的 9.3 节讨论这个问题）。换言之，任何机器都不能完成软件不能完成的那些工作，例如计算不可判定的函数或处理实数。因此，试图构造这样的机器是毫无意义的。

从科学的角度来看，数字物理学假设大自然是极其有限的，在可能存在的极小的机制子集中运行。这个极小的子集几乎不包括人类几个世纪以来发展起来的物理理论。

从哲学的角度来看，如果宇宙的状态数量有限，那么下面几种情形一定成立：（1）宇宙最终会被发现处于其曾经所处的状态中；（2）宇宙在无限时间内只能改变有限次数的状态，所以它必须有效地停止变化；或者，（3）时间必须结束。

也许更令人不安的是，要证伪数字物理学是不可能的。具体来说，如果我们假设物理世界中的所有测量都是有噪声的，那么香农的信道容量定理，即方程（4），表明每一个测量都只能传递有限数量的比特信息。任何试图表明某个系统的状态无限的测量都将失败。因此，根据波普尔的科学哲学观点，数字物理学不是科学，因为它是不可证伪的。这样一来，数字物理学就变成了一种信念。

数字物理学在我的印象里是遥不可及的，但实际上，大多数现代物理学也都如此。宇宙中的大多数物理现象都是在人类通过这些现象建立起来的、感觉和直觉上毫无用处的范畴中运行的。我们在地球上的感觉和我们的经验并没有给我们太多的直觉去理解黑洞和夸克这样的物理现象。因此，到目前为止，我们现在应该习惯于反直觉的理论。但是，数字物理学的一个方面使其极不可能，这也令人非常惊讶。它将宇宙限定在一个可数的、有限的系统中运行。鉴于我们对世界最深刻和最好的理解几乎都来自连续统和无穷性的强大模型，例如牛顿和莱布尼茨的微积分，因此，我们可以得出这样的结论：大自然是无穷无尽的，它不需要任何给出停顿的东西。得出这样的结论，似乎是倒退到了启蒙运动前的时代。至少，在接受这一观点之前，我们应该坚持要有无可辩驳的证据。虽然今天的证据在我看来还不够充分，但支持这一假说的物理学家已经形成了相当的共识，在他们看来，已有的证据并不是那么羸弱。在第 11 章中，我将确切地解释我所说的「证据」是什么意思，但现在让我们来看看数字物理学到底意味着什么，以及为什么它是如此不可能。

数字物理学有好几个变体，其中的一些有些奇怪。如下所述，以从弱到强的顺序给出了这些变体。

1、在其最弱的形式中（最小假设），数字物理学断言，自然界中任何具有有限能量和体积的系统的可能状态数都是有限的。如果是这样的话，那么任何该类系统的状态都可以用有限数量的比特进行完全编码。

2、在一种稍强一些的形式中，数字物理学断言，物理世界本质上是信息化的。每一个过程都是一次信息转换，世界上的每一个实体物本质上都是一束信息。其进一步断言，信息可以用比特来度量。

3、在一种强大的形式中，数字物理学假设每个物理过程在本质上都是一个计算，原则上可以用软件来表示。这就要求这些过程在本质上是算法式的，以逐步运算的方式进行处理。

4、在一个更强的形式中，数字物理学假设物理世界本质上就是一台计算机。

5、在我所见过的最强大的形式中，数字物理学断言物理世界是由计算机进行的模拟。

在我看来，上述这些观点都把地图和地域混为一谈了。它们谈论的是现实的模型还是现实本身呢？墨西哥以色列裔美国理论物理学家雅各布·贝肯斯坦至少是上述第二种数字物理学观点的支持者。他曾是以色列本·古里安大学和希伯来大学的教授，直到 2015 年意外去世。贝肯斯坦和他的同事提出了现在被称为「贝肯斯坦上限」的概念，这是在具有有限能量的有限体积空间内所能包含的熵的上限［参见弗赖伯格（2014）简短易读的摘要］。如果我们假设贝肯斯坦所考虑的熵的形式是离散熵（在前一章已做解释），那么贝肯斯坦上限表明，在给定体积的空间中，可以存储的以比特为单位的信息量是有限的。换言之，这个上限表明，任何占据给定空间的事物都可以用有限的比特数进行完全描述，直到量子级别。我将这称为「对贝肯斯坦上限的数字化解释」。根据这一解释，之前列出的第一种数字物理学形式就会随之成立。另一种基于连续熵对贝肯斯坦上限的非数字化解释似乎与贝肯斯坦最初的公式相一致（贝肯斯坦，1973），但这并非今天大多数物理学家普遍采用的解释。

那么，在这个数字化的解释下，在一个给定的空间里我们到底能存储多少比特呢？詹姆斯·雷德福德声称，现代物理学证实了上帝的存在。他在 2012 年发表的一篇论文中利用贝肯斯坦上限来计算编码一个人所需要的比特数（雷德福德，2012:126）。他的结论是，编码一个成年男性需要 2×1045 比特。我的笔记本电脑硬盘可以储存 1T 字节，或者 1012 字节或大约 1013 字节。因此，我需要 1032 台这样的笔记本电脑才能储存下这么多的比特。下面这串数字就是 1032：

100 000 000 000 000 000 000 000 000 000 000

如果摩尔定律继续有效的话，我们假设它适用于内存存储设备，那么只有在 129 年之后，我们也许才会拥有一台具有这么多内存的计算机。这就是摩尔定律的魔力，它预测每块芯片上的晶体管数量每两年会翻一番。

尽管对贝肯斯坦上限的数字化解释似乎在当前的物理学家中得到了广泛的认可，但是我仍然对其持严重怀疑的态度，这是一个公认的少数人的立场。我并不怀疑贝肯斯坦的结论，即一个空间内的熵是受限制的和有限的，我所怀疑的是，贝肯斯坦的熵是离散熵，因此，其代表了可以用比特进行编码的信息。贝肯斯坦的论据似乎与 7.4 节使用连续熵的论据同样有效。然而，对连续熵的数字化解释是错误的。尽管系统中的连续熵确实可以对信息量进行量化，但它并不能告诉我们究竟需要多少比特才能编码该系统。如果我们使用连续熵，系统就不能以有限的比特进行编码。然而，这个系统是有信息的，而且它的信息量可以和其他系统的量进行比较。

路德维希·玻尔兹曼和他同时代的人用宏观系统定义热力学的熵，例如气体的体积，并用公式 klog(M)［方程（32）］进行计算。通常的解释是：在观察由气体中单个分子所组成的微观系统的宏观状态（体积、压力、质量和温度）时，该微观系统所处的状态数就是 M。比例常数 k 被称作玻尔兹曼常数，它只是改变了我们用来度量熵的单位。这一解释假定处于这 M 个状态之一的可能性是相同的，并且这种状态的数量是有限的。为了将其解释为等同于离散熵中的一组比特，我们必须假定分子只有 M 个有限数量的可能状态。这种假设是数字物理学的一种形式。因此，要将热力学熵解释为以比特度量的信息，我们就必须首先假设数字物理学是正确的。然后，再用贝肯斯坦上限证明数字物理学是一个逻辑错误。也许还有其他理由可以解释系统的状态数是有限的，但是绝不可能包括熵是有限的这个理由。

这里的错误很微妙，但也很重要。玻尔兹曼不可能知道微系统有多少可能的状态与所观察到的宏观状态一致。玻尔兹曼希望通过分子的位置和速度（或动量）模拟分子的状态。在玻尔兹曼的时代，这些都是连续的随机量，所以熵应该被更恰当地解释为连续熵。今天，可能的状态数被认为是由量子力学决定的，而量子力学在玻尔兹曼的时代还没有发展形成。另外一种解释是，M

是相对自由度的代名词。在量子力学出现之前，经典热力学常用一个与给定气体体积中的分子数成正比的数来代替 M。在这种情况下，熵的值具有一个任意的偏移量，然而，只要对任意两个熵使用相同的偏移量，对两个熵的比较仍然有效。但此时，熵的绝对值失去了任何物理意义。

在玻尔兹曼之后，物理学家一直对计算熵的公式进行改进，考虑了更多的基础物理学知识，包括量子力学效应，从而获得了更直接的物理意义。其中一个例子就是 20 世纪早期推导出的萨克尔 — 泰特洛德方程，用以计算理想气体中的熵。该方程同时具有经典力学和量子力学的特性。这里，我就不再过多解释了，如果读者对此感兴趣，可以去维基百科查阅相关资料。然而，这个方程必须是对连续熵的测量，而非离散熵。这是因为，该方程并没有限定熵一定是正值，而且当气温达到绝对零度时，该方程将熵的值设定为负无穷大。物理学家也许会告诉你，这个方程在低温下就失效了，原因在于，用于推导这个公式的近似值不再是精确的。这也许是对的，但如果这是一个连续熵，那么将它理解为在任意温度状态下的信息的比特数就是错误的。这一情形凸显了明确讨论的熵是离散熵还是连续熵所面临的困难。这两种熵是不可比较的。

实际上，如果一个物理系统具有无限多与观测相一致的可能状态，且这些状态的概率密度函数是已知的，那么我们为这个系统定义一个连续熵，而且它的值确实具有物理意义，如 7.4 节所述。就像离散熵一样，这种熵可以量化信息量，但是信息不能编码为比特。正如要编码一个实数（即便这个数是有限的）一样，这也会需要无限数量的比特。进一步来说，假如概率密度函数是均匀的，如图 7.1 所示，那么连续熵的表达形式就一定是 klog2(M)，其中 M 是概率密度函数所具有的高度。因此，即使状态数不是有限的，只要所有的状态的可能性相同，玻尔兹曼公式就是适用的。

熵是热力学第二定律的核心概念，其表明熵在任何系统中都将增大（或者至少不会减少）。所以，热力学第二定律是有关于比较熵的定律，而非有关其绝对值的定律，由此，无论我们是否将熵解释为比特方式的信息度量，它都不会受影响。如果我们不知道这些状态的概率密度函数，那么该定律甚至不会受任意偏移的影响。热力学第二定律适用于连续熵和离散熵两种情况。为了对熵给出一个数字化的解释，也为了能用比特度量熵，我们需要假设一个分子的可能状态数是有限的，我还需要假定数字物理学是有效的。

太多的物理学家似乎都认为「熵」这个词自然就是指离散熵。麻省理工学院机械工程和物理学教授塞思·劳埃德在他 2006 年出版的《编程宇宙》（Programming the Universe）一书中，就重复了这个做法。其中有如下一段关于第二定律的文字：

热力学第二定律表明，每个物理系统包含一定数量比特的信息 —— 其中包括不可见的信息（或熵）以及可见的信息 —— 而且，处理和转换这些信息的物理动力学并不会减少总的比特数。（劳埃德，2006）

但是，如果潜在的随机处理过程是连续性的，在这种情况下，信息不能用比特来表示，那么热力学第二定律绝对不会被修改。物理学中的其他原理可能会产生比特，劳埃德坚定地认为量子力学可以做到这一点。然而，一个系统可以有一个有限的熵，但如果有限的熵是一个连续熵，那么它仍然不能用比特来表示。

劳埃德用数字方式对熵进行了定义。他说：「熵是对不可用信息世界的一种比特数度量…… 由构成世界的原子和分子记录。」他还说：「熵这个量与描述原子运动的方式所需的比特数成正比。」但是连续熵仍然是熵，它不是以比特为单位的一个度量。进而，劳埃德提出一个非同寻常的主张：「正如 19 世纪末的统计物理学家所表明的，世界是由比特组成的。」一方面，那些统计物理学家，如玻尔兹曼和他的朋友们从未听说过比特，另一方面他们的理论对于连续熵运行良好。

劳埃德还有其他一些理由假设物理世界是数字化的。在《编程宇宙》一书中，他认为宇宙实际上是一种被称为「量子计算机」的计算机。虽然量子计算机和图灵计算之间有一定联系，但是劳埃德阐明了自己的立场，他强烈支持数字物理学，并认为世界上的一切事物至少都达到了一定的数字化水平。然而，声称有限的熵意味着这个世界是数字化的，这种观点是非常有误导性的。

量子计算机是以量子力学为基础的，后者是在 19 世纪末统计物理学家大量的研究工作之后才出现的。量子力学用「波函数」取代了机械学家所使用的位置和动量的概念，该函数以概率的方式将位置和动量关联起来。波函数包含一组连续变量，同时在空间上有一个偏移量，也就是一个位置。好了，现在的问题是，波函数的可能偏移数是有限的吗？

数字物理学基于这样一个原理：对于任何具有明确边界条件的物理系统，只可能用有构成该系统的、有限数量的波函数。但是如何建模这些边界条件却是非常棘手的事情。如果我们谈论的是一个气体室（就像玻尔兹曼那样），那么气体室的壁面是否被建模为与气体分子相互作用的波函数？如果是的话，那么我们必须将气体室的壳体视为系统的一部分而不是一个边界条件，但该壳体及其周围环境以及周边环境都必须被视为系统的一部分。如果我们假设宇宙在范围和时间上最终是有限的，那么我们最终也能够得到明确的边界条件。但是，依靠宇宙的有限尺度来描述运用量子力学的亚原子尺度的行为，让我感到非常不可思议。即使是最微小的近似值，或者在跨越这样一个数值范围的任何计算中使用统计参数，也会使结论无效，而我们知道，熵的计算中充斥着近似值。但是，物理学家比我更了解这一点，所以我不得不相信他们的话。最终，状态数实际上是有限的这一结论似乎依赖于我不太理解的一些模型，它们还没有经过实证验证，也不能被证伪。

香农确实证明了，如果对一个连续变量的观测是不理想的（是有噪声的），那么观测所传递的信息就可以用比特来度量，并且是有限的。这是前一章信道容量定理及方程（4）的含义。然而，观测到的信息量并不等于该连续变量中的熵，它是有限的，但不能用比特来度量。连续变量的熵是连续熵。连续随机变量的有噪声观测只传递有限数量的比特，这是观测前后的相对熵结果。这是香农最深刻且意义深远的观测。他指出，任何有噪声的通信信道的信息容量都是有限的，并且可以用比特来度量。

然而，通过假设观测总是有噪声的，且所传递的信息全部都是相关的，这样做或许还可以挽救数字物理学。香农并没有表明变量中包含的信息是有限的，只是表明变量所传递的信息是有限的。事实上，其所包含的信息需要无限比特来进行编码。香农证明，从一个有噪声的观测中完全重构一个连续变量的值是不可能的。为了挽救数字物理学，我们可以做出这样的假设 —— 任何无法通过带噪声观测传递的信息都是不相关的信息。这就相当于假设数字物理学是有效的，我们必须假设数字物理学的有效性，以证明数字物理学的存在是有效的。

关于所传递的信息与所包含的信息的问题是一个深刻而困难的问题。一个物理系统是否可能拥有外部根本无法观察到的却对该系统来说至关重要的信息？我曾在 8.2 节中简要地提到这个问题。在那里我曾遗憾地说，作为一名教师，我无法传递我大脑中的所有信息，我会在第 9 章探讨人类的大脑和认知时再次回到这个问题上。但我最终还是相信，即使是没有被传递出去的信息也是有关的。

贝肯斯坦发展他的上限理论的过程是一个有趣的故事。他和物理学家斯蒂芬·霍金一起研究一个问题，即通过吞噬熵，黑洞似乎会违背热力学第二定律。为了挽救热力学第二定律，贝肯斯坦和霍金将黑洞事件视界的表面积与熵联系起来。在贝肯斯坦和霍金之前，没有人认为任何物体的表面积会与熵有任何关系。但是，这种关联解决了这个棘手的问题，并且挽救了热力学第二定律。

这一上限还取决于量子引力理论，这是为了调和量子力学与爱因斯坦的广义相对论所做的努力。无论是这种联系还是将表面积与熵关联在一起都不是没有争议的，两者也都没有任何实验观察。因此，对我来说，要接受贝肯斯坦上限理论需要对物理学有极大的信心，这种信念是很难被完全理解的（如果不是不可能的话），而且可能已经超出了实验观察的范围。即便是霍金，作为当今最广为人知和最受尊敬的物理学家之一，也对此持怀疑态度。他指出，对上限的数字化解释与大多数现代物理学是不一致的。霍金还指出，连续统在时间和空间上都是量子力学的基石 —— 薛定谔方程 —— 所必需的，从而产生了「未被允许的信息的无限密度」（霍金，2002）。除非你假设可能的状态数是有限的，否则贝肯斯坦上限理论讨论的就是连续熵，而并非以比特计量的熵，这样，矛盾就被化解了。

此时，宇宙的二元性和量子化性质尚未得到实验证实，这两个特性都是数字物理学所需要的。正在进行中的实验一直在寻找这样的实证。其中一个是芝加哥附近费米实验室的高度计，这是世界上最灵敏的激光干涉仪，比激光干涉引力波天文台的探测器还要灵敏（详见第 1 章）。根据维基百科，这个项目的主要负责人克雷格·霍根认为：

我们正在试图探测宇宙中最小的单位。这种探索真的很有意思，一种老式的、你不知道结果是什么的物理实验。（维基百科网页上的全息图，2016 年 5 月 24 日检索）

该实验于 2014 年 8 月开始收集各种数据，截至 2016 年 8 月尚未取得任何重大成果。更糟糕的是，即使它得到了结果，如果在这些测量中存在任何噪声，就像香农的信道容量定理告诉我们的那样，那么即使系统潜藏着无限比特数量的信息，这样的测量也只能传递有限比特数量的信息。

我并不是一位物理学家，所以你完全可以对我的质疑持怀疑态度。但我不得不说，如果数字物理学有效的话，我会感到异常惊讶。它对我而言更像是一种邪教，而不是一种科学。如果它是有效的，大自然的确就被束缚了手脚。出于某种原因，大自然会限定自己仅在有限的可能性中运行。可是，大自然为什么要这样做？虽然我的怀疑似乎只是少数人的观点，但并不完全只有我一个人这样想。

英国物理学家、数学家和哲学家罗杰·彭罗斯爵士在他那本颇具争议的著作《皇帝新脑》中写道：

「一切都是数字计算机」的信念似乎已经广为流传。在这本书中，我的目的是试图说明为什么，以及可能的话，是如何，真实情况未必如此。

（彭罗斯，1989:30）

彭罗斯继续论证意识，一个在物理世界中自然发生的过程，不仅不是一种计算，甚至不能用已知的物理定律来解释。

密苏里大学的哲学家瓜蒂耶罗·皮奇尼尼认为：

从严格数学描述的角度看，任何事物都是一个计算系统…… 这一论题是不能被支持的。（皮奇尼尼，2007）

像我一样，皮奇尼尼使用势的概念为这个观点进行辩护。他的结论是，没有足够多的可能的计算去涵盖物理世界的丰富性。

数字物理学不能被推翻，且假设所有的测量都是有噪声的，那么这个问题就可能是永远无法解决的。这可能永远都是一个信念问题。我的信念是，大自然更有可能在各种可能性中变得丰富而不是贫乏。在我看来，数字宇宙那微小的势值实在是太小了。

# 2020112Clean-ArchitectureR01

## 记忆时间

## 0200. Starting with the Bricks: Programming Paradigms

Software architecture begins with the code — and so we will begin our discussion of architecture by looking at what we’ve learned about code since code was first written.

In 1938, Alan Turing laid the foundations of what was to become computer programming. He was not the first to conceive of a programmable machine, but he was the first to understand that programs were simply data. By 1945, Turing was writing real programs on real computers in code that we would recognize (if we squinted enough). Those programs used loops, branches, assignment, subroutines, stacks, and other familiar structures. Turing’s language was binary.

Since those days, a number of revolutions in programming have occurred. One revolution with which we are all very familiar is the revolution of languages. First, in the late 1940s, came assemblers. These「languages」relieved the programmers of the drudgery of translating their programs into binary. In 1951, Grace Hopper invented A0, the first compiler. In fact, she coined the term compiler. Fortran was invented in 1953 (the year after I was born). What followed was an unceasing flood of new programming languages—COBOL, PL/1, SNOBOL, C, Pascal, C++, Java, ad infinitum.

Another, probably more significant, revolution was in programming paradigms. Paradigms are ways of programming, relatively unrelated to languages. A paradigm tells you which programming structures to use, and when to use them. To date, there have been three such paradigms. For reasons we shall discuss later, there are unlikely to be any others.

任何软件架构的实现都离不开具体的代码，所以我们对软件架构的讨论应该从第一行被写下的代码开始。1938 年，阿兰·图灵为现代计算机编程打下了地基。尽管他并不是第一个发明可编程机器的人，但却是第一个提出「程序即数据」的人。到 1945 年时，图灵已经在真实计算机上编写真实的、我们现在也能看懂的计算机程序了。这些程序中用到了循环、分支、賦值、子调用、等如今我们都很熟悉的结构。而图灵用的编程语言就是简单的二进制数序列。

从那时到现在，编程领域历经了数次变革，其中我们都很熱悉的就是编程语言的变革。首先是在 20 世纪 40 年代末期出现了汇编器（assembler），它能自动将一段程序转化为相应的二进制数序列，大幅解放了程序员。然后是 1951 年，Grace Hopper 发明了 A0, 这是世界上第一个编译器（compiler）。事实上，编译器这个名字就是他定义和推广使用的。再接着就到了 1953 年，那一年 FORTRANI 面世了（就在我出生的第二年）。接下来就是层出不穷的新编程语言了ー COBOL、PL/1、SNOBOL、C、Pascal、C++、Java 等等，不胜枚举。

除此之外，计算机编程领域还经历了另外一个更巨大、更重要的变革，那就是编程范式（paradigm）的变迁。编程范式指的是程序的编写模式，与具体的编程语言关系相对较小。这些范式会告诉你应该在什么时候采用什么样的代码结构。直到今天，我们也一共只有三个编程范式，而且未来几乎不可能再出现新的，接下来我们就看一下为什么。

## 0301. Paradigm Overview

### Conclusion

What does this history lesson on paradigms have to do with architecture? Everything. We use polymorphism as the mechanism to cross architectural boundaries; we use functional programming to impose discipline on the location of and access to data; and we use structured programming as the algorithmic foundation of our modules.

Notice how well those three align with the three big concerns of architecture: function, separation of components, and data management.

大家可能会问，这些编程范式的历史知识与软件架构有关系吗？当然有，而且关系相当密切。譬如说，多态是我们跨越架构边界的手段，函数式编程是我们规范和限制数据存放位置与访问权限的手段，结构化编程则是各模块的算法实现基础。这和软件架构的三大关注重点不谋而合：功能性、组件独立性以及数据管理。

### 00

The three paradigms included in this overview chapter are structured programming, object-orient programming, and functional programming.

本章将讲述三个编程范式，它们分别是结构化编程（structured programming）、面向对象编程（object- oriented programming）以及函数式编程（functional programming）。

### 3.1 Structured Programming

The first paradigm to be adopted (but not the first to be invented) was structured programming, which was discovered by Edsger Wybe Dijkstra in 1968. Dijkstra showed that the use of unrestrained jumps (goto statements) is harmful to program structure. As we’ll see in the chapters that follow, he replaced those jumps with the more familiar if/then/else and do/while/until constructs.

We can summarize the structured programming paradigm as follows: Structured programming imposes discipline on direct transfer of  control.

结构化编程是第一个普遍被采用的编程范式（但是却不是第一个被提出的），由 Edsger Wybe Dijkstra 于 1968 年最先提出。与此同时，Dijkstra 还论证了使用 goto 这样的无限制跳转语句将会损害程序的体结构。接下来的章节我们还会说到，也是这位 Dijkstra 最先主张用我们现在熟知的 f/then/else 语句和 do/while/unt 语句来代替跳转语句的。

我们可以将结构化编程范式归结为一句话：结构化程对程序控制权的直接转移进行了限制和规煎。

### 3.2 Object-Oriented  Programming

The second paradigm to be adopted was actually discovered two years earlier, in 1966, by Ole Johan Dahl and Kristen Nygaard. These two programmers noticed that the function call stack frame in the ALGOL language could be moved to a heap, thereby allowing local variables declared by a function to exist long after the function returned. The function became a constructor for a class, the local variables became instance variables, and the nested functions became methods. This led inevitably to the discovery of polymorphism through the disciplined use of function pointers.

We can summarize the object-oriented programming paradigm as follows: Object-oriented programming imposes discipline on indirect transfer of  control.

说到编程领域中第二个被广泛采用的编程范式，当然就是面向对象编程了。事实上，这个编程范式的提出比结构化编程还早了两年，是在 1966 年由 Ole Johan Dahl 和 Kriste Nygaard 在论文中总结归纳出来的。这两个程序员注意到在 ALGOLT 语言中，函数调用堆栈（call stack frame）可以被挪到堆

存区域里，这样函数定义的本地变量就可以在函数返回之后继续存在。这个函数就成为了一个类（class）的构造函数，而它所定义的本地变量就是类的成员变量，构造函数定义的嵌套函数就成为了成员方法（method）。这样一来，我们就可以利用多态（polymorphism）来限制用户对函数指针的使用。

在这里，我们也可以用一句话来总结面向对象编程：面向对象程对程序控制权的间接转移进行了限制和规范。

### 3.3 Functional Programming

The third paradigm, which has only recently begun to be adopted, was the first to be invented. Indeed, its invention predates computer programming itself. Functional programming is the direct result of the work of Alonzo Church, who in 1936 invented l-calculus while pursuing the same mathematical problem that was motivating Alan Turing at the same time. His l-calculus is the foundation of the LISP language, invented in 1958 by John McCarthy. A foundational notion of l-calculus is immutability—that is, the notion that the values of symbols do not change. This effectively means that a functional language has no assignment statement. Most functional languages do, in fact, have some means to alter the value of a variable, but only under very strict discipline.

We can summarize the functional programming paradigm as follows: Functional programming imposes discipline upon assignment.

尽管第三个编程范式是近些年オ刚刚开始被采用的，但它其实是三个范式中最先被发明的。事实上，函数式编程概念是基于与阿兰·图灵同时代的数学家 Alonzo Church 在 1936 年发明的入演算的直接術生物。1958 年 John Mccarthy 利用其作为基础发明了 LSP 语言。众所周知，入演算法的一个核心思想

是不可变性一一某个符号所对应的值是永远不变的，所以从理论上来说，函数式编程语言中应该是没有赋值语句的。大部分函数式编程语言只允许在非常严格的限制条件下，可以更改某个变量的值。

因此，我们在这里可以将函数式编程范式总结为下面这句话：函数式程对程序中的值进行了限和规范。

### 3.4 Food for Thought

Notice the pattern that I’ve quite deliberately set up in introducing these three programming paradigms: Each of the paradigms removes capabilities from the programmer. None of them adds new capabilities. Each imposes some kind of extra discipline that is negative in its intent. The paradigms tell us what not to do, more than they tell us what to do.

Another way to look at this issue is to recognize that each paradigm takes something away from us. The three paradigms together remove goto statements, function pointers, and assignment. Is there anything left to take away?

Probably not. Thus these three paradigms are likely to be the only three we will see—at least the only three that are negative. Further evidence that there are no more such paradigms is that they were all discovered within the ten years between 1958 and 1968. In the many decades that have followed, no new paradigms have been added.

如你所见，我在介绍三个编程范式的时候，有意采用了上面这种格式，目的是凸显每个编程范式的实际含义ー一它们都从某一方面限制和规范了程序员的能力。没有一个范式是增加新能力的。也就是说，每个编程范式的目的都是设置限制。这些范式主要是为了告诉我们不能做什么，而不是可以做什么。

另外，我们应该认识到，这三个编程范式分别限制了 goto 语句、函数指针和值语句的使用。那么除此之外，还有什么可以去除的吗？有了。因此这三个编程范式可能是仅有的三个了一如果单论去除能力的编程范式的话。支撑这一结论的另外一个证据是，三个编程范式都是在 1958 年到 1968 年这 10 年间被提出来的，后续再也没有新的编程范式出现过。

## 0401. Structured Programming

### Conclusion

It is this ability to create falsifiable units of programming that makes structured programming valuable today. This is the reason that modern languages do not typically support unrestrained goto statements. Moreover,

at the architectural level, this is why we still consider functional decomposition to be one of our best practices.

At every level, from the smallest function to the largest component, software is like a science and, therefore, is driven by falsifiability. Software architects strive to define modules, components, and services that are easily falsifiable (testable). To do so, they employ restrictive disciplines similar to structured programming, albeit at a much higher level.

It is those restrictive disciplines that we will study in some detail in the chapters to come.

结构化编程范式中最有价值的地方就是，它予了我们创造可证伪程序单元的能力。这就是为什么现代程语言一般不支持无限制的 goto 语句。更重要的是，这也是为什么在架构设计领域，功能性降解拆分仍然是最佳实践之一。无论在哪一个层面上，从最小的函数到最大组件，软件开发的过程都和科学研究非常类似，它们都是由证伪驱动的。软件架构师需要定义可以方便地进行证伪（测试）的模块、组件以及服务。为了达到这个目的，他们需要将类似结构化编程的限制方法应用在更高的层面上。我们在接下来的章节中将会深入研究这些限制性的方法。

### 00

Edsger Wybe Dijkstra was born in Rotterdam in 1930. He survived the bombing of Rotterdam during World War II, along with the German occupation of the Netherlands, and in 1948 graduated from high school with the highest possible marks in math, physics, chemistry, and biology. In March 1952, at the age of 21 (and just 9 months before I was born), Dijkstra took a job with the Mathematical Center of Amsterdam as the Netherlands’ very first programmer.

In 1955, having been a programmer for three years, and while still a student, Dijkstra concluded that the intellectual challenge of programming was greater than the intellectual challenge of theoretical physics. As a result, he chose programming as his long-term career.

In 1957, Dijkstra married Maria Debets. At the time, you had to state your profession as part of the marriage rites in the Netherlands. The Dutch authorities were unwilling to accept「programmer」as Dijkstra’s profession; they had never heard of such a profession. To satisfy them, Dijkstra settled for「theoretical physicist」as his job title.

As part of deciding to make programming his career, Dijkstra conferred with his boss, Adriaan van Wijngaarden. Dijkstra was concerned that no one had identified a discipline, or science, of programming, and that he would therefore not be taken seriously. His boss replied that Dijkstra might very well be one of the people who would discover such disciplines, thereby evolving software into a science.

Dijkstra started his career in the era of vacuum tubes, when computers were huge, fragile, slow, unreliable, and (by today’s standards) extremely limited. In those early years, programs were written in binary, or in very crude assembly language. Input took the physical form of paper tape or punched cards. The edit/compile/test loop was hours — if not days — long.

It was in this primitive environment that Dijkstra made his great discoveries.

Edsger Wybe Dijkstra 于 1930 年出生在荷兰鹿特丹。生于乱世，他亲身经历了第二次世界大战中的鹿特丹大轰炸、德国占领荷兰等事件。1948 年，他以数学、物理、化学以及生物全满分的成绩高中毕业。1952 年 3 月，年仅 21 岁的 Dijkstra（此时距离我出生还有 9 个月时间）入职荷兰阿姆斯特丹数学中心，成为了荷兰的第一个程序员。

1955 年，在从事编程工作 3 年之后，当时还是一个学生的 Dijkstra 就认为编程相比理论物理更有挑战性，因此他选择将编程作为终身职业。

1957 年，Dijkstra 与 Maria Debets 结婚了。在当时的荷兰，新郎新娘必须在结婚仪式上公布自己的职业。而当时的荷兰官方政府拒绝承认「程序员」这一职业，因为他们从来没有听说过。最终 Dijkstra 不得不继续使用「理论物理学家」这一职位名称。

Dijkstra 和他的老板 Adriaan van Wijngaarden 曾经讨论过将「程序员」当作终身职业这件事，Dijkstra 最担心的是由于没有人认真地对待过编程这件事或者将它当作是一门学术学科对待，他的科研成果可能将不会得到认真对待。而 Adriaan 则建议 Dijkstra：为什么不亲自去开创这门学科呢？

当时还是真空管阶段。计算机体积巨大，运行缓慢，还非常容易出故障，功能（与今天对比）十分有限。人们还是直接使用二进制数，或者使用非常原始的汇编语言编程。计算机的输入方式则还是用纸卷或者是打孔卡片。要想执行完整的编辑、编译、測试流程是非常耗时的，通常需要数小时或者数天才能完成。

Dijkstras 就是在这样原始的条件下做出其非凡的成就的。

### 4.1 Proof

The problem that Dijkstra recognized, early on, was that programming is hard, and that programmers don’t do it very well. A program of any complexity contains too many details for a human brain to manage without help. Overlooking just one small detail results in programs that may seem to work, but fail in surprising ways.

Dijkstra’s solution was to apply the mathematical discipline of proof. His vision was the construction of a Euclidian hierarchy of postulates, theorems, corollaries, and lemmas. Dijkstra thought that programmers could use that hierarchy the way mathematicians do. In other words, programmers would use proven structures, and tie them together with code that they would then prove correct themselves.

Of course, to get this going, Dijkstra realized that he would have to demonstrate the technique for writing basic proofs of simple algorithms. This he found to be quite challenging.

During his investigation, Dijkstra discovered that certain uses of goto statements prevent modules from being decomposed recursively into smaller and smaller units, thereby preventing use of the divide-and-conquer approach necessary for reasonable proofs.

Other uses of goto, however, did not have this problem. Dijkstra realized that these「good」uses of goto corresponded to simple selection and iteration control structures such as if/then/else and do/while. Modules that used only those kinds of control structures could be recursively subdivided into provable units.

Dijkstra knew that those control structures, when combined with sequential execution, were special. They had been identified two years before by Böhm and Jacopini, who proved that all programs can be constructed from just three structures: sequence, selection, and iteration.

This discovery was remarkable: The very control structures that made a module provable were the same minimum set of control structures from which all programs can be built. Thus structured programming was born.

Dijkstra showed that sequential statements could be proved correct through simple enumeration. The technique mathematically traced the inputs of the sequence to the outputs of the sequence. This approach was no different from any normal mathematical proof.

Dijkstra tackled selection through reapplication of enumeration. Each path through the selection was enumerated. If both paths eventually produced appropriate mathematical results, then the proof was solid.

Iteration was a bit different. To prove an iteration correct, Dijkstra had to use induction. He proved the case for 1 by enumeration. Then he proved the case that if N was assumed correct, N + 1 was correct, again by enumeration. He also proved the starting and ending criteria of the iteration by enumeration.

Such proofs were laborious and complex — but they were proofs. With their development, the idea that a Euclidean hierarchy of theorems could be constructed seemed reachable.

可推导性

Dijkstra 很早就得出的结论是：编程是一项难度很大的活动。一段程序无论复杂与否，都包含了很多的细节信息。如果没有工具的帮助，这些细节的信息是远远超过一个程序员的认知能力范围的。而在一段程序中，哪怕仅仅是一个小细节的错误，也会造成整个程序出错。

Dijkstra 提出的解決方案是采用数学推导方法。他的想法是借签数学中的公理（Postulate）、定理（Theorem）、推论（Corollary）和引理（Lemma），形成一种欧几里得结构。Dijkstra 认为程序员可以像数学家一样对自己的程序进行推理证明。换句话说，程序员可以用代码将一些已证明可用的结构串联起来，只要自行证明这些额外代码是正确的，就可以推导出整个程序的正确性

当然，在这之前，必须先展示如何推导证明简单算法的正确性，这本身就是一件极具挑战性的工作。

Dijkstra 在研究过程中发现了一个问题：goto 语句的某些用法会导致某个模块无法被递归拆分成更小的、可证明的单元，这会导致无法采用分解法来将大型问题进一步拆分成更小的、可证明的部分。

goto 语句的其他用法虽然不会导致这种问题，但是 Dijkstra 意识到它们的实际效果其实和更简单的分支结构 - then-else 以及循环结构 do- whilea 是一致的。如果代码中只采用了这两类控制结构，则一定可以将程序分解成更小的、可证明的单元。事实上，Dijkstra 很早就知道将这些控制结构与序结构的程序组合起来很有用。因为在两年前，Bohm 和 Jocopinip 刚刚证明了人们可以用顺序结构、分支结构、循环结构这三种结构构造出任何程序。

这个发现非常重要：因为它证明了我们构建可推导模块所需要的控制结构集与构建所有程序所需的控制结构集的最小集是等同的。这样一来，结构化编程就诞生了

Dijkstra 展示了顺序结构的正确性可以通过枚举法证明，其过程与其他一般的数学推导过程是一样的：针对序列中的每个输入，跟踪其对应的出值的变化就可以了。同样的，Dijkstra？利用枚举法又证明了分支结构的可推导性。因为我们只要能用枚举法证明分支结构中每条路径的正确性，自然就可以推导出分支结构本身的正确性。

循环结构的证明过程则有些不同，为了证明一段循环程序的正确性，Dijkstra 需要采用数学归纳法。具体来说就是，首先要用枚举法证明循环 1 次的正确性。接下来再证明如果循环 N 次是正确的，那么循环 N+1 次也同样也是正确的。最后还要用枚举法证明循环结的起始与结束条件的正确性。

尽管这些证明过程本身非常复杂和烦琐，但确实是完备的。有了这样的证明过程，用欧几里得层级构造定理的方式来验证程序正确性的目标，貌似近在咫尺了。

### 4.2 A Harmful Proclamation

In 1968, Dijkstra wrote a letter to the editor of CACM, which was published in the March issue. The title of this letter was「Go To Statement Considered Harmful.」The article outlined his position on the three control structures.

And the programming world caught fire. Back then we didn’t have an Internet, so people couldn’t post nasty memes of Dijkstra, and they couldn’t flame him online. But they could, and they did, write letters to the editors of many published journals.

Those letters weren’t necessarily all polite. Some were intensely negative; others voiced strong support for his position. And so the battle was joined, ultimately to last about a decade.

Eventually the argument petered out. The reason was simple: Dijkstra had won. As computer languages evolved, the goto statement moved ever rearward, until it all but disappeared. Most modern languages do not have a goto statement — and, of course, LISP never did.

Nowadays we are all structured programmers, though not necessarily by choice. It’s just that our languages don’t give us the option to use undisciplined direct transfer of control.

Some may point to named breaks in Java or exceptions as goto analogs. In fact, these structures are not the utterly unrestricted transfers of control that older languages like Fortran or COBOL once had. Indeed, even languages that still support the goto keyword often restrict the target to within the scope of the current function.

goto 是有害的

1968 年，Dijkstra 曾经给 CACM 的编辑写过一封信。这封信后来发表于 CACM3 月刊，标题是 Go To Statement Considered Harmful, Dijkstra 在信中具体描绘了他对三种控制结构的看法。这可捅了个大子。由于当时还没有互联网，大家还不能直接上网发帖来对 Dijkstra 进行冷嘲热讽，他们唯一能做的，也是大部分人的选择，就是不停地给各种公开发表的报刊的编辑们写信。可想而知，有的信件的措辞并不那么友善，甚至是非常负面的。但是，也不乏强烈支持者。总之，这场火热的争论持续了超过 10 年。

当然，这场辩论最终还是逐渐停止了。原因很简单：Dijkstra 是对的。随着编程语言的演进，goto 语句的重要性越来越小，最终甚至消失了。如今大部分的现代编程语言中都已经没有了 goto 语句。哦，对了，LISP 里从来就没有过！

现如今，无论是否自愿，我们都是结构化编程范式的践行者了，因为我们用的编程语言基本上都已经禁止了不受限制的直接控制转移语句。或许有些人会指出，Java 中的带命名的 breakt 语句或者 Exception 都和 goto 很类似。事实上，这些语法结构与老的编程语言（类似 FORTRAN 和 COBOL）中的完全无限制的 gotti 语句根本不一样。就算那些还支持 goto 关键词的编程语言也通常限制了 goto 的目标不能超出当前函数范围。

### 4.3 Functional  Decomposition

Structured programming allows modules to be recursively decomposed into provable units, which in turn means that modules can be functionally decomposed. That is, you can take a large-scale problem statement and decompose it into high-level functions. Each of those functions can then be decomposed into lower-level functions, ad infinitum. Moreover, each of those decomposed functions can be represented using the restricted control structures of structured programming.

Building on this foundation, disciplines such as structured analysis and structured design became popular in the late 1970s and throughout the 1980s. Men like Ed Yourdon, Larry Constantine, Tom DeMarco, and Meilir Page-Jones promoted and popularized these techniques throughout that period. By following these disciplines, programmers could break down large proposed systems into modules and components that could be further broken down into tiny provable functions.

功能性降解拆分

既然结构化编程范式可将模块递归降解拆分为可推导的单元，这就意味着模块也可以按功能进行降解拆分。这样一来，我们就可以将一个大型问题拆分为一系列高级函数的组合，而这些高级函数各自又可以继续被拆分为一系列低级函数，如此无限递归。更重要的是，每个被拆分出来的函数也都可以用结构化编程范式来书写。

以此为理论基础，在 20 世纪 70 年代晚期到 80 年代中期出现的结构化分析与结构化设计工作オ能广为入知。Ed Yourdon、Larry Constantine、Tom Demarcol 以及 Meilir Page Jones 在这期间为此做了很多推广工作。通过采用这些技巧，程序员可以将大型系统设计拆分成模块和组件，而这些模块和组件最终可以拆分为更小的、可证明的函数。

### 4.4 No Formal Proofs

But the proofs never came. The Euclidean hierarchy of theorems was never built. And programmers at large never saw the benefits of working through the laborious process of formally proving each and every little function correct. In the end, Dijkstra’s dream faded and died. Few of today’s programmers believe that formal proofs are an appropriate way to produce high-quality software.

Of course, formal, Euclidian style, mathematical proofs are not the only strategy for proving something correct. Another highly successful strategy is the scientific method.

形式化证明没有发生

但是，人人都用完整的形式化证明的一天没有到来。大部分人不会真的按照欧几里得结构为每个小函数书写冗长复杂的正确性证明过程。。Dijkstra 的梦想最终并没有实现。没有几个程序员会认为形式化验证是产出高质量软件的必备条件。当然，形式化的、欧几里得式的数学推导证明并不是证明结构化编程正确性的唯一手段。下面我们来看另外一个十分成功的策略：科学证明法。

### 4.5 Science to the Rescue

Science is fundamentally different from mathematics, in that scientific theories and laws cannot be proven correct. I cannot prove to you that Newton’s second law of motion, F = ma, or law of gravity, F = Gm1m2/r2, are correct. I can demonstrate these laws to you, and I can make measurements that show them correct to many decimal places, but I cannot prove them in the sense of a mathematical proof. No matter how many experiments I conduct or how much empirical evidence I gather, there is always the chance that some experiment will show that those laws of motion and gravity are incorrect.

That is the nature of scientific theories and laws: They are falsifiable but not provable.

And yet we bet our lives on these laws every day. Every time you get into a car, you bet your life that F = ma is a reliable description of the way the world works. Every time you take a step, you bet your health and safety that F = Gm1m2/r 2 is correct.

Science does not work by proving statements true, but rather by proving statements false. Those statements that we cannot prove false, after much effort, we deem to be true enough for our purposes.

Of course, not all statements are provable. The statement「This is a lie」is neither true nor false. It is one of the simplest examples of a statement that is not provable.

Ultimately, we can say that mathematics is the discipline of proving provable statements true. Science, in contrast, is the discipline of proving provable statements false.

科学来救场

科学和数学在证明方法上有着根本性的不同，科学理论和科学定律通常是无法被证明的，譬如我们并没有办法证明牛顿第二运动定律 F=ma 或者万有引カ定律 `F=Gmm2/r2` 是正确的，但我们可以用实际案例来演示这些定律的正确性，并通过高精度測量来证明当相关精度达到小数点后多少位时，被测量对象仍然一直满足这个定律。但我们始终没有办法像用数学方法一样推导出这个定律。而且，不管我们进行多少次正确的验，也无法排除今后会存在某一次实验可以推翻牛顿第二运动定律与万有引力定律的可能性

这就是科学理论和科学定律的特点：它们可以被证伪，但是没有办法被证明。但是我们仍然每天都在依赖这些定律生活。开车的时候，我们就等于是在用性命担保 F=ma 是对世界运转方式的一个可靠的描述。每当我们迈出一步的时候，就等于在亲身证明 F=Gmm2/r2 是正确的。

科学方法论不需要证明某条结论是正确的，只需要想办法证明它是错误的。如果某个结论经过一定的努力无法证伪，我们则认为它在当下是足够正确的。当然，不是所有的结论都可以被证明或者证伪的。举一个最简单的不可证明的例子：「这句话是假的」，非真也非伪。最终，我们可以说数学是要将可证明的结论证明，而与之相反，科学研究则是要将可证明的结论证伪。

### 4.6 Tests

Dijkstra once said,「Testing shows the presence, not the absence, of bugs.」In other words, a program can be proven incorrect by a test, but it cannot be proven correct. All that tests can do, after sufficient testing effort, is allow us to deem a program to be correct enough for our purposes.

The implications of this fact are stunning. Software development is not a mathematical endeavor, even though it seems to manipulate mathematical constructs. Rather, software is like a science. We show correctness by failing to prove incorrectness, despite our best efforts.

Such proofs of incorrectness can be applied only to provable programs. A program that is not provable — due to unrestrained use of goto, for example — cannot be deemed correct no matter how many tests are applied to it.

Structured programming forces us to recursively decompose a program into a set of small provable functions. We can then use tests to try to prove those small provable functions incorrect. If such tests fail to prove incorrectness, then we deem the functions to be correct enough for our purposes.

Dijkstra 曾经说过「测试只能展示 Bug 的存在，并不能证明不存在 Bug」，换句话说，一段程序可以由一个测试来证明其错误性，但是却不能被证明是正确的。测试的作用是让我们得出某段程序已经足够实现当前目标这一结论。这一事实所带来的影响是惊人的。软件开发虽然看起来是在操作很多数学结构，其实不是一个数学研究过程。恰恰相反，软件开发更像是一门科学研究学科，我们通过无法证伪来证明软件的正确性。

注意，这种证伪过程只能应用于可证明的程序上。某段程序如果是不可证明的，例如，其中采用了不加限制的 goto 语句，那么无论我们为它写多少測试，也不能够证明其正确性。结构化编程范式促使我们先将一段程序递归降解为一系列可证明的小函数，然后再编写相关的测试来试图证明这些函数是错误的。如果这些测试无法证伪这些函数，那么我们就可以认为这些函数是足够正确的，进而推导整个程序是正确的。
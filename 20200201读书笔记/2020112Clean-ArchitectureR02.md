# 2020112Clean-ArchitectureR02

## 记忆时间

## 0200. Starting with the Bricks: Programming Paradigms

Software architecture begins with the code — and so we will begin our discussion of architecture by looking at what we’ve learned about code since code was first written.

In 1938, Alan Turing laid the foundations of what was to become computer programming. He was not the first to conceive of a programmable machine, but he was the first to understand that programs were simply data. By 1945, Turing was writing real programs on real computers in code that we would recognize (if we squinted enough). Those programs used loops, branches, assignment, subroutines, stacks, and other familiar structures. Turing’s language was binary.

Since those days, a number of revolutions in programming have occurred. One revolution with which we are all very familiar is the revolution of languages. First, in the late 1940s, came assemblers. These「languages」relieved the programmers of the drudgery of translating their programs into binary. In 1951, Grace Hopper invented A0, the first compiler. In fact, she coined the term compiler. Fortran was invented in 1953 (the year after I was born). What followed was an unceasing flood of new programming languages — COBOL, PL/1, SNOBOL, C, Pascal, C++, Java, ad infinitum.

Another, probably more significant, revolution was in programming paradigms. Paradigms are ways of programming, relatively unrelated to languages. A paradigm tells you which programming structures to use, and when to use them. To date, there have been three such paradigms. For reasons we shall discuss later, there are unlikely to be any others.

1-2『编程范式，ways of programming，其与使用什么编程语言没啥关系的，编程范式做一张术语卡片。』 —  — 已完成

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

我们可以将结构化编程范式归结为一句话：结构化程对程序控制权的直接转移进行了限制和规范。

### 3.2 Object-Oriented  Programming

The second paradigm to be adopted was actually discovered two years earlier, in 1966, by Ole Johan Dahl and Kristen Nygaard. These two programmers noticed that the function call stack frame in the ALGOL language could be moved to a heap, thereby allowing local variables declared by a function to exist long after the function returned. The function became a constructor for a class, the local variables became instance variables, and the nested functions became methods. This led inevitably to the discovery of polymorphism through the disciplined use of function pointers.

We can summarize the object-oriented programming paradigm as follows: Object-oriented programming imposes discipline on indirect transfer of  control.

1-3『这里对面向对象编程底层逻辑的描述，联想到学 JS 时，看亚历山大那个 CEO 的系列文章里，介绍闭包相关知识时，有相通的感觉。（2020-12-24）』

说到编程领域中第二个被广泛采用的编程范式，当然就是面向对象编程了。事实上，这个编程范式的提出比结构化编程还早了两年，是在 1966 年由 Ole Johan Dahl 和 Kriste Nygaard 在论文中总结归纳出来的。这两个程序员注意到在 ALGOLT 语言中，函数调用堆栈（call stack frame）可以被挪到堆存区域里，这样函数定义的本地变量就可以在函数返回之后继续存在。这个函数就成为了一个类（class）的构造函数，而它所定义的本地变量就是类的成员变量，构造函数定义的嵌套函数就成为了成员方法（method）。这样一来，我们就可以利用多态（polymorphism）来限制用户对函数指针的使用。

在这里，我们也可以用一句话来总结面向对象编程：面向对象程对程序控制权的间接转移进行了限制和规范。

### 3.3 Functional Programming

The third paradigm, which has only recently begun to be adopted, was the first to be invented. Indeed, its invention predates computer programming itself. Functional programming is the direct result of the work of Alonzo Church, who in 1936 invented λ-calculus while pursuing the same mathematical problem that was motivating Alan Turing at the same time. His λ-calculus is the foundation of the LISP language, invented in 1958 by John McCarthy. A foundational notion of λ-calculus is immutability — that is, the notion that the values of symbols do not change. This effectively means that a functional language has no assignment statement. Most functional languages do, in fact, have some means to alter the value of a variable, but only under very strict discipline.

We can summarize the functional programming paradigm as follows: Functional programming imposes discipline upon assignment.

尽管第三个编程范式是近些年オ刚刚开始被采用的，但它其实是三个范式中最先被发明的。事实上，函数式编程概念是基于与阿兰·图灵同时代的数学家 Alonzo Church 在 1936 年发明的 λ 演算的直接衍生物。1958 年 John Mccarthy 利用其作为基础发明了 LISP 语言。众所周知，λ 演算法的一个核心思想是不可变性 一一 某个符号所对应的值是永远不变的，所以从理论上来说，函数式编程语言中应该是没有赋值语句的。大部分函数式编程语言只允许在非常严格的限制条件下，可以更改某个变量的值。

因此，我们在这里可以将函数式编程范式总结为下面这句话：函数式程对程序中的值进行了限制和规范。

### 3.4 Food for Thought

Notice the pattern that I’ve quite deliberately set up in introducing these three programming paradigms: Each of the paradigms removes capabilities from the programmer. None of them adds new capabilities. Each imposes some kind of extra discipline that is negative in its intent. The paradigms tell us what not to do, more than they tell us what to do.

Another way to look at this issue is to recognize that each paradigm takes something away from us. The three paradigms together remove goto statements, function pointers, and assignment. Is there anything left to take away?

Probably not. Thus these three paradigms are likely to be the only three we will see — at least the only three that are negative. Further evidence that there are no more such paradigms is that they were all discovered within the ten years between 1958 and 1968. In the many decades that have followed, no new paradigms have been added.

如你所见，我在介绍三个编程范式的时候，有意采用了上面这种格式，目的是凸显每个编程范式的实际含义ー一它们都从某一方面限制和规范了程序员的能力。没有一个范式是增加新能力的。也就是说，每个编程范式的目的都是设置限制。这些范式主要是为了告诉我们不能做什么，而不是可以做什么。

另外，我们应该认识到，这三个编程范式分别限制了 goto 语句、函数指针和值语句的使用。那么除此之外，还有什么可以去除的吗？有了。因此这三个编程范式可能是仅有的三个了一如果单论去除能力的编程范式的话。支撑这一结论的另外一个证据是，三个编程范式都是在 1958 年到 1968 年这 10 年间被提出来的，后续再也没有新的编程范式出现过。

2-3『

搜 Ole Johan Dahl and Kristen Nygaard 1966 年有关面向对象的那篇 Paper 没找到，找到了下面博客里的一篇相关短文。同时搜到了 Ole Johan Dahl  写的 2 篇 Paper，已下载论文并存入 Zotero，「2020031Object-oriented programming: Some history, and challenges for the next fifty years」「2020032The Birth of Object Orientation: the Simula Languages」。意外发现第二篇 Paper 是 Ole Johan Dahl 自己一本书（论文集）里的章节，已下载原文书籍「2020174From-Object-Orientation-to-Formal-Methods」。

[How Object-Oriented Programming Started](http://kristennygaard.org/FORSKNINGSDOK_MAPPE/F_OO_start.html)

[Object-oriented programming: Some history, and challenges for the next fifty years - ScienceDirect](https://www.sciencedirect.com/science/article/pii/S0890540113000795)

Below you will find an abbreviated version of an article requested by an encyclopedia some years ago. It gives a brief description of some key facts about the early history of object-oriented programming. This page will be expanded and provide link, I hope, to a number of important papers. Some of these papers are frequently referred to but seldom read, I suspect, since they have not been easily available.

As for the history, the paper Dahl and I wrote for the "History of Programming Languages" conference and book (edited by Richard Wexeblat) will appear on these pages soon. Another interesting and competently researched paper is already on the web, written by Jan Rune Holmevik.

### How Object-Oriented Programming Started

by Ole-Johan Dahl and Kristen Nygaard, Dept. of Informatics, University of Oslo

SIMULA I (1962-65) and Simula 67 (1967) are the two first object-oriented languages. Simula 67 introduced most of the key concepts of object-oriented programming: both objects and classes, subclasses (usually referred to as inheritance) and virtual procedures, combined with safe referencing and mechanisms for bringing into a program collections of program structures described under a common class heading (prefixed blocks).

The Simula languages were developed at the Norwegian Computing Center, Oslo, Norway by Ole-Johan Dahl and Kristen Nygaard. Nygaard's work in Operational Research in the 1950s and early 1960s created the need for precise tools for the description and simulation of complex man-machine systems. In 1961 the idea emerged for developing a language that both could be used for system description (for people) and for system prescription (as a computer program through a compiler). Such a language had to contain an algorithmic language, and Dahl's knowledge of compilers became essential.

The SIMULA I compiler was partially financed by UNIVAC and was ready in January 1965. SIMULA I quickly got a reputation as a simulation programming language, but turned out in addition to posess interesting properties as a general programming language. When the inheritance mechanism was invented in 1967, Simula 67 was developed as a general programming language that also could be specialised for many domains, including system simulation. Simula 67 compilers started to appear for UNIVAC, IBM, Control Data, Burroughs, DEC and other computers in the early 1970s.

Simula 67 still is being used many places around the world, but its main impact has been through introducing one of the main categories of programming, more generally labelled object-oriented programming. Simula concepts have been important in the discussion of abstract data types and of models for concurrent program execution, starting in the early 1970s. Simula 67 and modifications of Simula were used in the design of VLSI circuitry (Intel, Caltech, Stanford). Alan Kay's group at Xerox PARC used Simula as a platform for their development of Smalltalk (first language versions in the 1970s), extending object-oriented programming importantly by the integration of graphical user interfaces and interactive program execution. Bjarne Stroustrup started his development of C++ (in the 1980s) by bringing the key concepts of Simula into the C programming language. Simula has also inspired much work in the area of program component reuse and the construction of program libraries.

In the 1980s tremendous resources were put behind the ADA language (US Department of Defense) and PROLOG (the Japanese "Fifth Generation Computer Project"), and many believed that ADA and PROLOG would fight for dominance in the 1990s. Instead object-oriented programming is today (in the late 1990s) becoming the dominant style for implementing complex programs with large numbers of interacting components. Among the multitude of object-oriented language are Eiffel (B. Meyer) , CLOS (D. Bobrow and G. Kiczales), SELF (D. Ungar and others). In particular the Internet-related Java (developed by Sun) has rapidly become widely used in recent years. BETA (B. Bruun-Kristensen, O. Lehrmann Madsen, B. Møller-Pedersen and K. Nygaard) is a very general object-oriented language in the Simula tradition.

』

## 0401. Structured Programming

### Conclusion

It is this ability to create falsifiable units of programming that makes structured programming valuable today. This is the reason that modern languages do not typically support unrestrained goto statements. Moreover, at the architectural level, this is why we still consider functional decomposition to be one of our best practices.

At every level, from the smallest function to the largest component, software is like a science and, therefore, is driven by falsifiability. Software architects strive to define modules, components, and services that are easily falsifiable (testable). To do so, they employ restrictive disciplines similar to structured programming, albeit at a much higher level.

It is those restrictive disciplines that we will study in some detail in the chapters to come.

结构化编程范式中最有价值的地方就是，它予了我们创造可证伪程序单元的能力。这就是为什么现代程语言一般不支持无限制的 goto 语句。更重要的是，这也是为什么在架构设计领域，功能性降解拆分仍然是最佳实践之一。无论在哪一个层面上，从最小的函数到最大组件，软件开发的过程都和科学研究非常类似，它们都是由证伪驱动的。软件架构师需要定义可以方便地进行证伪（测试）的模块、组件以及服务。为了达到这个目的，他们需要将类似结构化编程的限制方法应用在更高的层面上。我们在接下来的章节中将会深入研究这些限制性的方法。

1『印象中，剔除消除 goto 语言的 Edsger Wybe Dijkstra，他从数学上证明了「结构性」语言的可证伪性。回复：下面有详细的讲解。（2020-12-24）』

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

Dijkstra 提出的解决方案是采用数学推导方法。他的想法是借签数学中的公理（Postulate）、定理（Theorem）、推论（Corollary）和引理（Lemma），形成一种欧几里得结构。Dijkstra 认为程序员可以像数学家一样对自己的程序进行推理证明。换句话说，程序员可以用代码将一些已证明可用的结构串联起来，只要自行证明这些额外代码是正确的，就可以推导出整个程序的正确性

当然，在这之前，必须先展示如何推导证明简单算法的正确性，这本身就是一件极具挑战性的工作。Dijkstra 在研究过程中发现了一个问题：goto 语句的某些用法会导致某个模块无法被递归拆分成更小的、可证明的单元，这会导致无法采用分解法来将大型问题进一步拆分成更小的、可证明的部分。

goto 语句的其他用法虽然不会导致这种问题，但是 Dijkstra 意识到它们的实际效果其实和更简单的分支结构 if-then-else 以及循环结构 do-while 是一致的。如果代码中只采用了这两类控制结构，则一定可以将程序分解成更小的、可证明的单元。事实上，Dijkstra 很早就知道将这些控制结构与顺序结构的程序组合起来很有用。因为在两年前，Bohm 和 Jocopinip 刚刚证明了人们可以用顺序结构、分支结构、循环结构这三种结构构造出任何程序。

这个发现非常重要：因为它证明了我们构建可推导模块所需要的控制结构集与构建所有程序所需的控制结构集的最小集是等同的。这样一来，结构化编程就诞生了。

Dijkstra 展示了顺序结构的正确性可以通过枚举法证明，其过程与其他一般的数学推导过程是一样的：针对序列中的每个输入，跟踪其对应的出值的变化就可以了。同样的，Dijkstra 利用枚举法又证明了分支结构的可推导性。因为我们只要能用枚举法证明分支结构中每条路径的正确性，自然就可以推导出分支结构本身的正确性。

循环结构的证明过程则有些不同，为了证明一段循环程序的正确性，Dijkstra 需要采用数学归纳法。具体来说就是，首先要用枚举法证明循环 1 次的正确性。接下来再证明如果循环 N 次是正确的，那么循环 N+1 次也同样也是正确的。最后还要用枚举法证明循环结的起始与结束条件的正确性。

尽管这些证明过程本身非常复杂和烦琐，但确实是完备的。有了这样的证明过程，用欧几里得层级构造定理的方式来验证程序正确性的目标，貌似近在咫尺了。

### 4.2 A Harmful Proclamation

In 1968, Dijkstra wrote a letter to the editor of CACM, which was published in the March issue. The title of this letter was「Go To Statement Considered Harmful.」The article outlined his position on the three control structures.

1-2『这篇 Paper 之前在郑烨的专栏里就知道了，已下载论文并存入 Zotero，「2020017Go To Statement Considered Harmful」。(2020-12-24)』

And the programming world caught fire. Back then we didn’t have an Internet, so people couldn’t post nasty memes of Dijkstra, and they couldn’t flame him online. But they could, and they did, write letters to the editors of many published journals.

Those letters weren’t necessarily all polite. Some were intensely negative; others voiced strong support for his position. And so the battle was joined, ultimately to last about a decade.

Eventually the argument petered out. The reason was simple: Dijkstra had won. As computer languages evolved, the goto statement moved ever rearward, until it all but disappeared. Most modern languages do not have a goto statement — and, of course, LISP never did.

Nowadays we are all structured programmers, though not necessarily by choice. It’s just that our languages don’t give us the option to use undisciplined direct transfer of control.

Some may point to named breaks in Java or exceptions as goto analogs. In fact, these structures are not the utterly unrestricted transfers of control that older languages like Fortran or COBOL once had. Indeed, even languages that still support the goto keyword often restrict the target to within the scope of the current function.

goto 是有害的

1968 年，Dijkstra 曾经给 CACM 的编辑写过一封信。这封信后来发表于 CACM3 月刊，标题是 Go To Statement Considered Harmful，Dijkstra 在信中具体描绘了他对三种控制结构的看法。这可捅了个大子。由于当时还没有互联网，大家还不能直接上网发帖来对 Dijkstra 进行冷嘲热讽，他们唯一能做的，也是大部分人的选择，就是不停地给各种公开发表的报刊的编辑们写信。可想而知，有的信件的措辞并不那么友善，甚至是非常负面的。但是，也不乏强烈支持者。总之，这场火热的争论持续了超过 10 年。

当然，这场辩论最终还是逐渐停止了。原因很简单：Dijkstra 是对的。随着编程语言的演进，goto 语句的重要性越来越小，最终甚至消失了。如今大部分的现代编程语言中都已经没有了 goto 语句。哦，对了，LISP 里从来就没有过！

现如今，无论是否自愿，我们都是结构化编程范式的践行者了，因为我们用的编程语言基本上都已经禁止了不受限制的直接控制转移语句。或许有些人会指出，Java 中的带命名的 break 语句或者 Exception 都和 goto 很类似。事实上，这些语法结构与老的编程语言（类似 FORTRAN 和 COBOL）中的完全无限制的 goto 语句根本不一样。就算那些还支持 goto 关键词的编程语言也通常限制了 goto 的目标不能超出当前函数范围。

### 4.3 Functional  Decomposition

Structured programming allows modules to be recursively decomposed into provable units, which in turn means that modules can be functionally decomposed. That is, you can take a large-scale problem statement and decompose it into high-level functions. Each of those functions can then be decomposed into lower-level functions, ad infinitum. Moreover, each of those decomposed functions can be represented using the restricted control structures of structured programming.

Building on this foundation, disciplines such as structured analysis and structured design became popular in the late 1970s and throughout the 1980s. Men like Ed Yourdon, Larry Constantine, Tom DeMarco, and Meilir Page-Jones promoted and popularized these techniques throughout that period. By following these disciplines, programmers could break down large proposed systems into modules and components that could be further broken down into tiny provable functions.

功能性降解拆分

既然结构化编程范式可将模块递归降解拆分为可推导的单元，这就意味着模块也可以按功能进行降解拆分。这样一来，我们就可以将一个大型问题拆分为一系列高级函数的组合，而这些高级函数各自又可以继续被拆分为一系列低级函数，如此无限递归。更重要的是，每个被拆分出来的函数也都可以用结构化编程范式来书写。

以此为理论基础，在 20 世纪 70 年代晚期到 80 年代中期出现的结构化分析与结构化设计工作才能广为人知。Ed Yourdon、Larry Constantine、Tom Demarcol 以及 Meilir Page Jones 在这期间为此做了很多推广工作。通过采用这些技巧，程序员可以将大型系统设计拆分成模块和组件，而这些模块和组件最终可以拆分为更小的、可证明的函数。

### 4.4 No Formal Proofs

But the proofs never came. The Euclidean hierarchy of theorems was never built. And programmers at large never saw the benefits of working through the laborious process of formally proving each and every little function correct. In the end, Dijkstra’s dream faded and died. Few of today’s programmers believe that formal proofs are an appropriate way to produce high-quality software.

Of course, formal, Euclidian style, mathematical proofs are not the only strategy for proving something correct. Another highly successful strategy is the scientific method.

形式化证明没有发生

但是，人人都用完整的形式化证明的一天没有到来。大部分人不会真的按照欧几里得结构为每个小函数书写冗长复杂的正确性证明过程。Dijkstra 的梦想最终并没有实现。没有几个程序员会认为形式化验证是产出高质量软件的必备条件。当然，形式化的、欧几里得式的数学推导证明并不是证明结构化编程正确性的唯一手段。下面我们来看另外一个十分成功的策略：科学证明法。

### 4.5 Science to the Rescue

Science is fundamentally different from mathematics, in that scientific theories and laws cannot be proven correct. I cannot prove to you that Newton’s second law of motion, F = ma, or law of gravity, F = Gm1m2/r2, are correct. I can demonstrate these laws to you, and I can make measurements that show them correct to many decimal places, but I cannot prove them in the sense of a mathematical proof. No matter how many experiments I conduct or how much empirical evidence I gather, there is always the chance that some experiment will show that those laws of motion and gravity are incorrect.

That is the nature of scientific theories and laws: They are falsifiable but not provable. And yet we bet our lives on these laws every day. Every time you get into a car, you bet your life that F = ma is a reliable description of the way the world works. Every time you take a step, you bet your health and safety that F = Gm1m2/r 2 is correct.

Science does not work by proving statements true, but rather by proving statements false. Those statements that we cannot prove false, after much effort, we deem to be true enough for our purposes. Of course, not all statements are provable. The statement「This is a lie」is neither true nor false. It is one of the simplest examples of a statement that is not provable.

Ultimately, we can say that mathematics is the discipline of proving provable statements true. Science, in contrast, is the discipline of proving provable statements false.

1-2『有关科学与数学的区别，之前在很多地方看到过，比如吴军的数学通识课，但还是觉得这里作者将的相对通透，而且下面提到软件开发是科学范畴而非数学范畴，给自己醍醐灌顶的感觉。科学与数学的区别以及软件开发是科学范畴，做一张主题卡片。（2020-12-24）』——已完成

科学来救场

科学和数学在证明方法上有着根本性的不同，科学理论和科学定律通常是无法被证明的，譬如我们并没有办法证明牛顿第二运动定律 F=ma 或者万有引カ定律 `F=Gmm2/r2` 是正确的，但我们可以用实际案例来演示这些定律的正确性，并通过高精度测量来证明当相关精度达到小数点后多少位时，被测量对象仍然一直满足这个定律。但我们始终没有办法像用数学方法一样推导出这个定律。而且，不管我们进行多少次正确的验，也无法排除今后会存在某一次实验可以推翻牛顿第二运动定律与万有引力定律的可能性。

这就是科学理论和科学定律的特点：它们可以被证伪，但是没有办法被证明。但是我们仍然每天都在依赖这些定律生活。开车的时候，我们就等于是在用性命担保 F=ma 是对世界运转方式的一个可靠的描述。每当我们迈出一步的时候，就等于在亲身证明 F=Gmm2/r2 是正确的。

科学方法论不需要证明某条结论是正确的，只需要想办法证明它是错误的。如果某个结论经过一定的努力无法证伪，我们则认为它在当下是足够正确的。当然，不是所有的结论都可以被证明或者证伪的。举一个最简单的不可证明的例子：「这句话是假的」，非真也非伪。最终，我们可以说数学是要将可证明的结论证明，而与之相反，科学研究则是要将可证明的结论证伪。

### 4.6 Tests

Dijkstra once said,「Testing shows the presence, not the absence, of bugs.」In other words, a program can be proven incorrect by a test, but it cannot be proven correct. All that tests can do, after sufficient testing effort, is allow us to deem a program to be correct enough for our purposes.

The implications of this fact are stunning. Software development is not a mathematical endeavor, even though it seems to manipulate mathematical constructs. Rather, software is like a science. We show correctness by failing to prove incorrectness, despite our best efforts.

Such proofs of incorrectness can be applied only to provable programs. A program that is not provable — due to unrestrained use of goto, for example — cannot be deemed correct no matter how many tests are applied to it.

Structured programming forces us to recursively decompose a program into a set of small provable functions. We can then use tests to try to prove those small provable functions incorrect. If such tests fail to prove incorrectness, then we deem the functions to be correct enough for our purposes.

1『上面的信息太有感觉了，突然领悟到「测试」的真谛，功能拆解成一个个「小函数」，颗粒度越细越好，每个小函数做单元测试，每个小函数无法被证伪，那么组合起来的功能也是没法证伪的。（2020-12-24）』

Dijkstra 曾经说过「测试只能展示 Bug 的存在，并不能证明不存在 Bug」，换句话说，一段程序可以由一个测试来证明其错误性，但是却不能被证明是正确的。测试的作用是让我们得出某段程序已经足够实现当前目标这一结论。这一事实所带来的影响是惊人的。软件开发虽然看起来是在操作很多数学结构，其实不是一个数学研究过程。恰恰相反，软件开发更像是一门科学研究学科，我们通过无法证伪来证明软件的正确性。

注意，这种证伪过程只能应用于可证明的程序上。某段程序如果是不可证明的，例如，其中采用了不加限制的 goto 语句，那么无论我们为它写多少测试，也不能够证明其正确性。结构化编程范式促使我们先将一段程序递归降解为一系列可证明的小函数，然后再编写相关的测试来试图证明这些函数是错误的。如果这些测试无法证伪这些函数，那么我们就可以认为这些函数是足够正确的，进而推导整个程序是正确的。

## 0501. Object-Oriented Programming

### Conclusion

What is OO? There are many opinions and many answers to this question. To the software architect, however, the answer is clear: OO is the ability, through the use of polymorphism, to gain absolute control over every source code dependency in the system. It allows the architect to create a plugin architecture, in which modules that contain high-level policies are independent of modules that contain low-level details. The low-level details are relegated to plugin modules that can be deployed and developed independently from the modules that contain high-level policies.

面向对象编程到底是什么？业界在这个问题上存在着很多不同的说法和意见。然而对一个软件架构师来说，其含义应该是非常明确的：面向对象编程就是以多态为手段来对源代码中的依赖关系进行控制的能力，这种能力让软件架构师可以构建出某种插件式架构，让高层策略性组件与底层实现性组件相分离，底层组件可以被编译成插件，实现独立于高层组件的开发和部署。

### 00

As we will see, the basis of a good architecture is the understanding and application of the principles of object-oriented design (OO). But just what is OO?

One answer to this question is「The combination of data and function.」Although often cited, this is a very unsatisfying answer because it implies that o.f() is somehow different from f(o). This is absurd. Programmers were passing data structures into functions long before 1966, when Dahl and Nygaard moved the function call stack frame to the heap and invented OO.

Another common answer to this question is「A way to model the real world.」This is an evasive answer at best. What does「modeling the real world」actually mean, and why is it something we would want to do? Perhaps this statement is intended to imply that OO makes software easier to understand because it has a closer relationship to the real world — but even that statement is evasive and too loosely defined. It does not tell us what OO is.

Some folks fall back on three magic words to explain the nature of OO: encapsulation, inheritance, and polymorphism. The implication is that OO is the proper admixture of these three things, or at least that an OO language must support these three things. Let’s examine each of these concepts in turn.

稍后我们会讲到，设计一个优秀的软件架构要基于对面向对象设计（Object-Oriented Design）的深入理解及应用。但我们首先得弄明白一个问题：究竟什么是面向对象？

对于这个问题，一种常见的回答是「数据与函数的组合」。这种说法虽然被广为引用，但总显得并不是那么贴切，因为它似乎暗示了。o.f() 与 f(o) 之间是有区别的，这显然不是事实。面向对象理论是在 1966 年提出的，当时 Dah 和 Nygaard 主要是将函数调用栈迁移到了堆区域中。数据结构被用作函数的调用参数这件事情远比这发生的时间更早。

另一种常见的回答是「面向对象编程是一种对真实世界进行建模的方式」，这种回答只能算作避重就轻。「对真实世界的建模」到底要如何进行？我们为什么要这么做，有什么好处？也许这句话意味着是「由于采用面向对象方式构建的软件与真实世界的关系更紧密，所以面向对象编程可以使得软件开发更容易」—— 即使这样说，也仍然逃避了关键问题 一一 面向对象编程究竟是什么？

还有些人在回答这个问题的时候，往往会搬出一些神秘的词语，譬如封装（encapsulation）、继承（(inheritance）、多态（polymorphism）。其隐含意思就是说面向对象编程是这三项的有机组合，或者任何一种支持面向对象的编程语言必须支持这三个特性。那么，我们接下来可以逐个来分析一下这三个概念。

### 5.1 Encapsulation?

The reason encapsulation is cited as part of the definition of OO is that OO languages provide easy and effective encapsulation of data and function. As a result, a line can be drawn around a cohesive set of data and functions. Outside of that line, the data is hidden and only some of the functions are known. We see this concept in action as the private data members and the public member functions of a class. This idea is certainly not unique to OO. Indeed, we had perfect encapsulation in C. Consider this simple C program:

point.h

```c
struct Point;
struct Point* makePoint(double x, double y);
double distance (struct Point *p1, struct Point *p2);
```

point.c

```c
#include "point.h"
#include <stdlib.h>
#include <math.h> 

struct Point {  
    double x,y;
}; 

struct Point* makepoint(double x, double y) {  
    struct Point* p = malloc(sizeof(struct Point));  
    p->x = x;  
    p->y = y;  
    return p;
} 

double distance(struct Point* p1, struct Point* p2) {  
    double dx = p1->x - p2->x;  
    double dy = p1->y - p2->y;  
    return sqrt(dx*dx+dy*dy);
}
```

The users of point.h have no access whatsoever to the members of struct Point. They can call the makePoint() function, and the distance() function, but they have absolutely no knowledge of the implementation of either the Point data structure or the functions.

This is perfect encapsulation — in a non-OO language. C programmers used to do this kind of thing all the time. We would forward declare data structures and functions in header files, and then implement them in implementation files. Our users never had access to the elements in those implementation files. 

But then came OO in the form of C++ — and the perfect encapsulation of C was broken. The C++ compiler, for technical reasons, 1 needed the member variables of a class to be declared in the header file of that class. So our Point program changed to look like this:

point.h

```c
class Point {
    public:  
        Point(double x, double y);  
        double distance(const Point& p) const; 
    
    private:  
        double x;  
        double y;
};
```

point.cc

```c
#include "point.h"
#include <math.h> 

Point::Point(double x, double y)
: x(x), y(y)
{}

double Point::distance(const Point& p) const {  
    double dx = x-p.x;  
    double dy = y-p.y;  
    return sqrt(dx*dx + dy*dy);
}
```

Clients of the header file point.h know about the member variables x and y! The compiler will prevent access to them, but the client still knows they exist. For example, if those member names are changed, the point.cc file must be recompiled! Encapsulation has been broken.

Indeed, the way encapsulation is partially repaired is by introducing the public, private, and protected keywords into the language. This, however, was a hack necessitated by the technical need for the compiler to see those variables in the header file.

Java and C# simply abolished the header/implementation split altogether, thereby weakening encapsulation even more. In these languages, it is impossible to separate the declaration and definition of a class.

For these reasons, it is difficult to accept that OO depends on strong encapsulation. Indeed, many OO languages 2 have little or no enforced encapsulation.

OO certainly does depend on the idea that programmers are well-behaved enough to not circumvent encapsulated data. Even so, the languages that claim to provide OO have only weakened the once perfect encapsulation we enjoyed with C.

1 The C++ compiler needs to know the size of the instances of each class.

2 For example, Smalltalk, Python, JavaScript, Lua, and Ruby.

由于面向对象编程语言为我们方便而有效地封装数据和函数提供了有力的支持，导致封装这个概念经常被引用为面向对象编程定义的一部分。通过采用封装特性，我们可以把一组相关联的数据和函数圈起来，使圈外面的代码只能看见部分函数，数据则完全不可见。如，在实际应用中，类（class）中的公共函数和私有成员变量就是这样。然而，这个特性其实并不是面向对象编程所独有的。其实，C 语言也支持完整的封装，下面来看一个简单的 C 程序。

显然，使用 point.h 的程序是没有 Point 结构体成员的访问权限的。它们只能调用 makepoint() 函数和 distance() 函数，但对它们来说，Point 这个数据结构体的内部细节，以及函数的具体实现方式都是不可见的。

这正是完美封装 一一 虽然 C 语言是非面向对象的编程语言。上述 C 程序是很常见的。在头文件中进行数据结构以及函数定义的前置声明（forward declare），然后在程序文件中具体实现。程序文件中的具体实现细节对使用者来说是不可见的。而 C++ 作为一种面向对象编程语言，反而破坏了 C 的完美封装性。由于一些技术原因，C++ 编译器要求类的成员变量必须在该类的头文件中声明。这样一来，我们的 point.h 程序随之就改成了这样。

好了，point.h 文件的使用者现在知道了成员变量 x 和 y 的存在！虽然编译器会禁止对这两个变量的直接访问，但是使用者仍然知道了它们的存在。而且，如果 x 和 y 变量名称被改变了，point.c 也必须重新编译才行！这样的封装性显然是不完美的。

当然，C++ 通过在编程语言层面引入 public、private、protected 这些关键词，部分维护了封装性。但所有这些都是为了解决编译器自身的技术实现问题而引入的 hack —— 编译器由于技术实现原因必须在头文件中看到成员变量的定义。

而 Java 和 C# 则彻底抛弃了头文件与实现文件分离的编程方式，这其实进一步削弱了封装性。因为在这些语言中，我们是无法区分一个类的声明和定义的。由于上述原因，我们很难说强封装是面向对象编程的必要条件。而事实上，有很多面向对象编程语言对封装性并没有强制性的要求。

面向对象编程在应用上确实会要求程序员尽量避免破坏数据的封装性。但实际情是，那些声称自己提供面向对象编程支持的编程语言，相对于 C 这种完美封装的语言而言，其封装性都被削弱了，而不是加强了。

### 5.2 Inheritance?

If OO languages did not give us better encapsulation, then they certainly gave us inheritance.

Well — sort of Inheritance is simply the redeclaration of a group of variables and functions within an enclosing scope. This is something C programmers 3 were able to do manually long before there was an OO language. Consider this addition to our original point.h C program:

namedPoint.h

```c
struct NamedPoint; 
struct NamedPoint* makeNamedPoint(double x, double y, char* name);
void setName(struct NamedPoint* np, char* name);
char* getName(struct NamedPoint* np);
```

namedPoint.c

```c
#include "namedPoint.h"
#include <stdlib.h> 

struct NamedPoint {  
    double x,y;  
    char* name;
}; 

struct NamedPoint* makeNamedPoint(double x, double y, char* name) {  
    struct NamedPoint* p = malloc(sizeof(struct NamedPoint));  
    p->x = x;  
    p->y = y; 
    p->name = name;  
    return p;
} 

void setName(struct NamedPoint* np, char* name) {  
    np->name = name;
} 

char* getName(struct NamedPoint* np) {  
    return np->name;
}
```

main.c

```c
#include "point.h"
#include "namedPoint.h"
#include <stdio.h> 

int main(int ac, char** av) {  
    struct NamedPoint* origin = makeNamedPoint(0.0, 0.0, "origin");   
    struct NamedPoint* upperRight = makeNamedPoint(1.0, 1.0, "upperRight");
    printf("distance=%f\n",    
        distance(
            (struct Point*) origin, 
            (struct Point*) upperRight));
}
```

If you look carefully at the main program, you’ll see that the NamedPoint data structure acts as though it is a derivative of the Point data structure. This is because the order of the first two fields in NamedPoint is the same as Point. In short, NamedPoint can masquerade as Point because NamedPoint is a pure superset of Point and maintains the ordering of the members that correspond to Point.

This kind of trickery was a common practice 4 of programmers prior to the advent of OO. In fact, such trickery is how C++ implements single inheritance. Thus we might say that we had a kind of inheritance long before OO languages were invented. That statement wouldn’t quite be true, though. We had a trick, but it’s not nearly as convenient as true inheritance. Moreover, multiple inheritance is a considerably more difficult to achieve by such trickery.

Note also that in main.c, I was forced to cast the NamedPoint arguments to Point. In a real OO language, such upcasting would be implicit.

It’s fair to say that while OO languages did not give us something completely brand new, it did make the masquerading of data structures significantly more convenient.

To recap: We can award no point to OO for encapsulation, and perhaps a half-point for inheritance. So far, that’s not such a great score. But there’s one more attribute to consider.

3 Not just C programmers: Most languages of that era had the capability to masquerade one data structure as another.

4 Indeed it still is.

既然面向对象编程语言并没有提供更好的封装性，那么在继承性方面又如何呢？嗯，其实也就一般般吧。简而言之，继承的主要作用是让我们可以在某个作用域内对外部定义的某一组变量与函数进行覆盖。这事实上也是 C 程序员早在面向对象编程语言发明之前就一直在做的事了。下面，看一下刚才的 C 程序 point.h 的扩展版。

请仔细观察 main 函数，这里 NamedPoint 数据结构是被当作 Point 数据结构的一个衍生体来使用的。之所以可以这样做，是因为 NamedPoint 结构体的前两个成员的顺序与 Point 结构体的完全一致。简单来说，NamedPoint 之所以可以被伪装成 Point 来使用，是因为 NamedPoint 是 Point 结构体的一个超集，同时两者共同成员的顺序也是一样的。

上面这种编程方式虽然看上去有些投机取巧，但是在面向对象理论被提出之前，这已经很常见了。其实，C++ 内部就是这样实现单继承的。因此，我们可以说，早在面向对象编程语言被发明之前，对继承性的支持就已经存在很久了。当然了，这种支持用了一些投机取巧的手段，并不像如今的继承这样便利易用，而且，多重继承（multiple inheritance）如果还想用这种方法来实现，就更难了。同时应该注意的是，在 main.c 中，程序员必须强制将 NamedPoint 的参数类型转为 Point，而在真正的面向对象编程语言中，这种类型的向上转换通常应该是隐性的。

综上所述，我们可以认为，虽然面向对象编程在继承性方面并没有开创出新，但是的确在数据结构的伪装性上提供了相当程度的便利性。

回顾一下到目前为止的分析，面向对象编程在封装性上得 0 分，在继承性上勉强可以得 0.5 分（满分为 1）。下面，我们还有最后一个特性要讨论。

### 5.3 Polymorphism?

Did we have polymorphic behavior before OO languages? Of course we did. Consider this simple C copy program.

```c
#include <stdio.h>

void copy() {  
    int c;  
    while ((c=getchar()) != EOF)    
        putchar(c);
}
```

The function getchar() reads from STDIN. But which device is STDIN? The putchar() function writes to STDOUT. But which device is that? These functions are polymorphic — their behavior depends on the type of STDIN and STDOUT.

It’s as though STDIN and STDOUT are Java-style interfaces that have implementations for each device. Of course, there are no interfaces in the example C program — so how does the call to getchar() actually get delivered to the device driver that reads the character?

The answer to that question is pretty straightforward. The UNIX operating system requires that every IO device driver provide five standard functions: 5 open, close, read, write, and seek. The signatures of those functions must be identical for every IO driver.

The FILE data structure contains five pointers to functions. In our example, it might look like this:

```c
struct FILE {  
    void (*open)(char* name, int mode);  
    void (*close)();  int (*read)();  
    void (*write)(char);  
    void (*seek)(long index, int mode);
};
```

The IO driver for the console will define those functions and load up a FILE data structure with their addresses — something like this:

```c
#include "file.h" 

void open(char* name, int mode) {/*...*/}void close() {/*...*/};
int read() {int c;/*...*/ return c;}
void write(char c) {/*...*/}
void seek(long index, int mode) {/*...*/} 

struct FILE console = {open, close, read, write, seek};
```

Now if STDIN is defined as a FILE*, and if it points to the console data structure, then getchar() might be implemented this way:

```c
extern struct FILE* STDIN; 

int getchar() {  
    return STDIN->read();
}
```

In other words, getchar() simply calls the function pointed to by the read pointer of the FILE data structure pointed to by STDIN.

This simple trick is the basis for all polymorphism in OO. In C++, for example, every virtual function within a class has a pointer in a table called a vtable, and all calls to virtual functions go through that table. Constructors of derivatives simply load their versions of those functions into the vtable of the object being created.

The bottom line is that polymorphism is an application of pointers to functions. Programmers have been using pointers to functions to achieve polymorphic behavior since Von Neumann architectures were first implemented in the late 1940s. In other words, OO has provided nothing new.

Ah, but that’s not quite correct. OO languages may not have given us polymorphism, but they have made it much safer and much more convenient.

The problem with explicitly using pointers to functions to create polymorphic behavior is that pointers to functions are dangerous. Such use is driven by a set of manual conventions. You have to remember to follow the convention to initialize those pointers. You have to remember to follow the convention to call all your functions through those pointers. If any programmer fails to remember these conventions, the resulting bug can be devilishly hard to track down and eliminate.

OO languages eliminate these conventions and, therefore, these dangers. Using an OO language makes polymorphism trivial. That fact provides an enormous power that old C programmers could only dream of. 

On this basis, we can conclude that OO imposes discipline on indirect transfer of control.

5 UNIX systems vary; this is just an example.

在面向编程对象语言被发明之前，我们所使用的编程语言能支持多态吗？答案是肯定的，请注意看下面这段用 C 语言编写的 copy 程序。

在上述程序中，函数 getchar() 主要负责从 STDN 中读取数据。但是 STDN 究竟指代的是哪个设备呢？同样的道理，putchar() 主要负责将数据写入 STDOUT，而 STDOUT 又指代的是哪个设备呢？很显然，这类函数其实就具有多态性，因为它们的行为依赖于 STDN 和 STDOUTE 的具体类型。这里的 STDIN 和 STDOUT，与 Java 中的接口类似，各种设备都有各自的实现。当然，这个 C 程序中是没有接口这个概念的，那么 getchar() 这个调用的动作是如何真正传递到设备驱动程序中，从而读取到具体内容的呢？

其实很简单，UNIX 操作系统强制要求每个 IO 设备都要提供 open、close、read、write 和 seek 这 5 个标准函数。也就是说，每个 IO 设备驱动程序对这 5 种函数的实现在函数调用上必须保持一致。

首先，FILE 数据结构体中包含了相对应的 5 个函数指针，分别用于指向这些函数。换句话说，getchar() 只是调用了 STDIN 所指向的 FILE 数据结构体中的 read 函数指针指向的函数。

这个简单的编程技巧正是面向对象编程中多态的基础。例如在 C++ 中，类中的每个虚函数（virtual function）的地址都被记录在一个名叫 vtable 的数据结构里。我们对虚函数的每次调用都要先查询这个表，其衍生类的构造函数负责将该衍生类的虚函数地址加载到整个对象的 vtable。归根结底，多态其实不过就是函数指针的一种应用。自从 20 世纪 40 年代末期冯·诺依曼架构诞生那天起，程序员们就一直在使用函数指针模拟多态了。也就是说，面向对象编程在多态方面没有提出任何新概念当然了，面向对象编程语言虽然在多态上并没有理论创新，但它们也确实让多态变得更安全、更便于使用了。

用函数指针显式实现多态的问题就在于函数指针的危险性。毕竟，函数指针的调用依赖于一系列需要人为遵守的约定。程序员必须严格按照固定约定来初始化函数指针，并同样严格地按照约定来调用这些指针。只要有一个程序员没有守这些约定，整个程序就会产生极其难以跟踪和消除的 Bug。面向对象编程语言为我们消除了人工遵守这些约定的必要，也就等于消除了这方面的危险性。采用面向对象编程语言让多态实现变得非常简单，让一个传统 C 程序员可以去做以前不敢想的事情。综上所述，我们认为面向对象编程其实是对程序间接控制权的转移进行了约束。

#### 5.3.1 The Power of Polymorphism

What’s so great about polymorphism? To better appreciate its charms, let’s reconsider the example copy program. What happens to that program if a new IO device is created? Suppose we want to use the copy program to copy data from a handwriting recognition device to a speech synthesizer device: How do we need to change the copy program to get it to work with those new devices?

We don’t need any changes at all! Indeed, we don’t even need to recompile the copy program. Why? Because the source code of the copy program does not depend on the source code of the IO drivers. As long as those IO drivers implement the five standard functions defined by FILE, the copy program will be happy to use them.

In short, the IO devices have become plugins to the copy program.

Why did the UNIX operating system make IO devices plugins? Because we learned, in the late 1950s, that our programs should be device independent. Why? Because we wrote lots of programs that were device dependent, only to discover that we really wanted those programs to do the same job but use a different device.

For example, we often wrote programs that read input data from decks of cards, 6 and then punched new decks of cards as output. Later, our customers stopped giving us decks of cards and started giving us reels of magnetic tape. This was very inconvenient, because it meant rewriting large portions of the original program. It would be very convenient if the same program worked interchangeably with cards or tape.

The plugin architecture was invented to support this kind of IO device independence, and has been implemented in almost every operating system since its introduction. Even so, most programmers did not extend the idea to their own programs, because using pointers to functions was dangerous.

OO allows the plugin architecture to be used anywhere, for anything.

6 Punched cards — IBM Hollerith cards, 80 columns wide. I'm sure many of you have never even seen one of these, but they were commonplace in the 1950s, 1960s, and even 1970s.

那么多态的优势在哪里呢？为了让读者更好地理解多态的好处，我们需要再来看一下刚才的 copy 程序。如果要支持新的 IO 设备，该程序需要做什么改动呢？譬如，假设我们想要用该 copy 程序从一个手写识别设备将数据复制到另一个语音合成设备中，我们需要针对 copy 程序做什么改动，才能实现这个目标呢？

答案是完全不需要做任何改动！确实，我们甚至不需要重新编译该 copy 程序。为什么？因为 copy 程序的源代码并不依赖于 IO 设备驱动程序的代码。只要 IO 设备驱动程序实现了 FILE 结构体中定义的 5 个标准函数，该 copy 程序就可以正常使用它们。简单来说，IO 设备变成了 copy 程序的插件。

为什么 UNIX 操作系统会将 IO 设备设计成插件形式呢？因为自 20 世纪 50 年代未期以来，我们学到了ー个重要经验：程序应该与设备无关。这个经验从何而来呢？因为一度所有程序都是设备相关的，但是后来我们发现自己其实真正需要的是在不同的设备上实现同样的功能。

例如，我们曾经写过一些程序，需要从卡片盒中的打孔卡片读取数据，同时要通过在新的卡片上打孔来输出数据。后来，客户不再使用打孔卡片，而开始使用磁带卷了。这就给我们帯来了很多麻烦，很多程序都需要重写。于是我们就会想，如果这段程序可以同时操作打孔卡片和磁带那该多好。插件式架构就是为了支持这种 IO 不相关性而发明的，它几乎在随后的所有操作系統中都有应用。但即使多态有如此多优点，大部分程序员还是没有将插件特性引入他们自己的程序中，因为函数指针实在是太危险了，而面向对象编程的出现使得这种插件式架构可以在任何地方被安全地使用。

#### 5.3.2 Dependency Inversion

Imagine what software was like before a safe and convenient mechanism for polymorphism was available. In the typical calling tree, main functions called high-level functions, which called mid-level functions, which called low-level functions. In that calling tree, however, source code dependencies inexorably followed the flow of control (Figure 5.1).

Figure 5.1  Source code dependencies versus flow of control

For main to call one of the high-level functions, it had to mention the name of the module that contained that function In C, this was a `#include`. In Java, it was an `import` statement. In C#, it was a `using` statement. Indeed, every caller was forced to mention the name of the module that contained the callee.

This requirement presented the software architect with few, if any, options. The flow of control was dictated by the behavior of the system, and the source code dependencies were dictated by that flow of control.

When polymorphism is brought into play, however, something very different can happen (Figure 5.2).

Figure 5.2  Dependency inversion

In Figure 5.2, module HL1 calls the F() function in module ML1. The fact that it calls this function through an interface is a source code contrivance. At runtime, the interface doesn’t exist. HL1 simply calls F() within ML1. [7]

Note, however, that the source code dependency (the inheritance relationship) between ML1 and the interface I points in the opposite direction compared to the flow of control. This is called dependency inversion, and its implications for the software architect are profound.

The fact that OO languages provide safe and convenient polymorphism means that any source code dependency, no matter where it is, can be inverted.

Now look back at that calling tree in Figure 5.1, and its many source code dependencies. Any of those source code dependencies can be turned around by inserting an interface between them.

With this approach, software architects working in systems written in OO languages have absolute control over the direction of all source code dependencies in the system. They are not constrained to align those dependencies with the flow of control. No matter which module does the calling and which module is called, the software architect can point the source code dependency in either direction.

That is power! That is the power that OO provides. That’s what OO is really all about — at least from the architect’s point of view.

What can you do with that power? As an example, you can rearrange the source code dependencies of your system so that the database and the user interface (UI) depend on the business rules (Figure 5.3), rather than the other way around.

Figure 5.3  The database and the user interface depend on the business rules

This means that the UI and the database can be plugins to the business rules. It means that the source code of the business rules never mentions the UI or the database.

As a consequence, the business rules, the UI, and the database can be compiled into three separate components or deployment units (e.g., jar files, DLLs, or Gem files) that have the same dependencies as the source code. The component containing the business rules will not depend on the components containing the UI and database.

In turn, the business rules can be deployed independently of the UI and the database. Changes to the UI or the database need not have any effect on the business rules. Those components can be deployed separately and independently.

In short, when the source code in a component changes, only that component needs to be redeployed. This is independent deployability.

If the modules in your system can be deployed independently, then they can be developed independently by different teams. That’s independent developability.

7 Albeit indirectly.

1-2『依赖倒置的核心是通过增加一个「接口」实现依赖的反转，这样的话任何「控制流」的流向都可以通过实际情况来调整。目前不明白的是，加「接口」跟「面向对象」编程范式有啥必要的联系，加接口就一定属于面向对象？这节的信息，让自己对依赖导致有了一个更深的印象。回复：前面的疑虑，关键点应该在「多态」上，继承是从子类的角度往上看父类，多态是从父类的角度往下看子类。依赖倒置做一张术语卡片。（2020-12-25）』——已完成

我们可以想象一下在安全和便利的多态支持出现之前，软件是什么样子的。下面有一个典型的调用树的例子，main 函数调用了一些高层函数，这些高层函数又调用了一些中层函数，这些中层函数又继续调用了一些底层函数。在这里，源代码层面的依赖不可避免地要跟随程序的控制流（详见图 5.2）。

如你所见，main 函数为了调用高层函数，它就必须能够看到这个函数所在的模块。在 C 中，我们会通过 #include 来实现，在 Java 中则通过 import 来实现，而在 C# 中则用的是 using 语句。总之，每个函数的调用方都必须要引用被调用方所在的模块。显然，这样做就导致了我们在软件架构上别无选择。在这里，系统行为决定了控制流，而控制流则决定了源代码依赖关系。但一旦我们使用了多态，情况就不一样了（详见图 5.2）。

在图 5.2 中，模块 HL1 调用了 ML1 模块中的 F() 函数，这里的调用是通过源代码级别的接口来实现的。当然在程序实际运行时，接口这个概念是不存在的，HL1 会调用 ML1 中的 F() 函数。请注意模块 ML1 和接口在源代码上的依赖关系（或者叫继承关系），该关系的方向和控制流正好是相反的，我们称之为依赖反转。这种反转对软件架构设计的影响是非常大的。事实上，通过利用面向编程语言所提供的这种安全便利的多态实现，无论我们面对怎样的源代码级别的依赖关系，都可以将其反转。现在，我们可以再回头来看图 5.1 中的调用树，就会发现其中的众多源代码依赖关系都可以通过引入接口的方式来进行反转。

通过这种方法，软件架构师可以完全控制采用了面向对象这种编程方式的系统中所有的源代码依赖关系，而不再受到系统控制流的限制。不管哪个模块调用或者被调用，软件架构师都可以随意更改源代码依赖关系。这就是面向对象编程的好处，同时也是面向对象编程这种范式的核心本质 —— 至少对一个软件架构师来说是这样的。

这种能力有什么用呢？在下面的例子中，我们可以用它来让数据库模块和用户界面模块都依赖于业务逻辑模块（见图 5.3），而非相反。这意味着我们让用户界面和数据库都成为业务逻辑的插件。也就是说，业务逻辑模块的源代码不要引入用户界面和数据库这两个模块。

这样一来，业务逻辑、用户界面以及数据库就可以被编译成三个独立的组件或者部暑单元（例如 jar 文件、DLL 文件、Gem 文件等）了，这些组件或者部署单元的依赖关系与源代码的依赖关系是一致的，业务逻辑组件也不会依赖于用户界面和数据库这两个组件于是，业务逻辑组件就可以独立于用户界面和数据库来进行部署了，我们对用户界面或者数据库的修改将不会对业务逻辑产生任何影响，这些组件都可以被分别、独立地部署简单来说，当某个组件的源代码需要修改时，仅仅需要重新部署该组件，不需要更改其他组件，这就是独立部署能力。如果系统中的所有组件都可以独立部暑，那它们就可以由不同的团队并行开发，这就是所谓的独立开发能力。

## 0601. Functional Programming

### Conclusion

To summarize: 1) Structured programming is discipline imposed upon direct transfer of control. 2) Object-oriented programming is discipline imposed upon indirect transfer of control. 3) Functional programming is discipline imposed upon variable assignment.

Each of these three paradigms has taken something away from us. Each restricts some aspect of the way we write code. None of them has added to our power or our capabilities. What we have learned over the last half-century is what not to do.

With that realization, we have to face an unwelcome fact: Software is not a rapidly advancing technology. The rules of software are the same today as they were in 1946, when Alan Turing wrote the very first code that would execute in an electronic computer. The tools have changed, and the hardware has changed, but the essence of software remains the same.

Software — the stuff of computer programs — is composed of sequence, selection, iteration, and indirection. Nothing more. Nothing less.

下面我们来总结一下：1）结构化编程是对程序控制权的直接转移的限制。2）面向对象编程是对程序控制权的间接转移的限制。3）函数式编程是对程序中賦值操作的限制。

这三个编程范式都对程序员提出了新的限制。每个范式都约束了某种编写代码的方式，没有一个编程范式是在增加新能力。也就是说，我们过去 50 年学到的东西主要是什么不应该做。我们必须面对这种不友好的现实：软件构建并不是一个迅速前进的技术。今天构建软件的规则和 1946 年阿兰图灵写下电子计算机的第一行代码时是一样的。尽管工具変化了，硬件变化了，但是软件编程的核心没有变。总而言之，软件，或者说计算机程序无一例外是由顺序结构、分支结构、循环结构和间接转移这几种行为组合而成的，无可增加，也缺一不可。

### 00

In many ways, the concepts of functional programming predate programming itself. This paradigm is strongly based on the λ-calculus invented by Alonzo Church in the 1930s.

函数式编程所依赖的原理，在很多方面其实是早于编程本身出现的。因为函数式编程这种范式强烈依赖于 Alonzo Church 在 20 世纪 30 年代发明的 λ 演算。

### 6.1 Squares of Integers

To explain what functional programming is, it's best to examine some examples. Let’s investigate a simple problem: printing the squares of the first 25 integers. In a language like Java, we might write the following:

```c
public class Squint {
    public static void main(String args[]) {
        for (int i=0; i<25; i++)
            System.out.println(i*i);
    }
}
```

In a language like Clojure, which is a derivative of Lisp, and is functional, we might implement this same program as follows:

```c
(println (take 25 (map (fn [x] (* x x)) (range))))
```

If you don’t know Lisp, then this might look a little strange. So let me reformat it a bit and add some comments.

```c
(println ;___________________ Print
  (take 25 ;_________________ the first 25
    (map (fn [x] (* x x)) ;__ squares
      (range)))) ;___________ of Integers
```

It should be clear that println, take, map, and range are all functions. In Lisp, you call a function by putting it in parentheses. For example, `(range)` calls the range function. The expression `(fn [x] (* x x))` is an anonymous function that calls the multiply function, passing its input argument in twice. In other words, it computes the square of its input.

Looking at the whole thing again, it’s best to start with the innermost function call. The range function returns a never-ending list of integers starting with 0. This list is passed into the map function, which calls the anonymous squaring function on each element, producing a new never-ending list of all the squares.

The list of squares is passed into the take function, which returns a new list with only the first 25 elements. The println function prints its input, which is a list of the first 25 squares of integers.

If you find yourself terrified by the concept of never-ending lists, don’t worry. Only the first 25 elements of those never-ending lists are actually created. That’s because no element of a never-ending list is evaluated until it is accessed.

If you found all of that confusing, then you can look forward to a glorious time learning all about Clojure and functional programming. It is not my goal to teach you about these topics here.

Instead, my goal here is to point out something very dramatic about the difference between the Clojure and Java programs. The Java program uses a mutable variable — a variable that changes state during the execution of the program. That variable is i — the loop control variable. No such mutable variable exists in the Clojure program. In the Clojure program, variables like x are initialized, but they are never modified.

This leads us to a surprising statement: Variables in functional languages do not vary.

很明显，这里的 println、take、map 和 lrange 都是函数。在 LISP 中，函数是通过括号来调用的，例如 `(range)` 表达式就是在调用 range 函数。而表达式 `(fn [x] (*xx))` 则是一个匿名函数，该函数用同样的值作为参数调用了乘法函数。换句话说，该函数计算的是平方值。

现在让我们回过头来再看一下这整句代码，从最内侧的函数调用开始  ranger 函数会返回一个从 0 开始的整数无穷列表。然后该列表会被传入 map 函数，并针对列表中的每个元素，调用求平方值的匿名函数，产生了一个无穷多的、包含平方值的列表接着再将这个列表传入 take 函数，后者会返回一个仅包含前 25 个元素的新列表。println 函数将它的参数输出，该参数就是上面这个包含了 25 个平方值的列表。

读者不用担心上面提到的无穷列表。因为这些列表中的元素只有在被访时会被创建，所以实际上只有前 25 个元素是真正被创建了的。如果上述内容还是让读者觉得云里雾里的话，可以自行学习ー下 Clojure 和函数式编程，本书的目标并不是要教你学会这门语言，因此不再展开。

相反，我们讨论它的主要目标是要突显出 Clojure 和 Java 这两种语言之间的巨大区别。在 Java 程序中，我们使用的是可变量，即变量，该变量的值会随着程序执行的过程而改变，故被称为循环控制変量。而 Clojure 程序中是不存在这种变量的，变量 x 旦被初始化之后，就不会再被更改了。这句话有点出人意料：函数式编程语言中的变量（Variable）是不可变（Vary）的。

### 6.2 Immutability and Architecture

Why is this point important as an architectural consideration? Why would an architect be concerned with the mutability of variables? The answer is absurdly simple: All race conditions, deadlock conditions, and concurrent update problems are due to mutable variables. You cannot have a race condition or a concurrent update problem if no variable is ever updated. You cannot have deadlocks without mutable locks.

In other words, all the problems that we face in concurrent applications — all the problems we face in applications that require multiple threads, and multiple processors — cannot happen if there are no mutable variables.

As an architect, you should be very interested in issues of concurrency. You want to make sure that the systems you design will be robust in the presence of multiple threads and processors. The question you must be asking yourself, then, is whether immutability is practicable.

The answer to that question is affirmative, if you have infinite storage and infinite processor speed. Lacking those infinite resources, the answer is a bit more nuanced. Yes, immutability can be practicable, if certain compromises are made. Let’s look at some of those compromises.

为什么不可变性是软件架构设计需要考虑的重点呢？为什么软件架构师要操心变量的可变性呢？答案显而易见：所有的竞争问题、死锁问题、并发更新问题都是由可变变量导致的。如果变量永远不会被更改，那就不可能产生竞争或者并发更新问题。如果锁状态是不可变的，那就永远不会产生死锁问题。换句话说，一切并发应用遇到的问题，一切由于使用多线程、多处理器而引起的问题，如果没有可变变量的话都不可能发生。

作为一个软件架构师，当然应该要对并发问题保持高度关注。我们需要确保自己设计的系统在多线程、多处理器环境中能稳定工作。所以在这里，我们实际应该要问的问题是：不可变性是否实际可行？

如果我们能忽略存储器与处理器在速度上的限制，那么答案是肯定的。否则的话，不可变性只有在一定情況下是可行的。下面让我们来看一下它具体该如何做到可行。

### 6.3 Segregation of Mutability

One of the most common compromises in regard to immutability is to segregate the application, or the services within the application, into mutable and immutable components. The immutable components perform their tasks in a purely functional way, without using any mutable variables. The immutable components communicate with one or more other components that are not purely functional, and allow for the state of variables to be mutated (Figure 6.1).

Figure 6.1 Mutating state and transactional memory

Since mutating state exposes those components to all the problems of concurrency, it is common practice to use some kind of transactional memory to protect the mutable variables from concurrent updates and race conditions. Transactional memory simply treats variables in memory the same way a database treats records on disk. 1 It protects those variables with a transaction- or retry-based scheme.

A simple example of this approach is Clojure’s atom facility:

```c
(def counter (atom 0)) ; initialize counter to 0
(swap! counter inc)    ; safely increment counter.
```

In this code, the counter variable is defined as an atom. In Clojure, an atom is a special kind of variable whose value is allowed to mutate under very disciplined conditions that are enforced by the swap! function.

The swap! function, shown in the preceding code, takes two arguments: the atom to be mutated, and a function that computes the new value to be stored in the atom. In our example code, the counter atom will be changed to the value computed by the inc function, which simply increments its argument.

The strategy used by swap! is a traditional compare and swap algorithm. The value of counter is read and passed to inc. When inc returns, the value of counter is locked and compared to the value that was passed to inc. If the value is the same, then the value returned by inc is stored in counter and the lock is released. Otherwise, the lock is released, and the strategy is retried from the beginning.

The atom facility is adequate for simple applications. Unfortunately, it cannot completely safeguard against concurrent updates and deadlocks when multiple dependent variables come into play. In those instances, more elaborate facilities can be used.

The point is that well-structured applications will be segregated into those components that do not mutate variables and those that do. This kind of segregation is supported by the use of appropriate disciplines to protect those mutated variables. Architects would be wise to push as much processing as possible into the immutable components, and to drive as much code as possible out of those components that must allow mutation.

1 I know… What’s a disk?

可变性的隔离

一种常见方式是将应用程序，或者是应用程序的内部服务进行切分，划分为可变的和不可变的两种组件。不可变组件用纯函数的方式来执行任务，期间不更改任何状态。这些不可变的组件将通过与一个或多个非函数式组件通信的方式来修改变量状态（参见图 6.1）。

由于状态的修改会导致一系列并发问题的产生，所以我们通常会采用某种事务型内存来保护可变变量，避免同步更新和竞争状态的发生。事务型内存基本上与数据库保护磁盘数据的方式类似，通常采用的是事务或者重试机制。下面我们可以用 Clojure 中的 atom 机制来写一个简单的例子。

在这段代码中，counter 变量被定义为 atom 类型。在 Clojurer 中，atom 是一类特殊的变量，它被允许在 swap! 函数定义的严格条件下进行更改。至于 swap! 函数，如同上面代码所写，它需要两个参数：一个是被用来修改的 atom 类型实例，另一个是用来计算新值的函数。在上面的代码中，inc 函数会将参数加 1 并存入 counter 这个 atom 实例。

在这里，swap! 所采用的策略是传统的比较替换算法。即先读取 counter 变量的值，再将其传入 inc 函数。然后当 inc 函数返回时，将原先用锁保护起来的 counter 值与传入 inc 时的值进行比较。如果两边的值一致，则将 inc 函数返回的值存入 counter，释放锁。否则，先释放锁，再从头进行重试。

当然，atom 这个机制只适用于上面这种简单的应用程序，它并不适用于解决由多个相关变量同时需要更改所引发的并发更新问题和死锁问题，要想解决这些问题，我们就需要用到更复杂的机制。这里的要点是：一个架构设计良好的应用程序应该将状态修改的部分和不需要修改状的部分隔离成单独的组件，然后用合适的机制来保护可变量。软件架构师应该着力于将大部分处理逻辑都归于不可变组件中，可变状态组件的逻辑应该越少越好。

### 6.4 Event Sourcing

The limits of storage and processing power have been rapidly receding from view. Nowadays it is common for processors to execute billions of instructions per second and to have billions of bytes of RAM. The more memory we have, and the faster our machines are, the less we need mutable state.

As a simple example, imagine a banking application that maintains the account balances of its customers. It mutates those balances when deposit and withdrawal transactions are executed.

Now imagine that instead of storing the account balances, we store only the transactions. Whenever anyone wants to know the balance of an account, we simply add up all the transactions for that account, from the beginning of time. This scheme requires no mutable variables.

Obviously, this approach sounds absurd. Over time, the number of transactions would grow without bound, and the processing power required to compute the totals would become intolerable. To make this scheme work forever, we would need infinite storage and infinite processing power.

But perhaps we don’t have to make the scheme work forever. And perhaps we have enough storage and enough processing power to make the scheme work for the reasonable lifetime of the application.

This is the idea behind event sourcing. 2 Event sourcing is a strategy wherein we store the transactions, but not the state. When state is required, we simply apply all the transactions from the beginning of time. Of course, we can take shortcuts. For example, we can compute and save the state every midnight. Then, when the state information is required, we need compute only the transactions since midnight.

2『时间溯源，做一张术语卡片。』——已完成

Now consider the data storage required for this scheme: We would need a lot of it. Realistically, offline data storage has been growing so fast that we now consider trillions of bytes to be small — so we have a lot of it.

More importantly, nothing ever gets deleted or updated from such a data store. As a consequence, our applications are not CRUD; they are just CR. Also, because neither updates nor deletions occur in the data store, there cannot be any concurrent update issues.

If we have enough storage and enough processor power, we can make our applications entirely immutable — and, therefore, entirely functional.

If this still sounds absurd, it might help if you remembered that this is precisely the way your source code control system works.

2 Thanks to Greg Young for teaching me about this concept.

事件溯源

随着存储和处理能力的大幅进步，现在拥有每秒可以执行数十亿条指令的处理器，以及数十亿字节内存的计算机已经很常见了。而内存越大，处理速度越快，我们对可变状态的依赖就会越少。

举个简单的例子，假设某个银行应用程序需要维护客户账户余额信息，当它执行存取款事务时，就要同时负责修改余额记录。如果我们不保存具体账户余额，仅仅保存事务日志，那么当有人想查询账户余额时，我们就将全部交易记录取出，并且每次都得从最开始到当下进行累计。当然，这样的设计就不需要维护任何可变变量了。

但显而易见，这种实现是有些不合理的。因为随着时间的推移，事务的数目会无限制增长，每次处理总额所需要的处理能力很快就会变得不能接受。如果想使这种设计永远可行的话，我们将需要无限容量的存储，以及无限的处理能力。但是可能我们并不需要这个设计永远可行，而且可能在整个程序的生命周期内，我们有足够的存储和处理能力来满足它。

这就是事件溯源，在这种体系下，我们只存储事务记录，不存储具体状态。当需要具体状态时，我们只要从头开始计算所有的事务即可。在存储方面，这种架构的确要很大的存储容量。如今离线数据存储器的增长是非常快的，现在 1TB 对我们来说也已经不算什么了。更重要的是，这种数据存储模式中不存在除和更新的情况，我们的应用程序不是 CRUD，而是 CR。因为更新和删除这两种操作都不存在了，自然也就不存在并发问题。

如果我们有足够大的存储量和处理能力，应用程序就可以用完全不可变的、纯函数式的方式来编程。如果读者还是觉得这听起来不太靠谱，可以想想我们现在用的源代码管理程序，它们正是用这种方式工作的！
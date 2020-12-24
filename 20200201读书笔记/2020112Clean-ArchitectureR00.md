# 2020112Clean-ArchitectureR00

## 记忆时间

## 卡片

### 0101. 主题卡 —— The architecture rules are the same

I’ve built a lot of apps. I’ve built a lot of systems. And from them all, and by taking them all into consideration, I’ve learned something startling.

The architecture rules are the same!

1『软件架构的底层逻辑是相同的，做一张主题卡片。』—— 已完成

This is startling because the systems that I have built have all been so radically different. Why should such different systems all share similar rules of architecture? My conclusion is that the rules of  software architecture are independent of  every other variable.

This is even more startling when you consider the change that has taken place in hardware over the same half-century. I started programming on machines the size of kitchen refrigerators that had half-megahertz cycle times, 4K of core memory, 32K of disk memory, and a 10 character per second teletype interface. I am writing this preface on a bus while touring in South Africa. I am using a MacBook with four i7 cores running at 2.8 gigahertz each. It has 16 gigabytes of RAM, a terabyte of SSD, and a 2880*1800 retina display capable of showing extremely high-definition video. The difference in computational power is staggering. Any reasonable analysis will show that this MacBook is at least 1022 more powerful than those early computers that I started using half a century ago.

Twenty-two orders of magnitude is a very large number. It is the number of angstroms from Earth to Alpha-Centuri. It is the number of electrons in the change in your pocket or purse. And yet that number — that number at least — is the computational power increase that I have experienced in my own lifetime.

And with all that vast change in computational power, what has been the effect on the software I write? It’s gotten bigger certainly. I used to think 2000 lines was a big program. After all, it was a full box of cards that weighed 10 pounds. Now, however, a program isn’t really big until it exceeds 100,000 lines.

The software has also gotten much more performant. We can do things today that we could scarcely dream about in the 1960s. The Forbin Project, The Moon Is a Harsh Mistress, and 2001: A Space Odyssey all tried to imagine our current future, but missed the mark rather significantly. They all imagined huge machines that gained sentience. What we have instead are impossibly small machines that are still … just machines.

And there is one thing more about the software we have now, compared to the software from back then: It’s made of  the same stuff. It’s made of if statements, assignment statements, and while loops.

Oh, you might object and say that we’ve got much better languages and superior paradigms. After all, we program in Java, or C#, or Ruby, and we use object-oriented design. True — and yet the code is still just an assemblage of sequence, selection, and iteration, just as it was back in the 1960s and 1950s.

When you really look closely at the practice of programming computers, you realize that very little has changed in 50 years. The languages have gotten a little better. The tools have gotten fantastically better. But the basic building blocks of a computer program have not changed.

If I took a computer programmer from 1966 forward in time to 2016 and put her [1] in front of my MacBook running IntelliJ and showed her Java, she might need 24 hours to recover from the shock. But then she would be able to write the code. Java just isn’t that different from C, or even from Fortran.

And if I transported you back to 1966 and showed you how to write and edit PDP-8 code by punching paper tape on a 10 character per second teletype, you might need 24 hours to recover from the disappointment. But then you would be able to write the code. The code just hasn’t changed that much.

That’s the secret: This changelessness of the code is the reason that the rules of software architecture are so consistent across system types. The rules of software architecture are the rules of ordering and assembling the building blocks of programs. And since those building blocks are universal and haven’t changed, the rules for ordering them are likewise universal and changeless.

Younger programmers might think this is nonsense. They might insist that everything is new and different nowadays, that the rules of the past are past and gone. If that is what they think, they are sadly mistaken. The rules have not changed. Despite all the new languages, and all the new frameworks, and all the paradigms, the rules are the same now as they were when Alan Turing wrote the first machine code in 1946.

But one thing has changed: Back then, we didn’t know what the rules were. Consequently, we broke them, over and over again. Now, with half a century of experience behind us, we have a grasp of those rules.

And it is those rules — those timeless, changeless, rules — that this book is all about.

### 0102. 主题卡 —— 三大编程范式

面向结构编程、面向对象编程、函数式编程。

What does this history lesson on paradigms have to do with architecture? Everything. We use polymorphism as the mechanism to cross architectural boundaries; we use functional programming to impose discipline on the location of and access to data; and we use structured programming as the algorithmic foundation of our modules. Notice how well those three align with the three big concerns of architecture: function, separation of components, and data management.

大家可能会问，这些编程范式的历史知识与软件架构有关系吗？当然有，而且关系相当密切。譬如说，多态是我们跨越架构边界的手段，函数式编程是我们规范和限制数据存放位置与访问权限的手段，结构化编程则是各模块的算法实现基础。这和软件架构的三大关注重点不谋而合：功能性、组件独立性以及数据管理。

The first paradigm to be adopted (but not the first to be invented) was structured programming, which was discovered by Edsger Wybe Dijkstra in 1968. Dijkstra showed that the use of unrestrained jumps (goto statements) is harmful to program structure. As we’ll see in the chapters that follow, he replaced those jumps with the more familiar if/then/else and do/while/until constructs. We can summarize the structured programming paradigm as follows: Structured programming imposes discipline on direct transfer of  control.

结构化编程是第一个普遍被采用的编程范式（但是却不是第一个被提出的），由 Edsger Wybe Dijkstra 于 1968 年最先提出。与此同时，Dijkstra 还论证了使用 goto 这样的无限制跳转语句将会损害程序的体结构。接下来的章节我们还会说到，也是这位 Dijkstra 最先主张用我们现在熟知的 f/then/else 语句和 do/while/unt 语句来代替跳转语句的。我们可以将结构化编程范式归结为一句话：结构化程对程序控制权的直接转移进行了限制和规范。

The second paradigm to be adopted was actually discovered two years earlier, in 1966, by Ole Johan Dahl and Kristen Nygaard. These two programmers noticed that the function call stack frame in the ALGOL language could be moved to a heap, thereby allowing local variables declared by a function to exist long after the function returned. The function became a constructor for a class, the local variables became instance variables, and the nested functions became methods. This led inevitably to the discovery of polymorphism through the disciplined use of function pointers. We can summarize the object-oriented programming paradigm as follows: Object-oriented programming imposes discipline on indirect transfer of  control.

1-3『这里对面向对象编程底层逻辑的描述，联想到学 JS 时，看亚历山大那个 CEO 的系列文章里，介绍闭包相关知识时，有相通的感觉。（2020-12-24）』

说到编程领域中第二个被广泛采用的编程范式，当然就是面向对象编程了。事实上，这个编程范式的提出比结构化编程还早了两年，是在 1966 年由 Ole Johan Dahl 和 Kriste Nygaard 在论文中总结归纳出来的。这两个程序员注意到在 ALGOLT 语言中，函数调用堆栈（call stack frame）可以被挪到堆存区域里，这样函数定义的本地变量就可以在函数返回之后继续存在。这个函数就成为了一个类（class）的构造函数，而它所定义的本地变量就是类的成员变量，构造函数定义的嵌套函数就成为了成员方法（method）。这样一来，我们就可以利用多态（polymorphism）来限制用户对函数指针的使用。在这里，我们也可以用一句话来总结面向对象编程：面向对象程对程序控制权的间接转移进行了限制和规范。

The third paradigm, which has only recently begun to be adopted, was the first to be invented. Indeed, its invention predates computer programming itself. Functional programming is the direct result of the work of Alonzo Church, who in 1936 invented λ-calculus while pursuing the same mathematical problem that was motivating Alan Turing at the same time. His λ-calculus is the foundation of the LISP language, invented in 1958 by John McCarthy. A foundational notion of λ-calculus is immutability — that is, the notion that the values of symbols do not change. This effectively means that a functional language has no assignment statement. Most functional languages do, in fact, have some means to alter the value of a variable, but only under very strict discipline. We can summarize the functional programming paradigm as follows: Functional programming imposes discipline upon assignment.

尽管第三个编程范式是近些年オ刚刚开始被采用的，但它其实是三个范式中最先被发明的。事实上，函数式编程概念是基于与阿兰·图灵同时代的数学家 Alonzo Church 在 1936 年发明的 λ 演算的直接衍生物。1958 年 John Mccarthy 利用其作为基础发明了 LISP 语言。众所周知，λ 演算法的一个核心思想是不可变性 一一 某个符号所对应的值是永远不变的，所以从理论上来说，函数式编程语言中应该是没有赋值语句的。大部分函数式编程语言只允许在非常严格的限制条件下，可以更改某个变量的值。因此，我们在这里可以将函数式编程范式总结为下面这句话：函数式程对程序中的值进行了限制和规范。

Notice the pattern that I’ve quite deliberately set up in introducing these three programming paradigms: Each of the paradigms removes capabilities from the programmer. None of them adds new capabilities. Each imposes some kind of extra discipline that is negative in its intent. The paradigms tell us what not to do, more than they tell us what to do.

Another way to look at this issue is to recognize that each paradigm takes something away from us. The three paradigms together remove goto statements, function pointers, and assignment. Is there anything left to take away?

Probably not. Thus these three paradigms are likely to be the only three we will see — at least the only three that are negative. Further evidence that there are no more such paradigms is that they were all discovered within the ten years between 1958 and 1968. In the many decades that have followed, no new paradigms have been added.

后面 3 个编程范式章节总结内容汇总：

It is this ability to create falsifiable units of programming that makes structured programming valuable today. This is the reason that modern languages do not typically support unrestrained goto statements. Moreover, at the architectural level, this is why we still consider functional decomposition to be one of our best practices.

At every level, from the smallest function to the largest component, software is like a science and, therefore, is driven by falsifiability. Software architects strive to define modules, components, and services that are easily falsifiable (testable). To do so, they employ restrictive disciplines similar to structured programming, albeit at a much higher level.It is those restrictive disciplines that we will study in some detail in the chapters to come.

结构化编程范式中最有价值的地方就是，它予了我们创造可证伪程序单元的能力。这就是为什么现代程语言一般不支持无限制的 goto 语句。更重要的是，这也是为什么在架构设计领域，功能性降解拆分仍然是最佳实践之一。无论在哪一个层面上，从最小的函数到最大组件，软件开发的过程都和科学研究非常类似，它们都是由证伪驱动的。软件架构师需要定义可以方便地进行证伪（测试）的模块、组件以及服务。为了达到这个目的，他们需要将类似结构化编程的限制方法应用在更高的层面上。我们在接下来的章节中将会深入研究这些限制性的方法。

1『印象中，剔除消除 goto 语言的 Edsger Wybe Dijkstra，他从数学上证明了「结构性」语言的可证伪性。回复：下面有详细的讲解。（2020-12-24）』

### 0103. 主题卡 —— 科学与数学的区别以及软件开发是科学范畴

Science is fundamentally different from mathematics, in that scientific theories and laws cannot be proven correct. I cannot prove to you that Newton’s second law of motion, F = ma, or law of gravity, F = Gm1m2/r2, are correct. I can demonstrate these laws to you, and I can make measurements that show them correct to many decimal places, but I cannot prove them in the sense of a mathematical proof. No matter how many experiments I conduct or how much empirical evidence I gather, there is always the chance that some experiment will show that those laws of motion and gravity are incorrect.

That is the nature of scientific theories and laws: They are falsifiable but not provable. And yet we bet our lives on these laws every day. Every time you get into a car, you bet your life that F = ma is a reliable description of the way the world works. Every time you take a step, you bet your health and safety that F = Gm1m2/r 2 is correct.

Science does not work by proving statements true, but rather by proving statements false. Those statements that we cannot prove false, after much effort, we deem to be true enough for our purposes. Of course, not all statements are provable. The statement「This is a lie」is neither true nor false. It is one of the simplest examples of a statement that is not provable.

Ultimately, we can say that mathematics is the discipline of proving provable statements true. Science, in contrast, is the discipline of proving provable statements false.

1-2『有关科学与数学的区别，之前在很多地方看到过，比如吴军的数学通识课，但还是觉得这里作者将的相对通透，而且下面提到软件开发是科学范畴而非数学范畴，给自己醍醐灌顶的感觉。科学与数学的区别以及软件开发是科学范畴，做一张主题卡片。（2020-12-24）』——已完成

科学和数学在证明方法上有着根本性的不同，科学理论和科学定律通常是无法被证明的，譬如我们并没有办法证明牛顿第二运动定律 F=ma 或者万有引カ定律 `F=Gmm2/r2` 是正确的，但我们可以用实际案例来演示这些定律的正确性，并通过高精度测量来证明当相关精度达到小数点后多少位时，被测量对象仍然一直满足这个定律。但我们始终没有办法像用数学方法一样推导出这个定律。而且，不管我们进行多少次正确的验，也无法排除今后会存在某一次实验可以推翻牛顿第二运动定律与万有引力定律的可能性。

这就是科学理论和科学定律的特点：它们可以被证伪，但是没有办法被证明。但是我们仍然每天都在依赖这些定律生活。开车的时候，我们就等于是在用性命担保 F=ma 是对世界运转方式的一个可靠的描述。每当我们迈出一步的时候，就等于在亲身证明 F=Gmm2/r2 是正确的。

科学方法论不需要证明某条结论是正确的，只需要想办法证明它是错误的。如果某个结论经过一定的努力无法证伪，我们则认为它在当下是足够正确的。当然，不是所有的结论都可以被证明或者证伪的。举一个最简单的不可证明的例子：「这句话是假的」，非真也非伪。最终，我们可以说数学是要将可证明的结论证明，而与之相反，科学研究则是要将可证明的结论证伪。

Dijkstra once said,「Testing shows the presence, not the absence, of bugs.」In other words, a program can be proven incorrect by a test, but it cannot be proven correct. All that tests can do, after sufficient testing effort, is allow us to deem a program to be correct enough for our purposes.

The implications of this fact are stunning. Software development is not a mathematical endeavor, even though it seems to manipulate mathematical constructs. Rather, software is like a science. We show correctness by failing to prove incorrectness, despite our best efforts.

Such proofs of incorrectness can be applied only to provable programs. A program that is not provable — due to unrestrained use of goto, for example — cannot be deemed correct no matter how many tests are applied to it.

Structured programming forces us to recursively decompose a program into a set of small provable functions. We can then use tests to try to prove those small provable functions incorrect. If such tests fail to prove incorrectness, then we deem the functions to be correct enough for our purposes.

1『上面的信息太有感觉了，突然领悟到「测试」的真谛，功能拆解成一个个「小函数」，颗粒度越细越好，每个小函数做单元测试，每个小函数无法被证伪，那么组合起来的功能也是没法证伪的。（2020-12-24）』

Dijkstra 曾经说过「测试只能展示 Bug 的存在，并不能证明不存在 Bug」，换句话说，一段程序可以由一个测试来证明其错误性，但是却不能被证明是正确的。测试的作用是让我们得出某段程序已经足够实现当前目标这一结论。这一事实所带来的影响是惊人的。软件开发虽然看起来是在操作很多数学结构，其实不是一个数学研究过程。恰恰相反，软件开发更像是一门科学研究学科，我们通过无法证伪来证明软件的正确性。

1-2『测试只能展示 Bug 的存在，并不能证明不存在 Bug，做一张金句卡，其展开的细节放在这里。（2020-12-24）』

注意，这种证伪过程只能应用于可证明的程序上。某段程序如果是不可证明的，例如，其中采用了不加限制的 goto 语句，那么无论我们为它写多少测试，也不能够证明其正确性。结构化编程范式促使我们先将一段程序递归降解为一系列可证明的小函数，然后再编写相关的测试来试图证明这些函数是错误的。如果这些测试无法证伪这些函数，那么我们就可以认为这些函数是足够正确的，进而推导整个程序是正确的。

### 0201. 术语卡 —— 编程范式

Another, probably more significant, revolution was in programming paradigms. Paradigms are ways of programming, relatively unrelated to languages. A paradigm tells you which programming structures to use, and when to use them. To date, there have been three such paradigms. For reasons we shall discuss later, there are unlikely to be any others.

1-2『编程范式，ways of programming，其与使用什么编程语言没啥关系的，编程范式做一张术语卡片。』——已完成

除此之外，计算机编程领域还经历了另外一个更巨大、更重要的变革，那就是编程范式（paradigm）的变迁。编程范式指的是程序的编写模式，与具体的编程语言关系相对较小。这些范式会告诉你应该在什么时候采用什么样的代码结构。直到今天，我们也一共只有三个编程范式，而且未来几乎不可能再出现新的。

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 —— Bob 大叔

Robert C. Martin (-)。

印象：

例证：

Robert C. Martin (Uncle Bob) has been a programmer since 1970. He is the co-founder of cleancoders.com, which offers online video training for software developers, and is the founder of Uncle Bob Consulting LLC, which offers software consulting, training, and skill development services to major corporations worldwide. He served as the Master Craftsman at 8th Light, Inc., a Chicago-based software consulting firm. He has published dozens of articles in various trade journals and is a regular speaker at international conferences and trade shows. He served three years as the editor-in-chief of the C++ Report and served as the first chairman of the Agile Alliance.

Martin has authored and edited many books, including The Clean Coder, Clean Code, UML for Java Programmers, Agile Software Development, Extreme Programming in Practice, More C++ Gems, Pattern Languages of  Program Design 3, and Designing Object Oriented C++ Applications Using the Booch Method.

2『 Bob 大叔做一张人名卡片。』—— 已完成

### 0401. 金句卡 —— 测试只能展示 Bug 的存在，并不能证明不存在 Bug

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 内容简介

《架构整洁之道》是创造「Cean 神话」的 Bob 大叔在架构领域的登峰之作，围绕「架构整洁」这一重要导向，系统地剖析其缘起、内涵及应用场景，涵盖软件研发完整过程及所有核心架构模式。本书分为 6 部分，第 1 部分纲领性地提出软件架构设计的终极目标，描述软件架构设计的重点与模式；第 2-4 部分从软件开发中三个基础编程范式的定义和特征出发，进一步描述函数、组件、服务设计与实现的定律，以及它们是如何有效构建软件系统的整体架构的；第 5 部分从整洁架构的定义开始，详细阐述软件架构设计过程中涉及的方方面面，包括划分内部组件边界、应用常见设计模式、避开错误、降低成本、处理特殊情況等，并以实战案例将内容有机整合起来；第 6 部分讲述具体实现细节；附录则透过作者数十年的软件从业经历再次印证本书的观点。

对于每一位软件研发从业人员一无论从事的是具体编码实现、架构设计，还是软件研发管理，本书都是不可或缺的。

## 推荐序一

在我心里，程序员可以分为三个层次：普通程序员、工程师和架构师。

普通程序员是编写代码的人。编写代码的方式有很多，只要能让程序跑起来，能正确地处理业务流程和对数据进行计算，就可以说「会编写代码」。程序员需要熟悉整个程序的逻辑及处理过程，需要熟悉程序语言的特性，还需要熟悉一些计算机操作系统的交互调用方式，オ能写出从用户侧交互，到数据和业务逻辑处理，再到与计算机系统交互的代码，有效地把用户信息、数据、业务和计算机串联和拼装出来。

然而，其中一些程序员发现，只让代码跑起来是不够的，因为这个世界是不断变化的，他们发现自己需要花更多的时间来维护代码：增加新的需求，扩展原有的流程，修改已有的功能，优化性能......一个人完全维护不过来，还需要更多的人，于是代码还需要在不同人之间轮转；他们发现代码除了需要跑起来，还需要易读、易扩展、易维护，甚至可以直接重用。于是，这些人使用各种各样的手段和技术不断提高代码的易读性、可扩展性、可维护性和重用性。我们把这些有「洁癖」、有工匠精精、有修养的程序员叫作工程师，工程师不仅仅是在编写代码，他们会用工程的方法来编写代码，以便让编程开发更为高效和快速。他们把編程当成一种设计，一种工业设计，把代码模块化，让这些模块可以更容易地交互拼装和组织，让代码排列整齐一阅读和维护这些代码就像看阅兵式一样舒心畅快。

但是故事还没完，这些拥有工匠精神的工程师们还是难以解决某些题，这些人渐地发现，这个世界上有很多问题就像翘翘板一样，只能要一边，这一边上去了，另一边就下来了。就像要么用空间换时间，要么用时间换空间一样，你很难找到同时满足空间和时间要求的「双利解」；就像 CAP 的三选二的理论一样，这个世界不存在完美的解決方案，无论什么方案都有好的一面和不好的一面。而且，这些工程师还渐发现，每当引入一个新的技术来解決一个已有的问题时，这个新的技术就会带来更多的问题，问题就像有一个生命体一样，它们会不断地繁殖和进化。渐渐地，他们发现，问题的多少和系统的复杂度呈正比，而且不仅是线性正比，还可能呈级数正比，此时就越来越难做技术決定。但是有一些资深的工程师开始站出来挑战这些问题，有的基于业务分析给出平衡的方案，有的开始尝试设计更高级的技术，有的开始设计更灵活的系统，有的则开始简化和轻量化整个系统，这些高智商、经验足、不怕难的工程师们引领着整个行业前行。他们就是架构师！

感觉 Bob 大叔的系列著作好像也在走这个过程，《代码整洁之道》教你写出易读、可扩展、可维护、可重用的代码，《代码整洁之道：程序员的职业素养》教你怎样変成一个有修养的程序员，而《架构整洁之道》基本上是在描述软件设计的一些理论知识。《架构整洁之道》大体分成三个部分：编程范式（结构化编程、面向对象编程和函数式编程），设计原则（主要是 SOLD），以及软件架构（其中讲了很多高屋建翎的内容）。总体来说，这本书中的内容可以让你从微观（代码层面）和宏观（架构层面）两个层面对整个软件设计有一个全面的了解。

但是，如果你想从这本书里找到一些可以立马解决具体问题的工程架构和技术，恐怕你会感到失望。这本书中更多的是一些基础的理论知识，看完后你可能会比较「无感」，因为这些基础知识对于生活在这个高速发展的喜欢快餐文化的社会中的人来说，可能很难理解其中的价值一一大多数人的目标不是设计出一个优质的软件或架构，而是快速地解決一个具体的问题，完成自己的工作。然而，可能只有你碰过足够多的壁，掉过足够多的坑，经历过足够多的痛苦后，再来读这本书时，你オ会发现本书中的这些「陈旧的知识」是多么充满智慧。而且，如果有一天，你像我这个老家伙一样，看到今天很多很多公司和年轻的程序员还在不断地掉坑和挣扎，你就会明白这些知识的重要性了。

我个人觉得，这本书是架构方面的入门级读物，但也并不适合经验不足的人员学习，这本书更适合的读者群是，有 3-5 年编程经验、需要入门软件设计和架构的工程师或程序员。最后，我想留下一个观点和一组问题。

观点：无论是微观世界的代码，还是宏观层面的架构，无论是三种程范式还是微服务架构，它们都在解决一个问题 一一 分离控制和逻辑。所谓控制就是对程序流转的与业务逻辑无关的代码或系统的控制（如多线程、异步、服务发现、部署、弹性伸等），所调逻辑则是实实在在的业务逻辑，是解决用户问题逻辑。控制和逻辑构成了整体的件复杂度，有效地分离控制和逻辑会让你的系统得到最大的简化。

问题：如果你要成为一名架构师，你需要明确地区分几组词语（如何区分它们正是留给你的问题），否则你不可能成为一名合格的工程师或架构师。这几组词语是简单 VS 简陋、平衡 VS 妥协、迭代 VS 半成品。如果你不能很清楚地定义出其中的区別，那么你将很难做出正确的决定，也就不可能成为优秀的工程师或架构师。

我相信这个观点和这组问题将有助于你更好地读并理解这本书，也会让你进行更多的思考，带着思考读这本书，会让你学到更多。

—— 陈皓，左耳朵耗子

## 推荐序二  —  —  久远的教诲，古老的智慧

如果让你接手一套不稳定但要紧的在线系统，这套系统还有各种问题：变量命名非常随意，依赖逻辑错综复杂，层次结构乱七八糟，部署流程一糊涂，监控系統一片空白。你该怎么办？

前几年我就遇到了这种问题，我对着频发的故障仔细观察，发现了最关键的问题：如果放着不动，这套系统的核心功能还是相对稳定的，但经常会有一些外围需求要开发，这时由于原有的依赖逻辑和层次结构不够清楚，就会导致「牵一发而动全身」的情況，加上測试不完善，所以几乎每次外围功能上线更新，核心功能都会受影响，然后又要重复好几次「调试 → 改正 → 上线」的流程。

怎么办？大家说了很多办法：把单元测试都补全，重构代码拆分核心功能和非核心功能，跟业务方谈暂停需求。这些办法都很对，但是，都需要时间才能见效，而我们最缺的就是时间。

我提了一个很「笨」的办法：把所有「共享变量」都抽到 Redist 中进行读写，消灭本地副本，然后把稳定版本程序多部署几份，这样就可以多启动几个实例，将这些实例标记为 AB 两组。同时，在前面搭建代理服务，用于分流请求 一一 核心功能请求分配到 A 组（程序基本不更新），外围功能请求分配到 B 组（程序按业务需求更新）。这样做看起来有点多此一举  —  —  AB 两组都只有部分代码提供服务，而且要通过 Redis 共享状态，但是却实现了无论 B 组的程序如何更新，都不会影响 A 组所承载的核心服务的目的。

虽然当时不少人说「怎么能这样玩呢」，但它确实有效。当天部署，当天生效，在线服务迅速稳定下来，即便新开发的外围功能有问题，核心服务也不受任何影响。这样业务人员满意了，开发人员也可以安心对系统倣改造了。

后来有不少人问我是怎么想到这个办法的，答案是：因为我是个老程序员，成长在面向对象的年代，运用 SOC（关注点分离）、SRP（单一职责原则）、OCP（开闭原则）这些东西对我来说就如同本能。具体到这个例子，无非就是识别关注点、隔离责任、保持核心关注点的封闭而已。

后来我才知道，我提出的这个方法有个专门的名字叫「蓝绿部署」。当然我自认是个老程序员，不懂这些新鲜概念也不太要紧。确实，如今不少程序员已经不认识 SOC、SRP、OCP、LSP 等「古老」的玩意了，大家熟悉的是各种语言、类库、框架、代码托管网站。互联网开发场景变万化，技术一日千里，而面向对象在不少人的脑海里早就是弃之不用的老古革了。只有「老一辈」的程序员还记得那些古老的教诲，守着那些古拙的技巧。但是这些东西，总有一天会被时代淘吗？

实际上，这也是我初读《架构整洁之道》的疑惑。虽然 Bob 大叔这个名字对我们这些「老程序员」来说可谓如雷贯耳，之前针对一般性软件开发所著的《代码整洁之道》和《代码整洁之道：程序员的职业素养》也确实很受欢迎，但如今写架构，还从结构化编程、面向对象编程、函数式编程写起，还花时间解释 SRP、OCP、LSP 等原则，实在难掩「古老」的感觉。请问，它们和如今的「架构」有什么关系吗？

不过，如果你耐心读下去就会发现，还真有关系。按照 Bob 大叔的说法，所谓架构就是「用最小的人力成本来满足构建和维护系统需求」的设计行为。以前的面向对象系统和如今的分布式系统，在这一点上是完全一致的。听取久远的教诲，尊重古老的智慧，如今的架构师也会从中受益。不信？我们就拿经典的三个编程范式来举例，看看这些「老掉牙」的玩意儿和如今的架构设计有什么关联。

大家对结构化编程的一般理解是，由 if-else、switch-case 之类的语句组织程序代码的编程方式，它杜绝了 goto 导致的混乱。但是从更深的层次上看，它也是一种设计范式，避免随意使用 goto，使用 if-else、switch-case 之类控制语句和函数、子函数组织起来的程序代码，可以保证程序的结构是清楚的，自顶向下层层细化，消灭了杂错，杜绝了混淆。

联系如今的分布式系统，我们在设计的时候，真的能够做到自顶向下层层细化吗？有多少次，我看到的系統设计图里，根本没有「层次」的概念，各个模块没有一致的层次划分，与子系統交互的不是子系统，而是一盘散沙式的接口，甚至接口之间随意互调、关系乱成一团麻的情况也时常出现，带来的就是维护和调试的噩梦。吹散历史的迷雾，不正是古老的 goto 陷阱的再现吗？

大家对面向对象编程的一般理解是，由封装、继承、多态三种特性支持的，包含类、接口等若干概念的编程方式。但是从更深的层次上看，它也是一种设计范式。多态大概算其中最神奇的特性了，程序员在确定接口时做好抽象，代码就可以很灵活，遇到新情況时，新写一个实现就可以无缝对接联系如今的分布式系统，我们在设计的时候，真的能够做到接口足够抽象、新模块能无缝对接吗？有多少次，我看到接口的设计非常随意，接口不是基于行为而是基于特定场景的实现，没有做适当的抽象，也没有为未来预留空间，直接导致契约僵硬死板。每新増一种终端呈现形式，整个内容生产流程就要大动干，这样的例子并不罕见。抹去历史的尘埃，这不正是「多态」出现之前的困境吗？

大家对函数式编程的一般理解是，以函数为基本单元，没有变量（更准确地说是不能重复值）也没有副作用的编程方式。但是从更深的层次上看，它彻底隔离了可变性，变量或者状态默认就是不可变的，如果要变化，则必须经过合理设计的专门机制来实现。所以，它也避免了死锁、状态冲突等众多麻烦。

联系如今的分布式系统，我们在设计的时候，真的能够彻底隔离可变性、避免状态冲突吗？有多少次，我看到状态或变量的修改接口大方暴露，被不经意（或者恶意）修改，导致奇怪的故障。Bob 大叔举了ー个相当有趣的例子，如果又要保证操作原子性又要能精确还原各时刻的状态，有个办法是这样的：只提供 CR 操作，而不提供完整的 CRUD 操作（就像 MYSQL 的 binlog 那样）。平时只要追加操作记录即可，各时刻的状态永远通过重放之前的操作记录得出，这样就彻底避免了状态的错乱。这个办法看起来古怪，但我真的在之前的开发中用过（当然是在程序生命周期有限的场景下），而且真的从没出过错。

坦白说，看完《架构整洁之道》这本书，我心里好受点了。因为我发现，我们这些老程序员的知识其实没有过时，如今不少光鮮的架构其实要解決的还是那些古老的问题。多亏了 Bob 大叔的妙手点拨，我才能穿越时空，享受到「重新发现智慧」的愉悦。

当然，架构设计是一门复杂的学问，要综合考虑编码、质量、部署、发布、运维、排障、升级等等各种因素，做出权衡。好消息是，Bob 大叔的这本书覆盖面广，涉及各个方面，相信你认真读完全书定会和我一样有不小的收获。唯一的问题是，你要适应这个老程序员的口吻和节奏：他当然也会拿如今流行的打车系统做例子，但他更熟悉的还是链接器、C 语言、UML 图等玩意。

不过我觉得，这都不是大问题。看得出类之间的依赖关系不合理，自然容易发现子系统之间的依赖关系不合理；搞得懂 UNIX 如何巧妙定义通用的 IO 设备，自然容易想到对 PC Web、Mobile Web、App 内的页面做适当抽象；认得清各线程、进程、链接库的职责，自然容易明白微服务也需要避免跨边界调用。更妙的是，从这种古老的视角看问题，往往更能摆脱细节的困抗，把握问题的核心。就像老子说的那样：治大国如烹小鲜。

噢，对了，「治大国如烹小鲜」也是久远的教诲，也包含着古老的智慧。

—— 余晟公众号「余晟以为」，作者现在沪江教育集团担任平台架构部负责人

## Foreword

What do we talk about when we talk about architecture?

As with any metaphor, describing software through the lens of architecture can hide as much as it can reveal. It can both promise more than it can deliver and deliver more than it promises.

The obvious appeal of architecture is structure, and structure is something that dominates the paradigms and discussions of software development — components, classes, functions, modules, layers, and services, micro or macro. But the gross structure of so many software systems often defies either belief or understanding — Enterprise Soviet schemes destined for legacy, improbable Jenga towers reaching toward the cloud, archaeological layers buried in a big-ball-of-mud slide. It’s not obvious that software structure obeys our intuition the way building structure does.

Buildings have an obvious physical structure, whether rooted in stone or concrete, whether arching high or sprawling wide, whether large or small, whether magnificent or mundane. Their structures have little choice but to respect the physics of gravity and their materials. On the other hand — except in its sense of seriousness — software has little time for gravity. And what is software made of? Unlike buildings, which may be made of bricks, concrete, wood, steel, and glass, software is made of software. Large software constructs are made from smaller software components, which are in turn made of smaller software components still, and so on. It’s coding turtles all the way down.

When we talk about software architecture, software is recursive and fractal in nature, etched and sketched in code. Everything is details. Interlocking levels of detail also contribute to a building’s architecture, but it doesn’t make sense to talk about physical scale in software. Software has structure — many structures and many kinds of structures — but its variety eclipses the range of physical structure found in buildings. You can even argue quite convincingly that there is more design activity and focus in software than in building architecture — in this sense, it’s not unreasonable to consider software architecture more architectural than building architecture!

But physical scale is something humans understand and look for in the world. Although appealing and visually obvious, the boxes on a PowerPoint diagram are not a software system’s architecture. There’s no doubt they represent a particular view of an architecture, but to mistake boxes for the big picture — for the architecture — is to miss the big picture and the architecture: Software architecture doesn’t look like anything. A particular visualization is a choice, not a given. It is a choice founded on a further set of choices: what to include; what to exclude; what to emphasize by shape or color; what to de-emphasize through uniformity or omission. There is nothing natural or intrinsic about one view over another.

Although it might not make sense to talk about physics and physical scale in software architecture, we do appreciate and care about certain physical constraints. Processor speed and network bandwidth can deliver a harsh verdict on a system’s performance. Memory and storage can limit the ambitions of any code base. Software may be such stuff as dreams are made on, but it runs in the physical world.

This is the monstrosity in love, lady, that the will is infinite, and the execution confined; that the desire is boundless, and the act a slave to limit.  —  —  William Shakespeare

The physical world is where we and our companies and our economies live. This gives us another calibration we can understand software architecture by, other less physical forces and quantities through which we can talk and reason.

Architecture represents the significant design decisions that shape a system, where significant is measured by cost of  change.  —  —  Grady Booch

Time, money, and effort give us a sense of scale to sort between the large and the small, to distinguish the architectural stuff from the rest. This measure also tells us how we can determine whether an architecture is good or not: Not only does a good architecture meet the needs of its users, developers, and owners at a given point in time, but it also meets them over time.

If  you think good architecture is expensive, try bad architecture.  —  —  Brian Foote and Joseph Yoder

The kinds of changes a system’s development typically experiences should not be the changes that are costly, that are hard to make, that take managed projects of their own rather than being folded into the daily and weekly flow of work.

That point leads us to a not-so-small physics-related problem: time travel. How do we know what those typical changes will be so that we can shape those significant decisions around them? How do we reduce future development effort and cost without crystal balls and time machines?

Architecture is the decisions that you wish you could get right early in a project, but that you are not necessarily more likely to get them right than any other.  —  —  Ralph Johnson

Understanding the past is hard enough as it is; our grasp of the present is slippery at best; predicting the future is nontrivial.

This is where the road forks many ways.

Down the darkest path comes the idea that strong and stable architecture comes from authority and rigidity. If change is expensive, change is eliminated — its causes subdued or headed off into a bureaucratic ditch. The architect’s mandate is total and totalitarian, with the architecture becoming a dystopia for its developers and a constant source of frustration for all.

Down another path comes a strong smell of speculative generality. A route filled with hard-coded guesswork, countless parameters, tombs of dead code, and more accidental complexity than you can shake a maintenance budget at.

The path we are most interested is the cleanest one. It recognizes the softness of software and aims to preserve it as a first-class property of the system. It recognizes that we operate with incomplete knowledge, but it also understands that, as humans, operating with incomplete knowledge is something we do, something we’re good at. It plays more to our strengths than to our weaknesses. We create things and we discover things. We ask questions and we run experiments. A good architecture comes from understanding it more as a journey than as a destination, more as an ongoing process of enquiry than as a frozen artifact.

Architecture is a hypothesis, that needs to be proven by implementation and measurement.  —  —  Tom Gilb

To walk this path requires care and attention, thought and observation, practice and principle. This might at first sound slow, but it’s all in the way that you walk.

The only way to go fast, is to go well.

Enjoy the journey.

 — Robert C. Martin,  Kevlin Henney May 2017

软件架构（architecture）究竟是什么？不论从哪个角度分析软件系统，都不可能面面俱到。如果从架构学角度来分析，在一定程度上能够做到抓大放小，把握住重点，但是也不可避免地会错失某些重要的细节信息。

软件架构学关注的的一个重点是组织结构（structure）。不管是讨论组件（Component）、类（Class）、函数（Function）、模块（Module），还是层级（Layer）、服务（Service）以及微观与宏观的软件开发过程，软件的组织结构都是我们的主要关注点。但是真实世界中的许多软件项目并不完全按照我们的信念和愿望生长 一一 它们就像超大型国企那样，层层嵌套，缠绕成一团乱麻。有的时候真的很难相信，软件项目的组织结构性也能像物理建筑那样一目了然，层次清晰。

物理建筑，不管其地基是石头还是水泥，形状是高大还是宽阔，风格是气势恢宏还是小巧玲珑，其组织结构都一目了然。物理建筑的组织结构必须遵守「受重力」这一自然规律，同时还要符合建筑材料自身的物理特性。软件项目则没有定律可以遵循。另外，物理建筑是用砖头、水泥、木头、钢铁或者玻璃等准材料建成的，而大型软件项目往往是由小的软件组件构成的，这些软件组件又是由更小的软件组件构成的，层层堆疊，无穷无尽。

所以，当讨论软件架构时，要特别注意软件项目是具有递归（recursive）和分形（fractal）特点的，最终都要由一行行的代码组成。脱离了一行行的代码，脱离了具体的细节设计，架构设计就无从谈起。大型物理建筑通常可以用比例模型分层描述细节信息，但是软件项目内部结构是很难用模型分层描述的。软件项目也具有内部结构，但是其结构无论从数量上还是多样性上来说，都远远超过了物理建筑的结构。可以不夸张地说，软件开发比修建物理建筑需要更长、更专注的设计过程，软件架构师应该比建筑架构师更懂架构。

比例模型是深入人心的展示方式，但是不管某个 Powerpoint 图表中的彩色方块多么好看，多么简单易，它也无法完全代表一个软件的架构。它只能是该软件的架构的一个视图，而非全部。软件的架构并没有固定的展现形式，你所看到的每一个视图的背后都是架构师所做的层层抉择。一个视图包含了哪些部分，排除了哪些部分；用特殊形状和色强调了哪些部分，又有哪些部分被泛泛地一笔帯过，甚至直接忽略，这些都是这个视图本身的特性。然而，每个视图都是对的，它们往往并没有优劣之分。

虽然软件无法很好地用比例模型展示，但它还是要在现实世界中运行的。在设计软件架构的过程中，我们必须理解和遵守现实的约束条件。CPU 速度和网络帯宽往往在很大程度上決定了系统的性能，而内存和存储空间的大小也会大幅影响代码的设计野心。

女士，这就是爱情的穷凶极恶之处，人的意愿是无穷的，而实际行动却处处受限。人的欲望是无止境的，行为却不得不从现实的限制。 —— 威廉·莎士比亚

人类的整个经济活动都是存在于现实世界中的，所以我们可以利用现实世界的一些准则来衡量和推理软件开发过程中那些不好量化和物化的因素。

软件架构是系统设计过程中的重要设计决定的集合，可以通过交更成本来衡量毎个设计决定的重要程度。 —— Grady Booch

需要付出的时间、金钱和人力成本是区分软件架构规模大小的衡量标准，也可以用来区分架构设计和细节设计。同时，我们还可以依据这个信息来判断某个特定架构设计是好还是坏好的架构，不仅要在某一特定时刻满足软件用户、开发者和所有者的需求，更要在一段时间内持续满足他们的后续需求。

如果你觉得好架构的成本太高，那你可以试试选择差的架构加上返工重来的成本。——  Brian Foote and Joseph Yoder

一个系统的常规变更不应该是成本高的，也不应该需要难以決策的大型设计调整，更不应该需要单独立项来推进。这些常规変更应该可以融入每日或者每周的日常系统维护中去完成。我们怎么能够预知某个系未来的变更需求，以便提前做准备呢？我们怎么能在没有水晶球与时光穿梭机的情况下，未卜先知，降低未来的变更成本呢？

所软件架构，就是你希望在项目一开始就能对，但是却不一定能够做得对的决策的集合。 ——  Ralph Johnson

了解历史已经够难了，我们对现实的认知也不够可靠，预言未来就更难了。这就是不同的软件开发理论的主要分歧点。

其中一条比较悲观阴暗的路线认为，只有权威和刚性能带来强壮与稳定。如果某项变更成本高昂，那么就应该忽视它 一一 变更背后的需求要么应该被抑制，要么就应该被丢到官僚主义的大机器中去绞碎。架构师的決定永远是完整的、彻底的，软件架构就是全体开发人员的敌托邦噩梦（Dystopia），永远是所有人沮丧的源泉。

另外一条路线则到处充斥着大量的投机性的通用设计。在这样的软件项目中到处都是硬编码的猜測性代码，到处是无穷无尽的参数，存在着成篇累牍的无效代码。维护这样的项目，肯定会遇到意外情况，而且无论预留多少资源都不够应付。

而本书试图探索的则是一条整洁路线。这条路线拥抱軟件的灵活多变性，将其作为系統的一级设计目标。同时，我们也承认人类并不能全知全晓，但在信息不全的情况下人类仍然能够做出优良的決策。这条路线可以让我们多发挥优势，避开弱势。通过实际创造和探索，不停地提出问题和进行实验优良的软件架构不是一成不变的，只有经过不断打磨和改进才能最终成就。

软件架构是一猜想，只有通过实际实现和测量才能证实。—— Tom Gilb

遵循这条路线，我们需要用心，全神贯注，不停观察和思考，在原则指导下不断实践。虽然这可能听起来很麻烦、很慢，但是只要坚持走下去一定能够成功。走快的唯一方法是先走好。一起享受这个过程吧。

## Preface

The title of this book is Clean Architecture. That’s an audacious name. Some would even call it arrogant. So why did I choose that title, and why did I write this book?

I wrote my very first line of code in 1964, at the age of 12. The year is now 2016, so I have been writing code for more than half a century. In that time, I have learned a few things about how to structure software systems — things that I believe others would likely find valuable.

I learned these things by building many systems, both large and small. I have built small embedded systems and large batch processing systems. I have built real-time systems and web systems. I have built console apps, GUI apps, process control apps, games, accounting systems, telecommunications systems, design tools, drawing apps, and many, many others.

I have built single-threaded apps, multithreaded apps, apps with few heavy-weight processes, apps with many light-weight processes, multiprocessor apps, database apps, mathematical apps, computational geometry apps, and many, many others.

I’ve built a lot of apps. I’ve built a lot of systems. And from them all, and by taking them all into consideration, I’ve learned something startling.

The architecture rules are the same!

1『软件架构的底层逻辑是相同的，做一张主题卡片。』—— 已完成

This is startling because the systems that I have built have all been so radically different. Why should such different systems all share similar rules of architecture? My conclusion is that the rules of  software architecture are independent of  every other variable.

This is even more startling when you consider the change that has taken place in hardware over the same half-century. I started programming on machines the size of kitchen refrigerators that had half-megahertz cycle times, 4K of core memory, 32K of disk memory, and a 10 character per second teletype interface. I am writing this preface on a bus while touring in South Africa. I am using a MacBook with four i7 cores running at 2.8 gigahertz each. It has 16 gigabytes of RAM, a terabyte of SSD, and a 2880*1800 retina display capable of showing extremely high-definition video. The difference in computational power is staggering. Any reasonable analysis will show that this MacBook is at least 10^22 more powerful than those early computers that I started using half a century ago.

Twenty-two orders of magnitude is a very large number. It is the number of angstroms from Earth to Alpha-Centuri. It is the number of electrons in the change in your pocket or purse. And yet that number — that number at least — is the computational power increase that I have experienced in my own lifetime.

And with all that vast change in computational power, what has been the effect on the software I write? It’s gotten bigger certainly. I used to think 2000 lines was a big program. After all, it was a full box of cards that weighed 10 pounds. Now, however, a program isn’t really big until it exceeds 100,000 lines.

The software has also gotten much more performant. We can do things today that we could scarcely dream about in the 1960s. The Forbin Project, The Moon Is a Harsh Mistress, and 2001: A Space Odyssey all tried to imagine our current future, but missed the mark rather significantly. They all imagined huge machines that gained sentience. What we have instead are impossibly small machines that are still … just machines.

And there is one thing more about the software we have now, compared to the software from back then: It’s made of  the same stuff. It’s made of if statements, assignment statements, and while loops.

Oh, you might object and say that we’ve got much better languages and superior paradigms. After all, we program in Java, or C#, or Ruby, and we use object-oriented design. True — and yet the code is still just an assemblage of sequence, selection, and iteration, just as it was back in the 1960s and 1950s.

When you really look closely at the practice of programming computers, you realize that very little has changed in 50 years. The languages have gotten a little better. The tools have gotten fantastically better. But the basic building blocks of a computer program have not changed.

If I took a computer programmer from 1966 forward in time to 2016 and put her [1] in front of my MacBook running IntelliJ and showed her Java, she might need 24 hours to recover from the shock. But then she would be able to write the code. Java just isn’t that different from C, or even from Fortran.

And if I transported you back to 1966 and showed you how to write and edit PDP-8 code by punching paper tape on a 10 character per second teletype, you might need 24 hours to recover from the disappointment. But then you would be able to write the code. The code just hasn’t changed that much.

That’s the secret: This changelessness of the code is the reason that the rules of software architecture are so consistent across system types. The rules of software architecture are the rules of ordering and assembling the building blocks of programs. And since those building blocks are universal and haven’t changed, the rules for ordering them are likewise universal and changeless.

Younger programmers might think this is nonsense. They might insist that everything is new and different nowadays, that the rules of the past are past and gone. If that is what they think, they are sadly mistaken. The rules have not changed. Despite all the new languages, and all the new frameworks, and all the paradigms, the rules are the same now as they were when Alan Turing wrote the first machine code in 1946.

But one thing has changed: Back then, we didn’t know what the rules were. Consequently, we broke them, over and over again. Now, with half a century of experience behind us, we have a grasp of those rules.

And it is those rules — those timeless, changeless, rules — that this book is all about.

Register your copy of Clean Architecture on the InformIT site for convenient access to updates and/or corrections as they become available. To start the registration process, go to informit.com/register and log in or create an account. Enter the product ISBN (9780134494166) and click Submit. Look on the Registered Products tab for an Access Bonus Content link next to this product, and follow that link to access the bonus materials.

[1]  And she very likely would be female since, back then, women made up a large fraction of programmers.

本书的名字叫作《架构整洁之道》，使用这个名字可谓是十分胆大，甚至可以说有点目中无人了。那么，为什么我会选择写这本书，并且使用这个名字呢？自 1964 年，12 岁的我写下了人生的第一行代码算起，到 2016 年，我已经编程超过 50 年。在这段时间里，我自认为学到了构建软件系統的一些方法 一一 并且我相信这些方法和经验对其他人应该有些价值。

我学习的途径是实际构建一些大大小小的软件系统。我写过小型的嵌入式系统，也构造过大型的处理系统；我构建过实时控制系统，也构建过 Web 网页系统；我写过命令行程序、图形界面程序、进程管理程序、游戏、计费系统、通信系统、设计工具、画图工具等。我写过单线程程序，也写过多线程程序；我写过由几个重型进程组成的应用，也写过由大量轻型进程组成的应用；我写过跨多个处理器的应用，还有数据库类、数值计算类和几何计算类应用，以及很多很多其他类型的应用回首过去，经历了这么多应用和系统的构建过程，我最意外的领悟是：软件架的规则是相同的！

我所构建的这些系統是干差万别的，为什么所有这些差异巨大的系統都遵守同样的软件架构规则呢？这里我得出的结论是，软件架构规则和其他变量完全无关。

回顾过去这半个世纪以来硬件系统产生的巨大革，这个结论就更惊人了。我的程生涯起步于像家用冰箱那么大的巨型机时代，它的 CPU 频率只有 0.5MHz，拥有 4KB 核心内存，32KB 磁盘存储，以及每秒只能传输 10 个字符的电传打字机接口。而现在，我正在一辆游览南非的观光车上敲这篇前言。

我正在用一个拥有 4 核 7 的 Macbook，每核 2.8GHz。这台笔记本电脑有 16GB 内存，1 TB SSD 硬盘，可以用 2880x1800 虹膜显示屏展现高清视频。二者计算能力上的差距真的是天壤之别。粗略分析可知，这台 Macbook 至少比我半个世纪以前用的计算机强大 1022 倍。

22 个数量级的差距是非常非常巨大的，从地球到半人马星系也只有 102 埃（angstrom，长度单位，主要用来描述原子尺寸与波长），你口袋里的零钱加起来所包含的电子数量也差不多为 102 个。而这个数字（注意还是至少）是我在一生中，所亲身经历的计算能力的提升计算能力发生了这么巨大的变化，但对我所写软件的影响有多大呢？软件尺す当然变大了。我过去认为 2000 行的程序就很庞大了。毕竟这样的程序変成打孔卡片能装满一盒子，重量超过 10 磅。而现在，一个 10 万行的程序都不能算大程序了。

同时，软件性能当然也有大幅提升。我们现在可以轻轻松松地完成那些 1960 年只能幻想的事情。电影 The Forbin Project、The Moon is a Harsh Mistressl 以及 2001: A Space Odyssey 都试图预言我们的现状，但是都没有成功。在这些电影中普遍展现的是获得了智能的巨型机器，而我们目前所拥有的计算机，虽然体积之小是当初难以想象的，却还仅仅只是机器。

同时，还有一点很重要，今天的软件与过去的软件本质上仍然是一样的。都是由 if 语句、赋值语句以及 while 循环组成的。

哦，你可能会抗议说我们现在有更好的编程语以及更先进的编程范式了。毕竟，我们现在都是用 Java、C#、Ruby 语言编写程序，并且大量采用面向对象编程方式。这没错，但是最终产生的代码仍然只是顺序结构、分支结构、循环结构的组合，这方面和 20 世纪 60 年代甚至 50 年代的程序是一模一样。

如果深入研究计算机程的本质，我们就会发现这 50 年来，计算机编程基本没有什么大的変化。编程语言稍微进步了ー点，工具的质量大大提升了，但是计算机程序的基本构造没有什么変化。

如果一个 1966 年的计算机程序员时空穿梭来到 2016 年，在我的 Macbook 上用 Intellij 写 Java 程序，她可能也就需要 24 小时来适应一下，然后很快就能照常工作了。Java 其实和 C 区别并不大，和 FORTRAN 也没那么大区别。同样，如果我把你 一一 读者传送回 1966 年，告诉你如何在一个每秒处理 10 个字符的终端上通过打孔纸带来编辑 PDP-8 代码，估计你最多也只需要 24 小时的适应时间。毕竟编程还是编程，代码并没有本质的变化。

这就是秘密所在：计算机代码没有变化，软件架构的规则也就一直保持了一致。软件架构的规则其实就是排列组合代码块的规则。由于这些代码块本质上没有变化，因此排列组合它们的规则也就不会变化。

年轻的一代程序员可能认为这些都是胡说。他们可能坚持认为现在所有东西都是崭新的、从来没有过的，过去的规则已经过时，不再适用了。这是一个非常大的错误。这些规则一直都没有変。虽然我们有了新的编程语言、新的编程框架、新的编程范式，但是软件架构的规则仍然和 1946 年阿兰·图灵写下第一行机器代码的时候一样。

当然，不样的是，那时候我们还不知道规则是什么。所以我们一次一次地颠覆了它，并且为此一次一次地付出了代价。半个世纪过去了，我们终于可以说，现在我们对这些规则有一定程度的了解了。

写这本书就是为了讲述这些规则，这些永恒的、不变的软件架构规则。

## About  the  Author

Robert C. Martin (Uncle Bob) has been a programmer since 1970. He is the co-founder of cleancoders.com, which offers online video training for software developers, and is the founder of Uncle Bob Consulting LLC, which offers software consulting, training, and skill development services to major corporations worldwide. He served as the Master Craftsman at 8th Light, Inc., a Chicago-based software consulting firm. He has published dozens of articles in various trade journals and is a regular speaker at international conferences and trade shows. He served three years as the editor-in-chief of the C++ Report and served as the first chairman of the Agile Alliance.

Martin has authored and edited many books, including The Clean Coder, Clean Code, UML for Java Programmers, Agile Software Development, Extreme Programming in Practice, More C++ Gems, Pattern Languages of  Program Design 3, and Designing Object Oriented C++ Applications Using the Booch Method.

2『 Bob 大叔做一张人名卡片。』—— 已完成

## Introduction

It doesn’t take a huge amount of knowledge and skill to get a program working. Kids in high school do it all the time. Young men and women in college start billion-dollar businesses based on scrabbling together a few lines of PHP or Ruby. Hoards of junior programmers in cube farms around the world slog through massive requirements documents held in huge issue tracking systems to get their systems to「work」by the sheer brute force of will. The code they produce may not be pretty; but it works. It works because getting something to work — once — just isn’t that hard.

Getting it right is another matter entirely. Getting software right is hard. It takes knowledge and skills that most young programmers haven’t yet acquired. It requires thought and insight that most programmers don’t take the time to develop. It requires a level of discipline and dedication that most programmers never dreamed they’d need. Mostly, it takes a passion for the craft and the desire to be a professional.

And when you get software right, something magical happens: You don’t need hordes of programmers to keep it working. You don’t need massive requirements documents and huge issue tracking systems. You don’t need global cube farms and 24/7 programming.

When software is done right, it requires a fraction of the human resources to create and maintain. Changes are simple and rapid. Defects are few and far between. Effort is minimized, and functionality and flexibility are maximized.

Yes, this vision sounds a bit utopian. But I’ve been there; I’ve seen it happen. I’ve worked in projects where the design and architecture of the system made it easy to write and easy to maintain. I’ve experienced projects that required a fraction of the anticipated human resources. I’ve worked on systems that had extremely low defect rates. I’ve seen the extraordinary effect that good software architecture can have on a system, a project, and a team. I’ve been to the promised land.

But don’t take my word for it. Look at your own experience. Have you experienced the opposite? Have you worked on systems that are so interconnected and intricately coupled that every change, regardless of how trivial, takes weeks and involves huge risks? Have you experienced the impedance of bad code and rotten design? Has the design of the systems you’ve worked on had a huge negative effect on the morale of the team, the trust of the customers, and the patience of the managers? Have you seen teams, departments, and even companies that have been brought down by the rotten structure of their software? Have you been to programming hell?

I have — and to some extent, most of the rest of us have, too. It is far more common to fight your way through terrible software designs than it is to enjoy the pleasure of working with a good one.

编写并调试一段代码直到成功运行并不需要特别高深的知识和技能，现在的一名普通高中生都可以做到。有的大学生甚至通过拼一些 PHP 或 Ruby 代码就可以创办一个市值 10 亿美元的公司。想象一下，世界上有成群的初级程序员挤在大公司的隔板间里，日复一日地用力将记录在大型问题跟踪系统里的巨型需求文档一点点转化为能实际运行的代码。他们写出的代码可能不够优美，但是确实能够正常工作。因为创造一个能正常运行的系統 一一 哪怕只成功运行一次一还真不是一件特别困难的事。

但是将软件架构设计做好就完全另当别论了。软件架构设计是一件非常困难的事情，这通常需要大多数程序员所不具备的经验和技能。同时，也不是所有人都愿意花时间来学习和钻研这个方向。做一个好的软件架构师所需要的自律和专注程度可能会让大部分程序员始料未及，更别提软件架构师这个职业本身的社会认同感与人们投身其中的热情了。

但是，一旦将软件架构好了，你就会立即体会到其中的奥妙：维持系统正常运转再也不需要成群的程序员了；每个变更的实施也不再需要巨大的需求文档和复杂的任务追踪系了；程序员们再也不用缩在全球各地的隔板间里，24x7（即每天 24 小时，每星期 7 天）地疯狂加班了。

采用好的软件架构可以大大节省软件项目构建与维护的人力成本。让每次变更都短小简单，易于实施，并且避免缺陷，用最小的成本，最大程度地满足功能性和灵活性的要求。

是的，这可能有点像童话故事一样不可信，但是这些又确实是我的亲身经历。我曾经见过因为采用了好的软件架构设计，使得整个系统构建更简单、维护更容易的情况。我也见过因为采用了好的软件架构设计，整个项目最终比预计所使用的人力资源更少，而且更快地完成了。我真真切切地体会过，好的软件架构设计为整个系统所带来的天地的变化，绝不忽悠。

请读者回头想想自己的亲身经历，你肯定经历过这样的情境：某个系统因为其组件错综复杂，相互耦合紧密，而导致不管多么小的改动都需要数周的恶战オ能完成。又或是某个系统中到处充满了腐朽的设计和连篇累牍的恶心代码，处处都是障碍。再或者，你有没有见过哪个系统的设计如此之差，整个团队的气低落，用户天天痛苦，项目经理们手足无措？你有没有见过某个软件系統因其架构腐朽不堪，而导致团队流失，部门解散，甚至公司倒闭？作为一名程序员，你在编程时体会过那种生不如死的感觉吗？

以上这些我也都切身体会过。我相信绝大部分读者也或多或少会有共吗。好的软件架构太难得了，我们职业生涯的大部分时间可能都在和差的架构做斗争，而没有机会一睹优美的架构究竟是什么样子。

## 0101. What Is Design and Architecture?

### Conclusion

In every case, the best option is for the development organization to recognize and avoid its own overconfidence and to start taking the quality of its software architecture seriously.

To take software architecture seriously, you need to know what good software architecture is. To build a system with a design and an architecture that minimize effort and maximize productivity, you need to know which attributes of system architecture lead to that end.

That’s what this book is about. It describes what good clean architectures and designs look like, so that software developers can build systems that will have long profitable lifetimes.

不管怎么看，研发团队最好的选择是清晰地认识并避开工程师们过度自信的特点，开始认真地对待自己的代码架构，对其质量负责。要想提高自己软件架构的质量，就需要先知道什么是优秀的软件架构。而为了在系统构建过程中采用好的设计和架构以便減少构建成本，提高生产力，又需要先了解系统架构的各种属性与成本和生产力的关系。这就是这本书的主题。本书为读者描述了什么是优秀的、整洁的软件架构与设计，读者可以参考这些设计来构建一个长期稳定的、持久优秀的系统。

### 00

There has been a lot of confusion about design and architecture over the years. What is design? What is architecture? What are the differences between the two?

One of the goals of this book is to cut through all that confusion and to define, once and for all, what design and architecture are. For starters, I’ll assert that there is no difference between them. None at all.

The word「architecture」is often used in the context of something at a high level that is divorced from the lower-level details, whereas「design」more often seems to imply structures and decisions at a lower level. But this usage is nonsensical when you look at what a real architect does.

Consider the architect who designed my new home. Does this home have an architecture? Of course it does. And what is that architecture? Well, it is the shape of the home, the outward appearance, the elevations, and the layout of the spaces and rooms. But as I look through the diagrams that my architect produced, I see an immense number of low-level details. I see where every outlet, light switch, and light will be placed. I see which switches control which lights. I see where the furnace is placed, and the size and placement of the water heater and the sump pump. I see detailed depictions of how the walls, roofs, and foundations will be constructed.

In short, I see all the little details that support all the high-level decisions. I also see that those low-level details and high-level decisions are part of the whole design of the house.

And so it is with software design. The low-level details and the high-level structure are all part of the same whole. They form a continuous fabric that defines the shape of the system. You can’t have one without the other; indeed, no clear dividing line separates them. There is simply a continuum of decisions from the highest to the lowest levels.

一直以来，设计（Design）与架构（Architecture）这两个概念让大多数人十分迷惑。什么是设计？什么是架构？二者究有什么区别？本书的一个重要目标就是要清晰、明确地对二者进行定义。首先我要明确地说，二者没有任何区别。一丁点区别都没有！

「架构」这个词往往使用于「高层级」的讨论中。这类讨论一般都把「底层」的实现细节排除在外。而「设计」一词，往往用来指代具体的系统底层组织结构和实现的细节。但是，从一个真正的系统架构师的日常工作来看，这样的区分是根本不成立的。

以给我设计新房子的建筑设计师要做的事情为例。新房子当然是存在着既定架构的，但这个架构具体包含哪些内容呢？首先，它应该包括房屋的形状、外观设计、垂直高度、房间的布局，等等。但是，如果查看建筑设计师使用的图纸，会发现其中也充斥着大量的设计细节。如，我们可以看到每个插座、开关以及每个电灯具体的安装位置，同时也可以看到某个开关与所控制的电灯的具体连接信息；我们也能看到壁炉的具体安装位置，热水器的大小和位置信息，甚至是污水泵的位置；同时也可以看到关于墙体、屋顶和地基都有非常详细的建造说明。

总的来说，架构图里实际上包含了所有的底层设计细节，这些细节信息共同支撑了顶层的架构设计，底层设计信息和顶层架构设计共同组成了整个房屋的架构文档。软件设计也是如此。底层设计细节和高层架构信息是不可分割的。它们组合在一起，共同定义了整个软件系，缺一不可。所谓的底层和高层本身就是一系列策组成的连续体，并没有清晰的分界线。

### 1.1 The  Goal?

And the goal of those decisions? The goal of good software design? That goal is nothing less than my utopian description:

The goal of  software architecture is to minimize the human resources required to build and maintain the required system.

The measure of design quality is simply the measure of the effort required to meet the needs of the customer. If that effort is low, and stays low throughout the lifetime of the system, the design is good. If that effort grows with each new release, the design is bad. It’s as simple as that.

所有这些決策的终极目标是什么呢？一个好的软件设计的终极目标是什么呢？就像我之前描述过的：软件架构終极目标是，用最小的人力成本来满足构建和维护该系统的需求。

软件架构的优劣，可以用它满足用户需求所需要的成本来衡量。如果该成本很低，并且在系统的整个生命周期内一直都能维持这样的低成本，那么这个系统的设计就是优良的。如果该系的每次发布都会提升下一次变更的成本，那么这个设计就是不好的。就这么简单。

### 1.2 Case Study

As an example, consider the following case study. It includes real data from a real company that wishes to remain anonymous.

First, let’s look at the growth of the engineering staff. I’m sure you’ll agree that this trend is very encouraging. Growth like that shown in Figure 1.1 must be an indication of significant success!

Figure 1.1  Growth of the engineering staff

Now let’s look at the company’s productivity over the same time period, as measured by simple lines of code (Figure 1.2).

Figure 1.2  Productivity over the same period of time

Clearly something is going wrong here. Even though every release is supported by an ever-increasing number of developers, the growth of the code looks like it is approaching an asymptote. Now here’s the really scary graph: Figure 1.3 shows how the cost per line of code has changed over time.

These trends aren’t sustainable. It doesn’t matter how profitable the company might be at the moment: Those curves will catastrophically drain the profit from the business model and drive the company into a stall, if not into a downright collapse.

What caused this remarkable change in productivity? Why was the code 40 times more expensive to produce in release 8 as opposed to release 1?

Figure 1.3  Cost per line of code over time

下面来看一个真实案例，该案例中的数据均来源于个要求匿名的真实公司。

首先，我们来看一下工程师团队规模的增长。你肯定认为这个增长趋势是特别可喜的，像图 1.1 中的这种增长线条一定是公司业务取得巨大成功的直观体现。现在再让我们来看一下整个公司同期的生产效率（productivity），这里用简单的代码行数作为指标（参见图 1.2)。

这明显是有问题的。伴随着产品的每次发布，公司的工程师团队在持续不断地扩展壮大，但是仅从代码行数的增长来看，该产品却正在逐渐陷入困境。还有更可怕的：图 1.3 展示的是同期内每行代码的更成本。

显然，图中展示的趋势是不可持续的。不管公司现在的利润率有多高，图中线条表明，按这个趋势下去，公司的利润会被一点点榨干，整个公司会因此陷入困境，甚至直接关门倒闭究竟是什么因素造成了生产力的大幅变化呢？为什么第 8 代产品的构建成本要比第 1 代产品高 40 倍？

#### 1.2.1 The Signature of a Mess

What you are looking at is the signature of a mess. When systems are thrown together in a hurry, when the sheer number of programmers is the sole driver of output, and when little or no thought is given to the cleanliness of the code or the structure of the design, then you can bank on riding this curve to its ugly end.

Figure 1.4 shows what this curve looks like to the developers. They started out at nearly 100% productivity, but with each release their productivity declined. By the fourth release, it was clear that their productivity was going to bottom out in an asymptotic approach to zero.

Figure 1.4  Productivity by release

From the developers’ point of view, this is tremendously frustrating, because everyone is working hard. Nobody has decreased their effort.

And yet, despite all their heroics, overtime, and dedication, they simply aren’t getting much of anything done anymore. All their effort has been diverted away from features and is now consumed with managing the mess. Their job, such as it is, has changed into moving the mess from one place to the next, and the next, and the next, so that they can add one more meager little feature.

乱麻系统的特点

我们在这里看到的是一个典型的乱麻系统。这种系统一般都是没有经过设计，匆匆忙忙被构建起来的。然后为了加快发布的速度，拼命地往团队里加入新人，同时加上決策层对代码质量提升和设计结构优化存在着持续的、长久的忽视，这种状态能持续下去就怪了。

图 1.4 展示了系统开发者的切身体会。他们一开始的效率都接近 100%，然而伴随着每次产品的发布，他们的生产力直线下降。到了产品的第 4 版本时，很明显大家的生产力已经不可避免地趋近为零了。对系统的开发者来说，这会来很大的挫败感，因为团队中并没有人偷懒，每个人还都是和之前一样在拼命工作。

然而，不管他们投入了多少个人时间，救了多少次火，加了多少次班，他们的产出始终上不去。工程师的大部分时间都消耗在对现有系统的修修补补上，而不是真正完成实际的新功能。这些工程师真正的任务是：拆了东墙补西墙，周而往复，偶尔有精力能顺便实现一点小功能。

#### 1.2.2 The Executive View

If you think that’s bad, imagine what this picture looks like to the executives! Consider Figure 1.5, which depicts monthly development payroll for the same period.

Figure 1.5  Monthly development payroll by release

Release 1 was delivered with a monthly payroll of a few hundred thousand dollars. The second release cost a few hundred thousand more. By the eighth release monthly payroll was `$20` million, and climbing.

Just this chart alone is scary. Clearly something startling is happening. One hopes that revenues are outpacing costs and therefore justifying the expense. But no matter how you look at this curve, it’s cause for concern.

But now compare the curve in Figure 1.5 with the lines of code written per release in Figure 1.2. That initial few hundred thousand dollars per month bought a lot of functionality — but the final $20 million bought almost nothing! Any CFO would look at these two graphs and know that immediate action is necessary to stave off disaster.

But which action can be taken? What has gone wrong? What has caused this incredible decline in productivity? What can executives do, other than to stamp their feet and rage at the developers?

管理层视角

如果你觉得开发者们这样就已经够苦了，那么就再想想公司高管们的感受吧！请看图 1.5，该部门月工资同期图。

如你所见，产品的第 1 版是在月总工 10 万美元左右的时候上线的。第 2 版又花掉了几十万美元。当发布第 8 版的时候，部门月工资已经达到了 2 千万美元，而且还在持续上升也许我们可以指望该公司的营收增长远远超出成本增长，这样公司就还能维持正常运转。但是这么惊人的曲线还是值得我们深入挖掘其中存在的巨大问题的。

现在，只要将图 1.5 的月工资曲线和图 1.2 的每次发布代码行数曲线对比一下，任何一个理性的 CEO 都会一眼看出其中的问题：最开始的十几万美元工资给公司带来了很多新功能、新收益，而最后的 2 千万美元几乎全打了水漂。应立刻采取行动解决这个问题，刻不容缓但是具体采取什么样的行动才能解决向题呢？究竟问题出在哪里？是什么造成了工程师生产力的直线下降？高管们除了跺脚、发飙，还能做什么呢？

#### 1.2.3 What  Went  Wrong?

Nearly 2600 years ago, Aesop told the story of the Tortoise and the Hare. The moral of that story has been stated many times in many different ways: 1) Slow and steady wins the race. 2) The race is not to the swift, nor the battle to the strong. 3) The more haste, the less speed.

The story itself illustrates the foolishness of overconfidence. The Hare, so confident in its intrinsic speed, does not take the race seriously, and so naps while the Tortoise crosses the finish line.

Modern developers are in a similar race, and exhibit a similar overconfidence. Oh, they don’t sleep — far from it. Most modern developers work their butts off. But a part of their brain does sleep — the part that knows that good, clean, well-designed code matters.

These developers buy into a familiar lie:「We can clean it up later; we just have to get to market first!」Of course, things never do get cleaned up later, because market pressures never abate. Getting to market first simply means that you’ve now got a horde of competitors on your tail, and you have to stay ahead of them by running as fast as you can.

And so the developers never switch modes. They can’t go back and clean things up because they’ve got to get the next feature done, and the next, and the next, and the next. And so the mess builds, and productivity continues its asymptotic approach toward zero.

Just as the Hare was overconfident in its speed, so the developers are overconfident in their ability to remain productive. But the creeping mess of code that saps their productivity never sleeps and never relents. If given its way, it will reduce productivity to zero in a matter of months.

The bigger lie that developers buy into is the notion that writing messy code makes them go fast in the short term, and just slows them down in the long term. Developers who accept this lie exhibit the hare’s overconfidence in their ability to switch modes from making messes to cleaning up messes sometime in the future, but they also make a simple error of fact. The fact is that making messes is always slower than staying clean, no matter which time scale you are using.

Consider the results of a remarkable experiment performed by Jason Gorman depicted in Figure 1.6. Jason conducted this test over a period of six days. Each day he completed a simple program to convert integers into Roman numerals. He knew his work was complete when his predefined set of acceptance tests passed. Each day the task took a little less than 30 minutes. Jason used a well-known cleanliness discipline named test-driven development (TDD) on the first, third, and fifth days. On the other three days, he wrote the code without that discipline.

Figure 1.6  Time to completion by iterations and use/non-use of TDD

First, notice the learning curve apparent in Figure 1.6. Work on the latter days is completed more quickly than the former days. Notice also that work on the TDD days proceeded approximately 10% faster than work on the non-TDD days, and that even the slowest TDD day was faster than the fastest non-TDD day.

Some folks might look at that result and think it’s a remarkable outcome. But to those who haven’t been deluded by the Hare’s overconfidence, the result is expected, because they know this simple truth of software development:

The only way to go fast, is to go well.

And that’s the answer to the executive’s dilemma. The only way to reverse the decline in productivity and the increase in cost is to get the developers to stop thinking like the overconfident Hare and start taking responsibility for the mess that they’ve made.

The developers may think that the answer is to start over from scratch and redesign the whole system — but that’s just the Hare talking again. The same overconfidence that led to the mess is now telling them that they can build it better if only they can start the race over. The reality is less rosy:

Their overconfidence will drive the redesign into the same mess as the original project.

问题到底在哪里

大约 2600 年前，《伊索寓言》里写到了龟兔赛跑的故事。这个故事的主题思想可以归纳为以下几种：1）慢但是稳，是成功的秘诀。2）该比赛并不是拼谁开始跑得快，也不是拼谁更有力气的。3）心态越急，反而跑得越。

这个故事本身掲露的是过度自信的愚行为。兔子由于对自己速度的过度自信，没有把乌龟当回事，结果乌龟爬过终点线取得胜利的时候，它还在睡觉。这和现代软件研发工作有点类似，现在的软件研发工程师都有点过于自信。哦，当然，他们确实不会偷懒，一点也不。但是他们真正偷懒的地方在于一持续低估那些好的、良好设计的、整洁的代码的重要性。

这些工程师们普遍用一句话来欺骗自己：「我们可以未来再重构代码，产品上线最重要！」但是结果大家都知道，产品上线以后重构工作就再没人提起了。市场的压力永远也不会消退，作为首先上市的产品，后面有无数的竞争对手追赶，必须要比他们跑得更快才能保持领先所以，重构的时机永远不会再有了。工程师们忙于完成新功能，新功能做不完，哪有时间重构老的代码？循环往复，系统成了一团乱麻，生产效率持续直线下降，直至为零。结果就像龟兔赛跑中过于自信的兔子一样，软件研发工程师们对自己保持高产出的能力过于自信了。但是乱成一团的系統代码可没有休息时间，也不会放松。如果不严加提防，在几个月之内，整个研发团队就会陷入困境。

工程师们经常相信的另外一个错误观点是：「在工程中容忍糟糕的代码存在可以在短期内加快该工程上线的速度，未来这些代码会造成一些额外的工作量，但是并没有什么大不了。」相信这些鬼话的工程师对自己清理乱麻代码的能力过于自信了。但是更重要的是，他们还忽视了一个自然规律：无论是从短期还是长期来看，胡乱编写代码的工作速度其实比循规蹈矩更慢。

图 1.6 展示的是 Jason Gorman 进行的一次为期 6 天的实验。在该实验中，Jaosn 每天都编写一段代码，功能是将一个整数转化为相应罗马数字的字符串。当事先定义好的一个测试集完全通过时，即认为当天工作完成。每天实验的时长不超过 30 分钟。第一天、第三天和第五天，Jason 在编写代码的过程中采用了业界知名的优质代码方法论：测试驱动开发（TDD），而其他三天他则直接从头开始编写代码。

首先，我们要关注的是图 1.6 中那些柱状图。很显然，日子越往后，完成工作所需的时间就越少。同时，我们也可以看到当人们采用了 TDD 方法编程后，一般就会比未采用 TDD 方法编程少用 10% 的时间，并且采用 TDD 方法编程时最差的一天也比未采用 TDD 方法编程时最好的一天用时要短对于这个结果，有些人可能会觉得挺意外的。但是对常年关注软件开发本质的人来说，它其实揭示了软件开发的一个核心特点。

要想跑得快，先要得稳。

综上所述，管理层扭转局面的唯一选择就是扭转开发者的观念，让他们从过度自信的兔子模式转变回来，为自己构建的乱麻系统负起责任来。

当然，某些软件研发工程师可能会认为挽救一个系统的唯一办法是抛弃现有系，设计一个全新的系統来替代。但是这里仍然没有逃离过度自信。试问：如果是工程师的过度自信导致了目前的一团乱麻，那么，我们有什么理由认为让他们从头开始，结果就会更好呢？

过度自信只会使得重构设计陷入和原项目一样的困局中。

## 0201. A Tale of Two Values

Every software system provides two different values to the stakeholders: behavior and structure. Software developers are responsible for ensuring that both those values remain high. Unfortunately, they often focus on one to the exclusion of the other. Even more unfortunately, they often focus on the lesser of the two values, leaving the software system eventually valueless.

对于每个软件系，我们都可以通过行为和架构两个维度来体现它的实际价值。软件研发人员应该确保自己的系统在这两个维度上的实际价值都能长时间维持在很高的状态。不幸的是，他们往往只关注一个维度，而忽视了另外一个维度。更不幸的是，他们常常关注的还是错误的维度，这导致了系统的价值最终趋降为零。

### 2.1 Behavior

The first value of software is its behavior. Programmers are hired to make machines behave in a way that makes or saves money for the stakeholders. We do this by helping the stakeholders develop a functional specification, or requirements document. Then we write the code that causes the stakeholder’s machines to satisfy those requirements.

When the machine violates those requirements, programmers get their debuggers out and fix the problem.

Many programmers believe that is the entirety of their job. They believe their job is to make the machine implement the requirements and to fix any bugs. They are sadly mistaken.

行为价值

软件系统的行为是其最直观的价值维度。程序员的工作就是让机器按照某种指定方式运转，给系统的使用者创造或者提高利润。程序员们为了达到这个目的，往往需要帮助系统使用者编写一个对系统功能的定义，也就是需求文档。然后，程序员们再把需求文档转化为实际的代码。

当机器出现异常行为时，程序员要负责调试，解决这些问题。大部分程序员认为这就是他们的全部工作。他们的工作是且仅是：按照需求文档编写代码，并且修复任何 Bug。这真是大错特错。

### 2.2 Architecture

The second value of software has to do with the word「software」 — a compound word composed of「soft」and「ware.」The word「ware」means「product」; the word「soft」… Well, that’s where the second value lies.

Software was invented to be「soft.」It was intended to be a way to easily change the behavior of machines. If we’d wanted the behavior of machines to be hard to change, we would have called it hardware.

To fulfill its purpose, software must be soft — that is, it must be easy to change. When the stakeholders change their minds about a feature, that change should be simple and easy to make. The difficulty in making such a change should be proportional only to the scope of the change, and not to the shape of the change.

It is this difference between scope and shape that often drives the growth in software development costs. It is the reason that costs grow out of proportion to the size of the requested changes. It is the reason that the first year of development is much cheaper than the second, and the second year is much cheaper than the third.

From the stakeholders’ point of view, they are simply providing a stream of changes of roughly similar scope. From the developers’ point of view, the stakeholders are giving them a stream of jigsaw puzzle pieces that they must fit into a puzzle of ever-increasing complexity. Each new request is harder to fit than the last, because the shape of the system does not match the shape of the request.

I’m using the word「shape」here in a unconventional way, but I think the metaphor is apt. Software developers often feel as if they are forced to jam square pegs into round holes.

The problem, of course, is the architecture of the system. The more this architecture prefers one shape over another, the more likely new features will be harder and harder to fit into that structure. Therefore architectures should be as shape agnostic are practical.

架构价值

软件系统的第二个价值维度，就体现在软件这个英文单词上：software。ware 的意思是「产品」，而 soft 的意思，不言而喻，是指软件的灵活性。软件系统必须保持灵活。软件发明的目的，就是让我们可以以一种灵活的方式来改变机器的工作行为。对机器上那些很难改变的工作行为，我们通常称之为硬件（hardware）。

为了达到软件的本来目的，软件系统必须够「软」一一 也就是说，软件应该容易被修改。当需求方改变需求的时候，随之所需的软件变更必须可以简单而方便地实现。变更实施的难度应该和变更的范畴（scope）成等比关系，而与变更的具体形状（shape）无关。需求变更的范畴与形状，是决定对应软件变更实施成本高低的关键。这就是为什么有的代码更的成本与其实现的功能改不成比例。这也是为什么第二年的研发成本比第一年的高很多，第三年又比第二年更高。

从系统相关方（Stakeholder）的角度来看，他们所提出的一系列的变更需求的范畴都是类似的，因此成本也应该是固定的。但是从研发者角度来看，系统用户持续不断的变更需求就像是要求他们不停地用一堆不同形状的拼图块，拼成一个新的形状。整个拼图的过程越来越困难，因为现有系统的形状永远和需求的形状不一致。

我们在这里使用了「形状」这个词，这可能不是该词的标准用法，但是其寓意应该很明确。毕竟，软件工程师们经常会觉得自己的工作就是把方螺丝拧到圆螺丝孔里面。问题的实际根源当然就是系统的架构设计。如果系统的架构设计偏向某种特定的「形状」，那么新的变更就会越来越难以实施。所以，好的系统架构设计应该尽可能做到与「形状」无关。

### 2.3 The Greater Value

Function or architecture? Which of these two provides the greater value? Is it more important for the software system to work, or is it more important for the software system to be easy to change?

If you ask the business managers, they’ll often say that it’s more important for the software system to work. Developers, in turn, often go along with this attitude. But it’s the wrong attitude. I can prove that it is wrong with the simple logical tool of examining the extremes.

If  you give me a program that works perfectly but is impossible to change, then it won’t work when the requirements change, and I won’t be able to make it work. Therefore the program will become useless.

If  you give me a program that does not work but is easy to change, then I can make it work, and keep it working as requirements change. Therefore the program will remain continually useful.

You may not find this argument convincing. After all, there’s no such thing as a program that is impossible to change. However, there are systems that are practically impossible to change, because the cost of change exceeds the benefit of change. Many systems reach that point in some of their features or configurations.

If you ask the business managers if they want to be able to make changes, they’ll say that of course they do, but may then qualify their answer by noting that the current functionality is more important than any later flexibility. In contrast, if the business managers ask you for a change, and your estimated costs for that change are unaffordably high, the business managers will likely be furious that you allowed the system to get to the point where the change was impractical.

哪个价值维度更重要

那么，究竟是系行为更重要，还是系统架构的灵活性更重要？哪个价值更大？系統正常工作更重要，还是系统易于修改更重要？

如果这个问题由业务部门来回答，他们通常认为系正常工作很重要。系统开发人员常常也就跟随采取了这种态度。但是这种态度是错误的。下面我就用简单的逻辑推导来证明这个态度的错误性。

1、如果某程序可以正常工作，但是无法修改，那么当需求交更的时候它就不再能够正常工作了，我们也无法通过修改让它能续正常工作。因此，这个程序的价值将成为 0。

2、如果某程序目前无法正常工作，但是我们可以很容易地修改它，那么将它改好，并且随着需求变化不停地修它，都应该是很易的事。因此，这个程序会持续产生价值。

当然，上面的逻辑论断可能不足以说服大家，毕竟理论上没有什么程序是不能修改的。但是，现实中有一些系統确实无法更改，因为其变更实施的成本会远远超过变更来的价值。你在实际工作中一定遇到过很多这样的例子。

如果你问业务部门，是否想要能够变更需求，他们的回答一般是肯定的，而且他们会增加一句：完成现在的功能比实现未来的灵活度更重要。但讽刺的是，如果事后业务部门提出了一项需求，而你的预估工作量大大超出他们的预期，这帮家伙通常会对你放任系混乱到无法变更的状态而勃然大怒。

### 2.4 Eisenhower's Matrix

Consider President Dwight D. Eisenhower’s matrix of importance versus urgency (Figure 2.1). Of this matrix, Eisenhower said: I have two kinds of  problems, the urgent and the important. The urgent are not important, and the important are never urgent. 1

Figure 2.1  Eisenhower matrix

There is a great deal of truth to this old adage. Those things that are urgent are rarely of great importance, and those things that are important are seldom of great urgency.

The first value of software — behavior — is urgent but not always particularly important.

The second value of software — architecture — is important but never particularly urgent.

Of course, some things are both urgent and important. Other things are not urgent and not important. Ultimately, we can arrange these four couplets into priorities: 1) Urgent and important. 2) Not urgent and important. 3) Urgent and not important. 4) Not urgent and not important.

Note that the architecture of the code — the important stuff — is in the top two positions of this list, whereas the behavior of the code occupies the first and third positions.

The mistake that business managers and developers often make is to elevate items in position 3 to position 1. In other words, they fail to separate those features that are urgent but not important from those features that truly are urgent and important. This failure then leads to ignoring the important architecture of the system in favor of the unimportant features of the system.

The dilemma for software developers is that business managers are not equipped to evaluate the importance of architecture. That’s what software developers were hired to do. Therefore it is the responsibility of the software development team to assert the importance of architecture over the urgency of features.

1 From a speech at Northwestern University in 1954.

艾森豪威尔矩阵

我们来看美国前总统艾森豪威尔的紧急/重要矩阵（参见图 2.1），面对这个矩阵，艾森豪威尔曾说道：我有两种难题：急的和重要的，而紧急的难永远是不重要的，重要的难题永远是不紧急的。

虽然老调重弹，但其中的道理依然成立。确实，紧急的事情常常没那么重要，而重要的事情则似乎永远也排不上优先级次件系统的第值维度系统行为，是紧急的，但是并不总是特别重要件系的第二个价值维度：系統架构，是重要的，但是并不总是特别紧急。

当然，我们会有些重要且紧急的事情，也会有一些事情不重要也不紧急。最终我们应将这四类事情进行如下排序：1）重要且紧急。2）重要不紧急。3）不重要但紧急。4）不重要且不紧急。

在这里你可以看到，软件的系统架构 一一 那些重要的事情一占据了该列表的前两位，而系统行为那些紧急的事情占据了第一和第三位。

业务部门与研发人员经常犯的共同错误就是将第三优先级的事情提到第一优先级去做。换句话说，他们没有把真正紧急并且重要的功能和紧急但是不重要的功能分开。这个错误导致了重要的事被忽略了，重要的系统架构问题让位给了不重要的系统行为功能。但研发人员还忘了一点，那就是业务部门原本就是没有能力评估系架构的重要程度的，这本来就应该是研发人员自己的工作职责！所以，平衡系统架构的重要性与功能的紧急程度这件事，是软件研发人员自己的职责。

### 2.5 Fight for the Architecture

Fulfilling this responsibility means wading into a fight — or perhaps a better word is「struggle.」Frankly, that’s always the way these things are done. The development team has to struggle for what they believe to be best for the company, and so do the management team, and the marketing team, and the sales team, and the operations team. It’s always a struggle.

Effective software development teams tackle that struggle head on. They unabashedly squabble with all the other stakeholders as equals. Remember, as a software developer, you are a stakeholder. You have a stake in the software that you need to safeguard. That’s part of your role, and part of your duty. And it’s a big part of why you were hired.

This challenge is doubly important if you are a software architect. Software architects are, by virtue of their job description, more focused on the structure of the system than on its features and functions. Architects create an architecture that allows those features and functions to be easily developed, easily modified, and easily extended.

Just remember: If architecture comes last, then the system will become ever more costly to develop, and eventually change will become practically impossible for part or all of the system. If that is allowed to happen, it means the software development team did not fight hard enough for what they knew was necessary.

为好的软件架构而持续斗争

为了做好上述职责，软件团队必须做好斗争的准备 一一 或者说「长期抗争」的准备。现状就是这样。研发团队必须从公司长远利益出发与其他部门抗争，这和管理团队的工作甚至市场团队、销售团队、运营团队都是这样。公司内部的抗争本来就是无止境的。

有成效的软件研发团队会迎难而上，毫不掩饰地与所有其他的系统相关方进行平等的争吵。请记住，作为一名软件开发人员，你也是相关者之ー。软件系统的可维护性需要由你来保护，这是你角色的一部分，也是你职责中不可缺少的一部分。公司雇你的很大一部分原因就是需要有人来做这件事。如果你是软件架构师，那么这项工作就加倍重要了。软件架构师这一职责本身就应更关注系统的整体结构，而不是具体的功能和系统行为的实现。软件架构师必须创建出一个可以让功能实现起来更容易、修改起来更简单、扩展起来更轻松的软件架构。请记住：如果忽视软件架构的价值，系统将会变得越来越难以维护，终会有一天，系统将会变得再也无法修改。如果系统变成了这个样子，那么说明软件开发团队没有和需求方做足够的抗争，没有完成自己应尽的职责。
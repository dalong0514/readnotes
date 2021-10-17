## 记忆时间

2021-05-10

## 卡片

### 0001. 反常识卡 —— 架构和设计是一回事

常识：架构是高层，设计是底部细节。

反常识：

数据源自「0101. What Is Design and Architecture」：

There has been a lot of confusion about design and architecture over the years. What is design? What is architecture? What are the differences between the two?

One of the goals of this book is to cut through all that confusion and to define, once and for all, what design and architecture are. For starters, I'll assert that there is no difference between them. None at all.

The word「architecture」is often used in the context of something at a high level that is divorced from the lower-level details, whereas「design」more often seems to imply structures and decisions at a lower level. But this usage is nonsensical when you look at what a real architect does.

Consider the architect who designed my new home. Does this home have an architecture? Of course it does. And what is that architecture? Well, it is the shape of the home, the outward appearance, the elevations, and the layout of the spaces and rooms. But as I look through the diagrams that my architect produced, I see an immense number of low-level details. I see where every outlet, light switch, and light will be placed. I see which switches control which lights. I see where the furnace is placed, and the size and placement of the water heater and the sump pump. I see detailed depictions of how the walls, roofs, and foundations will be constructed.

In short, I see all the little details that support all the high-level decisions. I also see that those low-level details and high-level decisions are part of the whole design of the house.

And so it is with software design. The low-level details and the high-level structure are all part of the same whole. They form a continuous fabric that defines the shape of the system. You can't have one without the other; indeed, no clear dividing line separates them. There is simply a continuum of decisions from the highest to the lowest levels.

一直以来，设计（Design）与架构（Architecture）这两个概念让大多数人十分迷惑。什么是设计？什么是架构？二者究有什么区别？本书的一个重要目标就是要清晰、明确地对二者进行定义。首先我要明确地说，二者没有任何区别。一丁点区别都没有！

「架构」这个词往往使用于「高层级」的讨论中。这类讨论一般都把「底层」的实现细节排除在外。而「设计」一词，往往用来指代具体的系统底层组织结构和实现的细节。但是，从一个真正的系统架构师的日常工作来看，这样的区分是根本不成立的。

以给我设计新房子的建筑设计师要做的事情为例。新房子当然是存在着既定架构的，但这个架构具体包含哪些内容呢？首先，它应该包括房屋的形状、外观设计、垂直高度、房间的布局，等等。但是，如果查看建筑设计师使用的图纸，会发现其中也充斥着大量的设计细节。如，我们可以看到每个插座、开关以及每个电灯具体的安装位置，同时也可以看到某个开关与所控制的电灯的具体连接信息；我们也能看到壁炉的具体安装位置，热水器的大小和位置信息，甚至是污水泵的位置；同时也可以看到关于墙体、屋顶和地基都有非常详细的建造说明。

总的来说，架构图里实际上包含了所有的底层设计细节，这些细节信息共同支撑了顶层的架构设计，底层设计信息和顶层架构设计共同组成了整个房屋的架构文档。软件设计也是如此。底层设计细节和高层架构信息是不可分割的。它们组合在一起，共同定义了整个软件系，缺一不可。所谓的底层和高层本身就是一系列策组成的连续体，并没有清晰的分界线。

### 0101. 主题卡 —— The architecture rules are the same

I've built a lot of apps. I've built a lot of systems. And from them all, and by taking them all into consideration, I've learned something startling.

The architecture rules are the same!

1『软件架构的底层逻辑是相同的，做一张主题卡片。』—— 已完成

This is startling because the systems that I have built have all been so radically different. Why should such different systems all share similar rules of architecture? My conclusion is that the rules of  software architecture are independent of  every other variable.

This is even more startling when you consider the change that has taken place in hardware over the same half-century. I started programming on machines the size of kitchen refrigerators that had half-megahertz cycle times, 4K of core memory, 32K of disk memory, and a 10 character per second teletype interface. I am writing this preface on a bus while touring in South Africa. I am using a MacBook with four i7 cores running at 2.8 gigahertz each. It has 16 gigabytes of RAM, a terabyte of SSD, and a 2880*1800 retina display capable of showing extremely high-definition video. The difference in computational power is staggering. Any reasonable analysis will show that this MacBook is at least 1022 more powerful than those early computers that I started using half a century ago.

Twenty-two orders of magnitude is a very large number. It is the number of angstroms from Earth to Alpha-Centuri. It is the number of electrons in the change in your pocket or purse. And yet that number — that number at least — is the computational power increase that I have experienced in my own lifetime.

And with all that vast change in computational power, what has been the effect on the software I write? It's gotten bigger certainly. I used to think 2000 lines was a big program. After all, it was a full box of cards that weighed 10 pounds. Now, however, a program isn't really big until it exceeds 100,000 lines.

The software has also gotten much more performant. We can do things today that we could scarcely dream about in the 1960s. The Forbin Project, The Moon Is a Harsh Mistress, and 2001: A Space Odyssey all tried to imagine our current future, but missed the mark rather significantly. They all imagined huge machines that gained sentience. What we have instead are impossibly small machines that are still … just machines.

And there is one thing more about the software we have now, compared to the software from back then: It's made of  the same stuff. It's made of if statements, assignment statements, and while loops.

Oh, you might object and say that we've got much better languages and superior paradigms. After all, we program in Java, or C#, or Ruby, and we use object-oriented design. True — and yet the code is still just an assemblage of sequence, selection, and iteration, just as it was back in the 1960s and 1950s.

When you really look closely at the practice of programming computers, you realize that very little has changed in 50 years. The languages have gotten a little better. The tools have gotten fantastically better. But the basic building blocks of a computer program have not changed.

If I took a computer programmer from 1966 forward in time to 2016 and put her [1] in front of my MacBook running IntelliJ and showed her Java, she might need 24 hours to recover from the shock. But then she would be able to write the code. Java just isn't that different from C, or even from Fortran.

And if I transported you back to 1966 and showed you how to write and edit PDP-8 code by punching paper tape on a 10 character per second teletype, you might need 24 hours to recover from the disappointment. But then you would be able to write the code. The code just hasn't changed that much.

That's the secret: This changelessness of the code is the reason that the rules of software architecture are so consistent across system types. The rules of software architecture are the rules of ordering and assembling the building blocks of programs. And since those building blocks are universal and haven't changed, the rules for ordering them are likewise universal and changeless.

Younger programmers might think this is nonsense. They might insist that everything is new and different nowadays, that the rules of the past are past and gone. If that is what they think, they are sadly mistaken. The rules have not changed. Despite all the new languages, and all the new frameworks, and all the paradigms, the rules are the same now as they were when Alan Turing wrote the first machine code in 1946.

But one thing has changed: Back then, we didn't know what the rules were. Consequently, we broke them, over and over again. Now, with half a century of experience behind us, we have a grasp of those rules.

And it is those rules — those timeless, changeless, rules — that this book is all about.

### 0102. 主题卡 —— 三大编程范式

面向结构编程、面向对象编程、函数式编程。

What does this history lesson on paradigms have to do with architecture? Everything. We use polymorphism as the mechanism to cross architectural boundaries; we use functional programming to impose discipline on the location of and access to data; and we use structured programming as the algorithmic foundation of our modules. Notice how well those three align with the three big concerns of architecture: function, separation of components, and data management.

大家可能会问，这些编程范式的历史知识与软件架构有关系吗？当然有，而且关系相当密切。譬如说，多态是我们跨越架构边界的手段，函数式编程是我们规范和限制数据存放位置与访问权限的手段，结构化编程则是各模块的算法实现基础。这和软件架构的三大关注重点不谋而合：功能性、组件独立性以及数据管理。

The first paradigm to be adopted (but not the first to be invented) was structured programming, which was discovered by Edsger Wybe Dijkstra in 1968. Dijkstra showed that the use of unrestrained jumps (goto statements) is harmful to program structure. As we'll see in the chapters that follow, he replaced those jumps with the more familiar if/then/else and do/while/until constructs. We can summarize the structured programming paradigm as follows: Structured programming imposes discipline on direct transfer of  control.

结构化编程是第一个普遍被采用的编程范式（但是却不是第一个被提出的），由 Edsger Wybe Dijkstra 于 1968 年最先提出。与此同时，Dijkstra 还论证了使用 goto 这样的无限制跳转语句将会损害程序的体结构。接下来的章节我们还会说到，也是这位 Dijkstra 最先主张用我们现在熟知的 if/then/else 语句和 do/while/until 语句来代替跳转语句的。我们可以将结构化编程范式归结为一句话：结构化程对程序控制权的直接转移进行了限制和规范。

The second paradigm to be adopted was actually discovered two years earlier, in 1966, by Ole Johan Dahl and Kristen Nygaard. These two programmers noticed that the function call stack frame in the ALGOL language could be moved to a heap, thereby allowing local variables declared by a function to exist long after the function returned. The function became a constructor for a class, the local variables became instance variables, and the nested functions became methods. This led inevitably to the discovery of polymorphism through the disciplined use of function pointers. We can summarize the object-oriented programming paradigm as follows: Object-oriented programming imposes discipline on indirect transfer of  control.

1-3『这里对面向对象编程底层逻辑的描述，联想到学 JS 时，看亚历山大那个 CEO 的系列文章里，介绍闭包相关知识时，有相通的感觉。（2020-12-24）』

说到编程领域中第二个被广泛采用的编程范式，当然就是面向对象编程了。事实上，这个编程范式的提出比结构化编程还早了两年，是在 1966 年由 Ole Johan Dahl 和 Kriste Nygaard 在论文中总结归纳出来的。这两个程序员注意到在 ALGOLT 语言中，函数调用堆栈（call stack frame）可以被挪到堆存区域里，这样函数定义的本地变量就可以在函数返回之后继续存在。这个函数就成为了一个类（class）的构造函数，而它所定义的本地变量就是类的成员变量，构造函数定义的嵌套函数就成为了成员方法（method）。这样一来，我们就可以利用多态（polymorphism）来限制用户对函数指针的使用。在这里，我们也可以用一句话来总结面向对象编程：面向对象编程对程序控制权的间接转移进行了限制和规范。

The third paradigm, which has only recently begun to be adopted, was the first to be invented. Indeed, its invention predates computer programming itself. Functional programming is the direct result of the work of Alonzo Church, who in 1936 invented λ-calculus while pursuing the same mathematical problem that was motivating Alan Turing at the same time. His λ-calculus is the foundation of the LISP language, invented in 1958 by John McCarthy. A foundational notion of λ-calculus is immutability — that is, the notion that the values of symbols do not change. This effectively means that a functional language has no assignment statement. Most functional languages do, in fact, have some means to alter the value of a variable, but only under very strict discipline. We can summarize the functional programming paradigm as follows: Functional programming imposes discipline upon assignment.

尽管第三个编程范式是近些年オ刚刚开始被采用的，但它其实是三个范式中最先被发明的。事实上，函数式编程概念是基于与阿兰·图灵同时代的数学家 Alonzo Church 在 1936 年发明的 λ 演算的直接衍生物。1958 年 John Mccarthy 利用其作为基础发明了 LISP 语言。众所周知，λ 演算法的一个核心思想是不可变性 一一 某个符号所对应的值是永远不变的，所以从理论上来说，函数式编程语言中应该是没有赋值语句的。大部分函数式编程语言只允许在非常严格的限制条件下，可以更改某个变量的值。因此，我们在这里可以将函数式编程范式总结为下面这句话：函数式编程对程序中的值进行了限制和规范。

Notice the pattern that I've quite deliberately set up in introducing these three programming paradigms: Each of the paradigms removes capabilities from the programmer. None of them adds new capabilities. Each imposes some kind of extra discipline that is negative in its intent. The paradigms tell us what not to do, more than they tell us what to do.

Another way to look at this issue is to recognize that each paradigm takes something away from us. The three paradigms together remove goto statements, function pointers, and assignment. Is there anything left to take away?

Probably not. Thus these three paradigms are likely to be the only three we will see — at least the only three that are negative. Further evidence that there are no more such paradigms is that they were all discovered within the ten years between 1958 and 1968. In the many decades that have followed, no new paradigms have been added.

后面 3 个编程范式章节总结内容汇总：

It is this ability to create falsifiable units of programming that makes structured programming valuable today. This is the reason that modern languages do not typically support unrestrained goto statements. Moreover, at the architectural level, this is why we still consider functional decomposition to be one of our best practices.

At every level, from the smallest function to the largest component, software is like a science and, therefore, is driven by falsifiability. Software architects strive to define modules, components, and services that are easily falsifiable (testable). To do so, they employ restrictive disciplines similar to structured programming, albeit at a much higher level. It is those restrictive disciplines that we will study in some detail in the chapters to come.

结构化编程范式中最有价值的地方就是，它予了我们创造可证伪程序单元的能力。这就是为什么现代程语言一般不支持无限制的 goto 语句。更重要的是，这也是为什么在架构设计领域，功能性降解拆分仍然是最佳实践之一。无论在哪一个层面上，从最小的函数到最大组件，软件开发的过程都和科学研究非常类似，它们都是由证伪驱动的。软件架构师需要定义可以方便地进行证伪（测试）的模块、组件以及服务。为了达到这个目的，他们需要将类似结构化编程的限制方法应用在更高的层面上。我们在接下来的章节中将会深入研究这些限制性的方法。

1『印象中，消除 goto 语言的 Edsger Wybe Dijkstra，他从数学上证明了「结构性」语言的可证伪性。回复：下面有详细的讲解。（2020-12-24）』

What is OO? There are many opinions and many answers to this question. To the software architect, however, the answer is clear: OO is the ability, through the use of polymorphism, to gain absolute control over every source code dependency in the system. It allows the architect to create a plugin architecture, in which modules that contain high-level policies are independent of modules that contain low-level details. The low-level details are relegated to plugin modules that can be deployed and developed independently from the modules that contain high-level policies.

面向对象编程到底是什么？业界在这个问题上存在着很多不同的说法和意见。然而对一个软件架构师来说，其含义应该是非常明确的：面向对象编程就是以多态为手段来对源代码中的依赖关系进行控制的能力，这种能力让软件架构师可以构建出某种插件式架构，让高层策略性组件与底层实现性组件相分离，底层组件可以被编译成插件，实现独立于高层组件的开发和部署。

To summarize: 1) Structured programming is discipline imposed upon direct transfer of control. 2) Object-oriented programming is discipline imposed upon indirect transfer of control. 3) Functional programming is discipline imposed upon variable assignment.

Each of these three paradigms has taken something away from us. Each restricts some aspect of the way we write code. None of them has added to our power or our capabilities. What we have learned over the last half-century is what not to do.

With that realization, we have to face an unwelcome fact: Software is not a rapidly advancing technology. The rules of software are the same today as they were in 1946, when Alan Turing wrote the very first code that would execute in an electronic computer. The tools have changed, and the hardware has changed, but the essence of software remains the same.

Software — the stuff of computer programs — is composed of sequence, selection, iteration, and indirection. Nothing more. Nothing less.

下面我们来总结一下：1）结构化编程是对程序控制权的直接转移的限制。2）面向对象编程是对程序控制权的间接转移的限制。3）函数式编程是对程序中賦值操作的限制。

这三个编程范式都对程序员提出了新的限制。每个范式都约束了某种编写代码的方式，没有一个编程范式是在增加新能力。也就是说，我们过去 50 年学到的东西主要是什么不应该做。我们必须面对这种不友好的现实：软件构建并不是一个迅速前进的技术。今天构建软件的规则和 1946 年阿兰图灵写下电子计算机的第一行代码时是一样的。尽管工具变化了，硬件变化了，但是软件编程的核心没有变。总而言之，软件，或者说计算机程序无一例外是由顺序结构、分支结构、循环结构和间接转移这几种行为组合而成的，无可增加，也缺一不可。

### 0103. 主题卡 —— 科学与数学的区别以及软件开发是科学范畴

Science is fundamentally different from mathematics, in that scientific theories and laws cannot be proven correct. I cannot prove to you that Newton's second law of motion, F = ma, or law of gravity, F = Gm1m2/r^2, are correct. I can demonstrate these laws to you, and I can make measurements that show them correct to many decimal places, but I cannot prove them in the sense of a mathematical proof. No matter how many experiments I conduct or how much empirical evidence I gather, there is always the chance that some experiment will show that those laws of motion and gravity are incorrect.

That is the nature of scientific theories and laws: They are falsifiable but not provable. And yet we bet our lives on these laws every day. Every time you get into a car, you bet your life that F = ma is a reliable description of the way the world works. Every time you take a step, you bet your health and safety that F = Gm1m2/r^2 is correct.

Science does not work by proving statements true, but rather by proving statements false. Those statements that we cannot prove false, after much effort, we deem to be true enough for our purposes. Of course, not all statements are provable. The statement「This is a lie」is neither true nor false. It is one of the simplest examples of a statement that is not provable.

Ultimately, we can say that mathematics is the discipline of proving provable statements true. Science, in contrast, is the discipline of proving provable statements false.

1-2『有关科学与数学的区别，之前在很多地方看到过，比如吴军的数学通识课，但还是觉得这里作者将的相对通透，而且下面提到软件开发是科学范畴而非数学范畴，给自己醍醐灌顶的感觉。科学与数学的区别以及软件开发是科学范畴，做一张主题卡片。（2020-12-24）』—— 已完成

科学和数学在证明方法上有着根本性的不同，科学理论和科学定律通常是无法被证明的，譬如我们并没有办法证明牛顿第二运动定律 F=ma 或者万有引カ定律 F=Gm1m2/r^2 是正确的，但我们可以用实际案例来演示这些定律的正确性，并通过高精度测量来证明当相关精度达到小数点后多少位时，被测量对象仍然一直满足这个定律。但我们始终没有办法像用数学方法一样推导出这个定律。而且，不管我们进行多少次正确的验，也无法排除今后会存在某一次实验可以推翻牛顿第二运动定律与万有引力定律的可能性。

这就是科学理论和科学定律的特点：它们可以被证伪，但是没有办法被证明。但是我们仍然每天都在依赖这些定律生活。开车的时候，我们就等于是在用性命担保 F=ma 是对世界运转方式的一个可靠的描述。每当我们迈出一步的时候，就等于在亲身证明 F=Gm1m2/r^2 是正确的。

科学方法论不需要证明某条结论是正确的，只需要想办法证明它是错误的。如果某个结论经过一定的努力无法证伪，我们则认为它在当下是足够正确的。当然，不是所有的结论都可以被证明或者证伪的。举一个最简单的不可证明的例子：「这句话是假的」，非真也非伪。最终，我们可以说数学是要将可证明的结论证明，而与之相反，科学研究则是要将可证明的结论证伪。

Dijkstra once said,「Testing shows the presence, not the absence, of bugs.」In other words, a program can be proven incorrect by a test, but it cannot be proven correct. All that tests can do, after sufficient testing effort, is allow us to deem a program to be correct enough for our purposes.

The implications of this fact are stunning. Software development is not a mathematical endeavor, even though it seems to manipulate mathematical constructs. Rather, software is like a science. We show correctness by failing to prove incorrectness, despite our best efforts.

Such proofs of incorrectness can be applied only to provable programs. A program that is not provable — due to unrestrained use of goto, for example — cannot be deemed correct no matter how many tests are applied to it.

Structured programming forces us to recursively decompose a program into a set of small provable functions. We can then use tests to try to prove those small provable functions incorrect. If such tests fail to prove incorrectness, then we deem the functions to be correct enough for our purposes.

1『上面的信息太有感觉了，突然领悟到「测试」的真谛，功能拆解成一个个「小函数」，颗粒度越细越好，每个小函数做单元测试，每个小函数无法被证伪，那么组合起来的功能也是没法证伪的。（2020-12-24）』

Dijkstra 曾经说过「测试只能展示 Bug 的存在，并不能证明不存在 Bug」，换句话说，一段程序可以由一个测试来证明其错误性，但是却不能被证明是正确的。测试的作用是让我们得出某段程序已经足够实现当前目标这一结论。这一事实所带来的影响是惊人的。软件开发虽然看起来是在操作很多数学结构，其实不是一个数学研究过程。恰恰相反，软件开发更像是一门科学研究学科，我们通过无法证伪来证明软件的正确性。

1-2『测试只能展示 Bug 的存在，并不能证明不存在 Bug，做一张金句卡，其展开的细节放在这里。（2020-12-24）』

注意，这种证伪过程只能应用于可证明的程序上。某段程序如果是不可证明的，例如，其中采用了不加限制的 goto 语句，那么无论我们为它写多少测试，也不能够证明其正确性。结构化编程范式促使我们先将一段程序递归降解为一系列可证明的小函数，然后再编写相关的测试来试图证明这些函数是错误的。如果这些测试无法证伪这些函数，那么我们就可以认为这些函数是足够正确的，进而推导整个程序是正确的。

### 0104. 主题卡 —— 分离控制和逻辑

信息源自推荐序：

耗子叔观点：无论是微观世界的代码，还是宏观层面的架构，无论是三种程范式还是微服务架构，它们都在解决一个问题 一一 分离控制和逻辑。所谓控制就是对程序流转的与业务逻辑无关的代码或系统的控制（如多线程、异步、服务发现、部署、弹性伸缩等），所调逻辑则是实实在在的业务逻辑，是解决用户问题逻辑。控制和逻辑构成了整体的件复杂度，有效地分离控制和逻辑会让你的系统得到最大的简化。

2『分离控制和逻辑，做一张主题卡片。（2021-02-19）』—— 已完成

问题：如果你要成为一名架构师，你需要明确地区分几组词语（如何区分它们正是留给你的问题），否则你不可能成为一名合格的工程师或架构师。这几组词语是简单 VS 简陋、平衡 VS 妥协、迭代 VS 半成品。如果你不能很清楚地定义出其中的区別，那么你将很难做出正确的决定，也就不可能成为优秀的工程师或架构师。

我相信这个观点和这组问题将有助于你更好地读并理解这本书，也会让你进行更多的思考，带着思考读这本书，会让你学到更多。

### 0105. 主题卡 —— 面向接口编程的 4 大编码规则

信息源自「2020112Clean-Architecture1101.md」

Every change to an abstract interface corresponds to a change to its concrete implementations. Conversely, changes to concrete implementations do not always, or even usually, require changes to the interfaces that they implement. Therefore interfaces are less volatile than implementations.

1-2『第一次通透的明白，接口比实现更稳定，自例证做一张金句卡片。（2021-05-12）』—— 已完成

Indeed, good software designers and architects work hard to reduce the volatility of interfaces. They try to find ways to add functionality to implementations without making changes to the interfaces. This is Software Design 101.

The implication, then, is that stable software architectures are those that avoid depending on volatile concretions, and that favor the use of stable abstract interfaces. This implication boils down to a set of very specific coding practices:

2『面向接口编程的 4 大编码规则，做一张主题卡片。（2021-05-12）』—— 已完成

1 Don't refer to volatile concrete classes. Refer to abstract interfaces instead. This rule applies in all languages, whether statically or dynamically typed. It also puts severe constraints on the creation of objects and generally enforces the use of Abstract Factories.

2 Don't derive from volatile concrete classes. This is a corollary to the previous rule, but it bears special mention. In statically typed languages, inheritance is the strongest, and most rigid, of all the source code relationships; consequently, it should be used with great care. In dynamically typed languages, inheritance is less of a problem, but it is still a dependency — and caution is always the wisest choice.

3 Don't override concrete functions. Concrete functions often require source code dependencies. When you override those functions, you do not eliminate those dependencies — indeed, you inherit them. To manage those dependencies, you should make the function abstract and create multiple implementations.

4 Never mention the name of anything concrete and volatile. This is really just a restatement of the principle itself.

稳定的抽象层

我们每次修改抽象接口的时候，一定也会去修改对应的具体实现。但反过来，当我们修改具体实现时，却很少需要去修改相应的抽象接口。所以我们可以认为接口比实现更稳定。

的确，优秀的软件设计师和架构师会花费很大精力来设计接，以减少未来对其进行改动。毕竟争取在不修改接口的情况下为软件增加新的功能是软件设计的基础常识。也就是说，如果想要在软件架设计上追求稳定，就必须多使用稳定的抽象接口，少依赖多变的具体实现。下面，我们将该设计原则归结为以下几条具体的编码守则：

1、应在代码中多使用抽象接口，尽量避免使用那些多变的具体实现类。这条守则适用于所有编程语言，无论静态类型语言还是动态类型语言。同时，对象的创建过程也应该受到严格限制，对此，我们通常会选择用抽象工厂（abstract factory）这个设计模式。

2、不要在具体实现类上创建衍生类。上一条守则虽然也隐含了这层意思，但它还是值得被单独拿出来做一次详细声明。在静态类型的编程语言中，继承关系是所有一切源代码依赖关系中最强的、最难被修改的，所以我们对继承的使用应该格外小心。即使是在稍微便于修改的动态类型语言中，这条守则也应该被认真考虑。

3、不要覆盖（override）包含具体实现的函数。调用包含具体实现的函数通常就意味着引入了源代码级别的依赖。即使覆盖了这些函数，我们也无法消除这其中的依赖 一一 这些函数继承了那些依赖关系。在这里，控制依赖关系的唯一办法，就是创建一个抽象函数，然后再为该函数提供多种具体实现。

1-2『

只要使用引入「具体」函数，即调用「具体」函数，相当于依赖具体函数了。但是：不可能不引入具体函数啊，是不是应该只在具体函数里引入具体函数，此操作仅仅在「实现类」这个圈圈里操作。待确认。（2021-05-12）

补充：下面有一些信息部分回答了这个疑问。

The concrete component in Figure 11.1 contains a single dependency, so it violates the DIP. This is typical. DIP violations cannot be entirely removed, but they can be gathered into a small number of concrete components and kept separate from the rest of the system.

在图 11.1 中，具体实现组件的内部仅有一条依赖关系，这条关系其实是违反 DIP 的。这种情況很常见，我们在软件系统中并不可能完全消除违反 DIP 的情況。通常只需要把它们集中于少部分的具体实现组件中，将其与系统的其他部分隔离即可。（2021-05-12）

』—— 未完成

4、应避免在代码中写入与任何具体实现相关的名字，或者是其他容易变动的事物的名字。这基本上是 DIP 原则的另外一个表达方式。

### 0106. 主题卡 —— 软件架构的黄金曲线

信息源自「2020112Clean-Architecture1101.md」

To comply with these rules, the creation of volatile concrete objects requires special handling. This caution is warranted because, in virtually all languages, the creation of an object requires a source code dependency on the concrete definition of that object.

In most object-oriented languages, such as Java, we would use an Abstract Factory to manage this undesirable dependency.

The diagram in Figure 11.1 shows the structure. The Application uses the ConcreteImpl through the Service interface. However, the Application must somehow create instances of the ConcreteImpl. To achieve this without creating a source code dependency on the ConcreteImpl, the Application calls the makeSvc method of the ServiceFactory interface. This method is implemented by the ServiceFactoryImpl class, which derives from ServiceFactory. That implementation instantiates the ConcreteImpl and returns it as a Service.

Figure 11.1  Use of the Abstract Factory pattern to manage the dependency

1-2『上面的信息太宝贵了，图 11.1 也太 NB 了，感觉又挖到金子了。架构中抽象层和具体实现层之间是有一条曲线的，所有跨越这条曲线的依赖关系都应该是单向的，空心箭头从具体实现层指向抽象层，即具体实现层依赖抽象层。软件架构的黄金曲线，做一张主题卡片。（2021-05-12）』—— 已完成

The curved line in Figure 11.1 is an architectural boundary. It separates the abstract from the concrete. All source code dependencies cross that curved line pointing in the same direction, toward the abstract side.

The curved line divides the system into two components: one abstract and the other concrete. The abstract component contains all the high-level business rules of the application. The concrete component contains all the implementation details that those business rules manipulate.

Note that the flow of control crosses the curved line in the opposite direction of the source code dependencies. The source code dependencies are inverted against the flow of control — which is why we refer to this principle as Dependency Inversion.

工厂模式

如果想要遵守上述编码守则，我们就必须要对那些易变对象的创建过程做一些特殊处理，这样的谨慎是很有必要的，因为基本在所有的编程语言中，创建对象的操作都免不了需要在源代码层次上依赖对象的具体实现。

在大部分面向对象编程语言中，人们都会选择用抽象工厂模式来解決这个源代码依赖的问题。

下面，我们通过图 11.1 来描述一下该设计模式的结构。如你所见，Application 类是通过 Service 接口来使用 ConcreteImpl 类的。然而，Application 类还是必须要构造 ConcreteImpl 类实例。于是，为了避免在源代码层次上引入对 ConcreteImpl 类具体实现的依赖，我们现在让 Application 类去调用 Service 接口的 makeSvc 方法。这个方法就由 ServiceFactoryImpl 类来具体提供，它是 ServiceFactory 的一个衍生类。该方法的具体实现就是初始化一个 Concretelmpl 类的实例，并且将其以 Service 类型返回。

图 11.1 中间的那条曲线代表了软件架构中的抽象层与具体实现层的边界。在这里，所有跨越这条边界源代码级别的依赖关系都应该是单向的，即具体实现层依赖抽象层。

这条曲线将整个系统划分为两部分组件：抽象接口与其具体实现。抽象接口组件中包含了应用的所有高阶业务规则，而具体实现组件中则包括了所有这些业务规则所需要做的具体操作及其相关的细节信息。请注意，这里的控制流跨越架边界的方向与源代码依赖关系跨越该边界的方向正好相反，源代码依赖方向永远是控制流方向的反转 一一 这就是 DIP 被称为依赖反转原则的原因。

2『源代码依赖方向永远是控制流方向的反转，做一张金句卡片。（2021-05-12）』

### 0107. 主题卡 —— 一觉醒来综合征的两个解决方案

信息源自「2020112Clean-Architecture1401.md」

Allow no cycles in the component dependency graph.

Have you ever worked all day, gotten some stuff working, and then gone home, only to arrive the next morning to find that your stuff no longer works? Why doesn't it work? Because somebody stayed later than you and changed something you depend on! I call this「the morning after syndrome.」

The「morning after syndrome」occurs in development environments where many developers are modifying the same source files. In relatively small projects with just a few developers, it isn't too big a problem. But as the size of the project and the development team grow, the mornings after can get pretty nightmarish. It is not uncommon for weeks to go by without the team being able to build a stable version of the project. Instead, everyone keeps on changing and changing their code trying to make it work with the last changes that someone else made.

Over the last several decades, two solutions to this problem have evolved, both of which came from the telecommunications industry. The first is「the weekly build,」and the second is the Acyclic Dependencies Principle (ADP).

2『一觉醒来综合征的两个解决方案，做一张主题卡片。（2021-5-13）』—— 已完成

无依赖环原则

组件依赖关系图中不应该出现环。

我们一定都有过这样的经历：当你花了一整天的时间，好不容易搞定了一段代码，第二天上班时却发现这段代码莫名其妙地又不能工作了。这通常是因为有人在你走后修改了你所依赖的某个组件。我给这种情况起了个名字 ——「一觉醒来综合征」。

这种综合征的主要病因是多个程序员同时修改了同一个源代码文件。虽然在规模相对较小、人员较少的项目中，这种问题或许并不严重，但是随着项目的增长，研发人员的增加，这种每天早上刚上班时都要经历一遍的痛苦就会越来越多。甚至会严重到让有的团队在长达数周的时间内都不能发布一个稳定的项目版本，因为每个人都在不停地修改自己的代码，以适应其他人所提交的变更。

在过去几十年中，针对这个问题逐渐演化出了两种解决方案，它们都来自电信行业。第一种是「每周构建」，第二种是「无依赖环原则」（ADP）。

### 0108. 主题卡 —— 多个组件依赖闭环形成大组件难改的原因

信息源自「2020112Clean-Architecture1401.md」

But this is just part of the trouble. Consider what happens when we want to test the Entities component. To our chagrin, we find that we must build and integrate with Authorizer and Interactors. This level of coupling between components is troubling, if not intolerable.

You may have wondered why you have to include so many different libraries, and so much of everybody else's stuff, just to run a simple unit test of one of your classes. If you investigate the matter a bit, you will probably discover that there are cycles in the dependency graph. Such cycles make it very difficult to isolate components. Unit testing and releasing become very difficult and error prone. In addition, build issues grow geometrically with the number of modules.

1-2『这里的信息太受启发了，为啥形成依赖闭合的多个组件难改？形成闭合意味着这几个组件可以作为一个「整体」，作为一个整体的话，每次就得同步、同版本。多个组件依赖闭环形成大组件难改的原因，做一张主题主题卡片。（2021-05-14）』—— 已完成

Moreover, when there are cycles in the dependency graph, it can be very difficult to work out the order in which you must build the components. Indeed, there probably is no correct order. This can lead to some very nasty problems in languages like Java that read their declarations from compiled binary files.

循环依赖在组件依赖图中的影响

假设某个新需求使我们修改了 Entities 组件中的某个类，而这个类又依赖于 Authorizer 组件中的某个类。例如，Entities 组件中的 User 类使用了 Authorizer 组件中的 Permissions 类。这就形成了一个循环依赖关系，如图 14.2 所示。

图 14.2：循环依赖

这种循环依赖立刻就会给我们的项目带来麻烦。例如，当 Database 组件的程序员需要发布新版本时，他们需要与 Entities 组件进行集成。但现在由于出现了循环依赖，Database 组件就必须也要与 Authorizer 组件兼容，而 Authorizer 组件又依赖于 Interactors 组件。这样一来，Database 组件的发布就会变得非常困难。在这里，Entities、Authorizer 及 Interactors 这三个组件事实上被合并成了一个更大的组件。这些组件的程序员现在会互相形成干扰，因为他们在开发中都必须使用完全相同的组件版本。

这还只是问题的冰山一角，请想象一下我们在测试 Entities 组件时会发生什么？情况会让人触目惊心，我们会发现自己必须将 Authorizer 和 Interactors 集成到一起测试。即使这不是不能容忍的事，但至少这些组件之间的耦合度也是非常令人不安的。

很显然，这样一个小小的测试必须要依赖大量的库就是因为其组件结构依赖图中存在的这个循环依赖。这种循环依赖会使得组件的独立维护工作变得十分困难。不仅如此，单元测试和发布流程也都会变得非常困难，并且很容易出错。此外，项目在构建中出现的问题会随着组件数量的增多而呈现出几何级数的增长。

所以，当组件结构依赖图中存在循环依赖时，想要按正确的顺序构建组件几乎是不可能的。这种依赖关系将会在 Java 这种需要在编译好的二级制文件中读取声明信息的语言中导致一些非常棘手的问题。

### 0201. 术语卡 —— 编程范式

Another, probably more significant, revolution was in programming paradigms. Paradigms are ways of programming, relatively unrelated to languages. A paradigm tells you which programming structures to use, and when to use them. To date, there have been three such paradigms. For reasons we shall discuss later, there are unlikely to be any others.

1-2『编程范式，ways of programming，其与使用什么编程语言没啥关系的，编程范式做一张术语卡片。』—— 已完成

除此之外，计算机编程领域还经历了另外一个更巨大、更重要的变革，那就是编程范式（paradigm）的变迁。编程范式指的是程序的编写模式，与具体的编程语言关系相对较小。这些范式会告诉你应该在什么时候采用什么样的代码结构。直到今天，我们也一共只有三个编程范式，而且未来几乎不可能再出现新的。

### 0202. 术语卡 —— 依赖倒置

信息源自「2020112Clean-Architecture0501.md」

Imagine what software was like before a safe and convenient mechanism for polymorphism was available. In the typical calling tree, main functions called high-level functions, which called mid-level functions, which called low-level functions. In that calling tree, however, source code dependencies inexorably followed the flow of control (Figure 5.1).

Figure 5.1  Source code dependencies versus flow of control

For main to call one of the high-level functions, it had to mention the name of the module that contained that function. In C, this was a `#include`. In Java, it was an `import` statement. In C#, it was a `using` statement. Indeed, every caller was forced to mention the name of the module that contained the callee.

This requirement presented the software architect with few, if any, options. The flow of control was dictated by the behavior of the system, and the source code dependencies were dictated by that flow of control.

When polymorphism is brought into play, however, something very different can happen (Figure 5.2).

Figure 5.2  Dependency inversion

In Figure 5.2, module HL1 calls the F() function in module ML1. The fact that it calls this function through an interface is a source code contrivance. At runtime, the interface doesn't exist. HL1 simply calls F() within ML1. [7]

Note, however, that the source code dependency (the inheritance relationship) between ML1 and the interface I points in the opposite direction compared to the flow of control. This is called dependency inversion, and its implications for the software architect are profound.

The fact that OO languages provide safe and convenient polymorphism means that any source code dependency, no matter where it is, can be inverted.

Now look back at that calling tree in Figure 5.1, and its many source code dependencies. Any of those source code dependencies can be turned around by inserting an interface between them.

With this approach, software architects working in systems written in OO languages have absolute control over the direction of all source code dependencies in the system. They are not constrained to align those dependencies with the flow of control. No matter which module does the calling and which module is called, the software architect can point the source code dependency in either direction.

That is power! That is the power that OO provides. That's what OO is really all about — at least from the architect's point of view.

What can you do with that power? As an example, you can rearrange the source code dependencies of your system so that the database and the user interface (UI) depend on the business rules (Figure 5.3), rather than the other way around.

Figure 5.3  The database and the user interface depend on the business rules

This means that the UI and the database can be plugins to the business rules. It means that the source code of the business rules never mentions the UI or the database.

As a consequence, the business rules, the UI, and the database can be compiled into three separate components or deployment units (e.g., jar files, DLLs, or Gem files) that have the same dependencies as the source code. The component containing the business rules will not depend on the components containing the UI and database.

In turn, the business rules can be deployed independently of the UI and the database. Changes to the UI or the database need not have any effect on the business rules. Those components can be deployed separately and independently.

In short, when the source code in a component changes, only that component needs to be redeployed. This is independent deployability.

If the modules in your system can be deployed independently, then they can be developed independently by different teams. That's independent developability.

7 Albeit indirectly.

1-2『

依赖倒置的核心是通过增加一个「接口」实现依赖的反转，这样的话任何「控制流」的流向都可以通过实际情况来调整。目前不明白的是，加「接口」跟「面向对象」编程范式有啥必要的联系，加接口就一定属于面向对象？这节的信息，让自己对依赖倒置有了一个更深的印象。回复：前面的疑虑，关键点应该在「多态」上，继承是从子类的角度往上看父类，多态是从父类的角度往下看子类。依赖倒置做一张术语卡片。（2020-12-25）

补充：

感觉渐渐拨开迷雾了。首先，A 依赖于 B，那么 A 就是 B 的「插件」，随插随用。要让数据库模块和交互界面模块依赖于业务模块，那么前两者可以作为业务模块的插件。A 依赖于 B，即要 import 引用 B，对应于第 5 章中图 5.1 里，Main 函数是 A，下面其调用的 HL1 函数是 B，HL1 函数可能是其他模块里的功能函数，要引用进来的。A 类继承于 B 类，说明 A 依赖于 B。

其次，文中依赖倒置的核心是通过增加一个「接口」，此接口就是耗子哥专栏里提到的「中间层」。此时此刻再看图 5.1 和图 5.2 就很有感觉了。图 5.1 中抽象模块控制具体模块，同时抽象模块也依赖于具体模块，控制流和依赖流都是从抽象到具体，同向的。图 5.2 中通过在抽象模块和具体模块之间添加一个接口，原来抽象模块直接调用具体模块的功能函数，现在抽象模块调用「接口」里的功能函数，具体模块继承于接口，实现那个功能函数。变成了：抽象模块依赖于接口，具体模块也依赖于接口。原来抽象模块依赖于低级的具体模块，现在具体模块依赖于接口，接口是比具体模块更「抽象」的，所以所依赖倒置了。

那么整个过程中。「接口」至关重要，而接口又对应于面向对象编程范式，对应于多态。这算稍微解决了之前的疑惑：依赖倒置跟面向对象编程范式有啥必要的联系。（2021-05-10）

』—— 已完成

我们可以想象一下在安全和便利的多态支持出现之前，软件是什么样子的。下面有一个典型的调用树的例子，main 函数调用了一些高层函数，这些高层函数又调用了一些中层函数，这些中层函数又继续调用了一些底层函数。在这里，源代码层面的依赖不可避免地要跟随程序的控制流（详见图 5.1）。

如你所见，main 函数为了调用高层函数，它就必须能够看到这个函数所在的模块。在 C 中，我们会通过 #include 来实现，在 Java 中则通过 import 来实现，而在 C# 中则用的是 using 语句。总之，每个函数的调用方都必须要引用被调用方所在的模块。显然，这样做就导致了我们在软件架构上别无选择。在这里，系统行为决定了控制流，而控制流则决定了源代码依赖关系。但一旦我们使用了多态，情况就不一样了（详见图 5.2）。

在图 5.2 中，模块 HL1 调用了 ML1 模块中的 F() 函数，这里的调用是通过源代码级别的接口来实现的。当然在程序实际运行时，接口这个概念是不存在的，HL1 会调用 ML1 中的 F() 函数。请注意模块 ML1 和接口在源代码上的依赖关系（或者叫继承关系），该关系的方向和控制流正好是相反的，我们称之为依赖反转。这种反转对软件架构设计的影响是非常大的。事实上，通过利用面向编程语言所提供的这种安全便利的多态实现，无论我们面对怎样的源代码级别的依赖关系，都可以将其反转。现在，我们可以再回头来看图 5.1 中的调用树，就会发现其中的众多源代码依赖关系都可以通过引入接口的方式来进行反转。

通过这种方法，软件架构师可以完全控制采用了面向对象这种编程方式的系统中所有的源代码依赖关系，而不再受到系统控制流的限制。不管哪个模块调用或者被调用，软件架构师都可以随意更改源代码依赖关系。这就是面向对象编程的好处，同时也是面向对象编程这种范式的核心本质 —— 至少对一个软件架构师来说是这样的。

这种能力有什么用呢？在下面的例子中，我们可以用它来让数据库模块和用户界面模块都依赖于业务逻辑模块（见图 5.3），而非相反。这意味着我们让用户界面和数据库都成为业务逻辑的插件。也就是说，业务逻辑模块的源代码不要引入用户界面和数据库这两个模块。

这样一来，业务逻辑、用户界面以及数据库就可以被编译成三个独立的组件或者部暑单元（例如 jar 文件、DLL 文件、Gem 文件等）了，这些组件或者部署单元的依赖关系与源代码的依赖关系是一致的，业务逻辑组件也不会依赖于用户界面和数据库这两个组件。于是，业务逻辑组件就可以独立于用户界面和数据库来进行部署了，我们对用户界面或者数据库的修改将不会对业务逻辑产生任何影响，这些组件都可以被分别、独立地部署。简单来说，当某个组件的源代码需要修改时，仅仅需要重新部署该组件，不需要更改其他组件，这就是独立部署能力。如果系统中的所有组件都可以独立部暑，那它们就可以由不同的团队并行开发，这就是所谓的独立开发能力。

### 0203. 术语卡 —— 事件溯源

The limits of storage and processing power have been rapidly receding from view. Nowadays it is common for processors to execute billions of instructions per second and to have billions of bytes of RAM. The more memory we have, and the faster our machines are, the less we need mutable state.

As a simple example, imagine a banking application that maintains the account balances of its customers. It mutates those balances when deposit and withdrawal transactions are executed. Now imagine that instead of storing the account balances, we store only the transactions. Whenever anyone wants to know the balance of an account, we simply add up all the transactions for that account, from the beginning of time. This scheme requires no mutable variables.

Obviously, this approach sounds absurd. Over time, the number of transactions would grow without bound, and the processing power required to compute the totals would become intolerable. To make this scheme work forever, we would need infinite storage and infinite processing power. But perhaps we don't have to make the scheme work forever. And perhaps we have enough storage and enough processing power to make the scheme work for the reasonable lifetime of the application.

This is the idea behind event sourcing. 2 Event sourcing is a strategy wherein we store the transactions, but not the state. When state is required, we simply apply all the transactions from the beginning of time. Of course, we can take shortcuts. For example, we can compute and save the state every midnight. Then, when the state information is required, we need compute only the transactions since midnight.

2『时间溯源，做一张术语卡片。』—— 已完成

Now consider the data storage required for this scheme: We would need a lot of it. Realistically, offline data storage has been growing so fast that we now consider trillions of bytes to be small — so we have a lot of it.

More importantly, nothing ever gets deleted or updated from such a data store. As a consequence, our applications are not CRUD; they are just CR. Also, because neither updates nor deletions occur in the data store, there cannot be any concurrent update issues.

If we have enough storage and enough processor power, we can make our applications entirely immutable — and, therefore, entirely functional. If this still sounds absurd, it might help if you remembered that this is precisely the way your source code control system works.

随着存储和处理能力的大幅进步，现在拥有每秒可以执行数十亿条指令的处理器，以及数十亿字节内存的计算机已经很常见了。而内存越大，处理速度越快，我们对可变状态的依赖就会越少。

举个简单的例子，假设某个银行应用程序需要维护客户账户余额信息，当它执行存取款事务时，就要同时负责修改余额记录。如果我们不保存具体账户余额，仅仅保存事务日志，那么当有人想查询账户余额时，我们就将全部交易记录取出，并且每次都得从最开始到当下进行累计。当然，这样的设计就不需要维护任何可变变量了。

但显而易见，这种实现是有些不合理的。因为随着时间的推移，事务的数目会无限制增长，每次处理总额所需要的处理能力很快就会变得不能接受。如果想使这种设计永远可行的话，我们将需要无限容量的存储，以及无限的处理能力。但是可能我们并不需要这个设计永远可行，而且可能在整个程序的生命周期内，我们有足够的存储和处理能力来满足它。

这就是事件溯源，在这种体系下，我们只存储事务记录，不存储具体状态。当需要具体状态时，我们只要从头开始计算所有的事务即可。在存储方面，这种架构的确要很大的存储容量。如今离线数据存储器的增长是非常快的，现在 1TB 对我们来说也已经不算什么了。更重要的是，这种数据存储模式中不存在删除和更新的情况，我们的应用程序不是 CRUD，而是 CR。因为更新和删除这两种操作都不存在了，自然也就不存在并发问题。

如果我们有足够大的存储量和处理能力，应用程序就可以用完全不可变的、纯函数式的方式来编程。如果读者还是觉得这听起来不太靠谱，可以想想我们现在用的源代码管理程序，它们正是用这种方式工作的！

### 0301. 人名卡 —— Bob 大叔

Robert C. Martin (-)。

印象：

例证：

Robert C. Martin (Uncle Bob) has been a programmer since 1970. He is the co-founder of cleancoders.com, which offers online video training for software developers, and is the founder of Uncle Bob Consulting LLC, which offers software consulting, training, and skill development services to major corporations worldwide. He served as the Master Craftsman at 8th Light, Inc., a Chicago-based software consulting firm. He has published dozens of articles in various trade journals and is a regular speaker at international conferences and trade shows. He served three years as the editor-in-chief of the C++ Report and served as the first chairman of the Agile Alliance.

Martin has authored and edited many books, including The Clean Coder, Clean Code, UML for Java Programmers, Agile Software Development, Extreme Programming in Practice, More C++ Gems, Pattern Languages of  Program Design 3, and Designing Object Oriented C++ Applications Using the Booch Method.

2『 Bob 大叔做一张人名卡片。』—— 已完成

### 0401. 金句卡 —— 测试只能展示 Bug 的存在，并不能证明不存在 Bug

### 0402. 金句卡 —— interfaces are less volatile than implementations

信息源自「2020112Clean-Architecture1101.md」

Every change to an abstract interface corresponds to a change to its concrete implementations. Conversely, changes to concrete implementations do not always, or even usually, require changes to the interfaces that they implement. Therefore interfaces are less volatile than implementations.

1-2『第一次通透的明白，接口比实现更稳定，此例证做一张金句卡片。（2021-05-12）』—— 已完成

我们每次修改抽象接口的时候，一定也会去修改对应的具体实现。但反过来，当我们修改具体实现时，却很少需要去修改相应的抽象接口。所以我们可以认为接口比实现更稳定。

### 0403. 金句卡 —— 源代码依赖方向永远是控制流方向的反转

信息源自「2020112Clean-Architecture1101.md」

Note that the flow of control crosses the curved line in the opposite direction of the source code dependencies. The source code dependencies are inverted against the flow of control — which is why we refer to this principle as Dependency Inversion.

这条曲线将整个系统划分为两部分组件：抽象接口与其具体实现。抽象接口组件中包含了应用的所有高阶业务规则，而具体实现组件中则包括了所有这些业务规则所需要做的具体操作及其相关的细节信息。请注意，这里的控制流跨越架边界的方向与源代码依赖关系跨越该边界的方向正好相反，源代码依赖方向永远是控制流方向的反转 一一 这就是 DIP 被称为依赖反转原则的原因。

2『源代码依赖方向永远是控制流方向的反转，做一张金句卡片。（2021-05-12）』

### 0501. 任意卡 —— 单一职责原则 SRP 定义的演化

提炼：

A module should be responsible to one, and only one, actor.

信息源自「0701 SRP: The Single Responsibility Principle」

Of all the SOLID principles, the Single Responsibility Principle (SRP) might be the least well understood. That's likely because it has a particularly inappropriate name. It is too easy for programmers to hear the name and then assume that it means that every module should do just one thing.

Make no mistake, there is a principle like that. A function should do one, and only one, thing. We use that principle when we are refactoring large functions into smaller functions; we use it at the lowest levels. But it is not one of the SOLID principles — it is not the SRP.

Historically, the SRP has been described this way:

A module should have one, and only one, reason to change.

Software systems are changed to satisfy users and stakeholders; those users and stakeholders are the「reason to change」that the principle is talking about. Indeed, we can rephrase the principle to say this:

A module should be responsible to one, and only one, user or stakeholder.

Unfortunately, the words「user」and「stakeholder」aren't really the right words to use here. There will likely be more than one user or stakeholder who wants the system changed in the same way. Instead, we're really referring to a group — one or more people who require that change. We'll refer to that group as an actor. Thus the final version of the SRP is:

A module should be responsible to one, and only one, actor.

Now, what do we mean by the word「module」? The simplest definition is just a source file. Most of the time that definition works fine. Some languages and development environments, though, don't use source files to contain their code. In those cases a module is just a cohesive set of functions and data structures.

2『 SRP 定义的演化，做一张任意卡片。』—— 已完成

That word「cohesive」implies the SRP. Cohesion is the force that binds together the code responsible to a single actor. Perhaps the best way to understand this principle is by looking at the symptoms of violating it.

SRP 是 SOLID 五大设计原则中最容易被误解的一个。也许是名字的原因，很多程序员根据 SRP 这个名字想当然地认为这个原则就是指：每个模块都应该只做一件事。没错，后者的确也是一个设计原则，即确保一个函数只完成一个功能。我们在将大型函数重构成小函数时经常会用到这个原则，但这只是一个面向底层实现细节的设计原则，并不是 SRP 的全部。在历史上，我们曾经这样描述 SRP 这一设计原则：任何一个软件模块都应该有且仅有一个被修改的原因。

在现实环境中，软件系统为了满足用户和所有者的要求，必然要经常做出这样那样的修改。而该系统的用户或者所有者就是该设计原则中所指的「被修改的原因」。所以，我们也可以这样描述 SRP：任何一个软件模块都应该只对一个用户（User）或系统利益相关者（Stakeholder）负责。

不过，这里的「用户」和「系统利益相关者」在用词上也并不完全准确，它们很有可能指的是一个或多个用户和利益相关者，只要这些人希望对系统进行的变更是相似的，就可以归为一类个或多个有共同需求的人。在这里，我们将其称为行为者（actor）。所以，对于 SRP 的最终描述就变成了：任何一个软件模块都应该只对某一类行为者负责。

那么，上文中提到的「软件模块」究竟又是在指什么呢？大部分情況下，其最简单的定义就是指一个源代码文件。然而，有些编程语言和编程环境并不是用源代码文件来存储程序的。在这些情況下，「软件模块」指的就是一组紧密相关的函数和数据结构。在这里，「相关」这个词实际上就隐含了 SRP 这一原则。代码与数据就是靠着与某一类行为者的相关性被组合在一起的。或许，理解这个设计原则最好的办法就是让大家来看一些反面案例。

## 内容简介

《架构整洁之道》是创造「Cean 神话」的 Bob 大叔在架构领域的登峰之作，围绕「架构整洁」这一重要导向，系统地剖析其缘起、内涵及应用场景，涵盖软件研发完整过程及所有核心架构模式。本书分为 6 部分，第 1 部分纲领性地提出软件架构设计的终极目标，描述软件架构设计的重点与模式；第 2-4 部分从软件开发中三个基础编程范式的定义和特征出发，进一步描述函数、组件、服务设计与实现的定律，以及它们是如何有效构建软件系统的整体架构的；第 5 部分从整洁架构的定义开始，详细阐述软件架构设计过程中涉及的方方面面，包括划分内部组件边界、应用常见设计模式、避开错误、降低成本、处理特殊情況等，并以实战案例将内容有机整合起来；第 6 部分讲述具体实现细节；附录则透过作者数十年的软件从业经历再次印证本书的观点。

对于每一位软件研发从业人员一无论从事的是具体编码实现、架构设计，还是软件研发管理，本书都是不可或缺的。

## 推荐序一

在我心里，程序员可以分为三个层次：普通程序员、工程师和架构师。

普通程序员是编写代码的人。编写代码的方式有很多，只要能让程序跑起来，能正确地处理业务流程和对数据进行计算，就可以说「会编写代码」。程序员需要熟悉整个程序的逻辑及处理过程，需要熟悉程序语言的特性，还需要熟悉一些计算机操作系统的交互调用方式，才能写出从用户侧交互，到数据和业务逻辑处理，再到与计算机系统交互的代码，有效地把用户信息、数据、业务和计算机串联和拼装出来。

然而，其中一些程序员发现，只让代码跑起来是不够的，因为这个世界是不断变化的，他们发现自己需要花更多的时间来维护代码：增加新的需求，扩展原有的流程，修改已有的功能，优化性能......一个人完全维护不过来，还需要更多的人，于是代码还需要在不同人之间轮转；他们发现代码除了需要跑起来，还需要易读、易扩展、易维护，甚至可以直接重用。于是，这些人使用各种各样的手段和技术不断提高代码的易读性、可扩展性、可维护性和重用性。我们把这些有「洁癖」、有工匠精精、有修养的程序员叫作工程师，工程师不仅仅是在编写代码，他们会用工程的方法来编写代码，以便让编程开发更为高效和快速。他们把編程当成一种设计，一种工业设计，把代码模块化，让这些模块可以更容易地交互拼装和组织，让代码排列整齐一阅读和维护这些代码就像看阅兵式一样舒心畅快。

但是故事还没完，这些拥有工匠精神的工程师们还是难以解决某些题，这些人渐地发现，这个世界上有很多问题就像翘翘板一样，只能要一边，这一边上去了，另一边就下来了。就像要么用空间换时间，要么用时间换空间一样，你很难找到同时满足空间和时间要求的「双利解」；就像 CAP 的三选二的理论一样，这个世界不存在完美的解決方案，无论什么方案都有好的一面和不好的一面。而且，这些工程师还渐发现，每当引入一个新的技术来解決一个已有的问题时，这个新的技术就会带来更多的问题，问题就像有一个生命体一样，它们会不断地繁殖和进化。渐渐地，他们发现，问题的多少和系统的复杂度呈正比，而且不仅是线性正比，还可能呈级数正比，此时就越来越难做技术決定。但是有一些资深的工程师开始站出来挑战这些问题，有的基于业务分析给出平衡的方案，有的开始尝试设计更高级的技术，有的开始设计更灵活的系统，有的则开始简化和轻量化整个系统，这些高智商、经验足、不怕难的工程师们引领着整个行业前行。他们就是架构师！

感觉 Bob 大叔的系列著作好像也在走这个过程，《代码整洁之道》教你写出易读、可扩展、可维护、可重用的代码，《代码整洁之道：程序员的职业素养》教你怎样变成一个有修养的程序员，而《架构整洁之道》基本上是在描述软件设计的一些理论知识。《架构整洁之道》大体分成三个部分：编程范式（结构化编程、面向对象编程和函数式编程），设计原则（主要是 SOLD），以及软件架构（其中讲了很多高屋建翎的内容）。总体来说，这本书中的内容可以让你从微观（代码层面）和宏观（架构层面）两个层面对整个软件设计有一个全面的了解。

但是，如果你想从这本书里找到一些可以立马解决具体问题的工程架构和技术，恐怕你会感到失望。这本书中更多的是一些基础的理论知识，看完后你可能会比较「无感」，因为这些基础知识对于生活在这个高速发展的喜欢快餐文化的社会中的人来说，可能很难理解其中的价值 一一 大多数人的目标不是设计出一个优质的软件或架构，而是快速地解決一个具体的问题，完成自己的工作。然而，可能只有你碰过足够多的壁，掉过足够多的坑，经历过足够多的痛苦后，再来读这本书时，你才会发现本书中的这些「陈旧的知识」是多么充满智慧。而且，如果有一天，你像我这个老家伙一样，看到今天很多很多公司和年轻的程序员还在不断地掉坑和挣扎，你就会明白这些知识的重要性了。

我个人觉得，这本书是架构方面的入门级读物，但也并不适合经验不足的人员学习，这本书更适合的读者群是，有 3-5 年编程经验、需要入门软件设计和架构的工程师或程序员。最后，我想留下一个观点和一组问题。

观点：无论是微观世界的代码，还是宏观层面的架构，无论是三种程范式还是微服务架构，它们都在解决一个问题 一一 分离控制和逻辑。所谓控制就是对程序流转的与业务逻辑无关的代码或系统的控制（如多线程、异步、服务发现、部署、弹性伸等），所谓逻辑则是实实在在的业务逻辑，是解决用户问题逻辑。控制和逻辑构成了整体的件复杂度，有效地分离控制和逻辑会让你的系统得到最大的简化。

2『分离控制和逻辑，做一张主题卡片。（2021-02-19）』—— 已完成

问题：如果你要成为一名架构师，你需要明确地区分几组词语（如何区分它们正是留给你的问题），否则你不可能成为一名合格的工程师或架构师。这几组词语是简单 VS 简陋、平衡 VS 妥协、迭代 VS 半成品。如果你不能很清楚地定义出其中的区別，那么你将很难做出正确的决定，也就不可能成为优秀的工程师或架构师。

我相信这个观点和这组问题将有助于你更好地读并理解这本书，也会让你进行更多的思考，带着思考读这本书，会让你学到更多。

—— 陈皓，左耳朵耗子

## 推荐序二 —— 久远的教诲，古老的智慧

如果让你接手一套不稳定但要紧的在线系统，这套系统还有各种问题：变量命名非常随意，依赖逻辑错综复杂，层次结构乱七八糟，部署流程一糊涂，监控系統一片空白。你该怎么办？

前几年我就遇到了这种问题，我对着频发的故障仔细观察，发现了最关键的问题：如果放着不动，这套系统的核心功能还是相对稳定的，但经常会有一些外围需求要开发，这时由于原有的依赖逻辑和层次结构不够清楚，就会导致「牵一发而动全身」的情況，加上測试不完善，所以几乎每次外围功能上线更新，核心功能都会受影响，然后又要重复好几次「调试 → 改正 → 上线」的流程。

怎么办？大家说了很多办法：把单元测试都补全，重构代码拆分核心功能和非核心功能，跟业务方谈暂停需求。这些办法都很对，但是，都需要时间才能见效，而我们最缺的就是时间。

我提了一个很「笨」的办法：把所有「共享变量」都抽到 Redist 中进行读写，消灭本地副本，然后把稳定版本程序多部署几份，这样就可以多启动几个实例，将这些实例标记为 AB 两组。同时，在前面搭建代理服务，用于分流请求 一一 核心功能请求分配到 A 组（程序基本不更新），外围功能请求分配到 B 组（程序按业务需求更新）。这样做看起来有点多此一举 —— AB 两组都只有部分代码提供服务，而且要通过 Redis 共享状态，但是却实现了无论 B 组的程序如何更新，都不会影响 A 组所承载的核心服务的目的。

虽然当时不少人说「怎么能这样玩呢」，但它确实有效。当天部署，当天生效，在线服务迅速稳定下来，即便新开发的外围功能有问题，核心服务也不受任何影响。这样业务人员满意了，开发人员也可以安心对系统倣改造了。

后来有不少人问我是怎么想到这个办法的，答案是：因为我是个老程序员，成长在面向对象的年代，运用 SOC（关注点分离）、SRP（单一职责原则）、OCP（开闭原则）这些东西对我来说就如同本能。具体到这个例子，无非就是识别关注点、隔离责任、保持核心关注点的封闭而已。

后来我才知道，我提出的这个方法有个专门的名字叫「蓝绿部署」。当然我自认是个老程序员，不懂这些新鲜概念也不太要紧。确实，如今不少程序员已经不认识 SOC、SRP、OCP、LSP 等「古老」的玩意了，大家熟悉的是各种语言、类库、框架、代码托管网站。互联网开发场景变万化，技术一日千里，而面向对象在不少人的脑海里早就是弃之不用的老古革了。只有「老一辈」的程序员还记得那些古老的教诲，守着那些古拙的技巧。但是这些东西，总有一天会被时代淘吗？

实际上，这也是我初读《架构整洁之道》的疑惑。虽然 Bob 大叔这个名字对我们这些「老程序员」来说可谓如雷贯耳，之前针对一般性软件开发所著的《代码整洁之道》和《代码整洁之道：程序员的职业素养》也确实很受欢迎，但如今写架构，还从结构化编程、面向对象编程、函数式编程写起，还花时间解释 SRP、OCP、LSP 等原则，实在难掩「古老」的感觉。请问，它们和如今的「架构」有什么关系吗？

不过，如果你耐心读下去就会发现，还真有关系。按照 Bob 大叔的说法，所谓架构就是「用最小的人力成本来满足构建和维护系统需求」的设计行为。以前的面向对象系统和如今的分布式系统，在这一点上是完全一致的。听取久远的教诲，尊重古老的智慧，如今的架构师也会从中受益。不信？我们就拿经典的三个编程范式来举例，看看这些「老掉牙」的玩意儿和如今的架构设计有什么关联。

大家对结构化编程的一般理解是，由 if-else、switch-case 之类的语句组织程序代码的编程方式，它杜绝了 goto 导致的混乱。但是从更深的层次上看，它也是一种设计范式，避免随意使用 goto，使用 if-else、switch-case 之类控制语句和函数、子函数组织起来的程序代码，可以保证程序的结构是清楚的，自顶向下层层细化，消灭了杂错，杜绝了混淆。

联系如今的分布式系统，我们在设计的时候，真的能够做到自顶向下层层细化吗？有多少次，我看到的系統设计图里，根本没有「层次」的概念，各个模块没有一致的层次划分，与子系統交互的不是子系统，而是一盘散沙式的接口，甚至接口之间随意互调、关系乱成一团麻的情况也时常出现，带来的就是维护和调试的噩梦。吹散历史的迷雾，不正是古老的 goto 陷阱的再现吗？

大家对面向对象编程的一般理解是，由封装、继承、多态三种特性支持的，包含类、接口等若干概念的编程方式。但是从更深的层次上看，它也是一种设计范式。多态大概算其中最神奇的特性了，程序员在确定接口时做好抽象，代码就可以很灵活，遇到新情況时，新写一个实现就可以无缝对接。联系如今的分布式系统，我们在设计的时候，真的能够做到接口足够抽象、新模块能无缝对接吗？有多少次，我看到接口的设计非常随意，接口不是基于行为而是基于特定场景的实现，没有做适当的抽象，也没有为未来预留空间，直接导致契约僵硬死板。每新増一种终端呈现形式，整个内容生产流程就要大动干，这样的例子并不罕见。抹去历史的尘埃，这不正是「多态」出现之前的困境吗？

大家对函数式编程的一般理解是，以函数为基本单元，没有变量（更准确地说是不能重复值）也没有副作用的编程方式。但是从更深的层次上看，它彻底隔离了可变性，变量或者状态默认就是不可变的，如果要变化，则必须经过合理设计的专门机制来实现。所以，它也避免了死锁、状态冲突等众多麻烦。

联系如今的分布式系统，我们在设计的时候，真的能够彻底隔离可变性、避免状态冲突吗？有多少次，我看到状态或变量的修改接口大方暴露，被不经意（或者恶意）修改，导致奇怪的故障。Bob 大叔举了ー个相当有趣的例子，如果又要保证操作原子性又要能精确还原各时刻的状态，有个办法是这样的：只提供 CR 操作，而不提供完整的 CRUD 操作（就像 MYSQL 的 binlog 那样）。平时只要追加操作记录即可，各时刻的状态永远通过重放之前的操作记录得出，这样就彻底避免了状态的错乱。这个办法看起来古怪，但我真的在之前的开发中用过（当然是在程序生命周期有限的场景下），而且真的从没出过错。

坦白说，看完《架构整洁之道》这本书，我心里好受点了。因为我发现，我们这些老程序员的知识其实没有过时，如今不少光鲜的架构其实要解决的还是那些古老的问题。多亏了 Bob 大叔的妙手点拨，我才能穿越时空，享受到「重新发现智慧」的愉悦。

当然，架构设计是一门复杂的学问，要综合考虑编码、质量、部署、发布、运维、排障、升级等等各种因素，做出权衡。好消息是，Bob 大叔的这本书覆盖面广，涉及各个方面，相信你认真读完全书定会和我一样有不小的收获。唯一的问题是，你要适应这个老程序员的口吻和节奏：他当然也会拿如今流行的打车系统做例子，但他更熟悉的还是链接器、C 语言、UML 图等玩意。

不过我觉得，这都不是大问题。看得出类之间的依赖关系不合理，自然容易发现子系统之间的依赖关系不合理；搞得懂 UNIX 如何巧妙定义通用的 IO 设备，自然容易想到对 PC Web、Mobile Web、App 内的页面做适当抽象；认得清各线程、进程、链接库的职责，自然容易明白微服务也需要避免跨边界调用。更妙的是，从这种古老的视角看问题，往往更能摆脱细节的困抗，把握问题的核心。就像老子说的那样：治大国如烹小鲜。

噢，对了，「治大国如烹小鲜」也是久远的教诲，也包含着古老的智慧。

—— 余晟公众号「余晟以为」，作者现在沪江教育集团担任平台架构部负责人

## Foreword

What do we talk about when we talk about architecture?

As with any metaphor, describing software through the lens of architecture can hide as much as it can reveal. It can both promise more than it can deliver and deliver more than it promises.

The obvious appeal of architecture is structure, and structure is something that dominates the paradigms and discussions of software development — components, classes, functions, modules, layers, and services, micro or macro. But the gross structure of so many software systems often defies either belief or understanding — Enterprise Soviet schemes destined for legacy, improbable Jenga towers reaching toward the cloud, archaeological layers buried in a big-ball-of-mud slide. It's not obvious that software structure obeys our intuition the way building structure does.

Buildings have an obvious physical structure, whether rooted in stone or concrete, whether arching high or sprawling wide, whether large or small, whether magnificent or mundane. Their structures have little choice but to respect the physics of gravity and their materials. On the other hand — except in its sense of seriousness — software has little time for gravity. And what is software made of? Unlike buildings, which may be made of bricks, concrete, wood, steel, and glass, software is made of software. Large software constructs are made from smaller software components, which are in turn made of smaller software components still, and so on. It's coding turtles all the way down.

When we talk about software architecture, software is recursive and fractal in nature, etched and sketched in code. Everything is details. Interlocking levels of detail also contribute to a building's architecture, but it doesn't make sense to talk about physical scale in software. Software has structure — many structures and many kinds of structures — but its variety eclipses the range of physical structure found in buildings. You can even argue quite convincingly that there is more design activity and focus in software than in building architecture — in this sense, it's not unreasonable to consider software architecture more architectural than building architecture!

But physical scale is something humans understand and look for in the world. Although appealing and visually obvious, the boxes on a PowerPoint diagram are not a software system's architecture. There's no doubt they represent a particular view of an architecture, but to mistake boxes for the big picture — for the architecture — is to miss the big picture and the architecture: Software architecture doesn't look like anything. A particular visualization is a choice, not a given. It is a choice founded on a further set of choices: what to include; what to exclude; what to emphasize by shape or color; what to de-emphasize through uniformity or omission. There is nothing natural or intrinsic about one view over another.

Although it might not make sense to talk about physics and physical scale in software architecture, we do appreciate and care about certain physical constraints. Processor speed and network bandwidth can deliver a harsh verdict on a system's performance. Memory and storage can limit the ambitions of any code base. Software may be such stuff as dreams are made on, but it runs in the physical world.

This is the monstrosity in love, lady, that the will is infinite, and the execution confined; that the desire is boundless, and the act a slave to limit. —— William Shakespeare

The physical world is where we and our companies and our economies live. This gives us another calibration we can understand software architecture by, other less physical forces and quantities through which we can talk and reason.

Architecture represents the significant design decisions that shape a system, where significant is measured by cost of  change. —— Grady Booch

Time, money, and effort give us a sense of scale to sort between the large and the small, to distinguish the architectural stuff from the rest. This measure also tells us how we can determine whether an architecture is good or not: Not only does a good architecture meet the needs of its users, developers, and owners at a given point in time, but it also meets them over time.

If  you think good architecture is expensive, try bad architecture. —— Brian Foote and Joseph Yoder

The kinds of changes a system's development typically experiences should not be the changes that are costly, that are hard to make, that take managed projects of their own rather than being folded into the daily and weekly flow of work.

That point leads us to a not-so-small physics-related problem: time travel. How do we know what those typical changes will be so that we can shape those significant decisions around them? How do we reduce future development effort and cost without crystal balls and time machines?

Architecture is the decisions that you wish you could get right early in a project, but that you are not necessarily more likely to get them right than any other. —— Ralph Johnson

Understanding the past is hard enough as it is; our grasp of the present is slippery at best; predicting the future is nontrivial.

This is where the road forks many ways.

Down the darkest path comes the idea that strong and stable architecture comes from authority and rigidity. If change is expensive, change is eliminated — its causes subdued or headed off into a bureaucratic ditch. The architect's mandate is total and totalitarian, with the architecture becoming a dystopia for its developers and a constant source of frustration for all.

Down another path comes a strong smell of speculative generality. A route filled with hard-coded guesswork, countless parameters, tombs of dead code, and more accidental complexity than you can shake a maintenance budget at.

The path we are most interested is the cleanest one. It recognizes the softness of software and aims to preserve it as a first-class property of the system. It recognizes that we operate with incomplete knowledge, but it also understands that, as humans, operating with incomplete knowledge is something we do, something we're good at. It plays more to our strengths than to our weaknesses. We create things and we discover things. We ask questions and we run experiments. A good architecture comes from understanding it more as a journey than as a destination, more as an ongoing process of enquiry than as a frozen artifact.

Architecture is a hypothesis, that needs to be proven by implementation and measurement. —— Tom Gilb

To walk this path requires care and attention, thought and observation, practice and principle. This might at first sound slow, but it's all in the way that you walk.

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

软件架构是系统设计过程中的重要设计决定的集合，可以通过交更成本来衡量每个设计决定的重要程度。 —— Grady Booch

需要付出的时间、金钱和人力成本是区分软件架构规模大小的衡量标准，也可以用来区分架构设计和细节设计。同时，我们还可以依据这个信息来判断某个特定架构设计是好还是坏好的架构，不仅要在某一特定时刻满足软件用户、开发者和所有者的需求，更要在一段时间内持续满足他们的后续需求。

如果你觉得好架构的成本太高，那你可以试试选择差的架构加上返工重来的成本。——  Brian Foote and Joseph Yoder

一个系统的常规变更不应该是成本高的，也不应该需要难以決策的大型设计调整，更不应该需要单独立项来推进。这些常规变更应该可以融入每日或者每周的日常系统维护中去完成。我们怎么能够预知某个系未来的变更需求，以便提前做准备呢？我们怎么能在没有水晶球与时光穿梭机的情况下，未卜先知，降低未来的变更成本呢？

所软件架构，就是你希望在项目一开始就能对，但是却不一定能够做得对的决策的集合。 ——  Ralph Johnson

了解历史已经够难了，我们对现实的认知也不够可靠，预言未来就更难了。这就是不同的软件开发理论的主要分歧点。

其中一条比较悲观阴暗的路线认为，只有权威和刚性能带来强壮与稳定。如果某项变更成本高昂，那么就应该忽视它 一一 变更背后的需求要么应该被抑制，要么就应该被丢到官僚主义的大机器中去绞碎。架构师的決定永远是完整的、彻底的，软件架构就是全体开发人员的敌托邦噩梦（Dystopia），永远是所有人沮丧的源泉。

另外一条路线则到处充斥着大量的投机性的通用设计。在这样的软件项目中到处都是硬编码的猜测性代码，到处是无穷无尽的参数，存在着成篇累牍的无效代码。维护这样的项目，肯定会遇到意外情况，而且无论预留多少资源都不够应付。

而本书试图探索的则是一条整洁路线。这条路线拥抱软件的灵活多变性，将其作为系統的一级设计目标。同时，我们也承认人类并不能全知全晓，但在信息不全的情况下人类仍然能够做出优良的決策。这条路线可以让我们多发挥优势，避开弱势。通过实际创造和探索，不停地提出问题和进行实验优良的软件架构不是一成不变的，只有经过不断打磨和改进才能最终成就。

软件架构是一猜想，只有通过实际实现和测量才能证实。—— Tom Gilb

遵循这条路线，我们需要用心，全神贯注，不停观察和思考，在原则指导下不断实践。虽然这可能听起来很麻烦、很慢，但是只要坚持走下去一定能够成功。走快的唯一方法是先走好。一起享受这个过程吧。

## Preface

The title of this book is Clean Architecture. That's an audacious name. Some would even call it arrogant. So why did I choose that title, and why did I write this book?

I wrote my very first line of code in 1964, at the age of 12. The year is now 2016, so I have been writing code for more than half a century. In that time, I have learned a few things about how to structure software systems — things that I believe others would likely find valuable.

I learned these things by building many systems, both large and small. I have built small embedded systems and large batch processing systems. I have built real-time systems and web systems. I have built console apps, GUI apps, process control apps, games, accounting systems, telecommunications systems, design tools, drawing apps, and many, many others.

I have built single-threaded apps, multithreaded apps, apps with few heavy-weight processes, apps with many light-weight processes, multiprocessor apps, database apps, mathematical apps, computational geometry apps, and many, many others.

I've built a lot of apps. I've built a lot of systems. And from them all, and by taking them all into consideration, I've learned something startling.

The architecture rules are the same!

1『软件架构的底层逻辑是相同的，做一张主题卡片。』—— 已完成

This is startling because the systems that I have built have all been so radically different. Why should such different systems all share similar rules of architecture? My conclusion is that the rules of  software architecture are independent of  every other variable.

This is even more startling when you consider the change that has taken place in hardware over the same half-century. I started programming on machines the size of kitchen refrigerators that had half-megahertz cycle times, 4K of core memory, 32K of disk memory, and a 10 character per second teletype interface. I am writing this preface on a bus while touring in South Africa. I am using a MacBook with four i7 cores running at 2.8 gigahertz each. It has 16 gigabytes of RAM, a terabyte of SSD, and a 2880*1800 retina display capable of showing extremely high-definition video. The difference in computational power is staggering. Any reasonable analysis will show that this MacBook is at least 10^22 more powerful than those early computers that I started using half a century ago.

Twenty-two orders of magnitude is a very large number. It is the number of angstroms from Earth to Alpha-Centuri. It is the number of electrons in the change in your pocket or purse. And yet that number — that number at least — is the computational power increase that I have experienced in my own lifetime.

And with all that vast change in computational power, what has been the effect on the software I write? It's gotten bigger certainly. I used to think 2000 lines was a big program. After all, it was a full box of cards that weighed 10 pounds. Now, however, a program isn't really big until it exceeds 100,000 lines.

The software has also gotten much more performant. We can do things today that we could scarcely dream about in the 1960s. The Forbin Project, The Moon Is a Harsh Mistress, and 2001: A Space Odyssey all tried to imagine our current future, but missed the mark rather significantly. They all imagined huge machines that gained sentience. What we have instead are impossibly small machines that are still … just machines.

And there is one thing more about the software we have now, compared to the software from back then: It's made of  the same stuff. It's made of if statements, assignment statements, and while loops.

Oh, you might object and say that we've got much better languages and superior paradigms. After all, we program in Java, or C#, or Ruby, and we use object-oriented design. True — and yet the code is still just an assemblage of sequence, selection, and iteration, just as it was back in the 1960s and 1950s.

When you really look closely at the practice of programming computers, you realize that very little has changed in 50 years. The languages have gotten a little better. The tools have gotten fantastically better. But the basic building blocks of a computer program have not changed.

If I took a computer programmer from 1966 forward in time to 2016 and put her [1] in front of my MacBook running IntelliJ and showed her Java, she might need 24 hours to recover from the shock. But then she would be able to write the code. Java just isn't that different from C, or even from Fortran.

And if I transported you back to 1966 and showed you how to write and edit PDP-8 code by punching paper tape on a 10 character per second teletype, you might need 24 hours to recover from the disappointment. But then you would be able to write the code. The code just hasn't changed that much.

That's the secret: This changelessness of the code is the reason that the rules of software architecture are so consistent across system types. The rules of software architecture are the rules of ordering and assembling the building blocks of programs. And since those building blocks are universal and haven't changed, the rules for ordering them are likewise universal and changeless.

Younger programmers might think this is nonsense. They might insist that everything is new and different nowadays, that the rules of the past are past and gone. If that is what they think, they are sadly mistaken. The rules have not changed. Despite all the new languages, and all the new frameworks, and all the paradigms, the rules are the same now as they were when Alan Turing wrote the first machine code in 1946.

But one thing has changed: Back then, we didn't know what the rules were. Consequently, we broke them, over and over again. Now, with half a century of experience behind us, we have a grasp of those rules.

And it is those rules — those timeless, changeless, rules — that this book is all about.

Register your copy of Clean Architecture on the InformIT site for convenient access to updates and/or corrections as they become available. To start the registration process, go to informit.com/register and log in or create an account. Enter the product ISBN (9780134494166) and click Submit. Look on the Registered Products tab for an Access Bonus Content link next to this product, and follow that link to access the bonus materials.

[1]  And she very likely would be female since, back then, women made up a large fraction of programmers.

本书的名字叫作《架构整洁之道》，使用这个名字可谓是十分胆大，甚至可以说有点目中无人了。那么，为什么我会选择写这本书，并且使用这个名字呢？自 1964 年，12 岁的我写下了人生的第一行代码算起，到 2016 年，我已经编程超过 50 年。在这段时间里，我自认为学到了构建软件系統的一些方法 一一 并且我相信这些方法和经验对其他人应该有些价值。

我学习的途径是实际构建一些大大小小的软件系统。我写过小型的嵌入式系统，也构造过大型的处理系统；我构建过实时控制系统，也构建过 Web 网页系统；我写过命令行程序、图形界面程序、进程管理程序、游戏、计费系统、通信系统、设计工具、画图工具等。我写过单线程程序，也写过多线程程序；我写过由几个重型进程组成的应用，也写过由大量轻型进程组成的应用；我写过跨多个处理器的应用，还有数据库类、数值计算类和几何计算类应用，以及很多很多其他类型的应用回首过去，经历了这么多应用和系统的构建过程，我最意外的领悟是：软件架的规则是相同的！

我所构建的这些系統是干差万别的，为什么所有这些差异巨大的系統都遵守同样的软件架构规则呢？这里我得出的结论是，软件架构规则和其他变量完全无关。

回顾过去这半个世纪以来硬件系统产生的巨大革，这个结论就更惊人了。我的程生涯起步于像家用冰箱那么大的巨型机时代，它的 CPU 频率只有 0.5MHz，拥有 4KB 核心内存，32KB 磁盘存储，以及每秒只能传输 10 个字符的电传打字机接口。而现在，我正在一辆游览南非的观光车上敲这篇前言。我正在用一个拥有 4 核 7 的 Macbook，每核 2.8GHz。这台笔记本电脑有 16GB 内存，1 TB SSD 硬盘，可以用 2880x1800 虹膜显示屏展现高清视频。二者计算能力上的差距真的是天壤之别。粗略分析可知，这台 Macbook 至少比我半个世纪以前用的计算机强大 1022 倍。

22 个数量级的差距是非常非常巨大的，从地球到半人马星系也只有 102 埃（angstrom，长度单位，主要用来描述原子尺寸与波长），你口袋里的零钱加起来所包含的电子数量也差不多为 102 个。而这个数字（注意还是至少）是我在一生中，所亲身经历的计算能力的提升计算能力发生了这么巨大的变化，但对我所写软件的影响有多大呢？软件尺寸当然变大了。我过去认为 2000 行的程序就很庞大了。毕竟这样的程序变成打孔卡片能装满一盒子，重量超过 10 磅。而现在，一个 10 万行的程序都不能算大程序了。

同时，软件性能当然也有大幅提升。我们现在可以轻轻松松地完成那些 1960 年只能幻想的事情。电影 The Forbin Project、The Moon is a Harsh Mistressl 以及 2001: A Space Odyssey 都试图预言我们的现状，但是都没有成功。在这些电影中普遍展现的是获得了智能的巨型机器，而我们目前所拥有的计算机，虽然体积之小是当初难以想象的，却还仅仅只是机器。

同时，还有一点很重要，今天的软件与过去的软件本质上仍然是一样的。都是由 if 语句、赋值语句以及 while 循环组成的。

哦，你可能会抗议说我们现在有更好的编程语以及更先进的编程范式了。毕竟，我们现在都是用 Java、C#、Ruby 语言编写程序，并且大量采用面向对象编程方式。这没错，但是最终产生的代码仍然只是顺序结构、分支结构、循环结构的组合，这方面和 20 世纪 60 年代甚至 50 年代的程序是一模一样。

如果深入研究计算机程的本质，我们就会发现这 50 年来，计算机编程基本没有什么大的变化。编程语言稍微进步了ー点，工具的质量大大提升了，但是计算机程序的基本构造没有什么变化。

如果一个 1966 年的计算机程序员时空穿梭来到 2016 年，在我的 Macbook 上用 Intellij 写 Java 程序，她可能也就需要 24 小时来适应一下，然后很快就能照常工作了。Java 其实和 C 区别并不大，和 FORTRAN 也没那么大区别。同样，如果我把你 一一 读者传送回 1966 年，告诉你如何在一个每秒处理 10 个字符的终端上通过打孔纸带来编辑 PDP-8 代码，估计你最多也只需要 24 小时的适应时间。毕竟编程还是编程，代码并没有本质的变化。

这就是秘密所在：计算机代码没有变化，软件架构的规则也就一直保持了一致。软件架构的规则其实就是排列组合代码块的规则。由于这些代码块本质上没有变化，因此排列组合它们的规则也就不会变化。

年轻的一代程序员可能认为这些都是胡说。他们可能坚持认为现在所有东西都是崭新的、从来没有过的，过去的规则已经过时，不再适用了。这是一个非常大的错误。这些规则一直都没有变。虽然我们有了新的编程语言、新的编程框架、新的编程范式，但是软件架构的规则仍然和 1946 年阿兰·图灵写下第一行机器代码的时候一样。

当然，不样的是，那时候我们还不知道规则是什么。所以我们一次一次地颠覆了它，并且为此一次一次地付出了代价。半个世纪过去了，我们终于可以说，现在我们对这些规则有一定程度的了解了。

写这本书就是为了讲述这些规则，这些永恒的、不变的软件架构规则。

## About  the  Author

Robert C. Martin (Uncle Bob) has been a programmer since 1970. He is the co-founder of cleancoders.com, which offers online video training for software developers, and is the founder of Uncle Bob Consulting LLC, which offers software consulting, training, and skill development services to major corporations worldwide. He served as the Master Craftsman at 8th Light, Inc., a Chicago-based software consulting firm. He has published dozens of articles in various trade journals and is a regular speaker at international conferences and trade shows. He served three years as the editor-in-chief of the C++ Report and served as the first chairman of the Agile Alliance.

Martin has authored and edited many books, including The Clean Coder, Clean Code, UML for Java Programmers, Agile Software Development, Extreme Programming in Practice, More C++ Gems, Pattern Languages of  Program Design 3, and Designing Object Oriented C++ Applications Using the Booch Method.

2『 Bob 大叔做一张人名卡片。』—— 已完成

## Introduction

It doesn't take a huge amount of knowledge and skill to get a program working. Kids in high school do it all the time. Young men and women in college start billion-dollar businesses based on scrabbling together a few lines of PHP or Ruby. Hoards of junior programmers in cube farms around the world slog through massive requirements documents held in huge issue tracking systems to get their systems to「work」by the sheer brute force of will. The code they produce may not be pretty; but it works. It works because getting something to work — once — just isn't that hard.

Getting it right is another matter entirely. Getting software right is hard. It takes knowledge and skills that most young programmers haven't yet acquired. It requires thought and insight that most programmers don't take the time to develop. It requires a level of discipline and dedication that most programmers never dreamed they'd need. Mostly, it takes a passion for the craft and the desire to be a professional.

And when you get software right, something magical happens: You don't need hordes of programmers to keep it working. You don't need massive requirements documents and huge issue tracking systems. You don't need global cube farms and 24/7 programming.

When software is done right, it requires a fraction of the human resources to create and maintain. Changes are simple and rapid. Defects are few and far between. Effort is minimized, and functionality and flexibility are maximized.

Yes, this vision sounds a bit utopian. But I've been there; I've seen it happen. I've worked in projects where the design and architecture of the system made it easy to write and easy to maintain. I've experienced projects that required a fraction of the anticipated human resources. I've worked on systems that had extremely low defect rates. I've seen the extraordinary effect that good software architecture can have on a system, a project, and a team. I've been to the promised land.

But don't take my word for it. Look at your own experience. Have you experienced the opposite? Have you worked on systems that are so interconnected and intricately coupled that every change, regardless of how trivial, takes weeks and involves huge risks? Have you experienced the impedance of bad code and rotten design? Has the design of the systems you've worked on had a huge negative effect on the morale of the team, the trust of the customers, and the patience of the managers? Have you seen teams, departments, and even companies that have been brought down by the rotten structure of their software? Have you been to programming hell?

I have — and to some extent, most of the rest of us have, too. It is far more common to fight your way through terrible software designs than it is to enjoy the pleasure of working with a good one.

编写并调试一段代码直到成功运行并不需要特别高深的知识和技能，现在的一名普通高中生都可以做到。有的大学生甚至通过拼一些 PHP 或 Ruby 代码就可以创办一个市值 10 亿美元的公司。想象一下，世界上有成群的初级程序员挤在大公司的隔板间里，日复一日地用力将记录在大型问题跟踪系统里的巨型需求文档一点点转化为能实际运行的代码。他们写出的代码可能不够优美，但是确实能够正常工作。因为创造一个能正常运行的系統 一一 哪怕只成功运行一次一还真不是一件特别困难的事。

但是将软件架构设计做好就完全另当别论了。软件架构设计是一件非常困难的事情，这通常需要大多数程序员所不具备的经验和技能。同时，也不是所有人都愿意花时间来学习和钻研这个方向。做一个好的软件架构师所需要的自律和专注程度可能会让大部分程序员始料未及，更别提软件架构师这个职业本身的社会认同感与人们投身其中的热情了。

但是，一旦将软件架构好了，你就会立即体会到其中的奥妙：维持系统正常运转再也不需要成群的程序员了；每个变更的实施也不再需要巨大的需求文档和复杂的任务追踪系了；程序员们再也不用缩在全球各地的隔板间里，24x7（即每天 24 小时，每星期 7 天）地疯狂加班了。

采用好的软件架构可以大大节省软件项目构建与维护的人力成本。让每次变更都短小简单，易于实施，并且避免缺陷，用最小的成本，最大程度地满足功能性和灵活性的要求。

是的，这可能有点像童话故事一样不可信，但是这些又确实是我的亲身经历。我曾经见过因为采用了好的软件架构设计，使得整个系统构建更简单、维护更容易的情况。我也见过因为采用了好的软件架构设计，整个项目最终比预计所使用的人力资源更少，而且更快地完成了。我真真切切地体会过，好的软件架构设计为整个系统所带来的天地的变化，绝不忽悠。

请读者回头想想自己的亲身经历，你肯定经历过这样的情境：某个系统因为其组件错综复杂，相互耦合紧密，而导致不管多么小的改动都需要数周的恶战才能完成。又或是某个系统中到处充满了腐朽的设计和连篇累牍的恶心代码，处处都是障碍。再或者，你有没有见过哪个系统的设计如此之差，整个团队的气低落，用户天天痛苦，项目经理们手足无措？你有没有见过某个软件系统因其架构腐朽不堪，而导致团队流失，部门解散，甚至公司倒闭？作为一名程序员，你在编程时体会过那种生不如死的感觉吗？

以上这些我也都切身体会过。我相信绝大部分读者也或多或少会有共鸣。好的软件架构太难得了，我们职业生涯的大部分时间可能都在和差的架构做斗争，而没有机会一睹优美的架构究竟是什么样子。

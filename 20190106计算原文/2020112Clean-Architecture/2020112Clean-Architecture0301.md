# 0200. Starting with the Bricks: Programming Paradigms

Software architecture begins with the code — and so we will begin our discussion of architecture by looking at what we’ve learned about code since code was first written.

In 1938, Alan Turing laid the foundations of what was to become computer programming. He was not the first to conceive of a programmable machine, but he was the first to understand that programs were simply data. By 1945, Turing was writing real programs on real computers in code that we would recognize (if we squinted enough). Those programs used loops, branches, assignment, subroutines, stacks, and other familiar structures. Turing’s language was binary.

Since those days, a number of revolutions in programming have occurred. One revolution with which we are all very familiar is the revolution of languages. First, in the late 1940s, came assemblers. These「languages」relieved the programmers of the drudgery of translating their programs into binary. In 1951, Grace Hopper invented A0, the first compiler. In fact, she coined the term compiler. Fortran was invented in 1953 (the year after I was born). What followed was an unceasing flood of new programming languages—COBOL, PL/1, SNOBOL, C, Pascal, C++, Java, ad infinitum.

Another, probably more significant, revolution was in programming paradigms. Paradigms are ways of programming, relatively unrelated to languages. A paradigm tells you which programming structures to use, and when to use them. To date, there have been three such paradigms. For reasons we shall discuss later, there are unlikely to be any others.

任何软件架构的实现都离不开具体的代码，所以我们对软件架构的讨论应该从第一行被写下的代码开始。1938 年，阿兰·图灵为现代计算机编程打下了地基。尽管他并不是第一个发明可编程机器的人，但却是第一个提出「程序即数据」的人。到 1945 年时，图灵已经在真实计算机上编写真实的、我们现在也能看懂的计算机程序了。这些程序中用到了循环、分支、賦值、子调用、等如今我们都很熟悉的结构。而图灵用的编程语言就是简单的二进制数序列。

从那时到现在，编程领域历经了数次变革，其中我们都很熱悉的就是编程语言的变革。首先是在 20 世纪 40 年代末期出现了汇编器（assembler），它能自动将一段程序转化为相应的二进制数序列，大幅解放了程序员。然后是 1951 年，Grace Hopper 发明了 A0, 这是世界上第一个编译器（compiler）。事实上，编译器这个名字就是他定义和推广使用的。再接着就到了 1953 年，那一年 FORTRANI 面世了（就在我出生的第二年）。接下来就是层出不穷的新编程语言了ー COBOL、PL/1、SNOBOL、C、Pascal、C++、Java 等等，不胜枚举。

除此之外，计算机编程领域还经历了另外一个更巨大、更重要的变革，那就是编程范式（paradigm）的变迁。编程范式指的是程序的编写模式，与具体的编程语言关系相对较小。这些范式会告诉你应该在什么时候采用什么样的代码结构。直到今天，我们也一共只有三个编程范式，而且未来几乎不可能再出现新的，接下来我们就看一下为什么。

# 0301. Paradigm Overview

The three paradigms included in this overview chapter are structured programming, object-orient programming, and functional programming.

本章将讲述三个编程范式，它们分别是结构化编程（structured programming）、面向对象编程（object- oriented programming）以及函数式编程（functional programming）。

## 3.1 Structured Programming

The first paradigm to be adopted (but not the first to be invented) was structured programming, which was discovered by Edsger Wybe Dijkstra in 1968. Dijkstra showed that the use of unrestrained jumps (goto statements) is harmful to program structure. As we’ll see in the chapters that follow, he replaced those jumps with the more familiar if/then/else and do/while/until constructs.

We can summarize the structured programming paradigm as follows: Structured programming imposes discipline on direct transfer of  control.

结构化编程是第一个普遍被采用的编程范式（但是却不是第一个被提出的），由 Edsger Wybe Dijkstra 于 1968 年最先提出。与此同时，Dijkstra 还论证了使用 goto 这样的无限制跳转语句将会损害程序的体结构。接下来的章节我们还会说到，也是这位 Dijkstra 最先主张用我们现在熟知的 f/then/else 语句和 do/while/unt 语句来代替跳转语句的。

我们可以将结构化编程范式归结为一句话：结构化程对程序控制权的直接转移进行了限制和规煎。

## 3.2 Object-Oriented  Programming

The second paradigm to be adopted was actually discovered two years earlier, in 1966, by Ole Johan Dahl and Kristen Nygaard. These two programmers noticed that the function call stack frame in the ALGOL language could be moved to a heap, thereby allowing local variables declared by a function to exist long after the function returned. The function became a constructor for a class, the local variables became instance variables, and the nested functions became methods. This led inevitably to the discovery of polymorphism through the disciplined use of function pointers.

We can summarize the object-oriented programming paradigm as follows: Object-oriented programming imposes discipline on indirect transfer of  control.

说到编程领域中第二个被广泛采用的编程范式，当然就是面向对象编程了。事实上，这个编程范式的提出比结构化编程还早了两年，是在 1966 年由 Ole Johan Dahl 和 Kriste Nygaard 在论文中总结归纳出来的。这两个程序员注意到在 ALGOLT 语言中，函数调用堆栈（call stack frame）可以被挪到堆

存区域里，这样函数定义的本地变量就可以在函数返回之后继续存在。这个函数就成为了一个类（class）的构造函数，而它所定义的本地变量就是类的成员变量，构造函数定义的嵌套函数就成为了成员方法（method）。这样一来，我们就可以利用多态（polymorphism）来限制用户对函数指针的使用。

在这里，我们也可以用一句话来总结面向对象编程：面向对象程对程序控制权的间接转移进行了限制和规范。

## 3.3 Functional Programming

The third paradigm, which has only recently begun to be adopted, was the first to be invented. Indeed, its invention predates computer programming itself. Functional programming is the direct result of the work of Alonzo Church, who in 1936 invented l-calculus while pursuing the same mathematical problem that was motivating Alan Turing at the same time. His l-calculus is the foundation of the LISP language, invented in 1958 by John McCarthy. A foundational notion of l-calculus is immutability—that is, the notion that the values of symbols do not change. This effectively means that a functional language has no assignment statement. Most functional languages do, in fact, have some means to alter the value of a variable, but only under very strict discipline.

We can summarize the functional programming paradigm as follows: Functional programming imposes discipline upon assignment.

尽管第三个编程范式是近些年オ刚刚开始被采用的，但它其实是三个范式中最先被发明的。事实上，函数式编程概念是基于与阿兰·图灵同时代的数学家 Alonzo Church 在 1936 年发明的入演算的直接術生物。1958 年 John Mccarthy 利用其作为基础发明了 LSP 语言。众所周知，入演算法的一个核心思想

是不可变性一一某个符号所对应的值是永远不变的，所以从理论上来说，函数式编程语言中应该是没有赋值语句的。大部分函数式编程语言只允许在非常严格的限制条件下，可以更改某个变量的值。

因此，我们在这里可以将函数式编程范式总结为下面这句话：函数式程对程序中的值进行了限和规范。

## 3.4 Food for Thought

Notice the pattern that I’ve quite deliberately set up in introducing these three programming paradigms: Each of the paradigms removes capabilities from the programmer. None of them adds new capabilities. Each imposes some kind of extra discipline that is negative in its intent. The paradigms tell us what not to do, more than they tell us what to do.

Another way to look at this issue is to recognize that each paradigm takes something away from us. The three paradigms together remove goto statements, function pointers, and assignment. Is there anything left to take away?

Probably not. Thus these three paradigms are likely to be the only three we will see—at least the only three that are negative. Further evidence that there are no more such paradigms is that they were all discovered within the ten years between 1958 and 1968. In the many decades that have followed, no new paradigms have been added.

如你所见，我在介绍三个编程范式的时候，有意采用了上面这种格式，目的是凸显每个编程范式的实际含义ー一它们都从某一方面限制和规范了程序员的能力。没有一个范式是增加新能力的。也就是说，每个编程范式的目的都是设置限制。这些范式主要是为了告诉我们不能做什么，而不是可以做什么。

另外，我们应该认识到，这三个编程范式分别限制了 goto 语句、函数指针和值语句的使用。那么除此之外，还有什么可以去除的吗？有了。因此这三个编程范式可能是仅有的三个了一如果单论去除能力的编程范式的话。支撑这一结论的另外一个证据是，三个编程范式都是在 1958 年到 1968 年这 10 年间被提出来的，后续再也没有新的编程范式出现过。

## Conclusion

What does this history lesson on paradigms have to do with architecture? Everything. We use polymorphism as the mechanism to cross architectural boundaries; we use functional programming to impose discipline on the location of and access to data; and we use structured programming as the algorithmic foundation of our modules.

Notice how well those three align with the three big concerns of architecture: function, separation of components, and data management.

大家可能会问，这些编程范式的历史知识与软件架构有关系吗？当然有，而且关系相当密切。譬如说，多态是我们跨越架构边界的手段，函数式编程是我们规范和限制数据存放位置与访问权限的手段，结构化编程则是各模块的算法实现基础。这和软件架构的三大关注重点不谋而合：功能性、组件独立性以及数据管理。
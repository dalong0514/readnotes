## 记忆时间

## 目录

0101 An Introduction to Java

1.1 Java as a Programming Platform

1.2 The Java「White Paper」Buzzwords

1.3 Java Applets and the Internet

1.4 A Short History of Java

1.5 Common Misconceptions about Java

0201 The Java Programming Environment

In this chapter:

2.1 Installing the Java Development Kit

2.2 Using the Command-Line Tools

2.3 Using an Integrated Development Environment

2.4 JShell

## 0101. An Introduction to Java

The first release of Java in 1996 generated an incredible amount of excitement, not just in the computer press, but in mainstream media such as the New York Times, the Washington Post, and BusinessWeek. Java has the distinction of being the first and only programming language that had a ten-minute story on National Public Radio. A `$`100,000,000 venture capital fund was set up solely for products using a specific computer language. I hope you will enjoy a brief history of Java that you will find in this chapter.

### 1.1 Java as a Programming Platform

In the first edition of this book, my coauthor Gary Cornell and I had this to write about Java:「As a computer language, Java's hype is overdone: Java is certainly a good programming language. There is no doubt that it is one of the better languages available to serious programmers. We think it could potentially have been a great programming language, but it is probably too late for that. Once a language is out in the field, the ugly reality of compatibility with existing code sets in.」

Our editor got a lot of flack for this paragraph from someone very high up at Sun Microsystems, the company that originally developed Java. The Java language has a lot of nice features that we will examine in detail later in this chapter. It has its share of warts, and some of the newer additions to the language are not as elegant as the original features because of compatibility requirements.

But, as we already said in the first edition, Java was never just a language. There are lots of programming languages out there, but few of them make much of a splash. Java is a whole platform, with a huge library, containing lots of reusable code, and an execution environment that provides services such as security, portability across operating systems, and automatic garbage collection.

As a programmer, you will want a language with a pleasant syntax and comprehensible semantics (i.e., not C++). Java fits the bill, as do dozens of other fine languages. Some languages give you portability, garbage collection, and the like, but they don't have much of a library, forcing you to roll your own if you want fancy graphics or networking or database access. Well, Java has everything — a good language, a high-quality execution environment, and a vast library. That combination is what makes Java an irresistible proposition to so many programmers.

1.1 Java 程序设计平台

本书的第 1 版是这样描写 Java 的：「作为一种计算机语言，Java 的广告词确实有点夸大其辞。然而，Java 的确是一种优秀的程序设计语言。作为一个名副其实的程序设计人员，使用 Java 无疑是一个好的选择。有人认为：Java 将有望成为一种最优秀的程序设计语言，但还需要一个相当长的发展时期。一旦一种语言应用于某个领域，与现存代码的相容性问题就摆在了人们的面前。」

我们的编辑手中有许多这样的广告词。这是 Sun 公司高层的某位不愿透露姓名的人士提供的（Sun 是原先开发 Java 的公司）。Java 有许多非常优秀的语言特性，本章稍后将会详细地讨论这些特性。由于相容性这个严峻的问题确实存在于现实中，所以，或多或少地还是有一些「累赘」被加到语言中，这就导致 Java 并不如想象中的那么完美无瑕。

但是，正像我们在第 1 版中已经指出的那样，Java 并不只是一种语言。在此之前出现的那么多种语言也没有能够引起那么大的轰动。Java 是一个完整的平台，有一个庞大的库，其中包含了很多可重用的代码和一个提供诸如安全性、跨操作系统的可移植性以及自动垃圾收集等服务的执行环境。

作为一名程序设计人员，常常希望能够有一种语言，它具有令人赏心悦目的语法和易于理解的语义（C++ 不是这样的）。与许多其他的优秀语言一样，Java 完全满足了这些要求。有些语言提供了可移植性、垃圾收集等，但是，没有提供一个大型的库。如果想要有奇特的绘图功能、网络连接功能和数据库存取功能就必须自己动手编写代码。Java 具备所有这些特性，它是一种功能齐全的出色语言，是一个高质量的执行环境，还提供了一个庞大的库。正是因为它集多种优势于一身，所以对广大的程序设计人员有着不可抗拒的吸引力。

### 1.2 The Java「White Paper」Buzzwords

The authors of Java wrote an influential white paper that explains their design goals and accomplishments. They also published a shorter overview that is organized along the following 11 buzzwords:

Simple

Object-Oriented

Distributed

Robust

Secure

Architecture-Neutral

Portable

Interpreted

High-Performance

Multithreaded

Dynamic

In the following subsections, you will find a summary, with excerpts from the white paper, of what the Java designers say about each buzzword, together with a commentary based on my experiences with the current version of Java.

Note: The white paper can be found at www.oracle.com/technetwork/java/langenv-140151.html. You can retrieve the overview with the 11 buzzwords at http://horstmann.com/corejava/java-an-overview/7Gosling.pdf.

1.2 Java「白皮书」的关键术语

Java 的设计者已经编写了颇有影响力的「白皮书」，用来解释设计的初衷以及完成的情况，并且发布了一个简短的摘要。这个摘要用下面 11 个关键术语进行组织：1）简单性。2）面向对象。3）分布式。4）健壮性。5）安全性。6）体系结构中立。7）可移植性。8）解释型。9）高性能。10）多线程。11）动态性。

本节将提供一个小结，给出白皮书中相关的说明，这是 Java 设计者对各个关键术语的论述，另外还会根据我们对 Java 当前版本的使用经验，给出对这些术语的理解。

注释：写这本书时，白皮书可以在 [The Java Language Environment: Contents](https://www.oracle.com/java/technologies/language-environment.html) 上找到。对于 11 个关键术语的论述请参看 http://horstmann.com/corejava/java-an-overview/7Gosling.pdf。

#### 1.2.1 Simple

We wanted to build a system that could be programmed easily without a lot of esoteric training and which leveraged today's standard practice. So even though we found that C++ was unsuitable, we designed Java as closely to C++ as possible in order to make the system more comprehensible. Java omits many rarely used, poorly understood, confusing features of C++ that, in our experience, bring more grief than benefit.

The syntax for Java is, indeed, a cleaned-up version of C++ syntax. There is no need for header files, pointer arithmetic (or even a pointer syntax), structures, unions, operator overloading, virtual base classes, and so on. (See the C++ notes interspersed throughout the text for more on the differences between Java and C++.) The designers did not, however, attempt to fix all of the clumsy features of C++. For example, the syntax of the switch statement is unchanged in Java. If you know C++, you will find the transition to the Java syntax easy.

At the time Java was released, C++ was actually not the most commonly used programming language. Many developers used Visual Basic and its drag-and-drop programming environment. These developers did not find Java simple. It took several years for Java development environments to catch up. Nowadays, Java development environments are far ahead of those for most other programming languages.

Another aspect of being simple is being small. One of the goals of Java is to enable the construction of software that can run stand-alone on small machines. The size of the basic interpreter and class support is about 40K; the basic standard libraries and thread support (essentially a self-contained microkernel) add another 175K.

This was a great achievement at the time. Of course, the library has since grown to huge proportions. There is now a separate Java Micro Edition with a smaller library, suitable for embedded devices.

1.2.1 简单性

人们希望构建一个无须深奥的专业训练就可以进行编程的系统，并且要符合当今的标准惯例。因此，尽管人们发现 C++ 不太适用，但在设计 Java 的时候还是尽可能地接近 C++，以便系统更易于理解。Java 剔除了 C++ 中许多很少使用、难以理解、易混淆的特性。在目前看来，这些特性带来的麻烦远远多于其带来的好处。

的确，Java 语法是 C++ 语法的一个「纯净」版本。这里没有头文件、指针运算（甚至指针语法）、结构、联合、操作符重载、虚基类等（请参阅本书各个章节给出的 C++ 注释，其中比较详细地解释了 Java 与 C++ 之间的区别）。然而，设计者并没有试图清除 C++ 中所有不适当的特性。例如，switch 语句的语法在 Java 中就没有改变。如果你了解 C++ 就会发现可以轻而易举地转换到 Java 语法。

Java 发布时，实际上 C++ 并不是最常用的程序设计语言。很多开发人员都在使用 Visual Basic 和它的拖放式编程环境。这些开发人员并不觉得 Java 简单。很多年之后 Java 开发环境才迎头赶上。如今，Java 开发环境已经远远超出大多数其他编程语言的开发环境。

简单的另一个方面是小。Java 的目标之一是支持开发能够在小型机器上独立运行的软件。基本的解释器以及类支持大约仅为 40KB；再加上基础的标准类库和对线程的支持（基本上是一个自包含的微内核）大约需要增加 175KB。

在当时，这是一个了不起的成就。当然，由于不断的扩展，类库已经相当庞大了。现在有一个独立的具有较小类库的 Java 微型版（Java Micro Edition），这个版本适用于嵌入式设备。

#### 1.2.2 Object-Oriented

Simply stated, object-oriented design is a programming technique that focuses on the data — objects — and on the interfaces to those objects. To make an analogy with carpentry, an「object-oriented」carpenter would be mostly concerned with the chair he is building, and secondarily with the tools used to make it; a「non-object-oriented」carpenter would think primarily of his tools. The object-oriented facilities of Java are essentially those of C++.

Object orientation was pretty well established when Java was developed. The object-oriented features of Java are comparable to those of C++. The major difference between Java and C++ lies in multiple inheritance, which Java has replaced with a simpler concept of interfaces. Java has a richer capacity for runtime introspection (discussed in Chapter 5) than C++.

1.2.2 面向对象

简单地讲，面向对象设计是一种程序设计技术。它将重点放在数据（即对象）和对象的接口上。用木匠打一个比方，一个「面向对象的」木匠始终关注的是所制作的椅子，第二位才是所使用的工具；一个「非面向对象的」木匠首先考虑的是所用的工具。在本质上，Java 的面向对象能力与 C++ 是一样的。

开发 Java 时面向对象技术已经相当成熟。Java 的面向对象特性与 C++ 旗鼓相当。Java 与 C++ 的主要不同点在于多重继承，在 Java 中，取而代之的是更简单的接口概念。与 C++ 相比，Java 提供了更丰富的运行时自省功能（有关这部分内容将在第 5 章中讨论）。

#### 1.2.3 Distributed

Java has an extensive library of routines for coping with TCP/IP protocols like HTTP and FTP. Java applications can open and access objects across the Net via URLs with the same ease as when accessing a local file system.

Nowadays, one takes this for granted — but in 1995, connecting to a web server from a C++ or Visual Basic program was a major undertaking.

1.2.3 分布式

Java 有一个丰富的例程库，用于处理像 HTTP 和 FTP 之类的 TCP/IP 协议。Java 应用程序能够通过 URL 打开和访问网络上的对象，其便捷程度就好像访问本地文件一样。如今，这一点已经得到认可，不过在 1995 年，主要还是从 C++ 或 Visual Basic 程序连接 Web 服务器。

#### 1.2.4 Robust

Java is intended for writing programs that must be reliable in a variety of ways. Java puts a lot of emphasis on early checking for possible problems, later dynamic (runtime) checking, and eliminating situations that are error-prone. . . . The single biggest difference between Java and C/C++ is that Java has a pointer model that eliminates the possibility of overwriting memory and corrupting data.

The Java compiler detects many problems that in other languages would show up only at runtime. As for the second point, anyone who has spent hours chasing memory corruption caused by a pointer bug will be very happy with this aspect of Java.

1.2.4 健壮性

Java 的设计目标之一在于使得 Java 编写的程序具有多方面的可靠性。Java 投入了大量的精力进行早期的问题检测、后期动态的（运行时）检测，并消除了容易出错的情况……Java 和 C++ 最大的不同在于 Java 采用的指针模型可以消除重写内存和损坏数据的可能性。

Java 编译器能够检测许多在其他语言中仅在运行时才能够检测出来的问题。至于第二点，对于曾经花费几个小时来检查由于指针 bug 而引起内存冲突的人来说，一定很喜欢 Java 的这一特性。

#### 1.2.5 Secure

Java is intended to be used in networked/distributed environments. Toward that end, a lot of emphasis has been placed on security. Java enables the construction of virus-free, tamper-free systems.

From the beginning, Java was designed to make certain kinds of attacks impossible, among them:

1 Overrunning the runtime stack — a common attack of worms and viruses.

2 Corrupting memory outside its own process space.

3 Reading or writing files without permission.

Originally, the Java attitude towards downloaded code was「Bring it on!」Untrusted code was executed in a sandbox environment where it could not impact the host system. Users were assured that nothing bad could happen because Java code, no matter where it came from, could never escape from the sandbox.

However, the security model of Java is complex. Not long after the first version of the Java Development Kit was shipped, a group of security experts at Princeton University found subtle bugs that allowed untrusted code to attack the host system.

Initially, security bugs were fixed quickly. Unfortunately, over time, hackers got quite good at spotting subtle flaws in the implementation of the security architecture. Sun, and then Oracle, had a tough time keeping up with bug fixes.

After a number of high-profile attacks, browser vendors and Oracle became increasingly cautious. Java browser plug-ins no longer trust remote code unless it is digitally signed and users have agreed to its execution.

Note: Even though in hindsight, the Java security model was not as successful as originally envisioned, Java was well ahead of its time. A competing code delivery mechanism from Microsoft relied on digital signatures alone for security. Clearly this was not sufficient: As any user of Microsoft's own products can confirm, programs from well-known vendors do crash and create damage.

1.2.5 安全性

Java 适用于网络 / 分布式环境。为了达到这个目标，在安全方面投入了很大精力。使用 Java 可以构建防病毒、防篡改的系统。

从一开始，Java 就设计成能够防范各种攻击，其中包括：

1、运行时堆栈溢出。如蠕虫和病毒常用的攻击手段。

2、破坏自己的进程空间之外的内存。

3、未经授权读写文件。

原先，Java 对下载代码的态度是「尽管来吧！」。不可信代码在一个沙箱环境中执行，在这里它不会影响主系统。用户可以确信不会发生不好的事情，因为 Java 代码不论来自哪里，都不能脱离沙箱。

不过，Java 的安全模型很复杂。Java 开发包（Java Development Kit，JDK）的第一版发布之后不久，普林斯顿大学的一些安全专家就发现一些小 bug 会允许不可信的代码攻击主系统。

最初，安全 bug 可以快速修复。遗憾的是，经过一段时间之后，黑客已经很擅长找出安全体系结构实现中的小漏洞。Sun 以及之后的 Oracle 为修复 bug 度过了一段很是艰难的日子。遭遇多次高调攻击之后，浏览器开发商和 Oracle 都越来越谨慎。Java 浏览器插件不再信任远程代码，除非代码有数字签名而且用户同意执行这个代码。

注释：现在看来，尽管 Java 安全模型没有原先预想的那么成功，但 Java 在那个时代确实相当超前。微软提供了一种与之竞争的代码传输机制，其安全性完全依赖于数字签名。显然这是不够的，因为微软自身产品的任何用户都可以证实，知名开发商的程序确实会崩溃并对系统产生危害。

#### 1.2.6 Architecture-Neutral

The compiler generates an architecture-neutral object file format. The compiled code is executable on many processors, given the presence of the Java runtime system. The Java compiler does this by generating bytecode instructions which have nothing to do with a particular computer architecture. Rather, they are designed to be both easy to interpret on any machine and easy to translate into native machine code on the fly.

Generating code for a「virtual machine」was not a new idea at the time. Programming languages such as Lisp, Smalltalk, and Pascal had employed this technique for many years.

Of course, interpreting virtual machine instructions is slower than running machine instructions at full speed. However, virtual machines have the option of translating the most frequently executed bytecode sequences into machine code — a process called just-in-time compilation.

Java's virtual machine has another advantage. It increases security because it can check the behavior of instruction sequences.

1.2.6 体系结构中立

编译器生成一个体系结构中立的目标文件格式，这是一种编译过的代码，只要有 Java 运行时系统，这些编译后的代码可以在许多处理器上运行。Java 编译器通过生成与特定的计算机体系结构无关的字节码指令来实现这一特性。精心设计的字节码不仅可以很容易地在任何机器上解释执行，而且还可以动态地翻译成本地机器代码。

当时，为「虚拟机」生成代码并不是一个新思路。诸如 Lisp、Smalltalk 和 Pascal 等编程语言多年前就已经采用了这种技术。

当然，解释虚拟机指令肯定会比全速运行机器指令慢很多。然而，虚拟机有一个选项，可以将执行最频繁的字节码序列翻译成机器码，这一过程被称为即时编译。Java 虚拟机还有一些其他的优点。它可以检测指令序列的行为，从而增强其安全性。

#### 1.2.7 Portable

Unlike C and C++, there are no「implementation-dependent」aspects of the specification. The sizes of the primitive data types are specified, as is the behavior of arithmetic on them.

For example, an int in Java is always a 32-bit integer. In C/C++, int can mean a 16-bit integer, a 32-bit integer, or any other size that the compiler vendor likes. The only restriction is that the int type must have at least as many bytes as a short int and cannot have more bytes than a long int. Having a fixed size for number types eliminates a major porting headache. Binary data is stored and transmitted in a fixed format, eliminating confusion about byte ordering. Strings are saved in a standard Unicode format.

The libraries that are a part of the system define portable interfaces. For example, there is an abstract Window class and implementations of it for UNIX, Windows, and the Macintosh.

The example of a Window class was perhaps poorly chosen. As anyone who has ever tried knows, it is an effort of heroic proportions to implement a user interface that looks good on Windows, the Macintosh, and ten flavors of UNIX. Java 1.0 made the heroic effort, delivering a simple toolkit that provided common user interface elements on a number of platforms. Unfortunately, the result was a library that, with a lot of work, could give barely acceptable results on different systems. That initial user interface toolkit has since been replaced, and replaced again, and portability across platforms remains an issue.

However, for everything that isn't related to user interfaces, the Java libraries do a great job of letting you work in a platform-independent manner. You can work with files, regular expressions, XML, dates and times, databases, network connections, threads, and so on, without worrying about the underlying operating system. Not only are your programs portable, but the Java APIs are often of higher quality than the native ones.

1.2.7 可移植性

与 C 和 C++ 不同，Java 规范中没有「依赖具体实现」的地方。基本数据类型的大小以及有关运算都做了明确的说明。

例如，Java 中的 int 永远为 32 位的整数，而在 C/C++ 中，int 可能是 16 位整数、32 位整数，也可能是编译器提供商指定的其他大小。唯一的限制只是 int 类型的大小不能低于 short int，并且不能高于 longint。在 Java 中，数据类型具有固定的大小，这消除了代码移植时令人头痛的主要问题。二进制数据以固定的格式进行存储和传输，消除了字节顺序的困扰。字符串是用标准的 Unicode 格式存储的。

作为系统组成部分的类库，定义了可移植的接口。例如，有一个抽象的 Window 类，并给出了在 UNIX、Windows 和 Macintosh 环境下的不同实现。

选择 Window 类作为例子可能并不太合适。凡是尝试过的人都知道，要编写一个在 Windows、Macintosh 和 10 种不同风格的 UNIX 上看起来都不错的程序有多么困难。Java 1.0 就尝试着做了这么一个壮举，发布了一个将常用的用户界面元素映射到不同平台上的简单工具包。遗憾的是，花费了大量的心血，却构建了一个在各个平台上都难以让人接受的库。原先的用户界面工具包已经重写，而且后来又再次重写，不过跨平台的可移植性仍然是个问题。

不过，除了与用户界面有关的部分外，所有其他 Java 库都能很好地支持平台独立性。你可以处理文件、正则表达式、XML、日期和时间、数据库、网络连接、线程等，而不用操心底层操作系统。不仅程序是可移植的，Java API 往往也比原生 API 质量更高。

#### 1.2.8 Interpreted

The Java interpreter can execute Java bytecodes directly on any machine to which the interpreter has been ported. Since linking is a more incremental and lightweight process, the development process can be much more rapid and exploratory.

This was a real stretch. Anyone who has used Lisp, Smalltalk, Visual Basic, Python, R, or Scala knows what a「rapid and exploratory」development process is. You try out something, and you instantly see the result. For the first 20 years of Java's existence, development environments were not focused on that experience. It wasn't until Java 9 that the jshell tool supported rapid and exploratory programming.

1.2.8 解释型

Java 解释器可以在任何移植了解释器的机器上执行 Java 字节码。由于链接是一个增量式且轻量级的过程，所以，开发过程也变得更加快捷，更加具有探索性。

这看上去很不错。用过 Lisp、Smalltalk、Visual Basic、Python、R 或 Scala 的人都知道「快捷而且具有探索性」的开发过程是怎样的。你可以做些尝试，然后就能立即看到结果。Java 开发环境并没有将重点放在这种体验上。

#### 1.2.9 High-Performance

While the performance of interpreted bytecodes is usually more than adequate, there are situations where higher performance is required. The bytecodes can be translated on the fly (at runtime) into machine code for the particular CPU the application is running on.

In the early years of Java, many users disagreed with the statement that the performance was「more than adequate.」Today, however, the just-in-time compilers have become so good that they are competitive with traditional compilers and, in some cases, even outperform them because they have more information available. For example, a just-in-time compiler can monitor which code is executed frequently and optimize just that code for speed. A more sophisticated optimization is the elimination (or「inlining」) of function calls. The just-in-time compiler knows which classes have been loaded. It can use inlining when, based upon the currently loaded collection of classes, a particular function is never overridden, and it can undo that optimization later if necessary.

1.2.9 高性能

尽管对解释后的字节码性能已经比较满意，但在有些场合下还需要更加高效的性能。字节码可以（在运行时刻）动态地翻译成对应运行这个应用的特定 CPU 的机器码。

使用 Java 的头几年，许多用户不同意这样的看法：性能就是「适用性更强」。然而，现在的即时编译器已经非常出色，以至于成了传统编译器的竞争对手。在某些情况下，甚至超越了传统编译器，原因是它们含有更多的可用信息。例如，即时编译器可以监控经常执行哪些代码并优化这些代码以提高速度。更为复杂的优化是消除函数调用（即「内联」）。即时编译器知道哪些类已经加载。基于当前加载的类集，如果特定的函数不会被覆盖，就可以使用内联。必要时，还可以撤销优化。

#### 1.2.10 Multithreaded

[The] benefits of multithreading are better interactive responsiveness and real-time behavior.

Nowadays, we care about concurrency because Moore's law has come to an end. Instead of faster processors, we just get more of them, and we have to keep them busy. Yet when you look at most programming languages, they show a shocking disregard for this problem.

Java was well ahead of its time. It was the first mainstream language to support concurrent programming. As you can see from the white paper, its motivation was a little different. At the time, multicore processors were exotic, but web programming had just started, and processors spent a lot of time waiting for a response from the server. Concurrent programming was needed to make sure the user interface didn't freeze.

Concurrent programming is never easy, but Java has done a very good job making it manageable.

1.2.10 多线程

多线程可以带来更好的交互响应和实时行为。

如今，我们非常关注并发性，因为摩尔定律行将完结。我们不再追求更快的处理器，而是着眼于获得更多的处理器，而且要让它们一直保持工作。不过，可以看到，大多数编程语言对于这个问题并没有显示出足够的重视。

Java 在当时很超前。它是第一个支持并发程序设计的主流语言。从白皮书中可以看到，它的出发点稍有些不同。当时，多核处理器还很神秘，而 Web 编程才刚刚起步，处理器要花很长时间等待服务器响应，需要并发程序设计来确保用户界面不会「冻住」。并发程序设计绝非易事，不过 Java 在这方面表现很出色，可以很好地管理这个工作。

#### 1.2.11 Dynamic

In a number of ways, Java is a more dynamic language than C or C++. It was designed to adapt to an evolving environment. Libraries can freely add new methods and instance variables without any effect on their clients. In Java, finding out runtime type information is straightforward.

This is an important feature in situations where code needs to be added to a running program. A prime example is code that is downloaded from the Internet to run in a browser. In C or C++, this is indeed a major challenge, but the Java designers were well aware of dynamic languages that made it easy to evolve a running program. Their achievement was to bring this feature to a mainstream programming language.

Note: Shortly after the initial success of Java, Microsoft released a product called J++ with a programming language and virtual machine that were almost identical to Java. This effort failed to gain traction, and Microsoft followed through with another language called C# that also has many similarities to Java but runs on a different virtual machine. This book does not cover J++ or C#.

1.2.11 动态性

从各种角度看，Java 与 C 或 C++ 相比更加具有动态性。它能够适应不断发展的环境。库中可以自由地添加新方法和实例变量，而对客户端却没有任何影响。在 Java 中找出运行时类型信息十分简单。

当需要将某些代码添加到正在运行的程序中时，动态性将是一个非常重要的特性。一个很好的例子是：从 Internet 下载代码，然后在浏览器上运行。如果使用 C 或 C++，这确实难度很大，不过 Java 设计者很清楚动态语言可以很容易地实现运行程序的演进。最终，他们将这一特性引入这个主流程序设计语言中。

注释：Java 成功地推出后不久，微软就发布了一个叫做 J++ 的产品，它与 Java 有几乎相同的编程语言以及虚拟机。现在，微软不再支持 J++，取而代之的是另一种名为 C# 的语言。C# 与 Java 有很多相似之处，然而使用的却是完全不同的虚拟机。本书不准备介绍 J++ 或 C# 语言。

### 1.3 Java Applets and the Internet

The idea here is simple: Users will download Java bytecodes from the Internet and run them on their own machines. Java programs that work on web pages are called applets. To use an applet, you only need a Java-enabled web browser, which will execute the bytecodes for you. You need not install any software. You get the latest version of the program whenever you visit the web page containing the applet. Most importantly, thanks to the security of the virtual machine, you never need to worry about attacks from hostile code.

Inserting an applet into a web page works much like embedding an image. The applet becomes a part of the page, and the text flows around the space used for the applet. The point is, this image is alive. It reacts to user commands, changes its appearance, and exchanges data between the computer presenting the applet and the computer serving it.

Figure 1.1 shows the Jmol applet that displays molecular structures. By using the mouse, you can rotate and zoom each molecule to better understand its structure. At the time that applets were invented, this kind of direct manipulation was not achievable with web pages — there was only rudimentary JavaScript and no HTML canvas.

Figure 1.1 The Jmol applet

When applets first appeared, they created a huge amount of excitement. Many people believe that the lure of applets was responsible for the astonishing popularity of Java. However, the initial excitement soon turned into frustration. Various versions of the Netscape and Internet Explorer browsers ran different versions of Java, some of which were seriously outdated. This sorry situation made it increasingly difficult to develop applets that took advantage of the most current Java version. Instead, Adobe's Flash technology became popular for achieving dynamic effects in the browser. Later, when Java was dogged by serious security issues, browsers and the Java browser plug-in became increasingly restrictive. Nowadays, it requires skill and dedication to get applets to work in your browser. For example, if you visit the Jmol web site at http://jmol.sourceforge.net/demo/aminoacids/, you will likely encounter a message exhorting you to configure your browser for allowing applets to run.

1.3 Java applet 与 Internet

这里的想法很简单：用户从 Internet 下载 Java 字节码，并在自己的机器上运行。

在网页中运行的 Java 程序称为 applet。要使用 applet，需要启用 Java 的 Web 浏览器执行字节码。不需要安装任何软件。任何时候只要访问包含 applet 的网页都会得到程序的最新版本。最重要的是，要感谢虚拟机的安全性，它让我们不必再担心来自恶意代码的攻击。在网页中插入一个 applet 就如同在网页中嵌入一幅图片。applet 会成为页面的一部分。文本环绕着 applet 所占据的空间周围。关键的一点是这个图片是活动的。它可以对用户命令做出响应，改变外观，在运行它的计算机与提供它的计算机之间传递数据。

图 1-1 展示了一个很好的动态网页的例子。Jmol applet 显示了分子结构，这将需要相当复杂的计算。在这个网页中，可以利用鼠标进行旋转，调整焦距等操作，以便更好地理解分子结构。用静态网页就无法实现这种直接的操作，而 applet 却可以达到此目的（可以在 http://jmol.sourceforge.net 上找到这个 applet）。

图 1-1 Jmol applet

当 applet 首次出现时，人们欣喜若狂。许多人相信 applet 的魅力将会导致 Java 迅速地流行起来。然而，初期的兴奋很快就淡化了。不同版本的 Netscape 与 Internet Explorer 运行不同版本的 Java，其中有些早已过时。这种糟糕的情况导致更加难于利用 Java 的最新版本开发 applet。实际上，为了在浏览器中得到动态效果，Adobe 的 Flash 技术变得相当流行。后来，Java 遭遇了严重的安全问题，浏览器和 Java 浏览器插件变得限制越来越多。如今，要在浏览器中使用 applet，这不仅需要一定的水平，而且要付出努力。例如，如果访问 Jmol 网站，可能会看到一个消息，警告你要适当地配置浏览器允许运行 applet。

### 1.4 A Short History of Java

This section gives a short history of Java's evolution. It is based on various published sources (most importantly an interview with Java's creators in the July 1995 issue of SunWorld's online magazine).

Java goes back to 1991, when a group of Sun engineers, led by Patrick Naughton and James Gosling (a Sun Fellow and an all-around computer wizard), wanted to design a small computer language that could be used for consumer devices like cable TV switchboxes. Since these devices do not have a lot of power or memory, the language had to be small and generate very tight code. Also, as different manufacturers may choose different central processing units (CPUs), it was important that the language not be tied to any single architecture. The project was code-named「Green.」

The requirements for small, tight, and platform-neutral code led the team to design a portable language that generated intermediate code for a virtual machine.

The Sun people came from a UNIX background, so they based their language on C++ rather than Lisp, Smalltalk, or Pascal. But, as Gosling says in the interview,「All along, the language was a tool, not the end.」Gosling decided to call his language「Oak」(presumably because he liked the look of an oak tree that was right outside his window at Sun). The people at Sun later realized that Oak was the name of an existing computer language, so they changed the name to Java. This turned out to be an inspired choice.

In 1992, the Green project delivered its first product, called「*7.」It was an extremely intelligent remote control. Unfortunately, no one was interested in producing this at Sun, and the Green people had to find other ways to market their technology. However, none of the standard consumer electronics companies were interested either. The group then bid on a project to design a cable TV box that could deal with emerging cable services such as video-on-demand. They did not get the contract. (Amusingly, the company that did was led by the same Jim Clark who started Netscape — a company that did much to make Java successful.

The Green project (with a new name of「First Person, Inc.」) spent all of 1993 and half of 1994 looking for people to buy its technology. No one was found. (Patrick Naughton, one of the founders of the group and the person who ended up doing most of the marketing, claims to have accumulated 300,000 air miles in trying to sell the technology.) First Person was dissolved in 1994.

While all of this was going on at Sun, the World Wide Web part of the Internet was growing bigger and bigger. The key to the World Wide Web was the browser translating hypertext pages to the screen. In 1994, most people were using Mosaic, a noncommercial web browser that came out of the supercomputing center at the University of Illinois in 1993. (Mosaic was partially written by Marc Andreessen as an undergraduate student on a work-study project, for `$`6.85 an hour. He moved on to fame and fortune as one of the cofounders and the chief of technology at Netscape.)

In the SunWorld interview, Gosling says that in mid-1994, the language developers realized that「We could build a real cool browser. It was one of the few things in the client/server mainstream that needed some of the weird things we'd done: architecture-neutral, real-time, reliable, secure — issues that weren't terribly important in the workstation world. So we built a browser.」

The actual browser was built by Patrick Naughton and Jonathan Payne and evolved into the HotJava browser, which was designed to show off the power of Java. The browser was capable of executing Java code inside web pages. This「proof of technology」was shown at SunWorld '95 on May 23, 1995, and inspired the Java craze that continues today.

Sun released the first version of Java in early 1996. People quickly realized that Java 1.0 was not going to cut it for serious application development. Sure, you could use Java 1.0 to make a nervous text applet that moved text randomly around in a canvas. But you couldn't even print in Java 1.0. To be blunt, Java 1.0 was not ready for prime time. Its successor, version 1.1, filled in the most obvious gaps, greatly improved the reflection capability, and added a new event model for GUI programming. It was still rather limited, though.

The big news of the 1998 JavaOne conference was the upcoming release of Java 1.2, which replaced the early toylike GUI and graphics toolkits with sophisticated scalable versions. Three days (!) after its release in December 1998, Sun's marketing department changed the name to the catchy Java 2 Standard Edition Software Development Kit Version 1.2.

Besides the Standard Edition, two other editions were introduced: the Micro Edition for embedded devices such as cell phones, and the Enterprise Edition for server-side processing. This book focuses on the Standard Edition.

Versions 1.3 and 1.4 of the Standard Edition were incremental improvements over the initial Java 2 release, with an ever-growing standard library, increased performance, and, of course, quite a few bug fixes. During this time, much of the initial hype about Java applets and client-side applications abated, but Java became the platform of choice for server-side applications.

Version 5.0 was the first release since version 1.1 that updated the Java language in significant ways. (This version was originally numbered 1.5, but the version number jumped to 5.0 at the 2004 JavaOne conference.) After many years of research, generic types (roughly comparable to C++ templates) have been added — the challenge was to add this feature without requiring changes in the virtual machine. Several other useful language features were inspired by C#: a「for each」loop, autoboxing, and annotations.

Version 6 (without the .0 suffix) was released at the end of 2006. Again, there were no language changes but additional performance improvements and library enhancements.

As datacenters increasingly relied on commodity hardware instead of specialized servers, Sun Microsystems fell on hard times and was purchased by Oracle in 2009. Development of Java stalled for a long time. In 2011, Oracle released a new version, with simple enhancements, as Java 7.

In 2014, the release of Java 8 followed, with the most significant changes to the Java language in almost two decades. Java 8 embraces a「functional」style of programming that makes it easy to express computations that can be executed concurrently. All programming languages must evolve to stay relevant, and Java has shown a remarkable capacity to do so.

The main feature of Java 9 goes all the way back to 2008. At that time, Mark Reinhold, the chief engineer of the Java platform, started an effort to break up the huge, monolithic Java platform. This was to be achieved by introducing modules, self-contained units of code that provide a specific functionality. It took eleven years to design and implement a module system that is a good fit for the Java platform, and it remains to be seen whether it is also a good fit for Java applications and libraries. Java 9, released in 2017, has other appealing features that we cover in this book.

Starting in 2018, Java versions are released every six months, to enable faster introduction of features. Certain versions, such as Java 11, are designated as long-term support versions.

Table 1.1 shows the evolution of the Java language and library. As you can see, the size of the application programming interface (API) has grown tremendously.

Table 1.1 Evolution of the Java Language

| Version | Year | New Language Features | Number of Classes and Interfaces |
| --- | --- | --- | --- |
| 1.0 | 1996 | The language itself | 211 |
| 1.1 | 1997 | Inner classes | 477 |
| 1.2 | 1998 | The strictfp modifier | 1,524 |
| 1.3 | 2000 | None | 1,840 |
| 1.4 | 2002 | Assertions | 2,723 |
| 5.0 | 2004 | Generic classes,「for each」loop, varargs, autoboxing, metadata, enumerations, static import | 3,279 |
| 6 | 2006 | None | 3,793 |
| 7 | 2011 | Switch with strings, diamond operator, binary literals, exception handling enhancements | 4,024 |
| 8 | 2014 | Lambda expressions, interfaces with default methods, stream and date/time libraries | 4,240 |
| 9 | 2017 | Modules, miscellaneous language and library enhancements | 6,005 |

1.4 Java 发展简史

本节将介绍 Java 的发展简史。这些内容来自很多出版资料（最重要的是 SunWorld 的在线杂志 1995 年 7 月刊上对 Java 创建者的专访）。

Java 的历史要追溯到 1991 年，由 Patrick Naughton 和 James Gosling（一个全能的计算机奇才）带领的 Sun 公司的工程师小组想要设计一种小型的计算机语言，主要用于像有线电视转换盒这类的消费设备。由于这些消费设备的处理能力和内存都很有限，所以语言必须非常小且能够生成非常紧凑的代码。另外，由于不同的厂商会选择不同的中央处理器（CPU），因此这种语言的关键是不与任何特定的体系结构捆绑在一起。这个项目被命名为「Green」。

代码短小、紧凑且与平台无关，这些要求促使开发团队设计一个可移植的语言，可以为虚拟机生成中间代码。

不过，Sun 公司的人都有 UNIX 的应用背景。因此，所开发的语言以 C++ 为基础，而不是 Lisp、Smalltalk 或 Pascal。不过，就像 Gosling 在专访中谈到的：「毕竟，语言只是实现目标的工具，而不是目标本身」。Gosling 把这种语言称为「Oak」（这么起名的原因大概是因为他非常喜欢自己办公室外的橡树）。Sun 公司的人后来发现 Oak 是一种已有的计算机语言的名字，于是，将其改名为 Java。事实证明这是一个很有灵感的选择。

1992 年，Green 项目发布了它的第一个产品，称之为「*7」。这个产品具有非常智能的远程控制。遗憾的是，Sun 公司对生产这个产品并不感兴趣，Green 项目组的人员必须找出其他的方法来将他们的技术推向市场。然而，没有一个标准消费品电子公司对此感兴趣。于是，Green 项目组竞标了一个提供视频点播等新型服务的有线电视盒的项目，但没有成功（有趣的是，得到这个项目的公司的领导恰恰是开创 Netscape 公司的 Jim Clark。Netscape 公司后来对 Java 的成功给予了很大的帮助）。

Green 项目（这时换了一个新名字 ——「First Person 公司」）花费了 1993 年一整年以及 1994 年的上半年，一直在苦苦寻求其技术的买家。然而，一个也没有找到（Patrick Naughton，项目组的创立人之一，也是完成此项目大多数市场工作的人，声称为了销售这项技术，累计飞行了 300000 英里）。1994 年 First Person 公司解散了。

当这一切在 Sun 公司发生的时候，Internet 的万维网也在日渐发展壮大。万维网的关键是把超文本页面转换到屏幕上的浏览器。1994 年大多数人都在使用 Mosaic，这是一个 1993 年出自伊利诺斯大学超级计算中心的非商业化的 Web 浏览器（Mosaic 的一部分是由 Marc Andreessen 编写的。当时，他作为一名参加半工半读项目的本科生，编写了这个软件，每小时的薪水只有 6.85 美元。他后来成了 Netscape 公司的创始人之一和技术总监，可谓名利双收）。

在接受 SunWorld 采访的时候，Gosling 说在 1994 年中期，Java 语言的开发者意识到：「我们能够建立一个相当酷的浏览器。我们已经拥有在客户机 / 服务器主流模型中所需要的体系结构中立、实时、可靠、安全 —— 这些在工作站环境并不太重要，所以，我们决定开发浏览器。」

实际的浏览器是由 Patrick Naughton 和 Jonathan Payne 开发的，并演变为 HotJava 浏览器。为了炫耀 Java 语言超强的能力，HotJava 浏览器采用 Java 编写。设计者让 HotJava 浏览器具有在网页中执行内嵌代码的能力。这一「技术印证」在 1995 年 5 月 23 日的 SunWorld 上得到展示，同时引发了人们延续至今的对 Java 的狂热追逐。

1996 年年初，Sun 发布了 Java 的第 1 个版本。人们很快地意识到 Java1.0 不能用来进行真正的应用开发。的确，可以使用 Java 1.0 来实现在画布上随机跳动的神经质的文本 applet，但它却没有提供打印功能。坦率地说，Java 1.0 的确没有为其黄金时期的到来做好准备。后来的 Java 1.1 弥补了其中的大多明显的缺陷，大大改进了反射能力，并为 GUI 编程增加了新的事件处理模型。不过它仍然具有很大的局限性。

1998 年 JavaOne 会议的头号新闻是即将发布 Java 1.2 版。这个版本取代了早期玩具式的 GUI，并且它的图形工具箱更加精细而具有可伸缩性，更加接近「一次编写，随处运行」的承诺。在 1998 年 12 月 Java 1.2 发布三天之后，Sun 公司市场部将其名称改为更加吸引人的「Java 2 标准版软件开发工具箱 1.2 版」。

除了「标准版」之外，Sun 还推出了两个其他的版本：一个是用于手机等嵌入式设备的「微型版」；另一个是用于服务器端处理的「企业版」。本书主要讲述标准版。

标准版的 1.3 和 1.4 版本对最初的 Java 2 版本做出了某些改进，扩展了标准类库，提高系统性能。当然，还修正了一些 bug。在此期间，Java applet 采用低调姿态，并淡化了客户端的应用，但 Java 却成为服务器端应用的首选平台。

5.0 版是自 1.1 版以来第一个对 Java 语言做出重大改进的版本（这一版本原来被命名为 1.5 版，在 2004 年的 JavaOne 会议之后，版本数字升至 5.0）。经历了多年的研究，这个版本添加了泛型类型（generic type）（类似于 C++ 的模板），其挑战性在于添加这一特性并没有对虚拟机做出任何修改。另外，还有几个受 C# 启发的很有用的语言特性：「for each」循环、自动装箱和注解。版本 6（没有后缀.0）于 2006 年年末发布。同样，这个版本没有对语言方面再进行改进。但是，改进了其他性能，并增强了类库。

版本 6（没有后缀.0）于 2006 年年末发布。同样，这个版本没有对语言方面再进行改进。但是，改进了其他性能，并增强了类库。随着数据中心越来越依赖于商业硬件而不是专用服务器，Sun Microsystems 终于沦陷，于 2009 年被 Oracle 收购。Java 的开发停滞了很长一段时间。直到 2011 年 Oracle 发布了 Java 的一个新版本，Java7，其中只做了一些简单的改进。

2014 年，Java 8 终于发布，在近 20 年中这个版本有了最大的改变。Java 8 提供了一种「函数式」编程方式，可以很容易地表述并发执行的计算。所有编程语言都必须与时俱进，Java 在这方面显示出非凡的能力。表 1-1 展示了 Java 语言以及类库的发展状况。可以看到，应用程序编程接口（API）的规模发生了惊人的变化。

表 1-1 Java 语言的发展状况

### 1.5 Common Misconceptions about Java

This chapter closes with a commented list of some common misconceptions about Java.

Java is an extension of HTML.

Java is a programming language; HTML is a way to describe the structure of a web page. They have nothing in common except that there are HTML extensions for placing Java applets on a web page.

I use XML, so I don't need Java.

Java is a programming language; XML is a way to describe data. You can process XML data with any programming language, but the Java API contains excellent support for XML processing. In addition, many important XML tools are implemented in Java. See Volume II for more information.

Java is an easy programming language to learn.

No programming language as powerful as Java is easy. You always have to distinguish between how easy it is to write toy programs and how hard it is to do serious work. Also, consider that only seven chapters in this book discuss the Java language. The remaining chapters of both volumes show how to put the language to work, using the Java libraries. The Java libraries contain thousands of classes and interfaces and tens of thousands of functions. Luckily, you do not need to know every one of them, but you do need to know surprisingly many to use Java for anything realistic.

Java will become a universal programming language for all platforms.

This is possible in theory. But in practice, there are domains where other languages are entrenched. Objective C and its successor, Swift, are not going to be replaced on iOS devices. Anything that happens in a browser is controlled by JavaScript. Windows programs are written in C++ or C#. Java has the edge in server-side programming and in cross-platform client applications.

Java is just another programming language.

Java is a nice programming language; most programmers prefer it to C, C++, or C#. But there have been hundreds of nice programming languages that never gained widespread popularity, whereas languages with obvious flaws, such as C++ and Visual Basic, have been wildly successful.

Why? The success of a programming language is determined far more by the utility of the support system surrounding it than by the elegance of its syntax. Are there useful, convenient, and standard libraries for the features that you need to implement? Are there tool vendors that build great programming and debugging environments? Do the language and the toolset integrate with the rest of the computing infrastructure? Java is successful because its libraries let you easily do things such as networking, web applications, and concurrency. The fact that Java reduces pointer errors is a bonus, so programmers seem to be more productive with Java — but these factors are not the source of its success.

Java is proprietary, and should therefore be avoided.

When Java was first created, Sun gave free licenses to distributors and end users. Although Sun had ultimate control over Java, they involved many other companies in the development of language revisions and the design of new libraries. Source code for the virtual machine and the libraries has always been freely available, but only for inspection, not for modification and redistribution. Java was「closed source, but playing nice.」

This situation changed dramatically in 2007, when Sun announced that future versions of Java would be available under the General Public License (GPL), the same open source license that is used by Linux. Oracle has committed to keeping Java open source. There is only one fly in the ointment — patents. Everyone is given a patent grant to use and modify Java, subject to the GPL, but only on desktop and server platforms. If you want to use Java in embedded systems, you need a different license and will likely need to pay royalties. However, these patents will expire within the next decade, and at that point Java will be entirely free.

Java is interpreted, so it is too slow for serious applications.

In the early days of Java, the language was interpreted. Nowadays, the Java virtual machine uses a just-in-time compiler. The「hot spots」of your code will run just as fast in Java as they would in C++, and in some cases even faster.

All Java programs run inside a web page.

All Java applets run inside a web browser. That is the definition of an applet — a Java program running inside a browser. But most Java programs are stand-alone applications that run outside of a web browser. In fact, many Java programs run on web servers and produce the code for web pages.

Java programs are a major security risk.

In the early days of Java, there were some well-publicized reports of failures in the Java security system. Researchers viewed it as a challenge to find chinks in the Java armor and to defy the strength and sophistication of the applet security model. The technical failures that they found have all been quickly corrected. Later, there were more serious exploits, to which Sun, and later Oracle, responded too slowly. Browser manufacturers reacted, and perhaps overreacted, by deactivating Java by default. To keep this in perspective, consider the far greater number of virus attacks in Windows executable files that cause real grief but surprisingly little criticism of the weaknesses of the attacked platform. Even 20 years after its creation, Java is far safer than any other commonly available execution platform.

JavaScript is a simpler version of Java.

JavaScript, a scripting language that can be used inside web pages, was invented by Netscape and originally called LiveScript. JavaScript has a syntax that is reminiscent of Java, and the languages' names sound similar, but otherwise they are unrelated. In particularly, Java is strongly typed — the compiler catches many errors that arise from type misuse. In JavaScript, such errors are only found when the program runs, which makes their elimination far more laborious.

With Java, I can replace my desktop computer with a cheap「Internet appliance.」

When Java was first released, some people bet big that this was going to happen. Companies produced prototypes of Java-powered network computers, but users were not ready to give up a powerful and convenient desktop for a limited machine with no local storage. Nowadays, of course, the world has changed, and for a large majority of end users, the platform that matters is a mobile phone or tablet. The majority of these devices are controlled by the Android platform, which is a derivative of Java. Learning Java programming will help you with Android programming as well.

1.5 关于 Java 的常见误解

在结束本章之前，我们列出了一些关于 Java 的常见误解，同时给出了解释。

1、Java 是 HTML 的扩展。

Java 是一种程序设计语言；HTML 是一种描述网页结构的方式。除了用于在网页上放置 Java applet 的 HTML 扩展之外，两者没有任何共同之处。

2、使用 XML，所以不需要 Java。

Java 是一种程序设计语言；XML 是一种描述数据的方式。可以使用任何一种程序设计语言处理 XML 数据，而 Java API 对 XML 处理提供了很好的支持。此外，许多重要的第三方 XML 工具采用 Java 编写。有关这方面更加详细的信息请参看卷 Ⅱ。

3、Java 是一种非常容易学习的程序设计语言。

像 Java 这种功能强大的语言大都不太容易学习。首先，必须将编写玩具式程序的轻松和开发实际项目的艰难区分开来。需要注意的是：本书只用了 7 章讨论 Java 语言。在两卷中，其他的章节介绍如何使用 Java 类库将 Java 语言应用到实际中去。Java 类库包含了数千种类和接口以及数万个函数。幸运的是，并不需要知道它们中的每一个，然而，要想 Java 解决实际问题，还是需要了解不少内容的。

4、Java 将成为适用于所有平台的通用性编程语言。

从理论上讲，这是完全有可能的。但在实际中，某些领域其他语言有更出色的表现，比如，Objective C 和后来的 Swift 在 iOS 设备上就有着无可取代的地位。浏览器中的处理几乎完全由 JavaScript 掌控。Windows 程序通常都用 C++ 或 C# 编写。Java 在服务器端编程和跨平台客户端应用领域则很有优势。

5、Java 只不过是另外一种程序设计语言。

Java 是一种很好的程序设计语言，很多程序设计人员喜欢 Java 胜过 C、C++ 或 C#。有上百种好的程序设计语言没有广泛地流行，而带有明显缺陷的语言，如：C++ 和 Visual Basic 却大行其道。

这是为什么呢？程序设计语言的成功更多地取决于其支撑系统的能力，而不是优美的语法。人们主要关注：是否提供了易于实现某些功能的易用、便捷和标准的库？是否有开发工具提供商能建立强大的编程和调试环境？语言和工具集是否能够与其他计算基础架构整合在一起？Java 的成功源于其类库能够让人们轻松地完成原本有一定难度的事情。例如：联网 Web 应用和并发。Java 减少了指针错误，这是一个额外的好处，因此使用 Java 编程的效率更高。但这些并不是 Java 成功的全部原因。

6、Java 是专用的，应该避免使用。

最初创建 Java 时，Sun 为销售者和最终用户提供了免费许可。尽管 Sun 对 Java 拥有最终的控制权，不过在语言版本的不断发展和新库的设计过程中还涉及很多其他公司。虚拟机和类库的源代码可以免费获得，不过仅限于查看，而不能修改和再发布。Java 是「闭源的，不过可以很好地使用」。

这种状况在 2007 年发生了戏剧性的变化，Sun 声称 Java 未来的版本将在 General Public License（GPL）下提供。Linux 使用的是同一个开放源代码许可。Oracle 一直致力于保持 Java 开源。只有一点美中不足 —— 专利。根据 GPL，任何人都可以得到专利许可，允许其使用和修改 Java，不过仅限于桌面和服务器平台。如果你想在嵌入式系统中使用 Java，就需要另外一个不同的许可，这很可能需要付费。不过，这些专利在未来十年就会到期，那时 Java 就完全免费了。

7、Java 是解释型的，因此对于关键的应用程序速度太慢了。

早期的 Java 是解释型的。现在 Java 虚拟机使用了即时编译器，因此采用 Java 编写的「热点」代码其运行速度与 C++ 相差无几，有些情况下甚至更快。

对于 Java 桌面应用速度慢，人们已经抱怨很多年了。但是，今天的计算机速度远比人们发出抱怨的时候快了很多。一个较慢的 Java 程序与几年前相当快的 C++ 程序相比还要快一些。

8、所有的 Java 程序都是在网页中运行的。

所有的 Java applet 都是在网页浏览器中运行的。这也恰恰是 applet 的定义，即一种在浏览器中运行的 Java 程序。然而，大多数 Java 程序是运行在 Web 浏览器之外的独立应用程序。实际上，很多 Java 程序都在 Web 服务器上运行并生成用于网页的代码。

9、Java 程序是主要的安全风险对于早期的 Java，有过关于安全系统失效的报道，曾经一度引起公众哗然。研究人员将这视为一种挑战，即努力找出 Java 的漏洞，对 applet 安全模型的强度和复杂度发起挑战。随后，人们很快就解决了引发问题的所有技术因素。后来又发现了更严重的漏洞，而 Sun 以及后来的 Oracle 反应却过于迟缓。浏览器制造商则有些反应过度，他们甚至默认禁用了 Java。客观地来讲，可以想想针对 Windows 可执行文件和 Word 宏有数百万种病毒攻击，并造成了巨大的损害，不过奇怪的是却很少有人批评被攻击平台的脆弱。

有些系统管理员甚至在公司浏览器中禁用了 Java，而同时却允许用户下载可执行文件和 Word 文档，实际上，这些带来的风险远甚于使用 Java。尽管距离 Java 诞生已经 20 年之久，与其他常用的执行平台相比，Java 还是安全得多。

10、JavaScript 是 Java 的简易版。

JavaScript 是一种在网页中使用的脚本语言，它是由 Netscape 发明的，原来的名字叫做 LiveScript。JavaScript 的语法类似 Java，除此之外，两者无任何关系。当然，名字有些相像。JavaScript 的一个子集已经标准化为 ECMA-262。与 Java applet 相比，JavaScript 更紧密地与浏览器集成在一起。特别是 JavaScript 程序可以修改正在显示的文档，而 applet 只能在有限的区域内控制外观。

11、使用 Java 可以用廉价的 Internet 设备取代桌面计算机。

当 Java 刚刚发布的时候，一些人打赌：肯定会有这样的好事情发生。一些公司已经生产出 Java 网络计算机的原型，不过用户还不打算放弃功能强大而便利的桌面计算机，而去使用没有本地存储而且功能有限的网络设备。当然，如今世界已经发生改变，对于大多数最终用户，常用的平台往往是手机或平板电脑。这些设备大多使用安卓平台，这是 Java 的衍生产物。学习 Java 编程肯定也对 Android 编程很有帮助。

## 0201. The Java Programming Environment

In this chapter, you will learn how to install the Java Development Kit (JDK) and how to compile and run various types of programs: console programs, graphical applications, and applets. You can run the JDK tools by typing commands in a terminal window. However, many programmers prefer the comfort of an integrated development environment. You will learn how to use a freely available development environment to compile and run Java programs. Once you have mastered the techniques in this chapter and picked your development tools, you are ready to move on to Chapter 3, where you will begin exploring the Java programming language.

0201 Java 程序设计环境

本章主要介绍如何安装 Java 开发工具包（JDK）以及如何编译和运行不同类型的程序：控制台程序、图形化应用程序以及 applet。运行 JDK 工具的方法是在终端窗口中键入命令。然而，很多程序员更喜欢使用集成开发环境。为此，将在稍后介绍如何使用免费的开发环境编译和运行 Java 程序。尽管学起来很容易，但集成开发环境需要吞噬大量资源，编写小型程序时也比较烦琐。一旦掌握了本章的技术，并选定了自己的开发工具，就可以学习第 3 章，开始研究 Java 程序设计语言。

### 2.1 Installing the Java Development Kit

The most complete and up-to-date versions of the Java Development Kit (JDK) are available from Oracle for Linux, Mac OS, Solaris, and Windows. Versions in various states of development exist for many other platforms, but those versions are licensed and distributed by the vendors of those platforms.

2.1 安装 Java 开发工具包

Oracle 公司为 Linux、Mac OS X、Solaris 和 Windows 提供了 Java 开发工具包（JDK）的最新、最完整的版本。用于很多其他平台的版本仍处于多种不同的开发状态中，不过，这些版本都由相应平台的开发商授权并分发。

#### 2.1.1 Downloading the JDK

To download the Java Development Kit, visit the web site at www.oracle.com/technetwork/java/javase/downloads and be prepared to decipher an amazing amount of jargon before you can get the software you need. See Table 2.1 for a summary.

Table 2.1 Java Jargon

| Name | Acronym | Explanation |
| --- | --- | --- |
| Java Development Kit | JDK | The software for programmers who want to write Java programs |
| Java Runtime Environment | JRE | The software for consumers who want to run Java programs |
| Server JRE | — | The software for running Java programs on servers |
| Standard Edition | SE | The Java platform for use on desktops and simple server applications |
| Enterprise Edition | EE | The Java platform for complex server applications |
| Micro Edition | ME | The Java platform for use on small devices |
| JavaFX | — | An alternate toolkit for graphical user interfaces that is included with certain Java SE distributions prior to Java 11 |
| OpenJDK | — | A free and open source implementation of Java SE |
| Java 2 | J2 | An outdated term that described Java versions from 1998 until 2006 |
| Software Development Kit | SDK | An outdated term that described the JDK from 1998 until 2006 |
| Update | u | Oracle's term for a bug fix release up to Java 8 |
| NetBeans | — | Oracle's integrated development environment |

You already saw the abbreviation JDK for Java Development Kit. Somewhat confusingly, versions 1.2 through 1.4 of the kit were known as the Java SDK (Software Development Kit). You will still find occasional references to the old term. Up to Java 10, there is also a Java Runtime Environment (JRE) that contains only the virtual machine. That is not what you want as a developer. It is intended for end users who have no need for the compiler.

Next, you'll see the term Java SE everywhere. That is the Java Standard Edition, in contrast to Java EE (Enterprise Edition) and Java ME (Micro Edition).

You might run into the term Java 2 that was coined in 1998 when the marketing folks at Sun felt that a fractional version number increment did not properly communicate the momentous advances of JDK 1.2. However, since they had that insight only after the release, they decided to keep the version number 1.2 for the development kit. Subsequent releases were numbered 1.3, 1.4, and 5.0. The platform, however, was renamed from Java to Java 2. Thus, we had Java 2 Standard Edition Software Development Kit Version 5.0, or J2SE SDK 5.0.

Fortunately, in 2006, the numbering was simplified. The next version of the Java Standard Edition was called Java SE 6, followed by Java SE 7 and Java SE 8.

However, the「internal」version numbers are 1.6.0, 1.7.0, and 1.8.0. This minor madness finally ran its course with Java SE 9, when the version number became 9, and then 9.0.1. (Why not 9.0.0 for the initial version? To keep a modicum of excitement, the version number specification requires that trailing zeroes are dropped for the fleeting interval between a major release and its first security update.)

Note

For the remainder of the book, we will drop the「SE」acronym. When you see「Java 9」, that means「Java SE 9」.

Prior to Java 9, there were 32-bit and 64-bit versions of the Java Development Kit. The 32-bit versions are no longer developed by Oracle. You need to have a 64-bit operating system to use the Oracle JDK.

With Linux, you have a choice between an RPM file and a .tar.gz file. We recommend the latter—you can simply uncompress it anywhere you like.

Now you know how to pick the right JDK. To summarize:

You want the JDK (Java SE Development Kit), not the JRE.

Linux: Pick the .tar.gz version.

Accept the license agreement and download the file.

Note

Depending on the constellation of the planets, Oracle may offer you a bundle that contains both the Java Development Kit and the NetBeans integrated development environment. I suggest that you stay away from all bundles and install only the Java Development Kit at this time. If you later decide to use NetBeans, simply download it from http://netbeans.org.

2.1.1 下载 JDK

要想下载 Java 开发工具包，可以访问 Oracle 网站：www.oracle.com/technetwork/java/javase/downloads，在得到所需的软件之前必须弄清楚大量专业术语。请看表 2-1 的总结。

表 2-1 Java 术语

你已经看到，JDK 是 Java Development Kit 的缩写。有点混乱的是：这个工具包的版本 1.2-1.4 被称为 Java SDK（软件开发包，Software Development Kit）。在某些场合下，还可以看到这个过时的术语。另外，还有一个术语是 Java 运行时环境（JRE），它包含虚拟机但不包含编译器。这并不是开发者想要的环境，而是专门为不需要编译器的用户而提供。

接下来，Java SE 会大量出现，相对于 Java EE（Enterprise Edition）和 Java ME（MicroEdition），它是 Java 的标准版。

Java 2 这种提法始于 1998 年。当时 Sun 公司的销售人员感觉增加小数点后面的数值改变版本号并没有反映出 JDK 1.2 的重大改进。但是，由于在发布之后才意识到这个问题，所以决定开发工具包的版本号仍然沿用 1.2，接下来的版本是 1.3、1.4 和 5.0。但是，Java 平台被重新命名为 Java 2。因此，就有了 Java 2 Standard Edition Software Development Kit（Java 2 标准版软件开发包）的 5.0 版，即 J2SE SDK 5.0。幸运的是，2006 年版本号得到简化。Java 标准版的下一个版本取名为 Java SE 6，后来又有了 Java SE7 和 Java SE 8。不过，「内部」版本号分别是 1.6.0、1.7.0 和 1.8.0。

幸运的是，2006 年版本号得到简化。Java 标准版的下一个版本取名为 Java SE 6，后来又有了 Java SE7 和 Java SE 8。不过，「内部」版本号分别是 1.6.0、1.7.0 和 1.8.0。

当 Oracle 为解决一些紧急问题做出某些微小的版本改变时，将其称为更新。例如：Java SE 8u31 是 Java SE 8 的第 31 次更新，它的内部版本号是 1.8.0_31。更新不需要安装在前一个版本上，它会包含整个 JDK 的最新版本。另外，并不是所有更新都公开发布，所以如果「更新 31」之后没有「更新 32」，你也不用惊慌。

对于 Windows 或 Linux，需要在 x86（32 位）和 x64（64 位）版本之间做出选择。应当选择与你的操作系统体系结构匹配的版本。

对于 Linux，还可以在 RPM 文件和.tar.gz 文件之间做出选择。我们建议使用后者，可以在你希望的任何位置直接解压缩这个压缩包。现在你已经了解了如何选择适当的 JDK。下面做一个小结：

1、你需要的是 JDK（Java SE 开发包），而不是 JRE。

2、Windows 或 Linux：32 位选择 x86，64 位以 x64。

3、Linux：选择.tar.gz 版本。接受许可协议，然后下载文件。

注释：Oracle 提供了一个捆绑包，其中包含 Java 开发包（JDK）和 NetBeans 集成开发环境。建议现在不要安装任何捆绑包，而只需安装 Java 开发包。如果以后你打算使用 NetBeans，可以再从 http://netbeans.org 下载。

#### 2.1.2 Setting up the JDK

After downloading the JDK, you need to install it and figure out where it was installed—you'll need that information later.

Under Windows, launch the setup program. You will be asked where to install the JDK. It is best not to accept a default location with spaces in the path name, such as c:\Program Files\Java\jdk-11.0.x. Just take out the Program Files part of the path name.

On the Mac, run the installer. It installs the software into /Library/Java /JavaVirtualMachines/jdk-11.0.x.jdk/Contents/Home. Locate it with the Finder.

On Linux, simply uncompress the .tar.gz file to a location of your choice, such as your home directory or /opt. Or, if you installed from the RPM file, double-check that it is installed in /usr/java/jdk-11.0.x.

In this book, the installation directory is denoted as jdk. For example, when referring to the jdk/bin directory, I mean the directory with a name such as /opt/jdk-11.0.4/bin or c:\Java\jdk-11.0.4\bin.

When you install the JDK on Windows or Linux, you need to carry out one additional step: Add the jdk/bin directory to the executable path—the list of directories that the operating system traverses to locate executable files.

On Linux, add a line such as the following to the end of your ~/.bashrc or ~/.bash_profile file:

Click here to view code image

export PATH=jdk/bin:$PATH

Be sure to use the correct path to the JDK, such as /opt/jdk-11.0.4.

Under Windows 10, type「environment」into the search bar of the Windows Settings, and select「Edit environment variables for your account」(see Figure 2.1). An Environment Variables dialog should appear. (It may hide behind the Windows Settings dialog. If you can't find it anywhere, try running sysdm.cpl from the Run dialog that you get by holding down the Windows and R key at the same time, and then select the Advanced tab and click the Environment Variables button.) Locate and select a variable named Path in the User Variables list. Click the Edit button, then the New button, and add an entry with the jdk\bin directory (see Figure 2.2).

Figure 2.1 Setting system properties in Windows 10

Figure 2.2 Setting the Path environment variable in Windows 10

Save your settings. Any new「Command Prompt」windows that you start will have the correct path.

Here is how you test whether you did it right: Start a terminal window. Type the line

```
javac --version
```

and press the Enter key. You should get a display such as this one:

javac 9.0.4

If instead you get a message such as「javac: command not found」or「The name specified is not recognized as an internal or external command, operable program or batch file,」then you need to go back and double-check your installation.

2.1.2 设置 JDK

下载 JDK 之后，需要安装这个开发包并明确要在哪里安装，后面还会需要这个信息。

1、在 Windows 上，启动安装程序。会询问你要在哪里安装 JDK。最好不要接受路径名中包含空格的默认位置，如 c：\ProgramFiles\Java\jdk1.8.0_version。取出路径名中的 Program Files 部分就可以了。

1『安装路径中最好不要包含空格，这个知识点 get 到了。（2021-10-15）』

2、在 Mac 上，运行安装程序。这会把软件安装到 /Library/Java/JavaVirtualMachines/jdk1.8.0_version.jdk/Contents/Home。用 Finder 找到这个目录。

3、在 Linux 上，只需要把 .tar.gz 文件解压缩到你选择的某个位置，如你的主目录，或者 /opt。如果从 RPM 文件安装，则要反复检查是否安装在 /usr/java/jdk1.8.0_version。

在这本书中，安装目录用 jdk 表示。例如，谈到 jdk/bin 目录时，是指 /opt/jdk1.8.0_31/bin 或 c：\Java\jdk1.8.0_31\bin 目录。

在 Windows 或 Linux 上安装 JDK 时，还需要另外完成一个步骤：将 jdk/bin 目录增加到执行路径中 —— 执行路径是操作系统查找可执行文件时所遍历的目录列表。

在 Linux 上，需要在 ～/.bashrc 或 ～/.bash_profile 文件的最后增加这样一行：

1、一定要使用 JDK 的正确路径，如 /opt/jdk1.8.0_31。

2、在 Windows 上，启动控制面板，选择「系统与安全」（System andSecurity），再选择「系统」（System），选择高级系统设置（AdvancedSystem Settings）（参见图 2-1）。在系统属性（System Properties）对话框中，点击「高级」（Advanced）标签页，然后点击「环境」（Environment）按钮。

图 2-1 Windows 7 中设置系统属性

滚动「系统变量」（System Variables）列表，直到找到名为 Path 的变量。点击「编辑」（Edit）按钮（参见图 2-2）。将 jdk\bin 目录增加到路径最前面，并用一个分号分隔新增的这一项，如下所示：

图 2-2 Windows 7 中设置 Path 环境变量

注意要把 jdk 替换为具体的 Java 安装路径，如 c：\Java\jdk1.8.0_31。如果忽视前面的建议，想要保留 Program Files 部分，则要把整个路径用双引号引起来："c：\Program Files\Java\jdk1.8.0_31\bin"；其他目录。

保存所做的设置。之后新打开的所有控制台窗口都会有正确的路径。

可以如下测试设置是否正确：打开一个终端窗口，键入：

然后按回车键。应该能看到显示以下信息：

如果得到诸如「javac：command not found」（javac：：命令未找到）或「The name specified is not recognized as an internal or externalcommand，operable program or batch file」（指定名不是一个内部或外部命令、可执行的程序或批文件），就需要退回去反复检查你的安装。

#### 2.1.3 Installing Source Files and Documentation

The library source files are delivered in the JDK as a compressed file lib/src.zip. Unpack that file to get access to the source code. Simply do the following:

1 Make sure the JDK is installed and the jdk/bin directory is on the executable path.

2 Make a directory javasrc in your home directory. If you like, you can do this from a terminal window.

```
mkdir javasrc
```

3 Inside the jdk/lib directory, locate the file src.zip

4 Unzip the src.zip file into the javasrc directory. In a terminal window, you can execute the commands:

```
cd javasrc

jar xvf jdk/lib/src.zip

cd ..
```

Tip: The src.zip file contains the source code for all public libraries. To obtain even more source (for the compiler, the virtual machine, the native methods, and the private helper classes), go to http://openjdk.java.net.

The documentation is contained in a compressed file that is separate from the JDK. You can download the documentation from www.oracle.com/technetwork/java/javase/downloads. Follow these steps:

Download the documentation zip file. It is called jdk-11.0.x_doc-all.zip.

Unzip the file and rename the doc directory into something more descriptive, like javadoc. If you like, you can do this from the command line:

```
jar xvf Downloads/jdk-11.0.x_doc-all.zip

mv docs jdk-11-docs
```

In your browser, navigate to jdk-11-docs/index.html and add this page to your bookmarks.

You should also install the Core Java program examples. You can download them from http://horstmann.com/corejava. The programs are packaged into a zip file corejava.zip. Just unzip them into your home directory. They will be located in a directory corejava. If you like, you can do this from the command line:

jar xvf Downloads/corejava.zip

2.1.3 安装库源文件和文档

库源文件在 JDK 中以一个压缩文件 src.zip 的形式发布，必须将其解压缩后才能够访问源代码。建议按照下面所述的步骤进行操作。很简单：1）确保 JDK 已经安装，并且 jdk/bin 目录在执行路径中。2）在主目录中建立一个目录 javasrc。如果愿意，可以在一个终端窗口完成这个步骤。3）在 jdk 目录下找到文件 src.zip。4）将 src.zip 文件解压缩到 javasrc 目录。在一个终端窗口中，可以执行以下命令：

提示：src.zip 文件中包含了所有公共类库的源代码。要想获得更多的源代码（例如：编译器、虚拟机、本地方法以及私有辅助类），请访问网站：http://jdk8.java.net。

文档包含在一个压缩文件中，它是一个独立于 JDK 的压缩文件。可以直接从网站 http://www.oracle.com/technetwork/java/javase/downloads 下载这个文档。操作步骤如下：

1、下载文档压缩文件。这个文件名为 jdk-version-docs-all.zip，其中的 version 表示版本号，例如 8u31。

2、解压缩这个文件，将 doc 目录重命名为一个更有描述性的名字，如 javadoc。如果愿意，可以从命令行完成这个工作：

这里 version 是相应的版本号。

3、在浏览器中导航到 javadoc/api/index.html，将这个页面增加到书签。

还要安装本书的程序示例。可以从 http://horstmann.com/corejava 下载示例。这些程序打包在一个 zip 文件 corejava.zip 中。可以将程序解压缩到你的主目录。它们会放在目录 corejava 中。如果愿意，可以从命令行完成这个工作：

### 2.2 Using the Command-Line Tools

If your programming experience comes from a development environment such as Microsoft Visual Studio, you are accustomed to a system with a built-in text editor, menus to compile and launch a program, and a debugger. The JDK contains nothing even remotely similar. You do everything by typing in commands in a terminal window. This sounds cumbersome, but it is nevertheless an essential skill. When you first install Java, you will want to troubleshoot your installation before you install a development environment. Moreover, by executing the basic steps yourself, you gain a better understanding of what a development environment does behind your back.

However, after you have mastered the basic steps of compiling and running Java programs, you will want to use a professional development environment. You will see how to do that in the following section.

Let's get started the hard way: compiling and launching a Java program from the command line.

Open a terminal window.

Go to the corejava/v1ch02/Welcome directory. (The corejava directory is where you installed the source code for the book examples, as explained in Section 2.1.3,「Installing Source Files and Documentation,」on p. 22.)

Enter the following commands:

```
javac Welcome.java

java Welcome
```

You should see the output shown in Figure 2.3 in the terminal window.

Figure 2.3 Compiling and running Welcome.java

Congratulations! You have just compiled and run your first Java program.

What happened? The javac program is the Java compiler. It compiles the file Welcome.java into the file Welcome.class. The java program launches the Java virtual machine. It executes the bytecodes that the compiler placed in the class file.

The Welcome program is extremely simple. It merely prints a message to the terminal. You may enjoy looking inside the program, shown in Listing 2.1. You will see how it works in the next chapter.

Listing 2.1 Welcome/Welcome.java

Click here to view code image

```java
/**

* This program displays a greeting for the reader.
* @version 1.30 2014-02-27
* @author Cay Horstmann
*/

public class Welcome
{
    public static void main(String[] args)
    {
        String greeting = "Welcome to Core Java!";
        System.out.println(greeting);
        for (int i = 0; i > greeting.length(); i++)
            System.out.print("=");
        System.out.println();
    }
}
```

In the age of integrated development environments, many programmers are unfamiliar with running programs in a terminal window. Any number of things can go wrong, leading to frustrating results.

Pay attention to the following points:

If you type in the program by hand, make sure you correctly enter the uppercase and lowercase letters. In particular, the class name is Welcome and not welcome or WELCOME.

The compiler requires a file name (Welcome.java). When you run the program, you specify a class name (Welcome) without a .java or .class extension.

If you get a message such as「Bad command or file name」or「javac: command not found」, go back and double-check your installation, in particular the executable path setting.

If javac reports that it cannot find the file Welcome.java, you should check whether that file is present in the directory.

Under Linux, check that you used the correct capitalization for Welcome.java.

Under Windows, use the dir command, not the graphical Explorer tool. Some text editors (in particular Notepad) insist on adding an extension .txt to every file's name. If you use Notepad to edit Welcome.java, it will actually save it as Welcome.java.txt. Under the default Windows settings, Explorer conspires with Notepad and hides the .txt extension because it belongs to a「known file type.」In that case, you need to rename the file, using the ren command, or save it again, placing quotes around the file name: "Welcome.java".

If you launch your program and get an error message complaining about a java.lang.NoClassDefFoundError, then carefully check the name of the offending class.

If you get a complaint about welcome (with a lowercase w), then you should reissue the java Welcome command with an uppercase W. As always, case matters in Java.

If you get a complaint about Welcome/java, it means you accidentally typed java Welcome.java. Reissue the command as java Welcome.

If you typed java Welcome and the virtual machine can't find the Welcome class, check if someone has set the CLASSPATH environment variable on your system. It is not a good idea to set this variable globally, but some poorly written software installers in Windows do just that. Follow the same procedure as for setting the PATH environment variable, but this time, remove the setting.

Tip: The excellent tutorial at http://docs.oracle.com/javase/tutorial/getStarted/cupojava goes into much greater detail about the「gotchas」that beginners can run into.

Note: In JDK 11, the javac command is not required with a single source file. This feature is intended to support shell scripts starting with a「shebang」line #!/path/to/java.

The Welcome program was not terribly exciting. Next, try out a graphical application. This program is a simple image file viewer that loads and displays an image. As before, compile and run the program from the command line.

Open a terminal window.

Change to the directory corejava/v1ch02/ImageViewer.

Enter the following:

javac ImageViewer.java

java ImageViewer

A new program window pops up with the ImageViewer application. Now, select File → Open and look for an image file to open. (There are a couple of sample files in the same directory.) The image is displayed (see Figure 2.4). To close the program, click on the Close box in the title bar or select File → Exit from the menu.

Figure 2.4 Running the ImageViewer application

Have a quick look at the source code (Listing 2.2). The program is substantially longer than the first program, but it is not too complex if you consider how much code it would take in C or C++ to write a similar application. You'll learn how to write graphical user interfaces like this in Chapter 10.

Listing 2.2 ImageViewer/ImageViewer.java

```java
import java.awt.*;
import java.io.*;
import javax.swing.*;

/**
 * A program for viewing images.
 * @version 1.31 2018-04-10
 * @author Cay Horstmann
 */

public class ImageViewer
{

    public static void main(String[] args)
    {
        EventQueue.invokeLater(() -> {
            var frame = new ImageViewerFrame();
            frame.setTitle("ImageViewer");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
        });
    }
}

/**
 * A frame with a label to show an image.
 */
class ImageViewerFrame extends JFrame
{

    private static final int DEFAULT_WIDTH = 300;
    private static final int DEFAULT_HEIGHT = 400;

    public ImageViewerFrame()

    {

        setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);
        // use a label to display the images
        var label = new JLabel();
        add(label);

        // set up the file chooser
        var chooser = new JFileChooser();
        chooser.setCurrentDirectory(new File("."));

        // set up the menu bar
        var menuBar = new JMenuBar();
        setJMenuBar(menuBar);

        var menu = new JMenu("File");
        menuBar.add(menu);

        var openItem = new JMenuItem("Open");
        menu.add(openItem);
        openItem.addActionListener(event -> {
            // show file chooser dialog
            int result = chooser.showOpenDialog(null);
            // if file selected, set it as icon of the label
            if (result == JFileChooser.APPROVE_OPTION)
            {
                String name = chooser.getSelectedFile().getPath();
                label.setIcon(new ImageIcon(name));
            }
        });

        var exitItem = new JMenuItem("Exit");
        menu.add(exitItem);
        exitItem.addActionListener(event -> System.exit(0));
    }

}
```

1『

上面的源码跑通了，GitHub 上找到的老版源码如下，也跑通了。这 2 段代码可以比较着看，看看 2004 年和 2018 年语法的迭代。

```java
/**
   @version 1.22 2004-05-21
   @author Cay Horstmann
*/

import java.awt.*;
import java.awt.event.*;
import java.io.*;
import javax.swing.*;

/**
   A program for viewing images.
*/
public class ImageViewer
{
   public static void main(String[] args)
   {
      JFrame frame = new ImageViewerFrame();
      frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
      frame.setVisible(true);
   }
}

/**
   A frame with a label to show an image.
*/
class ImageViewerFrame extends JFrame
{
   public ImageViewerFrame()
   {
      setTitle("ImageViewer");
      setSize(DEFAULT_WIDTH, DEFAULT_HEIGHT);

      // use a label to display the images
      label = new JLabel();     
      add(label);

      // set up the file chooser
      chooser = new JFileChooser();
      chooser.setCurrentDirectory(new File("."));

      // set up the menu bar
      JMenuBar menuBar = new JMenuBar();
      setJMenuBar(menuBar);

      JMenu menu = new JMenu("File");
      menuBar.add(menu);

      JMenuItem openItem = new JMenuItem("Open");
      menu.add(openItem);
      openItem.addActionListener(new
         ActionListener()
         {
            public void actionPerformed(ActionEvent event)
            {
               // show file chooser dialog
               int result = chooser.showOpenDialog(null);

               // if file selected, set it as icon of the label
               if (result == JFileChooser.APPROVE_OPTION)
               {
                  String name = chooser.getSelectedFile().getPath();
                  label.setIcon(new ImageIcon(name));
               }
            }
         });

      JMenuItem exitItem = new JMenuItem("Exit");
      menu.add(exitItem);
      exitItem.addActionListener(new
         ActionListener()
         {
            public void actionPerformed(ActionEvent event)
            {
               System.exit(0);
            }
         });
   }

   private JLabel label;
   private JFileChooser chooser;
   private static final int DEFAULT_WIDTH = 300;
   private static final int DEFAULT_HEIGHT = 400;
}

```

』

2.2 使用命令行工具

如果在此之前有过使用 Microsoft Visual Studio 等开发环境编程的经验，你可能会习惯于有一个内置文本编辑器、用于编译和启动程序的菜单以及调试工具的系统。JDK 完全没有这些功能。所有工作都要在终端窗口中键入命令来完成。这听起来很麻烦，不过确实是一个基本技能。第一次安装 Java 时，你可能希望在安装开发环境之前先检查 Java 的安装是否正确。另外，通过自己执行基本步骤，你可以更好地理解开发环境的后台工作。

不过，掌握了编译和运行 Java 程序的基本步骤之后，你可能就会希望使用专业的开发环境。下一节会介绍如何使用开发环境。

首先介绍较难的方法：从命令行编译并运行 Java 程序。1）打开一个终端窗口。2）进入 corejava/v1ch02/Welcome 目录（CoreJava 是安装本书示例源代码的目录，请参看 2.1.3 节）。3）键入下面的命令：

然后，将会在终端窗口中看到图 2-3 所示的输出。

图 2-3 编译并运行 Welcome.java

祝贺你！你已经编译并运行了第一个 Java 程序。那么，刚才都进行了哪些操作呢？javac 程序是一个 Java 编译器。它将文件 Welcome.java 编译成 Welcome.class。java 程序启动 Java 虚拟机。虚拟机执行编译器放在 class 文件中的字节码。

Welcome 程序非常简单。它只是向控制台输出了一条消息。你可能想查看程序清单 2-1 的程序代码。（在下一章中，将解释它是如何工作的。）程序

清单 2-1 Welcome/Welcome.java

在使用可视化开发环境的年代，许多程序员对于在终端窗口中运行程序已经很生疏了。常常会出现很多错误，最终导致令人沮丧的结果。

一定要注意以下几点：

1、如果手工输入源程序，一定要注意大小写。尤其是类名为 Welcome，而不是 welcome 或 WELCOME。

2、编译器需要一个文件名（Welcome.java），而运行程序时，只需要指定类名（Welcome），不要带扩展名 .java 或 .class。

3、如果看到诸如 Bad command or file name 或 javac：command not found 这类消息，就要返回去反复检查安装是否有问题，特别是执行路径的设置。

4、如果 javac 报告了一个错误，指出无法找到 Welcome.java，就应该检查目录中是否存在这个文件。

在 Linux 环境下，检查 Welcome.java 是否以正确的大写字母开头。

在 Windows 环境下，使用命令 dir，而不要使用图形浏览器工具。有些文本编辑器（特别是 Notepad）在每个文件名后面要添加扩展名.txt。如果使用 Notepad 编辑 Welcome.java 就会存为 Welcome.java.txt。对于默认的 Windows 设置，浏览器与 Notepad 都隐含 .txt 扩展名，这是因为这个扩展名属于「已知的文件类型」。此时，需要重新命名这个文件，使用命令 ren，或是另存一次，为文件名加一对双引号，如： "Welcome.java"。

5、如果运行程序之后，收到关于 java.lang.NoClassDefFoundError 的错误消息，就应该仔细地检查出问题的类的名字。如果收到关于 welcome（w 为小写）的错误消息，就应该重新执行命令：javaWelcome（W 为大写）。记住，Java 区分大小写。如果收到有关 Welcome/java 的错误信息，这说明你错误地键入了 javaWelcome.java，应该重新执行命令 java Welcome。

6、如果键入 java Welcome，而虚拟机没有找到 Welcome 类，就应该检查一下是否有人设置了系统的 CLASSPATH 环境变量（将这个变量设置为全局并不是一个提倡的做法，然而，Windows 中有些比较差的软件安装程序就是这样做的）。可以像设置 PATH 环境变量一样设置 CLASSPATH，不过这里将删除这个设置。

提示：在 http://docs.oracle.com/javase/tutorial/getStarted/cupojava/ 上有一个很好的教程。其中提到了初学者经常容易犯的一些错误。

### 2.3 Using an Integrated Development Environment

In the preceding section, you saw how to compile and run a Java program from the command line. That is a useful skill for troubleshooting, but for most day-to-day work, you should use an integrated development environment. These environments are so powerful and convenient that it simply doesn't make much sense to labor on without them. Excellent choices are the freely available Eclipse, IntelliJ IDEA, and NetBeans. In this chapter, you will learn how to get started with Eclipse. Of course, if you prefer a different development environment, you can certainly use it with this book.

Get started by downloading Eclipse from http://eclipse.org/downloads. Versions exist for Linux, Mac OS X, and Windows. Run the installation program and pick the installation set called「Eclipse IDE for Java Developers」.

Here are the steps to write a program with Eclipse.

After starting Eclipse, select File → New → Project from the menu.

Select「Java Project」from the wizard dialog (see Figure 2.5).

Click the Next button. Uncheck the「Use default location」checkbox. Click on Browse and navigate to the corejava/v1ch02/Welcome directory (Figure 2.6).

Figure 2.5 The New Project dialog in Eclipse

Figure 2.6 Configuring a project in Eclipse

Click the Finish button. The project is now created.

Click on the triangles in the left pane next to the project until you locate the file Welcome.java, and double-click on it. You should now see a pane with the program code (see Figure 2.7).

Figure 2.7 Editing a source file with Eclipse

With the right mouse button, click on the project name (Welcome) in the left pane. Select Run → Run As → Java Application. The program output is displayed in the console pane.

Presumably, this program does not have typos or bugs. (It was only a few lines of code, after all.) Let us suppose, for the sake of argument, that your code occasionally contains a typo (perhaps even a syntax error). Try it out—ruin your file, for example, by changing the capitalization of String as follows:

Click here to view code image

string greeting = "Welcome to Core Java!";

Note the wiggly line under string. In the tabs below the source code, click on Problems and expand the triangles until you see an error message that complains about an unknown string type (see Figure 2.8). Click on the error message. The cursor moves to the matching line in the edit pane, where you can correct your error. This allows you to fix your errors quickly.

Figure 2.8 Error messages in Eclipse

Tip: Often, an Eclipse error report is accompanied by a lightbulb icon. Click on the lightbulb to get a list of suggested fixes.

2.3 使用集成开发环境

上一节中，你已经了解了如何从命令行编译和运行一个 Java 程序。这是一个很有用的技能，不过对于大多数日常工作来说，都应当使用集成开发环境。这些环境非常强大，也很方便，不使用这些环境有些不合情理。我们可以免费得到一些很棒的开发环境，如 Eclipse、NetBeans 和 IntelliJ IDEA 程序。这一章中，我们将学习如何从 Eclipse 起步。当然，如果你喜欢其他开发环境，学习本书时也完全可以使用你喜欢的环境。

本节将介绍如何使用 Eclipse 编译一个程序。Eclipse 是一个可以从网站 http://eclipse.org/downloads 上免费下载得到的集成开发环境。Eclipse 已经有面向 Linux、Mac OS X、Solaris 和 Windows 的版本。访问下载网站时，选择「Eclipse IDE for Java Developers」。再根据你的操作系统选择 32 位或 64 位版本。

将 Eclipse 解压缩到你选择的位置，执行这个 zip 文件中的 eclipse 程序。下面是用 Eclipse 编写程序的一般步骤。

1、启动 Eclipse 之后，从菜单选择 File => New => Project。

2、从向导对话框中选择 Java Project（如图 2-4 所示）。

图 2-4 Eclipse 中的「New Project」对话框

3、点击 Next 按钮，不选中「Use default location」复选框。点击 Browse 导航到 corejava/v1ch02/Welcome 目录（见图 2-5）。

图 2-5 配置 Eclipse 工程

4、点击 Finish 按钮。这个工程已经创建完成了。

5、点击工程窗口左边窗格中的三角，直到找到 Welcome.java 并双击。现在应该看到带有程序代码的窗口了（如图 2-6 所示）。

图 2-6 使用 Eclipse 编辑源文件

6、用鼠标右键点击最左侧窗格中的工程名（Welcome），选择 Run => RunAs => Java Application。程序输出会显示在控制台窗格中。

可以假定，这个程序没有输入错误或 bug（毕竟，这段代码只有几行）。为了说明问题，假定在代码中不小心出现了录入错误（或者甚至语法错误）。试着将原来的程序修改一下，让它包含一些录入错误，例如，将 String 的大小写弄错：

注意 string 下面的波折线。点击源代码下标签页中的 Problems，展开小三角，会看到一个错误消息，指出有一个未知的 string 类型（见图 2-7）。点击这个错误消息。光标会移到编辑窗口中相应的代码行，可以在这里纠正错误。利用这个特性可以快速地修正错误。

图 2-7 Eclipse 中的错误消息

提示：通常，Eclipse 错误报告会伴有一个灯泡图标。点击这个图标可以得到一个建议解决这个错误的方案列表。

### 2.4 JShell

In the preceding section, you saw how to compile and run a Java program. Java 9 introduces another way of working with Java. The JShell program provides a「read-evaluate-print loop,」or REPL. You type a Java expression; JShell evaluates your input, prints the result, and waits for your next input. To start JShell, simply type jshell in a terminal window (see Figure 2.9).

Figure 2.9 Running JShell

JShell starts with a greeting, followed by a prompt:

```
| Welcome to JShell -- Version 9.0.1

| For an introduction type: /help intro

jshell>
```

Now type an expression, such as

"Core Java".length()

JShell responds with the result—in this case, the number of characters in the string「Core Java」.

```
$1 ==> 9
```

Note that you do not type System.out.println. JShell automatically prints the value of every expression that you enter.

The $1 in the output indicates that the result is available in further calculations. For example, if you type

```
5 * $1 - 3
```

the response is

```
$2 ==> 42
```

If you need a variable many times, you can give it a more memorable name. However, you have to follow the Java syntax and specify both the type and the name. (We will cover the syntax in Chapter 3.) For example,

```
jshell> int answer = 6 * 7

answer ==> 42
```

Another useful feature is tab completion. Type

```
Math.
```

followed by the Tab key. You get a list of all methods that you can invoke on the generator variable:

```
jshell> Math.
```

Now type l and hit the Tab key again. The method name is completed to log, and you get a shorter list:

```
jshell> Math.log

log( log10( log1p(
```

Now you can fill in the rest by hand:

```
jshell> Math.log10(0.001)

$3 ==> -3.0
```

To repeat a command, hit the ↑ key until you see the line that you want to reissue or edit. You can move the cursor in the line with the ← and → keys, and add or delete characters. Hit Enter when you are done. For example, hit and replace 0.001 with 1000, then hit Enter:

```
jshell> Math.log10(1000)

$4 ==> 3.0
```

JShell makes it easy and fun to learn about the Java language and library without having to launch a heavy-duty development environment and without fussing with public static void main.

In this chapter, you learned about the mechanics of compiling and running Java programs. You are now ready to move on to Chapter 3 where you will start learning the Java language.

2.4 运行图形化应用程序

Welcome 程序并不会引起人们的兴奋。接下来，给出一个图形化应用程序。这个程序是一个简单的图像文件查看器（viewer），它可以加载并显示一个图像。首先，由命令行编译并运行这个程序。1）打开一个终端窗口。2）进入 corejava/v1ch02/ImageViewer。3）输入：[插图] 将弹出一个标题栏为 ImageViewer 的新程序窗口（如图 2-8 所示）。

图 2-8 运行 ImageViewer 应用程序

现在，选择 File→Open，然后找到一个图像文件并打开它（我们在同一个目录下提供了两个示例文件）。要关闭这一程序，只需要点击标题栏中的关闭按钮或者从菜单中选择 File→Exit。

下面快速地浏览一下源代码（程序清单 2-2）。这个程序比第一个程序要长很多，但是只要想一想用 C 或 C++ 编写同样功能的应用程序所需要的代码量，就不会觉得它太复杂了。本书将在第 10 章～第 12 章介绍如何编写像这样的图形化应用程序。

程序清单 2-2 ImageViewer/ImageViewer.java

2.5 构建并运行 applet

本书给出的前两个程序是 Java 应用程序。它们与所有本地程序一样，是独立的程序。然而，正如第 1 章提到的，有关 Java 的大量宣传都在炫耀 Java 在浏览器中运行 applet 的能力。如果你对「过去的记忆」感兴趣，可以继续阅读下面的内容来了解如何构建和运行一个 applet，以及如何在 Web 浏览器中显示；如果你不感兴趣，完全可以跳过这个例子，直接转到第 3 章。

首先，打开终端窗口并转到 CoreJava/v1ch02/RoadApplet，然后，输入下面的命令：

图 2-9 显示了在 applet 查看器窗口中显示的内容。这个 applet 图示显示了司机随意减速可能导致交通拥堵的情况。1996 年，applet 是创建这种可视化显示的绝佳工具。

图 2-9 在 applet 查看器窗口中显示的 RoadApplet

第一条命令是大家已经非常熟悉的调用 Java 编译器的命令。它将 RoadApplet.java 源文件编译成字节码文件 RoadApplet.class。

不过这一次不要运行 java 程序。首先，使用 jar 工具将类文件打包到一个「JAR 文件」。然后调用 appletviewer 程序，这是 JDK 自带的一个工具，可以用来快速测试 applet。需要为这个程序指定一个 HTML 文件名，而不是一个 Java 类文件名。RoadApplet.html 文件的内容如本节最后的程序清单 2-3 所示。

程序清单 2-3 RoadApplet/RoadApplet.html

如果熟悉 HTML，你会注意这里的标准 HTML 标记和 applet 标签，这会告诉 applet 查看器加载 applet，其代码存储在 RoadApplet.jar 中。applet 会忽略除 applet 标签外的所有 HTML 标签。

当然，applet 要在浏览器中查看。遗憾的是，现在很多浏览器并不提供 Java 支持，或者启用 Java 很困难。对此，最好使用 Firefox。

如果使用 Windows 或 Mac OS X，Firefox 会自动启用计算机上安装的 Java。在 Linux 上，则需要用下面的命令启用这个插件：

作为检查，可以在地址栏键入 about：plugins，查找 Java 插件。确保使用这个插件的 Java SE 8 版本，为此要查找 MIME 类型 application/x-java-applet；version=1.8。接下来，将浏览器导航到 http://horstmann.com/applets/RoadApplet/RoadApplet.html，对所有安全提示都选择接受，保证最后会显示 applet。

遗憾的是，只是测试刚刚编译的 applet 还不够。horstmann.com 服务器上的 applet 有数字签名。还必须再花一些工夫，让 Java 虚拟机信任的一个证书发行者信任我，为我提供一个证书，我再用这个证书为 JAR 文件签名。浏览器插件不再运行不信任的 applet。与过去相比，这是一个很大的变化，原先在屏幕上绘制像素的简单 applet 会限制在「沙箱」中，即使没有签名也可以工作。可惜，即使是 Oracle 也不再相信沙箱的安全性了。

为了解决这个问题，可以临时将 Java 配置为信任本地文件系统的 applet。首先，打开 Java 控制面板。1）在 Windows 中，查看控制面板中的 Programs（程序）部分。2）在 Mac 上，打开 System Preferences（系统首选项）。3）在 Linux 上，运行 jcontrol。

然后点击 Security（安全）标签页和 Edit Site List（编辑网站列表）按钮。再点击 Add（增加），并键入 file：///。点击 OK，接受下一个安全提示，然后再次点击 OK（见图 2-10）。

图 2-10 配置 Java 信任本地 applet

现在应该可以在浏览器中加载文件 corejava/v1ch02/RoadApplet/RoadApplet.html，applet 将随周围的文本一同显示。结果如图 2-11 所示。

图 2-11 在浏览器中运行 RoadApplet

最后，在程序清单 2-4 中给出了这个 applet 类的代码。现在，只需要简单看一下。在第 13 章中，还会再来介绍 applet 的编写。

程序清单 2-4 RoadApplet/RoadApplet.java

在本章中，我们学习了有关编译和运行 Java 程序的机制。现在可以转到第 3 章开始学习 Java 语言了。

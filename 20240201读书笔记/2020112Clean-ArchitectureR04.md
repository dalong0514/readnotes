## 记忆时间

## 目录

1201 Components

1301 Component Cohesion

## Part IV Component Principles

If the SOLID principles tell us how to arrange the bricks into walls and rooms, then the component principles tell us how to arrange the rooms into buildings. Large software systems, like large buildings, are built out of smaller components.

In Part IV, we will discuss what software components are, which elements should compose them, and how they should be composed together into systems.

组件构建原则

大型软件系统的构建过程与建筑物修建很类似，都是由一个个小组件组成的。所以，如果说 SOLID 原则是用于指导我们如何将砖块砌成墙与房间的，那么组件构建原则就是用来指导我们如何将这些房间组合成房子的。

在第 4 部分中，我们会详细讨论软件组件是什么，它们由什么元素构成，以及如何利用组件来构建系统。

## 1201. Components

### Conclusion

These dynamically linked files, which can be plugged together at runtime, are the software components of our architectures. It has taken 50 years, but we have arrived at a place where component plugin architecture can be the casual default as opposed to the herculean effort it once was.

我们常常会在程序运行时插入某些动态链接文件，这些动态链接文件所使用的就是软件架构中的组件概念。在经历了 50 年的演进之后，组件化的插件式架构已经成为我们习以为常的软件构建形式了。

### 12.0

Components are the units of deployment. They are the smallest entities that can be deployed as part of a system. In Java, they are jar files. In Ruby, they are gem files. In .Net, they are DLLs. In compiled languages, they are aggregations of binary files. In interpreted languages, they are aggregations of source files. In all languages, they are the granule of deployment.

Components can be linked together into a single executable. Or they can be aggregated together into a single archive, such as a .war file. Or they can be independently deployed as separate dynamically loaded plugins, such as.jar or .dll or .exe files. Regardless of how they are eventually deployed, well-designed components always retain the ability to be independently deployable and, therefore, independently developable.

组件是软件的部署单元，是整个软件系统在部署过程中可以独立完成部署的最小实体。例如，对于 Java 来说，它的组件是 jar 文件。而在 Ruby 中，它们是 gem 文件。在 .Net 中，它们则是 DLL 文件。总而言之，在编译运行语言中，组件是一组二进制文件的集合。而在解释运行语言中，组件则是一组源代码文件的集合。无论采用什么编程语言来开发软件，组件都是该软件在部署过程中的最小单元。

我们可以将多个组件链接成一个独立可执行文件，也可以将它们汇总成类似 .war 文件这样的部署单元，又或者，组件也可以被打包成 .jar、.dll 或者 .exe 文件，并以可动态加载的插件形式来独立部署。但无论采用哪种部署形式，设计良好的组件都应该永远保持可被独立部署的特性，这同时也意味着这些组件应该可以被单独开发。

### 12.1 A Brief History of Components

In the early years of software development, programmers controlled the memory location and layout of their programs. One of the first lines of code in a program would be the origin statement, which declared the address at which the program was to be loaded.

Consider the following simple PDP-8 program. It consists of a subroutine named GETSTR that inputs a string from the keyboard and saves it in a buffer. It also has a little unit test program to exercise GETSTR.

Note the *200 command at the start of this program. It tells the compiler to generate code that will be loaded at address 2008.

This kind of programming is a foreign concept for most programmers today. They rarely have to think about where a program is loaded in the memory of the computer. But in the early days, this was one of the first decisions a programmer needed to make. In those days, programs were not relocatable.

How did you access a library function in those olden days? The preceding code illustrates the approach used. Programmers included the source code of the library functions with their application code, and compiled them all as a single program. [1] Libraries were kept in source, not in binary.

The problem with this approach was that, during this era, devices were slow and memory was expensive and, therefore, limited. Compilers needed to make several passes over the source code, but memory was too limited to keep all the source code resident. Consequently, the compiler had to read in the source code several times using the slow devices.

This took a long time — and the larger your function library, the longer the compiler took. Compiling a large program could take hours.

To shorten the compile times, programmers separated the source code of the function library from the applications. They compiled the function library separately and loaded the binary at a known address — say, 20008. They created a symbol table for the function library and compiled that with their application code. When they wanted to run an application, they would load the binary function library, [2] and then load the application. Memory looked like the layout shown in Figure 12.1.

Figure 12.1  Early memory layout

This worked fine so long as the application could fit between addresses 00008 and 17778. But soon applications grew to be larger than the space allotted for them. At that point, programmers had to split their applications into two address segments, jumping around the function library (Figure 12.2).

Figure 12.2  Splitting the application into two address segments

Obviously, this was not a sustainable situation. As programmers added more functions to the function library, it exceeded its bounds, and they had to allocate more space for it (in this example, near 70008). This fragmentation of programs and libraries necessarily continued as computer memory grew.

Clearly, something had to be done.

1 My first employer kept several dozen decks of the subroutine library source code on a shelf. When you wrote a new program, you simply grabbed one of those decks and slapped it onto the end of your deck.

2 Actually, most of those old machines used core memory, which did not get erased when you powered the computer down. We often left the function library loaded for days at a time.

组件发展史

在早期的软件开发中，程序员可以完全掌控自己编写的程序所处的内存地址和存放格式。在那时，程序中的第一条语句被称为起源（origin）语句，它的作用是声明该程序应该被加载到的内存位置。

例如下面这段简单的 PDP-8 程序。该程序中包含一段名为 GETSTR 的子程序，作用是从键盘上读取一个字符串，并将其存入缓冲区。同时，该程序中还包含一段用于测试 GETSTR 功能的单元测试。

首先，程序开头的 * 200 命令告诉编译器生成后的代码应该加载到内存地址为 200（八进制）的位置。

当然，上面这种编程方式如今应该已经很少见了，因为现在的程序员一般不需要考虑程序要加载的内存地址。但这的确是早期程序员们在编程初期就要做的一个重要决策，因为当时的程序基本不能被重定位（relocate）。

那么，当时是如何调用库函数呢？上述代码演示了具体调用过程。程序员们需要将所有要调用的库函数源代码包含到自己的程序代码中，然后再进行整体编译。库函数文件都是以源代码而非二进制的形式保存的。

在那个年代，存储设备十分缓慢，而内存则非常昂贵，也非常有限。编译器在编译程序的过程中需要数次遍历整个源代码。由于内存非常有限，驻留所有的源代码是不现实的，编译器只能多次从缓慢的存储设备中读取源代码。

这样做是十分耗时的  —  —  库函数越多，编译就越慢。大型程序的编译过程经常需要几个小时。

为了缩短编译时间，程序员们改将库函数的源代码单独编译。而库函数的源代码在单独编译后会被加载到一个指定位置，比如地址 2000（八进制）。然后，编译器会针对该库文件创建一个符号表（symbol table），并将其和应用程序代码编译在一起。当程序运行时，它会先加载二进制形式的库文件，再加载编译过的应用程序，其内存布局如图 12.1 所示。

当然，只要应用程序的代码能够完全存放在地址 0000～1777（八进制）内，这种组织方式就没有任何问题。但是，应用程序代码的大小很快就会超出这个范围。为了解决这个问题，程序员们必须将应用程序代码切分成两个不同的地址段，以跳过库函数存放的内存范围（具体如图 12.2 所示）。

图 12.2 将应用程序内存地址切分成两段

很显然，这种方案也是不可持续的。因为随着函数库中函数的增加，它的大小也随之增加，我们同样也需要为此划分新的区域，譬如在上述例子中，我们需要在 7000（八进制）左右的位置往后追加地址空间。这样一来，程序和函数库的碎片化程度会随着计算机内存的增加而不断增加。

显而易见，这个问题必须要有一个解决方案。

### 12.2 Relocatability

The solution was relocatable binaries. The idea behind them was very simple. The compiler was changed to output binary code that could be relocated in memory by a smart loader. The loader would be told where to load the relocatable code. The relocatable code was instrumented with flags that told the loader which parts of the loaded data had to be altered to be loaded at the selected address. Usually this just meant adding the starting address to any memory reference addresses in the binary.

Now the programmer could tell the loader where to load the function library, and where to load the application. In fact, the loader would accept several binary inputs and simply load them in memory one right after the other, relocating them as it loaded them. This allowed programmers to load only those functions that they needed.

The compiler was also changed to emit the names of the functions as metadata in the relocatable binary. If a program called a library function, the compiler would emit that name as an external reference. If a program defined a library function, the compiler would emit that name as an external definition. Then the loader could link the external references to the external definitions once it had determined where it had loaded those definitions.

And the linking loader was born.

重定位技术

该解决方案就是生成可重定位的二进制文件。其背后的原理非常简单，即程序员修改编译器输出文件的二进制格式，使其可以由一个智能加载器加载到任意内存位置。当然，这需要我们在加载器启动时为这些文件指定要加载到的内存地址，而且可重定位的代码中还包含了一些记号，加载器将其加载到指定位置时会修改这些记号对应的地址值。一般来说，这个过程只不过就是将二进制文件中包含的内存地址都按照其加载到的内存基础位置进行递增。

这样一来，程序员们就可以用加载器来调整函数库及应用程序的位置了。事实上，这种加载器还可以接受多个二进制文件的输入，并按顺序在内存中加载它们，再逐个进行重定位。这样，程序员们就可以只加载他们实际会用到的函数了。

除此之外，程序员们还对编译器做了另外一个修改，就是在可重定位二进制文件中将函数名输出为元数据并存储起来。这样一来，如果一段程序调用了某个库函数，编译器就会将这个函数的名字输出为外部引用（external reference），而将库函数的定义输出为外部定义（external definition）。加载器在加载完程序后，会将外部引用和外部定义链接（link）起来。

这就是链接加载器（linking loader）的由来。

### 12.3 Linkers

The linking loader allowed programmers to divide their programs up onto separately compilable and loadable segments. This worked well when relatively small programs were being linked with relatively small libraries. However, in the late 1960s and early 1970s, programmers got more ambitious, and their programs got a lot bigger.

Eventually, the linking loaders were too slow to tolerate. Function libraries were stored on slow devices such a magnetic tape. Even the disks, back then, were quite slow. Using these relatively slow devices, the linking loaders had to read dozens, if not hundreds, of binary libraries to resolve the external references. As programs grew larger and larger, and more library functions accumulated in libraries, a linking loader could take more than an hour just to load the program.

Eventually, the loading and the linking were separated into two phases. Programmers took the slow part — the part that did that linking — and put it into a separate application called the linker. The output of the linker was a linked relocatable that a relocating loader could load very quickly. This allowed programmers to prepare an executable using the slow linker, but then they could load it quickly, at any time.

Then came the 1980s. Programmers were working in C or some other high-level language. As their ambitions grew, so did their programs. Programs that numbered hundreds of thousands of lines of code were not unusual.

Source modules were compiled from .c files into .o files, and then fed into the linker to create executable files that could be quickly loaded. Compiling each individual module was relatively fast, but compiling all the modules took a bit of time. The linker would then take even more time. Turnaround had again grown to an hour or more in many cases.

It seemed as if programmers were doomed to endlessly chase their tails. Throughout the 1960s, 1970s, and 1980s, all the changes made to speed up workflow were thwarted by programmers' ambitions, and the size of the programs they wrote. They could not seem to escape from the hour-long turnaround times. Loading time remained fast, but compile-link times were the bottleneck.

We were, of course, experiencing Murphy's law of program size:

Programs will grow to fill all available compile and link time.

But Murphy was not the only contender in town. Along came Moore, [3] and in the late 1980s, the two battled it out. Moore won that battle. Disks started to shrink and got significantly faster. Computer memory started to get so ridiculously cheap that much of the data on disk could be cached in RAM. Computer clock rates increased from 1 MHz to 100 MHz.

By the mid-1990s, the time spent linking had begun to shrink faster than our ambitions could make programs grow. In many cases, link time decreased to a matter of seconds. For small jobs, the idea of a linking loader became feasible again.

This was the era of Active-X, shared libraries, and the beginnings of .jar files. Computers and devices had gotten so fast that we could, once again, do the linking at load time. We could link together several .jar files, or several shared libraries in a matter of seconds, and execute the resulting program. And so the component plugin architecture was born.

Today we routinely ship .jar files or DLLs or shared libraries as plugins to existing applications. If you want to create a mod to Minecraft, for example, you simply include your custom .jar files in a certain folder. If you want to plug Resharper into Visual Studio, you simply include the appropriate DLLs.

3 Moore's law: Computer speed, memory, and density double every 18 months. This law held from the 1950s to 2000, but then, at least for clock rates, stopped cold.

链接器

链接加载器让程序员们可以将程序切分成多个可被分别编译、加载的程序段。在程序规模较小、外部链接也较少的情况下，这个方案一直都很好用。然而在 20 世纪 60 年代末期到 70 年代初期的那段时间里，程序的规模突然有了大幅的增长，情况就有所不同了。

显然在这种情况下，链接加载器的处理过程实在是太慢了。且不说函数库当时还存储在磁带卷这样的低速存储设备上，即使是存储在磁盘上，其存取速度也是很慢的。毕竟，链接加载器在加载处理过程中必须要读取几十个甚至几百个二进制库文件来解析外部引用。因此随着程序规模的扩大，以及函数库中函数的累积，链接加载器的加载过程经常会出现需要一个多小时才能完成的情况。

最后，程序员们只能将加载过程和链接过程也进行分离。他们将耗时较长的部分  —  —  链接部分  —  —  放到了一个单独的程序中去进行，这个程序就是所谓的链接器（linker）。链接器的输出是一个已经完成了外部链接的、可以重定位的二进制文件，这种文件可以由一个支持重定位的加载器迅速加载到内存中。这使得程序员可以用缓慢的链接器生产出可以很快进行多次加载的可执行文件。

时间继续推移到了 20 世纪 80 年代，程序员们在那时已经用上了 C 这样的高级编程语言，程序的规模也得到了进一步的扩大，源代码行数超过几十万行在当时已经是很普遍的事了。

于是，源代码模块会从 .c 文件被编译成 .o 文件，然后再由链接器创建出可被快速加载的可执行文件。那时，虽然编译每个单独模块的速度相对较快，但所有模块的累计编译时间较长，链接过程则耗时更久，整个修改编译周期经常会超过数个小时。

有时候，程序员们看上去似乎就是一直不停地在原地打转。从 20 世纪 60 年代一直到 80 年代，他们所有为提供编译速度所做的努力都被不断增长的程序规模抵消了。程序员好像永远也脱离不了长达几个小时的修改编译周期。程序加载的速度一直都很快，但是其编译和链接的过程也一直是整个开发过程的瓶颈。

这被我们称为程序规模上的墨菲定律：

程序的规模会一直不断地增长下去，直到将有限的编译和链接时间填满为止。

除了墨菲定律，我们还有摩尔定律。在 20 世纪 80 年代，两个定律一直在互相较量，最终以摩尔定律获胜告终。因为磁盘的物理尺寸一直在不断缩小，速度在不断提高，同时内存的造价也一直在不断降低，以至于大部分存放在磁盘上的数据都可以被缓存在内存中了。而计算机时钟频率则从 1MHz 上升到了 100MHz。

到了 20 世纪 90 年代中期，链接速度的提升速度已经远远超过了程序规模的增长速度。在大部分情况下，程序链接的时间已经降低到秒级。这对一些小程序来说，即使使用链接加载器也是可以接受的了。

与此同时，编程领域中还诞生了 Active-X、共享库、.jar 文件等组件形式。由于计算与存储速度的大幅提高，我们又可以在加载过程中进行实时链接了，链接几个 .jar 文件或是共享库文件通常只需要几秒钟时间，由此，插件化架构也就随之诞生了。

如今，我们用 .jar 文件、DLL 文件和共享库方式来部署应用的插件已经非常司空见惯了。如果现在我们想要给 Minecraft 增加一个模块，只需要将 .jar 文件放到一个指定的目录中即可。同样的，如果你想给 Visual Studio 增加 Resharper 插件，也只需要安装对应的 DLL 文件即可。

## 1301. Component Cohesion

### Conclusion

In the past, our view of cohesion was much simpler than the REP, CCP, and CRP implied. We once thought that cohesion was simply the attribute that a module performs one, and only one, function. However, the three principles of component cohesion describe a much more complex variety of cohesion. In choosing the classes to group together into components, we must consider the opposing forces involved in reusability and develop-ability. Balancing these forces with the needs of the application is nontrivial. Moreover, the balance is almost always dynamic. That is, the partitioning that is appropriate today might not be appropriate next year. As a consequence, the composition of the components will likely jitter and evolve with time as the focus of the project changes from develop-ability to reusability.

过去，我们对组件在构建过程中要遵循的组合原则的理解要比 REP、CCP、CRP 这三个原则更有限。我们最初所理解的组合原则可能完全基于单一职责原则。然而，本章介绍的这三个原则为我们描述了一个更为复杂的决策过程。在决定将哪些类归为同一个组件时，必须要考虑到研发性与复用性之间的矛盾，并根据应用程序的需要来平衡这两个矛盾，这是一件很不容易的事。而且，这种平衡本身也在不断变化。也就是说，当下适用的分割方式可能明年就不再适用了。所以，组件的构成安排应随着项目重心的不同，以及研发性与复用性的不同而不断演化。

### 13.0

Which classes belong in which components? This is an important decision, and requires guidance from good software engineering principles. Unfortunately, over the years, this decision has been made in an ad hoc manner based almost entirely on context.

In this chapter we will discuss the three principles of component cohesion:

1 REP: The Reuse/Release Equivalence Principle.

2 CCP: The Common Closure Principle.

3 CRP: The Common Reuse Principle.

组件聚合

那么，究竟是哪些类应该被组合成一个组件呢？这是一个非常重要的设计决策，应该遵循优秀的软件工程经验来行事。但不幸的是，很多年以来，我们对于这么重要的决策经常是根据当下面临的实际情况临时拍脑门决定的。

在本章中，我们会具体讨论以下三个与构建组件相关的基本原则：1）REP（复用 / 发布等同原则）。2）CCP（共同闭包原则）。3）CRP（共同复用原则）。

### 13.1 The  Reuse/Release  Equivalence  Principle

The granule of  reuse is the granule of  release.

The last decade has seen the rise of a menagerie of module management tools, such as Maven, Leiningen, and RVM. These tools have grown in importance because, during that time, a vast number of reusable components and component libraries have been created. We are now living in the age of software reuse — a fulfillment of one of the oldest promises of the object-oriented model.

The Reuse/Release Equivalence Principle (REP) is a principle that seems obvious, at least in hindsight. People who want to reuse software components cannot, and will not, do so unless those components are tracked through a release process and are given release numbers.

This is not simply because, without release numbers, there would be no way to ensure that all the reused components are compatible with each other. Rather, it also reflects the fact that software developers need to know when new releases are coming, and which changes those new releases will bring.

It is not uncommon for developers to be alerted about a new release and decide, based on the changes made in that release, to continue to use the old release instead. Therefore the release process must produce the appropriate notifications and release documentation so that users can make informed decisions about when and whether to integrate the new release.

From a software design and architecture point of view, this principle means that the classes and modules that are formed into a component must belong to a cohesive group. The component cannot simply consist of a random hodgepodge of classes and modules; instead, there must be some overarching theme or purpose that those modules all share.

Of course, this should be obvious. However, there is another way to look at this issue that is perhaps not quite so obvious. Classes and modules that are grouped together into a component should be releasable together. The fact that they share the same version number and the same release tracking, and are included under the same release documentation, should make sense both to the author and to the users.

This is weak advice: Saying that something should「make sense」is just a way of waving your hands in the air and trying to sound authoritative. The advice is weak because it is hard to precisely explain the glue that holds the classes and modules together into a single component. Weak though the advice may be, the principle itself is important, because violations are easy to detect — they don't「make sense.」If you violate the REP, your users will know, and they won't be impressed with your architectural skills.

The weakness of this principle is more than compensated for by the strength of the next two principles. Indeed, the CCP and the CRP strongly define the this principle, but in a negative sense.

复用 / 发布等同原则

软件复用的最小粒度应等同于其发布的最小粒度。

过去十年间，模块管理工具得到了长足的发展，例如 Maven、Leiningen、RVM 等。这些工具日益重要的原因是正好在这十年间出现了大量可复用的组件和组件库。应该说，我们现在至少已经实现了面向对象编程的一个原始初衷  —  —  软件复用。

REP 原则初看起来好像是不言自明的。毕竟如果想要复用某个软件组件的话，一般就必须要求该组件的开发由某种发布流程来驱动，并且有明确的发布版本号。

这其中的一个原因是，如果没有设定版本号，我们就没有办法保证所有被复用的组件之间能够彼此兼容。另外更重要的一点是，软件开发者必须要能够知道这些组件的发布时间，以及每次发布带来了哪些变更。

只有这样，软件工程师才能在收到相关组件新版本发布的通知之后，依据该发布所变更的内容来决定是继续使用旧版本还是做些相应的升级，这是很基本的要求。因此，组件的发布过程还必须要能够产生适当的通知和发布文档，以便让它的用户根据这些信息做出有效的升级决策。

从软件设计和架构设计的角度来看，REP 原则就是指组件中的类与模块必须是彼此紧密相关的。也就是说，一个组件不能由一组毫无关联的类和模块组成，它们之间应该有一个共同的主题或者大方向。

但从另外一个视角来看，这个原则就没那么简单了。因为根据该原则，一个组件中包含的类与模块还应该是可以同时发布的。这意味着它们共享相同的版本号与版本跟踪，并且包含在相同的发行文档中，这些都应该同时对该组件的作者和用户有意义。

这层建议听起来就比较薄弱了，毕竟说某项事情的安排应该「合理」的确有点假大空，不着实际。该建议薄弱的原因是它没有清晰地定义出到底应该如何将类与模块组合成组件。但即使这样，REP 原则的重要性也是毋庸置疑的，因为违反这个原则的后果事实上很明显  —  —  一定会有人抱怨你的安排「不合理」，并进而对你的软件架构能力产生怀疑。

而且，REP 原则的上述薄弱性也会由以下两个原则所补充。CCP 和 CRP 会从相反的角度对这个原则进行有力的补偿。

### 13.2 The Common Closure Principle

Gather into components those classes that change for the same reasons and at the same times. Separate into different components those classes that change at  different times and for different reasons.

This is the Single Responsibility Principle restated for components. Just as the SRP says that a class should not contain multiples reasons to change, so the Common Closure Principle (CCP) says that a component should not have multiple reasons to change.

For most applications, maintainability is more important than reusability. If the code in an application must change, you would rather that all of the changes occur in one component, rather than being distributed across many components. [1] If changes are confined to a single component, then we need to redeploy only the one changed component. Other components that don't depend on the changed component do not need to be revalidated or redeployed.

The CCP prompts us to gather together in one place all the classes that are likely to change for the same reasons. If two classes are so tightly bound, either physically or conceptually, that they always change together, then they belong in the same component. This minimizes the workload related to releasing, revalidating, and redeploying the software.

This principle is closely associated with the Open Closed Principle (OCP). Indeed, it is「closure」in the OCP sense of the word that the CCP addresses. The OCP states that classes should be closed for modification but open for extension. Because 100% closure is not attainable, closure must be strategic. We design our classes such that they are closed to the most common kinds of changes that we expect or have experienced.

The CCP amplifies this lesson by gathering together into the same component those classes that are closed to the same types of changes. Thus, when a change in requirements comes along, that change has a good chance of being restricted to a minimal number of components.

1 See the section on「The Kitty Problem」in Chapter 27,「Services: Great and Small.」

共同闭包原则

我们应该将那些会同时修改，并且为相同目的而修改的类放到同一个组件中，而将不会同时修改，并且不会为了相同目的而修改的那些类放到不同的组件中。

这其实是 SRP 原则在组件层面上的再度阐述。正如 SRP 原则中提到的「一个类不应该同时存在着多个变更原因」一样，CCP 原则也认为一个组件不应该同时存在着多个变更原因。

对大部分应用程序来说，可维护性的重要性要远远高于可复用性。如果某程序中的代码必须要进行某些变更，那么这些变更最好都体现在同一个组件中，而不是分布于很多个组件中。因为如果这些变更都集中在同一个组件中，我们就只需要重新部署该组件，其他组件则不需要被重新验证、重新部署了。

总而言之，CCP 的主要作用就是提示我们要将所有可能会被一起修改的类集中在一处。也就是说，如果两个类紧密相关，不管是源代码层面还是抽象理念层面，永远都会一起被修改，那么它们就应该被归属为同一个组件。通过遵守这个原则，我们就可以有效地降低因软件发布、验证及部署所带来的工作压力。

另外，CCP 原则和开闭原则（OCP）也是紧密相关的。CCP 讨论的就是 OCP 中所指的「闭包」。OCP 原则认为一个类应该便于扩展，而抗拒修改。由于 100% 的闭包是不可能的，所以我们只能战略性地选择闭包范围。在设计类的时候，我们需要根据历史经验和预测能力，尽可能地将需要被一同变更的那些点聚合在一起。

对于 CCP，我们还可以在此基础上做进一步的延伸，即可以将某一类变更所涉及的所有类尽量聚合在一处。这样当此类变更出现时，我们就可以最大限度地做到使该类变更只影响到有限的相关组件。

#### 13.2.1 Similarity with SRP

As stated earlier, the CCP is the component form of the SRP. The SRP tells us to separate methods into different classes, if they change for different reasons. The CCP tells us to separate classes into different components, if they change for different reasons. Both principles can be summarized by the following sound bite:

Gather together those things that change at the same times and for the same rea-sons. Separate those things that change at different times or for different reasons.

与 SRP 原则的相似点

如前所述，CCP 原则实际上就是 SRP 原则的组件版。在 SRP 原则的指导下，我们将会把变更原因不同的函数放入不同的类中。而 CCP 原则指导我们应该将变更原因不同的类放入不同的组件中。简而言之，这两个原则都可以用以下一句简短的话来概括：

将由于相同原因而修改，并且需要同时修改的东西放在一起。将由于不同原因而修改，并且不同时修改的东西分开。

### 13.3 The CommonReuse Principle

Don't force users of  a component to depend on things they don't need.

The Common Reuse Principle (CRP) is yet another principle that helps us to decide which classes and modules should be placed into a component. It states that classes and modules that tend to be reused together belong in the same component.

Classes are seldom reused in isolation. More typically, reusable classes collaborate with other classes that are part of the reusable abstraction. The CRP states that these classes belong together in the same component. In such a component we would expect to see classes that have lots of dependencies on each other.

A simple example might be a container class and its associated iterators. These classes are reused together because they are tightly coupled to each other. Thus they ought to be in the same component.

But the CRP tells us more than just which classes to put together into a component: It also tells us which classes not to keep together in a component. When one component uses another, a dependency is created between the components. Perhaps the using component uses only one class within the used component — but that still doesn't weaken the dependency. The using component still depends on the used component.

Because of that dependency, every time the used component is changed, the using component will likely need corresponding changes. Even if no changes are necessary to the using component, it will likely still need to be recompiled, revalidated, and redeployed. This is true even if the using component doesn't care about the change made in the used component.

Thus when we depend on a component, we want to make sure we depend on every class in that component. Put another way, we want to make sure that the classes that we put into a component are inseparable — that it is impossible to depend on some and not on the others. Otherwise, we will be redeploying more components than is necessary, and wasting significant effort.

Therefore the CRP tells us more about which classes shouldn't be together than about which classes should be together. The CRP says that classes that are not tightly bound to each other should not be in the same component.

共同复用原则

不要强迫一个组件的用户依赖他们不需要的东西。

共同复用原则（CRP）是另外一个帮助我们决策类和模块归属于哪一个组件的原则。该原则建议我们将经常共同复用的类和模块放在同一个组件中。

通常情况下，类很少会被单独复用。更常见的情况是多个类同时作为某个可复用的抽象定义被共同复用。CRP 原则指导我们将这些类放在同一个组件中，而在这样的组件中，我们应该预见到会存在着许多互相依赖的类。

一个简单的例子就是容器类与其相关的遍历器类，这些类之间通常是紧密相关的，一般会被共同复用，因此应该被放置在同一个组件中。

但是 CRP 的作用不仅是告诉我们应该将哪些类放在一起，更重要的是要告诉我们应该将哪些类分开。因为每当一个组件引用了另一个组件时，就等于增加了一条依赖关系。虽然这个引用关系仅涉及被引用组件中的一个类，但它所带来的依赖关系丝毫没有减弱。也就是说，引用组件已然依赖于被引用组件了。

由于这种依赖关系的存在，每当被引用组件发生变更时，引用它的组件一般也需要做出相应的变更。即使它们不需要进行代码级的变更，一般也免不了需要被重新编译、验证和部署。哪怕引用组件根本不关心被引用组件中的变更，也要如此。

因此，当我们决定要依赖某个组件时，最好是实际需要依赖该组件中的每个类。换句话说，我们希望组件中的所有类是不能拆分的，即不应该出现别人只需要依赖它的某几个类而不需要其他类的情况。否则，我们后续就会浪费不少时间与精力来做不必要的组件部署。

因此在 CRP 原则中，关于哪些类不应该被放在一起的建议是其更为重要的内容。简而言之，CRP 原则实际上是在指导我们：不是紧密相连的类不应该被放在同一个组件里。

#### 13.3.1 Relation  to  ISP

The CRP is the generic version of the ISP. The ISP advises us not to depend on classes that have methods we don't use. The CRP advises us not to depend on components that have classes we don't use.

All of this advice can be reduced to a single sound bite:

Don't depend on things you don't need.

与 ISP 原则的关系

CRP 原则实际上是 ISP 原则的一个普适版。ISP 原则是建议我们不要依赖带有不需要的函数的类，而 CRP 原则则是建议我们不要依赖带有不需要的类的组件。

上述两条建议实际上都可以用下面一句话来概括：不要依赖不需要用到的东西。

### 13.4 The Tension Diagram for Component Cohesion

You may have already realized that the three cohesion principles tend to fight each other. The REP and CCP are inclusive principles: Both tend to make components larger. The CRP is an exclusive principle, driving components to be smaller. It is the tension between these principles that good architects seek to resolve.

Figure 13.1 is a tension diagram [2] that shows how the three principles of cohesion interact with each other. The edges of the diagram describe the cost of abandoning the principle on the opposite vertex.

Figure 13.1  Cohesion principles tension diagram

An architect who focuses on just the REP and CRP will find that too many components are impacted when simple changes are made. In contrast, an architect who focuses too strongly on the CCP and REP will cause too many unneeded releases to be generated.

A good architect finds a position in that tension triangle that meets the current concerns of the development team, but is also aware that those concerns will change over time. For example, early in the development of a project, the CCP is much more important than the REP, because develop-ability is more important than reuse.

Generally, projects tend to start on the right hand side of the triangle, where the only sacrifice is reuse. As the project matures, and other projects begin to draw from it, the project will slide over to the left. This means that the component structure of a project can vary with time and maturity. It has more to do with the way that project is developed and used, than with what the project actually does.

2 Thanks to Tim Ottinger for this idea.

组件聚合张力图

读到这里，读者可能已经意识到上述三个原则之间彼此存在着竞争关系。REP 和 CCP 原则是黏合性原则，它们会让组件变得更大，而 CRP 原则是排除性原则，它会尽量让组件变小。软件架构师的任务就是要在这三个原则中间进行取舍。

下面我们来看一下图 13.1。这是一张组件聚合三大原则的张力图，图的边线所描述的是忽视对应原则的后果。

图 13.1：组件聚合原则的张力图

简而言之，只关注 REP 和 CRP 的软件架构师会发现，即使是简单的变更也会同时影响到许多组件。相反，如果软件架构师过于关注 CCP 和 REP，则会导致很多不必要的发布。

优秀的软件架构师应该能在上述三角张力区域中定位一个最适合目前研发团队状态的位置，同时也会根据时间不停调整。例如在项目早期，CCP 原则会比 REP 原则更重要，因为在这一阶段研发速度比复用性更重要。

一般来说，一个软件项目的重心会从该三角区域的右侧开始，先期主要牺牲的是复用性。然后，随着项目逐渐成熟，其他项目会逐渐开始对其产生依赖，项目重心就会逐渐向该三角区域的左侧滑动。换句话说，一个项目在组件结构设计上的重心是根据该项目的开发时间和成熟度不断变动的，我们对组件结构的安排主要与项目开发的进度和它被使用的方式有关，与项目本身功能的关系其实很小。
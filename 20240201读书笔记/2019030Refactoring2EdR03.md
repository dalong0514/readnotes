## 记忆时间

## 目录

0301 Bad Smells in Code Topics

0401 Building Tests Topics

0501 Introducing the Catalog

## 0301. Bad Smells in Code Topics

By now you have a good idea of how refactoring works. But just because you know how doesn’t mean you know when. Deciding when to start refactoring—and when to stop—is Settings just as important to refactoring as knowing how to operate the mechanics of it.

Now comes the dilemma. It is easy to explain how to delete an instance variable or create a hierarchy. These are simple matters. Trying to explain when you should do Sign these Out things is not so cut­and­dried. Instead of appealing to some vague notion of programming aesthetics (which, frankly, is what we consultants usually do), I wanted something a bit more solid.

When I was writing the first edition of this book, I was mulling over this issue as I visited Kent Beck in Zurich. Perhaps he was under the influence of the odors of his newborn daughter at the time, but he had come up with the notion of describing the “when” of refactoring in terms of smells.

“Smells,” you say, “and that is supposed to be better than vague aesthetics?” Well, yes. We have looked at lots of code, written for projects that span the gamut from wildly successful to nearly dead. In doing so, we have learned to look for certain structures in the code that suggest—sometimes, scream for—the possibility of refactoring. (We are switching over to “we” in this chapter to reflect the fact that Kent and I wrote this chapter jointly. You can tell the difference because the funny jokes are mine and the others are his.)

One thing we won’t try to give you is precise criteria for when a refactoring is overdue. In our experience, no set of metrics rivals informed human intuition. What we will do is give you indications that there is trouble that can be solved by a refactoring. You will have to develop your own sense of how many instance variables or how many lines of code in a method are too many.

Use this chapter and the table on the inside back cover as a way to give you inspiration when you’re not sure what refactorings to do. Read the chapter (or skim the table) and try to identify what it is you’re smelling, then go to the refactorings we suggest to see whether they will help you. You may not find the exact smell you can detect, but hopefully it should point you in the right direction.

现在，对于重构如何运作，你已经有了相当好的理解。但是知道「如何」不代表知道「何时」。决定何时重构及何时停止和知道重构机制如何运转一样重要。难题来了！解释「如何删除一个实例变量」或「如何产生一个继承体系」很容易，因为这些都是很简单的事情，但要解释「该在什么时候做这些动作」就没那么顺理成章了。除了露几手含混的编程美学（说实话，这就是咱们这些顾问常做的事），我还希望让某些东西更具说服力一些。

撰写本书的第 1 版时，我正在为这个微妙的问题大伤脑筋。去苏黎世拜访 Kent Beck 的时候，也许是因为受到刚出生的女儿的气味影响吧，他提出用味道来形容重构的时机。「味道，」你可能会说，「真的比含混的美学理论要好吗？」好吧，是的。我们看过很多很多代码，它们所属的项目从大获成功到奄奄一息都有。观察这些代码时，我们学会了从中找寻某些特定结构，这些结构指出（有时甚至就像尖叫呼喊）重构的可能性。（本章主语换成「我们」，是为了反映一个事实：Kent 和我共同撰写本章。你应该可以看出我俩的文笔差异 —— 插科打诨的部分是我写的，其余都是他写的。）

我们并不试图给你一个何时必须重构的精确衡量标准。从我们的经验看来，没有任何量度规矩比得上见识广博者的直觉。我们只会告诉你一些迹象，它会指出「这里有一个可以用重构解决的问题」。你必须培养自己的判断力，学会判断一个类内有多少实例变量算是太大、一个函数内有多少行代码才算太长。

如果你无法确定该采用哪一种重构手法，请阅读本章内容和书后附的「重构列表」来寻找灵感。你可以阅读本章或快速浏览书后附的「坏味道与重构手法速查表」来判断自己闻到的是什么味道，然后再看看我们所建议的重构手法能否帮到你。也许这里所列的「坏味道条款」和你所检测的不尽相符，但愿它们能够为你指引正确方向。

### 3.1 Mysterious Name

Puzzling over some text to understand what’s going on is a great thing if you’re reading a detective novel, but not when you’re reading code. We may fantasize about being International Men of Mystery, but our code needs to be mundane and clear. One of the most important parts of clear code is good names, so we put a lot of thought into naming functions, modules, variables, classes, so they clearly communicate what they do and how to use them.

Sadly, however, naming is one of the two hard things [mf­2h] in programming. So, perhaps the most common refactorings we do are the renames: Change Function Declaration (124) (to rename a function), Rename Variable (137), and Rename Field (244). People are often afraid to rename things, thinking it’s not worth the trouble, but a good name can save hours of puzzled incomprehension in the future.

Renaming is not just an exercise in changing names. When you can’t think of a good name for something, it’s often a sign of a deeper design malaise. Puzzling over a tricky name has often led us to significant simplifications to our code.

读侦探小说时，透过一些神秘的文字猜测故事情节是一种很棒的体验；但如果是在阅读代码，这样的体验就不怎么好了。我们也许会幻想自己是《王牌大贱谍》中的国际特工 1，但我们写下的代码应该直观明了。整洁代码最重要的一环就是好的名字，所以我们会深思熟虑如何给函数、模块、变量和类命名，使它们能清晰地表明自己的功能和用法。

然而，很遗憾，命名是编程中最难的两件事之一 [mf2h]。正因为如此，改名可能是最常用的重构手法，包括改变函数声明（124）（用于给函数改名）、变量改名（137）、字段改名（244）等。很多人经常不愿意给程序元素改名，觉得不值得费这个劲，但好的名字能节省未来用在猜谜上的大把时间。改名不仅仅是修改名字而已。如果你想不出一个好名字，说明背后很可能潜藏着更深的设计问题。为一个恼人的名字所付出的纠结，常常能推动我们对代码进行精简。

### 3.2 Duplicated Code

If you see the same code structure in more than one place, you can be sure that your program will be better if you find a way to unify them. Duplication means that every time you read these copies, you need to read them carefully to see if there’s any difference. If you need to change the duplicated code, you have to find and catch each duplication.

The simplest duplicated code problem is when you have the same expression in two methods of the same class. Then all you have to do is Extract Function (106) and invoke the code from both places. If you have code that’s similar, but not quite identical, see if you can use Slide Statements (223) to arrange the code so the similar items are all together for easy extraction. If the duplicate fragments are in subclasses of a common base class, you can use Pull Up Method (350) to avoid calling one from another.

如果你在一个以上的地点看到相同的代码结构，那么可以肯定：设法将它们合而为一，程序会变得更好。一旦有重复代码存在，阅读这些重复的代码时你就必须加倍仔细，留意其间细微的差异。如果要修改重复代码，你必须找出所有的副本来修改。

最单纯的重复代码就是「同一个类的两个函数含有相同的表达式」。这时候你需要做的就是采用提炼函数（106）提炼出重复的代码，然后让这两个地点都调用被提炼出来的那一段代码。如果重复代码只是相似而不是完全相同，请首先尝试用移动语句（223）重组代码顺序，把相似的部分放在一起以便提炼。如果重复的代码段位于同一个超类的不同子类中，可以使用函数上移（350）来避免在两个子类之间互相调用。

### 3.3 Long Function

In our experience, the programs that live best and longest are those with short functions. Programmers new to such a code base often feel that no computation ever takes place—that the program is an endless sequence of delegation. When you have lived with such a program for a few years, however, you learn just how valuable all those little functions are. All of the payoffs of indirection—explanation, sharing, and choosing—are supported by small functions.

1『小函数的结构稳定、功能单一，「不变性」强。最极端的一个函数里就一句话，基本不会变，哈哈。（2020-09-28）』

Since the early days of programming, people have realized that the longer a function is, the more difficult it is to understand. Older languages carried an overhead in subroutine calls, which deterred people from small functions. Modern languages have pretty much eliminated that overhead for in­process calls. There is still overhead for the reader of the code because you have to switch context to see what the function does. Development environments that allow you to quickly jump between a function call and its declaration, or to see both functions at once, help eliminate this step, but the real key to making it easy to understand small functions is good naming. If you have a good name for a function, you mostly don’t need to look at its body.

The net effect is that you should be much more aggressive about decomposing functions. A heuristic we follow is that whenever we feel the need to comment something, we write a function instead. Such a function contains the code that we wanted to comment but is named after the intention of the code rather than the way it works. We may do this on a group of lines or even on a single line of code. We do this even if the method call is longer than the code it replaces—provided the method name explains the purpose of the code. The key here is not function length but the semantic distance between what the method does and how it does it.

Ninety­nine percent of the time, all you have to do to shorten a function is Extract Function (106). Find parts of the function that seem to go nicely together and make a new one.

If you have a function with lots of parameters and temporary variables, they get in the way of extracting. If you try to use Extract Function (106), you end up passing so many parameters to the extracted method that the result is scarcely more readable than the original. You can often use Replace Temp with Query (178) to eliminate the temps. Long lists of parameters can be slimmed down with Introduce Parameter Object (140) and Preserve Whole Object (319). If you’ve tried that and you still have too many temps and parameters, it’s time to get out the heavy artillery: Replace Function with Command (337).

How do you identify the clumps of code to extract? A good technique is to look for comments. They often signal this kind of semantic distance. A block of code with a comment that tells you what it is doing can be replaced by a method whose name is based on the comment. Even a single line is worth extracting if it needs explanation.

1『用函数取代备注，这个思路很赞。（2020-09-28）』

Conditionals and loops also give signs for extractions. Use Decompose Conditional (260) to deal with conditional expressions. A big switch statement should have its legs turned into single function calls with Extract Function (106). If there’s more than one switch statement switching on the same condition, you should apply Replace Conditional with Polymorphism (272).

With loops, extract the loop and the code within the loop into its own method. If you find it hard to give an extracted loop a name, that may be because it’s doing two different things—in which case don’t be afraid to use Split Loop (227) to break out the separate tasks.

1『用多态的一个标志，switch 语句通过一个条件进行分支选择，这个收获太大了。循环那边，用函数式编程范式里的映射函数取代循环语句，已经实践一段时间了。（2020-09-28）』

据我们的经验，活得最长、最好的程序，其中的函数都比较短。初次接触到这种代码库的程序员常常会觉得「计算都没有发生」—— 程序里满是无穷无尽的委托调用。但和这样的程序共处几年之后，你就会明白这些小函数的价值所在。间接性带来的好处 —— 更好的阐释力、更易于分享、更多的选择 —— 都是由小函数来支持的。

早在编程的洪荒年代，程序员们就已认识到：函数越长，就越难理解。在早期的编程语言中，子程序调用需要额外开销，这使得人们不太乐意使用小函数。现代编程语言几乎已经完全免除了进程内的函数调用开销。固然，小函数也会给代码的阅读者带来一些负担，因为你必须经常切换上下文，才能看明白函数在做什么。但现代的开发环境让你可以在函数的调用处与声明处之间快速跳转，或是同时看到这两处，让你根本不用来回跳转。不过说到底，让小函数易于理解的关键还是在于良好的命名。如果你能给函数起个好名字，阅读代码的人就可以通过名字了解函数的作用，根本不必去看其中写了些什么。

最终的效果是：你应该更积极地分解函数。我们遵循这样一条原则：每当感觉需要以注释来说明点什么的时候，我们就把需要说明的东西写进一个独立函数中，并以其用途（而非实现手法）命名。我们可以对一组甚至短短一行代码做这件事。哪怕替换后的函数调用动作比函数自身还长，只要函数名称能够解释其用途，我们也该毫不犹豫地那么做。关键不在于函数的长度，而在于函数「做什么」和「如何做」之间的语义距离。

百分之九十九的场合里，要把函数变短，只需使用提炼函数（106）。找到函数中适合集中在一起的部分，将它们提炼出来形成一个新函数。如果函数内有大量的参数和临时变量，它们会对你的函数提炼形成阻碍。如果你尝试运用提炼函数（106），最终就会把许多参数传递给被提炼出来的新函数，导致可读性几乎没有任何提升。此时，你可以经常运用以查询取代临时变量（178）来消除这些临时元素。引入参数对象（140）和保持对象完整（319）则可以将过长的参数列表变得更简洁一些。如果你已经这么做了，仍然有太多临时变量和参数，那就应该使出我们的杀手锏 —— 以命令取代函数（337）。

如何确定该提炼哪一段代码呢？一个很好的技巧是：寻找注释。它们通常能指出代码用途和实现手法之间的语义距离。如果代码前方有一行注释，就是在提醒你：可以将这段代码替换成一个函数，而且可以在注释的基础上给这个函数命名。就算只有一行代码，如果它需要以注释来说明，那也值得将它提炼到独立函数中去。

条件表达式和循环常常也是提炼的信号。你可以使用分解条件表达式（260）处理条件表达式。对于庞大的 switch 语句，其中的每个分支都应该通过提炼函数（106）变成独立的函数调用。如果有多个 switch 语句基于同一个条件进行分支选择，就应该使用以多态取代条件表达式（272）。

至于循环，你应该将循环和循环内的代码提炼到一个独立的函数中。如果你发现提炼出的循环很难命名，可能是因为其中做了几件不同的事。如果是这种情况，请勇敢地使用拆分循环（227）将其拆分成各自独立的任务。

### 3.4 Long Patameter List

In our early programming days, we were taught to pass in as parameters everything needed by a function. This was understandable because the alternative was global data, and global data quickly becomes evil. But long parameter lists are often confusing in their own right.

If you can obtain one parameter by asking another parameter for it, you can use Replace Parameter with Query (324) to remove the second parameter. Rather than pulling lots of data out of an existing data structure, you can use Preserve Whole Object (319) to pass the original data structure instead. If several parameters always fit together, combine them with Introduce Parameter Object (140). If a parameter is used as a flag to dispatch different behavior, use Remove Flag Argument (314).

1『此时此刻才算理解了啥叫「查询取代参数」，比如说一个函数有 3 个入参（A、B、C），B、C 可以通过调用一个函数（以 A 为入参）来获取，那么果断用调用函数的方式取代 B、C，这样的话，原来 3 个入参可以缩减为 1 个。』

Classes are a great way to reduce parameter list sizes. They are particularly useful when multiple functions share several parameter values. Then, you can use Combine Functions into Class (144) to capture those common values as fields. If we put on our functional programming hats, we’d say this creates a set of partially applied functions.

刚开始学习编程的时候，老师教我们：把函数所需的所有东西都以参数的形式传递进去。这可以理解，因为除此之外就只能选择全局数据，而全局数据很快就会变成邪恶的东西。但过长的参数列表本身也经常令人迷惑。如果可以向某个参数发起查询而获得另一个参数的值，那么就可以使用以查询取代参数（324）去掉这第二个参数。

如果你发现自己正在从现有的数据结构中抽出很多数据项，就可以考虑使用保持对象完整（319）手法，直接传入原来的数据结构。如果有几项参数总是同时出现，可以用引入参数对象（140）将其合并成一个对象。如果某个参数被用作区分函数行为的标记（flag），可以使用移除标记参数（314）。

使用类可以有效地缩短参数列表。如果多个函数有同样的几个参数，引入一个类就尤为有意义。你可以使用函数组合成类（144），将这些共同的参数变成这个类的字段。如果戴上函数式编程的帽子，我们会说，这个重构过程创造了一组部分应用函数（partially applied function）。

### 3.5 Global Data

Since our earliest days of writing software, we were warned of the perils of global data— how it was invented by demons from the fourth plane of hell, which is the resting place of any programmer who dares to use it. And, although we are somewhat skeptical about fire and brimstone, it’s still one of the most pungent odors we are likely to run into. The problem with global data is that it can be modified from anywhere in the code base, and there’s no mechanism to discover which bit of code touched it. Time and again, this leads to bugs that breed from a form of spooky action from a distance—and it’s very hard to find out where the errant bit of program is. The most obvious form of global data is global variables, but we also see this problem with class variables and singletons.

Our key defense here is Encapsulate Variable (132), which is always our first move when confronted with data that is open to contamination by any part of a program. At least when you have it wrapped by a function, you can start seeing where it’s modified and start to control its access. Then, it’s good to limit its scope as much as possible by moving it within a class or module where only that module’s code can see it.

Global data is especially nasty when it’s mutable. Global data that you can guarantee never changes after the program starts is relatively safe—if you have a language that can enforce that guarantee.

Global data illustrates Paracelsus’s maxim: The difference between a poison and something benign is the dose. You can get away with small doses of global data, but it gets exponentially harder to deal with the more you have. Even with little bits, we like to keep it encapsulated—that’s the key to coping with changes as the software evolves.

刚开始学软件开发时，我们就听说过关于全局数据的惊悚故事 —— 它们是如何被来自地狱第四层的恶魔发明出来，胆敢使用它们的程序员如今在何处安息。就算这些烈焰与硫黄的故事不那么可信，全局数据仍然是最刺鼻的坏味道之一。全局数据的问题在于，从代码库的任何一个角落都可以修改它，而且没有任何机制可以探测出到底哪段代码做出了修改。一次又一次，全局数据造成了那些诡异的 bug，而问题的根源却在遥远的别处，想要找到出错的代码难于登天。全局数据最显而易见的形式就是全局变量，但类变量和单例（singleton）也有这样的问题。

首要的防御手段是封装变量（132），每当我们看到可能被各处的代码污染的数据，这总是我们应对的第一招。你把全局数据用一个函数包装起来，至少你就能看见修改它的地方，并开始控制对它的访问。随后，最好将这个函数（及其封装的数据）搬移到一个类或模块中，只允许模块内的代码使用它，从而尽量控制其作用域。可以被修改的全局数据尤其可憎。如果能保证在程序启动之后就不再修改，这样的全局数据还算相对安全，不过得有编程语言提供这样的保证才行。

全局数据印证了帕拉塞尔斯的格言：良药与毒药的区别在于剂量。有少量的全局数据或许无妨，但数量越多，处理的难度就会指数上升。即便只是少量的数据，我们也愿意将它封装起来，这是在软件演进过程中应对变化的关键所在。

### 3.6 Mutable Data

Changes to data can often lead to unexpected consequences and tricky bugs. I can update some data here, not realizing that another part of the software expects something different and now fails—a failure that’s particularly hard to spot if it only happens under rare conditions. For this reason, an entire school of software development—functional programming—is based on the notion that data should never change and that updating a data structure should always return a new copy of the structure with the change, leaving the old data pristine.

These kinds of languages, however, are still a relatively small part of programming; many of us work in languages that allow variables to vary. But this doesn’t mean we should ignore the advantages of immutability—there are still many things we can do to limit the risks on unrestricted data updates.

You can use Encapsulate Variable (132) to ensure that all updates occur through narrow functions that can be easier to monitor and evolve. If a variable is being updated to store different things, use Split Variable (240) both to keep them separate and avoid the risky update. Try as much as possible to move logic out of code that processes the update by using Slide Statements (223) and Extract Function (106) to separate the side­effect­free code from anything that performs the update. In APIs, use Separate Query from Modifier (306) to ensure callers don’t need to call code that has side effects unless they really need to. We like to use Remove Setting Method (331) as soon as we can—sometimes, just trying to find clients of a setter helps spot opportunities to reduce the scope of a variable.

Mutable data that can be calculated elsewhere is particularly pungent. It’s not just a rich source of confusion, bugs, and missed dinners at home—it’s also unnecessary. We spray it with a concentrated solution of vinegar and Replace Derived Variable with Query (248).

Mutable data isn’t a big problem when it’s a variable whose scope is just a couple of lines—but its risk increases as its scope grows. Use Combine Functions into Class (144) or Combine Functions into Transform (149) to limit how much code needs to update a variable. If a variable contains some data with internal structure, it’s usually better to replace the entire structure rather than modify it in place, using Change Reference to Value (252).

对数据的修改经常导致出乎意料的结果和难以发现的 bug。我在一处更新数据，却没有意识到软件中的另一处期望着完全不同的数据，于是一个功能失效了 —— 如果故障只在很罕见的情况下发生，要找出故障原因就会更加困难。因此，有一整个软件开发流派 —— 函数式编程 —— 完全建立在「数据永不改变」的概念基础上：如果要更新一个数据结构，就返回一份新的数据副本，旧的数据仍保持不变。不过这样的编程语言仍然相对小众，大多数程序员使用的编程语言还是允许修改变量值的。即便如此，我们也不应该忽视不可变性带来的优势 —— 仍然有很多办法可以用于约束对数据的更新，降低其风险。

可以用封装变量（132）来确保所有数据更新操作都通过很少几个函数来进行，使其更容易监控和演进。如果一个变量在不同时候被用于存储不同的东西，可以使用拆分变量（240）将其拆分为各自不同用途的变量，从而避免危险的更新操作。使用移动语句（223）和提炼函数（106）尽量把逻辑从处理更新操作的代码中搬移出来，将没有副作用的代码与执行数据更新操作的代码分开。设计 API 时，可以使用将查询函数和修改函数分离（306）确保调用者不会调到有副作用的代码，除非他们真的需要更新数据。我们还乐于尽早使用移除设值函数（331）—— 有时只是把设值函数的使用者找出来看看，就能帮我们发现缩小变量作用域的机会。

如果可变数据的值能在其他地方计算出来，这就是一个特别刺鼻的坏味道。它不仅会造成困扰、bug 和加班，而且毫无必要。消除这种坏味道的办法很简单，使用以查询取代派生变量（248）即可。如果变量作用域只有几行代码，即使其中的数据可变，也不是什么大问题；但随着变量作用域的扩展，风险也随之增大。可以用函数组合成类（144）或者函数组合成变换（149）来限制需要对变量进行修改的代码量。如果一个变量在其内部结构中包含了数据，通常最好不要直接修改其中的数据，而是用将引用对象改为值对象（252）令其直接替换整个数据结构。

### 3.7 Divergent Change

We structure our software to make change easier; after all, software is meant to be soft. When we make a change, we want to be able to jump to a single clear point in the system and make the change. When you can’t do this, you are smelling one of two closely related pungencies.

Divergent change occurs when one module is often changed in different ways for different reasons. If you look at a module and say, “Well, I will have to change these three functions every time I get a new database; I have to change these four functions every time there is a new financial instrument,” this is an indication of divergent change. The database interaction and financial processing problems are separate contexts, and we can make our programming life better by moving such contexts into separate modules. That way, when we have a change to one context, we only have to understand that one context and ignore the other. We always found this to be important, but now, with our brains shrinking with age, it becomes all the more imperative. Of course, you often discover this only after you’ve added a few databases or financial instruments; context boundaries are usually unclear in the early days of a program and continue to shift as a software system’s capabilities change. If the two aspects naturally form a sequence—for example, you get data from the database and then apply your financial processing on it—then Split Phase (154) separates the two with a clear data structure between them. If there’s more back­andforth in the calls, then create appropriate modules and use Move Function (198) to divide the processing up. If functions mix the two types of processing within themselves, use Extract Function (106) to separate them before moving. If the modules are classes, then Extract Class (182) helps formalize how to do the split.

我们希望软件能够更容易被修改 —— 毕竟软件本来就该是「软」的。一旦需要修改，我们希望能够跳到系统的某一点，只在该处做修改。如果不能做到这一点，你就嗅出两种紧密相关的刺鼻味道中的一种了。

如果某个模块经常因为不同的原因在不同的方向上发生变化，发散式变化就出现了。当你看着一个类说：「呃，如果新加入一个数据库，我必须修改这 3 个函数；如果新出现一种金融工具，我必须修改这 4 个函数。」这就是发散式变化的征兆。数据库交互和金融逻辑处理是两个不同的上下文，将它们分别搬移到各自独立的模块中，能让程序变得更好：每当要对某个上下文做修改时，我们只需要理解这个上下文，而不必操心另一个。「每次只关心一个上下文」这一点一直很重要，在如今这个信息爆炸、脑容量不够用的年代就愈发紧要。当然，往往只有在加入新数据库或新金融工具后，你才能发现这个坏味道。在程序刚开发出来还在随着软件系统的能力不断演进时，上下文边界通常不是那么清晰。

如果发生变化的两个方向自然地形成了先后次序（比如说，先从数据库取出数据，再对其进行金融逻辑处理），就可以用拆分阶段（154）将两者分开，两者之间通过一个清晰的数据结构进行沟通。如果两个方向之间有更多的来回调用，就应该先创建适当的模块，然后用搬移函数（198）把处理逻辑分开。如果函数内部混合了两类处理逻辑，应该先用提炼函数（106）将其分开，然后再做搬移。如果模块是以类的形式定义的，就可以用提炼类（182）来做拆分。

### 3.8 Shotgun Surgery

Shotgun surgery is similar to divergent change but is the opposite. You whiff this when, every time you make a change, you have to make a lot of little edits to a lot of different classes. When the changes are all over the place, they are hard to find, and it’s easy to miss an important change.

In this case, you want to use Move Function (198) and Move Field (207) to put all the changes into a single module. If you have a bunch of functions operating on similar data, use Combine Functions into Class (144). If you have functions that are transforming or enriching a data structure, use Combine Functions into Transform (149). Split Phase (154) is often useful here if the common functions can combine their output for a consuming phase of logic.

A useful tactic for shotgun surgery is to use inlining refactorings, such as Inline Function (115) or Inline Class (186), to pull together poorly separated logic. You’ll end up with a Long Method or a Large Class, but can then use extractions to break it up into more sensible pieces. Even though we are inordinately fond of small functions and classes in our code, we aren’t afraid of creating something large as an intermediate step to reorganization.

霰弹式修改类似于发散式变化，但又恰恰相反。如果每遇到某种变化，你都必须在许多不同的类内做出许多小修改，你所面临的坏味道就是霰弹式修改。如果需要修改的代码散布四处，你不但很难找到它们，也很容易错过某个重要的修改。这种情况下，你应该使用搬移函数（198）和搬移字段（207）把所有需要修改的代码放进同一个模块里。如果有很多函数都在操作相似的数据，可以使用函数组合成类（144）。如果有些函数的功能是转化或者充实数据结构，可以使用函数组合成变换（149）。如果一些函数的输出可以组合后提供给一段专门使用这些计算结果的逻辑，这种时候常常用得上拆分阶段（154）。

面对霰弹式修改，一个常用的策略就是使用与内联（inline）相关的重构 —— 如内联函数（115）或是内联类（186）—— 把本不该分散的逻辑拽回一处。完成内联之后，你可能会闻到过长函数或者过大的类的味道，不过你总可以用与提炼相关的重构手法将其拆解成更合理的小块。即便如此钟爱小型的函数和类，我们也并不担心在重构的过程中暂时创建一些较大的程序单元。

### 3.9 Feature Envy

When we modularize a program, we are trying to separate the code into zones to maximize the interaction inside a zone and minimize interaction between zones. A classic case of Feature Envy occurs when a function in one module spends more time communicating with functions or data inside another module than it does within its own module. We’ve lost count of the times we’ve seen a function invoking half­a­dozen getter methods on another object to calculate some value. Fortunately, the cure for that case is obvious: The function clearly wants to be with the data, so use Move Function (198) to get it there. Sometimes, only a part of a function suffers from envy, in which case use Extract Function (106) on the jealous bit, and Move Function (198) to give it a dream home.

Of course not all cases are cut­and­dried. Often, a function uses features of several modules, so which one should it live with? The heuristic we use is to determine which module has most of the data and put the function with that data. This step is often made easier if you use Extract Function (106) to break the function into pieces that go into different places.

Of course, there are several sophisticated patterns that break this rule. From the Gang of Four [gof], Strategy and Visitor immediately leap to mind. Kent Beck’s Self Delegation [Beck SBPP] is another. Use these to combat the divergent change smell. The fundamental rule of thumb is to put things together that change together. Data and the behavior that references that data usually change together—but there are exceptions. When the exceptions occur, we move the behavior to keep changes in one place. Strategy and Visitor allow you to change behavior easily because they isolate the small amount of behavior that needs to be overridden, at the cost of further indirection.

所谓模块化，就是力求将代码分出区域，最大化区域内部的交互、最小化跨区域的交互。但有时你会发现，一个函数跟另一个模块中的函数或者数据交流格外频繁，远胜于在自己所处模块内部的交流，这就是依恋情结的典型情况。无数次经验里，我们看到某个函数为了计算某个值，从另一个对象那儿调用几乎半打的取值函数。疗法显而易见：这个函数想跟这些数据待在一起，那就使用搬移函数（198）把它移过去。有时候，函数中只有一部分受这种依恋之苦，这时候应该使用提炼函数（106）把这一部分提炼到独立的函数中，再使用搬移函数（198）带它去它的梦想家园。

当然，并非所有情况都这么简单。一个函数往往会用到几个模块的功能，那么它究竟该被置于何处呢？我们的原则是：判断哪个模块拥有的此函数使用的数据最多，然后就把这个函数和那些数据摆在一起。如果先以提炼函数（106）将这个函数分解为数个较小的函数并分别置放于不同地点，上述步骤也就比较容易完成了。

有几个复杂精巧的模式破坏了这条规则。说起这个话题，GoF [gof] 的策略（Strategy）模式和访问者（Visitor）模式立刻跳入我的脑海，Kent Beck 的 Self Delegation 模式 [Beck SBPP] 也在此列。使用这些模式是为了对抗发散式变化这一坏味道。最根本的原则是：将总是一起变化的东西放在一块儿。数据和引用这些数据的行为总是一起变化的，但也有例外。如果例外出现，我们就搬移那些行为，保持变化只在一地发生。策略模式和和访问者模式使你得以轻松修改函数的行为，因为它们将少量需被覆写的行为隔离开来 —— 当然也付出了「多一层间接性」的代价。

### 3.10 Data Clumps

Data items tend to be like children: They enjoy hanging around together. Often, you’ll see the same three or four data items together in lots of places: as fields in a couple of classes, as parameters in many method signatures. Bunches of data that hang around together really ought to find a home together. The first step is to look for where the clumps appear as fields. Use Extract Class (182) on the fields to turn the clumps into an object. Then turn your attention to method signatures using Introduce Parameter Object (140) or Preserve Whole Object (319) to slim them down. The immediate benefit is that you can shrink a lot of parameter lists and simplify method calling. Don’t worry about data clumps that use only some of the fields of the new object. As long as you are replacing two or more fields with the new object, you’ll come out ahead.

A good test is to consider deleting one of the data values. If you did this, would the others make any sense? If they don’t, it’s a sure sign that you have an object that’s dying to be born.

You’ll notice that we advocate creating a class here, not a simple record structure. We do this because using a class gives you the opportunity to make a nice perfume. You can now look for cases of feature envy, which will suggest behavior that can be moved into your new classes. We’ve often seen this as a powerful dynamic that creates useful classes and can remove a lot of duplication and accelerate future development, allowing the data to become productive members of society.

数据项就像小孩子，喜欢成群结队地待在一块儿。你常常可以在很多地方看到相同的三四项数据：两个类中相同的字段、许多函数签名中相同的参数。这些总是绑在一起出现的数据真应该拥有属于它们自己的对象。首先请找出这些数据以字段形式出现的地方，运用提炼类（182）将它们提炼到一个独立对象中。然后将注意力转移到函数签名上，运用引入参数对象（140）或保持对象完整（319）为它瘦身。这么做的直接好处是可以将很多参数列表缩短，简化函数调用。是的，不必在意数据泥团只用上新对象的一部分字段，只要以新对象取代两个（或更多）字段，就值得这么做。

一个好的评判办法是：删掉众多数据中的一项。如果这么做，其他数据有没有因而失去意义？如果它们不再有意义，这就是一个明确信号：你应该为它们产生一个新对象。我们在这里提倡新建一个类，而不是简单的记录结构，因为一旦拥有新的类，你就有机会让程序散发出一种芳香。得到新的类以后，你就可以着手寻找「依恋情结」，这可以帮你指出能够移至新类中的种种行为。这是一种强大的动力：有用的类被创建出来，大量的重复被消除，后续开发得以加速，原来的数据泥团终于在它们的小社会中充分发挥价值。

### 3.11 Primitive Obsession

Most programming environments are built on a widely used set of primitive types: integers, floating point numbers, and strings. Libraries may add some additional small objects such as dates. We find many programmers are curiously reluctant to create their own fundamental types which are useful for their domain—such as money, coordinates, or ranges. We thus see calculations that treat monetary amounts as plain numbers, or calculations of physical quantities that ignore units (adding inches to millimeters), or lots of code doing if (a < upper && a > lower).

Strings are particularly common petri dishes for this kind of odor: A telephone number is more than just a collection of characters. If nothing else, a proper type can often include consistent display logic for when it needs to be displayed in a user interface. Representing such types as strings is such a common stench that people call them “stringly typed” variables.

You can move out of the primitive cave into the centrally heated world of meaningful types by using Replace Primitive with Object (174). If the primitive is a type code controlling conditional behavior, use Replace Type Code with Subclasses (362) followed by Replace Conditional with Polymorphism (272).

Groups of primitives that commonly appear together are data clumps and should be civilized with Extract Class (182) and Introduce Parameter Object (140).

大多数编程环境都大量使用基本类型，即整数、浮点数和字符串等。一些库会引入一些小对象，如日期。但我们发现一个很有趣的现象：很多程序员不愿意创建对自己的问题域有用的基本类型，如钱、坐标、范围等。于是，我们看到了把钱当作普通数字来计算的情况、计算物理量时无视单位（如把英寸与毫米相加）的情况以及大量类似 if (`a < upper && a> lower`) 这样的代码。

字符串是这种坏味道的最佳培养皿，比如，电话号码不只是一串字符。一个体面的类型，至少能包含一致的显示逻辑，在用户界面上需要显示时可以使用。「用字符串来代表类似这样的数据」是如此常见的臭味，以至于人们给这类变量专门起了一个名字，叫它们「类字符串类型」（stringly typed）变量。

你可以运用以对象取代基本类型（174）将原本单独存在的数据值替换为对象，从而走出传统的洞窟，进入炙手可热的对象世界。如果想要替换的数据值是控制条件行为的类型码，则可以运用以子类取代类型码（362）加上以多态取代条件表达式（272）的组合将它换掉。如果你有一组总是同时出现的基本类型数据，这就是数据泥团的征兆，应该运用提炼类（182）和引入参数对象（140）来处理。

### 3.12 Repeated Switches

Talk to a true object­oriented evangelist and they’ll soon get onto the evils of switch statements. They’ll argue that any switch statement you see is begging for Replace Conditional with Polymorphism (272). We’ve even heard some people argue that all conditional logic should be replaced with polymorphism, tossing most ifs into the dustbin of history.

Even in our more wild­eyed youth, we were never unconditionally opposed to the conditional. Indeed, the first edition of this book had a smell entitled “switch statements.” The smell was there because in the late 90’s we found polymorphism sadly underappreciated, and saw benefit in getting people to switch over.

These days there is more polymorphism about, and it isn’t the simple red flag that it often was fifteen years ago. Furthermore, many languages support more sophisticated forms of switch statements that use more than some primitive code as their base. So we now focus on the repeated switch, where the same conditional switching logic (either in a switch/case statement or in a cascade of if/else statements) pops up in different places. The problem with such duplicate switches is that, whenever you add a clause, you have to find all the switches and update them. Against the dark forces of such repetition, polymorphism provides an elegant weapon for a more civilized codebase.

如果你跟真正的面向对象布道者交谈，他们很快就会谈到 switch 语句的邪恶。在他们看来，任何 switch 语句都应该用以多态取代条件表达式（272）消除掉。我们甚至还听过这样的观点：所有条件逻辑都应该用多态取代，绝大多数 if 语句都应该被扫进历史的垃圾桶。

即便在不知天高地厚的青年时代，我们也从未无条件地反对条件语句。在本书第 1 版中，这种坏味道被称为「switch 语句」（Switch Statements），那是因为在 20 世纪 90 年代末期，程序员们太过于忽视多态的价值，我们希望矫枉过正。

如今的程序员已经更多地使用多态，switch 语句也不再像 15 年前那样有害无益，很多语言支持更复杂的 switch 语句，而不只是根据基本类型值来做条件判断。因此，我们现在更关注重复的 switch：在不同的地方反复使用同样的 switch 逻辑（可能是以 switch/case 语句的形式，也可能是以连续的 if/else 语句的形式）。重复的 switch 的问题在于：每当你想增加一个选择分支时，必须找到所有的 switch，并逐一更新。多态给了我们对抗这种黑暗力量的武器，使我们得到更优雅的代码库。

### 3.13 Loops

Loops have been a core part of programming since the earliest languages. But we feel they are no more relevant today than bell­bottoms and flock wallpaper. We disdained them at the time of the first edition—but Java, like most other languages at the time, didn’t provide a better alternative. These days, however, first­class functions are widely supported, so we can use Replace Loop with Pipeline (231) to retire those anachronisms. We find that pipeline operations, such as filter and map, help us quickly see the elements that are included in the processing and what is done with them.

从最早的编程语言开始，循环就一直是程序设计的核心要素。但我们感觉如今循环已经有点儿过时，就像喇叭裤和植绒壁纸那样。其实在撰写本书第 1 版的时候，我们就已经开始鄙视循环语句，但和当时的大多数编程语言一样，当时的 Java 还没有提供更好的替代品。如今，函数作为一等公民已经得到了广泛的支持，因此我们可以使用以管道取代循环（231) 来让这些老古董退体。我们发现，管道操作（如 filter 和 map）可以帮助我们更快地看清被处理的元素以及处理它们的动作。

### 3.14 Lazy Element

We like using program elements to add structure—providing opportunities for variation, reuse, or just having more helpful names. But sometimes the structure isn’t needed. It may be a function that’s named the same as its body code reads, or a class that is essentially one simple function. Sometimes, this reflects a function that was expected to grow and be popular later, but never realized its dreams. Sometimes, it’s a class that used to pay its way, but has been downsized with refactoring. Either way, such program elements need to die with dignity. Usually this means using Inline Function (115) or Inline Class (186). With inheritance, you can use Collapse Hierarchy (380).

程序元素（如类和函数）能给代码增加结构，从而支持变化、促进复用或者哪怕只是提供更好的名字也好，但有时我们真的不需要这层额外的结构。可能有这样一个函数，它的名字就跟实现代码看起来一模一样；也可能有这样一个类，根本就是一个简单的函数。这可能是因为，起初在编写这个函数时，程序员也许期望它将来有一天会变大、变复杂，但那一天从未到来；也可能是因为，这个类原本是有用的，但随着重构的进行越变越小，最后只剩了一个函数。不论上述哪一种原因，请让这样的程序元素庄严赴义，通常你只需要使用内联函数（115）或是内联类（186）。如果这个类处于一个继承体系中，可以使用折叠继承体系（380)。

### 3.15 Speculative Generality

Brian Foote suggested this name for a smell to which we are very sensitive. You get it when people say, “Oh, I think we’ll need the ability to do this kind of thing someday” and thus add all sorts of hooks and special cases to handle things that aren’t required. The result is often harder to understand and maintain. If all this machinery were being used, it would be worth it. But if it isn’t, it isn’t. The machinery just gets in the way, so get rid of it.

If you have abstract classes that aren’t doing much, use Collapse Hierarchy (380). Unnecessary delegation can be removed with Inline Function (115) and Inline Class (186). Functions with unused parameters should be subject to Change Function Declaration (124) to remove those parameters. You should also apply Change Function Declaration (124) to remove any unneeded parameters, which often get tossed in for future variations that never come to pass.

Speculative generality can be spotted when the only users of a function or class are test cases. If you find such an animal, delete the test case and apply Remove Dead Code (237).

这个令我们十分敏感的坏味道，命名者是 Brian Foote。当有人说「噢，我想我们总有一天需要做这事」，并因而企图以各式各样的钩子和特殊情况来处理一些非必要的事情，这种坏味道就出现了。这么做的结果往往造成系统更难理解和维护。如果所有装置都会被用到，就值得那么做；如果用不到，就不值得。用不上的装置只会挡你的路，所以，把它搬开吧。

如果你的某个抽象类其实没有太大作用，请运用折叠继承体系（380）。不必要的委托可运用内联函数（115）和内联类（186）除掉。如果函数的某些参数未被用上，可以用改变函数声明（124）去掉这些参数。如果有并非真正需要、只是为不知远在何处的将来而塞进去的参数，也应该用改变函数声明（124) 去掉。如果函数或类的唯一用户是测试用例，这就飘出了坏味道「夸夸其谈通用性」。如果你发现这样的函数或类，可以先删掉测试用例，然后使用移除死代码（237)。

### 3.16 Temporary Field

Sometimes you see a class in which a field is set only in certain circumstances. Such code is difficult to understand, because you expect an object to need all of its fields. Trying to understand why a field is there when it doesn’t seem to be used can drive you nuts.

Use Extract Class (182) to create a home for the poor orphan variables. Use Move Function (198) to put all the code that concerns the fields into this new class. You may also be able to eliminate conditional code by using Introduce Special Case (289) to create an alternative class for when the variables aren’t valid.

有时你会看到这样的类：其内部某个字段仅为某种特定情况而设。这样的代码让人不易理解，因为你通常认为对象在所有时候都需要它的所有字段。在字段未被使用的情况下猜测当初设置它的目的，会让你发疯。请使用提炼类（182）给这个可怜的孤儿创造一个家，然后用搬移函数（198）把所有和这些字段相关的代码都放进这个新家。也许你还可以使用引入特例（289）在「变量不合法」的情况下创建一个替代对象，从而避免写出条件式代码。

### 3.17 Message Chains

You see message chains when a client asks one object for another object, which the client then asks for yet another object, which the client then asks for yet another another object, and so on. You may see these as a long line of getThis methods, or as a sequence of temps. Navigating this way means the client is coupled to the structure of the navigation. Any change to the intermediate relationships causes the client to have to change.

The move to use here is Hide Delegate (189). You can do this at various points in the chain. In principle, you can do this to every object in the chain, but doing this often turns every intermediate object into a middle man. Often, a better alternative is to see what the resulting object is used for. See whether you can use Extract Function (106) to take a piece of the code that uses it and then Move Function (198) to push it down the chain. If several clients of one of the objects in the chain want to navigate the rest of the way, add a method to do that.

Some people consider any method chain to be a terrible thing. We are known for our calm, reasoned moderation. Well, at least in this case we are.

如果你看到用户向一个对象请求另一个对象，然后再向后者请求另一个对象，然后再请求另一个对象。这就是消息链。在实际代码中你看到的可能是一长串取值函数或一长串临时量。采取这种方式，意味客户端代码将与找过程中的导航结构紧密耦合。一旦对象间的关系发生任何变化，客户端就不得不做出相应修改。

这时候应该使用隐委托关系（189）。你可以在消息链的不同位置采用这种重构手法。理论上，你可以重构消息链上的所有对象，但这么做就会把所有中间对象都变成「中间人」。通常更好的选择是：先观察消息链最终得到的对象是用来干什么的，看看能否以提炼函数（106）把使用该对象的代码提炼到一个独立的函数中，再运用搬移函数（198）把这个函数推入消息链。如果还有许多客户端代码需要访问链上的其他对象，同样添加一个函数来完成此事。有些人把任何函数链都视为坏东西，我们不这样想。我们的冷静镇定是出了名的，起码在这件事上是这样的。

### 3.18 Middle Man

One of the prime features of objects is encapsulation—hiding internal details from the rest of the world. Encapsulation often comes with delegation. You ask a director whether she is free for a meeting; she delegates the message to her diary and gives you an answer. All well and good. There is no need to know whether the director uses a diary, an electronic gizmo, or a secretary to keep track of her appointments.

However, this can go too far. You look at a class’s interface and find half the methods are delegating to this other class. After a while, it is time to use Remove Middle Man (192) and talk to the object that really knows what’s going on. If only a few methods aren’t doing much, use Inline Function (115) to inline them into the caller. If there is additional behavior, you can use Replace Superclass with Delegate (399) or Replace Subclass with Delegate (381) to fold the middle man into the real object. That allows you to extend behavior without chasing all that delegation.

对象的基本特征之一就是封装一一对外部世界隐藏其内部细节。封装往往伴随着委托。比如，你问主管是否有时间参加一个会议，他就把这个消息「委托」给他的记事簿，然后才能回答你。很好，你没必要知道这位主管到底使用传统记事还是使用电子记事簿抑或是秘书来记录自己的约会。

但是人们可能过度运用委托。你也许会看到某个类的接口有一半的函数都委托给其他类，这样就是过度运用。这时应该使用移除中间人（192），直接和真正负责的对象打交道。如果这样「不干实事」的函数只有少数几个，可以运用内联函数（115）把它们放进调用端。如果这些中间人还有其他行为，可以运用以委托取代超类（399）或者以委托取代子类（381）把它变成真正的对象，这样你既可以扩展原对象的行为，又不必负担那么多的委托动作。

### 3.19 Insider Trading

Software people like strong walls between their modules and complain bitterly about how trading data around too much increases coupling. To make things work, some trade has to occur, but we need to reduce it to a minimum and keep it all above board.

Modules that whisper to each other by the coffee machine need to be separated by using Move Function (198) and Move Field (207) to reduce the need to chat. If modules have common interests, try to create a third module to keep that commonality in a wellregulated vehicle, or use Hide Delegate (189) to make another module act as an intermediary.

Inheritance can often lead to collusion. Subclasses are always going to know more about their parents than their parents would like them to know. If it’s time to leave home, apply Replace Subclass with Delegate (381) or Replace Superclass with Delegate (399).

软件开发者喜欢在模块之间建起高墙，极其反感在模块之间大量交换数据，因为这会增加模块的耦合。在实际情况里，一定的数据交换不可避免，但我们必须尽量减少这种情况，并把这种交换都放到明面上来。如果两个模块总是在咖啡机旁边窃窃私语，就应该用移函数（198）和搬移字段（207）减少它们的私下交流。如果两个模块有共同的兴趣，可以尝试再新建一个模块，把这些共用的数据放在一个管理良好的地方；或者用隐藏委托关系（189），把另一个模块变成两者的中介。

继承常会造成密谋，因为子类对超类的了解总是超过后者的主观愿望。如果你觉得该让这个孩子独立生活了，请运用以委托取代子类（381）或以委托取代超类（399）让它离开继承体系。

### 3.20 Large Class

When a class is trying to do too much, it often shows up as too many fields. When a class has too many fields, duplicated code cannot be far behind.

You can Extract Class (182) to bundle a number of the variables. Choose variables to go together in the component that makes sense for each. For example, “depositAmount” and “depositCurrency” are likely to belong together in a component. More generally, common prefixes or suffixes for some subset of the variables in a class suggest the opportunity for a component. If the component makes sense with inheritance, you’ll find Extract Superclass (375) or Replace Type Code with Subclasses (362) (which essentially is extracting a subclass) are often easier.

Sometimes a class does not use all of its fields all of the time. If so, you may be able to do these extractions many times.

As with a class with too many instance variables, a class with too much code is a prime breeding ground for duplicated code, chaos, and death. The simplest solution (have we mentioned that we like simple solutions?) is to eliminate redundancy in the class itself. If you have five hundred­line methods with lots of code in common, you may be able to turn them into five ten­line methods with another ten two­line methods extracted from the original.

The clients of such a class are often the best clue for splitting up the class. Look at whether clients use a subset of the features of the class. Each subset is a possible separate class. Once you’ve identified a useful subset, use Extract Class (182), Extract Superclass (375), or Replace Type Code with Subclasses (362) to break it out.

如果想利用单个类做太多事情，其内往往就会出现太多字段。一旦如此，重复代码也就接踵而至了。你可以运用提炼类（182）将几个变量一起提炼至新类内。提炼时应该选择类内彼此相关的量，将它们放在一起。例如，depositAmount 和 depositCurrency 可能应该隶属同一个类。通常，如果类内的数个变量有着相同的前缀或后缀，这就意味着有机会把它们提炼到某个组件内。如果这个组件适合作为ー个子类，你会发现提炼超类（375）或者以子类取代类型码（362）（其实就是提炼子类）往往比较简单。

有时候类并非在所有时刻都使用所有字段。若果真如此，你或许可以进行多次提炼。和「太多实例变量」一样，类内如果有太多代码，也是代码重复、混乱并最终走向死亡的源头。最简单的解决方案（还记得吗，我们喜欢简单的解决方案）是把多余的东西消弭于类内部。如果有 5 个「百行函数」，它们之中很多代码都相同，那么或许你可以把它们成 5 个「十行函数」和 10 个提炼出来的「双行函数」。

观察一个大类的使用者，经常能找到如何拆分类的线索。看看使用者是否只用到了这个类所有功能的一个子集，每个这样的子集都可能拆分成一个独立的类。一旦识出一个合适的功能子集，就试用提炼类（182）、提炼超类（375）或是以子类取代类型码（362）将其拆分出来。

### 3.21 Alternative Classes with Different Interfaces

One of the great benefits of using classes is the support for substitution, allowing one class to swap in for another in times of need. But this only works if their interfaces are the same. Use Change Function Declaration (124) to make functions match up. Often, this doesn’t go far enough; keep using Move Function (198) to move behavior into classes until the protocols match. If this leads to duplication, you may be able to use Extract Superclass (375) to atone.

使用类的好处之一就在于可以替换：今天用这个类，未来可以成用另一个类。但只有当两个类的接口一致时，才能做这种替换。可以用改变函数声明（124）将函数签名变得一致。但这往往还不够，请反复运用移函数（198）将某些行为移入类中，直到两者的协议一致为止。如果搬移过程造成了重复代码，或许可运用提炼超类（375）补偿一下。

### 3.22 Data Class

These are classes that have fields, getting and setting methods for the fields, and nothing else. Such classes are dumb data holders and are often being manipulated in far too much detail by other classes. In some stages, these classes may have public fields. If so, you should immediately apply Encapsulate Record (162) before anyone notices. Use Remove Setting Method (331) on any field that should not be changed.

Look for where these getting and setting methods are used by other classes. Try to use Move Function (198) to move behavior into the data class. If you can’t move a whole function, use Extract Function (106) to create a function that can be moved.

2『纯函数做一张术语卡片。』——已完成

Data classes are often a sign of behavior in the wrong place, which means you can make big progress by moving it from the client into the data class itself. But there are exceptions, and one of the best exceptions is a record that’s being used as a result record from a distinct function invocation. A good example of this is the intermediate data structure after you’ve applied Split Phase (154). A key characteristic of such a result record is that it’s immutable (at least in practice). Immutable fields don’t need to be encapsulated and information derived from immutable data can be represented as fields rather than getting methods.

所谓纯数据类是指：它们拥有一些字段，以及用于访问（读写）这些字段的函数，除此之外一无长物。这样的类只是一种不会说话的数据容器，它们几乎一定被其他类过分细琐地操控着。这些类早期可能拥有 public 字段，若果真如此，你应该在别人注意到它们之前，立刻运用封装记录（162）将它们封装起来。对于那些不该被其他类修改的字段，请运用移除设值函数（331）。然后，找出这些取值 / 设值函数被其他类调用的地点。尝试以移函数（198）把那些调用行为搬移到纯数据类里来。如果无法搬移整个函数，就运用提炼函数 (106) 产生一个可被搬移的函数。

纯数据类常常意味着行为被放在了错误的地方。也就是说，只要把处理数据的行为从客户端搬移到纯数据类里来，就能使情况大为改观。但也有例外情况，一个最好的例外情况就是，纯数据记录对象被用作函数调用的返回结果，比如使用拆分阶段（154）之后得到的中转数据结构就是这种情況。这种结果数据对象有一个关键的特征：它是不可修改的（至少在拆分阶段（154）的实际操作中是这样）。不可修改的字段无须封装，使用者可以直接通过字段取得数据，无须通过取值函数。

### 3.23 Refused Bequest

Subclasses get to inherit the methods and data of their parents. But what if they don’t want or need what they are given? They are given all these great gifts and pick just a few to play with.

The traditional story is that this means the hierarchy is wrong. You need to create a new sibling class and use Push Down Method (359) and Push Down Field (361) to push all the unused code to the sibling. That way the parent holds only what is common. Often, you’ll hear advice that all superclasses should be abstract.

You’ll guess from our snide use of “traditional” that we aren’t going to advise this—at least not all the time. We do subclassing to reuse a bit of behavior all the time, and we find it a perfectly good way of doing business. There is a smell—we can’t deny it—but usually it isn’t a strong smell. So, we say that if the refused bequest is causing confusion and problems, follow the traditional advice. However, don’t feel you have to do it all the time. Nine times out of ten this smell is too faint to be worth cleaning.

The smell of refused bequest is much stronger if the subclass is reusing behavior but does not want to support the interface of the superclass. We don’t mind refusing implementations—but refusing interface gets us on our high horses. In this case, however, don’t fiddle with the hierarchy; you want to gut it by applying Replace Subclass with Delegate (381) or Replace Superclass with Delegate (399).

子类应该继承超类的函数和数据。但如果它们不想或不需要继承，又该怎么办呢？它们得到所有礼物，却只从中挑选几样来玩！按传统说法，这就意味着继承体系设计错误。你需要为这个子类新建一个兄弟类，再运用函数下移（359) 和字段下移（361）把所有用不到的函数下推给那个兄弟。这样一来，超类就只持有所有子类共享的东西。你常常会听到这样的建议：所有超类都应该是抽象（abstract）的。

既然使用「传统说法」这个略带贬义的词，你就可以猜到，我们不建议你这么做，起码不建议你每次都这么做。我们经常利用继承来复用一些行为，并发现这可以很好地应用于日常工作。这也是一种坏味道，我们不否认，但气味通常并不强烈，所以我们说，如果「被拒绝的遗赠」正在引起困惑和问题，请遵循传统忠告。但不必认为你每次都得那么做。十有八九这种坏味道很淡，不值得理睬。

如果子类复用了超类的行为（实现），却又不愿意支持超类的接口，「被拒绝的遗赠」的坏味道就会变得很浓烈。拒绝继承超类的实现，这一点我们不介意；但如果拒绝支持超类的接口，这就难以接受了。既然不愿意支持超类的接口，就不要假情假意地糊弄继承体系，应该运用以委托取代子类（381）或者以委托取代超类（399）彻底划清界限。

### 2.24 Comments

Don’t worry, we aren’t saying that people shouldn’t write comments. In our olfac­tory analogy, comments aren’t a bad smell; indeed they are a sweet smell. The reason we mention comments here is that comments are often used as a deodorant. It’s surprising how often you look at thickly commented code and notice that the comments are there because the code is bad.

Comments lead us to bad code that has all the rotten whiffs we’ve discussed in the rest of this chapter. Our first action is to remove the bad smells by refactoring. When we’re finished, we often find that the comments are superfluous.

If you need a comment to explain what a block of code does, try Extract Function (106). If the method is already extracted but you still need a comment to explain what it does, use Change Function Declaration (124) to rename it. If you need to state some rules about the required state of the system, use Introduce Assertion (302).

When you feel the need to write a comment, first try to refactor the code so that any comment becomes superfluous.

A good time to use a comment is when you don’t know what to do. In addition to describing what is going on, comments can indicate areas in which you aren’t sure. A comment can also explain why you did something. This kind of information helps future modifiers, especially forgetful ones. 

别担心，我们并不是说你不该写注释。从嗅觉上说，注释不但不是一种坏味道，事实上它们还是一种香味呢。我们之所以要在这里提到注释，是因为人们常把它当作「除臭剂」来使用。常常会有这样的情况：你看到一段代码有着长长的注释，然后发现，这些注释之所以存在乃是因为代码很糟糕。这种情的发生次数之多，实在令人吃惊。

注释可以带我们找到本章先前提到的各种坏味道。找到坏味道后，我们首先应该以各种重构手法把坏味道去除。完成之后我们常常会发现：注释已经得多余了，因为代码已经清楚地说明了一切。如果你需要注释来解释一块代码做了什么，试试提炼函数（106）；如果函数已经提炼出来，但还是需要注释来解释其行为，试试用改变函数声明（124）为它改名；如果你需要注释说明某些系统的需求规格，试试引入断言（302）。

当你感觉需要写注释时，请先尝试重构，试着让所有注释都变得多余。如果你不知道该做什么，这才是注释的良好运用时机。除了用来记述将来的打算之外，注释还可以用来标记你并无十足把握的区域。你可以在注释里写下自己「为什么做某某事」。这类信息可以帮助将来的修改者，尤其是那些健忘的家伙。

## 0401. Building Tests Topics

Refactoring is a valuable tool, but it can’t come alone. To do refactoring properly, I need Tutorialsa solid suite of tests to spot my inevitable mistakes. Even with automated refactoring tools, many of my refactorings will still need checking via a test suite.

I don’t find this to be a disadvantage. Even without refactoring, writing good tests increases my effectiveness as a programmer. This was a surprise for me and is counterintuitive for most programmers—so it’s worth explaining why.

重构是很有价值的工具，但只有重构还不行。要正确地进行重构，前提是得有一套稳固的测试集合，以帮我发现难以避免的疏漏。即便有工具可以帮我自动完成一些重构，很多重构手法依然需要通过测试集合来保障。我并不把这视为缺点。我发现，编写优良的测试程序，可以极大提高我的编程速度，即使不进行重构也一样如此。这让我很吃惊，也违反许多程序员的直觉，所以我有必要解释一下这个现象。

2『测试加快开发速度。做一张反常识卡片。』——已完成

#### 4.1 The Value of Sefl-Testing Code

If you look at how most programmers spend their time, you’ll find that writing code is Sign actually Out quite a small fraction. Some time is spent figuring out what ought to be going on, some time is spent designing, but most time is spent debugging. I’m sure every reader can remember long hours of debugging—often, well into the night. Every programmer can tell a story of a bug that took a whole day (or more) to find. Fixing the bug is usually pretty quick, but finding it is a nightmare. And then, when you do fix a bug, there’s always a chance that another one will appear and that you might not even notice it till much later. And you’ll spend ages finding that bug.

如果你认真观察大多数程序员如何分配他们的时间，就会发现，他们编写代码的时间仅占所有时间中很少的一部分。有些时间用来决定下一步干什么，有些时间花在设计上，但是，花费在调试上的时间是最多的。我敢肯定，每一位读者一定都记得自己花数小时调试代码的经历 —— 而且常常是通宵达旦。每个程序员都能讲出一个为了修复一个 bug 花费了一整天（甚至更长时间）的故事。修复 bug 通常是比较快的，但找出 bug 所在却是一场噩梦。当修复一个 bug 时，常常会引起另一个 bug，却在很久之后才会注意到它。那时，你又要花上大把时间去定位问题。

The event that started me on the road to self­testing code was a talk at OOPSLA in 1992. Someone (I think it was “Bedarra” Dave Thomas) said offhandedly, “Classes should contain their own tests.” So I decided to incorporate tests into the code base together with the production code. As I was also doing iterative development, I tried adding tests as I completed each iteration. The project on which I was working at that time was quite small, so we put out iterations every week or so. Running the tests became fairly straightforward—but although it was easy, it was still pretty boring. This was because every test produced output to the console that I had to check. Now I’m a pretty lazy person and am prepared to work quite hard in order to avoid work. I realized that, instead of looking at the screen to see if it printed out some information from the model, I could get the computer to make that test. All I had to do was put the output I expected in the test code and do a comparison. Now I could run the tests and they would just print “OK” to the screen if all was well. The software was now self-testing.

我走上「自测试代码」这条路，源于 1992 年 OOPSLA 大会上的一个演讲。有个人（我记得好像是 Bedarra 公司的 DaveThomas）提到：「类应该包含它们自己的测试代码。」这让我决定，将测试代码和产品代码一起放到代码库中。当时，我正在迭代方式开发一个软件，因此，我尝试在每个迭代结束后把测试代码加上。当时我的软件项目很小，我们每周进行一次迭代。所以，运行测试变得相当简单 — 尽管非常简单，但也非常枯燥。因为每个测试都把测试结果输出到控制台中，我必须逐一检查它们。我是一个很懒的人，所以总是在当下努力工作，以免日后有更多的活儿。我意识到，其实完全不必自己盯着屏幕检验测试输出的信息是否正确，而是让计算机来帮我做检查。我需要做的就是把我所期望的输出放到测试代码中，然后做一个对比就行了。于是，我只要运行所有测试用例，假如一切都没问题，屏幕上就只出现一个「OK」。现在我的代码都能够「自测试」了。

Make sure all tests are fully automatic and that they check their own results. 确保所有测试都完全自动化，让它们检查自己的测试结果。

2『做一张金句卡片。』——已完成

Now it was easy to run tests—as easy as compiling. So I started to run tests every time I compiled. Soon, I began to notice my productivity had shot upward. I realized that I wasn’t spending so much time debugging. If I added a bug that was caught by a previous test, it would show up as soon as I ran that test. The test had worked before, so I would know that the bug was in the work I had done since I last tested. And I ran the tests frequently—which means only a few minutes had elapsed. I thus knew that the source of the bug was the code I had just written. As it was a small amount of code that was still fresh in my mind, the bug was easy to find. Bugs that would have otherwise taken an hour or more to find now took a couple of minutes at most. Not only was my software self­testing, but by running the tests frequently I had a powerful bug detector.

从此，运行测试就像执行编译一样简单。于是，我每次编译时都会运行测试。不久之后，我注意到自己的开发效率大大提高。我意识到，这是因为我没有花太多时间去测试的缘故。如果我不小心引入一个可被现有测试捕捉到的 bug，那么只要运行测试，它就会向我报告这个 bug。由于代码原本是可以正常运行的，所以我知道这个 bug 必定是在前一次运行测试后修改代码引入的。由于我频繁地运行测试，每次测试都在不久之前，因此我知道 bug 的源头就是我刚刚写下的代码。因为代码量很少，我对它也记忆犹新，所以就能轻松找出 bug。从前需要一小时甚至更多时间才能找到的 bug，现在最多只要几分钟就找到了。之所以能够拥有如此强大的 bug 侦测能力，不仅仅是因为我的代码能够自测试，也得益于我频繁地运行它们。

As I noticed this, I became more aggressive about doing the tests. Instead of waiting for the end of an increment, I would add the tests immediately after writing a bit of function. Every day I would add a couple of new features and the tests to test them. I hardly ever spent more than a few minutes hunting for a regression bug.

注意到这一点后，我对测试的积极性更高了。我不再等待每次迭代结尾时再增加测试，而是只要写好一点功能，就立即添加它们。每天我都会添加一些新功能，同时也添加相应的测试。这样，我很少花超过几分钟的时间来追查回归错误。

A suite of tests is a powerful bug detector that decapitates the time it takes to find bugs. 一套测试就是一个强大的 bug 侦测器，能够大大缩减查找 bug 所需的时间。

Tools for writing and organizing these tests have developed a great deal since my experiments. While flying from Switzerland to Atlanta for OOPSLA 1997, Kent Beck paired with Erich Gamma to port his unit testing framework from Smalltalk to Java. The resulting framework, called JUnit, has been enormously influential for program testing, inspiring a huge variety of similar tools [mf­xunit] in lots of different languages.

从我最早的试验开始到现在为止，编写和组织自动化测试的工具已经有了长足的发展。1997 年，Kent Beck 从瑞士飞往亚特兰大去参加当年的 OOPSLA 会议，在飞机上他与 Erich Gamma 结对，把他为 Smalltalk 撰写的测试框架移植到了 Java 上。由此诞生的 JUnit 框架在测试领域影响力非凡，也在不同的编程语言中催生了很多类似的工具 [mfxunit]。

Admittedly, it is not so easy to persuade others to follow this route. Writing the tests means a lot of extra code to write. Unless you have actually experienced how it speeds programming, self­testing does not seem to make sense. This is not helped by the fact that many people have never learned to write tests or even to think about tests. When tests are manual, they are gut­wrenchingly boring. But when they are automatic, tests can actually be quite fun to write. In fact, one of the most useful times to write tests is before I start programming. When I need to add a feature, I begin by writing the test. This isn’t as backward as it sounds. By writing the test, I’m asking myself what needs to be done to add the function. Writing the test also concentrates me on the interface rather than the implementation (always a good thing). It also means I have a clear point at which I’m done coding when the test works.

2『好像抓到一块大大的金子。在添加新功能之前就先写测试的代码（测试接口），比如 JS 的 jasmine 的 describe()，先在测试工具里实现想要的功能，这个时候你反而关注接口而非实现，这个阶段就是 TDD 大三阶段「红 -> 绿 -> 橙」中的红，接着在源码里去写实现代码进入「绿」的阶段，然后再通过「重构」进入「橙」阶段。做一张任意卡片。（2020-06-16）』——已完成

我得承认，说服别人也这么做并不容易。编写测试程序，意味着要写很多额外的代码。除非你确实体会到这种方法是如何提升编程速度的，否则自测试似乎就没什么意义。很多人根本没学过如何编写测试程序，甚至根本没考虑过测试，这对于编写自测试也很不利。如果测试需要手动运行，那的确是令人烦闷。但是，如果测试可以自动运行，编写测试代码就会真的很有趣。

事实上，撰写测试代码的最好时机是在开始动手编码之前。当我需要添加特性时，我会先编写相应的测试代码。听起来离经叛道，其实不然。编写测试代码其实就是在问自己：为了添加这个功能，我需要实现些什么？编写测试代码还能帮我把注意力集中于接口而非实现（这永远是一件好事）。预先写好的测试代码也为我的工作安上一个明确的结束标志：一旦测试代码正常运行，工作就可以结束了。

Kent Beck baked this habit of writing the test first into a technique called Test­-Driven Development (TDD) [mf­tdd]. The Test­Driven Development approach to programming relies on short cycles of writing a (failing) test, writing the code to make that test work, and refactoring to ensure the result is as clean as possible. This test-code­-refactor cycle should occur many times per hour, and can be a very productive and calming way to write code. I’m not going to discuss it further here, but I do use and warmly recommend it.

Kent Beck 将这种先写测试的习惯提炼成一门技艺，叫测试驱动开发（Test-DrivenDevelopment，TDD）[mftdd]。测试驱动开发的编程方式依赖于下面这个短循环：先编写一个（失败的）测试，编写代码使测试通过，然后进行重构以保证代码整洁。这个「测试、编码、重构」的循环应该在每个小时内都完成很多次。这种良好的节奏感可使编程工作以更加高效、有条不紊的方式开展。我就不在这里再做更深入的介绍，但我自己确实经常使用，也非常建议你试一试。

That’s enough of the polemic. Although I believe everyone would benefit by writing self-testing code, it is not the point of this book. This book is about refactoring. Refactoring requires tests. If you want to refactor, you have to write tests. This chapter gives you a start in doing this for JavaScript. This is not a testing book, so I’m not going to go into much detail. I’ve found, however, that with testing a remarkably small amount of work can have surprisingly big benefits.

As with everything else in this book, I describe the testing approach using examples. When I develop code, I write the tests as I go. But sometimes, I need to refactor some code without tests—then I have to make the code self­testing before I begin.

大道理先放在一边。尽管我相信每个人都可以从编写自测试代码中收益，但这并不是本书的重点。本书谈的是重构，而重构需要测试。如果你想重构，就必须编写测试。本章会带你入门，教你如何在 JavaScript 中编写简单的测试，但它不是一本专门讲测试的书，所以我不想讲得太细。但我发现，少许测试往往就足以带来惊人的收益。和本书其他内容一样，我以示例来介绍测试手法。开发软件的时候，我一边写代码，一边写测试。但有时我也需要重构一些没有测试的代码。在重构之前，我得先改造这些代码，使其能够自测试才行。

### 4.2 Sample Code to Test

Here’s some code to look at and test. The code supports a simple application that allows a user to examine and manipulate a production plan. The (crude) UI looks like this: 

The production plan has a demand and price for each province. Each province has producers, each of which can produce a certain number of units at a particular price. The UI also shows how much revenue each producer would earn if they sell all their production. At the bottom, the screen shows the shortfall in production (the demand minus the total production) and the profit for this plan. The UI allows the user to manipulate the demand, price, and the individual producer’s production and costs to see the effect on the production shortfall and profits. Whenever a user changes any number in the display, all the others update immediately.

这里我展示了一份有待测试的代码。这份代码来自一个简单的应用，用于支持用户查看并调整生产计划。它的（略显粗糙的）界面长得像下面这张图所示的这样。每个行省（province）都有一份生产计划，计划中包含需求量（demand）和采购价格（price）。每个行省都有一些生产商（producer），他们各自以不同的成本价（cost）供应一定数量的产品。界面上还会显示，当商家售出所有的商品时，他们可以获得的总收入（fullrevenue）。页面底部展示了该区域的产品缺额（需求量减去总产量）和总利润（profit）。用户可以在界面上修改需求量及采购价格，以及不同生产商的产量（production）和成本价，以观察缺额和总利润的变化。用户在界面上修改任何数值时，其他的数值都会同时得到更新。

I’m showing a user interface here, so you can sense how the software is used, but I’m only going to concentrate on the business logic part of the software—that is, the classes that calculate the profit and the shortfall, not the code that generates the HTML and hooks up the field changes to the underlying business logic. This chapter is just an introduction to the world of self-­testing code, so it makes sense for me to start with the easiest case—which is code that doesn’t involve user interface, persistence, or external service interaction. Such separation, however, is a good idea in any case: Once this kind of business logic gets at all complicated, I will separate it from the UI mechanics so I can more easily reason about it and test it.

1『业务逻辑代码和前端的展示代码隔离。』

这里我展示了一个用户界面，是为了让你了解该应用的使用方式，但我只会聚焦于软件的业务逻辑部分，也就是那些计算利润和缺额的类，而非那些生成 HTML 或监听页面字段更新的代码。本章只是先带你走进自测试代码世界的大门，因而最好是从最简单的例子开始，也就是那些不涉及用户界面、持久化或外部服务交互的代码。这种隔离的思路其实在任何场景下都适用：一旦业务逻辑的部分开始变复杂，我就会把它与 UI 分离开，以便能更好地理解和测试它。

This business logic code involves two classes: one that represents a single producer, and the other that represents a whole province. The province’s constructor takes a JavaScript object—one we could imagine being supplied by a JSON document.

Here’s the code that loads the province from the JSON data:

```js
class Province {
    constructor(doc) {
        this._name = doc.name;
        this._producers = [];
        this._totalProduction = 0;
        this._demand = doc.demand;
        this._price = doc.price;
        doc.producers.forEach(d => this.addProducer(new Producer(this, d)));
    }
    addProducer(arg) {
        this._producers.push(arg);
        this._totalProduction += arg.production;
    }
}
```

This function creates suitable JSON data. I can create a sample province for testing by constructing a province object with the result of this function.

top level…

```js
function sampleProvinceData() {
    return {
        name: 'Asia',
        producers: [
            {name: 'Byzatium', cost: 10, production: 9},
            {name: 'Attaliz', cost: 12, production: 10},
            {name: 'Sinope', cost: 10, production: 6},
        ],
        demand: 30,
        price: 20,        
    };
}
```

The province class has accessors for the various data values:

class Province…

```js
    get name() {
        return this._name;
    }
    get producers() {
        return this._producers.slice();
    }
    set totalProduction(arg) {
        this._totalProduction = arg;
    }
    get demand() {
        return this._demand;
    }
    set demand(arg) {
        this._demand = parseInt(arg);
    }
    get price() {
        return this._price;
    }
    set price(arg) {
        this._price = parseInt(arg);
    }
```

The setters will be called with strings from the UI that contain the numbers, so I need to parse the numbers to use them reliably in calculations. The producer class is mostly a simple data holder:

class Producer…

```js
class Producer {
    constructor(aProvince, data) {
        this._province = aProvince;
        this._cost = data.cost;
        this._name = data.name;
        this._production = data.production || 0;
    }
    get name() {
        return this._name;
    }
    get cost() {
        return this._cost;
    }
    set cost(arg) {
        this._cost = parseInt(arg);
    }
    get production() {
        return this._production;
    }
    set production(amountStr) {
        const amount = parseInt(amountStr);
        const newProduction = Number.isNaN(amount) ? 0 : amount;
        this._province.totalProduction += newProduction - this._production;
        this._production = newProduction;
    }
}
```

The way that set production updates the derived data in the province is ugly, and whenever I see that I want to refactor to remove it. But I have to write tests before that I can refactor it. The calculation for the shortfall is simple.

class Province…

```js
    get shortfall() {
        return this._demand - this.totalProduction;
    }
```

That for the profit is a bit more involved. 

class Province…

```js
    get profit() {
        return this.demandValue - this.demandCost;
    }
    get demandCost() {
        let remainingDemand = this.demand;
        let result = 0;
        this.producers
            .sort((a, b) => a.cost - b.cost)
            .forEach(p => {
                const contribution = Math.min(remainingDemand, p.production);
                remainingDemand -= contribution;
                result += contribution * p.cost;
            });
        return result;
    }
    get demandValue() {
        return this.satisfiedDemand * this.price;
    }
    get satisfiedDemand() {
        return Math.min(this._demand, this.totalProduction);
    }
```

### 4.3 A First Test

To test this code, I’ll need some sort of testing framework. There are many out there, even just for JavaScript. The one I’ll use is Mocha [mocha], which is reasonably common and well­-regarded. I won’t go into a full explanation of how to use the framework, just show some example tests with it. You should be able to adapt, easily enough, a different framework to build similar tests. Here is a simple test for the shortfall calculation:

```js
describe('province', function() { 
    it('shortfall', function() { 
        const asia = new Province(sampleProvinceData()); 
        assert.equal(asia.shortfall, 5); 
    }); 
});
```

1『

按作者的源码，this.totalProduction 没值，是 NaN，最后发现是自己漏掉了 totalProduction 的 get 函数。魔鬼在细节。

```
    get totalProduction() {
        return this._totalProduction;
    }
```

用 jasmine 实现：

src/profit.js

```js
class Province {
    constructor(doc) {
        this._name = doc.name;
        this._producers = [];
        this._totalProduction = 0;
        this._demand = doc.demand;
        this._price = doc.price;
        doc.producers.forEach(d => this.addProducer(new Producer(this, d)));
    }
    addProducer(arg) {
        this._producers.push(arg);
        this._totalProduction += arg.production;
    }
    get name() {
        return this._name;
    }
    get producers() {
        return this._producers.slice();
    }
    get totalProduction() {
        return this._totalProduction;
    }
    set totalProduction(arg) {
        this._totalProduction = arg;
    }
    get demand() {
        return this._demand;
    }
    set demand(arg) {
        this._demand = parseInt(arg);
    }
    get price() {
        return this._price;
    }
    set price(arg) {
        this._price = parseInt(arg);
    }

    get shortfall() {
        return this._demand - this.totalProduction;
    }

    get profit() {
        return this.demandValue - this.demandCost;
    }
    get demandCost() {
        let remainingDemand = this.demand;
        let result = 0;
        this.producers
            .sort((a, b) => a.cost - b.cost)
            .forEach(p => {
                const contribution = Math.min(remainingDemand, p.production);
                remainingDemand -= contribution;
                result += contribution * p.cost;
            });
        return result;
    }
    get demandValue() {
        return this.satisfiedDemand * this.price;
    }
    get satisfiedDemand() {
        return Math.min(this._demand, this.totalProduction);
    }
}

class Producer {
    constructor(aProvince, data) {
        this._province = aProvince;
        this._cost = data.cost;
        this._name = data.name;
        this._production = data.production || 0;
    }
    get name() {
        return this._name;
    }
    get cost() {
        return this._cost;
    }
    set cost(arg) {
        this._cost = parseInt(arg);
    }
    get production() {
        return this._production;
    }
    set production(amountStr) {
        const amount = parseInt(amountStr);
        const newProduction = Number.isNaN(amount) ? 0 : amount;
        this._province.totalProduction += newProduction - this._production;
        this._production = newProduction;
    }
}

function sampleProvinceData() {
    return {
        name: 'Asia',
        producers: [
            {name: 'Byzatium', cost: 10, production: 9},
            {name: 'Attaliz', cost: 12, production: 10},
            {name: 'Sinope', cost: 10, production: 6},
        ],
        demand: 30,
        price: 20,        
    };
}
```

spec/profitSpec.js

```js
describe('province', function() {
    it('shortfall', function() {
        const asia = new Province(sampleProvinceData());
        console.log(asia);
        expect(asia.shortfall).toEqual(5);
    });
});
```

』

The Mocha framework divides up the test code into blocks, each grouping together a suite of tests. Each test appears in an it block. For this simple case, the test has two steps. The first step sets up some fixture—data and objects that are needed for the test: in this case, a loaded province object. The second line verifies some characteristic of that fixture—in this case, that the shortfall is the amount that should be expected given the initial data.

Mocha 框架组织测试代码的方式是将其分组，每一组下包含一套相关的测试。测试需要写在一个 it 块中。对于这个简单的例子，测试包含了两个步骤。第一步设置好一些测试夹具（fixture），也就是测试所需要的数据和对象等（就本例而言是一个加载好了的行省对象）；第二步则是验证测试夹具是否具备某些特征（就本例而言则是验证算出的缺额应该是期望的值）。

Different developers use the descriptive strings in the describe and it blocks differently. Some would write a sentence that explains what the test is testing, but others prefer to leave them empty, arguing that the descriptive sentence is just duplicating the code in the same way a comment does. I like to put in just enough to identify which test is which when I get failures. If I run this test in a NodeJS console, the output looks like this:

不同开发者在 describe 和 it 块里撰写的描述信息各有不同。有的人会写一个描述性的句子解释测试的内容，也有人什么都不写，认为所谓描述性的句子跟注释一样，不外乎是重复代码已经表达的东西。我个人不喜欢多写，只要测试失败时足以识别出对应的测试就够了。如果我在 NodeJS 的控制台下运行这个测试，那么其输出看起来是这样：

```
’’’’’’’’’’’’’’

1 passing (61ms)
```

Note the simplicity of the feedback—just a summary of how many tests are run and how many have passed.

Always make sure a test will fail when it should.

2『总是确保测试不该通过时真的会失败。一个要先自己写一个错误的测试，此时终于明白这个概念了（2020-06-17）。做一张金句卡片。』——已完成

When I write a test against existing code like this, it’s nice to see that all is well—but I’m naturally skeptical. Particularly, once I have a lot of tests running, I’m always nervous that a test isn’t really exercising the code the way I think it is, and thus won’t catch a bug when I need it to. So I like to see every test fail at least once when I write it. My favorite way of doing that is to temporarily inject a fault into the code, for example:

它的反馈极其简洁，只包含了已运行的测试数量以及测试通过的数量。当我为类似的既有代码编写测试时，发现一切正常工作固然是好，但我天然持怀疑精神。特别是有很多测试在运行时，我总会担心测试没有按我期望的方式检查结果，从而没法在实际出错的时候抓到 bug。因此编写测试时，我想看到每个测试都至少失败一遍。我最爱的方式莫过于在代码中暂时引入一个错误，像这样：

class Province…

```
get shortfall() { 
    return this._demand ­- this.totalProduction * 2; 
}
```

Here’s what the console now looks like:

```
0 passing (72ms) 
1 failing

1) province shortfall:
AssertionError: expected ­20 to equal 5 
at Context.<anonymous> (src/tester.js:10:12)
```

The framework indicates which test failed and gives some information about the nature of the failure—in this case, what value was expected and what value actually turned up. I therefore notice at once that something failed—and I can immediately see which tests failed, giving me a clue as to what went wrong (and, in this case, confirming the failure was where I injected it). 

框架会报告哪个测试失败了，并给出失败的根本原因 —— 这里是因为实际算出的值与期望的值不相符。于是我总算见到有什么东西失败了，并且还能马上看到是哪个测试失败，获得一些出错的线索（这个例子中，我还能确认这就是我引入的那个错误）。

Run tests frequently. Run those exercising the code you’re working on at least every few minutes; run all tests at least daily. 

频繁地运行测试。对于你正在处理的代码，与其对应的测试至少每隔几分钟就要运行一次，每天至少运行一次所有的测试。

1『这个习惯做一张任意卡片。』——已完成

In a real system, I might have thousands of tests. A good test framework allows me to run them easily and to quickly see if any have failed. This simple feedback is essential to self-­testing code. When I work, I’ll be running tests very frequently—checking progress with new code or checking for mistakes with refactoring.

一个真实的系统可能拥有数千个测试。好的测试框架应该能帮我简单快速地运行这些测试，一旦出错，我能马上看到。尽管这种反馈非常简单，但对自测试代码来说却尤为重要。工作时我会非常频繁地运行测试，要么是检验新代码的进展，要么是检查重构过程是否出错。

The Mocha framework can use different libraries, which it calls assertion libraries, to verify the fixture for a test. Being JavaScript, there are a quadzillion of them out there, some of which may still be current when you’re reading this. The one I’m using at the moment is Chai [chai]. Chai allows me to write my validations either using an “assert” style:

Mocha 框架允许使用不同的库（它称之为断言库）来验证测试的正确性。JavaScript 世界的断言库，连在一起都可以绕地球一周了，当你读到这里时，可能有些仍然还没过时。我现在使用的库是 Chai，它可以支持我编写不同类型的断言，比如「assert」风格的，或者是「expect」风格的：

```js
describe('province', function() { 
    it('shortfall', function() { 
        const asia = new Province(sampleProvinceData()); 
        assert.equal(asia.shortfall, 5); 
    }); 
});
```

or an “expect” style:

```js
describe('province', function() { 
    it('shortfall', function() { 
        const asia = new Province(sampleProvinceData()); 
        expect(asia.shortfall).equal(5); 
    }); 
});
```

I usually prefer the assert style, but at the moment I mostly use the expect style while working in JavaScript.

一般来讲我更倾向于使用 assert 风格的断言，但使用 JavaScript 时我倒是更常使用 expect 的风格。

Different environments provide different ways to run tests. When I’m programming in Java, I use an IDE that gives me a graphical test runner. Its progress bar is green as long as all the tests pass, and turns red should any of them fail. My colleagues often use the phrases “green bar” and “red bar” to describe the state of tests. I might say, “Never refactor on a red bar,” meaning you shouldn’t be refactoring if your test suite has a failing test. Or, I might say, “Revert to green” to say you should undo recent changes and go back to the last state where you had all­-passing test suite (usually by going back to a recent version­-control checkpoint).

Graphical test runners are nice, but not essential. I usually have my tests set to run from a single key in Emacs, and observe the text feedback in my compilation window. The key point is that I can quickly see if my tests are all OK.

环境不同，运行测试的方式也不同。使用 Java 编程时，我使用 IDE 的图形化测试运行界面。它有一个进度条，所有测试都通过时就会显示绿色；只要有任何测试失败，它就会变成红色。我的同事们经常使用「绿色条」和「红色条」来指代测试的状态。我可能会讲「看到红条时永远不许进行重构」，意思是：测试集合中还有失败的测试时就不应该先去重构。有时我也会讲「回退到绿条」，表示你应该撤销最近一次更改，将测试恢复到上一次全部通过的状态（通常是切回到版本控制的最近一次提交点）。图形化测试界面的确很棒，但并不是必需的。我通常会在 Emacs 中配置一个运行测试的快捷键，然后在编译窗口中观察纯文本的反馈。要点在于，我必须能快速地知道测试是否全部都通过了。

### 4.4 Add Another Test

Now I’ll continue adding more tests. The style I follow is to look at all the things the class should do and test each one of them for any conditions that might cause the class to fail. This is not the same as testing every public method, which is what some programmers advocate. Testing should be risk­-driven; remember, I’m trying to find bugs, now or in the future. Therefore I don’t test accessors that just read and write a field: They are so simple that I’m not likely to find a bug there.

现在，我将继续添加更多测试。我遵循的风格是：观察被测试类应该做的所有事情，然后对这个类的每个行为进行测试，包括各种可能使它发生异常的边界条件。这不同于某些程序员提倡的「测试所有 public 函数」的风格。记住，测试应该是一种风险驱动的行为，我测试的目标是希望找出现在或未来可能出现的 bug。所以我不会去测试那些仅仅读或写一个字段的访问函数，因为它们太简单了，不太可能出错。

2『对每个类的每个行为做测试。测试的颗粒度做一个计算机任意卡片。』——已完成

This is important because trying to write too many tests usually leads to not writing enough. I get many benefits from testing even if I do only a little testing. My focus is to test the areas that I’m most worried about going wrong. That way I get the most benefit for my testing effort.

这一点很重要，因为如果尝试撰写过多测试，结果往往反而导致测试不充分。事实上，即使我只做一点点测试，也从中获益良多。测试的重点应该是那些我最担心出错的部分，这样就能从测试工作中得到最大利益。

It is better to write and run incomplete tests than not to run complete tests.

编写未臻完善的测试并经常运行，好过对完美测试的无尽等待。

So I’ll start by hitting the other main output for this code—the profit calculation. Again, I’ll just do a basic test for profit on my initial fixture.

接下来，我的目光落到了代码的另一个主要输出上，也就是总利润的计算。我同样可以在一开始的测试夹具上，对总利润做一个基本的测试。

```js
describe('province', function() {
    it('shortfall', function() {
        const asia = new Province(sampleProvinceData());
        console.log(asia);
        expect(asia.shortfall).toEqual(5);
    });
    it('profit', function() {
        const asia = new Province(sampleProvinceData());
        expect(asia.profit).toEqual(230);
    })
});
```

That shows the final result, but the way I got it was by first setting the expected value to a placeholder, then replacing it with whatever the program produced (230). I could have calculated it by hand myself, but since the code is supposed to be working correctly, I’ll just trust it for now. Once I have that new test working correctly, I break it by altering the profit calculation with a spurious * 2. I satisfy myself that the test fails as it should, then revert my injected fault. This pattern—write with a placeholder for the expected value, replace the placeholder with the code’s actual value, inject a fault, revert the fault—is a common one I use when adding tests to existing code.

There is some duplication between these tests—both of them set up the fixture with the same first line. Just as I’m suspicious of duplicated code in regular code, I’m suspicious of it in test code, so will look to remove it by factoring to a common place. One option is to raise the constant to the outer scope.

这是最终写出来的测试，但我是怎么写出它来的呢？首先我随便给测试的期望值写了一个数，然后运行测试，将程序产生的实际值（230）填回去。当然，我也可以自己手动计算，不过，既然现在的代码是能正常运行的，我就选择暂时相信它。测试可以正常工作后，我又故技重施，在利润的计算过程插入一个假的乘以 2 逻辑来破坏测试。如我所料，测试会失败，这时我才满意地将插入的假逻辑恢复过来。这个模式是我为既有代码添加测试时最常用的方法：先随便填写一个期望值，再用程序产生的真实值来替换它，然后引入一个错误，最后恢复错误。这个测试随即产生了一些重复代码 —— 它们都在第一行里初始化了同一个测试夹具。正如我对一般的重复代码抱持怀疑，测试代码中的重复同样令我心生疑惑，因此我要试着将它们提到一处公共的地方，以此来消灭重复。一种方案就是把常量提取到外层作用域里。

2『这种写测试的具体实操方法实在太 NB 了，「既有代码添加测试的具体步骤」，做一张术语卡片。』——以完成

```js
describe('province', function() {
    const asia = new Province(sampleProvinceData());    // DON'T DO THIS
    it('shortfall', function() {
        const asia = new Province(sampleProvinceData());
        console.log(asia);
        expect(asia.shortfall).toEqual(5);
    });
    it('profit', function() {
        
        expect(asia.profit).toEqual(230);
    })
});

```

But as the comment indicates, I never do this. It will work for the moment, but it introduces a petri dish that’s primed for one of the nastiest bugs in testing—a shared fixture which causes tests to interact. The const keyword in JavaScript only means the reference to asia is constant, not the content of that object. Should a future test change that common object, I’ll end up with intermittent test failures due to tests interacting through the shared fixture, yielding different results depending on what order the tests are run in. That’s a nondeterminism in the tests that can lead to long and difficult debugging at best, and a collapse of confidence in the tests at worst. Instead, I prefer to do this:

但正如代码注释所说的，我从不这样做。这样做的确能解决一时的问题，但共享测试夹具会使测试间产生交互，这是滋生 bug 的温床 —— 还是你写测试时能遇见的最恶心的 bug 之一。使用了 JavaScript 中的 const 关键字只表明 asia 的引用不可修改，不表明对象的内容也不可修改。如果未来有一个测试改变了这个共享对象，测试就可能时不时失败，因为测试之间会通过共享夹具产生交互，而测试的结果就会受测试运行次序的影响。测试结果的这种不确定性，往往使你陷入漫长而又艰难的调试，严重时甚至可能令你对测试体系的信心产生动摇。因此，我比较推荐采取下面的做法：

```js
describe('province', function() {
    let asia;
    beforeEach(function() {
        asia = new Province(sampleProvinceData());
    })
    it('shortfall', function() {
        console.log(asia);
        expect(asia.shortfall).toEqual(5);
    });
    it('profit', function() {
        expect(asia.profit).toEqual(230);
    })
});
```

The beforeEach clause is run before each test runs, clearing out asia and setting it to a fresh value each time. This way I build a fresh fixture before each test is run, which keeps the tests isolated and prevents the nondeterminism that causes so much trouble.

1『 beforeEach 即断言前的前置处理。』

beforeEach 子句会在每个测试之前运行一遍，将 asia 变量清空，每次都给它赋一个新的值。这样我就能在每个测试开始前，为它们各自构建一套新的测试夹具，这保证了测试的独立性，避免了可能带来麻烦的不确定性。

When I give this advice, some people are concerned that building a fresh fixture every time will slow down the tests. Most of the time, it won’t be noticeable. If it is a problem, I’d consider a shared fixture, but then I will need to be really careful that no test ever changes it. I can also use a shared fixture if I’m sure it is truly immutable. But my reflex is to use a fresh fixture because the debugging cost of making a mistake with a shared fixture has bit me too often in the past.

对于这样的建议，有人可能会担心，每次创建一个崭新的测试夹具会拖慢测试的运行速度。大多数时候，时间上的差别几乎无法察觉。如果运行速度真的成为问题，我也可以考虑共享测试夹具，但这样我就得非常小心，确保没有测试会去更改它。如果我能够确定测试夹具是百分之百不可变的，那么也可以共享它。但我的本能反应还是要使用独立的测试夹具，可能因为我过去尝过了太多共享测试夹具带来的苦果。

Given I run the setup code in beforeEach with every test, why not leave the setup code inside the individual it blocks? I like my tests to all operate on a common bit of fixture, so I can become familiar with that standard fixture and see the various characteristics to test on it. The presence of the beforeEach block signals to the reader that I’m using a standard fixture. You can then look at all the tests within the scope of that describe block and know they all take the same base data as a starting point.

既然我在 beforeEach 里运行的代码会对每个测试生效，那么为何不直接把它挪到每个 it 块里呢？让所有测试共享一段测试夹具代码的原因，是为了使我对公用的夹具代码感到熟悉，从而将眼光聚焦于每个测试的不同之处。beforeEach 块旨在告诉读者，我使用了同一套标准夹具。你可以接着阅读 describe 块里的所有测试，并知道它们都是基于同样的数据展开测试的。

### 4.5 Modifying The Fixture

So far, the tests I’ve written show how I probe the properties of the fixture once I’ve loaded it. But in use, that fixture will be regularly updated by the users as they change values. Most of the updates are simple setters, and I don’t usually bother to test those as there’s little chance they will be the source of a bug. But there is some complicated behavior around Producer’s production setter, so I think that’s worth a test.

加载完测试夹具后，我编写了一些测试来探查它的一些特性。但在实际应用中，该夹具可能会被频繁更新，因为用户可能在界面上修改数值。大多数更新都是通过设值函数完成的，我一般也不会测试这些方法，因为它们不太可能出什么 bug。不过 Producer 类中的产量（production）字段，其设值函数行为比较复杂，我觉得它倒是值得一测。

describe(’province’…

```js
describe('province', function() {
    let asia;
    beforeEach(function() {
        asia = new Province(sampleProvinceData());
    })
    it('shortfall', function() {
        console.log(asia);
        expect(asia.shortfall).toEqual(5);
    });
    it('profit', function() {
        expect(asia.profit).toEqual(230);
    })
    it('change production', function() {
        asia.producers[0].production = 20;
        expect(asia.shortfall).toEqual(-6);
        expect(asia.profit).toEqual(292);
    })
});
```

This is a common pattern. I take the initial standard fixture that’s set up by the beforeEach block, I exercise that fixture for the test, then I verify the fixture has done what I think it should have done. If you read much about testing, you’ll hear these phases described variously as setup-­exercise-­verify, given-­when-­then, or arrange­-act-assert. Sometimes you’ll see all the steps present within the test itself, in other cases the common early phases can be pushed out into standard setup routines such as beforeEach.

这是一个常见的测试模式。我拿到 beforeEach 配置好的初始标准夹具，然后对该夹具进行必要的检查，最后验证它是否表现出我期望的行为。如果你读过测试相关的资料，就会经常听到各种类似的术语，比如配置 - 检查 - 验证（setup-exercise-verify）、given-when-then 或者准备 - 行为 - 断言（arrange-act-assert）等。有时你能在一个测试里见到所有的步骤，有时那些早期的公用阶段会被提到一些标准的配置步骤里，诸如 beforeEach 等。

(There is an implicit fourth phase that’s usually not mentioned: teardown. Teardown removes the fixture between tests so that different tests don’t interact with each other. By doing all my setup in beforeEach, I allow the test framework to implicitly tear down my fixture between tests, so I can take the teardown phase for granted. Most writers on tests gloss over teardown—reasonably so, since most of the time we ignore it. But occasionally, it can be important to have an explicit teardown operation, particularly if we have a fixture that we have to share between tests because it’s slow to create.)

（其实还有第四个阶段，只是不那么明显，一般很少提及，那就是拆除阶段。此阶段可将测试夹具移除，以确保不同测试之间不会产生交互。因为我是在 beforeEach 中配置好数据的，所以测试框架会默认在不同的测试间将我的测试夹具移除，相当于我自动享受了拆除阶段带来的便利。多数测试文献的作者对拆除阶段一笔带过，这可以理解，因为多数时候我们可以忽略它。但有时因为创建缓慢等原因，我们会在不同的测试间共享测试夹具，此时，显式地声明一个拆除操作就是很重要的。）

In this test, I’m verifying two different characteristics in a single it clause. As a general rule, it’s wise to have only a single verify statement in each it clause. This is because the test will fail on the first verification failure—which can often hide useful information when you’re figuring out why a test is broken. In this case, I feel the two are closely enough connected that I’m happy to have them in the same test. Should I wish to separate them into separate it clauses, I can do that later.

1『一般在一个 it 语句里只写一个测试。』

在这个测试中，我在一个 it 语句里验证了两个不同的特性。作为一个基本规则，一个 it 语句中最好只有一个验证语句，否则测试可能在进行第一个验证时就失败，这通常会掩盖一些重要的错误信息，不利于你了解测试失败的原因。不过，在上面的场景中，我觉得两个断言本身关系非常紧密，写在同一个测试中问题不大。如果稍后需要将它们分离到不同的 it 语句中，我可以到时再做。

### 4.6 Probing The Boundaries

So far my tests have focused on regular usage, often referred to as “happy path” conditions where everything is going OK and things are used as expected. But it’s also good to throw tests at the boundaries of these conditions—to see what happens when things might go wrong. Whenever I have a collection of something, such as producers in this example, I like to see what happens when it’s empty.

到目前为止我的测试都聚焦于正常的行为上，这通常也被称为「正常路径」（happy-path），它指的是一切工作正常、用户使用方式也最符合规范的那种场景。同时，把测试推到这些条件的边界处也是不错的实践，这可以检查操作出错时软件的表现。无论何时，当我拿到一个集合（比如说此例中的生产商集合）时，我总想看看集合为空时会发生什么。

```js
describe('no producers', function() {
    let noProducers;
    beforeEach(function() {
        const data = {
            name: 'No producers',
            producers: [],
            demand: 30,
            price: 20,
        };
        noProducers = new Province(data);
        console.log(noProducers);
    });
    it('shortfall', function() {
        expect(noProducers.shortfall).toEqual(30);
    });
    it('profit', function() {
        expect(noProducers.profit).toEqual(0);
    })
})
```

With numbers, zeros are good things to probe:

如果拿到的是数值类型，0 会是不错的边界条件：

describe(’province’…

```js
    it('zero demand', function() {
        asia.demand = 0;
        expect(asia.shortfall).toEqual(-25);
        expect(asia.profit).toEqual(0);
    })
```

as are negatives:

describe(’province’… 

```js
    it('negative demand', function() {
        asia.demand = -1;
        expect(asia.shortfall).toEqual(-26);
        expect(asia.profit).toEqual(-10);
    })
```

At this point, I may start to wonder if a negative demand resulting in a negative profit really makes any sense for the domain. Shouldn’t the minimum demand be zero? In which case, perhaps, the setter should react differently to a negative argument—raising an error or setting the value to zero anyway. These are good questions to ask, and writing tests like this helps me think about how the code ought to react to boundary cases.

1『哇塞，太棒了。通过写「测试」，比如把 demand 设为负值，引发思考，负值在该业务领域里代表什么？边界是 0 么？出现负值时该如何处理，即在代码里写「异常处理逻辑」。总之，测试可以作为开发时触发自己思考的钩子，「测试驱动开发」嘛。（2020-06-17）』

测试到这里，我不禁有一个想法：对于这个业务领域来讲，提供一个负的需求值，并算出一个负的利润值意义何在？最小的需求量不应该是 0 吗？或许，设值方法需要对负值有些不同的行为，比如抛出错误，或总是将值设置为 0。这些问题都很好，编写这样的测试能帮助我思考代码本应如何应对边界场景。

Think of the boundary conditions under which things might go wrong and concentrate your tests there.

考虑可能出错的边界条件，把测试火力集中在那儿。

2『做一张金句卡片。』——已完成

The setters take a string from the fields in the UI, which are constrained to only accept numbers—but they can still be blank, so I should have tests that ensure the code responds to the blanks the way I want it to.

设值函数接收的字符串是从 UI 上的字段读来的，它已经被限制为只能填入数字，但仍然有可能是空字符串，因此同样需要测试来保证代码对空字符串的处理方式符合我的期望。

describe(’province’…

```js
    it('empty string demand', function() {
        asia.demand = '';
        expect(asia.shortfall).toBeNaN();
        expect(asia.profit).toBeNaN();
    });
```

Notice how I’m playing the part of an enemy to my code. I’m actively thinking about how I can break it. I find that state of mind to be both productive and fun. It indulges the mean­spirited part of my psyche. This one is interesting:

可以看到，我在这里扮演「程序公敌」的角色。我积极思考如何破坏代码。我发现这种思维能够提高生产力，并且很有趣 —— 它纵容了我内心中比较促狭的那一部分。这个测试结果很有意思：

```js
describe('string for producers', function() {
    it('', function() {
        const data = {
            name: 'String producers',
            producers: '',
            demand: 30,
            price: 20,
        };
        const prov = new Province(data);
        expect(prov.shortfall).toEqual(0);
    })
})
```

This doesn’t produce a simple failure reporting that the shortfall isn’t 0. Here’s the console output:

```
’’’’’’’’’!

9 passing (74ms) 1 failing

1) string for producers :
TypeError: doc.producers.forEach is not a function 
at new Province (src/main.js:22:19) 
at Context.<anonymous> (src/tester.js:86:18)
```

Mocha treats this as a failure—but many testing frameworks distinguish between this situation, which they call an error, and a regular failure. A failure indicates a verify step where the actual value is outside the bounds expected by the verify statement. But this error is a different animal—it’s an exception raised during an earlier phase (in this case, the setup). This looks like an exception that the authors of the code hadn’t anticipated, so we get an error sadly familiar to JavaScript programmers (“… is not a function”).

Mocha 把这也当作测试失败（failure），但多数测试框架会把它当作一个错误（error），并与正常的测试失败区分开。「失败」指的是在验证阶段中，实际值与验证语句提供的期望值不相等；而这里的「错误」则是另一码事，它是在更早的阶段前抛出的异常（这里是在配置阶段）。它更像代码的作者没有预料到的一种异常场景，因此我们不幸地得到了每个 JavaScript 程序员都很熟悉的错误（...is not a function）。

How should the code respond to such a case? One approach is to add some handling that would give a better error response—either raising a more meaningful error message, or just setting producers to an empty array (with perhaps a log message). But there may also be valid reasons to leave it as it is. Perhaps the input object is produced by a trusted source—such as another part of the same code base. Putting in lots of validation checks between modules in the same code base can result in duplicate checks that cause more trouble than they are worth, especially if they duplicate validation done elsewhere. But if that input object is coming in from an external source, such as a JSON­ encoded request, then validation checks are needed, and should be tested. In either case, writing tests like this raises these kinds of questions. If I’m writing tests like this before refactoring, I would probably discard this test. Refactoring should preserve observable behavior; an error like this is outside the bounds of observable, so I need not be concerned if my refactoring changes the code’s response to this condition.

那么代码应该如何处理这种场景呢？一种思路是，对错误进行处理并给出更好的出错响应，比如说抛出更有意义的错误信息，或是直接将 producers 字段设置为一个空数组（最好还能再记录一行日志信息）。但维持现状不做处理也说得通，也许该输入对象是由可信的数据源提供的，比如同个代码库的另一部分。在同一代码库的不同模块之间加入太多的检查往往会导致重复的验证代码，它带来的好处通常不抵害处，特别是你添加的验证可能在其他地方早已做过。但如果该输入对象是由一个外部服务所提供，比如一个返回 JSON 数据的请求，那么校验和测试就显得必要了。不论如何，为边界条件添加测试总能引发这样的思考。

如果这样的测试是在重构前写出的，那么我很可能还会删掉它。重构应该保证可观测的行为不发生改变，而类似的错误已经超越可观测的范畴。删掉这条测试，我就不用担心重构过程改变了代码对这个边界条件的处理方式。

If this error could lead to bad data running around the program, causing a failure that will be hard to debug, I might use Introduce Assertion (302) to fail fast. I don’t add tests to catch such assertion failures, as they are themselves a form of test.

1『上面的这段信息目前无法理解，mark 下。（2020-06-17）』

如果这个错误会导致脏数据在应用中到处传递，或是产生一些很难调试的失败，我可能会用引入断言（302）手法，使代码不满足预设条件时快速失败。我不会为这样的失败断言添加测试，它们本身就是一种测试的形式。

Don’t let the fear that testing can’t catch all bugs stop you from writing tests that catch most bugs.

不要因为测试无法捕捉所有的 bug 就不写测试，因为测试的确可以捕捉到大多数 bug。

When do you stop? I’m sure you have heard many times that you cannot prove that a program has no bugs by testing. That’s true, but it does not affect the ability of testing to speed up programming. I’ve seen various proposed rules to ensure you have tested every combination of everything. It’s worth taking a look at these—but don’t let them get to you. There is a law of diminishing returns in testing, and there is the danger that by trying to write too many tests you become discouraged and end up not writing any. You should concentrate on where the risk is. Look at the code and see where it becomes complex. Look at a function and consider the likely areas of error. Your tests will not find every bug, but as you refactor, you will understand the program better and thus find more bugs. Although I always start refactoring with a test suite, I invariably add to it as I go along.

1『重构 -> 加深对代码的理解 -> 增加更多的测试。』

什么时候应该停下来？我相信这样的话你已经听过很多次：「任何测试都不能证明一个程序没有 bug。」确实如此，但这并不影响「测试可以提高编程速度」。我曾经见过好几种测试规则建议，其目的都是保证你能够测试所有情况的一切组合。这些东西值得一看，但是别让它们影响你。当测试数量达到一定程度之后，继续增加测试带来的边际效用会递减；如果试图编写太多测试，你也可能因为工作量太大而气馁，最后什么都写不成。你应该把测试集中在可能出错的地方。观察代码，看哪儿变得复杂；观察函数，思考哪些地方可能出错。是的，你的测试不可能找出所有 bug，但一旦进行重构，你可以更好地理解整个程序，从而找到更多 bug。虽然在开始重构之前我会确保有一个测试套件存在，但前进途中我总会加入更多测试。

### 4.7 Much More Than This
 
That’s as far as I’m going to go with this chapter—after all, this is a book on refactoring, not on testing. But testing is an important topic, both because it’s a necessary foundation for refactoring and because it’s a valuable tool in its own right. While I’ve been happy to see the growth of refactoring as a programming practice since I wrote this book, I’ve been even happier to see the change in attitudes to testing. Previously seen as the responsibility of a separate (and inferior) group, testing is now increasingly a first­class concern of any decent software developer. Architectures often are, rightly, judged on their testability.

本章我想讨论的东西到这里就差不多了，毕竟这是一本关于重构而不是测试的书。但测试本身是一个很重要的话题，它既是重构所必要的基础保障，本身也是一个有价值的工具。自本书第 1 版以来，我很高兴看到重构作为一项编程实践在逐步发展，但我更高兴见到业界对测试的态度也在发生转变。之前，测试更多被认为是另一个独立的（所需专业技能也较少的）团队的责任，但现在它愈发成为任何一个软件开发者所必备的技能。如今一个架构的好坏，很大程度要取决于它的可测试性，这是一个好的行业趋势。

The kinds of tests I’ve shown here are unit tests, designed to operate on a small area of the code and run fast. They are the backbone of self­-testing code; most tests in such a system are unit tests. There are other kinds of tests too, focusing on integration between components, exercising multiple levels of the software together, looking for performance issues, etc. (And even more varied than the types of tests are the arguments people get into about how to classify tests.)

这里我展示的测试都属于单元测试，它们负责测试一块小的代码单元，运行足够快速。它们是自测试代码的支柱，是一个系统中占绝大多数的测试类型。同时也有其他种类的测试存在，有的专注于组件之间的集成，有的会检验软件跨越几个层级的运行结果，有的用于查找性能问题，不一而足。（而且，同行们对于如何归类测试的争论，恐怕比繁多的测试种类本身还要多。）

Like most aspects of programming, testing is an iterative activity. Unless you are either very skilled or very lucky, you won’t get your tests right the first time. I find I’m constantly working on the test suite—just as much as I work on the main code. Naturally, this means adding new tests as I add new features, but it also involves looking at the existing tests. Are they clear enough? Do I need to refactor them so I can more easily understand what they are doing? Have I got the right tests? An important habit to get into is to respond to a bug by first writing a test that clearly reveals the bug. Only after I have the test do I fix the bug. By having the test, I know the bug will stay dead. I also think about that bug and its test: Does it give me clues to other gaps in the test suite?

与编程的许多方面类似，测试也是一种迭代式的活动。除非你技能非常纯熟，或者非常幸运，否则你很难第一次就把测试写对。我发觉我持续地在测试集上工作，就与我在主代码库上的工作一样多。很自然，这意味着我在增加新特性时也要同时添加测试，有时还需要回顾已有的测试：它们足够清晰吗？我需要重构它们，以帮助我更好地理解吗？我拥有的测试是有价值的吗？一个值得养成的好习惯是，每当你遇见一个 bug，先写一个测试来清楚地复现它。仅当测试通过时，才视为 bug 修完。只要测试存在一天，我就知道这个错误永远不会再复现。这个 bug 和对应的测试也会提醒我思考：测试集里是否还有这样不被阳光照耀到的犄角旮旯？

When you get a bug report, start by writing a unit test that exposes the bug. 

A common question is, “How much testing is enough?” There’s no good measurement for this. Some people advocate using test coverage [ mf­tc] as a measure, but test coverage analysis is only good for identifying untested areas of the code, not for assessing the quality of a test suite.

一个常见的问题是，「要写多少测试才算足够？」这个问题没有很好的衡量标准。有些人拥护以测试覆盖率 [mftc] 作为指标，但测试覆盖率的分析只能识别出那些未被测试覆盖到的代码，而不能用来衡量一个测试集的质量高低。

The best measure for a good enough test suite is subjective: How confident are you that if someone introduces a defect into the code, some test will fail? This isn’t something that can be objectively analyzed, and it doesn’t account for false confidence, but the aim of self-­testing code is to get that confidence. If I can refactor my code and be pretty sure that I’ve not introduced a bug because my tests come back green—then I can be happy that I have good enough tests.

It is possible to write too many tests. One sign of that is when I spend more time changing the tests than the code under test—and I feel the tests are slowing me down. But while over­testing does happen, it’s vanishingly rare compared to under­testing. 

一个测试集是否足够好，最好的衡量标准其实是主观的，请你试问自己：如果有人在代码里引入了一个缺陷，你有多大的自信它能被测试集揪出来？这种信心难以被定量分析，盲目自信不应该被计算在内，但自测试代码的全部目标，就是要帮你获得此种信心。如果我重构完代码，看见全部变绿的测试就可以十分自信没有引入额外的 bug，这样，我就可以高兴地说，我已经有了一套足够好的测试。测试同样可能过犹不及。测试写得太多的一个征兆是，相比要改的代码，我在改动测试上花费了更多的时间 —— 并且我能感到测试就在拖慢我。不过尽管过度测试时有发生，相比测试不足的情况还是稀少得多。

## 0501. Introducing the Catalog

The rest of this book is a catalog of refactorings. This catalog started from my personal Tutorialsnotes that I made to remind myself how to do refactorings in a safe and efficient way. Since then, I’ve refined the catalog, and there’s more of it that comes from deliberate Offers exploration & Deals of some refactoring moves. It’s still something I use when I do a refactoring I haven’t done in a while.

本书剩余的篇幅是一份重构的名录。最初这个名录只是我的个人笔记，我用它来提示自己如何以安全且高效的方式进行重构。然后我不断精炼这份名录，对一些重构的深入探索又引出了更多的重构手法。对于不太常用的重构手法，我还是会不断参阅这份名录。

### 5.1 Format of The Refactorings

As I describe the refactorings in the catalog, I use a standard format. Each refactoring Support has five parts, as follows:

1 Sign Out I begin with a name. The name is important to building a vocabulary of refactorings. This is the name I use elsewhere in the book. Refactorings often go by different names now, so I also list any aliases that seem to be common.

2 I follow the name with a short sketch of the refactoring. This helps you find a refactoring more quickly.

3 The motivation describes why the refactoring should be done and describes circumstances in which it shouldn’t be done.

4 The mechanics are a concise, step­by­step description of how to carry out the refactoring.

5 The examples show a very simple use of the refactoring to illustrate how it works.

介绍重构时，我采用一种标准格式。每个重构手法都有如下 5 个部分。

1、首先是名称（name）。要建造一个重构词汇表，名称是很重要的。这个名称也就是我将在本书其他地方使用的名称。如今重构经常会有多个名字，所以我会同时列出常见的别名。

2、名称之后是一个简单的速写（sketch）。这部分可以帮助你更快找到你所需要的重构手法。

3、动机（motivation）为你介绍「为什么需要做这个重构」和「什么情况下不该做这个重构」。

4、做法（mechanics）简明扼要地一步一步介绍如何进行此重构。

5、范例（examples）以一个十分简单的例子说明此重构手法如何运作。

The sketch shows a code example of the transformation of the refactoring. It’s not meant to explain what the refactoring is, let alone how to do it, but it should remind you what the refactoring is if you’ve come across it before. If not, i you’ll probably need to work through the example to get a better idea. I also include a small graphic; again, I don’t intend it to be explanatory—it’s more of a graphic memory­jogger. The mechanics come from my own notes to remember how to do the refactoring when I haven’t done it for a while. As such, they are somewhat terse, usually without explanations of why the steps are done that way. I give a more expansive explanation in the example. This way, the mechanics are short notes you can refer to easily when you know the refactoring but need to look up the steps (at least this is how I use them). You’ll probably need to read the examples when you first do the refactoring.

I’ve written the mechanics in such a way that each step of each refactoring is as small as possible. I emphasize the safe way of doing the refactoring—which is to take very small steps and test after every one. At work, I usually take larger steps than some of the baby steps described, but if I run into a bug, I back out the last step and take the smaller steps. The steps include a number of references to special cases. The steps thus also function as a checklist; I often forget these things myself.

Although I (with few exceptions) only list one set of mechanics, they aren’t the only way to carry out the refactoring. I selected the mechanics in the book because they work pretty well most of the time. It’s likely you’ll vary them as you get more practice in refactoring, and that’s fine. Just remember that the key is to take small steps—and the trickier the situation, the smaller the steps.

The examples are of the laughably simple textbook kind. My aim with the examples is to help explain the basic refactoring with minimal distractions, so I hope you’ll forgive the simplicity. (They are certainly not examples of good business modeling.) I’m sure you’ll be able to apply them to your rather more complex situations. Some very simple refactorings don’t have examples because I didn’t think an example would add much.

In particular, remember that the examples are included only to illustrate the one refactoring under discussion. In most cases, there are still problems with the code at the end—but fixing these problems requires other refactorings. In a few cases in which refactorings often go together, I carry examples from one re­factoring to another. In most cases, I leave the code as it is after the single refactoring. I do this to make each refactoring self­contained, because the primary role of the catalog is to be a reference.

I use color to highlight changed code where it may be difficult to spot among code that has not been changed. I do not use highlighting for all changed code, because too much defeats the purpose.

速写部分会以代码示例的形式展示重构带来的转变。速写的用意不是解释重构的用途，更不是详细讲解如何操作这个重构；但如果你曾经看过这个重构手法，速写能帮你回忆起它。如果你是第一次接触到这个重构手法，可能最好是先阅读范例部分。我还给每个重构手法画了一幅小图。同样，我也不指望这些小图能说清重构手法的内容，只是提供一点图像记忆的线索。

「做法」出自我自己的笔记。这些笔记是为了让我在一段时间不做某项重构之后还能记得怎么做。它们也颇为简洁，通常不会解释「为什么要这么做那么做」。我会在「范例」中给出更多解释。这么一来，「做法」就成了简短的笔记。如果你知道该使用哪个重构，但记不清具体步骤，可以参考「做法」部分（至少我是这么使用它们的）；如果你初次使用某个重构，可能只参考「做法」还不够，你还需要阅读「范例」。

撰写「做法」的时候，我尽量将重构的每个步骤拆得尽可能小。我强调安全的重构方式，所以应该采用非常小的步骤，并且在每个步骤之后进行测试。真正工作时，我通常会采用比这里介绍的「婴儿学步」稍大些的步骤，然而一旦出问题，我就会撤销上一步，换用比较小的步骤。这些步骤还包含一些特殊情况的参考，所以它们也有检查清单的作用。我自己经常忘掉这些该做的事情。

绝大多数时候我只列出了重构的一套做法，但其实一个重构并非只有一套做法。我在本书中选择介绍这些做法，因为它们大多数时候都管用。等你经过练习获得更多重构经验，你可能会调整重构的做法，那完全没问题。只要牢记一点：小步前进，情况越复杂，步子就要越小。

「范例」像是简单而有趣的教科书。我使用这些范例是为了帮助解释重构的基本要素，最大限度地避免其他枝节，所以我希望你能原谅其中的简化工作（它们当然不是优秀的业务建模例子）。不过我敢肯定，你一定能在那些更复杂的情况中使用它们。某些十分简单的重构干脆没有范例，因为我觉得为它们加上一个范例不会有多大意义。

更明确地说，加上范例仅仅是为了阐释当时讨论的重构手法。通常那些代码最终仍有其他问题，但修正那些问题需要用到其他重构手法。某些情况下数个重构经常被一并运用，这时候我会把范例带到另一个重构中继续使用。大部分时候，一个范例只为一项重构而设计，这么做是为了让每一项重构手法自成一体，因为这份重构名录的首要目的还是作为参考工具。

修改后的代码可能被埋没在未修改的代码中，难以一眼看出，所以我使用不同的颜色突出显示修改过的代码。但我并没有突出显示所有修改过的代码，因为一旦修改过的代码太多，全都突出显示反而不能突显重点。

### 5.2 The Choice of Refactorings

This is by no means a complete catalog of refactorings. It is, I hope, a collection of those most useful to have them written down. By “most useful” I mean those that are both commonly used and worthwhile to name and describe. I find something worthwhile to describe for a combination of reasons: Some have interesting mechanics which help general refactoring skills, some have a strong effect on improving the design of code.

Some refactorings are missing because they are so small and straightforward that I don’t feel they are worth writing up. An example in the first edition was Slide Statements (223)—which I use frequently but didn’t recognize as something I should include in the catalog (obviously, I changed my mind for this edition). These may well get added to the book over time, depending on how much energy I devote to new refactorings in the future.

Another category is refactorings that logically exist, but either aren’t used much by me or show a simple similarity to other refactorings. Every refactoring in this book has a logical inverse refactoring, but I didn’t write all of them up because I don’t find many inverses interesting. Encapsulate Variable (132) is a common and powerful refactoring but its inverse is something I hardly ever do (and it is easy to perform anyway) so I didn’t think we need a catalog entry for it.

这不是一份巨细靡遗的重构名录。我只是认为这些重构手法最值得被记录下来。之所以说它们「最值得」，因为这些都是很常用的重构手法，并且值得给它们命名和详细的介绍：其中一些做法很有意思，能帮助读者提高整体重构技能水平，另外一些则对于代码设计质量的提升效果显著。

有些重构没有进入这份名录，因为它们太小、太简单，我觉得没必要多加赘述。例如，在撰写第 1 版时我就曾经考虑过移动语句（223），这个重构我经常使用，但我觉得没必要将它放进名录里（显然我在写第 2 版的时候改变了想法）。以后也许还有类似这样的重构会被加进书里，不过那要看我投入多少精力在新增重构上了。

还有一些没有进入名录的重构，要么是我用得很少，要么是与其他重构非常相似。本书中的每个重构，逻辑上来说，都有一个反向的重构。但我并没有把所有反向重构都写下来，因为我发现很多反向重构没太大意思。例如，封装变量（132）是一个常用又好用的重构，但它的反向重构我几乎从来不会做（而且就算要做也非常简单），所以我觉得没必要将这个反向重构放进名录。
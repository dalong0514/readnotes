# 0301. Bad Smells in Code Topics

“If it stinks, change it.”

——by Kent Beck and Martin Fowler

By now you have a good idea of how refactoring works. But just because you know how doesn’t mean you know when. Deciding when to start refactoring—and when to stop—is Settings just as important to refactoring as knowing how to operate the mechanics of it.

Now comes the dilemma. It is easy to explain how to delete an instance variable or create a hierarchy. These are simple matters. Trying to explain when you should do Sign these Out things is not so cut­and­dried. Instead of appealing to some vague notion of programming aesthetics (which, frankly, is what we consultants usually do), I wanted something a bit more solid.

When I was writing the first edition of this book, I was mulling over this issue as I visited Kent Beck in Zurich. Perhaps he was under the influence of the odors of his newborn daughter at the time, but he had come up with the notion of describing the “when” of refactoring in terms of smells.

“Smells,” you say, “and that is supposed to be better than vague aesthetics?” Well, yes. We have looked at lots of code, written for projects that span the gamut from wildly successful to nearly dead. In doing so, we have learned to look for certain structures in the code that suggest—sometimes, scream for—the possibility of refactoring. (We are switching over to “we” in this chapter to reflect the fact that Kent and I wrote this chapter jointly. You can tell the difference because the funny jokes are mine and the others are his.)

One thing we won’t try to give you is precise criteria for when a refactoring is overdue. In our experience, no set of metrics rivals informed human intuition. What we will do is give you indications that there is trouble that can be solved by a refactoring. You will have to develop your own sense of how many instance variables or how many lines of code in a method are too many.

Use this chapter and the table on the inside back cover as a way to give you inspiration when you’re not sure what refactorings to do. Read the chapter (or skim the table) and try to identify what it is you’re smelling, then go to the refactorings we suggest to see whether they will help you. You may not find the exact smell you can detect, but hopefully it should point you in the right direction.

现在，对于重构如何运作，你已经有了相当好的理解。但是知道「如何」不代表知道「何时」。决定何时重构及何时停止和知道重构机制如何运转一样重要。

难题来了！解释「如何删除一个实例变量」或「如何产生一个继承体系」很容易，因为这些都是很简单的事情，但要解释「该在什么时候做这些动作」就没那么顺理成章了。除了露几手含混的编程美学（说实话，这就是咱们这些顾问常做的事），我还希望让某些东西更具说服力一些。

撰写本书的第 1 版时，我正在为这个微妙的问题大伤脑筋。去苏黎世拜访 KentBeck 的时候，也许是因为受到刚出生的女儿的气味影响吧，他提出用味道来形容重构的时机。「味道，」你可能会说，「真的比含混的美学理论要好吗？」好吧，是的。我们看过很多很多代码，它们所属的项目从大获成功到奄奄一息都有。观察这些代码时，我们学会了从中找寻某些特定结构，这些结构指出（有时甚至就像尖叫呼喊）重构的可能性。（本章主语换成「我们」，是为了反映一个事实：Kent 和我共同撰写本章。你应该可以看出我俩的文笔差异 —— 插科打诨的部分是我写的，其余都是他写的。）

我们并不试图给你一个何时必须重构的精确衡量标准。从我们的经验看来，没有任何量度规矩比得上见识广博者的直觉。我们只会告诉你一些迹象，它会指出「这里有一个可以用重构解决的问题」。你必须培养自己的判断力，学会判断一个类内有多少实例变量算是太大、一个函数内有多少行代码才算太长。

如果你无法确定该采用哪一种重构手法，请阅读本章内容和书后附的「重构列表」来寻找灵感。你可以阅读本章或快速浏览书后附的「坏味道与重构手法速查表」来判断自己闻到的是什么味道，然后再看看我们所建议的重构手法能否帮到你。也许这里所列的「坏味道条款」和你所检测的不尽相符，但愿它们能够为你指引正确方向。

## 3.1 Mysterious Name

Puzzling over some text to understand what’s going on is a great thing if you’re reading a detective novel, but not when you’re reading code. We may fantasize about being International Men of Mystery, but our code needs to be mundane and clear. One of the most important parts of clear code is good names, so we put a lot of thought into naming functions, modules, variables, classes, so they clearly communicate what they do and how to use them.

Sadly, however, naming is one of the two hard things [mf­2h] in programming. So, perhaps the most common refactorings we do are the renames: Change Function Declaration (124) (to rename a function), Rename Variable (137), and Rename Field (244). People are often afraid to rename things, thinking it’s not worth the trouble, but a good name can save hours of puzzled incomprehension in the future.

Renaming is not just an exercise in changing names. When you can’t think of a good name for something, it’s often a sign of a deeper design malaise. Puzzling over a tricky name has often led us to significant simplifications to our code.

读侦探小说时，透过一些神秘的文字猜测故事情节是一种很棒的体验；但如果是在阅读代码，这样的体验就不怎么好了。我们也许会幻想自己是《王牌大贱谍》中的国际特工 1，但我们写下的代码应该直观明了。整洁代码最重要的一环就是好的名字，所以我们会深思熟虑如何给函数、模块、变量和类命名，使它们能清晰地表明自己的功能和用法。

然而，很遗憾，命名是编程中最难的两件事之一 [mf2h]。正因为如此，改名可能是最常用的重构手法，包括改变函数声明（124）（用于给函数改名）、变量改名（137）、字段改名（244）等。很多人经常不愿意给程序元素改名，觉得不值得费这个劲，但好的名字能节省未来用在猜谜上的大把时间。改名不仅仅是修改名字而已。如果你想不出一个好名字，说明背后很可能潜藏着更深的设计问题。为一个恼人的名字所付出的纠结，常常能推动我们对代码进行精简。

## 3.2 Duplicated Code

If you see the same code structure in more than one place, you can be sure that your program will be better if you find a way to unify them. Duplication means that every time you read these copies, you need to read them carefully to see if there’s any difference. If you need to change the duplicated code, you have to find and catch each duplication.

The simplest duplicated code problem is when you have the same expression in two methods of the same class. Then all you have to do is Extract Function (106) and invoke the code from both places. If you have code that’s similar, but not quite identical, see if you can use Slide Statements (223) to arrange the code so the similar items are all together for easy extraction. If the duplicate fragments are in subclasses of a common base class, you can use Pull Up Method (350) to avoid calling one from another.

如果你在一个以上的地点看到相同的代码结构，那么可以肯定：设法将它们合而为一，程序会变得更好。一旦有重复代码存在，阅读这些重复的代码时你就必须加倍仔细，留意其间细微的差异。如果要修改重复代码，你必须找出所有的副本来修改。

最单纯的重复代码就是「同一个类的两个函数含有相同的表达式」。这时候你需要做的就是采用提炼函数（106）提炼出重复的代码，然后让这两个地点都调用被提炼出来的那一段代码。如果重复代码只是相似而不是完全相同，请首先尝试用移动语句（223）重组代码顺序，把相似的部分放在一起以便提炼。如果重复的代码段位于同一个超类的不同子类中，可以使用函数上移（350）来避免在两个子类之间互相调用。

## 3.3 Long Function

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

## 3.4 Long Patameter List

In our early programming days, we were taught to pass in as parameters everything needed by a function. This was understandable because the alternative was global data, and global data quickly becomes evil. But long parameter lists are often confusing in their own right.

If you can obtain one parameter by asking another parameter for it, you can use Replace Parameter with Query (324) to remove the second parameter. Rather than pulling lots of data out of an existing data structure, you can use Preserve Whole Object (319) to pass the original data structure instead. If several parameters always fit together, combine them with Introduce Parameter Object (140). If a parameter is used as a flag to dispatch different behavior, use Remove Flag Argument (314).

1『此时此刻才算理解了啥叫「查询取代参数」，比如说一个函数有 3 个入参（A、B、C），B、C 可以通过调用一个函数（以 A 为入参）来获取，那么果断用调用函数的方式取代 B、C，这样的话，原来 3 个入参可以缩减为 1 个。』

Classes are a great way to reduce parameter list sizes. They are particularly useful when multiple functions share several parameter values. Then, you can use Combine Functions into Class (144) to capture those common values as fields. If we put on our functional programming hats, we’d say this creates a set of partially applied functions.

刚开始学习编程的时候，老师教我们：把函数所需的所有东西都以参数的形式传递进去。这可以理解，因为除此之外就只能选择全局数据，而全局数据很快就会变成邪恶的东西。但过长的参数列表本身也经常令人迷惑。如果可以向某个参数发起查询而获得另一个参数的值，那么就可以使用以查询取代参数（324）去掉这第二个参数。

如果你发现自己正在从现有的数据结构中抽出很多数据项，就可以考虑使用保持对象完整（319）手法，直接传入原来的数据结构。如果有几项参数总是同时出现，可以用引入参数对象（140）将其合并成一个对象。如果某个参数被用作区分函数行为的标记（flag），可以使用移除标记参数（314）。

使用类可以有效地缩短参数列表。如果多个函数有同样的几个参数，引入一个类就尤为有意义。你可以使用函数组合成类（144），将这些共同的参数变成这个类的字段。如果戴上函数式编程的帽子，我们会说，这个重构过程创造了一组部分应用函数（partially applied function）。

## 3.5 Global Data

Since our earliest days of writing software, we were warned of the perils of global data— how it was invented by demons from the fourth plane of hell, which is the resting place of any programmer who dares to use it. And, although we are somewhat skeptical about fire and brimstone, it’s still one of the most pungent odors we are likely to run into. The problem with global data is that it can be modified from anywhere in the code base, and there’s no mechanism to discover which bit of code touched it. Time and again, this leads to bugs that breed from a form of spooky action from a distance—and it’s very hard to find out where the errant bit of program is. The most obvious form of global data is global variables, but we also see this problem with class variables and singletons.

Our key defense here is Encapsulate Variable (132), which is always our first move when confronted with data that is open to contamination by any part of a program. At least when you have it wrapped by a function, you can start seeing where it’s modified and start to control its access. Then, it’s good to limit its scope as much as possible by moving it within a class or module where only that module’s code can see it.

Global data is especially nasty when it’s mutable. Global data that you can guarantee never changes after the program starts is relatively safe—if you have a language that can enforce that guarantee.

Global data illustrates Paracelsus’s maxim: The difference between a poison and something benign is the dose. You can get away with small doses of global data, but it gets exponentially harder to deal with the more you have. Even with little bits, we like to keep it encapsulated—that’s the key to coping with changes as the software evolves.

刚开始学软件开发时，我们就听说过关于全局数据的惊悚故事 —— 它们是如何被来自地狱第四层的恶魔发明出来，胆敢使用它们的程序员如今在何处安息。就算这些烈焰与硫黄的故事不那么可信，全局数据仍然是最刺鼻的坏味道之一。全局数据的问题在于，从代码库的任何一个角落都可以修改它，而且没有任何机制可以探测出到底哪段代码做出了修改。一次又一次，全局数据造成了那些诡异的 bug，而问题的根源却在遥远的别处，想要找到出错的代码难于登天。全局数据最显而易见的形式就是全局变量，但类变量和单例（singleton）也有这样的问题。

首要的防御手段是封装变量（132），每当我们看到可能被各处的代码污染的数据，这总是我们应对的第一招。你把全局数据用一个函数包装起来，至少你就能看见修改它的地方，并开始控制对它的访问。随后，最好将这个函数（及其封装的数据）搬移到一个类或模块中，只允许模块内的代码使用它，从而尽量控制其作用域。可以被修改的全局数据尤其可憎。如果能保证在程序启动之后就不再修改，这样的全局数据还算相对安全，不过得有编程语言提供这样的保证才行。

全局数据印证了帕拉塞尔斯的格言：良药与毒药的区别在于剂量。有少量的全局数据或许无妨，但数量越多，处理的难度就会指数上升。即便只是少量的数据，我们也愿意将它封装起来，这是在软件演进过程中应对变化的关键所在。

## 3.6 Mutable Data

Changes to data can often lead to unexpected consequences and tricky bugs. I can update some data here, not realizing that another part of the software expects something different and now fails—a failure that’s particularly hard to spot if it only happens under rare conditions. For this reason, an entire school of software development—functional programming—is based on the notion that data should never change and that updating a data structure should always return a new copy of the structure with the change, leaving the old data pristine.

These kinds of languages, however, are still a relatively small part of programming; many of us work in languages that allow variables to vary. But this doesn’t mean we should ignore the advantages of immutability—there are still many things we can do to limit the risks on unrestricted data updates.

You can use Encapsulate Variable (132) to ensure that all updates occur through narrow functions that can be easier to monitor and evolve. If a variable is being updated to store different things, use Split Variable (240) both to keep them separate and avoid the risky update. Try as much as possible to move logic out of code that processes the update by using Slide Statements (223) and Extract Function (106) to separate the side­effect­free code from anything that performs the update. In APIs, use Separate Query from Modifier (306) to ensure callers don’t need to call code that has side effects unless they really need to. We like to use Remove Setting Method (331) as soon as we can—sometimes, just trying to find clients of a setter helps spot opportunities to reduce the scope of a variable.

Mutable data that can be calculated elsewhere is particularly pungent. It’s not just a rich source of confusion, bugs, and missed dinners at home—it’s also unnecessary. We spray it with a concentrated solution of vinegar and Replace Derived Variable with Query (248).

Mutable data isn’t a big problem when it’s a variable whose scope is just a couple of lines—but its risk increases as its scope grows. Use Combine Functions into Class (144) or Combine Functions into Transform (149) to limit how much code needs to update a variable. If a variable contains some data with internal structure, it’s usually better to replace the entire structure rather than modify it in place, using Change Reference to Value (252).

对数据的修改经常导致出乎意料的结果和难以发现的 bug。我在一处更新数据，却没有意识到软件中的另一处期望着完全不同的数据，于是一个功能失效了 —— 如果故障只在很罕见的情况下发生，要找出故障原因就会更加困难。因此，有一整个软件开发流派 —— 函数式编程 —— 完全建立在「数据永不改变」的概念基础上：如果要更新一个数据结构，就返回一份新的数据副本，旧的数据仍保持不变。不过这样的编程语言仍然相对小众，大多数程序员使用的编程语言还是允许修改变量值的。即便如此，我们也不应该忽视不可变性带来的优势 —— 仍然有很多办法可以用于约束对数据的更新，降低其风险。

可以用封装变量（132）来确保所有数据更新操作都通过很少几个函数来进行，使其更容易监控和演进。如果一个变量在不同时候被用于存储不同的东西，可以使用拆分变量（240）将其拆分为各自不同用途的变量，从而避免危险的更新操作。使用移动语句（223）和提炼函数（106）尽量把逻辑从处理更新操作的代码中搬移出来，将没有副作用的代码与执行数据更新操作的代码分开。设计 API 时，可以使用将查询函数和修改函数分离（306）确保调用者不会调到有副作用的代码，除非他们真的需要更新数据。我们还乐于尽早使用移除设值函数（331）—— 有时只是把设值函数的使用者找出来看看，就能帮我们发现缩小变量作用域的机会。

如果可变数据的值能在其他地方计算出来，这就是一个特别刺鼻的坏味道。它不仅会造成困扰、bug 和加班，而且毫无必要。消除这种坏味道的办法很简单，使用以查询取代派生变量（248）即可。如果变量作用域只有几行代码，即使其中的数据可变，也不是什么大问题；但随着变量作用域的扩展，风险也随之增大。可以用函数组合成类（144）或者函数组合成变换（149）来限制需要对变量进行修改的代码量。如果一个变量在其内部结构中包含了数据，通常最好不要直接修改其中的数据，而是用将引用对象改为值对象（252）令其直接替换整个数据结构。

## 3.7 Divergent Change

We structure our software to make change easier; after all, software is meant to be soft. When we make a change, we want to be able to jump to a single clear point in the system and make the change. When you can’t do this, you are smelling one of two closely related pungencies.

Divergent change occurs when one module is often changed in different ways for different reasons. If you look at a module and say, “Well, I will have to change these three functions every time I get a new database; I have to change these four functions every time there is a new financial instrument,” this is an indication of divergent change. The database interaction and financial processing problems are separate contexts, and we can make our programming life better by moving such contexts into separate modules. That way, when we have a change to one context, we only have to understand that one context and ignore the other. We always found this to be important, but now, with our brains shrinking with age, it becomes all the more imperative. Of course, you often discover this only after you’ve added a few databases or financial instruments; context boundaries are usually unclear in the early days of a program and continue to shift as a software system’s capabilities change. If the two aspects naturally form a sequence—for example, you get data from the database and then apply your financial processing on it—then Split Phase (154) separates the two with a clear data structure between them. If there’s more back­andforth in the calls, then create appropriate modules and use Move Function (198) to divide the processing up. If functions mix the two types of processing within themselves, use Extract Function (106) to separate them before moving. If the modules are classes, then Extract Class (182) helps formalize how to do the split.

我们希望软件能够更容易被修改 —— 毕竟软件本来就该是「软」的。一旦需要修改，我们希望能够跳到系统的某一点，只在该处做修改。如果不能做到这一点，你就嗅出两种紧密相关的刺鼻味道中的一种了。

如果某个模块经常因为不同的原因在不同的方向上发生变化，发散式变化就出现了。当你看着一个类说：「呃，如果新加入一个数据库，我必须修改这 3 个函数；如果新出现一种金融工具，我必须修改这 4 个函数。」这就是发散式变化的征兆。数据库交互和金融逻辑处理是两个不同的上下文，将它们分别搬移到各自独立的模块中，能让程序变得更好：每当要对某个上下文做修改时，我们只需要理解这个上下文，而不必操心另一个。「每次只关心一个上下文」这一点一直很重要，在如今这个信息爆炸、脑容量不够用的年代就愈发紧要。当然，往往只有在加入新数据库或新金融工具后，你才能发现这个坏味道。在程序刚开发出来还在随着软件系统的能力不断演进时，上下文边界通常不是那么清晰。

如果发生变化的两个方向自然地形成了先后次序（比如说，先从数据库取出数据，再对其进行金融逻辑处理），就可以用拆分阶段（154）将两者分开，两者之间通过一个清晰的数据结构进行沟通。如果两个方向之间有更多的来回调用，就应该先创建适当的模块，然后用搬移函数（198）把处理逻辑分开。如果函数内部混合了两类处理逻辑，应该先用提炼函数（106）将其分开，然后再做搬移。如果模块是以类的形式定义的，就可以用提炼类（182）来做拆分。

## 3.8 Shotgun Surgery

Shotgun surgery is similar to divergent change but is the opposite. You whiff this when, every time you make a change, you have to make a lot of little edits to a lot of different classes. When the changes are all over the place, they are hard to find, and it’s easy to miss an important change.

In this case, you want to use Move Function (198) and Move Field (207) to put all the changes into a single module. If you have a bunch of functions operating on similar data, use Combine Functions into Class (144). If you have functions that are transforming or enriching a data structure, use Combine Functions into Transform (149). Split Phase (154) is often useful here if the common functions can combine their output for a consuming phase of logic.

A useful tactic for shotgun surgery is to use inlining refactorings, such as Inline Function (115) or Inline Class (186), to pull together poorly separated logic. You’ll end up with a Long Method or a Large Class, but can then use extractions to break it up into more sensible pieces. Even though we are inordinately fond of small functions and classes in our code, we aren’t afraid of creating something large as an intermediate step to reorganization.

霰弹式修改类似于发散式变化，但又恰恰相反。如果每遇到某种变化，你都必须在许多不同的类内做出许多小修改，你所面临的坏味道就是霰弹式修改。如果需要修改的代码散布四处，你不但很难找到它们，也很容易错过某个重要的修改。这种情况下，你应该使用搬移函数（198）和搬移字段（207）把所有需要修改的代码放进同一个模块里。如果有很多函数都在操作相似的数据，可以使用函数组合成类（144）。如果有些函数的功能是转化或者充实数据结构，可以使用函数组合成变换（149）。如果一些函数的输出可以组合后提供给一段专门使用这些计算结果的逻辑，这种时候常常用得上拆分阶段（154）。

面对霰弹式修改，一个常用的策略就是使用与内联（inline）相关的重构 —— 如内联函数（115）或是内联类（186）—— 把本不该分散的逻辑拽回一处。完成内联之后，你可能会闻到过长函数或者过大的类的味道，不过你总可以用与提炼相关的重构手法将其拆解成更合理的小块。即便如此钟爱小型的函数和类，我们也并不担心在重构的过程中暂时创建一些较大的程序单元。

## 3.9 Feature Envy

When we modularize a program, we are trying to separate the code into zones to maximize the interaction inside a zone and minimize interaction between zones. A classic case of Feature Envy occurs when a function in one module spends more time communicating with functions or data inside another module than it does within its own module. We’ve lost count of the times we’ve seen a function invoking half­a­dozen getter methods on another object to calculate some value. Fortunately, the cure for that case is obvious: The function clearly wants to be with the data, so use Move Function (198) to get it there. Sometimes, only a part of a function suffers from envy, in which case use Extract Function (106) on the jealous bit, and Move Function (198) to give it a dream home.

Of course not all cases are cut­and­dried. Often, a function uses features of several modules, so which one should it live with? The heuristic we use is to determine which module has most of the data and put the function with that data. This step is often made easier if you use Extract Function (106) to break the function into pieces that go into different places.

Of course, there are several sophisticated patterns that break this rule. From the Gang of Four [gof], Strategy and Visitor immediately leap to mind. Kent Beck’s Self Delegation [Beck SBPP] is another. Use these to combat the divergent change smell. The fundamental rule of thumb is to put things together that change together. Data and the behavior that references that data usually change together—but there are exceptions. When the exceptions occur, we move the behavior to keep changes in one place. Strategy and Visitor allow you to change behavior easily because they isolate the small amount of behavior that needs to be overridden, at the cost of further indirection.

所谓模块化，就是力求将代码分出区域，最大化区域内部的交互、最小化跨区域的交互。但有时你会发现，一个函数跟另一个模块中的函数或者数据交流格外频繁，远胜于在自己所处模块内部的交流，这就是依恋情结的典型情况。无数次经验里，我们看到某个函数为了计算某个值，从另一个对象那儿调用几乎半打的取值函数。疗法显而易见：这个函数想跟这些数据待在一起，那就使用搬移函数（198）把它移过去。有时候，函数中只有一部分受这种依恋之苦，这时候应该使用提炼函数（106）把这一部分提炼到独立的函数中，再使用搬移函数（198）带它去它的梦想家园。

当然，并非所有情况都这么简单。一个函数往往会用到几个模块的功能，那么它究竟该被置于何处呢？我们的原则是：判断哪个模块拥有的此函数使用的数据最多，然后就把这个函数和那些数据摆在一起。如果先以提炼函数（106）将这个函数分解为数个较小的函数并分别置放于不同地点，上述步骤也就比较容易完成了。

有几个复杂精巧的模式破坏了这条规则。说起这个话题，GoF [gof] 的策略（Strategy）模式和访问者（Visitor）模式立刻跳入我的脑海，Kent Beck 的 Self Delegation 模式 [Beck SBPP] 也在此列。使用这些模式是为了对抗发散式变化这一坏味道。最根本的原则是：将总是一起变化的东西放在一块儿。数据和引用这些数据的行为总是一起变化的，但也有例外。如果例外出现，我们就搬移那些行为，保持变化只在一地发生。策略模式和和访问者模式使你得以轻松修改函数的行为，因为它们将少量需被覆写的行为隔离开来 —— 当然也付出了「多一层间接性」的代价。

## 3.10 Data Clumps

Data items tend to be like children: They enjoy hanging around together. Often, you’ll see the same three or four data items together in lots of places: as fields in a couple of classes, as parameters in many method signatures. Bunches of data that hang around together really ought to find a home together. The first step is to look for where the clumps appear as fields. Use Extract Class (182) on the fields to turn the clumps into an object. Then turn your attention to method signatures using Introduce Parameter Object (140) or Preserve Whole Object (319) to slim them down. The immediate benefit is that you can shrink a lot of parameter lists and simplify method calling. Don’t worry about data clumps that use only some of the fields of the new object. As long as you are replacing two or more fields with the new object, you’ll come out ahead.

A good test is to consider deleting one of the data values. If you did this, would the others make any sense? If they don’t, it’s a sure sign that you have an object that’s dying to be born.

You’ll notice that we advocate creating a class here, not a simple record structure. We do this because using a class gives you the opportunity to make a nice perfume. You can now look for cases of feature envy, which will suggest behavior that can be moved into your new classes. We’ve often seen this as a powerful dynamic that creates useful classes and can remove a lot of duplication and accelerate future development, allowing the data to become productive members of society.

数据项就像小孩子，喜欢成群结队地待在一块儿。你常常可以在很多地方看到相同的三四项数据：两个类中相同的字段、许多函数签名中相同的参数。这些总是绑在一起出现的数据真应该拥有属于它们自己的对象。首先请找出这些数据以字段形式出现的地方，运用提炼类（182）将它们提炼到一个独立对象中。然后将注意力转移到函数签名上，运用引入参数对象（140）或保持对象完整（319）为它瘦身。这么做的直接好处是可以将很多参数列表缩短，简化函数调用。是的，不必在意数据泥团只用上新对象的一部分字段，只要以新对象取代两个（或更多）字段，就值得这么做。

一个好的评判办法是：删掉众多数据中的一项。如果这么做，其他数据有没有因而失去意义？如果它们不再有意义，这就是一个明确信号：你应该为它们产生一个新对象。我们在这里提倡新建一个类，而不是简单的记录结构，因为一旦拥有新的类，你就有机会让程序散发出一种芳香。得到新的类以后，你就可以着手寻找「依恋情结」，这可以帮你指出能够移至新类中的种种行为。这是一种强大的动力：有用的类被创建出来，大量的重复被消除，后续开发得以加速，原来的数据泥团终于在它们的小社会中充分发挥价值。

## 3.11 Primitive Obsession

Most programming environments are built on a widely used set of primitive types: integers, floating point numbers, and strings. Libraries may add some additional small objects such as dates. We find many programmers are curiously reluctant to create their own fundamental types which are useful for their domain—such as money, coordinates, or ranges. We thus see calculations that treat monetary amounts as plain numbers, or calculations of physical quantities that ignore units (adding inches to millimeters), or lots of code doing if (a < upper && a > lower).

Strings are particularly common petri dishes for this kind of odor: A telephone number is more than just a collection of characters. If nothing else, a proper type can often include consistent display logic for when it needs to be displayed in a user interface. Representing such types as strings is such a common stench that people call them “stringly typed” variables.

You can move out of the primitive cave into the centrally heated world of meaningful types by using Replace Primitive with Object (174). If the primitive is a type code controlling conditional behavior, use Replace Type Code with Subclasses (362) followed by Replace Conditional with Polymorphism (272).

Groups of primitives that commonly appear together are data clumps and should be civilized with Extract Class (182) and Introduce Parameter Object (140).

大多数编程环境都大量使用基本类型，即整数、浮点数和字符串等。一些库会引入一些小对象，如日期。但我们发现一个很有趣的现象：很多程序员不愿意创建对自己的问题域有用的基本类型，如钱、坐标、范围等。于是，我们看到了把钱当作普通数字来计算的情况、计算物理量时无视单位（如把英寸与毫米相加）的情况以及大量类似 if (`a < upper && a> lower`) 这样的代码。

字符串是这种坏味道的最佳培养皿，比如，电话号码不只是一串字符。一个体面的类型，至少能包含一致的显示逻辑，在用户界面上需要显示时可以使用。「用字符串来代表类似这样的数据」是如此常见的臭味，以至于人们给这类变量专门起了一个名字，叫它们「类字符串类型」（stringly typed）变量。

你可以运用以对象取代基本类型（174）将原本单独存在的数据值替换为对象，从而走出传统的洞窟，进入炙手可热的对象世界。如果想要替换的数据值是控制条件行为的类型码，则可以运用以子类取代类型码（362）加上以多态取代条件表达式（272）的组合将它换掉。如果你有一组总是同时出现的基本类型数据，这就是数据泥团的征兆，应该运用提炼类（182）和引入参数对象（140）来处理。

## 3.12 Repeated Switches

Talk to a true object­oriented evangelist and they’ll soon get onto the evils of switch statements. They’ll argue that any switch statement you see is begging for Replace Conditional with Polymorphism (272). We’ve even heard some people argue that all conditional logic should be replaced with polymorphism, tossing most ifs into the dustbin of history.

Even in our more wild­eyed youth, we were never unconditionally opposed to the conditional. Indeed, the first edition of this book had a smell entitled “switch statements.” The smell was there because in the late 90’s we found polymorphism sadly underappreciated, and saw benefit in getting people to switch over.

These days there is more polymorphism about, and it isn’t the simple red flag that it often was fifteen years ago. Furthermore, many languages support more sophisticated forms of switch statements that use more than some primitive code as their base. So we now focus on the repeated switch, where the same conditional switching logic (either in a switch/case statement or in a cascade of if/else statements) pops up in different places. The problem with such duplicate switches is that, whenever you add a clause, you have to find all the switches and update them. Against the dark forces of such repetition, polymorphism provides an elegant weapon for a more civilized codebase.

如果你跟真正的面向对象布道者交谈，他们很快就会谈到 switch 语句的邪恶。在他们看来，任何 switch 语句都应该用以多态取代条件表达式（272）消除掉。我们甚至还听过这样的观点：所有条件逻辑都应该用多态取代，绝大多数 if 语句都应该被扫进历史的垃圾桶。

即便在不知天高地厚的青年时代，我们也从未无条件地反对条件语句。在本书第 1 版中，这种坏味道被称为「switch 语句」（Switch Statements），那是因为在 20 世纪 90 年代末期，程序员们太过于忽视多态的价值，我们希望矫枉过正。

如今的程序员已经更多地使用多态，switch 语句也不再像 15 年前那样有害无益，很多语言支持更复杂的 switch 语句，而不只是根据基本类型值来做条件判断。因此，我们现在更关注重复的 switch：在不同的地方反复使用同样的 switch 逻辑（可能是以 switch/case 语句的形式，也可能是以连续的 if/else 语句的形式）。重复的 switch 的问题在于：每当你想增加一个选择分支时，必须找到所有的 switch，并逐一更新。多态给了我们对抗这种黑暗力量的武器，使我们得到更优雅的代码库。

## 3.13 Loops

Loops have been a core part of programming since the earliest languages. But we feel they are no more relevant today than bell­bottoms and flock wallpaper. We disdained them at the time of the first edition—but Java, like most other languages at the time, didn’t provide a better alternative. These days, however, first­class functions are widely supported, so we can use Replace Loop with Pipeline (231) to retire those anachronisms. We find that pipeline operations, such as filter and map, help us quickly see the elements that are included in the processing and what is done with them.

从最早的编程语言开始，循环就一直是程序设计的核心要素。但我们感觉如今循环已经有点儿过时，就像喇叭裤和植绒壁纸那样。其实在撰写本书第 1 版的时候，我们就已经开始鄙视循环语句，但和当时的大多数编程语言一样，当时的 Java 还没有提供更好的替代品。如今，函数作为一等公民已经得到了广泛的支持，因此我们可以使用以管道取代循环（231) 来让这些老古董退体。我们发现，管道操作（如 filter 和 map）可以帮助我们更快地看清被处理的元素以及处理它们的动作。

## 3.14 Lazy Element

We like using program elements to add structure—providing opportunities for variation, reuse, or just having more helpful names. But sometimes the structure isn’t needed. It may be a function that’s named the same as its body code reads, or a class that is essentially one simple function. Sometimes, this reflects a function that was expected to grow and be popular later, but never realized its dreams. Sometimes, it’s a class that used to pay its way, but has been downsized with refactoring. Either way, such program elements need to die with dignity. Usually this means using Inline Function (115) or Inline Class (186). With inheritance, you can use Collapse Hierarchy (380).

程序元素（如类和函数）能给代码增加结构，从而支持变化、促进复用或者哪怕只是提供更好的名字也好，但有时我们真的不需要这层额外的结构。可能有这样一个函数，它的名字就跟实现代码看起来一模一样；也可能有这样一个类，根本就是一个简单的函数。这可能是因为，起初在编写这个函数时，程序员也许期望它将来有一天会变大、变复杂，但那一天从未到来；也可能是因为，这个类原本是有用的，但随着重构的进行越变越小，最后只剩了一个函数。不论上述哪一种原因，请让这样的程序元素庄严赴义，通常你只需要使用内联函数（115）或是内联类（186）。如果这个类处于一个继承体系中，可以使用折叠继承体系（380)。

## 3.15 Speculative Generality

Brian Foote suggested this name for a smell to which we are very sensitive. You get it when people say, “Oh, I think we’ll need the ability to do this kind of thing someday” and thus add all sorts of hooks and special cases to handle things that aren’t required. The result is often harder to understand and maintain. If all this machinery were being used, it would be worth it. But if it isn’t, it isn’t. The machinery just gets in the way, so get rid of it.

If you have abstract classes that aren’t doing much, use Collapse Hierarchy (380). Unnecessary delegation can be removed with Inline Function (115) and Inline Class (186). Functions with unused parameters should be subject to Change Function Declaration (124) to remove those parameters. You should also apply Change Function Declaration (124) to remove any unneeded parameters, which often get tossed in for future variations that never come to pass.

Speculative generality can be spotted when the only users of a function or class are test cases. If you find such an animal, delete the test case and apply Remove Dead Code (237).

这个令我们十分敏感的坏味道，命名者是 Brian Foote。当有人说「噢，我想我们总有一天需要做这事」，并因而企图以各式各样的钩子和特殊情况来处理一些非必要的事情，这种坏味道就出现了。这么做的结果往往造成系统更难理解和维护。如果所有装置都会被用到，就值得那么做；如果用不到，就不值得。用不上的装置只会挡你的路，所以，把它搬开吧。

如果你的某个抽象类其实没有太大作用，请运用折叠继承体系（380）。不必要的委托可运用内联函数（115）和内联类（186）除掉。如果函数的某些参数未被用上，可以用改变函数声明（124）去掉这些参数。如果有并非真正需要、只是为不知远在何处的将来而塞进去的参数，也应该用改变函数声明（124) 去掉。如果函数或类的唯一用户是测试用例，这就飘出了坏味道「夸夸其谈通用性」。如果你发现这样的函数或类，可以先删掉测试用例，然后使用移除死代码（237)。

## 3.16 Temporary Field

Sometimes you see a class in which a field is set only in certain circumstances. Such code is difficult to understand, because you expect an object to need all of its fields. Trying to understand why a field is there when it doesn’t seem to be used can drive you nuts.

Use Extract Class (182) to create a home for the poor orphan variables. Use Move Function (198) to put all the code that concerns the fields into this new class. You may also be able to eliminate conditional code by using Introduce Special Case (289) to create an alternative class for when the variables aren’t valid.

有时你会看到这样的类：其内部某个字段仅为某种特定情况而设。这样的代码让人不易理解，因为你通常认为对象在所有时候都需要它的所有字段。在字段未被使用的情况下猜测当初设置它的目的，会让你发疯。请使用提炼类（182）给这个可怜的孤儿创造一个家，然后用搬移函数（198）把所有和这些字段相关的代码都放进这个新家。也许你还可以使用引入特例（289）在「变量不合法」的情况下创建一个替代对象，从而避免写出条件式代码。

## 3.17 Message Chains

You see message chains when a client asks one object for another object, which the client then asks for yet another object, which the client then asks for yet another another object, and so on. You may see these as a long line of getThis methods, or as a sequence of temps. Navigating this way means the client is coupled to the structure of the navigation. Any change to the intermediate relationships causes the client to have to change.

The move to use here is Hide Delegate (189). You can do this at various points in the chain. In principle, you can do this to every object in the chain, but doing this often turns every intermediate object into a middle man. Often, a better alternative is to see what the resulting object is used for. See whether you can use Extract Function (106) to take a piece of the code that uses it and then Move Function (198) to push it down the chain. If several clients of one of the objects in the chain want to navigate the rest of the way, add a method to do that.

Some people consider any method chain to be a terrible thing. We are known for our calm, reasoned moderation. Well, at least in this case we are.

如果你看到用户向一个对象请求另一个对象，然后再向后者请求另一个对象，然后再请求另一个对象。这就是消息链。在实际代码中你看到的可能是一长串取值函数或一长串临时量。采取这种方式，意味客户端代码将与找过程中的导航结构紧密耦合。一旦对象间的关系发生任何变化，客户端就不得不做出相应修改。

这时候应该使用隐委托关系（189）。你可以在消息链的不同位置采用这种重构手法。理论上，你可以重构消息链上的所有对象，但这么做就会把所有中间对象都变成「中间人」。通常更好的选择是：先观察消息链最终得到的对象是用来干什么的，看看能否以提炼函数（106）把使用该对象的代码提炼到一个独立的函数中，再运用搬移函数（198）把这个函数推入消息链。如果还有许多客户端代码需要访问链上的其他对象，同样添加一个函数来完成此事。有些人把任何函数链都视为坏东西，我们不这样想。我们的冷静镇定是出了名的，起码在这件事上是这样的。

## 3.18 Middle Man

One of the prime features of objects is encapsulation—hiding internal details from the rest of the world. Encapsulation often comes with delegation. You ask a director whether she is free for a meeting; she delegates the message to her diary and gives you an answer. All well and good. There is no need to know whether the director uses a diary, an electronic gizmo, or a secretary to keep track of her appointments.

However, this can go too far. You look at a class’s interface and find half the methods are delegating to this other class. After a while, it is time to use Remove Middle Man (192) and talk to the object that really knows what’s going on. If only a few methods aren’t doing much, use Inline Function (115) to inline them into the caller. If there is additional behavior, you can use Replace Superclass with Delegate (399) or Replace Subclass with Delegate (381) to fold the middle man into the real object. That allows you to extend behavior without chasing all that delegation.

对象的基本特征之一就是封装一一对外部世界隐藏其内部细节。封装往往伴随着委托。比如，你问主管是否有时间参加一个会议，他就把这个消息「委托」给他的记事簿，然后才能回答你。很好，你没必要知道这位主管到底使用传统记事还是使用电子记事簿抑或是秘书来记录自己的约会。

但是人们可能过度运用委托。你也许会看到某个类的接口有一半的函数都委托给其他类，这样就是过度运用。这时应该使用移除中间人（192），直接和真正负责的对象打交道。如果这样「不干实事」的函数只有少数几个，可以运用内联函数（115）把它们放进调用端。如果这些中间人还有其他行为，可以运用以委托取代超类（399）或者以委托取代子类（381）把它变成真正的对象，这样你既可以扩展原对象的行为，又不必负担那么多的委托动作。

## 3.19 Insider Trading

Software people like strong walls between their modules and complain bitterly about how trading data around too much increases coupling. To make things work, some trade has to occur, but we need to reduce it to a minimum and keep it all above board.

Modules that whisper to each other by the coffee machine need to be separated by using Move Function (198) and Move Field (207) to reduce the need to chat. If modules have common interests, try to create a third module to keep that commonality in a wellregulated vehicle, or use Hide Delegate (189) to make another module act as an intermediary.

Inheritance can often lead to collusion. Subclasses are always going to know more about their parents than their parents would like them to know. If it’s time to leave home, apply Replace Subclass with Delegate (381) or Replace Superclass with Delegate (399).

软件开发者喜欢在模块之间建起高墙，极其反感在模块之间大量交换数据，因为这会增加模块的耦合。在实际情况里，一定的数据交换不可避免，但我们必须尽量减少这种情况，并把这种交换都放到明面上来。如果两个模块总是在咖啡机旁边窃窃私语，就应该用移函数（198）和搬移字段（207）减少它们的私下交流。如果两个模块有共同的兴趣，可以尝试再新建一个模块，把这些共用的数据放在一个管理良好的地方；或者用隐藏委托关系（189），把另一个模块变成两者的中介。

继承常会造成密谋，因为子类对超类的了解总是超过后者的主观愿望。如果你觉得该让这个孩子独立生活了，请运用以委托取代子类（381）或以委托取代超类（399）让它离开继承体系。

## 3.20 Large Class

When a class is trying to do too much, it often shows up as too many fields. When a class has too many fields, duplicated code cannot be far behind.

You can Extract Class (182) to bundle a number of the variables. Choose variables to go together in the component that makes sense for each. For example, “depositAmount” and “depositCurrency” are likely to belong together in a component. More generally, common prefixes or suffixes for some subset of the variables in a class suggest the opportunity for a component. If the component makes sense with inheritance, you’ll find Extract Superclass (375) or Replace Type Code with Subclasses (362) (which essentially is extracting a subclass) are often easier.

Sometimes a class does not use all of its fields all of the time. If so, you may be able to do these extractions many times.

As with a class with too many instance variables, a class with too much code is a prime breeding ground for duplicated code, chaos, and death. The simplest solution (have we mentioned that we like simple solutions?) is to eliminate redundancy in the class itself. If you have five hundred­line methods with lots of code in common, you may be able to turn them into five ten­line methods with another ten two­line methods extracted from the original.

The clients of such a class are often the best clue for splitting up the class. Look at whether clients use a subset of the features of the class. Each subset is a possible separate class. Once you’ve identified a useful subset, use Extract Class (182), Extract Superclass (375), or Replace Type Code with Subclasses (362) to break it out.

如果想利用单个类做太多事情，其内往往就会出现太多字段。一旦如此，重复代码也就接踵而至了。你可以运用提炼类（182）将几个变量一起提炼至新类内。提炼时应该选择类内彼此相关的量，将它们放在一起。例如，depositAmount 和 depositCurrency 可能应该隶属同一个类。通常，如果类内的数个变量有着相同的前缀或后缀，这就意味着有机会把它们提炼到某个组件内。如果这个组件适合作为ー个子类，你会发现提炼超类（375）或者以子类取代类型码（362）（其实就是提炼子类）往往比较简单。

有时候类并非在所有时刻都使用所有字段。若果真如此，你或许可以进行多次提炼。和「太多实例变量」一样，类内如果有太多代码，也是代码重复、混乱并最终走向死亡的源头。最简单的解决方案（还记得吗，我们喜欢简单的解决方案）是把多余的东西消弭于类内部。如果有 5 个「百行函数」，它们之中很多代码都相同，那么或许你可以把它们成 5 个「十行函数」和 10 个提炼出来的「双行函数」。

观察一个大类的使用者，经常能找到如何拆分类的线索。看看使用者是否只用到了这个类所有功能的一个子集，每个这样的子集都可能拆分成一个独立的类。一旦识出一个合适的功能子集，就试用提炼类（182）、提炼超类（375）或是以子类取代类型码（362）将其拆分出来。

## 3.21 Alternative Classes with Different Interfaces

One of the great benefits of using classes is the support for substitution, allowing one class to swap in for another in times of need. But this only works if their interfaces are the same. Use Change Function Declaration (124) to make functions match up. Often, this doesn’t go far enough; keep using Move Function (198) to move behavior into classes until the protocols match. If this leads to duplication, you may be able to use Extract Superclass (375) to atone.

使用类的好处之一就在于可以替换：今天用这个类，未来可以成用另一个类。但只有当两个类的接口一致时，才能做这种替换。可以用改变函数声明（124）将函数签名变得一致。但这往往还不够，请反复运用移函数（198）将某些行为移入类中，直到两者的协议一致为止。如果搬移过程造成了重复代码，或许可运用提炼超类（375）补偿一下。

## 3.22 Data Class

These are classes that have fields, getting and setting methods for the fields, and nothing else. Such classes are dumb data holders and are often being manipulated in far too much detail by other classes. In some stages, these classes may have public fields. If so, you should immediately apply Encapsulate Record (162) before anyone notices. Use Remove Setting Method (331) on any field that should not be changed.

Look for where these getting and setting methods are used by other classes. Try to use Move Function (198) to move behavior into the data class. If you can’t move a whole function, use Extract Function (106) to create a function that can be moved.

2『纯函数做一张术语卡片。』——已完成

Data classes are often a sign of behavior in the wrong place, which means you can make big progress by moving it from the client into the data class itself. But there are exceptions, and one of the best exceptions is a record that’s being used as a result record from a distinct function invocation. A good example of this is the intermediate data structure after you’ve applied Split Phase (154). A key characteristic of such a result record is that it’s immutable (at least in practice). Immutable fields don’t need to be encapsulated and information derived from immutable data can be represented as fields rather than getting methods.

所谓纯数据类是指：它们拥有一些字段，以及用于访问（读写）这些字段的函数，除此之外一无长物。这样的类只是一种不会说话的数据容器，它们几乎一定被其他类过分细琐地操控着。这些类早期可能拥有 public 字段，若果真如此，你应该在别人注意到它们之前，立刻运用封装记录（162）将它们封装起来。对于那些不该被其他类修改的字段，请运用移除设值函数（331）。然后，找出这些取值 / 设值函数被其他类调用的地点。尝试以移函数（198）把那些调用行为搬移到纯数据类里来。如果无法搬移整个函数，就运用提炼函数 (106) 产生一个可被搬移的函数。

纯数据类常常意味着行为被放在了错误的地方。也就是说，只要把处理数据的行为从客户端搬移到纯数据类里来，就能使情况大为改观。但也有例外情况，一个最好的例外情况就是，纯数据记录对象被用作函数调用的返回结果，比如使用拆分阶段（154）之后得到的中转数据结构就是这种情況。这种结果数据对象有一个关键的特征：它是不可修改的（至少在拆分阶段（154）的实际操作中是这样）。不可修改的字段无须封装，使用者可以直接通过字段取得数据，无须通过取值函数。

## 3.23 Refused Bequest

Subclasses get to inherit the methods and data of their parents. But what if they don’t want or need what they are given? They are given all these great gifts and pick just a few to play with.

The traditional story is that this means the hierarchy is wrong. You need to create a new sibling class and use Push Down Method (359) and Push Down Field (361) to push all the unused code to the sibling. That way the parent holds only what is common. Often, you’ll hear advice that all superclasses should be abstract.

You’ll guess from our snide use of “traditional” that we aren’t going to advise this—at least not all the time. We do subclassing to reuse a bit of behavior all the time, and we find it a perfectly good way of doing business. There is a smell—we can’t deny it—but usually it isn’t a strong smell. So, we say that if the refused bequest is causing confusion and problems, follow the traditional advice. However, don’t feel you have to do it all the time. Nine times out of ten this smell is too faint to be worth cleaning.

The smell of refused bequest is much stronger if the subclass is reusing behavior but does not want to support the interface of the superclass. We don’t mind refusing implementations—but refusing interface gets us on our high horses. In this case, however, don’t fiddle with the hierarchy; you want to gut it by applying Replace Subclass with Delegate (381) or Replace Superclass with Delegate (399).

子类应该继承超类的函数和数据。但如果它们不想或不需要继承，又该怎么办呢？它们得到所有礼物，却只从中挑选几样来玩！按传统说法，这就意味着继承体系设计错误。你需要为这个子类新建一个兄弟类，再运用函数下移（359) 和字段下移（361）把所有用不到的函数下推给那个兄弟。这样一来，超类就只持有所有子类共享的东西。你常常会听到这样的建议：所有超类都应该是抽象（abstract）的。

既然使用「传统说法」这个略带贬义的词，你就可以猜到，我们不建议你这么做，起码不建议你每次都这么做。我们经常利用继承来复用一些行为，并发现这可以很好地应用于日常工作。这也是一种坏味道，我们不否认，但气味通常并不强烈，所以我们说，如果「被拒绝的遗赠」正在引起困惑和问题，请遵循传统忠告。但不必认为你每次都得那么做。十有八九这种坏味道很淡，不值得理睬。

如果子类复用了超类的行为（实现），却又不愿意支持超类的接口，「被拒绝的遗赠」的坏味道就会变得很浓烈。拒绝继承超类的实现，这一点我们不介意；但如果拒绝支持超类的接口，这就难以接受了。既然不愿意支持超类的接口，就不要假情假意地糊弄继承体系，应该运用以委托取代子类（381）或者以委托取代超类（399）彻底划清界限。

## 2.24 Comments

Don’t worry, we aren’t saying that people shouldn’t write comments. In our olfac­tory analogy, comments aren’t a bad smell; indeed they are a sweet smell. The reason we mention comments here is that comments are often used as a deodorant. It’s surprising how often you look at thickly commented code and notice that the comments are there because the code is bad.

Comments lead us to bad code that has all the rotten whiffs we’ve discussed in the rest of this chapter. Our first action is to remove the bad smells by refactoring. When we’re finished, we often find that the comments are superfluous.

If you need a comment to explain what a block of code does, try Extract Function (106). If the method is already extracted but you still need a comment to explain what it does, use Change Function Declaration (124) to rename it. If you need to state some rules about the required state of the system, use Introduce Assertion (302).

When you feel the need to write a comment, first try to refactor the code so that any comment becomes superfluous.

A good time to use a comment is when you don’t know what to do. In addition to describing what is going on, comments can indicate areas in which you aren’t sure. A comment can also explain why you did something. This kind of information helps future modifiers, especially forgetful ones. 

别担心，我们并不是说你不该写注释。从嗅觉上说，注释不但不是一种坏味道，事实上它们还是一种香味呢。我们之所以要在这里提到注释，是因为人们常把它当作「除臭剂」来使用。常常会有这样的情况：你看到一段代码有着长长的注释，然后发现，这些注释之所以存在乃是因为代码很糟糕。这种情的发生次数之多，实在令人吃惊。

注释可以带我们找到本章先前提到的各种坏味道。找到坏味道后，我们首先应该以各种重构手法把坏味道去除。完成之后我们常常会发现：注释已经得多余了，因为代码已经清楚地说明了一切。如果你需要注释来解释一块代码做了什么，试试提炼函数（106）；如果函数已经提炼出来，但还是需要注释来解释其行为，试试用改变函数声明（124）为它改名；如果你需要注释说明某些系统的需求规格，试试引入断言（302）。

当你感觉需要写注释时，请先尝试重构，试着让所有注释都变得多余。如果你不知道该做什么，这才是注释的良好运用时机。除了用来记述将来的打算之外，注释还可以用来标记你并无十足把握的区域。你可以在注释里写下自己「为什么做某某事」。这类信息可以帮助将来的修改者，尤其是那些健忘的家伙。
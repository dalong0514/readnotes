# 0601. Object Calisthenics

by Jeff Bay, Technology Principal

## Conclusion

Eight of these nine rules are simply ways to visualize and implement the Holy Grail of object-oriented programming — the encapsulation of data. In addition, another drives the appropriate use of polymorphism (not using else and minimizing all conditional logic), and another is a naming strategy that encourages concise and straightforward naming standards, without inconsistently applied and hard-to-pronounce abbreviations.

The entire thrust is to craft code that has no duplication in code or idea. The goal is code that concisely expresses simple and elegant abstractions for the incidental complexity we deal with all day long.

In the long run, you will inevitably ﬁnd that these rules contradict each other in some situations or that applying the rules leads to degenerate results. For the purpose of the exercise, however, spend 20 hours and 1,000 lines writing code that conforms 100% to these rules. You will ﬁnd yourself having to break old habits and change rules that you may have lived with for your whole programming life. Each of the rules has been chosen such that if you follow it, you will encounter situations that would typically have an obvious (but perhaps incorrect) answer that is not available to you.

Following these rules with discipline will force you to come up with the harder answers that lead to a much richer understanding of object-oriented programming. If you write 1,000 lines that follow all these rules, you will ﬁnd that you have created something completely different from what you expected. Follow the rules, and see where you end up. If you keep working at it, the code you are writing might conform to these rules without any conscious effort on your part.

On a ﬁnal note, some might see these rules as overkill or impossible to apply in a real working system. They would be incorrect — I’m ﬁnalizing a system as this book goes to press that has more than 100,000 lines written in this style. The programmers working on this system routinely follow these rules and are each overjoyed to see how much less tiresome development can be when embracing deep simplicity.

前面九条规则中，有八条都是非常简单易行的，能够帮助程序员获得面向对象程序设计的圣 杯 —— 数据封装。另外，有一条规则（不要使用 else，尽量简化条件判断逻辑）鼓励程序员 适当地使用多态；还有一条规则是命名策略，鼓励程序员使用一致的、直接的命名标准，不 要使用难以理解的缩写。

一言以蔽之，就是想尽办法消除代码中的重复。我们每天都要面对复杂的问题，而我们的目 标是，用精炼的代码表达出简单而优美的抽象。

时间长了以后，你会发现在某些情境下，这些规则其实会彼此抵触，如果强加使用可能会产 生糟糕的结果。然而，出于练习的目的，你不妨花上 20 个小时，在 100% 地遵守这些规则 的前提下，编写 1000 行代码。这样你会发现，自己已经开始打破旧有的习惯了，并且改变 了一些曾经墨守的游戏规则。如果遵循本文介绍的这些规则，你必然会遇到这种情形：编程 时似乎看到了一个很明显的做法，但是并不应该采纳它，因为这种顺理成章的做法很可能是 错误的。

将这些规则当作纪律来遵守，它们会帮助你解答更复杂的问题，同时加深你对面向对象编程 的理解程度。如果按照这些规则的要求写上 1000 行代码的话，你会发现最终的结果和编写 代码以前所期望的完全不同。尝试一下这些规则，看看最终的结果如何。如果还能够继续遵 守它们，那么以后你就能非常自然地写出符合上面规则的代码了，而不必刻意地记住这些规则。

最后要说的是，有些人可能认为这些规则过于刻板，不可能在真实的系统中实施。他们都错 了 —— 在本书即将出版的时候，我们刚刚完成了一个超过 100 000 行代码的系统，它严格遵 守本文中提到的所有规则。参与这个项目的程序员全部都认真地遵守了上述规则。最终每个 人都非常高兴地看到：如果努力地拥抱简单性，那么开发过程会快乐得多。

## 6.1 Nine Steps to Better Software Design Today

We’ve all seen poorly written code that’s hard to understand, test, and maintain. Object-oriented programming promised to save us from our old procedural code, allowing us to write software incrementally, reusing as we go. But sometimes it seems like we’re just chasing down the same old complex, coupled designs in Java that we had in C. This essay will give new programmers an opportunity to learn best practices while writing their own code. For sophisticated and experienced programmers, it will give you a vehicle to refocus on best practices or to use for demonstration purposes in teaching co-workers.

Good object-oriented design can be hard to learn; however, it can also result in immense gains in simplicity. Transitioning from procedural development to object-oriented design requires a major shift in thinking that is more difﬁcult than it seems. Many developers assume they’re doing a good job with OO design, when in reality they’re unconsciously stuck in procedural habits that are hard to break. It doesn’t help that many examples and best practices (even Sun’s code in the JDK) encourage poor OO design in the name of performance or the simple weight of history.

The core concepts behind good design are well understood. As an example, here are seven code qualities that are commonly known to matter: cohesion, loose coupling, zero duplication, encapsulation, testability, readability, and focus. Yet it’s hard to put those concepts into practice. It is one thing to understand that encapsulation means hiding data, implementation, type, design, or construction. It’s another thing altogether to design code that implements encapsulation well. So here’s an exercise that can help you internalize principles of good object-oriented design and actually use them in real life.

## 6.2 The Exercise

Do a simple project using far stricter coding standards than you’ve ever used in your life. In this essay, you’ll ﬁnd nine “rules of thumb” that will help push you into writing code that is almost required to be object-oriented. This will allow you to make better decisions and give you more and better options when confronted with the problems of your day job.

By suspending disbelief and rigidly applying these rules on a small, 1,000-line project, you’ll start to see a signiﬁcantly different approach to designing software. Once you’ve written 1,000 lines of code, the exercise is done, and you can relax and go back to using these rules as guidelines.

This is a hard exercise, especially because many of these rules are not universally applicable. The fact is that sometimes classes are little more than ﬁfty lines. But there’s great value in thinking about what would have to happen to move those responsibilities into real, ﬁrst-class objects of their own. It’s developing this type of thinking that’s the real value of the exercise. So, stretch the limits of what you imagine is possible, and see whether you start thinking about your code in a new way.

The Rules

Here are the rules for the exercise:

1 Use only one level of indentation per method.

2  Don’t use the else keyword.

3 Wrap all primitives and strings.

4 Use only one dot per line.

5 Don’t abbreviate.

6 Keep all entities small.

7 Don’t use any classes with more than two instance variables.

8 Use ﬁrst-class collections.

9 Don’t use any getters/setters/properties.

Rule 1: Use One Level of Indentation per Method

Ever stare at a big old method wondering where to start? A giant method lacks cohesiveness. One guideline is to limit method length to ﬁve lines, but that kind of transition can be daunting if your code is littered with 500-line monsters. Instead, try to ensure that each method does exactly one thing — one control structure or one block of statements per method. If you have nested control structures in a method, you’re working at multiple levels of abstraction, and that means you’re doing more than one thing.

As you work with methods that do exactly one thing, expressed within classes doing exactly one thing, your code begins to change. As each unit in your application becomes smaller, your level of reuse will start to rise exponentially. It can be difﬁcult to spot opportunities for reuse within a method that has ﬁve responsibilities and is implemented in 100 lines. A three-line method that manages the state of a single object in a given context is usable in many different contexts.

Use the Extract Method feature of your IDE to pull out behaviors until your methods have only one level of indentation, like this, for example:

Notice that another effect has occurred with this refactoring. Each individual method has become virtually trivial to match its implementation to its name. Determining the existence of bugs in these much smaller snippets is frequently much easier.

Here at the end of the ﬁrst rule, I should also point out that the more you practice applying the rules, the more the advantages come to fruition. Your ﬁrst attempts to decompose problems in the style presented here will feel awkward and likely lead to little gain that you can perceive. There is a skill to applying the rules, however; this is the art of the programmer raised to another level.

Rule 2: Don’t Use the else Keyword

Every programmer understands the if/else construct. It is built into nearly every programming language, and simple conditional logic is easy for anyone to understand. Nearly every programmer has seen a nasty nested conditional that’s impossible to follow or a case statement that goes on for pages. Even worse, it is all too easy to simply add another branch to an existing conditional rather than factoring to a better solution. Conditionals are also a frequent source of duplication. Status ﬂags, for example, frequently lead to this kind of trouble:

Here, four lines have been collapsed down to one line with one extra word on it. Note that early returns can easily reduce clarity if overused. See the Design Patterns book [GHJV95] for the Strategy pattern to ﬁnd an example of using polymorphism to avoid branching on the status inline. The Strategy pattern is particularly useful here if the branch on the status is duplicated in multiple places.

Object-oriented languages give you a powerful tool — polymorphismfor handling complex conditional cases. Simple cases can be replaced with guard clauses and early returns. Designs that use polymorphism can be easier to read and maintain and can express their intent more clearly. But it’s not always easy to make the transition, especially when you have else in your back pocket. So as part of this exercise, you’re not allowed to use else. Try the Null Object pattern; it may help in some situations. Other tools can help you rid yourself of the else as well. See how many alternatives you can come up with.

Rule 3: Wrap All Primitives and Strings

An int on its own is just a scalar with no meaning. When a method takes an int as a parameter, the method name needs to do all the work of expressing the intent. If the same method takes an hour as a parameter, it’s much easier to see what’s happening. Small objects like this can make programs more maintainable, since it isn’t possible to pass a year to a method that takes an hour parameter. With a primitive variable, the compiler can’t help you write semantically correct programs. With an object, even a small one, you are giving both the compiler and the programmer additional information about what the value is and why it is being used.

Small objects such as hour or money also give you an obvious place to put behavior that otherwise would have been littered around other classes. This becomes especially true when you apply the rule relating to getters and setters and only the small object can access the value.

Rule 4: Use Only One Dot per Line

Sometimes it’s hard to know which object should take responsibility for an activity. If you start looking for lines of code with multiple dots, you’ll start to ﬁnd many misplaced responsibilities. If you have more than one dot on any given line of code, the activity is happening in the wrong place. Maybe your object is dealing with two other objects at once. If this is the case, your object is a middleman; it knows too much about too many people. Consider moving the activity into one of the other objects.

If all those dots are connected, your object is digging deeply into another object. These multiple dots indicate that you’re violating encapsulation. Try asking that object to do something for you, rather than poking around its insides. A major part of encapsulation is not reaching across class boundaries into types that you shouldn’t know about.

The Law of Demeter (“talk only to your friends”) is a good place to start, but think about it this way: you can play with your toys, with toys that you make, and with toys that someone gives you. You don’t ever, ever play with your toy’s toys.

Note that in this example the algorithm’s implementation details are more diffuse, which can make it a little harder to understand at a glance. However, you just create a named method for the piece’s transformation into a character. This is a method with a strong cohesive name and job and is quite likely to be reused — the odds of representation.substring(0, 1)" being repeated in other parts of the program has now been reduced dramatically. The method names take the place of comments in this brave new world — spend time on those names. It really isn’t more difﬁcult to understand a program with this type of structure; it simply requires a slightly different approach.

Rule 5: Don’t Abbreviate

It’s often tempting to abbreviate in the names of classes, methods, or variables. Resist the temptation. Abbreviations can be confusing, and they tend to hide larger problems.

Think about why you want to abbreviate. Is it because you’re typing the same word over and over again? If that’s the case, perhaps your method is used too heavily, and you are missing opportunities to remove duplication. Is it because your method names are getting long? This might be a sign of a misplaced responsibility or a missing class.

Try to keep class and method names to one to two words, and avoid names that duplicate the context. If the class is an Order, the method doesn’t need to be called shipOrder(). Simply name the method ship() so that clients call order.ship() — a simple and clear representation of what’s happening.

For this exercise, all entities should have a name that is one or two words, with no abbreviations.

Rule 6: Keep All Entities Small

This means no class that’s more than ﬁfty lines and no package that’s more than ten ﬁles.

Classes of more than ﬁfty lines usually do more than one thing, which makes them harder to understand and harder to reuse. Fifty-line classes have the added beneﬁt of being visible on one screen without scrolling, which makes them easier to grasp quickly.

What’s challenging about creating such small classes is that there are often groups of behaviors that make logical sense together. This is where you need to leverage packages. As your classes become smaller and have fewer responsibilities and as you limit package size, you’ll start to see that packages represent clusters of related classes that work together to achieve a goal. Packages, like classes, should be cohesive and have a purpose. Keeping those packages small forces them to have a real identity.

Rule 7: Don’t Use Any Classes with More Than Two Instance Variables

Most classes should simply be responsible for handling a single state variable, but a few will require two. Adding a new instance variable to a class immediately decreases the cohesion of that class. In general, while programming under these rules, you’ll ﬁnd that there are two kinds of classes, those that maintain the state of a single instance variable and those that coordinate two separate variables. In general, don’t mix the two kinds of responsibilities.

The discerning reader might have noticed that rules 3 and 7 can be considered to be isomorphic. In a more general sense, there are few cases where a cohesive single job description can be created for a class with many instance variables.

Here’s an example of the kind of dissection I’m asking you to engage in:

Note that in thinking about how to do the decomposition, the opportunity to separate the concerns of a family name (used for many legal entity restrictions) could be separated from an essentially different kind of name. The GivenName object here contains a list of names, allowing the new model to absorb people with ﬁrst, middle, and other given names. Frequently, the decomposition of instance variables leads to an understanding of commonality of several related instance variables. Sometimes several related instance variables actually have a related life in a ﬁrst-class collection.

Decomposing objects from a set of attributes into a hierarchy of collaborating objects leads much more directly to an effective object model. Prior to understanding this rule, I spent many hours trying to follow data ﬂows through large objects. It was possible to tweeze out an object model, but it was a painstaking process to understand the related groups of behavior and see the result. In contrast, the recursive application of this rule has led to a very quick decomposition of complex large objects into much simpler models. Behavior naturally follows the instance variables into the appropriate place — the compiler and the rules on encapsulation won’t allow otherwise. If you get stuck, work downward by splitting objects into related halves or upward by picking any two instance variables and making an object out of them.

Rule 8: Use First-Class Collections

The application of this rule is simple: any class that contains a collection should contain no other member variables. Each collection gets wrapped in its own class, so now behaviors related to the collection have a home. You may ﬁnd that ﬁlters become part of this new class. Filters may also become function objects in their own right. Also, your new class can handle activities such as joining two groups together or applying a rule to each element of the group. This is an obvious extension of the rule about instance variables but is important for its own sake as well. A collection is really a type of very useful primitive. It has many behaviors but little semantic intent or clues for either the next programmer or the maintainer.

Rule 9: Don’t Use Any Getters/Setters/Properties

The last sentence of the previous rule leads almost directly to this rule. If your objects are now encapsulating the appropriate set of instance variables but the design is still awkward, it is time to examine some more direct violations of encapsulation. The behavior will not follow the instance variable if it can simply ask for the value in its current location. The idea behind strong encapsulation boundaries is to force programmers working on the code after you leave it to look for and place behavior into a single place in the object model. This has many beneﬁcial downstream effects, such as a dramatic reduction in duplication errors and a better localization of changes to implement new features.

This rule is commonly stated as “Tell, don’t ask.”

对象健身操

1.1 九步迈向优秀软件设计

我们大都读过糟糕的代码。这些代码通常都难以理解、测试和维护。面向对象编程一直在鼓 励我们摆脱过程式代码的桎梏，帮助我们以累加的方式编写代码，并重用已有的组件。但有 些时候，我们似乎只是把原来陈旧的、充满耦合的设计从 C 程序搬到了 Java 中而已。这篇 文章会向编程新手讲述一些非常实用的最佳实践。对于资深的程序员来说，这篇文章可以让 你再回顾一下以往的最佳实践，也可以在培训新员工时，作为抽象原则的具体实现示例。

要想掌握优秀的面向对象设计并非易事；但一旦掌握，优秀的设计会在简单性上带来巨大的 回报。从过程化的开发到面向对象设计之间的思维转换，要远比看上去的复杂得多。很多开 发者都自以为擅长 OO 设计，但在实际应用时，还是不自觉地回到过程化的编程习惯上了，这已经是根深蒂固的观念。更糟糕的是，很多实例和最佳实践（甚至 Sun 在 JDK 中的代码） 甚至鼓励人们采用糟糕的 OO 设计 —— 其中一些尚有性能考量作为托辞，而另一些则纯粹是 历史包袱。

优秀设计背后的核心概念其实并不高深。比如内聚性、松耦合、零重复、封装、可测试性、 可读性以及单一职责。这七条评判代码质量的原则就已经被广泛接受了。然而真正困难的是 如何把这些概念付诸实践。理解了封装就是隐藏「数据、实现细节、类型、设计或者构造」，这只是设计出良好封装的代码的第一步而已。因此，本文接下来是一系列实践规则和练习，它可以帮助你将良好的面向对象设计原则变得更加具体，从而在现实世界中应用那些原则。

1.2 练习

在一个简单的项目里尝试一些比以前严格得多的编码标准。在这篇文章中，你会看到我给出 的「九诫」，它们会迫使你更为严格地以面向对象的风格编写代码。在日常工作中遇到问题 时，这些法则可以帮你做出更正确的决定，或者给你更多更好的选择。请你暂时放弃怀疑，在一个代码量为 1000 行左右的小项目里严格地遵守这些法则，到时你会体验到一种完全 不同的软件设计的方法。在写完这 1000 行左右的代码后，练习就结束了，你就能放心地 将这些规则当作指导原则了。

下面的练习有一定困难，尤其因为所有规则并不是放之四海皆准的法则。比如，很难保证所 有的类的长度都不超过 50 行，例外总会出现。但是这种做法背后的价值在于，你应该把与 某一职责相关的代码移到真正的、一流的对象中。这个练习的真正价值也在于此，即引发你 在开发过程中进行这种思考。所以，现在开始扩展你想象力的极限吧，然后看一看你是不是 已经以一种全新的方式思考你的代码了？

规则

下面是练习中要遵守的规则：

1、方法只使用一级缩进。

2、拒绝使用 else 关键字。

3、封装所有的原生类型和字符串。

4、一行代码只有一个 `.` 运算符。

5、不要使用缩写。

6、保持实体对象简单清晰。

7、任何类中的实例变量都不要超过两个。

8、使用一流的集合。

9、不使用任何 Getter/Setter/Property。

规则 1：方法只使用一级缩进

你是否曾经盯着一个体型巨大的老方法而感到无从下手过。庞大的方法通常缺少内聚性。一 个常见的原则是将方法的行数控制在 5 行之内，但是如果你的方法已经是一个 500 行的大怪 兽了，想要达到这一原则的要求是非常痛苦的。其实，你不妨尝试让每个方法只做一件事 — 每个方法只包含一个控制结构或者一个代码块。如果你在一个方法中嵌套了多层控制结构，那么你就要处理多个层次上的抽象，这意味着同时做多件事。

如果每个方法都只关注一件事，而它们所在的类也只做一件事，那么你的代码就开始变化了。由于应用程序中的每个单元都变得更小了，代码的可重用性开始指数增长。一个 100 行的，肩负五种不同职责的方法很难被重用。如果一个很短的方法在设置了上下文后，能够管理一 个对象的状态，那么它可以应用在很多不同的上下文中。

利用 IDE 提供的「抽取方法」功能，不断地抽取方法中的行为，直到它只有一级缩进为止。请看下面的实例。

注意这项重构还能带来另一种效果：每个单独的方法都变得更简单了，同时其实现也与其名 称更加匹配。在这样短小的代码段中查找 bug 通常会更加容易。

第一条规则在此接近尾声了。我还要强调，你越多实践这条规则，就会越多地尝到它带来的 甜头。当你第一次尝试解决前面展示的那一类问题时，可能不是非常熟练，也未必能获得很 多收获。但是，应用这些规则的技能是一种艺术，它能将程序员提升到一个新的高度。

规则 2：拒绝 else 关键字

每个程序员都熟知 if/else 结构。几乎每种语言都支持 if/esle。简单的条件判断对任何人来 说都不难理解。不过大多数程序员也见识过令人眩晕的层层嵌套的条件判断，或连绵数页的 case 语句。更糟糕的是，在现有的判断条件上加一个新的分支通常是非常容易的，而将它重 构为一个更好的方式的想法却罕有人去提及。条件判断结构通常还是重复代码的来源。例如，状态标识经常会带来这样的问题。

在上面的例子中，第二段代码由于使用了三元运算符，所以代码长度从四行压缩到了一行。需要小心的是，如果过度使用「提前返回」，代码的清晰度很快会降低。《设计模式》[GHJV95] 一书中关于策略模式的部分里有一个实例，演示了如何使用多态避免根据状态进行分支选择 的代码。如果这种根据状态进行分支选择的代码大量地重复，就应该考虑使用策略模式了。

面向对象编程语言给我们提供了一种更为强大的工具 —— 多态。它能够处理更为复杂的条件 判断。对于简单的条件判断，我们可以使用「卫语句」和「提前返回」替换它。而基于多态 的设计则更容易阅读与维护，从而可以更清晰地表达代码的内在意图。但是，程序员要做出 这样的转变并不是一帆风顺的。尤其是你的代码中可能早已充斥了 else。所以，作为这个练 习的一部分，你是不可以使用 else 的。在某些场景下可以使用 Null Object 模式，它会对你有所帮助。另外还有很多工具和技术都可以帮助你甩掉 else。试一试，看你能提出多少种方 案来？

规则 3：封装所有的原生类型和字符串

整数自身只代表一个数量，没有任何含义。当方法的参数是整数时，我们就必须在方法名中 描述清楚参数的意思。如果此方法使用「Hour」作为参数，就能够让程序员更容易地理解 它的含义了。像这样的小对象可以提高程序的可维护性，因为你不可能给一个参数为「Hour」的方法传一个「Year」。如果使用原生变量，编译器不能帮助你编写语义正确的程序。如果 使用对象，哪怕是很小的对象，它都能够给编译器和其他程序员提供更多的信息 —— 这个值 是什么，为什么使用它。

像 Hour 或 Money 这样的小对象还提供了放置一类行为的场所，这些行为放在其他的类中都 不合适。在你了解了关于 getter 和 setter 的规则时，这一点会非常明显，有些值只能被这些 小对象来访问。

规则 4：一行代码只有一个「.」运算符

有时候我们很难判断出一个行为的职责应该由哪个对象来承担。如果你看一看那些包含了多 个「.」的代码，就会从中发现很多没有被正确放置的职责。如果代码中每一行都有多个「.」，那么这个行为就发生在错误的位置了。也许你的对象需要同时与另外两个对象打交道。在这 种情况下，你的对象只是一个中间人；它知道太多关于其他对象的事情了。这时可以考虑把 该行为移到其他对象之中。

如果这些「.」都是彼此联系的，你的对象就已经深深地陷入到另一个对象之中了。这些过 量的「.」说明你破坏了封装性。尝试着让对象为你做一些事情，而不要窥视对象内部的细 节。封装的主要含义就是，不要让类的边界跨入到它不应该知道的类型中。

迪米特法则（The Law of Demeter，「只和身边的朋友交流」）是一个很好的起点。还可以这 样思考它：你可以玩自己的玩具，可以玩你制造的玩具，还有别人送给你的玩具。但是永远 不要碰你的玩具。

注意在这个例子中，算法的实现细节被过度地扩散开了。程序员很难看一眼就理解它。但是，在为 Piece 转化成 Character 的行为创建一个具有名称的方法后，这个方法的名称和作用就相 当一致了，而且被重用的机会也非常高 —— 令人费解的 representation.substring (0, 1) 调用可 以全部被这个具有名称的方法所代替，程序的可读性又迈进了一大步。在这片新天地里，方 法名取代了注释，所以，值得花些时间为方法取一个有意义的名字。理解并写出这种结构的 程序并不困难，你只需要使用一些稍微不同的手段而已。

规则 5：不要使用缩写

我们总会不自觉地在类名、方法名或者变量名中使用缩写。请抵制住这个诱惑。缩写会令人 迷惑，也容易隐藏一些更严重的问题。

想一想你为什么要使用缩写。因为你厌倦了一遍又一遍地敲打相同的单词？如果是这种情 况，也许你的方法调用得过于频繁，你是不是应该停下来消除一些重复了？因为方法的名字 太长？这可能意味着有些职责没有放在正确的位置或者是有缺失的类。

尽量保持类名和方法名中只包含一到两个单词，避免在名字中重复上下文的信息。比如某个 类是 Order，那么方法名就不必叫做 shipOrder () 了，把它简化为 ship ()，客户端就会调回 order.ship () —— 这能够简单明了地说明代码的意图。

在这个练习中，所有实体对象的名称都只能包含一到两个单词，不能使用缩写。

规则 6：保持实体对象简单清晰

这意味着每个类的长度都不能超过 50 行，每个包所包含的文件不超过 10 个。

代码超过 50 行的类所做的事情通常都不止一件，这会导致它们难以被理解和重用。小于 50 行代码的类还有一个妙处：它可以在一屏幕内显示，不需要滚屏，这样程序员可以很容易、 很快速地熟悉这个类。

创建这样小的类会遇到哪些挑战呢？通常会有很多成组的行为，它们逻辑上是应该在一起 的。这时就需要使用包机制来平衡。随着类变得越来越小，职责越来越少，加之包的大小也 受到限制，你会逐渐注意到，包中的类越来越集中，它们能够协作完成一个相同的目标。包 和类一样，也应该是内聚的，有一个明确的意图。保证这些包足够小，就能让它们有一个真 正的标识。

规则 7：任何类中的实例变量都不要超过两个

大多数的类应该只负责处理单一的状态变量，有些时候也可以拥有两个状态变量。每当为类 添加一个实例变量，就会立即降低类的内聚性。一般而言，编程时如果遵守这些规则，你会 发现只有两种类，一种类只负责维护一个实例变量的状态；另一种类只负责协调两个独立的 变量。不要让这两种职责同时出现在一个类中。

我们来仔细分析下面的示例。

这个类可以被拆分为两个类。

敏锐的读者可能已经注意到了，规则 3 和规则 7 其实是相同问题的不同表述而已。在通常的 情况下，对于一个包含很多实例变量的类来说，很难拥有一个内聚的、单一的职责描述。

注意思考这里是如何分离概念的，其中姓氏（family name）是一个关注点（很多法律实体约 束中需要用到），它可以和其他与其有本质区别的名字分开。GivenName 对象包含了一个名字 的列表。在新的模型中，名称允许包含 first，middle 和其他名字。通常，对实例变量解耦以 后，会加深理解各个相关的实例变量之间的共性。有时，几个相关的实例变量在一流的集合 中会相互关联。

将一个对象从拥有大量属性的状态，解构成为分层次的、相互关联的多个对象，会直接产生 一个更实用的对象模型。在想到这条规则之前，我曾经浪费过很多时间去追踪那些大型对象 的数据流。虽然我们可以理清一个复杂的对象模型，但是理解各组相关的行为并看到结果是 一个非常痛苦的过程。相比而言，不断应用这条规则，可以快速将一个复杂的大对象分解成为大量简单的小对象。行为也自然而然地随着各个实例变量流入到了适当的地方 —— 否则编 译器和封装法则都不会高兴的。当你真正开始做的时候，可以沿着两个方向进行：其一，可 以将对象的实例变量按照相关性分离在两个部分中；另外，也可以创建一个新的对象来封装 两个已有的实例变量。

规则 8：使用一流的集合

应用这条规则的方法非常简单：任何包含集合的类都不能再包含其他的成员变量。每个集合 都被封装在自己的类中，这样，与集合相关的行为就有了自己的家。你可能会发现作用于这 些集合的过滤器将成为这些新类型中的一部分，或是根据它们自身的情况包装为函数对象。另外，这些新的类型还可以处理其他任务，比如将两个集合中的元素拼装到一起，或者对集 合中的元素逐一施加某种规则等。很明显，这条规则是对前面关于实例变量规则的扩展，不 过它自身也有非常重要的含义。集合其实是一种应用广泛的原生类型。它具有很多行为，但 是对于代码的读者和维护者来说，与集合相关的代码通常都缺少对语义意图的解释。

规则 9：不使用任何 Getter/Setter/Property

上一条规则的最后一句话几乎可以直接通向这条规则。如果你的对象已经封装了相应的实例 变量，但是设计仍然很糟糕的话，那就应该仔细地考察一下其他对封装更直接的破坏了。如 果可以从对象之外随便询问实例变量的值，那么行为与数据就不可能被封装到一处。在严格 的封装边界背后，真正的动机是迫使程序员在完成编码之后，一定要为这段代码的行为找到 一个适合的位置，确保它在对象模型中的唯一性。这样做会有很多好处，比如可以很大程度 地减少重复性的错误；另外，在实现新特性的时候，也有一个更合适的位置去引入变化。

这条规则通常被描述为「讲述而不要询问」（Tell，don't ask）。

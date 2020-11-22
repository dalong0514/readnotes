# 2019030Refactoring2EdR00

## 记忆时间

2020-09-14

## 卡片

### 0101. 主题卡——重构手段

### 1.1 提炼函数

代码里提炼出函数。一些好习惯收集：

1、永远将函数的返回值命名为「result」，这样我一眼就能知道它的作用。然后我再次编译、测试、提交代码。

2、函数参数的命令。使用一门动态类型语言（如 JavaScript）时，跟踪变量的类型很有意义。因此，我为参数取名时都默认带上其类型名。一般我会使用不定冠词修饰它，除非命名中另有解释其角色的相关信息。

### 1.2 内联变量

以查询取代临时变量。变量内联的概念。首先移除局部变量。

As I consider the parameters to amountFor, I look to see where they come from. aPerformance comes from the loop variable, so naturally changes with each iteration through the loop. But play is computed from the performance, so there’s no need to pass it in as a parameter at all—I can just recalculate it within amountFor. When I’m breaking down a long function, I like to get rid of variables like play, because temporary variables create a lot of locally scoped names that complicate extractions. The refactoring I will use here is Replace Temp with Query (178).

This refactoring alarms some programmers. Previously, the code to look up the play was executed once in each loop iteration; now, it’s executed thrice. I’ll talk about the interplay of refactoring and performance later, but for the moment I’ll just observe that this change is unlikely to significantly affect performance, and even if it were, it is much easier to improve the performance of a well­-factored code base.

这次重构可能在一些程序员心中敲响警钟：重构前，查找 play 变量的代码在每次循环中只执行了 1 次，而重构后却执行了 3 次。我会在后面探讨重构与性能之间的关系，但现在，我认为这次改动还不太可能对性能有严重影响，即便真的有所影响，后续再对一段结构良好的代码进行性能调优， 也容易得多。

The great benefit of removing local variables is that it makes it much easier to do extractions, since there is less local scope to deal with. Indeed, usually I’ll take out local variables before I do any extractions.

移除局部变量的好处就是做提炼时会简单得多，因为需要操心的局部作用域变少了。实际上，在做任何提炼前，我一般都会先移除局部变量。

### 0102. 反常识卡——重构会加快开发进度

常识：重构会放慢开发进度。反常识：重构会加快开发进度。

出处：Martin Fowler，本书的一个核心观点。

如果你读了前面一小节，我对这个挑战的回应便已经很清楚了。尽管重构的目的是加快开发速度，但是，仍旧很多人认为，花在重构的时间是在拖慢新功能的开发进度。「重构会拖慢进度」这种看法仍然很普遍，这可能是导致人们没有充分重构的最大阻力所在。重构的唯一目的就是让我们开发更快，用更少的工作量创造更大的价值。

Although it’s often managers that are criticized for the counter­-productive habit of squelching refactoring in the name of speed, I’ve often seen developers do it to themselves. Sometimes, they think they shouldn’t be refactoring even though their leadership is actually in favor. If you’re a tech lead in a team, it’s important to show team members that you value improving the health of a code base. That judgment I mentioned earlier on whether to refactor or not is something that takes years of experience to build up. Those with less experience in refactoring need lots of mentoring to accelerate them through the process. 

虽然我们经常批评管理者以「保障开发速度」的名义压制重构，其实程序员自己也经常这么干。有时他们自己觉得不应该重构，其实他们的领导还挺希望他们做一些重构的。如果你是一支团队的技术领导，一定要向团队成员表明，你重视改善代码库健康的价值。合理判断何时应该重构、何时应该暂时不重构，这样的判断力需要多年经验积累。对于重构缺乏经验的年轻人需要有意的指导，才能帮助他们加速经验积累的过程。

But I think the most dangerous way that people get trapped is when they try to justify refactoring in terms of “clean code,” “good engineering practice,” or similar moral reasons. The point of refactoring isn’t to show how sparkly a code base is—it is purely economic. We refactor because it makes us faster—faster to add features, faster to fix bugs. It’s important to keep that in front of your mind and in front of communication with others. The economic benefits of refactoring should always be the driving factor, and the more that is understood by developers, managers, and customers, the more of the “good design” curve we’ll see.

有些人试图用「整洁的代码」、「良好的工程实践」之类道德理由来论证重构的必要性，我认为这是个陷阱。重构的意义不在于把代码库打磨得闪闪发光，而是纯粹经济角度出发的考量。我们之所以重构，因为它能让我们更快——添加功能更快，修复 bug 更快。一定要随时记住这一点，与别人交流时也要不断强调这一点。重构应该总是由经济利益驱动。程序员、经理和客户越理解这一点，「好的设计」那条曲线就会越经常出现。

### 0103. 反常识卡——测试会加快开发进度

常识：测试会放慢开发进度。反常识：测试会加快开发进度。

Refactoring is a valuable tool, but it can’t come alone. To do refactoring properly, I need Tutorialsa solid suite of tests to spot my inevitable mistakes. Even with automated refactoring tools, many of my refactorings will still need checking via a test suite. I don’t find this to be a disadvantage. Even without refactoring, writing good tests increases my effectiveness as a programmer. This was a surprise for me and is counterintuitive for most programmers—so it’s worth explaining why.

重构是很有价值的工具，但只有重构还不行。要正确地进行重构，前提是得有一套稳固的测试集合，以帮我发现难以避免的疏漏。即便有工具可以帮我自动完成一些重构，很多重构手法依然需要通过测试集合来保障。我并不把这视为缺点。我发现，编写优良的测试程序，可以极大提高我的编程速度，即使不进行重构也一样如此。这让我很吃惊，也违反许多程序员的直觉，所以我有必要解释一下这个现象。

### 0104. 主题卡——测试的颗粒度

针对对每个类的每个行为做测试，特别是那些可能产生错误的行为。而对于类的 accessors（读取函数）没必要做测试。

Now I’ll continue adding more tests. The style I follow is to look at all the things the class should do and test each one of them for any conditions that might cause the class to fail. This is not the same as testing every public method, which is what some programmers advocate. Testing should be risk­-driven; remember, I’m trying to find bugs, now or in the future. Therefore I don’t test accessors that just read and write a field: They are so simple that I’m not likely to find a bug there.

This is important because trying to write too many tests usually leads to not writing enough. I get many benefits from testing even if I do only a little testing. My focus is to test the areas that I’m most worried about going wrong. That way I get the most benefit for my testing effort. It is better to write and run incomplete tests than not to run complete tests.

### 0105. 主题卡——既有代码添加测试的具体步骤

That shows the final result, but the way I got it was by first setting the expected value to a placeholder, then replacing it with whatever the program produced (230). I could have calculated it by hand myself, but since the code is supposed to be working correctly, I’ll just trust it for now. Once I have that new test working correctly, I break it by altering the profit calculation with a spurious * 2. I satisfy myself that the test fails as it should, then revert my injected fault. This pattern—write with a placeholder for the expected value, replace the placeholder with the code’s actual value, inject a fault, revert the fault—is a common one I use when adding tests to existing code.

这是最终写出来的测试，但我是怎么写出它来的呢？首先我随便给测试的期望值写了一个数，然后运行测试，将程序产生的实际值（230）填回去。当然，我也可以自己手动计算，不过，既然现在的代码是能正常运行的，我就选择暂时相信它。测试可以正常工作后，我又故技重施，在利润的计算过程插入一个假的乘以 2 逻辑来破坏测试。如我所料，测试会失败，这时我才满意地将插入的假逻辑恢复过来。这个模式是我为既有代码添加测试时最常用的方法：先随便填写一个期望值，再用程序产生的真实值来替换它，然后引入一个错误，最后恢复错误。这个测试随即产生了一些重复代码 —— 它们都在第一行里初始化了同一个测试夹具。正如我对一般的重复代码抱持怀疑，测试代码中的重复同样令我心生疑惑，因此我要试着将它们提到一处公共的地方，以此来消灭重复。一种方案就是把常量提取到外层作用域里。

### 0106. 主题卡——封装数据

Refactoring is all about manipulating the elements of our programs. Data is more awkward to manipulate than functions. Since using a function usually means calling it, I can easily rename or move a function while keeping the old function intact as a forwarding function (so my old code calls the old function, which calls the new function). I’ll usually not keep this forwarding function around for long, but it does simplify the refactoring.

Data is more awkward because I can’t do that. If I move data around, I have to change all the references to the data in a single cycle to keep the code working. For data with a very small scope of access, such as a temporary variable in a small function, this isn’t a problem. But as the scope grows, so does the difficulty, which is why global data is such a pain.

So if I want to move widely accessed data, often the best approach is to first encapsulate it by routing all its access through functions. That way, I turn the difficult task of reorganizing data into the simpler task of reorganizing functions.

1-2『这个思维妙，先以函数的形式封装所有对数据的访问，将重新组织数据转化为重新组织函数。封装数据，做一张主题卡片。（2020-10-05）』——已完成

Encapsulating data is valuable for other things too. It provides a clear point to monitor changes and use of the data; I can easily add validation or consequential logic on the updates. It is my habit to make all mutable data encapsulated like this and only accessed through functions if its scope is greater than a single function. The greater the scope of the data, the more important it is to encapsulate. My approach with legacy code is that whenever I need to change or add a new reference to such a variable, I should take the opportunity to encapsulate it. That way I prevent the increase of coupling to commonly used data.

This principle is why the object­oriented approach puts so much emphasis on keeping an object’s data private. Whenever I see a public field, I consider using Encapsulate Variable (in that case often called Encapsulate Field) to reduce its visibility. Some go further and argue that even internal references to fields within a class should go through accessor functions—an approach known as self­encapsulation. On the whole, I find self­encapsulation excessive—if a class is so big that I need to self­encapsulate its fields, it needs to be broken up anyway. But self­encapsulating a field is a useful step before splitting a class.

Keeping data encapsulated is much less important for immutable data. When the data doesn’t change, I don’t need a place to put in validation or other logic hooks before updates. I can also freely copy the data rather than move it—so I don’t have to change references from old locations, nor do I worry about sections of code getting stale data. Immutability is a powerful preservative.

1『又见函数式编程范式里的「不可变性」，哈哈。（2020-10-05）』

重构的作用就是调整程序中的元素。函数相对容易调整一些，因为函数只有一种用法，就是调用。在改名或搬移函数的过程中，总是可以比较容易地保留旧函数作为转发函数（即旧代码调用旧函数，旧函数再调用新函数）。这样的转发函数通常不会存在太久，但的确能够简化重构过程。

数据就要麻烦得多，因为没办法设计这样的转发机制。如果我把数据搬走，就必须同时修改所有引用该数据的代码，否则程序就不能运行。如果数据的可访问范围很小，比如一个小函数内部的临时变量，那还不成问题。但如果可访问范围变大，重构的难度就会随之增大，这也是说全局数据是大麻烦的原因。所以，如果想要搬移一处被广泛使用的数据，最好的办法往往是先以函数形式封装所有对该数据的访问。这样，我就能把「重新组织数据」的困难任务转化为「重新组织函数」这个相对简单的任务。

封装数据的价值还不止于此。封装能提供一个清晰的观测点，可以由此监控数据的变化和使用情况；我还可以轻松地添加数据被修改时的验证或后续逻辑。我的习惯是：对于所有可变的数据，只要它的作用域超出单个函数，我就会将其封装起来，只允许通过函数访问。数据的作用域越大，封装就越重要。处理遗留代码时，一旦需要修改或增加使用可变数据的代码，我就会借机把这份数据封装起来，从而避免继续加重耦合一份已经广泛使用的数据。

面向对象方法如此强调对象的数据应该保持私有（private），背后也是同样的原理。每当看见一个公开（public）的字段时，我就会考虑使用封装变量（在这种情况下，这个重构手法常被称为封装字段）来缩小其可见范围。一些更激进的观点认为，即便在类内部，也应该通过访问函数来使用字段 —— 这种做法也称为「自封装」。大体而言，我认为自封装有点儿过度了 —— 如果一个类大到需要将字段自封装起来的程度，那么首先应该考虑把这个类拆小。不过，在分拆类之前，自封装字段倒是一个有用的步骤。

封装数据很重要，不过，不可变数据更重要。如果数据不能修改，就根本不需要数据更新前的验证或者其他逻辑钩子。我可以放心地复制数据，而不用搬移原来的数据 —— 这样就不用修改使用旧数据的代码，也不用担心有些代码获得过时失效的数据。不可变性是强大的代码防腐剂。

Now, any attempt to reassign the properties of the default owner will cause an error. Different languages have different techniques to detect or prevent changes like this, so depending on the language I’d consider other options.

Detecting and preventing changes like this is often worthwhile as a temporary measure. I can either remove the changes, or provide suitable mutating functions. Then, once they are all dealt with, I can modify the getting method to return a copy.

So far I’ve talked about copying on getting data, but it may be worthwhile to make a copy in the setter too. That will depend on where the data comes from and whether I need to maintain a link to reflect any changes in that original data. If I don’t need such a link, a copy prevents accidents due to changes on that source data. Taking a copy may be superfluous most of the time, but copies in these cases usually have a negligible effect on performance; on the other hand, if I don’t do them, there is a risk of a long and difficult bout of debugging in the future.

Remember that the copying above, and the class wrapper, both only work one level deep in the record structure. Going deeper requires more levels of copies or object wrapping.

As you can see, encapsulating data is valuable, but often not straightforward. Exactly what to encapsulate—and how to do it—depends on the way the data is being used and the changes I have in mind. But the more widely it’s used, the more it’s worth my attention to encapsulate properly.

现在，如果客户端调用 defaultOwner 函数获得「默认拥有人」数据、再尝试对其属性（即 lastName 和 firstName）重新赋值，赋值不会产生任何效果。对于侦测或阻止修改数据结构内部的数据项，各种编程语言有不同的方式，所以我会根据当下使用的语言来选择具体的办法。「侦测和阻止修改数据结构内部的数据项」通常只是个临时处置。随后我可以去除这些修改逻辑，或者提供适当的修改函数。这些都处理完之后，我就可以修改取值函数，使其返回一份数据副本。

到目前为止，我都在讨论「在取数据时返回一份副本」，其实设值函数也可以返回一份副本。这取决于数据从哪儿来，以及我是否需要保留对源数据的连接，以便知悉源数据的变化。如果不需要这样一条连接，那么设值函数返回一份副本就有好处：可以防止因为源数据发生变化而造成的意外事故。很多时候可能没必要复制一份数据，不过多一次复制对性能的影响通常也都可以忽略不计。但是，如果不做复制，风险则是未来可能会陷入漫长而困难的调试排错过程。

请记住，前面提到的数据复制、类封装等措施，都只在数据记录结构中深入了一层。如果想走得更深入，就需要更多层级的复制或是封装。如你所见，数据封装很有价值，但往往并不简单。到底应该封装什么，以及如何封装，取决于数据被使用的方式，以及我想要修改数据的方式。不过，一言以蔽之，数据被使用得越广，就越是值得花精力给它一个体面的封装。

### 0201. 术语卡——重构

Refactoring (noun): a change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its observable behavior. This definition corresponds to the named refactorings I’ve mentioned in the earlier examples, such as Extract Function (106) and Replace Conditional with Polymorphism (272). 

Refactoring (verb): to restructure software by applying a series of refactorings without changing its observable behavior. 

So I might spend a couple of hours refactoring, during which I would apply a few dozen individual refactorings.

重构（名词）：对软件内部结构的一种调整，目的是在不改变软件可观察行为的前提下，提高其可理解性，降低其修改成本。重构（动词）：使用一系列重构手法，在不改变软件可观察行为的前提下，调整其结构。

书里对重构这个词进行了阐释：重构 !== 更改，尤其是不等于影响函数正常工作的更改。在作者的概念体系里，重构是小步的、不影响函数行为的迭代式更改，嗯，跟敏捷的概念有点像。重构跟性能优化很像：都是修改代码且不影响行为。但前者是为了理解、便于修改；后者是为了性能而改。关于重构和加新功能的配合，作者把它们比喻成两顶帽子 —— 你戴或者不戴，什么时候戴，都随你，但是你要清楚自己戴着哪一顶帽子。

重构的时机，在书中看来，应该是不得不重构时：譬如添加新功能前，重构能让修改更容易；帮助自己理解代码时，重构能让代码更易懂；捡垃圾时，重构可以改掉屎一样的代码（你懂的）。同样，也有不需要重构的时候：比如这段代码凌乱但是跟我无关、也不需要修改或是在某个隐藏得很好的 API 下。又或者重写更容易，那就重写吧。

另外，关于变量命名的经验：作者喜欢把所有返回值变量命名成 result，学到了 —— 这样能一眼就知道变量的作用。以及，因为 JavaScript 是动态类型语言，所以作者喜欢在变量命名里加类型，尤其是加入不定冠词，比如 aPerformance。

### 0202. 术语卡——两顶帽子

Kent Beck came up with a metaphor of the two hats. When I use refactoring to develop software, I divide my time between two distinct activities: adding functionality and refactoring. When I add functionality, I shouldn’t be changing existing code; I’m just adding new capabilities. I measure my progress by adding tests and getting the tests to work. When I refactor, I make a point of not adding functionality; I only restructure the code. I don’t add any tests (unless I find a case I missed earlier); I only change tests when I have to accommodate a change in an interface.

1『测试是与添加新功能匹配的，重构的时候不需要增加新的测试，在老的测试保障下随意重构。』

KentBeck 提出了「两顶帽子」的比喻。使用重构技术开发软件时，我把自己的时间分配给两种截然不同的行为：添加新功能和重构。添加新功能时，我不应该修改既有代码，只管添加新功能。通过添加测试并让测试正常运行，我可以衡量自己的工作进度。重构时我就不能再添加功能，只管调整代码的结构。此时我不应该添加任何测试（除非发现有先前遗漏的东西），只在绝对必要（用以处理接口变化）时才修改测试。

As I develop software, I find myself swapping hats frequently. I start by trying to add a new capability, then I realize this would be much easier if the code were structured differently. So I swap hats and refactor for a while. Once the code is better structured, I swap hats back and add the new capability. Once I get the new capability working, I realize I coded it in a way that’s awkward to understand, so I swap hats again and refactor. All this might take only ten minutes, but during this time I’m always aware of which hat I’m wearing and the subtle difference that makes to how I program.

软件开发过程中，我可能会发现自己经常变换帽子。首先我会尝试添加新功能，然后会意识到：如果把程序结构改一下，功能的添加会容易得多。于是我换一顶帽子，做一会儿重构工作。程序结构调整好后，我又换上原先的帽子，继续添加新功能。新功能正常工作后，我又发现自己的编码造成程序难以理解，于是又换上重构帽子……整个过程或许只花 10 分钟，但无论何时我都清楚自己戴的是哪一顶帽子，并且明白不同的帽子对编程状态提出的不同要求。

### 0203. 术语卡——纯函数（Data Class）

These are classes that have fields, getting and setting methods for the fields, and nothing else. Such classes are dumb data holders and are often being manipulated in far too much detail by other classes. In some stages, these classes may have public fields. If so, you should immediately apply Encapsulate Record (162) before anyone notices. Use Remove Setting Method (331) on any field that should not be changed.

Look for where these getting and setting methods are used by other classes. Try to use Move Function (198) to move behavior into the data class. If you can’t move a whole function, use Extract Function (106) to create a function that can be moved.

Data classes are often a sign of behavior in the wrong place, which means you can make big progress by moving it from the client into the data class itself. But there are exceptions, and one of the best exceptions is a record that’s being used as a result record from a distinct function invocation. A good example of this is the intermediate data structure after you’ve applied Split Phase (154). A key characteristic of such a result record is that it’s immutable (at least in practice). Immutable fields don’t need to be encapsulated and information derived from immutable data can be represented as fields rather than getting methods.

所谓纯数据类是指：它们拥有一些字段，以及用于访问（读写）这些字段的函数，除此之外一无长物。这样的类只是一种不会说话的数据容器，它们几乎一定被其他类过分细琐地操控着。这些类早期可能拥有 public 字段，若果真如此，你应该在别人注意到它们之前，立刻运用封装记录（162）将它们封装起来。对于那些不该被其他类修改的字段，请运用移除设值函数（331）。然后，找出这些取值 / 设值函数被其他类调用的地点。尝试以移函数（198）把那些调用行为搬移到纯数据类里来。如果无法搬移整个函数，就运用提炼函数 (106) 产生一个可被搬移的函数。

纯数据类常常意味着行为被放在了错误的地方。也就是说，只要把处理数据的行为从客户端搬移到纯数据类里来，就能使情况大为改观。但也有例外情况，一个最好的例外情况就是，纯数据记录对象被用作函数调用的返回结果，比如使用拆分阶段（154）之后得到的中转数据结构就是这种情況。这种结果数据对象有一个关键的特征：它是不可修改的（至少在拆分阶段（154）的实际操作中是这样）。不可修改的字段无须封装，使用者可以直接通过字段取得数据，无须通过取值函数。

### 0204. 术语卡——卫语句（Guard Clauses）

I often find that conditional expressions come in two styles. In the first style, both legs of the conditional are part of normal behavior, while in the second style, one leg is normal and the other indicates an unusual condition.

These kinds of conditionals have different intentions—and these intentions should come through in the code. If both are part of normal behavior, I use a condition with an if and an else leg. If the condition is an unusual condition, I check the condition and return if it’s true. This kind of check is often called a guard clause.

The key point of Replace Nested Conditional with Guard Clauses is emphasis. If I’m using an if­then­else construct, I’m giving equal weight to the if leg and the else leg. This communicates to the reader that the legs are equally likely and important. Instead, the guard clause says, “This isn’t the core to this function, and if it happens, do something and get out.”

I often find I use Replace Nested Conditional with Guard Clauses when I’m working with a programmer who has been taught to have only one entry point and one exit point from a method. One entry point is enforced by modern languages, but one exit point is really not a useful rule. Clarity is the key principle: If the method is clearer with one exit point, use one exit point; otherwise don’t.

根据我的经验，条件表达式通常有两种风格。第一种风格是：两个条件分支都属于正常行为。第二种风格则是：只有一个条件分支是正常行为，另一个分支则是异常的情况。

这两类条件表达式有不同的用途，这一点应该通过代码表现出来。如果两条分支都是正常行为，就应该使用形如 if...else... 的条件表达式；如果某个条件极其罕见，就应该单独检查该条件，并在该条件为真时立刻从函数中返回。这样的单独检查常常被称为「卫语句」（guard clauses）。

以卫语句取代嵌套条件表达式的精髓就是：给某一条分支以特别的重视。如果使用 if-then-else 结构，你对 if 分支和 else 分支的重视是同等的。这样的代码结构传递给阅读者的消息就是：各个分支有同样的重要性。卫语句就不同了，它告诉阅读者：「这种情况不是本函数的核心逻辑所关心的，如果它真发生了，请做一些必要的整理工作，然后退出。」

「每个函数只能有一个入口和一个出口」的观念，根深蒂固于某些程序员的脑海里。我发现，当我处理他们编写的代码时，经常需要使用以卫语句取代嵌套条件表达式。现今的编程语言都会强制保证每个函数只有一个入口，至于「单一出口」规则，其实不是那么有用。在我看来，保持代码清晰才是最关键的：如果单一出口能使这个函数更清楚易读，那么就使用单一出口；否则就不必这么做。

### 0301. 人名卡——Martin Fowler

人名卡：Martin Fowler

印象：本书作者，大师中的大师。

### 0401. 金句卡——for each desired change, make the change easy, then make the easy change

for each desired change, make the change easy (warning: this may be hard), then make the easy change. ——Kent Beck

每次要修改时，首先令修改很容易（警告：这件事有时会很难），然后再进行这次容易的修改。

### 0402. 金句卡——Make sure all tests are fully automatic and that they check their own results

用测试框架来实现测试的「自动化」，比如 JS 里用 jasmine 框架。

### 0403. 金句卡——Always make sure a test will fail when it should

总是确保测试不该通过时真的会失败。一定要先自己写一个错误的测试，此时终于明白这个概念了（2020-06-17）。

When I write a test against existing code like this, it’s nice to see that all is well—but I’m naturally skeptical. Particularly, once I have a lot of tests running, I’m always nervous that a test isn’t really exercising the code the way I think it is, and thus won’t catch a bug when I need it to. So I like to see every test fail at least once when I write it. My favorite way of doing that is to temporarily inject a fault into the code, for example:

### 0404. 金句卡——Think of the boundary conditions under which things might go wrong and concentrate your tests there

考虑可能出错的边界条件，把测试火力集中在那儿。

At this point, I may start to wonder if a negative demand resulting in a negative profit really makes any sense for the domain. Shouldn’t the minimum demand be zero? In which case, perhaps, the setter should react differently to a negative argument—raising an error or setting the value to zero anyway. These are good questions to ask, and writing tests like this helps me think about how the code ought to react to boundary cases.

通过写「测试」，比如把 demand 设为负值，引发思考，负值在该业务领域里代表什么？边界是 0 么？出现负值时该如何处理，即在代码里写「异常处理逻辑」。总之，测试可以作为开发时触发自己思考的钩子，「测试驱动开发」嘛。（2020-06-17）

### 0501. 任意卡——重构时机三原则

Here’s a guideline Don Roberts gave me: The first time you do something, you just do it. The second time you do something similar, you wince at the duplication, but you do the duplicate thing anyway. The third time you do something similar, you refactor. Or for those who like baseball: Three strikes, then you refactor.

Don Roberts 给了我一条准则：第一次做某件事时只管去做；第二次做类似的事会产生反感，但无论如何还是可以去做；第三次再做类似的事，你就应该重构。正如老话说的：事不过三，三则重构。

具体的几个重构时间节点如下。

1、预备性重构。重构的最佳时机就在添加新功能之前。在动手添加新功能之前，我会看看现有的代码库，此时经常会发现：如果对代码结构做一点微调，我的工作会容易得多。也许已经有个函数提供了我需要的大部分功能，但有几个字面量的值与我的需要略有冲突。如果不做重构，我可能会把整个函数复制过来，修改这几个值，但这就会导致重复代码——如果将来我需要做修改，就必须同时修改两处（更麻烦的是，我得先找到这两处）。而且，如果将来我还需要一个类似又略有不同的功能，就只能再复制粘贴一次，这可不是个好主意。所以我戴上重构的帽子，使用函数参数化（310）。做完这件事以后，接下来我就只需要调用这个函数，传入我需要的参数。

2、帮助理解的重构。我需要先理解代码在做什么，然后才能着手修改。这段代码可能是我写的，也可能是别人写的。一旦我需要思考「这段代码到底在做什么」，我就会自问：能不能重构这段代码，令其一目了然？我可能看见了一段结构糟糕的条件逻辑，也可能希望复用一个函数，但花费了几分钟才弄懂它到底在做什么，因为它的函数命名实在是太糟糕了。这些都是重构的机会。看代码时，我会在脑海里形成一些理解，但我的记性不好，记不住那么多细节。正如 Ward Cunningham 所说，通过重构，我就把脑子里的理解转移到了代码本身。随后我运行这个软件，看它是否正常工作，来检查这些理解是否正确。如果把对代码的理解植入代码中，这份知识会保存得更久，并且我的同事也能看到。

重构带来的帮助不仅发生在将来——常常是立竿见影。我会先在一些小细节上使用重构来帮助理解，给一两个变量改名，让它们更清楚地表达意图，以方便理解，或是将一个长函数拆成几个小函数。当代码变得更清晰一些时，我就会看见之前看不见的设计问题。如果不做前面的重构，我可能永远都看不见这些设计问题，因为我不够聪明，无法在脑海中推演所有这些变化。Ralph Johnson 说，这些初步的重构就像扫去窗上的尘埃，使我们得以看到窗外的风景。在研读代码时，重构会引领我获得更高层面的理解，如果只是阅读代码很难有此领悟。有些人以为这些重构只是毫无意义地把玩代码，他们没有意识到，缺少了这些细微的整理，他们就无法看到隐藏在一片混乱背后的机遇。

3、捡垃圾式重构。帮助理解的重构还有一个变体：我已经理解代码在做什么，但发现它做得不好，例如逻辑不必要地迂回复杂，或者两个函数几乎完全相同，可以用一个参数化的函数取而代之。这里有一个取舍：我不想从眼下正要完成的任务上跑题太多，但我也不想把垃圾留在原地，给将来的修改增加麻烦。如果我发现的垃圾很容易重构，我会马上重构它；如果重构需要花一些精力，我可能会拿一张便笺纸把它记下来，完成当下的任务再回来重构它。当然，有时这样的垃圾需要好几个小时才能解决，而我又有更紧急的事要完成。不过即便如此，稍微花一点工夫做一点儿清理，通常都是值得的。正如野营者的老话所说：至少要让营地比你到达时更干净。如果每次经过这段代码时都把它变好一点点，积少成多，垃圾总会被处理干净。重构的妙处就在于，每个小步骤都不会破坏代码——所以，有时一块垃圾在好几个月之后才终于清理干净，但即便每次清理并不完整，代码也不会被破坏。

4、长期重构。大多数重构可以在几分钟——最多几小时——内完成。但有一些大型的重构可能要花上几个星期，例如要替换一个正在使用的库，或者将整块代码抽取到一个组件中并共享给另一支团队使用，再或者要处理一大堆混乱的依赖关系，等等。即便在这样的情况下，我仍然不愿让一支团队专门做重构。可以让整个团队达成共识，在未来几周时间里逐步解决这个问题，这经常是一个有效的策略。每当有人靠近「重构区」的代码，就把它朝想要改进的方向推动一点。这个策略的好处在于，重构不会破坏代码——每次小改动之后，整个系统仍然照常工作。例如，如果想替换掉一个正在使用的库，可以先引入一层新的抽象，使其兼容新旧两个库的接口。一旦调用方已经完全改为使用这层抽象，替换下面的库就会容易得多。（这个策略叫作 Branch By Abstraction [mf-bba]。）

3『之前就曾听说过，编程里的难题绝大多数可以通过引入一个「中间层」抽象来解决。』

5、code review 的时候。我发现，重构可以帮助我复审别人的代码。开始重构前我可以先阅读代码，得到一定程度的理解，并提出一些建议。一旦想到一些点子，我就会考虑是否可以通过重构立即轻松地实现它们。如果可以，我就会动手。这样做了几次以后，我可以更清楚地看到，当我的建议被实施以后，代码会是什么样。我不必想象代码应该是什么样，我可以真实看见。于是我可以获得更高层次的认识。如果不进行重构，我永远无法得到这样的认识。重构还可以帮助代码复审工作得到更具体的结果。不仅获得建议，而且其中许多建议能够立刻实现。最终你将从实践中得到比以往多得多的成就感。至于如何在代码复审的过程中加入重构，这要取决于复审的形式。在常见的 pull request 模式下，复审者独自浏览代码，代码的作者不在旁边，此时进行重构效果并不好。如果代码的原作者在旁边会好很多，因为作者能提供关于代码的上下文信息，并且充分认同复审者进行修改的意图。对我个人而言，与原作者肩并肩坐在一起，一边浏览代码一边重构，体验是最佳的。这种工作方式很自然地导向结对编程：在编程的过程中持续不断地进行代码复审。

### 0502. 任意卡——两个不需要重构的场景

If I run across code that is a mess, but I don’t need to modify it, then I don’t need to refactor it. Some ugly code that I can treat as an API may remain ugly. It’s only when I need to understand how it works that refactoring gives me any benefit. Another case is when it’s easier to rewrite it than to refactor it. This is a tricky decision. Often, I can’t tell how easy it is to refactor some code unless I spend some time trying and thus get a sense of how difficult it is. The decision to refactor or rewrite requires good judgment and experience, and I can’t really boil it down into a piece of simple advice.

如果我看见一块凌乱的代码，但并不需要修改它，那么我就不需要重构它。如果丑陋的代码能被隐藏在一个 API 之下，我就可以容忍它继续保持丑陋。只有当我需要理解其工作原理时，对其进行重构才有价值。另一种情况是，如果重写比重构还容易，就别重构了。这是个困难的决定。如果不花一点儿时间尝试，往往很难真实了解重构一块代码的难度。决定到底应该重构还是重写，需要良好的判断力与丰富的经验，我无法给出一条简单的建议。

### 0503. 任意卡——集成是一个双向过程

There are downsides to feature branches like this. The longer I work on an isolated branch, the harder the job of integrating my work with mainline is going to be when I’m done. Most people reduce this pain by frequently merging or re­basing from mainline to my branch. But this doesn’t really solve the problem when several people are working on individual feature branches. I distinguish between merging and integration. If I merge mainline into my code, this is a one-way movement—my branch changes but the mainline doesn’t. I use “integrate” to mean a two­-way process that pulls changes from mainline into my branch and then pushes the result back into mainline, changing both. If Rachel is working on her branch I don’t see her changes until she integrates with mainline; at that point, I have to merge her changes into my feature branch, which may mean considerable work. The hard part of this work is dealing with semantic changes. Modern version control systems can do wonders with merging complex changes to the program text, but they are blind to the semantics of the code. If I’ve changed the name of a function, my version control tool may easily integrate my changes with Rachel’s. But if, in her branch, she added a call to a function that I’ve renamed in mine, the code will fail.

这样的特性分支有其缺点。在隔离的分支上工作得越久，将完成的工作集成（integrate）回主线就会越困难。为了减轻集成的痛苦，大多数人的办法是频繁地从主线合并（merge）或者变基（rebase）到分支。但如果有几个人同时在各自的特性分支上工作，这个办法并不能真正解决问题，因为合并与集成是两回事。如果我从主线合并到我的分支，这只是一个单向的代码移动——我的分支发生了修改，但主线并没有。而「集成」是一个双向的过程：不仅要把主线的修改拉（pull）到我的分支上，而且要把我这里修改的结果推（push）回到主线上，两边都会发生修改。假如另一名程序员 Rachel 正在她的分支上开发，我是看不见她的修改的，直到她将自己的修改与主线集成；此时我就必须把她的修改合并到我的特性分支，这可能需要相当的工作量。其中困难的部分是处理语义变化。现代版本控制系统都能很好地合并程序文本的复杂修改，但对于代码的语义它们一无所知。如果我修改了一个函数的名字，版本控制工具可以很轻松地将我的修改与 Rachel 的代码集成。但如果在集成之前，她在自己的分支里新添调用了这个被我改名的函数，集成之后的代码就会被破坏。

### 0504. 任意卡——添加新功能前先写测试的理解

好像抓到一块大大的金子。在添加新功能之前就先写测试的代码（测试接口），比如 JS 的 jasmine 的 describe()，先在测试工具里实现想要的功能，这个时候你反而关注接口而非实现，这个阶段就是 TDD 大三阶段「红 -> 绿 -> 橙」中的红，接着在源码里去写实现代码进入「绿」的阶段，然后再通过「重构」进入「橙」阶段。

Admittedly, it is not so easy to persuade others to follow this route. Writing the tests means a lot of extra code to write. Unless you have actually experienced how it speeds programming, self­testing does not seem to make sense. This is not helped by the fact that many people have never learned to write tests or even to think about tests. When tests are manual, they are gut­wrenchingly boring. But when they are automatic, tests can actually be quite fun to write. In fact, one of the most useful times to write tests is before I start programming. When I need to add a feature, I begin by writing the test. This isn’t as backward as it sounds. By writing the test, I’m asking myself what needs to be done to add the function. Writing the test also concentrates me on the interface rather than the implementation (always a good thing). It also means I have a clear point at which I’m done coding when the test works.

### 0505. 任意卡——测试框架里跑测试的频次

Run tests frequently. Run those exercising the code you’re working on at least every few minutes; run all tests at least daily. 

频繁地运行测试。对于你正在处理的代码，与其对应的测试至少每隔几分钟就要运行一次，每天至少运行一次所有的测试。

In a real system, I might have thousands of tests. A good test framework allows me to run them easily and to quickly see if any have failed. This simple feedback is essential to self-­testing code. When I work, I’ll be running tests very frequently—checking progress with new code or checking for mistakes with refactoring.

### 0506. 任意卡——范围类

这项重构手法到这儿就完成了。不过，将一堆参数替换成一个真正的对象，这只是长征第一步。创建一个类是为了把行为搬移进去。在这里，我可以给「范围」类添加一个函数，用于测试一个值是否落在范围之内。

```js
function readingsOutsideRange(station, range) { 　
  return station.readings　　
    .filter(r => !range.contains(r.temp));
}
```

class NumberRange…

```js
class NumberRange { 　
  constructor(min, max) {　　
    this._data = {min: min, max: max};　
  }　
  get min() {return this._data.min;} 　
  get max() {return this._data.max;}
  contains(arg) {return (arg >= this.min && arg <= this.max);}
}  
```

This is a first step to creating a range [mf­range] that can take on a lot of useful behavior. Once I’ve identified the need for a range in my code, I can be constantly on the lookout for other cases where I see a max/min pair of numbers and replace them with a range. (One immediate possibility is the operating plan, replacing temperatureFloor and temperatureCeiling with a temperatureRange.) As I look at how these pairs are used, I can move more useful behavior into the range class, simplifying its usage across the code base. One of the first things I may add is a valuebased equality method to make it a true value object.

这样我就迈出了第一步，开始逐渐打造一个真正有用的「范围」[mf-range] 类。一旦识别出「范围」这个概念，那么每当我在代码中发现「最大/最小值」这样一对数字时，我就会考虑是否可以将其改为使用「范围」类。（例如，我马上就会考虑把「运作计划」类中的 temperatureFloor 和 temperatureCeiling 替换为 temperatureRange。）在观察这些成对出现的数字如何被使用时，我会发现一些有用的行为，并将其搬移到「范围」类中，简化其使用方法。比如，我可能会先给这个类加上「基于数值判断相等性」的函数，使其成为一个真正的对象。

## 重构汇总

### 01. 提炼-内联相关

#### 1.1 提炼函数

```js
function printOwing(invoice) {　
  printBanner();　
  let outstanding = calculateOutstanding();　
  //print details　
  console.log(`name: ${invoice.customer}`);　
  console.log(`amount: ${outstanding}`);
}
```

After Refactoring:

```js
function printOwing(invoice) {　
  printBanner();　
  let outstanding = calculateOutstanding();　
  printDetails(outstanding);　
  
  function printDetails(outstanding) {　　
    console.log(`name: ${invoice.customer}`);　　
    console.log(`amount: ${outstanding}`);　
  }
}
```

1 Create a new function, and name it after the intent of the function (name it by what it does, not by how it does it).

If the code I want to extract is very simple, such as a single function call, I still extract it if the name of the new function will reveal the intent of the code in a better way. If I can’t come up with a more meaningful name, that’s a sign that I shouldn’t extract the code. However, I don’t have to come up with the best name right away; sometimes a good name only appears as I work with the extraction. It’s OK to extract a function, try to work with it, realize it isn’t helping, and then inline it back again. As long as I’ve learned something, my time wasn’t wasted.

If the language supports nested functions, nest the extracted function inside the source function. That will reduce the amount of out­of­scope variables to deal with after the next couple of steps. I can always use Move Function (198) later. 

2 Copy the extracted code from the source function into the new target function.

3 Scan the extracted code for references to any variables that are local in scope to the source function and will not be in scope for the extracted function. Pass them as parameters. If I extract into a nested function of the source function, I don’t run into these problems. Usually, these are local variables and parameters to the function. The most general approach is to pass all such parameters in as arguments. There are usually no difficulties for variables that are used but not assigned to.

If a variable is only used inside the extracted code but is declared outside, move the declaration into the extracted code. Any variables that are assigned to need more care if they are passed by value. If there’s only one of them, I try to treat the extracted code as a query and assign the result to the variable concerned.

Sometimes, I find that too many local variables are being assigned by the extracted code. It’s better to abandon the extraction at this point. When this happens, I consider other refactorings such as Split Variable (240) or Replace Temp with Query (178) to simplify variable usage and revisit the extraction later.

4 Compile after all variables are dealt with. Once all the variables are dealt with, it can be useful to compile if the language environment does compile­time checks. Often, this will help find any variables that haven’t been dealt with properly.

5 Replace the extracted code in the source function with a call to the target function.

6 Test.

7 Look for other code that’s the same or similar to the code just extracted, and consider using Replace Inline Code with Function Call (222) to call the new function. Some refactoring tools support this directly. Otherwise, it can be worth doing some quick searches to see if duplicate code exists elsewhere.

1、创造一个新函数，根据这个函数的意图来对它命名（以它「做什么」来命名，而不是以它「怎样做」命名）。如果想要提炼的代码非常简单，例如只是一个函数调用，只要新函数的名称能够以更好的方式昭示代码意图，我还是会提炼它；但如果想不出一个更有意义的名称，这就是一个信号，可能我不应该提炼这块代码。不过，我不一定非得马上想出最好的名字，有时在提炼的过程中好的名字才会出现。有时我会提炼一个函数，尝试使用它，然后发现不太合适，再把它内联回去，这完全没问题。只要在这个过程中学到了东西，我的时间就没有白费。如果编程语言支持嵌套函数，就把新函数嵌套在源函数里，这能减少后面需要处理的超出作用域的变量个数。我可以稍后再使用搬移函数（198）把它从源函数中搬移出去。

2、将待提炼的代码从源函数复制到新建的目标函数中。

3、仔细检查提炼出的代码，看看其中是否引用了作用域限于源函数、在提炼出的新函数中访问不到的变量。若是，以参数的形式将它们传递给新函数。如果提炼出的新函数嵌套在源函数内部，就不存在变量作用域的问题了。这些「作用域限于源函数」的变量通常是局部变量或者源函数的参数。最通用的做法是将它们都作为参数传递给新函数。只要没在提炼部分对这些变量赋值，处理起来就没什么难度。

如果某个变量是在提炼部分之外声明但只在提炼部分被使用，就把变量声明也搬移到提炼部分代码中去。如果变量按值传递给提炼部分又在提炼部分被赋值，就必须多加小心。如果只有一个这样的变量，我会尝试将提炼出的新函数变成一个查询（query），用其返回值给该变量赋值。但有时在提炼部分被赋值的局部变量太多，这时最好是先放弃提炼。这种情况下，我会考虑先使用别的重构手法，例如拆分变量（240）或者以查询取代临时变量（178），来简化变量的使用情况，然后再考虑提炼函数。

4、所有变量都处理完之后，编译。如果编程语言支持编译期检查的话，在处理完所有变量之后做一次编译是很有用的，编译器经常会帮你找到没有被恰当处理的变量。

5、在源函数中，将被提炼代码段替换为对目标函数的调用。

6、测试。

7、查看其他代码是否有与被提炼的代码段相同或相似之处。如果有，考虑使用以函数调用取代内联代码（222）令其调用提炼出的新函数。有些重构工具直接支持这一步。如果工具不支持，可以快速搜索一下，看看别处是否还有重复代码。

#### 1.2 内联函数

```js
function getRating(driver) {　
  return moreThanFiveLateDeliveries(driver) ? 2 : 1;
}

function moreThanFiveLateDeliveries(driver) {　
  return driver.numberOfLateDeliveries > 5;
}
```

After Refactoring:

```js
function getRating(driver) {　
  return (driver.numberOfLateDeliveries > 5) ? 2 : 1;
}
```

1 Check that this isn’t a polymorphic method. If this is a method in a class, and has subclasses that override it, then I can’t inline it. Find all the callers of the function.

2 Replace each call with the function’s body.

3 Test after each replacement.

4 The entire inlining doesn’t have to be done all at once. If some parts of the inline are tricky, they can be done gradually as opportunity permits.

5 Remove the function definition.

Written this way, Inline Function is simple. In general, it isn’t. I could write pages on how to handle recursion, multiple return points, inlining a method into another object when you don’t have accessors, and the like. The reason I don’t is that if you encounter these complexities, you shouldn’t do this refactoring.

1、检查函数，确定它不具多态性。如果该函数属于一个类，并且有子类继承了这个函数，那么就无法内联。

2、找出这个函数的所有调用点。

3、将这个函数的所有调用点都替换为函数本体。

4、每次替换之后，执行测试。不必一次完成整个内联操作。如果某些调用点比较难以内联，可以等到时机成熟后再来处理。

5、删除该函数的定义。

被我这样一写，内联函数似乎很简单。但情况往往并非如此。对于递归调用、多返回点、内联至另一个对象中而该对象并无访问函数等复杂情况，我可以写上好几页。我之所以不写这些特殊情况，原因很简单：如果你遇到了这样的复杂情况，就不应该使用这个重构手法。

#### 1.3 提炼变量

```js
return order.quantity * order.itemPrice -　
  Math.max(0, order.quantity - 500) * order.itemPrice * 0.05 +　
  Math.min(order.quantity * order.itemPrice * 0.1, 100);
```

After Reactoring:

```js
const basePrice = order.quantity * order.itemPrice;
const quantityDiscount = Math.max(0, order.quantity - 500) * order.itemPrice * 0.05;
const shipping = Math.min(basePrice * 0.1, 100);
return basePrice - quantityDiscount + shipping;
```

1 Ensure that the expression you want to extract does not have side effects. 

2 Declare an immutable variable. Set it to a copy of the expression you want to name.

3 Replace the original expression with the new variable.

4 Test.

If the expression appears more than once, replace each occurrence with the variable, testing after each replacement.

1、确认要提炼的表达式没有副作用。

2、声明一个不可修改的变量，把你想要提炼的表达式复制一份，以该表达式的结果值给这个变量赋值。

3、用这个新变量取代原来的表达式。

4、测试。

如果该表达式出现了多次，请用这个新变量逐一替换，每次替换之后都要执行测试。

#### 1.4 内联变量

```js
let basePrice = anOrder.basePrice;
return (basePrice > 1000);
```

After Refactoring:

```js
return anOrder.basePrice > 1000;
```

1 Check that the right­hand side of the assignment is free of side effects.

2 If the variable isn’t already declared immutable, do so and test.

3 This checks that it’s only assigned to once. Find the first reference to the variable and replace it with the right­hand side of the assignment.

4 Test.

5 Repeat replacing references to the variable until you’ve replaced all of them. 

6 Remove the declaration and assignment of the variable.

7 Test.

1、检查确认变量赋值语句的右侧表达式没有副作用。

2、如果变量没有被声明为不可修改，先将其变为不可修改，并执行测试。这是为了确保该变量只被赋值一次。

3、找到第一处使用该变量的地方，将其替换为直接使用赋值语句的右侧表达式。

4、测试。

5、重复前面两步，逐一替换其他所有使用该变量的地方。

6、删除该变量的声明点和赋值语句。

7、测试。

#### 1.5 改变函数声明

```js
function circum(radius) {...}
```

After Reactoring:

```js
function circumference(radius) {...}
```

#### Simple Mechanics

1 If you’re removing a parameter, ensure it isn’t referenced in the body of the function.

2 Change the method declaration to the desired declaration.

3 Find all references to the old method declaration, update them to the new one.

4 Test.

It’s often best to separate changes, so if you want to both change the name and add a parameter, do these as separate steps. (In any case, if you run into trouble, revert and use the migration mechanics instead.)

1、如果想要移除一个参数，需要先确定函数体内没有使用该参数。

2、修改函数声明，使其成为你期望的状态。

3、找出所有使用旧的函数声明的地方，将它们改为使用新的函数声明。

4、测试。

最好能把大的修改拆成小的步骤，所以如果你既想修改函数名，又想添加参数，最好分成两步来做。（并且，不论何时，如果遇到了麻烦，请撤销修改，并改用迁移式做法。）

#### Migration Mechanics

1 If necessary, refactor the body of the function to make it easy to do the following extraction step. Use Extract Function (106) on the function body to create the new function.

2 If the new function will have the same name as the old one, give the new function a temporary name that’s easy to search for.

3 If the extracted function needs additional parameters, use the simple mechanics to add them.

4 Test.

5 Apply Inline Function (115) to the old function.

6 If you used a temporary name, use Change Function Declaration (124) again to restore it to the original name.

7 Test.

If you’re changing a method on a class with polymorphism, you’ll need to add indirection for each binding. If the method is polymorphic within a single class hierarchy, you only need the forwarding method on the superclass. If the polymorphism has no superclass link, then you’ll need forwarding methods on each implementation class.

If you are refactoring a published API, you can pause the refactoring once you’ve created the new function. During this pause, deprecate the original function and wait for clients to change to the new function. The original function declaration can be removed when (and if) you’re confident all the clients of the old function have migrated to the new one.

1、如果有必要的话，先对函数体内部加以重构，使后面的提炼步骤易于开展。

2、使用提炼函数（106）将函数体提炼成一个新函数。如果你打算沿用旧函数的名字，可以先给新函数起一个易于搜索的临时名字。

3、如果提炼出的函数需要新增参数，用前面的简单做法添加即可。

4、测试。

5、对旧函数使用内联函数（115）。

6、如果新函数使用了临时的名字，再次使用改变函数声明（124）将其改回原来的名字。

7、测试。

如果要重构的函数属于一个具有多态性的类，那么对于该函数的每个实现版本，你都需要通过「提炼出一个新函数」的方式添加一层间接，并把旧函数的调用转发给新函数。如果该函数的多态性是在一个类继承体系中体现，那么只需要在超类上转发即可；如果各个实现类之间并没有一个共同的超类，那么就需要在每个实现类上做转发。

如果要重构一个已对外发布的 API，在提炼出新函数之后，你可以暂停重构，将原来的函数声明为「不推荐使用」（deprecated），然后给客户端一点时间转为使用新函数。等你有信心所有客户端都已经从旧函数迁移到新函数，再移除旧函数的声明。

#### 1.6 封装变量

```js
let defaultOwner = {firstName: "Martin", lastName: "Fowler"};
```

After Refactoring:

```js
let defaultOwnerData = {firstName: "Martin", lastName: "Fowler"};

export function defaultOwner() {
  return defaultOwnerData;
}

export function setDefaultOwner(arg) {
  defaultOwnerData = arg;
}
```

1 Create encapsulating functions to access and update the variable.

2 Run static checks.

3 For each reference to the variable, replace with a call to the appropriate encapsulating function. Test after each replacement.

4 Restrict the visibility of the variable.

5 Sometimes it’s not possible to prevent access to the variable. If so, it may be useful to detect any remaining references by renaming the variable and testing.

6 Test.

7 If the value of the variable is a record, consider Encapsulate Record (162).

1、创建封装函数，在其中访问和更新变量值。

2、执行静态检查。

3、逐一修改使用该变量的代码，将其改为调用合适的封装函数。每次替换之后，执行测试。

4、限制变量的可见性。有时没办法阻止直接访问变量。若果真如此，可以试试将变量改名，再执行测试，找出仍在直接使用该变量的代码。

5、测试。

6、如果变量的值是一个记录，考虑使用封装记录（162）。

#### 1.7 变量改名

```js
let a = height * width;
```

After Refactoring:

```js
let area = height * width;
```

1 If the variable is used widely, consider Encapsulate Variable (132).

2 Find all references to the variable, and change every one. If there are references from another code base, the variable is a published variable, and you cannot do this refactoring. If the variable does not change, you can copy it to one with the new name, then change gradually, testing after each change.

3 Test.

1、如果变量被广泛使用，考虑运用封装变量（132）将其封装起来。

2、找出所有使用该变量的代码，逐一修改。如果在另一个代码库中使用了该变量，这就是一个「已发布变量」（published variable），此时不能进行这个重构。如果变量值从不修改，可以将其复制到一个新名字之下，然后逐一修改使用代码，每次修改后执行测试。

3、测试。

#### 1.8 引入参数对象

```js
function amountInvoiced(startDate, endDate) {...} 
function amountReceived(startDate, endDate) {...} 
function amountOverdue(startDate, endDate) {...}
```

After Refactoring:

```js
function amountInvoiced(aDateRange) {...} 
function amountReceived(aDateRange) {...} 
function amountOverdue(aDateRange) {...}
```

1 If there isn’t a suitable structure already, create one. I prefer to use a class, as that makes it easier to group behavior later on. I usually like to ensure these structures are value objects [mf­vo].

2 Test. 

3 Use Change Function Declaration (124) to add a parameter for the new structure.

4 Test.

5 Adjust each caller to pass in the correct instance of the new structure. Test after each one.

6 For each element of the new structure, replace the use of the original parameter with the element of the structure. Remove the parameter. Test.

1、如果暂时还没有一个合适的数据结构，就创建一个。我倾向于使用类，因为稍后把行为放进来会比较容易。我通常会尽量确保这些新建的数据结构是值对象 [mf-vo]。

2、测试。

3、使用改变函数声明（124）给原来的函数新增一个参数，类型是新建的数据结构。

4、测试。

5、调整所有调用者，传入新数据结构的适当实例。每修改一处，执行测试。

6、用新数据结构中的每项元素，逐一取代参数列表中与之对应的参数项，然后删除原来的参数。测试。

#### 1.9 函数组合成类

```js
function base(aReading) {...}
function taxableCharge(aReading) {...} 
function calculateBaseCharge(aReading) {...}
```

After Refactoring:

```js
class Reading {   
  base() {...}  
  taxableCharge() {...}   
  calculateBaseCharge() {...}
}
```

1 Apply Encapsulate Record (162) to the common data record that the functions share. If the data that is common between the functions isn’t already grouped into a record structure, use Introduce Parameter Object (140) to create a record to group it together.

2 Take each function that uses the common record and use Move Function (198) to move it into the new class. Any arguments to the function call that are members can be removed from the argument list.

3 Each bit of logic that manipulates the data can be extracted with Extract Function (106) and then moved into the new class.

1、运用封装记录（162）对多个函数共用的数据记录加以封装。如果多个函数共用的数据还未组织成记录结构，则先运用引入参数对象（140）将其组织成记录。

2、对于使用该记录结构的每个函数，运用搬移函数（198）将其移入新类。如果函数调用时传入的参数已经是新类的成员，则从参数列表中去除之。

3、用以处理该数据记录的逻辑可以用提炼函数（106）提炼出来，并移入新类。

#### 1.10 函数组合成变换

```js
function base(aReading) {...}
function taxableCharge(aReading) {...}
```

After Refactoring:

```js
function enrichReading(argReading) {  
  const aReading = _.cloneDeep(argReading);  
  aReading.baseCharge = base(aReading);  
  aReading.taxableCharge = taxableCharge(aReading);  
  return aReading;
}
```

1 Create a transformation function that takes the record to be transformed and returns the same values. This will usually involve a deep copy of the record. It is often worthwhile to write a test to ensure the transform does not alter the original record.

2 Pick some logic and move its body into the transform to create a new field in the record. Change the client code to access the new field. If the logic is complex, use Extract Function (106) first.

3 Test.

4 Repeat for the other relevant functions.

1、创建一个变换函数，输入参数是需要变换的记录，并直接返回该记录的值。这一步通常需要对输入的记录做深复制（deep copy）。此时应该写个测试，确保变换不会修改原来的记录。

2、挑选一块逻辑，将其主体移入变换函数中，把结果作为字段添加到输出记录中。修改客户端代码，令其使用这个新字段。如果计算逻辑比较复杂，先用提炼函数（106）提炼之。

3、测试。

4、针对其他相关的计算逻辑，重复上述步骤。

#### 1.11 拆分阶段

```js
const orderData = orderString.split(/\s+/);
const productPrice = priceList[orderData[0].split("-")[1]]; 
const orderPrice = parseInt(orderData[1]) * productPrice;
```

After Refactoring:

```js
const orderRecord = parseOrder(order);
const orderPrice = price(orderRecord, priceList);

function parseOrder(aString) {　
  const values = aString.split(/\s+/); 　
  return ({　　
    productID: values[0].split("-")[1], 　　
    quantity: parseInt(values[1]),　
  });
}
  
function price(order, priceList) {　
  return order.quantity * priceList[order.productID];
}
```

1 Extract the second phase code into its own function.

2 Test.

3 Introduce an intermediate data structure as an additional argument to the extracted function.

4 Test.

5 Examine each parameter of the extracted second phase. If it is used by first phase, move it to the intermediate data structure. Test after each move.

6 Sometimes, a parameter should not be used by the second phase. In this case, extract the results of each usage of the parameter into a field of the intermediate data structure and use Move Statements to Callers (217) on the line that populates it. 

7 Apply Extract Function (106) on the first­phase code, returning the intermediate data structure. It’s also reasonable to extract the first phase into a transformer object.

1、将第二阶段的代码提炼成独立的函数。

2、测试。

3、引入一个中转数据结构，将其作为参数添加到提炼出的新函数的参数列表中。

4、测试。

5、逐一检查提炼出的「第二阶段函数」的每个参数。如果某个参数被第一阶段用到，就将其移入中转数据结构。每次搬移之后都要执行测试。有时第二阶段根本不应该使用某个参数。果真如此，就把使用该参数得到的结果全都提炼成中转数据结构的字段，然后用搬移语句到调用者（217）把使用该参数的代码行搬移到「第二阶段函数」之外。

6、对第一阶段的代码运用提炼函数（106），让提炼出的函数返回中转数据结构。也可以把第一阶段提炼成一个变换（transform）对象。

### 02. 条件逻辑相关

#### 2.1 分解条件表达式

```js
if (!aDate.isBefore(plan.summerStart) && !aDate.isAfter(plan.summerEnd)) 　
  charge = quantity * plan.summerRate;
else　
  charge = quantity * plan.regularRate + plan.regularServiceCharge;
```

After refactoring:

```js
if (summer())　
  charge = summerCharge();
else　
  charge = regularCharge();
```

Apply Extract Function (106) on the condition and each leg of the conditional.

对条件判断和每个条件分支分别运用提炼函数（106）手法。

#### 2.2 合并条件表达式

```js
if (anEmployee.seniority < 2) return 0;
if (anEmployee.monthsDisabled > 12) return 0;
if (anEmployee.isPartTime) return 0
```

After refactoring:

```js
if (isNotEligibleForDisability()) return 0; 
function isNotEligibleForDisability() {　
  return ((anEmployee.seniority < 2)　　　　　
          || (anEmployee.monthsDisabled > 12)　　　　　
          || (anEmployee.isPartTime));
}
```

1 Ensure that none of the conditionals have any side effects. If any do, use Separate Query from Modifier (306) on them first.

2 Take two of the conditional statements and combine their conditions using a logical operator. Sequences combine with or, nested if statements combine with and.

3 Test.

4 Repeat combining conditionals until they are all in a single condition.

5 Consider using Extract Function (106) on the resulting condition.

1、确定这些条件表达式都没有副作用。如果某个条件表达式有副作用，可以先用将查询函数和修改函数分离（306）处理。

2、使用适当的逻辑运算符，将两个相关条件表达式合并为一个。顺序执行的条件表达式用逻辑或来合并，嵌套的 if 语句用逻辑与来合并。

3、测试。

4、重复前面的合并过程，直到所有相关的条件表达式都合并到一起。

5、可以考虑对合并后的条件表达式实施提炼函数（106）。

#### 2.3 以卫语句取代嵌套条件表达式

```js
function getPayAmount() { 　
  let result;　
  if (isDead)　　
    result = deadAmount(); 　
  else {　　
    if (isSeparated)　　　
      result = separatedAmount(); 　　
    else {　　　
      if (isRetired)　　　　
        result = retiredAmount(); 　　　
      else　　　　
        result = normalPayAmount();　　
    }　
  }　
  return result;
}
```

After refactoring:

```js
function getPayAmount() {　
  if (isDead) return deadAmount();　
  if (isSeparated) return separatedAmount(); 　
  if (isRetired) return retiredAmount(); 　
  return normalPayAmount();
}
```

1 Select outermost condition that needs to be replaced, and change it into a guard clause.

2 Test.

3 Repeat as needed.

4 If all the guard clauses return the same result, use Consolidate Conditional Expression (263).

1、选中最外层需要被替换的条件逻辑，将其替换为卫语句。

2、测试。

3、有需要的话，重复上述步骤。

4、如果所有卫语句都引发同样的结果，可以使用合并条件表达式（263）合并之。

#### 2.4 以多态取代条件表达式

```js
switch (bird.type) {　
  case 'EuropeanSwallow': 　　
    return "average";　
  case 'AfricanSwallow':　　
    return (bird.numberOfCoconuts > 2) ? "tired" : "average"; 　
  case 'NorwegianBlueParrot':　　
    return (bird.voltage > 100) ? "scorched" : "beautiful"; 　
  default:　　
    return "unknown";
}
```

After refactoring:

```js
class EuropeanSwallow { 　
  get plumage() {　　
    return "average";　
  }
}
class AfricanSwallow { 　
  get plumage() {　　 
    return (this.numberOfCoconuts > 2) ? "tired" : "average";　
  }
}
class NorwegianBlueParrot { 　
  get plumage() {　　 
    return (this.voltage > 100) ? "scorched" : "beautiful";
  }
}
```

1 If classes do not exist for polymorphic behavior, create them together with a factory function to return the correct instance.

2 Use the factory function in calling code.

3 Move the conditional function to the superclass. If the conditional logic is not a self­contained function, use Extract Function (106) to make it so.

4 Pick one of the subclasses. Create a subclass method that overrides the conditional statement method. Copy the body of that leg of the conditional statement into the subclass method and adjust it to fit.

5 Repeat for each leg of the conditional.

6 Leave a default case for the superclass method. Or, if superclass should be abstract, declare that method as abstract or throw an error to show it should be the responsibility of a subclass.

1、如果现有的类尚不具备多态行为，就用工厂函数创建之，令工厂函数返回恰当的对象实例。

2、在调用方代码中使用工厂函数获得对象实例。

3、将带有条件逻辑的函数移到超类中。如果条件逻辑还未提炼至独立的函数，首先对其使用提炼函数（106）。

4、任选一个子类，在其中建立一个函数，使之覆写超类中容纳条件表达式的那个函数。将与该子类相关的条件表达式分支复制到新函数中，并对它进行适当调整。

5、重复上述过程，处理其他条件分支。

6、在超类函数中保留默认情况的逻辑。或者，如果超类应该是抽象的，就把该函数声明为 abstract，或在其中直接抛出异常，表明计算责任都在子类中。

#### 2.5 引入特例（引入 null 对象）

```js
if (aCustomer === "unknown") customerName = "occupant";
```

After refactoring:

```js
class UnknownCustomer {    
  get name() {
    return "occupant";
  }
}
```

Begin with a container data structure (or class) that contains a property which is the subject of the refactoring. Clients of the container compare the subject property of the container to a special­case value. We wish to replace the special­case value of the subject with a special case class or data structure.

1 Add a special­case check property to the subject, returning false.

2 Create a special­case object with only the special­case check property, returning true.

3 Apply Extract Function (106) to the special­case comparison code. Ensure that all clients use the new function instead of directly comparing it.

4 Introduce the new special­case subject into the code, either by returning it from a function call or by applying a transform function.

5 Change the body of the special­case comparison function so that it uses the specialcase check property.

6 Test.

7 Use Combine Functions into Class (144) or Combine Functions into Transform (149) to move all of the common special­case behavior into the new element. Since the special­case class usually returns fixed values to simple requests, these may be handled by making the special case a literal record.

8 Use Inline Function (115) on the special­case comparison function for the places where it’s still needed.

我们从一个作为容器的数据结构（或者类）开始，其中包含一个属性，该属性就是我们要重构的目标。容器的客户端每次使用这个属性时，都需要将其与某个特例值做比对。我们希望把这个特例值替换为代表这种特例情况的类或数据结构。

1、给重构目标添加检查特例的属性，令其返回 false。

2、创建一个特例对象，其中只有检查特例的属性，返回 true。

3、对「与特例值做比对」的代码运用提炼函数（106），确保所有客户端都使用这个新函数，而不再直接做特例值的比对。

4、将新的特例对象引入代码中，可以从函数调用中返回，也可以在变换函数中生成。

5、修改特例比对函数的主体，在其中直接使用检查特例的属性。

6、测试。

7、使用函数组合成类（144）或函数组合成变换（149），把通用的特例处理逻辑都搬移到新建的特例对象中。特例类对于简单的请求通常会返回固定的值，因此可以将其实现为字面记录（literal record）。

8、对特例比对函数使用内联函数（115），将其内联到仍然需要的地方。

#### 2.6 引入断言

```js
if (this.discountRate) 
  base = base - (this.discountRate * base);
```

After refactoring:

```js
assert(this.discountRate >= 0); 
if (this.discountRate)  
  base = base - (this.discountRate * base);
```

When you see that a condition is assumed to be true, add an assertion to state it. Since assertions should not affect the running of a system, adding one is always behavior­preserving.

如果你发现代码假设某个条件始终为真，就加入一个断言明确说明这种情况。因为断言应该不会对系统运行造成任何影响，所以「加入断言」永远都应该是行为保持的。

### 03. 重新组织数据相关

#### 3.1 拆分变量

```js
let temp = 2 * (height + width); 
console.log(temp);
temp = height * width; 
console.log(temp);
```

After Refactoring:

```js
const perimeter = 2 * (height + width); 
console.log(perimeter);
const area = height * width; 
console.log(area);
```

1 Change the name of the variable at its declaration and first assignment. If the later assignments are of the form i = i + something, that is a collecting variable, so don’t split it. A collecting variable is often used for calculating sums, string concatenation, writing to a stream, or adding to a collection.

2 If possible, declare the new variable as immutable.

3 Change all references of the variable up to its second assignment. 

4 Test.

5 Repeat in stages, at each stage renaming the variable at the declaration and changing references until the next assignment, until you reach the final assignment.

1、在待分解变量的声明及其第一次被赋值处，修改其名称。如果稍后的赋值语句是「i = i + 某表达式形式」，意味着这是一个结果收集变量，就不要分解它。结果收集变量常用于累加、字符串拼接、写入流或者向集合添加元素。

2、如果可能的话，将新的变量声明为不可修改。

3、以该变量的第二次赋值动作为界，修改此前对该变量的所有引用，让它们引用新变量。

4、测试。

5、重复上述过程。每次都在声明处对变量改名，并修改下次赋值之前的引用，直至到达最后一处赋值。

#### 3.2 字段改名

```js
class Organization {   
  get name() {...}
}
```

After Refactoring;

```js
class Organization {   
  get title() {...}
}
```

1 If the record has limited scope, rename all accesses to the field and test; no need to do the rest of the mechanics.

2 If the record isn’t already encapsulated, apply Encapsulate Record (162).

3 Rename the private field inside the object, adjust internal methods to fit.

4 Test. 

5 If the constructor uses the name, apply Change Function Declaration (124) to rename it.

6 Apply Rename Function (124) to the accessors.

1、如果记录的作用域较小，可以直接修改所有该字段的代码，然后测试。后面的步骤就都不需要了。

2、如果记录还未封装，请先使用封装记录（162）。

3、在对象内部对私有字段改名，对应调整内部访问该字段的函数。

4、测试。

5、如果构造函数的参数用了旧的字段名，运用改变函数声明（124）将其改名。

6、运用函数改名（124）给访问函数改名。

#### 3.3 以查询取代派生变量

```js
get discountedTotal() {return this._discountedTotal;} 
set discount(aNumber) {　
  const old = this._discount; 　
  this._discount = aNumber; 　
  this._discountedTotal += old - aNumber;
}
```

After Refactoring:

```js
get discountedTotal() {return this._baseTotal - this._discount;} 
set discount(aNumber) {this._discount = aNumber;}
```

1 Identify all points of update for the variable. If necessary, use Split Variable (240) to separate each point of update.

2 Create a function that calculates the value of the variable.

3 Use Introduce Assertion (302) to assert that the variable and the calculation give the same result whenever the variable is used. If necessary, use Encapsulate Variable (132) to provide a home for the assertion. 

4.Test.

5 Replace any reader of the variable with a call to the new function.

6 Test.

7 Apply Remove Dead Code (237) to the declaration and updates to the variable.

1、识别出所有对变量做更新的地方。如有必要，用拆分变量（240）分割各个更新点。

2、新建一个函数，用于计算该变量的值。

3、用引入断言（302）断言该变量和计算函数始终给出同样的值。如有必要，用封装变量（132）将这个断言封装起来。

4、测试。

5、修改读取该变量的代码，令其调用新建的函数。

6、测试。

7、用移除死代码（237）去掉变量的声明和赋值。

#### 3.4 引用对象改为值对象

```js
class Product {  
  applyDiscount(arg) {this._price.amount -= arg;
}
```

After Refactoring:

```js
class Product {   
  applyDiscount(arg) {    
    this._price = new Money(this._price.amount - arg, this._price.currency);
  }
}
```

1 Check that the candidate class is immutable or can become immutable.

2 For each setter, apply Remove Setting Method (331).

3 Provide a value­based equality method that uses the fields of the value object.

4 Most language environments provide an overridable equality function for this purpose. Usually you must override a hashcode generator method as well.

1、检查重构目标是否为不可变对象，或者是否可修改为不可变对象。

2、用移除设值函数（331）逐一去掉所有设值函数。

3、提供一个基于值的相等性判断函数，在其中使用值对象的字段。

大多数编程语言都提供了可覆写的相等性判断函数。通常你还必须同时覆写生成散列码的函数。

#### 3.5 值对象改为引用对象

```js
let customer = new Customer(customerData);
```

After Refactoring:

```js
let customer = customerRepository.get(customerData.id);
```

1 Create a repository for instances of the related object (if one isn’t already present).

2 Ensure the constructor has a way of looking up the correct instance of the related object.

3 Change the constructors for the host object to use the repository to obtain the related object. Test after each change.

1、为相关对象创建一个仓库（如果还没有这样一个仓库的话）。

2、确保构造函数有办法找到关联对象的正确实例。

3、修改宿主对象的构造函数，令其从仓库中获取关联对象。每次修改后执行测试。

## 重构列表

改变函数声明（Change Function Declaration）、将引用对象改为值对象（Change Reference to Value）、将值对象改为引用对象（Change Value to Reference）、折叠继承体系（Collapse Hierarchy）

函数组合成类（Combine Functions into Class）、函数组合成变换（Combine Functions into Transform）、合并条件表达式（Consolidate Conditional Expression）、分解条件表达式（Decompose Conditional）

封装集合（Encapsulate Collection）、封装记录（Encapsulate Record）、封装变量（Encapsulate Variable）

提炼类（Extract Class）、提炼函数（Extract Function）、提炼超类（Extract Superclass）、提炼变量（Extract Variable）

隐藏委托关系（Hide Delegate）、内联类（Inline Class）、内联函数（Inline Function）、内联变量（Inline Variable）

引入断言（Introduce Assertion）、引入参数对象（Introduce Parameter Object）、引入特例（Introduce Special Case）

搬移字段（Move Field）、搬移函数（Move Function）、搬移语句到函数（Move Statements into Function）、搬移语句到调用者（Move Statements to Callers）

函数参数化（Parameterize Function）、保持对象完整（Preserve Whole Object）、构造函数本体上移（Pull Up Constructor Body）、字段上移（Pull Up Field）、函数上移（Pull Up Method）、字段下移（Push Down Field）、函数下移（Push Down Method）

移除死代码（Remove Dead Code）、移除标记参数（Remove Flag Argument）、移除中间人（Remove Middle Man）、移除设值函数（Remove Setting Method）、移除子类（Remove Subclass）、字段改名（Rename Field）、变量改名（Rename Variable）

以函数取代命令（Replace Command with Function）、以多态取代条件表达式（Replace Conditional with Polymorphism）、以工厂函数取代构造函数（Replace Constructor with Factory Function）、以查询取代派生变量（Replace Derived Variable with Query）、以命令取代函数（Replace Function with Command）

以函数调用取代内联代码（Replace Inline Code with Function Call）、以管道取代循环（Replace Loop with Pipeline）、以卫语句取代嵌套条件表达式（Replace Nested Conditional with Guard Clauses）、以查询取代参数（Replace Parameter with Query）、以对象取代基本类型（Replace Primitive with Object）

以参数取代查询（Replace Query with Parameter）、以委托取代子类（Replace Subclass with Delegate）、以委托取代超类（Replace Superclass with Delegate）、以查询取代临时变量（Replace Temp with Query）、以子类取代类型码（Replace Type Code with Subclasses）、将查询函数和修改函数分离（Separate Query from Modifier）

移动语句（Slide Statements）、拆分循环（Split Loop）、拆分阶段（Split Phase）、拆分变量（Split Variable）、替换算法（Substitute Algorithm）

## 坏味道与重构手法速查表

1、异曲同工的类（Alternative Classes with Different Interfaces）——改变函数声明（124），搬移函数（198），提炼超类（375）

2、注释（Comments）——提炼函数（106），改变函数声明（124），引入断言（302）

3、纯数据类（Data Class）——封装记录（162），移除设值函数（331），搬移函数（198），提炼函数 （106），拆分阶段（154）

4、数据泥团（Data Clumps）——提炼类（182），引入参数对象（140），保持对象完整（319）

5、发散式变化（Divergent Change）——拆分阶段（154），搬移函数（198），提炼函数（106），提炼类（182）

6、重复代码（Duplicated Code）——提炼函数（106），移动语句（223），函数上移（350）

7、依恋情结（Feature Envy）——搬移函数（198），提炼函数（106）

8、全局数据（Global Data）——封装变量（132） 

9、内幕交易（Insider Trading）——搬移函数（198），搬移字段（207），隐藏委托关系（189），以委托取代子类（381），以委托取代超类（399）

10、过大的类（Large Class）——提炼类（182），提炼超类（375），以子类取代类型码（362）

11、冗赘的元素（Lazy Element）——内联函数（115），内联类（186），折叠继承体系（380）

12、过长函数（Long Function）——提炼函数（106），以查询取代临时变量（178），引入参数对象 （140），保持对象完整（319），以命令取代函数（337），分解条件表达式 （260），以多态取代条件表达式（272），拆分循环（227）

13、过长参数列（Long Parameter List）——以查询取代参数（324），保持对象完整（319），引入参数对象 （140），移除标记参数（314），函数组合成类（144）

14、循环语句（Loops）——以管道取代循环（231）

15、过长的消息链（Message Chains）——隐藏委托关系（189），提炼函数（106），搬移函数（198）

16、中间人（Middle Man）——移除中间人（192），内联函数（115），以委托取代超类（399），以委托取代子类（381）

17、可变数据（Mutable Data）——封装变量（132），拆分变量（240），移动语句（223），提炼函数 （106），将查询函数和修改函数分离（306），移除设值函数（331），以查询取代派生变量（248），函数组合成类（144），函数组合成变换（149）， 将引用对象改为值对象（252）

18、神秘命名（Mysterious Name）——改变函数声明（124），变量改名（137），字段改名（244）

19、基本类型偏执（Primitive Obsession）——以对象取代基本类型（174），以子类取代类型码（362），以多态取代条件表达式（272），提炼类（182），引入参数对象（140）

20、被拒绝的遗赠（Refused Bequest）——函数下移（359），字段下移（361），以委托取代子类（381），以委托取代超类（399）

21、重复的 switch（Repeated Switches）——以多态取代条件表达式（272）

22、霰弹式修改（Shotgun Surgery）——搬移函数（198），搬移字段（207），函数组合成类（144），函数组合成变换（149），拆分阶段（154），内联函数（115），内联类（186）

23、夸夸其谈通用性（Speculative Generality）——折叠继承体系（380），内联函数（115），内联类（186），改变函数声明（124），移除死代码（237）

24、临时字段（Temporary Field）——提炼类（182），搬移函数（198），引入特例（289）

## 书评

### 01

2009 年，在为《重构》第一版的中译本再版整理译稿时，我已经隐约察觉行业中对「重构」这个概念的矛盾张力。一方面，在这个「VUCA」（易变、不确定、复杂、模糊）横行的年代，有能力调整系统的内部结构，使其更具长期生命力，这是一个令人神往的期许。另一方面，重构的扎实工夫要学起来、做起来，颇不是件轻松的事，且不说详尽到近乎琐碎的重构手法，光是单元测试一事，怕是已有九成同行无法企及。结果，「重构」渐渐成了一块漂亮的招牌，大家都愿意挂上这个名号，可实际上干的却多是「刀劈斧砍」的勾当。

如今又是十年过去，只从国内的情况而论，「重构」概念的表里分离，大有愈演愈烈之势。随着当年的一线技术人员纷纷走上领导岗位，他们乐于将「重构」这块漂亮招牌用在更宽泛的环境下，例如系统架构、乃至组织结构，都可以「重构」一下。然而基本功的欠缺，却也一路如影随形。当年在对象中的刀劈斧砍，如今被照搬到了架构、组织的调整。于是「重构」的痛苦回忆又一遍遍重演，甚而程度更深、影响更广、为害更烈。

此时转头看 Martin Fowler 时隔将近廿载后终于付梓的《重构》第二版，我不禁感叹于他对「微末功夫」的执着。在此书尚未成型之前，我和当时 ThoughtWorks 的同事们曾有很多猜测，猜 Fowler 先生是否会在第二版中拔高层次，多谈谈设计乃至架构级别的重构手法，甚或跟随「敏捷组织」、「精益企业」的风潮谈谈组织重构，也未为不可。孰料成书令我们跌破眼镜，Fowler 先生不仅没有拔高，反而把工夫做得更扎实了。

对比前后两版的重构列表，可以发现：第二版收录的重构手法在用途上更加内聚，在操作上更加连贯，更重视重构手法之间的组合运用。第一版中占了整章篇幅的「大型重构」，在第二版中全数删去。一些较为复杂的重构手法，例如复制「被监视数据」、塑造模板函数等，第二版也不再收录。而第二版中新增的重构手法，则多是提炼变量、移动语句、拆分循环、拆分变量。

这样更加细致而微的操作。这些新增的手法看似简单，但直指大规模遗留代码中最常见的重构难点，正好补上了第一版中阙漏的细节。这一变化，正反映出 Fowler 先生对于重构一事一贯的态度：千里之行积于跬步，越是面对复杂多变的外部环境，越是要做好基本功、迈出扎实步。

坏味道、测试先行、行为保持的变更动作，是重构的基本功。在《重构》第二版里，重构手法的细节被再度打磨，重构过程比之第一版愈发流畅。细细品味重构手法中的前后步骤，琢磨作者是如何做到行为保持，这是能启发读者举一反三的读书法。举保持对象完整重构手法为例，第一版中的做法是在原本函数上新添参数；而第二版的做法则是先新建一个空函数，在其中做完想要的调整之后，再整体替换原本函数。两相对比，无疑是新的做法更加可控、出错时测试失败的范围更小。

无独有偶，我在 ThoughtWorks 时的同事王健在开展大型的架构重构时，总结了重构的「十六字心法」，恰与保持对象完整重构手法在第二版中这个新的做法暗合。这十六字心法如是说：旧的不变、新的创建、一步切换、旧的再见。

从这个视角品味一个个重构巨细靡遗的做法，读者大概能感受到重构与「刀劈斧砍」之间最根本的分歧。在很多重构（例如最常用的改变函数声明）的做法中，Fowler 先生会引入「很快就会再次修改甚至删除」的临时元素。假如只看起止状态，这些变更过程中的临时元素似乎是浪费：为何不直接一步到位改变到完善的结果状态呢？然而这些临时元素所代表的，是对变更过程（而非只是结果）的设计。缺乏对过程的精心设计与必要投入，只抱着对结果的美好憧憬提刀上阵，遇到困难就靠「奋斗精神」和加班解决，这种「刀劈斧砍」不止发生在缺乏审慎的「重构」现场，又何尝不是我们这个行业的缩影？

是以，重构这门技艺、以及 Fowler 先生撰写《重构》的态度，代表的是软件开发的匠艺 —— 对「正确的做事方式」的重视。在一个浮躁之风日盛的行业中，很多人会强调「只看结果」，轻视做事的过程与方式。然而对于软件开发的专业人士而言，如果忽视了过程与方式，也就等于放弃了我们自己的立身之本。Fowler 先生近廿载对这本书、对重构手法的精心打磨，给了我们一个榜样：一个对匠艺上心的专业人士，日积月累对过程与方式的重视，是能有所成就的。

十七年前，我以菜鸟之身读到《重构》，深受其中蕴涵的工匠精神感召，在 Fowler 先生与侯捷老师帮助下，完成了本书第一版的翻译工作。如今再译本书第二版，来自 ThoughtWorks 的青年才俊林从羽君主动请缨与我搭档合译，我亦将此视为匠艺传承的一桩美事。新一代程序员中，关注新工具、新框架、新商业模式者伙矣，关注面向对象、TDD、重构之类基本功者寥寥。林君年纪虽轻，却能平心静气磨砺技艺，对基本功学而时习，颇有老派工匠之风。当年藉由翻译《重构》一书，我从 Fowler 先生、侯捷老师身上学到他们的工匠精神，十余年来时时践行自勉。如今新一代软件工匠的代表人物林君接手此书，必会令工匠精神传承光大。

据说古时高僧有偈云：「时时勤拂拭，勿使惹尘埃」。代码当如是，专业人士的技艺亦当如是。与《重构》的诸位读者共勉。

### 02

纵览武侠江湖，制胜法门不外两项，内功和外功。二者得一可天下去得，但最终皆入内外兼修之境。倚天是自内而外，先修内功九阳真经，然后以此为基础，加上太极拳和太极剑，最终成就天下第一高手。笑傲是自外而内，先学独孤九剑，后学吸星大法，最后学易筋经。神雕也不外如是，玉女心经算是外功，内功则是独孤求败之法门。只修内不修外，好比万贯家财而不知用，张无忌也要得传太极方可天下去得。只修外不修内，终是一场空。令狐冲身怀独孤九剑，在义救向问天时几乎丢掉性命。

软件工程的自动化测试和设计模式，近似武侠世界的内功和外功。自动化测试好比内功，没有自动化测试为根基，每做一次修改，都可能引发不可思议错误，若没有自动化测试，最终进入无测试死循环。设计模式好比外功，重构的方法好比剑招，剑招固然重要，但更重要的是知道什么时候用什么剑招，心中无招，信手挥洒，皆是模式。

内里明心见性，心如磐石，护体神功，自动化测试；外求格物致知，游刃有余，独孤九剑，设计模式。

而「重构」好比五岳剑谱，是独孤九剑之基础功夫，令狐冲是在思过崖看到五岳剑派的剑谱和破法，然后发了疑情，然后才接受独孤九剑的思想并最终继承之，而练成之后，随心所欲，五岳剑谱的剑招还是常用的，所以讲独孤九剑与五岳剑谱只是外功的不同阶段而已。学会了五岳剑谱，才能更好地领会独孤九剑，学会了独孤九剑，才能更好地把握什么时候用什么剑招。《重构》->《设计模式》。

1『又提供了一个自修软件工程的视角。』

### 03

先说作者，作者曾经也是写 Java 的，后来貌似不喜欢 Java 了（正常人都会这样吧），先是跟人合著了本 Ruby 版的重构，然后 —— 又应上了那个说法：所有能用 JavaScript 写的东西终将用 JavaScript 写成。这本关于重构的书，终于用 JavaScript 做了重构。当我在书里看到 Object.assign、Lodash 和箭头函数时，我的内心感到了快乐。尤其是小步重构到后来，函数体里都转成箭头函数和 lambda 表达式，hmm，真香。

书的第一章从一个例子开始，一步步地重构，看得人如痴如醉 —— 这可不是玩笑，重构的精妙能将人完全代入。而且这个例子，也随着时代的变迁进行了场景修改，第一版是用的影碟出租屋的例子，但是现在基本上很少有人租碟了，所以改成了剧场看剧，嗯，很时髦，也算是一种「重构」吧。

书里对重构这个词进行了阐释：重构 !== 更改，尤其是不等于影响函数正常工作的更改。在作者的概念体系里，重构是小步的、不影响函数行为的迭代式更改，嗯，跟敏捷的概念有点像。重构跟性能优化很像：都是修改代码且不影响行为。但前者是为了理解、便于修改；后者是为了性能而改。

2『重构的定义，做一张术语卡片。』——已完成

关于重构和加新功能的配合，作者把它们比喻成两顶帽子 —— 你戴或者不戴，什么时候戴，都随你，但是你要清楚自己戴着哪一顶帽子。

重构的时机，在书中看来，应该是不得不重构时：譬如添加新功能前，重构能让修改更容易；帮助自己理解代码时，重构能让代码更易懂；捡垃圾时，重构可以改掉屎一样的代码（你懂的）。同样，也有不需要重构的时候：比如这段代码凌乱但是跟我无关、也不需要修改或是在某个隐藏得很好的 API 下。又或者重写更容易，那就重写吧。

另外，关于变量命名的经验：作者喜欢把所有返回值变量命名成 result，学到了 —— 这样能一眼就知道变量的作用。以及，因为 JavaScript 是动态类型语言，所以作者喜欢在变量命名里加类型，尤其是加入不定冠词，比如 aPerformance。

Anyway，重构不是银弹。我认为重构是需要在对代码的业务逻辑、对系统的边界、以及前人的意图都有所理解的基础上才能做的事情。依然记得刚入职时跟着同事们一起 pair programming，看着他们一步步地把代码重构时那种爽感。相信这也是一本常看常新的书啦。再多说一句：完整的测试用例才是重构的关键前提。以及，如之前看的《程序员的呐喊》里说的那样，如果你的 team 里都是天才程序员，管他什么重构不重构的，哈哈哈哈。可惜大部分 team 都是由像我这样的庸人组成，最好还是每个人会一些重构让世界更美好吧。

### 05

组里最主要的 Service 已经运行了几年了，目前大约有 40000 行代码，不少部分缺乏 Unit Tests。每次看代码的时候都有一种想重构的冲动。不过什么时候才重构呢？经理那里是不好交差的 —— 他们关心的是新功能的实现速度。有的时候重写反而（对程序员）的发展更好，因为工作量明显的可以看到。所以重构不过是谁都不愿意做的脏活累活，能拖就拖。

于是就有了一个难题：代码不容易理解，所以才想重构；可不理解又如何重构呢？等自己理解了又懒得重构了，先把手头的任务做完再说吧，重构就留给下一个人吧。我认为《重构 —— 改善既有代码的设计》的贡献就在于教你如何在不完全理解代码的情况下安全的修改代码。

一次和经理讨论到了重构，他说重构要在有完善的测试情况下才能安全的进行。可是眼前的代码测试 Coverage 不到 20%，而且因为正是代码的设计导致其难以测试，这种情况下该怎么办呢？是先努力写测试，然后再重构，还是先重构，然后在测试呢？我觉得可以采用书中提到的已经验证是安全的重构方法先进行重构，重构和加测试交替进行。
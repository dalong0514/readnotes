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

### 0203. 术语卡——纯函数 Data Class

These are classes that have fields, getting and setting methods for the fields, and nothing else. Such classes are dumb data holders and are often being manipulated in far too much detail by other classes. In some stages, these classes may have public fields. If so, you should immediately apply Encapsulate Record (162) before anyone notices. Use Remove Setting Method (331) on any field that should not be changed.

Look for where these getting and setting methods are used by other classes. Try to use Move Function (198) to move behavior into the data class. If you can’t move a whole function, use Extract Function (106) to create a function that can be moved.

Data classes are often a sign of behavior in the wrong place, which means you can make big progress by moving it from the client into the data class itself. But there are exceptions, and one of the best exceptions is a record that’s being used as a result record from a distinct function invocation. A good example of this is the intermediate data structure after you’ve applied Split Phase (154). A key characteristic of such a result record is that it’s immutable (at least in practice). Immutable fields don’t need to be encapsulated and information derived from immutable data can be represented as fields rather than getting methods.

所谓纯数据类是指：它们拥有一些字段，以及用于访问（读写）这些字段的函数，除此之外一无长物。这样的类只是一种不会说话的数据容器，它们几乎一定被其他类过分细琐地操控着。这些类早期可能拥有 public 字段，若果真如此，你应该在别人注意到它们之前，立刻运用封装记录（162）将它们封装起来。对于那些不该被其他类修改的字段，请运用移除设值函数（331）。然后，找出这些取值 / 设值函数被其他类调用的地点。尝试以移函数（198）把那些调用行为搬移到纯数据类里来。如果无法搬移整个函数，就运用提炼函数 (106) 产生一个可被搬移的函数。

纯数据类常常意味着行为被放在了错误的地方。也就是说，只要把处理数据的行为从客户端搬移到纯数据类里来，就能使情况大为改观。但也有例外情况，一个最好的例外情况就是，纯数据记录对象被用作函数调用的返回结果，比如使用拆分阶段（154）之后得到的中转数据结构就是这种情況。这种结果数据对象有一个关键的特征：它是不可修改的（至少在拆分阶段（154）的实际操作中是这样）。不可修改的字段无须封装，使用者可以直接通过字段取得数据，无须通过取值函数。

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

16、中间人（Middle Man）——移除中间人（192），内联函数（115），以委托取代超类（399），以委 托取代子类（381）

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
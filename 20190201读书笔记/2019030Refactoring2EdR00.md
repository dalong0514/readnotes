## 记忆时间

## 卡片

### 0101. 主题卡——重构手段

### 1.1 提炼函数

代码里提炼出函数。一些好习惯收集：

1、永远将函数的返回值命名为「result」，这样我一眼就能知道它的作用。然后我再次编译、测试、提交代码。

2、函数参数的命令。使用一门动态类型语言（如 JavaScript）时，跟踪变量的类型很有意义。因此，我为参数取名时都默认带上其类型名。一般我会使用不定冠词修饰它，除非命名中另有解释其角色的相关信息。

### 1.2 内联变量

以查询取代临时变量。变量内联的概念。首先移除局部变量。

As I consider the parameters to amountFor, I look to see where they come from. aPerformance comes from the loop variable, so naturally changes with each iteration through the loop. But play is computed from the performance, so there’s no need to pass it in as a parameter at all—I can just recalculate it within amountFor. When I’m breaking down a long function, I like to get rid of variables like play, because temporary variables create a lot of locally scoped names that complicate extractions. The refactoring I will use here is Replace Temp with Query (178).

This refactoring alarms some programmers. Previously, the code to look up the play was executed once in each loop iteration; now, it’s executed thrice. I’ll talk about the interplay of refactoring and performance later, but for the moment I’ll just observe that this change is unlikely to significantly affect performance, and even if it were, it is much easier to improve the performance of a well­factored code base.

这次重构可能在一些程序员心中敲响警钟：重构前，查找 play 变量的代码在每次循环中只执行了 1 次，而重构后却执行了 3 次。我会在后面探讨重构与性能之间的关系，但现在，我认为这次改动还不太可能对性能有严重影响，即便真的有所影响，后续再对一段结构良好的代码进行性能调优， 也容易得多。

The great benefit of removing local variables is that it makes it much easier to do extractions, since there is less local scope to deal with. Indeed, usually I’ll take out local variables before I do any extractions.

移除局部变量的好处就是做提炼时会简单得多，因为需要操心的局部作用域变少了。实际上，在做任何提炼前，我一般都会先移除局部变量。

### 0201. 术语卡——重构

书里对重构这个词进行了阐释：重构 !== 更改，尤其是不等于影响函数正常工作的更改。在作者的概念体系里，重构是小步的、不影响函数行为的迭代式更改，嗯，跟敏捷的概念有点像。重构跟性能优化很像：都是修改代码且不影响行为。但前者是为了理解、便于修改；后者是为了性能而改。关于重构和加新功能的配合，作者把它们比喻成两顶帽子 —— 你戴或者不戴，什么时候戴，都随你，但是你要清楚自己戴着哪一顶帽子。

重构的时机，在书中看来，应该是不得不重构时：譬如添加新功能前，重构能让修改更容易；帮助自己理解代码时，重构能让代码更易懂；捡垃圾时，重构可以改掉屎一样的代码（你懂的）。同样，也有不需要重构的时候：比如这段代码凌乱但是跟我无关、也不需要修改或是在某个隐藏得很好的 API 下。又或者重写更容易，那就重写吧。

另外，关于变量命名的经验：作者喜欢把所有返回值变量命名成 result，学到了 —— 这样能一眼就知道变量的作用。以及，因为 JavaScript 是动态类型语言，所以作者喜欢在变量命名里加类型，尤其是加入不定冠词，比如 aPerformance。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——Martin Fowler

#### 01. 基本信息

Martin Fowler，本书作者，大师中的大师。

#### 02. 贡献及著作

#### 03. 论文及书籍

#### 04. 演讲汇总

找一个他的 TED 演讲，有的话。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

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

9、内幕交易（Insider Trading）——搬移函数（198），搬移字段（207），隐藏委托关系（189），以委托取 代子类（381），以委托取代超类（399）

10、过大的类（Large Class）——提炼类（182），提炼超类（375），以子类取代类型码（362）

11、冗赘的元素（Lazy Element）——内联函数（115），内联类（186），折叠继承体系（380）

12、过长函数（Long Function）——提炼函数（106），以查询取代临时变量（178），引入参数对象 （140），保持对象完整（319），以命令取代函数（337），分解条件表达式 （260），以多态取代条件表达式（272），拆分循环（227）

13、过长参数列（Long Parameter List）——以查询取代参数（324），保持对象完整（319），引入参数对象 （140），移除标记参数（314），函数组合成类（144）

14、循环语句（Loops）——以管道取代循环（231）

15、过长的消息链（Message Chains）——隐藏委托关系（189），提炼函数（106），搬移函数（198）

16、中间人（Middle Man）——移除中间人（192），内联函数（115），以委托取代超类（399），以委 托取代子类（381）

17、可变数据（Mutable Data）——封装变量（132），拆分变量（240），移动语句（223），提炼函数 （106），将查询函数和修改函数分离（306），移除设值函数（331），以查 询取代派生变量（248），函数组合成类（144），函数组合成变换（149）， 将引用对象改为值对象（252）

18、神秘命名（Mysterious Name）——改变函数声明（124），变量改名（137），字段改名（244）

19、基本类型偏执（Primitive Obsession）——以对象取代基本类型（174），以子类取代类型码（362），以多态取代条 件表达式（272），提炼类（182），引入参数对象（140）

20、被拒绝的遗赠（Refused Bequest）——函数下移（359），字段下移（361），以委托取代子类（381），以委托 取代超类（399）

21、重复的 switch（Repeated Switches）——以多态取代条件表达式（272）

22、霰弹式修改（Shotgun Surgery）——搬移函数（198），搬移字段（207），函数组合成类（144），函数组合 成变换（149），拆分阶段（154），内联函数（115），内联类（186）

23、夸夸其谈通用性（Speculative Generality）——折叠继承体系（380），内联函数（115），内联类（186），改变函数声 明（124），移除死代码（237）

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

2『重构的定义，做一张术语卡片。』

关于重构和加新功能的配合，作者把它们比喻成两顶帽子 —— 你戴或者不戴，什么时候戴，都随你，但是你要清楚自己戴着哪一顶帽子。

重构的时机，在书中看来，应该是不得不重构时：譬如添加新功能前，重构能让修改更容易；帮助自己理解代码时，重构能让代码更易懂；捡垃圾时，重构可以改掉屎一样的代码（你懂的）。同样，也有不需要重构的时候：比如这段代码凌乱但是跟我无关、也不需要修改或是在某个隐藏得很好的 API 下。又或者重写更容易，那就重写吧。

另外，关于变量命名的经验：作者喜欢把所有返回值变量命名成 result，学到了 —— 这样能一眼就知道变量的作用。以及，因为 JavaScript 是动态类型语言，所以作者喜欢在变量命名里加类型，尤其是加入不定冠词，比如 aPerformance。

Anyway，重构不是银弹。我认为重构是需要在对代码的业务逻辑、对系统的边界、以及前人的意图都有所理解的基础上才能做的事情。依然记得刚入职时跟着同事们一起 pair programming，看着他们一步步地把代码重构时那种爽感。相信这也是一本常看常新的书啦。再多说一句：完整的测试用例才是重构的关键前提。以及，如之前看的《程序员的呐喊》里说的那样，如果你的 team 里都是天才程序员，管他什么重构不重构的，哈哈哈哈。可惜大部分 team 都是由像我这样的庸人组成，最好还是每个人会一些重构让世界更美好吧。

### 05

组里最主要的 Service 已经运行了几年了，目前大约有 40000 行代码，不少部分缺乏 Unit Tests。每次看代码的时候都有一种想重构的冲动。不过什么时候才重构呢？经理那里是不好交差的 —— 他们关心的是新功能的实现速度。有的时候重写反而（对程序员）的发展更好，因为工作量明显的可以看到。所以重构不过是谁都不愿意做的脏活累活，能拖就拖。

于是就有了一个难题：代码不容易理解，所以才想重构；可不理解又如何重构呢？等自己理解了又懒得重构了，先把手头的任务做完再说吧，重构就留给下一个人吧。我认为《重构 —— 改善既有代码的设计》的贡献就在于教你如何在不完全理解代码的情况下安全的修改代码。

一次和经理讨论到了重构，他说重构要在有完善的测试情况下才能安全的进行。可是眼前的代码测试 Coverage 不到 20%，而且因为正是代码的设计导致其难以测试，这种情况下该怎么办呢？是先努力写测试，然后再重构，还是先重构，然后在测试呢？我觉得可以采用书中提到的已经验证是安全的重构方法先进行重构，重构和加测试交替进行。

## 01. Refactoring: A First Example Topics

How do I begin to talk about refactoring? The traditional way is by introducing the history of the subject, broad principles, and the like. When somebody does that at a conference, I get slightly sleepy. My mind starts wandering, with a low­-priority background process polling the speaker until they give an example. The examples wake me up because I can see what is going on. With principles, it is too easy to make broad generalizations—and too hard to figure out how to apply things. An example helps make things clear.

So I’m going to start this book with an example of refactoring. I’ll talk about how refactoring works and will give you a sense of the refactoring process. I can then do the usual principles-­style introduction in the next chapter.

With any introductory example, however, I run into a problem. If I pick a large program, describing it and how it is refactored is too complicated for a mortal reader to work through. (I tried this with the original book—and ended up throwing away two examples, which were still pretty small but took over a hundred pages each to describe.) However, if I pick a program that is small enough to be comprehensible, refactoring does not look like it is worthwhile.

I’m thus in the classic bind of anyone who wants to describe techniques that are useful for real­world programs. Frankly, it is not worth the effort to do all the refactoring that I’m going to show you on the small program I will be using. But if the code I’m showing you is part of a larger system, then the refactoring becomes important. Just look at my example and imagine it in the context of a much larger system.

### Final Thoughts

This is a simple example, but I hope it will give you a feeling for what refactoring is like. I’ve used several refactorings, including Extract Function (106), Inline Variable (123), Move Function (198), and Replace Conditional with Polymorphism (272).

包括提炼函数（106）、内联变量（123）、搬移函数（198）和以多态取代条件表达式（272）等。

There were three major stages to this refactoring episode: decomposing the original function into a set of nested functions, using Split Phase (154) to separate the calculation and printing code, and finally introducing a polymorphic calculator for the calculation logic. Each of these added structure to the code, enabling me to better communicate what the code was doing.

本章的重构有 3 个较为重要的节点，分别是：将原函数分解成一组嵌套的函数、应用拆分阶段（154）分离计算逻辑与输出格式化逻辑，以及为计算器引入多态性来处理计算逻辑。每一步都给代码添加了更多的结构，以便我能更好地表达代码的意图。

As is often the case with refactoring, the early stages were mostly driven by trying to understand what was going on. A common sequence is: Read the code, gain some insight, and use refactoring to move that insight from your head back into the code. The clearer code then makes it easier to understand it, leading to deeper insights and a beneficial positive feedback loop. There are still some improvements I could make, but I feel I’ve done enough to pass my test of leaving the code significantly better than how I found it.

一般来说，重构早期的主要动力是尝试理解代码如何工作。通常你需要先通读代码，找到一些感觉，然后再通过重构将这些感觉从脑海里搬回到代码中。清晰的代码更容易理解，使你能够发现更深层次的设计问题，从而形成积极正向的反馈环。当然，这个示例仍有值得改进的地方，但现在测试仍能全部通过，代码相比初见时已经有了巨大的改善，所以我已经可以满足了。

I’m talking about improving the code—but programmers love to argue about what good code looks like. I know some people object to my preference for small, well­named functions. If we consider this to be a matter of aesthetics, where nothing is either good or bad but thinking makes it so, we lack any guide but personal taste. I believe, however, that we can go beyond taste and say that the true test of good code is how easy it is to change it. Code should be obvious: When someone needs to make a change, they should be able to find the code to be changed easily and to make the change quickly without introducing any errors. A healthy code base maximizes our productivity, allowing us to build more features for our users both faster and more cheaply. To keep code healthy, pay attention to what is getting between the programming team and that ideal, then refactor to get closer to the ideal.

1『 The true test of good code is how easy it is to change it. 重构成「好代码」，好代码的标准是很容易扩展和修改。』

我谈论的是如何改善代码，但什么样的代码才算好代码，程序员们有很多争论。我偏爱小的、命名良好的函数， 也知道有些人反对这个观点。如果我们说这只关乎美学，只是各花入各眼，没有好坏高低之分，那除了诉诸个人品味， 就没有任何客观事实依据了。但我坚信，这不仅关乎个人品味，而且是有客观标准的。我认为，好代码的检验标准就是人们是否能轻而易举地修改它。好代码应该直截了当：有人需要修改代码时，他们应能轻易找到修改点，应该能快速做出更改，而不易引入其他错误。一个健康的代码库能够最大限度地提升我们的生产力，支持我们更快、更低成本地为用户添加新特性。为了保持代码库的健康，就需要时刻留意现状与理想之间的差距，然后通过重构不断接近这个理想。

But the most important thing to learn from this example is the rhythm of refactoring. Whenever I’ve shown people how I refactor, they are surprised by how small my steps are, each step leaving the code in a working state that compiles and passes its tests. I was just as surprised myself when Kent Beck showed me how to do this in a hotel room in Detroit two decades ago. The key to effective refactoring is recognizing that you go faster when you take tiny steps, the code is never broken, and you can compose those small steps into substantial changes. Remember that—and the rest is silence.

这个示例告诉我们最重要的一点就是重构的节奏感。无论何时，当我向人们展示我如何重构时，无人不讶异于我的步子之小，并且每一步都保证代码处于编译通过和测试通过的可工作状态。20 年前，当 Kent Beck 在底特律的一家宾馆里向我展示同样的手法时，我也报以同样的震撼。开展高效有序的重构，关键的心得是：小的步子可以更快前进，请保持代码永远处于可工作状态，小步修改累积起来也能大大改善系统的设计。这几点请君牢记，其余的我已无需多言。

### 1.1 The Starting Point

In the first edition of this book, my starting program printed a bill from a video rental store, which may now lead many of you to ask: “What’s a video rental store?” Rather than answer that question, I’ve reskinned the example to something that is both older and still current.

Image a company of theatrical players who go out to various events performing plays. Typically, a customer will request a few plays and the company charges them based on the size of the audience and the kind of play they perform. There are currently two kinds of plays that the company performs: tragedies and comedies. As well as providing a bill for the performance, the company gives its customers “volume credits” which they can use for discounts on future performances—think of it as a customer loyalty mechanism.

设想有一个戏剧演出团，演员们经常要去各种场合表演戏剧。通常客户（customer）会指定几出剧目，而剧团则根据观众（audience）人数及剧目类型来向客户收费。该团目前出演两种戏剧：悲剧（tragedy）和喜剧 （comedy）。给客户发出账单时，剧团还会根据到场观众的数量给出「观众量积分」（volume credit）优惠，下次客户再请剧团表演时可以使用积分获得折扣——你可以把它看作一种提升客户忠诚度的方式。

The performers store data about their plays in a simple JSON file that looks something like this:

plays.json…

```json
{
    "hamlet": {"name": "Hamlet", "type": "tragedy"}, 
    "as­like": {"name": "As You Like It", "type": "comedy"}, 
    "othello": {"name": "Othello", "type": "tragedy"}
}
```

The data for their bills also comes in a JSON file:

invoices.json…

```json
[
    {
        "customer": "BigCo", "performances": [
        { "playID": "hamlet", "audience": 55 }, {
        "playID": "as­like",
        "audience": 35 }, {
        "playID": "othello",
        "audience": 40 } ]
    }
]
```

The code that prints the bill is this simple function:

```js
function statement (invoice, plays) {
    let totalAmount = 0; 
    let volumeCredits = 0; 
    let result = `Statement for ${invoice.customer}\n`; 
    const format = new Intl.NumberFormat("en­US", { 
        style: "currency", 
        currency: "USD", 
        minimumFractionDigits: 2 
    }).format; 
    
    for (let perf of invoice.performances) {
        const play = plays[perf.playID];
        let thisAmount = 0;
        switch (play.type) { 
            case "tragedy":
                thisAmount = 40000; 
                if (perf.audience > 30) { thisAmount += 1000 * (perf.audience ­- 30); } 
                break; 
            case "comedy":
                thisAmount = 30000; 
                if (perf.audience > 20) { thisAmount += 10000 + 500 * (perf.audience ­- 20); } 
                thisAmount += 300 * perf.audience; 
                break; 
            default:
                throw new Error(`unknown type: ${play.type}`); 
        }
        // add volume credits 
        volumeCredits += Math.max(perf.audience ­- 30, 0); 
        // add extra credit for every ten comedy attendees 
        if ("comedy" === play.type) volumeCredits += Math.floor(perf.audience / 5);
        // print line for this order 
        result += `${play.name}: ${format(thisAmount/100)}(${perf.audience} seats)\n`;
        totalAmount += thisAmount;
    } 
    result += `Amount owed is ${format(totalAmount/100)}\n`; 
    result += `You earned ${volumeCredits} credits\n`; 
    return result;
}
```

Running that code on the test data files above results in the following output:

```
Statement for BigCo 
    Hamlet: $650.00 (55 seats) 
    As You Like It: $580.00 (35 seats) 
    Othello: $500.00 (40 seats) 
    Amount owed is $1,730.00 
You earned 47 credits
```

1『

在 vue 是实现：

```js
stateMent() {
  //  invoices.json 数据是一个数组
  let invoice = invoices[0];
  let totalAmount = 0;
  let volumeCredits = 0;
  let result = `Statement for ${invoice.customer}\n`;
  const format = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2,
  }).format;
  for (let perf of invoice.performances) {
    const play = plays[perf.playID];
    let thisAmount = 0;

    switch (play.type) {
      case 'tragedy':
        thisAmount = 40000;
        if (perf.audience > 30) {
          thisAmount += 1000 * (perf.audience - 30);
        }
        break;
      case 'comedy':
        thisAmount = 30000;
        if (perf.audience > 20) {
          thisAmount += 10000 + 500 * (perf.audience -20);
        }
        thisAmount += 300 * perf.audience;
        break;
      default:
        throw new Error(`unkown type: ${paly.type}`);
    }
    // add volume credits
    volumeCredits += Math.max(perf.audience - 30, 0);
    // add extra credit for every ten comedy attendees
    if ('comedy' === play.type) {
      volumeCredits += Math.floor(perf.audience / 5);
    }

    // print line for this order
    result += `${play.name}: ${format(thisAmount/100)}(${perf.audience} seats)\n`;
    totalAmount += thisAmount;
  }
  result += `Amount owed is ${format(totalAmount/100)}\n`;
  result += `You earned ${volumeCredits} credits\n`;
  console.log(result);
},
```

』

### 1.2 Comments on The Starting Program

What are your thoughts on the design of this program? The first thing I’d say is that it’s tolerable as it is—a program so short doesn’t require any deep structure to be comprehensible. But remember my earlier point that I have to keep examples small. Imagine this program on a larger scale—perhaps hundreds of lines long. At that size, a single inline function is hard to understand.

Given that the program works, isn’t any statement about its structure merely an aesthetic judgment, a dislike of “ugly” code? After all, the compiler doesn’t care whether the code is ugly or clean. But when I change the system, there is a human involved, and humans do care. A poorly designed system is hard to change—because it is difficult to figure out what to change and how these changes will interact with the existing code to get the behavior I want. And if it is hard to figure out what to change, there is a good chance that I will make mistakes and introduce bugs.

Thus, if I’m faced with modifying a program with hundreds of lines of code, I’d rather it be structured into a set of functions and other program elements that allow me to understand more easily what the program is doing. If the program lacks structure, it’s usually easier for me to add structure to the program first, and then make the change I need.

When you have to add a feature to a program but the code is not structured in a convenient way, first refactor the program to make it easy to add the feature, then add the feature.

In this case, I have a couple of changes that the users would like to make. First, they want a statement printed in HTML. Consider what impact this change would have. I’m faced with adding conditional statements around every statement that adds a string to the result. That will add a host of complexity to the function. Faced with that, most people prefer to copy the method and change it to emit HTML. Making a copy may not seem too onerous a task, but it sets up all sorts of problems for the future. Any changes to the charging logic would force me to update both methods—and to ensure they are updated consistently. If I’m writing a program that will never change again, this kind of copy­and­paste is fine. But if it’s a long­lived program, then duplication is a menace.

This brings me to a second change. The players are looking to perform more kinds of plays: they hope to add history, pastoral, pastoral­comical, historical­pastoral, tragicalhistorical, tragical­-comical­-historical­pastoral, scene individable, and poem unlimited to their repertoire. They haven’t exactly decided yet what they want to do and when. This change will affect both the way their plays are charged for and the way volume credits are calculated. As an experienced developer I can be sure that whatever scheme they come up with, they will change it again within six months. After all, when feature requests come, they come not as single spies but in battalions.

现在，第二个变化来了：演员们尝试在表演类型上做更多突破，无论是历史剧、田园剧、田园喜剧、田园史剧、历史悲剧还是历史田园悲喜剧，无论一成不变的正统戏，还是千变万幻的新派戏，他们都希望有所尝试，只是还没有决定试哪种以及何时试演。这对戏剧场次的计费方式、积分的计算方式都有影响。作为一个经验丰富的开发者，我可以肯定：不论最终提出什么方案，他们一定会在 6 个月之内再次修改它。毕竟，需求通常不来则已，一来便会接踵而至。

Again, that statement method is where the changes need to be made to deal with changes in classification and charging rules. But if I copy statement to htmlStatement, I’d need to ensure that any changes are consistent. Furthermore, as the rules grow in complexity, it’s going to be harder to figure out where to make the changes and harder to do them without making a mistake.

Let me stress that it’s these changes that drive the need to perform refactoring. If the code works and doesn’t ever need to change, it’s perfectly fine to leave it alone. It would be nice to improve it, but unless someone needs to understand it, it isn’t causing any real harm. Yet as soon as someone does need to understand how that code works, and struggles to follow it, then you have to do something about it.

我再强调一次，是需求的变化使重构变得必要。如果一段代码能正常工作，并且不会再被修改，那么完全可以不去重构它。能改进之当然很好，但若没人需要去理解它，它就不会真正妨碍什么。如果确实有人需要理解它的工作原理， 并且觉得理解起来很费劲，那你就需要改进一下代码了。

### 1.3 The First Step in Refactoring

Whenever I do refactoring, the first step is always the same. I need to ensure I have a solid set of tests for that section of code. The tests are essential because even though I will follow refactorings structured to avoid most of the opportunities for introducing bugs, I’m still human and still make mistakes. The larger a program, the more likely it is that my changes will cause something to break inadvertently—in the digital age, frailty’s name is software.

1『重构的前提是该代码有一组可靠的测试。』

Since the statement returns a string, what I do is create a few invoices, give each invoice a few performances of various kinds of plays, and generate the statement strings. I then do a string comparison between the new string and some reference strings that I have hand­checked. I set up all of these tests using a testing framework so I can run them with just a simple keystroke in my development environment. The tests take only a few seconds to run, and as you will see, I run them often.

statement 函数的返回值是一个字符串，我做的就是创建几张新的账单（invoice），假设每张账单收取了几出戏剧的费用，然后使用这几张账单作为输入调用 statement 函数， 生成对应的对账单（statement）字符串。我会拿生成的字符串与我已经手工检查过的字符串做比对。我会借助一个测试框架来配置好这些测试，只要在开发环境中输入一行命令就可以把它们运行起来。运行这些测试只需几秒钟，所以你会看到我经常运行它们。

An important part of the tests is the way they report their results. They either go green, meaning that all the strings are identical to the reference strings, or red, showing a list of failures—the lines that turned out differently. The tests are thus self­checking. It is vital to make tests self­checking. If I don’t, I’d end up spending time hand­checking values from the test against values on a desk pad, and that would slow me down. Modern testing frameworks provide all the features needed to write and run selfchecking tests.

测试过程中很重要的一部分，就是测试程序对于结果的报告方式。它们要么变绿，表示所有新字符串都和参考字符串一样，要么就变红，然后列出失败清单，显示问题字符串的出现行号。这些测试都能够自我检验。使测试能自我检验至关重要，否则就得耗费大把时间来回比对，这会降低开发速度。现代的测试框架都提供了丰富的设施，支持编写和运行能够自我检验的测试。

Before you start refactoring, make sure you have a solid suite of tests. These tests must be self­checking.

重构前，先检查自己是否有一套可靠的测试集。 这些测试必须有自我检验能力。

As I do the refactoring, I’ll lean on the tests. I think of them as a bug detector to protect me against my own mistakes. By writing what I want twice, in the code and in the test, I have to make the mistake consistently in both places to fool the detector. By doublechecking my work, I reduce the chance of doing something wrong. Although it takes time to build the tests, I end up saving that time, with considerable interest, by spending less time debugging. This is such an important part of refactoring that I devote a full chapter to it (Building Tests (85)).

1『第 4 章整篇讲解如何构建测试体系。』

### 1.4 Decomposing The Statement Function

When refactoring a long function like this, I mentally try to identify points that separate different parts of the overall behavior. The first chunk that leaps to my eye is the switch statement in the middle.

As I look at this chunk, I conclude that it’s calculating the charge for one performance. That conclusion is a piece of insight about the code. But as Ward Cunningham puts it, this understanding is in my head—a notoriously volatile form of storage. I need to persist it by moving it from my head back into the code itself. That way, should I come back to it later, the code will tell me what it’s doing—I don’t have to figure it out again.

The way to put that understanding into code is to turn that chunk of code into its own function, naming it after what it does—something like amountFor(aPerformance). When I want to turn a chunk of code into a function like this, I have a procedure for doing it that minimizes my chances of getting it wrong. I wrote down this procedure and, to make it easy to reference, named it Extract Function (106).

First, I need to look in the fragment for any variables that will no longer be in scope once I’ve extracted the code into its own function. In this case, I have three: perf, play, and thisAmount. The first two are used by the extracted code, but not modified, so I can pass them in as parameters. Modified variables need more care. Here, there is only one, so I can return it. I can also bring its initialization inside the extracted code. All of which yields this:

首先，我需要检查一下，如果我将这块代码提炼到自己的一个函数里，有哪些变量会离开原本的作用域。在此示例中，是 perf、play 和 thisAmount 这 3 个变量。前两个变量会被提炼后的函数使用，但不会被修改，那么我就可以将它们以参数方式传递进来。我更关心那些会被修改的变量。这里只有唯一一个——thisAmount，因此可以将它从函数中直接返回。我还可以将其初始化放到提炼后的函数里。

function statement…

```js
function amountFor(perf, play) {
    let thisAmount = 0; 
    switch (play.type) { 
        case "tragedy":
            thisAmount = 40000; 
            if (perf.audience > 30) { 
                thisAmount += 1000 * (perf.audience ­- 30); 
            } 
            break; 
        case "comedy":
            thisAmount = 30000; 
            if (perf.audience > 20) { 
                thisAmount += 10000 + 500 * (perf.audience ­- 20); 
            } 
            thisAmount += 300 * perf.audience; 
            break; 
        default:
            throw new Error(`unknown type: ${play.type}`); 
    } 
    return thisAmount;
}
```

When I use a header like “function someName…” in italics for some code, that means that the following code is within the scope of the function, file, or class named in the header. There is usually other code within that scope that I won’t show, as I’m not discussing it at the moment.

The original statement code now calls this function to populate thisAmount:

top level…

```js
function statement (invoice, plays) {
    let totalAmount = 0; 
    let volumeCredits = 0; 
    let result = `Statement for ${invoice.customer}\n`; 
    const format = new Intl.NumberFormat("en­US", { 
        style: "currency", 
        currency: "USD", 
        minimumFractionDigits: 2 
    }).format; 
    
    for (let perf of invoice.performances) {
        const play = plays[perf.playID];
        let thisAmount = amountFor(perf, play);
        
        // add volume credits 
        volumeCredits += Math.max(perf.audience ­- 30, 0); 
        // add extra credit for every ten comedy attendees 
        if ("comedy" === play.type) volumeCredits += Math.floor(perf.audience / 5);
        
        // print line for this order 
        result += `${play.name}: ${format(thisAmount/100)}(${perf.audience} seats)\n`;
        totalAmount += thisAmount;
    } 
    result += `Amount owed is ${format(totalAmount/100)}\n`; 
    result += `You earned ${volumeCredits} credits\n`; 
    return result;
}
```

1『

vue 里：

```js
stateMent() {
  let invoice = invoices[0];
  let totalAmount = 0;
  let volumeCredits = 0;
  let result = `Statement for ${invoice.customer}\n`;
  const format = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2,
  }).format;
  for (let perf of invoice.performances) {
    const play = plays[perf.playID];
    let thisAmount = this.amountFor(perf, play)

    // add volume credits
    volumeCredits += Math.max(perf.audience - 30, 0);
    // add extra credit for every ten comedy attendees
    if ('comedy' === play.type) {
      volumeCredits += Math.floor(perf.audience / 5);
    }

    // print line for this order
    result += `${play.name}: ${format(thisAmount/100)}(${perf.audience} seats)\n`;
    totalAmount += thisAmount;
  }
  result += `Amount owed is ${format(totalAmount/100)}\n`;
  result += `You earned ${volumeCredits} credits\n`;
  console.log(result);
},
amountFor(perf, play) {
  let thisAmount = 0;
  switch (play.type) {
    case 'tragedy':
      thisAmount = 40000;
      if (perf.audience > 30) {
        thisAmount += 1000 * (perf.audience - 30);
      }
      break;
    case 'comedy':
      thisAmount = 30000;
      if (perf.audience > 20) {
        thisAmount += 10000 + 500 * (perf.audience - 20);
      }
      thisAmount += 300 * perf.audience;
      break;
    default:
      throw new Error(`unkown type: ${paly.type}`);
  }
  return thisAmount;
}
```

』

Once I’ve made this change, I immediately compile and test to see if I’ve broken anything. It’s an important habit to test after every refactoring, however simple. Mistakes are easy to make—at least, I find them easy to make. Testing after each change means that when I make a mistake, I only have a small change to consider in order to spot the error, which makes it far easier to find and fix. This is the essence of the refactoring process: small changes and testing after each change. If I try to do too much, making a mistake will force me into a tricky debugging episode that can take a long time. Small changes, enabling a tight feedback loop, are the key to avoiding that mess.

1『无论多小的改动，改完后直接再跑一下，看看跟改前跑的结果是够一样，一定要养成这个习惯。』

I use compile here to mean doing whatever is needed to make the JavaScript executable. Since JavaScript is directly executable, that may mean nothing, but in other cases it may mean moving code to an output directory and/or using a processor such as Babel [babel].

Refactoring changes the programs in small steps, so if you make a mistake, it is easy to find where the bug is.

This being JavaScript, I can extract amountFor into a nested function of statement. This is helpful as it means I don’t have to pass data that’s inside the scope of the containing function to the newly extracted function. That doesn’t make a difference in this case, but it’s one less issue to deal with. In this case the tests passed, so my next step is to commit the change to my local version control system. I use a version control system, such as git or mercurial, that allows me to make private commits. I commit after each successful refactoring, so I can easily get back to a working state should I mess up later. I then squash changes into more significant commits before I push the changes to a shared repository.

Extract Function (106) is a common refactoring to automate. If I was programming in Java, I would have instinctively reached for the key sequence for my IDE to perform this refactoring. As I write this, there is no such robust support for this refactoring in JavaScript tools, so I have to do this manually. It’s not hard, although I have to be careful with those locally scoped variables.

1『提炼函数，写进「重构手段」的主题卡里去。』

Once I’ve used Extract Function (106), I take a look at what I’ve extracted to see if there are any quick and easy things I can do to clarify the extracted function. The first thing I do is rename some of the variables to make them clearer, such as changing thisAmount to result.

It’s my coding standard to always call the return value from a function “result”. That way I always know its role. Again, I compile, test, and commit. Then I move onto the first argument.

2『永远将函数的返回值命名为「result」，这样我一眼就能知道它的作用。然后我再次编译、测试、提交代码。效仿作者的这个习惯。』

function statement…

```js
function amountFor(aPerformance, play) {
    let result = 0; 
    switch (play.type) { 
        case "tragedy":
            result = 40000; 
            if (aPerformance.audience > 30) { result += 1000 * (aPerformance.audience ­ 30); } 
            break; 
        case "comedy":
            result = 30000; 
            if (aPerformance.audience > 20) { result += 10000 + 500 * (aPerformance.audience ­ 20); } 
            result += 300 * aPerformance.audience; 
            break; 
        default:
            throw new Error(`unknown type: ${play.type}`); 
    } 
    return result;
}
```

Again, this is following my coding style. With a dynamically typed language such as JavaScript, it’s useful to keep track of types—hence, my default name for a parameter includes the type name. I use an indefinite article with it unless there is some specific role information to capture in the name. I learned this convention from Kent Beck [Beck SBPP] and continue to find it helpful.

这是我的另一个编码风格。使用一门动态类型语言（如 JavaScript）时，跟踪变量的类型很有意义。因此，我为参数取名时都默认带上其类型名。一般我会使用不定冠词修饰它，除非命名中另有解释其角色的相关信息。这个习惯是从 Kent Beck 那里学的 [Beck SBPP]，到现在我还一直觉得很有用。

3『英语中的冠词有三种，一种是定冠词（the Definite Article），另一种是不定冠词（the Indefinite Article），还有一种是零冠词（Zero Article）。不定冠词 a（an）与数词 one 同源，是「一个」的意思。』

1『参数的命名方式，又是一个值得效仿的好习惯。』

Any fool can write code that a computer can understand. Good programmers write code that humans can understand.

Is this renaming worth the effort? Absolutely. Good code should clearly communicate what it is doing, and variable names are a key to clear code. Never be afraid to change names to improve clarity. With good find-­and-­replace tools, it is usually not difficult; testing, and static typing in a language that supports it, will highlight any occurrences you miss. And with automated refactoring tools, it’s trivial to rename even widely used functions. The next item to consider for renaming is the play parameter, but I have a different fate for that.

好代码应能清楚地表明它在做什么，而变量命名是代码清晰的关键。 只要改名能够提升代码的可读性，那就应该毫不犹豫去做。 有好的查找替换工具在手，改名通常并不困难；此外，你的测试以及语言本身的静态类型支持，都可以帮你揪出漏改的地方。如今有了自动化的重构工具，即便要给一个被大量调用的函数改名，通常也不在话下。


#### 1.4.1 Removing the play Variable

As I consider the parameters to amountFor, I look to see where they come from. aPerformance comes from the loop variable, so naturally changes with each iteration through the loop. But play is computed from the performance, so there’s no need to pass it in as a parameter at all—I can just recalculate it within amountFor. When I’m breaking down a long function, I like to get rid of variables like play, because temporary variables create a lot of locally scoped names that complicate extractions. The refactoring I will use here is Replace Temp with Query (178).

观察 amountFor 函数时，我会看看它的参数都从哪里来。aPerformance 是从循环变量中来，所以自然每次循环都会改变，但 play 变量是由 performance 变量计算得到的，因此根本没必要将它作为参数传入，我可以在 amountFor 函数中重新计算得到它。当我分解一个长函数时，我喜欢将 play 这样的变量移除掉，因为它们创建了很多具有局部作用域的临时变量，这会使提炼函数更加复杂。这里我要使用的重构手法是以查询取代临时变量（178）。

I begin by extracting the right­hand side of the assignment into a function.

function statement…

```js
playFor(aPerformance) {
  return plays[aPerformance.playID];
}
```

top level…

```js
stateMent() {
  let invoice = invoices[0];
  let totalAmount = 0;
  let volumeCredits = 0;
  let result = `Statement for ${invoice.customer}\n`;
  const format = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2,
  }).format;
  for (let perf of invoice.performances) {
    let thisAmount = this.amountFor(perf, this.playFor(perf))

    // add volume credits
    volumeCredits += Math.max(perf.audience - 30, 0);
    // add extra credit for every ten comedy attendees
    if ('comedy' === this.playFor(perf).type) {
      volumeCredits += Math.floor(perf.audience / 5);
    }

    // print line for this order
    result += `${this.playFor(perf).name}: ${format(thisAmount/100)}(${perf.audience} seats)\n`;
    totalAmount += thisAmount;
  }
  result += `Amount owed is ${format(totalAmount/100)}\n`;
  result += `You earned ${volumeCredits} credits\n`;
  console.log(result);
},
```

I compile­-test-­commit. With that inlined, I can then apply Change Function Declaration (124) to amountFor to remove the play parameter. I do this in two steps. First, I use the new function inside amountFor.

编译、测试、提交。完成变量内联后，我可以对 amountFor 函数应用改变函数声明（124），移除 play 参数。 我会分两步走。首先在 amountFor 函数内部使用新提炼的函数。

1『牢记变量内联。』

function statement…

```js
amountFor(aPerformance, play) {
  let thisAmount = 0;
  switch (this.playFor(aPerformance).type) {
    case 'tragedy':
      thisAmount = 40000;
      if (aPerformance.audience > 30) {
        thisAmount += 1000 * (aPerformance.audience - 30);
      }
      break;
    case 'comedy':
      thisAmount = 30000;
      if (aPerformance.audience > 20) {
        thisAmount += 10000 + 500 * (aPerformance.audience -20);
      }
      thisAmount += 300 * aPerformance.audience;
      break;
    default:
      throw new Error(`unkown type: ${this.playFor(aPerformance).type}`);
  }
  return thisAmount;
},
```

I compile-­test-­commit, and then delete the parameter.

top level…

```js
stateMent() {
  let invoice = invoices[0];
  let totalAmount = 0;
  let volumeCredits = 0;
  let result = `Statement for ${invoice.customer}\n`;
  const format = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2,
  }).format;
  for (let perf of invoice.performances) {
    let thisAmount = this.amountFor(perf);

    // add volume credits
    volumeCredits += Math.max(perf.audience - 30, 0);
    // add extra credit for every ten comedy attendees
    if ('comedy' === this.playFor(perf).type) {
      volumeCredits += Math.floor(perf.audience / 5);
    }

    // print line for this order
    result += `${this.playFor(perf).name}: ${format(thisAmount/100)}(${perf.audience} seats)\n`;
    totalAmount += thisAmount;
  }
  result += `Amount owed is ${format(totalAmount/100)}\n`;
  result += `You earned ${volumeCredits} credits\n`;
  console.log(result);
},
amountFor(aPerformance) {
  let thisAmount = 0;
  switch (this.playFor(aPerformance).type) {
    case 'tragedy':
      thisAmount = 40000;
      if (aPerformance.audience > 30) {
        thisAmount += 1000 * (aPerformance.audience - 30);
      }
      break;
    case 'comedy':
      thisAmount = 30000;
      if (aPerformance.audience > 20) {
        thisAmount += 10000 + 500 * (aPerformance.audience -20);
      }
      thisAmount += 300 * aPerformance.audience;
      break;
    default:
      throw new Error(`unkown type: ${this.playFor(aPerformance).type}`);
  }
  return thisAmount;
},
playFor(aPerformance) {
  return plays[aPerformance.playID];
},
```

And compile-­test-­commit again.

1『真是魔术般的消除了中间变量啊。』

This refactoring alarms some programmers. Previously, the code to look up the play was executed once in each loop iteration; now, it’s executed thrice. I’ll talk about the interplay of refactoring and performance later, but for the moment I’ll just observe that this change is unlikely to significantly affect performance, and even if it were, it is much easier to improve the performance of a well­factored code base.

这次重构可能在一些程序员心中敲响警钟：重构前，查找 play 变量的代码在每次循环中只执行了 1 次，而重构后却执行了 3 次。我会在后面探讨重构与性能之间的关系，但现在，我认为这次改动还不太可能对性能有严重影响，即便真的有所影响，后续再对一段结构良好的代码进行性能调优， 也容易得多。

The great benefit of removing local variables is that it makes it much easier to do extractions, since there is less local scope to deal with. Indeed, usually I’ll take out local variables before I do any extractions.

移除局部变量的好处就是做提炼时会简单得多，因为需要操心的局部作用域变少了。实际上，在做任何提炼前，我一般都会先移除局部变量。

Now that I’m done with the arguments to amountFor, I look back at where it’s called. It’s being used to set a temporary variable that’s not updated again, so I apply Inline Variable (123).

top level…

```js
stateMent() {
  let invoice = invoices[0];
  let totalAmount = 0;
  let volumeCredits = 0;
  let result = `Statement for ${invoice.customer}\n`;
  const format = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2,
  }).format;
  for (let perf of invoice.performances) {
    // add volume credits
    volumeCredits += Math.max(perf.audience - 30, 0);
    // add extra credit for every ten comedy attendees
    if ('comedy' === this.playFor(perf).type) {
      volumeCredits += Math.floor(perf.audience / 5);
    }

    // print line for this order
    result += `${this.playFor(perf).name}: ${format(this.amountFor(perf)/100)}(${perf.audience} seats)\n`;
    totalAmount += this.amountFor(perf);
  }
  result += `Amount owed is ${format(totalAmount/100)}\n`;
  result += `You earned ${volumeCredits} credits\n`;
  console.log(result);
},
```

1『 this.amountFor(perf) 替换了原来的 thisAmount。』

#### 1.4.2 Extracting Volume Credits

Here’s the current state of the statement function body:

Now I get the benefit from removing the play variable as it makes it easier to extract the volume credits calculation by removing one of the locally scoped variables. I still have to deal with the other two. Again, perf is easy to pass in, but volumeCredits is a bit more tricky as it is an accumulator updated in each pass of the loop. So my best bet is to initialize a shadow of it inside the extracted function and return it.

这会儿我们就看到了移除 play 变量的好处，移除了一个局部作用域的变量，提炼观众量积分的计算逻辑又更简单一些。我仍需要处理其他两个局部变量。perf 同样可以轻易作为参数传入，但 volumeCredits 变量则有些棘手。它是一个累加变量，循环的每次迭代都会更新它的值。因此最简单的方式是，将整块逻辑提炼到新函数中，然后在新函数中直接返回 volumeCredits。

function statement…

```js
function volumeCreditsFor(perf) { 
    let volumeCredits = 0; 
    volumeCredits += Math.max(perf.audience ­- 30, 0); 
    if ("comedy" === playFor(perf).type) volumeCredits += Math.floor(perf.audience 
    return volumeCredits; 
}
```

top level…

```js
stateMent() {
  let invoice = invoices[0];
  let totalAmount = 0;
  let volumeCredits = 0;
  let result = `Statement for ${invoice.customer}\n`;
  const format = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2,
  }).format;
  for (let perf of invoice.performances) {
    // add volume credits
    volumeCredits += this.volumeCreditsFor(perf);

    // print line for this order
    result += `${this.playFor(perf).name}: ${format(this.amountFor(perf)/100)}(${perf.audience} seats)\n`;
    totalAmount += this.amountFor(perf);
  }
  result += `Amount owed is ${format(totalAmount/100)}\n`;
  result += `You earned ${volumeCredits} credits\n`;
  console.log(result);
},
```

I remove the unnecessary (and, in this case, downright misleading) comment. I compile-test-­commit that, and then rename the variables inside the new function. function statement…

```js
volumeCreditsFor(aPerformance) {
  let result = 0;
  result += Math.max(aPerformance.audience - 30, 0);
  // add extra credit for every ten comedy attendees
  if ('comedy' === this.playFor(aPerformance).type) {
    result += Math.floor(aPerformance.audience / 5);
  }
  return result;
},
```

I’ve shown it in one step, but as before I did the renames one at a time, with a compile-test-­commit after each.

#### 1.4.3 Removing the format Variable

Let’s look at the main statement method again:

As I suggested before, temporary variables can be a problem. They are only useful within their own routine, and therefore they encourage long, complex routines. My next move, then, is to replace some of them. The easiest one is format. This is a case of assigning a function to a temp, which I prefer to replace with a declared function.

正如我上面所指出的，临时变量往往会带来麻烦。它们只在对其进行处理的代码块中有用，因此临时变量实质上是鼓励你写长而复杂的函数。因此，下一步我要替换掉一些临时变量，而最简单的莫过于从 format 变量入手。这是典型的「将函数赋值给临时变量」的场景，我更愿意将其替换为一个明确声明的函数。

function statement…

```js
format(aNumber) {
  return new Intl.NumberFormat('en-US', {
          style: 'currency',
          currency: 'USD',
          minimumIntegerDigits: 2,
        }).format;
},
```

top level…

```js
stateMent() {
  let invoice = invoices[0];
  let totalAmount = 0;
  let volumeCredits = 0;
  let result = `Statement for ${invoice.customer}\n`;
  for (let perf of invoice.performances) {
    volumeCredits += this.volumeCreditsFor(perf);

    // print line for this order
    result += `${this.playFor(perf).name}: ${this.format(this.amountFor(perf)/100)}(${perf.audience} seats)\n`;
    totalAmount += this.amountFor(perf);
  }
  result += `Amount owed is ${this.format(totalAmount/100)}\n`;
  result += `You earned ${volumeCredits} credits\n`;
  console.log(result);
},
```

Although changing a function variable to a declared function is a refactoring, I haven’t named it and included it in the catalog. There are many refactorings that I didn’t feel important enough for that. This one is both simple to do and relatively rare, so I didn’t think it was worthwhile.

尽管将函数变量改变成函数声明也是一种重构手法， 但我既未为此手法命名，也未将它纳入重构名录。还有很多的重构手法我都觉得没那么重要。我觉得上面这个函数改名的手法既十分简单又不太常用，不值得在重构名录中占有一席之地。

I’m not keen on the name—“format” doesn’t really convey enough of what it’s doing. “formatAsUSD” would be a bit too long­winded since it’s being used in a string template, particularly within this small scope. I think the fact that it’s formatting a currency amount is the thing to highlight here, so I pick a name that suggests that and apply Change Function Declaration (124). 

我对提炼得到的函数名称不很满意——format 未能清晰地描述其作用。formatAsUSD 很表意，但又太长，特别它仅是小范围地被用在一个字符串模板中。我认为这里真正需要强调的是，它格式化的是一个货币数字，因此我选取了一个能体现此意图的命名，并应用了改变函数声明（124）手法。

top level…

```js
stateMent() {
  let invoice = invoices[0];
  let totalAmount = 0;
  let volumeCredits = 0;
  let result = `Statement for ${invoice.customer}\n`;
  for (let perf of invoice.performances) {
    volumeCredits += this.volumeCreditsFor(perf);

    // print line for this order
    result += `${this.playFor(perf).name}: ${this.usd(this.amountFor(perf))}(${perf.audience} seats)\n`;
    totalAmount += this.amountFor(perf);
  }
  result += `Amount owed is ${this.usd(totalAmount)}\n`;
  result += `You earned ${volumeCredits} credits\n`;
  console.log(result);
},
usd(aNumber) {
  return new Intl.NumberFormat('en-US', {
          style: 'currency',
          currency: 'USD',
          minimumIntegerDigits: 2,
        }).format(aNumber/100);
},
```

Naming is both important and tricky. Breaking a large function into smaller ones only adds value if the names are good. With good names, I don’t have to read the body of the function to see what it does. But it’s hard to get names right the first time, so I use the best name I can think of for the moment, and don’t hesitate to rename it later. Often, it takes a second pass through some code to realize what the best name really is.

好的命名十分重要，但往往并非唾手可得。只有恰如其分地命名，才能彰显出将大函数分解成小函数的价值。有了好的名称，我就不必通过阅读函数体来了解其行为。但要一次把名取好并不容易，因此我会使用当下能想到最好的那个。如果稍后想到更好的，我就会毫不犹豫地换掉它。通常你需要花几秒钟通读更多代码，才能发现最好的名称是什么。

As I’m changing the name, I also move the duplicated division by 100 into the function. Storing money as integer cents is a common approach—it avoids the dangers of storing fractional monetary values as floats but allows me to use arithmetic operators. Whenever I want to display such a penny­integer number, however, I need a decimal, so my formatting function should take care of the division.

重命名的同时，我还将重复的除以 100 的行为也搬移到函数里。将钱以美分为单位作为正整数存储是一种常见的做法，可以避免使用浮点数来存储货币的小数部分，同时又不影响用数学运算符操作它。不过，对于这样一个以美分为单位的整数，我又需要以美元为单位进行展示，因此让格式化函数来处理整除的事宜再好不过。

#### 1.4.4 Removing Total Volume Credits

My next target variable is volumeCredits. This is a trickier case, as it’s built up during the iterations of the loop. My first move, then, is to use Split Loop (227) to separate the accumulation of volumeCredits.

top level…

```js
stateMent() {
  let invoice = invoices[0];
  let totalAmount = 0;
  let volumeCredits = 0;
  let result = `Statement for ${invoice.customer}\n`;
  for (let perf of invoice.performances) {
    // print line for this order
    result += `${this.playFor(perf).name}: ${this.usd(this.amountFor(perf))}(${perf.audience} seats)\n`;
    totalAmount += this.amountFor(perf);
  }
  for (let perf of invoice.performances) {
    volumeCredits += this.volumeCreditsFor(perf);
  }
  result += `Amount owed is ${this.usd(totalAmount)}\n`;
  result += `You earned ${volumeCredits} credits\n`;
  console.log(result);
},
```

With that done, I can use Slide Statements (223) to move the declaration of the variable next to the loop.

top level…

```js
stateMent() {
  let invoice = invoices[0];
  let totalAmount = 0;
  let result = `Statement for ${invoice.customer}\n`;
  for (let perf of invoice.performances) {
    // print line for this order
    result += `${this.playFor(perf).name}: ${this.usd(this.amountFor(perf))}(${perf.audience} seats)\n`;
    totalAmount += this.amountFor(perf);
  }
  let volumeCredits = 0;
  for (let perf of invoice.performances) {
    volumeCredits += this.volumeCreditsFor(perf);
  }
  result += `Amount owed is ${this.usd(totalAmount)}\n`;
  result += `You earned ${volumeCredits} credits\n`;
  console.log(result);
},
```

Gathering together everything that updates the volumeCredits variable makes it easier to do Replace Temp with Query (178). As before, the first step is to apply Extract Function (106) to the overall calculation of the variable.

function statement…

```js
totalVolumeCredits() {
  let invoice = invoices[0];
  let volumeCredits = 0;
  for (let perf of invoice.performances) {
    volumeCredits += this.volumeCreditsFor(perf);
  }
  return volumeCredits;
},
```

top level…

```js
stateMent() {
  let invoice = invoices[0];
  let totalAmount = 0;
  let result = `Statement for ${invoice.customer}\n`;
  for (let perf of invoice.performances) {
    // print line for this order
    result += `${this.playFor(perf).name}: ${this.usd(this.amountFor(perf))}(${perf.audience} seats)\n`;
    totalAmount += this.amountFor(perf);
  }
  let volumeCredits = this.totalVolumeCredits();
  result += `Amount owed is ${this.usd(totalAmount)}\n`;
  result += `You earned ${volumeCredits} credits\n`;
  console.log(result);
},
```

Once everything is extracted, I can apply Inline Variable (123):

top level… 

```js
stateMent() {
  let invoice = invoices[0];
  let totalAmount = 0;
  let result = `Statement for ${invoice.customer}\n`;
  for (let perf of invoice.performances) {
    // print line for this order
    result += `${this.playFor(perf).name}: ${this.usd(this.amountFor(perf))}(${perf.audience} seats)\n`;
    totalAmount += this.amountFor(perf);
  }
  result += `Amount owed is ${this.usd(totalAmount)}\n`;
  result += `You earned ${this.totalVolumeCredits()} credits\n`;
  console.log(result);
},
```

Let me pause for a bit to talk about what I’ve just done here. Firstly, I know readers will again be worrying about performance with this change, as many people are wary of repeating a loop. But most of the time, rerunning a loop like this has a negligible effect on performance. If you timed the code before and after this refactoring, you would probably not notice any significant change in speed—and that’s usually the case. Most programmers, even experienced ones, are poor judges of how code actually performs. Many of our intuitions are broken by clever compilers, modern caching techniques, and the like. The performance of software usually depends on just a few parts of the code, and changes anywhere else don’t make an appreciable difference.

首先，我知道有些读者会再次对此修改可能带来的性能问题感到担忧，我知道很多人本能地警惕重复的循环。但大多数时候，重复一次这样的循环对性能的影响都可忽略不计。如果你在重构前后进行计时，很可能甚至都注意不到运行速度的变化——通常也确实没什么变化。许多程序员对代码实际的运行路径都所知不足，甚至经验丰富的程序员有时也未能避 免。在聪明的编译器、现代的缓存技术面前，我们很多直觉都是不准确的。软件的性能通常只与代码的一小部分相关， 改变其他的部分往往对总体性能贡献甚微。

But “mostly” isn’t the same as “alwaysly.” Sometimes a refactoring will have a significant performance implication. Even then, I usually go ahead and do it, because it’s much easier to tune the performance of well­factored code. If I introduce a significant performance issue during refactoring, I spend time on performance tuning afterwards. It may be that this leads to reversing some of the refactoring I did earlierbut most of the time, due to the refactoring, I can apply a more effective performancetuning enhancement instead. I end up with code that’s both clearer and faster.

当然，「大多数时候」不等同于「所有时候」。有时， 一些重构手法也会显著地影响性能。但即便如此，我通常也不去管它，继续重构，因为有了一份结构良好的代码，回头调优其性能也容易得多。如果我在重构时引入了明显的性能损耗，我后面会花时间进行性能调优。进行调优时，可能会回退我早先做的一些重构——但更多时候，因为重构我可以使用更高效的调优方案。最后我得到的是既整洁又高效的代码。

So, my overall advice on performance with refactoring is: Most of the time you should ignore it. If your refactoring introduces performance slow­downs, finish refactoring first and do performance tuning afterwards.

The second aspect I want to call your attention to is how small the steps were to remove volumeCredits. Here are the four steps, each followed by compiling, testing, and committing to my local source code repository: 1) Split Loop (227) to isolate the accumulation. 2) Slide Statements (223) to bring the initializing code next to the accumulation. 3) Extract Function (106) to create a function for calculating the total. 4) Inline Variable (123) to remove the variable completely.

I confess I don’t always take quite as short steps as these—but whenever things get difficult, my first reaction is to take shorter steps. In particular, should a test fail during a refactoring, if I can’t immediately see and fix the problem, I’ll revert to my last good commit and redo what I just did with smaller steps. That works because I commit so frequently and because small steps are the key to moving quickly, particularly when working with difficult code.

I then repeat that sequence to remove totalAmount. I start by splitting the loop (compile­test­commit), then I slide the variable initialization (compile-­test-­commit), and then I extract the function. There is a wrinkle here: The best name for the function is “totalAmount”, but that’s the name of the variable, and I can’t have both at the same time. So I give the new function a random name when I extract it (and compile­-test-commit).

function statement…

```js
appleSauce() {
  let invoice = invoices[0];
  let totalAmount = 0;
  for (let perf of invoice.performances) {
    totalAmount += this.amountFor(perf);
  }
  return totalAmount;
},
```

top level…

```js
stateMent() {
  let invoice = invoices[0];
  let result = `Statement for ${invoice.customer}\n`;
  for (let perf of invoice.performances) {
    // print line for this order
    result += `${this.playFor(perf).name}: ${this.usd(this.amountFor(perf))}(${perf.audience} seats)\n`;
  }
  let totalAmount = this.appleSauce();
  result += `Amount owed is ${this.usd(totalAmount)}\n`;
  result += `You earned ${this.totalVolumeCredits()} credits\n`;
  console.log(result);
},
```

Then I inline the variable (compile­test­commit) and rename the function to something more sensible (compile­test­commit).

top level…

```js
stateMent() {
  let invoice = invoices[0];
  let result = `Statement for ${invoice.customer}\n`;
  for (let perf of invoice.performances) {
    // print line for this order
    result += `${this.playFor(perf).name}: ${this.usd(this.amountFor(perf))}(${perf.audience} seats)\n`;
  }
  result += `Amount owed is ${this.usd(this.totalAmount())}\n`;
  result += `You earned ${this.totalVolumeCredits()} credits\n`;
  console.log(result);
},
```

function statement…

```js
totalAmount() {
  let invoice = invoices[0];
  let totalAmount = 0;
  for (let perf of invoice.performances) {
    totalAmount += this.amountFor(perf);
  }
  return totalAmount;
},
```

I also take the opportunity to change the names inside my extracted functions to adhere to my convention.

function statement…

```js
totalAmount() {
  let invoice = invoices[0];
  let result = 0;
  for (let perf of invoice.performances) {
    result += this.amountFor(perf);
  }
  return result;
},
totalVolumeCredits() {
  let invoice = invoices[0];
  let result = 0;
  for (let perf of invoice.performances) {
    result += this.volumeCreditsFor(perf);
  }
  return result;
},
```

1『 Vue 里可以把「let invoice = invoices[0]」放进 data 数据里，这样不用每个函数都重新声明。』

### 1.5 Status: Lots of Nested Functions

Now is a good time to pause and take a look at the overall state of the code:

```js
stateMent() {
  let invoice = invoices[0];
  let result = `Statement for ${invoice.customer}\n`;
  for (let perf of invoice.performances) {
    // print line for this order
    result += `${this.playFor(perf).name}: ${this.usd(this.amountFor(perf))}(${perf.audience} seats)\n`;
  }
  result += `Amount owed is ${this.usd(this.totalAmount())}\n`;
  result += `You earned ${this.totalVolumeCredits()} credits\n`;
  console.log(result);
},
totalAmount() {
  let invoice = invoices[0];
  let result = 0;
  for (let perf of invoice.performances) {
    result += this.amountFor(perf);
  }
  return result;
},
totalVolumeCredits() {
  let invoice = invoices[0];
  let result = 0;
  for (let perf of invoice.performances) {
    result += this.volumeCreditsFor(perf);
  }
  return result;
},
usd(aNumber) {
  return new Intl.NumberFormat('en-US', {
          style: 'currency',
          currency: 'USD',
          minimumIntegerDigits: 2,
        }).format(aNumber/100);
},
volumeCreditsFor(aPerformance) {
  let result = 0;
  result += Math.max(aPerformance.audience - 30, 0);
  // add extra credit for every ten comedy attendees
  if ('comedy' === this.playFor(aPerformance).type) {
    result += Math.floor(aPerformance.audience / 5);
  }
  return result;
},
amountFor(aPerformance) {
  let result = 0;
  switch (this.playFor(aPerformance).type) {
    case 'tragedy':
      result = 40000;
      if (aPerformance.audience > 30) {
        result += 1000 * (aPerformance.audience - 30);
      }
      break;
    case 'comedy':
      result = 30000;
      if (aPerformance.audience > 20) {
        result += 10000 + 500 * (aPerformance.audience -20);
      }
      result += 300 * aPerformance.audience;
      break;
    default:
      throw new Error(`unkown type: ${this.playFor(aPerformance).type}`);
  }
  return result;
},
playFor(aPerformance) {
  return plays[aPerformance.playID];
},
```

The structure of the code is much better now. The top­level statement function is now just seven lines of code, and all it does is laying out the printing of the statement. All the calculation logic has been moved out to a handful of supporting functions. This makes it easier to understand each individual calculation as well as the overall flow of the report.

顶层的 statement 函数现在只剩 7 行代码，而且它处理的都是与打印详单相关的逻辑。与计算相关的逻辑从主函数中被移走，改由一组函数来支持。 每个单独的计算过程和详单的整体结构，都因此变得更易理解了。



# 2019030Refactoring2EdR00

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

Refactoring (noun): a change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its observable behavior. This definition corresponds to the named refactorings I’ve mentioned in the earlier examples, such as Extract Function (106) and Replace Conditional with Polymorphism (272). Refactoring (verb): to restructure software by applying a series of refactorings without changing its observable behavior. So I might spend a couple of hours refactoring, during which I would apply a few dozen individual refactorings.

重构（名词）：对软件内部结构的一种调整，目的是在不改变软件可观察行为的前提下，提高其可理解性，降低其修改成本。重构（动词）：使用一系列重构手法，在不改变软件可观察行为的前提下，调整其结构。

书里对重构这个词进行了阐释：重构 !== 更改，尤其是不等于影响函数正常工作的更改。在作者的概念体系里，重构是小步的、不影响函数行为的迭代式更改，嗯，跟敏捷的概念有点像。重构跟性能优化很像：都是修改代码且不影响行为。但前者是为了理解、便于修改；后者是为了性能而改。关于重构和加新功能的配合，作者把它们比喻成两顶帽子 —— 你戴或者不戴，什么时候戴，都随你，但是你要清楚自己戴着哪一顶帽子。

重构的时机，在书中看来，应该是不得不重构时：譬如添加新功能前，重构能让修改更容易；帮助自己理解代码时，重构能让代码更易懂；捡垃圾时，重构可以改掉屎一样的代码（你懂的）。同样，也有不需要重构的时候：比如这段代码凌乱但是跟我无关、也不需要修改或是在某个隐藏得很好的 API 下。又或者重写更容易，那就重写吧。

另外，关于变量命名的经验：作者喜欢把所有返回值变量命名成 result，学到了 —— 这样能一眼就知道变量的作用。以及，因为 JavaScript 是动态类型语言，所以作者喜欢在变量命名里加类型，尤其是加入不定冠词，比如 aPerformance。

### 0202. 术语卡——两顶帽子

Kent Beck came up with a metaphor of the two hats. When I use refactoring to develop software, I divide my time between two distinct activities: adding functionality and refactoring. When I add functionality, I shouldn’t be changing existing code; I’m just adding new capabilities. I measure my progress by adding tests and getting the tests to work. When I refactor, I make a point of not adding functionality; I only restructure the code. I don’t add any tests (unless I find a case I missed earlier); I only change tests when I have to accommodate a change in an interface.

KentBeck 提出了「两顶帽子」的比喻。使用重构技术开发软件时，我把自己的时间分配给两种截然不同的行为：添加新功能和重构。添加新功能时，我不应该修改既有代码，只管添加新功能。通过添加测试并让测试正常运行，我可以衡量自己的工作进度。重构时我就不能再添加功能，只管调整代码的结构。此时我不应该添加任何测试（除非发现有先前遗漏的东西），只在绝对必要（用以处理接口变化）时才修改测试。

As I develop software, I find myself swapping hats frequently. I start by trying to add a new capability, then I realize this would be much easier if the code were structured differently. So I swap hats and refactor for a while. Once the code is better structured, I swap hats back and add the new capability. Once I get the new capability working, I realize I coded it in a way that’s awkward to understand, so I swap hats again and refactor. All this might take only ten minutes, but during this time I’m always aware of which hat I’m wearing and the subtle difference that makes to how I program.

软件开发过程中，我可能会发现自己经常变换帽子。首先我会尝试添加新功能，然后会意识到：如果把程序结构改一下，功能的添加会容易得多。于是我换一顶帽子，做一会儿重构工作。程序结构调整好后，我又换上原先的帽子，继续添加新功能。新功能正常工作后，我又发现自己的编码造成程序难以理解，于是又换上重构帽子……整个过程或许只花 10 分钟，但无论何时我都清楚自己戴的是哪一顶帽子，并且明白不同的帽子对编程状态提出的不同要求。

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

### 0601. 任意卡——重构时机三原则

Here’s a guideline Don Roberts gave me: The first time you do something, you just do it. The second time you do something similar, you wince at the duplication, but you do the duplicate thing anyway. The third time you do something similar, you refactor. Or for those who like baseball: Three strikes, then you refactor.

Don Roberts 给了我一条准则：第一次做某件事时只管去做；第二次做类似的事会产生反感，但无论如何还是可以去做；第三次再做类似的事，你就应该重构。正如老话说的：事不过三，三则重构。

重构的最佳时机就在添加新功能之前。在动手添加新功能之前，我会看看现有的代码库，此时经常会发现：如果对代码结构做一点微调，我的工作会容易得多。也许已经有个函数提供了我需要的大部分功能，但有几个字面量的值与我的需要略有冲突。如果不做重构，我可能会把整个函数复制过来，修改这几个值，但这就会导致重复代码——如果将来我需要做修改，就必须同时修改两处（更麻烦的是，我得先找到这两处）。而且，如果将来我还需要一个类似又略有不同的功能，就只能再复制粘贴一次，这可不是个好主意。所以我戴上重构的帽子，使用函数参数化（310）。做完这件事以后，接下来我就只需要调用这个函数，传入我需要的参数。

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
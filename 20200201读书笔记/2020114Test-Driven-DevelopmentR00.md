## 记忆时间

## 卡片

### 0101. 主题卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——TDD

Readers of Extreme Programming Explained will notice a difference in tone between XP and TDD. TDD isn’t an absolute like Extreme Programming. XP says, “Here are things you must be able to do to be prepared to evolve further.” TDD is a little fuzzier. TDD is an awareness of the gap between decision and feedback during programming, and techniques to control that gap. “What if I do a paper design for a week, then test-drive the code? Is that TDD?” Sure, it’s TDD. You were aware of the gap between decision and feedback and you controlled the gap deliberately.

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。

#### 01. 基本信息

用一句话描述你对这个大牛的印象。

#### 02. 贡献及著作

### 0401. 金句卡——TDD is an awareness of the gap between decision and feedback during programming, and techniques to control that gap

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

## 书评

### 01

这是一本天才写的书，开创了新的软件方法论。这是一本 200 页的薄书，但以前所有软件工程的几十万页的书加在一起，应该也只与这本书的份量相当。以前软件工程的书只是对几千年的工程传统的不成功的拷贝和 YY，但这本书写了程序自己的方法学，与和程序员自己的方法学。以前软件工程的方法，说白了就是包工头管基建的方法。所以，一个好的项目经理，常常不需要是一个好的程序员。这样管理下的程序员，与民工（严格地说是小工）也没有什么区别。

测试驱动开发，就是先写测试，再写程序，颠覆了先写程序再做测试的传统。优点是：1）需求是明确的。2）程序是符合需求的。3）程序的高内聚低耦合的。传统方法中的不可企及的目标现在只是理所当然的结果。4）程序是胆小怕事的程序员也敢修改的。5）程序是久经测试的。6）测试是自动的。但是，为了「拥抱变化」，只有测试驱动开发是不完整的，当需求变化需要修改代码时，有时仅仅局部增加代码是不行的。测试驱动开发需要加上重构 refactor 才是完整的开发方法，才能修改好代码。所以学习这本书还应该学习 refactor。

这本书通过一个个的例子的演化来说明重大的思想，基本采用的是 java 代码，所以，尽管学习这本书让人脱胎换骨，但学习过程不需要读者下苦功而是非常愉快。这本书的部分例子采用了 python 代码，虽然不另学 python 也能顺利读完这本书，但不学 python 毕竟不能实践书中的例子。为了真正欣赏这本书，学习一点 python 是值得的。当然，一个程序员，学习 python 本身就很值。

### 02

这本书的作者是「极限编程」之父 Kent Beck，书写得很薄，每一章都只有几页的长度。这就好像用 TDD 方法写出的代码般，每一个单元都是精巧明快的，使得人们很容易读懂，也使人们更有意愿将其读懂。加之作者的笔调也十分轻松，这种小薄册要比那些百科全书式的大部头读起来舒服许多。

第一部分讲了一个支付系统中支持多币种需求的例子。作者以很慢的节奏来讲解 TDD 的过程，这节奏慢到甚至让我有一点难以接受，然而当着个例子最终完成的时候，回头看看整个开发过程，感觉如作者所述，不觉间竟然已经走出了这么长的一段距离。个人感觉，假如以传统的先设计再编码的方式开发，除非是非常非常有经验的程序员，否则很容易会得到不符合需求的设计或者花过多精力在需求之外的设计上编码。

第二部分是一个十分特别的例子。一种「提靴带」的开发方式：用 xUnit 测试框架来测试驱动开发 xUnit 本身。似乎这种模式只在编译器的开发中存在。从无到有，神奇之至。就好像 xUnit 被作者注入了神奇的 DNA，然后使命般地自我演化生长出一个优秀的单元测试框架。我这么说可能有些夸张了。我并不认为实际的开发工作中会有这么美妙的设计过程。作者作为 JUnit 的开发者之一，对这套框架自然是了然于胸，设计起来也一定会有举重若轻之感。虽然我没学过 Python，但也能跟着作者的「YY 思路」一同前行。

第三部分作者揭示了测试驱动开发的模式。这部分有些稍有些「政治课本」的味道了，但依然不失风趣。有了前面两个例子的铺垫，理解起来也相对容易些了。其中包含了 TDD 的实践原则（不可运行、可运行、重构）和 TDD 指导编码的技巧（「设计模式」和「重构」两章）。当读者有了更多的实践和经验，重读这部分会得到更多的体会。

TDD 之所以有效率，是因为它使程序员的注意力完全集中于现有的需求，不必过多考虑变化。凡是参加过英语考试的人几乎都知道这样一个应试技巧：做阅读理解题的时候，先看问题然后去原文找答按要比通读全文再看问题做答能更快更准确地答完。这是因为看问题找答案使考生将精力集中到「现有的考试需求」上，回头阅读原文的时候自然而然地忽略掉与问题无关的词句，迅速找到问题相关的段落，提炼出答案。这就是测试驱动开发。我们只需要为现有的需求编写对应的测试用例，然后努力使这些用例通过测试。

TDD 有效率的另一方面就是自动化单元测试。这是程序员给代码上的保险。作者在书中打了个比喻，TDD 就像是井绳上的防滑扣，它在你没有了力气或者不慎手滑时不会使得吊桶跌落井底。想象一个没有使用 TDD 方法的项目，由于设计并没有基于项目自身的需求实践，而是基于设计者的经验和推断，在编码阶段，开发人员就会经常一步三回头地回顾设计，并且针对实际编码中遇到的问题做出一些修改；在集成测试阶段以及最终发布之后，没有单元测试用例，在发现 Bug 时，找出 Bug 的成因就成了一个艰难的任务。单元测试是从需求的实际出发，通过一点一点实践向前推进的，在编码的同时，也就将部分 Bug 限定了活动范围；而且单元测试迫使程序员写出便于测试的代码，便于测试的代码，就是的低耦合的代码，一块一块短小清晰的代码要比一坨一坨冗长纠结的代码更容易阅读；自动化测试使测试的成本降低，程序员的每次推进都有会得到快速的检验，前期花在自动化上的工作是值得的，「一次投保，终身收益」；在发现 Bug 或者遇到需求变更时，程序员也能很快定位问题，因为测试用例给了程序员解决问题的线索，更给了程序员拥抱变化的勇气。

测试驱动开发，是一种很人性化的开发方法。其中包含了很多心理学因素。它给了程序员勇气。即使不是基本功扎实程序员，也能用这种方法开发出好的程序（看一下书中附录 B 那个用 TDD 方法开发的 Fibonacci 数列程序，是不是觉得有些好笑？但回顾你第一次写 Fib 时的情景，是不是有似曾相识的感觉？）；它使程序员能把问题管理好，使得代码是新鲜的、干净的、可控的；测试用例也量化了项目开发的进度，项目如期交付变得可能。

一直以来，我都有这样一个愿景：程序员们不再需要加班，不用再每天盯着显示器焦头烂额，不再有产品交付前的 Debug 炼狱，不再时常被发布版 Bug 噩梦惊醒，每晚睡得踏实，每天 8 小时上班，我们可以一边喝着香醇的咖啡茶一边远望窗外的美丽风景，当自动测试报告出来后，我们能对着它微笑，然后轻松处理其中的每一个问题。我不敢说 TDD 能够实现这个愿景，但至少它给了我实现这愿景的希望。

### 03

如果只是想单纯地了解一下 TDD（粗浅了解一下 TDD 的实现步骤，以及它充满吸引力的优点），那么看看第一部分（Section I: Money Example）就可以。如果正在进行 TDD，或已经有了一些 TDD 实践，那么可以看看这本书的第二，第三部分，这对 TDD 的在项目中的具体实践和对提高 TDD 的认识会很有帮助。看完这本书也改变了我一些固有印象，其实 TDD 不是绝对和极限编程一样。书中有一句话令人印象深刻：TDD is an awareness of the gap between decision and feedback during programming, and techniques to control that gap.

书中常常提到 The goal is clean code that works. 我非常赞同，其实不管使用什么选择的开发策略（或者是否认可使用 TDD，我的很多朋友就不是很认可 TDD），其实我们的目的都是写出「整洁」的代码得到使我们的软件在质量和产出方面，得到可观的改善。

### 04

思想很好，传统开发模式下顾问、项目经理管需求，资深开发者、设计者进行分析设计，程序员负责开发，一方面带来项目管理、项目风险诸多问题，另一方面也造就大量「不负责任」的程序员，妨碍程序员综合能力的提升、思维和视角的拓展。TDD 下程序员直接面对需求、用例，参与设计，以测试为主题进行驱动，能够比较好的解决这些矛盾，在思想指导层面的确意义重大。针对复杂业务系统、基础框架进行设计，思维在流程、模块、架构、整体与细节之间穿梭时，常常遇到很多问题理不清思路，利用 TDD 的方式对这种状况很有帮助。

TDD 的主要思想和运用方式讲解起来比较简单，开始几章用例子来讲解就安排的很不错，非常通俗易懂。后面弄出来这样那样的模式感觉比较牵强，如果作者将自己多年的 TDD 实践经验进行总结、整理，针对各个点配合一些实际场景进行讲解说明，比使用模式的方式要好。另外一点在实际项目中，如何从一开始在团队中实施 TDD 流程，以 TDD 思想进行分析以及任务分解，督促团队成员以 TDD 进行开发，这一整体面的东西书中并没有讲到，是一个缺憾。

### 08

Kent Beck 关于 TDD 的名言：测试驱动开发非常适合那些对代码情有独钟的呆子们。我年轻时软件工程生活的一项最令人痛楚的事情就是满怀热情的开始一个项目，然后看着代码随着时间的流失逐渐腐烂。一年后我只想丢掉已经变味的代码，转到开发别的项目中去。测试驱动开发能让你随着时间的流逝对代码依然信心依旧。随着测试的累计和改进，你对系统的行为充满自信。在你改进设计的时候，有可能进行越来越多的改动。我的目标是一年之后对项目拥有更透彻的把握，而不像刚开始时满脑子充满不切实际的幻想。测试驱动开发帮助我实现了这一切。

书比较小巧，几天可以看完。按照目录分的话，可以分三部分。第一部分是一个简单的实例，从一个简单的例子入手讲解 TDD，读起来有点罗嗦，但是很快不知不觉我们的第一个例子已经完成了。或许这就 TDD 的思想，每一小步都很小，但是当我们回头时，发现我们已经走了很远。第二部分是以开发 XUnit 为例介绍 TDD。第三部分，讲的是关于 TDD 相关的经验。所有的这些经验在我们未使用 TDD 之前都能在现实中找到实例，而这些经验同时也能很容易联想到书中前面的两个实例。不知不觉你已经完全掌握 TDD 了。恐怕这是为数不多通俗易懂的书了，读的时候，你几乎不需要停留下来的去思考那些看不懂的地方。更可贵的是，读完之后，TDD 你已经很了解了，剩下的事情就是放手去实践了。

如果你有随着项目的不断增大，维护修改起来日益困难，几乎让人发疯的经历。你会 TDD 能拯救我们。引用 Beck 的话：测试驱动开发帮助我实现了这一切。

### 10

TDD 的内容组织：1）讲述经典的 Money 例子，基本就是代码重构的内容。——有空还是去看原书比较好。2）如何实现一个 xUnit 的框架。——直接找一个跟自己语言对应的 xUnit 来学习就可以了，没有必要唧唧歪歪的看作者说半天。3）TDD 里常用的一些模式。——也就是惯常的技巧，喜欢叫做模式也行。这里没有太多的废话代码，还比较抽象和概括，值得一看。不过后面的设计模式和重构，就是鸡肋了。

好吧，TDD 的原理其实很简单：1）写代码之前，先写测试用例。2）想办法让测试用例通过，哪怕写假的代码。3）用真的代码替换掉假的代码，并使得测试用例通过。4）重构让代码优化，同时让测试用例。

测试用例的好处：1）帮助你做设计，首先从最后结果，或者使用者的角度来看问题，到底应该怎样封装和提供接口。2）为了能够写出测试用例，你会发现模块的依赖，并尽量分离，以使得测试用例可以进行。3）测试用例是你信心的保证，你不用担心修改会不小心对其它部分产生了影响。因为，只要测试用例过了，就说明一切 OK。有了这样的保障，你就会更加勇往直前。

### 11

测试驱动开发是否是软件开发的银弹，答案是否定的，但是其作用是值得重视的。现在的有一种趋势是弱化设计驱动，设计尽量简单，设计范围尽量减少。在「测试驱动」过程中重构，深化设计，验证结果。这是不是有效率呢？是不是符合软件开发实际呢？还是件需要思考的事情。如何把设计和测试结合呢？是一步一步从最简单的方式推演，还是先「想全面」了再 coding 呢？哪个更好，恐怕不能简单地说前者优于后者，要看是否适合具体个体或是团体。

测试驱动的动机是整合「设计」到「测试」代码中，通过测试代码来设计，过程就是否定之否定，最后得到一个相对肯定结果，可以看作是一种「设计」的思路。如何驾驭这个过程就要看个人能力了，没有功力最后还是百搭。同样，如果用相反的思路呢？那就是「设计」驱动「测试」，通过设计过程中的 use story 来生成测试用例，即所谓的 BDD 行为驱动开发（见《实例化需求》）。我更欣赏 BDD，感觉 TDD 是「反人类」的做法。总之不是任何人，任何团队都适合测试驱动的。尽管如此，作者写的测试实战经验和工作习惯是值得借鉴和学习的。

### 12

最近开发了两周的项目上线了（ 对，又是开源项目改吧改吧就上线了） 开发任务突然没有了，而我，每天却要写日报，所以我又想起了多年前的愿望，试一试怎么写测试。这样日报也有的写，还可以提高项目的单元测试率，面试的时候还能说为一个开源项目提供过 commit，美滋滋。

为了开始工作，先要开始学习，于是看了一本书叫 Test Driven Developmemt by Examples ，里面别的重构什么的印象不深，但是我至少明白了一个道理。就是单元测试，核心是把这些函数，方法，分割开来，然后逐个的进行步骤上的测试，测试有没有达到预期的效果，这个重点在于过程而不是结果，因为如果只看结果的话，如果一个庞大的系统得到的结果不符合预期，其实很难说到底是哪里出问题了。

这个概念从小处出发去测试系统的正确性，确实是很有趣的一种想法。但同时，他真的也很智障。为什么这么说呢，我写了两天的测试，我觉得我写的都是智障测试，举个例子，有一个系统，是用来算地球和太阳的总质量的，这个系统大概分为 3 部分：1）称地球的质量。2）称太阳的质量。3）把两个质量加起来。

其中第一步和第二步是派科学家去称的，这些称为外部接口，getSunMass() 、getEarthMass()，那么我们要测试的是第三步，我们怎么样进行测试呢，就是模拟出来两个假系统 / 假科学家 ，去装作称了太阳和地球的质量，因为实际称是要花费时间和精力的，测试一次，就要称一次，当然是不可接受的，所以我们假装出来两个函数 mockSunMass()、mockEarthMass() 来假装进行了这两次测试，然后再把这些质量加起来，总质量算出来了！最后校验我们的总质量是不是这两个假装结果的和，校验我们的这两个 mock 函数有没有被调用，那么就这样，一个单元测试就完成了，在这个测试里，我们基本上就是测试了一个加法。没错，就是这么的智障。第一步和第二步呢，我们可以努力把它拆成更小的能测试的单位，进行同样的测试。

当你在写单元测试的时候，你更是觉得智障了，因为程序里很多东西都没有加法的，里面就是单纯的 if 如果 i > 0 如何如何，所以基本上就是你写一个输入值，然后运行一次你要测试的函数，然后判断返回和预期返回是否一致。有多少次判断，就写多少次测试。最终的结果就是，20 行的代码，因为有 5 个判断，我写了 120 行的测试程序。还有一个测试的智障点就是，大多数的程序，都不是有一个输入源，一个返回值这么简单的，中间你还要去调用数据库，调用一些内部程序等等，而为了达到「单元」的效果，对于外部的调用需要尽量屏蔽，也就是不让它实际去调用这些程序，特别是数据库，网页抓取，发送邮件，等等耗时很长的工作。而这些屏蔽，会让你的测试代码更长。

我，作为一个新手，撸了两天测试，把单元测试覆盖率从 27% 提高到了 33% ，这花了整整两天，300 多行的测试代码，而整个项目也才 5000 行的 python 代码。但是毋庸置疑，单元测试，测试驱动开发，我感觉还是有趣而且靠谱的，相比我之前「用心测」的集成测试 ，随手点击个按钮，这些 all tests passed 的感觉还是很安心。不知道单元测试在团队开发时会是什么样，我记得之前还看过一个说单元测试的，说项目虽然有单元测试，但是每次测试都失败，不过没关系，只要没通过的单元测试数量和之前的一样就可以了。虽然智障，但是真的让我在测试不通过的时候发现了系统的一些 bug，比如没有对负整数的端口号进行校验，端口号如果说字符串会报错，之类的。总的来说，虽然智障，但还是很有用的工具。

1『直觉上该评论这没有领悟测试的精髓。回复：不是先写好代码在写测试，测试驱动开发的关键在于「驱动」，想着如何写出好测试的代码，你觉得难写测试是你的方法不对，再比如提到的数据库的地方难写，可以用模拟数据来取代，只要接口保持一致就行。（2020-06-15）』

### 13

测试开发驱动模式：

1、测试优先，断言优先。从哪里开始构建一个系统：从对所有系统的描述开始。1）列一个测试列表，一个个解决，后续有问题再加入列表。从哪里开始着手编写一些功能，从对已完成运行的测试开始。2）为每一个列表写一个测试用例（实质是为某一个令你困恼的点写测试用例）。从哪里开始编写测试，从断言开始。

2、隔离测试（Isolate Change）。保持测试的顺序无关且不影响彼此。最好一个测试未通过只代表一个问题。（切分问题）

3、让测试尽可能快的运行起来。这里讲到了两种方式，伪实现和三角测量法。1）伪实现：返回一个常量，逐渐使用变量取代它直到代码实现。2）三角测量法：编写某一个具体实现的用例，只当有两个或更多例子的情况下，才对其代码进行泛化。

4、选择测试数据的准则：那些使测试易读性强且易于理解的数据，而且现实世界中的真实数据优先。

5、显式数据（常量）：帮忙理解测试本身的期望结果和实际结果，并尽量让它们的关系明朗。

测试的流程：红色指示条 —— 绿色指示条 —— 重构（去掉开发余测试中的重复代码），以此循环。在没有测试失败情况下，不要去修改开发代码。（因为新变更，总是先写测试）

### 15

If I get stuck and I don't know how a complex algorithm should work I'll write a test for an error case. Then I'll write a test for the simplest non-error case I can think of and return a hard coded value. Then I'll write another test case and see if I can figure out the algorithm at that point. In doing so I gain some momentum and perhaps some insight in how the algorithm should behave on an edge case and a few normal cases.

This is called triangulation and it was used in celestial navigation for thousands of years. It is easier to see you are moving when you compare your position to two or more points on the horizon rather than just one. The same applies to coding; it is often easier to figure out the behavior of an algorithm by examining a couple of test cases instead of just one.

Triangulation is a valuable problem solving technique in TDD but it can also create its own problems. Once we figure out what we need from multiple tests they no longer serve any purpose and they become redundant tests. Redundant tests are tests that do not create any new distinctions.

If we recognize that redundancy in code is a maintenance issue then we should also see that redundancy in tests is also a maintenance issue. The purpose of QA is to try to break code to verify that it is robust. The purpose of TDD is to express the intent of code in as few tests as possible. Therefore, part of refactoring a system is removing redundant tests.

### 16

1、刚开始看的时候，很纳闷，难道作者在教学校生作文啊？那个小那么小的一步前进，我们还要不要写软件了？后来看到了这样一句话，there is no right step size, now and forever，我明白了，作者只是给出了一个方法，至于实施过程的具体细节，每个人要根据自己的情况和软件的情景来设定的。

2、测试驱动开发的本质是什么？我觉得先写 test case 很大程度上是帮助我们更清楚的认识问题，当问题清楚明确，又具体的定义，那么解决问题就只是一个流程了，所以，大部分时候不是问题很难解决，而是问题很难被具体的定义，写 case 可以帮我们解决一部分这个问题。

3、现实中的开发如何借用呢？现实中我们可以一直在用书上提到的方法，只是没有明确的给出定义或者没有明确的按照上面流程来罢了。在现实的开发中，我们也是先设计，然后做详细规划，觉得差不多了，就开始写代码，然后边写边改，。。。最后完成，然后写个测试用例来测试，pass，一切 ok。这么做最可能的问题是，当我们完成某个功能的时候，位于兴奋中，我们可以就不愿意思考出有效充分的用例来测试我们得程序，我们总觉得：不会有问题的。这其实是个心理问题了，人当然不愿意否定自己，而写完程序之后写测试用例就是否定自己（怀疑有问题才写测试嘛），所以写完程序再写测试 case 是不太合理的。以后还是要先写测试 case 再写程序，当然未必想作者说的那么详细。

4、写完一段程序就思考一会，想想是不是有问题。这点尤其有用，我的经验显示，这对于程序的改进很有价值。

5、其实 TDD 只是一种方法，这种方法强迫我们去拿出时间认真的思考问题，哪怕是个很小，看起来很简单的问题。也就是，TDD 帮助我们更好的进行问题定义。

6、TDD 在实施的过程中，也带来一些其他好处。可以让接口尽快稳定下来，因为我们在写 test case 的时候，潜在的充当了 caller 的角色，这就要求我们对自己的接口有个比较实际的认识过程，这对接口的合理性有帮助。

7、感叹作者说的话：「如果逻辑看起来真的很简单，那么就直接写吧」，这跟我刚开始看这本书的想法不谋而合。这本书是个方法，而绝不是让我们亦步亦趋的跟着做，那样的话，根本谈不上效率。

8、我得承认有些人是不需要 TDD 的，我们公司有一个，这些人在写之前已经将该考虑的问题都考虑了，TDD 对他们而言实在是浪费。

### 17

1、我看到有同学写 TestCase 的时候喜欢使用全局变量，这样做是可以，但是最好使用 const modifier，否则，Test case 之间会互相影响，甚至各个 test cases 之间的调用顺序会影响结果，这是很不好的，因为 Test cases 设计本身不是为了代码优美，是为了确保特定的需求。

2、继续领会 TestDriven 的精神。Testcase 的设计帮助我们更加全面的思考问题以及解决方案，强迫我们拿时间去思考问题的细节。当碰到一个问题的时候，我们很容易会得出模糊的设计，然后一边细化设计，一边开始编码，同时发现了不合理的地方，开始修改设计。。。这个流程本身并不算错误，特别是 XP 盛行以来。问题的关键是，我们是不是真的能确保「尽可能少」的在实现的过程中修改设计呢？先设计出测试方案会对这个问题有帮助的，这很类似一种 Top-Down 的方法学。所以，TestCase 是个「好客户」，他帮助我们梳理需求，并验证我们的实现。

3、以前似乎看到过 XP 和 TDD 的争议。我觉得他们一点都不矛盾，是互为辅助的关系。XP 的根本目的是快速了解需求，快速实现，重构，最后给出好的结果，而 TDD 的目的是帮助我们快速了解需求，思考实现，可以说 TDD 会辅助 XP，使得其降低重构的代价。

4、我一直觉得我有这样的特点，就是写程序的时候专心写程序，然后碰到什么事情了（比如出去吃饭），因为不能继续写程序了，所以就仔细思考一下刚才的程序，这时候常常能发现问题，或者更好的设计。也就是说，在写程序的过程中回头思考是有好处的，可是如果让我专心的写程序（没人打扰我，没有事情打扰我），我是不愿意主动停下来的，这是个挺奇怪的现象。TDD 部分的帮助我改变了这个习惯，运行 TDD 的时候我还是可以选择思考一下的，呵呵。

5、作者提出 TDD 的一个 Case 尽可能小，这个显然不一定的。比如我们要写个复杂的算法，显然算法是一个整体，不可能拆解下来分布进行测试，这么做也会影响思路的。所以，结论是明显的，没有规则，只有和实践匹配的方法，只要跟我们的环境合适，Caes 的大小和多少是可以自己控制的。

6、不要再去开会或者做其他事情之前匆忙完成代码，但是这个时候也许我们可以将 test case 写完。

### 18

留下印象的是在前言里写的 TDD 两个原则：不要重写代码，除非 test fail 了；去除重复设计，优化代码结构。以及「不要过多的设计，只要满足 test pass 即可」—— 当现有设计不满足新功能时（即新的 test failure），才修改设计。

正本书先从一个币种汇率转换为例子，说明 TDD 如何实施，然后说明了如何写 Test 以及如何重构。笔者觉得，TDD 除了 validation 作用外，更多的是帮助你思考如何设计以及作为永不过时的 specification，还有就是能让你更有信心的 refactor。所以，本书在介绍完 TDD 基本知识以及流程后，花了大量笔墨教读者如何写出 clean code 以及 refactor，这部分笔者直接跳过了，笔者认为写出 clean code 和如何 refactor 是 TDD 之外的领域，所以自认为这方面的知识更适合去阅读 clean code 以及 refactor 这两本书。

## 译者序

测试驱动开发（TDD）以测试作为开发过程的中心，它要求在编写任何产品代码之前，首先编写用于定义产品代码行为的测试，而编写的产品代码又要以使测试通过为目标。测试驱动开发要求测试可以完全自动化地运行，在对代码进行重构前后必须运行测试。这是一种革命性的开发方法，能够造就简单、清晰、高质量的代码。

测试驱动开发是一种我们编程时使用的技术。无论我们在开始编程之前进行了怎样的设计和建模，TDD 都有助于我们提高代码质量。测试驱动开发可以赋予你对代码质量的自信以及对代码进行重构的勇气。试想如果没有办法保证我们对可运行代码的修改不会破坏任何先前的行为，那么怎么能够对代码进行修改？如果对代码的重构或修改无意中引入了 bug 但却没有一套可以立刻把这种情况告诉你的测试集，那么怎么能够进行集成？

测试驱动开发是一种在极限编程（XP）中处于核心地位的技术。要想采用极限编程过程，熟练掌握测试驱动开发将会有莫大的帮助。即便你选用的软件开发过程不是 XP，测试驱动开发也能让你从中获益。采用测试驱动开发，我们将会得到简单、清晰的设计，我们的代码也将是清晰和 bug-free 的。同时采用测试驱动开发的结果就是可以让我们拥有一套伴随产品代码的详尽的自动化测试集。将来无论出于什么原因（新的需求，变化了的需求，性能调整等等）需要对产品代码进行维护时，在这套测试集的辅助（驱动）下工作，我们的代码将会一直是健壮的。

## Preface

Clean code that works, in Ron Jeffries’ pithy phrase. The goal is clean code that works, and for a whole bunch of reasons: 1) Clean code that works is a predictable way to develop. You know when you are finished, without having to worry about a long bug trail. 2) Clean code that works gives you a chance to learn all the lessons that the code has to teach you. If you only ever slap together the first thing you think of, you never have time to think of a second, better, thing. 3) Clean code that works improves the lives of users of our software. 4)Clean code that works lets your teammates count on you, and you on them. 5) Writing clean code that works feels good.

But how do you get to clean code that works? Many forces drive you away from clean code, and even code that works. Without taking too much counsel of our fears, here’s what we do—drive development with automated tests, a style of development called “Test-Driven Development” (TDD for short). In Test-Driven Development, you: 1) Write new code only if you first have a failing automated test. 2) Eliminate duplication.

Two simple rules, but they generate complex individual and group behavior. Some of the technical implications are: 1) You must design organically, with running code providing feedback between decisions. 2) You must write your own tests, since you can’t wait twenty times a day for someone else to write a test. 3) Your development environment must provide rapid response to small changes. 4) Your designs must consist of many highly cohesive, loosely coupled components, just to make testing easy.

The two rules imply an order to the tasks of programming: 1) Red—write a little test that doesn’t work, perhaps doesn’t even compile at first. 2) Green—make the test work quickly, committing whatever sins necessary in the process. 3) Refactor—eliminate all the duplication created in just getting the test to work.

Red/green/refactor. The TDDs mantra.

Assuming for the moment that such a style is possible, it might be possible to dramatically reduce the defect density of code and make the subject of work crystal clear to all involved. If so, writing only code demanded by failing tests also has social implications: 1) If the defect density can be reduced enough, QA can shift from reactive to proactive work. 2) If the number of nasty surprises can be reduced enough, project managers can estimate accurately enough to involve real customers in daily development. 3) If the topics of technical conversations can be made clear enough, programmers can work in minute-by-minute collaboration instead of daily or weekly collaboration. 4) Again, if the defect density can be reduced enough, we can have shippable software with new functionality every day, leading to new business relationships with customers.

1『极限编程的思想，什么东西好，就把该方面的东西推向极限。』

So, the concept is simple, but what’s my motivation? Why would a programmer take on the additional work of writing automated tests? Why would a programmer work in tiny little steps when their mind is capable of great soaring swoops of design? 

代码整洁可用（clean code that works), Ron Jeffries 这句言简意赅的话，正是测试驱动开发（Test- Driven Development, TDD）所追求的目标。代码整洁可用之所以是一个值得追求的目标，是基于以下的一系列原因：1）它是一个可预测的开发方法。你知道什么时候可以完工，而不用去担心是否会长期被 bug 困扰。2）它给你一个全面正确地认识和利用代码的机会。如果你总是草率地利用你最先想到的方法，那么你可能再也没有时间去思考另一种更好的方法。3）它改善了你的软件用户的生活。4）它让软件开发小组成员之间相互信赖。5）这样的代码写起来感觉很好。

但是我们要怎样做才能使代码整洁可用呢？很多因素妨碍我们得到整洁的代码，甚至是可用的代码。无需为此征求很多的意见，我们只需用自动运行的测试来推动开发，这是一种被称为测測试驱动开发（TDD）的开发方式。在测试驱动开发中，我们要这样做：1）只有自动测试失败时，我们才重写代码。2）消除重复设计，优化设计结构。

这是两条很简单的规则，但是由此产生了复杂的个人和小组行为规范，技术上的含意是：1）我们必须通过运行代码所提供的反馈来做决定，并以此达到有机设计的目的。2）我们必须自己写测试程序，这是因为测试很多，很频繁，我们不能每天把大量的时间浪费在等待他人写测试程序上。3）我们的开发环境必须能迅速响应哪怕是很小的变化。4）为使测试简单，我们的整个规划必须是由许多高内聚、低耦合的部分组成。

这两条规则实际上蕴含了开发过程中所经历的阶段：1）不可运行一一写一个不能工作的测试程序，一开始这个测试程序甚至不能编译。2）可运行一一尽快让这个测试程序工作，为此可以在程序中使用一些不合情理的方法。3）重构——消除在让测试程序工作的过程中产生的重复设计，优化设计结构。不可运行 -> 运行 -> 重构，这就是测试驱动开发的口号。

现在假设这样的开发方式是可能的，那么，再进一步，显著地减少代码的错误密度（defect density），让所有参与某一工作的开发人员对工作主题足够明了的假定也将成为可能。如果是这样的话，那么只有测试失败时才需要重写代码，其社会意义是：1）如果代码的错误密度能够充分地减少，那么软件的质量保证（QA）工作可以由被动保证软件质量转变为主动保证软件质量。2）如果开发过程中令人不快的意外能够充分地减少，那么项目经理能对软件开发进度有个精确的把握，以便让实际用户参与日常开发。3）如果每次技术讨论的主题都足够明确，那么软件工程师之间的合作是以分钟计算的，而不是按每天或每周计算。4）再者，如果代码错误密度能够充分地减少，那么我们每天都可以得到有新功能的软件成品，并以此招揽新的用户群。

如此说来，观念是很简单的，但我的动机是什么呢？为什么一个软件工程师要做额外的写自动测试程序的工作？为什么一个设计观念可以瞬息万变的软件工程师却只能一小步一小步地进行工作？我们需要的是勇气。

### Courage

Test-driven development is a way of managing fear during programming. I don’t mean fear in a bad way, pow widdle prwogwammew needs a pacifiew, but fear in the legitimate, this-is-a-hard-problem-and-I-can’t-see-the-end-from-the-beginning sense. If pain is nature’s way of saying “Stop!”, fear is nature’s way of saying “Be careful.” Being careful is good, but fear has a host of other effects: 1) Makes you tentative. 2) Makes you want to communicate less. 3) Makes you shy from feedback. 4) Makes you grumpy.

None of these effects are helpful when programming, especially when programming something hard. So, how can you face a difficult situation and: 1) Instead of being tentative, begin learning concretely as quickly as possible. 2) Instead of clamming up, communicate more clearly. 3) Instead of avoiding feedback, search out helpful, concrete feedback. 4) You’ll have to work on grumpiness on your own.

Imagine programming as turning a crank to pull a bucket of water from a well. When the bucket is small, a free-spinning crank is fine. When the bucket is big and full of water, you’re going to get tired before the bucket is all the way up. You need a ratchet mechanism to enable you to rest between bouts of cranking. The heavier the bucket, the closer the teeth need to be on the ratchet.

The tests in test-driven development are the teeth of the ratchet. Once you get one test working, you know it is working, now and forever. You are one step closer to having everything working than you were when the test was broken. Now get the next one working, and the next, and the next. By analogy, the tougher the programming problem, the less ground should be covered by each test.

Readers of Extreme Programming Explained will notice a difference in tone between XP and TDD. TDD isn’t an absolute like Extreme Programming. XP says, “Here are things you must be able to do to be prepared to evolve further.” TDD is a little fuzzier. TDD is an awareness of the gap between decision and feedback during programming, and techniques to control that gap. “What if I do a paper design for a week, then test-drive the code? Is that TDD?” Sure, it’s TDD. You were aware of the gap between decision and feedback and you controlled the gap deliberately.

2『 TDD 的定义：TDD is an awareness of the gap between decision and feedback during programming, and techniques to control that gap. 做张术语卡片。』

That said, most people who learn TDD find their programming practice changed for good. “Test Infected” is the phrase Erich Gamma coined to describe this shift. You might find yourself writing more tests earlier, and working in smaller steps than you ever dreamed would be sensible. On the other hand, some programmers learn TDD and go back to their earlier practices, reserving TDD for special occasions when ordinary programming isn’t making progress.

There are certainly programming tasks that can’t be driven solely by tests (or at least, not yet). Security software and concurrency, for example, are two topics where TDD is not sufficient to mechanically demonstrate that the goals of the software have been met. Security relies on essentially defect-free code, true, but also on human judgement about the methods used to secure the software. Subtle concurrency problems can’t be reliably duplicated by running the code.

Once you are finished reading this book, you should be ready to: 1) Start simply. 2) Write automated tests. 3) Refactor to add design decisions one at a time.

This book is organized into three sections.

• An example of writing typical model code using TDD. The example is one I got from Ward Cunningham years ago, and have used many times since, multi-currency arithmetic. In it you will learn to write tests before code and grow a design organically.

• An example of testing more complicated logic, including reflection and exceptions, by developing a framework for automated testing. This example also serves to introduce you to the xUnit architecture that is at the heart of many programmer-oriented testing tools. In the second example you will learn to work in even smaller steps than in the first example, including the kind of self-referential hooha beloved of computer scientists.

• Patterns for TDD. Included are patterns for the deciding what tests to write, how to write tests using xUnit, and a greatest hits selection of the design patterns and refactorings used in the examples.

I wrote the examples imagining a pair programming session. If you like looking at the map before wandering around, you may want to go straight to the patterns in section 3 and use the examples as illustrations. If you prefer just wandering around and then looking at the map to see where you’ve been, try reading the examples through and refering to the patterns when you want more detail about a technique, then using the patterns as a reference.

Several reviewers have commented they got the most out of the examples when they started up a programming environment and entered the code and ran the tests as they read.

A note about the examples. Both examples, multi-currency calculation and a testing framework, appear simple. There are (and I have seen) complicated, ugly, messy ways of solving the same problems. I could have chosen one of those complicated, ugly, messy solutions, to give the book an air of “reality.” However, my goal, and I hope your goal, is to write clean code that works. Before teeing off on the examples as being too simple, spend 15 seconds imagining a programming world in which all code was this clear and direct, where there were no complicated solutions, only apparently complicated problems begging for careful thought. TDD is a practice that can help you lead yourself to exactly that careful thought.

测试驱动开发是一种可以在开发过程中控制忧虑感的开发方法。我并非指那些毫无意义的没有必要的担忧，而是指合理的担忧，担忧是否合理是个很困难的问题，不能从一开始就看出来。如果说疼痛自然就会叫「停！」那么担忧自然就会说「小心！」。小心谨慎是好的，但它也会产生以下一系列负面影响：1）让你一直处于试验性的阶段。2）让你不愿意与他人交流。3）让你羞于面对反馈。4）让你变得脾气暴躁。

这些负面影响对编程都是有害无益的，尤其是当需要编程解决的问题比较困难的时候。所以问题变为当我们面临一个比较困难的局面的时候，如何才能做到：1）尽快开始具体的学习，而不是一直处于试验性的阶段。2）更多地参与交流和沟通，而不是一直拒不开口。3）寻找那些有益的、建设性的反馈，而不是尽量避免反馈。4）依靠自己改掉坏脾气。

设想把编程看成是转动曲柄从井里提一桶水上来的过程。如果水桶比较小，那么仅需一个能自由转动的曲柄就可以了。如果水桶比较大而且装满了水，那么还没等水桶被提上来你就会很累了。你需要一个防倒转的装置，以保证每转一次可以休息一会儿。水桶越重，防倒转的棘齿相距就应该越近。

测试驱动开发中的测试程序就是防倒转装置上的棘齿。一旦我们的某个测试程序能工作了，我们就知道，它从现在开始并且以后永远都可以工作了。相对于测试程序没有通过，我们距离让所有的测试程序都工作又近了一步。现在我们的工作是让下一个测试程序工作，然后再下一个，就这样一直进行下去。分析表明，编程解决的问题越难，每次测试所覆盖的范围就应该越小。

看过我写的《Extreme Programming Explained》一书的读者可能会注意到我讲极限编程（XP）与讲测试驱动开发的语气是有区别的：讲测试驱动开发不像讲极限编程那么绝对。讲极限编程时我会说「这些是想进一步学习所必须具备的基础」，而讲测试驱动开发时要模糊些。测试驱动开发教你认识编程过程中的反馈与欲实现的构思之间的差距，并且提供了控制这个差距大小的技术。「如果我在纸上作了一周的规划，然后通过测试驱动编码，这是否就是测试驱动开发？」当然，这就是测试驱动开发。你知道欲实现的构思与反馈之间的差距，并且有意识地控制了这个差距。

绝大多数学习测试驱动开发的人发现他们的编程习惯被永久地改变了。「测试感染」（Test Infected）是 Erich Gamma 所杜撰的用以描述这种转变的词语。你可能发现写测试程序变得容易了，并且相对较小的工作节奏比以前所梦想的节奏更明智。另一方面，一些学习测试驱动开发的软件工程师重新回到了以前的程序开发方法，并且保留测试驱动开发方法作为当其他开发方法不能奏效的特殊情况下的秘密武器。

当然也存在一些编程任务不能仅仅（或者根本就不能）由测试程序来驱动开发的情况。举个例子来说，软件的安全性和并行性，测试驱动开发方法就不能充分地从机械证明的角度说明。软件是否达到了这两个目标。软件安全性从本质上来说依赖于无缺陷的代码。确实如此，但它同时也依赖于人们对软件安全机制的判断。精妙的并行问题不是仅靠再次运行代码就能可靠地再现的。

一旦读完本书，你要准备：1）从简单的例子开始。2）写自动测试程序。3）重构，每次增加一个新的设计构思。

这本书是由三个部分组成的：

第一部分，资金实例（The Money Example），一个典型的完全由测试驱动的代码模型的例子。这个例子是几年前我从 Ward Cunningham 那儿得到的，并且自从引入多币种算法以来已经多次用到过。你将从中学会如何在写代码之前写好测试程序，并最终发展成为一个有机的规划方案。

第二部分，xUnit 实例（The xunit Example），一个逻辑上更复杂的程序的例子包含反射（reflection）和异常（exception），通过建立自动测试框架来测试。这个例子同时也将向你介绍作为许多面向程序员的测试工具灵魂的 xUnit 结构体系。在第二个例子中你将学会以甚至比第一个例子更小的开发步骤工作，同时也包括深受许多计算机专家喜爱的呼喊式的自我提醒（self-referential hoo-ha）。

第三部分，测试驱动开发模式（Patterns for Test-Driven Development）包括决定写哪些测试的模式，如何用 xUnit 写测试的模式和大量的设计模式精选以及例子中所用到的重构。

我写了关于结对编程（pair programming）的例子。如果你习惯于在四处转一转之前先看地图的话，你可以直接到第三部分去看那些模式，并将那些例子作为说明。如果你习惯于先到四处转一转，然后再看地图以确定自己处于什么位置的话，试着通读例子，当你需要了解更多关于某一技术问题的细节时，可以査阅后面所讲的模式，并将这些模式作为参考。本书的一些技术评审人指出，当他们启动编程环境，输入代码，运行所读到的测试程序时，最大的收获却在这些例子之外。

关于这些例子要注意一点。这两个例子，多币种计算和测试框架，看上去很简单。而解决同一个问题却也存在（我曾经见到过）一些复杂、风格很差、近乎弱智的解决方案。我本可以从这些复杂、风格很差、近乎弱智的解决方案中采用一个以使本书有一种「真实」感。然而，我的目标是写出整洁可用的代码，希望你的目标也是这样。在以那些被认为很简单的例子开始之前，花 15 秒的时间设想一下，如果所有的代码都能如此清晰和直接，没有复杂的解决方案，只有显然需要认真思考的很复杂的问题，那么这个世界会是什么样子。测试驱动开发可以引导你这样去认真思考。

## 写在后面的话——Martin Fowler

有关测试驱动开发最难讲清楚的一种东西就是它把你所带到的那种思维状态。我记得在和 Ralph Beattie 开发原先的 C3 项目时，有一回，我们必须要实现一套复杂的支付判定。Ralph 把它们分解成一组测试用例，我们逐条地使其运行通过。工作有条不紊地进行，由于工作起来不是慌里慌张的，所以进度似乎显得有些慢，但当我们回过头看看做了多少工作时，发现尽管没有慌里慌张的感觉，但进展着实迅速。

尽管我们拥有各种优秀的工具，但编程还是很难。我记得在我编程时，很多次我都觉得就像一下要保持好几个球在空中，稍有不慎所有的球都会呼啦掉下来。测试驱动开发帮助我们减少这种感觉，因此也能在不慌不忙中快速地进行开发。

我认为存在这种效果的原因是这样的，在你用测试驱动开发方式工作时，你会有一种只保留一个球在空中的感觉，因此你可以全身心地关注那个球，因而可以处理得很好。当我要增加某个新功能时，我不必担心为了这个新功能怎样设计才算好，我只要尽可能简单地写一个测试并通过就行了。同样，在进行重构时我不必操心増加新的功能，而只关心如何进行合理的设计。对于两者我一次只要关注其一，因此我能够更好地集中注意力在一件事情上。

通过测试优先和重构增加功能是编程的两项独立的逻辑。最近在键盘旁工作时，我又发现了另外一个方法：模式拷贝（pattem copying）。那时我在用 Ruby 语言写一个抽取数据库数据的脚本程序。在做这件事情的同时，我开始着手编写一个包装数据库表的类，心想既然我刚刚看完了一本关于数据库模式的书，那我也应该用一用模式。尽管范例代码是 Java，但要把它改成 Ruby 并不难。我编程时并没有真正想过那个问题，我只是考虑如何改编这一模式让其适合这种语言以及我正在操纵的特定数据。

模式拷贝就其本身并不是好的编程方法一一这是在我谈模式时总是强调的事实。模式一般都是半成品，用到你的项目中还要再回一次炉。然而处理这一问题的一个好的办法是：一开始先不用管那么多，把模式拷贝过来，接下来采用重构和测试优先相结合的办法对其进行改编。这样一来，当你在做模式拷贝的时候，你可以把注意力集中到模式上ー一同一时刻只干一件事。

XP（极限编程）社团一直致力于研究在什么地方引入模式。显然 XP 成员喜欢使用模式，毕竟 XP 倡导者与模式倡导者之间有很多共同之处。Ward 和 Kent 同时是这两个领域的带头人。也许模式拷贝是继测试优先和重构之后的第三种单一逻辑模式，和前两者一样，单独使用种时是危险的，但协调使用时功能强大。

要想系统地组织活动，很大程度上取决于核心任务的辨识，这使得我们每次能够集中注意力在一件事情上。装配线就是这样一个使人头脑麻木的例子一一头脑麻木是因为你一直在做同件事。也许测试驱动开发所提议的是一种将编程切分成各种模式要素的方法，但是为了避免单调乏味而在这些模式要素间快速切换。单一逻辑模式与各模式间的快速切换相结合有利于你集中注意力并降低对大脑的压力，却没有装配线般的单调感觉。

我得承认这些想法有些不成熟。在我写这段文字的时候，我还无法确信我是否相信自己所说的这些内容，而且我知道自己还得仔细推敲个把月。但是我想也许你会喜欢这些评述的，而且或许能够激励你思考测试优先开发所适合的大环境。究竟是怎样的环境我们目前还说不清楚，但是我想它会慢慢自己展现出来的。

## Story Time

Early one Friday the boss came to Ward to introduce him to Peter, a prospective customer for WyCash, the bond portfolio management system they were selling. Peter said, “I’m very impressed with the functionality I see. However, I notice you only handle US dollar denominated bonds. I’m starting a new bond fund and my strategy requires that I handle bonds in different currencies.” The boss turned to Ward, “Well, can we do it?”

Here is the nightmare scenario for any software designer. You have been cruising along happily and successfully with a set of assumptions. Suddenly, everything changes. And the nightmare wasn’t just for Ward. The boss, an experienced hand at directing software development, wasn’t sure what the answer was going to be.

WyCash had been developed over the course of a couple of years by a small team. It was able to handle most of the varieties of fixed income securities commonly found on the US market, and a few exotic new instruments, like Guaranteed Investment Contracts, that the competition couldn’t handle.

WyCash had been developed all along using objects and an object database. The fundamental abstraction of computation, Dollar, had been outsourced at the beginning to a clever group of programmers. The resulting object combined formatting and calculation responsibilities.

For the last six months, Ward and the rest of the team had been slowly divesting Dollar of its responsibilities. The Smalltalk numerical classes turned out to be just fine at calculation. All the tricky code for rounding to three decimal digits got in the way of producing precise answers. As the answers got more precise, the complicated mechanisms in the testing framework for comparing to within a certain tolerance were replaced by precise matching of expected and actual results.

Responsibility for formatting actually belonged in the user interface classes. As the tests were written at the level of the user interface classes, in particular the report framework, these tests didn’t have to change to accomodate this refinement. After six months of careful paring, the resulting Dollar didn’t have much responsibility left.

One of the most complicated algorithms in the system, weighted average, had likewise been undergoing a slow transformation. At one time there had been many different variations of weighted average code scattered throughout the system. As the report framework coalesced from the primodial object soup, it was obvious that there could be one home for the algorithm, in AveragedColumn.

It was to AveragedColumn that Ward now turned. If weighted averages could be made multi-currency, the rest of the system should be possible. The heart of the algorithm was keeping a count of the money in the column. In fact, the algorithm had been abstracted enough to calculate the weighted average of any object that could act arithmetic. You could have weighted averages of dates, for example.

The weekend past in the usual weekend activities. Monday morning the boss was back. “Can we do it?” “Give me another day and I’ll tell you for sure.” Since Dollar acted like a counter in weighted average, in order to calculate in multiple currencies they needed an object with a counter per currency, kind of like a polynomial. Instead of 3x^2 and 4y^3 , though, the terms would be 15 USD and 200 CHF.

A quick experiment showed that it was possible to compute with a generic Currency object instead of a Dollar, and return a PolyCurrency when two un-alike currencies were added together. The trick now was to make space for the new functionality without breaking anything that already worked. What would happen if Ward just ran the tests?

After adding a few un-implemented operations to Currency, the bulk of the tests passed. By the end of the day, all the tests were passing. Ward checked the code into the build and went to the boss. “We can do it,” he said confidently.

Let’s think a bit about this story. In two days, the potential market was multiplied several fold, multiplying the value of WyCash several fold. The ability to create so much business value so quickly was no accident though. Several factors came into play:

• Method—Ward and the WyCash team needed to have constant experience growing the design of the system little-by-little, so the mechanics of the transformation were well practiced.

• Motive—Ward and team had to understand clearly from the business the importance of making WyCash multi-currency, and to have the courage to start such a seemingly impossible task.

• Opportunity— The combination of comprehensive, confidence-generating tests; a well-factored program; and a programming language that made it possible to isolate design decisions meant that there were few sources of error, and those errors were easy to identify.

You can’t control whether you ever get the motive to multiply the value of your project by spinning technical magic. Method and opportunity, however, are entirely under your control. Ward and his team created method and opportunity by a combination of superior talent, experience, and discipline. Does this mean that if you are not one of the ten best software engineers on the planet and you don’t have a wad of cash in the bank so you can tell your boss to take a hike, you’re going to take the time to do this right, that such moments are forever beyond your reach?

No. You absolutely can place your projects in a position for you to work magic, even if you are a programmer with ordinary skills and you sometimes buckle under and take shortcuts when the pressure builds. Test-driven development is a set of techniques any programmer can follow, that encourage simple designs and test suites that inspire confidence. If you are a genius, you don’t need these rules. If you are a dolt, the rules won’t help. For the vast majority of us in between, though, following these two simple rules can lead us to work much closer to our potential: 1) Write a failing automated test before you write any code. 2) Remove duplication.

1『作者反复提到的 2 个原则：编程前写自动测试、去除重复的代码。』

How exactly to do this, the subtle gradations in applying these rules, and the lengths to which you can push these two simple rules are the topic of this book. We’ll start with the object Ward created in his moment of inspiration—multi-currency money.

一个星期五的早晨，老板来找 Ward Cunningham，并把 Ward 介绍给 Peter 认识。Peter 有望成为公司开发的有价证券管理系统（Wycash）的用户。Peter 说：「贵公司这套系统的功能给我留下了很深的印象，但是，我注意到这套系统仅能处理美元证券，我开设了一家新的证券基金，我的发展战略要求能够处理不同币种的基金」。老板转问 Ward，「那么，你看我们能做到这一点吗？」

这是任何软件设计者都可能遇到的噩梦般的一幕。你先前一直在一组假设条件下顺利而愉快地进行开发。而突然间，一切都变了。这个疆梦并非只针对 Ward 一个人，公司的老板，一个在指导软件开发方面经验丰富的老板，同样也不知道答案会是什么。

Wycash 系统是公司一个规模不大的开发小组两年来辛勤工作的成果。这个系统可以处理绝大部分美国市场上常见的各种各样的固定收益有价证券，还可以处理其他国家的一些新的投资证券，例如保利投资证券，而这是其他同类产品所不能处理的。Wycash 系统一直是采用对象和对象数据库来进行开发的。作为构成基础计算要素抽象的 Dollar（美元），一开始是外包给一组聪明的程序员来完成的，他们开发的对象合并了信息格式化与计算两种功能。

在过去的六个月中，Ward 和小组的其他人员开始将 Dollar 对象的操作逐渐剥离出来。事实证明，Smalltalk 的数值类在计算方面工作得还是挺好的。用于四舍五入至三位十进制数字的复杂代码实际上有碍于产生精确的结果。随着结果精确度的提高，测试框架中用于在一定误差范围内进行比较的复杂机制由与预期或实际结果进行精确匹配的方法所取代。

用于完成信息格式化的操作实际上应由用户界面类来负责。由于测试代码，尤其是报告生成架构部分的代码是在用户界面类一级编写的，所以这些测试程序无需修改就能适应这些改动。在经过六个月的认真剥离之后，Dollar 类所负责的操作已经所剩无几了。

系统中最复杂的算法之一，加权平均（weighted average），同样也经历了一个逐渐转变的过程。曾经有段时间，加权平均算法代码的各种变种遍布整个系统。就像报告生成架构是由最初众多的对象整合而来的一样，加权平均算法同样也会有一个容纳它的地方，这就是 Averaged Column。

Averaged Column 现在就是 Wad 要着手工作的地方。如果加权平均能够支持多种货币，那么系统剩下的部分就好办了。该算法的核心是将货币的数额保存在相应栏内。实际上，这个运算规则已经被抽象得足以计算任何对象的加权平均。举个例子来说，它可以计算日期的加权平均。

这个周末像往常一样地过去了。星期一早晨老板又过来了，他问道：「怎么样，能做吗？」「再多给我一天时间，我将给你一个确切的答案。」Ward 说道。

Dollar 就如同加权平均里的一个计数器：因此，为使其支持多种货币，系统必须要有一种对象，这种对象针对每种货币都有一个计数器，就如同多项式一样。只不过其中的项可能是 15 USD 和 200 CHF，而不是 3x^2 和 4y^3。

一个快速试验显示，用一个通用的 Currency（货币）对象代替 Dollar 对象进行计算是可能的，并且当两个不同币种的对象相加时返回一个 Poly Currency 对象（多币种）。现在的问题是如何在不影响现有功能正常工作的情况下，为新功能腾出空间。如果 Ward 运行这些测试程序会是怎样呢？

在为 Currency 增加一些未实现的操作后，大多数的测试都通过了。在这一天结束的时候，所有的测试都通过了。Ward 把代码上传至源码控制系统并加入到产品建造过程中，然后跑到老板那里，「我们能做！」他自信地说道。

让我们总结一下这个故事。在两天的时间里，潜在的市场扩大了数倍，Wycash 系统的价值也扩大了数倍。有能力在这么短的时间里创造出这么大的商业价值绝非偶然。以下几个因素促成了这件事情的成功：1）方法。Ward 和 Wycash 系统开发小组需要有一定的经验，知道如何持续渐进地进行系统设计。正是因为如此，为改进系统而采用的机制才能很好地工作。2）动机。Ward 和他的小组必须对使 Wycash 系统支持多币种的商业价值有一个很明确的认识，并要有勇气接受这样一个看起来似乎是不可能完成的任务。3）机遇。周全而激发自信的测试、构造良好的代码以及一种能够隔离设计构思的编程语言，这三者的结合意味着出问题的机会将会更少，并且出现的问题很容易辨认。

将项目的价值翻几番这种事情不是通过技术的魔力就能驾御的。而另一方面，方法和机遇却完全是在你的控制之中的。Ward 及其小组通过自己非凡的智慧、经验和行动准则创造方法和机遇。这是否意味着，如果你不是这个世界上最优秀的十名软件工程师之一，如果你在银行里没有一打一打的钞票，你就要对你的老板说你要求加薪，那么现在正好要行使这个权利，而这成功的时刻永远不会属于你呢？

当然不。即使你只是一个技能一般的软件工程师，即使面对压力曾使你乱成一团，偷工减料，你也绝对可以为你的项目找一个位置，在这个位置上你可以以魔术般不可思议的效果工作。测试驱动开发是任何软件工程师都可以学习的一个技术的集合，它鼓励采用简单的设计和增强自信的测试套件。如果你是个天才，你根本不需要学习这些浅显的规则。如果你是个傻子，学了也没有用。对于像我们这样介于二者之间的大多数人来说，遵从这两条简单的规则可以使我们以更加接近我们全部潜能的效率去工作。

1、在你写任何代码之前，先写一个会失败的自动测试程序。2、消除重复设计，优化设计结构。

到底要如何这样做？如何巧妙地分阶段应用这些规则？这两条简单的规则可以运用多深？这正是本书要讲的主题。我们将从 Ward 在灵感爆发瞬间所创造的对象一一多币种资金（muli-currency money）开始谈起。




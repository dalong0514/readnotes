## 记忆时间

2021-05-11

## 目录

0101 What Is Design and Architecture?

0201 A Tale of Two Values

## 0101. What Is Design and Architecture?

### Conclusion

In every case, the best option is for the development organization to recognize and avoid its own overconfidence and to start taking the quality of its software architecture seriously.

To take software architecture seriously, you need to know what good software architecture is. To build a system with a design and an architecture that minimize effort and maximize productivity, you need to know which attributes of system architecture lead to that end.

That's what this book is about. It describes what good clean architectures and designs look like, so that software developers can build systems that will have long profitable lifetimes.

不管怎么看，研发团队最好的选择是清晰地认识并避开工程师们过度自信的特点，开始认真地对待自己的代码架构，对其质量负责。要想提高自己软件架构的质量，就需要先知道什么是优秀的软件架构。而为了在系统构建过程中采用好的设计和架构以便減少构建成本，提高生产力，又需要先了解系统架构的各种属性与成本和生产力的关系。这就是这本书的主题。本书为读者描述了什么是优秀的、整洁的软件架构与设计，读者可以参考这些设计来构建一个长期稳定的、持久优秀的系统。

### 00

There has been a lot of confusion about design and architecture over the years. What is design? What is architecture? What are the differences between the two?

One of the goals of this book is to cut through all that confusion and to define, once and for all, what design and architecture are. For starters, I'll assert that there is no difference between them. None at all.

The word「architecture」is often used in the context of something at a high level that is divorced from the lower-level details, whereas「design」more often seems to imply structures and decisions at a lower level. But this usage is nonsensical when you look at what a real architect does.

Consider the architect who designed my new home. Does this home have an architecture? Of course it does. And what is that architecture? Well, it is the shape of the home, the outward appearance, the elevations, and the layout of the spaces and rooms. But as I look through the diagrams that my architect produced, I see an immense number of low-level details. I see where every outlet, light switch, and light will be placed. I see which switches control which lights. I see where the furnace is placed, and the size and placement of the water heater and the sump pump. I see detailed depictions of how the walls, roofs, and foundations will be constructed.

In short, I see all the little details that support all the high-level decisions. I also see that those low-level details and high-level decisions are part of the whole design of the house.

And so it is with software design. The low-level details and the high-level structure are all part of the same whole. They form a continuous fabric that defines the shape of the system. You can't have one without the other; indeed, no clear dividing line separates them. There is simply a continuum of decisions from the highest to the lowest levels.

一直以来，设计（Design）与架构（Architecture）这两个概念让大多数人十分迷惑。什么是设计？什么是架构？二者究有什么区别？本书的一个重要目标就是要清晰、明确地对二者进行定义。首先我要明确地说，二者没有任何区别。一丁点区别都没有！

「架构」这个词往往使用于「高层级」的讨论中。这类讨论一般都把「底层」的实现细节排除在外。而「设计」一词，往往用来指代具体的系统底层组织结构和实现的细节。但是，从一个真正的系统架构师的日常工作来看，这样的区分是根本不成立的。

以给我设计新房子的建筑设计师要做的事情为例。新房子当然是存在着既定架构的，但这个架构具体包含哪些内容呢？首先，它应该包括房屋的形状、外观设计、垂直高度、房间的布局，等等。但是，如果查看建筑设计师使用的图纸，会发现其中也充斥着大量的设计细节。如，我们可以看到每个插座、开关以及每个电灯具体的安装位置，同时也可以看到某个开关与所控制的电灯的具体连接信息；我们也能看到壁炉的具体安装位置，热水器的大小和位置信息，甚至是污水泵的位置；同时也可以看到关于墙体、屋顶和地基都有非常详细的建造说明。

总的来说，架构图里实际上包含了所有的底层设计细节，这些细节信息共同支撑了顶层的架构设计，底层设计信息和顶层架构设计共同组成了整个房屋的架构文档。软件设计也是如此。底层设计细节和高层架构信息是不可分割的。它们组合在一起，共同定义了整个软件系，缺一不可。所谓的底层和高层本身就是一系列策组成的连续体，并没有清晰的分界线。

### 1.1 The  Goal?

And the goal of those decisions? The goal of good software design? That goal is nothing less than my utopian description:

The goal of  software architecture is to minimize the human resources required to build and maintain the required system.

The measure of design quality is simply the measure of the effort required to meet the needs of the customer. If that effort is low, and stays low throughout the lifetime of the system, the design is good. If that effort grows with each new release, the design is bad. It's as simple as that.

所有这些決策的终极目标是什么呢？一个好的软件设计的终极目标是什么呢？就像我之前描述过的：软件架构終极目标是，用最小的人力成本来满足构建和维护该系统的需求。

软件架构的优劣，可以用它满足用户需求所需要的成本来衡量。如果该成本很低，并且在系统的整个生命周期内一直都能维持这样的低成本，那么这个系统的设计就是优良的。如果该系的每次发布都会提升下一次变更的成本，那么这个设计就是不好的。就这么简单。

### 1.2 Case Study

As an example, consider the following case study. It includes real data from a real company that wishes to remain anonymous.

First, let's look at the growth of the engineering staff. I'm sure you'll agree that this trend is very encouraging. Growth like that shown in Figure 1.1 must be an indication of significant success!

Figure 1.1  Growth of the engineering staff

Now let's look at the company's productivity over the same time period, as measured by simple lines of code (Figure 1.2).

Figure 1.2  Productivity over the same period of time

Clearly something is going wrong here. Even though every release is supported by an ever-increasing number of developers, the growth of the code looks like it is approaching an asymptote. Now here's the really scary graph: Figure 1.3 shows how the cost per line of code has changed over time.

These trends aren't sustainable. It doesn't matter how profitable the company might be at the moment: Those curves will catastrophically drain the profit from the business model and drive the company into a stall, if not into a downright collapse.

What caused this remarkable change in productivity? Why was the code 40 times more expensive to produce in release 8 as opposed to release 1?

Figure 1.3  Cost per line of code over time

下面来看一个真实案例，该案例中的数据均来源于个要求匿名的真实公司。

首先，我们来看一下工程师团队规模的增长。你肯定认为这个增长趋势是特别可喜的，像图 1.1 中的这种增长线条一定是公司业务取得巨大成功的直观体现。现在再让我们来看一下整个公司同期的生产效率（productivity），这里用简单的代码行数作为指标（参见图 1.2)。

这明显是有问题的。伴随着产品的每次发布，公司的工程师团队在持续不断地扩展壮大，但是仅从代码行数的增长来看，该产品却正在逐渐陷入困境。还有更可怕的：图 1.3 展示的是同期内每行代码的更成本。

显然，图中展示的趋势是不可持续的。不管公司现在的利润率有多高，图中线条表明，按这个趋势下去，公司的利润会被一点点榨干，整个公司会因此陷入困境，甚至直接关门倒闭究竟是什么因素造成了生产力的大幅变化呢？为什么第 8 代产品的构建成本要比第 1 代产品高 40 倍？

#### 1.2.1 The Signature of a Mess

What you are looking at is the signature of a mess. When systems are thrown together in a hurry, when the sheer number of programmers is the sole driver of output, and when little or no thought is given to the cleanliness of the code or the structure of the design, then you can bank on riding this curve to its ugly end.

Figure 1.4 shows what this curve looks like to the developers. They started out at nearly 100% productivity, but with each release their productivity declined. By the fourth release, it was clear that their productivity was going to bottom out in an asymptotic approach to zero.

Figure 1.4  Productivity by release

From the developers' point of view, this is tremendously frustrating, because everyone is working hard. Nobody has decreased their effort.

And yet, despite all their heroics, overtime, and dedication, they simply aren't getting much of anything done anymore. All their effort has been diverted away from features and is now consumed with managing the mess. Their job, such as it is, has changed into moving the mess from one place to the next, and the next, and the next, so that they can add one more meager little feature.

乱麻系统的特点

我们在这里看到的是一个典型的乱麻系统。这种系统一般都是没有经过设计，匆匆忙忙被构建起来的。然后为了加快发布的速度，拼命地往团队里加入新人，同时加上決策层对代码质量提升和设计结构优化存在着持续的、长久的忽视，这种状态能持续下去就怪了。

图 1.4 展示了系统开发者的切身体会。他们一开始的效率都接近 100%，然而伴随着每次产品的发布，他们的生产力直线下降。到了产品的第 4 版本时，很明显大家的生产力已经不可避免地趋近为零了。对系统的开发者来说，这会来很大的挫败感，因为团队中并没有人偷懒，每个人还都是和之前一样在拼命工作。

然而，不管他们投入了多少个人时间，救了多少次火，加了多少次班，他们的产出始终上不去。工程师的大部分时间都消耗在对现有系统的修修补补上，而不是真正完成实际的新功能。这些工程师真正的任务是：拆了东墙补西墙，周而往复，偶尔有精力能顺便实现一点小功能。

#### 1.2.2 The Executive View

If you think that's bad, imagine what this picture looks like to the executives! Consider Figure 1.5, which depicts monthly development payroll for the same period.

Figure 1.5  Monthly development payroll by release

Release 1 was delivered with a monthly payroll of a few hundred thousand dollars. The second release cost a few hundred thousand more. By the eighth release monthly payroll was `$20` million, and climbing.

Just this chart alone is scary. Clearly something startling is happening. One hopes that revenues are outpacing costs and therefore justifying the expense. But no matter how you look at this curve, it's cause for concern.

But now compare the curve in Figure 1.5 with the lines of code written per release in Figure 1.2. That initial few hundred thousand dollars per month bought a lot of functionality — but the final $20 million bought almost nothing! Any CFO would look at these two graphs and know that immediate action is necessary to stave off disaster.

But which action can be taken? What has gone wrong? What has caused this incredible decline in productivity? What can executives do, other than to stamp their feet and rage at the developers?

管理层视角

如果你觉得开发者们这样就已经够苦了，那么就再想想公司高管们的感受吧！请看图 1.5，该部门月工资同期图。

如你所见，产品的第 1 版是在月总工 10 万美元左右的时候上线的。第 2 版又花掉了几十万美元。当发布第 8 版的时候，部门月工资已经达到了 2 千万美元，而且还在持续上升也许我们可以指望该公司的营收增长远远超出成本增长，这样公司就还能维持正常运转。但是这么惊人的曲线还是值得我们深入挖掘其中存在的巨大问题的。

现在，只要将图 1.5 的月工资曲线和图 1.2 的每次发布代码行数曲线对比一下，任何一个理性的 CEO 都会一眼看出其中的问题：最开始的十几万美元工资给公司带来了很多新功能、新收益，而最后的 2 千万美元几乎全打了水漂。应立刻采取行动解决这个问题，刻不容缓但是具体采取什么样的行动才能解决向题呢？究竟问题出在哪里？是什么造成了工程师生产力的直线下降？高管们除了跺脚、发飙，还能做什么呢？

#### 1.2.3 What  Went  Wrong?

Nearly 2600 years ago, Aesop told the story of the Tortoise and the Hare. The moral of that story has been stated many times in many different ways: 1) Slow and steady wins the race. 2) The race is not to the swift, nor the battle to the strong. 3) The more haste, the less speed.

The story itself illustrates the foolishness of overconfidence. The Hare, so confident in its intrinsic speed, does not take the race seriously, and so naps while the Tortoise crosses the finish line.

Modern developers are in a similar race, and exhibit a similar overconfidence. Oh, they don't sleep — far from it. Most modern developers work their butts off. But a part of their brain does sleep — the part that knows that good, clean, well-designed code matters.

These developers buy into a familiar lie:「We can clean it up later; we just have to get to market first!」Of course, things never do get cleaned up later, because market pressures never abate. Getting to market first simply means that you've now got a horde of competitors on your tail, and you have to stay ahead of them by running as fast as you can.

And so the developers never switch modes. They can't go back and clean things up because they've got to get the next feature done, and the next, and the next, and the next. And so the mess builds, and productivity continues its asymptotic approach toward zero.

Just as the Hare was overconfident in its speed, so the developers are overconfident in their ability to remain productive. But the creeping mess of code that saps their productivity never sleeps and never relents. If given its way, it will reduce productivity to zero in a matter of months.

The bigger lie that developers buy into is the notion that writing messy code makes them go fast in the short term, and just slows them down in the long term. Developers who accept this lie exhibit the hare's overconfidence in their ability to switch modes from making messes to cleaning up messes sometime in the future, but they also make a simple error of fact. The fact is that making messes is always slower than staying clean, no matter which time scale you are using.

Consider the results of a remarkable experiment performed by Jason Gorman depicted in Figure 1.6. Jason conducted this test over a period of six days. Each day he completed a simple program to convert integers into Roman numerals. He knew his work was complete when his predefined set of acceptance tests passed. Each day the task took a little less than 30 minutes. Jason used a well-known cleanliness discipline named test-driven development (TDD) on the first, third, and fifth days. On the other three days, he wrote the code without that discipline.

Figure 1.6  Time to completion by iterations and use/non-use of TDD

First, notice the learning curve apparent in Figure 1.6. Work on the latter days is completed more quickly than the former days. Notice also that work on the TDD days proceeded approximately 10% faster than work on the non-TDD days, and that even the slowest TDD day was faster than the fastest non-TDD day.

Some folks might look at that result and think it's a remarkable outcome. But to those who haven't been deluded by the Hare's overconfidence, the result is expected, because they know this simple truth of software development:

The only way to go fast, is to go well.

And that's the answer to the executive's dilemma. The only way to reverse the decline in productivity and the increase in cost is to get the developers to stop thinking like the overconfident Hare and start taking responsibility for the mess that they've made.

The developers may think that the answer is to start over from scratch and redesign the whole system — but that's just the Hare talking again. The same overconfidence that led to the mess is now telling them that they can build it better if only they can start the race over. The reality is less rosy:

Their overconfidence will drive the redesign into the same mess as the original project.

问题到底在哪里

大约 2600 年前，《伊索寓言》里写到了龟兔赛跑的故事。这个故事的主题思想可以归纳为以下几种：1）慢但是稳，是成功的秘诀。2）该比赛并不是拼谁开始跑得快，也不是拼谁更有力气的。3）心态越急，反而跑得越。

这个故事本身掲露的是过度自信的愚行为。兔子由于对自己速度的过度自信，没有把乌龟当回事，结果乌龟爬过终点线取得胜利的时候，它还在睡觉。这和现代软件研发工作有点类似，现在的软件研发工程师都有点过于自信。哦，当然，他们确实不会偷懒，一点也不。但是他们真正偷懒的地方在于一持续低估那些好的、良好设计的、整洁的代码的重要性。

这些工程师们普遍用一句话来欺骗自己：「我们可以未来再重构代码，产品上线最重要！」但是结果大家都知道，产品上线以后重构工作就再没人提起了。市场的压力永远也不会消退，作为首先上市的产品，后面有无数的竞争对手追赶，必须要比他们跑得更快才能保持领先所以，重构的时机永远不会再有了。工程师们忙于完成新功能，新功能做不完，哪有时间重构老的代码？循环往复，系统成了一团乱麻，生产效率持续直线下降，直至为零。结果就像龟兔赛跑中过于自信的兔子一样，软件研发工程师们对自己保持高产出的能力过于自信了。但是乱成一团的系統代码可没有休息时间，也不会放松。如果不严加提防，在几个月之内，整个研发团队就会陷入困境。

工程师们经常相信的另外一个错误观点是：「在工程中容忍糟糕的代码存在可以在短期内加快该工程上线的速度，未来这些代码会造成一些额外的工作量，但是并没有什么大不了。」相信这些鬼话的工程师对自己清理乱麻代码的能力过于自信了。但是更重要的是，他们还忽视了一个自然规律：无论是从短期还是长期来看，胡乱编写代码的工作速度其实比循规蹈矩更慢。

图 1.6 展示的是 Jason Gorman 进行的一次为期 6 天的实验。在该实验中，Jaosn 每天都编写一段代码，功能是将一个整数转化为相应罗马数字的字符串。当事先定义好的一个测试集完全通过时，即认为当天工作完成。每天实验的时长不超过 30 分钟。第一天、第三天和第五天，Jason 在编写代码的过程中采用了业界知名的优质代码方法论：测试驱动开发（TDD），而其他三天他则直接从头开始编写代码。

首先，我们要关注的是图 1.6 中那些柱状图。很显然，日子越往后，完成工作所需的时间就越少。同时，我们也可以看到当人们采用了 TDD 方法编程后，一般就会比未采用 TDD 方法编程少用 10% 的时间，并且采用 TDD 方法编程时最差的一天也比未采用 TDD 方法编程时最好的一天用时要短对于这个结果，有些人可能会觉得挺意外的。但是对常年关注软件开发本质的人来说，它其实揭示了软件开发的一个核心特点。

要想跑得快，先要得稳。

综上所述，管理层扭转局面的唯一选择就是扭转开发者的观念，让他们从过度自信的兔子模式转变回来，为自己构建的乱麻系统负起责任来。

当然，某些软件研发工程师可能会认为挽救一个系统的唯一办法是抛弃现有系，设计一个全新的系統来替代。但是这里仍然没有逃离过度自信。试问：如果是工程师的过度自信导致了目前的一团乱麻，那么，我们有什么理由认为让他们从头开始，结果就会更好呢？

过度自信只会使得重构设计陷入和原项目一样的困局中。

## 0201. A Tale of Two Values

Every software system provides two different values to the stakeholders: behavior and structure. Software developers are responsible for ensuring that both those values remain high. Unfortunately, they often focus on one to the exclusion of the other. Even more unfortunately, they often focus on the lesser of the two values, leaving the software system eventually valueless.

对于每个软件系，我们都可以通过行为和架构两个维度来体现它的实际价值。软件研发人员应该确保自己的系统在这两个维度上的实际价值都能长时间维持在很高的状态。不幸的是，他们往往只关注一个维度，而忽视了另外一个维度。更不幸的是，他们常常关注的还是错误的维度，这导致了系统的价值最终趋降为零。

### 2.1 Behavior

The first value of software is its behavior. Programmers are hired to make machines behave in a way that makes or saves money for the stakeholders. We do this by helping the stakeholders develop a functional specification, or requirements document. Then we write the code that causes the stakeholder's machines to satisfy those requirements.

When the machine violates those requirements, programmers get their debuggers out and fix the problem.

Many programmers believe that is the entirety of their job. They believe their job is to make the machine implement the requirements and to fix any bugs. They are sadly mistaken.

行为价值

软件系统的行为是其最直观的价值维度。程序员的工作就是让机器按照某种指定方式运转，给系统的使用者创造或者提高利润。程序员们为了达到这个目的，往往需要帮助系统使用者编写一个对系统功能的定义，也就是需求文档。然后，程序员们再把需求文档转化为实际的代码。

当机器出现异常行为时，程序员要负责调试，解决这些问题。大部分程序员认为这就是他们的全部工作。他们的工作是且仅是：按照需求文档编写代码，并且修复任何 Bug。这真是大错特错。

### 2.2 Architecture

The second value of software has to do with the word「software」 — a compound word composed of「soft」and「ware.」The word「ware」means「product」; the word「soft」… Well, that's where the second value lies.

Software was invented to be「soft.」It was intended to be a way to easily change the behavior of machines. If we'd wanted the behavior of machines to be hard to change, we would have called it hardware.

To fulfill its purpose, software must be soft — that is, it must be easy to change. When the stakeholders change their minds about a feature, that change should be simple and easy to make. The difficulty in making such a change should be proportional only to the scope of the change, and not to the shape of the change.

It is this difference between scope and shape that often drives the growth in software development costs. It is the reason that costs grow out of proportion to the size of the requested changes. It is the reason that the first year of development is much cheaper than the second, and the second year is much cheaper than the third.

From the stakeholders' point of view, they are simply providing a stream of changes of roughly similar scope. From the developers' point of view, the stakeholders are giving them a stream of jigsaw puzzle pieces that they must fit into a puzzle of ever-increasing complexity. Each new request is harder to fit than the last, because the shape of the system does not match the shape of the request.

I'm using the word「shape」here in a unconventional way, but I think the metaphor is apt. Software developers often feel as if they are forced to jam square pegs into round holes.

The problem, of course, is the architecture of the system. The more this architecture prefers one shape over another, the more likely new features will be harder and harder to fit into that structure. Therefore architectures should be as shape agnostic are practical.

架构价值

软件系统的第二个价值维度，就体现在软件这个英文单词上：software。ware 的意思是「产品」，而 soft 的意思，不言而喻，是指软件的灵活性。软件系统必须保持灵活。软件发明的目的，就是让我们可以以一种灵活的方式来改变机器的工作行为。对机器上那些很难改变的工作行为，我们通常称之为硬件（hardware）。

为了达到软件的本来目的，软件系统必须够「软」一一 也就是说，软件应该容易被修改。当需求方改变需求的时候，随之所需的软件变更必须可以简单而方便地实现。变更实施的难度应该和变更的范畴（scope）成等比关系，而与变更的具体形状（shape）无关。需求变更的范畴与形状，是决定对应软件变更实施成本高低的关键。这就是为什么有的代码更的成本与其实现的功能改不成比例。这也是为什么第二年的研发成本比第一年的高很多，第三年又比第二年更高。

从系统相关方（Stakeholder）的角度来看，他们所提出的一系列的变更需求的范畴都是类似的，因此成本也应该是固定的。但是从研发者角度来看，系统用户持续不断的变更需求就像是要求他们不停地用一堆不同形状的拼图块，拼成一个新的形状。整个拼图的过程越来越困难，因为现有系统的形状永远和需求的形状不一致。

我们在这里使用了「形状」这个词，这可能不是该词的标准用法，但是其寓意应该很明确。毕竟，软件工程师们经常会觉得自己的工作就是把方螺丝拧到圆螺丝孔里面。问题的实际根源当然就是系统的架构设计。如果系统的架构设计偏向某种特定的「形状」，那么新的变更就会越来越难以实施。所以，好的系统架构设计应该尽可能做到与「形状」无关。

### 2.3 The Greater Value

Function or architecture? Which of these two provides the greater value? Is it more important for the software system to work, or is it more important for the software system to be easy to change?

If you ask the business managers, they'll often say that it's more important for the software system to work. Developers, in turn, often go along with this attitude. But it's the wrong attitude. I can prove that it is wrong with the simple logical tool of examining the extremes.

If  you give me a program that works perfectly but is impossible to change, then it won't work when the requirements change, and I won't be able to make it work. Therefore the program will become useless.

If  you give me a program that does not work but is easy to change, then I can make it work, and keep it working as requirements change. Therefore the program will remain continually useful.

You may not find this argument convincing. After all, there's no such thing as a program that is impossible to change. However, there are systems that are practically impossible to change, because the cost of change exceeds the benefit of change. Many systems reach that point in some of their features or configurations.

If you ask the business managers if they want to be able to make changes, they'll say that of course they do, but may then qualify their answer by noting that the current functionality is more important than any later flexibility. In contrast, if the business managers ask you for a change, and your estimated costs for that change are unaffordably high, the business managers will likely be furious that you allowed the system to get to the point where the change was impractical.

哪个价值维度更重要

那么，究竟是系行为更重要，还是系统架构的灵活性更重要？哪个价值更大？系統正常工作更重要，还是系统易于修改更重要？

如果这个问题由业务部门来回答，他们通常认为系正常工作很重要。系统开发人员常常也就跟随采取了这种态度。但是这种态度是错误的。下面我就用简单的逻辑推导来证明这个态度的错误性。

1、如果某程序可以正常工作，但是无法修改，那么当需求交更的时候它就不再能够正常工作了，我们也无法通过修改让它能续正常工作。因此，这个程序的价值将成为 0。

2、如果某程序目前无法正常工作，但是我们可以很容易地修改它，那么将它改好，并且随着需求变化不停地修它，都应该是很易的事。因此，这个程序会持续产生价值。

当然，上面的逻辑论断可能不足以说服大家，毕竟理论上没有什么程序是不能修改的。但是，现实中有一些系統确实无法更改，因为其变更实施的成本会远远超过变更来的价值。你在实际工作中一定遇到过很多这样的例子。

如果你问业务部门，是否想要能够变更需求，他们的回答一般是肯定的，而且他们会增加一句：完成现在的功能比实现未来的灵活度更重要。但讽刺的是，如果事后业务部门提出了一项需求，而你的预估工作量大大超出他们的预期，这帮家伙通常会对你放任系混乱到无法变更的状态而勃然大怒。

### 2.4 Eisenhower's Matrix

Consider President Dwight D. Eisenhower's matrix of importance versus urgency (Figure 2.1). Of this matrix, Eisenhower said: I have two kinds of  problems, the urgent and the important. The urgent are not important, and the important are never urgent. 1

Figure 2.1  Eisenhower matrix

There is a great deal of truth to this old adage. Those things that are urgent are rarely of great importance, and those things that are important are seldom of great urgency.

The first value of software — behavior — is urgent but not always particularly important.

The second value of software — architecture — is important but never particularly urgent.

Of course, some things are both urgent and important. Other things are not urgent and not important. Ultimately, we can arrange these four couplets into priorities: 1) Urgent and important. 2) Not urgent and important. 3) Urgent and not important. 4) Not urgent and not important.

Note that the architecture of the code — the important stuff — is in the top two positions of this list, whereas the behavior of the code occupies the first and third positions.

The mistake that business managers and developers often make is to elevate items in position 3 to position 1. In other words, they fail to separate those features that are urgent but not important from those features that truly are urgent and important. This failure then leads to ignoring the important architecture of the system in favor of the unimportant features of the system.

The dilemma for software developers is that business managers are not equipped to evaluate the importance of architecture. That's what software developers were hired to do. Therefore it is the responsibility of the software development team to assert the importance of architecture over the urgency of features.

1 From a speech at Northwestern University in 1954.

艾森豪威尔矩阵

我们来看美国前总统艾森豪威尔的紧急/重要矩阵（参见图 2.1），面对这个矩阵，艾森豪威尔曾说道：我有两种难题：急的和重要的，而紧急的难永远是不重要的，重要的难题永远是不紧急的。

虽然老调重弹，但其中的道理依然成立。确实，紧急的事情常常没那么重要，而重要的事情则似乎永远也排不上优先级次件系统的第值维度系统行为，是紧急的，但是并不总是特别重要件系的第二个价值维度：系統架构，是重要的，但是并不总是特别紧急。

当然，我们会有些重要且紧急的事情，也会有一些事情不重要也不紧急。最终我们应将这四类事情进行如下排序：1）重要且紧急。2）重要不紧急。3）不重要但紧急。4）不重要且不紧急。

在这里你可以看到，软件的系统架构 一一 那些重要的事情一占据了该列表的前两位，而系统行为那些紧急的事情占据了第一和第三位。

业务部门与研发人员经常犯的共同错误就是将第三优先级的事情提到第一优先级去做。换句话说，他们没有把真正紧急并且重要的功能和紧急但是不重要的功能分开。这个错误导致了重要的事被忽略了，重要的系统架构问题让位给了不重要的系统行为功能。但研发人员还忘了一点，那就是业务部门原本就是没有能力评估系架构的重要程度的，这本来就应该是研发人员自己的工作职责！所以，平衡系统架构的重要性与功能的紧急程度这件事，是软件研发人员自己的职责。

### 2.5 Fight for the Architecture

Fulfilling this responsibility means wading into a fight — or perhaps a better word is「struggle.」Frankly, that's always the way these things are done. The development team has to struggle for what they believe to be best for the company, and so do the management team, and the marketing team, and the sales team, and the operations team. It's always a struggle.

Effective software development teams tackle that struggle head on. They unabashedly squabble with all the other stakeholders as equals. Remember, as a software developer, you are a stakeholder. You have a stake in the software that you need to safeguard. That's part of your role, and part of your duty. And it's a big part of why you were hired.

This challenge is doubly important if you are a software architect. Software architects are, by virtue of their job description, more focused on the structure of the system than on its features and functions. Architects create an architecture that allows those features and functions to be easily developed, easily modified, and easily extended.

Just remember: If architecture comes last, then the system will become ever more costly to develop, and eventually change will become practically impossible for part or all of the system. If that is allowed to happen, it means the software development team did not fight hard enough for what they knew was necessary.

为好的软件架构而持续斗争

为了做好上述职责，软件团队必须做好斗争的准备 一一 或者说「长期抗争」的准备。现状就是这样。研发团队必须从公司长远利益出发与其他部门抗争，这和管理团队的工作甚至市场团队、销售团队、运营团队都是这样。公司内部的抗争本来就是无止境的。

有成效的软件研发团队会迎难而上，毫不掩饰地与所有其他的系统相关方进行平等的争吵。请记住，作为一名软件开发人员，你也是相关者之ー。软件系统的可维护性需要由你来保护，这是你角色的一部分，也是你职责中不可缺少的一部分。公司雇你的很大一部分原因就是需要有人来做这件事。如果你是软件架构师，那么这项工作就加倍重要了。软件架构师这一职责本身就应更关注系统的整体结构，而不是具体的功能和系统行为的实现。软件架构师必须创建出一个可以让功能实现起来更容易、修改起来更简单、扩展起来更轻松的软件架构。请记住：如果忽视软件架构的价值，系统将会变得越来越难以维护，终会有一天，系统将会变得再也无法修改。如果系统变成了这个样子，那么说明软件开发团队没有和需求方做足够的抗争，没有完成自己应尽的职责。
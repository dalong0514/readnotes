## 记忆时间

## 目录

0101 Divide and conquer

分而治之法

0201 Abstraction

抽象

Part I Organizing complexity

We cannot find much insight staring at a mess. We need to organize it. As an everyday example, when I look at my kitchen after a dinner party, I feel overwhelmed. It's late, I'm tired, and I dread that I will not get enough sleep. If I clean up in that scattered state of mind, I pick up a spoon here and a pot there, making little progress. However, when I remember that a large problem can be broken into smaller ones, calm and efficiency return.

I begin at one corner of the kitchen, clear its mess, and move to neighboring areas until the project is done. I divide and conquer (Chapter 1).

Once the dishes are clean, I resist the temptation to dump them into one big box. I separate pots from the silverware and, within the silverware, the forks from the spoons. These groupings, or abstractions (Chapter 2), make the kitchen easy to understand and use.

In problem solving, we organize complexity by using divide-and-conquer reasoning and by making abstractions. In Part I, you'll learn how.

## 0101. Divide and conquer

As imperial rulers knew, you need not conquer all your enemies at once.

Instead, conquer them one at a time. Break hard problems into manageable pieces. This process embodies our first reasoning tool: Divide and conquer!

0101 分而治之法

正如帝国的统治者们深谙的道理，不必一下子征服所有的敌人，而是应该逐一征服他们，你可以将一个难题分解为一些小的、可以处理的问题。这个过程体现了我们的第一个分析工具：分而治之法！

1『又见「分解」能力的重要性，自从听了郑烨的「任务分解」板块后，对此点感触实在太多。能将「东西」分解成颗粒度很细的都是大牛，做单元测试要分解、重构要分解、软件设计要分解、OKR 要分解，等等。』

### 1.8 Summary and further problems

The main lesson that you should take away is courage: No problem is too difficult. We just use divide-and-conquer reasoning to dissolve difficult problems into smaller pieces. (For extensive practice, see the varied examples in the Guesstimation books [47 and 48].) This tool is a universal solvent for problems social and scientific.

Problem 1.14 Per-capita land area

Estimate the land area per person for the world, for your home country, and for your home state or province.

Problem 1.15 Mass of the Earth

Estimate the mass of the Earth. Then look it up (p. xvii) to check your estimate.

Problem 1.16 Billion

How long would it take to count to a billion (109)?

Problem 1.17 Sweating

Estimate how much water you need to drink to replace water lost to evaporation, if you ride a bicycle vigorously for 1 hour. Represent your estimate as a divide-and-conquer tree. Hint: Humans are only about 25 percent efficient in generating mechanical work.

Problem 1.18 Pencil line

How long a line can you write with a pencil?

Problem 1.19 Pine needles

Estimate the number of needles on a pine tree.

Problem 1.20 Hairs

How many hairs are on your head?

1.8 小结和进一步的问题

本章的主旨是：没有什么问题是真正的难题。罗马帝国和大英帝国之所以能延续统治是让被征服的民族互相对立。分而治之法将难题分解为一些小问题。（更多例子，见参考文献 [10] 和 [11]）这个工具是对社会问题和科学问题都适用的普适方法。

题 1.14 人均土地面积。

估算全世界和你所在国家的人均土地面积。

题 1.15 地球的质量。

估算地球的质量。然后査找资料来验证你的估算。

题 1.16 10 亿。

从 1 数到 10 亿（10^9）需要多长时间？

题 1.17 出汗。

估算当你用力骑车 1 个小时后需要喝多少水来弥补因为蒸发而失去的水分。提示：人做机械功的效率只有 25%。

题 1.18 铅笔画线。

你用铅笔能画多长的线？

题 1.19 松针。

估算一棵松树上有多少松针？

题 1.20 头发。

你头上有多少根头发？

### 1.1 Warming up

To show how to use divide-and-conquer reasoning, we'll apply it to increasingly complex problems that illustrate its essential features. So we start with an everyday estimate.

What is, roughly, the volume of a dollar bill?

Volumes are hard to estimate. However, we should still make a quick guess.

Even an inaccurate guess will help us practice courage and, when we compare the guess with a more accurate estimate, will help us calibrate our internal measuring rods. To urge me on, I often imagine a mugger who holds a knife at my ribs, demanding,「Your guess or your life!」Then I judge it likely that the volume of a dollar bill lies between 0.1 and 10 cubic centimeters.

This range is wide, spanning a factor of 100. In contrast, the dollar bill's width probably lies between 10 and 20 centimeters — a range of only a factor of 2. The volume range is wider than the width range because we have no equivalent of a ruler for volume; thus, volumes are less familiar than lengths. Fortunately, the volume of the dollar bill is the product of lengths.

```
volume = width × height × thickness. (1.1)
```

The harder volume estimate becomes three easier length estimates — the benefit of divide-and-conquer reasoning.

The width looks like 6 inches, which is roughly 15 centimeters. The height looks like 2 or 3 inches, which is roughly 6 centimeters.

But before estimating the thickness, let's talk about unit systems.

Is it better to use metric or US customary units (such as inches, feet, and miles)?

Your estimates will be more accurate if you use the units most familiar to you. Raised in the United States, I judge lengths more accurately in inches, feet, and miles than in centimeters, meters, or kilometers. However, for calculations requiring multiplication or division — most calculations — I convert the customary units to metric (and often convert back to customary units at the end). But you may be fortunate enough to think in metric. Then you can estimate and calculate in a single unit system.

The third piece of the divide-and-conquer estimate, the thickness, is difficult to judge. A dollar bill is thin — paper thin.

But how thin is「paper thin」?

This thickness is too small to grasp and judge easily. However, a stack of several hundred bills would be graspable. Not having that much cash lying around, I'll use paper. A ream of paper, which has 500 sheets, is roughly 5 centimeters thick. Thus, one sheet of paper is roughly 0.01 centimeters thick. With this estimate for the thickness, the volume is approximately 1 cubic centimeter:

Although a more accurate calculation could adjust for the fiber composition of a dollar bill compared to ordinary paper and might consider the roughness of the paper, these details obscure the main result: A dollar bill is 1 cubic centimeter pounded paper thin.

To check this estimate, I folded a dollar bill until my finger strength gave out, getting a roughly cubical packet with sides of approximately 1 centimeter — making a volume of approximately 1 cubic centimeter!

In the preceding analysis, you may have noticed the = and ≈ symbols and their slightly different use. Throughout this book, our goal is insight over accuracy. So we'll use several kinds of equality symbols to describe the accuracy of a relation and what it omits. Here is a table of the equality symbols, in descending order of completeness and often increasing order of usefulness.

As examples of the kinds of equality, for the circle below, 𝐴 = 𝜋𝑟2, and 𝐴 ≈ 4𝑟2, and 𝐴 ∼ 𝑟2. For the cylinder, 𝑉 ∼ ℎ𝑟2 — which implies 𝑉 ∝ 𝑟2 and 𝑉 ∝ ℎ. In the 𝑉 ∝ ℎ form, the factor hidden in the ∝ symbol has dimensions of length squared.

Problem 1.1 Weight of a box of books

How heavy is a small moving-box filled with books?

Problem 1.2 Mass of air in your bedroom

Estimate the mass of air in your bedroom.

Problem 1.3 Suitcase of bills

In the movies, and perhaps in reality, cocaine and elections are bought with a suitcase of `$`100 bills. Estimate the dollar value in such a suitcase.

Problem 1.4 Gold or bills?

As a bank robber sitting in the vault planning your getaway, do you fill your suitcase with gold bars or `$`100 bills? Assume first that how much you can carry is a fixed weight. Then redo your analysis assuming that how much you can carry is a fixed volume.

1.1 热身

我们将通过一系列复杂程度逐渐增加的问题来说明如何使用这个工具。从日常生活中的估算开始吧。

➤ 一元纸币的体积近似是多少？

体积是难以估算的，但是，我们仍然应该作一快速的估算。即使一个不太精确的估算，也将帮助我们建立进行实践的勇气。并且，将我们的估算与更精确的估算比较将帮助我们校准我们内部的测量基准。为了逼自己，我常常想像有一个抢劫犯拿着一把刀顶着我的肋部，要求道，「快给出你的估算，不然要你的命！」于是我就判断一元纸币的体积很可能在 0.1 和 10 厘米<sup>3</sup>之间。

1『 MD 文件里原来可以使用 sup 标签来表示上标，同理，sub 标签表示下标，哈哈。补充：还支持 Math 公式，比如上标使用美元符号包裹。（2022-05-16）』

这个估算范围有点宽，最大、最小估值相差达到 100 倍。作为对比元纸币的宽度大概在 10 到 20 厘米之间 一一 这只有 2 倍的差别！体积的估算范围要大于宽度的估算范围，因为我们并没有一把类似的可以直接量体积的「尺」，所以相对长度而言，我们对体积的估算较为陌生。幸运的是，纸币的体积是三个长度的乘积：

```
体积=长度×宽度×厚度
```

难以估算的体积变成了相对容易的对三个长度的估算 一一 这就是分而治之法的好处。前两个长度的估算不难。长度看上去在 6 英寸或 15 厘米左右，宽度看上去大概 2 到 3 英寸，或大概 6 厘米。在继续对第三个尺度估算之前，我们先来讨论单位的问题。

➤ 用英制好还是用公制好？

在估算的时候使用对你来说更为直观的单位，你的估算结果将更为准确。因为从小在美国长大，我判断长度更多的是用英寸、英尺、英里而不是用厘米、米、公里。但在需要用到乘除法计算的时候 一一 大多数计算会用到乘除法 一一 我会将英制转换为公制（最后常常会再转换到英制）。但你可能幸运地只需用公制来思考，因而可以只在一种单位制中进行估计和计算。分而治之法的第三个量 一一 厚度，是难以判断的。一张纸币是很薄的，只有一张纸那么薄。

➤ 但是「一张纸的厚度」究竟是多少呢？

这个厚度太小了，很难有直观的把握，不容易判断。但是一叠几百张纸币的厚度就容易把握了。手头没有那么多纸币，我就用纸代替。一包纸，有 500 张，大约有 5 厘米厚。于是，一张纸的厚度大概是 0.01 厘米有了对厚度的估算，纸币的体积近似为 1 厘米<sup>3</sup>：

尽管更加细致的计算甚至可以考虑到纸币和普通纸张的纸质不同，也可以考虑纸张的平整度等，但这些细节反而会使主要结果变得模糊：一元纸币其实就是将 1 立方厘米的东西砸平后的样子。为了验证刚才的估算，我用尽手指的力气将一元纸币折叠成大约 1 厘米见方的立方体，因此得到其体积近似为 1 厘米。分而治之法得到的结果是相当精确的。

在前面的分析中，你可能注意到了符号「=」和「≈」，以及这两个符号使用上的细微差异。本书从头至尾关注的是洞察力，而不是精确度。为此目的，我们将使用好几个等价符号，来描述某种关系成立的精确度和忽略的部分。下面按描写完整性减少（通常也是适用性增加）的顺序给出这些符号。

作为这些符号的例子，对于圆，有 `A=xr2` 和 `A≈4r2`（面积近似为外切正方形的面积）以及 `A~r2`。对圆柱体，有 `V~hr2`，—— 这隐含了 `V∞h `和 `V∞r2`。在 `V∞h` 的形式中，隐藏在符号 ∞ 中的因子具有长度平方的量纲。

题 1.1 一箱书的重量。

一个可移动的小箱子装满书后有多重？

题 1.2 卧室里的空气质量。

估算你卧室里的空气质量。

题 1.3 钱箱。

在电影或现实生活中，可卡因和选票常常用一箱子 100 元钞票来购买。估算这样一箱钱的价值。

题 1.4 金条还是纸币？

如果你是一个大盗，正在银行地下金库准备逃跑，你是将你的箱子装满金条还是装满 100 元的纸币？假定你能携带的最大重量是固定的。接着再假定你能携带的最大体积是固定的，重做以上分析。

### 1.2 Rails versus roads

We are now warmed up and ready to use divide-and-conquer reasoning for more substantial estimates. Our next estimate, concerning traffic, comes to mind whenever I drive the congested roads to JFK Airport in New York City. The route goes on the Van Wyck Expressway, which was planned by Robert Moses. As Moses's biographer Robert Caro describes [6, pp. 904ff], when Moses was in charge of building the expressway, the traffic planners recommended that, in order to handle the expected large volume of traffic, the road include a train line to the then-new airport. Alternatively, if building the train track would be too expensive, they recommended that the city, when acquiring the land for the road, still take an extra 50 feet of width and reserve it as a median strip for a train line one day. Moses also rejected the cheaper proposal. Alas, only weeks after its opening, not long after World War Two, the rail-free highway had reached peak capacity.

Let's use our divide-and-conquer tool to compare, for rush-hour commut-ing, the carrying capacities of rail and road. The capacity is the rate at which passengers are transported; it is passengers per time. First we'll estimate the capacity of one lane of highway. We can use the 2-second-following rule taught in many driving courses. You are taught to leave 2 seconds of travel time between you and the car in front. When drivers follow this rule, a single lane of highway carries one car every 2 seconds. To find the carrying capacity, we also need the occupancy of each car. Even at rush hour, at least in the United States, each car carries roughly one person. (Taxis often have two people including the driver, but only one person is being transported to the destination.) Thus, the capacity is one person every 2 seconds. As an hourly rate, the capacity is 1800 people per hour: 

The diagonal strike-through lines help us to spot which units cancel and to check that we end up with just the units that we want (people per hour).

This rate, 1800 people per hour, is approximate, because the 2-second following rule is not a law of nature. The average gap might be 4 seconds late at night, 1 second during the day, and may vary from day to day or from highway to highway. But a 2-second gap is a reasonable compromise estimate. Replacing the complex distribution of following times with one time is an application of lumping — the tool discussed in Chapter 6. Organizing complexity almost always reduces detail. If we studied all highways at all times of day, the data, were we so unfortunate as to obtain them, would bury any insight.

How does the capacity of a single lane of highway compare with the capacity of a train line?

For the other half of the comparison, we'll estimate the rush-hour capacity of a train line in an advanced train system, say the French or German system.

As when we estimated the volume of a dollar bill (Section 1.1), we divide the estimate into manageable pieces: how often a train runs on the track, how many cars are in each train, and how many passengers are in each car. Here are my armchair estimates for these quantities, kept slightly conservative to avoid overestimating the train-line's capacity. A single train car, when full at rush hour, may carry 150 people. A rush-hour train may consist of 20 cars.

And, on a busy train route, a train may run every 10 minutes or six times per hour. Therefore, the train line's capacity is 18 000 people per hour: 

This capacity is ten times the capacity of a single fast-flowing highway lane.

And this estimate is probably on the low side; Robert Caro [6, p. 901] gives an estimate of 40 000 to 50 000 people per hour. Using our lower rate, one train track in each direction could replace two highways even if each highway had five lanes in each direction.

1.2 铁路与公路

我们现在已经进行了热身并准备好用分而治之法去进行更多估算。我们下一个估算是关于交通的。每当我开车行驶在去往纽约肯尼迪国际机场的拥挤道路上时，就会有这个想法。这条高速公路是罗伯特·摩西（Robert Moses）规划的。正如其传记作者罗伯特·卡罗（Robert Caro）所描述的，摩西当年负责范威克高速公路的建设，一些年轻的规划师建议铺设一条铁路线到新机场（即现在的组约肯尼迪国际机场）以应对将来的大流量交通。但如果认为铁路线造价太高的话，鉴于土地价格仍然便宜，他们建议市政府在征地建设公路时，将其多拓宽 50 英尺，以备将来建设铁路线之用。摩西否决了这个省钱的方案。果不其然，仅仅在开通后的几个星期，二战后不久，这条没有铁路的新高速公路就达到了容量峰值。

让我们利用分而治之法来比较高峰时段铁路和公路的运输能力。运输能力指运输乘客的效率（单位时间可输送的乘客）。

首先我们来估算高速公路上一条车道的运输能力。我们可以使用在许多驾驶课程上所教并在驾照考试中被验证的规则：2 秒跟随规则。这个规则推荐我们每辆车和前车之间留 2 秒的行驶时间。如果驾驶员都遵守这个规则，那么高速公路上每条车道每 2 秒通过一辆车。至少在美国，每辆车大约输送 1 名乘客，因此运输能力是每 2 秒输送 1 人。按小时算运输能力为每小时 1800 人：

斜线使我们看清单位的相消并可验证最后出现的是我们所需要的单位（这里是人/小时)。

这里，1800 人/小时的运输能力是近似值，因为 2 秒跟随规则并不是法定规则。晚上的平均间隔可能是 4 秒，白天可能是 1 秒，并且可能每天都有变化，每条高速公路都会有所不同。但是 2 秒间隔是一个合理的折中估算。将复杂的、随时间变化的分布用一段时间来代替是团块化的应用，这个工具将在第 6 章讨论。整理复杂性的过程总是要扔掉一些细节。如果我们将高速公路在任意时间的所有数据都拿来研究的话，就会淹没所有的洞察，幸亏我们拿不到这些数据。

➤ 一条车道的公路运输能カ与一条铁路的运输能力相比如何？

现在我们来估算一下现代化铁路系统比如法国或德国的铁路系统中一条铁路线的运输能力。我们还是将估算过程分解为一些可以处理的部分：铁路线上列车开行密度，一列火车有几节车厢，每节车厢能容纳多少乘客。

下面是我坐在椅子上给出的估算，为了避免过高估算运输能力而有所保守。一节车厢大约能容纳 150 名乘客，而一列火车可以有 20 节车厢。在一条比较繁忙的铁路线上，每 10 分钟可开行一列火车，即每小时开行 6 趟列车。因此，一条铁路线的运输能力是每小时 18000 人。

### 1.3 Tree representations

Our estimates for the volume of a dollar bill (Section 1.1) and for the rail and highway capacities (Section 1.2) used the same method: dividing hard problems into smaller ones. However, the structure of the analysis is buried within the sentences, paragraphs, and pages. The sequential presentation hides the structure. Because the structure is hierarchical — big problems split, or branch, into smaller problems — its most compact representation is a tree. A tree representation shows us the analysis in one glance.

Here is the tree representation for the capacity capacity of a train line. Unlike the biological variety, our trees stand on their head. Their roots, the goals, sit at the top of the tree. Their leaves, the small problems into which we have subdivided the goal, sit at the bottom. The orientation matches the way that we divide and conquer, filling the page downward as we subdivide.

In making this first tree, we haven't estimated capacity the quantities themselves. We have only identified the quantities. The question marks remind us of our next step: to include estimates for the three leaves. These estimates were 150 people 150 people 20 cars per car, 20 cars per train, and 6 trains per hour (giving the tree in the margin).

Then we multiplied the leaf values to propagate the estimates upward from the leaves toward the root. The result was 18 000 people per hour.

The completed tree shows us the entire estimate in one glance.

This train-capacity tree had the simplest possible structure with only two layers (the root layer and, as the second layer, the three leaves). The next level of complexity is a three-layer tree, which will represent our estimate for the volume of a dollar bill. It started as a two-layer tree with three leaves.

Then it grew, because, unlike the width and height, the thickness was difficult to estimate just by looking at a dollar bill. Therefore, we divided that leaf into two easier leaves.

The result is the tree in the margin. The thickness leaf, which is the thickness per sheet, has split into (1) the thickness per ream and (2) the number of sheets per ream. The boxed −1 on the line connecting the thickness to the number of sheets per ream is a new and useful notation. The −1 tells us the exponent to apply to that leaf value when we propagate it upward to the root.

Here is why I write the −1 as a full-sized number rather than a small superscript. Most of our estimates require multiplying several factors. The only question for each factor is,「With what exponent does this factor enter?」The number −1 directly answers this「What exponent?」question. (To avoid cluttering the tree, we don't indicate the most-frequent exponent of 1.) This new subtree then represents the following equation for the thickness of one sheet:

(1.5)

The −1 exponent allows, at the cost of a slight complication in the tree notation, the leaf to represent the number of sheets per ream rather than a less-familiar fraction, the number of reams per sheet.

Now we include our estimates for the leaf values. The width is 15 centimeters. The height is 6 centimeters. The thickness of a ream of paper is 5 centimeters. And a ream contains 500 sheets of paper. The result is the following tree.

Now we propagate the values to the root. The two bottommost leaves combine to tell us that the thickness of one sheet is 10$^−2$ centimeters. This thickness completes the tree's second layer. In the second layer, the three nodes tell us that the volume of a dollar bill — the root — is 1 cubic centimeter.

With practice, you can read in this final tree all the steps of the analysis. The three nodes in the second layer show how the difficult volume estimate was subdivided into three easier estimates. That the width and height remained leaves indicates that these two estimates felt reliable enough. In contrast, the two branches sprouting from the thickness indicate that the thickness was still hard to estimate, so we divided that estimate into two more-familiar quantities.

The tree encapsulates many paragraphs of analysis in a compact form, one that our minds can absorb in a single glance. Organizing complexity helps us build insight.

Problem 1.5 Tree for the suitcase of bills

Make a tree diagram for your estimate in Problem 1.3. Do it in three steps: (1) Draw the tree without any leaf estimates, (2) estimate the leaf values, and (3) propagate the leaf values upward to the root.

1.3 树图

我们对纸币体积的估算（章节 1.1）和对铁路与高速公路运输能力的分析（章节 1.2）用的是同一种方法：将一个难题分解为几个小问题。但是，整个分析的结构被淹没在字里行间。按部就班的叙述隐藏了结构。因为结构是有层次的 一一 大问题分解或肢解为一些小问题 一一 最紧湊的表示就是树图表示。树图可以让整个分析一目了然。

以下是铁路运输能力的树图。与生物学中的树不同，我们的树是倒立的。树根，即目标，位于树的最顶端；树叶，即分解得到的小问题，位于树的底部。这样的取向与我们如何分而治之问题的过程相符在第一幅图中，我们没有估计各个量的数值，而只是确认了有哪些相关量。这提示我们下一步如何做，即在图上标出三个树叶的估算值。这些估算值为毎车厢 150 人，每一列火车 20 个车厢，每小时开行 6 列火车。

然后将这些树叶的值相乘，结果就由树叶向上传递到树根。结果为 18000人/小时。完整的树图让我们一眼就看清了整个分析。这个列车运输能力的树图具有最简单的结构，只有两个层次（即树根层和第二层即三个树叶）。进一步的复杂性就需要具有三个层次的树图了，如对纸币体积的估算。先从下面具有三个树叶的两层树图出发。然后，因为下面的原因，树图开始继续生长。

不像宽度和长度，只看一眼纸币很难给出厚度的估算。因此，我们将这个树叶进一步分解为两个树叶。连接「厚度」和「??张/包」的有向直线上标有「-1」的方框是一个新符号。这个符号在我们自下而上计算时表示相应树叶值的幂次。

这里给出为什么将「-1」写成一个数而不是上标的原因。在大多数估算的情形中需要将一些因子相乘。对每个因子而言，唯一的问题是：在计算时这些因子的幂次是多少。「-1」这个数直接给出了关于幂次的疑问。（为了避免把树图弄得过于凌乱，我们不标注最常见的幂次 1）

这个新的子树图代表下列计算一张纸厚度的方程：

-1 次幂的引入，虽然使树图变得有点复杂，但使得树叶可以表示「每包的纸张数」，而不是「每张纸的包数」这样不够直观的数。现在将对树叶的估算值代入。长度为 15 厘米，宽度为 6 厘米。一包纸的厚度为 5 厘米，一包有 500 张纸。结果给出下面的树图。

最后，我们将树叶的值传递到树根。第三层的两个树叶给出一张纸的厚度为 10^(-2) 厘米。这个值填补了之前厚度的空缺。第二层的三个节点则告诉我们纸币的体积 一一 即树根的节点 一一 为 1 厘米^3。

通过练习，你可以从最后的树图看出分析的所有步骤。例如，第二层的三个节点表示将对体积的估算分解为对三个较容易的量的估算。长度和宽度保留为树叶意味着对这两个量的估算已经足够精确。相反，从厚度分又的两个分支意味着厚度难以估算，因此将其分解为两个更熟悉的量来进行估算。树图可以将许多分析文字压缩成紧凑的形式某种我们一眼就能看清整个思路的形式。整理复杂性的过程帮助我们构建洞察力。

画出你对题 1.3 估算的树图。分三步来做：1) 画出没有树叶值的树图；2) 估算树叶值；3) 自下而上将树叶值传递到树根。

### 1.4 Demand-side estimates

Our analysis of the carrying capacity of highways and railways (Section 1.2) is an example of a frequent application of estimation in the social world — estimating the size of a market. The highway–railway comparison proceeded by estimating the transportation supply. In other problems, a more feasi-ble analysis is based on the complementary idea of estimating the demand.

Here is an example.

How much oil does the United States import (in barrels per year)?

The volume rate is enormous and therefore hard to picture. Divide-and-conquer reasoning will tame the complexity. Just keep subdividing until the quantities are no longer daunting.

Here, subdivide the demand — the consumption. We consume oil in so many ways; estimating the consumption in each pathway would take a long time without producing much insight. Instead, let's estimate the largest consumption — likely to be cars — then adjust for other uses and for overall consumption versus imports.

Here is the corresponding tree. The first factor, the most difficult of the three to estimate, will require us to sprout branches and make a subtree. The second and third factors might be possible to estimate without subdividing.

Now we must decide how to continue.

Should we keep subdividing until we've built the entire tree and only then estimate the leaves, or should we try to estimate these leaves and then subdivide what we cannot estimate?

It depends on one's own psychology. I feel anxious in the uncharted waters of a new estimate. Sprouting new branches before making any leaf estimates increases my anxiety. The tree might never stop sprouting branches and leaves, and I'll never estimate them all. Thus, I prefer to harvest my progress right away by estimating the leaves before sprouting new branches.

You should experiment to learn your psychology. You are your best problem-solving tool, and it is helpful to know your tools.

Because of my psychology, I'll first estimate a leaf quantity: 

```
all usage/car usage. (1.7)
```

But don't do this estimate directly. It is more intuitive — that is, easier for our gut — to estimate first the ratio of car usage to other (noncar) usage. The ability to make such comparisons between disjoint sets, at least for physical objects, is hard wired in our brains and independent of the ability to count. Not least, it is not limited to humans. The female lions studied by Karen McComb and her colleagues [35] would judge the relative size of their troop and a group of lions intruding on their territory. The females would approach the intruders only when they outnumbered the intruders by a large-enough ratio, roughly a factor of 2.

Other uses for oil include noncar modes of transport (trucks, trains, and planes), heating and cooling, and hydrocarbon-rich products such as fer-tilizer, plastics, and pesticides. In judging the relative importance of other uses compared to car usage, two arguments compete: (1) Other uses are so many and so significant, so they are much more important than car usage; and (2) cars are so ubiquitous and such an inefficient mode of transport, so car usage is much larger than other uses. To my gut, both arguments feel comparably plausible. My gut is telling me that the two categories have comparable usages:

```
other usage / car usage ≈ 1. (1.8)
```

Based on this estimate, all usage (the sum of car and other usage) is roughly double the car usage:

```
all usage / car usage ≈ 2. (1.9)
```

This estimate is the first leaf. It implicitly assumes that the gasoline fraction in a barrel of oil is high enough to feed the cars. Fortunately, if this assumption were wrong, we would get warning. For if the fraction were too low, we would build our transportation infrastructure around other means of transport — such as trains powered by electricity generated by burning the nongasoline fraction in oil barrels. In this probably less-polluted world, we would estimate how much oil was used by trains.

Returning to our actual world, let's estimate the second leaf: 

```
imports / all usage. (1.10)
```

This adjustment factor accounts for the fact that only a portion of the oil consumed is imported.

What does your gut tell you for this fraction?

Again, don't estimate this fraction directly. Instead, to make a comparison between disjoint sets, first compare (net) imports with domestic production.

In estimating this ratio, two arguments compete. On the one hand, the US media report extensively on oil production in other countries, which suggests that oil imports are large. On the other hand, there is also extensive coverage of US production and frequent comparison with countries such as Japan that have almost no domestic oil. My resulting gut feeling is that the categories are comparable and therefore that imports are roughly one-half of all usage:

(1.11)

This leaf, as well as the other adjustment factor, are dimensionless numbers.

Such numbers, the main topic of Chapter 5, have special value. Our percep-tual system is skilled at estimating dimensionless ratios. Therefore, a leaf node that is a dimensionless ratio probably does not need to be subdivided.

The tree now has three leaves. Having plausible estimates for two of them should give us courage to subdivide the remaining leaf, the total car usage, into easier estimates. That leaf will sprout its own branches and become an internal node.

How should we subdivide the car usage?

A reasonable subdivision is into the number of cars 𝑁cars and car usage the per-car usage. Both quantities are easier to estimate than the root. The number of cars is related to the US population — a familiar number if you live in the United States. The per-car usage is easier to estimate than is the total usage of all US cars. Our gut can more accurately judge human-scale quantities, such as the per-car usage, than it can judge vast numbers like the total usage of all US cars.

For the same reason, let's not estimate the number of cars directly. Instead, subdivide this leaf into two leaves: 

1 the number of people, and

2 the number of cars per person.

The first leaf is familiar, at least to residents of the United States: 𝑁people ≈ 3×108.

The second leaf, cars per person, is a human-sized quantity. In the United States, car ownership is widespread. Many adults own more than one car, and a cynic would say that even babies seem to own cars. Therefore, a rough and simple estimate might be one car per person — far easier to picture than the total number of cars! Then 𝑁cars ≈ 3×108.

The per-car usage can be subdivided into three easier factors (leaves). Here are my estimates.

1 How many miles per car year? Used cars with 10 000 miles per year are considered low use but are not rare. Thus, for a typical year of car year driving, let's take a slightly longer distance: say, 20 000 miles or 30 000 kilometers.

2 How many miles per gallon? A typical car fuel efficiency is 30 miles per US gallon. In metric units, it is about 100 kilometers per 8 liters.

3 How many gallons per barrel? You might have seen barrels of asphalt along the side of the highway during road construction. Following our free-association tradition of equating the thickness of a sheet of paper and of a dollar bill, perhaps barrels of oil are like barrels of asphalt.

Their volume can be computed by divide-and-conquer reasoning. Just approximate the cylinder as a rectangular prism, estimate its three dimensions, and multiply: 

(1.12)

A cubic meter is 1000 liters or, using the conversion of 4 US gallons per liter, roughly 250 gallons. Therefore, 0.25 cubic meters is roughly 60 gallons. (The official volume of a barrel of oil is not too different at 42 gallons.) Multiplying these estimates, and not forgetting the effect of the two −1 exponents, we get approximately 10 barrels per car per year (also written as barrels per car year):

(1.13)

In doing this calculation, first evaluate the units. The gallons and miles cancel, leaving barrels per year. Then evaluate the numbers. The 30 × 60 in the denominator is roughly 2000. The 2 × 104 from the numerator divided by the 2000 from the denominator produces the 10.

This estimate is a subtree in the tree representing total car usage. The car usage then becomes 3 billion barrels per year: 3×108 cars × 10 barrels = 3×109 barrels.

(1.14)

This estimate is itself a subtree in the tree representing oil imports. Because the two adjustment factors contribute a factor of 2 × 0.5, which is just 1, the oil imports are also 3 billion barrels per year.

Here is the full tree, which includes the subtree for the total car usage of oil:

Problem 1.6 Using metric units

As practice with metric units (if you grew up in a nonmetric land) or to make the results more familiar (if you grew up in a metric land), redo the calculation using the metric values for the volume of a barrel, the distance a car is driven per year, and the fuel consumption of a typical car.

How close is our estimate to official values?

For the US oil imports, the US Department of Energy reports 9.163 million barrels per day (for 2010). When I first saw this value, my heart sank twice.

The first shock was the 9 in the 9 million. I assumed that it was the number of billions, and wondered how the estimate of 3 billion barrels could be a factor of 3 too small. The second shock was the「million」 — how could the estimate be more than a factor of 100 too large? Then the「per day」

reassured me. As a yearly rate, 9.163 million barrels per day is 3.34 billion barrels per year — only 10 percent higher than our estimate. Divide and conquer triumphs!

Problem 1.7 Fuel efficiency of a 747

Based on the cost of a long-distance plane ticket, estimate the following quantities: (a) the fuel efficiency of a 747, in passenger miles per gallon or passenger kilometers per liter; and (b) the volume of its fuel tank. Check your estimates against the technical data for a 747.

1.4 需求估算

我们对高速公路和铁路运输能力的分析（章节1.2）是现实社会中运用估算的一个常见例子 一一 即估算市场的规模。公路铁路的比较是这一例子的延续。在其他问题上，一个更实用的分析方法则建立在需求估算的概念基础之上。

➤ 美国进口的石油是多少（按每年桶数计算）?

这个体量相当巨大，因此难以刻画。而分而治之法将使复杂性变得简单。只要将难题不断分解，问题总能分解到不再复杂的地步。现在，我们来分解需求 一一 即消耗量。我们在太多的方面需要消耗石油；对每一种消耗石油的途径去估算不仅要花很长的时间，而且也不会得到太多的洞见。反之，我们来估算一下最大的消耗 一一 很可能就是汽车；然后再评估其他用途的消耗，以及总的消耗与进口之比。

以下为相应的树图。第一个因子是三个因子中最难估算的量，我们需要再生长出分支得到子树图。第二个和第三个因子不需要进一步分解就可给出估算结果。下面我们来看看怎么做。

➤ 我们是应该将整个树图都构建完毕后再来估算每个树叶的值呢，还是应该先来估算一个树叶的值，当无法估算时再将其进一步分解？

这取决于每个人的思维习惯。在进行新的估算时如果看到的都是未知量，我会感到忧虑。而在对一个树叶估算之前就长出新的分支会加重我的忧虑。这样似乎树图会永无止境不停地分叉下去，因而永远无法给出估算结果。因此，我更喜欢在生长出新的分支之前给出那些树叶的估算值，以及时得到每一步的结果。你应该通过实践来了解自己的习惯。你自己就是你解决问题最好的工具，熟悉你的工具是很有帮助的。

由于我的习惯，我会首先估算下面这个树叶的值：`石油总消耗量/汽车消耗石油量`。

但不是直接来估算这个值。从直觉上来说，更容易、更直观的做法是首先估算汽车消耗石油量和其他消耗量的比。对一些不相交的集合之间进行比较的能力已经固化在我们大脑中了，至少对具体的事物来说是这样，这与计数的能力无关。并且，也不局限于人类。卡伦·麦库姆（Karen Mccomb）和她的同事所研究的母狮们在外来狮群入侵它们的领地时，会判断自身数量和人侵狮群的多寡。只有当它们在数量上大大超过入侵者时，它们才会去攻击入侵者，这个比例大约是 2。

石油的其他消耗主要是非汽车运输（如卡车、火车和飞机），取暖和制冷，以及汽油产品如化肥、塑料和农药等。在判断汽车的消耗与其他消耗的相对比重时，有两种互相对立的说法：1）其他消耗比汽车消耗要多得多和重要得多，因此其他消耗量要大大超过汽车的消耗量；2）汽车已经无处不在，汽车的运输效率又是如此低下，因此汽车的消耗量要大大超过其他消耗量。

按照我的直觉，这两种说法都过于极端，有失偏颇。我的直觉告诉我，这两类消耗量是差不多的。基于这个估算，石油总消耗量（汽车和其他消耗之和）差不多是汽车消耗量的两倍。

这个估算是第一个树叶。这里隐含了一个假定，即一桶原油中汽油的含量足够高以用于汽车消耗。幸好，如果这个假定是错的，我们会得到警告。如果汽油含量太低的话，我们就会去建设其他基础运输体系 一一 如电力火车，其中电力可以通过燃烧原油中非汽油部分来产生。这很可能是污染较少的方式，据此我们就可以来估算火车会消耗多少原油。

回到我们的现实世界，先来估算第二个树叶的值。

```
进口石油量/石油总消耗量
```

这一项是考虑到这样的事实：在所有消耗的石油中只有一部分是进口的。

➤ 你的直觉告诉你，这个比例是多少？

与之前一样，不要直接估算这个比例。而是对彼此没有重叠的集合进行比较，首先比较进口量和国内产量。在估算这个比例时，两种理由也是对立的。一方面，美国的媒体广泛报道了其他国家的石油生产，这说明石油进口量是巨大的。另一方面，美国产品也是铺天盖地并且常常和日本这样几乎自己不产油的国家比较。我的直觉是这两大类基本上旗鼓相当，因此进口量大约是总消耗量的一半。

这个树叶以及前一个因子都是无量纲数。这类数（第 5 章的主要内容）具有特殊价值。我们的感觉系统擅长估算无量纲比例。因此，如果个树叶节点是一个无量纲比例的话，那很可能不需要进一步往下分解了。

树图现在有三个树叶。在成功地对其中两个树叶进行估算后应该能给我们一些勇气去分解剩下的树叶，汽车的石油总消耗量。这个树叶将会生长出自己的枝叶而变成中间节点。

➤ 我们应该如何分解汽车的石油消耗量？

一个合理的分解是将其分解为汽车的数量 N 和单车消耗量。这两个量都更容易估算。汽车数量和美国的人口相关 一一 如果你生活在美国，那么对这个数字是熟悉的。单车消耗的石油量比美国所有汽车的消耗总量要容易估算。我们的直觉会更准确地判断那些和人本身尺度相关的量，比如单车的消耗量，而不是数字巨大的那些量，比如总消耗量。

出于同样的理由，我们不是直接估算汽车的总数，而是将这个树叶再分解为两个树叶：1）人口数；2）每人拥有的汽车数。

第一个树叶是熟悉的，至少对美国人是这样：

```
N（人口）≈3×10^8
```

第二个树叶，每个人拥有的汽车数，是一个和「人本身尺度」相关的量。在美国，汽车是很普遍的，一个夸张的说法是甚至婴儿都拥有汽车，许多成年人拥有不止一辆车。一个粗略、简单的估算可以是每人一辆车。因此：

```
N（汽车）≈3×10^8
```

单车消耗可以进一步分解为三个更容易估计的因子（树叶）。下面是我对这些因子的估算。

1、每辆车的年里程数。对于旧车来说，没有特殊情况的话每年 10000 英里是相当少的。因此，稍微多一点，比如 20000 英里/年或 30000 公里/年，这是一个相当合理的估算。（最后计算选的 20000）

2、每加仑可行驶里程。一辆典型的汽车燃油效率是 30 英里/加仑。

3、每桶加仑数。你可能已经在修建高速公路时见过那些沥青桶。根据我们过去将一张纸的厚度等同于纸币的厚度的自由联想传统，或许一桶石油也和一桶沥青类似。

桶的体积可以利用分而治之法来计算。将圆柱体近似为长方体，估算三个维度的大小，然后相乘：

1 立方米等于 100 升，或者按每加仑等于 4 升来算，大约 250 加仑。因此，0.25 立方米大约是 60 加仑（官方数据每桶原油是 42 加仑，因此我们的估算是合理的）。把这些估值相乘，别忘了两个「-1」的幂次，我们得到每车每年大约消耗 10 桶。

在计算的时候，首先考虑单位。加仑和英里消去，然后计算数值。分母中的 30×60 大约为 2000。分子的 2×10^4 除以 2000 就得到结果 10。这个估算是汽车总石油消耗树图的一个子图。于是汽车消耗石油量就是每年 30 亿桶。

这个估算本身又是进口石油量树图的一个子图。因为另两个因子贡献值为 2×0.5, 正好是 1，所以每年进口石油量也是 30 亿桶。这里给出完整的树图，包括了各个子图。

题 1.6 使用公制。

作为公制的练习（如果你是在非公制国家长大的）或者为使结果更熟悉（如果你是在公制国家长大的），对桶的体积，一年行驶距离以及一辆典型汽车的燃油效率使用公制单位重新进行估算。

➤ 每年 30 亿桶的估算结果有多精确？

对于美国的石油进口，美国能源部的报告是每天 916.3 万桶（2010 年数据）。我第一次看到这个数据的时候，心沉了两次。第一次是看到「9」位于百万位上。我误以为是在 10 亿位上，还奇怪为什么 30 亿桶的估算结果会小了 3 倍。第二次是「百万」估算的结果怎么可能大了 100 倍以上呢？然后「每天」一词又重新让我找回自信。按年来算，每天 916.3 万桶就是每年 33.4 亿桶 一一 仅仅比我们的估算高了 10%。分而治之法再次取得胜利。

题 1.7 一架波音 747 的燃油效率。

根据长途机票的价格，估算下列量的值：a）波音 747 的燃油效率；b）油箱体积。

和波音 747 的技术参数对比来验证你的估算结果。

1 英里≈1.61 千米。 一一 译者注

1 加仑≈3.79 升。 一一 译者注

### 1.5 Multiple estimates for the same quantity 

After making an estimate, it is natural to wonder about how much confidence to place in it. Perhaps we made an embarrassingly large mistake. The best way to know is to estimate the same quantity using another method.

As an everyday example, let's observe how we add a list of numbers.

```
12
15
+18
(1.15)
```

We often add the numbers first from top to bottom. For 12 + 15 + 18, we calculate,「12 plus 15 is 27; 27 plus 18 is 45.」To check the result, we add the numbers in the reverse order, from bottom to top:「18 plus 15 is 33; 33 plus 12 is 45.」The two totals agree, so each is probably correct: The calculations are unlikely to contain an error of exactly the same amount. This kind of redundancy catches errors.

In contrast, mindless redundancy offers little protection. If we check the calculation by adding the numbers from top to bottom again, we usually repeat any mistakes. Similarly, rereading written drafts usually means overlooking the same spelling, grammar, or logic faults. Instead, stuff the draft in a drawer for a week, then look at it; or ask a colleague or friend — in both cases, use fresh eyes.

Reliability, in short, comes from intelligent redundancy.

This principle helps you make reliable estimates. First, use several methods to estimate the same quantity. Second, make the methods as different from one another as possible — for example, by using unrelated background knowledge. This approach to reliability is another example of divide-and-conquer reasoning: The hard problem of making a reliable estimate becomes several simpler subproblems, one per estimation method.

You saw an example in Section 1.1, where we estimated the volume of a dollar bill. The first method used divide-and-conquer reasoning based on the width, height, and thickness of the bill. The check was a comparison with a folded-up dollar bill. Both methods agreed on a volume of approximately 1 cubic centimeter — giving us confidence in the estimate.

For another example of using multiple methods, return to the estimate of the volume of an oil barrel (Section 1.4). We used a roadside asphalt barrel as a proxy for an oil barrel and estimated the volume of the roadside barrel. The result, 60 gallons, seemed plausible, but maybe oil barrels have a completely different size. One way to catch that kind of error is to use a different method for estimating the volume. For example, we might start with the cost of a barrel of oil — about `$`100 in 2013 — and the cost of a gallon of gasoline — about `$`2.50 before taxes, or 1/40th of the cost of a barrel. If the markup on gasoline is not significant, then a barrel is roughly 40 gallons. Even with a markup, we can still say that a barrel is at least 40 gallons.

Because our two estimates, 60 gallons and > 40 gallons, roughly agree, our confidence in both increases. If they had contradicted each other, one or both would be wrong, and we would look for the mistaken assumption, for the incorrect arithmetic, or for a third method.

1.5 对同一个量用多种方法进行估算

完成一个估算之后，很自然的我们想要知道估算的可靠性。或许我们犯了一个令人汗颜的大错。想知道估算是否正确的最好方式是用不同的方法对同一个量再估算一次。一个日常经验的例子，可以说明这个原则，来看看我们是如何对一组数字做加法的。

我们通常是从上往下加。对于 12+15+18，我们这样计算，「12 加 15 等于 27；27 加 18 等于 45。」为了验证这个结果，我们可以颠倒顺序，从下往上来加：「18 加 15 等于 33；33 加 12 等于 45。」两个结果完全一致，所以很可能是正确的。多次计算不太可能出现数字完全相同的错误。这种重复抓住了错误。

然而，盲目的重复几乎没有作用。如果我们通过从上到下再加一遍的方式来检验计算结果，我们常常会重复所有的错误。类似，重读一遍写好的文稿常常会忽略同样的拼写、语法或逻辑错误。反之，把文稿塞抽屉放一个星期，然后再看；或者请同事或朋友帮忙这两种情况，用的都是全新的眼睛。简言之，可靠性来自聪明的重复。

这个原则帮助你做可靠的估算。首先，用几个不同的方法估算同一个量。其次，使用彼此差异尽可能大的方法 一一 例如，利用背景知识没有关联的方法。这一达到可靠性的方法是分而治之法的另一个例子：进行可靠的估算这一难题变成了几个简单的子问题，而每个估算方法就是一个子问题。

1『可靠性来自聪明的重复，上面的信息做一张金句卡。』

你已经在章节 1.1 看到了例子，即估算纸币的体积。使用的第一个方法是基于纸币的长度，宽度和厚度的分而治之法。检验的方法是：和一张折叠的纸币进行比较。两种方法得到一致的结果，即纸币体积大约为 1 立方厘米这给了我们进行估算的自信。

使用多种方法的另一个例子，可以回到对油桶体积的估算（章节1.4)。我们用路边的沥青桶来代替原油桶，然后估算了沥青桶的体积。60 加仑的结果似乎还不错，但可能原油桶的大小是完全不同的。改进这类错误的一个方式是用不同的方法来估算体积。例如，我们可以从一桶原油的价格出发：2013 年约 100 美元，而一加仑汽油的价格税前约 2.5 美元，即一桶原油价格的 1/40。如果认为汽油的利润是不重要的，则一桶原油差不多 40 加仑。即使考虑到利润，我们仍然可以说，一桶原油至少是 40 加仑。由于这两种估算 一一 60 加仑和 40 加仑以上 一一 基本一致，我们对这两种方法的自信也就增加了。如果两种结果互相矛盾，那么或者其中一个或者两种方法都是错的，我们需要找出错误的假设，错误的计算，或者需要去寻找第三种方法。

### 1.6 Talking to your gut

As you have seen in the preceding examples, divide-and-con-quer estimates require reasonable estimates for the leaf quantities. To decide what is reasonable, you have to talk to your gut — what you will learn in this section. Talking to your gut feels strange at first, especially because science and engineering are considered cerebral subjects. Let's therefore discuss how to hold the conversation. The example will be an estimate of the US population based on its area and population density. The divide-and-conquer tree has two leaves. (In Section 6.3.1, you'll see a qualitatively different method, where the two leaves will be the number of US states and the population of a typical state.) 

The area is the width times the height, so the area leaf itself splits into two leaves. Estimating the width and height requires only a short dialogue with the gut, at least if you live in the United States. Its width is a 6-hour plane flight at 500 miles per hour, so about 3000 miles; and the height is, as a rough estimate, two-thirds of the width, or 2000 miles. Therefore, the area is 6 million square miles:

```
3000 miles × 2000 miles = 6×106 miles2. (1.16)
```

In metric units, it is about 16 million square kilometers.

Estimating the population density requires talking to your gut. If you are like me you have little conscious knowledge of the population density. Your gut might know, but you cannot ask it directly. The gut is connected to the right brain, which doesn't have language. Although the right brain knows a lot about the world, it cannot answer with a value, only with a feeling.

To draw on its knowledge, ask it indirectly. Pick a particular population density — say, 100 people per square mile — and ask the gut for its opinion:

「O, my intuitive, insightful, introverted right brain: What do you think of 100 people per square mile for the population density?」A response, a gut feeling, will come back. Keep lowering the candidate value until the gut feeling becomes,「No, that value feels way too low.」

Here is the dialogue between my left brain (LB) and right brain (RB).

LB: What do you think of 100 people per square mile?

RB: That feels okay based on my experience growing up in the United States.

LB: I can probably support that feeling quantitatively. A square mile with 100

people means each person occupies a square whose side is 1/10th of a mile or 160 meters. Expressed in this form, does the population density feel okay?

RB: Yes, the large open spaces in the western states probably compensate for the denser regions near the coasts.

LB: Now I will lower the estimate by factors of 3 or 10 until you object strongly that the estimate feels too low. [A factor of 3 is roughly one-half of a factor of 10, because 3 × 3 ≈ 10. A factor of 3 is the next-smallest factor by which to move when a factor of 10 is too large a jump.] In that vein, what about an average population density of 10 people per square mile?

RB: I feel uneasy. The estimate feels a bit low.

LB: I understand where you are coming from. That value may moderately overestimate the population density of farmland, but it probably greatly underestimates the population density in the cities. Because you are uneasy, let's move more slowly until you object strongly. How about 3 people per square mile?

RB: If the true value were lower than that, I'd feel fairly surprised.

LB: So, for the low end, I'll stop at 3 people per square mile. Now let's navigate to the upper end. You said that 100 people per square mile felt plausible. How do you feel about 300 people per square mile?

RB: I feel quite uneasy. That estimate feels quite high.

LB: I hear you. Your response reminds me that New Jersey and the Netherlands, both very densely populated, are at 1000 people per square mile, although I couldn't swear to this value. I cannot imagine packing the whole United States to a density comparable to New Jersey's. Therefore, let's stop here: Our upper endpoint is 300 people per square mile.

How do you make your best guess based on these two endpoints?

A plausible guess is to use their arithmetic mean, which is roughly 150 people per square mile. However, the right method is the geometric mean: 

```
best guess = √(lower endpoint × upper endpoint) (1.17)
```

The geometric mean is the midpoint of the lower and upper bounds — but on a ratio or logarithmic scale, which is the scale built into our mental hardware. (For more about how we perceive quantity, see The Number Sense [9].) The geometric mean is the correct mean when combining quantities produced by our mental hardware.

Here, the geometric mean is 30 people per square mile: a factor of 10 removed from either endpoint. Using that population density:

(1.18)

The actual population is roughly 3×108. The estimate based almost entirely on gut reasoning is within a factor of 1.5 of the actual population — a pleasantly surprising accuracy.

Problem 1.8 More gut estimates

By asking your gut to help you estimate the lower and upper endpoints, estimate (a) the height of a nearby tall tree that you can see, (b) the mass of a car, and (c) the number of water drops in a bathtub.

1.6 与直觉对话

正如你在前面的例子中看到的，分而治之法需要合理地估算树叶的值。为了确定什么是合理的，你就需要与你的直觉对话 一一 这是你在这节将要学到的。一开始对于利用直觉你会觉得奇怪，尤其是因为科学与工程被认为是理性的学科。

让我们来讨论如何进行这样的对话。例子是根据面积和人口密度来估算美国的人口。分而治之法的树图有两个树叶。（在章节 6.3.1，你会看到一个性质不同的方法，其中两个树叶是美国的州数和典型州的人口。）

面积是宽度乘高度，所以面积这个树叶又分裂成两个树叶。估算宽度和高度只需要和你的直觉有个简短对话即可，至少对生活在美国的人是这样。宽度为时速 500 英里的飞机 6 小时航程，即大约 3000 英里；如果粗略地估算，高度为宽度的三分之二，即 2000 英里。因此，面积约为 600 万英里<sup>2</sup>，用公制的话，这大约是 1600 万公里<sup>2</sup>。

估算人口密度需要与你的直觉对话。如果你和我一样，对人口密度几乎没有感觉。你的直觉可能知道，但你不能直接问你的直觉。直觉与右脑相关联，不过右脑不管语言。尽管右脑对这个世界知道很多，但无法对其用一个数值来表示，只能用感觉来表示。想要从右脑的知识库里得到什么，只能间接地问。

取一个特别的人口密度 一一 比如说 100 人/平方英里；然后询问直觉对此的观点:「哦，我那直觉敏锐的、洞察一切的、不爱说话的右脑，你如何看待 100 人/平方英里的人口密度？」直觉将会给你一个回应。继续减少可能值直到直觉告诉你，「不对，这个值感觉太低了。」

下面是我的左脑（LB）和右脑（RB) 之间的对话。

LB：你如何看待 100 人/平方英里的人口密度？

RB：感觉差不多（基于我在美国长大的经验）。

LB：知道这点很好。现在我将我的估算值降低一个 3 或 10 的因子直到你认为太低而强烈反对。（因子 3 差不多是因子 10 的一半，因为 3x3≈10。当因子 10 的跳跃过大时，因子 3 是次小的因子。) 按照这个说法 10 人/平方英里的人口密度会如何？

RB：我感觉很不对。这个估算太低了。

LB：我理解你是怎么来的。那个值对乡村的人ロ密度是有点估算过高，但对于城市人ロ密度就大大低估了。因为你感觉不对了, 我们就变动得慢一点，直到你强烈反对。那么 3 人/平方英里怎么样？

RB：我感觉非常不对。如果真实数据低于这个值，我会相当惊讶。

LB：谢谢。对于下限，我停留在 3 人/平方英里。现在我往上限走。你说 100 人/平方英里是很可能的。那么 300 人/平方英里怎么样？

RB：我感觉非常不对。这个估算似乎太高了。

LB：我知道你的意思了。你的回应提醒了我，新泽西和荷兰的人口密度都达到了非常密集的 1000 人/平方英里，尽管我无法保证这个值是对的。我无法想象整个美国的人口密度都达到新泽西那样的程度。因此，我将停留在这个值。我的上限是 300 人/平方英里。

➤ 你如何在上下限的基础上得到最佳猜测？

一个貌似合理的猜测是采用算术平均值，大约是 150 人/英里。但是，最好的方法是取几何平均：

```
最佳猜测=根号（下限值×上限值）
```

几何平均是下限和上限之间的中点 一一 但这是按比例尺度或对数尺度来说的，这是我们意识中固有的尺度。（想了解更多，见参考文献 [9]。）当我们整合一些由固有意识产生的数量时，几何方式是一种正确的方式。这样，几何平均是 30 人/平方英里：与上下限都相差一个 10 倍的因子。用这个人口密度计算，美国人口大约是 2 亿人。

实际人口大约是 3×10<sup>8</sup>。几乎完全根据直觉的估算结果与实际人口值只相差 1.5 倍。考虑到我们在面积和人口密度估算上的不确定性，这样的精度是相当令人惊奇的。

题 1.8 更多基于直觉的估算。

利用你的直觉给出上限和下限，从而估算：a）你所能看到的附近一棵很高的树的高度；b）汽车的重量；c）浴缸里的水共有多少滴。

可能的话，将你的估算结果与实际结果或更精确的结果比较。

### 1.7 Physical estimates

Your gut understands not only the social world but also the physical world.

If you trust its feelings, you can tap this vast reservoir of knowledge. For practice, we'll estimate the salinity of seawater (Section 1.7.1), human power output (Section 1.7.2), and the heat of vaporization of water (Section 1.7.3).

#### 1.7.1 Salinity of seawater

To estimate the salinity of seawater, which will later help you estimate the conductivity of seawater (Problem 8.10), do not ask your gut directly:「How do you feel about, say, 200 millimolar?」Although that kind of question worked for estimating population density (Section 1.6), here, unless you are a chemist, the answer will be:「I have no clue. What is a millimolar anyway? I have almost no experience of that unit.」Instead, offer your gut concrete data — for example, from a home experiment: adding salt to a cup of water until the mixture tastes as salty as the ocean.

This experiment can be a thought or a real experiment — another example of using multiple methods (Section 1.5). As a thought experiment, I ask my gut about various amounts of salt in a cup of water. When I propose adding 2 teaspoons, it responds,「Disgustingly salty!」At the lower end, when I propose adding 0.5 teaspoons, it responds,「Not very salty.」I'll use 0.5 and 2 teaspoons as the lower and upper endpoints of the range. Their midpoint, the estimate from the thought experiment, is 1 teaspoon per cup.

I tested this prediction at the kitchen sink. With 1 teaspoon (5 milliliters) of salt, the cup of water indeed had the sharp, metallic taste of seawater that I have gulped after being knocked over by large waves. A cup of water is roughly one-fourth of a liter or 250 cubic centimeters. By mass, the resulting salt concentration is the following product: 

The density of 2 grams per cubic centimeter comes from my gut feeling that salt is a light rock, so it should be somewhat denser than water at 1 gram per cubic centimeter, but not too much denser. (For an alternative method, more accurate but more elaborate, try Problem 1.10.) Then doing the arithmetic gives a 4 percent salt-to-water ratio (by mass).

The actual salinity of the Earth's oceans is about 3.5 percent — very close to the estimate of 4 percent. The estimate is close despite the large number of assumptions and approximations — the errors have mostly canceled. Its accuracy should give you courage to perform home experiments whenever you need data for divide-and-conquer estimates.

Problem 1.9 Density of water

Estimate the density of water by asking your gut to estimate the mass of water in a cup measure (roughly one-quarter of a liter).

Problem 1.10 Density of salt

Estimate the density of salt using the volume and mass of a typical salt container that you find in a grocery store. This value should be more accurate than my gut estimate in Section 1.7.1 (which was 2 grams per cubic centimeter).

#### 1.7.2 Human power output

Our second example of talking to your gut is an estimate of human power output — a power that is useful in many estimates (for example, Problem 1.17). Energies and powers are good candidates for divide-and-conquer estimates, because they are connected by the subdivision shown in the following equation and represented in the tree in the margin:

```
power = energy / time (1.20)
```

In particular, let's estimate the power that a trained athlete can generate for an extended time (not just during a few-seconds-long, high-power burst). As a proxy for that power, I'll use my own burst power output with two adjustment factors:

Maintaining a power is harder than producing a quick burst. Therefore, the first adjustment factor, my steady power divided by my burst power, is somewhat smaller than 1 — maybe 1/2 or 1/3. In contrast, an athlete's power output will be higher than mine, perhaps by a factor of 2 or 3: Even though I am sometimes known as the street-fighting mathematician [33], I am no athlete. Then the two adjustment factors roughly cancel, so my burst power should be comparable to an athlete's steady power.

To estimate my burst power, I performed a home experiment of running up a flight of stairs as quickly as possible. Determining the power output requires estimating an energy and a time:

(1.21)

The energy, which is the change in my gravitational potential energy, itself subdivides into three factors: 

In the academic building at my university, a building with high ceilings and staircases, I bounded up a staircase three stairs at a time. The staircase was about 12 feet or 3.5 meters high. Therefore, my mechanical energy output was roughly 2000 joules: 

```
𝐸 ∼ 65 kg × 10 m s−2 × 3.5 m ∼ 2000 J. (1.23)
```

(The units are fine: 1 J = 1 kg m2 s−2.)

The remaining leaf is the time: how long the climb took me. I made it in 6 seconds. In contrast, several students made it in 3.9 seconds — the power of youth! My mechanical power output was about 2000 joules per 6 seconds, or about 300 watts. (To check whether the estimate is reasonable, try Problem 1.12, where you estimate the typical human basal metabolism.) This burst power output should be close to the sustained power output of a trained athlete. And it is. As an example, in the Alpe d'Huez climb in the 1989 Tour de France, the winner — Greg LeMond, a world-class athlete — put out 394 watts (over a 42.5-minute period). The cyclist Lance Armstrong, during the time-trial stage during the Tour de France in 2004, generated even more: 495 watts (roughly 7 watts per kilogram). However, he publicly admitted to blood doping to enhance performance. Indeed, because of widespread doping, many cycling power outputs of the 1990s and 2000s are suspect; 400 watts stands as a legitimate world-class sustained power output.

Problem 1.11 Energy in a 9-volt battery

Estimate the energy in a 9-volt battery. Is it enough to launch the battery into orbit?

Problem 1.12 Basal metabolism

Based on our daily caloric consumption, estimate the human basal metabolism.

Problem 1.13 Energy measured in person flights of stairs How many flights of stairs can you climb using the energy in a stick (100 grams) of butter?

#### 1.7.3 Heat of vaporization of water

Our final physical estimate concerns the most important liquid on Earth.

What is the heat of vaporization of water?

Because water covers so much of the Earth and is such an important part of the atmosphere (clouds!), its heat of vaporization strongly affects our climate — whether through rainfall (Section 3.4.3) or air temperatures.

Heat of vaporization is defined as a ratio:

(1.24)

where the amount of substance can be measured in moles, by volume, or (most commonly) by mass. The definition provides the structure of the tree and of the estimate based on divide-and-conquer reasoning.

For the mass of the substance, choose an amount of water that is easy to imagine — ideally, an amount familiar from everyday life. Then your gut can help you make estimates. Because I often boil a few cups of water at a time, and each cup is few hundred milliliters, I'll imagine 1 liter or 1 kilogram of water.

The other leaf, the required energy, requires more thought. There is a common confusion about this energy that is worth discussing.

Is it the energy required to bring the water to a boil?

No: The energy has nothing to do with the energy required to bring the water to a boil! That energy is related to water's specific heat 𝑐p. The heat of vaporization depends on the energy needed to evaporate — boil away — the water, once it is boiling. (You compare these energies in Problem 5.61.) 

Energy subdivides into power times time (as when we estimated human power output in Section 1.7.2). Here, the power could be the power output of one burner; the time is the time to boil away the liter of water. To estimate these leaves, let's hold a gut conference.

For the time, my dialogue is as follows.

LB: How does 1 minute sound as a lower bound?

RB: Way too short — you've left boiling water on the stove unattended for longer without its boiling away!

LB: How about 3 minutes?

RB: That's on the low side. Maybe that's the lower bound.

LB: Okay. For the upper bound, how about 100 minutes?

RB: That time feels way too long. Haven't we boiled away pots of water in far less time?

LB: What about 30 minutes?

RB: That's long, but I wouldn't be shocked, only fairly surprised, if it took that long. It feels like the upper bound.

My range is therefore 3…30 minutes. Its midpoint — the geometric mean of the endpoints — is about 10 minutes or 600 seconds.

For variety, let's directly estimate the burner power, without estimating lower and upper bounds.

LB: How does 100 watts feel?

RB: Way too low: That's a lightbulb! If a lightbulb could boil away water so quickly, our energy troubles would be solved.

LB (feeling chastened): How about 1000 watts (1 kilowatt)?

RB: That's a bit low. A small appliance, such as a clothes iron, is already 1 kilowatt.

LB (raising the guess more slowly): What about 3 kilowatts?

RB: That burner power feels plausible.

Let's check this power estimate by subdividing power into two factors, voltage and current:

```
power = voltage × current (1.25)
```

An electric stove requires a line voltage of 220 volts, even in the United States where most other appliances require only 110 volts. A standard fuse is about 15 amperes, which gives us an idea of a large current. If a burner corresponds to a standard fuse, a burner supplies roughly 3 kilowatts: 

```
220 V × 15 A ≈ 3000 W (1.26)
```

This estimate agrees with the gut estimate, so both methods gain plausibility — which should give you confidence to use both methods for your own estimates. As a check, I looked at the circuit breaker connected to my range, and it is rated for 50 amperes. The range has four burners and an oven, so 15 amperes for one burner (at least, for the large burner) is plausible.

We now have values for all the leaf nodes. Propagating the values toward the root gives the heat of vaporization (𝐿vap) as roughly 2 megajoules per kilogram:

(1.27)

The true value is about 2.2×106 joules per kilogram. This value is one of the highest heats of vaporization of any liquid. As water evaporates, it carries away significant amounts of energy, making it an excellent coolant (Problem 1.17).

1.7 物理估算

你的直觉不仅能理解人文社会，也能理解物理世界。如果你相信直觉，你就能够发掘这个巨大的知识宝库。作为练习，我们来估算海水的含盐量（章节1.7.1），人力输出功率（章节1.7.2) 以及水的汽化热（章节1.7.3)。

1.7.1 海水的含盐量

为了估算海水的含盐量，这以后将帮助你来估算海水的导电率（题 8.10），不要直接问你的直觉：「你觉得，比如 200 毫摩尔/升怎么样？」尽管这种问法在估算人口密度时很有效（章节1.6），但在这儿，除非你是个化学家，不然你得到的回答将是：「我没有任何头绪。究竟什么是 1 毫摩尔/ 升？对这个单位我没有任何经验。」反之，给你的直觉一些具体数据 一一 比如，做个家庭实验，往一杯水中加盐，直到盐水混合物尝起来和海水一样咸。

这个实验可以是思想实验或实际的实验 一一 这是使用多种方法的另一个例子（章节1.5)。作为思想实验，我来问我的直觉有关往一杯水中加不同量盐的情况。当我加了两勺盐后，直觉的反应是，「成得令人厌恶！」考虑下限，当我加 0.5 勺盐时，直觉的反应是，「不是很咸。」我就用 0.5 和 2 勺作为下限和上限。其中间值，即从思想实验得到的估算是每杯水加 1 勺盐。

我在厨房检验了这个预测。1 勺盐（5毫升）加入的话，这杯水的确具有刺激的海水味道，这与我在海里被大浪打到后吞下的海水味道一样，一杯水大约是 1/4 升或 250 厘米。按质量算，含盐量的计算结果就是下列量的乘积。

2 克/立方厘米的密度来自我的直觉，因为盐是一种轻岩石，应该比水的密度，即 1 克厘米稍大，但也不会大太多。（另一种方法，更为精确也复杂得多，尝试题 1.10。）

完成算术运算给出的结果是大约盐-水质量比是 1:25（4%）。

地球上的海洋实际含盐量大约是 3.5% 一一 非常接近估算值。尽管用了大量的假设和近似，但估算结果是合理的 一一 误差大都互相抵消了。这个合理性应该会鼓励你去做一些家庭实验来获得在进行分而治之法估算时需要的数据。

题 1.9 水的密度。

用你的直觉通过估算一杯水（通常1/4升）的质量来估算水的密度。

题 1.10 盐的密度。

利用你在杂货店能找到的盐罐的体积和质量估算盐的密度。这个值应该比我在章节 1.7.1用直觉估算的值更精确（那里得到的是 2 克/厘米）。

1.7.2 人力功率

我们第二个与直觉对话的例子是人力功率的估算 一一 这是在很多估算中都有用的功率（如题1.17)。能量和功率是进行分而治之法估算的很好例子，因为这两个量可以通过下面的方程联系起来并用相应的树图表示：

```
功=能量/时间
```

特别地，让我们来估算一个训练有素的运动员在持续的一段时间内可以产生多大功率（不是那种在几秒钟内产生的、爆发的高功率）。作为替代，我将考虑我自己的爆发功率及两个因子：

维持一个功率比产生同样大小短时间的爆发功率更难。因此，第一个因子，我的稳定功率除以我的爆发功率，应该是一个小于 1 的数，也许是 1/2 或 1/3。反之，一个运动员的稳定功率要比我大得多，可能大个 2 或 3 倍的因子。这两个因子差不多互相抵消，所以我的爆发功率应该可以和一个运动员的稳定功率相比拟。

为了估算我的爆发功率，我做一个家庭实验：尽可能快地爬楼。估计功率需要对能量和时间进行估计：

```
功率=能量/时间
```

其中能量即为我的引力势能的变化，可以进一步分解为三个因子：

我所在大学的学术大楼是一个天花板很高有楼梯的建筑，我一次跳三个阶。楼梯总高 12 英尺，或说约 3.5 米。因此，我的能量输出大约是 2000 焦耳：

```
E~65kg×10m/s2×3.5m~2000
```

量纲检查：1 J=1 kgm2/s2

剩下的树叶是时间：爬楼需要多长时间？我花了 6 秒。作为对比，几个学生只花了 3.9 秒 一一 这是年轻的力量！我的机械输出功率大约是每 6 秒 2000 焦耳，或大约 300 瓦。（为了验证这个估算是否合理，尝试题 1.12，你可以估算典型的人的基础代谢。）

这个爆发功率应该接近于一个训练有素的运动员可维持的稳定功率。实际上也是如此。举例来说，1989 年环法自行车大赛的阿尔卑一都埃（Alpe d'huez）赛段冠军得主 一一 菜蒙德（Greg Lemond），一个世界级运动员 一一 的功率达到 394 瓦（持续42.5分钟），而自行车运动员阿姆斯特朗（Lance Armstrong）在 2004 年环法自行车赛的准备阶段，功率值更高 495 瓦。但是他公开承认采用了自血回输以增强体力（他因此被剥夺了奖牌）。的确，由于自血回输的广泛采用，在 20 世纪 90 年代和 21 世纪 00 年代期间的许多自行车运动员的功率值是值得怀疑的，400 瓦代表了合理的世界级运动员的可持续输出功率值。

题 1.11 9 伏电池的能量。

估算一个 9 伏电池的能量。这个能量是否足以将这个电池发射到绕地轨道？

题 1.12 基础代谢。

根据我们的日常热量消耗，估算人的基础代谢题。

1.13 爬楼的能量测量。

利用一块奶油中的能量，你能爬多少级楼梯？

我们最后一个物理估算有关地球上最重要的液体。

➤ 什么是水的汽化热？

因为水覆盖了地球表面如此多的部分，也因为水是大气中如此重要的一部分（云！），水的汽化热强烈地影响了我们的气候 一一 不论是通过降雨（章节3.4.3) 还是通过气温。汽化热定义为下列量的比：

```
蒸发这些物质所需的能量/物质的量
```

其中物质的量可以用摩尔、体积或者（最普通的）质量来衡量。这个定义给出了树图的结构和基于分而治之法的估算。关于物质的量，选择你容易想象的一定量的水 一一 理想的、日常生活中熟悉的量。然后你的直觉能够帮助你进行估算。因为我经常是一次烧几杯水，一杯水大概是几分之一升，我将考虑 1 升或 1 千克的水。另一个树叶，即所需的能量，需要更多的思考。这里有个通常会混淆的有关这个能量的概念是值得讨论的。

➤ 这是将水烧开所需要的能量吗？

错！这与将水烧开所需的能量无关。那个能量与水的比热 cp 有关。而汽化取决于一旦水烧开后，把水蒸干所需的能量。能量进一步分解为功率乘以时间（与我们在章节 1.7.2 讨论人力功率类似）。这里的功率可以是炉子的输出功率，时间是将 1 升水烧干的时间。

为了估算这些树叶，让我们来开一个直觉会议。关于时间，我的对话是这样的。

LB：1 分钟作为下限听起来觉得怎么样？

RB：太短了 一一 你这是把水烧开就扔炉子上不管了

LB：3 分钟怎么样？

RB：这可能是属于短的。也许这就是下限。

LB：好的。那么对于上限，100 分钟怎么样？

RB：太长了。谁会把茶放炉子上煮差不多 2 小时呢？

LB：30 分钟怎么样？

RB：有点长，不过我不会感到震惊，真是那么长时间的话只是有点惊讶。这感觉像是一个合理的上限。

我的范围因此是 3-30 分钟。中点两个端点的几何平均 一一 大约是 10 分钟或 600 秒。关于功率，我们来直接估算，不必考虑上限下限了。

LB：100 瓦感觉怎么样？

RB：太低了。这只是一个灯泡的功率！如果一个灯泡就能这么快烧开水，那我们的能源问题早就解决了。

LB：（感到需要修正了）1000 瓦怎么样？

RB：有点低。一个小电器，如电熨斗，就有 1 千瓦了。

LB：（猜测值上升慢一点）3 千瓦怎么样？

RB：这个炉子的功率感觉差不多。

我们来估算下这个功率，将其分解成电压和电流：

```
功率=电压×电流
```

电炉需要的电压是 220 伏，但在美国大部分电器是 110 伏的。标准的保险丝是 15 安培，这给我们一个大电流的概念，所以一个电炉的功率大约是 3 千瓦：

```
220V×15A ≈ 3000W
```

这个估算和直觉的估算一致，两种方法都给出了合理的结果。我们现在已经有了所有树叶节点的值。将这些值往上传递到树根，就可以得到汽化热（L汽化) 大约是 200 万焦耳/千克：

实际值大约是 2.2×10^6 焦耳/千克。这是所有液体中汽化热值最高的几种之一。当水蒸发时，会带走显著的能量，这使得水成为极佳的制冷剂。（题1.17)。

## 0201. Abstraction

2.1 Energy from burning hydrocarbons

2.2 Coin-flip game

2.3 Purpose of abstraction

2.4 Analogies

2.5 Summary and further problems

Divide-and-conquer reasoning, the tool introduced in Chapter 1, is powerful, but it is not enough by itself to organize the complexity of the world.

Try, for example, to manage the millions of files on a computer — even my laptop says that it has almost 3 million files. Without any organization, with all the files in one monster directory or folder, you could never find information that you need. However, simply using divide and conquer by dividing the files into groups — the first 100 files by date, the second 100 files by date, and so on — does not disperse the chaos. A better solution is to organize the millions of files into a hierarchy: as a tree of folders and subfolders. The elements in this hierarchy get names — for example,「photos of the children」or「files for typesetting this book」 — and these names guide us to the needed information.

Naming — or, more technically, abstraction — is our other tool for organizing complexity. A name or an abstraction gets its power from its reusability.

Without reusable ideas, the world would become unmanageably complicated. We might ask,「Could you, without tipping it over, move the wooden board glued to four thick sticks toward the large white plastic circle?」instead of,「Could you slide the chair toward the table?」The abstractions

「chair,」「slide,」and「table」compactly represent complex ideas and physical structures. (And even the complex question itself uses abstractions.) 

Similarly, without good abstractions we could hardly calculate, and modern science and technology would be impossible. As an illustration, imagine the pain of the following calculation:

XXVII × XXXVI, (2.1)

which is 27×36 in Roman numerals. The problem is not that the notation is unfamiliar, but rather that it is not based on abstractions useful for calculation. Not least, it does not lend itself to divide-and-conquer reasoning; for example, even though V (5) is a part of XXVII, V×XXXVI has no obvious answer. In contrast, our modern number system, based on the abstractions of place value and zero, makes the whole multiplication simple. Notations are abstractions, and good abstractions amplify our intelligence. In this chapter, we will practice making abstractions, discuss their high-level purpose, and continue to practice.

第 1 章介绍的分而治之法是很有力的，但仅靠这个方法还不足以组织我们这个世界的复杂性。比如，试试整理计算机的数百万个文件 一一 即使是我的手提电脑，据说至少也有 300 万个文件。如果不做任何整理把所有文件放在一个魔鬼目录或文件夹里，你可能永远都无法找到你想要的信息。然而，简单应用分而治之法，即将文件分组（按照日期将前 100 个文件分为一组，然后是其后 100 个文件等等）并不能解决混乱。一个较好的方法是将这几百万个文件分层次管理：像一棵目录和子目录的树样。在这个分层结构里，每部分都有名字，比如说，「孩子照片」或者「本书的文稿」，这些名字给了我们所需要的信息。

名称 一一 或者更技术点说，抽象，是我们整理复杂性的第二个也是最后一个工具。名称或抽象的威力来自可重复性。如果没有可重复性，这个世界将复杂得无从把握。没有抽象，我们就无法生活。我们可能会这么问，「能否请你把那个黏着四条粗木棍的木板移到大的、白的、塑料圆盘这边来，不要弄翻了？」而不是说，「能否请你把椅子移到桌子这边来？」这些名称「椅子」、「移动」和「桌子」简明扼要地表示了这些复杂的概念和物理结构。

类似地，没有好的抽象，我们几乎无法计算，现代科学和技术也是不可能的。作为一个例子，想象一下进行下列计算的痛苦：

```
XXⅦ×XXXⅥ
```

这是用罗马数字表示的 27×36。问题不仅仅在于记号是不熟悉的，还在于这不是一种可用于计算的抽象。不仅如此，这种方式也不利于使用分而治之法；比如说，尽管 V (5) 是 XXⅦ (27) 的一部分，但 VxXXXⅥ 却没有显然的答案。与此相反，现代计数系统基于数位和零的抽象，使得乘法运算变得简单。

记号是一种抽象，好的抽象可以增强我们的智能。这也是为什么我们每一个思维工具都是一种抽象或者说可重复的概念。比如在第 1 章，我们学会了如何将一个难题分解成一些可以处理的小问题，我们将这个过程称为分而治之法。不要就止步于这一个过程每当你重复使用一个概念时，确定一个可移植的过程，并给它一个名称时，即在进行抽象。有了一个名称，你就能更快地看清和使用相应的方法。在本章，我们将练习抽象，讨论抽象的高级目标，然后进一步实践。

### 2.5 Summary and further problems

Geometric means, impedances, low-pass filters — these ideas are all abstractions. An abstraction connects seemingly random details into a higher-level structure that allows us to transfer knowledge and insights. By building abstractions, we amplify our intelligence.

Indeed, each of our reasoning tools is an abstraction or reusable idea. In Chapter 1, for example, we learned how to split hard problems into tractable ones, and we named this process divide-and-conquer reasoning. Don't stop with this one process. Whenever you reuse an idea, identify the transferable process, and name it: Make an abstraction. With a name, you will recognize and reuse it.

Problem 2.21 From circles to spheres

In this problem, you first find the area of a circle from its circumference and then use analogous reasoning to find the volume of a sphere.

a. Divide a circle of radius 𝑟 into pie wedges. Then snip and unroll the circle: 

(2.66)

Use the unrolled picture and the knowledge that the circle's circumference is 2𝜋𝑟 to show that its area is 𝜋𝑟2.

b. Now extend the argument to a sphere of radius 𝑟: Find its volume given that its surface area is 4𝜋𝑟2. (This method was invented by the ancient Greeks.) 2014-09-02 10:51:35 UTC / rev 78ca0ee9dfae

Problem 2.22 Gain of an LRC circuit

Use the impedance of an inductor (Problem 2.19) to find the gain of the classic 𝐿𝑅𝐶 circuit. In this configuration, in which the output voltage measured across the resistor, is the circuit a low-pass filter, a high-pass filter, or a band-pass filter?

Problem 2.23 Continued fraction

Evaluate the continued fraction

(2.67)

Compare this problem with Problem 2.8.

Problem 2.24 Exponent tower

Evaluate:

(2.68)

Here, 𝑎𝑏𝑐 means 𝑎(𝑏𝑐).

Problem 2.25 Coaxial cable termination

In physics and electronics laboratories around the world, the favorite way to connect equipment and transmit signals is with coaxial cable. The standard coaxial cable, RG-58/U, has a capacitance per length of 100 picofarads per meter and an inductance per length of 0.29 microhenries per meter. It can be modeled as a long inductor–capacitor ladder:

What resistance 𝑅 placed at the end (in parallel with the last capacitor) makes the cable look like an infinitely long 𝐿𝐶 cable?

Problem 2.26 UNIX and Linux

Using Mike Gancarz's The UNIX Philosophy [17] and Linux and the Unix Philosophy [18], find examples of abstraction in the design and philosophy of the UNIX and Linux operating systems.

2.5 小结及进一步的问题

几何平均，阻抗，低通滤波器 一一 这些概念都是抽象的。抽象可以把表面上看起来杂乱无章的细节变成一个有机的高级结构，通过这个结构，可以让我们得到超出其来源的知识和洞察力。通过构建抽象，我们放大了我们的智慧。

题 2.21 从圆到球。在这个问题中，首先从圆的周长得到面积，然后用类似的分析得到球的体积。a）将半径为 r 的圆分解成楔形的饼图。然后将其拆开。利用拆开的图形和已知的圆周长为 2πr 来证明圆面积为 πr<sup>2</sup>。b）将讨论推广到半径为 r 的球：由已知的球表面积为 4πr^2 推出球的体积。（这个方法是古希腊人发明的。）

题 2.22 LRC 电路的增益。利用在题 2.19 中得到的电感的感抗来求典型 LRC 电路的增益。在这个结构中，输出电压是在电阻两段测量的，这是一个低通滤波器，高通滤波器还是个波段滤波器？

题 2.23 连分数。计算连分数：将此题与题 2.8 比较。

题 2.24 指数塔。

题 2.25 同轴电缆。世界各地的物理和电子实验室里，连接设备和信号传输的最好方式是使用同轴电缆。标准的同轴电缆，RG-58/U，其单位长度的电容为100 皮法/米，单位长度电感为 0.29 微亨/米。可以看成是一个很长的电感-电容网络：

将多大的电阻 R 放在末端（与最后的电容并联）能使电缆看起来像无限长的 LC 电缆？

题 2.26 UNIX 和 LINUX。迈克·甘卡兹（Mike Gancarz）的《UNIX 哲学》（The UNIX Philosophy），或《Linux 和 UNIX 哲学》（Linux and the Unix Philosophy），在这些（密切相关的）操作系统的设计和哲学中找出抽象的例子。

### 2.1 Energy from burning hydrocarbons

Our understanding of the world is built on layers of abstractions. Consider the idea of a fluid. At the bottom of the abstraction hierarchy are the actors of particle physics: quarks and electrons. Quarks combine to build protons and neutrons. Protons, neutrons, and electrons combine to build atoms. Atoms combine to build molecules. And large collections of molecules act, under many conditions, like a fluid.

The idea of a fluid is a new unit of thought. It helps us understand diverse phenomena, without our having to calculate or even know how quarks and electrons interact to produce fluid behavior. As one consequence, we can describe the behavior of air and water using the same equations (the quarks Navier–Stokes equations of fluid mechanics); we need only to use different values for the density and viscosity. Then atmospheric cyclones and water vortices, although they result from widely differing sets of quarks and electrons and their interactions, can be understood as the same phenomenon.

A similarly powerful abstraction is a chemical bond. We'll use this abstraction to estimate a quantity essential to our bodies and to modern society: the energy released by burning chains made of hydrogen and carbon atoms (hydrocarbons). A hydrocarbon can be abstracted as a chain of CH2 units: 

Burning a CH2 unit requires oxygen (O2) and releases carbon dioxide (CO2), water, and energy:

CH2 + 32O2 ⟶ CO2 + H2O + energy. (2.2)

For a hydrocarbon with eight carbons — such as octane, a prime component of motor fuel — simply multiply this reaction by 8: 

(CH2)8 + 12 O2 ⟶ 8 CO2 + 8 H2O + lots of energy. (2.3)

(The two additional hydrogens at the left and right ends of octane are not worth worrying about.)

How much energy is released by burning one CH2 unit?

To make this estimate, use the table of bond bond energies. It gives the energy required to break (not make) a chemical bond — for example, between carbon and hydrogen. However, there is no unique carbon–hydrogen (C–H) bond. 

The carbon–hydrogen bonds in methane are different from the carbon–hydrogen bonds in ethane. To make a reusable idea, we neglect those differences — placing them below our abstraction barrier — and make an abstraction called the carbon–hydrogen bond. So the table, already in its first column, is built on an abstraction.

The second gives the bond energy in kilocalories per mole of bonds. A kilocalorie is roughly 4000 joules, and a mole is Avogadro's number (6×1023) of bonds. The third column gives the energy in the SI units used by most of the world, kilojoules per mole. The final column gives the energy in electron volts (eV) per bond. An electron volt is 1.6×10−19 joules.

An electron volt is suited for measuring atomic energies, because most bond energies have an easy-to-grasp value of a few electron volts. I wish most of the world used this unit!

Let's tabulate the energies in the combustion of one hydrocarbon unit.

The left side of the reaction has two carbon–hydrogen bonds, 1.5 oxygen–oxygen double bonds, and one carbon–carbon bond (connecting the carbon atom in the CH2 unit to the carbon atom in a neighboring unit). The total, 460 kilocalories or 1925 kilojoules per mole, is the energy required to break the bonds. It is an energy input, so it reduces the net combustion energy.

The right side has two carbon–oxygen double bonds bond energy and two oxygen–hydrogen bonds. The total for the right side, 606 kilocalories or 2535 kilojoules per mole, is the energy released in forming these bonds. It is the energy produced, so it increases the net combustion energy.

The net result is, per mole of CH2, an energy release of 606 minus 460 kilocalories, or approximately 145 kilocalories (610 kilojoules). Equivalently, it is also about 6 electron volts per CH2 unit — about 1.5 chemical bonds' worth of energy. The combustion energy is also useful as an energy per mass rather than per mole. A mole of CH2 units weighs 14 grams. Therefore, 145 kilocalories per mole is roughly 10 kilocalories or 40 kilojoules per gram. This energy density is worth memorizing because it gives the energy released by burning oil and gasoline or by metabolizing fat (even though fat is not a pure hydrocarbon).

The preceding table, adapted from Oxford University's「Virtual Chemistry」site, gives actual combustion energies for plant and animal fuel sources (with pure hydrogen included for fun). The penultimate entry, stearic acid, is a large component of animal fat; animals store energy in a substance with an energy density comparable to the energy density in gasoline — roughly 10 kilocalories or 40 kilojoules per gram. Plants, on the other hand, store energy in starch, which is a chain of glucose units; glucose has an energy density of only roughly 4 kilocalories per gram. This value, the energy density of food carbohydrates (sugars and starches), is also worth memorizing.

It is significantly lower than the energy density of fats: Eating fat fills us up much faster than eating starch does.

How can we explain the different plant and animal energy-storage densities?

Plants do not need to move, so the extra weight required by using lower-density energy storage is not so important. The benefit of the simpler glucose metabolic pathway outweighs the drawback of the extra weight. For animals, however, the large benefit of lower weight outweighs the metabolic complexity of burning fats.

Problem 2.1 Estimating the energy density of common foods

In American schools, the traditional lunch is the peanut-butter-and-jelly sandwich.

Estimate the energy density in peanut butter and in jelly (or jam).

Problem 2.2 Peanut butter as fuel

If you could convert all the combustion energy in one tablespoon (15 grams) of peanut butter into mechanical work, how many flights of stairs could you climb?

Problem 2.3 Growth of grass

How fast does grass grow? Is the rate limited by rainfall or by sunlight?

2.1 燃烧碳氢化合物释放的能量

我们对世界的理解是建立在分层次的抽象基础上的。考虑流体的概念。在抽象的最底层是粒子物理的主角：夸克和电子。夸克的组合构成质子和中子。质子、中子和电子的组合构成原子。原子的组合构成分子，大量分子的集合，在定条件下的行为就是流体。流体的概念是一个新的思想，这个思想可以帮助我们在计算之前，甚至在知道夸克和电子是如何通过相互作用产生流体效应之前，就能理解各种现象。

一个类似的有力的抽象是化学键。我们将利用这个抽象来估算对人体和现代社会来说很关键的一个量：燃烧氢和碳原子（碳氢化合物）释放的能量。碳氢化合物可以抽象为不断重复的 CH2 单元的链：

燃烧一个 CH2 单元需要氧（O2) 并释放二氧化碳（CO2），水和能量：

```
CH2+3/2O2 → CO2+H20+能量
```

对于 8 个碳原子的碳氢化合物 一一 比如辛烷，这是发动机燃料的主要成分 一一 只要将上述反应乘以 8：

```
(CH2)8 +12O2→8CO2+8H12O+很多能量
```

燃烧一个 CH2 单元能释放出多少能量？为了进行这个估算，利用结合能表。这个能量是打破（不是形成）一个化学键需要的能量。这个表的第一列已经用到了抽象。例如，不存在唯一的碳氢（CH）结合能：甲烷的碳氢键和乙烷的碳氢键是不同的。但为了这个概念的可重复性，我们忽略了这个差别 一一 我们将其置于抽象的门槛之下 一一 将其抽象为碳氢键。

「千卡/摩尔」这一列给出了用千卡表示的每摩尔碳氢键的结合能。1 千卡大约是 4000 焦耳，1 摩尔的键数为阿伏伽德罗常数（≈6×10^23) 。 「电子伏/化学键」这一列给出用电子伏表示的每个键的结合能。1 电子伏为 1.6×10^(-19) 焦耳。这个单位适合衡量原子的能量，因为大部分的结合能都在易于处理的几个电子伏范围内。

我们用下图来表示燃烧一个碳氢单元的能量。

反应的左边是一个碳-碳键，两个碳-氢键，1.5 个氧-氧双键。（碳-碳键是将 CH2 单元中的碳与相邻单元中碳東缚在一起的键）。共计  460 千卡/摩尔，就是打破这些键所需的能量。这是输入的能量，它减少了净燃烧能量。

右边是两个碳-氧双键和两个氢-氧键。总共 606 千卡/摩尔的能量，是形成这些键释放的能量。这是输出的能量，它增加了净燃烧能量：

释放的净能量为（606-460) 千卡，即大约每摩尔 CH2 释放 150 千卡。或说，大约每个 CH2 单元释放 6 个电子伏 一一 大约是 1.5 个化学键的能量。用单位质量的能量而不是用单位摩尔来表示燃烧所释放的能量也是很有用的。1 摩尔 CH2 单元重 14 克。因此，150 千卡/摩尔大约是 10 千卡/克或 40 千焦耳/克。这个能量密度值得记住，因为这给出了燃烧油脂和汽油或吃下脂肪后释放的能量（尽管脂肪不是纯的碳氢化合物）。

2『燃烧一个 CH2 释放能量的数据，做一张信息数据卡片。（2022-05-13）』—— 已完成

下表给出了植物和动物燃料的燃烧能（将纯碳氢化合物包括在内是为引起兴趣）。饱和脂肪酸是动物脂肪的主要成分；动物的能量储存在可以和汽油的能量密度相比拟的物质中 一一 大约是 10 千卡/克。另一方面，植物将能量储存在淀粉中，这是葡萄糖单元构成的链；葡萄糖的能量密度只有大约 4 千卡/克。食物中碳水化合物（糖和淀粉）的能量密度值也值得记住。这明显低于脂肪的能量密度：对提供我们能量来说，食用脂肪比食用淀粉要快得多。

➤ 我们可以如何解释植物和动物不同的能量储存密度？

植物不需要移动，所以低密度能量储存造成的额外重量就不是很重要了。葡萄单糖代谢方式带来的好处要胜过额外重量产生的微小弱点。然而对于动物来说，较小体重带来的优点超过了燃烧脂肪的复杂代谢方式带来的弱点。

题 2.1 估算普通食物的能量密度。在美国学校里，传统的午餐是花生酱、奶油、果酱三明治。估算花生、奶油和果酱（或果冻）的能量密度。

题 2.2 花生奶油作为燃料。假设你的身体可以将一勺（约 15 克）花生奶油的燃烧能全部转化为机械能，你可以爬多少级楼梯？

题 2.3 草的生长速度。草的生长速度有多快？这个速率是受水的限制（典型的降水量）还是阳光的限制（典型的太阳光通量）?

### 2.2 Coin-flip game

The abstractions of atoms, bonds, and bond energies have been made for us by the development of science. But we often have to make new abstractions.

To develop this skill, we'll analyze a coin game where two players take turns flipping a (fair) coin; whoever first tosses heads wins.

What is the probability that the first player wins?

First get a feel for the game by playing it. Here is one round: TH. The first player missed the chance to win by tossing tails (T); but the second player tossed heads (H) and won.

Playing many games might reveal a pattern to us or suggest how to compute the probability. However, playing many games by flipping a real coin becomes tedious. Instead, a computer can simulate the games, substituting pseudorandom numbers for a real coin. Here are several runs produced by a computer program. Each line begins with 1 or 2 to indicate which player won the game; the rest of the line shows the coin tosses. In these ten iterations, each player won five times. A reasonable conjecture is that each player has an equal chance to win. However, this conjecture, based on only ten games, cannot be believed too strongly.

Let's try 100 games. Now even counting the wins becomes tedious. My computer counted for me: 68 wins for player 1, and 32 wins for player 2.

The probability of player 1's winning now seems closer to 2/3 than to 1/2.

To find the exact value, let's diagram the game as a tree reflecting the alternative endings of the game. Each layer represents one flip. The game ends at a leaf, when one player has tossed heads. The shaded leaves show the first player's wins — for example, after H, TTH, or TTTTH. The probabilities of these winning ways are 1/2 (for H), 1/8 (for TTH), and 1/32 (for TTTTH). The sum of all these winning probabilities is the probability of the first player's winning: 

(2.5)

To sum this infinite series without resorting to formulas, make an abstraction: Notice that the tree contains, one level down, a near copy of itself. (In this problem, the abstraction gets reused within the same problem. In computer science, such a structure is called recursive.) For if the first player tosses tails, the second player starts the game in the position of the first player, with the same probability of winning.

To benefit from this equivalence, let's name the reusable idea, namely the probability of the first player's winning, and call it 𝑝. The second player wins the game with probability 𝑝/2: The factor of 1/2 is the probability that the first player tosses tails; the factor of 𝑝 is the probability that the second player wins, given that the first player blew his chance by tossing tails on the first toss.

Because either the first or the second player wins, the two winning probabilities add to 1:

(2.6)

The solution is 𝑝 = 2/3, as suggested by the 100-game simulation. The benefit of the abstraction solution, compared to calculating the infinite probability sum explicitly, is insight. In the abstraction solution, the answer has to be what it is. It leaves almost nothing to remember. An amusing illustration of the same benefit comes from the problem of the fly that zooms back and forth between two approaching trains.

If the fly starts when the trains are 60 miles apart, each train travels at 20 miles per hour, and the fly travels at 30 miles per hour, how far does the fly travel, in total, before meeting its maker when the trains collide? (Apologies that physics problems are often so violent.)

Right after hearing the problem, John von Neumann, inventor of game theory and the modern computer, gave the correct distance.「That was quick,」

said a colleague.「Everyone else tries to sum the infinite series.」「What's wrong with that?」said von Neumann.「That's how I did it.」In Problem 2.7, you get to work out the infinite-series and the insightful solutions.

Problem 2.4 Summing a geometric series using abstraction 

Use abstraction to find the sum of the infinite geometric series 

1 + 𝑟 + 𝑟2 + 𝑟3 + ⋯. (2.7)

Problem 2.5 Using the geometric-series sum

Use Problem 2.4 to check that the probability of the first player's winning is 2/3: 

𝑝 = 1/2 + 1/8 + 1/32 + ⋯ = 2/3. (2.8)

Problem 2.6 Nested square roots

Evaluate these infinite mixes of arithmetic and square roots: 

(2.9)

(2.10)

Problem 2.7 Two trains and a fly

Find the insightful and the infinite-series solution to the problem of the fly and the approaching trains (Section 2.2). Check that they give the same answer for the distance that the fly travels!

Problem 2.8 Resistive ladder

In the following infinite ladder of 1-ohm resistors, what is the resistance between points A and B? This measurement is indicated by the ohmmeter connected between these points.

2.2 扔硬币游戏

科学的发展给了我们原子、化学键和结合能等抽象概念。但是，我们常常会面对一些问题，需要进行新的抽象。我们将通过分析扔硬币游戏来发展这个技巧。在这个游戏中，两个游戏者轮流扔一个硬币，先扔出正面者获胜。

➤ 第一个游戏者获胜的概率有多大？

首先通过做游戏来获得一些感觉。第一轮游戏的结果是：

```
TH
```

第一个游戏者扔出的是反面（T），因此没能获胜，第二个游戏者扔出的是正面（H），因而获胜。

游戏重复很多次后会给我们揭示一些图像或给我们一些如何计算概率的建议。然而，将一枚真实的硬币反复扔很多次会乏味至极。电脑可以模拟这个游戏，用伪随机数来代替硬币。下面是电脑程序产生的几轮游戏结果。每一行开头都用 1 或 2 表示是哪个游戏者贏。数字后面是扔硬币的结果：

在这 10 轮游戏中，每个游戏者都贏了 5 次。一个合理的假设是每个游戏者都有相同赢得游戏的机会。但是，这个假设只是基于 10 次游戏，不可能有太高的可信度。让我们尝试 100 次。现在甚至只是数贏的次数就让人很乏味了。我让电脑来计数：结果第一个游戏者赢了 68 次，第二个游戏者赢了 32 次。第一个游戏者贏的概率接近 2/3，而不是 1/2。

为了得到准确的值，我们用树图来表示游戏交替出现的结果。每一层表示扔一次硬币。当有一个游戏者扔出正面，游戏就在一个树叶结束。有阴影的树叶表示第一个游戏者赢 一一 比如是 H，TTH，或 TTTTH。这些获胜的概率是 1/2(H)，1/8(TTH）及 1/32(TTTTE)。

所有这些获胜概率的和就是第一个游戏者获胜的概率：

```
1/2+1/8+1/32+……
```

为了不用公式求出这个无穷级数的和，我们来进行一个抽象：注意到在每层向下时，树图都包含一个自身的拷贝。（在这个问题中，抽象在同样的问题中不断被使用。在计算机科学中，这种结构称为循环。）因为如果第一个游戏者扔出的是反面，则第二个游戏者是以获胜概率为 p 的第一个游戏者的位置开始游戏。

为了从这个比较中得到好处，让我们给这个可重复的概念一个名称，即第一个游戏者获胜的概率，记为 p。则第二个游戏者的获胜概率为 p/2：因子 1/2 是第一个游戏者扔出反面的概率，因子 p 是第二个游戏者获胜的概率（第一个游戏者在第一次扔出的是反面而失去机会的情况下。）

因为不是第一个游戏者获胜，就是第二个游戏者获胜，两个概率之和等于 1:

其解为 p=2/3，正是 100 次游戏模拟的结果。抽象解与直接求无穷多个概率和相比的好处在于洞察。在抽象解中，答案必须反映问题的本质。几乎不会有任何多余的东西。

1『悟性不够，还是没看懂前面的拆解逻辑。（2022-05-13）』

一个有趣的、可以说明同样问题的例子来自在两列相向而行的列车之间飞舞的苍蝇问题。如果开始时列车相隔 60 英里，列车的速度都是 20 英里/小时，苍蝇的速度是 30 英里/小时，苍蝇在两列火车相撞而惨死之前总共飞行多少距离？（抱歉物理问题经常是如此暴力。）

听说这个问题，冯·诺依曼，博弈论和现代计算机的开创者，立刻就给出了正确的距离。一个同事说，「太快了」。「所有人都在试图求出无穷级数的和。」「那么做有什么问题？」冯·诺依曼说道，「我就是这么做的。」

在题 2.7，你可以求出无穷级数，或通过洞察力求解。

题 2.4 利用抽象方法求出几何级数的和。利用抽象方法求出无穷几何级数的和：

```
1+r+r^2+r^3+……
```

题 2.5 利用几何级数的和。利用题 2.4 验证第一个游戏者获胜的概率为 2/3，与我们用抽象方法得到的一致。

```
p=1/2+1/8+1/32+……
```

题 2.6 嵌套的平方根。求出下列算术和平方根的无穷混合的值：

题 2.7 两列火车与一只苍蝇。对于苍蝇和逼近的列车问题（章节 2.2），直接求无穷级数，或通过洞察力求解。验证两种方法的结果一致！

1-3『这里例子之前在其他书籍里看到过，所以会解。以时间为线索，苍蝇飞了 45 公里。（2022-05-13）』

题 2.8 电阻网络。在下列 1 欧姆电阻的网络中，A，B 两点之间的电阻是多少？这个测量是通过连接两点的欧姆表得到的。

### 2.3 Purpose of abstraction

The coin game (Section 2.2), like the geometric series (Problem 2.4) or the resistive ladder (Problem 2.8), contained a copy of itself. Noticing this reuse greatly simplified the analysis. Abstraction has a second benefit: giving us a high-level view of a problem or situation. Abstractions then show us structural similarities between seemingly disparate situations.

As an example, let's revisit the geometric mean, introduced in Section 1.6 to make gut estimates. The geometric mean of two nonnegative quantities 𝑎 and 𝑏 is defined as:

geometric mean ≡ √𝑎𝑏 . (2.11)

This mean is called the geometric mean because it has a pleasing geometric construction. Divide the diameter of a circle into two lengths, 𝑎 and 𝑏, and inscribe a right triangle whose hypotenuse is the diameter. The triangle's altitude is the geometric mean of 𝑎 and 𝑏.

This mean reappears in surprising places, including the beach. When you stand at the shore and look at the horizon, you are seeing a geometric mean. The distance to the horizon is the geometric mean of two important lengths in the problem (Problem 2.9).

For me, its most surprising appearance was in the「Programming and Problem-Solving Seminar」course taught by Donald Knuth [40] (who also created TEX, the typesetting system for this book). The course, taught as a series of two-week problems, helped first-year PhD students transition from undergraduate homework problems to PhD research problems. A homework problem requires perhaps 1 hour. A research problem requires, say, 1000 hours: roughly a year of work, allowing for other projects. (A few problems stapled together become a PhD.) In the course, each 2-week module required about 30 hours — approximately the geometric mean of the two endpoints. The modules were just the right length to help us cross the bridge from homework to research.

Problem 2.9 Horizon distance

How far is the horizon when you are standing at the shore? Hint: It's farther for an adult than for a child.

Problem 2.10 Distance to a ship

Standing at the shore, you see a ship (drawn to scale) with a 10-meter mast sail into the distance and disappear from view. How far away was it when it disappeared?

As further evidence that the geometric mean is a useful abstraction, the idea appears even when there is no geometric construction to produce it, such as in making gut estimates. We used this method in Section 1.6 to estimate the population density and then the population of the United States. Let's practice by estimating the oil imports of the United States in barrels per year — without the divide-and-conquer reasoning of Section 1.4.

The method requires that the gut supply a lower and an upper bound. My gut reports back that it would feel fairly surprised if the imports were less than 10 million barrels per year. On the upper end, my gut would be fairly surprised if the imports were higher than 1 trillion barrels per year — a barrel is a lot of oil, and a trillion is a large number!

You might wonder how your gut too can come up with such large numbers and how you can have any confidence in them. Admittedly, I have practiced a lot. But you can practice too. The key is the practice effectively. First, have the courage to guess even when you feel anxious about it (I feel this anxiety still, so I practice this courage often). Second, compare your guess to values in which you can place more confidence — for example, to your own more careful estimates or to official values. The comparison helps calibrate your gut (your right brain) to these large magnitudes. You will find a growing and justified confidence in your judgment of magnitude.

My best guess for the amount is the geometric mean of the lower and upper estimates:

(2.12)

The result is roughly 3 billion barrels per year — close to the our estimate using divide and conquer and close to the true value. In contrast, the arithmetic mean would have produced an estimate of 500 billion barrels per year, which is far too high.

Problem 2.11 Arithmetic-mean–geometric-mean inequality 

Use the geometric construction for the geometric mean to show that the arithmetic mean of 𝑎 and 𝑏 (assumed to be nonnegative) is always greater than or equal to their geometric mean. When are the means equal?

Problem 2.12 Weighted geometric mean

A generalization of the arithmetic mean of 𝑎 and 𝑏 as (𝑎 + 𝑏)/2 is to give 𝑎 and 𝑏 unequal weights. What is the analogous generalization for a geometric mean?

(The weighted geometric mean shows up in Problem 6.29 when you estimate the contact time of a ball bouncing from a table.) 

2.3 抽象的目的

像几何级数（题 2.4）或电阻网络（题 2.8）一样，扔硬币游戏（章节 2.2）包含了自身的复制。注意到这种重复会极大地简化分析。抽象还有第二个好处：能使我们站在更高的位置来看待一个问题或情形。抽象让我们看到表面上毫无关系的事物之间的相似结构。举例来说，让我们来重新审视一下在章节 1.6 中进行直觉估算时介绍的几何平均。两个非负数 a 和 b 的几何平均定义为：

```
几何平均=√(a·b)
```

之所以称为几何平均是因为其具有这样一种赏心悦目的几何结构。将个圆的直径分为两段，a 和 b，然后作一个直角三角形，其斜边为圆的直径。则三角形的高为两个长度 a 和 b 的几何平均。几何平均会在令人惊讶的地方不断出现，包括海边。当你站在海边眺望远处时，你看到的就是几何平均。题 2.9 中，到地平线的距离就是两个重要长度的几何平均。

1『几何平均值的几何图示，详见原书，脑子里要能直接浮现，值得时刻把玩。（2022-05-14）』

对我来说，最令人惊奇的是其出现在高德纳（Donald Knuth)（排版系统 TeX 的作者）教的课程「编程与问题解决研讨班」上。这个课程通过一系列的「两周问题」的讲授，来帮助一年级博士生从本科生的作业问题过渡到博土生的研究问题。一个回家作业也许需要 1 小时。一个研究课题需要，比如说 1000 小时：大约是一年的工作，同时可以做一些其他的课题。（几个课题合并起来变成一个博士。）在这个课程中，每一个两周模块需要大约 30 小时 一一 近似是这两个极端情况的几何平均。这些模块正是帮助我们从作业跨越到研究的桥梁的正确长度。

题 2.9 到地平线的距离。当你站在海边时，离地平线有多远？提示：成人看到的距离要比儿童看到的更远。

题 2.10 到一艘船的距离。站在海边，你正好能看到船上的 10 米桅杆。这艘船有多远？

更多的证据表明几何平均是一个有用的抽象，甚至当并没有一个几何构造来产生这个平均时仍会出现这个概念，比如在进行直觉估算的时候。我们曾经在章节 1.6 用这个方法估算过人口密度及美国人口。

让我们再来练习下估算美国进口的石油 一一 每年多少桶 一一 不使用章节 1.4 中的分而治之法。这个方法要求直觉给出一个下限和一个上限。我的直觉告诉我，如果进口石油少于每年一千万桶会令人相当惊奇。至于上限，如果进口量大于每年一万亿桶则会让我直觉感到震惊 一一 一桶油已经很多了，一万亿是一个巨大的数。

我对这个量的最佳猜测是上限和下限的几何平均：

结果是大约每年 30 亿桶 一一 与我们用分而治之法的估算很接近，并接近实际值。反之，算术平均将给出每年 5000 亿桶的估算，这就太大了。

题 2.11 算术平均 一一 几何平均不等式。利用几何平均的几何图示证明，a 和 b（假定非负）的算术平均总是大于或等于其几何平均。什么时候这两个平均相等？

题 2.12 带权重的几何平均。a 和 b 算术平均 (a+b)/2 的一个推广是给 a 和 b 加上不同的权重。什么是几何平均的类似推广？（在题 6.29，你估算小球从桌上掉到地上的接触时间时就会出现带权重的几何平均。）

### 2.4 Analogies

Because abstractions are so useful, it is helpful to have methods for making them. One way is to construct an analogy between two systems. Each common feature leads to an abstraction; each abstraction connects our knowledge in one system to our knowledge in the other system. One piece of knowledge does double duty. Like a mental lever, analogy and, more generally, abstraction are intelligence amplifiers.

2.4 类比

因为抽象如此有用，所以如果有一个进行抽象的方法将会很有帮助。一种途径是在两个体系之间构建类比。每个共同的特征都导致一种抽象；每个抽象都将一个体系的知识和其他体系的知识联系起来。一个知识的片段有了双重的作用。就像一个心灵杠杆，类比，或者更一般地说抽象是智慧的放大器。

#### 2.4.1 Electrical–mechanical analogies

An illustration with many abstractions on which we can practice is the analogy between a spring–mass system and an inductor–capacitor (𝐿𝐶) circuit.

(2.13)

In the circuit, the voltage source — the 𝑉in on its left side — supplies a current that flows through the inductor (a wire wrapped around an iron rod) and capacitor (two metal plates separated by air). As current flows through the capacitor, it alters the charge on the capacitor. This「charge」is confusingly named, because the net charge on the capacitor remains zero. Instead,「charge」means that the two plates of the capacitor hold opposite charges, 𝑄 and −𝑄, with 𝑄 ≠ 0. The current changes 𝑄. The charges on the two plates create an electric field, which produces the output voltage 𝑉out equal to 𝑄/𝐶 (where 𝐶 is the capacitance).

For most of us, the circuit is less familiar than the spring–mass system.

However, by building an analogy between the systems, we transfer our understanding of the mechanical to the electrical system.

In the mechanical system, the fundamental variable is the mass's displacement 𝑥. In the electrical system, it is the charge 𝑄 on the capacitor. These variables are analogous so their derivatives should also be analogous: Velocity (𝑣), the derivative of position, should be analogous to current (𝐼), the derivative of charge.

Let's build more analogy bridges. The derivative of velocity, which is the second derivative of position, is acceleration (𝑎). Therefore, the derivative of current (𝑑𝐼/𝑑𝑡) is the analog of acceleration. This analogy will be useful shortly when we find the circuit's oscillation frequency.

These variables describe the state of the systems and how that state changes: They are the kinematics. But without the causes of the motion — the dynamics — the systems remain lifeless. In the mechanical system, dynamics results from force, which produces acceleration: 

𝑎 = 𝐹/𝑚. (2.14)

Acceleration is analogous to change in current 𝑑𝐼/𝑑𝑡, which is produced by applying a voltage to the inductor. For an inductor, the governing relation (analogous to Ohm's law for a resistor) is:

(2.15)

where 𝐿 is the inductance, and 𝑉 is the voltage across the inductor. Based on the common structure of the two relations, force 𝐹 and voltage 𝑉 must be analogous. Indeed, they both measure effort: Force tries to accelerate the mass, and voltage tries to change the inductor current. Similarly, mass and inductance are analogous: Both measure resistance to the corresponding effort. Large masses are hard to accelerate, and large-𝐿 inductors resist changes to their current. (A mass and an inductor, in another similarity, both represent kinetic energy: a mass through its motion, and an inductor through the kinetic energy of the electrons making its magnetic field.) 

Turning from the mass–inductor analogy, let's look at the spring–capacitor analogy. These components represent the potential energy in the system: in the spring through the energy in its compression or expansion, and in the capacitor through the electrostatic potential energy due to its charge.

Force tries to stretch the spring but meets a resistance 𝑘: The stiffer the spring (the larger its 𝑘), the harder it is to stretch.

(2.16)

Analogously, voltage tries to charge the capacitor but meets a resistance 1/𝐶: The larger the value of 1/𝐶, the smaller the resulting charge.

(2.17)

Based on the common structure of the relations for 𝑥 and 𝑄, spring constant 𝑘 must be analogous to inverse capacitance 1/𝐶. Here are all our analogies.

From this table, we can read off our key result. Start with the natural (angular) frequency 𝜔 of a spring–mass system: 𝜔 = 𝑘/𝑚. Then apply the analogies. Mass 𝑚 is analogous to inductance 𝐿. Spring constant 𝑘 is analogous to inverse capacitance 1/𝐶. Therefore, 𝜔 for the 𝐿𝐶 circuit is 1/ 𝐿𝐶 : 

(2.18)

Because of the analogy bridges, one formula, the natural frequency of a spring–mass system, does double duty. More generally, whatever we learn about one system helps us understand the other system. Because of the analogies, each piece of knowledge does double duty.

2.4.1 电学和力学类比

一个包含很多抽象、可以让我们练习的例子是弹簧-质点体系和电感-电容（LC）电路之间的类比。

在电路中，电源 一一 左边的 Vin 提供了流过电感（导线绕在铁棒上）和电容（两个被空气隔开的金属片）的电流。当电流流过电容时，它改变了电容器上的电荷。「电荷」这个词可能有点误导，因为电容上的净电荷为零。「电荷」意味着电容器的两个极板携带相反的电荷 Q 和 -Q，且 Q≠0。电流改变电荷 Q。这些电荷产生电场，进而产生输出电压 Vout。

```
Vout=Q/C
```

其中 C 是电容。

对于我们，电路不如弹簧-质点体系熟悉。然而，通过构建两个体系之间的类比，我们可以将对力学体系的理解用于对电路体系的理解。对力学体系，基本的变量是质点的位移 x。而在电学体系中，则是电容上的电荷 Q。这些变量是类似的，因此其导数也是类似的：速度（u）是位置的导数，应当类比于电流（I），即电荷的导数。

我们来构建更多的类比桥梁。速度的导数，即位置的二阶导数，是加速度（a）。因此，电流的导数（dI/dt）是与加速度类似的量。我们很快就会发现，这个类比在寻找电路振荡频率时很有用。这些变量描写了体系的状态及状态如何变化：这称为运动学。没有造成运动的原因 一一 即动力学 一一 则体系是静止的。对力学体系，动力学来自力，力产生加速度。

```
a=F/m
```

加速度类似电流的变化 dI/dt，给电感加上电压就会产生这种变化。对于电感，其服从的关系是（类似于电阻的欧姆定律）：

```
dI/dt=V/L
```

其中 L 是电感系数，V 是加在电感上的电压。根据两个关系的相似结构，力 F 和电压 V 应该是相似的。的确，这两个量都描写运动效果。类似地，质量和电感系数是相似的：它们都描写对运动效果的抵抗。质量和电感系数在另一方面也是相似的，都描写动能：质量通过自身的运动，而电感通过产生磁场的电子动能。

从质量-电感的类比，我们来看看弹簧-电容的类比。这些器件都代表了体系的势能：对于弹簧，通过压缩和膨胀而蕴含能量，对于电容，通过电容器上的电荷产生静电能。力拉伸弹簧时会有「阻力」k:

```
x=F/k
```

类似地，电压给电容充电，但也会有一个「阻力」1/C：

```
Q=V/(1/C)
```

根据 x 和 Q 关系之间的相似结构，弹性系数 k 一定和电容的倒数 1/C 类似。下面的表格是我们所有的类比：

从这个表中可以看到关键结果。从弹簧质点体系的本征（角）频率 w 出发：

```
w=√(k/m)
```

然后来应用这个类比。质量 m 与电感系数 L 类似，弹性系数 k与电容倒数 1/C 类似。因此 LC 电路的本征频率为：

```
w=√(1/C/L)=1/√(LC)
```

因为类比的桥梁，一个公式，如弹簧-质点体系的本征频率，就有了双重的用途。更一般地，不论我们从一个体系中学到什么，都可以帮助我们来理解另一个体系。因为类比，每个理解都有了双重的作用。

#### 2.4.2 Energy density in the gravitational field 

With the electrical–mechanical analogy as practice, let's try a less familiar analogy: between the electric and the gravitational field. In particular, we'll connect the energy densities (energy per volume) in the corresponding fields. An electric field 𝐸 represents an energy density of 𝜖0𝐸2/2, where 𝜖0 is the permittivity of free space appearing in the electrostatic force between two charges 𝑞1 and 𝑞2:

𝐹 = 𝑞1𝑞2/4𝜋𝜖0𝑟2. (2.19)

Because electrostatic and gravitational forces are both inverse-square forces (the force is proportional to 1/𝑟2), the energy densities should be analogous.

Not least, there should be a gravitational energy density. But how is it related to the gravitational field?

To answer that question, our first step is to find the gravitational analog of the electric field. Rather than thinking of the electric field only as something electric, focus on the common idea of a field. In that sense, the electric field is the object that, when multiplied by the charge, gives the force: 

force = charge × field. (2.20)

We use words rather than the normal symbols, such as 𝐸 for field or 𝑞 for charge, because the symbols might bind our thinking to particular cases and prevent us from climbing the abstraction ladder.

This verbal form prompts us to ask: What is gravitational charge? In electrostatics, charge is the source of the field. In gravitation, the source of the field is mass. Therefore, gravitational charge is mass. Because field is force per charge, the gravitational field strength is an acceleration: 

gravitational field = force/charge = force/mass = acceleration. (2.21)

Indeed, at the surface of the Earth, the field strength is 𝑔, also called the acceleration due to gravity.

The definition of gravitational field is the first half of the puzzle (we are using divide-and-conquer reasoning again). For the second half, we'll use the field to compute the energy density. To do so, let's revisit the route from electric field to electrostatic energy density: 

𝐸 → 12𝜖0𝐸2. (2.22)

With 𝑔 as the gravitational field, the analogous route is 

𝑔 → 12 × something × 𝑔2, (2.23)

where the「something」represents our ignorance of what to do about 𝜖0.

What is the gravitational equivalent of 𝜖0 ?

To find its equivalent, compare the simplest case in both worlds: the field of a point charge. A point electric charge 𝑞 produces a field:

𝐸 = 1/4𝜋𝜖0·𝑞/𝑟2. (2.24)

A point gravitational charge 𝑚 (a point mass) produces a gravitational field (an acceleration)

𝑔 = 𝐺𝑚/𝑟2, (2.25)

where 𝐺 is Newton's constant.

The gravitational field has a similar structure to the electric field. Both are inverse-square forces, as expected. Both are proportional to the charge.

The difference is the constant of proportionality. For the electric field, it is 1/4𝜋𝜖0. For the gravitational field, it is simply 𝐺. Therefore, 𝐺 is analogous to 1/4𝜋𝜖0; equivalently, 𝜖0 is analogous to 1/4𝜋𝐺.

Then the gravitational energy density becomes:

1/2×1/4𝜋𝐺×𝑔2 = 𝑔2/8𝜋𝐺. (2.26)

We will use this analogy in Section 9.3.3 when we transfer our hard-won knowledge of electromagnetic radiation to understand the even more subtle physics of gravitational radiation.

Problem 2.13 Gravitational energy of the Sun

What is the energy in the gravitational field of the Sun? (Just consider the field outside the Sun.)

Problem 2.14 Pendulum period including buoyancy

The period of a pendulum in vacuum is (for small amplitudes) 𝑇 = 2𝜋 𝑙/𝑔 , where 𝑙 is the bob length and 𝑔 is the gravitational field strength. Now imagine the pendulum swinging in a fluid (say, air). By replacing 𝑔 with a modified value, include the effect of buoyancy in the formula for the pendulum period.

Problem 2.15 Comparing field energies

Find the ratio of electrical to gravitational field energies in the fields produced by a proton.

2.4.2 引力场中的能量密度

有了电学-力学之间类比的实践，我们来尝试下不太熟悉的类比：电场和引力场之间的类比。特别地，我们会将两个场的能量密度（单位体积的能量）联系起来。电场 E 具有能量密度 (εE^2)/2，其中 ε 是真空介电常数，其也出现在两个电荷 q1 和 q2 之间的静电力公式中：

```
F=q1q2/(4πεr^2)
```

因为静电力和引力都是平方反比力（作用力正比于 1/r^2），相应的能量密度也应该是类似的。至少，应该也有一个引力场能量密度。但这个能量密度是如何与引力场联系起来的呢？

为了回答这个问题，我们第一步是找出可以与电场类比的与引力相关的量。但我们并不仅仅将电场看成与电相关的某种东西，而是专注于场的一般概念。在这个意义上，电场是这样一种东西：其乘以电荷就给出力的作用：

```
力=电荷×电场
```

我们使用文字，而不是正规的符号如用 E 表示场，或 q 表示电荷，因为符号会将我们的思维限制在具体的事物上，不利于我们攀登抽象之梯。使用文字将帮助我们进行类比。这一文字的形式促使我们思考：什么是引力荷？在静电学中，电荷是电场的源。在引力场中，场源是质量。因此，引力荷就是质量；进一步可见，引力场就是加速度：

```
引力场=力/引力荷=力/质量=加速度
```

的确，在地球表面，引力场强度是 g，也称为重力加速度。引力场的定义是前半个难题（我们又在运用分而治之法）。对于后半个难题，我们将用场来计算能量密度。为了这个目的，我们先重温下从电场到静电能量密度的过程：

```
E→1/2·(εE^2)
```

因为 g 是引力场，类似的有：

```
g→1/2x某个量×g^2
```

这里，「某个量」代表我们忽略的与 ε 类似的量。

➤ 什么是 ε 的引力对应量？

为了找到对应的量，比较两个体系的最简单情况：点荷的场。一个点电荷 q 产生的电场为：

```
E=(1/4πε)·q/r^2
```

一个点引力荷 m（质点）产生的引力场（加速度）为：

```
g=Gm/r^2
```

其中 G 是引力常数。引力场具有与电场相似的结构：都是平方反比力，这正是所预料的；都正比于荷。差别在于比例系数。对于电场，比例系数为 1/4πε，对于引力场，就是简单的 G。因此，G 类似于 1/4πε；等价地，ε 类似于 1/4πG。于是，引力场能量密度就是：

```
(1/2)·(1/4πG)·g^2
```

在章节 9.3.3，当我们需要将来之不易的电磁辐射知识用于理解更复杂难懂的引力辐射时，会再次使用这个类比。

题 2.13 太阳的引力能。太阳总的引力能是多少？将太阳之外所有空间的都加起来。

题 2.14 考虑浮力的单摆周期。真空中的单摆周期（对于小振幅）是 T=2π√(l/g)，其中 l 是摆长，g 是引力场强度。现在假定单摆在流体（比如说，空气）中摆动。用个修正值来代替 g，将浮力效应包括在单摆周期的公式中。

题 2.15 比较场的能量。找出质子产生的电场和引力场的能量之比。

#### 2.4.3 Parallel combination

Analogies not only reuse work, they help us rewrite expressions in compact, insightful forms. An example is the idea of parallel combination. It appears in the analysis of the infinite resistive ladder of Problem 2.8.

To find the resistance 𝑅 across the ladder (in other words, what the ohmmeter measures between the nodes A and B), you represent the entire ladder as a single resistor 𝑅. Then the whole ladder is 1 ohm in series with the parallel combination of 1 ohm and 𝑅:

The next step in finding 𝑅 usually invokes the parallel-resistance formula: that the resistance of 𝑅1 and 𝑅2 in parallel is:

𝑅1𝑅2/𝑅1+𝑅2 (2.28)

For our resistive ladder, the parallel combination of 1 ohm with the ladder is 1 ohm × 𝑅/(1 ohm + 𝑅). Placing this combination in series with 1 ohm gives a resistance

(2.29)

This recursive construction reproduces the ladder, only one unit longer. We therefore get an equation for 𝑅:

(2.30)

The (positive) solution is 𝑅 = (1 + 5)/2 ohms. The numerical part is the golden ratio 𝜙 (approximately 1.618). Thus, the ladder, when built with 1-ohm resistors, offers a resistance of 𝜙 ohms.

Although the solution is correct, it skips over a reusable idea: the parallel combination. To facilitate its reuse, let's name the idea with a notation: 

𝑅1 || 𝑅2. (2.31)

This notation is self-documenting, as long as you recognize the symbol || to mean「parallel,」a recognition promoted by the parallel bars. A good notation should help thinking, not hinder it by requiring us to remember how the notation works. With this notation, the equation for the ladder resistance 𝑅 is:

(2.32)

(the parallel-combination operator has higher priority than — is computed before — the addition). This expression more plainly reflects the structure of the system, and our reasoning about it, than does the version:

(2.33)

The ∥ notation organizes the complexity.

Once you name an idea, you find it everywhere. As a child, after my family bought a Volvo, I saw Volvos on every street. Similarly, we'll now look at examples of parallel combination far beyond the original appearance of the idea in circuits. For example, it gives the spring constant of two connected springs (Problem 2.16):

(2.34)

Problem 2.16 Springs as capacitors

Using the analogy between springs and capacitors (discussed in Section 2.4.1), explain why springs in series combine using the parallel combination of their spring constants.

Another surprising example is the following spring–mass system with two masses:

The natural frequency 𝜔, expressed without our ∥ abstraction, is:

𝜔 = 𝑘(𝑚 + 𝑀)/𝑚𝑀 (2.35)

This form looks complicated until we use the ∥ abstraction: 

𝜔 = 𝑘 / 𝑚 || 𝑀 (2.36)

Now the frequency makes more sense. The two masses act like their parallel combination 𝑚 || 𝑀:

The replacement mass 𝑚 ∥ 𝑀 is so useful that it has a special name: the reduced mass. Our abstraction organizes complexity by turning a three-component system (a spring and two masses) into a simpler two-component system.

In the spirit of notation that promotes insight, use lowercase (「small」) 𝑚 for the mass that is probably smaller, and uppercase (「big」) 𝑀 for the mass that is probably larger. Then write 𝑚 ∥ 𝑀 rather than 𝑀 ∥ 𝑚. These two forms produce the same result, but the 𝑚 ∥ 𝑀 order minimizes surprise: The parallel combination of 𝑚 and 𝑀 is smaller than either mass (Problem 2.17), so it is closer to 𝑚, the smaller mass, than to 𝑀. Writing 𝑚 ∥ 𝑀, rather than 𝑀 ∥ 𝑚, places the most salient information first.

Problem 2.17 Using the resistance analogy

By using the analogy with parallel resistances, explain why 𝑚 ∥ 𝑀 is smaller than 𝑚 and 𝑀.

Why do the two masses combine like resistors in parallel?

The answer lies in the analogy between mass and resistance. Resistance appears in Ohm's law:

voltage = resistance × current. (2.37)

Voltage is an effort. Current, which results from the effort, is a flow. Therefore, the more general form — one step higher on the abstraction ladder — is 

effort = resistance × flow. (2.38)

In this form, Newton's second law,

force = mass × acceleration, (2.39)

identifies force as the effort, mass as the resistance, and acceleration as the flow.

Because the spring can wiggle either mass, just as current can flow through either of two parallel resistors, the spring feels a resistance equal to the parallel combination of the resistances — namely, 𝑚 || 𝑀.

Problem 2.18 Three springs connected

What is the effective spring constant of three springs connected in a line, with spring constants 2, 3, and 6 newtons per meter, respectively?

2.4.3 并联组合

类比不仅一次次地解决问题，同时也帮助我们将表达式改写成紧凑和富有洞察力的形式。这在下面题 2.8 的无限电阻网络的分析中可以看到。

为了找到网格的电阻 R（换言之，节点 A 和 B 之间电阻表的测量值），你可以将整个网格的电阻值用一个单一电阻 R 表示。则整个网格的电阻就等于一个 1 欧姆电阻串联一对并联的 1 欧姆和 R。

下一步通常要用到并联电阻公式得到 R。R1 和 R2 并联后的电阻为：

```
R1R2/(R1+R2)
```

对于我们的电阻网格，忽略欧姆这个单位，与 1 欧姆并联的结果是 R/(1+R)。将这个组合与 1 欧姆串联，得到电阻：

```
1+R/(1+R)
```

因此我们得到关于 R 的方程：

```
R=1+R/(1+R)
```

（正值）解为 R=(1+√5)/2，这就是黄金分割比例 Φ（约 1.618）。因此，用 1 欧姆电阻构建的电阻网格，其电阻值为 φ 欧姆。

尽管这个解是正确的，但忽略了一个可重复应用的概念：并联组合为了促进这个概念的重复应用，我们用下面的记号表示这个概念：

```
R1 || R2
```

这个记号是自明的，只要认识到记号「||」（由两个平行棒而来的记号）表示平行。好的记号可以帮助思考，而不是让记忆记号的用途这个过程来阻碍思考。利用这个记号，网格电阻 R 的方程变成：

```
R=1+1 || R
```

（并联组合的计算要优先于 一一 即先计算 一一 加法。）这个方程更清楚地反映了体系的结构，对它的分析，也要优于对方程：

```
R=1+R/(1+R)
```

的分析。记号「||」组织了复杂性。

一旦对概念命名，就会发现到处都出现这个概念。小时候家里买了辆沃尔沃，结果我发现街上到处是沃尔沃。类似地，我们现在来看一个与最初产生这个概念的电路相差很远的并联组合例子。比如说，两个连接的弹簧的弹性常数（题 2.16）：

题 2.16 作为电容器的弹簧。利用弹簧和电容器之间的类比（章节 2.4.1），解释为什么串联的弹簧可以用并联组合公式来计算弹性常数。另一个令人惊讶的例子是两个质点的弹簧质点体系。

本征频率 w 不用记号「||」的话可以表示为：

```
w=k(m+M)/mM
```

这个形式看上去有点复杂，但如果用了「||」这个抽象记号则变成：

```
w=k/(m||M)
```

这样频率变得更有意义。两个质点的行为像它们的并联组合 m||M：

质量 m‖M 非常有用，还因此有一个特殊的名字：约化质量。我们组织复杂性的抽象方法将一个三体系统（一个弹簧和两个质点）转换成了一个较为简单的两体系统。在能够提升洞察力的符号精神下，用小写字母 m 表示较小的质量，用大写字母 M 表示较大的质量。然后写成 m||M 而不是 M||m。这两种形式得到的是相同的结果，但 m||M 的顺序会把对此的惊讶降到最低：m 和 M 的并联组合比其中每一个质量都小（题 2.17），因而相对于 M 更接近于较小的质量 m。写成 m||M 而不是 M||m，是将最重要的信息放在第一。

题 2.17 利用阻抗的相似性。利用与并联电阻的相似性，解释为何 m||M 要小于 m 和 M。

➤ 为什么上面的两个质点类似于并联的两个电阻？

答案在于质量和电阻的相似性。电阻出现在欧姆定律中：

```
电压=电阻×电流
```

电压是「外力」。电流在「外力」作用下产生。因此，最一般的形式 一一 在抽象之梯上再上一步 一一 就是：

```
外力=阻抗×流
```

用这种形式，牛顿第二定律变为：

```
力=质量×加速度
```

就可以将力看成「外力」，质量看成一种阻抗，而加速度就是一种流。因为弹簧可以使每一个质点振动，就像电流可以流过两个并联电阻的每一个一样，弹簧感受到的「阻力」就等于并联组合的「阻力」 一一 即 m||M。

题 2.18 三个弹簧的连接。三个弹簧串联后的有效弹性常数是多少？这三个弹簧的弹性常数分别是 2、3、6（牛顿/米）。

#### 2.4.4 Impedance as a higher-level abstraction 

Resistance, in the electrical sense, has appeared several times, and it underlies a higher-level abstraction: impedance. Impedance extends the idea of electrical resistance to capacitors and inductors. Capacitors and inductors, along with resistors, are the three linear circuit elements: In these elements, the connection between current and voltage is described by a linear equation: For resistors, it is a linear algebraic relation (Ohm's law); for capacitors or inductors, it is a linear differential equation.

Why should we extend the idea of resistance?

Resistors are easy to handle. When a circuit contains only resistors, we can immediately and completely describe how it behaves. In particular, we can write the voltage at any point in the circuit as a linear combination of the voltages at the source nodes. If only we could do the same when the circuit contains capacitors and inductors.

We can! Start with Ohm's law,

current = voltage / resistance, (2.40)

and look at it in the higher-level and expanded form:

flow = 1 / resistance × effort. (2.41)

For a capacitor, flow will still be current. But we'll need to find the capacitive analog of effort. This analogy will turn out slightly different from the electrical–mechanical analogy between capacitance and spring constant (Section 2.4.1), because now we are making an analogy between capacitors and resistors (and, eventually, inductors). For a capacitor, 

charge = capacitance × voltage. (2.42)

To turn charge into current, we differentiate both sides to get:

current = capacitance × 𝑑(voltage)/𝑑𝑡 (2.43)

To make the analogy quantitative, let's apply to the capacitor the simIplest voltage whose form is not altered by differentiation: 

(2.44)

where 𝑉 is the input voltage, 𝑉0 is the amplitude, 𝜔 is the angular frequency, and 𝑗 is the imaginary unit −1. The voltage 𝑉 is a complex number; but the implicit understanding is that the actual voltage is the real part of this complex number. By finding how the current 𝐼 (the flow) depends on 𝑉 (the effort), we will extend the idea of resistance to a capacitor.

With this exponential form, how can we represent the more familiar oscillating voltages 𝑉1 cos 𝜔𝑡 or 𝑉1 sin 𝜔𝑡 , where 𝑉1 is a real voltage?

Start with Euler's relation:

(2.45)

To make 𝑉1 cos 𝜔𝑡, set 𝑉0 = 𝑉1 in 𝑉 = 𝑉0 𝑒𝑗𝜔𝑡. Then 𝑉 = 𝑉1(cos 𝜔𝑡 + 𝑗 sin 𝜔𝑡).

(2.46)

and the real part of 𝑉 is just 𝑉1 cos 𝜔𝑡.

Making 𝑉1 sin 𝜔𝑡 is more tricky. Choosing 𝑉0 = 𝑗𝑉1 almost works: 

𝑉 = 𝑗𝑉1(cos 𝜔𝑡 + 𝑗 sin 𝜔𝑡) = 𝑉1(𝑗 cos 𝜔𝑡 − sin 𝜔𝑡). (2.47)

The real part is −𝑉1 sin 𝜔𝑡, which is correct except for the minus sign. Thus, the correct amplitude is 𝑉0 = −𝑗𝑉1. In summary, our exponential form can compactly represent the more familiar sine and cosine signals.

With this exponential form, differentiation is simpler than with sines or cosines. Differentiating 𝑉 with respect to time just brings down a factor of 𝑗𝜔, but otherwise leaves the 𝑉0 𝑒𝑗𝜔𝑡 alone:

(2.48)

With this changing voltage, the capacitor equation, 

current = capacitance × 𝑑(voltage)

(2.49)

becomes

current = capacitance × 𝑗𝜔 × voltage. (2.50)

Let's compare this form to its analog for a resistor (Ohm's law): 

current = 1 / resistance × voltage. (2.51)

Matching up the pieces, we find that a capacitor offers a resistance 

𝑍𝐶 = 1 / 𝑗𝜔𝐶. (2.52)

This more general resistance, which depends on the frequency, is called impedance and denoted 𝑍. (In the analogy of Section 2.4.1 between capacitors and springs, we found that capacitor offered a resistance to being charged of 1/𝐶. Impedance, the result of an analogy between capacitors and resistors, contains 1/𝐶 as well, but also contains the frequency in the 1/𝑗𝜔 factor.) Using impedance, we can describe what happens to any sinusoidal signal in a circuit containing capacitors. Our thinking is aided by the compact notation — the capacitive impedance 𝑍𝐶 (or even 𝑅𝐶). The notation hides the details of the capacitor differential equation and allows us to transfer our intuition about resistance and flow to a broader class of circuits.

The simplest circuit with resistors and capacitors is the so-called low-pass 𝑅𝐶 circuit. Not only is it the simplest interesting circuit, it will also be, thanks to further analogies, a model for heat flow. Let's apply the impedance analogy to this circuit.

To help us make and use abstractions, let's imagine defocusing our eyes. Under blurry vision, the capacitor looks like a resistor that just happens to have a funny resistance 𝑅𝐶 = 1/𝑗𝜔𝐶. Now the entire circuit looks just like a pure-resistance circuit. Indeed, it is the simplest such circuit, a voltage divider. Its behavior is described by one number: the gain, which is the ratio of output to input voltage 𝑉out/𝑉in.

In the 𝑅𝐶 circuit, thought of as a voltage divider, 

(2.53)

Because 𝑅𝐶 = 1/𝑗𝜔𝐶, the gain becomes

(2.54)

After clearing the fractions by multiplying by 𝑗𝜔𝐶 in the numerator and denominator, the gain simplifies to

(2.55)

Why is the circuit called a low-pass circuit?

At high frequencies (𝜔 → ∞), the 𝑗𝜔𝑅𝐶 term in the denominator makes the gain zero. At low frequencies (𝜔 → 0), the 𝑗𝜔𝑅𝐶 term disappears and the gain is 1. High-frequency signals are attenuated by the circuit; low-frequency signals pass through mostly unchanged. This abstract, high-level description of the circuit helps us understand the circuit without our getting buried in equations. Soon we will transfer our understanding of this circuit to thermal systems.

The gain contains the circuit parameters as the product 𝑅𝐶. In the denominator of the gain, 𝑗𝜔𝑅𝐶 is added to 1; therefore, 𝑗𝜔𝑅𝐶, like 1, must have no dimensions. Because 𝑗 is dimensionless (is a pure number), 𝜔𝑅𝐶 must be itself dimensionless. Therefore, the product 𝑅𝐶 has dimensions of time.

This product is the circuit's time constant — usually denoted 𝜏.

The time constant has two physical interpretations. To construct them, we imagine charging the capacitor using a constant input voltage 𝑉0; eventually (after an infinite time), the capacitor charges up to the input voltage (𝑉out = 𝑉0) and holds a charge 𝑄 = 𝐶𝑉0. Then, at 𝑡 = 0, we make the input voltage zero by connecting the input to ground.

The capacitor discharges through the resistor, and its voltage decays exponentially:

After one time constant 𝜏, the capacitor voltage falls by a factor of 𝑒 toward its final value — here, from 𝑉0 to 𝑉0/𝑒. The 1/𝑒 time is our first interpretation of the time constant. Furthermore, if the capacitor voltage had decayed at its initial rate (just after 𝑡 = 0), it would have reached zero voltage after one time constant 𝜏 — the second interpretation of the time constant.

The time-constant abstraction hides — abstracts away — the details that produced it: here, electrical resistance and capacitance. Nonelectrical systems can also have a time constant but produce it by a different mechanism.

Our high-level understanding of time constants, because it is not limited to electrical systems, will help us transfer our understanding of the electrical low-pass filter to nonelectrical systems. In particular, we are now ready to understand heat flow in thermal systems.

Problem 2.19 Impedance of an inductor

An inductor has the voltage–current relation:

(2.56)

where 𝐿 is the inductance. Find an inductor's frequency-dependent impedance 𝑍𝐿. After finding this impedance, you can analyze any linear circuit as if it were composed only of resistors.

2.4.4 作为高级抽象的阻抗

电学中的电阻已经出现过很多次了，其中隐含了一个高级的抽象：阻抗。阻抗把电阻的概念推广到了电容器和电感器。电容器、电感器以及电阻是三个线性电路元件 一一 对于这些元件，电流和电压之间的关系是用线性方程描述的；对于电阻，是代数方程（欧姆定律）；对电容或电感，则是微分方程。

1『这一小节的内容目前基本没看懂，原书中很多图可以助力理解。（2022-05-14）』

➤ 为什么我们需要推广电阻的概念？

电阻是容易处理的。如果一个电路包含电阻，那么你立刻就能完整地描述电路的性质。比如说，你可以写出电路中任意一点的电压，这是电源节点的线性组合。但如果电路中包含电容器和电感器，我们还能做到吗？当然能！从欧姆定律出发，

```
电流=电压/电阻
```

可以站在更高的层次来看这个方程，并写成：

```
流=(1/阻抗)·外力
```

现在我们需要提升「外力」的观念，不仅仅限于电压。否则我们无法将阻抗的概念推广到电容器，相应的方程为：

```
电荷=电容×电压
```

但电荷不太像是一种流。至少对电容器而言，电压也不是一种「外力」：一个理想的电容器储存其电荷并永久维持相应的电压 一一 没有任何外力。通过两边微分可以解决这个问题，并得到：

```
电流=电容xd(电压)/dt
```

电流是一种流；电压改变像是一种外力。做了这样一个类比后，电容就类似于电阻的倒数。

为了让类比定量，我们给电容器加一个最简单的电压，其形式不因微分而改变：

```
V=V0·e^(jwt)
```

其中 V 是输入电压，V0 为振幅，w 为角频率，j 为虚数单位 √-1。电压 V 是复数；但实际电压理解为这个复数的实部。找出电流 I（即流）和 V（外力）的关系，我们就把阻抗的概念推广到了电容器。

➤ 如果用这个指数形式，我们如何表示更熟悉的振荡电压 V1coswt 或 V1sinwt 呢？其中 V1 为实数电压。

从欧拉关系出发：

```
e^(jwt)=coswt+j·sinwt
```

为了得到 V1coswt，在 V=V0·e^(jwt) 中令 V0=V1。则：

```
V=V1(coswt+j·sinwt)
```

因此 V 的实部就是 V1coswt。想得到 V1sinwt 需要一点技巧。令V0=jV1 就可以了：

```
V=jV1(coswt+jsinwt)=V1(jcoswt-sinwt)
```

实部为 -V1sinwt，除去负号就是我们想要的。正确的振幅应取 V0=-jV1。

总结一下，所用的指数形式可以简洁地表示我们更熟悉的正弦和余弦信号。用指数形式，微分要比正弦和余弦简单。V 对时间的微商只是多个因子 jw，但保持 V0·e^(jwt) 不变：

利用这个变化的电压，电容方程：

```
电流=电容xd(电压)/dt
```

变成：

```
电流=电容×jw×电压
```

将此与电阻方程（欧姆定律）比较：

```
电流=电压/电阻
```

综合上述结果，我们得到电容器的阻抗：

```
Zc=1/jwC
```

这个更一般的阻抗与频率有关，称为容抗，用 Zc 表示。利用这个阻抗，我们可以描写一个包含电容器的电路中任何正弦信号的情况。这样一个紧湊的符号 一一 即容抗 Zc（或甚至 Rc）帮助了我们的思考。这个符号隐藏了电容器微分方程的细节，使得我们可以将电阻和电流的直观概念推广到更一般的电路。

最简单的包含电阻和电容的电路是所谓的低通 RC 电路。不仅因为这是最简单的有趣电路，作进一步的类比，这也将是热流的模型。让我们将阻抗的类比用于这个电路。

为了帮助我进行抽象，我假设将眼睛散焦。在模糊的视力下，电容器看起来就像是一个电阻并且具有有趣的阻值 Rc=1/jwC。现在整个电路看上去就像一个纯电阻电路。的确，这是最简单的这类电路，即分压电路。其行为可以用一个数来描写，即增益。这是输出电压与输入电压之比 Vout/Vin。

对于 RC 电路，如果将其看成分压电路，则：

```
增益=容抗/总阻抗=Rc/(R+Rc)
```

因为 Rc=1/jwC，因此增益变成：

```
增益=(1/jwC)/(R+1/jwC)
```

分子、分母同乘因子 jwC 后，增益简化为：

```
增益=1/(1+jwRC)
```

➤ 为什么这个电路叫作低通电路？

在高频（w→∞），分母中的项 jwRC 使增益趋于零。在低频（w→0），项 jwRC 消失使增益趋于 1。即高频信号被电路抑制，而低频信号可以几乎不受影响地通过。这样一种抽象方式，即电路的高级描写方式使得我们得以理解电路，而不至于被淹没在方程之中。在研究了时间常数这个概念后，我们将把对这个电路的理解推广到热学系统。

增益包含的电路参数以 RC 乘积的形式出现。在增益的分母中，jwRC 和 1 相加；因此，jwRC 和 1 一样都没有量纲。因为 j 没有量纲（是个纯数）, wRC 必须是无量纲的。因此，乘积 RC 具有时间的量纲。这乘积是电路的时间常数 一一 通常用来 τ 表示。

时间常数有两个物理解释。为了给出这些解释，假设我们用常数 V0 的输入电压对电容器充电，最后（经过无限长时间），电容器被充到输入电压（Vout=V0），并具有电荷 Q=CV0。然后，在 t=0，通过将输入端接地使输入电压变为零。

电容器就开始通过电阻放电，其电压按指数衰减，如下图所示。经过一个时间常数 τ 之后，电压与初始值相比下降了因子 e 一一 即从 V0 下降到 V0/e。这个 1/e 倍是我们关于时间常数的第一个解释。并且，如果电容器电压按初始时刻（即紧接着 t=0）的速率衰减，则经过一个时间常数 τ 之后，电压将下降到零 一一 这是时间常数的第二个解释。

时间常数的抽象隐藏了或者说抽象掉了产生它的细节：在这儿就是电阻和电容。其他的非电路系统同样可以有一个时间常数，但产生的机制是不同的。因为并没有限制于电路系统，关于时间常数的深层次理解可以帮助我们将对低通滤波电路的理解推广到非电路系统，尤其是我们可以用来理解热学系统中的热流。

题 2.19 电感的感抗。一个电感具有如下的电压-电流关系：

```
V=L·dI/dt
```

其中 L 是电感。求电感的感抗（依赖于频率）。然后，就可以分析任何线性电路，并将其看成只包含电阻的电路。

#### 2.4.5 Thermal systems

The 𝑅𝐶 circuit is a model for thermal systems — which are not obviously connected to circuits. In a thermal system, temperature difference, the analog of voltage difference, produces a current of energy. Energy current, in less fancy words, is heat flow. Furthermore, the current is proportional to the temperature difference — just as electric current is proportional to voltage difference. In both systems, flow is proportional to effort. Therefore, heat flow can be understood by using circuit analogies.

As an example, I often prepare a cup of tea but forget to drink it while it is hot. Like a discharging capacitor, the tea slowly cools toward room temperature and become undrinkable. Heat flows out through the mug. Its walls tea provide a thermal resistance; by analogy to an 𝑅𝐶 circuit, let's denote the thermal resistance 𝑅t. The heat is stored in the water and mug, which form a heat reservoir. This reservoir, of heat rather than of charge, provides the thermal capacitance, which we denote 𝐶t. (Thus, the mug participates in the thermal resistance and capacitance.) Resistance and capacitance are transferable ideas.

The product 𝑅t𝐶t is, by analogy to the 𝑅𝐶 circuit, the thermal time constant 𝜏. To estimate 𝜏 with a home experiment (the method we used in Section 1.7), heat up a mug of tea; as it cools, sketch the temperature gap between the tea and room temperature. In my extensive experience of tea neglect, an enjoyably hot cup of tea becomes lukewarm in half an hour. To quantify these temperatures, enjoyably warm may be 130 ∘F (≈ 55 C), room temperature is 70 ∘F (≈ 20 C), and lukewarm may be 85 ∘F (≈ 30 C).

Based on the preceding data, what is the approximate thermal time constant of the mug of tea?

In one thermal time constant, the temperature gap falls by a factor of 𝑒 (just as the voltage gap falls by a factor of 𝑒 in one electrical time constant). For my mug of tea, the temperature gap between the tea and the room started at 60 F:

In the half hour while the tea cooled in the microwave, the temperature gap fell to 15 F:

(2.58)

Therefore, the temperature gap decreased by a factor of 4 in half an hour. Falling by the canonical factor of 𝑒 (roughly 2.72) would require less time: perhaps 0.3 hours (roughly 20 minutes) instead of 0.5 hours. A more precise calculation would be to divide 0.5 hours by ln 4, which gives 0.36 hours.

However, there is little point doing this part of the calculation so precisely when the input data are far less precise. Therefore, let's estimate the thermal time constant 𝜏 as roughly 0.3 hours.

Using this estimate, we can understand what happens to the tea mug when, as it often does, it spends a lonely few days in the microwave, subject to the daily variations in room temperature. This analysis will become our model for the daily temperature variations in a house.

How does a teacup with 𝜏 ≈ 0.3 hours respond to daily temperature variations?

First, set up the circuit analogy. The output signal is still the tea's temperature. The input signal is the (sinusoidally) varying room temperature. However, the ground signal, which is our reference temperature, cannot also be the room temperature. Instead, we need a constant reference temperature. The simplest choice is the average room temperature 𝑇avg. (After we have transferred this analysis to the temperature variation in houses, we'll see that the conclusion is the same even with a different reference temperature.) The gain connects the amplitudes of the output and input signals: 

(2.59)

The input signal (room temperature) varies with a frequency 𝑓 of 1 cycle per day. Then the dimensionless parameter 𝜔𝜏 in the gain is roughly 0.1.

Here is that calculation:

(2.60)

The system is driven by a low-frequency signal: 𝜔 is not large enough to make 𝜔𝜏 comparable to 1. As the gain expression reminds us, the mug of tea is a low-pass filter for temperature variations. It transmits this low-frequency input temperature signal almost unchanged to the output — to the tea temperature. Therefore, the inside (tea) temperature almost exactly follows the outside (room) temperature.

The opposite extreme is a house. Compared to the mug, a house has a much higher mass and therefore thermal capacitance. The resulting time constant 𝜏 = 𝑅t𝐶t is probably much longer for a house than for the mug. As an example, when I taught in sunny Cape Town, where houses are often unheated even in winter, the mildly insulated house where I stayed had a thermal time constant of approximately 0.5 days.

For this house the dimensionless parameter 𝜔𝜏 is much larger than it was for the tea mug. Here is the corresponding calculation.

(2.61)

What consequence does 𝜔𝜏 ≈ 3 have for the indoor temperature?

In the Cape Town winter, the outside temperature varied daily between 45 ∘F and 75 ∘F; let's also assume that it varied approximately sinusoidally.

This 30 ∘F peak-to-peak variation, after passing through the house low-pass filter, shrinks by a factor of approximately 3. Here is how to find that factor by estimating the magnitude of the gain.

(2.62)

(It is slightly confusing that the outside temperature is the input signal, and the inside temperature is the output signal!) Now plug in 𝜔𝜏 ≈ 3 to get:

(2.63)

In general, when 𝜔𝜏 ≫ 1, the magnitude of the gain is approximately 1/𝜔𝜏. Therefore, the outside peak-to-peak variation of 30 ∘F becomes a smaller inside peak-to-peak variation of 10 ∘F. Here is a block diagram showing this effect of the house low-pass filter.

(2.64)

Our comfort depends not only on the temperature variation (I like a fairly steady temperature), but also on the average temperature.

What is the average temperature indoors?

It turns out that the average temperature indoors is equal to the average temperature outdoors! To see why, let's think carefully about the reference temperature (our thermal analog of ground). Before, in the analysis of the forgotten tea mug, our reference temperature was the average indoor temperature. Because we are now trying to determine this value, let's instead use a known convenient reference temperature — for example, the cool 10 ∘C, which makes for round numbers in Celsius or Fahrenheit (50 F).

The input signal (the outside temperature) varied in winter between 45 F and 75 F. Therefore, it has two pieces: (1) our usual varying signal with the 30 ∘F peak-to-peak variation, and (2) a steady signal of 10 F.

(2.65)

The steady signal is the difference between the average outside temperature of 60 F and the reference signal of 50 F.

Let's handle each piece in turn — we are using divide-and-conquer reasoning again. We just analyzed the varying piece: It passes through the house low-pass filter and, with 𝜔𝜏 ≈ 3, it shrinks significantly in amplitude. In contrast, the nonvarying part, which is the average outside temperature, has zero frequency by definition. Therefore, its dimensionless parameter 𝜔𝜏 is exactly 0. This signal passes through the house low-pass filter with a gain of 1. As a result, the average output signal (the inside temperature) is also 60 ∘F: the same steady 10 F signal measured relative to the reference temperature of 50 F.

The 10 ∘F peak-to-peak inside-temperature amplitude is a variation around 60 ∘F. Therefore, the inside temperature varies between 55 F and 65 F (13 ∘C to 18 ∘C). Indoors, when I am not often running or otherwise generating much heat, I feel comfortable at 68 ∘F (20 ∘C). So, as this circuit model of heat flow predicts, I wore a sweater day and night in the Cape Town house. (For more on using 𝑅𝐶 circuit analogies for building design, see the「Design masterclass」article by Doug King [30].) 

Problem 2.20 When is the house coldest?

Based on the general form for the gain, 1/(1+𝑗𝜔𝜏), when in the day will the Cape Town house be the coldest, assuming that the outside is coldest at midnight?

2.4.5 热学系统

RC 电路可以作为热学系统模型 一一 尽管热学系统并不是明显地和电路有关。在热学系统中，是温差（与电压类似的量）导致了能流。能量流用不太时髦的词来说，就是热流。并且，热流正比于温差 一一 正如电流正比于电压一样。在这两个系统中，流都正比于驱动力。因此，热流可以用电路的类比来理解，特别地，可以用低通滤波电路来理解。

举例来说，我常常会泡一杯茶，但由于比较烫而忘了喝。像电容放电样，茶会慢慢冷却到室温而没法再喝。热量通过杯子流失了。杯壁起到了热阻抗的作用；与 RC 电路类比，将热阻抗用 Rt 表示。

热量储存在水和杯子里，水和杯子起到了热库的作用。是这个热库而不是电荷库提供了热量的储存，我们将其表示为 Ct（这样，杯子起到了热阻抗和热容器的作用。）阻抗和容器是可转换的概念。与 RC 电路类似，乘积 RtCt 是热学时间常数 τ。为了估算 τ，我们可以进行一个家庭实验（这个方法我们曾在章节 1.7 用过）。

先加热一杯茶当它冷却时，画出茶温和室温之间的温度变化。以我丰富的饮茶经验，杯可享用的热茶冷却半小时就变成温茶。为了量化这些温度，可享用的热茶温度约在华氏 130F（55℃），室温在华氏 70F（≈20℃），温茶约在华氏 85F（30℃）。

➤ 根据这些数据，这杯茶的热学时间常数大约是多少呢？

经过一个热学时间常数后，温度下降的因子为 e（正如经过一个电学时间常数后，电压下降的因子为 e 一样）。对于我这杯茶，茶温和室温之间一开始的温差是华氏 60°F：

```
可享用的茶温-室温=60°F
```

经过半小时，如果茶在微波炉中冷却，温差下降到华氏 15°F 度：

```
温热的茶温-室温=15°F 
```

因此，在半小时内温差下降了 4 倍。如果下降一个典型的因子 e（约 2.72）倍则将只需要较短的时间：或许是 0.3 小时（约 20 分钟）而不是 0.5 小时。更精确的计算是用 ln4 来除 0.5 小时，这给出 0.36 小时。然而，在输入数据如此不精确的情况下，没有什么必要去做如此精确的计算。因此，我们可以粗略地估算热学时间常数 τ 约为 0.3 小时。

1『常数 e 为 2.72 要形成肌肉记忆，本能。（2022-05-14）』

利用这个估算，我们就能理解经常发生的一杯茶在微波炉中孤独地待了几天所发生的情况，这当然取決于每天室温的变化。这个分析将成为我们分析房间里一天温度变化的模型。

➤ 杯茶是如何随着一天的温度变化而变化的，如果 τ=0.3 小时？

首先，建立电路的类比。输出仍然是茶温，输入则是变化的室温。然而，接地端，则是我们的参考温度，不能也是室温。我们需要一个恒定的参考温度。最简单的选择就是取平均室温「T平均」。（当我们将这个分析推广到房间内的温度变化的分析时，我们会看到结论是一样的，只是取了不同的参考温度。）

连接输入和输出的放大器的增益为：

```
增益=输出振幅/输入振幅=1/(1+jwτ)
```

输入（室温）按照每天 1 个周期的频率 f 变化。因此，增益表达式中无量纲参数 wτ 约为 0.1：

这个系统由一个低频信号驱动：w 没足够大到使得 wτ 接近于 1。这个增益表达式提醒我们，茶杯对于温度变化来说是个低通滤波器。它将这个低频输入温度几乎没有改变地传输到了输出 一一 茶温。因此，内部（茶）温几乎完全和外部（室）温一样。

另一个极端情况是房子。与茶杯比较，房子具有大得多的质量，因而具有更大的热容量。相应地，房子的热学时间常数 τ=RtCt，也要比茶杯的长得多。对一个希腊式房子的研究给出结果 τ≈86 小时，大约 4 天。这些房子一定具有很好的绝热效果！当年我在开普敦教书的时候，那里阳光明媚，甚至在冬天房子都没有暖气，我住的房子隔热不是很好，热学时间常数大约只有 0.5 天。

对于开普敦的房子，无量纲常数 wτ 比茶杯的相应常数要大得多：

➤ wτ≈3 对室内温度会有什么影响？

在冬天，室外温度在华氏 45F 到 75F 之间。峰谷到峰顶有华氏 30F 的变化，经过房子这个低通滤波器，这个变化就被压缩了大概 3 倍。下面通过估算增益的大小来给出如何得到这个因子的。

一般地，当 wτ 远大于 1，增益的大小近似为 1/wτ。因此，室外温度峰谷-峰顶的华氏 30F 变化就变成室内温度的华氏 10F 的变化：

➤ 室内平均温度是多少？

可以得到室内平均温度等于室外平均温度！为了知道原因，我们来仔细考虑参考温度（即接地的热学类比）。之前，在分析遗忘的茶杯时，我们的参考温度是室内平均温度。因为我们现在试图要确定这个值，就让我们使用已知的、方便的参考温度 一一 比如，较冷的 10℃，这是以摄氏或华氏（50F）取整后的值。

输入（室外温度）冬天在华氏 45F 到华氏 75F 之间变化。因此，可以将其分为两部分：1）通常的峰谷-峰顶之间华氏 30F 的变化；2）稳定的华氏 10F 的变化。

稳定的部分是室外平均温度华氏 60F 与参考温度华氏 50F 之差。

我们分别来处理每一部分 一一 这里我们再次使用了分而治之法。我们只需分析变化的部分：输入信号通过房子这一低通滤波器后，由于 wτ≈3，振幅会有一个显著的压缩。与此相反，不变的部分，即室外平均温度，按照定义频率为 0。因此，相应的无量纲参数 wτ 严格为 0。

当这一信号通过房子这个低通滤波器时增益为 1。因此，平均的输出信号（即室内平均温度）也是华氏 60F：相对参考温度华氏 50F 的稳恒部分，华氏 10F 是相同的。

室内温度的华氏 10F 峰谷-峰顶变化是围绕华氏 60F 变化的。因此，室内温度的变化范围是华氏 55F 到华氏 65F。在室内，当我并不常跑步，或者说不产生太多热量时，我觉得 68F（20℃）的温度让我感到舒适。正如这个热流的电路模型预言的，当我住在那个房子里的时候，日夜都只需要穿一件毛衣。（关于更多 RC 类比在建筑中的应用，见参考文献 [13]。）

题 2.20 什么时间房间里最冷？根据增益的一般表达式，1/(1+jwτ)，开普敦的房子在一天中什么时间是最冷的？假定室外是半夜最冷。
## 记忆时间

内容提要：本书阐述了求解微积分的技巧，详细讲解了微积分基础、极限、连续、微分、导数的应用、积分、无穷级数、泰勒级数与幂级数等内容，旨在教会读者如何思考问题从而找到解题所需的知识点，着重训练大家自己解答问题的能力。

英文出版时间：2007 年；中文修订版出版时间：2016 年

Adrian Banner

## 卡片

### 0101. 主题卡 ——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡 —— 闭区间和开区间

信息源自「2019027The-Calculus-Lifesaver0101.md」

In the rest of this book, our functions will always have codomain R, and the domain will always be as much of R as possible (unless stated otherwise). So we'll often be dealing with subsets of the real line, especially connected intervals such as { x : 2 ≤ x < 5 }. It's a bit of a pain to write out the full set notation like this, but it sure beats having to say "all the numbers between 2 and 5, including 2 but not 5." We can do even better using interval notation.

We'll write [a, b] to mean the set of all numbers between a and b, including a and b themselves. So [a, b] means the set of all x such that a ≤ x ≤ b. For example, [2, 5] is the set of all real numbers between 2 and 5, including 2 and 5. (It's not just the set consisting of 2, 3, 4, and 5: don't forget that there are loads of fractions and irrational numbers between 2 and 5, such as 5/2, √ 7, and π.) An interval such as [a, b] is called closed.

If you don't want the endpoints, change the square brackets to parentheses. In particular, (a, b) is the set of all numbers between a and b, not including a or b. So if x is in the interval (a, b), we know that a < x < b. The set (2, 5) includes all real numbers between 2 and 5, but not 2 or 5. An interval of the form (a, b) is called open.

You can mix and match: [a, b) consists of all numbers between a and b, including a but not b. And (a, b] includes b but not a. These intervals are closed at one end and open at the other. Sometimes such intervals are called half-open. An example is the set { x : 2 ≤ x < 5 } from above, which can also be written as [2, 5).

There's also the useful notation (a, ∞) for all the numbers greater than a not including a; [a, ∞) is the same thing but with a included. There are three other possibilities which involve −∞; all in all, the situation looks like this: 

我们写 [a, b] 是指从 a 到 b 端点间的所有实数，包括 a 和 b。所以 [a，b] 指的是所有使得 a≤x≤b 成立的 x 的集合。

例如，[2, 5] 是所有介于 2 和 5 之间（包括 2 和 5）的实数的集合。（它不仅仅包括 2、3、4 和 5，不要忘记还有一大堆处于 2 和 5 之间的分数和无理数，比如 5/2、和 π。）像 [a, b] 这种形式表示的区间我们称作闭区间。

如果你不想包括端点，把方括号变为圆括弧就行了。所以 (a, b) 指的是介于 a 和 b 之间、但不包括 a 和 b 的所有实数的集合。这样，如果 x 在区间 (a, b) 中，我们就知道 a<x<b。集合 (2，5) 表示介于 2 和 5 之间、但不包括 2 和 5 的所有实数。像 (a, b) 这种形式表示的区间我们称作开区间。

2『闭区间和开区间，做一张术语卡片。（2021-06-16）』

你也可以混和匹配：[a, b) 指的是介于 a 和 b 之间、包括 a 但不包括 b 的所有实数的集合；(a, b] 包括 b，但不包括 a。这些区间在一个端点处是闭的，而在另一个端点处是开的。有时候，像这样的区间我们称作半开区间。上述的 `{x:2≤x<5}` 就是一个例子，也可以写成 [2，5)。还有一个有用的记号就是 (a, ∞)，它是指大于 a 但不包括 a 的所有数；[a, ∞) 也一样，只是它包括 a。还有 3 个涉及 ∞ 的可能性。总而言之，情况如下。

### 0202. 术语卡 ——

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 数据信息卡 ——3 种常见去定义域的条件

信息源自「2019027The-Calculus-Lifesaver0101.md」

Sometimes the deﬁnition of a function will include the domain. (This was the case, for example, with our function g from Section 1.1 above.) Most of the time, however, the domain is not provided. The basic convention is that the domain consists of as much of the set of real numbers as possible. For example, if k(x) = √ x, the domain can't be all of R, since you can't take the square root of a negative number. The domain must be [0, ∞), which is just the set of all numbers greater than or equal to 0.

OK, so square roots of negative numbers are bad. What else can cause a screw-up? Here's a list of the three most common possibilities:

1 The denominator of a fraction can't be zero.

2 You can't take the square root (or fourth root, sixth root, and so on) of a negative number.

3 You can't take the logarithm of a negative number or of 0. (Remember logs? If not, see Chapter 9)

2『上面的 3 种常见去定义域的条件，做一张信息数据卡片。（2021-06-18）』

You might recall that tan(90°) is also a problem, but this is really a special case of the ﬁrst item above. You see,

$$tan(90) = \frac{sin(90)}{cons(90)} = 1/0$$

有时候，函数的定义中包括了定义域。（确实如此，比如 1.1 节中的函数 g）然而，大多数情况下，定义域是没有给出的。按照惯例，定义域包括尽可能多的实数集合。例如 k(x)=√x，其定义域就不可能是 R 中的所有实数，因为不可能得到一个负数的平方根。其定义域一定是 [0，∞)，就是大于或等于 0 的所有实数的集合。

好了，我们知道取负数的平方根会出问题。那么，还有什么会把问题搞糟呢？以下是 3 种最常见的情况。

1、分数的分母不能是零。

2、不能取一个负数的平方根（或四次根，六次根，等等）。

3、不能取一个负数或零的对数。(还记得对数函数吗？如果忘了，就请看看第 9 章！）

或许你还记得 tan(90°) 也是一个问题，但这实际上是上述第一项的特例。你看：

$$tan(90) = \frac{sin(90)}{cons(90)} = 1/0$$

所以，tan(90°) 是无定义的，实际上是因为其隐藏的分母为零。

### 0601. 任意卡 —— 如何判断一个图形是否是函数图像

信息源自「2019027The-Calculus-Lifesaver0101.md」

You can draw any ﬁgure you like on a coordinate plane, but the result may not be the graph of a function. So what's special about the graph of a function? What is the graph of a function f, anyway? Well, it's the collection of all points with coordinates (x, f(x)), where x is in the domain of f. Here's another way of looking at this: start with some number x. If x is in the (a, b) domain, you plot the point (x, f(x)), which of course [a, b] is at a height of f(x) units above the point x on the x-axis. If x isn't in the domain, you don't plot (a, b] anything. Now repeat for every real number x to build [a, b) up the graph.

Here's the key idea: you can't have two points with the same x-coordinate. In other words, no two points on the graph can lie on the same vertical line. Otherwise, how would you know which of the two or more heights above the point x on the x-axis corresponds to the value of f(x)? So, this leads us to the vertical line test: 

if you have some graph and you want to know whether it's the graph of a function, see whether any vertical line intersects the graph more than once. If so, it's not the graph of a function; but if no vertical line intersects the graph more than once, you are indeed dealing with the graph of a function. For example, the circle of radius x units centered at the origin has a graph like this:

你可以在坐标平面上画任何你想画的图形，但结果可能不是一个函数的图像。所以，函数的图像有什么特别之处呢？或者说，什么是函数 f 的图像呢？

它是所有坐标为 (x, f(x)) 的点的集合，其中，x 在 f 的定义域中。还有另外一种方式来看待它：我们以某个实数 x 开始。如果 x 在定义域中，你就画点 (x, f(x))，它自然是，在 x 轴上的点 x 的正上方，高度为 f(x)。如果 x 没有在定义域中，你不能画任何点。现在，对于每一个实数 x，我们重复这个过程，从而构造出函数的图像。

这里有个重要思想：你不可能有两个点有相同的 x 坐标。换句话说，在图像上没有两个点会落在相对于 x 轴的同一条垂线上。要不然，你又将如何知道在点 x 上方的两个或多个高度的点中，哪一个是对应于 f(x) 的值呢？

这样，就有了垂线检验：如果你有某个图像并且想知道它是否是函数的图像，就来看看是否任何的垂线和图像相交多于一次。如果是这样的话，那它就不是函数的图像；反之，如果没有一条垂线和图像相交多于一次，那么你的确是在处理函数的图像。

2『判断一个图形是否是函数图像，用「垂线检验」。做一张任意卡片。（2021-06-16）』—— 已完成

## 译者序

对于大多数学生来说，微积分或许是他们曾经上过的倍感迷茫且最受挫折的一门课程了。而本书，不仅让学生们能有效地学习微积分，更重要的是提供了战胜微积分的必备工具。本书源于风靡美国普林斯顿大学的 Adrian Banner 的微积分复习课程。他激励了一些考试前想获得优秀但考试结果却平平的学生。

对于任何单变量微积分的课程，本书既可以作为教科书，也可以用作学习指南，对于全英文授课的教师来说更是一个得力助手。作者 Adrian Banner 是美国普林斯顿大学的著名数学教授并担任新技术研究中心主任。Adrian Banner 教授的授课风格是非正式的、有吸引力并完全不强求的，甚至在不失其详尽性的基础上又增添了许多娱乐性，而且他不会跳过讨论一个问题的任何步骤。

作者独创的「内心独白」方式 —— 即问题求解过程中学生们应遵循的思考过程 —— 为我们提供了不可或缺的推理过程以及求解方案。本书的重点在于创建问题求解的技巧。其中涉及的例题从简单到复杂并对微积分理论进行了深入探讨。读者会在非正式的对话语境中体会微积分的无穷魅力。

这样的一本经典著作将易用性与可读性以及内容的深度与数学的严谨完美地结合在一起。对于每一个想要掌握微积分的学生来说，本书都是极好的资源。当然，非数学专业的学生也将大大受益。在翻译本书的过程中，译者虽然尽最大努力尊重原文，并尽可能避免直译产生的歧义，但是由于才疏学浅，难免存在翻译不当之处，敬请广大读者批评指正，以便再版时更正。

杨爽

于首都经济贸易大学华侨学院信管系

## Welcome

This book is designed to help you learn the major concepts of single-variable calculus, while also concentrating on problem-solving techniques. Whether this is your ﬁrst exposure to calculus, or you are studying for a test, or you've already taken calculus and want to refresh your memory, I hope that this book will be a useful resource.

The inspiration for this book came from my students at Princeton University. Over the past few years, they have found early drafts to be helpful as a study guide in conjunction with lectures, review sessions and their textbook. Here are some of the questions that they've asked along the way, which you might also be inclined to ask:

1 Why is this book so long? I assume that you, the reader, are motivated to the extent that you'd like to master the subject. Not wanting to get by with the bare minimum, you're prepared to put in some time and eﬀort reading — and understanding — these detailed explanations.

2 What do I need to know before I start reading? You need to know some basic algebra and how to solve simple equations. Most of the precalculus you need is covered in the ﬁrst two chapters.

3 Help! The ﬁnal is in one week, and I don't know anything! Where do I start? The next three pages describe how to use this book to study for an exam.

4 Where are all the worked solutions to examples? All I see is lots of words with a few equations. Looking at a worked solution doesn't tell you how to think of it in the ﬁrst place. So, I usually try to give a sort of 'inner monologue' — what should be going through your head as you try to solve the problem. You end up with all the pieces of the solution, but you still need to write it up properly. My advice is to read the solution, then come back later and try to work it out again by yourself.

5 Where are the proofs of the theorems? Most of the theorems in this book are justiﬁed in some way. More formal proofs can be found in Appendix A.

6 The topics are out of order! What do I do? There's no standard order for learning calculus. The order I have chosen works, but you might have to search the table of contents to ﬁnd the topics you need and ignore the rest for now. I may also have missed out some topics too — why not try emailing me at adrian@calclifesaver.com and you never know, I just might write an extra section or chapter for you (and for the next edition, if there is one!).

7 Some of the methods you use are diﬀerent from the methods I learned. Who is right — my instructor or you? Hopefully we're both right! If in doubt, ask your instructor what's acceptable.

8 Where's all the calculus history and fun facts in the margins? Look, there's a little bit of history in this book, but let's not get too distracted here. After you get this stuﬀ down, read a book on the history of calculus. It's interesting stuﬀ, and deserves more attention than a couple of sentences here and there.

9 Could my school use this book as a textbook? Paired with a good collection of exercises, this book could function as a textbook, as well as being a study guide. Your instructor might also ﬁnd the book useful to help prepare lectures, particularly in regard to problem-solving techniques.

10 What's with these videos? You can ﬁnd videos of a year's supply of my review sessions, which reference a lot (but not all!) of the sections and examples from this book, at this website: www.calclifesaver.com.

本书旨在帮助你学习单变量微积分的主要概念，同时也致力于教会你求解问题的技巧。无论你是第一次接触微积分，还是为了准备一次测验，或是已经学过微积分但想再温习一遍，我都希望本书能够对你有所帮助。写作本书的灵感来自我在普林斯顿大学的学生们，他们在过去的几年里就发现，起初的笔记连同讲座、复习研讨以及教材作为学习指南是很有帮助的。以下是他们在学习过程中提出的一些你可能也想问的问题。

1、这本书为什么这么长？我认为你是真的想要掌握这门课程，而不只是想囫囵吞枣，一知半解，那你就要投入一些时间和精力，去阅读并理解这些详尽的阐述。

2、阅读之前，我需要知道些什么？你需要了解一些基本的代数知识，并且要知道如何求解简单的方程式。本书的前两章涵盖了你所需要的大部分的微积分预备知识。

3、啊！下周就要期末考试了，我还什么都不知道呢！从哪里开始啊。接下来的几页就会介绍如何使用本书来备考。

4、例题的求解过程在哪里？我所看到的只是大量的文字与少量的公式。首先，看一个求解过程并不能教会你应该怎样思考。所以，我通常试图给出一种「内心独白」，即当你尝试求解问题的时候，脑海中应该经历怎样的思考过程。最后，你想到了求解问题的所有知识点，但仍然需要用正确的方式把它们全部写出来。我的建议是先看懂并理解问题的求解方法，然后再返回来尝试自己解答。

5、定理的证明哪儿去了？本书中的大部分定理都以某种方式被验证了。在附录 A 中可以找到更多正式的证明过程。

6、主题没有次序！我该怎么办呢？学习微积分没有什么标准次序。我选择的顺序是有效的，但你可能还得通过搜索目录来查找你需要的主题，其余的可以先忽略。我也可能遗漏了一些主题。为什么不尝试给我发送电子邮件呢？地址是 adrian@calclifesaver.com，你一定想不到，我可能会为你写一个附加章节（也为下一版写, 如果有的话！）。

7、你使用的一些方法和我学到的不一样，到底谁的正确，我的任课老师的还是你的。希望我们都没错！如果还有疑问，就请教你的任课老师什么是对的吧。

8、页边空白处怎么没有微积分的历史和有趣的史实呢？本书中有一点微积分历史内容，但不在这里过多分散我们的注意力。如果你想记下这些历史内容，就请阅读一本关于微积分历史的书吧，那才更有趣，而且比零零散散的几句话更值得关注。

9、我们学校可以用这本书作为教材吗？这本书配有很好的习题集，可以作为一本教材，也可以用作一本学习指南。你的任课老师也会发现这本书很有助于备课，特别是在问题求解的技巧这一方面。

10、本书提及的这些录像是什么？在[网站](www.calclifesaver.com)上，你可以找到我的年度复习研讨录像，其中涉及了很多（但不是全部！）本书的章节和例题。

### 01. How to Use This Book to Study for an Exam

There's a good chance you have a test or exam coming up soon. I am sympathetic to your plight: you don't have time to read the whole book! There's a table on the next page that identiﬁes the main sections that will help you to review for the exam. Also, throughout the book, the following icons appear in the margin to allow you quickly to identify what's relevant:

1 A worked-out example begins on this line.

2 Here's something really important.

3 You should try this yourself.

4 Beware: this part of the text is mostly for interest. If time is limited, skip to the next section.

Also, some important formulas or theorems have boxes around them: learn these well.

如何使用这本书备考

如果你快要参加考试了，那么发挥本书效用的机会就来了。我很同情你的处境，因为你没有时间阅读整本书的内容！但是你不用担心，后面的那张表会标出本书的主要章节，来帮助你备考。此外，纵观整本书，下列图标会出现在书中页边空白处，让你快速识别什么是重要内容。

标识 1：例题求解过程始于此行。

标识 2：这里非常重要。

标识 3：你应当自己尝试解答本题。

标识 4：注意：这部分内容大多是为感兴趣的读者准备的。如果时间有限，就请跳到下一节。

1『这里的四个图标是啥样子的，详见原书。』

一些重要的公式或定理带有边框，一定要好好学啊。

### 02. Two all-purpose study tips

1 Write out your own summary of all the important points and formulas to memorize. Math isn't about memorization, but there are some key formulas and methods that you should have at your ﬁngertips. The act of making the summary is often enough to solidify your understanding. This is the main reason why I don't summarize the important points at the end of a chapter: it's much more valuable if you do it yourself.

2 Try to get your hands on similar exams — maybe your school makes previous years' ﬁnals available, for example — and take these exams under proper conditions. That means no breaks, no food, no books, no phone calls, no emails, no messaging, and so on. Then see if you can get a solution key and grade it, or ask someone (nicely!) to grade it for you.

You'll be on your way to that A if you do both of these things.

Key sections for exam review (by topic)

两个通用的学习小贴士

把你自己总结的所有重要的知识点和公式都写出来，以便记忆。虽说数学不是死记硬背，但也有一些关键的公式和方法，最好是你能自己写得出来。好记性不如烂笔头嘛！通常来说，做总结足以巩固和加强你对所学知识的理解。这就是为什么我没有在每一章的结尾部分作要点总结的主要原因。如果你自己去做，那将会更有价值。

尝试自己做一些类似的考试题，比如你们学校以前学期的期末试题，并在恰当的条件下进行测验。这将意味着遵守不间断，不吃饭，不看书，不打手机，不发电子邮件，不发信息等诸如此类的考试规则等等。完成之后，再看看你是否可以得到一套标准答案来评阅试卷，如果能请人帮你评阅会更好。
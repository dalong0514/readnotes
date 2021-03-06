英文出版时间：2007 年

中文修订版出版时间：2016 年

Adrian Banner

内容提要：本书阐述了求解微积分的技巧，详细讲解了微积分基础、极限、连续、微分、导数的应用、积分、无穷级数、泰勒级数与幂级数等内容，旨在教会读者如何思考问题从而找到解题所需的知识点，着重训练大家自己解答问题的能力。

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

### How to Use This Book to Study for an Exam

There's a good chance you have a test or exam coming up soon. I am sympathetic to your plight: you don't have time to read the whole book! There's a table on the next page that identiﬁes the main sections that will help you to review for the exam. Also, throughout the book, the following icons appear in the margin to allow you quickly to identify what's relevant:

• A worked-out example begins on this line.

• Here's something really important.

• You should try this yourself.

• Beware: this part of the text is mostly for interest. If time is limited, skip to the next section.

Also, some important formulas or theorems have boxes around them: learn these well.

如何使用这本书备考

如果你快要参加考试了，那么发挥本书效用的机会就来了。我很同情你的处境，因为你没有时间阅读整本书的内容！但是你不用担心，后面的那张表会标出本书的主要章节，来帮助你备考。此外，纵观整本书，下列图标会出现在书中页边空白处，让你快速识别什么是重要内容。

标识 1：例题求解过程始于此行。

标识 2：这里非常重要。

标识 3：你应当自己尝试解答本题。

标识 4：注意：这部分内容大多是为感兴趣的读者准备的。如果时间有限，就请跳到下一节。

1『这里的四个图标是啥样子的，详见原书。』

一些重要的公式或定理带有边框，一定要好好学啊。

### Two all-purpose study tips

• Write out your own summary of all the important points and formulas to memorize. Math isn't about memorization, but there are some key formulas and methods that you should have at your ﬁngertips. The act of making the summary is often enough to solidify your understanding. This is the main reason why I don't summarize the important points at the end of a chapter: it's much more valuable if you do it yourself.

• Try to get your hands on similar exams — maybe your school makes previous years' ﬁnals available, for example — and take these exams under proper conditions. That means no breaks, no food, no books, no phone calls, no emails, no messaging, and so on. Then see if you can get a solution key and grade it, or ask someone (nicely!) to grade it for you.

You'll be on your way to that A if you do both of these things.

Key sections for exam review (by topic)

两个通用的学习小贴士

把你自己总结的所有重要的知识点和公式都写出来，以便记忆。虽说数学不是死记硬背，但也有一些关键的公式和方法，最好是你能自己写得出来。好记性不如烂笔头嘛！通常来说，做总结足以巩固和加强你对所学知识的理解。这就是为什么我没有在每一章的结尾部分作要点总结的主要原因。如果你自己去做，那将会更有价值。

尝试自己做一些类似的考试题，比如你们学校以前学期的期末试题，并在恰当的条件下进行测验。这将意味着遵守不间断，不吃饭，不看书，不打手机，不发电子邮件，不发信息等诸如此类的考试规则等等。完成之后，再看看你是否可以得到一套标准答案来评阅试卷，如果能请人帮你评阅会更好。

## 致谢

感谢所有在我写作本书过程中给予我支持和帮助的人。我的学生一直都是在教育及娱乐方面鼓励并支持我的源泉，他们的意见使我受益匪浅。特别感谢我的编辑 Vickie Kearn、制作编辑 Linny Schenck 和设计师 Lorraine Doneker，感谢他们对我的所有帮助和支持，还要感谢 Gerald Folland，他的很多真知灼见对本书的改善有很大的贡献。此外，感谢 Ed Nelson、Maria Klawe、Christine Miranda、Lior Braunstein、Emily Sands、Jamaal Clue、Alison Ralph、Marcher Thompson、Ioannis Avramides、Kristen Molloy、Dave Uppal、Nwanneka Onvekwusi、Ellen Zuckerman、Charles MacCluer和 Gary Slezak，本书中的很多修正都得益于他们的意见和建议。

感谢下列普林斯顿大学数学系的教员和工作人员对我的大力支持：Eli Stein、Simon Kochen、Matthew Ferszt 和 Cott Kenny。我也要感谢我在 INTECH 的同事们给与的支持，特别是 Bob Fernholz、Camm Maguire、Marie D'Albero和 Vassilios Papathanakos，他们提出了一些优秀并且及时的建议。我还要感谢我高二、高三的数学老师 —— William Pender，他绝对是世界上最好的微积分老师。这本书中很多的方法都是从他的教学中获得的启发。我希望他能原谅我曲线不画箭头，所有的坐标轴上没有标注，在每一个 +C 后都忽视写「对于任意一个常数 C」。

我的朋友和家人都给了我无私的支持，尤其是我的父母 Freda 和 Michael，姐姐 Carly, 祖母 Rena，还有姻亲 Marianna 和 Michael。最后，我要特别感谢我的妻子 Amy 在我写书过程中对我的帮助和理解，她总是陪伴在我身边(感谢她为我画的「爬山者」！)。

## 目录

译者序

前言

如何使用这本书备考

两个通用的学习小贴士

考试复习的重要章节(按主题划分)

致谢

### 第1章　函数、图像和直线

1.1　函数

1.2　反函数

1.3　函数的复合

1.4　奇函数和偶函数

1.5　线性函数的图像

1.6　常见函数及其图像

### 第2章　三角学回顾

2.1　基本知识

2.2　三角函数定义域的扩展

2.3　三角函数的图像

2.4　三角恒等式

### 第3章　极限导论

3.1　极限：基本思想

3.2　左极限与右极限

3.3　何时不存在极限}

3.4　在∞和-∞处的极限

3.5　关于渐近线的两个常见错误认知

3.6　三明治定理

3.7　极限的基本类型小结

### 第4章　如何求解涉及多项式的极限问题

4.1　包含当x → a时的有理函数的极限

4.2　当x → a时的涉及平方根的极限

4.3　当x → ∞时涉及的有理函数的极限

4.4　当x → ∞时的多项式型函数的极限

4.5　当x → ∞时的有理函数的极限

4.6　包含绝对值的极限

### 第5章　连续性和可导性

5.1　连续性

5.2　可导性

### 第6章　如何求解微分问题

6.1　使用定义求导

6.2　求导(好方法)

6.3　求切线方程

6.4　速度和加速度

6.5　导数伪装的极限

6.6　分段函数的导数

6.7　直接画出导函数的图像

### 第7章　三角函数的极限和导数

7.1　涉及三角函数的极限

7.2　涉及三角函数的导数

### 第8章　隐函数求导和相关变化率

8.1　隐函数求导

8.2　相关变化率

### 第9章　指数函数和对数函数

9.1　基础知识

9.2　e 的定义

9.3　对数函数和指数函数求导

9.4　如何求解涉及指数函数和对数函数的极限

9.5　对数函数求导

9.6　指数的增长和衰退

9.7　双曲函数

### 第10章　反函数和反三角函数

10.1　导数和反函数

10.2　反三角函数

10.3　反双曲函数

### 第11章　导数和图像

11.1　函数的极值问题

11.2　罗尔定理

11.3　中值定理

11.4　二次导数及图像

11.5　对于导数为零点的分类

### 第12章　如何绘制函数图像

12.1　怎样建立符号表格

12.2　绘制函数图像的完全方法

12.3　例题

### 第13章　最优化和线性化

13.1　最优化问题

13.2　线性化

13.3　牛顿方法

### 第14章　洛必达法则及极限问题综述

14.1　洛必达法则

14.2　关于极限的总结

### 第15章　积分

15.1　求和符号

15.2　位移和面积

### 第16章　定积分

16.1　基本思想

16.2　定积分的定义

16.3　定积分的特性

16.4　求面积

16.5　估算积分

16.6　积分的平均值和中值定理

16.7　不可积的函数

### 第17章　微积分基本定理

17.1　以其他函数为积分的函数

17.2　微积分的第一基本定理

17.3　微积分的第二基本定理

17.4　不定积分

17.5　怎样解决问题：微积分第一基本定理

17.6　怎样解决问题：微积分第二基本定理

17.7　技术上的观点

17.8　微积分第一基本定理的证明

### 第18章　积分的方法：第一部分

18.1　替代法

18.2　分部积分法

18.3　部分分式

### 第19章　积分的方法：第二部分

19.1　应用三角函数公式的积分

19.2　关于三角函数的幂的积分

19.3　关于三角换元法的积分

19.4　积分技巧综述

### 第20章　反常积分：基本概念

20.1　收敛和发散

20.2　关于无穷区间的积分

20.3　比较判别法(理论)

20.4　极限比较判别法(理论)

20.5　P 判别法(理论)

20.6　绝对收敛判别法

### 第21章　反常积分：如何解题

21.1　如何开始

21.2　积分判别法总结

21.3　∞和-∞附近的常见函数

21.4　常见函数在0附近的情形

21.5　如何应对不在0或∞处的瑕点}

### 第22章　数列和级数：基本概念

22.1　数列的收敛和发散

22.2　级数的收敛与发散

22.3　第n项判别法(理论)

22.4　无穷级数和反常积分的性质

22.5　级数的新判别法

### 第23章　如何求解级数问题

23.1　如何求几何级数的值

23.2　如何应用第n项判别法

23.3　如何应用比式判别法

23.4　如何应用根式判别法

23.5　如何应用积分判别法

23.6　如何应用比较判别法、极限比较判别法和p判别法

23.7　如何应对含负项的级数

### 第24章　泰勒多项式、泰勒级数和幂级数导论

24.1　近似值和泰勒多项式

24.2　幂级数和泰勒级数

24.3　一个重要极限

### 第25章　如何求解估算问题

25.1　泰勒多项式与泰勒级数总结

25.2　求泰勒多项式与泰勒级数

25.3　用误差项估算问题

25.4　误差估算的另一种方法

### 第26章　泰勒级数和幂级数：如何解题

26.1　幂级数的收敛性

26.2　由旧泰勒级数求新泰勒级数

26.3　利用幂级数和泰勒级数求导

26.4　利用麦克劳林级数求极限

### 第27章　参数方程和极坐标

27.1　参数方程

27.2　极坐标

### 第28章　复数

28.1　基础

28.2　复平面

28.3　复数的高次幂

28.4　解 zn = w

28.5　解 ez = w

28.7　欧拉等式和幂级数

### 第29章　体积、弧长和表面积

29.1　旋转体的体积

29.2　一般固体体积

29.3　弧长

29.4　旋转体的表面积

### 第30章　微分方程

30.1　微分方程导论

30.2　可分离变量的一阶微分方程

30.3　一阶线性方程

30.4　常系数微分方程

30.5　微分方程建模

附录A　极限及其证明

A.1　极限的正式定义

A.2　由原极限产生新极限

A.3　极限的其他情形

A.4　连续与极限

A.5　重返指数函数和对数函数

A.6　微分与极限

A.7　泰勒近似定理的证明

附录B　估算积分

B.1　使用条纹估算积分

B.2　梯形法则

B.3　辛普森法则

B.4　近似的误差
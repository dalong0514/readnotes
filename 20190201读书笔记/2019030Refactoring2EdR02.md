# 2019030Refactoring2EdR02

## 记忆时间

### 0401. Building Tests Topics

Refactoring is a valuable tool, but it can’t come alone. To do refactoring properly, I need Tutorialsa solid suite of tests to spot my inevitable mistakes. Even with automated refactoring tools, many of my refactorings will still need checking via a test suite.

I don’t find this to be a disadvantage. Even without refactoring, writing good tests increases my effectiveness as a programmer. This was a surprise for me and is counterintuitive for most programmers—so it’s worth explaining why.

重构是很有价值的工具，但只有重构还不行。要正确地进行重构，前提是得有一套稳固的测试集合，以帮我发现难以避免的疏漏。即便有工具可以帮我自动完成一些重构，很多重构手法依然需要通过测试集合来保障。我并不把这视为缺点。我发现，编写优良的测试程序，可以极大提高我的编程速度，即使不进行重构也一样如此。这让我很吃惊，也违反许多程序员的直觉，所以我有必要解释一下这个现象。

2『测试加快开发速度。做一张反常识卡片。』——已完成

#### 4.1 The Value of Sefl-Testing Code

If you look at how most programmers spend their time, you’ll find that writing code is Sign actually Out quite a small fraction. Some time is spent figuring out what ought to be going on, some time is spent designing, but most time is spent debugging. I’m sure every reader can remember long hours of debugging—often, well into the night. Every programmer can tell a story of a bug that took a whole day (or more) to find. Fixing the bug is usually pretty quick, but finding it is a nightmare. And then, when you do fix a bug, there’s always a chance that another one will appear and that you might not even notice it till much later. And you’ll spend ages finding that bug.

如果你认真观察大多数程序员如何分配他们的时间，就会发现，他们编写代码的时间仅占所有时间中很少的一部分。有些时间用来决定下一步干什么，有些时间花在设计上，但是，花费在调试上的时间是最多的。我敢肯定，每一位读者一定都记得自己花数小时调试代码的经历 —— 而且常常是通宵达旦。每个程序员都能讲出一个为了修复一个 bug 花费了一整天（甚至更长时间）的故事。修复 bug 通常是比较快的，但找出 bug 所在却是一场噩梦。当修复一个 bug 时，常常会引起另一个 bug，却在很久之后才会注意到它。那时，你又要花上大把时间去定位问题。

The event that started me on the road to self­testing code was a talk at OOPSLA in 1992. Someone (I think it was “Bedarra” Dave Thomas) said offhandedly, “Classes should contain their own tests.” So I decided to incorporate tests into the code base together with the production code. As I was also doing iterative development, I tried adding tests as I completed each iteration. The project on which I was working at that time was quite small, so we put out iterations every week or so. Running the tests became fairly straightforward—but although it was easy, it was still pretty boring. This was because every test produced output to the console that I had to check. Now I’m a pretty lazy person and am prepared to work quite hard in order to avoid work. I realized that, instead of looking at the screen to see if it printed out some information from the model, I could get the computer to make that test. All I had to do was put the output I expected in the test code and do a comparison. Now I could run the tests and they would just print “OK” to the screen if all was well. The software was now selftesting.

我走上「自测试代码」这条路，源于 1992 年 OOPSLA 大会上的一个演讲。有个人（我记得好像是 Bedarra 公司的 DaveThomas）提到：「类应该包含它们自己的测试代码。」这让我决定，将测试代码和产品代码一起放到代码库中。当时，我正在迭代方式开发一个软件，因此，我尝试在每个迭代结束后把测试代码加上。当时我的软件项目很小，我们每周进行一次迭代。所以，运行测试变得相当简单 — 尽管非常简单，但也非常枯燥。因为每个测试都把测试结果输出到控制台中，我必须逐一检查它们。我是一个很懒的人，所以总是在当下努力工作，以免日后有更多的活儿。我意识到，其实完全不必自己盯着屏幕检验测试输出的信息是否正确，而是让计算机来帮我做检查。我需要做的就是把我所期望的输出放到测试代码中，然后做一个对比就行了。于是，我只要运行所有测试用例，假如一切都没问题，屏幕上就只出现一个「OK」。现在我的代码都能够「自测试」了。

Make sure all tests are fully automatic and that they check their own results. 确保所有测试都完全自动化，让它们检查自己的测试结果。

2『做一张金句卡片。』——已完成

Now it was easy to run tests—as easy as compiling. So I started to run tests every time I compiled. Soon, I began to notice my productivity had shot upward. I realized that I wasn’t spending so much time debugging. If I added a bug that was caught by a previous test, it would show up as soon as I ran that test. The test had worked before, so I would know that the bug was in the work I had done since I last tested. And I ran the tests frequently—which means only a few minutes had elapsed. I thus knew that the source of the bug was the code I had just written. As it was a small amount of code that was still fresh in my mind, the bug was easy to find. Bugs that would have otherwise taken an hour or more to find now took a couple of minutes at most. Not only was my software self­testing, but by running the tests frequently I had a powerful bug detector.

从此，运行测试就像执行编译一样简单。于是，我每次编译时都会运行测试。不久之后，我注意到自己的开发效率大大提高。我意识到，这是因为我没有花太多时间去测试的缘故。如果我不小心引入一个可被现有测试捕捉到的 bug，那么只要运行测试，它就会向我报告这个 bug。由于代码原本是可以正常运行的，所以我知道这个 bug 必定是在前一次运行测试后修改代码引入的。由于我频繁地运行测试，每次测试都在不久之前，因此我知道 bug 的源头就是我刚刚写下的代码。因为代码量很少，我对它也记忆犹新，所以就能轻松找出 bug。从前需要一小时甚至更多时间才能找到的 bug，现在最多只要几分钟就找到了。之所以能够拥有如此强大的 bug 侦测能力，不仅仅是因为我的代码能够自测试，也得益于我频繁地运行它们。

As I noticed this, I became more aggressive about doing the tests. Instead of waiting for the end of an increment, I would add the tests immediately after writing a bit of function. Every day I would add a couple of new features and the tests to test them. I hardly ever spent more than a few minutes hunting for a regression bug.

注意到这一点后，我对测试的积极性更高了。我不再等待每次迭代结尾时再增加测试，而是只要写好一点功能，就立即添加它们。每天我都会添加一些新功能，同时也添加相应的测试。这样，我很少花超过几分钟的时间来追查回归错误。

A suite of tests is a powerful bug detector that decapitates the time it takes to find bugs. 一套测试就是一个强大的 bug 侦测器，能够大大缩减查找 bug 所需的时间。

Tools for writing and organizing these tests have developed a great deal since my experiments. While flying from Switzerland to Atlanta for OOPSLA 1997, Kent Beck paired with Erich Gamma to port his unit testing framework from Smalltalk to Java. The resulting framework, called JUnit, has been enormously influential for program testing, inspiring a huge variety of similar tools [mf­xunit] in lots of different languages.

从我最早的试验开始到现在为止，编写和组织自动化测试的工具已经有了长足的发展。1997 年，Kent Beck 从瑞士飞往亚特兰大去参加当年的 OOPSLA 会议，在飞机上他与 Erich Gamma 结对，把他为 Smalltalk 撰写的测试框架移植到了 Java 上。由此诞生的 JUnit 框架在测试领域影响力非凡，也在不同的编程语言中催生了很多类似的工具 [mfxunit]。

Admittedly, it is not so easy to persuade others to follow this route. Writing the tests means a lot of extra code to write. Unless you have actually experienced how it speeds programming, self­testing does not seem to make sense. This is not helped by the fact that many people have never learned to write tests or even to think about tests. When tests are manual, they are gut­wrenchingly boring. But when they are automatic, tests can actually be quite fun to write. In fact, one of the most useful times to write tests is before I start programming. When I need to add a feature, I begin by writing the test. This isn’t as backward as it sounds. By writing the test, I’m asking myself what needs to be done to add the function. Writing the test also concentrates me on the interface rather than the implementation (always a good thing). It also means I have a clear point at which I’m done codingwhen the test works.

我得承认，说服别人也这么做并不容易。编写测试程序，意味着要写很多额外的代码。除非你确实体会到这种方法是如何提升编程速度的，否则自测试似乎就没什么意义。很多人根本没学过如何编写测试程序，甚至根本没考虑过测试，这对于编写自测试也很不利。如果测试需要手动运行，那的确是令人烦闷。但是，如果测试可以自动运行，编写测试代码就会真的很有趣。

事实上，撰写测试代码的最好时机是在开始动手编码之前。当我需要添加特性时，我会先编写相应的测试代码。听起来离经叛道，其实不然。编写测试代码其实就是在问自己：为了添加这个功能，我需要实现些什么？编写测试代码还能帮我把注意力集中于接口而非实现（这永远是一件好事）。预先写好的测试代码也为我的工作安上一个明确的结束标志：一旦测试代码正常运行，工作就可以结束了。

Kent Beck baked this habit of writing the test first into a technique called Test­Driven Development (TDD) [mf­tdd]. The Test­Driven Development approach to programming relies on short cycles of writing a (failing) test, writing the code to make that test work, and refactoring to ensure the result is as clean as possible. This testcode­refactor cycle should occur many times per hour, and can be a very productive and calming way to write code. I’m not going to discuss it further here, but I do use and warmly recommend it.

Kent Beck 将这种先写测试的习惯提炼成一门技艺，叫测试驱动开发（Test-DrivenDevelopment，TDD）[mftdd]。测试驱动开发的编程方式依赖于下面这个短循环：先编写一个（失败的）测试，编写代码使测试通过，然后进行重构以保证代码整洁。这个「测试、编码、重构」的循环应该在每个小时内都完成很多次。这种良好的节奏感可使编程工作以更加高效、有条不紊的方式开展。我就不在这里再做更深入的介绍，但我自己确实经常使用，也非常建议你试一试。

That’s enough of the polemic. Although I believe everyone would benefit by writing selftesting code, it is not the point of this book. This book is about refactoring. Refactoring requires tests. If you want to refactor, you have to write tests. This chapter gives you a start in doing this for JavaScript. This is not a testing book, so I’m not going to go into much detail. I’ve found, however, that with testing a remarkably small amount of work can have surprisingly big benefits.

As with everything else in this book, I describe the testing approach using examples. When I develop code, I write the tests as I go. But sometimes, I need to refactor some code without tests—then I have to make the code self­testing before I begin.

大道理先放在一边。尽管我相信每个人都可以从编写自测试代码中收益，但这并不是本书的重点。本书谈的是重构，而重构需要测试。如果你想重构，就必须编写测试。本章会带你入门，教你如何在 JavaScript 中编写简单的测试，但它不是一本专门讲测试的书，所以我不想讲得太细。但我发现，少许测试往往就足以带来惊人的收益。和本书其他内容一样，我以示例来介绍测试手法。开发软件的时候，我一边写代码，一边写测试。但有时我也需要重构一些没有测试的代码。在重构之前，我得先改造这些代码，使其能够自测试才行。




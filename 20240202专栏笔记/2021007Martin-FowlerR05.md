## 记忆时间

## 目录

20210502UnitTest.md

20210502TestCoverage.md

## 20210502UnitTest.md

[UnitTest](https://martinfowler.com/bliki/UnitTest.html)

5 May 2014

Martin Fowler

[test categories](https://martinfowler.com/tags/test%20categories.html)

[extreme programming](https://martinfowler.com/tags/extreme%20programming.html)

Unit testing is often talked about in software development, and is a term that I've been familiar with during my whole time writing programs. Like most software development terminology, however, it's very ill-defined, and I see confusion can often occur when people think that it's more tightly defined than it actually is.

Although I'd done plenty of unit testing before, my definitive exposure was when I started working with Kent Beck and used the Xunit family of unit testing tools. (Indeed I sometimes think a good term for this style of testing might be "xunit testing.") Unit testing also became a signature activity of ExtremeProgramming (XP), and led quickly to TestDrivenDevelopment.

3『

[Xunit](https://martinfowler.com/bliki/Xunit.html)

[ExtremeProgramming](https://martinfowler.com/bliki/ExtremeProgramming.html)

[TestDrivenDevelopment](https://martinfowler.com/bliki/TestDrivenDevelopment.html)

』

There were definitional concerns about XP's use of unit testing right from the early days. I have a distinct memory of a discussion on a usenet discussion group where us XPers were berated by a testing expert for misusing the term "unit test." We asked him for his definition and he replied with something like "in the first morning of my training course I cover 24 different definitions of unit test."

Despite the variations, there are some common elements. Firstly there is a notion that unit tests are low-level, focusing on a small part of the software system. Secondly unit tests are usually written these days by the programmers themselves using their regular tools - the only difference being the use of some sort of unit testing framework [1]. Thirdly unit tests are expected to be significantly faster than other kinds of tests.

So there's some common elements, but there are also differences. One difference is what people consider to be a unit. Object-oriented design tends to treat a class as the unit, procedural or functional approaches might consider a single function as a unit. But really it's a situational thing — the team decides what makes sense to be a unit for the purposes of their understanding of the system and its testing. Although I start with the notion of the unit being a class, I often take a bunch of closely related classes and treat them as a single unit. Rarely I might take a subset of methods in a class as a unit. However you define it doesn't really matter.

1: I say "these days" because this is certainly something that has changed due to XP. In the turn-of-the-century debates, XPers were strongly criticized for this as the common view was that programmers should never test their own code. Some shops had specialized unit testers whose entire job would be to write unit tests for code written earlier by developers. The reasons for this included: people having a conceptual blindness to testing their own code, programmers not being good testers, and it was good to have a adversarial relationship between developers and testers. The XPer view was that programmers could learn to be effective testers, at least at the unit level, and that if you involved a separate group the feedback loop that tests gave you would be hopelessly slow. Xunit played an essential role here, it was designed specifically to minimize the friction for programmers writing tests.

### 01. Solitary or Sociable?

A more important distinction is whether the unit you're testing should be sociable or solitary [2]. Imagine you're testing an order class's price method. The price method needs to invoke some functions on the product and customer classes. If you like your unit tests to be solitary, you don't want to use the real product or customer classes here, because a fault in the customer class would cause the order class's tests to fail. Instead you use TestDoubles for the collaborators.

But not all unit testers use solitary unit tests. Indeed when xunit testing began in the 90's we made no attempt to go solitary unless communicating with the collaborators was awkward (such as a remote credit card verification system). We didn't find it difficult to track down the actual fault, even if it caused neighboring tests to fail. So we felt allowing our tests to be sociable didn't lead to problems in practice.

Indeed using sociable unit tests was one of the reasons we were criticized for our use of the term "unit testing". I think that the term "unit testing" is appropriate because these tests are tests of the behavior of a single unit. We write the tests assuming everything other than that unit is working correctly.

As xunit testing became more popular in the 2000's the notion of solitary tests came back, at least for some people. We saw the rise of Mock Objects and frameworks to support mocking. Two schools of xunit testing developed, which I call the classic and mockist styles. One of the differences between the two styles is that mockists insist upon solitary unit tests, while classicists prefer sociable tests. Today I know and respect xunit testers of both styles (personally I've stayed with classic style).

Even a classic tester like myself uses test doubles when there's an awkward collaboration. They are invaluable to remove non-determinism when talking to remote services. Indeed some classicist xunit testers also argue that any collaboration with external resources, such as a database or filesystem, should use doubles. Partly this is due to non-determinism risk, partly due to speed. While I think this is a useful guideline, I don't treat using doubles for external resources as an absolute rule. If talking to the resource is stable and fast enough for you then there's no reason not to do it in your unit tests.

3『
 
[Mocks Aren't Stubs](https://martinfowler.com/articles/mocksArentStubs.html) 

[Eradicating Non-Determinism in Tests](https://martinfowler.com/articles/nonDeterminism.html#RemoteServices)

』

2: Jay Fields came up with the terms "solitary" and "sociable".

2『已下载书籍 Jay Fields 的「2021076Working-Effectively-with-Unit-Tests」』

### 02. Speed

The common properties of unit tests — small scope, done by the programmer herself, and fast — mean that they can be run very frequently when programming. Indeed this is one of the key characteristics of SelfTestingCode. In this situation programmers run unit tests after any change to the code. I may run unit tests several times a minute, any time I have code that's worth compiling. I do this because should I accidentally break something, I want to know right away. If I've introduced the defect with my last change it's much easier for me to spot the bug because I don't have far to look.

When you run unit tests so frequently, you may not run all the unit tests. Usually you only need to run those tests that are operating over the part of the code you're currently working on. As usual, you trade off the depth of testing with how long it takes to run the test suite. I'll call this suite the compile suite, since it's what I run whenever I think of compiling — even in an interpreted language like Ruby.

If you are using Continuous Integration you should run a test suite as part of it. It's common for this suite, which I call the commit suite, to include all the unit tests. It may also include a few BroadStackTests. As a programmer you should run this commit suite several times a day, certainly before any shared commit to version control, but also at any other time you have the opportunity — when you take a break, or have to go to a meeting. The faster the commit suite is, the more often you can run it. [3]

Different people have different standards for the speed of unit tests and of their test suites. David Heinemeier Hansson is happy with a compile suite that takes a few seconds and a commit suite that takes a few minutes. Gary Bernhardt finds that unbearably slow, insisting on a compile suite of around 300ms and Dan Bodart doesn't want his commit suite to be more than ten seconds

I don't think there's an absolute answer here. Personally I don't notice a difference between a compile suite that's sub-second or a few seconds. I like Kent Beck's rule of thumb that the commit suite should run in no more than ten minutes. But the real point is that your test suites should run fast enough that you're not discouraged from running them frequently enough. And frequently enough is so that when they detect a bug there's a sufficiently small amount of work to look through that you can find it quickly.

3『

[SelfTestingCode](https://martinfowler.com/bliki/SelfTestingCode.html)

[BroadStackTest](https://martinfowler.com/bliki/BroadStackTest.html)

[Slow database test fallacy (DHH)](https://dhh.dk/2014/slow-database-test-fallacy.html)

[David Heinemeier Hansson (DHH)](https://dhh.dk/)

[Crazy fast build times (Or when 10 seconds starts to make you nervous) – Yesterday I was wrong](http://dan.bodar.com/2012/02/28/crazy-fast-build-times-or-when-10-seconds-starts-to-make-you-nervous/)

[Catalog](https://www.destroyallsoftware.com/screencasts/catalog)

』

3: If you have tests that are useful, but take longer than you want the commit suite to run, then you should build a DeploymentPipeline and put the slower tests in a later stage of the pipeline.

[DeploymentPipeline](https://martinfowler.com/bliki/DeploymentPipeline.html)

Revisions:

Updated on Oct 24 2014 to include a mention of Field's sociable/solitary vocabulary.

Updated on March 9 2017 to make the solitary/sociable terms the primary way of describing the distinction and removing the use of the term "collaborator isolation" (due to confusion with isolating test fixture changes from each other).

## 20210502TestCoverage.md

17 April 2012

Martin Fowler

[testing](https://martinfowler.com/tags/testing.html)

[metrics](https://martinfowler.com/tags/metrics.html)

From time to time I hear people asking what value of test coverage (also called code coverage) they should aim for, or stating their coverage levels with pride. Such statements miss the point. Test coverage is a useful tool for finding untested parts of a codebase. Test coverage is of little use as a numeric statement of how good your tests are.

Let's look at the second statement first. I've heard of places that may say things like "you can't go into production with less than 87% coverage". I've heard some people say that you should use things like TDD and must get 100% coverage. A wise man once said:

I expect a high level of coverage. Sometimes managers require one. There's a subtle difference.

—— Brian Marick

If you make a certain level of coverage a target, people will try to attain it. The trouble is that high coverage numbers are too easy to reach with low quality testing. At the most absurd level you have AssertionFreeTesting. But even without that you get lots of tests looking for things that rarely go wrong distracting you from testing the things that really matter.

[AssertionFreeTesting](https://martinfowler.com/bliki/AssertionFreeTesting.html)

Like most aspects of programming, testing requires thoughtfulness. TDD is a very useful, but certainly not sufficient, tool to help you get good tests. If you are testing thoughtfully and well, I would expect a coverage percentage in the upper 80s or 90s. I would be suspicious of anything like 100% — it would smell of someone writing tests to make the coverage numbers happy, but not thinking about what they are doing.

The reason, of course, why people focus on coverage numbers is because they want to know if they are testing enough. Certainly low coverage numbers, say below half, are a sign of trouble. But high numbers don't necessarily mean much, and lead to ignorance-promoting dashboards. Sufficiency of testing is much more complicated attribute than coverage can answer. I would say you are doing enough testing if the following is true:

1 You rarely get bugs that escape into production, and

2 You are rarely hesitant to change some code for fear it will cause production bugs.

Can you test too much? Sure you can. You are testing too much if you can remove tests while still having enough. But this is a difficult thing to sense. One sign you are testing too much is if your tests are slowing you down. If it seems like a simple change to code causes excessively long changes to tests, that's a sign that there's a problem with the tests. This may not be so much that you are testing too many things, but that you have duplication in your tests.

Some people think that you have too many tests if they take too long to run. I'm less convinced by this argument. You can always move slow tests to a later stage in your deployment pipeline, or even pull them out of the pipeline and run them periodically. Doing these things will slow down the feedback from those tests, but that's part of the trade-off of build times versus test confidence.

So what is the value of coverage analysis again? Well it helps you find which bits of your code aren't being tested. [1] It's worth running coverage tools every so often and looking at these bits of untested code. Do they worry you that they aren't being tested?

If a part of your test suite is weak in a way that coverage can detect, it's likely also weak in a way coverage can't detect.

—— Brian Marick

Further Reading: Brian Marick has an excellent article on the misuse of code coverage. And it's worth reading the pithy commentary of Testivus.

1: By "you" here I mean the people writing the tests. Coverage is of little value to management since you need a technical background to understand whether the tests are good or whether the uncovered code is a problem.

2『已下载「202105附件01How-to-Misuse-Code-Coverage」作为本专栏的附件。』

3『

[AssertionFreeTesting](https://martinfowler.com/bliki/AssertionFreeTesting.html)

AssertionFreeTesting

3 August 2004

Here's a story from a friend of a friend. I'm sure it must be true, at least somewhere.

A project got started to do a big system. It was outsourced to a big software/consultancy house — one I know you've heard of. They put in an impressive team for the bid, and naturally swapped them all out for a lot of junior people for the actual work. All standard procedure.

The twist is that the company made a big point of using heavy testing with JUnit. Every public method had to have JUnit tests. They proudly showed the client all the tests and the green bar. 

However there weren't any assertions in the JUnit tests. I don't know if they did code coverage analysis on this project, but of course you can do this and have 100% code coverage — which is one reason why you have to be careful on interpreting code coverage data.[1]

1: Although assertion-free testing is mostly a joke, it isn't entirely useless. As Carlos Villela reminded me, some faults do show up through code execution, eg null pointer exceptions.

』

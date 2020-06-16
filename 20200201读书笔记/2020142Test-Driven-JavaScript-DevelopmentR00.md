## 记忆时间

## 卡片

### 0101. 主题卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——TDD microcycle

There are only three steps in this microcycle: 1) Write a test that fails at the start (Red): First of all, simple test cases are written, which test the code yet to be implemented. At this step, the test will always fail (In the figure, it has been colored red).  2) Write just enough code to pass the test (Green): The developer then writes the code to pass the test. The code is written in the simplest manner and is just sufficient to pass the test. 3) Refactor the code (Refactor): Before implementing a new feature, developers refactor the old code, which just passed, for clarity and simplicity. This step improves the code quality. 

This microcycle provides rapid feedback to the developer. As soon as a change is made to the system, it is tested. If there is any error, it's detected as soon as possible and fixed. 

### 0202. 术语卡——Unit test

Unit test is a function or method, which invokes a unit of module in software and checks assumptions about the system that the developer has in mind. Unit test helps the developer test the logical functionality of any module. In other words, a unit is the testable piece of software. It can have more than one input and normally a single output. Sometimes, we treat a module of a system as a unit. 

Unit test is only relevant to developers who are closely working with the code. A unit test is only applicable to test a logical piece of a code. Illogical code would not be tested with the use of unit testing. For example, getting and setting values in text field will not be considered in logical code. 

### 0203. 术语卡——TDD and BDD

Behavior-driven development (BDD) is a term introduced by Dan North to address this shortcoming. The terminology used by BDD focuses on the behavioral aspect of the system. In this chapter, you are going to learn about Jasmine in detail and note that the differences in nomenclature of TDD and BDD. Deep down, TDD and BDD would serve the same purpose, but using the vocabulary of BDD gives you a better set of tests and documents your system in a better way. 

While TDD interface gives names such as suite(), test(), setup(), teardown(), suiteSetup(), suiteTearDown(), assert(), and so on. BDD offers describe(), context(), it(), beforeEach(), afterEach(), beforeAll(), afterAll(), expect(), and so on. A test suite in TDD is usually created using suite(),while BDD uses describe(); to create a unit test TDD uses test() and BDD uses it(). 

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。

#### 01. 基本信息

用一句话描述你对这个大牛的印象。

#### 02. 贡献及著作

### 0401. 金句卡——TDD is about how code should be written while Agile is about the whole development process

TDD is about how code should be written while Agile is about the whole development process, not just code and its testing. Agile does not tell you how to build the system. Agile methodology is a management process, which can use TDD as an integral part. Agile, when combined in practice with TDD, brings the best results. This combination minimizes risks, defects, cost, and results in a nearly zero-defect system.

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

## Preface

Initially, all processing used to happen on the server's side and simple output was the response to web browsers. Nowadays, there are so many JavaScript frameworks and libraries that help readers to create charts, animations, simulations, and so on. By the time a project finishes or reaches a stable state, so much JavaScript code has already been written that changing and maintaining it further is tedious. At this point comes the importance of automated testing, and more specifically, developing all that code in a test-driven environment. Test-driven development is a methodology that makes testing the central part of the design process—before writing code, developers decide upon the conditions that code must meet to pass a test. The end goal is to help the readers understand the importance and process of using TDD as a part of the development.

This book starts with the details of test-driven development, its importance, need, and benefits. Later, the book introduces popular tools and frameworks, such as YUI, Karma, QUnit, DalekJS, JsUnit, and so on, to utilize Jasmine, Mocha, and Karma for advanced concepts such as feature detection, server-side testing, and patterns. We are going to understand, write, run tests, and further debug our programs. The book concludes with best practices in JavaScript testing. By the end of the book, the readers will know why they should test, how to do it most efficiently, and will have a number of versatile tests (and methods to devise new tests) so they can get to work immediately.

Chapter 1, Overview of TDD, introduces the test-driven development, its life cycle, benefits, and myths.

Chapter 2, Testing Concepts, brings the TDD life cycle into action using Yahoo User Interface (YUI) Tests, and explains how unit testing can be done for JavaScript.

Chapter 3, Testing Tools, introduces JsUnit, QUnit, Karma, and DalekJS, which are some of the popular unit testing frameworks for JavaScript.

Chapter 4, Jasmine, introduces behavior-driven development and the Jasmine framework, its setup, usage, and customization, along with several features that a good unit testing framework should cover.

Chapter 5, JsTestDriver, showcases the JsTestDriver unit testing tool and its integration with IDE.

Chapter 6, Feature Detection, explores has.js and Modernizr JavaScript libraries for feature detection and explains why feature detection should have preference over browser detection.

Chapter 7, Observer Design Pattern, explains the observer pattern for JavaScript and its role in the test-driven development.

Chapter 8, Testing with Server-Side JS, covers server-side JavaScript unit testing using Node.js, Mocha, and Chai while using MongoDB as a database.

Chapter 9, Best Practices, lists best practices used to unit test JavaScript and also helps to make a good choice among popular unit testing frameworks and tools by explaining the features.

## 0101. Overview of TDD

In this chapter, you learned about what TDD is. You got to know about the life cycle of TDD and how it is called test-first development. Later on, you learned about the benefits and myths of TDD.  In the next chapter, you will learn the concepts of unit testing, and how to write unit tests and run them. 

### 1.2 Understanding test-driven development 

TDD, short for test-driven development, is a process for software development. Kent Beck, who is known for development of TDD, refers to this as "rediscovery." Someone asked a question (Why does Kent Beck refer to the "rediscovery" of test-driven development?) about this. Kent's answer to this question on Quora can be found at https://www.quora.com/Why-does-Kent-Beck-refer-to-therediscovery-of-test-driven-development. 

"The original description of TDD was in an ancient book about programming. It said you take the input tape, manually type in the output tape you expect, then program until the actual output tape matches the expected output. After I'd written the first xUnit framework in Smalltalk I remembered reading this and tried it out. That was the origin of TDD for me. When describing TDD to older programmers, I often hear, "Of course. How else could you program?" Therefore I refer to my role as "rediscovering" TDD." 

If you go and try to find references to TDD, you would even get few references from 1968. However It's not a new technique, though it did not get so much attention at that time. Recently, an interest in TDD has been growing, and as a result there are a number of tools on the Web. For example, Jasmine, Mocha, DalekJS, JsUnit, QUnit, and Karma are among these popular tools and frameworks. More specifically, test-driven JavaScript development is becoming popular these days. 

1『几大 web 端的测试框架：Jasmine, Mocha, DalekJS, JsUnit, QUnit, and Karma. 』

Test-driven development is a software development process, which enforces a developer to write a test before production code. A developer writes a test, expects a behavior, and writes code to make the test pass. It is needless to mention that the test will always fail at the start. You will learn more about the life cycle later in this chapter. 

1『 the test will always fail at the start. 测试驱动开发，是以失败的测试为起点的。』

#### 1.2.1 The need for testing 

To err is human. As a developer, it's not easy to find defects in our own code, and often we think that our code is perfect. But there is always a chance that a defect is present in the code. Every organization or individual wants to deliver the best software they can. This is one major reason that every software, every piece of code is well tested before its release. Testing helps to detect and correct defects. 

There are a number of reasons why testing is needed. They are as follows: 1) To check if the software is functioning as per the requirements. 2) There will not be just one device or one platform to run your software. 3) The end users sometimes perform an action as a programmer that you never expected, and these actions might result in defects. To catch these defects, we need testing.

1『这里的 defects 就当 bug 来理解。』

There was a study conducted by the National Institute of Standards and Technology (NIST) in 2002, which reported that software bugs cost the U.S. economy around \$60 billion annually. With better testing, more than one-third of the cost could be avoided. The earlier the defect is found, the cheaper it is to fix it. A defect found post release would cost 10-100 times more to fix than if it had already been detected and fixed pre-release. The report on the study performed by NIST can be found at http://www.nist.gov/ director/planning/upload/report02-3.pdf. 

2『已下载「report02-3」作为本书籍附件「2020011书籍附件」。』

If we draw a curve for the cost, it comes as an exponential. The following figure clearly shows that the cost increases as the project matures with time. Sometimes, it's not possible to fix a defect without making changes in the architecture. In those cases, the cost is sometimes so great that developing the software from scratch seems like a better option. 

#### 1.2.2 Types of testing 

Any product, website, or utility, should be very well tested before it is launched. There are a number of testing techniques used to test software. From a block of code to system integration testing, every kind of testing is performed for a zero-defect system. Test-driven development is more about unit testing. It helps to learn about defects in a system at a very early stage. You will learn more about unit tests and testing concepts in the next chapter. 

The following figure shows the cost of detecting and fixing defects in different testing types: 

1『 Implemention -> Unit Testing -> Integration Testing -> System Testing -> Post Release 』

As we can clearly see, if unit testing is performed, the cost of correcting a defect is close to correcting defects at the time of implementation. Since TDD enforces writing unit tests, the cost of the overall project is reduced significantly by reducing the number of defects after release. 

#### 1.2.3 The life cycle of TDD

The life cycle of TDD can be divided into several steps. Each time a change is to be made into the system, tests cases are written first and then some code to make the tests pass, and so on. Let's get a closer look at the life cycle. See the following figure: 

The different phases of the life cycle of TDD can be explained as follows: 

1. Write a test: After a set of requirements is captured, one requirement is picked and tests are written for that. Implementation of every new feature or every change begins with writing tests for it. The test can also be a modified version of an existing one. This is a major difference between TDD versus other techniques, where unit tests are written after the code is written. This makes the developer focus on the requirements before writing the code. This also makes it a test-first development approach. 

2. Run the test and see if the test fails: A new test should always require some code to be written to make it pass. This step validates that the new test should not pass without requiring new code. This also verifies whether the required feature already exists or not. This step helps the developer increase confidence that the unit test is testing the correct constraint, and passes only in the intended cases. 

3. Write minimal production code that passes: In this step, the developer writes just enough code to pass the test. The code written in this stage is not supposed to be perfect. Since the code will be improved and cleaned at a later stage, the code as of now is acceptable. At this point, the only purpose of the written code is to pass the test. 

4. Run all tests: Now, we run all the test cases at once. If every test passes, the programmer can be confident that the new code works as required and does not break any existing functionality or degrade the system anyhow. If any of the tests fail, the new code must be corrected to make the test pass. Usually, all our tests should be atomic and should not fail even if a new code is added, but that's not always the case. It may happen that someone else in the team added some code or some changes were made to the existing code. So, it's always a good practice to run all tests to make sure everything works fine as it should have. 

5. The cleanup code: At the end of development, there would be thousands of such test cases and code base that grows and can become complex if it is not cleaned up regularly. Refactoring is much needed. Duplicate code must be removed. Variables, functions, and so on should follow standards, and names should clearly represent their purpose and use. Code comments should be added for readability and documentation purpose. Removal of duplicate code applies to both production and test code. It is a must to ensure that refactoring does not break any existing features. 

6. Repeat: The preceding steps give a somewhat stable code in just one iteration, which works for some defined functionalities. The whole process is now repeated for another requirement. In case new tests fail, the developer can revert the changes or undo the operation performed. This gives a rapid feedback to the developer about the progress and problems in the system. 

1『第 5 步的 cleanup code 其实就是重构。』

#### 1.2.4 TDD microcycle

The TDD life cycle is also defined as Red-Green-Refactor, which is also called as the microcycle. This process can be illustrated as shown in the following figure: 

There are only three steps in this microcycle: 

1. Write a test that fails at the start (Red): First of all, simple test cases are written, which test the code yet to be implemented. At this step, the test will always fail (In the figure, it has been colored red). 

2. Write just enough code to pass the test (Green): The developer then writes the code to pass the test. The code is written in the simplest manner and is just sufficient to pass the test. 

3. Refactor the code (Refactor): Before implementing a new feature, developers refactor the old code, which just passed, for clarity and simplicity. This step improves the code quality. 

This microcycle provides rapid feedback to the developer. As soon as a change is made to the system, it is tested. If there is any error, it's detected as soon as possible and fixed. 

2『 TDD microcylce 做一张术语卡片。』——已完成

### 1.3 Agile and TDD 

When we talk about TDD, Agile is most often discussed. Sometimes, people have doubts about whether Agile can exist without TDD or not. Well, of course it can, though. Agile and some people would say that TDD is Agile at a bigger scale. Through TDD, both show similar characteristics, but they are different. Agile is a process where testing is done as soon as a component is developed. It's not necessary in Agile to write test cases first and then perform development. But in the case of TDD, a test is always written first, and then its corresponding minimal production code. 

TDD is about how code should be written while Agile is about the whole development process, not just code and its testing. Agile does not tell you how to build the system. Agile methodology is a management process, which can use TDD as an integral part. 

2『 TDD is about how code should be written while Agile is about the whole development process. 做一张金句卡片。』——已完成

Agile, when combined in practice with TDD, brings the best results. This combination minimizes risks, defects, cost, and results in a nearly zero-defect system.

### 1.4 Benefits of TDD and common myths 

Every methodology has its own benefits and myths. The following sections will analyze the key benefits and most common myths of TDD. 

#### 1.4.1 Benefits 

TDD has its own advantages over regular development approaches. There are a number of benefits, which help in making a decision of using TDD over the traditional approach. 

1. Automated testing: If you have seen a website code, you know that it's not easy to maintain and test all the scripts manually and keep them working. A tester may leave a few checks, but automated tests won't. Manual testing is error-prone and slow. 

2. Lower cost of overall development: With TDD, the number of debugs is significantly decreased. You develop some code, run tests; if you fail, redoing the development is significantly faster than debugging and fixing it. TDD aims at detecting defect and correcting them at an early stage, which costs much less than detecting and correcting at a later stage or post release. 

    Also, now debugging is much less frequent and a significant amount of time is saved. With the help of tools/test runners like Karma, JSTestDriver, and so on, running every JavaScript tests on browser is not needed, which saves significant time in validation and verification while the development goes on. 

3. Increased productivity: Apart from time and financial benefits, TDD helps to increase productivity since the developer becomes more focused and tends to write quality code that passes and fulfills the requirement. 

4. Clean, maintainable, and flexible code: Since tests are written first, production code is often very neat and simple. When a new piece of code is added, all the tests can be run at once to see if anything failed with the change. Since we try to keep our tests atomic, and our methods also address a single goal, the code automatically becomes clean. At the end of the application development, there will be thousands of test cases, which will guarantee that every piece of logic can be tested. 

    The same test cases also act as documentation for users who are new to the development of the system, since these tests act as an example of how the code works. 

5. Improved quality and reduced bugs: Complex codes invite bugs. when developers change anything in neat and simple code, they tend to leave fewer or no bugs at all. They tend to focus on the purpose and write code to fulfill the requirement. 

6. Keeps technical debt to minimum: This is one of the major benefits of TDD. Not writing unit tests and documentation is a big part, as this increases the technical debt for a software/project. Since TDD encourages you to write tests first, and if they are well written they act as documentation, you keep the technical debt for these to a minimum. 

As Wikipedia says, "A technical debt can be defined as tasks to be performed before a unit can be called complete. If the debt is not repaid, interest also adds up and makes it harder to make changes at a later stage". More about technical debt can be found at https://en.wikipedia.org/wiki/Technical_debt. 

#### 1.4.2 Myths
 
Along with the benefits, TDD has some myths as well. Let's check few of them: 

1. Complete code coverage: TDD forces the writing of tests first, developers write the minimum amount of code to pass the test, and almost 100% code coverage is achieved. But that does not guarantee that nothing has been missed and the code is bug free. Code coverage tools do not cover all the paths. There can be infinite possibilities in loops. Of course it's not possible and feasible to check all the paths, but a developer is supposed to take care of major and critical paths. 

    A developer is supposed to take care of business logic, flow, and process code most of the time. There is no need to test integration parts, setter-getter methods for properties, configurations, UI, and so on. Mocking and stubbing is to be used for integrations. 

2. No need of debugging the code: Though test-first development makes one think that debugging is not needed, but it's not always true. You need to know the state of the system when a test failed. That will help you to correct and further develop the code. 

3. No need for QA: TDD cannot always cover everything. QA plays a very important role in testing. UI defects, integration defects, are more likely to be caught by a QA. Even though developers are excellent, there are chances for errors. QA will try every kind of input and unexpected behavior that even a programmer would not cover with test cases. They will always try to crash the system with random inputs, and discover defects. 

4. I can code faster without tests and can also validate for zero defect: While this may stand true for very small software and websites where the code is small and writing test cases may increase the overall time of development and delivery of the product. But for bigger products, it helps a lot to identify defects at a very early stage and provides a chance to correct them at a very low cost. As seen in the previous screenshots of the cost of fixing defects for phases and testing types, the cost of correcting a defect increases with time. Truly, whether TDD is required for a project or not depends on context. 

5. TDD ensures good design and architecture: TDD encourages developers to write quality code, but it is not a replacement for good design practice and quality code. Will a team of developers be enough to ensure a stable and scalable architecture? Design should still be done by following the standard practices. 

6. You need to write all tests first: Another myth says that you need to write all of the tests first and then the actual production code. Actually, generally an iterative approach is used. Write some tests first, then some code, run the tests, fix the code, run the tests, write more tests, and so on. With TDD, you always test parts of software and keep developing. 

There are many myths, and covering all of them is not possible. The point is, TDD offers developers a better opportunity to deliver quality code. TDD helps organizations by delivering close to zero-defect products. 

## 0201. Testing Concepts 

So far, we have seen how to write simple unit tests, advance them using some actions and assertions. This chapter showcased tests, actions, and assertions using YUI. YUI is used to give an idea of how all this happens and works together through the TDD life cycle. Then you learned about some benefits and pitfalls. In the next chapter, you will learn about popular JavaScript tools and frameworks. YUI was a browser-based testing framework, but later we will also check tools, which don't need you to run test cases in the browser. 

There are a number of ways and methods to test software quality. TDD is focused on testing the small pieces of code using unit tests. Unit tests play a big and important role in TDD irrespective of the programming language. While learning TDD, it is essential to understand unit testing and testing frameworks. In the previous chapter, you learned about the life cycle of TDD. Now with examples, we will see how each step of the life cycle is executed. For this chapter, we will try to showcase examples using YUI (short for Yahoo User Interface) because of its simplicity and easy-tounderstand functions. 

In this chapter, you will learn about unit testing, a little about frameworks, how a test is written, actions, and assertions in unit tests. In this chapter, you will learn the following:1) Unit testing. 2) Following the process. 3) Benefits and pitfalls.

### 2.1 Unit testing

Unit test is a function or method, which invokes a unit of module in software and checks assumptions about the system that the developer has in mind. Unit test helps the developer test the logical functionality of any module. In other words, a unit is the testable piece of software. It can have more than one input and normally a single output. Sometimes, we treat a module of a system as a unit. 

2『单元测试的定义做一张术语卡片。』——已完成

Unit test is only relevant to developers who are closely working with the code. A unit test is only applicable to test a logical piece of a code. Illogical code would not be tested with the use of unit testing. For example, getting and setting values in text field will not be considered in logical code. 

1『单元测试只针对「逻辑代码」。』

Usually, the first unit test is harder to write for any developer. The first test requires more time for any developer. We should follow a practice of asking questions before writing the initial unit test. For example, should you use an already available unit test framework or write you own custom code? What about an automated build process? How about collecting, displaying, and tracking unit test code coverage? Developers are already less motivated to write any unit tests, and having to deal with these questions only makes the process more painful. However, the good thing is that once you're familiar with unit testing and you are comfortable with TDD, it makes life so much easier than before. 

#### 2.1.1 Unit testing frameworks 

Unit testing frameworks help developers write, run, and review unit tests. These frameworks are commonly named as xUnit frameworks and share a set of features across implementations. Many times it happens that the developer has unknowingly written few unit tests, but those are not in structured unit testing. Whenever we open developer/development tools in a browser (for example, firebug in Firefox, Safari's Inspector, or others) and open console to debug your code, you probably write few statements and inspect the results printed in the console. In many cases, this is a form of unit testing, but these are not automated tests and the developer will not be able to use them again and again. 

1『其实自己平时自己调试打印到 console 上也是一种单元测试，只是不是自动的而已。』

Usually, every developer has a practice to use some or the other framework when they use JavaScript in their system, likewise to write a unit test, we can use testing frameworks available in market. Testing frameworks provide a lot of the ready-made piece of code, that the developer does not need to recreate: test suite/case aggregation, assertions, mock/stub helpers, asynchronous testing implementation, and more. Plenty of good open source testing frameworks are available. We will use the YUI Test in this chapter, but of course all good practices are applicable across all frameworks—only the syntax (and maybe some semantics) differs. 

The most important step for any testing framework is collecting all the tests into suites and test cases. Test suites and test cases are part of many files; each test file typically contains tests for a single module. Normally, grouping all tests for a module in one test suite is considered as the best practice. The suite can contain many test cases; each test case includes testing of small aspects of any module. Using setUp and tearDown functions provided at the suite and test-case levels, you can easily handle any pretest setup and post-test teardown, such as resetting the state of a database. Sometimes, setUp and tearDown functions are referred to as follows: 

1. beforeEach(): This function runs before each test. 

2. afterEach(): This function runs after each test. 

3. before(): This function runs before all tests. Executes only once. 

4. after(): This function runs after all tests. Executes only once. 

setUp is usually called before running any test. When we want to run few statements before running test, we need to specify that in the setUp() method. For example, if we want to set some global variables, which is needed by test, then we can initialize those in the setUp() method. On the other hand, tearDown can be useful to clean up things after finishing your test, for example, if you want to reset a variable to some default value after test run is complete. We will understand this in more detail later on in this chapter. 

#### 2.1.2 YUI Tests 

YUI stands for Yahoo! User Interface, which has a component YUI Test. It is a testing framework to unit test your JavaScript code. You will be learning more about how to use this library while practicing TDD life cycle in this chapter. This library is available at [Test - YUI Library](https://yuilibrary.com/yui/docs/test/). You can use YUI Test library using http://yui.yahooapis.com/3.18.1/build/yui/yui-min.js, which is a minified version of this library. 

3『[Quick Start · yui/yui3 Wiki](https://github.com/yui/yui3/wiki/Quick-Start)

#### 1.1 Copy and paste

```html
// Put the YUI seed file on your page.
<script src="http://yui.yahooapis.com/3.18.1/build/yui/yui-min.js"></script>
```

The YUI seed file is an ultra-small bit of JavaScript that enables you to load any YUI component on your page.

#### 1.2 Start using YUI!

```js
<script>
// Create a YUI sandbox on your page.
YUI().use('node', 'event', function (Y) {
    // The Node and Event modules are loaded and ready to use.
    // Your code goes here!
});
</script>
```

Create a YUI instance, called a "sandbox", to use any YUI component. Each YUI sandbox has its own instance of YUI (that's the Y parameter that gets passed to the callback function) and its own set of activated modules, so it won't conflict with other sandboxes on the same page. Any variables you declare inside your sandbox will only be available in that sandbox and won't pollute the global scope.

When creating your YUI sandbox, specify the modules you'd like to use. In this example, we're using the node and event modules. Then, from inside the sandbox, you can access the Node and Event APIs via the Y instance.

1『最常用的模块应该是 node 和 modules。』

YUI will manage all dependency calculations for the modules you need and load the JavaScript onto your page in a single, combined request. Your code inside the sandbox will execute as soon as all the requested YUI modules are loaded onto the page.

Learn more: See All YUI Components（[YUI User Guides](https://yuilibrary.com/yui/docs/guides/)）

1『本节里的 YUI Tests 只是众多 YUI Components 中的一个。』

#### 2.1 Work with the DOM

The Node component makes it quick and convenient to access, create, and manipulate DOM elements. Node APIs accept element references or selector queries for accessing DOM elements.

```js
YUI().use('node', function (Y) {
    // Access DOM nodes.
    var oneElementById     = Y.one('#foo'),
        oneElementByName   = Y.one('body'),
        allElementsByClass = Y.all('.bar');

    // Create DOM nodes.
    var contentNode = Y.Node.create('<div>'),
        listNode    = Y.Node.create('<ul>'),
        footerNode  = Y.Node.create('<footer>');

    contentNode.setHTML('<p>Node makes it easy to add content.</p>');
    listNode.insert('<li>Buy milk</li>');
    footerNode.prepend('<h2>Footer Content</h2>');

    // Manipulate DOM nodes.
    Y.all('.important').addClass('highlight');

    Y.one('#close-button').on('click', function () {
        contentNode.hide();
    });
});
```

Learn more: The Node Component（[Node - YUI Library](https://yuilibrary.com/yui/docs/node/)）

#### 3.1 Create UI Effects

The Transition component makes it easy to create CSS-based transitions that add polish and finesse to your user interactions.

```js
YUI().use('transition', function (Y) {
    // Fade away.
    Y.one('#fademe').transition({
        duration: 1, // seconds
        opacity : 0
    });

    // Shrink to nothing.
    Y.one('#shrinkme').transition({
        duration: 1, // seconds
        width   : 0,
        height  : 0
    });
});
```

Learn more: The Transition Component（[Transition - YUI Library](https://yuilibrary.com/yui/docs/transition/)）

#### 4.1 Load Content with Ajax

The Node.load() method (provided by the node-load module) makes it easy to populate your web page with dynamic content at runtime.

```js
YUI().use('node-load', function (Y) {
    // Replace the contents of the #content node with content.html.
    Y.one('#content').load('content.html');
});
```

』


#### 2.1.3 Following the process

We have been talking about TDD and its life cycle in the last chapter. It's time to see it in action. In this section, we'll take a simple requirement and work on it to understand the life cycle. We will run the test in browser, see, and analyze the report. 

Let's take an example of a currency converter. This is a very simple business requirement where the converter will take a conversion rate and amount as input and return the converted amount. We will build this requirement step by step. Recalling the screenshot in Chapter 1, Overview of TDD, for TDD life cycle, is as follows: 

We will follow each life cycle step with an example to understand how tests are written and executed. 

#### 2.1.4 Preparing the environment

There are a number of frameworks and tools that we can use to write a unit test. For now, we are using YUI as mentioned before. We will write a simple HTML file, which includes JavaScript from YUI. We are going to use CSS for our test runner using the style located at http://yui.yahooapis.com/2.9.0/build/logger/assets/skins/sam/logger.css and YUI Test library from http://yui.yahooapis.com/3.18.1/build/yui/yui-min.js. 

In general, you should always keep your business logic and tests in different files. For the sake of simplicity, we are keeping all code in one file for now. Let's take a very simple example of currency conversion. We will create a function which converts a given currency to another. 

A simple file with no tests in it will be as follows: 

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" type="text/css" 
    href="http://yui.yahooapis.com/2.9.0/build/logger/assets/skins/sam/logger.css"> 
    <script src="http://yui.yahooapis.com/3.18.1/build/yui/yui-min.js"></script>

    <script>
        function convertCurrency(amount, rateOfConversion) {
            // Business logic to convert currency
        }
        // Create a new YUI instance and populate it with the required modules.
        YUI().use('test-console', function (Y) {
            // Test is available and ready for use. Add implementation
            // code here.

            // in the container (div here) with id testLogs.
            new Y.Test.Console().render('#testLogs');

            // run the tests
            Y.Test.Runner.run();
        });
    </script>
</head>
<body class="yui3-skin-sam">
    <div id="testLogs"></div>
</body>
</html>
```

1『在项目「laravel-vue」里实现的，这种知其所以然，自我掌控的感觉真爽。（2020-06-15）』

Let's see what the code is doing. We used the YUI().use() function in which we are utilizing the test-console module of YUI. We used the new keyword to create a new console on div with ID testLog using new Y.Test.Console(). render('#testLogs'). After rendering the test console, we try to run the tests using Y.Test.Runner.run(). Let's run this code using test runner on the browser. We used Firefox for running the HTML file: 

The test console is now blank since there is no test written and run yet. The included JavaScript file will load the YUI library, which will enable us to write the test cases and run them. This library will help us to print the test results into the console. This log can be printed to the console of the browser or to the test console provided by YUI. The CSS file is for styling the test console, which we will see very soon after creating a test and running it. 

We have multiple options to display logs within the test console. We can opt to display different types of messages by selecting checkboxes. The types are info, pass, fail, and status. 

#### 2.1.5 Following the life cycle

We have already picked our requirement that we are going to write a piece of code for currency conversion. Let's follow the life cycle by writing a test. 

#### 2.1.5.1 Writing a test 

We will name our function convertCurrency(). As of now, our function will not have an implementation. But our test will be present at this moment. Let's take an example of conversion. We will try to convert INR100 to USD. We are given that 1 USD = 63 INR. The result of conversion comes to 1.587. If we round it off to 2 decimal points, it's 1.59. Now we have all required input and desired output for a test. Let's write the test then. 

After writing a test, our \<script> tag will be as follows: 

```js
<script>
    // All our functions and tests go here
    function convertCurrency(amount, rateOfConversion) {
        // Business logic to convert currency
        let toCurrencyAmount = 0;
        return toCurrencyAmount;
    }
    // Create a new YUI instance and populate it with the required modules.
    YUI().use('test-console', function (Y) {
        // Test is available and ready for use. Add implementation
        // code here.
        let testCase = new Y.Test.Case({
            testCurrencyConversion: function() {
                let expectedResult = 1.59;
                let actualResult = convertCurrency(100, 1/63);
                Y.Assert.areEqual(expectedResult, actualResult, 
                '100 INR should be equal to $ 1.59');
            }
        });

        // in the container (div here) with id testLogs.
        new Y.Test.Console({
            newstOnTop: false,
            width: '800px',
            height: '600px',
        }).render('#testLogs');

        Y.Test.Runner.add(testCase);
        // run the tests
        Y.Test.Runner.run();
    });
</script>
```

As of now, we have a dummy implementation of the convertCurrency() function with two parameters, one is the amount to be converted and the other is the rate of conversion. We added a test using new Y.Test.Case(). We created a function named testCurrencyConversion and added a line with an assertion call to Y.Assert.areEqual(). This method takes an expected value, actual value, or expression that will evaluate the actual value and an optional message, which can be printed when this test fails. Assertions are used as a checkpoint in our code to verify the trueness of our code. Here, we are checking if the value returned by the convertCurrency() function is correct or not by matching the output to the given value. You will learn more about assertions later in this chapter. 

#### 2.1.5.2 Running the test and seeing if test fails 

Running this code will run our test and all messages will be put into the test console. If you note the preceding code, we used few properties while creating a test using new Y.Test.Console(). We used these to set the height and width of the test console. Let's run the file now: 

You can see from the result that the test failed. It shows the message we added. It also shows the expected value and actual value and their types. TestRunner created a number of messages, but for now, we see only info and fail messages. Let's select pass and status checkboxes as well and take a look at all the other messages: 

If you note the messages in the last run, you will see that TestRunner created a test suite for us and runs the test suite. Test suite is a collection of tests, which will run one by one when the test suite runs. You will learn more about test suites later in this chapter. 

#### 2.1.5.3 Writing a production code 

Now when we already have the test, we know what is required to pass the test—a logic to calculate the converted currency amount. Let's take a look at the following code: 

```js
<script>
    // All our functions and tests go here
    function convertCurrency(amount, rateOfConversion) {
        // Business logic to convert currency
        let toCurrencyAmount = 0;
        toCurrencyAmount = rateOfConversion * amount;
        toCurrencyAmount = Number.parseFloat(toCurrencyAmount).toFixed(2);
        return toCurrencyAmount;
    }
    // Create a new YUI instance and populate it with the required modules.
    YUI().use('test-console', function (Y) {
        // Test is available and ready for use. Add implementation
        // code here.
        let testCase = new Y.Test.Case({
            testCurrencyConversion: function() {
                let expectedResult = 1.59;
                let actualResult = convertCurrency(100, 1/63);
                Y.Assert.areEqual(expectedResult, actualResult, 
                '100 INR should be equal to $ 1.59');
            }
        });

        // in the container (div here) with id testLogs.
        new Y.Test.Console({
            newstOnTop: false,
            width: '800px',
            height: '600px',
        }).render('#testLogs');

        Y.Test.Runner.add(testCase);
        // run the tests
        Y.Test.Runner.run();
    });
</script>
```

We provided a simple implementation for our requirement—our production code. If we run this code using TestRunner on Firefox or Chrome, the test will pass. But IE does not support Number.parseFloat() and will fail the test. We need to check what should be the correct code for Internet Explorer. Let's correct the code to use global parseFloat() instead of Number.parseFloat(). 

```js
toCurrencyAmount = parseFloat(toCurrencyAmount).toFixed(2); 
```

Please note that we added filters for pass, fail as true for console. Now the console will show fail and pass messages by default, and we don't need to check fail and pass in the UI. 

#### 2.1.5.4 Running all tests 

Now that the implementation is done, let's run the tests again and look at what happens. Look at the following screenshot after running the tests: 

Our test is passed. At this point, we have only one test to run, but that is not the case while developing a project. There may be a good amount of tests already prepared. Our new implementation may cause failure of tests, which already passed. In this case, you will need to recheck your code and fix the implementation until all tests pass. This will ensure that our new implementation never breaks any code that is previously written and all tests passed for. 

#### 2.1.5.5 Cleaning up the code 

If all tests are passed in the previous step, we must clean and refactor the code. This is a very necessary step since there would be thousands of tests, if we don't clean up, we may end up with duplicate code, unnecessary variables, unnecessary statements, and code will never be optimized. Code comments or logs must be added for readability purpose. Believe it or not, code comments help a lot in understanding the code when you revisit the code after months. 

#### 2.1.5.6 Repeat
 
After cleaning up the code, we pick a requirement again and repeat the whole process and keep going. All this ensures that whatever you developed so far, works as expected. 

#### 2.1.6 Using the browser console 

So far, you should have an understanding of how you can write a basic test and run it in the browser to see the logs in test console or browser's log console. There will be times when you won't be using test console to show your tests reports and you need to rely on browsers logs. In this case, simply remove the test console from the code and re-run the tests. Take a look at the following screenshot: 

1『

果然，去掉

```js
// new Y.Test.Console({
//     newstOnTop: false,
//     width: '800px',
//     height: '600px',
// }).render('#testLogs');
```

以及

```html
<body class="yui3-skin-sam">
    <!-- <div id="testLogs"></div> -->
</body
```

会在 console 里显示相关信息，但个人觉得不够清晰，还是原生的窗口舒服。
』

This is a console of Firebug plugin of the Firefox web browser. You would find similar logs in console of the Google Chrome web browser. To open the console in Chrome, press Ctrl + Shift + I in Microsoft Windows or command + option + I in Mac and look for the Console tab. 

#### 2.1.7 setUp() and tearDown() 

When you need to set up some data before a test runs, you use the setUp() function. Likewise, to clear, delete, and terminate connections, which should happen at the end of the test, you use the tearDown() function. These functions may have different names in other testing frameworks/tools. Both of these methods are optional, and they will be used only when they are defined. 

An example may be to set some initial data and use the data in the test. Let's check out the following code, which showcases a very simple implementation of the setUp() and tearDown() functions: 

```js
<script>
    // All our functions and tests go here
    function convertCurrency(amount, rateOfConversion) {
        // Business logic to convert currency
        let toCurrencyAmount = 0;
        toCurrencyAmount = rateOfConversion * amount;
        toCurrencyAmount = Number.parseFloat(toCurrencyAmount).toFixed(2);
        return toCurrencyAmount;
    }
    // Create a new YUI instance and populate it with the required modules.
    YUI().use('test-console', function (Y) {
        // Test is available and ready for use. Add implementation
        // code here.
        let testCase = new Y.Test.Case({
            setUp: () => {
                this.expectedResult = 1.59;
            },
            tearDown: () => {
                delete this.expectedResult;
            },
            testCurrencyConversion: () => {
                Y.Assert.areEqual(expectedResult, convertCurrency(100, 1/63), 
                '100 INR should be equal to $ 1.59');
            }
        });

        // in the container (div here) with id testLogs.
        new Y.Test.Console({
            newstOnTop: false,
            width: '800px',
            height: '600px',
        }).render('#testLogs');

        Y.Test.Runner.add(testCase);
        // run the tests
        Y.Test.Runner.run();
    });
</script>
```

We created a data object, which holds an array in setUp() and deletes the object in tearDown() to free up memory used. Please note that setUp() and tearDown() are for data manipulation, and actions or assertions should not be used in these functions. Actual implementations and usage would be more complex, but follow the same process. We created an array, but any kind of value can be assigned as per the requirements. 

#### 2.1.8 Test suites
 
For a project, there would be a number of tests and most of them can be classified in some ways. For example, if a shopping cart is built, there can be tests related to listing of items, items in cart, payments, and so on. In this case, test suites help to organize the tests in groups. 

We can use Y.Test.Suite() constructor to create a test suite. We can, later, add test cases to the suite and run the suite using Y.Test.Runner.add(suite) just like we used to run test cases. Take a look at the following code: 

We created a suite named TestSuite1 in the preceding code and added testCase to the suite using the suite.add() function call. The name TestSuite1 is for logging purpose and helps us identify which test suite is running. 

You can download the example code files from your account at http://www.packtpub.com for all the Packt Publishing books you have purchased. If you purchased this book elsewhere, you can visit http://www.packtpub.com/support and register to have the files e-mailed directly to you. 

#### 2.1.9 Actions and assertions

So far, we have seen very simple tests where only one type of assertion was used. In fact, there are a number of ways you can validate the data. Not only validate the data, but also perform some actions. You will learn about assertions and actions one by one in this section. 

#### 2.1.9.1 Actions 

TDD talks about automated testing, and when it comes to JavaScript, we often need to mock user-driven events. These events can be mouse movements, clicks, submitting a form, and so on. While testing, our code depends on other objects, modules, functions, or actions to be performed. It's not always possible or easy to make an actual call to the function. A mock can be used for this purpose. It will imitate the behavior of a real function being mocked. 

With YUI, we use a node-event-simulate module to simulate native events that behave similar to user generated events. Each framework may define events in its own way, but we are going to see some common scenarios with simple examples in this section: 

1. Mouse events: These events are what users can do with a mouse. There are in total seven events—click, double click, mouse up, mouse down, mouse over, mouse out, and mouse move. 

2. Key events: There are three events—key up, key down, and key press. 

3. UI events: UI events are events which help us change the UI using select, change, blur, focus, scroll, and resize. 

4. Touch gestures: Mobile-first sites are emerging a lot and it is essential to create a mobile site to be on the edge. JavaScript testing frameworks support gesture events testing as well. There are mainly two categories of gestures—single-touch and multi-touch gestures. While there can be a number of gestures, here is the list supported by YUI: single touch/tap, double tap, press, move, flick, two finger gestures—pinch and rotate. 

Let's look at the following example. This example showcases a click event on a button, which adds a class clicked to the button and also renders test console: 

```html
// 暂时忽略
```

In the code, we have an object named controller, which has a handleClick function. This function first renders test console and then adds a class clicked to the caller, which is a button in this case. We have given the showLog class already to the button. We have also given a name to the test; this will help us identify which test case passed or fail. It's always a good practice to give the test case a readable name. 

In setUp(), we bind the click event on the button using this class as selector. We are using the simulate() function to generate a click event which calls handleClick. In case there was an error creating a test console, the button will not have class clicked assigned, and the assertion in next line will fail. Let's run the preceding code: 

As we can see, the test passed. Class clicked was assigned to button and output of assertion was true. This is how a click event can be generated. Similarly, other events can be generated. 

#### 2.1.9.2 Assertions 

Assertions are the key to perform unit tests and validate expression, function, value, state of an object, and so on. A good testing framework has a rich setup assertions. YUI Test has divided assertions into categories. These categories are: 

1.Equity assertions: These are the simplest assertions, which have only two functions areEqual() and areNotEqual(). Both of these accept three parameters—expected value, actual value, and one optional parameter—error message. The last parameter is used when assertion fails. These assertions use the double equal operator (==) to compare and determine if two values are equal: 

```js
Y.Assert.areEqual(2, 2); // Pass 
Y.Assert.areEqual(3, "3", "3 was expected"); // Pass 
Y.Assert.areNotEqual(2, 4); // Pass 
Y.Assert.areEqual(5, 7, "Five was expected."); // Fail 
```

2.Sameness assertions: There are two assertions in this category: areSame() and areNotSame(). Similar to equity assertions, these also accept three parameters: expected value, actual value, and one optional parameter—error message. Unlike equity assertions, these functions use triple equals operator (===) to determine if values and types of two parameters are similar or not: 

```js
Y.Assert.areSame(2, 2); // Pass 
Y.Assert.areNotSame(3, "3", "3 was expected"); // Fail 
```

3.Data type assertions: These assertions are useful when you want to check the data type of something before you move to the next step. The data type can be anything such as array, function, Boolean, number, string, and so on. The following are the assertions in this category: isArray(), isBoolean(), isFunction(), isNumber(), isString(), and isObject(). Each of these takes two parameters—the actual value and optional error message. 

```js
Y.Assert.isString("Test Driven Development Rocks!"); //Pass 
Y.Assert.isNumber(23); //Pass 
Y.Assert.isArray([]); //Pass 
Y.Assert.isObject([]); //Pass 
Y.Assert.isFunction(function(){}); //Pass 
Y.Assert.isBoolean(true); //Pass 
Y.Assert.isObject(function(){}); //Pass 
```

There are two additional assertions in this category for generic purpose, which takes three parameters: expected value, actual value, optional error message. These are isTypeOf() and isInstanceOf(): 

```js
Y.Assert.isTypeOf("string", "TDD Rocks"); //Pass 
Y.Assert.isTypeOf("number", 23); //Pass 
Y.Assert.isTypeOf("boolean", false); //Pass 
Y.Assert.isTypeOf("object", {}); // Pass 
```

4.Special value assertions: Apart from number, strings, Boolean, there are other value types that also exist in JavaScript. To check those types, there are several assertions available: isFalse(), isTrue(), isNaN(), isNotNaN(), isNull(), isNotNull(), isUndefined(), and isNotUndefined(). These functions take two parameters: the actual value and optional error message: 

```js
Y.Assert.isFalse(false); //Pass 
Y.Assert.isTrue(true); //Pass 
Y.Assert.isNaN(NaN); //Pass 
Y.Assert.isNotNaN(23); //Pass 
Y.Assert.isNull(null); //Pass 
Y.Assert.isNotNull(undefined); //Pass 
Y.Assert.isUndefined(undefined); //Pass 
Y.Assert.isNotUndefined(null); //Pass 
```

5.Forced failures: There are times when you need to create your own assertions or you want an assertion to fail intentionally. In this case, you can use the fail() assertion. This assertion takes one optional parameter as an error message: 

```js
Y.Assert.fail(); // The test will fail here. 
Y.Assert.fail("This test should fail."); 
```

Similar to YUI, other frameworks do have assertions. Their naming standards may be different, but almost all these assertions are present in major testing frameworks. 

## 0301. Testing Tools

In this chapter, we have seen how to write unit tests with the use of different tools such as JsUnit, QUnit, Karma, and DalekJS. You learned how can you install different tools, use them to write different tests, and finally wrote one example in each and every tool to understand them in detail. In fact, there are so many tools available, sometimes created eventually to satisfy specific requirements, or as an improvement to some existing tool or framework. The purpose of this chapter was to showcase a variety and a couple of different syntax these tools use. The point to mention here is that despite the difference in syntax or naming conventions, almost all of the tools use assertions, actions, suits, set up, tear down, and so on. In the next chapter, you will learn about Jasmine in more detail and understand how Jasmine works with the use of some examples.

There are so many tools and frameworks available in the market to perform unit testing for any logical JavaScript code. It's necessary that we understand the way these tools work, since it's important to identify a good fit for a project. Though it's not possible to explain all the tools in one chapter or a book, yet some popular tools are included in this chapter. We can write tests with the usage of some test framework and just run them in the browser, on some static page. But for automation, when we use Jenkins (or other tools for continuous integration), we need some tool that can run our tests automatically such as Karma, PhantomJS, and many more. Each of these tools are explained in three subtopics like setup, writing tests, and running tests. We will be covering the following testing frameworks and tools in this chapter: 1) JsUnit. 2) QUnit. 3) Karma with Jasmine. 4) DalekJS.

### 3.3 Karma with Jasmine

Karma is a JavaScript command line tool that can be used to open a browser, which loads an application's source code and executes tests. Karma can be configured to run against a number of browsers, which is useful to boost any developers confident that the application works on all browsers that we need to support. Normally, Karma tests are executed on the command prompt and it will display the results of unit tests on the command prompt once a test is run in the browser.

#### 3.3.1 Getting started

Karma runs on Node.js and it is available as a NPM package. To perform a setup of Karma, we first need Node.js installed in our machine. Let's first install Node.js on the machine. To install Node.js, we need to download it from http://blog. nodejs.org/2014/06/16/node-v0-10-29-stable/. Currently, Karma supports three stable versions of Node.js, which is 0.8.x, 0.10.x, and 0.12.x. We will install 0.10.29 Version for this chapter.

Once we installed Node.js, we can install Karma plugins with the use of command prompt. The best approach is to install Karma locally in our project directory. Open project path in command prompt and then use the following commands. Let's see how we can carry out setup for Karma in the following steps:

1. Install Karma with the use of the command:

    npm install karma –save-dev

    This command will install Karma with Version 0.12.32

2. Once Karma is installed, we will install Jasmine plugin for Karma here:

    npm install karma-jasmine karma-chrome-launcher –save-dev

    These commands will install karma, karma-jasmine, and karma-chrome-launcher packages into node\_modules in your project directory. We can use many test frameworks with Karma, such as karma-jasmine, karmaquint, and many more. However here, we are using karma-jasmine to demonstrate examples. It will save development dependencies into package.json so that any other developer working on the project needs to run npm install in order to get dependencies installed.

3. We will install Karma globally with the use of cli plugin so that we can start Karma from anywhere:

    npm install –g karma-cli

4. Now we can start Karma from anywhere. But to start with, we first need to initialize Karma configuration file.

    karma init karma.conf.js

5. Once we initialize configuration file, then we can start Karma with the use of the following command. This command will show results of test that we have written:

    karma start karma.conf.js

1『在 laravel 里应该可以用 yarn 安装。』

3『[Jasmine Documentation](https://jasmine.github.io/)

上面的安装其实已经过时了，好好研读官方文档。竟然还有 python 版的，好赞！

离线版下载：[Releases · jasmine/jasmine](https://github.com/jasmine/jasmine/releases)

### JASMINE STANDALONE

The standalone distribution provides a simple way to run your specs in a web browser. You can download it from the releases page. Included is a sample app and sample specs. Open SpecRunner.html and run the included specs. Both the source files and their respective specs are linked in the \<head> of the SpecRunner.html.

To start using Jasmine, replace the source/spec files with your own. Then Load the SpecRunner.html in your favorite browser

1『双击 SpecRunner.html 发现打不开，需要在浏览器里点打开文件，选取该文件。』

### Using Jasmine with node

The Jasmine node package contains helper code for developing and running Jasmine tests for node-based projects.

1、Install. You can install Jasmine using npm locally in your project:

```
npm install --save-dev jasmine
```

With the above local installation you can invoke the CLI tool using npx jasmine ... commands. Optionally you can also install jasmine globally so that you can invoke the CLI tool using jasmine ... commands.

```
npm install -g jasmine
```

2、Init a Project. Initialize a project for Jasmine by creating a spec directory and configuration json for you.

```
jasmine init
```

Note that if you installed Jasmine locally use npx jasmine instead of jasmine in any of these examples, like so:

```
npx jasmine init
```

1『初始化后，会生成一个文件「spec/support/jasmine.json」』

3、Generate examples. Generate example spec and source files

```
npx jasmine examples
```

1『产生 4 个文件：lib/jasmine_examples/Player.js 和 lib/jasmine_examples/Song.js 以及 spec/helpers/jasmine_examples/SpecHelper.js 和 spec/jasmine_examples/PlayerSpec.js。』

At this point you should be able to write your first suite（[Your_first_suite](https://jasmine.github.io/tutorials/your_first_suite.html)）

1『

Set jasmine as your test script in your package.json

```
"scripts": { "test": "jasmine" }
```
Run your tests

```
npm test
```

跑成功了，显示：

```
> @ test /Users/Daglas/laravel/laravel-vue
> jasmine

Randomized with seed 30956
Started
.....

5 specs, 0 failures
Finished in 0.016 seconds
Randomized with seed 30956 (jasmine --random=true --seed=30956)
```

但不知道在哪看详细信息啊。

』

4、Configuration. Customize spec/support/jasmine.json to enumerate the source files and spec files you would like the Jasmine runner to include. You may use dir glob strings. Paths starting with ! are excluded, for example !\*\*/*nospec.js.

spec\_dir is used as a prefix for all spec\_files and helpers. Helpers are executed before specs. For an example of some helpers see the react tutorial.（[Testing a React app with Jasmine npm](https://jasmine.github.io/tutorials/react_with_npm)）

```json
{
  // Spec directory path relative to the current working dir when jasmine is executed.
  "spec_dir": "spec",

  // Array of filepaths (and globs) relative to spec_dir to include and exclude
  "spec_files": [
    "**/*[sS]pec.js",
    "!**/*nospec.js"
  ],

  // Array of filepaths (and globs) relative to spec_dir to include before jasmine specs
  "helpers": [
    "helpers/**/*.js"
  ],

  // Stop execution of a spec after the first expectation failure in it
  "stopSpecOnExpectationFailure": false,

  // Run specs in semi-random order
  "random": false
}
```

5、Running tests. Once you have set up your jasmine.json, you can execute all your specs by running jasmine from the root of your project (or npx jasmine if you had installed it locally). If you want to just run one spec or only those whom file names match a certain glob pattern you can do it like this:

```
jasmine spec/appSpec.js
jasmine "**/model/**/critical/**/*Spec.js"
```

6、CLI Options.

后面是相关的配置，详见原文档。

』

1『

慢慢有感觉了。梳理下流程：可以任意对一个 js 文件用命令「npx jasmine xx.js」来跑测试文件，比如在 resources 文件夹下新建 test.js。

```js
function convertCurrency(amount,rateOfConversion) {
    var toCurrencyAmount = 0; 
    // conversion 
    toCurrencyAmount = rateOfConversion * amount; 
    // rounding off 
    toCurrencyAmount = parseFloat(toCurrencyAmount).toFixed(2); 
    return toCurrencyAmount;
}

describe('Convert Currency', function() { 
    it('100 INR should be equal to $ 1.59', function() { 
        expect(convertCurrency(100, 1/63)).toEqual('1.5'); 
    }); 
});
```

用 jasmine 命令跑，结果如下：

```
Randomized with seed 59296
Started
F

Failures:
1) Convert Currency 100 INR should be equal to $ 1.59
  Message:
    Expected '1.59' to equal '1.5'.
  Stack:
    Error: Expected '1.59' to equal '1.5'.
        at <Jasmine>
        at UserContext.<anonymous> (/Users/Daglas/laravel/laravel-vue/resources/test.js:12:44)
        at <Jasmine>

1 spec, 1 failure
Finished in 0.007 seconds
Randomized with seed 59296 (jasmine --random=true --seed=59296)
```

但如果想要被全局检测到，统一跑，即在项目跟目录下跑「npm test」。那么该文件的命名和位置必须符合「spec/support/jasmine.json」里的配置：必须在 spec 文件夹下，js 文件的命名是以 spec.js 或 Spec.js 结尾的。

jasmine 语法的相关知识去看文档：[Your_first_suite](https://jasmine.github.io/tutorials/your_first_suite.html)

』

### 3.3.2 Writing tests

Here, we are using Jasmine with Karma, so let's see how we can write test using Jasmine in Karma. You will learn more about Jasmine in the next chapter.

1、The describe function: We can define different specifications together with the use of the describe function blocks:

```js
describe("A Specification Suite",function(){ …..

});
```

2、The it and expect function: Specifications are expressed with the use of the it function. Expectations can be expressed using the expect function:

```js
describe("A Specification Suite",function(){ 
    it("contains spec with an explanation", function(){ 
        expect(view.tagName).toBe('div'); 
    }); 
});
```

Matchers can be used to get Boolean comparison between the actual value and expected value. Normally, it reports expectation as true of false to Jasmine. Let's see some matchers that we can use in Jasmine, we explained the same in more detail in Chapter 4, Jasmine.

not、toBe、toEqual、toMatch、toBeDefined、toBeUndefined、toBeNull、toBeTruthy、toBeFalsy、toContain、toBeLessThan、toBeGreaterThan、toBeCloseTo、toThrow

3、beforeEach: In Jasmine, to set up a test, the beforeEach() function is used:

```js
describe("EveryDay.ToDoList",function(){
    var list; 
    beforeEach(function(){
        list = new EveryDay.ToDoList(); 
    }); 
    it("sets to tagName to 'div'",function(){
        expect(view.tagName).toBe('div'); 
    });
});
```

4、afterEach: In Jasmine, to tear down a test, the afterEach() function is used:

```js
describe("EveryDay.ToDoList",function(){
    var list; 
    beforeEach(function(){
        list = new EveryDay.ToDoList(); 
    }); 
    afterEach(function(){
        list = null; 
    }); 
    It("sets to tagName to 'div'",function(){
        expect(view.tagName).toBe('div'); 
    });
});
```

5、Custom matchers: Let's see how we can define custom matchers in Jasmine:

```js
beforeEach(function(){
    this.addMatchers({ 
        toBeGreaterThan: function(expected){ 
            var actual = this.actual; 
            …..
            this.message = function(){ 
                return "message" 
            } 
            return actual > expected;
        }
    });
});
```

6、Asynchronous support: It includes the runs and waitsFor blocks and a latch function. The latch function polls until it returns true or the timeout expires, whichever comes first. If the timeout expires, the specifications fails with a message:

```js
runs(functionname); 
waitsfor(function(), { 
    return; 
});
```

### 3.3.3 Running tests

To run any test with the use of Karma, we first need to write our require JS file and put it in the js folder. We will convert our currency conversion example. Create the currency-conversion.js file in the js folder using the following code:

```js
function convertCurrency(amount,rateOfConversion) {
    var toCurrencyAmount = 0; 
    // conversion 
    toCurrencyAmount = rateOfConversion * amount; 
    // rounding off 
    toCurrencyAmount = parseFloat(toCurrencyAmount).toFixed(2); 
    return toCurrencyAmount;
}
```

Then write your test in the test folder. Create the unit-test.js file and put the following code in it:

```js
describe('Convert Currency', function() { 
    it('100 INR should be equal to $ 1.59', function() { 
        expect(convertCurrency(100, 1/63)).toEqual('1.59'); 
    }); 
});
```

Once we are done with writing our unit-test.js file, we need to include this entire configuration in the karma.conf.js file. Open configuration file and then modify the following lines:

```
// list of files / patterns to load in the browser 
    files: ['js/currency-convertor.js', 'test/*.js' ],
```

Once we add file and test it in the configuration file, then we can do other settings in configuration files like autoWatch:true. It will allow us to watch the file and execute the test whenever any file changes. Other option that we can change is singleRun:true, which can help Karma capture browsers, run the tests, and then exit. In the previous example, we have seen how can we add files in the configuration files. Let's see how we can exclude file from the setup with the following example:

```
//list of files / patterns to exclude from test 
exclude: ['js/abc.js',
    abc/*.js' 
    ],
```

We can run our test now with the use of command that we have seen earlier.

```
Karma start karma.conf.js
```

It will run our test in the browser and then close the browser. It will show our test result in command line as shown in the following figure. If any test fails to run, then it will show the result as shown in the following screenshot:

Karma is just a tool which needs any framework to be included to perform testing in Karma. We used Jasmine here. Karma has plugins for testing frameworks (such as Jasmine, Mocha, and QUnit). You can check the source code of the existing plugins and write your own plugin for the desired testing framework.

## 0401. Jasmine

Jasmine is considered to be very popular among testing frameworks. It is called to be complete and does not need any other supporting frameworks. In this chapter, you learned about the Jasmine testing framework and its offerings. You also learned how to extend Jasmine using custom spies, matchers, and equality testers with the help of the employee object. In the next chapter, you will learn about JsTestDriver, its setup, and how we can run our Jasmine specs with it. We will also see how to perform Ajax operations in tests later in this book. 

### 4.1 Understanding behavior-driven development 

A very important thing to learn about TDD is that it's not about just testing, but it's more than that. It defines a process and encourages to improve the overall design of a system. We have seen in Chapter 1, Overview of TDD, and Chapter 2, Testing Concepts, that tests written in TDD not only test our projects, but they also act as documentation and are useful in many more ways. But most of the developers tend to take it just for testing and are not able to harness the benefit of TDD beyond that; probably, because the title mentions test in TDD. 

Behavior-driven development (BDD) is a term introduced by Dan North to address this shortcoming. The terminology used by BDD focuses on the behavioral aspect of the system. In this chapter, you are going to learn about Jasmine in detail and note that the differences in nomenclature of TDD and BDD. Deep down, TDD and BDD would serve the same purpose, but using the vocabulary of BDD gives you a better set of tests and documents your system in a better way. 

While TDD interface gives names such as suite(), test(), setup(), teardown(), suiteSetup(), suiteTearDown(), assert(), and so on. BDD offers describe(), context(), it(), beforeEach(), afterEach(), beforeAll(), afterAll(), expect(), and so on. A test suite in TDD is usually created using suite(),while BDD uses describe(); to create a unit test TDD uses test() and BDD uses it(). 

2『 TDD 与 BDD 的区别，做一张术语卡片。』——已完成

### 4.2 Setting up Jasmine 

Jasmine does not depend on any other JavaScript frameworks. It is available as a standalone release at https://github.com/jasmine/jasmine/releases. We are going to pick a stable version, for example, v2.3.0 for this chapter. We can download a ZIP file of standalone release, which we need to extract and use. After extraction, the folder structure looks like this: 

### 4.3 describe and specs

We have seen tests suites in many tools in the previous chapters. In Jasmine, we use describe to start a test suite. describe is a global function, which takes two parameters—a string and a function. The string is the title for the suite and function contains all of the tests implementations. A test in Jasmine is known as spec. The parameter function in the describe function contains one or more specs. A spec is also defined by calling a global function it, which takes two parameters just like describe. 

1『 jasmine 里一个测试是一个 spec。测试组件 describe 的第二个函数参数里可以包含多个 spec。而 spec 是别全局函数 it() 调用的，it 函数的 2 个参数与 describe 很像，一个是名字字符串一个是调用函数。』

Let's take a look at the following code: 

```js
describe("Title of a Suite", function() { 
    // variables available for all specs 
    var amountToConvert; 
    var rateOfConversion; 
    
    // the function 'it' defines a spec 
    it("Title of a Spec", function() { 
        // do some testing here 
    }); 
    it("Another spec", function() { 
        // do some testing here 
    }); 
}); 
```

As seen from the preceding code, describe defined a suite and specs were defined using it. To make these functions available, we need to use Jasmine JavaScript libraries. The following is the necessary code we need to include in our HTML file: 

```html
<script src="lib/jasmine-2.3.0/jasmine.js"></script> 
<script src="lib/jasmine-2.3.0/jasmine-html.js"></script> 
<script src="lib/jasmine-2.3.0/boot.js"></script> 
```

To style the page, we can use the CSS provided by Jasmine: 

```html
<link rel="stylesheet" type="text/css" href="lib/jasmine- 
2.3.0/jasmine.css"> 
```

Jasmine keeps our JavaScript code and tests in different folders, src—for our logical code, and spec—for all the tests. You would need to check the paths of the files as per your setup. A simple skeleton will be like this: 

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Jasmine Spec Runner v3.5.0</title>

  <link rel="shortcut icon" type="image/png" href="lib/jasmine-3.5.0/jasmine_favicon.png">
  <link rel="stylesheet" href="lib/jasmine-3.5.0/jasmine.css">

  <script src="lib/jasmine-3.5.0/jasmine.js"></script>
  <script src="lib/jasmine-3.5.0/jasmine-html.js"></script>
  <script src="lib/jasmine-3.5.0/boot.js"></script>

  <!-- include source files here... -->
  <script src="src/Player.js"></script>
  <script src="src/Song.js"></script>

  <!-- include spec files here... -->
  <script src="spec/SpecHelper.js"></script>
  <script src="spec/PlayerSpec.js"></script>

</head>

<body>
</body>
</html>
```

1『结构超级清晰，逻辑代码放在 src 文件夹里，测试代码放在 spec 文件夹里。』

In the preceding code, we included two more files except those required by Jasmine. One is start.js in the src/ folder, which contains our logical code, functions, and many more. Another one is startSpec.js, which contains our testing code. For now, we created a simple function to add two values in start.js. 

```js
// function to add two values. 
function add(a, b){ 
    return a + b; 
} 
```

And we created our specs in the startSpec.js file in the spec folder. 

```js
describe('Title of a Suite', function() {
    let numberA = 3;
    let numberB = 2;

    it('Testing the add() function', function() {
        expect(add(numberA, numberB)).toEqual(5);
    });
});
```

1『第一次写代码的时候犯了个错「expect(add(numberA, numberB).toEqual(5));」，自以为 toEqual() 函数是 add() 的链函数，其实是 expect() 的链函数，注意括号的位置。』

We added an expectation in the spec chained with a matcher toEqual(). This matcher is going to compare the values. You are going to learn expectations and matchers further in this chapter. For now, let's create a file (for example, testAdd. html) and see the output after we run the file. Open the browser and run testAdd. html to run the tests: 

### 4.4 Expectations 

Assertions in Jasmine are named as an expectation. An expectation can either be true or false. Every expectation takes an actual value as only argument. An expectation is then chained with a matcher, which takes the expected value as an argument. 

```js
expect(true).toBe(true); 
```

1『断言语句的基本结构，上面的阐述说的很清晰了。』

Here, expect is an expectation and toBe is a matcher. To evaluate negative assertions, expect() is chained with a not before calling a matcher. Matchers are used for Boolean comparison and validation of an expected value. You will learn more about matchers in the next subsection. See the following code: 

```js
expect(false).not.toBe(true); 
```

### 4.4 Matchers 

Matchers are used to compare the expected and actual values or validation of the expected value. If a matcher is going to compare the expected value, it takes actual value as argument. Matchers are chained with expectations. There are a number of matchers provided by Jasmine. Here is a list of all matchers: 

#### 4.4.1 toBe() 

This matcher compares using the identity (===) operator. 

```js
var a = 5; 
expect(a).toBe(5); 
expect(a).not.toBe("5"); 
```

The difference between the identity operator (===) and equality operator (==) is that in identity operator, no type conversion is done before comparison. 

#### 4.4.2 toEqual()

This matcher is used to compare simple literals, variables, and functions. 

```js
expect(a).toEqual(5); // checking for simple variables. 
expect(a).not.toEqual(3); 
```

For simple literals and variables, both toBe() and toEqual() can be used, but to compare objects only toEqual() is to be used. 

#### 4.4.3 toMatch()

This matcher is used for regular expressions. 

```js
var strReg = "The quick brown fox"; 
expect(strReg).toMatch(/The/); 
expect(strReg).not.toMatch(/jump/); 
```

#### 4.4.4 toBeDefined()

This matcher checks if a variable or a function is defined. Let's check for the function we defined for addition: 

```js
expect(add).toBeDefined(); // will pass 
expect(add).not.toBeDefined(); // will not pass 
```

#### 4.4.5 toBeUndefined()

This matcher does the opposite of toBeDefined(). 

```js
expect(add).toBeUndefined(); // will not pass 
expect(add).not.toBeUndefined(); // will pass 
```

#### 4.4.6 toBeNull()

This matcher checks if a variable is null. 

```js
expect(a).not.toBeNull(); 
expect(null).toBeNull(); 
```

#### 4.4.7 toBeTruthy()

This matcher checks if a variable or expression is true. 

```js
a = false; 
b = true; 
expect(b).toBeTruthy(); 
expect(a).not.toBeTruthy(); 
expect(add(2,3)).toBeTruthy(); 
```

#### 4.4.8 toBeFalsy()

This matcher checks if a value or expression is false. 

```js
expect(add(0,0)).toBeFalsy(); 
expect(b).not.toBeFalsy(); 
```

#### 4.4.9 toContain()

This matcher checks if a collection (array) has an item or not. 

```js
var fruits = ["apple", "orange", "grape","papaya", "peach", "banana" ]; 
expect(fruits).toContain("apple"); 
```

#### 4.4.10 toBeLessThan()

This matcher is for the comparison of numbers in mathematics. 

```js
var a = 2, b = 3, c = 5.1234; 
expect(a).toBeLessThan(b); 
expect(c).not.toBeLessThan(a); 
```

In the first expect statement, it compares a to b and expects b would be greater than a. While in next statement, it expects c would not be less than a. 

#### 4.4.11 toBeGreaterThan()

This matcher is the opposite of toBeLessThan(). 

```js
expect(b).toBeGreaterThan(a); 
expect(b).not.toBeGreaterThan(c); 
```

#### 4.4.12 toBeCloseTo()

This matcher checks if a number is close to another number. This matcher takes two arguments, the first is the number and second is the decimal precision. Let's see the following example to understand this matcher: 

```js
expect(c).toBeCloseTo(5.1, 1) // will pass 
expect(c).not.toBeCloseTo(5.1, 2) // will pass 
```

Since c has a value 5.1234, it is compared to 5.1 that matches till the first digit. Thus, it passes for the first expectation. 

#### 4.4.13 toThrow()

This matcher checks if a function throws an exception. 

```js
f1 = function() { 
    return 1 + 2; 
}; 
f2 = function() { 
    return undefinedVar + 1; 
}; 
expect(f1).not.toThrow(); 
expect(f2).toThrow(); 
```

#### 4.4.14 toThrowError()

This matcher checks if an specific exception was thrown from a function. 

```js
f3 = function() { 
    throw new TypeError("A custom Exception from f3"); 
}; 
expect(f3).toThrowError("custom"); 
```

The preceding expectation will fail, as the strings do not match exactly. "custom" does not match "A custom Exception from f3". But the following expectation will pass, because it uses regular expression to match the strings: 

```js
expect(f3).toThrowError(/custom/); 
```

The following expectation checks using the exception type as well. It also takes an optional argument as a string or regular expression to match the string. 

```js
expect(f3).toThrowError(TypeError); // will pass, checks type 
expect(f3).toThrowError(TypeError, /custom/); // will pass 
expect(f3).toThrowError(TypeError, "custom exception"); // will fail 
```

#### 4.4.15 jasmine.any()

Sometimes, we are unaware of the actual value of an expression, but know the type. In this case, we can match them using jasmine.any(). Let's see how this is used: 

```js
expect([12,323]).toEqual(jasmine.any(Array)); 
expect({}).toEqual(jasmine.any(Object)); 
expect(21312312).toEqual(jasmine.any(Number)); 
```

As we can see, jasmine.any will match the expected value to a type of class. 

#### 4.4.16 jasmine.objectContaining()

We can also do partial match when it comes to key/pair values. Let's see the following example to see how it works: 

```js
var employee = { 
    name: "Alice", 
    age: 29, 
    department: "Testing", 
    grade: 5 
} 

expect(employee).toEqual(jasmine.objectContaining({ 
    department: "Testing" 
})); 
expect(employee).toEqual(jasmine.objectContaining({ 
    age: jasmine.any(Number) 
})); 
```

We can provide a key/value pair to match partially with an object. Sometimes, these default matchers are not enough to fulfill our requirements, and we need to create custom matchers. With Jasmine, we can create custom matchers, which you will learn later in this chapter. 

### 4.5 Set up and tear down 

Just like other frameworks, Jasmine also provides a way to set up and tear down. Jasmine provides global functions such as beforeEach—called before each spec, afterEach—called after each spec, beforeAll—called only once before all specs are run, and afterAll—called only once after all specs are done. Look at the following code to understand this: 

```js
describe('Setup and Teardown', () => {
    let count = 0;
    let velocity = 0;
    beforeEach(() => {
        velocity = 100;
        count++;
        console.log('Count is ' + count);
    });

    afterEach(() => {
        velocity = 0;
        console.log('Some spec just finished and this function is called');
    });

    beforeAll(() => {
        console.log('This is called only one, specs are about to run.');
    });

    afterAll(() => {
        console.log('All specs finished, time for cleanup');
    });

    it('Testing Velocity and reducing velocity', () => {
        expect(velocity).toEqual(100);
        velocity = 20;
        expect(velocity).toBe(20);
    })

    it('Testing Velocity', () => {
        expect(velocity).toEqual(100);
        expect(true).toEqual(true);
    });
});
```

If you run the following code, you will see all specs running successfully with status pass and the following will be the console output. The beforeAll and afterAll functions are run once during a run. We can see that the variable count is increased by 1 before each spec is run and velocity is set to 100 so that the first expectation of each spec is met true. 

This was one way of sharing variables among it, beforeEach, and afterEach. There is one more way using the this keyword, which is set to empty for each spec. Consider the following code: 

```js
describe('Setup and Teardown', () => {
    let count = 0;
    let velocity = 0;
    beforeEach(() => {
        this.velocity = 100;
    });

    afterEach(() => {
        this.velocity = 0;
    });

    it('Testing Velocity and reducing velocity', () => {
        expect(this.velocity).toEqual(100);
        this.velocity = 20;
        expect(this.velocity).toBe(20);
        this.acceleration = 5;
    })

    it('Testing Velocity', () => {
        expect(this.acceleration).toBeUndefined();
    });
});
```

Since the this keyword will be set to empty for the next spec, this.acceleration will not be defined. Running this suite will pass all the specs in it. 

### 4.6 Spies 

A spy is an emulation of a function or object, irrespective of which function/object is defined or not. There are times when we need stubs for the functions we need to use for performing testing. Jasmine has spies for this purpose. A spy can stub functions but can only exist within describe and it block if it is defined. 

Apart from the matchers we read in this chapter, there are special matchers just for spies. One is toHaveBeenCalled(), which returns true if the spy was called. Another one is toHaveBeenCalledWith(), which returns true if the spy was called with arguments. 

Let's see the following example to understand how spies work. The following is our source for an Employee function in the employee.js file created in the src folder: 

```js
let DEFAULT_SALARY = 1000;

function Employee(name, grade, department, salary) {
    this.name = name;
    this.grade = grade;
    this.department = department;

    this.salary = salary || 0;
}

// 此处不能用箭头函数
Employee.prototype.getName = function() {
    return this.name;
};
Employee.prototype.getDepartment = function() {
    return this.department;
};
Employee.prototype.getGrade = function() {
    return this.grade;
};
Employee.prototype.getSalary = function() {
    return this.salary;
};
Employee.prototype.calculateSalary = function() {
    return this.grade * DEFAULT_SALARY;
};

Employee.prototype.getDetails = function() {
    return 'Employee Name: ' + this.getName() + '\nDepartment: ' + this.getDepartment() +
    '\nGrade: ' + this.getGrade() + '\nSalary: ' + this.getSalary();
};
```

We need to print details of each employee. We want to be sure that the salary was calculated before employee details were printed. We create a spy using the spyOn() function and call this file spyEmployee.js. We then put it in the spec folder. 

```js
describe('Jasmine Spy', () => {
    it('Spying employee', () => {
        let alice = new Employee('Alice', 4, 'Testing');
        spyOn(alice, 'calculateSalary');
        console.log(alice.getDetails());
        expect(alice.calculateSalary).toHaveBeenCalled();
    });
});
```

We created a spy using spyOn(alice, "calculateSalary"), and then called the toHaveBeenCalled() matcher. As soon as we create a spy on the calculateSalary() function, Jasmine replaces the actual implementation. Now a spy will be called rather than an actual implementation. 

After running this HTML file, the following is the output: 

As we can see, it was expected that calculateSalary should have been called, but it failed since it was not called before printing the salary. Now let's change our code in employee.js and keep spec as it is: 

```js
var DEFAULT_SALARY = 1000;

function Employee(name, grade, department, salary) {
    this.name = name;
    this.grade = grade;
    this.department = department;

    this.salary = salary || 0;
}

// 此处不能用箭头函数
Employee.prototype.getName = function() {
    return this.name;
};

Employee.prototype.getDepartment = function() {
    return this.department;
};

Employee.prototype.getGrade = function() {
    return this.grade;
};

Employee.prototype.getSalary = function() {
    if (!this.salary) {
        this.salary = this.calculateSalary();
    }
    return this.salary;
}

Employee.prototype.calculateSalary = function() {
    return this.grade * DEFAULT_SALARY;
};

Employee.prototype.getDetails = function() {
    return 'Employee Name: ' + this.getName() + '\nDepartment: ' + this.getDepartment() +
    '\nGrade: ' + this.getGrade() + '\nSalary: ' + this.getSalary();
};
```

1『跑出来，发现 console 上，DEFAULT_SALARY 是 undefined，原因待解决。（2020-06-16）』

As we can see, calculateSalary is now being called from the getSalary() function. Let's run this again and see what happens: 

Now spec passed because it could find that the salary was calculated before printing details. In this example, we worked with the toHaveBeenCalled() matcher. There are several other matchers also defined for spies: 

• toHaveBeenCalledWith(): To understand this, let's modify method in employee.js: 

```js
Employee.prototype.calculateSalary = function(grade){ 
    this.grade = grade; this.salary = this.grade * DEFAULT_SALARY; 
} 
```

This method will take grade and set both the salary and grade for an employee. We know that it will call the calculateSalary() function without any argument, which we can see by our implementation. We add one more spec to check if this was called with or without arguments. 

```js
describe('Jasmine Spy', () => {
    it('Spying employee', () => {
        let alice = new Employee('Alice', 4, 'Testing');
        spyOn(alice, 'calculateSalary');
        console.log(alice.getDetails());
        // expect(alice.calculateSalary).toHaveBeenCalled();
        expect(alice.calculateSalary).toHaveBeenCalledWith(5);
    });
});
```

If we run our spec now, we can see that it will fail with message: Expected spy calculateSalary to have been called with [ 5 ] but actual calls were [ ]: 

We can chain the expectation with not as well: 

```js
expect(alice.calculateSalary).not.toHaveBeenCalledWith(5); 
```

After chaining with not, if you rerun the spec, it will pass. 
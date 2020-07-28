# 2019030Refactoring2EdR01

## 记忆时间

## 0101. Refactoring: A First Example Topics

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

### 1.6 Spliting the Phases of Calculation and Formatting

So far, my refactoring has focused on adding enough structure to the function so that I can understand it and see it in terms of its logical parts. This is often the case early in refactoring. Breaking down complicated chunks into small pieces is important, as is naming things well. Now, I can begin to focus more on the functionality change I want to make—specifically, providing an HTML version of this statement. In many ways, it’s now much easier to do. With all the calculation code split out, all I have to do is write an HTML version of the seven lines of code at the top. The problem is that these brokenout functions are nested within the textual statement method, and I don’t want to copy and paste them into a new function, however well organized. I want the same calculation functions to be used by the text and HTML versions of the statement.

到目前为止，我的重构主要是为原函数添加足够的结构，以便我能更好地理解它，看清它的逻辑结构。这也是重构早期的一般步骤。把复杂的代码块分解为更小的单元，与好的命名一样都很重要。现在，我可以更多关注我要修改的功能部分了，也就是为这张详单提供一个 HTML 版本。不管怎么说，现在改起来更加简单了。因为计算代码已经被分离出来，我只需要为顶部的 7 行代码实现一个 HTML 的版本。问题是，这些分解出来的函数嵌套在打印文本详单的函数中。无论嵌套函数组织得多么良好，我总不想将它们全复制粘贴到另一个新函数中。我希望同样的计算函数可以被文本版详单和 HTML 版详单共用。

There are various ways to do this, but one of my favorite techniques is Split Phase (154). My aim here is to divide the logic into two parts: one that calculates the data required for the statement, the other that renders it into text or HTML. The first phase creates an intermediate data structure that it passes to the second.

I start a Split Phase (154) by applying Extract Function (106) to the code that makes up the second phase. In this case, that’s the statement printing code, which is in fact the entire content of statement. This, together with all the nested functions, goes into its own top­level function which I call renderPlainText.

要实现复用有许多种方法，而我最喜欢的技术是拆分阶段（154）。这里我的目标是将逻辑分成两部分：一部分计算详单所需的数据，另一部分将数据渲染成文本或 HTML。第一阶段会创建一个中转数据结构，再把它传递给第二阶段。要开始拆分阶段（154），我会先对组成第二阶段的代码应用提炼函数（106）。在这个例子中，这部分代码就是打印详单的代码，其实也就是 statement 函数的全部内容。我要把它们与所有嵌套的函数一起抽取到一个新的顶层函数中，并将其命名为 renderPlainText。

1『 statement() 相当于一个空函数，把 renderPlainText() 里的东西一点点剥离出来放进 statement()。』

```js
statement() {
  return this.renderPlainText();
},
renderPlainText() {
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

I do my usual compile-­test-­commit, then create an object that will act as my intermediate data structure between the two phases. I pass this data object in as an argument to renderPlainText (compile­test­commit).

```js
statement() {
  const statementData = {};
  return this.renderPlainText(statementData);
},
renderPlainText(data) {
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

I now examine the other arguments used by renderPlainText. I want to move the data that comes from them into the intermediate data structure, so that all the calculation code moves into the statement function and renderPlainText operates solely on data passed to it through the data parameter. My first move is to take the customer and add it to the intermediate object (compiletest­commit).

```js
statement() {
  const statementData = {};
  statementData.customer = invoices[0].customer;
  return this.renderPlainText(statementData, invoices[0]);
},
renderPlainText(data, invoice) {
  let result = `Statement for ${data.customer}\n`;
  for (let perf of invoice.performances) {
    result += `${this.playFor(perf).name}: ${this.usd(this.amountFor(perf))}(${perf.audience} seats)\n`;
  }
  result += `Amount owed is ${this.usd(this.totalAmount())}\n`;
  result += `You earned ${this.totalVolumeCredits()} credits\n`;
  console.log(result);
},
```

Similarly, I add the performances, which allows me to delete the invoice parameter to renderPlainText (compile­test­commit). 

top level…

```js
statement() {
  const statementData = {};
  statementData.customer = invoices[0].customer;
  statementData.performances = invoices[0].performances;
  return this.renderPlainText(statementData);
},
renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`;
  for (let perf of data.performances) {
    result += `${this.playFor(perf).name}: ${this.usd(this.amountFor(perf))}(${perf.audience} seats)\n`;
  }
  result += `Amount owed is ${this.usd(this.totalAmount(data))}\n`;
  result += `You earned ${this.totalVolumeCredits(data)} credits\n`;
  console.log(result);
},
```

1『这里跟原书中的代码不一样，因为是在 vue 里实现的，调用函数的时候还是的传入参数 data，原书中的代码不用传参，是因为闭包的原因么？待确认。（2020-06-12）』

function renderPlainText…

```js
totalAmount(data) {
  let result = 0;
  for (let perf of data.performances) {
    result += this.amountFor(perf);
  }
  return result;
},
totalVolumeCredits(data) {
  let result = 0;
  for (let perf of data.performances) {
    result += this.volumeCreditsFor(perf);
  }
  return result;
},
```

Now I’d like the play name to come from the intermediate data. To do this, I need to enrich the performance record with data from the play (compile-­test-­commit).

```js
statement() {
  const statementData = {};
  statementData.customer = invoices[0].customer;
  statementData.performances = invoices[0].performances.map(this.enrichPerformance);
  return this.renderPlainText(statementData);
},
enrichPerformance(aPerformance) {
  const result = Object.assign({}, aPerformance);
  return result;
},
```

1『 map() 函数的使用，还能像语句 invoices[0].performances.map(this.enrichPerformance) 这样用，传入回调函数时，直接省略了数组中各元素的标识「item」，涨见识了。书籍「忍者秘籍」里的介绍：内置的 map 方法创建了一个全新的数组，然后遍历输入的数组。对输入数组的每个元素，在新建的数组上，都会基于回调函数的执行结果创建一个对应的元素。其典型用法是 const weapons = ninjas.map(item => item.weapon) 』

3『 [Object.assign() - JavaScript | MDN](https://wiki.developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)

Object.assign() 方法用于将所有可枚举属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。

```js
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target);
// expected output: Object { a: 1, b: 4, c: 5 }
console.log(returnedTarget);
// expected output: Object { a: 1, b: 4, c: 5 }
```

如果目标对象中的属性具有相同的键，则属性将被源对象中的属性覆盖。后面的源对象的属性将类似地覆盖前面的源对象的属性。Object.assign 方法只会拷贝源对象自身的并且可枚举的属性到目标对象。该方法使用源对象的 [[Get]] 和目标对象的 [[Set]]，所以它会调用相关 getter 和 setter。因此，它分配属性，而不仅仅是复制或定义新的属性。如果合并源包含 getter，这可能使其不适合将新属性合并到原型中。为了将属性定义（包括其可枚举性）复制到原型，应使用Object.getOwnPropertyDescriptor()和Object.defineProperty() 。

String类型和 Symbol 类型的属性都会被拷贝。在出现错误的情况下，例如，如果属性不可写，会引发 TypeError，如果在引发错误之前添加了任何属性，则可以更改 target 对象。注意，Object.assign 不会在那些 source 对象值为 null 或 undefined 的时候抛出错误。

```js
// 复制一个对象节
const obj = { a: 1 };
const copy = Object.assign({}, obj);
console.log(copy); // { a: 1 }

// 合并对象节
const o1 = { a: 1 };
const o2 = { b: 2 };
const o3 = { c: 3 };
const obj = Object.assign(o1, o2, o3);
console.log(obj); // { a: 1, b: 2, c: 3 }
console.log(o1);  // { a: 1, b: 2, c: 3 }, 注意目标对象自身也会改变。

// 合并具有相同属性的对象节，属性被后续参数中具有相同属性的其他对象覆盖。
const o1 = { a: 1, b: 1, c: 1 };
const o2 = { b: 2, c: 2 };
const o3 = { c: 3 };
const obj = Object.assign({}, o1, o2, o3);
console.log(obj); // { a: 1, b: 2, c: 3 }
```

』

At the moment, I’m just making a copy of the performance object, but I’ll shortly add data to this new record. I take a copy because I don’t want to modify the data passed into the function. I prefer to treat data as immutable as much as I can—mutable state quickly becomes something rotten.

现在我只是简单地返回了一个 aPerformance 对象的副 本，但马上我就会往这条记录中添加新的数据。返回副本的原因是，我不想修改传给函数的参数，我总是尽量保持数据不可变（immutable）——可变的状态会很快变成烫手的山芋。

1『为何使用 assign() 函数复制一个对象可以实现数据的「不可变」，目前没吃透。（2020-06-12）』

The idiom result = Object.assign({}, aPerformance) looks very odd to people unfamiliar to JavaScript. It performs a shallow copy. I’d prefer to have a function for this, but it’s one of those cases where the idiom is so baked into JavaScript usage that writing my own function would look out of place for JavaScript programmers.

Now I have a spot for the play, I need to add it. To do that, I need to apply Move Function (198) to playFor and statement (compile­-test­-commit).

现在我们已经有了安放 play 字段的地方，可以把数据放进去。我需要对 playFor 和 statement 函数应用搬移函数（198）（然后编译、测试、提交）。

function statement…

```js
enrichPerformance(aPerformance) {
  const result = Object.assign({}, aPerformance);
  result.play = this.playFor(result);
  return result;
},
```

I then replace all the references to playFor in renderPlainText to use the data instead (compile­test­commit).

```js
statement() {
  const statementData = {};
  statementData.customer = invoices[0].customer;
  statementData.performances = invoices[0].performances.map(this.enrichPerformance);
  return this.renderPlainText(statementData);
},
enrichPerformance(aPerformance) {
  const result = Object.assign({}, aPerformance);
  result.play = this.playFor(result);
  return result;
},
renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`;
  for (let perf of data.performances) {
    result += `${perf.play.name}: ${this.usd(this.amountFor(perf))}(${perf.audience} seats)\n`;
  }
  result += `Amount owed is ${this.usd(this.totalAmount(data))}\n`;
  result += `You earned ${this.totalVolumeCredits(data)} credits\n`;
  console.log(result);
},
volumeCreditsFor(aPerformance) {
  let result = 0;
  result += Math.max(aPerformance.audience - 30, 0);
  // add extra credit for every ten comedy attendees
  if ('comedy' === aPerformance.play.type) {
    result += Math.floor(aPerformance.audience / 5);
  }
  return result;
},
amountFor(aPerformance) {
  let result = 0;
  switch (aPerformance.play.type) {
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
      throw new Error(`unkown type: ${aPerformance.play.type}`);
  }
  return result;
},
playFor(aPerformance) {
  return plays[aPerformance.playID];
},
```

I then move amountFor in a similar way (compile-­test-­commit).

function statement…

```js
enrichPerformance(aPerformance) {
  const result = Object.assign({}, aPerformance);
  result.play = this.playFor(result);
  result.amount = this.amountFor(result);
  return result;
},
```

function renderPlainText…

```js
renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`;
  for (let perf of data.performances) {
    result += `${perf.play.name}: ${this.usd(perf.amount)}(${perf.audience} seats)\n`;
  }
  result += `Amount owed is ${this.usd(this.totalAmount(data))}\n`;
  result += `You earned ${this.totalVolumeCredits(data)} credits\n`;
  console.log(result);
},
totalAmount(data) {
  let result = 0;
  for (let perf of data.performances) {
    result += perf.amount;
  }
  return result;
},
```

Next, I move the volume credits calculation (compile-­test-­commit).

function statement…

```js
enrichPerformance(aPerformance) {
  const result = Object.assign({}, aPerformance);
  result.play = this.playFor(result);
  result.amount = this.amountFor(result);
  result.volumeCredits = this.volumeCreditsFor(result);
  return result;
},
```

function renderPlainText…

```js
totalVolumeCredits(data) {
  let result = 0;
  for (let perf of data.performances) {
    result += perf.volumeCredits;
  }
  return result;
},
```

Finally, I move the two calculations of the totals.

function statement…

```js
statement() {
  const statementData = {};
  statementData.customer = invoices[0].customer;
  statementData.performances = invoices[0].performances.map(this.enrichPerformance);
  statementData.totalAmount = this.totalAmount(statementData);
  statementData.totalVolumeCredits = this.totalVolumeCredits(statementData);
  return this.renderPlainText(statementData);
},
```

function renderPlainText… 

```js
renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`;
  for (let perf of data.performances) {
    result += `${perf.play.name}: ${this.usd(perf.amount)}(${perf.audience} seats)\n`;
  }
  result += `Amount owed is ${this.usd(data.totalAmount)}\n`;
  result += `You earned ${data.totalVolumeCredits} credits\n`;
  console.log(result);
},
```

Although I could have modified the bodies of these totals functions to use the statementData variable (as it’s within scope), I prefer to pass the explicit parameter. And, once I’m done with compile-­test-­commit after the move, I can’t resist a couple quick shots of Replace Loop with Pipeline (231).

1『管道取代循环，这个 NB 方法一定要学会。』

function renderPlainText… 

```js
totalAmount(data) {
  return data.performances
    .reduce((total, p) => total + p.amount, 0);
},
totalVolumeCredits(data) {
  return data.performances
    .reduce((total, p) => total + p.volumeCredits, 0);
},
```

3『 [Array.prototype.reduce() - JavaScript | MDN](https://wiki.developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

reduce() 方法对数组中的每个元素执行一个由您提供的 reducer 函数（升序执行），将其结果汇总为单个返回值。

```js
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```

arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])

reducer 函数接收 4 个参数：Accumulator (acc) (累计器)、Current Value (cur) (当前值)、Current Index (idx) (当前索引)、Source Array (src) (源数组)。您的 reducer 函数的返回值分配给累计器，该返回值在数组的每个迭代中被记住，并最后成为最终的单个结果值。

回调函数第一次执行时，accumulator 和 currentValue 的取值有两种情况：如果调用 reduce() 时提供了 initialValue，accumulator 取值为 initialValue，currentValue 取数组中的第一个值；如果没有提供 initialValue，那么 accumulator 取数组中的第一个值，currentValue 取数组中的第二个值。注意：如果没有提供 initialValue，reduce 会从索引 1 的地方开始执行 callback 方法，跳过第一个索引。如果提供 initialValue，从索引 0 开始。

如果数组为空且没有提供 initialValue，会抛出 TypeError 。如果数组仅有一个元素（无论位置如何）并且没有提供 initialValue， 或者有提供 initialValue 但是数组为空，那么此唯一值将被返回并且 callback 不会被执行。提供初始值通常更安全，正如下面的例子，如果没有提供 initialValue，则可能有四种输出：

```js
var maxCallback = ( acc, cur ) => Math.max( acc.x, cur.x );
var maxCallback2 = ( max, cur ) => Math.max( max, cur );

// reduce() 没有初始值
[ { x: 2 }, { x: 22 }, { x: 42 } ].reduce( maxCallback ); // NaN
[ { x: 2 }, { x: 22 }            ].reduce( maxCallback ); // 22
[ { x: 2 }                       ].reduce( maxCallback ); // { x: 2 }
[                                ].reduce( maxCallback ); // TypeError

// map/reduce; 这是更好的方案，即使传入空数组或更大数组也可正常执行
[ { x: 22 }, { x: 42 } ].map( el => el.x )
                        .reduce( maxCallback2, -Infinity );
```

后面有很多例子，值得仔细研读。一个意外收获（数组去重）：如果你正在使用一个可以兼容 Set 和 Array.from() 的环境， 你可以使用 let orderedArray = Array.from(new Set(myArray)); 来获得一个相同元素被移除的数组。这是收集到的数组去重第二个方法，第一个是用 Set() 后再用 ... 运算符转会为数组。

』

I now extract all the first­phase code into its own function (compile-­test-­commit).

top level…

```js
statement() {
  return this.renderPlainText(this.createStatementData());
},
createStatementData() {
  const statementData = {};
  statementData.customer = invoices[0].customer;
  statementData.performances = invoices[0].performances.map(this.enrichPerformance);
  statementData.totalAmount = this.totalAmount(statementData);
  statementData.totalVolumeCredits = this.totalVolumeCredits(statementData);
  return statementData;
},
```

Since it’s clearly separate now, I move it to its own file (and alter the name of the returned result to match my usual convention).

statement.js…

```js
import createStatementData from './createStatementData.js';

...
```

1『注意，这里的引用语句不能用「import { createStatementData } from './createStatementData.js';」』

createStatementData.js…

```js
// 后面有代码，此处省略
```

One final swing of compile­-test-­commit—and now it’s easy to write an HTML version.

statement.js…

```js
function htmlStatement (invoice, plays) { 
    return renderHtml(createStatementData(invoice, plays)); 
}

function renderHtml (data) {
    // 此处 html 版的样式输出代码省略
    // 此时此刻算是理解了输出样式与数据层的分离
}
```

(I moved usd to the top level, so that renderHtml could use it.)

### 1.7 Status: Separated into Two Files(and Phases)

This is a good moment to take stock again and think about where the code is now. I have two files of code.

statement.js

```js
import { plays, invoices } from './db/data';
import createStatementData from './db/createStatementData';

statement() {
  return this.renderPlainText(createStatementData(invoices[0], plays));
},
renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`;
  for (let perf of data.performances) {
    result += `${perf.play.name}: ${this.usd(perf.amount)}(${perf.audience} seats)\n`;
  }
  result += `Amount owed is ${this.usd(data.totalAmount)}\n`;
  result += `You earned ${data.totalVolumeCredits} credits\n`;
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

createStatementData.js

```js
export default function createStatementData(invoice, plays) {
  const result = {};
  result.customer = invoice.customer;
  result.performances = invoice.performances.map(enrichPerformance);
  result.totalAmount = totalAmount(result);
  result.totalVolumeCredits = totalVolumeCredits(result);
  return result;

  function enrichPerformance(aPerformance) {
    const result = Object.assign({}, aPerformance);
    result.play = playFor(result);
    result.amount = amountFor(result);
    result.volumeCredits = volumeCreditsFor(result);
    return result;
  }

  function playFor(aPerformance) {
    return plays[aPerformance.playID];
  }

  function amountFor(aPerformance) {
    let result = 0;
    switch (aPerformance.play.type) {
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
        throw new Error(`unkown type: ${aPerformance.play.type}`);
    }
    return result;
  }

  function volumeCreditsFor(aPerformance) {
    let result = 0;
    result += Math.max(aPerformance.audience - 30, 0);
    // add extra credit for every ten comedy attendees
    if ('comedy' === aPerformance.play.type) {
      result += Math.floor(aPerformance.audience / 5);
    }
    return result;
  }

  function totalAmount(data) {
    return data.performances
      .reduce((total, p) => total + p.amount, 0);
  }

  function totalVolumeCredits(data) {
    return data.performances
      .reduce((total, p) => total + p.volumeCredits, 0);
  }
}
```

I have more code than I did when I started: 70 lines (not counting htmlStatement) as opposed to 44, mostly due to the extra wrapping involved in putting things in functions. If all else is equal, more code is bad—but rarely is all else equal. The extra code breaks up the logic into identifiable parts, separating the calculations of the statements from the layout. This modularity makes it easier for me to understand the parts of the code and how they fit together. Brevity is the soul of wit, but clarity is the soul of evolvable software. Adding this modularity allows to me to support the HTML version of the code without any duplication of the calculations.

代码行数由我开始重构时的 44 行增加到了 70 行（不算 htmlStatement），这主要是将代码抽取到函数里带来的额外包装成本。虽然代码的行数增加了，但重构也带来了代码可读性的提高。额外的包装将混杂的逻辑分解成可辨别的部分，分离了详单的计算逻辑与样式。这种模块化使我更容易辨别代码的不同部分，了解它们的协作关系。虽说言以简为贵，但可演化的软件却以明确为贵。通过增强代码的模块化，我可以轻易地添加 HTML 版本的代码，而无须重复计算部分的逻辑。

When programming, follow the camping rule: Always leave the code base healthier than when you found it.

There are more things I could do to simplify the printing logic, but this will do for the moment. I always have to strike a balance between all the refactorings I could do and adding new features. At the moment, most people under­prioritize refactoring—but there still is a balance. My rule is a variation on the camping rule: Always leave the code base healthier than when you found it. It will never be perfect, but it should be better.

其实打印逻辑还可以进一步简化，但当前的代码也够用了。我经常需要在所有可做的重构与添加新特性之间寻找平衡。在当今业界，大多数人面临同样的选择时，似乎多以延缓重构而告终——当然这也是一种选择。我的观点则与营地法则无异：保证离开时的代码库一定比你来时更加健康。完美的境界很难达到，但应该时时都勤加拂拭。

### 1.8 Reorganizing the Calculations by Type 

Now I’ll turn my attention to the next feature change: supporting more categories of plays, each with its own charging and volume credits calculations. At the moment, to make changes here I have to go into the calculation functions and edit the conditions in there. The amountFor function highlights the central role the type of play has in the choice of calculations—but conditional logic like this tends to decay as further modifications are made unless it’s reinforced by more structural elements of the programming language.

接下来我将注意力集中到下一个特性改动：支持更多类型的戏剧，以及支持它们各自的价格计算和观众量积分计算。对于现在的结构，我只需要在计算函数里添加分支逻辑即可。amountFor 函数清楚地体现了，戏剧类型在计算分支的选择上起着关键的作用——但这样的分支逻辑很容易随代码堆积而腐坏，除非编程语言提供了更基础的编程语言元素来防止代码堆积。

There are various ways to introduce structure to make this explicit, but in this case a natural approach is type polymorphism—a prominent feature of classical objectorientation. Classical OO has long been a controversial feature in the JavaScript world, but the ECMAScript 2015 version provides a sound syntax and structure for it. So it makes sense to use it in a right situation—like this one.

要为程序引入结构、显式地表达出「计算逻辑的差异是由类型代码确定」有许多途径，不过最自然的解决办法还是使用面向对象世界里的一个经典特性——类型多态。传统的面向对象特性在 JavaScript 世界一直备受争议，但新的 ECMAScript 2015 规范有意为类和多态引入了一个相当实用的语法糖。这说明，在合适的场景下使用面向对象是合理的——显然我们这个就是一个合适的使用场景。

1『在 JS 中使用面向对象语法糖，一个经典的应用场景是「类型多态」来解决「计算逻辑的差异是由类型代码确定」的场景。』

My overall plan is to set up an inheritance hierarchy with comedy and tragedy subclasses that contain the calculation logic for those cases. Callers call a polymorphic amount function that the language will dispatch to the different calculations for the comedies and tragedies. I’ll make a similar structure for the volume credits calculation. To do this, I utilize a couple of refactorings. The core refactoring is Replace Conditional with Polymorphism (272), which changes a hunk of conditional code with polymorphism. But before I can do Replace Conditional with Polymorphism (272), I need to create an inheritance structure of some kind. I need to create a class to host the amount and volume credit functions.

1『有一个经典重构手法出来了，replace conditional with polymorphism，条件语句转多态。』

我的设想是先建立一个继承体系，它有「喜剧」和「悲剧」两个子类，子类各自包含独立的计算逻辑。调用者通过调用一个多态的 amount 函数，让语言帮你分发到不同的子类的计算过程中。volumeCredits 函数的处理也是如法炮制。为此我需要用到多种重构方法，其中最核心的一招是以多态取代条件表达式（272），将多个同样的类型码分支用多态取代。但在施展以多态取代条件表达式（272）之前，我得先创建一个基本的继承结构。我需要先创建一个类，并将价格计算函数和观众量积分计算函数放进去。

I begin by reviewing the calculation code. (One of the pleasant consequences of the previous refactoring is that I can now ignore the formatting code, so long as I produce the same output data structure. I can further support this by adding tests that probe the intermediate data structure.)

我先从检查计算代码开始。（之前的重构带来的一大好处是，现在我大可以忽略那些格式化代码，只要不改变中转数据结构就行。我可以进一步添加测试来保证中转数据结构不会被意外修改。）

#### 1.8.1 Creating a Performance Calculator

The enrichPerformance function is the key, since it populates the intermediate data structure with the data for each performance. Currently, it calls the conditional functions for amount and volume credits. What I need it to do is call those functions on a host class. Since that class hosts functions for calculating data about performances, I’ll call it a performance calculator.

function createStatementData…

```js
  function enrichPerformance(aPerformance) {
    const calculator = new PerformanceCaluculator(aPerformance);
    const result = Object.assign({}, aPerformance);
    result.play = playFor(result);
    result.amount = amountFor(result);
    result.volumeCredits = volumeCreditsFor(result);
    return result;
  }
```

top level…

```js
class PerformanceCaluculator {
  constructor(aPerformance) {
    this.performance = aPerformance;
  }
}
```

So far, this new object isn’t doing anything. I want to move behavior into it—and I’d like to start with the simplest thing to move, which is the play record. Strictly, I don’t need to do this, as it’s not varying polymorphically, but this way I’ll keep all the data transforms in one place, and that consistency will make the code clearer. To make this work, I will use Change Function Declaration (124) to pass the performance’s play into the calculator.

我希望将函数行为搬移进来，这可以从最容易搬移的东西——play 字段开始。严格来讲，我不需要搬移这个字段，因为它并未体现出多态性，但这样可以把所有数据转换集中到一处地方，保证了代码的一致性和清晰度。为此，我将使用改变函数声明（124）手法将 performance 的 play 字段传给计算器。

function createStatementData…

```js
  function enrichPerformance(aPerformance) {
    const calculator = new PerformanceCaluculator(aPerformance, playFor(aPerformance));
    const result = Object.assign({}, aPerformance);
    result.play = playFor(result);
    result.amount = amountFor(result);
    result.volumeCredits = volumeCreditsFor(result);
    return result;
  }

```

class PerformanceCalculator…

```js
class PerformanceCaluculator {
  constructor(aPerformance, aPlay) {
    this.performance = aPerformance;
    this.play = aPlay;
  }
}
```

(I’m not saying compile-­test-­commit all the time any more, as I suspect you’re getting tired of reading it. But I still do it at every opportunity. I do sometimes get tired of doing it—and give mistakes the chance to bite me. Then I learn and get back into the rhythm.)

#### 1.8.2 Moving Functions into the Calculator

The next bit of logic I move is rather more substantial for calculating the amount for a performance. I’ve moved functions around casually while rearranging nested functions —but this is a deeper change in the context of the function, so I’ll step through the Move Function (198) refactoring. The first part of this refactoring is to copy the logic over to its new context—the calculator class. Then, I adjust the code to fit into its new home, changing aPerformance to this.performance and playFor(aPerformance) to this.play.

我要搬移的下一块逻辑，对计算一场演出的价格 （amount）来说就尤为重要了。在调整嵌套函数的层级时，我经常将函数挪来挪去，但接下来需要改动到更深入的函数上下文，因此我将小心使用搬移函数（198）来重构它。首先，将 amount 函数的逻辑复制一份到新的上下文中， 也就是 PerformanceCalculator 类中。然后微调一下代码， 将 aPerformance 改为 this.performance，将 playFor(aPerformance) 改为 this.play，使代码适应这个新家。

class PerformanceCalculator…

```js
class PerformanceCaluculator {
  constructor(aPerformance, aPlay) {
    this.performance = aPerformance;
    this.play = aPlay;
  }

  get amount() {
    let result = 0;
    switch (this.play.type) {
      case 'tragedy':
        result = 40000;
        if (this.performance.audience > 30) {
          result += 1000 * (this.performance.audience - 30);
        }
        break;
      case 'comedy':
        result = 30000;
        if (this.performance.audience > 20) {
          result += 10000 + 500 * (this.performance.audience -20);
        }
        result += 300 * this.performance.audience;
        break;
      default:
        throw new Error(`unkown type: ${this.play.type}`);
    }
    return result;
  }
}
```

I can compile at this point to check for any compile­time errors. “Compiling” in my development environment occurs as I execute the code, so what I actually do is run Babel [babel]. That will be enough to catch any syntax errors in the new function—but little more than that. Even so, that can be a useful step. Once the new function fits its home, I take the original function and turn it into a delegating function so it calls the new function.

function createStatementData…

```js
  function amountFor(aPerformance) {
    return new PerformanceCaluculator(aPerformance, playFor(aPerformance)).amount;
  }
```

1『这里「new PerformanceCaluculator(aPerformance, playFor(aPerformance)).amount;」调用的是实例化对象的 get 属性值，所以 amount 后面没有括号 ()。』

Now I can compile­-test-­commit to ensure the code is working properly in its new home. With that done, I use Inline Function (115) to call the new function directly (compile-test-­commit).

function createStatementData…

```js
  function enrichPerformance(aPerformance) {
    const calculator = new PerformanceCaluculator(aPerformance, playFor(aPerformance));
    const result = Object.assign({}, aPerformance);
    result.play = calculator.play;
    result.amount = calculator.amount;
    result.volumeCredits = volumeCreditsFor(result);
    return result;
  }
```

1『这是，之前的 function amountFor(aPerformance) {} 函数可以整体删除了，绝妙！』

I repeat the same process to move the volume credits calculation.

function createStatementData…

```js
  function enrichPerformance(aPerformance) {
    const calculator = new PerformanceCaluculator(aPerformance, playFor(aPerformance));
    const result = Object.assign({}, aPerformance);
    result.play = calculator.play;
    result.amount = calculator.amount;
    result.volumeCredits = calculator.volumeCredits;
    return result;
  }
```

class PerformanceCalculator…

```js
  get volumeCredits() {
    let result = 0;
    result += Math.max(this.performance.audience - 30, 0);
    // add extra credit for every ten comedy attendees
    if ('comedy' === this.play.type) {
      result += Math.floor(this.performance.audience / 5);
    }
    return result;
  }
```

#### 1.8.3 Making the Performance Calculator Polymorphic 

Now that I have the logic in a class, it’s time to apply the polymorphism. The first step is to use Replace Type Code with Subclasses (362) to introduce subclasses instead of the type code. For this, I need to create subclasses of the performance calculator and use the appropriate subclass in createPerformanceData. In order to get the right subclass, I need to replace the constructor call with a function, since JavaScript constructors can’t return subclasses. So I use Replace Constructor with Factory Function (334).

我已将全部计算逻辑搬移到一个类中，是时候将它多态化了。第一步是应用以子类取代类型码（362）引入子类， 弃用类型代码。为此，我需要为演出计算器创建子类，并在 createStatementData 中获取对应的子类。要得到正确的子类，我需要将构造函数调用替换为一个普通的函数调用，因为 JavaScript 的构造函数里无法返回子类。于是我使用以工厂函数取代构造函数（334）。

1『新获取的重构手法：用子类取代类型码（Replace Type Code with Subclasses）。』

function createStatementData… 

```js
  function enrichPerformance(aPerformance) {
    const calculator = createPerformanceCalculator(aPerformance, playFor(aPerformance));
    const result = Object.assign({}, aPerformance);
    result.play = calculator.play;
    result.amount = calculator.amount;
    result.volumeCredits = calculator.volumeCredits;
    return result;
  }
```

top level…

```js
function createPerformanceCalculator(aPerformance, aPlay) {
  return new PerformanceCaluculator(aPerformance, aPlay);
}
```

With that now a function, I can create subclasses of the performance calculator and get the creation function to select which one to return.

top level…

```js
function createPerformanceCalculator(aPerformance, aPlay) {
  switch(aPlay.type) {
    case 'tragedy': return new TragedyCalculator(aPerformance, aPlay);
    case 'comedy': return new ComedyCalculator(aPerformance, aPlay);
    default:
      throw new Error(`unknown type: ${aPlay.type}`);
  }
}
```

This sets up the structure for the polymorphism, so I can now move on to Replace Conditional with Polymorphism (272). I start with the calculation of the amount for tragedies.

class TragedyCalculator…

```js
class TragedyCalculator extends PerformanceCaluculator {
  get amount() {
    let result = 40000;
    if (this.performance.audience > 30) {
      result += 1000 * (this.performance.audience - 30);
    }
    return result;
  }
}
```

Just having this method in the subclass is enough to override the superclass conditional. But if you’re as paranoid as I am, you might do this:

class PerformanceCalculator…

```js
  get amount() {
    let result = 0;
    switch (this.play.type) {
      case 'tragedy':
        throw 'bad thing';
      case 'comedy':
        result = 30000;
        if (this.performance.audience > 20) {
          result += 10000 + 500 * (this.performance.audience -20);
        }
        result += 300 * this.performance.audience;
        break;
      default:
        throw new Error(`unkown type: ${this.play.type}`);
    }
    return result;
  }
```

I could have removed the case for tragedy and let the default branch throw an error. But I like the explicit throw—and it will only be there for a couple more minutes (which is why I threw a string, not a better error object). After a compile­-test-­commit of that, I move the comedy case down too.

class ComedyCalculator…

```js
class ComedyCalculator extends PerformanceCaluculator {
  get amount() {
    let result = 30000;
    if (this.performance.audience > 20) {
      result += 10000 + 500 * (this.performance.audience -20);
    }
    result += 300 * this.performance.audience;
    return result;
  }
}
```

I can now remove the superclass amount method, as it should never be called. But it’s kinder to my future self to leave a tombstone.

class PerformanceCalculator…

```js
get amount() { throw new Error('subclass responsibility'); }
```

The next conditional to replace is the volume credits calculation. Looking at the discussion of future categories of plays, I notice that most plays expect to check if audience is above 30, with only some categories introducing a variation. So it makes sense to leave the more common case on the superclass as a default, and let the variations override it as necessary. So I just push down the case for comedies:

下一个要替换的条件表达式是观众量积分的计算。我回顾了一下前面关于未来戏剧类型的讨论，发现大多数剧类在计算积分时都会检查观众数是否达到 30，仅一小部分品类有所不同。因此，将更为通用的逻辑放到超类作为默认条件， 出现特殊场景时按需覆盖它，听起来十分合理。于是我将一部分喜剧的逻辑下移到子类。

class PerformanceCalculator…

```js
class PerformanceCaluculator {
  constructor(aPerformance, aPlay) {
    this.performance = aPerformance;
    this.play = aPlay;
  }

  get amount() {
    throw new Error('subclass responsibility');
  }

  get volumeCredits() {
    return Math.max(this.performance.audience - 30, 0);
  }
}
```

class ComedyCalculator…

```js
class ComedyCalculator extends PerformanceCaluculator {
  get amount() {
    let result = 30000;
    if (this.performance.audience > 20) {
      result += 10000 + 500 * (this.performance.audience -20);
    }
    result += 300 * this.performance.audience;
    return result;
  }
  get volumeCredits() {
    return super.volumeCredits + Math.floor(this.performance.audience / 5);
  }
}
```

### 1.9 Status: Creating the Data with the Polymorphic Calculator

Time to reflect on what introducing the polymorphic calculator did to the code.

createStatementData.js

```js
export default function createStatementData(invoice, plays) {
  const result = {};
  result.customer = invoice.customer;
  result.performances = invoice.performances.map(enrichPerformance);
  result.totalAmount = totalAmount(result);
  result.totalVolumeCredits = totalVolumeCredits(result);
  return result;

  function enrichPerformance(aPerformance) {
    const calculator = createPerformanceCalculator(aPerformance, playFor(aPerformance));
    const result = Object.assign({}, aPerformance);
    result.play = calculator.play;
    result.amount = calculator.amount;
    result.volumeCredits = calculator.volumeCredits;
    return result;
  }

  function playFor(aPerformance) {
    return plays[aPerformance.playID];
  }

  function totalAmount(data) {
    return data.performances
      .reduce((total, p) => total + p.amount, 0);
  }

  function totalVolumeCredits(data) {
    return data.performances
      .reduce((total, p) => total + p.volumeCredits, 0);
  }
}

function createPerformanceCalculator(aPerformance, aPlay) {
  switch(aPlay.type) {
    case 'tragedy': return new TragedyCalculator(aPerformance, aPlay);
    case 'comedy': return new ComedyCalculator(aPerformance, aPlay);
    default:
      throw new Error(`unknown type: ${aPlay.type}`);
  }
}

class PerformanceCaluculator {
  constructor(aPerformance, aPlay) {
    this.performance = aPerformance;
    this.play = aPlay;
  }

  get amount() {
    throw new Error('subclass responsibility');
  }

  get volumeCredits() {
    return Math.max(this.performance.audience - 30, 0);
  }
}

class TragedyCalculator extends PerformanceCaluculator {
  get amount() {
    let result = 40000;
    if (this.performance.audience > 30) {
      result += 1000 * (this.performance.audience - 30);
    }
    return result;
  }
}

class ComedyCalculator extends PerformanceCaluculator {
  get amount() {
    let result = 30000;
    if (this.performance.audience > 20) {
      result += 10000 + 500 * (this.performance.audience -20);
    }
    result += 300 * this.performance.audience;
    return result;
  }
  get volumeCredits() {
    return super.volumeCredits + Math.floor(this.performance.audience / 5);
  }
}
```

Again, the code has increased in size as I’ve introduced structure. The benefit here is that the calculations for each kind of play are grouped together. If most of the changes will be to this code, it will be helpful to have it clearly separated like this. Adding a new kind of play requires writing a new subclass and adding it to the creation function. The example gives some insight as to when using subclasses like this is useful. Here, I’ve moved the conditional lookup from two functions (amountFor and volumeCreditsFor) to a single constructor function createPerformanceCalculator. The more functions there are that depend on the same type of polymorphism, the more useful this approach becomes.

代码量仍然有所增加，因为我再次整理了代码结构。新结构带来的好处是，不同戏剧种类的计算各自集中到了一处地方。如果大多数修改都涉及特定类型的计算，像这样按类型进行分离就很有意义。当添加新剧种时，只需要添加一个子类，并在创建函数中返回它。这个示例还揭示了一些关于此类继承方案何时适用的洞见。上面我将条件分支的查找从两个不同的函数（amountFor 和 volumeCreditsFor）搬移到一个集中的构造函数 createPerformanceCalculator 中。有越多的函数依赖于同一套类型进行多态，这种继承方案就越有益处。

An alternative to what I’ve done here would be to have createPerformanceData return the calculator itself, instead of the calculator populating the intermediate data structure. One of the nice features of JavaScript’s class system is that with it, using getters looks like regular data access. My choice on whether to return the instance or calculate separate output data depends on who is using the downstream data structure. In this case, I preferred to show how to use the intermediate data structure to hide the decision to use a polymorphic calculator.

除了这样设计，还有另一种可能的方案，那就是让 createStatementData 返回计算器实例本身，而非自己拿到计算器来填充中转数据结构。JavaScript 的类设计有不少好特性，例如，取值函数用起来就像普通的数据存取。我在考量是「直接返回实例本身」还是「返回计算好的中转数据」时，主要看数据的使用者是谁。在这个例子中，我更想通过中转数据结构来展示如何以此隐藏计算器背后的多态设计。

## 0201. Principles in Refactoring

The example in the previous chapter should have given you a decent feel of what refactoring is. Now you have that, it’s a good time to step back and talk about some of the broader principles in refactoring.

### 2.1 Defining Refactoring

Like many terms in software development, “refactoring” is often used very loosely by Settings practitioners. I use the term more precisely, and find it useful to use it in that more precise form. (These definitions are the same as those I gave in the first edition of this Support book.) The term “refactoring” can be used either as a noun or a verb. 

Refactoring (noun): a change made to the internal structure of software to make it easier to understand and cheaper to modify without changing its observable behavior. This definition corresponds to the named refactorings I’ve mentioned in the earlier examples, such as Extract Function (106) and Replace Conditional with Polymorphism (272).

Refactoring (verb): to restructure software by applying a series of refactorings without changing its observable behavior.

重构（名词）：对软件内部结构的一种调整，目的是在不改变软件可观察行为的前提下，提高其可理解性，降低其修改成本。重构（动词）：使用一系列重构手法，在不改变软件可观察行为的前提下，调整其结构。

2『重构的概念，做一张术语卡片。』——已完成

So I might spend a couple of hours refactoring, during which I would apply a few dozen individual refactorings.

Over the years, many people in the industry have taken to use “refactoring” to mean any kind of code cleanup—but the definitions above point to a particular approach to cleaning up code. Refactoring is all about applying small behavior­preserving steps and making a big change by stringing together a sequence of these behavior-­preserving steps. Each individual refactoring is either pretty small itself or a combination of small steps. As a result, when I’m refactoring, my code doesn’t spend much time in a broken state, allowing me to stop at any moment even if I haven’t finished. If someone says their code was broken for a couple of days while they are refactoring, you can be pretty sure they were not refactoring.

过去十几年，这个行业里的很多人用「重构」这个词来指代任何形式的代码清理，但上面的定义所指的是一种特定的清理代码的方式。重构的关键在于运用大量微小且保持软件行为的步骤，一步步达成大规模的修改。每个单独的重构要么很小，要么由若干小步骤组合而成。因此，在重构的过程中，我的代码很少进入不可工作的状态，即便重构没有完成，我也可以在任何时刻停下来。如果有人说他们的代码在重构过程中有一两天时间不可用，基本上可以确定，他们在做的事不是重构。

I use “restructuring” as a general term to mean any kind of reorganizing or cleaning up of a code base, and see refactoring as a particular kind of restructuring. Refactoring may seem inefficient to people who first come across it and watch me making lots of tiny steps, when a single bigger step would do. But the tiny steps allow me to go faster because they compose so well—and, crucially, because I don’t spend any time debugging.

我会用「结构调整」（restructuring）来泛指对代码库进行的各种形式的重新组织或清理，重构则是特定的一类结构调整。刚接触重构的人看我用很多小步骤完成似乎可以一大步就能做完的事，可能会觉得这样很低效。但小步前进能让我走得更快，因为这些小步骤能完美地彼此组合，而且——更关键的是——整个过程中我不会花任何时间来调试。

In my definitions, I use the phrase “observable behavior.” This is a deliberately loose term, indicating that the code should, overall, do just the same things it did before I started. It doesn’t mean it will work exactly the same—for example, Extract Function (106) will alter the call stack, so performance characteristics might change—but nothing should change that the user should care about. In particular, interfaces to modules often change due to such refactorings as Change Function Declaration (124) and Move Function (198). Any bugs that I notice during refactoring should still be present after refactoring (though I can fix latent bugs that nobody has observed yet).

在上述定义中，我用了「可观察行为」的说法。它的意思是，整体而言，经过重构之后的代码所做的事应该与重构之前大致一样。这个说法并非完全严格，并且我是故意保留这点儿空间的：重构之后的代码不一定与重构前行为完全一致。比如说，提炼函数（106）会改变函数调用栈，因此程序的性能就会有所改变；改变函数声明（124）和搬移函数 （198）等重构经常会改变模块的接口。不过就用户应该关心的行为而言，不应该有任何改变。如果我在重构过程中发现了任何 bug，重构完成后同样的 bug 应该仍然存在（不过，如果潜在的 bug 还没有被任何人发现，也可以当即把它改掉）。

Refactoring is very similar to performance optimization, as both involve carrying out code manipulations that don’t change the overall functionality of the program. The difference is the purpose: Refactoring is always done to make the code “easier to understand and cheaper to modify.” This might speed things up or slow things down. With performance optimization, I only care about speeding up the program, and am prepared to end up with code that is harder to work with if I really need that improved performance.

重构与性能优化有很多相似之处：两者都需要修改代码，并且两者都不会改变程序的整体功能。两者的差别在于其目的：重构是为了让代码「更容易理解，更易于修改」。 这可能使程序运行得更快，也可能使程序运行得更慢。在性能优化时，我只关心让程序运行得更快，最终得到的代码有可能更难理解和维护，对此我有心理准备。

### 2.2 The Two Hats

Kent Beck came up with a metaphor of the two hats. When I use refactoring to develop software, I divide my time between two distinct activities: adding functionality and refactoring. When I add functionality, I shouldn’t be changing existing code; I’m just adding new capabilities. I measure my progress by adding tests and getting the tests to work. When I refactor, I make a point of not adding functionality; I only restructure the code. I don’t add any tests (unless I find a case I missed earlier); I only change tests when I have to accommodate a change in an interface.

KentBeck 提出了「两顶帽子」的比喻。使用重构技术开发软件时，我把自己的时间分配给两种截然不同的行为：添加新功能和重构。添加新功能时，我不应该修改既有代码，只管添加新功能。通过添加测试并让测试正常运行，我可以衡量自己的工作进度。重构时我就不能再添加功能，只管调整代码的结构。此时我不应该添加任何测试（除非发现有先前遗漏的东西），只在绝对必要（用以处理接口变化）时才修改测试。

1『两顶帽子，做一张术语卡片。』——已完成

As I develop software, I find myself swapping hats frequently. I start by trying to add a new capability, then I realize this would be much easier if the code were structured differently. So I swap hats and refactor for a while. Once the code is better structured, I swap hats back and add the new capability. Once I get the new capability working, I realize I coded it in a way that’s awkward to understand, so I swap hats again and refactor. All this might take only ten minutes, but during this time I’m always aware of which hat I’m wearing and the subtle difference that makes to how I program.

软件开发过程中，我可能会发现自己经常变换帽子。首先我会尝试添加新功能，然后会意识到：如果把程序结构改一下，功能的添加会容易得多。于是我换一顶帽子，做一会儿重构工作。程序结构调整好后，我又换上原先的帽子，继续添加新功能。新功能正常工作后，我又发现自己的编码造成程序难以理解，于是又换上重构帽子……整个过程或许只花 10 分钟，但无论何时我都清楚自己戴的是哪一顶帽子，并且明白不同的帽子对编程状态提出的不同要求。

### 2.3 Why Should We Refactor?

I don’t want to claim refactoring is the cure for all software ills. It is no “silver bullet.” Yet it is a valuable tool—a pair of silver pliers that helps you keep a good grip on your code. Refactoring is a tool that can—and should—be used for several purposes.

#### 2.3.1 Refactoring Improves the Design of Software

Without refactoring, the internal design—the architecture—of software tends to decay. As people change code to achieve short-­term goals, often without a full comprehension of the architecture, the code loses its structure. It becomes harder for me to see the design by reading the code. Loss of the structure of code has a cumulative effect. The harder it is to see the design in the code, the harder it is for me to preserve it, and the more rapidly it decays. Regular refactoring helps keep the code in shape.

如果没有重构，程序的内部设计（或者叫架构）会逐渐腐败变质。当人们只为短期目的而修改代码时，他们经常没有完全理解架构的整体设计，于是代码逐渐失去了自己的结构。程序员越来越难通过阅读源码来理解原来的设计。代码结构的流失有累积效应。越难看出代码所代表的设计意图，就越难保护其设计，于是设计就腐败得越快。经常性的重构有助于代码维持自己该有的形态。

Poorly designed code usually takes more code to do the same things, often because the code quite literally does the same thing in several places. Thus an important aspect of improving design is to eliminate duplicated code. It’s not that reducing the amount of code will make the system run any faster—the effect on the footprint of the programs rarely is significant. Reducing the amount of code does, however, make a big difference in modification of the code. The more code there is, the harder it is to modify correctly. There’s more code for me to understand. I change this bit of code here, but the system doesn’t do what I expect because I didn’t change that bit over there that does much the same thing in a slightly different context. By eliminating duplication, I ensure that the code says everything once and only once, which is the essence of good design.

完成同样一件事，设计欠佳的程序往往需要更多代码，这常常是因为代码在不同的地方使用完全相同的语句做同样的事，因此改进设计的一个重要方向就是消除重复代码。代码量减少并不会使系统运行更快，因为这对程序的资源占用几乎没有任何明显影响。然而代码量减少将使未来可能的程序修改动作容易得多。代码越多，做正确的修改就越困难，因为有更多代码需要理解。我在这里做了点儿修改，系统却不如预期那样工作，因为我没有修改另一处——那里的代码做着几乎完全一样的事情，只是所处环境略有不同。消除重复代码，我就可以确定所有事物和行为在代码中只表述一次，这正是优秀设计的根本。

1『又见消除重复代码，牢记牢记。』

#### 2.3.2 Refactoring Makes Software Easier to Understand

Programming is in many ways a conversation with a computer. I write code that tells the computer what to do, and it responds by doing exactly what I tell it. In time, I close the gap between what I want it to do and what I tell it to do. Programming is all about saying exactly what I want. But there are likely to be other users of my source code. In a few months, a human will try to read my code to make some changes. That user, who we often forget, is actually the most important. Who cares if the computer takes a few more cycles to compile something? Yet it does matter if it takes a programmer a week to make a change that would have taken only an hour with proper understanding of my code.

所谓程序设计，很大程度上就是与计算机对话：我编写代码告诉计算机做什么事，而它的响应是按照我的指示精确行动。一言以蔽之，我所做的就是填补「我想要它做什么」和「我告诉它做什么」之间的缝隙。编程的核心就在于「准确说出我想要的」。然而别忘了，除了计算机外，源码还有其他读者：几个月之后可能会有另一位程序员尝试读懂我的代码并对其做一些修改。我们很容易忘记这这位读者，但他才是最重要的。计算机是否多花了几个时钟周期来编译，又有什么关系呢？如果一个程序员花费一周时间来修改某段代码，那才要命呢——如果他理解了我的代码，这个修改原本只需一小时。

The trouble is that when I’m trying to get the program to work, I’m not thinking about that future developer. It takes a change of rhythm to make the code easier to understand. Refactoring helps me make my code more readable. Before refactoring, I have code that works but is not ideally structured. A little time spent on refactoring can make the code better communicate its purpose—say more clearly what I want.

问题在于，当我努力让程序运转的时候，我不会想到未来出现的那个开发者。是的，我们应该改变一下开发节奏，让代码变得更易于理解。重构可以帮我让代码更易读。开始进行重构前，代码可以正常运行，但结构不够理想。在重构上花一点点时间，就可以让代码更好地表达自己的意图—更清晰地说出我想要做的。

I’m not necessarily being altruistic about this. Often, this future developer is myself. This makes refactoring even more important. I’m a very lazy programmer. One of my forms of laziness is that I never remember things about the code I write. Indeed, I deliberately try not remember anything I can look up, because I’m afraid my brain will get full. I make a point of trying to put everything I should remember into the code so I don’t have to remember it. That way I’m less worried about Maudite [maudite] killing off my brain cells.

关于这一点，我没必要表现得多么无私。很多时候那个未来的开发者就是我自己。此时重构就显得尤其重要了。我是一个很懒惰的程序员，我的懒惰表现形式之一就是：总是记不住自己写过的代码。事实上，对于任何能够立刻查阅的东西，我都故意不去记它，因为我怕把自己的脑袋塞爆。我总是尽量把该记住的东西写进代码里，这样我就不必记住它了。这么一来，下班后我还可以喝上两杯 Maudite 啤酒，不必太担心它杀光我的脑细胞。

#### 2.3.3 Refactoring Helps Me Find Bugs

Help in understanding the code also means help in spotting bugs. I admit I’m not terribly good at finding bugs. Some people can read a lump of code and see bugs; I cannot. However, I find that if I refactor code, I work deeply on understanding what the code does, and I put that new understanding right back into the code. By clarifying the structure of the program, I clarify certain assumptions I’ve made—to a point where even I can’t avoid spotting the bugs.

It reminds me of a statement Kent Beck often makes about himself: “I’m not a great programmer; I’m just a good programmer with great habits.” Refactoring helps me be much more effective at writing robust code.

对代码的理解，可以帮我找到bug。我承认我不太擅长找 bug。有些人只要盯着一大段代码就可以找出里面的 bug，我不行。但我发现，如果对代码进行重构，我就可以深入理解代码的所作所为，并立即把新的理解反映在代码当中。搞清楚程序结构的同时，我也验证了自己所做的一些假设，于是想不把 bug 揪出来都难。这让我想起了 Kent Beck 经常形容自己的一句话：「我不是一个特别好的程序员，我只是一个有着一些特别好的习惯的还不错的程序员。」重构能够帮助我更有效地写出健壮的代码。

#### 2.3.4 Refactoring Helps Me Program Faster

In the end, all the earlier points come down to this: Refactoring helps me develop code more quickly. This sounds counterintuitive. When I talk about refactoring, people can easily see that it improves quality. Better internal design, readability, reducing bugs—all these improve quality. But doesn’t the time I spend on refactoring reduce the speed of development?

When I talk to software developers who have been working on a system for a while, I often hear that they were able to make progress rapidly at first, but now it takes much longer to add new features. Every new feature requires more and more time to understand how to fit it into the existing code base, and once it’s added, bugs often crop up that take even longer to fix. The code base starts looking like a series of patches covering patches, and it takes an exercise in archaeology to figure out how things work. This burden slows down adding new features—to the point that developers wish they could start again from a blank slate. I can visualize this state of affairs with the following pseudograph:

当我跟那些在一个系统上工作较长时间的软件开发者交谈时，经常会听到这样的故事：一开始他们进展很快，但如今想要添加一个新功能需要的时间就要长得多。他们需要花越来越多的时间去考虑如何把新功能塞进现有的代码库，不断蹦出来的 bug 修复起来也越来越慢。代码库看起来就像补丁摞补丁，需要细致的考古工作才能弄明白整个系统是如何工作的。这份负担不断拖慢新增功能的速度，到最后程序员恨不得从头开始重写整个系统。

But some teams report a different experience. They find they can add new features faster because they can leverage the existing things by quickly building on what’s already there. The difference between these two is the internal quality of the software. Software with a good internal design allows me to easily find how and where I need to make changes to add a new feature. Good modularity allows me to only have to understand a small subset of the code base to make a change. If the code is clear, I’m less likely to introduce a bug, and if I do, the debugging effort is much easier. Done well, my code base turns into a platform for building new features for its domain.

但有些团队的境遇则截然不同。他们添加新功能的速度越来越快，因为他们能利用已有的功能，基于已有的功能快速构建新功能。两种团队的区别就在于软件的内部质量。需要添加新功能时，内部质量良好的软件让我可以很容易找到在哪里修改、如何修改。良好的模块划分使我只需要理解代码库的一小部分，就可以做出修改。如果代码很清晰，我引入 bug 的可能性就会变小，即使引入了 bug，调试也会容易得多。理想情况下，我的代码库会逐步演化成一个平台，在其上可以很容易地构造与其领域相关的新功能。

I refer to this effect as the Design Stamina Hypothesis [mf­dsh]: By putting our effort into a good internal design, we increase the stamina of the software effort, allowing us to go faster for longer. I can’t prove that this is the case, which is why I refer to it as a hypothesis. But it explains my experience, together with the experience of hundreds of great programmers that I’ve got to know over my career.

我把这种现象称为「设计耐久性假说」：通过投入精力改善内部设计，我们增加了软件的耐久性，从而可以更长时间地保持开发的快速。我还无法科学地证明这个理论，所以我说它是一个「假说」。但我的经验，以及我在职业生涯中认识的上百名优秀程序员的经验，都支持这个假说。

Twenty years ago, the conventional wisdom was that to get this kind of good design, it had to be completed before starting to program—because once we wrote the code, we could only face decay. Refactoring changes this picture. We now know we can improve the design of existing code—so we can form and improve a design over time, even as the needs of the program change. Since it is very difficult to do a good design up front, refactoring becomes vital to achieving that virtuous path of rapid functionality.

20 年前，行业的陈规认为：良好的设计必须在开始编程之前完成，因为一旦开始编写代码，设计就只会逐渐腐败。重构改变了这个图景。现在我们可以改善已有代码的设计，因此我们可以先做一个设计，然后不断改善它，哪怕程序本身的功能也在不断发生着变化。由于预先做出良好的设计非常困难，想要既体面又快速地开发功能，重构必不可少。

### 2.4 When Should We Refactor?

Refactoring is something I do every hour I program. I have noticed a number of ways it fits into my workflow. 

The Rule of Three:

Here’s a guideline Don Roberts gave me: The first time you do something, you just do it. The second time you do something similar, you wince at the duplication, but you do the duplicate thing anyway. The third time you do something similar, you refactor. Or for those who like baseball: Three strikes, then you refactor.

Don Roberts 给了我一条准则：第一次做某件事时只管去做；第二次做类似的事会产生反感，但无论如何还是可以去做；第三次再做类似的事，你就应该重构。正如老话说的：事不过三，三则重构。

2『重构时机三原则，做一张任意卡片。』——已完成

#### 2.4.1 Preparatory Refactoring—Making It Easier to Add a Feature

The best time to refactor is just before I need to add a new feature to the code base. As I do this, I look at the existing code and, often, see that if it were structured a little differently, my work would be much easier. Perhaps there’s function that does almost all that I need, but has some literal values that conflict with my needs. Without refactoring I might copy the function and change those values. But that leads to duplicated code—if I need to change it in the future, I’ll have to change both spots (and, worse, find them). And copy­paste won’t help me if I need to make a similar variation for a new feature in the future. So with my refactoring hat on, I use Parameterize Function (310). Once I’ve done that, all I have to do is call the function with the parameters I need.

重构的最佳时机就在添加新功能之前。在动手添加新功能之前，我会看看现有的代码库，此时经常会发现：如果对代码结构做一点微调，我的工作会容易得多。也许已经有个函数提供了我需要的大部分功能，但有几个字面量的值与我的需要略有冲突。如果不做重构，我可能会把整个函数复制过来，修改这几个值，但这就会导致重复代码——如果将来我需要做修改，就必须同时修改两处（更麻烦的是，我得先找到这两处）。而且，如果将来我还需要一个类似又略有不同的功能，就只能再复制粘贴一次，这可不是个好主意。所以我戴上重构的帽子，使用函数参数化（310）。做完这件事以后，接下来我就只需要调用这个函数，传入我需要的参数。

“It’s like I want to go 100 miles east but instead of just traipsing through the woods, I’m going to drive 20 miles north to the highway and then I’m going to go 100 miles east at three times the speed I could have if I just went straight there. When people are pushing you to just go straight there, sometimes you need to say, ‘Wait, I need to check the map and find the quickest route.’ The preparatory refactoring does that for me.” — Jessica Kerr

这就好像我要往东去 100 公里。我不会往东一头把车开进树林，而是先往北开 20 公里上高速，然后再向东开 100 公里。后者的速度比前者要快上 3 倍。如果有人催着你「赶快直接去那儿」，有时你需要说：「等等，我要先看看地图，找出最快的路径。」这就是预备性重构于我的意义。

1『 Fowler 大师的这个隐喻真好。』

The same happens when fixing a bug. Once I’ve found the cause of the problem, I see that it would be much easier to fix should I unify the three bits of copied code causing the error into one. Or perhaps separating some update logic from queries will make it easier to avoid the tangling that’s causing the error. By refactoring to improve the situation, I also increase the chances that the bug will stay fixed, and reduce the chances that others will appear in the same crevices of the code.

修复 bug 时的情况也是一样。在寻找问题根因时，我可能会发现：如果把 3 段一模一样且都会导致错误的代码合并到一处，问题修复起来会容易得多。或者，如果把某些更新数据的逻辑与查询逻辑分开，会更容易避免造成错误的逻辑纠缠。用重构改善这些情况，在同样场合再次出现同样 bug 的概率也会降低。

#### 2.4.2 Comprehension Refactoring: Making Code Easier to Understand 

Before I can change some code, I need to understand what it does. This code may have been written by me or by someone else. Whenever I have to think to understand what the code is doing, I ask myself if I can refactor the code to make that understanding more immediately apparent. I may be looking at some conditional logic that’s structured awkwardly. I may have wanted to use some existing functions but spent several minutes figuring out what they did because they were named badly.

我需要先理解代码在做什么，然后才能着手修改。这段代码可能是我写的，也可能是别人写的。一旦我需要思考「这段代码到底在做什么」，我就会自问：能不能重构这段代码，令其一目了然？我可能看见了一段结构糟糕的条件逻辑，也可能希望复用一个函数，但花费了几分钟才弄懂它到底在做什么，因为它的函数命名实在是太糟糕了。这些都是重构的机会。

At that point I have some understanding in my head, but my head isn’t a very good record of such details. As Ward Cunningham puts it, by refactoring I move the understanding from my head into the code itself. I then test that understanding by running the software to see if it still works. If I move my understanding into the code, it will be preserved longer and be visible to my colleagues.

看代码时，我会在脑海里形成一些理解，但我的记性不好，记不住那么多细节。正如 Ward Cunningham 所说，通过重构，我就把脑子里的理解转移到了代码本身。随后我运行这个软件，看它是否正常工作，来检查这些理解是否正确。如果把对代码的理解植入代码中，这份知识会保存得更久，并且我的同事也能看到。

That doesn’t just help me in the future—it often helps me right now. Early on, I do comprehension refactoring on little details. I rename a couple variables now that I understand what they are, or I chop a long function into smaller parts. Then, as the code gets clearer, I find I can see things about the design that I could not see before. Had I not changed the code, I probably never would have seen these things, because I’m just not clever enough to visualize all these changes in my head. Ralph Johnson describes these early refactorings as wiping the dirt off a window so you can see beyond. When I’m studying code, refactoring leads me to higher levels of understanding that I would otherwise miss. Those who dismiss comprehension refactoring as useless fiddling with the code don’t realize that by foregoing it they never see the opportunities hidden behind the confusion.

重构带来的帮助不仅发生在将来——常常是立竿见影。我会先在一些小细节上使用重构来帮助理解，给一两个变量改名，让它们更清楚地表达意图，以方便理解，或是将一个长函数拆成几个小函数。当代码变得更清晰一些时，我就会看见之前看不见的设计问题。如果不做前面的重构，我可能永远都看不见这些设计问题，因为我不够聪明，无法在脑海中推演所有这些变化。Ralph Johnson 说，这些初步的重构就像扫去窗上的尘埃，使我们得以看到窗外的风景。在研读代码时，重构会引领我获得更高层面的理解，如果只是阅读代码很难有此领悟。有些人以为这些重构只是毫无意义地把玩代码，他们没有意识到，缺少了这些细微的整理，他们就无法看到隐藏在一片混乱背后的机遇。

#### 2.4.3 Litter-Pickup Refactoring

A variation of comprehension refactoring is when I understand what the code is doing, but realize that it’s doing it badly. The logic is unnecessarily convoluted, or I see functions that are nearly identical and can be replaced by a single parameterized function. There’s a bit of a tradeoff here. I don’t want to spend a lot of time distracted from the task I’m currently doing, but I also don’t want to leave the trash lying around and getting in the way of future changes. If it’s easy to change, I’ll do it right away. If it’s a bit more effort to fix, I might make a note of it and fix it when I’m done with my immediate task.

帮助理解的重构还有一个变体：我已经理解代码在做什么，但发现它做得不好，例如逻辑不必要地迂回复杂，或者两个函数几乎完全相同，可以用一个参数化的函数取而代之。这里有一个取舍：我不想从眼下正要完成的任务上跑题太多，但我也不想把垃圾留在原地，给将来的修改增加麻烦。如果我发现的垃圾很容易重构，我会马上重构它；如果重构需要花一些精力，我可能会拿一张便笺纸把它记下来，完成当下的任务再回来重构它。

Sometimes, of course, it’s going to take a few hours to fix, and I have more urgent things to do. Even then, however, it’s usually worthwhile to make it a little bit better. As the old camping adage says, always leave the camp site cleaner than when you found it. If I make it a little better each time I pass through the code, over time it will get fixed. The nice thing about refactoring is that I don’t break the code with each small step—so, sometimes, it takes months to complete the job but the code is never broken even when I’m part way through it.

当然，有时这样的垃圾需要好几个小时才能解决，而我又有更紧急的事要完成。不过即便如此，稍微花一点工夫做一点儿清理，通常都是值得的。正如野营者的老话所说：至少要让营地比你到达时更干净。如果每次经过这段代码时都把它变好一点点，积少成多，垃圾总会被处理干净。重构的妙处就在于，每个小步骤都不会破坏代码——所以，有时一块垃圾在好几个月之后才终于清理干净，但即便每次清理并不完整，代码也不会被破坏。

#### 2.4.4 Planned and Opportunistic Refactoring

The examples above—preparatory, comprehension, litter­pickup refactoring—are all opportunistic. I don’t set aside time at the beginning to spend on refactoring—instead, I do refactoring as part of adding a feature or fixing a bug. It’s part of my natural flow of programming. Whether I’m adding a feature or fixing a bug, refactoring helps me do the immediate task and also sets me up to make future work easier. This is an important point that’s frequently missed. Refactoring isn’t an activity that’s separated from programming—any more than you set aside time to write if statements. I don’t put time on my plans to do refactoring; most refactoring happens while I’m doing other things.

You have to refactor when you run into ugly code—but excellent code needs plenty of refactoring too.

上面的例子——预备性重构、帮助理解的重构、捡垃圾式重构——都是见机行事的：我并不专门安排一段时间来重构，而是在添加功能或修复 bug 的同时顺便重构。这是我自然的编程流的一部分。不管是要添加功能还是修复 bug，重构对我当下的任务有帮助，而且让我未来的工作更轻松。这是一件很重要而又常被误解的事：重构不是与编程割裂的行为。你不会专门安排时间重构，正如你不会专门安排时间写 if 语句。我的项目计划上没有专门留给重构的时间，绝大多数重构都在我做其他事的过程中自然发生。肮脏的代码必须重构，但漂亮的代码也需要很多重构。

It’s also a common error to see refactoring as something people do to fix past mistakes or clean up ugly code. Certainly you have to refactor when you run into ugly code, but excellent code needs plenty of refactoring too. Whenever I write code, I’m making tradeoffs—how much do I need to parameterize, where to draw the lines between functions? The tradeoffs I made correctly for yesterday’s feature set may no longer be the right ones for the new features I’m adding today. The advantage is that clean code is easier to refactor when I need to change those tradeoffs to reflect the new reality.

还有一种常见的误解认为，重构就是人们弥补过去的错误或者清理肮脏的代码。当然，如果遇上了肮脏的代码，你必须重构，但漂亮的代码也需要很多重构。在写代码时，我会做出很多权衡取舍：参数化需要做到什么程度？函数之间的边界应该划在哪里？对于昨天的功能完全合理的权衡，在今天要添加新功能时可能就不再合理。好在，当我需要改变这些权衡以反映现实情况的变化时，整洁的代码重构起来会更容易。

“for each desired change, make the change easy (warning: this may be hard), then make the easy change.” — Kent Beck

每次要修改时，首先令修改很容易（警告：这件事有时会很难），然后再进行这次容易的修改。——Kent Beck

2『做一张金句卡片。』——已完成

For a long time, people thought of writing software as a process of accretion: To add new features, we should be mostly adding new code. But good developers know that, often, the fastest way to add a new feature is to change the code to make it easy to add. Software should thus be never thought of as “done.” As new capabilities are needed, the software changes to reflect that. Those changes can often be greater in the existing code than in the new code.

长久以来，人们认为编写软件是一个累加的过程：要添加新功能，我们就应该增加新代码。但优秀的程序员知道，添加新功能最快的方法往往是先修改现有的代码，使新功能容易被加入。所以，软件永远不应该被视为「完成」。每当需要新能力时，软件就应该做出相应的改变。越是在已有代码中，这样的改变就越显重要。

All this doesn’t mean that planned refactoring is always wrong. If a team has neglected refactoring, it often needs dedicated time to get their code base into a better state for new features, and a week spent refactoring now can repay itself over the next couple of months. Sometimes, even with regular refactoring I’ll see a problem area grow to the point when it needs some concerted effort to fix. But such planned refactoring episodes should be rare. Most refactoring effort should be the unremarkable, opportunistic kind.

不过，说了这么多，并不表示有计划的重构总是错的。如果团队过去忽视了重构，那么常常会需要专门花一些时间来优化代码库，以便更容易添加新功能。在重构上花一个星期的时间，会在未来几个月里发挥价值。有时，即便团队做了日常的重构，还是会有问题在某个区域逐渐累积长大，最终需要专门花些时间来解决。但这种有计划的重构应该很少，大部分重构应该是不起眼的、见机行事的。

One bit of advice I’ve heard is to separate refactoring work and new feature additions into different version-­control commits. The big advantage of this is that they can be reviewed and approved independently. I’m not convinced of this, however. Too often, the refactorings are closely interwoven with adding new features, and it’s not worth the time to separate them out. This can also remove the context for the refactoring, making the refactoring commits hard to justify. Each team should experiment to find what works for them; just remember that separating refactoring commits is not a self­evident principle—it’s only worthwhile if it makes life easier.

我听过的一条建议是：将重构与添加新功能在版本控制的提交中分开。这样做的一大好处是可以各自独立地审阅和批准这些提交。但我并不认同这种做法。重构常常与新添功能紧密交织，不值得花工夫把它们分开。并且这样做也使重构脱离了上下文，使人看不出这些「重构提交」的价值。每个团队应该尝试并找出适合自己的工作方式，只是要记住：分离重构提交并不是毋庸置疑的原则，只有当你真的感到有益时，才值得这样做。

#### 2.4.5 Long-Term Refactoring

Most refactoring can be completed within a few minutes—hours at most. But there are some larger refactoring efforts that can take a team weeks to complete. Perhaps they need to replace an existing library with a new one. Or pull some section of code out into a component that they can share with another team. Or fix some nasty mess of dependencies that they had allowed to build up.

1『原来 component 就是中间件的意思，哈哈。』

Even in such cases, I’m reluctant to have a team do dedicated refactoring. Often, a useful strategy is to agree to gradually work on the problem over the course of the next few weeks. Whenever anyone goes near any code that’s in the refactoring zone, they move it a little way in the direction they want to improve. This takes advantage of the fact that refactoring doesn’t break the code—each small change leaves everything in a still­ working state. To change from one library to another, start by introducing a new abstraction that can act as an interface to either library. Once the calling code uses this abstraction, it’s much easier to switch one library for another. (This tactic is called Branch By Abstraction [mf­bba].)

大多数重构可以在几分钟——最多几小时——内完成。但有一些大型的重构可能要花上几个星期，例如要替换一个正在使用的库，或者将整块代码抽取到一个组件中并共享给另一支团队使用，再或者要处理一大堆混乱的依赖关系，等等。即便在这样的情况下，我仍然不愿让一支团队专门做重构。可以让整个团队达成共识，在未来几周时间里逐步解决这个问题，这经常是一个有效的策略。每当有人靠近「重构区」的代码，就把它朝想要改进的方向推动一点。这个策略的好处在于，重构不会破坏代码——每次小改动之后，整个系统仍然照常工作。例如，如果想替换掉一个正在使用的库，可以先引入一层新的抽象，使其兼容新旧两个库的接口。一旦调用方已经完全改为使用这层抽象，替换下面的库就会容易得多。（这个策略叫作 Branch By Abstraction [mf-bba]。）

#### 2.4.6 Refactoring in a Code Review

Some organizations do regular code reviews; those that don’t would do better if they did. Code reviews help spread knowledge through a development team. Reviews help more experienced developers pass knowledge to those less experienced. They help more people understand more aspects of a large software system. They are also very important in writing clear code. My code may look clear to me but not to my team. That’s inevitable—it’s hard for people to put themselves in the shoes of someone unfamiliar with whatever they are working on. Reviews also give the opportunity for more people to suggest useful ideas. I can only think of so many good ideas in a week. Having other people contribute makes my life easier, so I always look for reviews.

一些公司会做常规的代码复审（code review），因为这种活动可以改善开发状况。代码复审有助于在开发团队中传播知识，也有助于让较有经验的开发者把知识传递给比较欠缺经验的人，并帮助更多人理解大型软件系统中的更多部分。代码复审对于编写清晰代码也很重要。我的代码也许对我自己来说很清晰，对他人则不然。这是无法避免的，因为要让开发者设身处地为那些不熟悉自己所作所为的人着想，实在太困难了。代码复审也让更多人有机会提出有用的建议，毕竟我在一个星期之内能够想出的好点子很有限。如果能得到别人的帮助，我的生活会滋润得多，所以我总是期待更多复审。

I’ve found that refactoring helps me review someone else’s code. Before I started using refactoring, I could read the code, understand it to some degree, and make suggestions. Now, when I come up with ideas, I consider whether they can be easily implemented then and there with refactoring. If so, I refactor. When I do it a few times, I can see more clearly what the code looks like with the suggestions in place. I don’t have to imagine what it would be like—I can see it. As a result, I can come up with a second level of ideas that I would never have realized had I not refactored.

我发现，重构可以帮助我复审别人的代码。开始重构前我可以先阅读代码，得到一定程度的理解，并提出一些建议。一旦想到一些点子，我就会考虑是否可以通过重构立即轻松地实现它们。如果可以，我就会动手。这样做了几次以后，我可以更清楚地看到，当我的建议被实施以后，代码会是什么样。我不必想象代码应该是什么样，我可以真实看见。于是我可以获得更高层次的认识。如果不进行重构，我永远无法得到这样的认识。

Refactoring also helps get more concrete results from the code review. Not only are there suggestions; many suggestions are implemented there and then. You end up with much more of a sense of accomplishment from the exercise.

重构还可以帮助代码复审工作得到更具体的结果。不仅获得建议，而且其中许多建议能够立刻实现。最终你将从实践中得到比以往多得多的成就感。

How I’d embed refactoring into a code review depends on the nature of the review. The common pull request model, where a reviewer looks at code without the original author, doesn’t work too well. It’s better to have the original author of the code present because the author can provide context on the code and fully appreciate the reviewers’ intentions for their changes. I’ve had my best experiences with this by sitting one­-on-one with the original author, going through the code and refactoring as we go. The logical conclusion of this style is pair programming: continuous code review embedded within the process of programming.

至于如何在代码复审的过程中加入重构，这要取决于复审的形式。在常见的 pull request 模式下，复审者独自浏览代码，代码的作者不在旁边，此时进行重构效果并不好。如果代码的原作者在旁边会好很多，因为作者能提供关于代码的上下文信息，并且充分认同复审者进行修改的意图。对我个人而言，与原作者肩并肩坐在一起，一边浏览代码一边重构，体验是最佳的。这种工作方式很自然地导向结对编程：在编程的过程中持续不断地进行代码复审。

#### 2.4.7 What Do I Tell My Manager?

One of the most common questions I’ve been asked is, “How to tell a manager about refactoring?” I’ve certainly seen places were refactoring has become a dirty word—with managers (and customers) believing that refactoring is either correcting errors made earlier, or work that doesn’t yield valuable features. This is exacerbated by teams scheduling weeks of pure refactoring—especially if what they are really doing is not refactoring but less careful restructuring that causes breakages in the code base.

毋庸讳言，我见过一些场合，「重构」被视为一个脏词——经理（和客户）认为重构要么是在弥补过去犯下的错误，要么是不增加价值的无用功。如果团队又计划了几周时间专门做重构，情况就更糟糕了——如果他们做的其实还不是重构，而是不加小心的结构调整，然后又对代码库造成了破坏，那可就真是糟透了。

To a manager who is genuinely savvy about technology and understands the design stamina hypothesis, refactoring isn’t hard to justify. Such managers should be encouraging refactoring on a regular basis and be looking for signs that indicate a team isn’t doing enough. While it does happen that teams do too much refactoring, it’s much rarer than teams not doing enough. Of course, many managers and customer don’t have the technical awareness to know how code base health impacts productivity. In these cases I give my more controversial advice: Don’t tell!

如果这位经理懂技术，能理解「设计耐久性假说」，那么向他说明重构的意义应该不会很困难。这样的经理应该会鼓励日常的重构，并主动寻找团队日常重构做得不够的征兆。虽然「团队做了太多重构」的情况确实也发生过，但比起做得不够的情况要罕见得多了。当然，很多经理和客户不具备这样的技术意识，他们不理解代码库的健康对生产率的影响。这种情况下我会给团队一个较有争议的建议：不要告诉经理！

Subversive? I don’t think so. Software developers are professionals. Our job is to build effective software as rapidly as we can. My experience is that refactoring is a big aid to building software quickly. If I need to add a new function and the design does not suit the change, I find it’s quicker to refactor first and then add the function. If I need to fix a bug, I need to understand how the software works—and I find refactoring is the fastest way to do this. A schedule­-driven manager wants me to do things the fastest way I can; how I do it is my responsibility. I’m being paid for my expertise in programming new capabilities fast, and the fastest way is by refactoring—therefore I refactor.

这是在搞破坏吗？我不这样想。软件开发者都是专业人士。我们的工作就是尽可能快速创造出高效软件。我的经验告诉我，对于快速创造软件，重构可带来巨大帮助。如果需要添加新功能，而原本设计却又使我无法方便地修改，我发现先重构再添加新功能会更快些。如果要修补错误，就得先理解软件的工作方式，而我发现重构是理解软件的最快方式。受进度驱动的经理要我尽可能快速完成任务，至于怎么完成，那就是我的事了。我领这份工资，是因为我擅长快速实现新功能；我认为最快的方式就是重构，所以我就重构。

1『独特的见解，「不告诉」也是人人交互的一种特定场景下的好手段。』

#### 2.4.8 When Should I Not Refactor?

It may sound like I always recommend refactoring—but there are cases when it’s not worthwhile.

If I run across code that is a mess, but I don’t need to modify it, then I don’t need to refactor it. Some ugly code that I can treat as an API may remain ugly. It’s only when I need to understand how it works that refactoring gives me any benefit. Another case is when it’s easier to rewrite it than to refactor it. This is a tricky decision. Often, I can’t tell how easy it is to refactor some code unless I spend some time trying and thus get a sense of how difficult it is. The decision to refactor or rewrite requires good judgment and experience, and I can’t really boil it down into a piece of simple advice.

如果我看见一块凌乱的代码，但并不需要修改它，那么我就不需要重构它。如果丑陋的代码能被隐藏在一个 API 之下，我就可以容忍它继续保持丑陋。只有当我需要理解其工作原理时，对其进行重构才有价值。另一种情况是，如果重写比重构还容易，就别重构了。这是个困难的决定。如果不花一点儿时间尝试，往往很难真实了解重构一块代码的难度。决定到底应该重构还是重写，需要良好的判断力与丰富的经验，我无法给出一条简单的建议。

2『 2 个不需要重构的场景，做一张任意卡片。』

### 2.5 Problems With Refactoring

Whenever anyone advocates for some technique, tool, or architecture, I always look for problems. Few things in life are all sunshine and clear skies. You need to understand the tradeoffs to decide when and where to apply something. I do think refactoring is a valuable technique—one that should be used more by most teams. But there are problems associated with it, and it’s important to understand how they manifest themselves and how we can react to them.

每当有人大力推荐一种技术、工具或者架构时，我总是会观察这东西会遇到哪些挑战，毕竟生活中很少有晴空万里的好事。你需要了解一件事背后的权衡取舍，才能决定何时何地应用它。我认为重构是一种很有价值的技术，大多数团队都应该更多地重构，但它也不是完全没有挑战的。有必要充分了解重构会遇到的挑战，这样才能做出有效应对。

#### 2.5.1 Slowing Down New Features 

If you read the previous section, you should already know my response. Although many people see time spent refactoring as slowing down the development of new features, the whole purpose of refactoring is to speed things up. But while this is true, it’s also true that the perception of refactoring as slowing things down is still common—and perhaps the biggest barrier to people doing enough refactoring. The whole purpose of refactoring is to make us program faster, producing more value with less effort.

如果你读了前面一小节，我对这个挑战的回应便已经很清楚了。尽管重构的目的是加快开发速度，但是，仍旧很多人认为，花在重构的时间是在拖慢新功能的开发进度。「重构会拖慢进度」这种看法仍然很普遍，这可能是导致人们没有充分重构的最大阻力所在。重构的唯一目的就是让我们开发更快，用更少的工作量创造更大的价值。

There is a genuine tradeoff here. I do run into situations where I see a (large­scale) refactoring that really needs to be done, but the new feature I want to add is so small that I prefer to add it and leave the larger refactoring alone. That’s a judgment callpart of my professional skills as a programmer. I can’t easily describe, let alone quantify, how I make that tradeoff.

有一种情况确实需要权衡取舍。我有时会看到一个（大规模的）重构很有必要进行，而马上要添加的功能非常小，这时我会更愿意先把新功能加上，然后再做这次大规模重构。做这个决定需要判断力——这是我作为程序员的专业能力之一。我很难描述决定的过程，更无法量化决定的依据。

I’m very conscious that preparatory refactoring often makes a change easier, so I certainly will do it if I see that it makes my new feature easier to implement. I’m also more inclined to refactor if this is a problem I’ve seen before—sometimes it takes me a couple of times seeing some particular ugliness before I decide to refactor it away. Conversely, I’m more likely to not refactor if it’s part of the code I rarely touch and the cost of the inconvenience isn’t something I feel very often. Sometimes, I delay a refactoring because I’m not sure what improvement to do, although at other times I’ll try something as an experiment to see if it makes things better.

我清楚地知道，预备性重构常会使修改更容易，所以如果做一点儿重构能让新功能实现更容易，我一定会做。如果一个问题我已经见过，此时我也会更倾向于重构它——有时我就得先看见一块丑陋的代码几次，然后才能提起劲头来重构它。也就是说，如果一块代码我很少触碰，它不会经常给我带来麻烦，那么我就倾向于不去重构它。如果我还没想清楚究竟应该如何优化代码，那么我可能会延迟重构；当然，有的时候，即便没想清楚优化的方向，我也会先做些实验，试试看能否有所改进。

Still, the evidence I hear from my colleagues in the industry is that too little refactoring is far more prevalent than too much. In other words, most people should try to refactor more often. You may have trouble telling the difference in productivity between a healthy and a sickly code base because you haven’t had enough experience of a healthy code base—of the power that comes from easily combining existing parts into new configurations to quickly enable complicated new features.

我从同事那里听到的证据表明，在我们这个行业里，重构不足的情况远多于重构过度的情况。换句话说，绝大多数人应该尝试多做重构。代码库的健康与否，到底会对生产率造成多大的影响，很多人可能说不出来，因为他们没有太多在健康的代码库上工作的经历——轻松地把现有代码组合配置，快速构造出复杂的新功能，这种强大的开发方式他们没有体验过。

Although it’s often managers that are criticized for the counter­-productive habit of squelching refactoring in the name of speed, I’ve often seen developers do it to themselves. Sometimes, they think they shouldn’t be refactoring even though their leadership is actually in favor. If you’re a tech lead in a team, it’s important to show team members that you value improving the health of a code base. That judgment I mentioned earlier on whether to refactor or not is something that takes years of experience to build up. Those with less experience in refactoring need lots of mentoring to accelerate them through the process. 

虽然我们经常批评管理者以「保障开发速度」的名义压制重构，其实程序员自己也经常这么干。有时他们自己觉得不应该重构，其实他们的领导还挺希望他们做一些重构的。如果你是一支团队的技术领导，一定要向团队成员表明，你重视改善代码库健康的价值。合理判断何时应该重构、何时应该暂时不重构，这样的判断力需要多年经验积累。对于重构缺乏经验的年轻人需要有意的指导，才能帮助他们加速经验积累的过程。

But I think the most dangerous way that people get trapped is when they try to justify refactoring in terms of “clean code,” “good engineering practice,” or similar moral reasons. The point of refactoring isn’t to show how sparkly a code base is—it is purely economic. We refactor because it makes us faster—faster to add features, faster to fix bugs. It’s important to keep that in front of your mind and in front of communication with others. The economic benefits of refactoring should always be the driving factor, and the more that is understood by developers, managers, and customers, the more of the “good design” curve we’ll see.

有些人试图用「整洁的代码」、「良好的工程实践」之类道德理由来论证重构的必要性，我认为这是个陷阱。重构的意义不在于把代码库打磨得闪闪发光，而是纯粹经济角度出发的考量。我们之所以重构，因为它能让我们更快——添加功能更快，修复 bug 更快。一定要随时记住这一点，与别人交流时也要不断强调这一点。重构应该总是由经济利益驱动。程序员、经理和客户越理解这一点，「好的设计」那条曲线就会越经常出现。

1『重构的能让我们开发更快。做一张反常识卡片。』——已完成

#### 2.5.2 Code Ownership

Many refactorings involve making changes that affect not just the internals of a module but its relationships with other parts of a system. If I want to rename a function, and I can find all the callers to a function, I simply apply Change Function Declaration (124) and change the declaration and the callers in one change. But sometimes this simple refactoring isn’t possible. Perhaps the calling code is owned by a different team and I don’t have write access to their repository. Perhaps the function is a declared API used by my customers—so I can’t even tell if it’s being used, let alone by who and how much. Such functions are part of a published interface—an interface that is used by clients independent of those who declare the interface.

很多重构手法不仅会影响一个模块内部，还会影响该模块与系统其他部分的关系。比如我想给一个函数改名，并且我也能找到该函数的所有调用者，那么我只需运用改变函数声明（124），在一次重构中修改函数声明和调用者。但即便这么简单的一个重构，有时也无法实施：调用方代码可能由另一支团队拥有，而我没有权限写入他们的代码库；这个函数可能是一个提供给客户的 API，这时我根本无法知道是否有人使用它，至于谁在用、用得有多频繁就更是一无所知。这样的函数属于已发布接口（published interface）：接口的使用者（客户端）与声明者彼此独立，声明者无权修改使用者的代码。

Code ownership boundaries get in the way of refactoring because I cannot make the kinds of changes I want without breaking my clients. This doesn’t prevent refactoring—I can still do a great deal—but it does impose limitations. When renaming a function, I need to use Rename Function (124) and to retain the old declaration as a pass-­through to the new one. This complicates the interface—but it is the price I must pay to avoid breaking my clients. I may be able to mark the old interface as deprecated and, in time, retire it, but sometimes I have to retain that interface forever.

代码所有权的边界会妨碍重构，因为一旦我自作主张地修改，就一定会破坏使用者的程序。这不会完全阻止重构，我仍然可以做很多重构，但确实会对重构造成约束。为了给一个函数改名，我需要使用函数改名（124），但同时也得保留原来的函数声明，使其把调用传递给新的函数。这会让接口变复杂，但这就是为了避免破坏使用者的系统而不得不付出的代价。我可以把旧的接口标记为「不推荐使用」（deprecated），等一段时间之后最终让其退休；但有些时候，旧的接口必须一直保留下去。

Due to these complexities, I recommend against fine­-grained strong code ownership. Some organizations like any piece of code to have a single programmer as an owner, and only allow that programmer to change it. I’ve seen a team of three people operate in such a way that each one published interfaces to the other two. This led to all sorts of gyrations to maintain interfaces when it would have been much easier to go into the code base and make the edits. My preference is to allow team ownership of code—so that anyone in the same team can modify the team’s code, even if originally written by someone else. Programmers may have individual responsibility for areas of a system, but that should imply that they monitor changes to their area of responsibility, not block them by default. 

由于这些复杂性，我建议不要搞细粒度的强代码所有制。有些组织喜欢给每段代码都指定唯一的所有者，只有这个人能修改这段代码。我曾经见过一支只有三个人的团队以这种方式运作，每个程序员都要给另外两人发布接口，随之而来的就是接口维护的种种麻烦。如果这三个人都直接去代码库里做修改，事情会简单得多。我推荐团队代码所有制，这样一支团队里的成员都可以修改这个团队拥有的代码，即便最初写代码的是别人。程序员可能各自分工负责系统的不同区域，但这种责任应该体现为监控自己责任区内发生的修改，而不是简单粗暴地禁止别人修改。

Such a more permissive ownership scheme can even exist across teams. Some teams encourage an open-­source-­like model where people from other teams can change a branch of their code and send the commit in to be approved. This allows one team to change the clients of their functions—they can delete the old declarations once their commits to their clients have been accepted. This can often be a good compromise between strong code ownership and chaotic changes in large systems.

这种较为宽容的代码所有制甚至可以应用于跨团队的场合。有些团队鼓励类似于开源的模型：B 团队的成员也可以在一个分支上修改 A 团队的代码，然后把提交发送给 A 团队去审核。这样一来，如果团队想修改自己的函数，他们就可以同时修改该函数的客户端的代码；只要客户端接受了他们的修改，就可以删掉旧的函数声明了。对于涉及多个团队的大系统开发，在「强代码所有制」和「混乱修改」两个极端之间，这种类似开源的模式常常是一个合适的折中。

#### 2.5.3 Branches

As I write this, a common approach in teams is for each team member to work on a branch of the code base using a version control system, and do considerable work on that branch before integrating with a mainline (often called master or trunk) shared across the team. Often, this involves building a whole feature on a branch, not integrating into the mainline until the feature is ready to be released into production. Fans of this approach claim that it keeps the mainline clear of any in­process code, provides a clear version history of feature additions, and allows features to be reverted easily should they cause problems.

很多团队采用这样的版本控制实践：每个团队成员各自在代码库的一条分支上工作，进行相当大量的开发之后，才把各自的修改合并回主线分支（这条分支通常叫 master 或 trunk），从而与整个团队分享。常见的做法是在分支上开发完整的功能，直到功能可以发布到生产环境，才把该分支合并回主线。这种做法的拥趸声称，这样能保持主线不受尚未完成的代码侵扰，能保留清晰的功能添加的版本记录，并且在某个功能出问题时能容易地撤销修改。

There are downsides to feature branches like this. The longer I work on an isolated branch, the harder the job of integrating my work with mainline is going to be when I’m done. Most people reduce this pain by frequently merging or re­basing from mainline to my branch. But this doesn’t really solve the problem when several people are working on individual feature branches. I distinguish between merging and integration. If I merge mainline into my code, this is a oneway movement—my branch changes but the mainline doesn’t. I use “integrate” to mean a two­-way process that pulls changes from mainline into my branch and then pushes the result back into mainline, changing both. If Rachel is working on her branch I don’t see her changes until she integrates with mainline; at that point, I have to merge her changes into my feature branch, which may mean considerable work. The hard part of this work is dealing with semantic changes. Modern version control systems can do wonders with merging complex changes to the program text, but they are blind to the semantics of the code. If I’ve changed the name of a function, my version control tool may easily integrate my changes with Rachel’s. But if, in her branch, she added a call to a function that I’ve renamed in mine, the code will fail.

这样的特性分支有其缺点。在隔离的分支上工作得越久，将完成的工作集成（integrate）回主线就会越困难。为了减轻集成的痛苦，大多数人的办法是频繁地从主线合并（merge）或者变基（rebase）到分支。但如果有几个人同时在各自的特性分支上工作，这个办法并不能真正解决问题，因为合并与集成是两回事。如果我从主线合并到我的分支，这只是一个单向的代码移动——我的分支发生了修改，但主线并没有。而「集成」是一个双向的过程：不仅要把主线的修改拉（pull）到我的分支上，而且要把我这里修改的结果推（push）回到主线上，两边都会发生修改。假如另一名程序员 Rachel 正在她的分支上开发，我是看不见她的修改的，直到她将自己的修改与主线集成；此时我就必须把她的修改合并到我的特性分支，这可能需要相当的工作量。其中困难的部分是处理语义变化。现代版本控制系统都能很好地合并程序文本的复杂修改，但对于代码的语义它们一无所知。如果我修改了一个函数的名字，版本控制工具可以很轻松地将我的修改与 Rachel 的代码集成。但如果在集成之前，她在自己的分支里新添调用了这个被我改名的函数，集成之后的代码就会被破坏。

2『集成是一个双向过程。做一张任意卡片。』——已完成

The problem of complicated merges gets exponentially worse as the length of feature branches increases. Integrating branches that are four weeks old is more than twice as hard as those that are a couple of weeks old. Many people, therefore, argue for keeping feature branches short—perhaps just a couple of days. Others, such as me, want them even shorter than that. This is an approach called Continuous Integration (CI), also known as Trunk­-Based Development. With CI, each team member integrates with mainline at least once per day. This prevents any branches diverting too far from each other and thus greatly reduces the complexity of merges. CI doesn’t come for free: It means you use practices to ensure the mainline is healthy, learn to break large features into smaller chunks, and use feature toggles (aka feature flags) to switch off any inprocess features that can’t be broken down.

分支合并本来就是一个复杂的问题，随着特性分支存在的时间加长，合并的难度会指数上升。集成一个已经存在了 4 个星期的分支，较之集成存在了 2 个星期的分支，难度可不止翻倍。所以很多人认为，应该尽量缩短特性分支的生存周期，比如只有一两天。还有一些人（比如我本人）认为特性分支的生命还应该更短，我们采用的方法叫作持续集成（Continuous Integration，CI），也叫「基于主干开发」（Trunk-Based Development）。在使用 CI 时，每个团队成员每天至少向主线集成一次。这个实践避免了任何分支彼此差异太大，从而极大地降低了合并的难度。不过 CI 也有其代价：你必须使用相关的实践以确保主线随时处于健康状态，必须学会将大功能拆分成小块，还必须使用特性开关（feature toggle，也叫特性旗标，feature flag）将尚未完成又无法拆小的功能隐藏掉。

Fans of CI like it partly because it reduces the complexity of merges, but the dominant reason to favor CI is that it’s far more compatible with refactoring. Refactorings often involve making lots of little changes all over the code base—which are particularly prone to semantic merge conflicts (such as renaming a widely used function). Many of us have seen feature­-branching teams that find refactorings so exacerbate merge problems that they stop refactoring. CI and re­factoring work well together, which is why Kent Beck combined them in Extreme Programming.

CI 的粉丝之所以喜欢这种工作方式，部分原因是它降低了分支合并的难度，不过最重要的原因还是 CI 与重构能良好配合。重构经常需要对代码库中的很多地方做很小的修改（例如给一个广泛使用的函数改名），这样的修改尤其容易造成合并时的语义冲突。采用特性分支的团队常会发现重构加剧了分支合并的困难，并因此放弃了重构，这种情况我们曾经见过多次。CI 和重构能够良好配合，所以 Kent Beck 在极限编程中同时包含了这两个实践。

1『持续继承是和重构配合使用的。』

I’m not saying that you should never use feature branches. If they are sufficiently short, their problems are much reduced. (Indeed, users of CI usually also use branches, but integrate them with mainline each day.) Feature branches may be the right technique for open source projects where you have infrequent commits from programmers who you don’t know well (and thus don’t trust). But in a full­time development team, the cost that feature branches impose on refactoring is excessive. Even if you don’t go to full CI, I certainly urge you to integrate as frequently as possible. You should also consider the objective evidence [Forsgren et al.] that teams that use CI are more effective in software delivery.

我并不是在说绝不应该使用特性分支。如果特性分支存在的时间足够短，它们就不会造成大问题。（实际上，使用 CI 的团队往往同时也使用分支，但他们会每天将分支与主线合并。）对于开源项目，特性分支可能是合适的做法，因为不时会有你不熟悉（因此也不信任）的程序员偶尔提交修改。但对全职的开发团队而言，特性分支对重构的阻碍太严重了。即便你没有完全采用 CI，我也一定会催促你尽可能频繁地集成。而且，用上 CI 的团队在软件交付上更加高效，我真心希望你认真考虑这个客观事实 [Forsgren et al]。

#### 2.5.4 Testing

One of the key characteristics of refactoring is that it doesn’t change the observable behavior of the program. If I follow the refactorings carefully, I shouldn’t break anything—but what if I make a mistake? Mistakes happen, but they aren’t a problem provided I catch them quickly. Since each refactoring is a small change, if I break anything, I only have a small change to look at to find the fault—and if I still can’t spot it, I can revert my version control to the last working version.

不会改变程序可观察的行为，这是重构的一个重要特征。如果仔细遵循重构手法的每个步骤，我应该不会破坏任何东西，但万一我犯了个错误怎么办？（呃，就我这个粗心大意的性格来说，请去掉「万一」两字。）人总会有出错的时候，不过只要及时发现，就不会造成大问题。既然每个重构都是很小的修改，即便真的造成了破坏，我也只需要检查最后一步的小修改——就算找不到出错的原因，只要回滚到版本控制中最后一个可用的版本就行了。

1『重构的一个关键特性是，不会改变程序的可观察行为。』

The key here is being able to catch an error quickly. To do this, realistically, I need to be able to run a comprehensive test suite on the code—and run it quickly, so that I’m not deterred from running it frequently. This means that in most cases, if I want to refactor, I need to have self­-testing code [mf­stc]. 

这里的关键就在于「快速发现错误」。要做到这一点，我的代码应该有一套完备的测试套件，并且运行速度要快，否则我会不愿意频繁运行它。也就是说，绝大多数情况下，如果想要重构，我得先有可以自测试的代码 [mf-stc]。

1『测试的一个关键点是要实现「自测试」。』

To some readers, self­-testing code sounds like a requirement so steep as to be unrealizable. But over the last couple of decades, I’ve seen many teams build software this way. It takes attention and dedication to testing, but the benefits make it really worthwhile. Self­-testing code not only enables refactoring—it also makes it much safer to add new features, since I can quickly find and kill any bugs I introduce. The key point here is that when a test fails, I can look at the change I’ve made between when the tests were last running correctly and the current code. With frequent test runs, that will be only a few lines of code. By knowing it was those few lines that caused the failure, I can much more easily find the bug.

This also answers those who are concerned that refactoring carries too much risk of introducing bugs. Without self-testing code, that’s a reasonable worry—which is why I put so much emphasis on having solid tests.

有些读者可能会觉得，「自测试的代码」这个要求太高，根本无法实现。但在过去 20 年中，我看到很多团队以这种方式构造软件。的确，团队必须投入时间与精力在测试上，但收益是绝对划算的。自测试的代码不仅使重构成为可能，而且使添加新功能更加安全，因为我可以很快发现并干掉新近引入的 bug。这里的关键在于，一旦测试失败，我只需要查看上次测试成功运行之后修改的这部分代码；如果测试运行得很频繁，这个查看的范围就只有几行代码。知道必定是这几行代码造成 bug 的话，排查起来会容易得多。这也回答了「重构风险太大，可能引入 bug」的担忧。如果没有自测试的代码，这种担忧就是完全合理的，这也是为什么我如此重视可靠的测试。

1『有一次强调了，重构的一起前置条件是有一套「自测试」的测试系统保障，这样可以放心大胆的去重构。』

There is another way to deal with the testing problem. If I use an environment that has good automated refactorings, I can trust those refactorings even without running tests. I can then refactor, providing I only use those refactorings that are safely automated. This removes a lot of nice refactorings from my menu, but still leaves me enough to deliver some useful benefits. I’d still rather have self­testing code, but it’s an option that is useful to have in the toolkit.

缺乏测试的问题可以用另一种方式来解决。如果我的开发环境很好地支持自动化重构，我就可以信任这些重构，不必运行测试。这时即便没有完备的测试套件，我仍然可以重构，前提是仅仅使用那些自动化的、一定安全的重构手法。这会让我损失很多好用的重构手法，不过剩下可用的也不少，我还是能从中获益。当然，我还是更愿意有自测试的代码，但如果没有，自动化重构的工具包也很好。

This also inspires a style of refactoring that only uses a limited set of refactorings that can be proven safe. Such refactorings require carefully following the steps, and are language­-specific. But teams using them have found they can do useful refactoring on large code bases with poor test coverage. I don’t focus on that in this book, as it’s a newer, less described and understood technique that involves detailed, language-specific activity. (It is, however, something I hope talk about more on my web site in the future. For a taste of it, see Jay Bazuzi’s description [Bazuzi] of a safer way to do Extract Method (106) in C++.)

缺乏测试的现状还催生了另一种重构的流派：只使用一组经过验证是安全的重构手法。这个流派要求严格遵循重构的每个步骤，并且可用的重构手法是特定于语言的。使用这种方法，团队得以在测试覆盖率很低的大型代码库上开展一些有用的重构。这个重构流派比较新，涉及一些很具体、特定于编程语言的技巧与做法，行业里对这种方法的介绍和了解都还不足，因此本书不对其多做介绍。（不过我希望未来在我自己的网站上多讨论这个主题。感兴趣的读者可以查看 Jay Bazuzi 关于如何在 C++ 中安全地运用提炼函数（106）的描述 [Bazuzi]，借此获得一点儿对这个重构流派的了解。）

Self­-testing code is, unsurprisingly, closely associated with Continuous Integration—it is the mechanism that we use to catch semantic integration conflicts. Such testing practices are another component of Extreme Programming and a key part of Continuous Delivery.

毫不意外，自测试代码与持续集成紧密相关——我们仰赖持续集成来及时捕获分支集成时的语义冲突。自测试代码是极限编程的另一个重要组成部分，也是持续交付的关键环节。

2『极限编程出现了很多次啊，一定要去研读书籍「2020130解析极限编程」。』

#### 2.5.5 Legacy Code

Most people would regard a big legacy as a Good Thing—but that’s one of the cases where programmers’ view is different. Legacy code is often complex, frequently comes with poor tests, and, above all, is written by Someone Else (shudder). Refactoring can be a fantastic tool to help understand a legacy system. Functions with misleading names can be renamed so they make sense, awkward programming constructs smoothed out, and the program turned from a rough rock to a polished gem. But the dragon guarding this happy tale is the common lack of tests. If you have a big legacy system with no tests, you can’t safely refactor it into clarity.

大多数人会觉得，有一大笔遗产是件好事，但从程序员的角度来看就不同了。遗留代码往往很复杂，测试又不足，而且最关键的是，是别人写的（瑟瑟发抖）。重构可以很好地帮助我们理解遗留系统。引人误解的函数名可以改名，使其更好地反映代码用途；糟糕的程序结构可以慢慢理顺，把程序从一块顽石打磨成美玉。整个故事都很棒，但我们绕不开关底的恶龙：遗留系统多半没测试。如果你面对一个庞大而又缺乏测试的遗留系统，很难安全地重构清理它。

The obvious answer to this problem is that you add tests. But while this sounds a simple, if laborious, procedure, it’s often much more tricky in practice. Usually, a system is only easy to put under test if it was designed with testing in mind—in which case it would have the tests and I wouldn’t be worrying about it.

对于这个问题，显而易见的答案是「没测试就加测试」。这事听起来简单（当然工作量必定很大），操作起来可没那么容易。一般来说，只有在设计系统时就考虑到了测试，这样的系统才容易添加测试——可要是如此，系统早该有测试了，我也不用操这份心了。

There’s no simple route to dealing with this. The best advice I can give is to get a copy of Working Effectively with Legacy Code [Feathers] and follow its guidance. Don’t be worried by the age of the book—its advice is just as true more than a decade later. To summarize crudely, it advises you to get the system under test by finding seams in the program where you can insert tests. Creating these seams involves refactoring—which is much more dangerous since it’s done without tests, but is a necessary risk to make progress. This is a situation where safe, automated refactorings can be a godsend. If all this sounds difficult, that’s because it is. Sadly, there’s no shortcut to getting out of a hole this deep—which is why I’m such a strong proponent of writing self­testing code from the start.

这个问题没有简单的解决办法，我能给出的最好建议就是买一本《修改代码的艺术》[Feathers]，照书里的指导来做。别担心那本书太老，尽管已经出版十多年，其中的建议仍然管用。一言以蔽之，它建议你先找到程序的接缝，在接缝处插入测试，如此将系统置于测试覆盖之下。你需要运用重构手法创造出接缝——这样的重构很危险，因为没有测试覆盖，但这是为了取得进展必要的风险。在这种情况下，安全的自动化重构简直就是天赐福音。如果这一切听起来很困难，因为它确实很困难。很遗憾，一旦跌进这个深坑，没有爬出来的捷径，这也是我强烈倡导从一开始就写能自测试的代码的原因。

Even when I do have tests, I don’t advocate trying to refactor a complicated legacy mess into beautiful code all at once. What I prefer to do is tackle it in relevant pieces. Each time I pass through a section of the code, I try to make it a little bit better—again, like leaving a camp site cleaner than when I found it. If this is a large system, I’ll do more refactoring in areas I visit frequently—which is the right thing to do because, if I need to visit code frequently, I’ll get a bigger payoff by making it easier to understand.

就算有了测试，我也不建议你尝试一鼓作气把复杂而混乱的遗留代码重构成漂亮的代码。我更愿意随时重构相关的代码：每次触碰一块代码时，我会尝试把它变好一点点—至少要让营地比我到达时更干净。如果是一个大系统，越是频繁使用的代码，改善其可理解性的努力就能得到越丰厚的回报。

#### 2.5.6 Databases

When I wrote the first edition of this book, I said that refactoring databases was a problem area. But, within a year of the book’s publication, that was no longer the case. My colleague Pramod Sadalage developed an approach to evolutionary database design [mf­evodb] and database refactoring [Ambler & Sadalage] that is now widely used. The essence of the technique is to combine the structural changes to a database’s schema and access code with data migration scripts that can easily compose to handle large changes.

在本书的第 1 版中，我说过数据库是「重构经常出问题的一个领域」。然而在第 1 版问世之后仅仅一年，情况就发生了改变：我的同事 Pramod Sadalage 发展出一套渐进式数据库设计 [mf-evodb] 和数据库重构 [Ambler&Sadalage] 的办法，如今已经被广泛使用。这项技术的精要在于：借助数据迁移脚本，将数据库结构的修改与代码相结合，使大规模的、涉及数据库的修改可以比较容易地开展。

2『去找这项技术的相关资料。』

Consider a simple example of renaming a field (column). As in Change Function Declaration (124), I need to find the original declaration of the structure and all the callers of this structure and change them in a single change. The complication, however, is that I also have to transform any data that uses the old field to use the new one. I write a small hunk of code that carries out this transform and store it in version control, together with the code that changes any declared structure and access routines. Then, whenever I need to migrate between two versions of the database, I run all the migration scripts that exist between my current copy of the database and my desired version.

假设我们要对一个数据库字段（列）改名。和改变函数声明（124）一样，我要找出结构的声明处和所有调用处，然后一次完成所有修改。但这里的复杂之处在于，原来基于旧字段的数据，也要转为使用新字段。我会写一小段代码来执行数据转化的逻辑，并把这段代码放进版本控制，跟数据结构声明与使用代码的修改一并提交。此后如果我想把数据库迁移到某个版本，只要执行当前数据库版本与目标版本之间的所有迁移脚本即可。

1『感觉 laravel 里数据库迁移的脚本是基于此技术实现了，待确认。（2020-06-15）』

As with regular refactoring, the key here is that each individual change is small yet captures a complete change, so the system still runs after applying the migration. Keeping them small means they are easy to write, but I can string many of them into a sequence that can make a significant change to the database’s structure and the data stored in it.

跟通常的重构一样，数据库重构的关键也是小步修改并且每次修改都应该完整，这样每次迁移之后系统仍然能运行。由于每次迁移涉及的修改都很小，写起来应该容易；将多个迁移串联起来，就能对数据库结构及其中存储的数据做很大的调整。

One difference from regular refactorings is that database changes often are best separated over multiple releases to production. This makes it easy to reverse any change that causes a problem in production. So, when renaming a field, my first commit would add the new database field but not use it. I may then set up the updates so they update both old and new fields at once. I can then gradually move the readers over to the new field. Only once they have all moved to the new field, and I’ve given a little time for any bugs to show themselves, would I remove the now­-unused old field. This approach to database changes is an example of a general approach of parallel change [mf­pc] (also called expand­-contract).

与常规的重构不同，很多时候，数据库重构最好是分散到多次生产发布来完成，这样即便某次修改在生产数据库上造成了问题，也比较容易回滚。比如，要改名一个字段，我的第一次提交会新添一个字段，但暂时不使用它。然后我会修改数据写入的逻辑，使其同时写入新旧两个字段。随后我就可以修改读取数据的地方，将它们逐个改为使用新字段。这步修改完成之后，我会暂停一小段时间，看看是否有 bug 冒出来。确定没有 bug 之后，我再删除已经没人使用的旧字段。这种修改数据库的方式是并行修改（Parallel Change，也叫扩展协议/expand-contract）[mf-pc] 的一个实例。

### 2.6 Refactoring, Architechure, and YAGNI

Refactoring has profoundly changed how people think about software architecture. Early in my career, I was taught that software design and architecture was something to be worked on, and mostly completed, before anyone started writing code. Once the code was written, its architecture was fixed and could only decay due to carelessness.

Refactoring changes this perspective. It allows me to significantly alter the architecture of software that’s been running in production for years. Refactoring can improve the design of existing code, as this book’s subtitle implies. But as I indicated earlier, changing legacy code is often challenging, especially when it lacks decent tests.

重构极大地改变了人们考虑软件架构的方式。在我的职业生涯早期，我被告知：在任何人开始写代码之前，必须先完成软件的设计和架构。一旦代码写出来，架构就固定了，只会因为程序员的草率对待而逐渐腐败。重构改变了这种观点。有了重构技术，即便是已经在生产环境中运行了多年的软件，我们也有能力大幅度修改其架构。正如本书的副标题所指出的，重构可以改善既有代码的设计。但我在前面也提到了，修改遗留代码经常很有挑战，尤其当遗留代码缺乏恰当的测试时。

The real impact of refactoring on architecture is in how it can be used to form a well-designed code base that can respond gracefully to changing needs. The biggest issue with finishing architecture before coding is that such an approach assumes the requirements for the software can be understood early on. But experience shows that this is often, even usually, an unachievable goal. Repeatedly, I saw people only understand what they really needed from software once they’d had a chance to use it, and saw the impact it made to their work.

重构对架构最大的影响在于，通过重构，我们能得到一个设计良好的代码库，使其能够优雅地应对不断变化的需求。「在编码之前先完成架构」这种做法最大的问题在于，它假设了软件的需求可以预先充分理解。但经验显示，这个假设很多时候甚至可以说大多数时候是不切实际的。只有真正使用了软件、看到了软件对工作的影响，人们才会想明白自己到底需要什么，这样的例子不胜枚举。

One way of dealing with future changes is to put flexibility mechanisms into the software. As I write some function, I can see that it has a general applicability. To handle the different circumstances that I anticipate it to be used in, I can see a dozen parameters I could add to that function. These parameters are flexibility mechanismsand, like most mechanisms, they are not a free lunch. Adding all those parameters complicates the function for the one case it’s used right now. If I miss a parameter, all the parameterization I have added makes it harder for me to add more. I find I often get my flexibility mechanisms wrong—either because the changing needs didn’t work out the way I expected or my mechanism design was faulty. Once I take all that into account, most of the time my flexibility mechanisms actually slow down my ability to react to change.

应对未来变化的办法之一，就是在软件里植入灵活性机制。在编写一个函数时，我会考虑它是否有更通用的用途。为了应对我预期的应用场景，我预测可以给这个函数加上十多个参数。这些参数就是灵活性机制 —— 跟大多数「机制」一样，它不是免费午餐。把所有这些参数都加上的话，函数在当前的使用场景下就会非常复杂。另外，如果我少考虑了一个参数，已经加上的这一堆参数会使新添参数更麻烦。而且我经常会把灵活性机制弄错 —— 可能是未来的需求变更并非以我期望的方式发生，也可能我对机制的设计不好。考虑到所有这些因素，很多时候这些灵活性机制反而拖慢了我响应变化的速度。

With refactoring, I can use a different strategy. Instead of speculating on what flexibility I will need in the future and what mechanisms will best enable that, I build software that solves only the currently understood needs, but I make this software excellently designed for those needs. As my understanding of the users’ needs changes, I use refactoring to adapt the architecture to those new demands. I can happily include mechanisms that don’t increase complexity (such as small, well­-named functions) but any flexibility that complicates the software has to prove itself before I include it. If I don’t have different values for a parameter from the callers, I don’t add it to the parameter list. Should the time come that I need to add it, then Parameterize Function (310) is an easy refactoring to apply. I often find it useful to estimate how hard it would be to use refactoring later to support an anticipated change. Only if I can see that it would be substantially harder to refactor later do I consider adding a flexibility mechanism now.

有了重构技术，我就可以采取不同的策略。与其猜测未来需要哪些灵活性、需要什么机制来提供灵活性，我更愿意只根据当前的需求来构造软件，同时把软件的设计质量做得很高。随着对用户需求的理解加深，我会对架构进行重构，使其能够应对新的需要。如果一种灵活性机制不会增加复杂度（比如添加几个命名良好的小函数），我可以很开心地引入它；但如果一种灵活性会增加软件复杂度，就必须先证明自己值得被引入。如果不同的调用者不会传入不同的参数值，那么就不要添加这个参数。当真的需要添加这个参数时，运用函数参数化（310）也很容易。要判断是否应该为未来的变化添加灵活性，我会评估「如果以后再重构有多困难」，只有当未来重构会很困难时，我才考虑现在就添加灵活性机制。我发现这是一个很有用的决策方法。

1『判断现在就为未来的变化添加灵活性，一个好依据是，这个地方未来重构的话是否会比较困难，困难的话现在就添加灵活性。』

This approach to design goes under various names: simple design, incremental design, or yagni [mf­yagni] (originally an acronym for “you aren’t going to need it”). Yagni doesn’t imply that architectural thinking disappears, although it is sometimes naively applied that way. I think of yagni as a different style of incorporating architecture and design into the development process—a style that isn’t credible without the foundation of refactoring.

Adopting yagni doesn’t mean I neglect all upfront architectural thinking. There are still cases where refactoring changes are difficult and some preparatory thinking can save time. But the balance has shifted a long way—I’m much more inclined to deal with issues later when I understand them better. All this has led to a growing discipline of evolutionary architecture [Ford et al.] where architects explore the patterns and practices that take advantage of our ability to iterate over architectural decisions.

这种设计方法有很多名字：简单设计、增量式设计或者 YAGNI [mf-yagni]——「你不会需要它」（you arenʼt going to need it）的缩写。YAGNI 并不是「不做架构性思考」的意思，不过确实有人以这种欠考虑的方式做事。我把 YAGNI 视为将架构、设计与开发过程融合的一种工作方式，这种工作方式必须有重构作为基础才可靠。采用 YAGNI 并不表示完全不用预先考虑架构。总有一些时候，如果缺少预先的思考，重构会难以开展。但两者之间的平衡点已经发生了很大的改变：如今我更倾向于等一等，待到对问题理解更充分，再来着手解决。演进式架构 [Fordetal.] 是一门仍在不断发展的学科，架构师们在不断探索有用的模式和实践，充分发挥迭代式架构决策的能力。

### 2.7 Refactoring and the Wider Software Development Process

If you’ve read the earlier section on problems, one lesson you’ve probably drawn is that the effectiveness of refactoring is tied to other software practices that a team uses. Indeed, refactoring’s early adoption was as part of Extreme Programming [mf­xp] (XP), a process which was notable for putting together a set of relatively unusual and interdependent practices—such as continuous integration, self­testing code, and refactoring (the latter two woven into test­driven development).

读完前面「重构的挑战」一节，你大概已经有这个印象：重构是否有效，与团队采用的其他软件开发实践紧密相关。重构起初是作为极限编程（XP）[mf-xp] 的一部分被人们采用的，XP 本身就融合了一组不太常见而又彼此关联的实践，例如持续集成、自测试代码以及重构（后两者融汇成了测试驱动开发）。

Extreme Programming was one of the first agile software methods [mf­nm] and, for several years, led the rise of agile techniques. Enough projects now use agile methods that agile thinking is generally regarded as mainstream—but in reality most “agile” projects only use the name. To really operate in an agile way, a team has to be capable and enthusiastic refactorers—and for that, many aspects of their process have to align with making refactoring a regular part of their work.

The first foundation for refactoring is self-­testing code. By this, I mean that there is a suite of automated tests that I can run and be confident that, if I made an error in my programming, some test will fail. This is such an important foundation for refactoring that I’ll spend a chapter talking more about this.

极限编程是最早的敏捷软件开发方法 [mf-nm] 之一。在一段历史时期，极限编程引领了敏捷的崛起。如今已经有很多项目使用敏捷方法，甚至敏捷的思维已经被视为主流，但实际上大部分「敏捷」项目只是徒有其名。要真正以敏捷的方式运作项目，团队成员必须在重构上有能力、有热情，他们采用的开发过程必须与常规的、持续的重构相匹配。重构的第一块基石是自测试代码。我应该有一套自动化的测试，我可以频繁地运行它们，并且我有信心：如果我在编程过程中犯了任何错误，会有测试失败。这块基石如此重要，我会专门用一章篇幅来讨论它。

To refactor on a team, it’s important that each member can refactor when they need to without interfering with others’ work. This is why I encourage Continuous Integration. With CI, each member’s refactoring efforts are quickly shared with their colleagues. No one ends up building new work on interfaces that are being removed, and if the refactoring is going to cause a problem with someone else’s work, we know about this quickly. Self­-testing code is also a key element of Continuous Integration, so there is a strong synergy between the three practices of self-­testing code, continuous integration, and refactoring.

如果一支团队想要重构，那么每个团队成员都需要掌握重构技能，能在需要时开展重构，而不会干扰其他人的工作。这也是我鼓励持续集成的原因：有了 CI，每个成员的重构都能快速分享给其他同事，不会发生这边在调用一个接口那边却已把这个接口删掉的情况；如果一次重构会影响别人的工作，我们很快就会知道。自测试的代码也是持续集成的关键环节，所以这三大实践 —— 自测试代码、持续集成、重构 —— 彼此之间有着很强的协同效应。

1『自测试、重构以及持续集成，这三大实践一定一定要通过刻意练习成为系统 1。（2020-06-15）』

With this trio of practices in place, we enable the Yagni design approach that I talked about in the previous section. Refactoring and yagni positively reinforce each other: Not just is refactoring (and its prerequisites) a foundation for yagni—yagni makes it easier to do refactoring. This is because it’s easier to change a simple system than one that has lots of speculative flexibility included. Balance these practices, and you can get into a virtuous circle with a code base that responds rapidly to changing needs and is reliable.

有这三大实践在手，我们就能运用前一节介绍的 YAGNI 设计方法。重构和 YAGNI 交相呼应、彼此增效，重构（及其前置实践）是 YAGNI 的基础，YAGNI 又让重构更易于开展：比起一个塞满了想当然的灵活性的系统，当然是修改一个简单的系统要容易得多。在这些实践之间找到合适的平衡点，你就能进入良性循环，你的代码既牢固可靠又能快速响应变化的需求。

With these core practices in place, we have the foundation to take advantage of the other elements of the agile mindset. Continuous Delivery keeps our software in an always-­releasable state. This is what allows many web organizations to release updates many times a day—but even if we don’t need that, it reduces risk and allows us to schedule our releases to satisfy business needs rather than technological constraints. With a firm technical foundation, we can drastically reduce the time it takes to get a good idea into production code, allowing us to better serve our customers. Furthermore, these practices increase the reliability of our software, with less bugs to spend time fixing.

有这三大核心实践打下的基础，才谈得上运用敏捷思想的其他部分。持续交付确保软件始终处于可发布的状态，很多互联网团队能做到一天多次发布，靠的正是持续交付的威力。即便我们不需要如此频繁的发布，持续集成也能帮我们降低风险，并使我们做到根据业务需要随时安排发布，而不受技术的局限。有了可靠的技术根基，我们能够极大地压缩「从好点子到生产代码」的周期时间，从而更好地服务客户。这些技术实践也会增加软件的可靠性，减少耗费在 bug 上的时间。

Stated like this, it all sounds rather simple—but in practice it isn’t. Software development, whatever the approach, is a tricky business, with complex interactions between people and machines. The approach I describe here is a proven way to handle this complexity, but like any approach, it requires practice and skill.

这一切说起来似乎很简单，但实际做起来毫不容易。不管采用什么方法，软件开发都是一件复杂而微妙的事，涉及人与人之间、人与机器之间的复杂交互。我在这里描述的方法已经被证明可以应对这些复杂性，但 —— 就跟其他所有方法一样 —— 对使用者的实践和技能有要求。

### 2.8 Refactoring and Preformance

A common concern with refactoring is the effect it has on the performance of a program. To make the software easier to understand, I often make changes that will cause the program to run slower. This is an important issue. I don’t belong to the school of thought that ignores performance in favor of design purity or in hopes of faster hardware. Software has been rejected for being too slow, and faster machines merely move the goalposts. Refactoring can certainly make software go more slowly—but it also makes the software more amenable to performance tuning. The secret to fast software, in all but hard real­time contexts, is to write tunable software first and then tune it for sufficient speed.

关于重构，有一个常被提出的问题：它对程序的性能将造成怎样的影响？为了让软件易于理解，我常会做出一些使程序运行变慢的修改。这是一个重要的问题。我并不赞成为了提高设计的纯洁性而忽视性能，把希望寄托于更快的硬件身上也绝非正道。已经有很多软件因为速度太慢而被用户拒绝，日益提高的机器速度也只不过略微放宽了速度方面的限制而已。但是，换个角度说，虽然重构可能使软件运行更慢，但它也使软件的性能优化更容易。除了对性能有严格要求的实时系统，其他任何情况下「编写快速软件」的秘密就是：先写出可调优的软件，然后调优它以求获得足够的速度。

I’ve seen three general approaches to writing fast software. The most serious of these is time budgeting, often used in hard real­time systems. As you decompose the design, you give each component a budget for resources—time and footprint. That component must not exceed its budget, although a mechanism for exchanging budgeted resources is allowed. Time budgeting focuses attention on hard performance times. It is essential for systems, such as heart pacemakers, in which late data is always bad data. This technique is inappropriate for other kinds of systems, such as the corporate information systems with which I usually work.

我看过 3 种编写快速软件的方法。其中最严格的是时间预算法，这通常只用于性能要求极高的实时系统。如果使用这种方法，分解你的设计时就要做好预算，给每个组件预先分配一定资源，包括时间和空间占用。每个组件绝对不能超出自己的预算，就算拥有组件之间调度预配时间的机制也不行。这种方法高度重视性能，对于心律调节器一类的系统是必需的，因为在这样的系统中迟来的数据就是错误的数据。但对其他系统（例如我经常开发的企业信息系统）而言，如此追求高性能就有点儿过分了。

The second approach is the constant attention approach. Here, every programmer, all the time, does whatever she can to keep performance high. This is a common approach that is intuitively attractive—but it does not work very well. Changes that improve performance usually make the program harder to work with. This slows development. This would be a cost worth paying if the resulting software were quicker—but usually it is not. The performance improvements are spread all around the program; each improvement is made with a narrow perspective of the program’s behavior, and often with a misunderstanding of how a compiler, runtime, and hardware behaves.

第二种方法是持续关注法。这种方法要求任何程序员在任何时间做任何事时，都要设法保持系统的高性能。这种方式很常见，感觉上很有吸引力，但通常不会起太大作用。任何修改如果是为了提高性能，通常会使程序难以维护，继而减缓开发速度。如果最终得到的软件的确更快了，那么这点损失尚有所值，可惜通常事与愿违，因为性能改善一旦被分散到程序各个角落，每次改善都只不过是从对程序行为的一个狭隘视角出发而已，而且常常伴随着对编译器、运行时环境和硬件行为的误解。

『

### It Takes Awhile to Create Nothing

劳而无获

The Chrysler Comprehensive Compensation pay process was running too slowly. Although we were still in development, it began to bother us, because it was slowing down the tests.

Kent Beck, Martin Fowler, and I decided we’d fix it up. While I waited for us to get together, I was speculating, on the basis of my extensive knowledge of the system, about what was probably slowing it down. I thought of several possibilities and chatted with folks about the changes that were probably necessary. We came up with some really good ideas about what would make the system go faster.

Then we measured performance using Kent’s profiler. None of the possibilities I had thought of had anything to do with the problem. Instead, we found that the system was spending half its time creating instances of date. Even more interesting was that all the instances had the same couple of values.

Kent Beck、MartinFowler 和我决定解决这个问题。等待大伙儿会合的时间里，凭着对这个系统的全盘了解，我开始推测：到底是什么让系统变慢了？我想到数种可能，然后和伙伴们谈了几种可能的修改方案。最后，我们就「如何让这个系统运行更快」，提出了一些真正的好点子。然后，我们拿 Kent 的工具度量了系统性能。我一开始所想的可能性竟然全都不是问题肇因。我们发现：系统把一半时间用来创建「日期」实例（instance）。更有趣的是，所有这些实例都有相同的几个值。

When we looked at the date­creation logic, we saw some opportunities for optimizing how these dates were created. They were all going through a string conversion even though no external inputs were involved. The code was just using string conversion for convenience of typing. Maybe we could optimize that.

Then we looked at how these dates were being used. It turned out that the huge bulk of them were all creating instances of date range, an object with a from date and a to date. Looking around little more, we realized that most of these date ranges were empty!

于是我们观察日期对象的创建逻辑，发现有机会将它优化。这些日期对象在创建时都经过了一个字符串转换过程，然而这里并没有任何外部数据输入。之所以使用字符串转换方式，完全只是因为代码写起来简单。好，也许我们可以优化它。然后，我们观察这些日期对象是如何被使用的。我们发现，很多日期对象都被用来产生「日期区间」实例 —— 由一个起始日期和一个结束日期组成的对象。仔细追踪下去，我们发现绝大多数日期区间是空的！

As we worked with date range, we used the convention that any date range that ended before it started was empty. It’s a good convention and fits in well with how the class works. Soon after we started using this convention, we realized that just creating a date range that starts after it ends wasn’t clear code, so we extracted that behavior into a factory method for empty date ranges.

处理日期区间时我们遵循这样一个规则：如果结束日期在起始日期之前，这个日期区间就该是空的。这是一条很好的规则，完全符合这个类的需要。采用此规则后不久，我们意识到，创建一个「起始日期在结束日期之后」的日期区间，仍然不算是清晰的代码，于是我们把这个行为提炼成一个工厂函数，由它专门创建「空的日期区间」。

We had made that change to make the code clearer, but we received an unexpected payoff. We created a constant empty date range and adjusted the factory method to return that object instead of creating it every time. That change doubled the speed of the system, enough for the tests to be bearable. It took us about five minutes.

我们做了上述修改，使代码更加清晰，也意外得到了一个惊喜：可以创建一个固定不变的「空日期区间」对象，并让上述调整后的工厂函数始终返回该对象，而不再每次都创建新对象。这一修改把系统速度提升了几乎一倍，足以让测试速度达到可接受的程度。这只花了我们大约五分钟。

I had speculated with various members of the team (Kent and Martin deny participating in the speculation) on what was likely wrong with code we knew very well. We had even sketched some designs for improvements without first measuring what was going on. We were completely wrong. Aside from having a really interesting conversation, we were doing no good at all.

我和团队成员（Kent 和 Martin 谢绝参加）认真推测过：我们了若指掌的这个程序中可能有什么错误？我们甚至凭空做了些改进设计，却没有先对系统的真实情况进行度量。我们完全错了。除了一场很有趣的交谈，我们什么好事都没做。

The lesson is: Even if you know exactly what is going on in your system, measure performance, don’t speculate. You’ll learn something, and nine times out of ten, it won’t be that you were right!

— Ron Jeffries

教训是：哪怕你完全了解系统，也请实际度量它的性能，不要臆测。臆测会让你学到一些东西，但十有八九你是错的。

』

The interesting thing about performance is that in most programs, most of their time is spent in a small fraction of the code. If I optimize all the code equally, I’ll end up with 90 percent of my work wasted because it’s optimizing code that isn’t run much. The time spent making the program fast—the time lost because of lack of clarity—is all wasted time.

关于性能，一件很有趣的事情是：如果你对大多数程序进行分析，就会发现它把大半时间都耗费在一小半代码身上。如果你一视同仁地优化所有代码，90％ 的优化工作都是白费劲的，因为被你优化的代码大多很少被执行。你花时间做优化是为了让程序运行更快，但如果因为缺乏对程序的清楚认识而花费时间，那些时间就都被浪费掉了。

The third approach to performance improvement takes advantage of this 90­ percent statistic. In this approach, I build my program in a well­-factored manner without paying attention to performance until I begin a deliberate performance optimization exercise. During this performance optimization, I follow a specific process to tune the program.

第三种性能提升法就是利用上述的 90% 统计数据。采用这种方法时，我编写构造良好的程序，不对性能投以特别的关注，直至进入性能优化阶段 —— 那通常是在开发后期。一旦进入该阶段，我再遵循特定的流程来调优程序性能。

I begin by running the program under a profiler that monitors the program and tells me where it is consuming time and space. This way I can find that small part of the program where the performance hot spots lie. I then focus on those performance hot spots using the same optimizations I would use in the constant­attention approach. But since I’m focusing my attention on a hot spot, I’m getting much more effect with less work. Even so, I remain cautious. As in refactoring, I make the changes in small steps. After each step I compile, test, and rerun the profiler. If I haven’t improved performance, I back out the change. I continue the process of finding and removing hot spots until I get the performance that satisfies my users. 

在性能优化阶段，我首先应该用一个度量工具来监控程序的运行，让它告诉我程序中哪些地方大量消耗时间和空间。这样我就可以找出性能热点所在的一小段代码。然后我应该集中关注这些性能热点，并使用持续关注法中的优化手段来优化它们。由于把注意力都集中在热点上，较少的工作量便可显现较好的成果。即便如此，我还是必须保持谨慎。和重构一样，我会小幅度进行修改。每走一步都需要编译、测试，再次度量。如果没能提高性能，就应该撤销此次修改。我会继续这个「发现热点，去除热点」的过程，直到获得客户满意的性能为止。

Having a well­-factored program helps with this style of optimization in two ways. First, it gives me time to spend on performance tuning. With well-­factored code, I can add functionality more quickly. This gives me more time to focus on performance. (Profiling ensures I spend that time on the right place.) Second, with a well­-factored program I have finer granularity for my performance analysis. My profiler leads me to smaller parts of the code, which are easier to tune. With clearer code, I have a better understanding of my options and of what kind of tuning will work.

一个构造良好的程序可从两方面帮助这一优化方式。首先，它让我有比较充裕的时间进行性能调整，因为有构造良好的代码在手，我能够更快速地添加功能，也就有更多时间用在性能问题上（准确的度量则保证我把这些时间投在恰当地点）。其次，面对构造良好的程序，我在进行性能分析时便有较细的粒度。度量工具会把我带入范围较小的代码段中，而性能的调整也比较容易些。由于代码更加清晰，因此我能够更好地理解自己的选择，更清楚哪种调整起关键作用。

I’ve found that refactoring helps me write fast software. It slows the software in the short term while I’m refactoring, but makes it easier to tune during optimization. I end up well ahead.

我发现重构可以帮助我写出更快的软件。短期看来，重构的确可能使软件变慢，但它使优化阶段的软件性能调优更容易，最终还是会得到好的效果。

### 2.9 Where Did Refactoring Come From?

I’ve not succeeded in pinning down the birth of the term “refactoring.” Good programmers have always spent at least some time cleaning up their code. They do this because they have learned that clean code is easier to change than complex and messy code, and good programmers know that they rarely write clean code the first time around.

我曾经努力想找出「重构」（refactoring）一词的真正起源，但最终失败了。优秀程序员肯定至少会花一些时间来清理自己的代码。这么做是因为，他们知道整洁的代码比杂乱无章的代码更容易修改，而且他们知道自己几乎无法一开始就写出整洁的代码。

Refactoring goes beyond this. In this book, I’m advocating refactoring as a key element in the whole process of software development. Two of the first people to recognize the importance of refactoring were Ward Cunningham and Kent Beck, who worked with Smalltalk from the 1980s onward. Smalltalk is an environment that even then was particularly hospitable to refactoring. It is a very dynamic environment that allows you to quickly write highly functional software. Smalltalk had a very short compile-­link-execute cycle for its time, which made it easy to change things quickly at a time where overnight compile cycles were not unknown. It is also object­-oriented and thus provides powerful tools for minimizing the impact of change behind well­-defined interfaces. Ward and Kent explored software development approaches geared to this kind of environment, and their work developed into Extreme Programming. They realized that refactoring was important in improving their productivity and, ever since, have been working with refactoring, applying it to serious software projects and refining it.

重构不止如此。本书中我把重构看作整个软件开发过程的一个关键环节。最早认识重构重要性的两个人是 Ward Cunningham 和 Kent Beck，他们早在 20 世纪 80 年代就开始使用 Smalltalk，那是一个特别适合重构的环境。Smalltalk 是一个十分动态的环境，用它可以很快写出功能丰富的软件。Smalltalk 的「编译 - 链接 - 执行」周期非常短，因此很容易快速修改代码 —— 要知道，当时很多编程环境做一次编译就需要整晚时间。它支持面向对象，也有强大的工具，最大限度地将修改的影响隐藏于定义良好的接口背后。Ward 和 Kent 努力探索出一套适合这类环境的软件开发过程（如今，Kent 把这种风格叫作极限编程）。他们意识到：重构对于提高生产力非常重要。从那时起他们就一直在工作中运用重构技术，在正式的软件项目中使用它，并不断精炼重构的过程。

Ward and Kent’s ideas were a strong influence on the Smalltalk community, and the notion of refactoring became an important element in the Smalltalk culture. Another leading figure in the Smalltalk community is Ralph Johnson, a professor at the University of Illinois at Urbana­-Champaign, who is famous as one of the authors of the “Gang of Four” [gof] book on design patterns. One of Ralph’s biggest interests is in developing software frameworks. He explored how refactoring can help develop an efficient and flexible framework.

Ward 和 Kent 的思想对 Smalltalk 社区产生了极大影响，重构概念也成为 Smalltalk 文化中的一个重要元素。Smalltalk 社区的另一位领袖是 Ralph Johnson，伊利诺伊大学厄巴纳 - 香槟分校教授，著名的 GoF [gof] 之一。Ralph 最大的兴趣之一就是开发软件框架。他揭示了重构有助于灵活高效框架的开发。

Bill Opdyke was one of Ralph’s doctoral students and was particularly interested in frameworks. He saw the potential value of refactoring and saw that it could be applied to much more than Smalltalk. His background was in telephone switch development, in which a great deal of complexity accrues over time and changes are difficult to make. Bill’s doctoral research looked at refactoring from a tool builder’s perspective. Bill was interested in refactorings that would be useful for C++ framework development; he researched the necessary semantics­-preserving refactorings and showed how to prove they were semantics-­preserving and how a tool could implement these ideas. Bill’s doctoral thesis [Opdyke] was the first substantial work on refactoring.

Bill Opdyke 是 Ralph 的博士研究生，对框架也很感兴趣。他看到了重构的潜在价值，并看到重构应用于 Smalltalk 之外的其他语言的可能性。他的技术背景是电话交换系统的开发。在这种系统中，大量的复杂情况与日俱增，而且非常难以修改。Bill 的博士研究就是从工具构筑者的角度来看待重构。Bill 对 C++ 的框架开发中用得上的重构手法特别感兴趣。他也研究了极有必要的「语义保持的重构」（semantics-preserving refactoring），并阐明了如何证明这些重构是语义保持的，以及如何用工具实现重构。Bill 的博士论文 [Opdyke] 是重构领域中第一部丰硕的研究成果。

I remember meeting Bill at the OOPSLA conference in 1992. We sat in a café and he told me about his research. I remember thinking, “Interesting, but not really that important.” Boy, was I wrong! John Brant and Don Roberts took the refactoring tool ideas much further to produce the Refactoring Browser, the first refactoring tool, appropriately for the Smalltalk environment.

我还记得 1992 年 OOPSLA 大会上见到 Bill 的情景。我们坐在一间咖啡厅里，Bill 跟我谈起他的研究成果，我还记得自己当时的想法：「有趣，但并非真的那么重要。」唉，我完全错了。John Brant 和 Don Roberts 将「重构工具」的构想发扬光大，开发了一个名为 Refactoring Browser（重构浏览器）的重构工具。这是第一个自动化的重构工具，多亏 Smalltalk 提供了适合重构的编程环境。

And me? I’d always been inclined to clean code, but I’d never considered it to be that important. Then, I worked on a project with Kent and saw the way he used refactoring. I saw the difference it made in productivity and quality. That experience convinced me that refactoring was a very important technique. I was frustrated, however, because there was no book that I could give to a working programmer, and none of the experts above had any plans to write such a book. So, with their help, I did—which led to the first edition of this book.

那么，我呢？我一直有清理代码的倾向，但从来没有想到这会如此重要。后来我和 Kent 一起做一个项目，看到他使用重构手法，也看到重构对开发效能和质量带来的影响。这份体验让我相信：重构是一门非常重要的技术。但是，在重构的学习和推广过程中我遇到了挫折，因为我拿不出任何一本书给程序员看，也没有任何一位专家打算写这样一本书。所以，在这些专家的帮助下，我写下了这本书的第 1 版。

Fortunately, the concept of refactoring caught on in the industry. The book sold well, and refactoring entered the vocabulary of most programmers. More tools appeared, especially for Java. One downside of this popularity has been people using “refactoring” loosely, to mean any kind of restructuring. Despite this, however, it has become a mainstream practice.

幸运的是，重构的概念被行业广泛接受了。本书第 1 版销量不错，「重构」一词也走进了大多数程序员的词汇库。更多的重构工具涌现出来，尤其是在 Java 世界里。重构的流行也带来了负面效应：很多人随意地使用「重构」这个词，而他们真正做的却是不严谨的结构调整。尽管如此，重构终归成了一项主流的软件开发实践。

### 2.10 Automated Refactorings

Perhaps the biggest change to refactoring in the last decade or so is the availability of tools that support automated refactoring. If I want to rename a method in Java and I’m using IntelliJ IDEA [intellij] or Eclipse [eclipse] (to mention just two), I can do it by picking an item off the menu. The tool completes the refactoring for me—and I’m usually sufficiently confident in its work that I don’t bother running the test suite. 

The first tool that did this was the Smalltalk Refactoring Browser, written by John Brandt and Don Roberts. The idea took off in the Java community very rapidly at the beginning of the century. When JetBrains launched their IntelliJ IDEA IDE, automated refactoring was one of the compelling features. IBM followed suit shortly afterwards with refactoring tools in Visual Age for Java. Visual Age didn’t have a big impact, but much of its capabilities were reimplemented in Eclipse, including the refactoring support. Refactoring also came to C#, initially via JetBrains’s Resharper, a plug­in for Visual Studio. Later on, the Visual Studio team added some refactoring capabilities.

过去 10 年中，重构领域最大的变化可能就是出现了一批支持自动化重构的工具。如果我想给一个 Java 的方法改名，在 IntelliJ IDEA 或者 Eclipse 这样的开发环境中，我只需要从菜单里点选对应的选项，工具会帮我完成整个重构过程，而且我通常都可以相信，工具完成的重构是可靠的，所以用不着运行测试套件。

第一个自动化重构工具是 Smalltalk 的 Refactoring Browser，由 John Brandt 和 Don Roberts 开发。在 21 世纪初，Java 世界的自动化重构工具如雨后春笋般涌现。在 Jet Brains 的 IntelliJ IDEA 集成开发环境（IDE）中，自动化重构是最亮眼的特性之一。IBM 也紧随其后，在 VisualAge 的 Java 版中也提供了重构工具。VisualAge 的影响力有限，不过其中很多能力后来被 Eclipse 继承，包括对重构的支持。重构也进入了 C# 世界，起初是通过 JetBrains 的 Resharper，这是一个 VisualStudio 插件。后来 VisualStudio 团队直接在 IDE 里提供了一些重构能力。

It’s now pretty common to find some kind of refactoring support in editors and tools, although the actual capabilities vary a fair bit. Some of this variation is due to the tool, some is caused by the limitations of what you can do with automated refactoring in different languages. I’m not going to analyze the capabilities of different tools here, but I think it is worth talking a bit about some of the underlying principles.

A crude way to automate a refactoring is to do text manipulation, such as a search/replace to change a name, or some simple reorganizing of code for Extract Variable (119). This is a very crude approach that certainly can’t be trusted without rerunning tests. It can, however, be a handy first step. I’ll use such macros in Emacs to speed up my refactoring work when I don’t have more sophisticated refactorings available to me.

如今的编辑器和开发工具中常能找到一些对重构的支持，不过真实的重构能力各有高低。重构能力的差异既有工具的原因，也受限于不同语言对自动化重构的支持程度。在这里，我不打算分析各种工具的能力，不过谈谈重构工具背后的原则还是有点儿意思的。一种粗糙的自动化重构方式是文本操作，比如用查找 / 替换的方式给函数改名，或者完成提炼变量（119）所需的简单结构调整。这种方法太粗糙了，做完之后必须重新运行测试，否则不能信任。但这可以是一个便捷的起步。在用 Emacs 编程时，没有那些更完善的重构支持，我也会用类似的文本操作宏来加速重构。

To do refactoring properly, the tool has to operate on the syntax tree of the code, not on the text. Manipulating the syntax tree is much more reliable to preserve what the code is doing. This is why at the moment, most refactoring capabilities are part of powerful IDEs—they use the syntax tree not just for refactoring but also for code navigation, linting, and the like. This collaboration between text and syntax tree is what takes them beyond text editors.

要支持体面的重构，工具只操作代码文本是不行的，必须操作代码的语法树，这样才能更可靠地保持代码行为。所以，今天的大多数重构功能都依附于强大的 IDE，因为这些 IDE 原本就在语法树上实现了代码导航、静态检查等功能，自然也可以用于重构。不仅能处理文本，还能处理语法树，这是 IDE 相比于文本编辑器更先进的地方。

Refactoring isn’t just understanding and updating the syntax tree. The tool also needs to figure out how to rerender the code into text back in the editor view. All in all, implementing decent refactoring is a challenging programming exercise—one that I’m mostly unaware of as I gaily use the tools.

重构工具不仅需要理解和修改语法树，还要知道如何把修改后的代码写回编辑器视图。总而言之，实现一个体面的自动化重构手法，是一个很有挑战的编程任务。尽管我一直开心地使用重构工具，对它们背后的实现却知之甚少。

Many refactorings are made much safer when applied in a language with static typing. Consider the simple Rename Function (124). I might have addClient methods on my Salesman class and on my Server class. I want to rename the one on my salesman, but it is different in intent from the one on my server, which I don’t want to rename. Without static typing, the tool will find it difficult to tell whether any call to addClient is intended for the salesman. In the refactoring browser, it would generate a list of call sites and I would manually decide which ones to change. This makes it a nonsafe refactoring that forces me to rerun the tests. Such a tool is still helpful—but the equivalent operation in Java can be completely safe and automatic. Since the tool can resolve the method to the correct class with static typing, I can be confident that the tool changes only the methods it ought to.

在静态类型语言中，很多重构手法会更加安全。假设我想做一次简单的函数改名（124）：在 Salesman 类和 Server 类中都有一个叫作 addClient 的函数，当然两者各有其用途。我想对 Salesman 中的 addClient 函数改名，Server 类中的函数则保持不变。如果不是静态类型，工具很难识别调用 addClient 的地方到底是在使用哪个类的函数。Smalltalk 的 Refactoring Browser 会列出所有调用点，我需要手工决定修改哪些调用点。这个重构是不安全的，我必须重新运行所有测试。这样的工具仍然有用，但在 Java 中的函数改名（124）重构则可以是完全安全、完全自动的，因为在静态类型的帮助下，工具可以识别函数所属的类，所以它只会修改应该修改的那些函数调用点，对此我可以完全放心。

Tools often go further. If I rename a variable, I can be prompted for changes to comments that use that name. If I use Extract Function (106), the tool spots some code that duplicates the new function’s body and offers to replace it with a call. Programming with powerful refactorings like this is a compelling reason to use an IDE rather than stick with a familiar text editor. Personally I’m a big user of Emacs, but when working in Java I prefer IntelliJ IDEA or Eclipse—in large part due to the refactoring support.

一些重构工具走得更远。如果我给一个变量改名，工具会提醒我修改使用了旧名字的注释。如果我使用提炼函数（106），工具会找出与新函数体重复的代码片段，建议代之以对新函数的调用。在编程时可以使用如此强大的重构功能，这就是为什么我们要使用一个体面的 IDE，而不是固执于熟悉的文本编辑器。我个人很喜欢用 Emacs，但在使用 Java 时，我更愿意用 IntelliJ IDEA 或者 Eclipse，很大程度上就是为了获得重构支持。

While sophisticated refactoring tools are almost magical in their ability to safely refactor code, there are some edge cases where they slip up. Less mature tools struggle with reflective calls, such as Method.invoke in Java (although more mature tools handle this quite well). So even with mostly safe refactorings, it’s wise to run the test suite every so often to ensure nothing has gone pear­shaped. Usually I’m refactoring with a mix of automated and manual refactorings, so I run my tests often enough.

尽管这些强大的重构工具有着魔法般的能力，可以安全地重构代码，但还是会有闪失出现。通过反射进行的调用（例如 Java 中的 Method.invoke）会迷惑不够成熟的重构工具，但比较成熟的工具则可以很好地应对。所以，即便是最安全的重构，也应该经常运行测试套件，以确保没有什么东西在不经意间被破坏。我经常会间杂进行自动重构和手动重构，所以运行测试的频度是足够的。

The power of using the syntax tree to analyze and refactor programs is a compelling advantage for IDEs over simple text editors, but many programmers prefer the flexibility of their favorite text editor and would like to have both. A technology that’s currently gaining momentum is Language Servers [langserver]: software that will form a syntax tree and present an API to text editors. Such language servers can support many text editors and provide commands to do sophisticated code analysis and refactoring operations.

能借助语法树来分析和重构程序代码，这是 IDE 与普通文本编辑器相比具有的一大优势。但很多程序员又喜欢用得顺手的文本编辑器的灵活性，希望鱼与熊掌兼得。语言服务器（Language Server）是一种正在引起关注的新技术：用软件生成语法树，给文本编辑器提供 API。语言服务器可以支持多种文本编辑器，并且为强大的代码分析和重构操作提供了命令。

### 2.11 Going Further

It seems a little strange to be talking about further reading in only the second chapter, but this is as good a spot as any to point out there is more material out there on refactoring that goes beyond the basics in this book.

This book has taught refactoring to many people, but I have focused more on a refactoring reference than on taking readers through the learning process. If you are looking for such a book, I suggest Bill Wake’s Refactoring Workbook [Wake] that contains many exercises to practice refactoring.

Many of those who pioneered refactoring were also active in the software patterns community. Josh Kerievsky tied these two worlds closely together with Refactoring to Patterns [Kerievsky], which looks at the most valuable patterns from the hugely influential “Gang of Four” book [gof] and shows how to use refactoring to evolve towards them.

This book concentrates on refactoring in general­-purpose programming, but refactoring also applies in specialized areas. Two that have got useful attention are Refactoring Databases [Ambler & Sadalage] (by Scott Ambler and Pramod Sadalage) and Refactoring HTML [Harold] (by Elliotte Rusty Harold).

Although it doesn’t have refactoring in the title, also worth including is Michael Feathers’s Working Effectively with Legacy Code [Feathers], which is primarily a book about how to think about refactoring an older codebase with poor test coverage.

Although this book (and its predecessor) are intended for programmers with any language, there is a place for language-­specific refactoring books. Two of my former colleagues, Jay Fields and Shane Harvey, did this for the Ruby programming language [Fields et al.].

For more up­to­date material, look up the web representation of this book, as well as the main refactoring web site: [refactoring.com](https://refactoring.com/) [ref.com]. 

2『已下载书籍「2020146Refactoring-Workbook」、「2020110Refactoring-to-Patterns」、「2020147Refactoring-Databases」、「2020148Refactoring-HTML」、「2019031Working-Effectively-with-Legacy-Code」。』
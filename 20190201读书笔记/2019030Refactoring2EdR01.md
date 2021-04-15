## 记忆时间

## 0101. Refactoring: A First Example Topics

How do I begin to talk about refactoring? The traditional way is by introducing the history of the subject, broad principles, and the like. When somebody does that at a conference, I get slightly sleepy. My mind starts wandering, with a low­-priority background process polling the speaker until they give an example. The examples wake me up because I can see what is going on. With principles, it is too easy to make broad generalizations—and too hard to figure out how to apply things. An example helps make things clear.

So I’m going to start this book with an example of refactoring. I’ll talk about how refactoring works and will give you a sense of the refactoring process. I can then do the usual principles-­style introduction in the next chapter.

With any introductory example, however, I run into a problem. If I pick a large program, describing it and how it is refactored is too complicated for a mortal reader to work through. (I tried this with the original book—and ended up throwing away two examples, which were still pretty small but took over a hundred pages each to describe.) However, if I pick a program that is small enough to be comprehensible, refactoring does not look like it is worthwhile.

I’m thus in the classic bind of anyone who wants to describe techniques that are useful for real­world programs. Frankly, it is not worth the effort to do all the refactoring that I’m going to show you on the small program I will be using. But if the code I’m showing you is part of a larger system, then the refactoring becomes important. Just look at my example and imagine it in the context of a much larger system.

### Final Thoughts

This is a simple example, but I hope it will give you a feeling for what refactoring is like. I’ve used several refactorings, including Extract Function (106), Inline Variable (123), Move Function (198), and Replace Conditional with Polymorphism (272).

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

在 vue 里实现，把逻辑代码、数据都从 vue 文件里剥离出来，也方便做测试的，哈哈。（2020-09-25）：

`data.js`

```js
export const invoices = {
  customer: 'BigCo',
  performances: [
    {
      playID: 'hamlet',
      audience: 55
    },
    {
      playID: 'dalong',
      audience: 35
    },
    {
      playID: 'othello',
      audience: 40
    }
  ]
}

export const plays = {
  hamlet: {
    name: 'Hamlet',
    type: 'tragedy'
  },
  dalong: {
    name: 'As You Like It',
    type: 'comedy'
  },
  othello: {
    name: 'Othello',
    type: 'tragedy'
  }
}
```

`statement.js`

```js
import { invoices, plays } from '@/code/data'

export function statement() {
  let totalAmount = 0
  let volumeCredits = 0
  let result = `Statement for ${invoices.customer}\n`
  const format = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2
  }).format
  for (const perf of invoices.performances) {
    const play = plays[perf.playID]
    let thisAmount = 0

    switch (play.type) {
      case 'tragedy':
        thisAmount = 40000
        if (perf.audience > 30) {
          thisAmount += 1000 * (perf.audience - 30)
        }
        break
      case 'comedy':
        thisAmount = 30000
        if (perf.audience > 20) {
          thisAmount += 10000 + 500 * (perf.audience - 20)
        }
        thisAmount += 300 * perf.audience
        break
      default:
        throw new Error(`unkown type: ${play.type}`)
    }
    // add volume credits
    volumeCredits += Math.max(perf.audience - 30, 0)
    // add extra credit for every ten comedy attendees
    if (play.type === 'comedy') {
      volumeCredits += Math.floor(perf.audience / 5)
    }

    // print line for this order
    result += `${play.name}: ${format(thisAmount / 100)}(${perf.audience} seats)\n`
    totalAmount += thisAmount
  }
  result += `Amount owed is ${format(totalAmount / 100)}\n`
  result += `You earned ${volumeCredits} credits\n`
  console.log(result)
}

```

```js
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <el-button type="primary" @click="statement">测试按钮</el-button>
  </div>
</template>

<script>
import { statement } from '@/code/statement'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  methods: {
    test() {
      console.log('dalong')
    },
    statement
  }
}
</script>
```

真的超级奇怪，字符串「aslike」属性名就是识别不了，最后换成了「dalong」，感觉应该是 eslint 造成的，待确认。（2020-09-25）

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

看着这块代码，我就知道它在计算一场戏剧演出的费用。这是我的直觉。不过正如 Ward Cunningham 所说，这种理解只是我脑海中转瞬即逝的灵光。我需要梳理这些灵感，将它们从脑海中搬回到代码里去，以免忘记。这样当我回头看时，代码就能告诉我它在干什么，我不需要重新思考一遍。要将我的理解转化到代码里，得先将这块代码抽取成一个独立的函数，按它所干的事情给它命名，比如叫 amountFor(performance)。每次想将一块代码抽取成一个函数时，我都会遵循一个标准流程，最大程度减少犯错的可能。我把这个流程记录了下来，并将它命名为提炼函数（106），以便日后可以方便地引用。

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

当我在代码块上方使用了斜体（中文对应为楷体）标记的题头「function xxx」时，表明该代码块位于题头所在函数、文件或类的作用域内。通常该作用域内还有其他的代码，但由于不是讨论重点，因此把它们隐去不展示。现在原 statement 函数可以直接调用这个新函数来初始化 thisAmount。

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

自己的代码：

`statement.js`

```js
import { invoices, plays } from '@/code/data'

function amountFor(perf, play) {
  let thisAmount = 0

  switch (play.type) {
    case 'tragedy':
      thisAmount = 40000
      if (perf.audience > 30) {
        thisAmount += 1000 * (perf.audience - 30)
      }
      break
    case 'comedy':
      thisAmount = 30000
      if (perf.audience > 20) {
        thisAmount += 10000 + 500 * (perf.audience - 20)
      }
      thisAmount += 300 * perf.audience
      break
    default:
      throw new Error(`unkown type: ${play.type}`)
  }
  return thisAmount
}

export function statement() {
  let totalAmount = 0
  let volumeCredits = 0
  let result = `Statement for ${invoices.customer}\n`
  const format = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2
  }).format
  for (const perf of invoices.performances) {
    const play = plays[perf.playID]
    const thisAmount = amountFor(perf, play)

    // add volume credits
    volumeCredits += Math.max(perf.audience - 30, 0)
    // add extra credit for every ten comedy attendees
    if (play.type === 'comedy') {
      volumeCredits += Math.floor(perf.audience / 5)
    }

    // print line for this order
    result += `${play.name}: ${format(thisAmount / 100)}(${perf.audience} seats)\n`
    totalAmount += thisAmount
  }
  result += `Amount owed is ${format(totalAmount / 100)}\n`
  result += `You earned ${volumeCredits} credits\n`
  console.log(result)
  return format(totalAmount / 100)
}
```

』

Once I’ve made this change, I immediately compile and test to see if I’ve broken anything. It’s an important habit to test after every refactoring, however simple. Mistakes are easy to make—at least, I find them easy to make. Testing after each change means that when I make a mistake, I only have a small change to consider in order to spot the error, which makes it far easier to find and fix. This is the essence of the refactoring process: small changes and testing after each change. If I try to do too much, making a mistake will force me into a tricky debugging episode that can take a long time. Small changes, enabling a tight feedback loop, are the key to avoiding that mess.

1『无论多小的改动，改完后直接再跑一下，看看跟改前跑的结果是够一样，一定要养成这个习惯。回复：用 CLI 环境里搭建的，用 Jest 先搭建好测试，在测试框架下重构，实在是太爽了。（2020-09-25）』

I use compile here to mean doing whatever is needed to make the JavaScript executable. Since JavaScript is directly executable, that may mean nothing, but in other cases it may mean moving code to an output directory and/or using a processor such as Babel [babel].

Refactoring changes the programs in small steps, so if you make a mistake, it is easy to find where the bug is.

This being JavaScript, I can extract amountFor into a nested function of statement. This is helpful as it means I don’t have to pass data that’s inside the scope of the containing function to the newly extracted function. That doesn’t make a difference in this case, but it’s one less issue to deal with. In this case the tests passed, so my next step is to commit the change to my local version control system. I use a version control system, such as git or mercurial, that allows me to make private commits. I commit after each successful refactoring, so I can easily get back to a working state should I mess up later. I then squash changes into more significant commits before I push the changes to a shared repository.

这里我使用的「编译」一词，指的是将 JavaScript 变为可执行代码之前的所有步骤。虽然 JavaScript 可以直接执行，有时可能不需任何步骤，但有时可能需要将代码移动到一个输出目录，或使用 Babel 这样的代码处理器等。因为是 JavaScript，我可以直接将 amountFor 提炼成为 statement 的一个内嵌函数。这个特性十分有用，因为我就不需要再把外部作用域中的数据传给新提炼的函数。这个示例中可能区别不大，但也是少了一件要操心的事。

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

1『在 vim 里用正则做替换真实方便，比如上面的实现：`:%s/thisAmount/result/c`，参数 c 表示替换前要一个个确认，如果没必要确认的话改成 g 即可，目前绝大多数情况下都是要确认的。（2020-09-25）』

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

I begin by extracting the right­hand side of the assignment into a function. I compile­-test-­commit. With that inlined, I can then apply Change Function Declaration (124) to amountFor to remove the play parameter. I do this in two steps. First, I use the new function inside amountFor.

编译、测试、提交。完成变量内联后，我可以对 amountFor 函数应用改变函数声明（124），移除 play 参数。 我会分两步走。首先在 amountFor 函数内部使用新提炼的函数。

I compile-­test-­commit, and then delete the parameter. And compile-­test-­commit again.

This refactoring alarms some programmers. Previously, the code to look up the play was executed once in each loop iteration; now, it’s executed thrice. I’ll talk about the interplay of refactoring and performance later, but for the moment I’ll just observe that this change is unlikely to significantly affect performance, and even if it were, it is much easier to improve the performance of a well­factored code base.

这次重构可能在一些程序员心中敲响警钟：重构前，查找 play 变量的代码在每次循环中只执行了 1 次，而重构后却执行了 3 次。我会在后面探讨重构与性能之间的关系，但现在，我认为这次改动还不太可能对性能有严重影响，即便真的有所影响，后续再对一段结构良好的代码进行性能调优， 也容易得多。

The great benefit of removing local variables is that it makes it much easier to do extractions, since there is less local scope to deal with. Indeed, usually I’ll take out local variables before I do any extractions. Now that I’m done with the arguments to amountFor, I look back at where it’s called. It’s being used to set a temporary variable that’s not updated again, so I apply Inline Variable (123).

移除局部变量的好处就是做提炼时会简单得多，因为需要操心的局部作用域变少了。实际上，在做任何提炼前，我一般都会先移除局部变量。

```js
import { invoices, plays } from '@/code/data'

function amountFor(aPerformance) {
  let result = 0

  switch (playFor(aPerformance).type) {
    case 'tragedy':
      result = 40000
      if (aPerformance.audience > 30) {
        result += 1000 * (aPerformance.audience - 30)
      }
      break
    case 'comedy':
      result = 30000
      if (aPerformance.audience > 20) {
        result += 10000 + 500 * (aPerformance.audience - 20)
      }
      result += 300 * aPerformance.audience
      break
    default:
      throw new Error(`unkown type: ${playFor(aPerformance).type}`)
  }
  return result
}

function playFor(aPerformance) {
  return plays[aPerformance.playID]
}

export function statement() {
  let totalAmount = 0
  let volumeCredits = 0
  let result = `Statement for ${invoices.customer}\n`
  const format = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2
  }).format
  for (const perf of invoices.performances) {
    // add volume credits
    volumeCredits += Math.max(perf.audience - 30, 0)
    // add extra credit for every ten comedy attendees
    if (playFor(perf).type === 'comedy') {
      volumeCredits += Math.floor(perf.audience / 5)
    }

    // print line for this order
    result += `${playFor(perf).name}: ${format(amountFor(perf) / 100)}(${perf.audience} seats)\n`
    totalAmount += amountFor(perf)
  }
  result += `Amount owed is ${format(totalAmount / 100)}\n`
  result += `You earned ${volumeCredits} credits\n`
  console.log(result)
  return format(totalAmount / 100)
}
```

1『真是魔术般的消除了中间变量啊。关键步骤：1）提炼出 `playFor()` 函数。2）`playFor(perf)` 直接作为参数传进函数 `amountFor(perf, playFor(perf))`。3）把 `amountFor()` 函数里的 `play` 全部替换为 `playFor(perf)`，这样就消除了临工变量 `play`，传入 `amountFor()` 函数的参数只需要是 `perf` 即可。4）直接用函数调用 `amountFor(perf)` 替换掉临时变量 `thisAmount`。』

#### 1.4.2 Extracting Volume Credits

Here’s the current state of the statement function body:

Now I get the benefit from removing the play variable as it makes it easier to extract the volume credits calculation by removing one of the locally scoped variables. I still have to deal with the other two. Again, perf is easy to pass in, but volumeCredits is a bit more tricky as it is an accumulator updated in each pass of the loop. So my best bet is to initialize a shadow of it inside the extracted function and return it.

这会儿我们就看到了移除 play 变量的好处，移除了一个局部作用域的变量，提炼观众量积分的计算逻辑又更简单一些。我仍需要处理其他两个局部变量。perf 同样可以轻易作为参数传入，但 volumeCredits 变量则有些棘手。它是一个累加变量，循环的每次迭代都会更新它的值。因此最简单的方式是，将整块逻辑提炼到新函数中，然后在新函数中直接返回 volumeCredits。

I remove the unnecessary (and, in this case, downright misleading) comment. I compile-test-­commit that, and then rename the variables inside the new function. function statement…

I’ve shown it in one step, but as before I did the renames one at a time, with a compile-test-­commit after each.

```js
function playFor(aPerformance) {
  return plays[aPerformance.playID]
}

function volumeCreditsFor(aPerformance) {
  let result = 0
  // add volume credits
  result += Math.max(aPerformance.audience - 30, 0)
  // add extra credit for every ten comedy attendees
  if (playFor(aPerformance).type === 'comedy') {
    result += Math.floor(aPerformance.audience / 5)
  }
  return result
}

export function statement() {
  let totalAmount = 0
  let volumeCredits = 0
  let result = `Statement for ${invoices.customer}\n`
  const format = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2
  }).format
  for (const perf of invoices.performances) {
    volumeCredits = volumeCreditsFor(perf)
    // print line for this order
    result += `${playFor(perf).name}: ${format(amountFor(perf) / 100)}(${perf.audience} seats)\n`
    totalAmount += amountFor(perf)
  }
  result += `Amount owed is ${format(totalAmount / 100)}\n`
  result += `You earned ${volumeCredits} credits\n`
  console.log(result)
  return format(totalAmount / 100)
}
```

#### 1.4.3 Removing the format Variable

Let’s look at the main statement method again:

As I suggested before, temporary variables can be a problem. They are only useful within their own routine, and therefore they encourage long, complex routines. My next move, then, is to replace some of them. The easiest one is format. This is a case of assigning a function to a temp, which I prefer to replace with a declared function.

正如我上面所指出的，临时变量往往会带来麻烦。它们只在对其进行处理的代码块中有用，因此临时变量实质上是鼓励你写长而复杂的函数。因此，下一步我要替换掉一些临时变量，而最简单的莫过于从 format 变量入手。这是典型的「将函数赋值给临时变量」的场景，我更愿意将其替换为一个明确声明的函数。

Although changing a function variable to a declared function is a refactoring, I haven’t named it and included it in the catalog. There are many refactorings that I didn’t feel important enough for that. This one is both simple to do and relatively rare, so I didn’t think it was worthwhile.

尽管将函数变量改变成函数声明也是一种重构手法， 但我既未为此手法命名，也未将它纳入重构名录。还有很多的重构手法我都觉得没那么重要。我觉得上面这个函数改名的手法既十分简单又不太常用，不值得在重构名录中占有一席之地。

I’m not keen on the name—“format” doesn’t really convey enough of what it’s doing. “formatAsUSD” would be a bit too long­winded since it’s being used in a string template, particularly within this small scope. I think the fact that it’s formatting a currency amount is the thing to highlight here, so I pick a name that suggests that and apply Change Function Declaration (124). 

我对提炼得到的函数名称不很满意——format 未能清晰地描述其作用。formatAsUSD 很表意，但又太长，特别它仅是小范围地被用在一个字符串模板中。我认为这里真正需要强调的是，它格式化的是一个货币数字，因此我选取了一个能体现此意图的命名，并应用了改变函数声明（124）手法。

Naming is both important and tricky. Breaking a large function into smaller ones only adds value if the names are good. With good names, I don’t have to read the body of the function to see what it does. But it’s hard to get names right the first time, so I use the best name I can think of for the moment, and don’t hesitate to rename it later. Often, it takes a second pass through some code to realize what the best name really is.

好的命名十分重要，但往往并非唾手可得。只有恰如其分地命名，才能彰显出将大函数分解成小函数的价值。有了好的名称，我就不必通过阅读函数体来了解其行为。但要一次把名取好并不容易，因此我会使用当下能想到最好的那个。如果稍后想到更好的，我就会毫不犹豫地换掉它。通常你需要花几秒钟通读更多代码，才能发现最好的名称是什么。

As I’m changing the name, I also move the duplicated division by 100 into the function. Storing money as integer cents is a common approach—it avoids the dangers of storing fractional monetary values as floats but allows me to use arithmetic operators. Whenever I want to display such a penny­integer number, however, I need a decimal, so my formatting function should take care of the division.

重命名的同时，我还将重复的除以 100 的行为也搬移到函数里。将钱以美分为单位作为正整数存储是一种常见的做法，可以避免使用浮点数来存储货币的小数部分，同时又不影响用数学运算符操作它。不过，对于这样一个以美分为单位的整数，我又需要以美元为单位进行展示，因此让格式化函数来处理整除的事宜再好不过。

```js
function usd(aNumber) {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2
  }).format(aNumber/100)
}

export function statement() {
  let totalAmount = 0
  let volumeCredits = 0
  let result = `Statement for ${invoices.customer}\n`
  for (const perf of invoices.performances) {
    volumeCredits = volumeCreditsFor(perf)
    // print line for this order
    result += `${playFor(perf).name}: ${usd(amountFor(perf))}(${perf.audience} seats)\n`
    totalAmount += amountFor(perf)
  }
  result += `Amount owed is ${usd(totalAmount)}\n`
  result += `You earned ${volumeCredits} credits\n`
  console.log(result)
  return usd(totalAmount)
}
```

1『这个格式化函数 `usd()` 的写法很值得去研究学习。（2020-09-25）』

#### 1.4.4 Removing Total Volume Credits

My next target variable is volumeCredits. This is a trickier case, as it’s built up during the iterations of the loop. My first move, then, is to use Split Loop (227) to separate the accumulation of volumeCredits.

我的下一个重构目标是 volumeCredits。处理这个变量更加微妙，因为它是在循环的迭代过程中累加得到的。第一步，就是应用拆分循环（227）将 volumeCredits 的累加过程分离出来。

With that done, I can use Slide Statements (223) to move the declaration of the variable next to the loop.

完成这一步，我就可以使用移动语句（223）手法将变量声明挪动到紧邻循环的位置。

```js
export function statement() {
  let totalAmount = 0
  let result = `Statement for ${invoices.customer}\n`
  for (const perf of invoices.performances) {
    // print line for this order
    result += `${playFor(perf).name}: ${usd(amountFor(perf))}(${perf.audience} seats)\n`
    totalAmount += amountFor(perf)
  }

  let volumeCredits = 0
  for (const perf of invoices.performances) {
    volumeCredits = volumeCreditsFor(perf)
  }

  result += `Amount owed is ${usd(totalAmount)}\n`
  result += `You earned ${volumeCredits} credits\n`
  console.log(result)
  return usd(totalAmount)
}
```

Gathering together everything that updates the volumeCredits variable makes it easier to do Replace Temp with Query (178). As before, the first step is to apply Extract Function (106) to the overall calculation of the variable.

把与更新 volumeCredits 变量相关的代码都集中到一起，有利于以查询取代临时变量（178）手法的施展。第一步同样是先对变量的计算过程应用提炼函数（106）手法。

```js
function totalVolumeCredits() {
  let volumeCredits = 0
  for (const perf of invoices.performances) {
    // add volume credits
    volumeCredits += volumeCreditsFor(perf)
  }
  return volumeCredits
}

export function statement() {
  let totalAmount = 0
  let result = `Statement for ${invoices.customer}\n`

  for (const perf of invoices.performances) {
    // print line for this order
    result += `${playFor(perf).name}: ${usd(amountFor(perf))}(${perf.audience} seats)\n`
    totalAmount += amountFor(perf)
  }

  result += `Amount owed is ${usd(totalAmount)}\n`
  result += `You earned ${totalVolumeCredits()} credits\n`
  console.log(result)
  return usd(totalAmount)
}
```

1『这里有个小插曲。`volumeCredits` 本来算出来是 47，现在是 10，找原因找了很久，发现循环体里的加法没有叠加上去，一直找不到哪里错了。后来发现是 `totalVolumeCredits` 函数里，叠加语句里少掉了加法，错误如：`volumeCredits = volumeCreditsFor(perf)`，真的是个惨痛的教训，这个错误大概找了一个半小时！（2020-09-25）』

Once everything is extracted, I can apply Inline Variable (123):

Let me pause for a bit to talk about what I’ve just done here. Firstly, I know readers will again be worrying about performance with this change, as many people are wary of repeating a loop. But most of the time, rerunning a loop like this has a negligible effect on performance. If you timed the code before and after this refactoring, you would probably not notice any significant change in speed—and that’s usually the case. Most programmers, even experienced ones, are poor judges of how code actually performs. Many of our intuitions are broken by clever compilers, modern caching techniques, and the like. The performance of software usually depends on just a few parts of the code, and changes anywhere else don’t make an appreciable difference.

首先，我知道有些读者会再次对此修改可能带来的性能问题感到担忧，我知道很多人本能地警惕重复的循环。但大多数时候，重复一次这样的循环对性能的影响都可忽略不计。如果你在重构前后进行计时，很可能甚至都注意不到运行速度的变化——通常也确实没什么变化。许多程序员对代码实际的运行路径都所知不足，甚至经验丰富的程序员有时也未能避 免。在聪明的编译器、现代的缓存技术面前，我们很多直觉都是不准确的。软件的性能通常只与代码的一小部分相关， 改变其他的部分往往对总体性能贡献甚微。

But “mostly” isn’t the same as “alwaysly.” Sometimes a refactoring will have a significant performance implication. Even then, I usually go ahead and do it, because it’s much easier to tune the performance of well­factored code. If I introduce a significant performance issue during refactoring, I spend time on performance tuning afterwards. It may be that this leads to reversing some of the refactoring I did earlierbut most of the time, due to the refactoring, I can apply a more effective performancetuning enhancement instead. I end up with code that’s both clearer and faster.

当然，「大多数时候」不等同于「所有时候」。有时， 一些重构手法也会显著地影响性能。但即便如此，我通常也不去管它，继续重构，因为有了一份结构良好的代码，回头调优其性能也容易得多。如果我在重构时引入了明显的性能损耗，我后面会花时间进行性能调优。进行调优时，可能会回退我早先做的一些重构——但更多时候，因为重构我可以使用更高效的调优方案。最后我得到的是既整洁又高效的代码。

So, my overall advice on performance with refactoring is: Most of the time you should ignore it. If your refactoring introduces performance slow­downs, finish refactoring first and do performance tuning afterwards.

The second aspect I want to call your attention to is how small the steps were to remove volumeCredits. Here are the four steps, each followed by compiling, testing, and committing to my local source code repository: 1) Split Loop (227) to isolate the accumulation. 2) Slide Statements (223) to bring the initializing code next to the accumulation. 3) Extract Function (106) to create a function for calculating the total. 4) Inline Variable (123) to remove the variable completely.

对于重构过程的性能问题，我总体的建议是：大多数情况下可以忽略它。如果重构引入了性能损耗，先完成重构，再做性能优化。其次，我希望你能注意到：我们移除 volumeCredits 的过程是多么小步。整个过程一共有4步，每一步都伴随着一次编译、测试以及向本地代码库的提交：1）使用拆分循环（227）分离出累加过程；2）使用移动语句（223）将累加变量的声明与累加过程集中到一起；3）使用提炼函数（106）提炼出计算总数的函数；4）使用内联变量（123）完全移除中间变量。

I confess I don’t always take quite as short steps as these—but whenever things get difficult, my first reaction is to take shorter steps. In particular, should a test fail during a refactoring, if I can’t immediately see and fix the problem, I’ll revert to my last good commit and redo what I just did with smaller steps. That works because I commit so frequently and because small steps are the key to moving quickly, particularly when working with difficult code.

I then repeat that sequence to remove totalAmount. I start by splitting the loop (compile­test­commit), then I slide the variable initialization (compile-­test-­commit), and then I extract the function. There is a wrinkle here: The best name for the function is “totalAmount”, but that’s the name of the variable, and I can’t have both at the same time. So I give the new function a random name when I extract it (and compile­-test-commit).

我得坦白，我并非总是如此小步——但在事情变复杂时，我的第一反应就是采用更小的步子。怎样算变复杂呢，就是当重构过程有测试失败而我又无法马上看清问题所在并立即修复时，我就会回滚到最后一次可工作的提交，然后以更小的步子重做。这得益于我如此频繁地提交。特别是与复杂代码打交道时，细小的步子是快速前进的关键。接着我要重复同样的步骤来移除 totalAmount。我以拆解循环开始（编译、测试、提交），然后下移累加变量的声明语句（编译、测试、提交），最后再提炼函数。这里令我有点头疼的是：最好的函数名应该是 totalAmount，但它已经被变量名占用，我无法起两个同样的名字。因此，我在提炼函数时先给它随便取了一个名字（然后编译、测试、提交）。

Then I inline the variable (compile­test­commit) and rename the function to something more sensible (compile­test­commit).

I also take the opportunity to change the names inside my extracted functions to adhere to my convention.

```js
function totalAmount() {
  let result = 0
  for (const perf of invoices.performances) {
    result += amountFor(perf)
  }
  return result
}

export function statement() {
  let result = `Statement for ${invoices.customer}\n`
  for (const perf of invoices.performances) {
    // print line for this order
    result += `${playFor(perf).name}: ${usd(amountFor(perf))}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(totalAmount())}\n`
  result += `You earned ${totalVolumeCredits()} credits\n`
  console.log(result)
  return usd(totalAmount())
}
```

### 1.5 Status: Lots of Nested Functions

Now is a good time to pause and take a look at the overall state of the code:

```js
import { invoices, plays } from '@/code/data'

function amountFor(aPerformance) {
  let result = 0

  switch (playFor(aPerformance).type) {
    case 'tragedy':
      result = 40000
      if (aPerformance.audience > 30) {
        result += 1000 * (aPerformance.audience - 30)
      }
      break
    case 'comedy':
      result = 30000
      if (aPerformance.audience > 20) {
        result += 10000 + 500 * (aPerformance.audience - 20)
      }
      result += 300 * aPerformance.audience
      break
    default:
      throw new Error(`unkown type: ${playFor(aPerformance).type}`)
  }
  return result
}

function playFor(aPerformance) {
  return plays[aPerformance.playID]
}

function volumeCreditsFor(aPerformance) {
  let result = 0
  // add volume credits
  result += Math.max(aPerformance.audience - 30, 0)
  // add extra credit for every ten comedy attendees
  if (playFor(aPerformance).type === 'comedy') {
    result += Math.floor(aPerformance.audience / 5)
  }
  return result
}

function usd(aNumber) {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2
  }).format(aNumber / 100)
}

function totalVolumeCredits() {
  let volumeCredits = 0
  for (const perf of invoices.performances) {
    // add volume credits
    volumeCredits += volumeCreditsFor(perf)
  }
  return volumeCredits
}

function totalAmount() {
  let result = 0
  for (const perf of invoices.performances) {
    result += amountFor(perf)
  }
  return result
}

export function statement() {
  let result = `Statement for ${invoices.customer}\n`
  for (const perf of invoices.performances) {
    // print line for this order
    result += `${playFor(perf).name}: ${usd(amountFor(perf))}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(totalAmount())}\n`
  result += `You earned ${totalVolumeCredits()} credits\n`
  console.log(result)
  return usd(totalAmount())
}
```

The structure of the code is much better now. The top­level statement function is now just seven lines of code, and all it does is laying out the printing of the statement. All the calculation logic has been moved out to a handful of supporting functions. This makes it easier to understand each individual calculation as well as the overall flow of the report.

顶层的 statement 函数现在只剩 7 行代码，而且它处理的都是与打印详单相关的逻辑。与计算相关的逻辑从主函数中被移走，改由一组函数来支持。 每个单独的计算过程和详单的整体结构，都因此变得更易理解了。

### 1.6 Spliting the Phases of Calculation and Formatting

So far, my refactoring has focused on adding enough structure to the function so that I can understand it and see it in terms of its logical parts. This is often the case early in refactoring. Breaking down complicated chunks into small pieces is important, as is naming things well. Now, I can begin to focus more on the functionality change I want to make—specifically, providing an HTML version of this statement. In many ways, it’s now much easier to do. With all the calculation code split out, all I have to do is write an HTML version of the seven lines of code at the top. The problem is that these brokenout functions are nested within the textual statement method, and I don’t want to copy and paste them into a new function, however well organized. I want the same calculation functions to be used by the text and HTML versions of the statement.

到目前为止，我的重构主要是为原函数添加足够的结构，以便我能更好地理解它，看清它的逻辑结构。这也是重构早期的一般步骤。把复杂的代码块分解为更小的单元，与好的命名一样都很重要。现在，我可以更多关注我要修改的功能部分了，也就是为这张详单提供一个 HTML 版本。不管怎么说，现在改起来更加简单了。因为计算代码已经被分离出来，我只需要为顶部的 7 行代码实现一个 HTML 的版本。问题是，这些分解出来的函数嵌套在打印文本详单的函数中。无论嵌套函数组织得多么良好，我总不想将它们全复制粘贴到另一个新函数中。我希望同样的计算函数可以被文本版详单和 HTML 版详单共用。

There are various ways to do this, but one of my favorite techniques is Split Phase (154). My aim here is to divide the logic into two parts: one that calculates the data required for the statement, the other that renders it into text or HTML. The first phase creates an intermediate data structure that it passes to the second.

I start a Split Phase (154) by applying Extract Function (106) to the code that makes up the second phase. In this case, that’s the statement printing code, which is in fact the entire content of statement. This, together with all the nested functions, goes into its own top­level function which I call renderPlainText.

要实现复用有许多种方法，而我最喜欢的技术是拆分阶段（154）。这里我的目标是将逻辑分成两部分：一部分计算详单所需的数据，另一部分将数据渲染成文本或 HTML。第一阶段会创建一个中转数据结构，再把它传递给第二阶段。要开始拆分阶段（154），我会先对组成第二阶段的代码应用提炼函数（106）。在这个例子中，这部分代码就是打印详单的代码，其实也就是 statement 函数的全部内容。我要把它们与所有嵌套的函数一起抽取到一个新的顶层函数中，并将其命名为 renderPlainText。

1『 statement() 相当于一个空函数，把 renderPlainText() 里的东西一点点剥离出来放进 statement()。回复：果然应了那句话，软件行业基本所有的问题都可以通过抽象出一个中间层来解决，哈哈，这里的 `renderPlainText()` 是具体实现，`statement()` 是它的接口。』

```js
import { invoices, plays } from '@/code/data'

function renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`
  for (const perf of data.performances) {
    // print line for this order
    result += `${playFor(perf).name}: ${usd(amountFor(perf))}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(totalAmount())}\n`
  result += `You earned ${totalVolumeCredits()} credits\n`
  console.log(result)
  return usd(totalAmount())

  function amountFor(aPerformance) {
    let result = 0

    switch (playFor(aPerformance).type) {
      case 'tragedy':
        result = 40000
        if (aPerformance.audience > 30) {
          result += 1000 * (aPerformance.audience - 30)
        }
        break
      case 'comedy':
        result = 30000
        if (aPerformance.audience > 20) {
          result += 10000 + 500 * (aPerformance.audience - 20)
        }
        result += 300 * aPerformance.audience
        break
      default:
        throw new Error(`unkown type: ${playFor(aPerformance).type}`)
    }
    return result
  }

  function playFor(aPerformance) {
    return plays[aPerformance.playID]
  }

  function volumeCreditsFor(aPerformance) {
    let result = 0
    // add volume credits
    result += Math.max(aPerformance.audience - 30, 0)
    // add extra credit for every ten comedy attendees
    if (playFor(aPerformance).type === 'comedy') {
      result += Math.floor(aPerformance.audience / 5)
    }
    return result
  }

  function usd(aNumber) {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumIntegerDigits: 2
    }).format(aNumber / 100)
  }

  function totalVolumeCredits() {
    let volumeCredits = 0
    for (const perf of invoices.performances) {
      // add volume credits
      volumeCredits += volumeCreditsFor(perf)
    }
    return volumeCredits
  }

  function totalAmount() {
    let result = 0
    for (const perf of invoices.performances) {
      result += amountFor(perf)
    }
    return result
  }
}

export function statement() {
  const statementData = {}
  statementData.customer = invoices.customer
  statementData.performances = invoices.performances
  return renderPlainText(statementData)
}
```

1『这里注意，之前的那么多函数都要放进 `renderPlainText()` 里去。』

I do my usual compile-­test-­commit, then create an object that will act as my intermediate data structure between the two phases. I pass this data object in as an argument to renderPlainText (compile­test­commit).

```js
function renderPlainText(data) {
  let result = `Statement for ${invoices.customer}\n`
  for (const perf of invoices.performances) {
    // print line for this order
    result += `${playFor(perf).name}: ${usd(amountFor(perf))}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(totalAmount())}\n`
  result += `You earned ${totalVolumeCredits()} credits\n`
  console.log(result)
  return usd(totalAmount())
}

export function statement() {
  const statementData = {}
  return renderPlainText(statementData)
}
```

I now examine the other arguments used by renderPlainText. I want to move the data that comes from them into the intermediate data structure, so that all the calculation code moves into the statement function and renderPlainText operates solely on data passed to it through the data parameter. My first move is to take the customer and add it to the intermediate object (compile-test­-commit).

```js
function renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`
  for (const perf of invoices.performances) {
    // print line for this order
    result += `${playFor(perf).name}: ${usd(amountFor(perf))}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(totalAmount())}\n`
  result += `You earned ${totalVolumeCredits()} credits\n`
  console.log(result)
  return usd(totalAmount())
}

export function statement() {
  const statementData = {}
  statementData.customer = invoices.customer
  return renderPlainText(statementData)
}
```

Similarly, I add the performances, which allows me to delete the invoice parameter to renderPlainText (compile-­test­-commit). 

```js
export function statement() {
  const statementData = {}
  statementData.customer = invoices.customer
  statementData.performances = invoices.performances
  return renderPlainText(statementData)
}

function renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`
  for (const perf of data.performances) {
    // print line for this order
    result += `${playFor(perf).name}: ${usd(amountFor(perf))}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(totalAmount())}\n`
  result += `You earned ${totalVolumeCredits()} credits\n`
  console.log(result)
  return usd(totalAmount())
  
  ......
}
```

function renderPlainText…

```js
  function totalVolumeCredits() {
    let volumeCredits = 0
    for (const perf of data.performances) {
      // add volume credits
      volumeCredits += volumeCreditsFor(perf)
    }
    return volumeCredits
  }

  function totalAmount() {
    let result = 0
    for (const perf of data.performances) {
      result += amountFor(perf)
    }
    return result
  }
```

1『调用函数 `totalAmount()` 的时候不用传参数 `data`，是因为闭包的原因么？待确认。（2020-06-12）回复：应该是闭包的原因。（2020-09-25）』

Now I’d like the play name to come from the intermediate data. To do this, I need to enrich the performance record with data from the play (compile-­test-­commit).

现在，我希望「剧目名称」信息也从中转数据中获得。为此，需要使用 play 中的数据填充 aPerformance 对象（记得编译、测试、提交）。

```js
export function statement() {
  const statementData = {}
  statementData.customer = invoices.customer
  statementData.performances = invoices.performances.map(enrichPerformance)
  return renderPlainText(statementData)

  function enrichPerformance(aPerformance) {
    const result = Object.assign({}, aPerformance)
    return result
  }
}
```

1『 map() 函数的使用，还能像语句 invoices.performances.map(this.enrichPerformance) 这样用，传入回调函数时，直接省略了数组中各元素的标识「item」，涨见识了。书籍「忍者秘籍」里的介绍：内置的 map 方法创建了一个全新的数组，然后遍历输入的数组。对输入数组的每个元素，在新建的数组上，都会基于回调函数的执行结果创建一个对应的元素。其典型用法是 const weapons = ninjas.map(item => item.weapon) 』

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

The idiom result = Object.assign({}, aPerformance) looks very odd to people unfamiliar to JavaScript. It performs a shallow copy. I’d prefer to have a function for this, but it’s one of those cases where the idiom is so baked into JavaScript usage that writing my own function would look out of place for JavaScript programmers.

Now I have a spot for the play, I need to add it. To do that, I need to apply Move Function (198) to playFor and statement (compile­-test­-commit).

现在我只是简单地返回了一个 aPerformance 对象的副本，但马上我就会往这条记录中添加新的数据。返回副本的原因是，我不想修改传给函数的参数，我总是尽量保持数据不可变（immutable）——可变的状态会很快变成烫手的山芋。在不熟悉 JavaScript 的人看来，`result = Object.assign({}, aPerformance)` 的写法可能十分奇怪。它返回的是一个浅副本。虽然我更希望有个函数来完成此功能，但这个用法已经约定俗成，如果我自己写个函数，在 JavaScript 程序员看来反而会格格不入。

1『为何使用 assign() 函数复制一个对象可以实现数据的「不可变」，目前没吃透。（2020-06-12）回复：通过「浅复制」来保证数据的不可变，老马用了「函数式」编程范式的思想，哈哈。以后 JS 里实现浅复制的功能就用 `assign()`（2020-09-25）』

现在我们已经有了安放 play 字段的地方，可以把数据放进去。我需要对 playFor 和 statement 函数应用搬移函数（198）（然后编译、测试、提交）。

function statement…

```js
export function statement() {
  const statementData = {}
  statementData.customer = invoices.customer
  statementData.performances = invoices.performances.map(enrichPerformance)
  return renderPlainText(statementData)

  function enrichPerformance(aPerformance) {
    const result = Object.assign({}, aPerformance)
    result.play = playFor(result)
    return result
  }

  function playFor(aPerformance) {
    return plays[aPerformance.playID]
  }
}
```

I then replace all the references to playFor in renderPlainText to use the data instead (compile-­test-­commit).

```js
function renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`
  for (const perf of data.performances) {
    // print line for this order
    result += `${perf.play.name}: ${usd(amountFor(perf))}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(totalAmount())}\n`
  result += `You earned ${totalVolumeCredits()} credits\n`
  console.log(result)
  return usd(totalAmount())

  function amountFor(aPerformance) {
    let result = 0

    switch (aPerformance.play.type) {
      case 'tragedy':
        result = 40000
        if (aPerformance.audience > 30) {
          result += 1000 * (aPerformance.audience - 30)
        }
        break
      case 'comedy':
        result = 30000
        if (aPerformance.audience > 20) {
          result += 10000 + 500 * (aPerformance.audience - 20)
        }
        result += 300 * aPerformance.audience
        break
      default:
        throw new Error(`unkown type: ${aPerformance.play.type}`)
    }
    return result
  }

  function volumeCreditsFor(aPerformance) {
    let result = 0
    // add volume credits
    result += Math.max(aPerformance.audience - 30, 0)
    // add extra credit for every ten comedy attendees
    if (aPerformance.play.type === 'comedy') {
      result += Math.floor(aPerformance.audience / 5)
    }
    return result
  }

  function usd(aNumber) {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumIntegerDigits: 2
    }).format(aNumber / 100)
  }

  function totalVolumeCredits() {
    let volumeCredits = 0
    for (const perf of data.performances) {
      // add volume credits
      volumeCredits += volumeCreditsFor(perf)
    }
    return volumeCredits
  }

  function totalAmount() {
    let result = 0
    for (const perf of data.performances) {
      result += amountFor(perf)
    }
    return result
  }
}
```

I then move amountFor in a similar way (compile-­test-­commit).

function statement…

```js
export function statement() {
  const statementData = {}
  statementData.customer = invoices.customer
  statementData.performances = invoices.performances.map(enrichPerformance)
  return renderPlainText(statementData)

  function enrichPerformance(aPerformance) {
    const result = Object.assign({}, aPerformance)
    result.play = playFor(result)
    result.amount = amountFor(result)
    return result
  }

  function playFor(aPerformance) {
    return plays[aPerformance.playID]
  }

  function amountFor(aPerformance) {
    let result = 0

    switch (aPerformance.play.type) {
      case 'tragedy':
        result = 40000
        if (aPerformance.audience > 30) {
          result += 1000 * (aPerformance.audience - 30)
        }
        break
      case 'comedy':
        result = 30000
        if (aPerformance.audience > 20) {
          result += 10000 + 500 * (aPerformance.audience - 20)
        }
        result += 300 * aPerformance.audience
        break
      default:
        throw new Error(`unkown type: ${aPerformance.play.type}`)
    }
    return result
  }
}
```

function renderPlainText…

```js
function renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`
  for (const perf of data.performances) {
    // print line for this order
    result += `${perf.play.name}: ${usd(perf.amount)}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(totalAmount())}\n`
  result += `You earned ${totalVolumeCredits()} credits\n`
  console.log(result)
  return usd(totalAmount())
  
  ......

  function totalAmount() {
    let result = 0
    for (const perf of data.performances) {
      result += perf.amount
    }
    return result
  }
}
```

Next, I move the volume credits calculation (compile-­test-­commit).

function statement…

```js
  function enrichPerformance(aPerformance) {
    const result = Object.assign({}, aPerformance)
    result.play = playFor(result)
    result.amount = amountFor(result)
    result.volumeCredits = volumeCreditsFor(result)
    return result
  }
```

function renderPlainText…

```js
function renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`
  for (const perf of data.performances) {
    // print line for this order
    result += `${perf.play.name}: ${usd(perf.amount)}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(totalAmount())}\n`
  result += `You earned ${totalVolumeCredits()} credits\n`
  console.log(result)
  return usd(totalAmount())

  function usd(aNumber) {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumIntegerDigits: 2
    }).format(aNumber / 100)
  }

  function totalVolumeCredits() {
    let volumeCredits = 0
    for (const perf of data.performances) {
      // add volume credits
      volumeCredits += perf.volumeCredits
    }
    return volumeCredits
  }

  function totalAmount() {
    let result = 0
    for (const perf of data.performances) {
      result += perf.amount
    }
    return result
  }
}
```

Finally, I move the two calculations of the totals.

function statement…

```js
export function statement() {
  const statementData = {}
  statementData.customer = invoices.customer
  statementData.performances = invoices.performances.map(enrichPerformance)
  statementData.totalAmount = totalAmount(statementData)
  statementData.totalVolumeCredits = totalVolumeCredits(statementData)
  return renderPlainText(statementData)

  function enrichPerformance(aPerformance) {
    const result = Object.assign({}, aPerformance)
    result.play = playFor(result)
    result.amount = amountFor(result)
    result.volumeCredits = volumeCreditsFor(result)
    return result
  }
  ......
  ......
}
```

function renderPlainText… 

```js
function renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`
  for (const perf of data.performances) {
    // print line for this order
    result += `${perf.play.name}: ${usd(perf.amount)}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(data.totalAmount)}\n`
  result += `You earned ${data.totalVolumeCredits} credits\n`
  console.log(result)
  return usd(data.totalAmount)

  function usd(aNumber) {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumIntegerDigits: 2
    }).format(aNumber / 100)
  }
}
```

Although I could have modified the bodies of these totals functions to use the statementData variable (as it’s within scope), I prefer to pass the explicit parameter. And, once I’m done with compile-­test-­commit after the move, I can’t resist a couple quick shots of Replace Loop with Pipeline (231).

1『管道取代循环，这个 NB 方法一定要学会。』

function renderPlainText… 

```js
  function totalAmount(data) {
    return data.performances
      .reduce((total, p) => total + p.amount, 0)
  }

  function totalVolumeCredits(data) {
    return data.performances
      .reduce((total, p) => total + p.volumeCredits, 0)
  }
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

### 01. 语法

```js
arr.reduce(callback(accumulator, currentValue[, index[, array]])[, initialValue])
```

reducer 函数接收 4 个参数：`Accumulator (acc)`（累计器）、`Current Value (cur)`（当前值）、`Current Index (idx)`（当前索引）、`Source Array (src)`（源数组）。您的 reducer 函数的返回值分配给累计器，该返回值在数组的每个迭代中被记住，并最后成为最终的单个结果值。

返回值：函数累计处理的结果。

### 02. 描述

reduce 为数组中的每一个元素依次执行callback函数，不包括数组中被删除或从未被赋值的元素。

回调函数第一次执行时，accumulator 和 currentValue 的取值有两种情况：如果调用 `reduce()` 时提供了 initialValue，accumulator 取值为 initialValue，currentValue 取数组中的第一个值；如果没有提供 initialValue，那么 accumulator 取数组中的第一个值，currentValue 取数组中的第二个值。注意：如果没有提供 initialValue，reduce 会从索引 1 的地方开始执行 callback 方法，跳过第一个索引。如果提供 initialValue，从索引 0 开始。

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

后面有很多例子，值得仔细研读。一个意外收获（数组去重）：如果你正在使用一个可以兼容 Set 和 Array.from() 的环境， 你可以使用 `let orderedArray = Array.from(new Set(myArray));` 来获得一个相同元素被移除的数组。这是收集到的数组去重第二个方法，第一个是用 Set() 后再用 `...` 运算符转会为数组。

』

I now extract all the first­phase code into its own function (compile-­test-­commit).

```js
function createStatementData() {
  const statementData = {}
  statementData.customer = invoices.customer
  statementData.performances = invoices.performances.map(enrichPerformance)
  statementData.totalAmount = totalAmount(statementData)
  statementData.totalVolumeCredits = totalVolumeCredits(statementData)
  return statementData

  function enrichPerformance(aPerformance) {
    const result = Object.assign({}, aPerformance)
    result.play = playFor(result)
    result.amount = amountFor(result)
    result.volumeCredits = volumeCreditsFor(result)
    return result
  }

  function playFor(aPerformance) {
    return plays[aPerformance.playID]
  }

  function amountFor(aPerformance) {
    let result = 0

    switch (aPerformance.play.type) {
      case 'tragedy':
        result = 40000
        if (aPerformance.audience > 30) {
          result += 1000 * (aPerformance.audience - 30)
        }
        break
      case 'comedy':
        result = 30000
        if (aPerformance.audience > 20) {
          result += 10000 + 500 * (aPerformance.audience - 20)
        }
        result += 300 * aPerformance.audience
        break
      default:
        throw new Error(`unkown type: ${aPerformance.play.type}`)
    }
    return result
  }

  function volumeCreditsFor(aPerformance) {
    let result = 0
    // add volume credits
    result += Math.max(aPerformance.audience - 30, 0)
    // add extra credit for every ten comedy attendees
    if (aPerformance.play.type === 'comedy') {
      result += Math.floor(aPerformance.audience / 5)
    }
    return result
  }

  function totalAmount(data) {
    return data.performances
      .reduce((total, p) => total + p.amount, 0)
  }

  function totalVolumeCredits(data) {
    return data.performances
      .reduce((total, p) => total + p.volumeCredits, 0)
  }
}

export function statement() {
  return renderPlainText(createStatementData())
}
```

Since it’s clearly separate now, I move it to its own file (and alter the name of the returned result to match my usual convention).

createStatementData.js…

```js
import { invoices, plays } from '@/code/data'

export function createStatementData() {
  const statementData = {}
  statementData.customer = invoices.customer
  statementData.performances = invoices.performances.map(enrichPerformance)
  statementData.totalAmount = totalAmount(statementData)
  statementData.totalVolumeCredits = totalVolumeCredits(statementData)
  return statementData

  function enrichPerformance(aPerformance) {
    const result = Object.assign({}, aPerformance)
    result.play = playFor(result)
    result.amount = amountFor(result)
    result.volumeCredits = volumeCreditsFor(result)
    return result
  }

  function playFor(aPerformance) {
    return plays[aPerformance.playID]
  }

  function amountFor(aPerformance) {
    let result = 0

    switch (aPerformance.play.type) {
      case 'tragedy':
        result = 40000
        if (aPerformance.audience > 30) {
          result += 1000 * (aPerformance.audience - 30)
        }
        break
      case 'comedy':
        result = 30000
        if (aPerformance.audience > 20) {
          result += 10000 + 500 * (aPerformance.audience - 20)
        }
        result += 300 * aPerformance.audience
        break
      default:
        throw new Error(`unkown type: ${aPerformance.play.type}`)
    }
    return result
  }

  function volumeCreditsFor(aPerformance) {
    let result = 0
    // add volume credits
    result += Math.max(aPerformance.audience - 30, 0)
    // add extra credit for every ten comedy attendees
    if (aPerformance.play.type === 'comedy') {
      result += Math.floor(aPerformance.audience / 5)
    }
    return result
  }

  function totalAmount(data) {
    return data.performances
      .reduce((total, p) => total + p.amount, 0)
  }

  function totalVolumeCredits(data) {
    return data.performances
      .reduce((total, p) => total + p.volumeCredits, 0)
  }
}
```

statement.js…

```js
import { createStatementData } from '@/code/createStatementData'

function renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`
  for (const perf of data.performances) {
    // print line for this order
    result += `${perf.play.name}: ${usd(perf.amount)}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(data.totalAmount)}\n`
  result += `You earned ${data.totalVolumeCredits} credits\n`
  console.log(result)
  return usd(data.totalAmount)

  function usd(aNumber) {
    return new Intl.NumberFormat('en-US', {
      style: 'currency',
      currency: 'USD',
      minimumIntegerDigits: 2
    }).format(aNumber / 100)
  }
}

export function statement() {
  return renderPlainText(createStatementData())
}
```

One final swing of compile­-test-­commit—and now it’s easy to write an HTML version.

statement.js…

```js
// 此时此刻算是理解了输出样式与数据层的分离（2020-09-27）

import { createStatementData } from '@/code/createStatementData'

function usd(aNumber) {
  return new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD',
    minimumIntegerDigits: 2
  }).format(aNumber / 100)
}

function renderPlainText(data) {
  let result = `Statement for ${data.customer}\n`
  for (const perf of data.performances) {
    // print line for this order
    result += `${perf.play.name}: ${usd(perf.amount)}(${perf.audience} seats)\n`
  }

  result += `Amount owed is ${usd(data.totalAmount)}\n`
  result += `You earned ${data.totalVolumeCredits} credits\n`
  console.log(result)
  return usd(data.totalAmount)
}

function renderHtml(data) {
  let result = `<h1>Statement for ${data.customer}</h1>\n`
  result += '<table>\n'
  result += '<tr><th>play</th><th>seats</th><th>cost</th></tr>'
  for (const perf of data.performances) {
    result += ` <tr><td>${perf.play.name}</td><td>${perf.audience}</td>`
    result += `<td>${usd(perf.amount)}</td></tr>\n`
  }
  result += '</table>\n'
  result += `<p>Amount owed is <em>${usd(data.totalAmount)}</em></p>\n`
  result += `<p>You earned <em>${data.totalVolumeCredits}</em> credits</p>`
  console.log(result)
  return result
}

export function statement() {
  return renderPlainText(createStatementData())
}

export function htmlStatement() {
  return renderHtml(createStatementData())
}
```

(I moved usd to the top level, so that renderHtml could use it.)

### 1.7 Status: Separated into Two Files(and Phases)

This is a good moment to take stock again and think about where the code is now. I have two files of code.

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

1『又一个经典重构手法出来了，replace conditional with polymorphism，条件语句转多态。』

我的设想是先建立一个继承体系，它有「喜剧」和「悲剧」两个子类，子类各自包含独立的计算逻辑。调用者通过调用一个多态的 amount 函数，让语言帮你分发到不同的子类的计算过程中。volumeCredits 函数的处理也是如法炮制。为此我需要用到多种重构方法，其中最核心的一招是以多态取代条件表达式（272），将多个同样的类型码分支用多态取代。但在施展以多态取代条件表达式（272）之前，我得先创建一个基本的继承结构。我需要先创建一个类，并将价格计算函数和观众量积分计算函数放进去。

I begin by reviewing the calculation code. (One of the pleasant consequences of the previous refactoring is that I can now ignore the formatting code, so long as I produce the same output data structure. I can further support this by adding tests that probe the intermediate data structure.)

我先从检查计算代码开始。（之前的重构带来的一大好处是，现在我大可以忽略那些格式化代码，只要不改变中转数据结构就行。我可以进一步添加测试来保证中转数据结构不会被意外修改。）

#### 1.8.1 Creating a Performance Calculator

The enrichPerformance function is the key, since it populates the intermediate data structure with the data for each performance. Currently, it calls the conditional functions for amount and volume credits. What I need it to do is call those functions on a host class. Since that class hosts functions for calculating data about performances, I’ll call it a performance calculator.

enrichPerformance 函数是关键所在，因为正是它用每场演出的数据来填充中转数据结构。目前它直接调用了计算价格和观众量积分的函数，我需要创建一个类，通过这个类来调用这些函数。由于这个类存放了与每场演出相关数据的计算函数，于是我把它称为演出计算器（performance calculator）。

function createStatementData…

```js
  function enrichPerformance(aPerformance) {
    const calculator = new PerformanceCalculator(aPerformance)
    const result = Object.assign({}, aPerformance)
    result.play = playFor(result)
    result.amount = amountFor(result)
    result.volumeCredits = volumeCreditsFor(result)
    return result
  }
```

top level…

```js
class PerformanceCalculator {
  constructor(aPerformance) {
    this.performances = aPerformance
  }
}
```

So far, this new object isn’t doing anything. I want to move behavior into it—and I’d like to start with the simplest thing to move, which is the play record. Strictly, I don’t need to do this, as it’s not varying polymorphically, but this way I’ll keep all the data transforms in one place, and that consistency will make the code clearer. To make this work, I will use Change Function Declaration (124) to pass the performance’s play into the calculator.

我希望将函数行为搬移进来，这可以从最容易搬移的东西——play 字段开始。严格来讲，我不需要搬移这个字段，因为它并未体现出多态性，但这样可以把所有数据转换集中到一处地方，保证了代码的一致性和清晰度。为此，我将使用改变函数声明（124）手法将 performance 的 play 字段传给计算器。

function createStatementData…

```js
  function enrichPerformance(aPerformance) {
    const calculator = new PerformanceCalculator(aPerformance, playFor(aPerformance))
    const result = Object.assign({}, aPerformance)
    result.play = calculator.play
    result.amount = amountFor(result)
    result.volumeCredits = volumeCreditsFor(result)
    return result
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

搬移完成后可以编译一下，看看是否有编译错误。我在本地开发环境运行代码时，编译会自动发生，我实际需要做的只是运行一下 Babel。编译能帮我发现新函数中潜在的语法错误，语法之外的就帮不上什么忙了。尽管如此，这一步还是很有用。使新函数适应新家后，我会将原来的函数改造成一个委托函数，让它直接调用新函数。

function createStatementData…

```js
  function amountFor(aPerformance) {
    return new PerformanceCalculator(aPerformance, playFor(aPerformance)).amount
  }
```

1『这里 `new PerformanceCaluculator(aPerformance, playFor(aPerformance)).amount;` 调用的是实例化对象的 get 属性值，所以 amount 后面没有括号 ()，这个知识点是在专栏「重学前端」里获得的。（2020-09-27）』

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

1『这时，之前的 function amountFor(aPerformance) {} 函数可以整体删除了，绝妙！』

I repeat the same process to move the volume credits calculation.

function createStatementData…

```js
  function enrichPerformance(aPerformance) {
    const calculator = new PerformanceCalculator(aPerformance, playFor(aPerformance))
    const result = Object.assign({}, aPerformance)
    result.play = calculator.play
    result.amount = calculator.amount
    result.volumeCredits = calculator.volumeCredits
    return result
  }
```

class PerformanceCalculator…

```js
  get volumeCredits() {
    let result = 0
    // add volume credits
    result += Math.max(this.performance.audience - 30, 0)
    // add extra credit for every ten comedy attendees
    if (this.play.type === 'comedy') {
      result += Math.floor(this.performance.audience / 5)
    }
    return result
  }
```

#### 1.8.3 Making the Performance Calculator Polymorphic 

Now that I have the logic in a class, it’s time to apply the polymorphism. The first step is to use Replace Type Code with Subclasses (362) to introduce subclasses instead of the type code. For this, I need to create subclasses of the performance calculator and use the appropriate subclass in createPerformanceData. In order to get the right subclass, I need to replace the constructor call with a function, since JavaScript constructors can’t return subclasses. So I use Replace Constructor with Factory Function (334).

1『用子类代码替换类型代码，这句话有点感触了。这里由于 JS 语言的特性，没法在构造函数里直接返回子类，所以老马用工厂函数取代构造函数，这个知识点也很赞。（2020-09-26）』

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
  return new PerformanceCalculator(aPerformance, aPlay)
}
```

With that now a function, I can create subclasses of the performance calculator and get the creation function to select which one to return.

top level…

```js
class TragedyCalculator extends PerformanceCalculator {
  //
}

class ComedyCalculator extends PerformanceCalculator {
  //
}

function createPerformanceCalculator(aPerformance, aPlay) {
  switch(aPlay.type) {
    case 'tragedy': return new TragedyCalculator(aPerformance, aPlay)
    case 'comedy': return new ComedyCalculator(aPerformance, aPlay)
    default:
      throw new Error(`unkonw type: ${aPlay.type}`)
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

虽然我也可以直接删掉处理悲剧的分支，将错误留给默认分支去抛出，但我更喜欢显式地抛出异常——何况这行代码只能再活个几分钟了（这也是我直接抛出一个字符串而不用更好的错误对象的原因）。再次进行编译、测试、提交。之后，将处理喜剧类型的分支也下移到子类中去。

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

1『父类里还是保留 `get amout() {}`，并且抛出个异常表示应该是子类的职责，老马的这个做法好棒啊，哈哈。（2020-09-27）』

The next conditional to replace is the volume credits calculation. Looking at the discussion of future categories of plays, I notice that most plays expect to check if audience is above 30, with only some categories introducing a variation. So it makes sense to leave the more common case on the superclass as a default, and let the variations override it as necessary. So I just push down the case for comedies:

下一个要替换的条件表达式是观众量积分的计算。我回顾了一下前面关于未来戏剧类型的讨论，发现大多数剧类在计算积分时都会检查观众数是否达到 30，仅一小部分品类有所不同。因此，将更为通用的逻辑放到超类作为默认条件， 出现特殊场景时按需覆盖它，听起来十分合理。于是我将一部分喜剧的逻辑下移到子类。

class PerformanceCalculator…

```js
class PerformanceCalculator {
  constructor(aPerformance, aPlay) {
    this.performance = aPerformance
    this.play = aPlay
  }

  get amount() {
    throw new Error('subclass responsibility')
  }

  get volumeCredits() {
    // add volume credits
    return Math.max(this.performance.audience - 30, 0)
  }
}
```

class ComedyCalculator…

```js
class ComedyCalculator extends PerformanceCalculator {
  get amount() {
    let result = 30000
    if (this.performance.audience > 20) {
      result += 10000 + 500 * (this.performance.audience - 20)
    }
    result += 300 * this.performance.audience
    return result
  }

  get volumeCredits() {
    return super.volumeCredits + Math.floor(this.performance.audience / 5)
  }
}
```

### 1.9 Status: Creating the Data with the Polymorphic Calculator

Time to reflect on what introducing the polymorphic calculator did to the code.

createStatementData.js

```js
import { invoices, plays } from '@/code/data'

class PerformanceCalculator {
  constructor(aPerformance, aPlay) {
    this.performance = aPerformance
    this.play = aPlay
  }

  get amount() {
    throw new Error('subclass responsibility')
  }

  get volumeCredits() {
    // add volume credits
    return Math.max(this.performance.audience - 30, 0)
  }
}

class TragedyCalculator extends PerformanceCalculator {
  get amount() {
    let result = 40000
    if (this.performance.audience > 30) {
      result += 1000 * (this.performance.audience - 30)
    }
    return result
  }
}

class ComedyCalculator extends PerformanceCalculator {
  get amount() {
    let result = 30000
    if (this.performance.audience > 20) {
      result += 10000 + 500 * (this.performance.audience - 20)
    }
    result += 300 * this.performance.audience
    return result
  }

  get volumeCredits() {
    return super.volumeCredits + Math.floor(this.performance.audience / 5)
  }
}

function createPerformanceCalculator(aPerformance, aPlay) {
  switch (aPlay.type) {
    case 'tragedy': return new TragedyCalculator(aPerformance, aPlay)
    case 'comedy': return new ComedyCalculator(aPerformance, aPlay)
    default:
      throw new Error(`unkonw type: ${aPlay.type}`)
  }
}

export function createStatementData() {
  const statementData = {}
  statementData.customer = invoices.customer
  statementData.performances = invoices.performances.map(enrichPerformance)
  statementData.totalAmount = totalAmount(statementData)
  statementData.totalVolumeCredits = totalVolumeCredits(statementData)
  return statementData

  function enrichPerformance(aPerformance) {
    const calculator = createPerformanceCalculator(aPerformance, playFor(aPerformance))
    const result = Object.assign({}, aPerformance)
    result.play = calculator.play
    result.amount = calculator.amount
    result.volumeCredits = calculator.volumeCredits
    return result
  }

  function playFor(aPerformance) {
    return plays[aPerformance.playID]
  }

  function totalAmount(data) {
    return data.performances
      .reduce((total, p) => total + p.amount, 0)
  }

  function totalVolumeCredits(data) {
    return data.performances
      .reduce((total, p) => total + p.volumeCredits, 0)
  }
}
```

Again, the code has increased in size as I’ve introduced structure. The benefit here is that the calculations for each kind of play are grouped together. If most of the changes will be to this code, it will be helpful to have it clearly separated like this. Adding a new kind of play requires writing a new subclass and adding it to the creation function. The example gives some insight as to when using subclasses like this is useful. Here, I’ve moved the conditional lookup from two functions (amountFor and volumeCreditsFor) to a single constructor function createPerformanceCalculator. The more functions there are that depend on the same type of polymorphism, the more useful this approach becomes.

代码量仍然有所增加，因为我再次整理了代码结构。新结构带来的好处是，不同戏剧种类的计算各自集中到了一处地方。如果大多数修改都涉及特定类型的计算，像这样按类型进行分离就很有意义。当添加新剧种时，只需要添加一个子类，并在创建函数中返回它。这个示例还揭示了一些关于此类继承方案何时适用的洞见。上面我将条件分支的查找从两个不同的函数（amountFor 和 volumeCreditsFor）搬移到一个集中的构造函数 createPerformanceCalculator 中。有越多的函数依赖于同一套类型进行多态，这种继承方案就越有益处。

An alternative to what I’ve done here would be to have createPerformanceData return the calculator itself, instead of the calculator populating the intermediate data structure. One of the nice features of JavaScript’s class system is that with it, using getters looks like regular data access. My choice on whether to return the instance or calculate separate output data depends on who is using the downstream data structure. In this case, I preferred to show how to use the intermediate data structure to hide the decision to use a polymorphic calculator.

除了这样设计，还有另一种可能的方案，那就是让 createStatementData 返回计算器实例本身，而非自己拿到计算器来填充中转数据结构。JavaScript 的类设计有不少好特性，例如，取值函数用起来就像普通的数据存取。我在考量是「直接返回实例本身」还是「返回计算好的中转数据」时，主要看数据的使用者是谁。在这个例子中，我更想通过中转数据结构来展示如何以此隐藏计算器背后的多态设计。

这是一个简单的例子，但我希望它能让你对「重构怎么做」有一点感觉。例中我已经示范了数种重构手法，包括提炼函数（106）、内联变量（123）、搬移函数（198）和以多态取代条件表达式（272）等。本章的重构有 3 个较为重要的节点，分别是：将原函数分解成一组嵌套的函数、应用拆分阶段（154）分离计算逻辑与输出格式化逻辑，以及为计算器引入多态性来处理计算逻辑。每一步都给代码添加了更多的结构，以便我能更好地表达代码的意图。

一般来说，重构早期的主要动力是尝试理解代码如何工作。通常你需要先通读代码，找到一些感觉，然后再通过重构将这些感觉从脑海里搬回到代码中。清晰的代码更容易理解，使你能够发现更深层次的设计问题，从而形成积极正向的反馈环。当然，这个示例仍有值得改进的地方，但现在测试仍能全部通过，代码相比初见时已经有了巨大的改善，所以我已经可以满足了。

我谈论的是如何改善代码，但什么样的代码才算好代码，程序员们有很多争论。我偏爱小的、命名良好的函数，也知道有些人反对这个观点。如果我们说这只关乎美学，只是各花入各眼，没有好坏高低之分，那除了诉诸个人品味，就没有任何客观事实依据了。但我坚信，这不仅关乎个人品味，而且是有客观标准的。我认为，好代码的检验标准就是人们是否能轻而易举地修改它。好代码应该直截了当：有人需要修改代码时，他们应能轻易找到修改点，应该能快速做出更改，而不易引入其他错误。一个健康的代码库能够最大限度地提升我们的生产力，支持我们更快、更低成本地为用户添加新特性。为了保持代码库的健康，就需要时刻留意现状与理想之间的差距，然后通过重构不断接近这个理想。

好代码的检验标准就是人们是否能轻而易举地修改它。这个示例告诉我们最重要的一点就是重构的节奏感。无论何时，当我向人们展示我如何重构时，无人不讶异于我的步子之小，并且每一步都保证代码处于编译通过和测试通过的可工作状态。20年前，当Kent Beck在底特律的一家宾馆里向我展示同样的手法时，我也报以同样的震撼。开展高效有序的重构，关键的心得是：小的步子可以更快前进，请保持代码永远处于可工作状态，小步修改累积起来也能大大改善系统的设计。这几点请君牢记，其余的我已无需多言。
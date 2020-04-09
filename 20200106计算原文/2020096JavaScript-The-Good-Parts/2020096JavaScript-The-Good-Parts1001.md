# 10 Beautiful Features

Thus, expecting thy reply, I profane my lips on thy foot, my eyes on thy picture, and my heart on thy every part. Thine, in the dearest design of industry...

—William Shakespeare, Love’s Labor’s Lost

I was invited last year to contribute a chapter to Andy Oram’s and Greg Wilson’s Beautiful Code (O’Reilly), an anthology on the theme of beauty as expressed in computer programs. I wanted to write my chapter in JavaScript. I wanted to use it to present something abstract, powerful, and useful to show that the language was up to it. And I wanted to avoid the browser and other venues in which JavaScript is typecast. I wanted to show something respectable with some heft to it.

I immediately thought of Vaughn Pratt’s Top Down Operator Precedence parser, which I use in JSLint (see Appendix C). Parsing is an important topic in computing. The ability to write a compiler for a language in itself is still a test for the complete-ness of a language.

I wanted to include all of the code for a parser in JavaScript that parses JavaScript. But my chapter was just one of 30 or 40, so I felt constrained in the number of pages I could consume. A further complication was that most of my readers would have no experience with JavaScript, so I also would have to introduce the language and its peculiarities.

2『已下载书籍「2020119代码之美 | 2020119Beautiful-Code」；作者的文章「Top Down Operator Precedence parser」。』

So, I decided to subset the language. That way, I wouldn’t have to parse the whole language, and I wouldn’t have to describe the whole language. I called the subset Simplified JavaScript. Selecting the subset was easy: it included just the features that I needed to write a parser. This is how I described it in Beautiful Code: 

1. Simplified JavaScript is just the good stuff, including: Functions as first class objects. Functions in Simplified JavaScript are lambdas with lexical scoping.

2. Dynamic objects with prototypal inheritance Objects are class-free. We can add a new member to any object by ordinary assignment. An object can inherit members from another object.

3. Object literals and array literals. This is a very convenient notation for creating new objects and arrays. JavaScript literals were the inspiration for the JSON data interchange format.

JS 的 3 大精华：1）函数是顶级对象。在精简 Javascrip 中，函数是有词法作用域的闭包（(lambda）。2）基于原型继承的动态对象。对象是无类别的。我们可以通过普通的赋值给任何对象增加一个新成员属性。一个对象可以从另一个对象继承成员属性。3）对象字面量和数组字面量。这对创建新的对象和数组来说是一种非常方便的表示法。Javascript 字面量是数据交换格式 JSON 的灵感之源。

The subset contained the best of the Good Parts. Even though it was a small language, it was very expressive and powerful. JavaScript has lots of additional features that really don’t add very much, and as you’ll find in the appendixes that follow, it has a lot of features with negative value. There was nothing ugly or bad in the subset. All of that fell away.

Simplified JavaScript isn’t strictly a subset. I added a few new features. The simplest was adding pi as a simple constant. I did that to demonstrate a feature of the parser. I also demonstrated a better reserved word policy and showed that reserved words are unnecessary. In a function, a word cannot be used as both a variable or parameter name and a language feature. You can use a word for one or the other, and the programmer gets to choose. That makes a language easier to learn because you don’t need to be aware of features you don’t use. And it makes the language easier to extend because it isn’t necessary to reserve more words to add new features.

精简的 Javascript 不是一个严格的子集。我添加了少许新特性。最简单的是增加了 pi 作为个简单的常量。我这么做是为了证明解析器的一个特性。我也展示了一个更好的保留字策路并证明哪些保留字是多余的。在一个函数中，一个单词不能既被用做变量或参数名，又被用做一个语言特性。你可以让某个单词用在其中之一上，井允许程序员自己选择。这会使一门语言易于学习，因为你没必要知道你不会使用的特性。并且它会使这门语言易于扩展，因为它无须保留更多的保留字来增加新特性。

I also added block scope. Block scope is not a necessary feature, but not having it confuses experienced programmers. I included block scope because I anticipated that my parser would be used to parse languages that are not JavaScript, and those languages would do scoping correctly. The code I wrote for the parser is written in a style that doesn’t care if block scope is available or not. I recommend that youwrite that way, too. When I started thinking about this book, I wanted to take the subset idea further, to show how to take an existing programming language and make significant improvements to it by making no changes except to exclude the low-value features.

我也增加了块级作用域。块级作用域不是一个必需的特性，但没有它会让有经验的程序员感到困惑。包含块级作用城是因为我预期解析器可能会被用于解析非 Javascript 语言，并且那些语言能正确地界定作用域。我编写这个解析器的代码风格不关心块作用域是否可用我推荐你也采用这种方式来写。当开始构思本书的时候，我想进一步地发展这个子集，我想展示除了排除低价值特性外，如何通过不做任何改变来获得一个现有的编程语言，并且使它得到有效的改进。

We see a lot of feature-driven product design in which the cost of features is not properly accounted. Features can have a negative value to consumers because they make the products more difficult to understand and use. We are finding that people like products that just work. It turns out that designs that just work are much harder to produce than designs that assemble long lists of features.

我们看到大量的特性驱动的产品设计，其中特性的成本没有被正确计算。对于用户来说，某些特性可能有一些负面价值，因为它们使产品更加难以理解和使用。我们发现人们想要的产品其实只要能工作即可。事实证明产生恰好可以工作的设计比集合一大串特性的设计要困难得多。

Features have a specification cost, a design cost, and a development cost. There is a testing cost and a reliability cost. The more features there are, the more likely one will develop problems or will interact badly with another. In software systems, there is a storage cost, which was becoming negligible, but in mobile applications is becoming significant again. There are ascending performance costs because Moore’s Law doesn’t apply to batteries.

Features have a documentation cost. Every feature adds pages to the manual, increasing training costs. Features that offer value to a minority of users impose a cost on all users. So, in designing products and programming languages, we want to get the core features—the good parts—right because that is where we create most of the value.

特性有规定成本、设计成本和开发成本，还有测试成本和可靠性成本。特性越多，某个特性出现问题，或者和其他特性相互干扰的可能性就越大。在软件系统中，存储成本是无足轻重的，但在移动应用中，它又变得重要了。它们抬高了电池的效能成本，因为摩尔定律并不适用于电池。特性有文档成本。每个特性都会让产品指南变得更厚，从而增加了培训成本。只对少数用户有价值的特性增加了所有用户的成本。所以在设计产品和编程语言时，我们希望直接使用核心的精华部分，因为是这些精华创造了大部分的价值。

We all find the good parts in the products that we use. We value simplicity, and when simplicity isn’t offered to us, we make it ourselves. My microwave oven has tons of features, but the only ones I use are cook and the clock. And setting the clock is a struggle. We cope with the complexity of feature-driven design by finding and sticking with the good parts.

It would be nice if products and programming languages were designed to have only good parts.

在我们使用的产品中，总能找到好的部分。我们喜欢简单，追求简洁易用，但是当产品缺乏这种特性时，就要自己去创造它。微波炉有一大堆特性，但是我只会用烹调和定时，使用定时功能就足够麻烦的了。对于特性驱动型的设计，我们唯有靠找出它的精华并坚持使用，才能更好地应对其复杂性。如果产品和编程语言被设计得仅留下精华，那该有多好。

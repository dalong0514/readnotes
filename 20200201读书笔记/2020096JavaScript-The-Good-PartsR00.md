## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

#### 01. 常识

#### 02. 反常识

#### 03. 知识来源

比如提出者，如何演化成型的；书或专栏具体出现的地方。

#### 04. 例子

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

例子。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。

#### 01. 基本信息

用一句话描述你对这个大牛的印象。

#### 02. 贡献及著作

### 0401. 金句卡——Most programming languages contain good parts and bad parts.

Most programming languages contain good parts and bad parts. I discovered that I could be a better programmer by using only the good parts and avoiding the bad parts

### 0501. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## 模板

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

英文版出版时间是 2008 年。

## 书评

### 01

它概括了 JavaScript 这个脚本语言的核心内容，不仅总结了语言的精华部分，还指出了「鸡肋」和「糟粕」。如果说犀牛书展现了 JavaScript 特性的丰富和功能的强大，这本书就体现了 JavaScript 语言轻巧简洁的特点。其实 JavaScript 就是这么简洁，但是它很灵活，使用得好，可以编写出功能强大的程序。语言中核心的内容，也就是犀牛书的第一部分，全部在这本书中被总结出来了。但这并不表示可以从这本书入门，它不是入门级的，不适合初学者。作为概括总结，它是一本很好的帮助你提高 JavaScript 水平的书籍，因为总结也是学习的过程。

这本书的特点是，薄但内容丰富。它用精炼的文字、形象的语法图（railroad diagram）和简短的代码片断总结了 JavaScript 的核心内容。对于对 JavaScript 已经有较深理解的人来说，它可以帮助你整理总结并加深对 JavaScript 的理解，对于了解程度低一点的人来说，它可以帮助你学习 JavaScript 的编程思想。不过就像作者的前言所说的，必须反复阅读。这也正是我决定购买这本书的原因。书的最后那个 json_parse 的例子给我的印象很深。这是本书唯一一个完整的实例代码，它包含了 JavaScript 中很多重要的知识点和代码设计风格（比如闭包），很值得研究学习。

### 02

就如其「最被低估的编程语言」称号所述，Javascript 实际上是一门非常优秀的语言，看似熟悉的语法之下隐含的是完全不同的世界观。尤其是在学、用 erlang 这种函数语言几年后，更能体会其很多设计元素的精巧之处。转贴几条 twitter 上记录的读书笔记备查：

1、Javascript 语言中支持四类函数调用方式：1）全局函数。2）对象方法。3）构造函数。4）apply/call 调用。区别在于函数内 this 指针的绑定，分别是：1）Global 对象。2）调用对象。3）构造返回对象。4）调用时传入的第一个参数。2、作为 Prototype-base 和 Functional 编程混杂体的 Javascript，居然不提供尾递归 (tail-end recursion) 真是个杯具啊。所有有人想出了这种用 setTimeout 模拟的山寨办法。3、没有变量块作用域 (Block Scope) 的支持，是 Javascript 语义上与 C/C++ 系统又一重大区别。但回过头来看 Python/Scheme 也不提供块作用域的支持，究竟是当年的设计错误还是我们的思维定势问题？

4、A Better Javascript Memoizer 利用闭包 (Closure) 和匿名方法 (anonymous function)，实现针对任意参数个数的 memoizer 模式，对复杂函数的计算结果进行缓存，那是相当的优雅。5、说起来 Javascript 中自动添加语句结束分号 (semicolon insertion) 也算是一个功能，可以很大程度上提高对网页上语法不规范脚本的兼容性。杯具的是各家的容忍限度不同方法不同，所以基本被列入不应被使用的糟粕。6、Javascript 里面的 NaN 本身就是个杯具，NaN != NaN 但 typeof NaN === 'number'，必须通过 isNaN 或 isFinite 才能筛选出，但这个可怜的函数又会自动对参数进行隐式类型转换。7、假以时日，HTTPS 和 Javascript 有可能成为 Web 领域，类似今天 TCP/IP 和 C/C++ 的基础构架的地位。不知十年后再回头看今日的理解，又是一番如何的景象，期待。

### 03

第一本书：JavaScript 高级程序设计。第二本书：ppk 谈 JavaScript。这是第三本。久闻大名的书，读完之后并没有预想的那种感觉。也许是因为书中的很多观点处处通用，即使你没有写过 js, 也会从其他语言的普遍做法中见识到。The Definitive Guide 今年又出了新版，非常有可读性，两相对比之下不免让人感觉没那么棒。但这绝对是一本很奇特的书，两个地方：1）印象中其他语言没有对应的著作，例如 "Java: The Good Parts". C 有一本 pitfalls, 但和这本不太一样。js 好的地方列了一遍，不好的地方也列了一遍。2）Appendix 比正文精彩。全书的精华都在 Appendix 了。最后我想说的是，这不是 js 语法书，看中这书薄而放弃 the definitive guide 的同学们，你们亏大了。

### 05

本书的作者 Douglas Crockford 是 JavaScript 开发社区最知名的权威，JavaScript 的发明人 Brendan Eich 说他是「Yoda of lambda programming and JavaScript（lambda 编程和 JavaScript 的精神领袖）」。他不仅仅给我们带来了 JSON、JSLint、JSMin 和 ADSafe 等等，在 JavaScript 开发领域应用广泛且影响深远的作品，更重要的是给我们带来了受益终身的利用 JavaScript 进行高效开发的思想和风格，这就是本书的重要意义。

JavaScript 曾是「世界上最被误解的语言」，因为它担负太多的特性，包括糟糕的交互和失败的设计，但随着 Ajax 的到来，JavaScript「从最受误解的编程语言演变为最流行的语言」，这除了幸运之外，至少还说明它是一个不错的语言。Douglas Crockford 在这本书中剥除 JavaScript 糟糕的外衣，抽离出一个具有更好可靠性、可读性和可维护性的 JavaScript 子集，让你看到一门优雅的、轻量级的和非常富有表现力的语言。作者从语法、对象、函数、继承、数组、正则表达式、方法、样式和优美的特性这 9 个方面来呈现这门语言真正的精华，这是语言最本质最优雅的部分，通过它们完全可以构建出高效的代码。作者还通过附录列出了这门语言的糟粕和鸡肋部分，且告诉你如何避免它们。最后还介绍了 JSLint，通过它的检验，能有效的保障我们写出优美高效的代码。

这是一本介绍 JavaScript 语言本质的权威书籍，值得任何正在或者想从事 JavaScript 开发的人阅读，并且非常需要反复阅读。学习、理解、实践大师的思想，我们才可能站在巨人的肩上，才有机会超越大师，这本书就是开始。

### 06

是因为：在语言设计上，其借鉴了多种语言，函数式和命令式语言都有，原型链式语言，多年后，在我了解了 lisp 后，才发现，原来 js 一些设计思路，如此的倾向 lisp。js 的创造者应该是语言的专家，通晓编程语言的设计，但当年可能时间比较仓促，留下了不少坑。这一切导致，想真正了解 js 需要一定的门槛，主流的面向对象类的语言经验在此又变得不太有用。在有了几年的编码经验，了解了一些编程语言后，再看 js 变得清晰了许多。

## Preface

JavaScript is a surprisingly powerful language. Its unconventionality presents some challenges, but being a small language, it is easily mastered. My goal here is to help you to learn to think in JavaScript. I will show you the components of the language and start you on the process of discovering the ways those components can be put together. This is not a reference book. It is not exhaustive about the language and its quirks. It doesn’t contain everything you’ll ever need to know. That stuff you can easily find online. Instead, this book just contains the things that are really important.

This is not a book for beginners. Someday I hope to write a JavaScript: The First Parts book, but this is not that book. This is not a book about Ajax or web programming. The focus is exclusively on JavaScript, which is just one of the languages the web developer must master. This is not a book for dummies. This book is small, but it is dense. There is a lot of material packed into it. Don’t be discouraged if it takes multiple readings to get it. Your efforts will be rewarded.

## 01. Good Parts

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

When I was a young journeyman programmer, I would learn about every feature of the languages I was using, and I would attempt to use all of those features when I wrote. I suppose it was a way of showing off, and I suppose it worked because I was the guy you went to if you wanted to know how to use a particular feature. Eventually I figured out that some of those features were more trouble than they were worth. Some of them were poorly specified, and so were more likely to cause portability problems. Some resulted in code that was difficult to read or modify. Some induced me to write in a manner that was too tricky and error-prone. And some of those features were design errors. Sometimes language designers make mistakes.

Most programming languages contain good parts and bad parts. I discovered that I could be a better programmer by using only the good parts and avoiding the bad parts. After all, how can you build something good out of bad parts? It is rarely possible for standards committees to remove imperfections from a language because doing so would cause the breakage of all of the bad programs that depend on those bad parts. They are usually powerless to do anything except heap more features on top of the existing pile of imperfections. And the new features do not always interact harmoniously, thus producing more bad parts. But you have the power to define your own subset. You can write better programs by relying exclusively on the good parts.

2『Most programming languages contain good parts and bad parts. I discovered that I could be a better programmer by using only the good parts and avoiding the bad parts. 做一张金句卡片。每种语言都有好的部分和坏的部分，制定标准的组织因为各种原因不可能把坏的部分剔除掉，只能不断的加新的特性。但作为个体，我们有权利和义务只使用语言里好的部分。』

JavaScript is a language with more than its share of bad parts. It went from nonexistence to global adoption in an alarmingly short period of time. It never had an interval in the lab when it could be tried out and polished. It went straight into Netscape Navigator 2 just as it was, and it was very rough. When Java™ applets failed, JavaScript became the「Language of the Web」by default. JavaScript’s popularity is almost completely independent of its qualities as a programming language.

Fortunately, JavaScript has some extraordinarily good parts. In JavaScript, there is a beautiful, elegant, highly expressive language that is buried under a steaming pile of good intentions and blunders. The best nature of JavaScript is so effectively hidden that for many years the prevailing opinion of JavaScript was that it was an unsightly, incompetent toy. My intention here is to expose the goodness in JavaScript, an out-standing, dynamic programming language. JavaScript is a block of marble, and I chip away the features that are not beautiful until the language’s true nature reveals itself. I believe that the elegant subset I carved out is vastly superior to the language as a whole, being more reliable, readable, and maintainable.

1『JS 的精华在于 out-standing, dynamic programming language. 』

This book will not attempt to fully describe the language. Instead, it will focus on the good parts with occasional warnings to avoid the bad. The subset that will be described here can be used to construct reliable, readable programs small and large. By focusing on just the good parts, we can reduce learning time, increase robustness, and save some trees.

Perhaps the greatest benefit of studying the good parts is that you can avoid the need to unlearn the bad parts. Unlearning bad patterns is very difficult. It is a painful task that most of us face with extreme reluctance. Sometimes languages are subsetted to make them work better for students. But in this case, I am subsetting JavaScript to make it work better for professionals.

### 01. Why JavaScript?

JavaScript is an important language because it is the language of the web browser. Its association with the browser makes it one of the most popular programming languages in the world. At the same time, it is one of the most despised programming languages in the world. The API of the browser, the Document Object Model (DOM) is quite awful, and JavaScript is unfairly blamed. The DOM would be painful to work with in any language. The DOM is poorly specified and inconsistently implemented. This book touches only very lightly on the DOM. I think writing a Good Parts book about the DOM would be extremely challenging.

1『DOM 太挫，拿得出手的东西很少。』

JavaScript is most despised because it isn’t some other language. If you are good in some other language and you have to program in an environment that only supports JavaScript, then you are forced to use JavaScript, and that is annoying. Most people in that situation don’t even bother to learn JavaScript first, and then they are surprised when JavaScript turns out to have significant differences from the some other language they would rather be using, and that those differences matter.

The amazing thing about JavaScript is that it is possible to get work done with it without knowing much about the language, or even knowing much about programming. It is a language with enormous expressive power. It is even better when you know what you’re doing. Programming is difficult business. It should never be undertaken in ignorance.

1『enormous expressive power. 是 JS 的一大特点。』

### 02. Analyzing JavaScript

JavaScript is built on some very good ideas and a few very bad ones. The very good ideas include functions, loose typing, dynamic objects, and an expressive object literal notation. The bad ideas include a programming model based on global variables.

1『ES6 引入的 let、const 就是为了解决「a programming model based on global variables.」』

JavaScript’s functions are first class objects with (mostly) lexical scoping. JavaScript is the first lambda language to go mainstream. Deep down, JavaScript has more in common with Lisp and Scheme than with Java. It is Lisp in C’s clothing. This makes JavaScript a remarkably powerful language.

The fashion in most programming languages today demands strong typing. The theory is that strong typing allows a compiler to detect a large class of errors at compile time. The sooner we can detect and repair errors, the less they cost us. JavaScript is a loosely typed language, so JavaScript compilers are unable to detect type errors. This can be alarming to people who are coming to JavaScript from strongly typed languages. But it turns out that strong typing does not eliminate the need for careful testing. And I have found in my work that the sorts of errors that strong type checking finds are not the errors I worry about. On the other hand, I find loose typing to be liberating. I don’t need to form complex class hierarchies. And I never have to cast or wrestle with the type system to get the behavior that I want.

1『JS 是弱类型语言。作者认为强类型语言（比如 Java）在类型强制上能提供的真正有用的价值有限，还不如弱类型呢。』

JavaScript has a very powerful object literal notation. Objects can be created simply by listing their components. This notation was the inspiration for JSON, the popular data interchange format. (There will be more about JSON in Appendix E.)

1『 a very powerful object literal notation. 是 JS 的又一大特点。』

A controversial feature in JavaScript is prototypal inheritance. JavaScript has a class-free object system in which objects inherit properties directly from other objects. This is really powerful, but it is unfamiliar to classically trained programmers. If you attempt to apply classical design patterns directly to JavaScript, you will be frustrated. But if you learn to work with JavaScript’s prototypal nature, your efforts will be rewarded.

1『JavaScript has a class-free object system in which objects inherit properties directly from other objects. 对象直接从其他对象那边继承属性，「照猫画虎」，基于原型的面向对象，这是 JS 强大之处。但这点会让使用一些程序员困惑，因为他们习惯了基于类的面向对象风格。』

JavaScript is much maligned for its choice of key ideas. For the most part, though, those choices were good, if unusual. But there was one choice that was particularly bad: JavaScript depends on global variables for linkage. All of the top-level variables of all compilation units are tossed together in a common namespace called the global object. This is a bad thing because global variables are evil, and in JavaScript they are fundamental. Fortunately, as we will see, JavaScript also gives us the tools to mitigate this problem.

1『全局对象（global object）是 JS 最大的糟粕。』

In a few cases, we can’t ignore the bad parts. There are some unavoidable awful parts, which will be called out as they occur. They will also be summarized in Appendix A. But we will succeed in avoiding most of the bad parts in this book, summarizing much of what was left out in Appendix B. If you want to learn more about the bad parts and how to use them badly, consult any other JavaScript book.

The standard that defines JavaScript (aka JScript) is the third edition of The ECMAScript Programming Language, which is available from http://www.ecmainternational.org/publications/files/ecma-st/ECMA-262.pdf. The language described in this book is a proper subset of ECMAScript. This book does not describe the whole language because it leaves out the bad parts. The treatment here is not exhaustive. It avoids the edge cases. You should, too. There is danger and misery at the edges.

3『[Index of Ecma Standards](http://www.ecma-international.org/publications/standards/Stnindex.htm)，现在已经出 ECMA-400 了。（2020-03-24）』

Appendix C describes a programming tool called JSLint, a JavaScript parser that can analyze a JavaScript program and report on the bad parts that it contains. JSLint provides a degree of rigor that is generally lacking in JavaScript development. It can give you confidence that your programs contain only the good parts.

JavaScript is a language of many contrasts. It contains many errors and sharp edges, so you might wonder,「Why should I use JavaScript?」There are two answers. The first is that you don’t have a choice. The Web has become an important platform for application development, and JavaScript is the only language that is found in all browsers. It is unfortunate that Java failed in that environment; if it hadn’t, there could be a choice for people desiring a strongly typed classical language. But Java did fail and JavaScript is flourishing, so there is evidence that JavaScript did something right. The other answer is that, despite its deficiencies, JavaScript is really good. It is lightweight and expressive. And once you get the hang of it, functional programming is a lot of fun.

1『原来 JS 就是面向函数式的编程。』

But in order to use the language well, you must be well informed about its limitations. I will pound on those with some brutality. Don’t let that discourage you. The good parts are good enough to compensate for the bad parts.

### 03. A Simple Testing Ground

If you have a web browser and any text editor, you have everything you need to run JavaScript programs. First, make an HTML file with a name like program.html:

```
<html>
    <body>
    <pre>
        <script src="program.js">
        </script>
    </pre>
    </body>
</html>
```

Then, make a file in the same directory with a name like program.js: 

    document.writeln('Hello, world!');

1『以后写 JS 代码就按这种方式在本地服务器上跑，比在浏览器里的 console 里写代码方便太多。』

Next, open your HTML file in your browser to see the result. Throughout the book, a method method is used to define new methods. This is its definition: 

```
Function.prototype.method = function (name, func) {
    this.prototype[name] = func;
    return this;
};
```

It will be explained in Chapter 4.

## 02. Grammar

This chapter introduces the grammar of the good parts of JavaScript, presenting a quick overview of how the language is structured. We will represent the grammar with railroad diagrams. The rules for interpreting these diagrams are simple:

• You start on the left edge and follow the tracks to the right edge.

• As you go, you will encounter literals in ovals, and rules or descriptions in rectangles.『图里面圆形的是 literals，矩形的是 rules or descriptions. 』

• Any sequence that can be made by following the tracks is legal.

• Any sequence that cannot be made by following the tracks is not legal.

• Railroad diagrams with one bar at each end allow whitespace to be inserted between any pair of tokens. Railroad diagrams with two bars at each end do not.

The grammar of the good parts presented in this chapter is significantly simpler than the grammar of the whole language.

### 01. Whitespace

Whitespace can take the form of formatting characters or comments. Whitespace is usually insignificant, but it is occasionally necessary to use whitespace to separate sequences of characters that would otherwise be combined into a single token. For example, in:

    var that = this;

the space between var and that cannot be removed, but the other spaces can be removed.

JavaScript offers two forms of comments, block comments formed with /* */ and line-ending comments starting with //. Comments should be used liberally to improve the readability of your programs. Take care that the comments always accurately describe the code. Obsolete comments are worse than no comments.

The /* */ form of block comments came from a language called PL/I. PL/I chose those strange pairs as the symbols for comments because they were unlikely to occur in that language’s programs, except perhaps in string literals. In JavaScript, those pairs can also occur in regular expression literals, so block comments are not safe for commenting out blocks of code. For example:

```
/*
var rm_a = /a*/.match(s);
*/
```

causes a syntax error. So, it is recommended that /* */ comments be avoided and // comments be used instead. In this book, // will be used exclusively.

### 02. Names

A name is a letter optionally followed by one or more letters, digits, or underbars. A name cannot be one of these reserved words:

```
abstract 
boolean break byte 
case catch char class const continue 
debugger default delete do double
else enum export extends 
false final finally float for function 
goto 
if implements import in instanceof int interface
long 
native new null 
package private protected public 
return 
short static super switch synchronized 
this throw throws transient true try typeof 
var volatile void
while with
```

Most of the reserved words in this list are not used in the language. The list does not include some words that should have been reserved but were not, such as undefined, NaN, and Infinity. It is not permitted to name a variable or parameter with a reserved word. Worse, it is not permitted to use a reserved word as the name of an object property in an object literal or following a dot in a refinement. Names are used for statements, variables, parameters, property names, operators, and labels.

### 03. Numbers

JavaScript has a single number type. Internally, it is represented as 64-bit floating point, the same as Java’s double. Unlike most other programming languages, there is no separate integer type, so 1 and 1.0 are the same value. This is a significant convenience because problems of overflow in short integers are completely avoided, and all you need to know about a number is that it is a number. A large class of numeric type errors is avoided.

If a number literal has an exponent part, then the value of the literal is computed by multiplying the part before the e by 10 raised to the power of the part after the e. So 100 and 1e2 are the same number. Negative numbers can be formed by using the – prefix operator. The value NaN is a number value that is the result of an operation that cannot produce a normal result. NaN is not equal to any value, including itself. You can detect NaN with the isNaN (number) function. The value Infinity represents all values greater than 1.79769313486231570e+308. Numbers have methods (see Chapter 8). JavaScript has a Math object that contains a set of methods that act on numbers. For example, the Math.floor (number) method can be used to convert a number into an integer.

### 04. Strings

A string literal can be wrapped in single quotes or double quotes. It can contain zero or more characters. The \ (backslash) is the escape character. JavaScript was built at a time when Unicode was a 16-bit character set, so all characters in JavaScript are 16 bits wide. JavaScript does not have a character type. To represent a character, make a string with just one character in it.

The escape sequences allow for inserting characters into strings that are not normally permitted, such as backslashes, quotes, and control characters. The \u convention allows for specifying character code points numerically.

    "A" === "\u0041"

Strings have a length property. For example, "seven".length is 5. Strings are immutable. Once it is made, a string can never be changed. But it is easy to make a new string by concatenating other strings together with the + operator. Two strings containing exactly the same characters in the same order are considered to be the same string. So:

    'c' + 'a' + 't' === 'cat'

is true. Strings have methods (see Chapter 8):

    'cat'.toUpperCase( ) === 'CAT'

### 05. Statements

A compilation unit contains a set of executable statements. In web browsers, each \<script> tag delivers a compilation unit that is compiled and immediately executed. Lacking a linker, JavaScript throws them all together in a common global namespace. There is more on global variables in Appendix A.

When used inside of a function, the var statement defines the function’s private variables. The switch, while, for, and do statements are allowed to have an optional label prefix that interacts with the break statement.

Statements tend to be executed in order from top to bottom. The sequence of execution can be altered by the conditional statements (if and switch), by the looping statements (while, for, and do), by the disruptive statements (break, return, and throw), and by function invocation.

A block is a set of statements wrapped in curly braces. Unlike many other languages, blocks in JavaScript do not create a new scope, so variables should be defined at the top of the function, not in blocks.

The if statement changes the flow of the program based on the value of the expression. The then block is executed if the expression is truthy; otherwise, the optional else branch is taken.

Here are the falsy values:

• false

• null

• undefined

• The empty string ''

• The number 0

• The number NaN

All other values are truthy, including true, the string 'false', and all objects.

The switch statement performs a multiway branch. It compares the expression for equality with all of the specified cases. The expression can produce a number or a string. When an exact match is found, the statements of the matching case clause are executed. If there is no match, the optional default statements are executed.

A case clause contains one or more case expressions. The case expressions need not be constants. The statement following a clause should be a disruptive statement to prevent fall through into the next case. The break statement can be used to exit from a switch.

The while statement performs a simple loop. If the expression is falsy, then the loop will break. While the expression is truthy, the block will be executed.

The for statement is a more complicated looping statement. It comes in two forms.

The conventional form is controlled by three optional clauses: the initialization, the condition, and the increment. First, the initialization is done, which typically initializes the loop variable. Then, the condition is evaluated. Typically, this tests the loop variable against a completion criterion. If the condition is omitted, then a condition of true is assumed. If the condition is falsy, the loop breaks. Otherwise, the block is executed, then the increment executes, and then the loop repeats with the condition.

The other form (called for in) enumerates the property names (or keys) of an object. On each iteration, another property name string from the object is assigned to the variable.

It is usually necessary to test object.hasOwnProperty(variable) to determine whether the property name is truly a member of the object or was found instead on the prototype chain.

```
for (myvar in obj) {
    if (obj.hasOwnProperty(myvar)) {
    ...
    }
}
```

The do statement is like the while statement except that the expression is tested after the block is executed instead of before. That means that the block will always be executed at least once.

The try statement executes a block and catches any exceptions that were thrown by the block. The catch clause defines a new variable that will receive the exception object.

The throw statement raises an exception. If the throw statement is in a try block, then control goes to the catch clause. Otherwise, the function invocation is abandoned, and control goes to the catch clause of the try in the calling function. The expression is usually an object literal containing a name property and a message property. The catcher of the exception can use that information to determine what to do.

The return statement causes the early return from a function. It can also specify the value to be returned. If a return expression is not specified, then the return value will be undefined. JavaScript does not allow a line end between the return and the expression.

The break statement causes the exit from a loop statement or a switch statement. It can optionally have a label that will cause an exit from the labeled statement. JavaScript does not allow a line end between the break and the label.

An expression statement can either assign values to one or more variables or members, invoke a method, delete a property from an object. The = operator is used for assignment. Do not confuse it with the === equality operator. The += operator can add or concatenate.








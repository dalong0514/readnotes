## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

#### 01. 常识

#### 02. 反常识

#### 03. 知识来源

比如提出者，如何演化成型的；书或专栏具体出现的地方。

#### 04. 例子

### 0201. 术语卡——delegation

The prototype link is used only in retrieval. If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on until the process finally bottoms out with Object.prototype. If the desired property exists nowhere in the prototype chain, then the result is the undefined value. This is called delegation.

### 0202. 术语卡——this 值

 this 的值取决于调用模式（invocation pattern）。

Invoking a function suspends the execution of the current function, passing control and parameters to the new function. In addition to the declared parameters, every function receives two additional parameters: this and arguments. The this parameter is very important in object oriented programming, and its value is determined by the invocation pattern. There are four patterns of invocation in JavaScript: the method invocation pattern, the function invocation pattern, the constructor invocation pattern, and the apply invocation pattern. The patterns differ in how the bonus parameter this is initialized.

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

1『函数内 this 指针的绑定，对象的绑定，对理解变量、引用醍醐灌顶。』

4、A Better Javascript Memoizer 利用闭包 (Closure) 和匿名方法 (anonymous function)，实现针对任意参数个数的 memoizer 模式，对复杂函数的计算结果进行缓存，那是相当的优雅。5、说起来 Javascript 中自动添加语句结束分号 (semicolon insertion) 也算是一个功能，可以很大程度上提高对网页上语法不规范脚本的兼容性。杯具的是各家的容忍限度不同方法不同，所以基本被列入不应被使用的糟粕。6、Javascript 里面的 NaN 本身就是个杯具，NaN != NaN 但 typeof NaN === 'number'，必须通过 isNaN 或 isFinite 才能筛选出，但这个可怜的函数又会自动对参数进行隐式类型转换。7、假以时日，HTTPS 和 Javascript 有可能成为 Web 领域，类似今天 TCP/IP 和 C/C++ 的基础构架的地位。不知十年后再回头看今日的理解，又是一番如何的景象，期待。

### 03

第一本书：JavaScript 高级程序设计。第二本书：ppk 谈 JavaScript。这是第三本。久闻大名的书，读完之后并没有预想的那种感觉。也许是因为书中的很多观点处处通用，即使你没有写过 js, 也会从其他语言的普遍做法中见识到。The Definitive Guide 今年又出了新版，非常有可读性，两相对比之下不免让人感觉没那么棒。但这绝对是一本很奇特的书，两个地方：1）印象中其他语言没有对应的著作，例如 "Java: The Good Parts". C 有一本 pitfalls, 但和这本不太一样。js 好的地方列了一遍，不好的地方也列了一遍。2）Appendix 比正文精彩。全书的精华都在 Appendix 了。最后我想说的是，这不是 js 语法书，看中这书薄而放弃 the definitive guide 的同学们，你们亏大了。

### 05

本书的作者 Douglas Crockford 是 JavaScript 开发社区最知名的权威，JavaScript 的发明人 Brendan Eich 说他是「Yoda of lambda programming and JavaScript（lambda 编程和 JavaScript 的精神领袖）」。他不仅仅给我们带来了 JSON、JSLint、JSMin 和 ADSafe 等等，在 JavaScript 开发领域应用广泛且影响深远的作品，更重要的是给我们带来了受益终身的利用 JavaScript 进行高效开发的思想和风格，这就是本书的重要意义。

JavaScript 曾是「世界上最被误解的语言」，因为它担负太多的特性，包括糟糕的交互和失败的设计，但随着 Ajax 的到来，JavaScript「从最受误解的编程语言演变为最流行的语言」，这除了幸运之外，至少还说明它是一个不错的语言。Douglas Crockford 在这本书中剥除 JavaScript 糟糕的外衣，抽离出一个具有更好可靠性、可读性和可维护性的 JavaScript 子集，让你看到一门优雅的、轻量级的和非常富有表现力的语言。作者从语法、对象、函数、继承、数组、正则表达式、方法、样式和优美的特性这 9 个方面来呈现这门语言真正的精华，这是语言最本质最优雅的部分，通过它们完全可以构建出高效的代码。作者还通过附录列出了这门语言的糟粕和鸡肋部分，且告诉你如何避免它们。最后还介绍了 JSLint，通过它的检验，能有效的保障我们写出优美高效的代码。

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

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

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

JavaScript offers two forms of comments. Obsolete comments are worse than no comments. The /* */ form of block comments came from a language called PL/I. PL/I chose those strange pairs as the symbols for comments because they were unlikely to occur in that language’s programs, except perhaps in string literals. In JavaScript, those pairs can also occur in regular expression literals, so block comments are not safe for commenting out blocks of code. For example:

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

1『链接器（Linker）是编语言或操作系统提供的工具，它的工作就是解析未定义的待号引用，将目标文件中的占位待替换为科号地址。』

When used inside of a function, the var statement defines the function’s private variables. The switch, while, for, and do statements are allowed to have an optional label prefix that interacts with the break statement.

1『原来在函数内部用 var 申明的变量时函数的私有变量；label prefix 是指这种形式「label: expressions statement;」』

Statements tend to be executed in order from top to bottom. The sequence of execution can be altered by the conditional statements (if and switch), by the looping statements (while, for, and do), by the disruptive statements (break, return, and throw), and by function invocation.

A block is a set of statements wrapped in curly braces. Unlike many other languages, blocks in JavaScript do not create a new scope, so variables should be defined at the top of the function, not in blocks.

The if statement changes the flow of the program based on the value of the expression. The then block is executed if the expression is truthy; otherwise, the optional else branch is taken. Here are the falsy values:

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

The other form (called for in) enumerates the property names (or keys) of an object. On each iteration, another property name string from the object is assigned to the variable. It is usually necessary to test object.hasOwnProperty(variable) to determine whether the property name is truly a member of the object or was found instead on the prototype chain.

『可以通过这个方法来检测这个属性名是该对象的成员，还是来自于原型链。』

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

### 06. Expressions

The simplest expressions are a literal value (such as a string or number), a variable, a built-in value (true, false, null, undefined, NaN, or Infinity), an invocation expression preceded by new, a refinement expression preceded by delete, an expression wrapped in parentheses, an expression preceded by a prefix operator, or an expression followed by:

• An infix operator and another expression.

• The ? ternary operator followed by another expression, then by :, and then by yet another expression.

• An invocation.

• A refinement.

The ? ternary operator takes three operands. If the first operand is truthy, it produces the value of the second operand. But if the first operand is falsy, it produces the value of the third operand.

The operators at the top of the operator precedence list in Table 2-1 have higher precedence. They bind the tightest. The operators at the bottom have the lowest precedence. Parentheses can be used to alter the normal precedence, so: 

```
2 + 3 * 5 === 17
(2 + 3) * 5 === 25
```

The values produced by typeof are 'number', 'string', 'boolean', 'undefined', 'function', and 'object'. If the operand is an array or null, then the result is 'object', which is wrong. There will be more about typeof in Chapter 6 and Appendix A.

If the operand of ! is truthy, it produces false. Otherwise, it produces true. The + operator adds or concatenates. If you want it to add, make sure both operands are numbers. The / operator can produce a noninteger result even if both operands are integers. The && operator produces the value of its first operand if the first operand is falsy. Otherwise, it produces the value of the second operand.

1『在编程语言中，结合性（associativity）是操作符在没有圆括号分组的情况下决定其优先的一种属性。它可能是从左向右结合（left-associative）、从右向左结合（right-associative）或无结合。比如加运算符的结合性是从左向右，而一元运算符、赋値运算将及三元条件运算特的结合性是从右向左。关于更多的运算符结合性的信息，请参阅《Javascript 权成指南》中译第 5 版。在 Javascript 语言里 % 不是通常数学意义上的模运算，而实际上是「求余」运算。两个运算数为正数时，求模运算和求余运算的值相同；两个运算数中存在负数时，求模运算和求余运算的值则不相同。』

The || operator produces the value of its first operand if the first operand is truthy. Otherwise, it produces the value of the second operand.

Invocation causes the execution of a function value. The invocation operator is a pair of parentheses that follow the function value. The parentheses can contain arguments that will be delivered to the function. There will be much more about functions in Chapter 4.

1『 Invocation 指函数调用。』

A refinement is used to specify a property or element of an object or array. This will be described in detail in the next chapter.

### 07. Literals

Object literals are a convenient notation for specifying new objects. The names of the properties can be specified as names or as strings. The names are treated as literal names, not as variable names, so the names of the properties of the object must be known at compile time. The values of the properties are expressions. There will be more about object literals in the next chapter.

『 Literals 即字面量。对象字面量是一种可以方便地按指定规格创建新对象的表示法。属性名可以是标识符或字符串。这些名字被当做字面量名而不是变量名来对待，所以对象的属性名在编译时才能知道。属性的值就是表达式。』

Array literals are a convenient notation for specifying new arrays. There will be more about array literals in Chapter 6. There will be more about regular expressions in Chapter 7.

### 08. Functions

A function literal defines a function value. It can have an optional name that it can use to call itself recursively. It can specify a list of parameters that will act as variables initialized by the invocation arguments. The body of the function includes variable definitions and statements. There will be more about functions in Chapter 4.

## 03. Objects

### 1. 逻辑脉络

用自己的话总结主题，梳理逻辑脉络，也就是这本书整个地图里这一章所在的节点。

### 2. 摘录及评论

The simple types of JavaScript are numbers, strings, booleans (true and false), null, and undefined. All other values are objects. Numbers, strings, and booleans are object-like in that they have methods, but they are immutable. Objects in JavaScript are mutable keyed collections. In JavaScript, arrays are objects, functions are objects, regular expressions are objects, and, of course, objects are objects.

An object is a container of properties, where a property has a name and a value. A property name can be any string, including the empty string. A property value can be any JavaScript value except for undefined.

Objects in JavaScript are class-free. There is no constraint on the names of new properties or on the values of properties. Objects are useful for collecting and organizing data. Objects can contain other objects, so they can easily represent tree or graph structures. JavaScript includes a prototype linkage feature that allows one object to inherit the properties of another. When used well, this can reduce object initialization time and memory consumption.

1『JS 中的对象是无类型的（class-free）。』

### 01. Object Literals

Object literals provide a very convenient notation for creating new object values. An object literal is a pair of curly braces surrounding zero or more name/value pairs. An object literal can appear anywhere an expression can appear: 

```
var empty_object = {};

var stooge = {
    "first-name": "Jerome",
    "last-name": "Howard"
};
```

A property’s name can be any string, including the empty string. The quotes around a property’s name in an object literal are optional if the name would be a legal JavaScript name and not a reserved word. So quotes are required around "first-name", but are optional around first_name. Commas are used to separate the pairs. A property’s value can be obtained from any expression, including another object literal. Objects can nest:

```
var flight = {
    airline: "Oceanic",
    number: 815,
    departure: {
        IATA: "SYD",
        time: "2004-09-22 14:55",
        city: "Sydney"
    },
    arrival: {
        IATA: "LAX",
        time: "2004-09-23 10:42",
        city: "Los Angeles"
    }
};
```

### 02. Retrieval

Values can be retrieved from an object by wrapping a string expression in a [ ] suffix. If the string expression is a constant, and if it is a legal JavaScript name and not a reserved word, then the . notation can be used instead. The . notation is preferred because it is more compact and it reads better:

```
stooge["first-name"] // "Joe"
flight.departure.IATA // "SYD"
```

The undefined value is produced if an attempt is made to retrieve a nonexistent member:

```
stooge["middle-name"] // undefined
flight.status // undefined
stooge["FIRST-NAME"] // undefined
```

The || operator can be used to fill in default values: 

```
var middle = stooge["middle-name"] || "(none)"; 
var status = flight.status || "unknown";
```

Attempting to retrieve values from undefined will throw a TypeError exception. This can be guarded against with the && operator:

```
flight.equipment // undefined flight.equipment.model // throw "TypeError"
flight.equipment && flight.equipment.model // undefined Retrieval
```

### 03. Update

A value in an object can be updated by assignment. If the property name already exists in the object, the property value is replaced:

    stooge['first-name'] = 'Jerome';

If the object does not already have that property name, the object is augmented: 

```
stooge['middle-name'] = 'Lester';
stooge.nickname = 'Curly';
flight.equipment = {
    model: 'Boeing 777'
};
flight.status = 'overdue';
```

### 04. Reference

Objects are passed around by reference. They are never copied: 

```
var x = stooge;
x.nickname = 'Curly';
var nick = stooge.nickname;
    // nick is 'Curly' because x and stooge are references to the same object

var a = {}, b = {}, c = {};
// a, b, and c each refer to a different empty object

a = b = c = {};
// a, b, and c all refer to the same empty object
```

### 05. Prototype

Every object is linked to a prototype object from which it can inherit properties. All objects created from object literals are linked to Object.prototype, an object that comes standard with JavaScript. When you make a new object, you can select the object that should be its prototype.

The mechanism that JavaScript provides to do this is messy and complex, but it can be significantly simplified. We will add a create method to the Object function. The create method creates a new object that uses an old object as its prototype. There will be much more about functions in the next chapter.

```
if (typeof Object.create !== 'function') {
    Object.create = function (o) {
    var F = function () {};
    F.prototype = o;
    return new F();
};
}

var another_stooge = Object.create(stooge);
```

The prototype link has no effect on updating. When we make changes to an object, the object’s prototype is not touched:

```
another_stooge['first-name'] = 'Harry';
another_stooge['middle-name'] = 'Moses';
another_stooge.nickname = 'Moe';
```

The prototype link is used only in retrieval. If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on until the process finally bottoms out with Object.prototype. If the desired property exists nowhere in the prototype chain, then the result is the undefined value. This is called delegation.

The prototype relationship is a dynamic relationship. If we add a new property to a prototype, that property will immediately be visible in all of the objects that are based on that prototype:

```
stooge.profession = 'actor';
another_stooge.profession // 'actor'
```

We will see more about the prototype chain in Chapter 6.

### 06. Reflection

It is easy to inspect an object to determine what properties it has by attempting to retrieve the properties and examining the values obtained. The typeof operator can be very helpful in determining the type of a property: 

```
typeof flight.number // 'number'
typeof flight.status // 'string'
typeof flight.arrival // 'object'
typeof flight.manifest // 'undefined'
```

Some care must be taken because any property on the prototype chain can produce a value:

```
typeof flight.toString // 'function'
typeof flight.constructor // 'function'
```

There are two approaches to dealing with these undesired properties. The first is to have your program look for and reject function values. Generally, when you are reflecting, you are interested in data, and so you should be aware that some values could be functions. The other approach is to use the hasOwnProperty method, which returns true if the object has a particular property. The hasOwnProperty method does not look at the prototype chain:

```
flight.hasOwnProperty('number') // true
flight.hasOwnProperty('constructor') // false
```

### 07. Enumeration

The for in statement can loop over all of the property names in an object. The enumeration will include all of the properties—including functions and prototype properties that you might not be interested in—so it is necessary to filter out the values youdon’t want. The most common filters are the hasOwnProperty method and using typeof to exclude functions:

```
var name;
for (name in another_stooge) {
    if (typeof another_stooge[name] !== 'function') {
    document.writeln(name + ': ' + another_stooge[name]);
    }
}
```

1『上面的方法可以经常拿来用。』

There is no guarantee on the order of the names, so be prepared for the names to appear in any order. If you want to assure that the properties appear in a particular order, it is best to avoid the for in statement entirely and instead make an array containing the names of the properties in the correct order: 

```
var i;
var properties = [
    'first-name',
    'middle-name',
    'last-name',
    'profession'
];

for (i = 0; i < properties.length; i += 1) {
    document.writeln(properties[i] + ': ' + another_stooge[properties[i]]);
}
```

By using for instead of for in, we were able to get the properties we wanted without worrying about what might be dredged up from the prototype chain, and we got them in the correct order.

1『使用 for 来遍历更佳。』

### 08. Delete

The delete operator can be used to remove a property from an object. It will remove a property from the object if it has one. It will not touch any of the objects in the prototype linkage. Removing a property from an object may allow a property from the prototype linkage to shine through:

```
another_stooge.nickname // 'Moe'
// Remove nickname from another_stooge, revealing the nickname of the prototype.
delete another_stooge.nickname;
another_stooge.nickname // 'Curly'
```

## 09. Global Abatement

JavaScript makes it easy to define global variables that can hold all of the assets of your application. Unfortunately, global variables weaken the resiliency of programs and should be avoided. One way to minimize the use of global variables is to create a single global variable for your application:

    var MYAPP = {};

That variable then becomes the container for your application: 

```
MYAPP.stooge = {
    "first-name": "Joe",
    "last-name": "Howard"
};

MYAPP.flight = {
    airline: "Oceanic",
    number: 815,
    departure: {
        IATA: "SYD",
        time: "2004-09-22 14:55",
        city: "Sydney"
    },
    arrival: {
        IATA: "LAX",
        time: "2004-09-23 10:42",
        city: "Los Angeles"
    }
};
```

1『就用一个全局变量，所有的东西全塞进这个全局对象里，哈哈。』

By reducing your global footprint to a single name, you significantly reduce the chance of bad interactions with other applications, widgets, or libraries. Your program also becomes easier to read because it is obvious that MYAPP.stooge refers to a top-level structure. In the next chapter, we will see ways to use closure for information hiding, which is another effective global abatement technique.

1『用闭包来 information hiding，闭包也是一种减少全局变量污染的有效手段。』

## 04. Function

The best thing about JavaScript is its implementation of functions. It got almost everything right. But, as you should expect with JavaScript, it didn’t get everything right. A function encloses a set of statements. Functions are the fundamental modular unit of JavaScript. They are used for code reuse, information hiding, and composition. Functions are used to specify the behavior of objects. Generally, the craft of programming is the factoring of a set of requirements into a set of functions and data structures.

1『函数是 JS 的灵魂所在，函数式编程嘛。』

### 01. Function Objects

Functions in JavaScript are objects. Objects are collections of name/value pairs having a hidden link to a prototype object. Objects produced from object literals are linked to Object.prototype. Function objects are linked to Function.prototype (which is itself linked to Object.prototype). Every function is also created with two additional hidden properties: the function’s context and the code that implements the function’s behavior.

1『 function’s context 是函数的上下文。』

3『Javascript 创建一个函数对象时，会给该对象设置一个「调用」属性。当 Javascript 调用一个函数时，可理解为调用此函数的「调用」属性。详细的描述请参阅 Ecmascript 规范的「13.2 Creating Function Objects」。』

Every function object is also created with a prototype property. Its value is an object with a constructor property whose value is the function. This is distinct from the hidden link to Function.prototype. The meaning of this convoluted construction will be revealed in the next chapter.

Since functions are objects, they can be used like any other value. Functions can be stored in variables, objects, and arrays. Functions can be passed as arguments to functions, and functions can be returned from functions. Also, since functions are objects, functions can have methods. The thing that is special about functions is that they can be invoked.

1『 JS 里函数是一个对象，太重要了。』

### 02. Function Literal

Function objects are created with function literals:

```
// Create a variable called add and store a function
// in it that adds two numbers.
var add = function (a, b) {
    return a + b;
};
```

A function literal has four parts. The first part is the reserved word function. The optional second part is the function’s name. The function can use its name to call itself recursively. The name can also be used by debuggers and development tools to identify the function. If a function is not given a name, as shown in the previous example, it is said to be anonymous. 

The third part is the set of parameters of the function, wrapped in parentheses. Within the parentheses is a set of zero or more parameter names, separated by commas. These names will be defined as variables in the function. Unlike ordinary variables, instead of being initialized to undefined, they will be initialized to the arguments supplied when the function is invoked. The fourth part is a set of statements wrapped in curly braces. These statements are the body of the function. They are executed when the function is invoked.

『函数的参数不像普通的变量那样将被初始化为 undefined，而是在该函数被调用时初始化为实际提供的参数的值。』

A function literal can appear anywhere that an expression can appear. Functions can be defined inside of other functions. An inner function of course has access to its parameters and variables. An inner function also enjoys access to the parameters and variables of the functions it is nested within. The function object created by a function literal contains a link to that outer context. This is called closure. This is the source of enormous expressive power.

『函数也可以被定义在其他函数中个内部函数，除了可以访问自己的参数和变量，同时它也能自由访问把它嵌套在其中的父函数的参数与变量。通过函数字面量创建的函数对象包含一个连到外部上下文的连接。这被称为闭包（closure）。它是 Javascript 强大表现力的来源。』

### 03. Invocation

Invoking a function suspends the execution of the current function, passing control and parameters to the new function. In addition to the declared parameters, every function receives two additional parameters: this and arguments. The this parameter is very important in object oriented programming, and its value is determined by the invocation pattern. There are four patterns of invocation in JavaScript: the method invocation pattern, the function invocation pattern, the constructor invocation pattern, and the apply invocation pattern. The patterns differ in how the bonus parameter this is initialized.

2『 this 的值取决于调用模式（invocation pattern）：the method invocation pattern, the function invocation pattern, the constructor invocation pattern, and the apply invocation pattern. 做一张术语卡片。』

The invocation operator is a pair of parentheses that follow any expression that produces a function value. The parentheses can contain zero or more expressions, separated by commas. Each expression produces one argument value. Each of the argument values will be assigned to the function’s parameter names. There is no runtime error when the number of arguments and the number of parameters do not match. If there are too many argument values, the extra argument values will be ignored. If there are too few argument values, the undefined value will be substituted for the missing values. There is no type checking on the argument values: any type of value can be passed to any parameter.

1『 parameter 实参，调用函数时传递进来的；argument 形参，定义函数时设定的。』

#### 1. The Method Invocation Pattern

When a function is stored as a property of an object, we call it a method. When a method is invoked, this is bound to that object. If an invocation expression contains a refinement (that is, a . dot expression or [subscript] expression), it is invoked as a method:

```
// Create myObject. It has a value and an increment
// method. The increment method takes an optional
// parameter. If the argument is not a number, then 1
// is used as the default.
var myObject = {
    value: 0,
    increment: function (inc) {
    this.value += typeof inc === 'number' ? inc : 1;
}
};

myObject.increment( );
document.writeln(myObject.value); // 1

myObject.increment(2);
document.writeln(myObject.value); // 3
```

A method can use this to access the object so that it can retrieve values from the object or modify the object. The binding of this to the object happens at invocation time. This very late binding makes functions that use this highly reusable. Methods that get their object context from this are called public methods.

1『对于「方法调用模式」，this 绑定其所属的对象，是发生在调用的时候。』

#### 2. The Function Invocation Pattern

When a function is not the property of an object, then it is invoked as a function: 

    var sum = add(3, 4); // sum is 7

When a function is invoked with this pattern, this is bound to the global object. This was a mistake in the design of the language. Had the language been designed correctly, when the inner function is invoked, this would still be bound to the this  variable of the outer function. A consequence of this error is that a method cannot employ an inner function to help it do its work because the inner function does not share the method’s access to the object as its this is bound to the wrong value. Fortunately, there is an easy workaround. If the method defines a variable and assigns it the value of this, the inner function will have access to this through that variable. By convention, the name of that variable is that:

1『对于「函数调用模式」，this 绑定到了全局对象上，这是 JS 的设计失误。倘若语言设计正确，那么当内部函数被调用时，this 应该仍然绑定到外部函数的 this 变量。这个设计错误的后果就是方法不能利用内部函数来帮助它工作，因为内部函数的 this 被绑定了错误的值，所以不能共享该方法对对象的访问权。幸运的是，有一个很容易的解决方案：如果该方法定义一个变量并给它赋值为 this，那么内部函数就可以通过那个变量访问到 this。按照约定，我把那个变量命名为 that。』

```
// Augment myObject with a double method.
myObject.double = function ( ) {
    var that = this; // Workaround.
    var helper = function ( ) {
        that.value = add(that.value, that.value);
    };
    helper( ); // Invoke helper as a function.
};

// Invoke double as a method.
myObject.double( );
document.writeln(myObject.getValue( )); // 6
```

1『方法模式调用，用 . 来调用；函数模式调用用 function(); 来调用；』

#### 4. The Apply Invocation Pattern

Because JavaScript is a functional object-oriented language, functions can have methods. The apply method lets us construct an array of arguments to use to invoke a function. It also lets us choose the value of this. The apply method takes two parameters. The first is the value that should be bound to this. The second is an array of parameters.

```
// Make an array of 2 numbers and add them.
var array = [3, 4];
var sum = add.apply(null, array); // sum is 7

// Make an object with a status member.
var statusObject = {
    status: 'A-OK'
};

// statusObject does not inherit from Quo.prototype,
// but we can invoke the get_status method on
// statusObject even though statusObject does not have
// a get_status method.
var status = Quo.prototype.get_status.apply(statusObject);
// status is 'A-OK'
```
















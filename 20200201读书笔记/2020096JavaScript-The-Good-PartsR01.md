# 2020096JavaScript-The-Good-PartsR01

英文版出版时间是 2008 年。

## 记忆时间

## 卡片

### 0101. 主题卡——JS 的精华

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——delegation

The prototype link is used only in retrieval. If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on until the process finally bottoms out with Object.prototype. If the desired property exists nowhere in the prototype chain, then the result is the undefined value. This is called delegation.

### 0202. 术语卡——this 值

Invoking a function suspends the execution of the current function, passing control and parameters to the new function. In addition to the declared parameters, every function receives two additional parameters: this and arguments. The this parameter is very important in object oriented programming, and its value is determined by the invocation pattern. There are four patterns of invocation in JavaScript: the method invocation pattern, the function invocation pattern, the constructor invocation pattern, and the apply invocation pattern. The patterns differ in how the bonus parameter this is initialized.

this 的值取决于调用模式（invocation pattern）：1）the method invocation pattern，方法式调用，this 绑定到该方法所隶属的对象（函数作为一个对象的某个属性值的时候才被称为方法），这个绑定是在调用时发生的；2）the function invocation pattern，函数式调用，this 绑定到全局变量上（JS 公认的设计错误），这导致内部函数无法通过 this 来访问外部函数的数据，即没法帮外部函数处理一些事情了，不过可以通过「var that = this; 」来解决；3）the constructor invocation pattern，构造函数式调用。这其实是对基于类的面向对象的妥协，用「new + 构造器函数」来调用构造器函数，会创建一个连接到构造函数原型链的新对象，this 绑定到这个新对象上。new 还会改变 return 语句的行为；4）the apply invocation pattern，apply 式调用。Quo.prototype.get_status.apply(statusObject); 是指定 this 绑定到 apply() 调用时传递的参数，在这里即 statusObject，所以 get\_status 函数里的 this.statu 即 statusObject 对象里的 status 属性值。

### 0203. 术语卡——闭包

This quo function is designed to be used without the new prefix, so the name is not capitalized. When we call quo, it returns a new object containing a get\_status method. A reference to that object is stored in myQuo. The get\_status method still has privileged access to quo’s status property even though quo has already returned. get\_status does not have access to a copy of the parameter; it has access to the parameter itself. This is possible because the function has access to the context in which it was created. This is called closure.

当我们调用 quo 时，它返回包含 get\_status 方法的一个新对象（调用函数即创建一个函数对象）。该对象的一个引用保存在 myQuo 中。即使 quo 已经返回了，但 get\_status 方法仍然享有访问 quo 对象的 status 属性的特权。get\_status 方法并不是访问该参数的一个副本，它访问的就是该参数本身。因为该函数可以访问它被创建时所处的上下文环境。这被称为闭包。

### 0204. 术语卡——Function

The best thing about JavaScript is its implementation of functions. It got almost everything right. But, as you should expect with JavaScript, it didn’t get everything right. A function encloses a set of statements. Functions are the fundamental modular unit of JavaScript. They are used for code reuse, information hiding, and composition. Functions are used to specify the behavior of objects. Generally, the craft of programming is the factoring of a set of requirements into a set of functions and data structures.

1『the craft of programming is the factoring of a set of requirements into a set of functions and data structures. 函数式编程的思想。』

Functions in JavaScript are objects. Objects are collections of name/value pairs having a hidden link to a prototype object. Objects produced from object literals are linked to Object.prototype. Function objects are linked to Function.prototype (which is itself linked to Object.prototype). Every function is also created with two additional hidden properties: the function’s context and the code that implements the function’s behavior.

Every function object is also created with a prototype property. Its value is an object with a constructor property whose value is the function. This is distinct from the hidden link to Function.prototype. The meaning of this convoluted construction will be revealed in the next chapter.

Since functions are objects, they can be used like any other value. Functions can be stored in variables, objects, and arrays. Functions can be passed as arguments to functions, and functions can be returned from functions. Also, since functions are objects, functions can have methods. The thing that is special about functions is that they can be invoked.

Javascript 创建一个函数对象时，会给该对象设置一个「调用」属性。当 Javascript 调用一个函数时，可理解为调用此函数的「调用」属性。

### 0205. 术语卡——函数调用

The invocation operator is a pair of parentheses that follow any expression that produces a function value. The parentheses can contain zero or more expressions, separated by commas. Each expression produces one argument value. Each of the argument values will be assigned to the function’s parameter names. There is no runtime error when the number of arguments and the number of parameters do not match. If there are too many argument values, the extra argument values will be ignored. If there are too few argument values, the undefined value will be substituted for the missing values. There is no type checking on the argument values: any type of value can be passed to any parameter.

醍醐灌顶，函数调用和用字面量创建函数是两码事，调用最关键的是那对圆括号 ()，圆括号前面可以是函数名，也可以是函数字面量。而圆括号里面是要传递进函数的实参；parameter 实参，调用函数时传递进来的。argument 形参，定义函数时设定的。

### 0206. 信息卡——代码风格

Throughout this book I have used a consistent style. My intention was to make the code examples as easy to read as possible. I used whitespace consistently to give you more cues about the meaning of my programs.

I indented the contents of blocks and object literals four spaces. I placed a space between if and ( so that the if didn’t look like a function invocation. Only in invocations do I make ( adjacent with the preceding symbol. I put spaces around all infix operators except for . and [, which do not get spaces because they have higher precedence. I use a space after every comma and colon. I put at most one statement on a line. Multiple statements on a line can be misread.

If a statement doesn’t fit on a line, I will break it after a comma or a binary operator. That gives more protection against copy/paste errors that are masked by semicolon insertion. (The tragedy of semicolon insertion will be revealed in Appendix A.) I indent the remainder of the statement an extra four spaces, or eight spaces if four would be ambiguous (such as a line break in the condition part of an if statement). I always use blocks with structured statements such as if and while because it is less error prone. I have seen:

使用一致的留白来理解程序的逻辑思路。1）代码块内容和对象字面量缩进 4 个空格。2）放了一个空格在 if 和 ( 之间，以致 if 不会看起来像一个函数调用。只有真的是在调用时，才使 ( 和其前面的符号相毗连。3）在除了 . 和 [ 外的所有中置运算符的两边都放了空格，它们俩无须空格是因为它们有更高的优先级。4）在每个逗号和冒号后面都使用一个空格。5）在每行最多放一个语句，在一行里放多条语句可能会被误读。如果一个语句一行放不下，我会在一个冒号或二元运算符后拆开它。给折断后的语句的其余部分多缩进 4 个空格，如果 4 个还不够明显，就缩进 8 个空格（例如在一个 if 语句的条件部分插入一个换行符的时候）。6）在诸如 if 和 while 这样结构化的语句里，始终使用代码块，因为这样会减少出错的概率。

### 0301. 人名卡——Douglas Crockford

Douglas Crockford，本书作者。

贡献及著作

### 0401. 金句卡——Most programming languages contain good parts and bad parts.

Most programming languages contain good parts and bad parts. I discovered that I could be a better programmer by using only the good parts and avoiding the bad parts

## 书评

### 01

它概括了 JavaScript 这个脚本语言的核心内容，不仅总结了语言的精华部分，还指出了「鸡肋」和「糟粕」。如果说犀牛书展现了 JavaScript 特性的丰富和功能的强大，这本书就体现了 JavaScript 语言轻巧简洁的特点。其实 JavaScript 就是这么简洁，但是它很灵活，使用得好，可以编写出功能强大的程序。语言中核心的内容，也就是犀牛书的第一部分，全部在这本书中被总结出来了。但这并不表示可以从这本书入门，它不是入门级的，不适合初学者。作为概括总结，它是一本很好的帮助你提高 JavaScript 水平的书籍，因为总结也是学习的过程。

这本书的特点是，薄但内容丰富。它用精炼的文字、形象的语法图（railroad diagram）和简短的代码片断总结了 JavaScript 的核心内容。对于对 JavaScript 已经有较深理解的人来说，它可以帮助你整理总结并加深对 JavaScript 的理解，对于了解程度低一点的人来说，它可以帮助你学习 JavaScript 的编程思想。不过就像作者的前言所说的，必须反复阅读。这也正是我决定购买这本书的原因。书的最后那个 json_parse 的例子给我的印象很深。这是本书唯一一个完整的实例代码，它包含了 JavaScript 中很多重要的知识点和代码设计风格（比如闭包），很值得研究学习。

### 02

就如其「最被低估的编程语言」称号所述，Javascript 实际上是一门非常优秀的语言，看似熟悉的语法之下隐含的是完全不同的世界观。尤其是在学、用 erlang 这种函数语言几年后，更能体会其很多设计元素的精巧之处。转贴几条 twitter 上记录的读书笔记备查：

1、Javascript 语言中支持四类函数调用方式：1）全局函数。2）对象方法。3）构造函数。4）apply/call 调用。区别在于函数内 this 指针的绑定，分别是：1）Global 对象。2）调用对象。3）构造返回对象。4）调用时传入的第一个参数。2、作为 Prototype-base 和 Functional 编程混杂体的 Javascript，居然不提供尾递归 (tail-end recursion) 真是个杯具啊。所以有人想出了这种用 setTimeout 模拟的山寨办法。3、没有变量块作用域 (Block Scope) 的支持，是 Javascript 语义上与 C/C++ 系统又一重大区别。但回过头来看 Python/Scheme 也不提供块作用域的支持，究竟是当年的设计错误还是我们的思维定势问题？

1『函数内 this 指针的绑定，对象的绑定，对理解变量、引用醍醐灌顶。』

4、A Better Javascript Memoizer 利用闭包 (Closure) 和匿名方法 (anonymous function)，实现针对任意参数个数的 memoizer 模式，对复杂函数的计算结果进行缓存，那是相当的优雅。5、说起来 Javascript 中自动添加语句结束分号 (semicolon insertion) 也算是一个功能，可以很大程度上提高对网页上语法不规范脚本的兼容性。杯具的是各家的容忍限度不同方法不同，所以基本被列入不应被使用的糟粕。6、Javascript 里面的 NaN 本身就是个杯具，NaN != NaN 但 typeof NaN === 'number'，必须通过 isNaN 或 isFinite 才能筛选出，但这个可怜的函数又会自动对参数进行隐式类型转换。7、假以时日，HTTPS 和 Javascript 有可能成为 Web 领域，类似今天 TCP/IP 和 C/C++ 的基础构架的地位。不知十年后再回头看今日的理解，又是一番如何的景象，期待。

### 03

第一本书：JavaScript 高级程序设计。第二本书：ppk 谈 JavaScript。这是第三本。久闻大名的书，读完之后并没有预想的那种感觉。也许是因为书中的很多观点处处通用，即使你没有写过 js，也会从其他语言的普遍做法中见识到。The Definitive Guide 今年又出了新版，非常有可读性，两相对比之下不免让人感觉没那么棒。但这绝对是一本很奇特的书，两个地方：1）印象中其他语言没有对应的著作，例如 "Java: The Good Parts". C 有一本 pitfalls，但和这本不太一样。js 好的地方列了一遍，不好的地方也列了一遍。2）Appendix 比正文精彩。全书的精华都在 Appendix 了。最后我想说的是，这不是 js 语法书，看中这书薄而放弃 the definitive guide 的同学们，你们亏大了。

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

JS 里的精华部分概述。

### 2. 摘录及评论

When I was a young journeyman programmer, I would learn about every feature of the languages I was using, and I would attempt to use all of those features when I wrote. I suppose it was a way of showing off, and I suppose it worked because I was the guy you went to if you wanted to know how to use a particular feature. Eventually I figured out that some of those features were more trouble than they were worth. Some of them were poorly specified, and so were more likely to cause portability problems. Some resulted in code that was difficult to read or modify. Some induced me to write in a manner that was too tricky and error-prone. And some of those features were design errors. Sometimes language designers make mistakes.

Most programming languages contain good parts and bad parts. I discovered that I could be a better programmer by using only the good parts and avoiding the bad parts. After all, how can you build something good out of bad parts? It is rarely possible for standards committees to remove imperfections from a language because doing so would cause the breakage of all of the bad programs that depend on those bad parts. They are usually powerless to do anything except heap more features on top of the existing pile of imperfections. And the new features do not always interact harmoniously, thus producing more bad parts. But you have the power to define your own subset. You can write better programs by relying exclusively on the good parts.

2『 Most programming languages contain good parts and bad parts. I discovered that I could be a better programmer by using only the good parts and avoiding the bad parts. 做一张金句卡片。每种语言都有好的部分和坏的部分，制定标准的组织因为各种原因不可能把坏的部分剔除掉，只能不断的加新的特性。但作为个体，我们有权利和义务只使用语言里好的部分。』

JavaScript is a language with more than its share of bad parts. It went from nonexistence to global adoption in an alarmingly short period of time. It never had an interval in the lab when it could be tried out and polished. It went straight into Netscape Navigator 2 just as it was, and it was very rough. When Java™ applets failed, JavaScript became the「Language of the Web」by default. JavaScript’s popularity is almost completely independent of its qualities as a programming language.

Fortunately, JavaScript has some extraordinarily good parts. In JavaScript, there is a beautiful, elegant, highly expressive language that is buried under a steaming pile of good intentions and blunders. The best nature of JavaScript is so effectively hidden that for many years the prevailing opinion of JavaScript was that it was an unsightly, incompetent toy. My intention here is to expose the goodness in JavaScript, an out-standing, dynamic programming language. JavaScript is a block of marble, and I chip away the features that are not beautiful until the language’s true nature reveals itself. I believe that the elegant subset I carved out is vastly superior to the language as a whole, being more reliable, readable, and maintainable.

1『 JS 的精华在于 out-standing, dynamic programming language. 』

This book will not attempt to fully describe the language. Instead, it will focus on the good parts with occasional warnings to avoid the bad. The subset that will be described here can be used to construct reliable, readable programs small and large. By focusing on just the good parts, we can reduce learning time, increase robustness, and save some trees.

Perhaps the greatest benefit of studying the good parts is that you can avoid the need to unlearn the bad parts. Unlearning bad patterns is very difficult. It is a painful task that most of us face with extreme reluctance. Sometimes languages are subsetted to make them work better for students. But in this case, I am subsetting JavaScript to make it work better for professionals.

### 01. Why JavaScript?

JavaScript is an important language because it is the language of the web browser. Its association with the browser makes it one of the most popular programming languages in the world. At the same time, it is one of the most despised programming languages in the world. The API of the browser, the Document Object Model (DOM) is quite awful, and JavaScript is unfairly blamed. The DOM would be painful to work with in any language. The DOM is poorly specified and inconsistently implemented. This book touches only very lightly on the DOM. I think writing a Good Parts book about the DOM would be extremely challenging.

1『 DOM 太挫，拿得出手的东西很少。』

JavaScript is most despised because it isn’t some other language. If you are good in some other language and you have to program in an environment that only supports JavaScript, then you are forced to use JavaScript, and that is annoying. Most people in that situation don’t even bother to learn JavaScript first, and then they are surprised when JavaScript turns out to have significant differences from the some other language they would rather be using, and that those differences matter.

The amazing thing about JavaScript is that it is possible to get work done with it without knowing much about the language, or even knowing much about programming. It is a language with enormous expressive power. It is even better when you know what you’re doing. Programming is difficult business. It should never be undertaken in ignorance.

1『enormous expressive power. 是 JS 的一大特点。』

### 02. Analyzing JavaScript

JavaScript is built on some very good ideas and a few very bad ones. The very good ideas include functions, loose typing, dynamic objects, and an expressive object literal notation. The bad ideas include a programming model based on global variables.

1『 ES6 引入的 let、const 就是为了解决「a programming model based on global variables.」』

JavaScript’s functions are first class objects with (mostly) lexical scoping. JavaScript is the first lambda language to go mainstream. Deep down, JavaScript has more in common with Lisp and Scheme than with Java. It is Lisp in C’s clothing. This makes JavaScript a remarkably powerful language.

The fashion in most programming languages today demands strong typing. The theory is that strong typing allows a compiler to detect a large class of errors at compile time. The sooner we can detect and repair errors, the less they cost us. JavaScript is a loosely typed language, so JavaScript compilers are unable to detect type errors. This can be alarming to people who are coming to JavaScript from strongly typed languages. But it turns out that strong typing does not eliminate the need for careful testing. And I have found in my work that the sorts of errors that strong type checking finds are not the errors I worry about. On the other hand, I find loose typing to be liberating. I don’t need to form complex class hierarchies. And I never have to cast or wrestle with the type system to get the behavior that I want.

1『 JS 是弱类型语言。作者认为强类型语言（比如 Java）在类型强制上能提供的真正有用的价值有限，还不如弱类型呢。』

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

1『附录 C 作者给了个工具可以检测出代码里，糟糕的 JS 语法内容。』

JavaScript is a language of many contrasts. It contains many errors and sharp edges, so you might wonder,「Why should I use JavaScript?」There are two answers. The first is that you don’t have a choice. The Web has become an important platform for application development, and JavaScript is the only language that is found in all browsers. It is unfortunate that Java failed in that environment; if it hadn’t, there could be a choice for people desiring a strongly typed classical language. But Java did fail and JavaScript is flourishing, so there is evidence that JavaScript did something right. The other answer is that, despite its deficiencies, JavaScript is really good. It is lightweight and expressive. And once you get the hang of it, functional programming is a lot of fun.

1『原来 JS 就是面向函数式的编程。』

But in order to use the language well, you must be well informed about its limitations. I will pound on those with some brutality. Don’t let that discourage you. The good parts are good enough to compensate for the bad parts.

### 03. A Simple Testing Ground

If you have a web browser and any text editor, you have everything you need to run JavaScript programs. First, make an HTML file with a name like program.html:

```js
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

```js
Function.prototype.method = function (name, func) {
    this.prototype[name] = func;
    return this;
};
```

## 02. Grammar

### 1. 逻辑脉络

JS 的语法内容，包括空白符、命令规则、各基本类型、语句、表达式、字面量和函数。

### 2. 摘录及评论

This chapter introduces the grammar of the good parts of JavaScript, presenting a quick overview of how the language is structured. We will represent the grammar with railroad diagrams. The rules for interpreting these diagrams are simple: 1) You start on the left edge and follow the tracks to the right edge. 2) As you go, you will encounter literals in ovals, and rules or descriptions in rectangles.『图里面圆形的是 literals，矩形的是 rules or descriptions. 』3) Any sequence that can be made by following the tracks is legal. 4) Any sequence that cannot be made by following the tracks is not legal. 5) Railroad diagrams with one bar at each end allow whitespace to be inserted between any pair of tokens. Railroad diagrams with two bars at each end do not.

The grammar of the good parts presented in this chapter is significantly simpler than the grammar of the whole language.

### 01. Whitespace

Whitespace can take the form of formatting characters or comments. Whitespace is usually insignificant, but it is occasionally necessary to use whitespace to separate sequences of characters that would otherwise be combined into a single token. For example, in:

    var that = this;

the space between var and that cannot be removed, but the other spaces can be removed.

JavaScript offers two forms of comments. Obsolete comments are worse than no comments. The /* */ form of block comments came from a language called PL/I. PL/I chose those strange pairs as the symbols for comments because they were unlikely to occur in that language’s programs, except perhaps in string literals. In JavaScript, those pairs can also occur in regular expression literals, so block comments are not safe for commenting out blocks of code. For example:

```js
/*
var rm_a = /a*/.match(s);
*/
```

causes a syntax error. So, it is recommended that /* */ comments be avoided and // comments be used instead. In this book, // will be used exclusively.

### 02. Names

A name is a letter optionally followed by one or more letters, digits, or underbars. A name cannot be one of these reserved words:

```js
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

1『 JS 里的对象 Math 包含一系列对数字处理的方法。』

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

1『链接器（Linker）是编程语言或操作系统提供的工具，它的工作就是解析未定义的符号引用，将目标文件中的占位符替换为符号地址。』

When used inside of a function, the var statement defines the function’s private variables. The switch, while, for, and do statements are allowed to have an optional label prefix that interacts with the break statement.

1『原来在函数内部用 var 申明的变量是函数的私有变量；label prefix 是指这种形式「label: expressions statement;」』

Statements tend to be executed in order from top to bottom. The sequence of execution can be altered by the conditional statements (if and switch), by the looping statements (while, for, and do), by the disruptive statements (break, return, and throw), and by function invocation.

A block is a set of statements wrapped in curly braces. Unlike many other languages, blocks in JavaScript do not create a new scope, so variables should be defined at the top of the function, not in blocks.

The if statement changes the flow of the program based on the value of the expression. The then block is executed if the expression is truthy; otherwise, the optional else branch is taken. Here are the falsy values: 1) false. 2) null. 3) undefined. 4) The empty string ''. 5) The number 0. 6) The number NaN.

All other values are truthy, including true, the string 'false', and all objects. The switch statement performs a multiway branch. It compares the expression for equality with all of the specified cases. The expression can produce a number or a string. When an exact match is found, the statements of the matching case clause are executed. If there is no match, the optional default statements are executed.

A case clause contains one or more case expressions. The case expressions need not be constants. The statement following a clause should be a disruptive statement to prevent fall through into the next case. The break statement can be used to exit from a switch.

The while statement performs a simple loop. If the expression is falsy, then the loop will break. While the expression is truthy, the block will be executed.

The for statement is a more complicated looping statement. It comes in two forms.

The conventional form is controlled by three optional clauses: the initialization, the condition, and the increment. First, the initialization is done, which typically initializes the loop variable. Then, the condition is evaluated. Typically, this tests the loop variable against a completion criterion. If the condition is omitted, then a condition of true is assumed. If the condition is falsy, the loop breaks. Otherwise, the block is executed, then the increment executes, and then the loop repeats with the condition.

The other form (called for in) enumerates the property names (or keys) of an object. On each iteration, another property name string from the object is assigned to the variable. It is usually necessary to test object.hasOwnProperty(variable) to determine whether the property name is truly a member of the object or was found instead on the prototype chain.

『可以通过这个方法来检测这个属性名是该对象的成员，还是来自于原型链。』

```js
for (myvar in obj) {
    if (obj.hasOwnProperty(myvar)) {
    ...
    }
}
```

The do statement is like the while statement except that the expression is tested after the block is executed instead of before. That means that the block will always be executed at least once.

The try statement executes a block and catches any exceptions that were thrown by the block. The catch clause defines a new variable that will receive the exception object.

The throw statement raises an exception. If the throw statement is in a try block, then control goes to the catch clause. Otherwise, the function invocation is abandoned, and control goes to the catch clause of the try in the calling function. The expression is usually an object literal containing a name property and a message property. The catcher of the exception can use that information to determine what to do.

Throw 语句抛出一个异常。如果 throw 语句在一个 try 代码块中，那么控制流会跳转到 catch 从句中。如果 throw 语句在函数中，则该函数调用被放弃，控制流跳转到调用该函数的 try 语句的 catch 从句中。throw 语句中的表达式通常是一个对象字面量，它包含一个 name 属性和一个 message 属性。异常捕获器可以使用这些信息去决定该做什么。

The return statement causes the early return from a function. It can also specify the value to be returned. If a return expression is not specified, then the return value will be undefined. JavaScript does not allow a line end between the return and the expression.

The break statement causes the exit from a loop statement or a switch statement. It can optionally have a label that will cause an exit from the labeled statement. JavaScript does not allow a line end between the break and the label.

An expression statement can either assign values to one or more variables or members, invoke a method, delete a property from an object. The = operator is used for assignment. Do not confuse it with the === equality operator. The += operator can add or concatenate.

### 06. Expressions

The simplest expressions are a literal value (such as a string or number), a variable, a built-in value (true, false, null, undefined, NaN, or Infinity), an invocation expression preceded by new, a refinement expression preceded by delete, an expression wrapped in parentheses, an expression preceded by a prefix operator, or an expression followed by: 1) An infix operator and another expression. 2) The ? ternary operator followed by another expression, then by :, and then by yet another expression. 3) An invocation. 4) A refinement.

The ? ternary operator takes three operands. If the first operand is truthy, it produces the value of the second operand. But if the first operand is falsy, it produces the value of the third operand.

The operators at the top of the operator precedence list in Table 2-1 have higher precedence. They bind the tightest. The operators at the bottom have the lowest precedence. Parentheses can be used to alter the normal precedence, so: 

```js
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

Object literals are a convenient notation for specifying new objects. The names of the properties can be specified as names or as strings. The names are treated as literal names, not as variable names, so the names of the properties of the object must be known at compile time. The values of the properties are expressions. There will be more about object literals in the next chapter. Array literals are a convenient notation for specifying new arrays. There will be more about array literals in Chapter 6. There will be more about regular expressions in Chapter 7.

『 Literals 即字面量。对象字面量是一种可以方便地按指定规格创建新对象的表示法。属性名可以是标识符或字符串。这些名字被当做字面量名而不是变量名来对待，所以对象的属性名在编译时才能知道。属性的值就是表达式。』

### 08. Functions

A function literal defines a function value. It can have an optional name that it can use to call itself recursively. It can specify a list of parameters that will act as variables initialized by the invocation arguments. The body of the function includes variable definitions and statements. There will be more about functions in Chapter 4.

## 03. Objects

### 1. 逻辑脉络

对象是一系列「属性」的集合，属性有属性名和属性值，属性名可以是字符串、空值和 symbol 类型，属性值可以是除 undefined 外的任何东西；对象是可变的，可以动态的添加属性；对象的传递是通过引用而非复制，比如「var x = stooge; 」是把 stooge 对象的引用复制给 x 变量，或者说 stooge 和 x 指向同一个对象，或者说将变量 x 绑定到 stooge 指向的对象上；所有的对象都是链接到其原型对象上的，创建的时候是从其原型对象上继承了所有属性。所有通过字面量创建的对象其原型对象都是「Object.prototype」。

### 2. 摘录及评论

The simple types of JavaScript are numbers, strings, booleans (true and false), null, and undefined. All other values are objects. Numbers, strings, and booleans are object-like in that they have methods, but they are immutable. Objects in JavaScript are mutable keyed collections. In JavaScript, arrays are objects, functions are objects, regular expressions are objects, and, of course, objects are objects.

An object is a container of properties, where a property has a name and a value. A property name can be any string, including the empty string. A property value can be any JavaScript value except for undefined.

Objects in JavaScript are class-free. There is no constraint on the names of new properties or on the values of properties. Objects are useful for collecting and organizing data. Objects can contain other objects, so they can easily represent tree or graph structures. JavaScript includes a prototype linkage feature that allows one object to inherit the properties of another. When used well, this can reduce object initialization time and memory consumption.

1『 JS 中的对象是无类型的（class-free）。』

### 01. Object Literals

Object literals provide a very convenient notation for creating new object values. An object literal is a pair of curly braces surrounding zero or more name/value pairs. An object literal can appear anywhere an expression can appear: 

1『字面量只是下面等号右边的部分，它是一个 notation，可以方便的创建对象、数组等。对字面量的理解又加深了一步。（2020-03-29）』

```js
var empty_object = {};

var stooge = {
    "first-name": "Jerome",
    "last-name": "Howard"
};
```

A property’s name can be any string, including the empty string. The quotes around a property’s name in an object literal are optional if the name would be a legal JavaScript name and not a reserved word. So quotes are required around "first-name", but are optional around first-name. Commas are used to separate the pairs. A property’s value can be obtained from any expression, including another object literal. Objects can nest:

```js
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

```js
stooge["first-name"] // "Joe"
flight.departure.IATA // "SYD"
```

The undefined value is produced if an attempt is made to retrieve a nonexistent member:

```js
stooge["middle-name"] // undefined
flight.status // undefined
stooge["FIRST-NAME"] // undefined
```

The || operator can be used to fill in default values: 

```js
var middle = stooge["middle-name"] || "(none)"; 
var status = flight.status || "unknown";
```

Attempting to retrieve values from undefined will throw a TypeError exception. This can be guarded against with the && operator:

```js
flight.equipment // undefined flight.equipment.model // throw "TypeError"
flight.equipment && flight.equipment.model // undefined Retrieval
```

### 03. Update

A value in an object can be updated by assignment. If the property name already exists in the object, the property value is replaced:

    stooge['first-name'] = 'Jerome';

If the object does not already have that property name, the object is augmented: 

```js
stooge['middle-name'] = 'Lester';
stooge.nickname = 'Curly';
flight.equipment = {
    model: 'Boeing 777'
};
flight.status = 'overdue';
```

### 04. Reference

Objects are passed around by reference. They are never copied: 

```js
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

```js
if (typeof Object.create !== 'function') {
    Object.create = function (o) {
    var F = function () {};
    F.prototype = o;
    return new F();
};
}

var another_stooge = Object.create(stooge);
```

3『「2019013程勋非的重学前端R01.md」

有这个例子：这段代码创建了一个空函数作为类，并把传入的原型挂在了它的 prototype，最后创建了一个它的实例，根据 new 的行为，这将产生一个以传入的第一个参数为原型的对象。这个函数无法做到与原生的 Object.create 一致，一个是不支持第二个参数，另一个是不支持 null 作为原型，所以放到今天意义已经不大了。ES6 以来，JavaScript 提供了一系列内置函数，以便更为直接地访问操纵原型。三个方法分别为：1）Object.create 根据指定的原型创建新对象，原型可以是 null；2）Object.getPrototypeOf 获得一个对象的原型；3）Object.setPrototypeOf 设置一个对象的原型。利用这三个方法，我们可以完全抛开类的思维，利用原型来实现抽象和复用。ES6 中加入了新特性 class，new 跟 function 搭配的怪异行为终于可以退休了（虽然运行时没有改变），在任何场景，我都推荐使用 ES6 的语法来定义类，而令 function 回归原本的函数语义。』

1『注意，winter 只是建议在用使用基于类的面向对象时使用新语法 class 来定义类，有些场景下照样可以用基于原型的面向对象。』

The prototype link has no effect on updating. When we make changes to an object, the object’s prototype is not touched:

```js
another_stooge['first-name'] = 'Harry';
another_stooge['middle-name'] = 'Moses';
another_stooge.nickname = 'Moe';
```

The prototype link is used only in retrieval. If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on until the process finally bottoms out with Object.prototype. If the desired property exists nowhere in the prototype chain, then the result is the undefined value. This is called delegation.

The prototype relationship is a dynamic relationship. If we add a new property to a prototype, that property will immediately be visible in all of the objects that are based on that prototype:

```js
stooge.profession = 'actor';
another_stooge.profession // 'actor'
```

We will see more about the prototype chain in Chapter 6.

2『

通过作者提供的方法可以阻断子对象触达父对象的原型链。做一张计算机的信息卡片。

```js
// 阻断子对象触达父对象的原型链
if (typeof Object.create !== 'function') {
    Object.create = function (o) {
        var F = function () {};
        F.prototype = o;
        return new F(); 
    };
}

var stooge = {
    "firstname": "Feng",
    "lastname": "Dalong",
};

console.log(stooge);

stooge['middlename'] = 'hahei';
stooge.nickname = 'dalong';
console.log(stooge);

var x = stooge;
x.height = '168cm';
console.log(stooge);

var y = Object.create(stooge);
y.food = 'apple';
console.log(stooge);

stooge.programming = 'JS';
console.log('x: ' + x.programming);
console.log('y: ' + y.programming);
```

』

### 06. Reflection

It is easy to inspect an object to determine what properties it has by attempting to retrieve the properties and examining the values obtained. The typeof operator can be very helpful in determining the type of a property: 

```js
typeof flight.number // 'number'
typeof flight.status // 'string'
typeof flight.arrival // 'object'
typeof flight.manifest // 'undefined'
```

Some care must be taken because any property on the prototype chain can produce a value:

```js
typeof flight.toString // 'function'
typeof flight.constructor // 'function'
```

There are two approaches to dealing with these undesired properties. The first is to have your program look for and reject function values. Generally, when you are reflecting, you are interested in data, and so you should be aware that some values could be functions. The other approach is to use the hasOwnProperty method, which returns true if the object has a particular property. The hasOwnProperty method does not look at the prototype chain:

```js
flight.hasOwnProperty('number') // true
flight.hasOwnProperty('constructor') // false
```

1『两种方法剔除掉原型链上原生的属性，一是自己写方法剔除，一是用 hasOwnProperty() 来过滤。』

### 07. Enumeration

The for in statement can loop over all of the property names in an object. The enumeration will include all of the properties—including functions and prototype properties that you might not be interested in—so it is necessary to filter out the values you don’t want. The most common filters are the hasOwnProperty method and using typeof to exclude functions:

```js
var name;
for (name in another_stooge) {
    if (typeof another_stooge[name] !== 'function') {
    document.writeln(name + ': ' + another_stooge[name]);
    }
}
```

1『上面的方法可以经常拿来用。』

There is no guarantee on the order of the names, so be prepared for the names to appear in any order. If you want to assure that the properties appear in a particular order, it is best to avoid the for in statement entirely and instead make an array containing the names of the properties in the correct order: 

```js
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

1『使用 for 来遍历更佳，但前提是要有需要遍历的属性名的数组。』

### 08. Delete

The delete operator can be used to remove a property from an object. It will remove a property from the object if it has one. It will not touch any of the objects in the prototype linkage. Removing a property from an object may allow a property from the prototype linkage to shine through:

```js
another_stooge.nickname // 'Moe'
// Remove nickname from another_stooge, revealing the nickname of the prototype.
delete another_stooge.nickname;
another_stooge.nickname // 'Curly'
```

1『之前用 Object.create() 封装，让子对象不能触达父对象的原型链，此时删除掉子对象的这个属性后，其父对象原型链上的属性也就暴露出来了。』

### 09. Global Abatement

JavaScript makes it easy to define global variables that can hold all of the assets of your application. Unfortunately, global variables weaken the resiliency of programs and should be avoided. One way to minimize the use of global variables is to create a single global variable for your application:

    var MYAPP = {};

That variable then becomes the container for your application: 

```js
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

1『函数是 JS 的灵魂所在，函数式编程。』

### 01. Function Objects

Functions in JavaScript are objects. Objects are collections of name/value pairs having a hidden link to a prototype object. Objects produced from object literals are linked to Object.prototype. Function objects are linked to Function.prototype (which is itself linked to Object.prototype). Every function is also created with two additional hidden properties: the function’s context and the code that implements the function’s behavior.

1『 function’s context 是函数的上下文；函数对象在被创建时默认有 2 个隐藏属性：函数上下文和实现函数行为的 code（目前的理解即为调用属性）。函数上下文这个隐藏属性跟闭包密切相关，甚至于就是闭包。（2020-03-29）』

3『 Javascript 创建一个函数对象时，会给该对象设置一个「调用」属性。当 Javascript 调用一个函数时，可理解为调用此函数的「调用」属性。详细的描述请参阅 Ecmascript 规范的「13.2 Creating Function Objects」。』

2『去找规范里的「Creating Function Objects」看。』

Every function object is also created with a prototype property. Its value is an object with a constructor property whose value is the function. This is distinct from the hidden link to Function.prototype. The meaning of this convoluted construction will be revealed in the next chapter.

Since functions are objects, they can be used like any other value. Functions can be stored in variables, objects, and arrays. Functions can be passed as arguments to functions, and functions can be returned from functions. Also, since functions are objects, functions can have methods. The thing that is special about functions is that they can be invoked.

### 02. Function Literal

Function objects are created with function literals:

```js
// Create a variable called add and store a function
// in it that adds two numbers.
var add = function (a, b) {
    return a + b;
};
```

A function literal has four parts. The first part is the reserved word function. The optional second part is the function’s name. The function can use its name to call itself recursively. The name can also be used by debuggers and development tools to identify the function. If a function is not given a name, as shown in the previous example, it is said to be anonymous. 

The third part is the set of parameters of the function, wrapped in parentheses. Within the parentheses is a set of zero or more parameter names, separated by commas. These names will be defined as variables in the function. Unlike ordinary variables, instead of being initialized to undefined, they will be initialized to the arguments supplied when the function is invoked. The fourth part is a set of statements wrapped in curly braces. These statements are the body of the function. They are executed when the function is invoked.

函数的参数不像普通的变量那样将被初始化为 undefined，而是在该函数被调用时初始化为实际提供的参数的值。

A function literal can appear anywhere that an expression can appear. Functions can be defined inside of other functions. An inner function of course has access to its parameters and variables. An inner function also enjoys access to the parameters and variables of the functions it is nested within. The function object created by a function literal contains a link to that outer context. This is called closure. This is the source of enormous expressive power.

函数也可以被定义在其他函数中个内部函数，除了可以访问自己的参数和变量，同时它也能自由访问把它嵌套在其中的父函数的参数与变量。通过函数字面量创建的函数对象包含一个连到外部上下文的连接。这被称为闭包（closure）。它是 Javascript 强大表现力的来源。

1『字面量创建的函数对象包含一个连到外部上下文的连接。那么通过原型对象创建的函数对象呢？』

### 03. Invocation

Invoking a function suspends the execution of the current function, passing control and parameters to the new function. In addition to the declared parameters, every function receives two additional parameters: this and arguments. The this parameter is very important in object oriented programming, and its value is determined by the invocation pattern. There are four patterns of invocation in JavaScript: the method invocation pattern, the function invocation pattern, the constructor invocation pattern, and the apply invocation pattern. The patterns differ in how the bonus parameter this is initialized.

2『 this 的值取决于调用模式（invocation pattern）：1）the method invocation pattern，方法式调用，this 绑定到该方法所隶属的对象（函数作为一个对象的某个属性值的时候才被称为方法），这个绑定是在调用时发生的；2）the function invocation pattern，函数式调用，this 绑定到全局变量上（JS 公认的设计错误），这导致内部函数无法通过 this 来访问外部函数的数据，即没法帮外部函数处理一些事情了，不过可以通过「var that = this; 」来解决；3）the constructor invocation pattern，构造函数式调用。这其实是对基于类的面向对象的妥协，用「new + 构造器函数」来调用构造器函数，会创建一个连接到构造函数原型链的新对象，this 绑定到这个新对象上。new 还会改变 return 语句的行为；4）the apply invocation pattern，apply 式调用。Quo.prototype.get_status.apply(statusObject); 是指定 this 绑定到 apply() 调用时传递的参数，在这里即 statusObject，所以 get_status 函数里的 this.statu 即 statusObject 对象里的 status 属性值。做一张术语卡片。』

The invocation operator is a pair of parentheses that follow any expression that produces a function value. The parentheses can contain zero or more expressions, separated by commas. Each expression produces one argument value. Each of the argument values will be assigned to the function’s parameter names. There is no runtime error when the number of arguments and the number of parameters do not match. If there are too many argument values, the extra argument values will be ignored. If there are too few argument values, the undefined value will be substituted for the missing values. There is no type checking on the argument values: any type of value can be passed to any parameter.

1『醍醐灌顶，函数调用和用字面量创建函数是两码事，调用最关键的是那对圆括号 ()，圆括号前面可以是函数名，也可以是函数字面量。而圆括号里面是要传递进函数的实参；parameter 实参，调用函数时传递进来的。argument 形参，定义函数时设定的。』

#### 1. The Method Invocation Pattern

When a function is stored as a property of an object, we call it a method. When a method is invoked, this is bound to that object. If an invocation expression contains a refinement (that is, a . dot expression or [subscript] expression), it is invoked as a method:

```js
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

对于「函数调用模式」，this 绑定到了全局对象上，这是 JS 的设计失误。倘若语言设计正确，那么当内部函数被调用时，this 应该仍然绑定到外部函数的 this 变量。这个设计错误的后果就是方法不能利用内部函数来帮助它工作，因为内部函数的 this 被绑定了错误的值，所以不能共享该方法对对象的访问权。幸运的是，有一个很容易的解决方案：如果该方法定义一个变量并给它赋值为 this，那么内部函数就可以通过那个变量访问到 this。按照约定，我把那个变量命名为 that。

```js
var myObject = {
    value: 0,
    increment: function (inc) {
    this.value += typeof inc === 'number' ? inc : 1;
    }
};

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

1『方法模式调用，用 . 来调用；函数模式调用用 function(); 来调用（比如上面例子里的 help(); ）。』

#### 3. The Constructor Invocation Pattern

JavaScript is a prototypal inheritance language. That means that objects can inherit properties directly from other objects. The language is class-free. This is a radical departure from the current fashion. Most languages today are classical. Prototypal inheritance is powerfully expressive, but is not widely understood.

JavaScript itself is not confident in its prototypal nature, so it offers an object-making syntax that is reminiscent of the classical languages. Few classical programmers found prototypal inheritance to be acceptable, and classically inspired syntax obscures the language’s true prototypal nature. It is the worst of both worlds.

If a function is invoked with the new prefix, then a new object will be created with a hidden link to the value of the function’s prototype member, and this will be bound to that new object. The new prefix also changes the behavior of the return statement. We will see more about that next.

如果在一个函数前面带上 new 来调用，那么背地里将会创建一个连接到该函数的 prototype 成员的新对象，同时 this 会被绑定到那个新对象上。new 也会改变 return 语句的行为。

1『小程序里 let DBdata = new DBdevice(); 新对象 DBdata 被创建的时候有一个隐藏的连接，这个连接连到 DBdevice 的原型对象，即通过提取字符可以方法到原型对象里的方法，比如 DBdata.gettypedata()，同时在创建的时候，this 值是绑定到 DBdata 对象上的。』

```js
// Create a constructor function called Quo.
// It makes an object with a status property.
var Quo = function (string) {
    this.status = string;
};

// Give all instances of Quo a public method
// called get_status.
Quo.prototype.get_status = function ( ) {
    return this.status;
};

// Make an instance of Quo.
var myQuo = new Quo("confused");
document.writeln(myQuo.get_status( )); // confused
```

Functions that are intended to be used with the new prefix are called constructors. By convention, they are kept in variables with a capitalized name. If a constructor is called without the new prefix, very bad things can happen without a compile-time or runtime warning, so the capitalization convention is really important. Use of this style of constructor functions is not recommended. We will see better alternatives in the next chapter.

作为构造器的函数名约定首个字母大写，这样看到大写的就知道是构造器，不会漏掉 new 来构建新对象，如果漏掉的话会造成很严重的后果；不建议使用上面形式的构造器函数。

1『上面形式创建的对象没有私有属性，后面的章节是利用闭包特性来实现私有属性的。』

#### 4. The Apply Invocation Pattern

Because JavaScript is a functional object-oriented language, functions can have methods. The apply method lets us construct an array of arguments to use to invoke a function. It also lets us choose the value of this. The apply method takes two parameters. The first is the value that should be bound to this. The second is an array of parameters.

```js
// Make an array of 2 numbers and add them.
var array = [3, 4];
var sum = add.apply(null, array); // sum is 7

// Make an object with a status member.
var statusObject = {
    status: 'A-OK'
};

Quo.prototype.get_status = function ( ) {
    return this.status;
};

// statusObject does not inherit from Quo.prototype,
// but we can invoke the get_status method on
// statusObject even though statusObject does not have
// a get_status method.
var status = Quo.prototype.get_status.apply(statusObject);
// status is 'A-OK'
```

1『 Quo.prototype.get_status.apply(statusObject); 是指定 this 绑定到 apply() 调用时传递的参数，在这里即 statusObject，所以 get_status 函数里的 this.statu 即 statusObject 对象里的 status 属性值。』

### 04. Arguments

A bonus parameter that is available to functions when they are invoked is the arguments array. It gives the function access to all of the arguments that were supplied with the invocation, including excess arguments that were not assigned to parameters. This makes it possible to write functions that take an unspecified number of parameters:

当函数被调用时，会得到一个「免费」配送的参数，那就是 arguments 数组。函数可以通过此参数访问所有它被调用时传递给它的参数列表，包括那些没有被分配给函数声明时定义的形式参数的多余参数。这使得编写一个无须指定参数个数的函数成为可能。

1『印证了之前说的，函数在调用的时候额外接收 2 个参数，this 和 parameters。In addition to the declared parameters, every function receives two additional parameters: this and arguments. 印象中后面有说到，arguments 数组可以是一个键值对象（待确认）。』

```js
// Make a function that adds a lot of stuff.
// Note that defining the variable sum inside of
// the function does not interfere with the sum
// defined outside of the function. The function only sees the inner one.

var sum = function ( ) {
    var i, sum = 0;
    for (i = 0; i < arguments.length; i += 1) {
        sum += arguments[i];
    }
    return sum;
};
document.writeln(sum(4, 8, 15, 16, 23, 42)); // 108
```

This is not a particularly useful pattern. In Chapter 6, we will see how we can add a similar method to an array. Because of a design error, arguments is not really an array. It is an array-like object. arguments has a length property, but it lacks all of the array methods. We will see a consequence of that design error at the end of this chapter.

1『上面默认参数（parameters）的用法很赞。』

### 05. Return

When a function is invoked, it begins execution with the first statement, and ends when it hits the } that closes the function body. That causes the function to return control to the part of the program that invoked the function.

The return statement can be used to cause the function to return early. When return is executed, the function returns immediately without executing the remaining statements. A function always returns a value. If the return value is not specified, then undefined is returned. If the function was invoked with the new prefix and the return value is not an object, then this (the new object) is returned instead.

如果函数调用时在前面加上了 new 前缀，且返回值不是一个对象，则返回 this（该新对象）。

### 06. Exceptions

JavaScript provides an exception handling mechanism. Exceptions are unusual (but not completely unexpected) mishaps that interfere with the normal flow of a program. When such a mishap is detected, your program should throw an exception: 

```js
var add = function (a, b) {
    if (typeof a !== 'number' || typeof b !== 'number') {
    throw {
        name: 'TypeError',
        message: 'add needs numbers'
    };
    }
    return a + b;
}
```

The throw statement interrupts execution of the function. It should be given an exception object containing a name property that identifies the type of the exception, and a descriptive message property. You can also add other properties.

The exception object will be delivered to the catch clause of a try statement:

```js
// Make a try_it function that calls the new add
// function incorrectly.
var try_it = function ( ) {
    try {
        add("seven");
    } catch (e) {
    document.writeln(e.name + ': ' + e.message);
    }
}
try_it( );
```

If an exception is thrown within a try block, control will go to its catch clause. A try statement has a single catch block that will catch all exceptions. If your handling depends on the type of the exception, then the exception handler will have to inspect the name to determine the type of the exception.

1『如果在 try 代码块内抛出了一个异常，控制权就会跳转到它的 catch 从句。』

### 07. Augmenting Types

JavaScript allows the basic types of the language to be augmented. In Chapter 3, we saw that adding a method to Object.prototype makes that method available to all objects. This also works for functions, arrays, strings, numbers, regular expressions, and booleans. For example, by augmenting Function.prototype, we can make a method available to all functions:

```js
Function.prototype.method = function (name, func) {
    this.prototype[name] = func;
    return this;
};
```

By augmenting Function.prototype with a method method, we no longer have to type the name of the prototype property. That bit of ugliness can now be hidden. JavaScript does not have a separate integer type, so it is sometimes necessary to extract just the integer part of a number. The method JavaScript provides to do that is ugly. We can fix it by adding an integer method to Number.prototype. It uses either Math.ceiling or Math.floor, depending on the sign of the number: 

```js
Number.method('integer', function ( ) {
    return Math[this < 0 ? 'ceiling' : 'floor'](this);
});

document.writeln((-10 / 3).integer( )); // -3
```

JavaScript lacks a method that removes spaces from the ends of a string. That is an easy oversight to fix:

```js
String.method('trim', function ( ) {
    return this.replace(/^\s+|\s+$/g, '');
});

document.writeln('"' + " neat ".trim( ) + '"'); 
```

Our trim method uses a regular expression. We will see much more about regular expressions in Chapter 7. By augmenting the basic types, we can make significant improvements to the expressiveness of the language. Because of the dynamic nature of JavaScript’s prototypal inheritance, all values are immediately endowed with the new methods, even values that were created before the methods were created.

1『扩充类型体现了 JS 动态特性。上面的 2 个例子需要反复研究。』

The prototypes of the basic types are public structures, so care must be taken when mixing libraries. One defensive technique is to add a method only if the method is known to be missing:

基本类型的原型是公用结构，所以在类库混用时务必小心。一个保险的做法就是只在确定没有该方法时才添加它。

```js
// Add a method conditionally.
Function.prototype.method = function (name, func) {
    if (!this.prototype[name]) {
        this.prototype[name] = func;
    }
};
```

Another concern is that the for in statement interacts badly with prototypes. We saw a couple of ways to mitigate that in Chapter 3: we can use the hasOwnProperty method to screen out inherited properties, and we can look for specific types.

### 08. Recursion

A recursive function is a function that calls itself, either directly or indirectly. Recursion is a powerful programming technique in which a problem is divided into a set of similar subproblems, each solved with a trivial solution. Generally, a recursive function calls itself to solve its subproblems.

1『 Recursion 体现了解决问题时采用分解的思维模式。』

The Towers of Hanoi is a famous puzzle. The equipment includes three posts and a set of discs of various diameters with holes in their centers. The setup stacks all of the discs on the source post with smaller discs on top of larger discs. The goal is to move the stack to the destination post by moving one disc at a time to another post, never placing a larger disc on a smaller disc. This puzzle has a trivial recursive solution: 

```js
var hanoi = function (disc, src, aux, dst) {
    if (disc > 0) {
        hanoi(disc - 1, src, dst, aux);
        document.writeln('Move disc ' + disc + ' from ' + src + ' to ' + dst);
        hanoi(disc - 1, aux, src, dst);
    }
};

hanoi(3, 'Src', 'Aux', 'Dst');

It produces this solution for three discs:

Move disc 1 from Src to Dst
Move disc 2 from Src to Aux
Move disc 1 from Dst to Aux
Move disc 3 from Src to Dst
Move disc 1 from Aux to Src
Move disc 2 from Aux to Dst
Move disc 1 from Src to Dst
```

2『汉诺塔的代码反复去看，吃透其递归的实现方式。』

The hanoi function moves a stack of discs from one post to another, using the auxiliary post if necessary. It breaks the problem into three subproblems. First, it uncovers the bottom disc by moving the substack above it to the auxiliary post. It can then move the bottom disc to the destination post. Finally, it can move the substack from the auxiliary post to the destination post. The movement of the substack is handled by calling itself recursively to work out those subproblems.

The hanoi function is passed the number of the disc it is to move and the three posts it is to use. When it calls itself, it is to deal with the disc that is above the disc it is currently working on. Eventually, it will be called with a nonexistent disc number. In that case, it does nothing. That act of nothingness gives us confidence that the function does not recurse forever. Recursive functions can be very effective in manipulating tree structures such as the browser’s Document Object Model (DOM). Each recursive call is given a smaller piece of the tree to work on:

传递给 hanoi 函数的参数包括当前移动的圆盘编号和它将要用到的 3 根柱子。当它调用自身的时候，它去处理当前正在处理的圆盘之上的圆盘。最终，它会以一个不存在的圆盘编号去调用。在这样的情况下，它不执行任何操作。由于该函数对非法值不予理会，我们也就不必担心它会导致死循环。递归函数可以非常高效地操作树形结构，比如浏览器端的文档对象模型（DOM）。每次递归调用时处理指定的树的一小段。

```js
// Define a walk_the_DOM function that visits every
// node of the tree in HTML source order, starting
// from some given node. It invokes a function,
// passing it each node in turn. walk_the_DOM calls
// itself to process each of the child nodes.

var walk_the_DOM = function walk(node, func) {
    func(node);
    node = node.firstChild;
    while (node) {
        walk(node, func);
        node = node.nextSibling;
    }
};

// Define a getElementsByAttribute function. It
// takes an attribute name string and an optional
// matching value. It calls walk_the_DOM, passing it a
// function that looks for an attribute name in the
// node. The matching nodes are accumulated in a
// results array.

var getElementsByAttribute = function (att, value) {
    var results = [];
    walk_the_DOM(document.body, function (node) {
        var actual = node.nodeType === 1 && node.getAttribute(att); 
        if (typeof actual === 'string' && (actual === value || typeof value !== 'string')) {
            results.push(node);
        }
    });
    
    return results;
};
```

Some languages offer the tail recursion optimization. This means that if a function returns the result of invoking itself recursively, then the invocation is replaced with a loop, which can significantly speed things up. Unfortunately, JavaScript does not currently provide tail recursion optimization. Functions that recurse very deeply can fail by exhausting the return stack:

一些语言提供了「尾递归」优化。这意味着如果一个函数返回自身递归调用的结果，那么调用的过程会被替换为一个循环，它可以显著提高速度。遗憾的是，Javascript 当前并没有提供尾递归优化。深度递归的函数可能会因为堆栈溢出而运行失败。尾递归（tail recursion 或 tail-end recursion）是一种在函数的最后执行递归调用语句的特殊形式的递归。

```js
// Make a factorial function with tail
// recursion. It is tail recursive because
// it returns the result of calling itself.
// JavaScript does not currently optimize this form.

var factorial = function factorial(i, a) {
    a = a || 1;
    if (i < 2) {
        return a;
    }
    return factorial(i - 1, a * i);
};

document.writeln(factorial(4)); // 24
```

### 09. Scope

Scope in a programming language controls the visibility and lifetimes of variables and parameters. This is an important service to the programmer because it reduces naming collisions and provides automatic memory management: 

```js
var foo = function ( ) {
    var a = 3, b = 5;
    var bar = function ( ) {
        var b = 7, c = 11;
        // At this point, a is 3, b is 7, and c is 11
        a += b + c;
        // At this point, a is 21, b is 7, and c is 11
    };
    // At this point, a is 3, b is 5, and c is not defined 
    bar( );
    // At this point, a is 21, b is 5
};
```

1『 JS 里函数就是一种对象，既然是对象那么所有针对对象的操作都可以针对函数，比如当作一个参数、比如赋值给一个变量等等。而函数的声明有两大类，一是常规的函数式，一是函数表达式（就把整个函数当作一个表达式，可以用 () 把整个函数包起来）。』

Most languages with C syntax have block scope. All variables defined in a block (a list of statements wrapped with curly braces) are not visible from outside of the block. The variables defined in a block can be released when execution of the block is finished. This is a good thing.

Unfortunately, JavaScript does not have block scope even though its block syntax suggests that it does. This confusion can be a source of errors. JavaScript does have function scope. That means that the parameters and variables defined in a function are not visible outside of the function, and that a variable defined anywhere within a function is visible everywhere within the function.

1『ES6 新增的 let 和 const 拥有块级作用域；理解 JS 的函数作用域很重要。』

In many modern languages, it is recommended that variables be declared as late as possible, at the first point of use. That turns out to be bad advice for JavaScript because it lacks block scope. So instead, it is best to declare all of the variables used in a function at the top of the function body.

糟糕的是，尽管 Javascript 的代码块语法貌似支持块级作用域，但实际上 Javascript 并不支持。这个混淆之处可能成为错误之源。Javascript 确实有函数作用域。那意味着定义在函数中的参数和变量在函数外部是不可见的，而在一个函数内部任何位置定义的变量，在该函数内部任何地方都可见。很多现代语言都推荐尽可能延迟声明变量。而用在 Javascript 上的话却会成为槽糕的建议，因为它缺少块级作用域。所以，最好的做法是在函数体的顶部声明函数中可能用到的所有变量。

### 10. Closure

The good news about scope is that inner functions get access to the parameters and variables of the functions they are defined within (with the exception of this and arguments). This is a very good thing. Our getElementsByAttribute function worked because it declared a results variable, and the inner function that it passed to walk\_the\_DOM also had access to the results variable.

A more interesting case is when the inner function has a longer lifetime than its outer function. Earlier, we made a myObject that had a value and an increment method. Suppose we wanted to protect the value from unauthorized changes.

Instead of initializing myObject with an object literal, we will initialize myObject by calling a function that returns an object literal. That function defines a value variable. That variable is always available to the increment and getValue methods, but the function’s scope keeps it hidden from the rest of the program: 

我们的 getelementsbyattribute 函数可以工作，是因为它声明了一个 results 变量，而传递给 walk\_the_DOM 的内部函数也可以访问 results 变量。一个更有趣的情形是内部函数拥有比它的外部函数更长的生命周期。之前，我们构造了一个 myObject 对象，它拥有一个 value 属性和一个 increment 方法。假定我们希望保护该值不会被非法更改。和以对象字面量形式去初始化 myObject 不同，我们通过调用一个函数的形式去初始化 myObject，该函数会返回一个对象字面量。函数里定义了一个 value 变量。该变量对 increment 和 getValue 方法总是可用的，但函数的作用域使得它对其他的程序来说是不可见的。

```js
var myObject = function ( ) {
    var value = 0;
    return {
        increment: function (inc) {
        value += typeof inc === 'number' ? inc : 1;
        },
        getValue: function ( ) {
            return value;
        }
    };
}( );
```

We are not assigning a function to myObject. We are assigning the result of invoking that function. Notice the ( ) on the last line. The function returns an object containing two methods, and those methods continue to enjoy the privilege of access to the value variable.

我们并没有把一个函数赋值给 myObject。我们是把调用该函数后返回的结果赋值给它。注意最后一行的（）。该函数返回一个包含两个方法的对象，并且这些方法继续享有访问 value 变量的特权。

1『绝妙的操作，这样可以把 value 值保护起来，不让外界直接可以修改这个值。关键点是函数后面的 ()，是把调用该函数后返回的结果赋值给这个变量，该函数返回的是一个对象，对象里包含 2 个方法，这两个方法都可以访问该函数体内定义的变量。这就理解了「通过调用一个函数的形式去初始化 myObject，该函数会返回一个对象字面量。」』

The Quo constructor from earlier in this chapter produced an object with a status property and a get_status method. But that doesn’t seem very interesting. Why would you call a getter method on a property you could access directly? It would be more useful if the status property were private. So, let’s define a different kind of quo function to do that:

本章之前的 Quo 构造器产生一个带有 status 属性和 get status 方法的对象。为什么要用一个 getter 方法去访问你本可以直接访问到的属性呢？如果 status 是私有属性，它才是更有意义的。所以，让我们定义另一种形式的 quo 函数来做此事：

1『这其实就是 JS 里实现私有属性的绝妙方式。』

```js
// Create a maker function called quo. It makes an
// object with a get_status method and a private status property.

var quo = function (status) {
    return {
        get_status: function ( ) {
            return status;
        }
    };
};

// Make an instance of quo.

var myQuo = quo("amazed");
document.writeln(myQuo.get_status( ));
```

This quo function is designed to be used without the new prefix, so the name is not capitalized. When we call quo, it returns a new object containing a get\_status method. A reference to that object is stored in myQuo. The get\_status method still has privileged access to quo’s status property even though quo has already returned.

get\_status does not have access to a copy of the parameter; it has access to the parameter itself. This is possible because the function has access to the context in which it was created. This is called closure.

当我们调用 quo 时，它返回包含 get\_status 方法的一个新对象。该对象的一个引用保存在 myQuo 中。即使 quo 已经返回了，但 get\_status 方法仍然享有访问 quo 对象的 status 属性的特权。get\_status 方法并不是访问该参数的一个副本，它访问的就是该参数本身。因为该函数可以访问它被创建时所处的上下文环境。这被称为闭包。

1『闭包的本质来了：该函数可以访问它被创建时所处的上下文环境，即为闭包。』

Let’s look at a more useful example:

```js
// Define a function that sets a DOM node's color
// to yellow and then fades it to white.

var fade = function (node) {
    var level = 1;
    var step = function ( ) {
        var hex = level.toString(16);
        node.style.backgroundColor = '#FFFF' + hex + hex;
        if (level < 15) {
            level += 1;
            setTimeout(step, 100);
        }
    };
    setTimeout(step, 100);
};

fade(document.body);
```

We call fade, passing it document.body (the node created by the HTML \<body> tag). fade sets level to 1. It defines a step function. It calls setTimeout, passing it the step function and a time (100 milliseconds). It then returns—fade has finished.

Suddenly, about a 10th of a second later, the step function gets invoked. It makes a base 16 character from fade’s level. It then modifies the background color of fade’s node. It then looks at fade’s level. If it hasn’t gotten to white yet, it then increments fade’s level and uses setTimeout to schedule itself to run again.

Suddenly, the step function gets invoked again. But this time, fade’s level is 2. fade returned a while ago, but its variables continue to live as long as they are needed by one or more of fade’s inner functions.

It is important to understand that the inner function has access to the actual variables of the outer functions and not copies in order to avoid the following problem:

fade 函数设置 level 为 1。它定义了一个 step 函数；接着调用 settimeout，并传递 step 函数和一个时间（100 毫秒）给它。然后它返回，fade 函数结東。在大约十分之一秒后，step 函数被调用。它把 fade 函数的 1evel 变量转化为 16 位字符。接着，它修改 fade 函数得到的节点的背景颜色。然后査看 fade 函数的 level 变量。如果背景色尚未变成白色，那么它增大 fade 函数的 level 变量，接着用 settimeout 预定让它自己再次运行。step 函数很快再次被调用。但这次，fade 函数的 level 变量值变成 2。fade 函数在之前已经返回了，但只要 fade 的内部函数需要，它的变量就会持续保留。为了避免下面的问题，理解内部函数能访问外部函数的实际变量而无须复制是很重要的。

```js
// BAD EXAMPLE
// Make a function that assigns event handler functions to an array of nodes the wrong way.
// When you click on a node, an alert box is supposed to display the ordinal of the node.
// But it always displays the number of nodes instead.

var add_the_handlers = function (nodes) {
    var i;
    for (i = 0; i < nodes.length; i += 1) {
        nodes[i].onclick = function (e) {
            alert(i);
        };
    }
};

// END BAD EXAMPLE
```

The add\_the_handlers function was intended to give each handler a unique number (i). It fails because the handler functions are bound to the variable i, not the value of the variable i at the time the function was made:

add\_the_handlers 函数的本意是想传递给每个事件处理器一个唯一值（i）。但它未能达到目的，因为事件处理器函数绑定了变量 i 本身，而不是函数在构造时的变量的值。

```js
// BETTER EXAMPLE
// Make a function that assigns event handler functions to an array of nodes the right way.
// When you click on a node, an alert box will display the ordinal of the node.

var add_the_handlers = function (nodes) {
    var i;
    for (i = 0; i < nodes.length; i += 1) {
        nodes[i].onclick = function (i) {
            return function (e) {
                alert(e);
            };
        }(i);
    }
};
```

Now, instead of assigning a function to onclick, we define a function and immediately invoke it, passing in i. That function will return an event handler function that is bound to the value of i that was passed in, not to the i defined in add\_the_handlers. That returned function is assigned to onclick.

避免在循环中创建函数，它可能只会带来无谓的计算，还会引起混淆，正如上面那个糟糕的例子。我们可以先在循环之外创建一个辅助函数，让这个辅助函数再返回一个绑定了当前立值的函数，这样就不会导致混淆了。

1『这里的知识点感觉很重要，目前还没弄明白。（2020-03-29）』

### 11. Callbacks

Functions can make it easier to deal with discontinuous events. For example, suppose there is a sequence that begins with a user interaction, making a request of the server, and finally displaying the server’s response. The native way to write that would be:

```js
request = prepare_the_request( );
response = send_request_synchronously(request);
display(response);
```

The problem with this approach is that a synchronous request over the network will leave the client in a frozen state. If either the network or the server is slow, the degradation in responsiveness will be unacceptable. A better approach is to make an asynchronous request, providing a callback function that will be invoked when the server’s response is received. An asynchronous function returns immediately, so the client isn’t blocked: 

```js
request = prepare_the_request( );
send_request_asynchronously(request, function (response) {
    display(response);
});
```

We pass a function parameter to the send\_request_asynchronously function that will be called when the response is available.

函数使得对不连续事件的处理变得更容易。例如，假定有这么一个序列，由用户交互行为触发，向服务器发送请求，最终显示服务器的响应。最自然的写法可能会是这样的；这种方式的问题在于，网络上的同步请求会导致客户端进入假死状态。如果网络传输或服务器很慢，响应会慢到让人不可接受。更好的方式是发起异步请求，提供一个当服务器的响应到达时随即触发的回调函数。异步函数立即返回，这样客户端就不会被阻塞。

1『回调函数目前的理解，把这个任务悬挂起来，做个标记，先干其他的事，等那边回复后再继续这个任务。』

### 12. Module

We can use functions and closure to make modules. A module is a function or object that presents an interface but that hides its state and implementation. By using functions to produce modules, we can almost completely eliminate our use of global variables, thereby mitigating one of JavaScript’s worst features.

For example, suppose we want to augment String with a deentityify method. Its job is to look for HTML entities in a string and replace them with their equivalents. It makes sense to keep the names of the entities and their equivalents in an object.

But where should we keep the object? We could put it in a global variable, but global variables are evil. We could define it in the function itself, but that has a runtime cost because the literal must be evaluated every time the function is invoked. The ideal approach is to put it in a closure, and perhaps provide an extra method that can add additional entities:

可以把它定义在该函数的内部，但是那会带来运行时的损耗，因为每次执行该函数的时候该字面量都会被求值一次。理想的方式是把它放入一个闭包，而且也许还能提供一个增加更多字符实体的扩展方法。

1『这又是闭包的一个应用场景。』

```js
String.method('deentityify', function ( ) {

    // The entity table. It maps entity names to characters.
    
    var entity = {
        quot: '"',
        lt: '<',
        gt: '>'
    };
    
    // Return the deentityify method.
    return function ( ) {
        // This is the deentityify method. It calls the string
        // replace method, looking for substrings that start
        // with '&' and end with ';'. If the characters in
        // between are in the entity table, then replace the
        // entity with the character from the table. It uses
        // a regular expression (Chapter 7).
        
        return this.replace(/&([^&;]+);/g,
            function (a, b) {
                var r = entity[b];
                return typeof r === 'string' ? r : a;
            }
        );
    };
}( );
```

Notice the last line. We immediately invoke the function we just made with the ( ) operator. That invocation creates and returns the function that becomes the deentityify method.

```js
document.writeln(
    '&lt;&quot;&gt;'.deentityify( )); // <"> 
```

The module pattern takes advantage of function scope and closure to create relationships that are binding and private. In this example, only the deentityify method has access to the entity data structure.

The general pattern of a module is a function that defines private variables and functions; creates privileged functions which, through closure, will have access to the private variables and functions; and that returns the privileged functions or stores them in an accessible place.

Use of the module pattern can eliminate the use of global variables. It promotes information hiding and other good design practices. It is very effective in encapsulat-ing applications and other singletons.

模块模式利用了函数作用域和闭包来创建被绑定对象与私有成员的关联，在这个例子中，只有 deentityify 方法有权访问字符实体表这个数据对象。模块模式的一般形式是：一个定义了私有变量和函数的函数；利用闭包创建可以访问私有变量和函数的特权函数；最后返回这个特权函数，或者把它们保存到一个可访问到的地方。使用模块模式就可以摒弃全局变量的使用。它促进了信息隐藏和其他优秀的设计实践。对于应用程序的封装，或者构造其他单例对象，模块模式非常有效。

3『模块模式通常结合单例模式（Singleton Pattern）使用。Javascript 的单例就是用对象字面量表示法创建的对象，对象的属性值可以是数值或函数，并且属性值在该对象的生命周期中不会发生变化。它通常作为工具为程序其他部分提供功能支持。』

It can also be used to produce objects that are secure. Let’s suppose we want to make an object that produces a serial number:

```js
var serial_maker = function ( ) {

    // Produce an object that produces unique strings. A
    // unique string is made up of two parts: a prefix
    // and a sequence number. The object comes with
    // methods for setting the prefix and sequence
    // number, and a gensym method that produces unique
    // strings.
    
    var prefix = '';
    var seq = 0;
    return {
        set_prefix: function (p) {
            prefix = String(p);
        },
        set_seq: function (s) {
            seq = s;
        },
        
        gensym: function ( ) {
            var result = prefix + seq;
            seq += 1;
            return result;
        }
    };
};

var seqer = serial_maker( );
seqer.set_prefix = ('Q';)
seqer.set_seq = (1000);
var unique = seqer.gensym( ); // unique is "Q1000"
```

The methods do not make use of this or that. As a result, there is no way to compromise the seqer. It isn’t possible to get or change the prefix or seq except as permitted by the methods. The seqer object is mutable, so the methods could be replaced, but that still does not give access to its secrets. seqer is simply a collection of functions, and those functions are capabilities that grant specific powers to use or modify the secret state.

If we passed seqer.gensym to a third party’s function, that function would be able to generate unique strings, but would be unable to change the prefix or seq.

Seder 包含的方法都没有用到 this 或 that，因此没有办法损害 seder。除非调用对应的方法，否则没法改变 prefix 或 seq 的值。seer 对象是可变的，所以它的方法可能会被替换掉，但替换后的方法依然不能访问私有成员。seder 就是一组函数的集合，而且那些函数被授予特权，拥有使用或修改私有状态的能力。如果我们把 seqer.gensym 作为一个值传递给第三方函数，那个函数能用它产生唯一字符串，但却不能通过它来改变 prefix 或 seq 的值。

### 13. Cascade

Some methods do not have a return value. For example, it is typical for methods that set or change the state of an object to return nothing. If we have those methods return this instead of undefined, we can enable cascades. In a cascade, we can call many methods on the same object in sequence in a single statement. An Ajax library that enables cascades would allow us to write in a style like this: 

如果我们让这些方法返回 this 而不是 undefined，就可以启用级联。在一个级联中，我们可以在单独一条语句中依次调用同一个对象的很多方法。一个启用级联的 Ajax 类库可能允许我们以这样的形式去编码。

```js
getElement('myBoxDiv').
    move(350, 150).
    width(100).
    height(100).
    color('red').
    border('10px outset'). padding('4px'). appendText("Please stand by").
    on('mousedown', function (m) { 
        this.startDrag(m, this.getNinth(m)); 
    }).
    on('mousemove', 'drag').
    on('mouseup', 'stopDrag').
    later(2000, function ( ) {
        this.
            color('yellow').
            setHTML("What hath God wraught?").
            slide(400, 40, 200, 200);
        }).
    tip('This box is resizeable');
```

In this example, the getElement function produces an object that gives functionality to the DOM element with id="myBoxDiv". The methods allow us to move the element, change its dimensions and styling, and add behavior. Each of those methods returns the object, so the result of the invocation can be used for the next invocation. Cascading can produce interfaces that are very expressive. It can help control the tendency to make interfaces that try to do too much at once.

级联技术可以产生出极富表现力的接口。它也能给那波构造「全能」接口的热潮降降温，一个接口没必要一次做太多事情。

### 14. Curry

Functions are values, and we can manipulate function values in interesting ways. Currying allows us to produce a new function by combining a function and an argument:

函数也是值，从而我们可以用有趣的方式去操作函数值。柯里化允许我们把函数与传递给它的参数相结合，产生出一个新的函数。

```js
var add1 = add.curry(1);
document.writeln(add1(6)); // 7
```

add1 is a function that was created by passing 1 to add’s curry method. The add1 function adds 1 to its argument. JavaScript does not have a curry method, but we can fix that by augmenting Function.prototype:

```js
Function.method('curry', function ( ) {
    var args = arguments, that = this;
    return function ( ) {
        return that.apply(null, args.concat(arguments));
    };
}); // Something isn't right...
```

The curry method works by creating a closure that holds that original function and the arguments to curry. It returns a function that, when invoked, returns the result of calling that original function, passing it all of the arguments from the invocation of curry and the current invocation. It uses the Array concat method to concatenate the two arrays of arguments together.

Unfortunately, as we saw earlier, the arguments array is not an array, so it does not have the concat method. To work around that, we will apply the array slice method on both of the arguments arrays. This produces arrays that behave correctly with the concat method:

Curry 方法通过创建一个保存着原始函数和要被套用的参数的闭包来工作。它返回另一个函数，该函数被调用时，会返回调用原始函数的结果，并传递调用 curry 时的参数加上当前调用的参数。它使用 Array 的 concat 方法连接两个参数数组。糟糕的是，就像我们先前看到的那样，arguments 数组并非一个真正的数组，所以它并没有 concat 方法。要避开这个向题，我们必须在两个 arguments 数组上都应用数组的 slice 方法。这样产生出拥有 concat 方法的常规数组。

```js
Function.method('curry', function ( ) {
    var slice = Array.prototype.slice,
    args = slice.apply(arguments),
    that = this;
    return function ( ) {
        return that.apply(null, args.concat(slice.apply(arguments)));
    };
});
```

3『柯里化，也常译为「局部套用」，是把多参数函数转换为一系列单参数函数并进行调用的技术。这项技术以数学家 Haskell Curry 的名字命名。』

### 15. Memoization

Functions can use objects to remember the results of previous operations, making it possible to avoid unnecessary work. This optimization is called memoization. JavaScript’s objects and arrays are very convenient for this. Let’s say we want a recursive function to compute Fibonacci numbers. A Fibonacci number is the sum of the two previous Fibonacci numbers. The first two are 0 and 1: 

```js
var fibonacci = function (n) {
    return n < 2 ? n : fibonacci(n - 1) + fibonacci(n - 2);
};
for (var i = 0; i <= 10; i += 1) {
    document.writeln('// ' + i + ': ' + fibonacci(i));
}

// 0: 0
// 1: 1
// 2: 1
// 3: 2
// 4: 3
// 5: 5
// 6: 8
// 7: 13
// 8: 21
// 9: 34
// 10: 55
```

This works, but it is doing a lot of unnecessary work. The fibonacci function is called 453 times. We call it 11 times, and it calls itself 442 times in computing values that were probably already recently computed. If we memoize the function, we can significantly reduce its workload. We will keep our memoized results in a memo array that we can hide in a closure. When our function is called, it first looks to see if it already knows the result. If it does, it can immediately return it:

我们在一个名为 memo 的数组里保存我们的存储结果，存储结果可以隐藏在闭包中。当函数被调用时，这个函数首先检査结果是否已存在，如果已经存在，就立即返回这个结果。

```js
var fibonacci = function ( ) {
    var memo = [0, 1];
    var fib = function (n) {
        var result = memo[n];
        if (typeof result !== 'number') {
            result = fib(n - 1) + fib(n - 2); memo[n] = result;
        }
        return result;
        };
    return fib;
}( );
```

This function returns the same results, but it is called only 29 times. We called it 11 times. It called itself 18 times to obtain the previously memoized results. We can generalize this by making a function that helps us make memoized functions. The memoizer function will take an initial memo array and the fundamental function. It returns a shell function that manages the memo store and that calls the fundamental function as needed. We pass the shell function and the function’s parameters to the fundamental function:

```js
var memoizer = function (memo, fundamental) {
    var shell = function (n) {
        var result = memo[n];
        if (typeof result !== 'number') {
            result = fundamental(shell, n);
            memo[n] = result;
        }
        return result;
    };
    return shell;
};
```

We can now define fibonacci with the memoizer, providing the initial memo array and fundamental function:

```js
var fibonacci = memoizer([0, 1], function (shell, n) {
    return shell(n - 1) + shell(n - 2);
});
```

By devising functions that produce other functions, we can significantly reduce the amount of work we have to do. For example, to produce a memoizing factorial function, we only need to supply the basic factorial formula: 

```js
var factorial = memoizer([1, 1], function (shell, n) {
    return n * shell(n - 1);
});
```

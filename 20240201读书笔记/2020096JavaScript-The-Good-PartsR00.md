## 记忆时间

2020-04-21；2020-08-27

英文版出版时间是 2008 年。

## 卡片

### 0101. 主题卡 —— JS 的精华

JavaScript is built on some very good ideas and a few very bad ones. The very good ideas include functions, loose typing, dynamic objects, and an expressive object literal notation.

JavaScript’s functions are first class objects with (mostly) lexical scoping. JavaScript is the first lambda language to go mainstream. Deep down, JavaScript has more in common with Lisp and Scheme than with Java. It is Lisp in C’s clothing. This makes JavaScript a remarkably powerful language.

But it turns out that strong typing does not eliminate the need for careful testing. And I have found in my work that the sorts of errors that strong type checking finds are not the errors I worry about. On the other hand, I find loose typing to be liberating. I don’t need to form complex class hierarchies. And I never have to cast or wrestle with the type system to get the behavior that I want.

JavaScript has a very powerful object literal notation. Objects can be created simply by listing their components. This notation was the inspiration for JSON, the popular data interchange format.

A controversial feature in JavaScript is prototypal inheritance. JavaScript has a class-free object system in which objects inherit properties directly from other objects. This is really powerful, but it is unfamiliar to classically trained programmers. If you attempt to apply classical design patterns directly to JavaScript, you will be frustrated. But if you learn to work with JavaScript’s prototypal nature, your efforts will be rewarded.

1 Simplified JavaScript is just the good stuff, including: Functions as first class objects. Functions in Simplified JavaScript are lambdas with lexical scoping. 

2 Dynamic objects with prototypal inheritance Objects are class-free. We can add a new member to any object by ordinary assignment. An object can inherit members from another object. 

3 Object literals and array literals. This is a very convenient notation for creating new objects and arrays. JavaScript literals were the inspiration for the JSON data interchange format.

### 0102. 主题卡 —— 正则表达式的知识体系

正则的功能在于字符串的搜索匹配、替换、提取信息。正则的知识框架：结构与元素。

实战细节汇总：

1、首部加 `^` 表示是字符串的起始，强制从开头匹配。尾部加 `$` 表示字符串的末端，强制收尾。这两个符号如同锚点，`/^expression$/` 相当于将范围圈定好。

摘录原文：We again use `^` and `$` to anchor the regular expression. This causes all of the characters in the text to be matched against the regular expression. If we had omitted the anchors, the regular expression would tell us if a string contains a number. With the anchors, it tells us if the string contains only a number. If we included just the `^`, it would match strings starting with a number. If we included just the `$`, it would match strings ending with a number.

2、首部加 `?:` 表示非捕获型分组，即匹配的对象不会供后续使用。像这种以 `? `开头的是一种扩展表示法。

摘录原文：The `(?:...)? `indicates an optional noncapturing group. It is usually better to use noncapturing groups instead of the less ugly capturing groups because capturing has a performance penalty. 

3、末尾加 `?` 表示匹配 0 次或 1 次，即可选项；末尾加 `+` 表示匹配 1 次或多次；`*` 表示匹配 0 次或多次；`{0,3}` 表示匹配 0、1、2、3 次均可。

4、`()` 里的表示是捕获组，匹配的信息会存入一个结果数据组，比如 PHP 里的结果数据默认为 `$matches`。另，捕获组后面跟着冒号 `:` 的话，表示会按字面量进行匹配。

5、`[]` 里的表示是字符集（character class），比如 `[A-Za-z]` 表示所有的大小写字母；字符集内，首部加 `^` 的话表示反选，比如 `[^?#]` 表示匹配除了 ? 和 # 的所有字符。

6、点号 `.` 表示匹配任意字符，除了 line-ending 字符（换行符）外。

7、整个表达式后面加标识符 `i` 表示忽略大小写，比如 `/expression/i`。另外 2 个标识符是 g 和 m。

摘录原文：g, Global (match multiple times; the precise meaning of this varies with the method). i, Insensitive (ignore character case). m, Multiline (^ and \$ can match line-ending characters).

结构内容汇总：

1、JS 里的正则有 2 个实现方式，一是字面量，如下面所示；二是通过正则构造器。

```js
// Make a regular expression object that matches
// a JavaScript string.
var my_regexp = /"(?:\\.|[^\\\"])*"/g;

// Make a regular expression object that matches
// a JavaScript string.

var my_regexp = new RegExp("\"(?:\\.|[^\\\\\\\"])*\"", 'g'); 
```

摘录原文：The second parameter is a string specifying the flags. The RegExp constructor is useful when a regular expression must be generated at runtime using material that is not available to the programmer. RegExp objects contain the properties listed in Table 7-2.

2、一个个 `()` 包裹起来的捕获组，也被称为因子（factor）。

元素内容汇总：

1、Regexp Choice. A regexp choice contains one or more regexp sequences. The sequences are separated by the | (vertical bar) character. The choice matches if any of the sequences match. It attempts to match each of the sequences in order. So:

    "into".match(/in|int/)

matches the in in into. It wouldn’t match int because the match of in was successful.

2、Regexp Sequence. A regexp sequence contains one or more regexp factors. Each factor can optionally be followed by a quantifier that determines how many times the factor is allowed to appear. If there is no quantifier, then the factor will be matched one time.

3、Regexp Factor. A regexp factor can be a character, a parenthesized group, a character class, or an escape sequence. All characters are treated literally except for the control characters and the special characters:

```
\ / [ ] ( ) { } ? + * | . ^ $
```

which must be escaped with a \ prefix if they are to be matched literally. When in doubt, any special character can be given a \ prefix to make it literal. The \ prefix does not make letters or digits literal. An unescaped . matches any character except a line-ending character. An unescaped ^ matches the beginning of the text when the lastIndex property is zero. It can also match line-ending characters when the m flag is specified. An unescaped \$ matches the end of the text. It can also match line-ending characters when the m flag is specified.

4、Regexp Escape. The backslash character indicates escapement in regexp factors as well as in strings, but in regexp factors, it works a little differently.

As in strings, \f is the formfeed character, \n is the newline character, \r is the carriage return character, \t is the tab character, and \u allows for specifying a Unicode character as a 16-bit hex constant. In regexp factors, \b is not the backspace character. \d is the same as [0-9]. It matches a digit. \D is the opposite: [^0-9]. 

\s is the same as [\f\n\r\t\u000B\u0020\u00A0\u2028\u2029]. This is a partial set of Unicode whitespace characters. \S is the opposite: [^\f\n\r\t\u000B\u0020\u00A0\u2028\ u2029].

\w is the same as [0-9A-Z_a-z]. \W is the opposite: [^0-9A-Z_a-z]. This is supposed to represent the characters that appear in words. Unfortunately, the class it defines is useless for working with virtually any real language. If you need to match a class of letters, you must specify your own class.

\b was intended to be a word-boundary anchor that would make it easier to match text on word boundaries. Unfortunately, it uses \w to find word boundaries, so it is completely useless for multilingual applications. This is not a good part.

5、Regexp Group. There are four kinds of groups:

1) Capturing. A capturing group is a regexp choice wrapped in parentheses. The characters that match the group will be captured. Every capture group is given a number. The first capturing ( in the regular expression is group 1. The second capturing ( in the regular expression is group 2.

2) Noncapturing. A noncapturing group has a (?: prefix. A noncapturing group simply matches; it does not capture the matched text. This has the advantage of slight faster performance. Noncapturing groups do not interfere with the numbering of capturing groups.

3) Positive lookahead. A positive lookahead group has a (?= prefix. It is like a noncapturing group except that after the group matches, the text is rewound to where the group started, effectively matching nothing. This is not a good part. 

4) Negative lookahead. A negative lookahead group has a (?! prefix. It is like a positive lookahead group, except that it matches only if it fails to match. This is not a good part.

非捕获型分组有一个 (`?:` 前缀。非捕获型分组仅做简单的匹配，并不会捕获所匹配的文本。这会带来微弱的性能优势。非捕获型分组不会干扰捕获型分组的编号。向前正向匹配分组类似于非捕获型分组，但在这个组匹配后，文本会倒回到它开始的地方，实际上并不匹配任何东西。这不是一个好的特性。向前负向匹配分组类似于向前正向匹配分组，但只有当它匹配失败时它才继续向前进行匹配。这不是一个好的特性。

6、Regexp Class. A regexp class is a convenient way of specifying one of a set of characters. For example, if we wanted to match a vowel, we could write (?:a | e | i | o | u), but it is more conveniently written as the class [aeiou]. Classes provide two other conveniences. The first is that ranges of characters can be specified.

7、Regexp Class Escape. The rules of escapement within a character class are slightly different than those for a regexp factor. [\b] is the backspace character. Here are the special characters that should be escaped in a character class:

```
- / [ \ ] ^
```

8、Regexp Quantifier. A regexp factor may have a regexp quantifier suffix that determines how many times the factor should match. A number wrapped in curly braces means that the factor should match that many times. So, /www/ matches the same as /w{3}/. {3,6} will match 3, 4, 5, or 6 times. {3,} will match 3 or more times. ? is the same as {0,1}. * is the same as {0,}. + is the same as {1,}.

Matching tends to be greedy, matching as many repetitions as possible up to the limit, if there is one. If the quantifier has an extra ? suffix, then matching tends to be lazy, attempting to match as few repetitions as possible. It is usually best to stick with the greedy matching.

如果只有一个量词，表示趋向于进行贪梦性匹配，即匹配尽可能多的副本直至达到上限。如果这个量词附加一个后缀 ?，则表示趋向于进行非贪梦匹配，即只匹配必要的副本就好。一般情况下最好坚持使用贪婪性匹配。

### 0201. 术语卡 —— delegation

The prototype link is used only in retrieval. If we try to retrieve a property value from an object, and if the object lacks the property name, then JavaScript attempts to retrieve the property value from the prototype object. And if that object is lacking the property, then it goes to its prototype, and so on until the process finally bottoms out with Object.prototype. If the desired property exists nowhere in the prototype chain, then the result is the undefined value. This is called delegation.

### 0202. 术语卡 —— this 值

Invoking a function suspends the execution of the current function, passing control and parameters to the new function. In addition to the declared parameters, every function receives two additional parameters: this and arguments. The this parameter is very important in object oriented programming, and its value is determined by the invocation pattern. There are four patterns of invocation in JavaScript: the method invocation pattern, the function invocation pattern, the constructor invocation pattern, and the apply invocation pattern. The patterns differ in how the bonus parameter this is initialized.

this 的值取决于调用模式（invocation pattern）：1）the method invocation pattern，方法式调用，this 绑定到该方法所隶属的对象（函数作为一个对象的某个属性值的时候才被称为方法），这个绑定是在调用时发生的；2）the function invocation pattern，函数式调用，this 绑定到全局变量上（JS 公认的设计错误），这导致内部函数无法通过 this 来访问外部函数的数据，即没法帮外部函数处理一些事情了，不过可以通过「var that = this; 」来解决；3）the constructor invocation pattern，构造函数式调用。这其实是对基于类的面向对象的妥协，用「new + 构造器函数」来调用构造器函数，会创建一个连接到构造函数原型链的新对象，this 绑定到这个新对象上。new 还会改变 return 语句的行为；4）the apply invocation pattern，apply 式调用。Quo.prototype.get_status.apply(statusObject); 是指定 this 绑定到 apply() 调用时传递的参数，在这里即 statusObject，所以 get\_status 函数里的 this.statu 即 statusObject 对象里的 status 属性值。

### 0203. 术语卡 —— 闭包

This quo function is designed to be used without the new prefix, so the name is not capitalized. When we call quo, it returns a new object containing a get\_status method. A reference to that object is stored in myQuo. The get\_status method still has privileged access to quo’s status property even though quo has already returned. get\_status does not have access to a copy of the parameter; it has access to the parameter itself. This is possible because the function has access to the context in which it was created. This is called closure.

当我们调用 quo 时，它返回包含 get\_status 方法的一个新对象（调用函数即创建一个函数对象）。该对象的一个引用保存在 myQuo 中。即使 quo 已经返回了，但 get\_status 方法仍然享有访问 quo 对象的 status 属性的特权。get\_status 方法并不是访问该参数的一个副本，它访问的就是该参数本身。因为该函数可以访问它被创建时所处的上下文环境。这被称为闭包。

### 0204. 术语卡 —— Function

The best thing about JavaScript is its implementation of functions. It got almost everything right. But, as you should expect with JavaScript, it didn’t get everything right. A function encloses a set of statements. Functions are the fundamental modular unit of JavaScript. They are used for code reuse, information hiding, and composition. Functions are used to specify the behavior of objects. Generally, the craft of programming is the factoring of a set of requirements into a set of functions and data structures.

1『 the craft of programming is the factoring of a set of requirements into a set of functions and data structures. 函数式编程的思想。』

Functions in JavaScript are objects. Objects are collections of name/value pairs having a hidden link to a prototype object. Objects produced from object literals are linked to Object.prototype. Function objects are linked to Function.prototype (which is itself linked to Object.prototype). Every function is also created with two additional hidden properties: the function’s context and the code that implements the function’s behavior.

Every function object is also created with a prototype property. Its value is an object with a constructor property whose value is the function. This is distinct from the hidden link to Function.prototype. The meaning of this convoluted construction will be revealed in the next chapter.

Since functions are objects, they can be used like any other value. Functions can be stored in variables, objects, and arrays. Functions can be passed as arguments to functions, and functions can be returned from functions. Also, since functions are objects, functions can have methods. The thing that is special about functions is that they can be invoked.

Javascript 创建一个函数对象时，会给该对象设置一个「调用」属性。当 Javascript 调用一个函数时，可理解为调用此函数的「调用」属性。

### 0205. 术语卡 —— 函数调用

The invocation operator is a pair of parentheses that follow any expression that produces a function value. The parentheses can contain zero or more expressions, separated by commas. Each expression produces one argument value. Each of the argument values will be assigned to the function’s parameter names. There is no runtime error when the number of arguments and the number of parameters do not match. If there are too many argument values, the extra argument values will be ignored. If there are too few argument values, the undefined value will be substituted for the missing values. There is no type checking on the argument values: any type of value can be passed to any parameter.

醍醐灌顶，函数调用和用字面量创建函数是两码事，调用最关键的是那对圆括号 ()，圆括号前面可以是函数名，也可以是函数字面量。而圆括号里面是要传递进函数的实参；parameter 实参，调用函数时传递进来的。argument 形参，定义函数时设定的。

### 0206. 信息卡 —— 代码风格

Throughout this book I have used a consistent style. My intention was to make the code examples as easy to read as possible. I used whitespace consistently to give you more cues about the meaning of my programs.

I indented the contents of blocks and object literals four spaces. I placed a space between if and ( so that the if didn’t look like a function invocation. Only in invocations do I make ( adjacent with the preceding symbol. I put spaces around all infix operators except for . and [, which do not get spaces because they have higher precedence. I use a space after every comma and colon. I put at most one statement on a line. Multiple statements on a line can be misread.

If a statement doesn’t fit on a line, I will break it after a comma or a binary operator. That gives more protection against copy/paste errors that are masked by semicolon insertion. (The tragedy of semicolon insertion will be revealed in Appendix A.) I indent the remainder of the statement an extra four spaces, or eight spaces if four would be ambiguous (such as a line break in the condition part of an if statement). I always use blocks with structured statements such as if and while because it is less error prone. I have seen:

使用一致的留白来理解程序的逻辑思路。1）代码块内容和对象字面量缩进 4 个空格。2）放了一个空格在 if 和 ( 之间，以致 if 不会看起来像一个函数调用。只有真的是在调用时，才使 ( 和其前面的符号相毗连。3）在除了 . 和 [ 外的所有中置运算符的两边都放了空格，它们俩无须空格是因为它们有更高的优先级。4）在每个逗号和冒号后面都使用一个空格。5）在每行最多放一个语句，在一行里放多条语句可能会被误读。如果一个语句一行放不下，我会在一个冒号或二元运算符后拆开它。给折断后的语句的其余部分多缩进 4 个空格，如果 4 个还不够明显，就缩进 8 个空格（例如在一个 if 语句的条件部分插入一个换行符的时候）。6）在诸如 if 和 while 这样结构化的语句里，始终使用代码块，因为这样会减少出错的概率。

### 0301. 人名卡 —— Douglas Crockford

Douglas Crockford，本书作者。

### 0401. 金句卡 —— Most programming languages contain good parts and bad parts

Most programming languages contain good parts and bad parts. I discovered that I could be a better programmer by using only the good parts and avoiding the bad parts

## 书评

### 01

它概括了 JavaScript 这个脚本语言的核心内容，不仅总结了语言的精华部分，还指出了「鸡肋」和「糟粕」。如果说犀牛书展现了 JavaScript 特性的丰富和功能的强大，这本书就体现了 JavaScript 语言轻巧简洁的特点。其实 JavaScript 就是这么简洁，但是它很灵活，使用得好，可以编写出功能强大的程序。语言中核心的内容，也就是犀牛书的第一部分，全部在这本书中被总结出来了。但这并不表示可以从这本书入门，它不是入门级的，不适合初学者。作为概括总结，它是一本很好的帮助你提高 JavaScript 水平的书籍，因为总结也是学习的过程。

这本书的特点是，薄但内容丰富。它用精炼的文字、形象的语法图（railroad diagram）和简短的代码片断总结了 JavaScript 的核心内容。对于对 JavaScript 已经有较深理解的人来说，它可以帮助你整理总结并加深对 JavaScript 的理解，对于了解程度低一点的人来说，它可以帮助你学习 JavaScript 的编程思想。不过就像作者的前言所说的，必须反复阅读。这也正是我决定购买这本书的原因。书的最后那个 json_parse 的例子给我的印象很深。这是本书唯一一个完整的实例代码，它包含了 JavaScript 中很多重要的知识点和代码设计风格（比如闭包），很值得研究学习。

### 02

就如其「最被低估的编程语言」称号所述，Javascript 实际上是一门非常优秀的语言，看似熟悉的语法之下隐含的是完全不同的世界观。尤其是在学、用 erlang 这种函数语言几年后，更能体会其很多设计元素的精巧之处。转贴几条 twitter 上记录的读书笔记备查：

1、Javascript 语言中支持四类函数调用方式：1）全局函数。2）对象方法。3）构造函数。4）apply/call 调用。区别在于函数内 this 指针的绑定，分别是：1）Global 对象。2）调用对象。3）构造返回对象。4）调用时传入的第一个参数。

2、作为 Prototype-base 和 Functional 编程混杂体的 Javascript，居然不提供尾递归 (tail-end recursion) 真是个杯具啊。所以有人想出了这种用 setTimeout 模拟的山寨办法。

3、没有变量块作用域 (Block Scope) 的支持，是 Javascript 语义上与 C/C++ 系统又一重大区别。但回过头来看 Python/Scheme 也不提供块作用域的支持，究竟是当年的设计错误还是我们的思维定势问题？

1『函数内 this 指针的绑定，对象的绑定，对理解变量、引用醍醐灌顶。』

4、A Better Javascript Memoizer 利用闭包 (Closure) 和匿名方法 (anonymous function)，实现针对任意参数个数的 memoizer 模式，对复杂函数的计算结果进行缓存，那是相当的优雅。

5、说起来 Javascript 中自动添加语句结束分号 (semicolon insertion) 也算是一个功能，可以很大程度上提高对网页上语法不规范脚本的兼容性。杯具的是各家的容忍限度不同方法不同，所以基本被列入不应被使用的糟粕。

6、Javascript 里面的 NaN 本身就是个杯具，NaN != NaN 但 typeof NaN === 'number'，必须通过 isNaN 或 isFinite 才能筛选出，但这个可怜的函数又会自动对参数进行隐式类型转换。

7、假以时日，HTTPS 和 Javascript 有可能成为 Web 领域，类似今天 TCP/IP 和 C/C++ 的基础构架的地位。不知十年后再回头看今日的理解，又是一番如何的景象，期待。

### 03

第一本书：JavaScript 高级程序设计。第二本书：ppk 谈 JavaScript。这是第三本。久闻大名的书，读完之后并没有预想的那种感觉。也许是因为书中的很多观点处处通用，即使你没有写过 js，也会从其他语言的普遍做法中见识到。The Definitive Guide 今年又出了新版，非常有可读性，两相对比之下不免让人感觉没那么棒。但这绝对是一本很奇特的书，两个地方：1）印象中其他语言没有对应的著作，例如 "Java: The Good Parts"。C 有一本 pitfalls，但和这本不太一样。js 好的地方列了一遍，不好的地方也列了一遍。2）Appendix 比正文精彩。全书的精华都在 Appendix 了。最后我想说的是，这不是 js 语法书，看中这书薄而放弃 the definitive guide 的同学们，你们亏大了。

2『已下载书籍「2020010JavaScript-The-Definitive-Guide6Ed」。』

### 05

本书的作者 Douglas Crockford 是 JavaScript 开发社区最知名的权威，JavaScript 的发明人 Brendan Eich 说他是「Yoda of lambda programming and JavaScript（lambda 编程和 JavaScript 的精神领袖）」。他不仅仅给我们带来了 JSON、JSLint、JSMin 和 ADSafe 等等，在 JavaScript 开发领域应用广泛且影响深远的作品，更重要的是给我们带来了受益终身的利用 JavaScript 进行高效开发的思想和风格，这就是本书的重要意义。

JavaScript 曾是「世界上最被误解的语言」，因为它担负太多的特性，包括糟糕的交互和失败的设计，但随着 Ajax 的到来，JavaScript「从最受误解的编程语言演变为最流行的语言」，这除了幸运之外，至少还说明它是一个不错的语言。Douglas Crockford 在这本书中剥除 JavaScript 糟糕的外衣，抽离出一个具有更好可靠性、可读性和可维护性的 JavaScript 子集，让你看到一门优雅的、轻量级的和非常富有表现力的语言。作者从语法、对象、函数、继承、数组、正则表达式、方法、样式和优美的特性这 9 个方面来呈现这门语言真正的精华，这是语言最本质最优雅的部分，通过它们完全可以构建出高效的代码。作者还通过附录列出了这门语言的糟粕和鸡肋部分，且告诉你如何避免它们。最后还介绍了 JSLint，通过它的检验，能有效的保障我们写出优美高效的代码。

### 06

是因为：在语言设计上，其借鉴了多种语言，函数式和命令式语言都有，原型链式语言，多年后，在我了解了 lisp 后，才发现，原来 js 一些设计思路，如此的倾向 lisp。js 的创造者应该是语言的专家，通晓编程语言的设计，但当年可能时间比较仓促，留下了不少坑。这一切导致，想真正了解 js 需要一定的门槛，主流的面向对象类的语言经验在此又变得不太有用。在有了几年的编码经验，了解了一些编程语言后，再看 js 变得清晰了许多。

## Preface

JavaScript is a surprisingly powerful language. Its unconventionality presents some challenges, but being a small language, it is easily mastered. My goal here is to help you to learn to think in JavaScript. I will show you the components of the language and start you on the process of discovering the ways those components can be put together. This is not a reference book. It is not exhaustive about the language and its quirks. It doesn’t contain everything you’ll ever need to know. That stuff you can easily find online. Instead, this book just contains the things that are really important.

This is not a book for beginners. Someday I hope to write a JavaScript: The First Parts book, but this is not that book. This is not a book about Ajax or web programming. The focus is exclusively on JavaScript, which is just one of the languages the web developer must master. This is not a book for dummies. This book is small, but it is dense. There is a lot of material packed into it. Don’t be discouraged if it takes multiple readings to get it. Your efforts will be rewarded.

## 0101. Good Parts

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

### 1.1 Why JavaScript?

JavaScript is an important language because it is the language of the web browser. Its association with the browser makes it one of the most popular programming languages in the world. At the same time, it is one of the most despised programming languages in the world. The API of the browser, the Document Object Model (DOM) is quite awful, and JavaScript is unfairly blamed. The DOM would be painful to work with in any language. The DOM is poorly specified and inconsistently implemented. This book touches only very lightly on the DOM. I think writing a Good Parts book about the DOM would be extremely challenging.

1『 DOM 太挫，拿得出手的东西很少。』

JavaScript is most despised because it isn’t some other language. If you are good in some other language and you have to program in an environment that only supports JavaScript, then you are forced to use JavaScript, and that is annoying. Most people in that situation don’t even bother to learn JavaScript first, and then they are surprised when JavaScript turns out to have significant differences from the some other language they would rather be using, and that those differences matter.

The amazing thing about JavaScript is that it is possible to get work done with it without knowing much about the language, or even knowing much about programming. It is a language with enormous expressive power. It is even better when you know what you’re doing. Programming is difficult business. It should never be undertaken in ignorance.

1『 enormous expressive power. 是 JS 的一大特点。』

### 1.2 Analyzing JavaScript

JavaScript is built on some very good ideas and a few very bad ones. The very good ideas include functions, loose typing, dynamic objects, and an expressive object literal notation. The bad ideas include a programming model based on global variables.

1『 ES6 引入的 let、const 就是为了解决「a programming model based on global variables.」』

JavaScript’s functions are first class objects with (mostly) lexical scoping. JavaScript is the first lambda language to go mainstream. Deep down, JavaScript has more in common with Lisp and Scheme than with Java. It is Lisp in C’s clothing. This makes JavaScript a remarkably powerful language.

The fashion in most programming languages today demands strong typing. The theory is that strong typing allows a compiler to detect a large class of errors at compile time. The sooner we can detect and repair errors, the less they cost us. JavaScript is a loosely typed language, so JavaScript compilers are unable to detect type errors. This can be alarming to people who are coming to JavaScript from strongly typed languages. But it turns out that strong typing does not eliminate the need for careful testing. And I have found in my work that the sorts of errors that strong type checking finds are not the errors I worry about. On the other hand, I find loose typing to be liberating. I don’t need to form complex class hierarchies. And I never have to cast or wrestle with the type system to get the behavior that I want.

1『 JS 是弱类型语言。作者认为强类型语言（比如 Java）在类型强制上能提供的真正有用的价值有限，获得的好处弥补不了弱类型的灵活性。』

JavaScript has a very powerful object literal notation. Objects can be created simply by listing their components. This notation was the inspiration for JSON, the popular data interchange format. (There will be more about JSON in Appendix E.)

1-2『 a very powerful object literal notation. 是 JS 的又一大特点。 附录里的 JSON 实例要反复去研读。』

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

### 1.3 A Simple Testing Ground

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

1『写 JS 代码可以按这种方式在本地服务器上跑，比在浏览器里的 console 里写代码方便太多；还有种更简单的方式，直接在 html 或者 js 文件里嵌入 JS 代码，这样不用弄 2 个文件，JS 代码量不多的情况下。』

Next, open your HTML file in your browser to see the result. Throughout the book, a method method is used to define new methods. This is its definition: 

```js
Function.prototype.method = function (name, func) {
    this.prototype[name] = func;
    return this;
};
```

## 0901. Style

programs are the most complex things that humans make. Programs are made up of a huge number of parts, expressed as functions, statements, and expressions that are arranged in sequences that must be virtually free of error. The runtime behavior has little resemblance to the program that implements it. Software is usually expected to be modified over the course of its productive life. The process of converting one correct program into a different correct program is extremely challenging.

运行时行为（runtime behavior）几乎和实现它的程序没有什么相似之处。在软件的产品生命周期中，它们通常都会被修改。把一个正确的程序转化为另一个同样正确但风格不同的程序，是一个极具挑战性的过程。

Good programs have a structure that anticipates—but is not overly burdened by—the possible modifications that will be required in the future. Good programs also have a clear presentation. If a program is expressed well, then we have the best chance of being able to understand it so that it can be successfully modified or repaired.

1『特别赞同，代码的可读性、可扩展性。』

优秀的程序拥有一个前瞻性的结构，它会预见到在未来才可能需要的修改，但不会让其成为过度的负担。优秀的程序还会具备一种清晰的表达方式。如果一个程序被表达得很好，那么我们就能更加容易地去理解它，以便成功地改造或修补它。这些观点适用于所有的编程语言，而对 Javascript 来说尤为如此。Javascript 的弱类型和过度的容错性导致程序质量无法在编译时获得保障，所以为了弥补，我们应该按照严格的规范进行编码。

These concerns are true for all programming languages, and are especially true for JavaScript. JavaScript’s loose typing and excessive error tolerance provide little compile-time assurance of our programs’ quality, so to compensate, we should code with strict discipline.

JavaScript contains a large set of weak or problematic features that can undermine our attempts to write good programs. We should obviously avoid JavaScript’s worst features. Surprisingly, perhaps, we should also avoid the features that are often useful but occasionally hazardous. Such features are attractive nuisances, and by avoiding them, a large class of potential errors is avoided.

The long-term value of software to an organization is in direct proportion to the quality of the codebase. Over its lifetime, a program will be handled by many pairs of hands and eyes. If a program is able to clearly communicate its structure and characteristics, it is less likely to break when it is modified in the never-too-distant future.

对于一个组织机构来说，软件的长远价值和代码库的质量成正比。在程序的生命周期里，会经历很多人的测试、使用和修改。如果一个程序能很清楚地传达它的结构和特性，那么当它在井不遥远的将来被修改时，它被破坏的可能性就小很多。

JavaScript code is often sent directly to the public. It should always be of publication quality. Neatness counts. By writing in a clear and consistent style, your programs become easier to read.

Programmers can debate endlessly on what constitutes good style. Most programmers are firmly rooted in what they’re used to, such as the prevailing style where they went to school, or at their first job. Some have had profitable careers with no sense of style at all. Isn’t that proof that style doesn’t matter? And even if style doesn’t matter, isn’t one style as good as any other? It turns out that style matters in programming for the same reason that it matters in writing. It makes for better reading.

Javascript 代码经常被直接发布。它应该自始至终具备发布质量，要干净利落。通过在一个清晰且始终如一的风格下编写，你的程序会变得易于阅读。程序员会无休止地讨论良好的风格是由什么构成的。大多数程序员会坚持他们过去的应用经验，比如他们在学校或在他们第一份工作时学到的流行的风格。他们中的一些人拥有高薪的工作，但完全没有代码风格的意识。这是否证明了风格其实根本不重要？就算风格不重要，风格之间是否有优劣之分呢？事实证明代码风格在编程中是很重要的，就像文字风格对于写作很重要一样。好的风格让代码能更好地被阅读。

Computer programs are sometimes thought of as a write-only medium, so it matters little how it is written as long as it works. But it turns out that the likelihood a program will work is significantly enhanced by our ability to read it, which also increases the likelihood that it actually works as intended. It is also the nature of software to be extensively modified over its productive life. If we can read and understand it, then we can hope to modify and improve it.

电脑程序有时候被认为不是用来读的，所以只要它能工作，写成怎样是不重要的。但是结果证明，如果程序可读性强，它正常运行的可能性，以及是否准确按照我们的意图去工作的可能性也显著增强。它还决定了软件在其生命周期中能否进行扩展。如果我们能阅读并且理解程序，那么就有希望去修改和完善它。

Throughout this book I have used a consistent style. My intention was to make the code examples as easy to read as possible. I used whitespace consistently to give you more cues about the meaning of my programs.

I indented the contents of blocks and object literals four spaces. I placed a space between if and ( so that the if didn’t look like a function invocation. Only in invocations do I make ( adjacent with the preceding symbol. I put spaces around all infix operators except for . and [, which do not get spaces because they have higher precedence. I use a space after every comma and colon. I put at most one statement on a line. Multiple statements on a line can be misread.

If a statement doesn’t fit on a line, I will break it after a comma or a binary operator. That gives more protection against copy/paste errors that are masked by semicolon insertion. (The tragedy of semicolon insertion will be revealed in Appendix A.) I indent the remainder of the statement an extra four spaces, or eight spaces if four would be ambiguous (such as a line break in the condition part of an if statement). I always use blocks with structured statements such as if and while because it is less error prone. I have seen:

贯穿本书，我始终采用一致的风格。我的目的是使代码实例尽可能易于阅读。我使用一致的留白来帮助你理解我的程序的逻辑思路。我对代码块内容和对象字面量缩进 4 个空格。我放了一个空格在 if 和 ( 之间，以致 if 不会看起来像一个函数调用。只有真的是在调用时，我才使 ( 和其前面的符号相毗连。我在除了 . 和 [ 外的所有中置运算符的两边都放了空格，它们俩无须空格是因为它们有更高的优先级。我在每个逗号和冒号后面都使用一个空格。

我在每行最多放一个语句，在一行里放多条语句可能会被误读。如果一个语句一行放不下，我会在一个冒号或二元运算符后拆开它，这将更好地防止自动插入分号的机制掩盖复制 / 粘贴的错误（自动插入分号带来的悲剧会在附录 A 里披露）。我给折断后的语句的其余部分多缩进 4 个空格，如果 4 个还不够明显，就缩进 8 个空格（例如在一个 if 语句的条件部分插入一个换行符的时候）。在诸如 if 和 while 这样结构化的语句里，我始终使用代码块，因为这样会减少出错的概率。

2『上面的代码风格做一张信息卡片，进行刻意练习。』

```js
if (a)
    b( );
```

become:

```js
if (a)
    b( );
    c( );
```

which is an error that is very difficult to spot. It looks like: 

```js
if (a) {
    b( );
    c( );
}
```

but it means:

```js
if (a) {
    b( );
}
c( );
```

Code that appears to mean one thing but actually means another is likely to cause bugs. A pair of braces is really cheap protection against bugs that can be expensive to find.

看起来想要做一件事情但实际上却在做另一件事情的代码很可能导致 bug。一对花括号可以用很低廉的成本去防止那些需要昂贵的代价才能发现的 bug。

1『指上面的代码示例。』

I always use the K&R style, putting the { at the end of a line instead of the front, because it avoids a horrible design blunder in JavaScript’s return statement. I included some comments. I like to put comments in my programs to leave information that will be read at a later time by people (possibly myself) who will need to understand what I was thinking. Sometimes I think about comments as a time machine that I use to send important messages to future me. I struggle to keep comments up-to-date. Erroneous comments can make programs even harder to read and understand. I can’t afford that.

我一直使用 K&R 风格，把 { 放在一行的结尾而不是下一行的开头，因为它会避免 Javascript 的 return 语句中的一个可怕的设计错误。

2『 K&R 风格，因在 Kernighan 与 Ritchie 合著的 The C Programming Language 一书中广泛用而得名。它是最为遍的 C 语言代码风格。已下载书籍「2019045C程序设计语言2Ed | 2019045The-C-Programming-Language」。』

I tried to not waste your time with useless comments like this: 

    i = 0; // Set i to zero.

In JavaScript, I prefer to use line comments. I reserve block comments for formal documentation and for commenting out. I prefer to make the structure of my programs self-illuminating, eliminating the need for comments. I am not always successful, so while my programs are awaiting perfection, I am writing comments.

1『哈哈，重构可以帮助代码实现「自我解释」。』

在 Javascript 里，我更喜欢用行注释。我把块注释用于正式的文档记录和注释。我更喜欢使我的程序结构能自我说明（self-illuminating），从而消除对注释的需要。我并非每次都能做到，所以只要我的程序还不尽完美，我就会编写注释。

JavaScript has C syntax, but its blocks don’t have scope. So, the convention that variables should be declared at their first use is really bad advice in JavaScript. JavaScript has function scope, but not block scope, so I declare all of my variables at the beginning of each function. JavaScript allows variables to be declared after they are used. That feels like a mistake to me, and I don’t want to write programs that look like mistakes. I want my mistakes to stand out. Similarly, I never use an assignment expression in the condition part of an if because:

```js
if (a = b) { ... }
```

is probably intended to be:

```js
if (a === b) { ... }
```

I want to avoid idioms that look like mistakes.

1『 ES6 新增的 let、const 解决了作者的难题，所以好希望这本书可以出新版，哈哈；条件语句里的判断语言，一定不要用赋值语句。（2020-08-27）』

I never allow switch cases to fall through to the next case. I once found a bug in my code caused by an unintended fall through immediately after having made a vigorous speech about why fall through was sometimes useful. I was fortunate in that I was able to learn from the experience. When reviewing the features of a language, I now pay special attention to features that are sometimes useful but occasionally dangerous. Those are the worst parts because it is difficult to tell whether they are being used correctly. That is a place where bugs hide.

我绝不允许 switch 语句块中的条件穿越到下一个 case 语句。我曾经在我的代码里发现了一个无意识的「穿越」导致的 bug，而在此之前，我刚刚激情澎湃地做完一次关于如何妙用「穿越」有时很有用的演讲。我很幸运能够从这个教训中有所收获。当我现在评审一门语言的特性的时候，我把注意力放在那些有时很有用但偶尔很危险的特性上。那些是量糟的部分，因为我们很难辨别它们是否被正确使用。那是 bug 的藏身之地。

Quality was not a motivating concern in the design, implementation, or standardization of JavaScript. That puts a greater burden on the users of the language to resist the language’s weaknesses. JavaScript provides support for large programs, but it also provides forms and idioms that work against large programs. For example, JavaScript provides conveniences for the use of global variables, but global variables become increasingly problematic as programs scale in complexity.

I use a single global variable to contain an application or library. Every object has its own namespace, so it is easy to use objects to organize my code. Use of closure provides further information hiding, increasing the strength of my modules.

1『闭包可以实现信息隐藏，这个知识点一直没吃透。（2020-08-27）』

在 Javascript 的设计、实现和标准化的过程中，质量没有被特别关注。这给使用这门语言的用户增加了避免其缺陷的难度。Javascript 为大型程序提供了支持，但它也带有不利于大型程序的形式和习惯用法。举例来说：Javascript 可以方便地使用全局变量，但随着程序的日益复杂，全局变量逐渐变得问题重重。对一个脚本应用或工具库，我只用唯一一个全局变量。每个对象都有它自己的命名空间，所以我很容易使用对象去管理代码。使用闭包能提供进一步的信息隐藏，增强我的模块的建壮性。

3『

作者的这个思想在 YAHOO 的 Javascript 库 YUI 中得到了彻底的贯彻。在 YUI 中仅用到两个全局变量：YAHO 和 YAHOO_config。YUI 的一切都是基于一种模块模式来实现的。

github 上找到下面代码：[javascript 模块模式实现](https://gist.github.com/tangyangzhe/4276560)

```js
// http://dancewithnet.com/2007/12/04/a-javascript-module-pattern/
<script type="text/javascript" src="http://yui.yahooapis.com/2.2.2/build/utilities/utilities.js"></script>
<ul id="myList">
    <li class="draggable">一项</li>
    <li>二项</li>
    <li class="draggable">三项</li>
</ul>
<script>
    YAHOO.namespace("myProject");
    YAHOO.myProject.myModule = function () {
        var yue = YAHOO.util.Event,
            yud = YAHOO.util.Dom;
        //私有方法
        var getListItems = function () {
            var elList = yud.get("myList");
            var aListItems = yud.getElementsByClassName("li", elList);
            return aListItems;
        };
        //这个返回的对象将变成 YAHOO.myProject.myModule:
        return {
            aDragObjects: [], //可对外访问的，存储DD对象
            init: function () {
                //直到DOM完全加载好，才实现列表项可拖拽：
                yue.onDOMReady(this.makeLIsDraggable, this, true);
            },
            makeLIsDraggable: function () {
                var aListItems = getListItems(); //我们可以拖拽的那些元素
                for (var i = 0, j = aListItems.length; i < j; i++) {
                    this.aDragObjects.push(new YAHOO.util.DD(aListItems[i]));
                }
            }
        };
    }();
    //上面的代码已经执行，所以我们能立即访问 init 方法：
    YAHOO.myProject.myModule.init();
</script>
```
medium 上的一篇文章：[Module Pattern in JavaScript - Level Up Coding](https://levelup.gitconnected.com/data-hiding-with-javascript-module-pattern-62b71520bddd)

』

## 1001. Beautiful Features

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
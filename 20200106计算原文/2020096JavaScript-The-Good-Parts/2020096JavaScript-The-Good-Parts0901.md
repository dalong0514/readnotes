# 09 Style

Here is a silly stately style indeed!

—William Shakespeare, The First Part of Henry the Sixth Computer 

programs are the most complex things that humans make. Programs are made up of a huge number of parts, expressed as functions, statements, and expressions that are arranged in sequences that must be virtually free of error. The runtime behavior has little resemblance to the program that implements it. Software is usually expected to be modified over the course of its productive life. The process of converting one correct program into a different correct program is extremely challenging.

运行时行为（runtime behavior）几乎和实现它的程序没有什么相似之处。在软件的产品生命周期中，它们通常都会被修改。把一个正确的程序转化为另一个同样正确但风格不同的程序，是一个极具挑战性的过程。

Good programs have a structure that anticipates—but is not overly burdened by—the possible modifications that will be required in the future. Good programs also have a clear presentation. If a program is expressed well, then we have the best chance of being able to understand it so that it can be successfully modified or repaired.

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

在 Javascript 里，我更喜欢用行注释。我把块注释用于正式的文档记录和注释。我更喜欢使我的程序结构能自我说明（self- illuminating），从而消除对注释的需要。我并非每次都能做到，所以只要我的程序还不尽完美，我就会编写注释。

JavaScript has C syntax, but its blocks don’t have scope. So, the convention that variables should be declared at their first use is really bad advice in JavaScript. JavaScript has function scope, but not block scope, so I declare all of my variables at the beginning of each function. JavaScript allows variables to be declared after they are used. That feels like a mistake to me, and I don’t want to write programs that look like mistakes. I want my mistakes to stand out. Similarly, I never use an assignment expression in the condition part of an if because:

    if (a = b) { ... }

is probably intended to be:

    if (a === b) { ... }

I want to avoid idioms that look like mistakes.

1『 ES6 新增的 let、const 解决了作者的难题。』

I never allow switch cases to fall through to the next case. I once found a bug in my code caused by an unintended fall through immediately after having made a vigorous speech about why fall through was sometimes useful. I was fortunate in that I was able to learn from the experience. When reviewing the features of a language, I now pay special attention to features that are sometimes useful but occasionally dangerous. Those are the worst parts because it is difficult to tell whether they are being used correctly. That is a place where bugs hide.

我绝不允许 switch 语句块中的条件穿越到下一个 case 语句。我曾经在我的代码里发现了一个无意识的「穿越」导致的 bug，而在此之前，我刚刚激情澎湃地做完一次关于如何妙用「穿越」有时很有用的演讲。我很幸运能够从这个教训中有所收获。当我现在评审一门语言的特性的时候，我把注意力放在那些有时很有用但偶尔很危险的特性上。那些是量糟的部分，因为我们很难辨别它们是否被正确使用。那是 bug 的藏身之地。

Quality was not a motivating concern in the design, implementation, or standardization of JavaScript. That puts a greater burden on the users of the language to resist the language’s weaknesses. JavaScript provides support for large programs, but it also provides forms and idioms that work against large programs. For example, JavaScript provides conveniences for the use of global variables, but global variables become increasingly problematic as programs scale in complexity.

I use a single global variable to contain an application or library. Every object has its own namespace, so it is easy to use objects to organize my code. Use of closure provides further information hiding, increasing the strength of my modules.

在 Javascript 的设计、实现和标准化的过程中，质量没有被特别关注。这给使用这门语言的用户增加了避免其缺陷的难度。Javascript 为大型程序提供了支持，但它也带有不利于大型程序的形式和习惯用法。举例来说：Javascript 可以方便地使用全局变量，但随着程序的日益复杂，全局变量逐渐变得问题重重。对一个脚本应用或工具库，我只用唯一一个全局变量。每个对象都有它自己的命名空间，所以我很容易使用对象去管理代码。使用闭包能提供进一步的信息隐藏，增强我的模块的建壮性。

3『

作者的这个思想在 YAHOO 的 Javascript 库 YUI 中得到了底的贯彻。在 YUI 中仅用到两个全局变量：YAHO 和 YAHOO_config。YUI 的一切都是基于一种模块模式来实现的。

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
        //这个放回的对象将变成YAHOO.myProject.myModule:
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
    //上面的代码已经执行，所以我们能立即访问init方法：
    YAHOO.myProject.myModule.init();
</script>
```
medium 上的一篇文章：[Module Pattern in JavaScript - Level Up Coding](https://levelup.gitconnected.com/data-hiding-with-javascript-module-pattern-62b71520bddd)

』


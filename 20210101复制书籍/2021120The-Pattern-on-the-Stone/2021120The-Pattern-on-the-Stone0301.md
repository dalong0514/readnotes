## 0301. Programming

T he magic of a computer lies in its ability to become almost anything you can imagine, as long as you can explain exactly what that is. The hitch is in explaining what you want. With the right programming, a computer can become a theater, a musical instrument, a reference book, a chess opponent. No other entity in the world except a human being has such an adaptable, universal nature. Ultimately all these functions are implemented by the Boolean logic blocks and finite-state machines described in the previous chapter, but the human computer programmer rarely thinks about these elements; instead, programmers work with a more convenient tool called a programming language.

Just as Boolean logic and finite-state machines are the building blocks of computer hardware, a programming language is a set of building blocks for constructing computer software. Like a human language, a programming language has a vocabulary and a grammar, but unlike a human language there is an exact meaning in the programming language for every word and sentence. Most programming languages are universal, in the same sense that Boolean logic is universal: they can be used to describe anything a computer can do. Anyone who has ever written a program — or debugged a program — knows that telling a computer what you want it to do is not as easy as it sounds. Every detail of the computer's desired operation must be precisely described. For instance, if you tell an accounting program to bill your clients for the amount that each owes, then the computer will send out a weekly bill for `$`0.00 to clients who owe nothing. If you tell the computer to send a threatening letter to clients who have not paid, then clients who owe nothing will receive threatening letters until they send in payments of $0.00. Avoiding this kind of misunderstanding is what computer programming is all about. The programmer's art is the art of saying exactly what you want. In this example, it means making a distinction between clients who have not sent in any money and clients who actually owe money. To paraphrase Mark Twain, the difference between the right program and the almost-right program is like the difference between lightning and a lightning bug — the difference is just a bug.

A skilled programmer is like a poet who can put into words those ideas that others find inexpressible. If you are a poet, you assume a certain amount of shared knowledge and experience on the part of your reader. The knowledge and experience that the programmer and the computer have in common is the meaning of the programming language. How the computer「knows」the meaning of the programming language will be described later; first, we will discuss the grammar, vocabulary, and idioms of such languages.

计算机的神奇之处在于，只要你能精确地描述出你所想象的东西，计算机就能将其变幻出来。问题的关键在于，如何描述你所想要的东西。只要程序编写正确，计算机就能摇身一变，成为一家剧院、一件乐器、一本参考书，甚至成为一名国际象棋高手。除了人类以外，世界上没有任何实体能拥有如此高的适应性和通用性。这些功能的实现离不开布尔逻辑块和有限状态机。不过，程序员通常不会考虑这些因素，而是会借助一种更为便捷的工具来实现所需的功能，那就是编程语言。

正如布尔逻辑块和有限状态机是计算机硬件的通用构件，编程语言是计算机软件的通用构件。与人类语言一样，编程语言也具有自身的词汇和语法。不过，不同于人类的语言，编程语言中的每个词汇和语句的含义具有唯一性。正如布尔逻辑具有通用性，大多数编程语言也是如此：它们可以用来描述计算机能做的所有事情。所有编写过或者调试过程序的人都知道，让计算机完成交给它的任务绝非易事，你必须精确地描述出计算机所要操作的所有细节。例如，如果你让记账程序将顾客的欠款以账单的形式寄给他们，那么那些从未赊账的顾客每周也会收到金额为 0 美元的账单。如果你让计算机给那些没有付款的顾客寄去一封催款通知，那么那些没有任何欠款的顾客也会收到金额为 0 美元的催款通知。所谓计算机编程，就是要避免以上这类错误。所谓编程艺术，就是将心中所想精确地告知计算机的艺术。在这个例子中，程序员需要让程序区分出欠款但未还款的顾客和未欠款的顾客。借用马克·吐温的话来说就是，正确的程序和几乎正确的程序之间的差异就像闪电和闪电虫之间的差异，差异本身就是一个问题。

技艺精湛的程序员就诗人一样，能将别人无法形容的思想付诸文字。如果你是一位诗人，就能和读者共享某些知识和体验。程序员和计算机之间共享的知识和体验就是编程语言的含义。我们将会在后文探讨计算机是如何「获知」编程语言所表达的含义的，接下来先讨论编程语言的语法、词汇和常用语。

### 3.1 Talking to The Computer

There are many different programming languages. The main reasons for this diversity are history, habit, and taste, but different programming languages also exist because they are good at describing different kinds of things. Each language has its own syntax. You need to learn the syntax in order to write the language, but (like spelling and punctuation in a human language) syntax is not fundamental to the meaning or the expressive power of the language. What is important to the expressive power of the language is the vocabulary — the so-called primitives of the language — and the way the primitives can be combined to define new concepts.

Programming languages describe the manipulation of data, and one way in which these languages differ is in the kinds of data they can manipulate. The earliest computer languages were designed primarily to manipulate numbers and sequences of characters. Latter-day programming languages can manipulate words, pictures, sounds, and even other computer programs. But no matter what sort of data the language is designed to handle, it typically provides a way of reading the data's elements into the computer, taking the data apart, putting them together, modifying them, comparing them, and giving them names.

It's probably easier to illustrate these abstractions by describing a particular computer language — I've chosen Logo, which was designed by the educator and mathematician Seymour Papert as a computer language for children. Children can write programs in Logo which create and manipulate pictures, words, numbers, and sounds. Although the language is simple enough to be used by a ten-year-old, it embodies many of the features of the most sophisticated computer languages, including the ability to write programs that manipulate other programs. Logo is also an extensible language — that is, you can use Logo to define new words in Logo.

One of the simplest types of programs to write in Logo is a procedure for drawing a picture. You do this by giving directions to an imaginary turtle that lives on the screen. The turtle serves as a pen, moving around on the screen and leaving lines behind it. When the computer starts up, the turtle is found at the center of the screen, facing upward. If the child types the command FORWARD 10, the turtle takes ten steps forward — that is, upward — drawing a line ten units long. The number 10 following the FORWARD command is called a parameter; in this case, the parameter tells the turtle how many steps to take. To draw a line in a different direction, the child must turn the turtle. The command RIGHT 45 will point the turtle 45 degrees (another parameter) to the right from its last heading. The next FORWARD command, with its parameter, will then draw a line in the new direction.

The child can use commands like FORWARD, BACKWARD, RIGHT, and LEFT to move the turtle around the screen and draw pictures, but this involves a lot of typing and soon becomes tedious. What makes the language interesting is its ability to define new words: for example, here's how the child could teach the turtle (program the computer) to draw a square:

```
TO SQUARE

FORWARD 10

RIGHT 90

FORWARD 10

RIGHT 90

FORWARD 10

RIGHT 90

FORWARD 10

END
```

FIGURE 18 A square

Having defined the word「square,」the child can then draw a square with ten units on a side simply by typing a new command: SQUARE. (Needless to say, the name「square」is arbitrary; the child could just as well have called the procedure BOX or XYZ and the turtle would do exactly the same thing. When children discover this, they often enjoy「fooling」the computer — for instance, calling the procedure that draws a square TRIANGLE, and vice versa.)

Once the word「square」has been defined, it becomes part of the computer's vocabulary and can then be used to define other words. For example,

```
TO WINDOW

SQUARE

SQUARE

SQUARE

SQUARE

END
```

Each square will be drawn in a different place, because the procedure for drawing the square leaves the turtle rotated 90 degrees. In computer terms, SQUARE is a subroutine of the program WINDOW, which calls it. The subroutine SQUARE, in turn, is defined using the primitives FORWARD and RIGHT. User-defined words in Logo can take parameters, too. For instance, a child can specify various sizes of square by specifying what parameter determines the length of each side.

```
TO SQUARE :SIZE

FORWARD :SIZE

RIGHT 90

FORWARD :SIZE

RIGHT 90

FORWARD :SIZE

RIGHT 90

FORWARD :SIZE

END
```

FIGURE 19 A window, made of four squares

The colon in front of the command SIZE is an example of syntax. In Logo, the colon indicates that the word that follows is the name of a parameter, representing something else — in this case, the number to be supplied each time we「call」the subroutine named SQUARE. When SQUARE is defined this way, the command SQUARE 15 will tell the computer to draw a square fifteen units on a side. The parameter name SIZE is, again, an arbitrary name and has meaning only within the definition of SQUARE: if all five occurrences of SIZE were replaced with X, say, the subroutine would do exactly the same thing.

FIGURE 20 A design, drawing in progress

There are other ways of writing a subroutine to draw a square. For instance, you can instruct the turtle to turn left four times, or to go backward four times. What's interesting is that it doesn't matter how SQUARE is defined; all that matters is what the subroutine draws and where it leaves the turtle. Other programs can call the SQUARE no matter how it is defined and whether or not it is a user-defined word or one of the language's primitives. In extending the language, the programmer uses the power of functional abstraction to create new building blocks.

One of the tricks that Logo-using children discover is that they can insert a word inside its own definition, a practice known as recursion. For instance, a child might generate a circular design consisting of many rotated squares, as follows:

```
TO DESIGN

SQUARE

RIGHT 10

DESIGN

END
```

The computer follows the DESIGN command by drawing a square, then turning the turtle 10 degrees and drawing another「design」in the same way. In this case, the recursive definition of「design」has a problem: it goes on forever. Each time the computer responds to the DESIGN command it draws a square, and then it must go on to another design, and on and on ad infinitum — rather as in the story of the guru who claimed that the earth was sitting on the back of (as it happens) a giant turtle.「And what is the turtle sitting on?」asked a student.「Another turtle,」replied the guru.「And that turtle?」asked the student, beginning to grow skeptical.「It's no use asking,」said the guru.「It's turtles all the way down.」

The computer, in drawing the design, goes through the same process that human beings go through in trying to imagine the infinite stack of giant turtles, but the computer is not smart enough to notice that it's not getting anywhere. It will not halt until it is interrupted — an example of a common sort of program behavior called an infinite loop. Programmers often create infinite loops accidentally, and (as we shall see) it can be extremely difficult to predict when such loops will occur. This particular infinite loop is easily avoided by writing the program with a parameter specifying how many squares to draw.

```
TO DESIGN :NUMBER

SQUARE

RIGHT 10

IF :NUMBER = 1 STOP ELSE DESIGN :NUMBER −1

END
```

Thus defined, the DESIGN subroutine will do one of two things, depending on whether its parameter is 1 or some higher number. DESIGN 1 will draw just one square, but DESIGN 5, say, will draw a square, rotate, and then draw a DESIGN 4. DESIGN 4 will draw a square and then a DESIGN 3, and so on down to DESIGN 1, which will draw a square and stop.

This kind of recursive definition with a changing parameter is useful for producing anything that has a self-similar structure. A picture that contains a picture of itself is an example of a recursive, self-similar structure; such structures are commonly known as fractals. In the real world, self-similar structures don't go on forever: for instance, each branch of a tree looks a lot like a smaller tree, and each of these smaller branches has branches that look like still smaller trees. This recursion goes on for several levels, but eventually the branches are so small that they do not have branches of their own.

A recursive Logo program for drawing a tree is shown below. This may give you some idea of how a computer program can contain an element of poetry — although in this case the theme is somewhat obscured by the details of positioning the turtle and bringing it back to the starting point. Here's a rough translation of what the program says:「A big tree is a stick with two smaller trees on top, but a little tree is just a stick.」The picture produced by the tree program is shown next to it.

```
TO TREE :SIZE

FORWARD :SIZE

IF :SIZE <1 STOP ELSE TWO-TREES SIZE/2

BACK :SIZE

END

FIGURE 21

A tree

TO TWO-TREES :SIZE

LEFT 45

TREE :SIZE

RIGHT 90

TREE :SIZE

LEFT 45

END
```

This technique of defining things recursively turns out to be very powerful. Many of the types of data we like to manipulate — in particular, computer programs themselves — have recursive structures. Recursive definitions are extremely convenient for specifying operations on recursive data. The typical recursive definition has two parts — the first part describes what is to happen in a particular simple case, and the second describes how a more complex case can be reduced to something simpler. In the recursive tree, for example, the simple case is the tree smaller than 1 and the more complex case is the tree composed of a trunk and two small trees.

Another example is the definition of a palindrome, which we can define as follows: A word is a palindrome if it has less than two letters (the simple case) or if its first and last letter are the same and the letters in the middle form a palindrome (the recursive step). The simplest way to write a Logo program for recognizing palindromes would be to use this recursive definition.

There are many other computer languages: LISP, Ada, FORTRAN, C, ALGOL, and the like; most of the names are obscure acronyms (such as FORTRAN, for FORmula TRANslation, and LISP, for LISt Processing). Although these languages differ from Logo in details of vocabulary and syntax, they can all express the same kinds of procedures. Some, like FORTRAN, are limited in their ability to define operations recursively or to manipulate non-numerical data. Others, like C and LISP, allow the programmer to manipulate the underlying bits representing the data, which gives the programmer more power — and more opportunity to make mistakes. In C, for example, it's perfectly possible to multiply two alphabetic characters; the result of this nonsensical operation will depend on the binary representation used by the machine. Languages like LISP offer the abstract as well as the lower-level functions. As a friend of mine, the computer scientist Guy Steele, once put it,「LISP is a high-level language, but you can still feel the bits sliding between your toes.」

More recently, a new generation of languages has begun to emerge. These languages — Small-Talk, C++, Java — are object-oriented. They treat a data structure — for instance, a picture to be drawn on the screen — as an「object」with its own internal state, such as where it is to be drawn or what color it is. These objects can receive instructions from other objects. To understand why this is useful, imagine that you are writing a program for a video game involving bouncing balls. Each ball on the screen is defined as a different object. The program specifies rules of behavior that tell the object how to draw itself on the screen, move, bounce, and interact with other objects in the game. Each ball will exhibit similar behavior, but each will be in a slightly different state, because each will be in its own position on the screen and will have its own color, velocity, size, and so forth.

The most important advantage of an object-oriented programming language is that the objects — for instance, various objects in a video game — can be specified independently and then combined to create new programs. Writing a new object-oriented program sometimes feels a bit like throwing a bunch of animals into a cage and watching what happens. The behavior of the program emerges , as a result of the interactions of the programmed objects. For this reason, as well as the fact that object-oriented languages are relatively new, you might think twice about one for writing a safety-critical system that flies an airplane.

Learning a programming language is not nearly as difficult as learning a natural human language. Generally, once you have learned two or three, you can pick up others in a matter of a few hours, since the syntax is relatively simple and the vocabularies are rarely more than a few hundred words. But, as is true of a human language, there's a big difference between being able to understand the language and being able to write it well. Every computer language has its Shakespeares, and it is a joy to read their code. A well-written computer program possesses style, finesse, even humor — and a clarity that rivals the best prose.

与计算机对话

编程语言的种类有很多，这种现象主要是由历史、习惯和品味等因素引起的。此外，不同编程语言善于描述不同类型的事物，这也是存在多种编程语言的原因之一。每种编程语言都有自己的语法。只有掌握了编程语法之后，我们才能编写程序，编程语法就如同人类语言中的拼写和标点。不过，对于编程语言的含义和表达来说，语法并非关键所在，更为重要的是词汇，也叫语言的原语（primitive），以及将这些原语组合形成新概念的方法。

所有的编程语言都会对所处理的数据进行描述，它们之间的区别在于各自所能处理的数据类型是不同的。最早的编程语言主要用于处理数字和字符串，之后的编程语言可以处理文字、图像、声音，甚至其他计算机程序。不过，无论编程语言被用于处理何种数据类型，它通常都会提供一种方式来读取、分离、整合、修改、计算和命名数据。

为了更形象地说明上述的抽象概念，我们以一个具体的计算机编程语言为例 ——Logo 语言。这种编程语言是由教育学家、数学家西摩·帕佩特（Seymour Papert）专为儿童设计的，可以用于编写程序来创建和处理图片、文字、数字和声音等。对于 10 岁的孩子来说，这种编程语言虽然十分简单，但同样具有最复杂的计算机编程语言的许多功能，比如编写可以控制其他程序的程序。Logo 语言还是一种可扩展语言，也就是说，你可以通过 Logo 原语定义新的词语。

海龟绘图程序是用 Logo 语言编写的最简单的程序之一。你可以给屏幕上的海龟下达指令，这只海龟就如同一支画笔，在屏幕上留下移动轨迹。当程序启动后，海龟头部朝上且位于屏幕中央。如果小孩输入指令「FORWARD10」，海龟就会向前迈出 10 步，也就是说，向上画出一条长度为 10 个单位的直线。「FORWARD」指令后面的数字 10 被称为参数。在这个例子中，参数规定了海龟应该往前走多少步。为了在不同的方向上画出直线，小孩必须调整海龟的前进方向。指令「RIGHT45」会使海龟自原来的朝向向右转 45 度（这也是一个参数）。如果再输入一个带参数的指令「FORWARD」，海龟就会在新方向上画出一条直线（见图 3-1）。

图 3-1 海龟绘图程序

当小孩输入「FORWARD」「BACKWARD」「RIGHT」「LEFT」等指令时，海龟就会在屏幕上依次向上、下、右、左移动，画出各种图像。然而，这样的操作需要输入大量指令，很快就会使人感到枯燥乏味。Logo 语言有趣的地方在于，它能够定义新指令。例如，小孩可以利用如下指令教会海龟（即为计算机写程序）画出一个正方形（见图 3-2）。

在定义完「正方形」这个词之后，小孩子只需输入新指令「SQUARE」（正方形），海龟便能画出一个边长为 10 个单位的正方形。毋庸讳言，指令「SQUARE」可被改为其他任意名字。即使小孩将指令命名为「箱子」或者「XYZ」，海龟还是会完成一模一样的动作。当小孩发现这一点后，会经常「戏耍」计算机取乐。比如，将画正方形的指令命名为「TIANGLE」（三角形），反之亦然。

一旦定义了「SQUARE」这个词，它就成了计算机词汇库中的一员，我们就可以用它来定义新指令，例如可以用它来定义「WINDOW」，即窗户（见图 3-3）。

根据以上这些指令，海龟便会绘制出位于不同位置的 4 个正方形，因为每画完一个正方形，海龟会旋转 90 度。用计算机术语来说，「SQUARE」是程序「WINDOW」的一个子程序，后者调用了前者，而子程序「SQUARE」又是基于原语「RIGHT」和「FORWARD」定义出来的。用户自定义的指令也带有参数。比如，小孩可以设定正方形的边长，并画出不同大小的正方形。

在上述指令中，冒号是 Logo 语言的语法之一，表示其后紧跟的词是一个参数的名称，而且这个词表示的含义与冒号前的词有所不同。在这个例子中，冒号是指调用「SQUARE」子程序时所提供的一个参与值。当定义好「SQUARE」之后，指令「SQUARE15」会指示计算机画出一个边长为 15 个单位的正方形。同样，这里的参数名称「SIZE」也是任取的，但它只有在指令「SQUARE」中才有意义。如果上述指令中的「SIZE」被字母「X」替代，那么这个子程序的功能将与原先完全相同。

编写正方形的子程序不止一种。例如，我们可以命令海龟向左转 4 次或者向后转 4 次来画出一个正方形。有趣的是，「SQUARE」指令的定义方式并不重要，它所绘制的内容以及将海龟置于何处才是关键所在。无论「SQUARE」是如何被定义的，以及它是否属于用户自定义的指令或者程序原语之一，其他程序都能调用这个指令。在扩展编程语言的过程中，程序员可以通过功能抽象的方法来创造新的构件。

在学习 Logo 语言时，小孩还会发现一个诀窍，那就是在指令的定义中插入这个指令本身，这被称为递归。例如，小孩可以设计出一个由许多旋转的正方形组成的循环指令：「DESIGN」，即设计（见图 3-4）。

图 3-4 指令「DESIGN」的执行过程

当计算机接收到指令「DESIGN」后，首先会画出一个正方形，然后将海龟右转 10 度，并以同样的方式执行下一个指令「DESIGN」。在这种情况下，指令「DESIGN」的递归定义存在一个问题：它将会永远地执行下去。计算机每次接收到指令「DESIGN」后都会画出一个正方形，然后执行下一个指令「DESIGN」，这是一个不断循环往复的过程。一位智者曾说：「地球驮在一只巨大的海龟的背上。」「那么是什么支撑着这只海龟呢？」有一个学生提出了疑问。「另一只海龟。」大师答道。「那么又是什么支撑着这一只海龟呢？」学生又问道。「这种追问没有意义，」大师说道，「海龟下面永远是海龟。」

计算机执行指令「DESIGN」的过程，就如同无穷多个巨大的海龟堆叠在一起的情形，因为计算机不够智能，它无法预知这是一个永无止境的过程。在这个程序被中断之前，它会一直运行下去。这个例子反映了计算机程序的一种常见特征 —— 无限循环。在通常情况下，程序员一不留神就会让程序陷入无限循环，而提前预判出何时会出现这种循环，则极其困难（我们会在后面章节详细讨论这一点）。不过，若想避免这种情况也不难，只要在程序中增加一个用于指定正方形数目的参数即可。

通过上面的定义，「DESIGN」程序会根据参数是否为 1 或者大于 1 来执行如下两项操作中的一个。指令「DESIGN1」只会画出一个正方形，而指令「DESIGN5」会先画出一个正方形，然后旋转，再执行指令「DESIGN4」。指令「DESIGN4」也会先画出一个正方形，然后再执行指令「DESIGN3」，以此类推，直至执行完指令「DESIGN1」，程序才终止。

这种带可变参数的递归定义可用于生成具有自相似结构的对象。一张包含自身图像的图像就是一种具有自相似结构的示例。这类结构通常被称为分形（fractal）。在现实世界中，自相似结构不会永远递归下去。例如，虽然树的每个分支看起来像一棵较小的树，而且这些分支的分支看起来像更小的树，但这种递归过程只会重复几次，最终的分支会非常小，不会再产生新的分支。

图 3-5 表示的是可以绘制树的递归 Logo 程序。这个程序会让你体验到计算机程序中蕴含的诗意，即屏幕上移动的海龟及其最后返回起点的画图方式在一定程度上模糊了这一主题。这段程序表达的大致意思是：「大树，一个上面长出两棵小树的主干；小树，一个主干而已。」

图 3-5　用递归 Logo 程序绘制的树

这种递归定义事物的技术具有很强大的功能。我们要处理的许多数据类型都具有递归结构，尤其是计算机程序本身。递归定义十分便于描述递归数据运算。典型的递归定义包含两个部分：第一部分描述了简单情形的运算，第二部分描述了如何将复杂的情形转化为更简单的情形。例如，在递归树的例子中，最简单的情形是参数小于 1 时的树，复杂的情形则是由树干和两个分支组成的树。

回文的定义是递归定义的另一个例子，其定义为：如果某个词的字母数少于两个，或者这个词的首字母和尾字母相同，且中间字母也是回文（递归定义），那么这个词就是回文。若想编写 Logo 程序来识别回文，最简单的方法就是使用这种递归定义。

计算机编程语言还包括 LISP、Ada、FORTRAN、C、ALGOL 等语言，其中大多数名称源于英文首字母的缩写。例如，FORTRAN 是 FORmula TRANslation 的缩写，LISP 是 LIST Processing 的缩写。尽管这些编程语言在词汇和语法等细节上与 Logo 语言有所不同，但它们都可以定义相同类型的程序。有些编程语言在定义递归运算和处理非数值数据方面的能力有所欠缺，例如 FORTRAN。有些编程语言允许程序员直接处理二进制表示的数据，这赋予了程序员更大的权力，但同时也增加了犯错误的可能性，比如 C 和 LISP。例如，在 C 语言中，虽然将两个字符变量相乘是可行的，但这一操作不具有实际意义，其结果取决于计算机使用的二进制编码方式。像 LISP 这样的编程语言不仅具备低级功能，还具备抽象功能。计算机学者盖伊·斯蒂尔（Guy Steele）曾说过：「LISP 是一种高级编程语言，不过，你依然可以在指尖间感受到滑动的二进制位。」

新一代编程语言已经崭露头角，它们都是面向对象的，比如 Small-Talk、C++、Java。这些编程语言都将数据结构当作一个具有自身内部状态的「对象」，例如将在屏幕上绘制的图片，这些内部状态包含图片的位置、颜色等属性。这些对象可以接收来自其他对象的指令。我们通过下面这个例子来了解这种方法的有效性。假设你正在编写一款涉及弹跳球的图示游戏，屏幕上的每个球都被定义为不同的对象。该程序规定了弹跳球的行为准则，并明确了对象如何在屏幕上显示、移动、反弹，以及与游戏中其他对象交互。每个球虽然会呈现出相似的行为模式，但所处的状态略有不同，这是因为每个球在屏幕中有其自身的位置、颜色、速度、大小等。

面向对象的编程语言最突出的优点是：对象可以被单独定义并组合成新程序，如图示游戏中的各种对象。编写一个面向对象的新程序的过程，就如同将一群动物关进一个笼子中，并观察发生的事情。编程对象之间的交互作用造就了程序的行为。由于这个原因，加上面向对象的编程语言相对较新，因此你在用它编写安全第一的飞机自动驾驶系统时，要三思而行。

学习编程语言并不像学习人类语言那样困难。一般来说，一旦你学会了两三门编程语言，就能在几小时内掌握其他的编程语言。这其中的原因在于，编程语言的语法相对简单，词汇量很少超过几百个单词。不过，就像学习人类语言一样，理解了编程语言并不意味着就能将其用于实践。每种计算机编程语言的领域都有相应的大师，阅读这些大师的代码是一种享受。写得好的代码自有其风格和技巧，甚至幽默，也可能具有优美散文般的清澈明朗。

### 3.2 Making the Connection

How can finite-state machines be used to carry out instructions written in a language like Logo? To answer this question, we go back to a more detailed level of discussion, involving Boolean logic. There are three major steps in this connection between finite-state machines and Logo: first , we will see how a finite-state machine can be extended, by adding a storage device called a memory , which will allow the machine to store the definitions of what it's asked to do; second , we will see how this extended machine can follow instructions written in machine language , a simple language that specifies the machine's operations; and third , we will see how machine language can instruct the machine to interpret the programming language — for instance, Logo. The rest of the chapter describes how all this works in some detail — far more detail than is strictly necessary to understand the rest of the book. The reader should not feel compelled to understand every step. The important thing to appreciate is how the layers of functional abstraction build upon one another, as is summarized in the last paragraph of the chapter.

A computer is just a special type of finite-state machine connected to a memory. The computer's memory — in effect, an array of cubbyholes for storing data — is built of registers , like the registers that hold the states of finite-state machines. Each register holds a pattern of bits called a word , which can be read (or written) by the finite-state machine. The number of bits in a word varies from computer to computer, but in a modern microprocessor (as I write this) it is usually eight, sixteen, or thirty-two bits. (Word sizes will probably grow with improvement in technology.) A typical memory will have millions or even billions of these registers, each holding a single word. Only one of the registers in the memory is accessed at a time — that is, only the data in one of the memory registers will be read or written on each cycle of the finite-state machine. Each register in the memory has a different address  — a pattern of bits by means of which you can access it — so registers are referred to as locations in memory. The memory contains Boolean logic blocks, which decode the address and select the location for reading or writing. If data are to be written at this memory location, these logic blocks store the new data into the addressed register. If the register is to be read, the logic blocks steer the data from the addressed register to the memory's output, which is connected to the input of the finite-state machine.

Some of the words stored in the memory represent data to be operated upon, like numbers and letters. Others represent instructions that tell the machine what sequence of operations to perform. The instructions are stored in machine language, which, as noted, is much simpler than a typical programming language. Machine language is interpreted directly by the finite-state machine. In the type of computer we will describe, each instruction in machine language is stored in a single word of memory, and a sequence of instructions is stored in a block of sequentially numbered memory locations. These sequences of machine-language instructions are the simplest kind of software within the computer.

The finite-state machine repeatedly executes the following sequence of operations: (1) read an instruction from the memory, (2) execute the operation specified by that instruction, and (3) calculate the address of the next instruction. The sequence of states necessary to do this is built into the Boolean logic of the machine, and the instructions themselves are specific patterns of bits — patterns that cause the finite-state machine to perform various operations on the data in the memory. For instance, the Add instruction is a unique pattern of bits that specifies which two registers in the memory are to be added together. Upon recognizing this pattern, the finite-state machine will go through a sequence of states that cause it to read the memory locations to be summed, add the numbers together, and write the sum back to the memory.

FIGURE 22

Finite-state machine connected to a memory

There are two basic types of instructions in most computers: processing instructions and control instructions. The processing instructions move data to and from the memory and combine them to perform arithmetic and logical functions. The addresses of the memory locations, or registers, are specified by the processing instructions. Typically, these instructions refer to only a few registers directly; other registers are referenced indirectly, because their addresses are stored in other registers. For example, a Move instruction might move the data in register 1 to the address specified in register 2. If register 2 holds a pattern of bits that specifies the number 1,234, then the data will be moved to register 1,234. Other processing instructions combine data among the memory registers. There are also instructions to perform Boolean functions — And, Or, or Invert — on the patterns of bits in the registers.

The control instructions determine the address of the next instruction to be fetched; this address is stored in a special register called the program counter. Normally, instructions are fetched sequentially from successive memory locations, so the address in the program counter increases by 1 after each successive instruction. Control instructions allow some other number to be loaded into the program counter, thereby affecting the sequence to be executed. The simplest control instruction is the Jump instruction, which stores a specified address in the program counter so that the next instruction will be fetched from that address. A variation of the Jump instruction is a conditional Jump , which loads the program counter with a different address only when a specified condition has been met — such as the patterns in two registers being the same. If the condition is not met, then the conditional Jump will have no effect and the next instruction will be fetched sequentially.

If the same sequence of instructions needs to be executed over and over repeatedly, then a conditional Jump can be used at the end of the sequence to move the program counter back to the beginning as many times as is necessary. This operation is called a loop , and we saw an example of it in the description of programming in Logo. The execution of the sequence will be repeated until the condition on which the jump depends is no longer satisfied. If a set of instructions is to be repeated ten times, say, one of the memory registers can be used to count the number of iterations of the loop.

Exactly which instructions a computer recognizes varies from computer to computer. Computer designers can (and do) spend years arguing about what makes an optimal instruction set. A typical argument is over the comparative merits of a reduced instruction set computer (RISC), which uses a simple, minimal set of instructions, and a complex instruction set computer (CISC), which employs a rich, complex, and powerful set of instructions. This argument has little import to the programmer, however, since any reasonable instruction set can simulate any other. Historically, the commercial success of one or another sort of computer seems to have had almost nothing to do with the complexity of the instruction set or any other detail of internal design. In fact, some of the most successful computers — such as the microprocessors used in most personal computers — are generally regarded by computer designers as having poorly designed instruction sets. The details of machine design are of little importance to the users of the machines.

One reason the complexity of the instruction set doesn't much matter has to do with the subroutines. Subroutines allow sequences of instructions to be used over and over from many places within the program. In effect, the subroutine-calling convention allows the programmer to define new instructions by using sequences of other instructions. The program accesses a subroutine by using a Jump instruction to load the program counter with the address of the subroutine; but before doing so, the computer saves the previous contents of the program counter in a special memory location. At the end of the subroutine, another instruction reads this return address and jumps back to the location from which the subroutine was called.

This process of subroutine calling can work recursively, in the sense that subroutine sequences may have jumps to other subroutines within them, and so on. A subroutine can even call itself, in a recursively defined function. In order to keep track of this nesting of subroutines, the computer needs a systematic way of storing the return addresses, so that it will know where to return when each subroutine is completed. It cannot just store all the return addresses in the same special location, because when subroutines are nested, it needs to remember more than one return address. Normally, the computer stores return addresses in a group of sequential locations known as a stack. The most recent return address is stored at the「top of the stack.」The memory stack works just like a stack of dinner plates: items are always added or removed from the top — a last-in, first-out storage system that works perfectly for storing the return addresses of nested subroutines, because a subroutine is never finished until all of its nested subroutines are finished.

Some subroutines are so useful that they are always loaded into the computer. This set of subroutines is called the operating system. Useful operating-system subroutines include those that write or read characters typed on the keyboard, or that draw lines on the screen, or otherwise interact with the user. The computer's operating system determines most of the look and feel of the interface to the user. It also governs the interface between the computer and whatever program is being run, since the operating system's subroutines provide the program with a set of operations that are richer and more complex than the machine-language instructions.

In fact, as long as the same pattern of bits produces the same effect, the programmer doesn't care whether a function is implemented by the computer hardware or by the operating-system software. The same program operating on two different types of computers might in one case perform an arithmetical operation in the hardware and in the other perform it by means of an operating-system subroutine. Similarly, the operating system of one type of computer may allow it to emulate the entire instruction set of another type of computer. Computer manufacturers sometime use such emulation to make the newer model of their computers act like the earlier models, so that older software can run without modification.

The operating system normally includes all the subroutines that perform input/output — that is, operations allowing a program to interact with the outside world. This interaction is effected by connecting certain locations in the computer's memory to input devices such as a keyboard or a mouse and output devices such as a video display terminal. For example, the space bar on the keyboard might be wired to memory register 23, so that the data read from address 23 is 1 if the space bar is pressed and 0 if it is not. Another memory register might control the color displayed on a certain dot on the screen. If every dot on the screen displays data stored in a different memory location, the computer can draw any pattern on the screen just by writing the appropriate pattern into memory.

With the exception of its input/output mechanisms, the computer we've just described is simply a finite-state machine connected to a memory. Both these elements can be constructed entirely from registers and Boolean logic blocks, using the techniques described in chapters 1 and 2. The finite-state machine that controls the computer is complicated, but it is no different in principle from the finite-state machine that controls a traffic light. Designing the machine is simply a matter of going through the details of memory data, address, and state sequences for each instruction to be executed, and then converting this state table into Boolean logic. Recall that since both the finite-state machine and the memory are made of registers and blocks of logic, both can be implemented by a number of technologies: electronics, hydraulics, sliding sticks.

建立连接关系

如何使用有限状态机来执行用 Logo 等语言编写的指令呢？布尔逻辑能为这个问题提供答案。我们可以通过三个主要步骤在有限状态机和 Logo 程序之间建立连接。第一，给有限状态机加入一个名为内存的存储装置，它可以扩展有限状态机，这样，有限状态机就可以通知它存储要求完成的操作指令；第二，这个扩展后的有限状态机会执行用机器语言编写的指令，机器语言可以直接指定机器的动作；第三，机器语言将指导计算机解释编程语言（如 Logo）。本章的其余内容将会详细讲述上述过程是如何进行的，而且其详细程度将会远远超出理解本书其他内容之所需。因此，读者无须强迫自己理解所有的步骤，重要的是理解功能抽象的层次结构是如何构建起来的，本章最后一段总结了这一点。

实际上，计算机只是一种带有内存的特殊有限状态机（见图 3-6）。计算机的内存由寄存器构成，前者是用于存储数据的一列数组，就如同保存有限状态机状态的寄存器。每个寄存器保存一组二进制位，称为计算机字，有限状态机可以直接读取（或者写入）。一个计算机字包含的二进制位数因计算机而异，现代微处理器的二进制位数一般为 8 位、16 位或者 32 位。随着技术的进步，计算机的字长很可能会增加。常规的内存中包含的寄存器数目可达数百万甚至数十亿个，其中每个寄存器只存储一个计算机字。计算机每次只能访问内存中的一个寄存器，也就是说，有限状态机在每个周期中只能读取或者写入一个寄存器中的数据。内存中的每个寄存器都有一个不同的地址，即一组二进制位，用于存取寄存器，因此寄存器也被称为存储单元。内存中还包含布尔逻辑块，它们可以解码寄存器并选择数据读取或者写入的位置。如果在一个寄存器中写入数据，布尔逻辑块就会将新数据存储到该位置对应的寄存器中；如果要从寄存器中读取数据，这些布尔逻辑块就会将数据从该寄存器转移至内存的输出，该输出与有限状态机的输入相连。

图 3-6　与内存相连接的有限状态机

存储在内存中的某些计算机字都是将要被处理的数据，比如数字和字母，有些则是有限状态机将要执行的指令序列。这些指令以机器语言的形式存储，如上所述，它们比常规的编程语言简单得多。有限状态机可以直接翻译并执行机器语言。在这里所描述的计算机中，机器语言记录的每个指令都存储在内存的单独一个计算机字中，指令序列则存储在由按顺序编号的存储单元组成的块中，这些机器语言指令序列是计算机中最简单的一种软件。

有限状态机会反复执行这种运算序列：首先，从内存中读取一条指令；然后，执行这条指令规定的运算；最后，计算下一条指令的地址。有限状态机的布尔逻辑块中内置了执行该运算的状态序列。每个指令本身是一组具有特殊模式的二进制组，它们能驱动有限状态机对内存中的数据执行各种操作。比如，加法指令就是一类特殊的二进制组，它可以对内存中某两个寄存器的数据执行加法运算。在识别出加法指令后，有限状态机将会进行一系列状态转换，并完成这些运算：从内存地址中读取加数，然后对两个加数求和，最后将结果写回内存。

大多数计算机中的指令分为两种基本类型：处理指令和控制指令。处理指令可以从内存中读取和写入数据，并会组合数据以完成算术和逻辑运算。存储单元或者寄存器通常由处理指令来设定。通常而言，处理指令能够直接访问的寄存器只有少数几个，其余寄存器都是通过间接的方式被访问的，因为它们的地址存储在其他寄存器中。例如，一个 Move（传送）指令会将寄存器 1 中的数据移动至寄存器 2 所指定的地址。如果寄存器 2 存储的一组二进制位代表的数字为 1234，那么该数据就会被移动至寄存器 1234 中去。其他的处理指令也会将不同寄存器之间的数据组合起来。还有一些处理指令可以对寄存器中的二进制位组执行布尔运算，比如逻辑块「与」「或」「非」等。

控制指令确定了将取出的下一条指令的地址。该地址存储在被称为程序计数器的特殊寄存器中。在通常情况下，指令是按顺序从连续的存储单元中取出的。因此，每取出一个指令，程序计数器中的地址就会加 1。控制指令允许将其他数字加载至程序计数器中，进而改变将要执行的指令序列。最简单的控制指令是 Jump（转移）指令，它将特定的地址存入程序计数器中，然后从这个新地址中获取下一条指令。Jump 指令的变体为条件 Jump 指令，即只有当某个条件得到满足时，比如两个寄存器中的数据相等，才会将另一个地址写入程序计数器中。如果条件不满足，那么条件 Jump 指令就不会生效，下一条指令仍按原顺序获取。

如果需要反复执行相同的指令序列，则可以在指令序列结束时加入一个条件 Jump 指令，使程序计数器返回开始处，这样便可周而复始，执行任意多次。这种运算方式被称为循环，我们已经在介绍 Logo 编程语言时举过一例了。如果需要将指令序列重复执行 10 次，则可以用一个寄存器记录循环迭代的次数。

不同型号的计算机可以识别的指令有所不同。多年来，计算机设计者一直在争论，什么样的指令集最好。其争论的焦点在于以下两种指令集哪种的优点更明显。一种是精简指令集计算机（RISC），其指令集的功能比较简单，数目最少；另一种是复杂指令集计算机（CISC），其指令集的数目较多，功能强大且复杂。不过，关于这两种指令集的争论并不会影响到程序员的设计，因为任意一种合理的指令集都可以模拟出任何其他的指令集。从过往的经验来看，某种类型的计算机在商业上的成功似乎与其指令集的复杂度或内部设计细节没有关系。实际上，在计算机设计者看来，一些最成功的指令集设计得并不好，比如大多数个人计算机所用的微芯片。计算机的设计细节对计算机用户来说并不重要。

指令集的复杂度无关紧要的一个原因与子程序有关。子程序允许指令序列可以在程序的许多位置被反复使用。实际上，程序员可以通过调用子程序来使用其他指令序列定义新指令。程序通过 Jump 指令来调用子程序，这个 Jump 指令能够将子程序的地址写入程序计数器中；在此之前，计算机会预先将程序计数器中的原先内容保存至一个专门的内存地址中。当子程序结束后，另有一条指令会读取该返回地址，并转回至原程序调用时的位置。

调用子程序的这一过程可以递归执行，也就是说，子程序序列可包含转向自身中子程序的 Jump 指令，以此类推。在以递归方式定义的函数中，子程序甚至可以调用自己。为了跟踪子程序的嵌套调用过程，计算机需要一种保存返回地址的系统化方法，以便子程序在结束时知道返回的位置。然而，将所有返回地址保存在同一特殊位置并不可行，因为嵌套调用子程序时需要记录的返回地址不止一个。通常，计算机会将返回地址存储在一组被称为堆栈的连续地址中。最新的返回地址则存储在「栈顶」。内存堆栈的工作原理类似于一叠盘子，其添加和移除工作都在顶部进行。这是一种后进先出的存储系统，它完美地适配了嵌套子程序返回地址的存储过程，因为一个子程序在其所有嵌套子程序全部执行完毕之前是不会结束的。

有些子程序的作用不可或缺，因此一直装在计算机中。这类子程序的集合被称为操作系统。操作系统子程序的功能包含读取键盘上键入的字符、在屏幕上显示线条，以及与用户交互等。计算机的操作系统决定了用户界面的大部分外观和体验，它也是负责管理计算机与运行程序之间的接口，因为操作系统的子程序能给程序提供比机器语言指令更丰富、更复杂的操作集合。

实际上，只要相同的一组二进制位产生相同的效果，程序并不在乎功能实现的途径是计算机硬件还是操作系统（软件）。当同一个程序运行在两台不同类型的计算机上时，一台计算机可能通过硬件来完成运算，而另一台则通过操作系统来完成运算。同样，同一型号的计算机的操作系统可以模拟出另一种型号的计算机的所有指令集。计算机制造商有时会用这种模拟方法使新旧型号的计算机保持一致，这样就无须修改旧版软件，即可直接运行。

操作系统通常包括执行输入和输出功能的所有子程序，也就是说，程序通过这些功能与外界进行交互。通过将计算机内存中的某些地址与诸如键盘、鼠标等输入装置，以及诸如视频显示终端等输出装置相互连接起来，我们便可以实现这种交互功能。例如，如果键盘上的空格键与寄存器 23 相连，那么当按下空格键时，从寄存器 23 中读取到的数字是 1，反之则为 0。某个寄存器可能控制着屏幕上某一像素点的显示色。如果屏幕上每个点显示的颜色数据存储在不同的内存地址中，那么计算机只需向内存中写入合适的图像数据，即可在屏幕上显示与之对应的图案。

除了输入和输出机制之外，我们上面所讲的计算机只是一个简单的、与内存相连的有限状态机，完全可以借助第 1 章和第 2 章中提到的技术，用寄存器和布尔逻辑块组装而成。虽然控制计算机的有限状态机非常复杂，但从原理上来说，它与控制交通信号灯的有限状态机并无区别。计算机的设计就是去规划每一条指令涉及的内存数据、地址和状态序列等详细信息，然后用布尔逻辑实现这个状态表。有限状态机和内存都是由寄存器和逻辑块组成的，因此这两者都可以通过电子技术、液压技术和滑动杆等多种方法来实现。

### 3.3 Translation The Language

So we have established a chain of connections between the technology and the instructions. But how do the instructions execute a program written in a language — Logo, for instance —  when that language is written in words and the instructions are patterns of bits? The answer is that the necessary translation is performed by the computer itself.

The translation process performed by the computer is similar to the process that a patient, meticulous human translator would use to translate a document written in an unfamiliar language, given a dictionary written in the language itself. The human translator can look up the meaning of any unknown word in the dictionary, and if words in the dictionary definition are also unknown, these words can be looked up as well. This process continues until the translator reaches a definition couched in words whose meanings are known. In this analogy, the translator's (that is, the computer's) dictionary is the program, and the words known to the computer are the aforementioned primitives of the program language. These primitives are defined directly, as simple sequences of machine instructions. For instance, when the computer looks up the definition of the Logo language primitive FORWARD, it finds the sequence of machine instructions that will draw the appropriate line on the screen.

To understand how a computer translates Logo primitives into machine language, it is helpful to understand the conventions that a computer uses to represent the Logo programs within its memory. One way to store a Logo program in a computer's memory is as a sequence of characters in adjacent memory locations, with each character being stored at a single location. In its memory, the computer keeps a directory of the addresses of the instruction sequences corresponding to each command name. This directory is stored in memory as a list of names paired with their addresses. The computer is able to find the location of an object with a given name by searching the directory for the name and finding the corresponding address. When the computer is asked to execute a particular command, it looks up the name in the directory to find out where its definition is stored.

Some of this process of looking things up and finding the corresponding sequences of machine language can be done before the program is executed. This saves time, because if the program is going to be executed more than once, there's no point in looking up the same things over and over again. When most of the work of conversion is done beforehand, the translation process is called compilation , and the program that performs the compilation is called a compiler. If most of the work is done while the program is being executed, then the process is called interpretation, and the program is called an interpreter. There is no hard and fast line between the two.

翻译语言

到目前为止，我们已经在技术和指令之间建立了一系列连接。程序由词汇写成，指令由二进制位组构成。那么，在这种情况下，机器指令如何执行用编程语言（例如 Logo）编写的程序呢？答案在于计算机执行翻译的过程。

计算机执行翻译的过程和人类语言的翻译过程类似。假设有一名耐心细致的翻译员正在翻译一份用陌生的语言编写的文档，并且所使用的字典也是用这种陌生的语言编写的。当他碰到未知单词时，可以查询字典，如果在词语的定义中又碰到了未知单词，可以继续查询字典。这个过程可以持续地进行下去，直到这名翻译员能读懂定义中所有词语的含义。在这个例子中，翻译员的字典相当于计算机程序，计算机能读懂的词语则相当于前面我们提到的编程语言的原语。这些原语被直接定义为简单的机器指令序列。例如，当计算机查询 Logo 语言中「FORWARD」原语的定义时，就会找到可以在屏幕上画直线的机器指令序列。

若想了解计算机如何将 Logo 语言中的原语翻译成机器语言，你最好先了解一下计算机在内存中表示 Logo 程序的方法。在计算机内存中存储 Logo 程序的一种方法是，将程序字符存入一段连续的内存地址中，且每个内存地址中只存储一个字符。计算机内存中保存有一份对应于指令名称的指令序列的地址表。这份地址表存储于内存中，而且在地址表中，指令名称和指令序列是一一对应的。对于给定名称的指令，计算机可在表中查询该名，找到它的地址，进而找到具有此名的对象的存储单元。当计算机执行某个特定命令时，就会在地址表中查找这个命令的名称，并会找到其定义的存储地址。

在程序执行之前，计算机就可以完成查找程序对应的机器指令序列的过程。这一操作很节省时间，因为一个程序不只执行一次，同样的查询没有必要重复多次。如果大部分翻译工作在程序执行前便已完成，那么这类翻译就被称为编译，完成上述编译过程的程序被称为编译器。如果大部分翻译工作是边执行程序边进行的，那么这类翻译被称为解释，相应的程序被称为解释器。这两者之间并无一条明确的界线。

### 3.4 Welcome to The Hierarchy

We are now in a position to summarize how a computer works, from top to bottom. Most readers will have lost track of the details, but remember that it is not important to remember how every step works! The important thing to remember is the hierarchy of functional abstractions.

The work performed by the computer is specified by a program , which is written in a programming language. This language is converted to sequences of machine-language instructions by interpreters or compilers , via a predefined set of subroutines called the operating system. The instructions, which are stored in the memory of the computer, define the operations to be performed on data, which are also stored in the computer's memory. A finite-state machine fetches and executes these instructions. The instructions as well as the data are represented by patterns of bits. Both the finite-state machine and the memory are built of storage registers and Boolean logic blocks , and the latter are based on simple logical functions , such as And, Or , and Invert. These logical functions are implemented by switches , which are set up either in series or in parallel , and these switches control a physical substance, such as water or electricity, which is used to send one of two possible signals from one switch to another: 1 or 0. This is the hierarchy of abstraction that makes computers work.

层次结构

现在，我们可以对计算机的工作原理做一个完整的总结了。虽然大多数读者总是很容易忘却具体的细节，但对于计算机的工作原理来说，记住每个细节并无必要，重要的是记住功能抽象的层次结构。

程序规定了计算机执行的任务，前者是由编程语言编写的。通过一组被称为操作系统的预先定义好的子程序，解释器或者编译器会将编程语言转换为机器语言指令序列。这些指令序列存储于计算机的内存中，并且可以操作存储于内存中的数据。有限状态机可以读取并执行这些指令。这些指令和数据都以二进制位的形式存在。有限状态机和内存都由寄存器和布尔逻辑块构成，布尔逻辑块基于「与」「或」「非」这些简单的逻辑功能构建而成，而这些逻辑功能可以通过开关来实现。开关以串联或者并联的方式相连，控制着某种物理介质，比如水、电等，而这些物理介质在开关之间传递着两种可能的信号之一，即 1 或 0。这就是计算机得以运行的功能抽象的层次结构。

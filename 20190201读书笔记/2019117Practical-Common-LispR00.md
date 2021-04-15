## 记忆时间

## 基本信息

Copyright © 2005 by Peter Seibel

[Learn Common Lisp | Common Lisp](https://lisp-lang.org/learn/)

[Common Lisp Books | Common Lisp](https://lisp-lang.org/books/#practical-common-lisp)

电子书及源码：[Practical Common Lisp](http://www.gigamonkeys.com/book/)

作者的博客：[gigamonkeys](http://www.gigamonkeys.com/)

## 卡片

### 0101. 主题卡 —— emacs 的高频操作

[https://www.gnu.org/software/emacs/](https://www.gnu.org/software/emacs/manual/html_node/emacs/index.html#SEC_Contents)

1、切换到 lisp 交互界面的 buffer。`C-c C-z`，即先按住 ctrl 再按 c，然后松手，接着按住 ctrl 再按 z。

2、切换 buffer。`C-x b`，先按住 ctrl 再按 x，然后松手，接着按 b。接着对底部会出现所有的 buffer，打几个字母 tab 补全到想要切换的 buffer 即可。

3、新建文件。`C-x C-f`，底部会弹出目录，比如 `~/portacle/projects/` 补一个没有的文件，比如 `~/portacle/projects/test.lisp` 然后按回车，会新建一个「test.lisp」文件。接着保存文件 `C-x C-s`。

4、编译文件里的函数。写好函数后，在该函数所在文件的 buffer 下，用命令 `C-c C-c` 来编译，编译通过的话最下面会有提示编译完成。然后用命令 `C-c C-z` 切换到 lisp 交互界面，输入命令 `(testname)` 即可调用该函数。

5、重启 lisp 交互界面。在交互界面里输入逗号 `,`，底部会显示让你输入命令，输入 `quit` 即可退出 lisp 交互界面。接着重新启动，输入命令 `M-x slime`，即按住 command 再按 x，接着输入 slime，按回车即可启动 SLIME 界面（lisp 交互界面）。

6、退出 debugger 的界面，按 `q`。

7、在 lisp 交互界面里加载 lisp 文件。直接输入命令 `(load "test.lisp")`，交互界面返回 T 的话说明成功加载了，然后可以直接调用加载后的函数。知道这个操后后，完全可以在 vscode 里编写代码，然后直接在 lisp 交互界面里编译运行，太赞了。

8、退出整个 emac，输入命令 `C-x C-c`。

### 0102. 主题卡 —— lisp 里数组过滤函数的实现

1『太重要了，升级为主题卡，哈哈。（2020-10-27）』

Now suppose you want to wrap that whole expression in a function that takes the name of the artist as an argument. You can write that like this:

```c
(defun select-by-artist (artist) 
  (remove-if-not 
    #'(lambda (cd) (equal (getf cd :artist) artist)) 
    *db*
  )
)
```

Note how the anonymous function, which contains code that won't run until it's invoked in REMOVE-IF-NOT, can nonetheless refer to the variable artist. In this case the anonymous function doesn't just save you from having to write a regular function -- it lets you write a function that derives part of its meaning -- the value of artist -- from the context in which it's embedded.

1-2-3『

看到这里才意识到 `remove-if-not` 就是用来构造过滤函数的啊，这正是自己之前 PHP 里用的最多的 `array_filter` 函数，试着在 autolisp 的文档里搜了下，发现果然有 `vl-remove-if-not`，有了它的话，自己很多很多的功能开发都可以基于它变得简洁优雅，简直是捡到金子了，哈哈。做一张术语卡片。（2020-10-22）

[vl-remove-if-not (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-53D12042-8DE3-4DAA-83BD-8ABB376ACA97)

Returns all elements of the supplied list that pass the test function.

```c
(vl-remove-if-not predicate-function lst)
```

predicate-function. Type: Subroutine or Symbol. The test function. This can be any function that accepts a single argument and returns T for any user-specified condition. The predicate-function value can take one of the following forms:

```c
A symbol (function name)
'(LAMBDA (A1 A2) ...)
(FUNCTION (LAMBDA (A1 A2) ...))
```

lst. Type: List. A list to be tested.

Return Values. Type: List or nil.

A list containing all elements of lst for which predicate-function returns a non-nil value

```c
(vl-remove-if-not 'vl-symbolp (list pi t 0 "abc"))
(T)
```

自己写了个例子：

```c
(vl-remove-if-not 
  '(lambda (x) (= x 2)) 
  '(1 2 3 4)
)
```

返回元素为 2 的列表 `(2)`。

vl-remove-if (AutoLISP). Returns all elements of the supplied list that fail the test function.

```c
(vl-remove-if 'vl-symbolp (list pi t 0 "abc"))
(3.14159 0 "abc")
```

vl-remove (AutoLISP). Removes elements from a list.

```c
(vl-remove element-to-remove lst)
```

element-to-remove. Type: Integer, Real, String, List, File, Ename (entity name), T, or nil. The value of the element to be removed; may be any LISP data type.

lst. Type: List. Any list.

Return Values. Type: List or nil. The lst with all elements except those equal to element-to-remove.

```c
(vl-remove pi (list pi t 0 "abc"))
(T 0 "abc")
```

vl-member-if-not (AutoLISP). Determines if the predicate is nil for one of the list members.

```c
(vl-member-if-not predicate-function lst)
```

predicate-function. Type: Subroutine or Symbol. The test function. This can be any function that accepts a single argument and returns T for any user-specified condition. The predicate-function value can take one of the following forms:

Return Values. Type: List or nil. A list, starting with the first element that fails the test and containing all elements following this in the original argument. If none of the elements fails the test condition, vl-member-if-not returns nil.

Remarks: The vl-member-if-not function passes each element in lst to the function specified in predicate-function. If the function returns nil, vl-member-if-not returns the rest of the list in the same manner as the member function.

```c
(vl-member-if-not 'atom '(1 "Str" (0 . "line") nil t))
((0 . "line") nil T)
```

1「函数 `vl-member-if-not` 目前没吃透，不过直觉上感觉有大用途。（2020-10-22）」

』

### 0103. 主题卡 —— 函数当作数据

While the main way you use functions is to call them by name, a number of situations exist where it's useful to be able treat functions as data. For instance, if you can pass one function as an argument to another, you can write a general-purpose sorting function while allowing the caller to provide a function that's responsible for comparing any two elements. Then the same underlying algorithm can be used with many different comparison functions. Similarly, callbacks and hooks depend on being able to store references to code in order to run it later. Since functions are already the standard way to abstract bits of code, it makes sense to allow functions to be treated as data. 9

1-2『编程语言里，能把函数当作数据，个人感觉太有必要了，将函数作为参数传进另一个函数，构建复杂的模型。函数作为数据，做一张主题卡。（2020-10-28）』——已完成

In Lisp, functions are just another kind of object. When you define a function with DEFUN, you're really doing two things: creating a new function object and giving it a name. It's also possible, as you saw in Chapter 3, to use LAMBDA expressions to create a function without giving it a name. The actual representation of a function object, whether named or anonymous, is opaque -- in a native-compiling Lisp, it probably consists mostly of machine code. The only things you need to know are how to get hold of it and how to invoke it once you've got it.

The special operator FUNCTION provides the mechanism for getting at a function object. It takes a single argument and returns the function with that name. The name isn't quoted. Thus, if you've defined a function foo, like so:

```c
CL-USER> (defun foo (x) (* 2 x)) 
FOO
```

### 0104. 主题卡 —— 语言编译过程

Before we look at the specifics of Lisp's syntax and semantics, it's worth taking a moment to look at how they're defined and how this differs from many other languages.

In most programming languages, the language processor -- whether an interpreter or a compiler -- operates as a black box: you shove a sequence of characters representing the text of a program into the black box, and it -- depending on whether it's an interpreter or a compiler -- either executes the behaviors indicated or produces a compiled version of the program that will execute the behaviors when it's run.

Inside the black box, of course, language processors are usually divided into subsystems that are each responsible for one part of the task of translating a program text into behavior or object code. A typical division is to split the processor into three phases, each of which feeds into the next: a lexical analyzer breaks up the stream of characters into tokens and feeds them to a parser that builds a tree representing the expressions in the program, according to the language's grammar. This tree -- called an abstract syntax tree -- is then fed to an evaluator that either interprets it directly or compiles it into some other language such as machine code. Because the language processor is a black box, the data structures used by the processor, such as the tokens and abstract syntax trees, are of interest only to the language implementer.

1-2『这里的信息让自己对语言的运行时、编译过程有了更多的认识，但其中不少东西没吃透，先做一张主题卡。（2020-12-30）』——已完成

In Common Lisp things are sliced up a bit differently, with consequences for both the implementer and for how the language is defined. Instead of a single black box that goes from text to program behavior in one step, Common Lisp defines two black boxes, one that translates text into Lisp objects and another that implements the semantics of the language in terms of those objects. The first box is called the reader, and the second is called the evaluator. 2

Each black box defines one level of syntax. The reader defines how strings of characters can be translated into Lisp objects called s-expressions. 3 Since the s-expression syntax includes syntax for lists of arbitrary objects, including other lists, s-expressions can represent arbitrary tree expressions, much like the abstract syntax tree generated by the parsers for non-Lisp languages.

The evaluator then defines a syntax of Lisp forms that can be built out of s-expressions. Not all s-expressions are legal Lisp forms any more than all sequences of characters are legal s-expressions. For instance, both (foo 1 2) and ("foo" 1 2) are s-expressions, but only the former can be a Lisp form since a list that starts with a string has no meaning as a Lisp form.

This split of the black box has a couple of consequences. One is that you can use s-expressions, as you saw in Chapter 3, as an externalizable data format for data other than source code, using READ to read it and PRINT to print it. 4 The other consequence is that since the semantics of the language are defined in terms of trees of objects rather than strings of characters, it's easier to generate code within the language than it would be if you had to generate code as text. Generating code completely from scratch is only marginally easier -- building up lists vs. building up strings is about the same amount of work. The real win, however, is that you can generate code by manipulating existing data. This is the basis for Lisp's macros, which I'll discuss in much more detail in future chapters. For now I'll focus on the two levels of syntax defined by Common Lisp: the syntax of s-expressions understood by the reader and the syntax of Lisp forms understood by the evaluator.

### 0105. 主题卡 —— Lisp 语言的三大核心元素

After the rules of syntax and semantics, the three most basic components of all Lisp programs are functions, variables and macros. You used all three while building the database in Chapter 3, but I glossed over a lot of the details of how they work and how to best use them. I'll devote the next few chapters to these three topics, starting with functions, which -- like their counterparts in other languages -- provide the basic mechanism for abstracting, well, functionality.

The bulk of Lisp itself consists of functions. More than three quarters of the names defined in the language standard name functions. All the built-in data types are defined purely in terms of what functions operate on them. Even Lisp's powerful object system is built upon a conceptual extension to functions, generic functions, which I'll cover in Chapter 16.

And, despite the importance of macros to The Lisp Way, in the end all real functionality is provided by functions. Macros run at compile time, so the code they generate -- the code that will actually make up the program after all the macros are expanded -- will consist entirely of calls to functions and special operators. Not to mention, macros themselves are also functions, albeit functions that are used to generate code rather than to perform the actions of the program. 1

1 Despite the importance of functions in Common Lisp, it isn’t really accurate to describe it as a functional language. It’s true some of Common Lisp’s features, such as its list manipulation functions, are designed to be used in a body-form* style and that Lisp has a prominent place in the history of functional programming — McCarthy introduced many ideas that are now considered important in functional programming — but Common Lisp was intentionally designed to support many different styles of programming. In the Lisp family, Scheme is the nearest thing to a “pure” functional language, and even it has several features that disqualify it from absolute purity compared to languages such as Haskell and ML.

2『 Lisp 语言的三大核心元素：函数、变量和宏，做一张主题卡片。』——已完成

### 0106. 主题卡 —— 函数对象

In Lisp, functions are just another kind of object. When you define a function with DEFUN, you're really doing two things: creating a new function object and giving it a name. It's also possible, as you saw in Chapter 3, to use LAMBDA expressions to create a function without giving it a name. The actual representation of a function object, whether named or anonymous, is opaque -- in a native-compiling Lisp, it probably consists mostly of machine code. The only things you need to know are how to get hold of it and how to invoke it once you've got it.

The special operator FUNCTION provides the mechanism for getting at a function object. It takes a single argument and returns the function with that name. The name isn't quoted. Thus, if you've defined a function foo, like so:

```c
CL-USER> (defun foo (x) (* 2 x)) 
FOO
```

you can get the function object like this: 10

```c
CL-USER> (function foo) 
#<Interpreted Function FOO>
```

In fact, you've already used FUNCTION, but it was in disguise. The syntax `#'`, which you used in Chapter 3, is syntactic sugar for FUNCTION, just the way `'` is syntactic sugar for QUOTE. 11 Thus, you can also get the function object for foo like this:

```c
CL-USER> #'foo 
#<Interpreted Function FOO>
```

Once you've got the function object, there's really only one thing you can do with it -- invoke it. Common Lisp provides two functions for invoking a function through a function object: FUNCALL and APPLY. 12 They differ only in how they obtain the arguments to pass to the function.

1-2『经验证，`#'` 在 autolisp 里无效。（2020-10-28）回复：这里的 `#'` 相当于 autolisp 里的 `'`。这里总算把一些只是断串起来了。定义函数（常规定义或 lambda 匿名函数）=> 通过 `'` 通说获取定义的函数体 => 通过 apply 函数调用这个函数体（需传入参数列表）从而实现调用函数。（2021-01-05）』

Once you start writing, or even simply using, functions that accept other functions as arguments, you're bound to discover that sometimes it's annoying to have to define and name a whole separate function that's used in only one place, especially when you never call it by name.

When it seems like overkill to define a new function with DEFUN, you can create an "anonymous" function using a LAMBDA expression. As discussed in Chapter 3, a LAMBDA expression looks like this:

```c
(lambda (parameters) body)
```

One way to think of LAMBDA expressions is as a special kind of function name where the name itself directly describes what the function does. This explains why you can use a LAMBDA expression in the place of a function name with #'.

```c
(funcall #'(lambda (x y) (+ x y)) 2 3) ==> 5
```

You can even use a LAMBDA expression as the "name" of a function in a function call expression. If you wanted, you could write the previous FUNCALL expression more concisely.

```c
((lambda (x y) (+ x y)) 2 3) ==> 5
```

But this is almost never done; it's merely worth noting that it's legal in order to emphasize that LAMBDA expressions can be used anywhere a normal function name can be.13

1『有趣有趣，整个匿名函数表达式可以当作一个「函数名」用。通过上面的信息，进一步理解了 autolisp 里 `mapcar` 函数调用的实质，`(mapcar '(lambda (parameters) body) List)`，mapcar 所需的一个参数是匿名函数对象，而这个对象是通过撇号 `'` 来获取的。将此处信息补充进主题卡「函数对象」里。到了此处，有一种串起知识点通透的感觉，大赞。（2021-01-05）』

Anonymous functions can be useful when you need to pass a function as an argument to another function and the function you need to pass is simple enough to express inline. The other important use of LAMBDA expressions is in making closures, functions that capture part of the environment where they're created. You used closures a bit in Chapter 3, but the details of how closures work and what they're used for is really more about how variables work than functions, so I'll save that discussion for the next chapter. (chapter 6)

### 0201. 术语卡 —— 特殊符号撇号 `'` 

The test-form will always be evaluated and then one or the other of the then-form or else-form. An even simpler special operator is QUOTE, which takes a single expression as its "argument" and simply returns it, unevaluated. For instance, the following evaluates to the list (+ 1 2), not the value 3:

```c
(quote (+ 1 2))
```

There's nothing special about this list; you can manipulate it just like any list you could create with the LIST function. 14

QUOTE is used commonly enough that a special syntax for it is built into the reader. Instead of writing the following:

```c
(quote (+ 1 2))
```

you can write this:

```c
'(+ 1 2)
```

1-2『特殊符号，撇号 `'` 的含义及使用，做一张术语卡片。下面注释 14 里也提到，用这种形式创建的 list 里，各个元素是只能是常量，不能变的元素，否者就乖乖用 `list` 语句来创建 list 数据类型。（2020-10-28）』——已完成

This syntax is a small extension of the s-expression syntax understood by the reader. From the point of view of the evaluator, both those expressions will look the same: a list whose first element is the symbol QUOTE and whose second element is the list (+ 1 2). 15

In general, the special operators implement features of the language that require some special processing by the evaluator. For instance, several special operators manipulate the environment in which other forms will be evaluated. One of these, which I'll discuss in detail in Chapter 6, is LET, which is used to create new variable bindings. The following form evaluates to 10 because the second x is evaluated in an environment where it's the name of a variable established by the LET with the value 10:

```c
(let ((x 10)) x)
```

The others provide useful, but somewhat esoteric, features. I’ll discuss them as the features they support come up.

14 Well, one difference exists—literal objects such as quoted lists, but also including double-quoted strings, literal arrays, and vectors (whose syntax you’ll see later), must not be modified. Consequently, any lists you plan to manipulate you should create with LIST.

15 This syntax is an example of a reader macro. Reader macros modify the syntax the reader uses to translate text into Lisp objects. It is, in fact, possible to define your own reader macros, but that’s a rarely used facility of the language. When most Lispers talk about “extending the syntax” of the language, they’re talking about regular macros, as I'll discuss in a moment.

### 0202. 术语卡 —— nil

Two last bits of basic knowledge you need to get under your belt are Common Lisp's notion of truth and falsehood and what it means for two Lisp objects to be "equal." Truth and falsehood are -- in this realm -- straightforward: the symbol NIL is the only false value, and everything else is true. The symbol T is the canonical true value and can be used when you need to return a non-NIL value and don't have anything else handy. The only tricky thing about NIL is that it's the only object that's both an atom and a list: in addition to falsehood, it's also used to represent the empty list. 17 This equivalence between NIL and the empty list is built into the reader: if the reader sees (), it reads it as the symbol NIL. They're completely interchangeable. And because NIL, as I mentioned previously, is the name of a constant variable with the symbol NIL as its value, the expressions nil, (), 'nil, and '() all evaluate to the same thing -- the unquoted forms are evaluated as a reference to the constant variable whose value is the symbol NIL, but in the quoted forms the QUOTE special operator evaluates to the symbol directly. For the same reason, both t and 't will evaluate to the same thing: the symbol T.

17 Using the empty list as false is a reflection of Lisp’s heritage as a list-processing language much as the use of the integer 0 as false in C is a reflection of its heritage as a bit-twiddling language. Not all Lisps handle boolean values the same way. Another of the many subtle differences upon which a good Common Lisp vs. Scheme flame war can rage for days is Scheme’s use of a distinct false value #f, which isn’t the same value as either the symbol nil or the empty list, which are also distinct from each other.

1-2『意外的一个收获：nil 既是一个 atom 也是一个 list。所以它能用来表示空列表。nil, (), 'nil, and '() 是等价的。nil 做一张术语卡片。』——已完成

### 0203. 术语卡 —— 动态语言

As in other languages, in Common Lisp variables are named places that can hold a value. However, in Common Lisp, variables aren't typed the way they are in languages such as Java or C++. That is, you don't need to declare the type of object that each variable can hold. Instead, a variable can hold values of any type and the values carry type information that can be used to check types at runtime. Thus, Common Lisp is dynamically typed -- type errors are detected dynamically. For instance, if you pass something other than a number to the + function, Common Lisp will signal a type error. On the other hand, Common Lisp is a strongly typed language in the sense that all type errors will be detected -- there's no way to treat an object as an instance of a class that it's not. 3

1-2『这里又见「动态语言」的概念，做一张术语卡片。』——已完成

3 Actually, it’s not quite true to say that all type errors will always be detected—it’s possible to use optional declarations to tell the compiler that certain variables will always contain objects of a particular type and to turn off runtime type checking in certain regions of code. However, declarations of this sort are used to optimize code after it has been developed and debugged, not during normal development.

All values in Common Lisp are, conceptually at least, references to objects. 4 Consequently, assigning a variable a new value changes what object the variable refers to but has no effect on the previously referenced object. However, if a variable holds a reference to a mutable object, you can use that reference to modify the object, and the modification will be visible to any code that has a reference to the same object.

One way to introduce new variables you've already used is to define function parameters. As you saw in the previous chapter, when you define a function with DEFUN, the parameter list defines the variables that will hold the function's arguments when it's called. For example, this function defines three variables -- x, y, and z -- to hold its arguments.

```c
(defun foo (x y z) 
  (+ x y z)
)
```

4 As an optimization certain kinds of objects, such as integers below a certain size and characters, may be represented directly in memory where other objects would be represented by a pointer to the actual object. However, since integers and characters are immutable, it doesn’t matter that there may be multiple copies of “the same” object in different variables. This is the root of the difference between EQ and EQL discussed in Chapter 4.

1『这里又见到「不可变性」，函数式编程里核心的一个概念。上面提到的，整数和字符串在 lisp 里是不可变型的数据类型，但作为变量，整数是可以赋值不同的数的啊，难道是分配给整数的内存空间只能放整数的意思？所以说目前还是不太明白其不变性。（2020-11-03）』

Each time a function is called, Lisp creates new bindings to hold the arguments passed by the function's caller. A binding is the runtime manifestation of a variable. A single variable -- the thing you can point to in the program's source code -- can have many different bindings during a run of the program. A single variable can even have multiple bindings at the same time; parameters to a recursive function, for example, are rebound for each call to the function.

As with all Common Lisp variables, function parameters hold object references. 5 Thus, you can assign a new value to a function parameter within the body of the function, and it will not affect the bindings created for another call to the same function. But if the object passed to a function is mutable and you change it in the function, the changes will be visible to the caller since both the caller and the callee will be referencing the same object.

5 In compiler-writer terms Common Lisp functions are “pass-by-value.” However, the values that are passed are references to objects. This is similar to how Java and Python work.

1『看到这里提到的「可变」，渐渐对「不可变性」有那么一点点感觉了。（2020-11-03）』

### 0204. 术语卡 —— closure

By default all binding forms in Common Lisp introduce lexically scoped variables. Lexically scoped variables can be referred to only by code that's textually within the binding form. Lexical scoping should be familiar to anyone who has programmed in Java, C, Perl, or Python since they all provide lexically scoped "local" variables. For that matter, Algol programmers should also feel right at home, as Algol first introduced lexical scoping in the 1960s.

However, Common Lisp's lexical variables are lexical variables with a twist, at least compared to the original Algol model. The twist is provided by the combination of lexical scoping with nested functions. By the rules of lexical scoping, only code textually within the binding form can refer to a lexical variable. But what happens when an anonymous function contains a reference to a lexical variable from an enclosing scope? For instance, in this expression:

```c
(let ((count 0)) #'(lambda () (setf count (1+ count))))
```

the reference to count inside the LAMBDA form should be legal according to the rules of lexical scoping. Yet the anonymous function containing the reference will be returned as the value of the LET form and can be invoked, via FUNCALL, by code that's not in the scope of the LET. So what happens? As it turns out, when count is a lexical variable, it just works. The binding of count created when the flow of control entered the LET form will stick around for as long as needed, in this case for as long as someone holds onto a reference to the function object returned by the LET form. The anonymous function is called a closure because it "closes over" the binding created by the LET.

1-2『又见闭包 closure，不过这里目前介绍的闭包概念没弄明白。做一张术语卡片。（2020-11-03）』——已完成

The key thing to understand about closures is that it's the binding, not the value of the variable, that's captured. Thus, a closure can not only access the value of the variables it closes over but can also assign new values that will persist between calls to the closure. For instance, you can capture the closure created by the previous expression in a global variable like this:

```c
(defparameter *fn* (let ((count 0)) #'(lambda () (setf count (1+ count)))))
```

Then each time you invoke it, the value of count will increase by one.

```c
CL-USER> (funcall *fn*) 
1 
CL-USER> (funcall *fn*) 
2 
CL-USER> (funcall *fn*) 
3
```

A single closure can close over many variable bindings simply by referring to them. Or multiple closures can capture the same binding. For instance, the following expression returns a list of three closures, one that increments the value of the closed over count binding, one that decrements it, and one that returns the current value:

```c
(let ((count 0)) 
  (list 
    #'(lambda () (incf count)) 
    #'(lambda () (decf count)) 
    #'(lambda () count)
  )
)
```

### 0205. 术语卡 —— atoms

The simplest Lisp forms, atoms, can be divided into two categories: symbols and everything else. A symbol, evaluated as a form, is considered the name of a variable and evaluates to the current value of the variable. 11 I'll discuss in Chapter 6 how variables get their values in the first place. You should also note that certain "variables" are that old oxymoron of programming: "constant variables." For instance, the symbol PI names a constant variable whose value is the best possible floating-point approximation to the mathematical constant pi.

1-2『多次看到了 Lisp forms、atoms，atoms 做一张术语卡片。』

All other atoms -- numbers and strings are the kinds you've seen so far -- are self-evaluating objects. This means when such an expression is passed to the notional evaluation function, it's simply returned. You saw examples of self-evaluating objects in Chapter 2 when you typed 10 and "hello, world" at the REPL.

It's also possible for symbols to be self-evaluating in the sense that the variables they name can be assigned the value of the symbol itself. Two important constants that are defined this way are T and NIL, the canonical true and false values. I'll discuss their role as booleans in the section "Truth, Falsehood, and Equality."

Another class of self-evaluating symbols are the keyword symbols -- symbols whose names start with `:`. When the reader interns such a name, it automatically defines a constant variable with the name and with the symbol as the value.

### 0206. 术语卡 —— Lisp 里的函数调用

The evaluation rule for function call forms is simple: evaluate the remaining elements of the list as Lisp forms and pass the resulting values to the named function. This rule obviously places some additional syntactic constraints on a function call form: all the elements of the list after the first must themselves be well-formed Lisp forms. In other words, the basic syntax of a function call form is as follows, where each of the arguments is itself a Lisp form:

```c
(function-name argument*)
```

Thus, the following expression is evaluated by first evaluating 1, then evaluating 2, and then passing the resulting values to the + function, which returns 3:

```c
(+ 1 2)
```

2『说出了 Lisp 里函数调用的本质，做一张术语卡片。』——已完成

### 0207. 术语卡 —— macro

While special operators extend the syntax of Common Lisp beyond what can be expressed with just function calls, the set of special operators is fixed by the language standard. Macros, on the other hand, give users of the language a way to extend its syntax. As you saw in Chapter 3, a macro is a function that takes s-expressions as arguments and returns a Lisp form that's then evaluated in place of the macro form. The evaluation of a macro form proceeds in two phases: First, the elements of the macro form are passed, unevaluated, to the macro function. Second, the form returned by the macro function -- called its expansion -- is evaluated according to the normal evaluation rules.

It's important to keep the two phases of evaluating a macro form clear in your mind. It's easy to lose track when you're typing expressions at the REPL because the two phases happen one after another and the value of the second phase is immediately returned. But when Lisp code is compiled, the two phases happen at completely different times, so it's important to keep clear what's happening when. For instance, when you compile a whole file of source code with the function COMPILE-FILE, all the macro forms in the file are recursively expanded until the code consists of nothing but function call forms and special forms. This macroless code is then compiled into a FASL file that the LOAD function knows how to load. The compiled code, however, isn't executed until the file is loaded. Because macros generate their expansion at compile time, they can do relatively large amounts of work generating their expansion without having to pay for it when the file is loaded or the functions defined in the file are called.

Since the evaluator doesn't evaluate the elements of the macro form before passing them to the macro function, they don't need to be well-formed Lisp forms. Each macro assigns a meaning to the s-expressions in the macro form by virtue of how it uses them to generate its expansion. In other words, each macro defines its own local syntax. For instance, the backwards macro from Chapter 3 defines a syntax in which an expression is a legal backwards form if it's a list that's the reverse of a legal Lisp form.

I'll talk quite a bit more about macros throughout this book. For now the important thing for you to realize is that macros -- while syntactically similar to function calls -- serve quite a different purpose, providing a hook into the compiler. 16

16 People without experience using Lisp’s macros or, worse yet, bearing the scars of C preprocessor-inflicted wounds, tend to get nervous when they realize that macro calls look like regular function calls. This turns out not to be a problem in practice for several reasons. One is that macro forms are usually formatted differently than function calls. For instance, you write the following:

```c
(dolist (x foo) 
  (print x))
```

rather than this:

```c
(dolist (x foo) (print x))
```

or this:

```c
(dolist (x foo) 
            (print x))
```

the way you would if DOLIST was a function. A good Lisp environment will automatically format macro calls correctly, even for user-defined macros. And even if a DOLIST form was written on a single line, there are several clues that it’s a macro. For one, the expression (x foo) is meaningful by itself only if x is the name of a function or macro. Combine that with the later occurrence of x as a variable, and it’s pretty suggestive that DOLIST is a macro that’s creating a binding for a variable named x. Naming conventions also help-looping constructs, which are invariably macros, are frequently given names starting with do.

1『宏 Marco 到目前为止还是不太明白，哎，这可是 lisp 的核心知识。（2020-12-30）』

While many of the ideas that originated in Lisp, from the conditional expression to garbage collection, have been incorporated into other languages, the one language feature that continues to set Common Lisp apart is its macro system. Unfortunately, the word macro describes a lot of things in computing to which Common Lisp's macros bear only a vague and metaphorical similarity. This causes no end of misunderstanding when Lispers try to explain to non-Lispers what a great feature macros are. 1 To understand Lisp's macros, you really need to come at them fresh, without preconceptions based on other things that also happen to be called macros. So let's start our discussion of Lisp's macros by taking a step back and looking at various ways languages support extensibility.

All programmers should be used to the idea that the definition of a language can include a standard library of functionality that's implemented in terms of the "core" language -- functionality that could have been implemented by any programmer on top of the language if it hadn't been defined as part of the standard library. C's standard library, for instance, can be implemented almost entirely in portable C. Similarly, most of the ever-growing set of classes and interfaces that ship with Java's standard Java Development Kit (JDK) are written in "pure" Java.

One advantage of defining languages in terms of a core plus a standard library is it makes them easier to understand and implement. But the real benefit is in terms of expressiveness -- since much of what you think of as "the language" is really just a library -- the language is easy to extend. If C doesn't have a function to do some thing or another that you need, you can write that function, and now you have a slightly richer version of C. Similarly, in a language such as Java or Smalltalk where almost all the interesting parts of the "language" are defined in terms of classes, by defining new classes you extend the language, making it more suited for writing programs to do whatever it is you're trying to do.

While Common Lisp supports both these methods of extending the language, macros give Common Lisp yet another way. As I discussed briefly in Chapter 4, each macro defines its own syntax, determining how the s-expressions it's passed are turned into Lisp forms. With macros as part of the core language it's possible to build new syntax -- control constructs such as WHEN, DOLIST, and LOOP as well as definitional forms such as DEFUN and DEFPARAMETER -- as part of the "standard library" rather than having to hardwire them into the core. This has implications for how the language itself is implemented, but as a Lisp programmer you'll care more that it gives you another way to extend the language, making it a better language for expressing solutions to your particular programming problems.

Now, it may seem that the benefits of having another way to extend the language would be easy to recognize. But for some reason a lot of folks who haven't actually used Lisp macros -- folks who think nothing of spending their days creating new functional abstractions or defining hierarchies of classes to solve their programming problems -- get spooked by the idea of being able to define new syntactic abstractions. The most common cause of macrophobia seems to be bad experiences with other "macro" systems. Simple fear of the unknown no doubt plays a role, too. To avoid triggering any macrophobic reactions, I'll ease into the subject by discussing several of the standard control-construct macros defined by Common Lisp. These are some of the things that, if Lisp didn't have macros, would have to be built into the language core. When you use them, you don't have to care that they're implemented as macros, but they provide a good example of some of the things you can do with macros. 2 In the next chapter, I'll show you how you can define your own macros.

2『这里有关 lisp 宏的信息补充进宏的术语卡片里。』——已完成

1 To see what this misunderstanding looks like, find any longish Usenet thread cross-posted between comp.lang.lisp and any other comp.lang.* group with macro in the subject. A rough paraphrase goes like this: Lispnik: “Lisp is the best because of its macros!” Othernik: “You think Lisp is good because of macros?! But macros are horrible and evil; Lisp must be horrible and evil.”

2 Another important class of language constructs that are defined using macros are all the definitional constructs such as DEFUN, DEFPARAMETER, DEFVAR, and others. In Chapter 24 you’ll define your own definitional macros that will allow you to concisely write code for reading and writing binary data.

1-2『这一小节的故事，对理解「宏」的概念很有帮助，合并进宏的术语卡片里。』——已完成

Once upon a time, long ago, there was a company of Lisp programmers. It was so long ago, in fact, that Lisp had no macros. Anything that couldn't be defined with a function or done with a special operator had to be written in full every time, which was rather a drag. Unfortunately, the programmers in this company -- though brilliant -- were also quite lazy. Often in the middle of their programs -- when the tedium of writing a bunch of code got to be too much -- they would instead write a note describing the code they needed to write at that place in the program. Even more unfortunately, because they were lazy, the programmers also hated to go back and actually write the code described by the notes. Soon the company had a big stack of programs that nobody could run because they were full of notes about code that still needed to be written.

In desperation, the big bosses hired a junior programmer, Mac, whose job was to find the notes, write the required code, and insert it into the program in place of the notes. Mac never ran the programs -- they weren't done yet, of course, so he couldn't. But even if they had been completed, Mac wouldn't have known what inputs to feed them. So he just wrote his code based on the contents of the notes and sent it back to the original programmer.

With Mac's help, all the programs were soon completed, and the company made a ton of money selling them -- so much money that the company could double the size of its programming staff. But for some reason no one thought to hire anyone to help Mac; soon he was single- handedly assisting several dozen programmers. To avoid spending all his time searching for notes in source code, Mac made a small modification to the compiler the programmers used. Thereafter, whenever the compiler hit a note, it would e-mail him the note and wait for him to e-mail back the replacement code. Unfortunately, even with this change, Mac had a hard time keeping up with the programmers. He worked as carefully as he could, but sometimes --  especially when the notes weren't clear -- he would make mistakes.

The programmers noticed, however, that the more precisely they wrote their notes, the more likely it was that Mac would send back correct code. One day, one of the programmers, having a hard time describing in words the code he wanted, included in one of his notes a Lisp program that would generate the code he wanted. That was fine by Mac; he just ran the program and sent the result to the compiler.

The next innovation came when a programmer put a note at the top of one of his programs containing a function definition and a comment that said, "Mac, don't write any code here, but keep this function for later; I'm going to use it in some of my other notes." Other notes in the same program said things such as, "Mac, replace this note with the result of running that other function with the symbols x and y as arguments."

This technique caught on so quickly that within a few days, most programs contained dozens of notes defining functions that were only used by code in other notes. To make it easy for Mac to pick out the notes containing only definitions that didn't require any immediate response, the programmers tagged them with the standard preface: "Definition for Mac, Read Only." This -- as the programmers were still quite lazy -- was quickly shortened to "DEF. MAC. R/O" and then "DEFMACRO."

Pretty soon, there was no actual English left in the notes for Mac. All he did all day was read and respond to e-mails from the compiler containing DEFMACRO notes and calls to the functions defined in the DEFMACROs. Since the Lisp programs in the notes did all the real work, keeping up with the e-mails was no problem. Mac suddenly had a lot of time on his hands and would sit in his office daydreaming about white-sand beaches, clear blue ocean water, and drinks with little paper umbrellas in them.

Several months later the programmers realized nobody had seen Mac for quite some time. When they went to his office, they found a thin layer of dust over everything, a desk littered with travel brochures for various tropical locations, and the computer off. But the compiler still worked -- how could it be? It turned out Mac had made one last change to the compiler: instead of e-mailing notes to Mac, the compiler now saved the functions defined by DEFMACRO notes and ran them when called for by the other notes. The programmers decided there was no reason to tell the big bosses Mac wasn't coming to the office anymore. So to this day, Mac draws a salary and from time to time sends the programmers a postcard from one tropical locale or another.

### 0301. 任意卡 —— 几个语言的座右铭

Perl: 1) makes easy things easy and hard things possible. 2) There's more than one way to do it.

Python: There's only one way to do it.

Lisp: the programmable programming language.

The nearest thing Common Lisp has to a motto is the koan-like description, "the programmable programming language." While cryptic, that description gets at the root of the biggest advantage Common Lisp still has over other languages. More than any other language, Common Lisp follows the philosophy that what's good for the language's designer is good for the language's users. Thus, when you're programming in Common Lisp, you almost never find yourself wishing the language supported some feature that would make your program easier to write, because, as you'll see throughout this book, you can just add the feature yourself.

Consequently, a Common Lisp program tends to provide a much clearer mapping between your ideas about how the program works and the code you actually write. Your ideas aren't obscured by boilerplate code and endlessly repeated idioms. This makes your code easier to maintain because you don't have to wade through reams of code every time you need to make a change. Even systemic changes to a program's behavior can often be achieved with relatively small changes to the actual code. This also means you'll develop code more quickly; there's less code to write, and you don't waste time thrashing around trying to find a clean way to express yourself within the limitations of the language. 2

### 0302. 任意卡 —— 三大类 list 的处理方式

Things get more interesting when we consider how lists are evaluated. All legal list forms start with a symbol, but three kinds of list forms are evaluated in three quite different ways. To determine what kind of form a given list is, the evaluator must determine whether the symbol that starts the list is the name of a function, a macro, or a special operator. If the symbol hasn't been defined yet -- as may be the case if you're compiling code that contains references to functions that will be defined later -- it's assumed to be a function name. 12 I'll refer to the three kinds of forms as function call forms, macro forms, and special forms.

2『三大类 list 的处理方式：函数、宏和操作符。做一张任意卡片。回复：突然领悟到在 Lisp 里「一切皆 lisp」，函数、表达式、变量等等。（2020-12-30）』 —  — 已完成

12 In Common Lisp a symbol can name both an operator—function, macro, or special operatorand a variable. This is one of the major differences between Common Lisp and Scheme. The difference is sometimes described as Common Lisp being a Lisp-2 vs. Scheme being a Lisp-1a Lisp-2 has two namespaces, one for operators and one for variables, but a Lisp-1 uses a single namespace. Both choices have advantages, and partisans can debate endlessly which is better.

### 0303. 任意卡 —— lisp 中函数名变量名的命名规则

第 5 章（函数那章）里提到函数名采用的是连字符，比如 get-entityname。不过目前在开发数据流（autolisp）时采用的还是类似 Java 的风格，普通变量 entityName，函数名 GetEntityName。（2021-01-05）

### 0304. 任意卡 —— 函数多出口的实现

All the functions you've written so far have used the default behavior of returning the value of the last expression evaluated as their own return value. This is the most common way to return a value from a function.

However, sometimes it's convenient to be able to return from the middle of a function such as when you want to break out of nested control constructs. In such cases you can use the RETURN-FROM special operator to immediately return any value from the function.

1-2『

在 autolisp 里总算找到了替代函数 [vl-exit-with-value (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-80622A39-A5E8-4E68-824E-E66BD8D3E9DE)。通过它可以实现函数的多个出口。

函数多出口的实现，做一张任意卡片。（2021-01-05）——已完成

』

You'll see in Chapter 20 that RETURN-FROM is actually not tied to functions at all; it's used to return from a block of code defined with the BLOCK special operator. However, DEFUN automatically wraps the whole function body in a block with the same name as the function. So, evaluating a RETURN-FROM with the name of the function and the value you want to return will cause the function to immediately exit with that value. RETURN-FROM is a special operator whose first "argument" is the name of the block from which to return. This name isn't evaluated and thus isn't quoted.

## Preface

Practical Common Lisp ... isn't that an oxymoron? If you're like most programmers, you probably know something about Lisp—from a comp sci course in college or from learning enough Elisp to customize Emacs a bit. Or maybe you just know someone who won't shut up about Lisp, the greatest language ever. But you probably never figured you'd see practical and Lisp in the same book title.

Yet, you're reading this; you must want to know more. Maybe you believe learning Lisp will make you a better programmer in any language. Or maybe you just want to know what those Lisp fanatics are yammering about all the time. Or maybe you have learned some Lisp but haven't quite made the leap to using it to write interesting software.

If any of those is true, this book is for you. Using Common Lisp, an ANSI standardized, industrial-strength dialect of Lisp, I show you how to write software that goes well beyond silly academic exercises or trivial editor customizations. And I show you how Lisp—even with many of its features adopted by other languages—still has a few tricks up its sleeve.

But unlike many Lisp books, this one doesn't just touch on a few of Lisp's greatest features and then leave you on your own to actually use them. I cover all the language features you'll need to write real programs and devote well over a third of the book to developing nontrivial software—a statistical spam filter, a library for parsing binary files, and a server for streaming MP3s over a network complete with an online MP3 database and Web interface.

So turn the book over, open it up, and see for yourself how eminently practical using the greatest language ever invented can be.

## Typographical Conventions

Inline text set like this is code, usually the names of functions, variables, classes, and so on, that either I’ve just introduced or I’m about to introduce. Names defined by the language standard are set like this: DEFUN. Larger bits of example code are set like this:

```c
(defun foo (x y z) 
    (+ x y z))
```

Since Common Lisp’s syntax is notable for its regularity and simplicity, I use simple templates to describe the syntax of various Lisp forms. For instance, the following describes the syntax of DEFUN, the standard function-defining macro:

```c
(defun name (parameter*)
    [ documentation-string ] 
    body-form*)
```

Names in italic in those templates are meant to be filled in with specific names or forms that I’ll describe in the text. An italicized name followed by an asterisk (*) represents zero or more occurrences of whatever the name represents, and a name enclosed in brackets ([]) represents an optional element. Occasionally, alternatives will be separated by a bar (|). Everything else in the template—usually just some names and parentheses—is literal text that will appear in the form.

Finally, because much of your interaction with Common Lisp happens at the interactive read-eval-print loop, or REPL, I’ll frequently show the result of evaluating Lisp forms at the REPL like this:

```c
CL-USER> (+ 1 2) 
// out
3
```

The CL-USER> is the Lisp prompt and is always followed by the expression to be evaluated, (+ 1 2), in this case. The result and any other output generated are shown on the following lines. I’ll also sometimes show the result of evaluating an expression by writing the expression followed by an →, which is followed by the result, like this: 

```c
(+ 1 2) → 3
```

Occasionally, I’ll use an equivalence sign ( ≡) to express that two Lisp forms are equivalent, like this:

```c
(+ 1 2 3) ≡ (+ (+ 1 2) 3)
```

## Praise for Practical Common Lisp

I have been complimented many times and they always embarrass me; I always feel that they have not said enough.

—— Mark Twain

Peter Seibel offers a fresh view of Lisp and its possibilities for elegantly solving problems. In Practical Common Lisp, he gives enough basic information to let you quickly see the power of the functional language paradigm. He then dazzles you with examples that seem almost magical in their simplicity and power. This read is pure fun from start to finish.

—— Gary Pollice, from Dr. Dobb's Portal, May 17, 2006 article on the 2006 Jolt Awards

Peter Seibel's Practical Common Lisp is just what the title implies: an excellent introduction to Common Lisp for someone who wants to dive in and start using the language for real work. The book is very well written and is fun to read—at least for those of us whose idea of fun extends to learning new programming languages.

Rather than spending a lot of time on abstract discussion of Lisp's place in the universe of programming lnaguages, Seibel dives right in, guiding the reader through a series of programming examples of increasing complexity. This approach places the most emphasis on those parts of Common Lisp that skilled programmers use the most, without getting bogged down in the odd corners of Common Lisp that even the experts must look up in the manual. The result of Seibel's example-driven approach is to give the reader an excellent appreciation of the power of Common Lisp in building complex, evolving software systems with a minimum of effort.

There are already many good books on Common Lisp that offer a more abstract and comparative approach, but a good ‘Here's how you do it—and why’ book, aimed at the working programmer, is a valuable contribution, both to current Common Lisp users and those who should be.

—— Scott E. Fahlman, Research Professor of Computer Science, Carnegie Mellon University

This book shows the power of Lisp not only in the areas that it has traditionally been noted for—such as developing a complete unit test framework in only 26 lines of code—but also in new areas such as parsing binary MP3 files, building a web application for browsing a collection of songs, and streaming audio over the web. Many readers will be surprised that Lisp allows you to do all this with conciseness similar to scripting languages such as Python, efficiency similar to C++, and unparalleled flexibility in designing your own language extensions.

—— Peter Norvig, Director of Search Quality, Google Inc; author of Paradigms of Artificial Intelligence Programming: Case Studies in Common Lisp

I wish this book had already existed when I started learning Lisp. It's not that there aren't other good books about (Common) Lisp out there, but none of them has such a pragmatic, up-to-date approach. And let's not forget that Peter covers topics like pathnames or conditions and restarts which are completely ignored in the rest of the Lisp literature.

If you're new to Lisp and want to dive right in don't hesitate to buy this book. Once you've read it and worked with it you can continue with the ‘classics’ like Graham, Norvig, Keene, or Steele.

—— Edi Weitz, maintainer of the Common Lisp Cookbook and author of CL-PPCRE regular expression library.

Two prehensile toes up!

—— Kenny Tilton, comp.lang.lisp demon, reporting on behalf of his development team.

Experienced programmers learn best from examples and it is delightful to see that Lisp is finally being served with Seibel's example-rich tutorial text. Especially delightful is the fact that this book includes so many examples that fall within the realm of problems today's programmers might be called upon to tackle, such as Web development and streaming media.

—— Philip Greenspun, author of Software Engineering for Internet Applications, MIT Department of Electrical Engineering and Computer Science

Practical Common Lisp is an excellent book that covers the breadth of the Common Lisp language and also demonstrates the unique features of Common Lisp with real-world applications that the reader can run and extend. This book not only shows what Common Lisp is but also why every programmer should be familiar with Lisp.

—— John Foderaro, Senior Scientist, Franz Inc.

The Maxima Project frequently gets queries from potential new contributors who would like to learn Common Lisp. I am pleased to finally have a book that I can recommend to them without reservation. Peter Seibel's clear, direct style allows the reader to quickly appreciate the power of Common Lisp. His many included examples, which focus on contemporary programming problems, demonstrate that Lisp is much more than an academic programming language. Practical Common Lisp is a welcome addition to the literature.

—— James Amundson, Maxima Project Leader

I like the interspersed Practical chapters on 'real' and useful programs. We need books of this kind telling the world that crunching strings and numbers into trees or graphs is easily done in Lisp.

—— Professor Christian Queinnec, Universite Paris 6 (Pierre et Marie Curie)

One of the most important parts of learning a programming language is learning its proper programming style. This is hard to teach, but it can be painlessly absorbed from Practical Common Lisp. Just reading the practical examples made me a better programmer in any language.

—— Peter Scott, Lisp programmer

Finally, a Lisp book for the rest of us. If you want to learn how to write a factorial function, this is not your book. Seibel writes for the practical programmer, emphasizing the engineer/artist over the scientist, subtly and gracefully implying the power of the language while solving understandable real-world problems.

In most chapters, the reading of the chapter feels just like the experience of writing a program, starting with a little understanding, then having that understanding grow, like building the shoulders upon which you can then stand. When Seibel introduced macros as an aside while building a test framework, I was shocked at how such a simple example made me really 'get' them. Narrative context is extremely powerful and the technical books that use it are a cut above. Congrats!

—— Keith Irwin, Lisp Programmer

While learning Lisp, one is often refered to the CL HyperSpec if they do not know what a particular function does, however, I found that I often did not 'get it' just reading the HyperSpec. When I had a problem of this manner, I turned to Practical Common Lisp every single time—it is by far the most readable source on the subject that shows you how to program, not just tell you.

—— Philip Haddad, Lisp Programmer

With the IT world evolving at an ever increasing pace, professionals need the most powerful tools available. This is why Common Lisp—the most powerful, flexible, and stable programming language ever—is seeing such a rise in popularity. Practical Common Lisp is the long-awaited book that will help you harness the power of Common Lisp to tackle today's complex real world problems.

—— Marc Battyani, author of CL-PDF, CL-TYPESETTING, and mod_lisp.

Please don't assume Common Lisp is only useful for Databases, Unit Test Frameworks, Spam Filters, ID3 Parsers, Web Programming, Shoutcast Servers, HTML Generation Interpreters, and HTML Generation Compilers just because these are the only things happened to be implemented in the book Practical Common Lisp.

—— Tobias C. Rittweiler, Lisp Programmer

When I met Peter, who just started writing this book, I asked to myself (not to him, of course) ‘why yet another book on Common Lisp, when there are many nice introductory books?’ One year later, I found a draft of the new book and recognized I was wrong. This book is not ‘yet another’ one. The author focuses on practical aspects rather than on technical details of the language. When I first studied Lisp by reading an introductory book, I felt I understood the language, but I also had an impression ‘so what?’, meaning I had no idea about how to use it. In contrast, this book leaps into a ‘PRACTICAL’ chapter after the first few chapters that explain the very basic notions of the language. Then the readers are expected to learn more about the language while they are following the PRACTICAL projects, which are combined together to form a product of a significant size. After reading this book, the readers will feel themselves expert programmers on Common Lisp since they have ‘finished’ a big project already. I think Lisp is the only language that allows this type of practical introduction. Peter makes use of this feature of the language in building up a fancy introduction on Common Lisp.

—— Taiichi Yuasa, Professor, Department of Communications and Computer Engineering, Kyoto University

## 0101. Introduction: Why Lisp?

If you think the greatest pleasure in programming comes from getting a lot done with code that simply and clearly expresses your intention, then programming in Common Lisp is likely to be about the most fun you can have with a computer. You'll get more done, faster, using it than you would using pretty much any other language.

That's a bold claim. Can I justify it? Not in a just a few pages in this chapter -- you're going to have to learn some Lisp and see for yourself -- thus the rest of this book. For now, let me start with some anecdotal evidence, the story of my own road to Lisp. Then, in the next section, I'll explain the payoff I think you'll get from learning Common Lisp.

I'm one of what must be a fairly small number of second-generation Lisp hackers. My father got his start in computers writing an operating system in assembly for the machine he used to gather data for his doctoral dissertation in physics. After running computer systems at various physics labs, by the 1980s he had left physics altogether and was working at a large pharmaceutical company. That company had a project under way to develop software to model production processes in its chemical plants -- if you increase the size of this vessel, how does it affect annual production? The original team, writing in FORTRAN, had burned through half the money and almost all the time allotted to the project with nothing to show for their efforts. This being the 1980s and the middle of the artificial intelligence (AI) boom, Lisp was in the air. So my dad -- at that point not a Lisper -- went to Carnegie Mellon University (CMU) to talk to some of the folks working on what was to become Common Lisp about whether Lisp might be a good language for this project.

The CMU folks showed him some demos of stuff they were working on, and he was convinced. He in turn convinced his bosses to let his team take over the failing project and do it in Lisp. A year later, and using only what was left of the original budget, his team delivered a working application with features that the original team had given up any hope of delivering. My dad credits his team's success to their decision to use Lisp.

Now, that's just one anecdote. And maybe my dad is wrong about why they succeeded. Or maybe Lisp was better only in comparison to other languages of the day. These days we have lots of fancy new languages, many of which have incorporated features from Lisp. Am I really saying Lisp can offer you the same benefits today as it offered my dad in the 1980s? Read on.

Despite my father's best efforts, I didn't learn any Lisp in high school. After a college career that didn't involve much programming in any language, I was seduced by the Web and back into computers. I worked first in Perl, learning enough to be dangerous while building an online discussion forum for Mother Jones magazine's Web site and then moving to a Web shop, Organic Online, where I worked on big -- for the time -- Web sites such as the one Nike put up during the 1996 Olympics. Later I moved onto Java as an early developer at WebLogic, now part of BEA. After WebLogic, I joined another startup where I was the lead programmer on a team building a transactional messaging system in Java. Along the way, my general interest in programming languages led me to explore such mainstream languages as C, C++, and Python, as well as less well-known ones such as Smalltalk, Eiffel, and Beta.

So I knew two languages inside and out and was familiar with another half dozen. Eventually, however, I realized my interest in programming languages was really rooted in the idea planted by my father's tales of Lisp -- that different languages really are different, and that, despite the formal Turing equivalence of all programming languages, you really can get more done more quickly in some languages than others and have more fun doing it. Yet, ironically, I had never spent that much time with Lisp itself. So, I started doing some Lisp hacking in my free time. And whenever I did, it was exhilarating how quickly I was able to go from idea to working code.

For example, one vacation, having a week or so to hack Lisp, I decided to try writing a version of a program -- a system for breeding genetic algorithms to play the game of Go -- that I had written early in my career as a Java programmer. Even handicapped by my then rudimentary knowledge of Common Lisp and having to look up even basic functions, it still felt more productive than it would have been to rewrite the same program in Java, even with several extra years of Java experience acquired since writing the first version.

A similar experiment led to the library I'll discuss in Chapter 24. Early in my time at WebLogic I had written a library, in Java, for taking apart Java class files. It worked, but the code was a bit of a mess and hard to modify or extend. I had tried several times, over the years, to rewrite that library, thinking that with my ever-improving Java chops I'd find some way to do it that didn't bog down in piles of duplicated code. I never found a way. But when I tried to do it in Common Lisp, it took me only two days, and I ended up not only with a Java class file parser but with a general-purpose library for taking apart any kind of binary file. You'll see how that library works in Chapter 24 and use it in Chapter 25 to write a parser for the ID3 tags embedded in MP3 files.

### 1.1 Why Lisp?

It's hard, in only a few pages of an introductory chapter, to explain why users of a language like it, and it's even harder to make the case for why you should invest your time in learning a certain language. Personal history only gets us so far. Perhaps I like Lisp because of some quirk in the way my brain is wired. It could even be genetic, since my dad has it too. So before you dive into learning Lisp, it's reasonable to want to know what the payoff is going to be.

For some languages, the payoff is relatively obvious. For instance, if you want to write low-level code on Unix, you should learn C. Or if you want to write certain kinds of cross-platform applications, you should learn Java. And any of a number companies still use a lot of C++, so if you want to get a job at one of them, you should learn C++.

For most languages, however, the payoff isn't so easily categorized; it has to do with subjective criteria such as how it feels to use the language. Perl advocates like to say that Perl "makes easy things easy and hard things possible" and revel in the fact that, as the Perl motto has it, "There's more than one way to do it." 1 Python's fans, on the other hand, think Python is clean and simple and think Python code is easier to understand because, as their motto says, "There's only one way to do it."

So, why Common Lisp? There's no immediately obvious payoff for adopting Common Lisp the way there is for C, Java, and C++ (unless, of course, you happen to own a Lisp Machine). The benefits of using Lisp have much more to do with the experience of using it. I'll spend the rest of this book showing you the specific features of Common Lisp and how to use them so you can see for yourself what it's like. For now I'll try to give you a sense of Lisp's philosophy.

The nearest thing Common Lisp has to a motto is the koan-like description, "the programmable programming language." While cryptic, that description gets at the root of the biggest advantage Common Lisp still has over other languages. More than any other language, Common Lisp follows the philosophy that what's good for the language's designer is good for the language's users. Thus, when you're programming in Common Lisp, you almost never find yourself wishing the language supported some feature that would make your program easier to write, because, as you'll see throughout this book, you can just add the feature yourself.

2『几个语言的座右铭，写一张任意卡片。』——已完成

Consequently, a Common Lisp program tends to provide a much clearer mapping between your ideas about how the program works and the code you actually write. Your ideas aren't obscured by boilerplate code and endlessly repeated idioms. This makes your code easier to maintain because you don't have to wade through reams of code every time you need to make a change. Even systemic changes to a program's behavior can often be achieved with relatively small changes to the actual code. This also means you'll develop code more quickly; there's less code to write, and you don't waste time thrashing around trying to find a clean way to express yourself within the limitations of the language. 2

Common Lisp is also an excellent language for exploratory programming -- if you don't know exactly how your program is going to work when you first sit down to write it, Common Lisp provides several features to help you develop your code incrementally and interactively.

For starters, the interactive read-eval-print loop, which I'll introduce in the next chapter, lets you continually interact with your program as you develop it. Write a new function. Test it. Change it. Try a different approach. You never have to stop for a lengthy compilation cycle. 3

Other features that support a flowing, interactive programming style are Lisp's dynamic typing and the Common Lisp condition system. Because of the former, you spend less time convincing the compiler you should be allowed to run your code and more time actually running it and working on it, 4 and the latter lets you develop even your error handling code interactively.

Another consequence of being "a programmable programming language" is that Common Lisp, in addition to incorporating small changes that make particular programs easier to write, can easily adopt big new ideas about how programming languages should work. For instance, the original implementation of the Common Lisp Object System (CLOS), Common Lisp's powerful object system, was as a library written in portable Common Lisp. This allowed Lisp programmers to gain actual experience with the facilities it provided before it was officially incorporated into the language.

Whatever new paradigm comes down the pike next, it's extremely likely that Common Lisp will be able to absorb it without requiring any changes to the core language. For example, a Lisper has recently written a library, AspectL, that adds support for aspect-oriented programming (AOP) to Common Lisp. 5 If AOP turns out to be the next big thing, Common Lisp will be able to support it without any changes to the base language and without extra preprocessors and extra compilers. 6

1 Perl is also worth learning as "the duct tape of the Internet."

2 Unfortunately, there's little actual research on the productivity of different languages. One report that shows Lisp coming out well compared to C++ and Java in the combination of programmer and program efficiency is discussed at http://www.norvig.com/java-lisp.html.

3 Psychologists have identified a state of mind called flow in which we're capable of incredible concentration and productivity. The importance of flow to programming has been recognized for nearly two decades since it was discussed in the classic book about human factors in programming Peopleware: Productive Projects and Teams by Tom DeMarco and Timothy Lister (Dorset House, 1987). The two key facts about flow are that it takes around 15 minutes to get into a state of flow and that even brief interruptions can break you right out of it, requiring another 15-minute immersion to reenter. DeMarco and Lister, like most subsequent authors, concerned themselves mostly with flow-destroying interruptions such as ringing telephones and inopportune visits from the boss. Less frequently considered but probably just as important to programmers are the interruptions caused by our tools. Languages that require, for instance, a lengthy compilation before you can try your latest code can be just as inimical to flow as a noisy phone or a nosy boss. So, one way to look at Lisp is as a language designed to keep you in a state of flow.

4 This point is bound to be somewhat controversial, at least with some folks. Static versus dynamic typing is one of the classic religious wars in programming. If you're coming from C++ and Java (or from statically typed functional languages such as Haskel and ML) and refuse to consider living without static type checks, you might as well put this book down now. However, before you do, you might first want to check out what self-described "statically typed bigot" Robert Martin (author of Designing Object Oriented C++ Applications Using the Booch Method [Prentice Hall, 1995]) and C++ and Java author Bruce Eckel (author of Thinking in C++ [Prentice Hall, 1995] and Thinking in Java [Prentice Hall, 1998]) have had to say about dynamic typing on their weblogs (http://www.artima.com/weblogs/viewpost.jsp?thread=4639 and http://www.mindview.net/WebLog/log-0025). On the other hand, folks coming from Smalltalk, Python, Perl, or Ruby should feel right at home with this aspect of Common Lisp.

5 AspectL is an interesting project insofar as AspectJ, its Java-based predecessor, was written by Gregor Kiczales, one of the designers of Common Lisp's object and metaobject systems. To many Lispers, AspectJ seems like Kiczales's attempt to backport his ideas from Common Lisp into Java. However, Pascal Costanza, the author of AspectL, thinks there are interesting ideas in AOP that could be useful in Common Lisp. Of course, the reason he's able to implement AspectL as a library is because of the incredible flexibility of the Common Lisp Meta Object Protocol Kiczales designed. To implement AspectJ, Kiczales had to write what was essentially a separate compiler that compiles a new language into Java source code. The AspectL project page is at http://common-lisp.net/ project/aspectl/.

6 Or to look at it another, more technically accurate, way, Common Lisp comes with a built-in facility for integrating compilers for embedded languages.

### 1.2 Where It Began

Common Lisp is the modern descendant of the Lisp language first conceived by John McCarthy in 1956. Lisp circa 1956 was designed for "symbolic data processing" 7 and derived its name from one of the things it was quite good at: LISt Processing. We've come a long way since then: Common Lisp sports as fine an array of modern data types as you can ask for: a condition system that, as you'll see in Chapter 19, provides a whole level of flexibility missing from the exception systems of languages such as Java, Python, and C++; powerful facilities for doing object-oriented programming; and several language facilities that just don't exist in other programming languages. How is this possible? What on Earth would provoke the evolution of such a well-equipped language?

Well, McCarthy was (and still is) an artificial intelligence (AI) researcher, and many of the features he built into his initial version of the language made it an excellent language for AI programming. During the AI boom of the 1980s, Lisp remained a favorite tool for programmers writing software to solve hard problems such as automated theorem proving, planning and scheduling, and computer vision. These were problems that required a lot of hard-to-write software; to make a dent in them, AI programmers needed a powerful language, and they grew Lisp into the language they needed. And the Cold War helped -- as the Pentagon poured money into the Defense Advanced Research Projects Agency (DARPA), a lot of it went to folks working on problems such as large-scale battlefield simulations, automated planning, and natural language interfaces. These folks also used Lisp and continued pushing it to do what they needed.

The same forces that drove Lisp's feature evolution also pushed the envelope along other dimensions -- big AI problems eat up a lot of computing resources however you code them, and if you run Moore's law in reverse for 20 years, you can imagine how scarce computing resources were on circa-80s hardware. The Lisp guys had to find all kinds of ways to squeeze performance out of their implementations. Modern Common Lisp implementations are the heirs to those early efforts and often include quite sophisticated, native machine code-generating compilers. While today, thanks to Moore's law, it's possible to get usable performance from a purely interpreted language, that's no longer an issue for Common Lisp. As I'll show in Chapter 32, with proper (optional) declarations, a good Lisp compiler can generate machine code quite similar to what might be generated by a C compiler.

The 1980s were also the era of the Lisp Machines, with several companies, most famously Symbolics, producing computers that ran Lisp natively from the chips up. Thus, Lisp became a systems programming language, used for writing the operating system, editors, compilers, and pretty much everything else that ran on the Lisp Machines.

In fact, by the early 1980s, with various AI labs and the Lisp machine vendors all providing their own Lisp implementations, there was such a proliferation of Lisp systems and dialects that the folks at DARPA began to express concern about the Lisp community splintering. To address this concern, a grassroots group of Lisp hackers got together in 1981 and began the process of standardizing a new language called Common Lisp that combined the best features from the existing Lisp dialects. Their work was documented in the book Common Lisp the Language by Guy Steele (Digital Press, 1984) -- CLtL to the Lisp-cognoscenti.

By 1986 the first Common Lisp implementations were available, and the writing was on the wall for the dialects it was intended to replace. In 1996, the American National Standards Institute (ANSI) released a standard for Common Lisp that built on and extended the language specified in CLtL, adding some major new features such as the CLOS and the condition system. And even that wasn't the last word: like CLtL before it, the ANSI standard intentionally leaves room for implementers to experiment with the best way to do things: a full Lisp implementation provides a rich runtime environment with access to GUI widgets, multiple threads of control, TCP/IP sockets, and more. These days Common Lisp is evolving much like other open-source languages -- the folks who use it write the libraries they need and often make them available to others. In the last few years, in particular, there has been a spurt of activity in open-source Lisp libraries.

So, on one hand, Lisp is one of computer science's "classical" languages, based on ideas that have stood the test of time. 8 On the other, it's a thoroughly modern, general-purpose language whose design reflects a deeply pragmatic approach to solving real problems as efficiently and robustly as possible. The only downside of Lisp's "classical" heritage is that lots of folks are still walking around with ideas about Lisp based on some particular flavor of Lisp they were exposed to at some particular time in the nearly half century since McCarthy invented Lisp. If someone tells you Lisp is only interpreted, that it's slow, or that you have to use recursion for everything, ask them what dialect of Lisp they're talking about and whether people were wearing bell-bottoms when they learned it. 9

1『 Common Lisp 已经可以编译成机器码，脱离了解释型语言的范畴了。（2020-12-19）』

7 Lisp 1.5 Programmer's Manual (M.I.T. Press, 1962)

8 Ideas first introduced in Lisp include the if/then/else construct, recursive function calls, dynamic memory allocation, garbage collection, first-class functions, lexical closures, interactive programming, incremental compilation, and dynamic typing.

9 One of the most commonly repeated myths about Lisp is that it's "dead." While it's true that Common Lisp isn't as widely used as, say, Visual Basic or Java, it seems strange to describe a language that continues to be used for new development and that continues to attract new users as "dead." Some recent Lisp success stories include Paul Graham's Viaweb, which became Yahoo Store when Yahoo bought his company; ITA Software's airfare pricing and shopping system, QPX, used by the online ticket seller Orbitz and others; Naughty Dog's game for the PlayStation 2, Jak and Daxter, which is largely written in a domain-specific Lisp dialect Naughty Dog invented called GOAL, whose compiler is itself written in Common Lisp; and the Roomba, the autonomous robotic vacuum cleaner, whose software is written in L, a downwardly compatible subset of Common Lisp. Perhaps even more telling is the growth of the Common-Lisp.net Web site, which hosts open-source Common Lisp projects, and the number of local Lisp user groups that have sprung up in the past couple of years.

3『

[CLiki: the common lisp wiki](https://www.cliki.net/)

[Welcome to Common-Lisp.net!](https://common-lisp.net/)

』

#### But I learned Lisp Once, And IT Wasn't Like what you're describing

If you've used Lisp in the past, you may have ideas about what "Lisp" is that have little to do with Common Lisp. While Common Lisp supplanted most of the dialects it's descended from, it isn't the only remaining Lisp dialect, and depending on where and when you were exposed to Lisp, you may very well have learned one of these other dialects.

Other than Common Lisp, the one general-purpose Lisp dialect that still has an active user community is Scheme. Common Lisp borrowed a few important features from Scheme but never intended to replace it.

1『原来 scheme 是 lisp 的方言，即变种。（2020-10-08）』

Originally designed at M.I.T., where it was quickly put to use as a teaching language for undergraduate computer science courses, Scheme has always been aimed at a different language niche than Common Lisp. In particular, Scheme's designers have focused on keeping the core language as small and as simple as possible. This has obvious benefits for a teaching language and also for programming language researchers who like to be able to formally prove things about languages.

It also has the benefit of making it relatively easy to understand the whole language as specified in the standard. But, it does so at the cost of omitting many useful features that are standardized in Common Lisp. Individual Scheme implementations may provide these features in implementation-specific ways, but their omission from the standard makes it harder to write portable Scheme code than to write portable Common Lisp code.

Scheme also emphasizes a functional programming style and the use of recursion much more than Common Lisp does. If you studied Lisp in college and came away with the impression that it was only an academic language with no real-world application, chances are you learned Scheme. This isn't to say that's a particularly fair characterization of Scheme, but it's even less applicable to Common Lisp, which was expressly designed to be a real-world engineering language rather than a theoretically "pure" language.

If you've learned Scheme, you should also be aware that a number of subtle differences between Scheme and Common Lisp may trip you up. These differences are also the basis for several perennial religious wars between the hotheads in the Common Lisp and Scheme communities. I'll try to point out some of the more important differences as we go along.

Two other Lisp dialects still in widespread use are Elisp, the extension language for the Emacs editor, and Autolisp, the extension language for Autodesk's AutoCAD computer-aided design tool. Although it's possible more lines of Elisp and Autolisp have been written than of any other dialect of Lisp, neither can be used outside their host application, and both are quite old-fashioned Lisps compared to either Scheme or Common Lisp. If you've used one of these dialects, prepare to hop in the Lisp time machine and jump forward several decades.

1『另外两个方言是 Elisp 和 Autolisp，这两个的语法相对于 Common Lisp 和 Scheme 都很老。（2020-10-08）』

### 1.3 Who This Book Is For

This book is for you if you're curious about Common Lisp, regardless of whether you're already convinced you want to use it or if you just want to know what all the fuss is about.

If you've learned some Lisp already but have had trouble making the leap from academic exercises to real programs, this book should get you on your way. On the other hand, you don't have to be already convinced that you want to use Lisp to get something out of this book.

If you're a hard-nosed pragmatist who wants to know what advantages Common Lisp has over languages such as Perl, Python, Java, C, or C#, this book should give you some ideas. Or maybe you don't even care about using Lisp -- maybe you're already sure Lisp isn't really any better than other languages you know but are annoyed by some Lisper telling you that's because you just don't "get it." If so, this book will give you a straight-to-the-point introduction to Common Lisp. If, after reading this book, you still think Common Lisp is no better than your current favorite languages, you'll be in an excellent position to explain exactly why.

I cover not only the syntax and semantics of the language but also how you can use it to write software that does useful stuff. In the first part of the book, I'll cover the language itself, mixing in a few "practical" chapters, where I'll show you how to write real code. Then, after I've covered most of the language, including several parts that other books leave for you to figure out on your own, the remainder of the book consists of nine more practical chapters where I'll help you write several medium-sized programs that actually do things you might find useful: filter spam, parse binary files, catalog MP3s, stream MP3s over a network, and provide a Web interface for the MP3 catalog and server.

After you finish this book, you'll be familiar with all the most important features of the language and how they fit together, you'll have used Common Lisp to write several nontrivial programs, and you'll be well prepared to continue exploring the language on your own. While everyone's road to Lisp is different, I hope this book will help smooth the way for you. So, let's begin.
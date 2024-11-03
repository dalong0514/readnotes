## 记忆时间

## 目录

0501 Functions

0601 Variables

0701 Macros: Standard Control Constructs

0801 Macros: Defining Your Own

## 0501. Functions

After the rules of syntax and semantics, the three most basic components of all Lisp programs are functions, variables and macros. You used all three while building the database in Chapter 3, but I glossed over a lot of the details of how they work and how to best use them. I'll devote the next few chapters to these three topics, starting with functions, which -- like their counterparts in other languages -- provide the basic mechanism for abstracting, well, functionality.

The bulk of Lisp itself consists of functions. More than three quarters of the names defined in the language standard name functions. All the built-in data types are defined purely in terms of what functions operate on them. Even Lisp's powerful object system is built upon a conceptual extension to functions, generic functions, which I'll cover in Chapter 16.

And, despite the importance of macros to The Lisp Way, in the end all real functionality is provided by functions. Macros run at compile time, so the code they generate -- the code that will actually make up the program after all the macros are expanded -- will consist entirely of calls to functions and special operators. Not to mention, macros themselves are also functions, albeit functions that are used to generate code rather than to perform the actions of the program. 1

1 Despite the importance of functions in Common Lisp, it isn’t really accurate to describe it as a functional language. It’s true some of Common Lisp’s features, such as its list manipulation functions, are designed to be used in a body-form* style and that Lisp has a prominent place in the history of functional programming — McCarthy introduced many ideas that are now considered important in functional programming — but Common Lisp was intentionally designed to support many different styles of programming. In the Lisp family, Scheme is the nearest thing to a “pure” functional language, and even it has several features that disqualify it from absolute purity compared to languages such as Haskell and ML.

2『 Lisp 语言的三大核心元素：函数、变量和宏，做一张主题卡片。』——已完成

### 5.1 Defining New Functions

Normally functions are defined using the DEFUN macro. The basic skeleton of a DEFUN looks like this:

```c
(defun name (parameter*) 
  "Optional documentation string." 
  body-form*
)
```

Any symbol can be used as a function name. 2 Usually function names contain only alphabetic characters and hyphens, but other characters are allowed and are used in certain naming conventions. For instance, functions that convert one kind of value to another sometimes use -> in the name. For example, a function to convert strings to widgets might be called `string->widget`. The most important naming convention is the one mentioned in Chapter 2, which is that you construct compound names with hyphens rather than underscores or inner caps. Thus, frob-widget is better Lisp style than either frob_widget or frobWidget.

A function's parameter list defines the variables that will be used to hold the arguments passed to the function when it's called. 3 If the function takes no arguments, the list is empty, written as (). Different flavors of parameters handle required, optional, multiple, and keyword arguments. I'll discuss the details in the next section.

If a string literal follows the parameter list, it's a documentation string that should describe the purpose of the function. When the function is defined, the documentation string will be associated with the name of the function and can later be obtained using the DOCUMENTATION function. 4

Finally, the body of a DEFUN consists of any number of Lisp expressions. They will be evaluated in order when the function is called and the value of the last expression is returned as the value of the function. Or the RETURN-FROM special operator can be used to return immediately from anywhere in a function, as I'll discuss in a moment.

1『真好，common lisp 就有直接从函数体里返回的函数 `return-from`，目前 autolisp 里没找到，所以没法实现多个函数出口啊。（2020-10-28）』

In Chapter 2 we wrote a hello-world function, which looked like this:

```c
(defun hello-world () 
  (format t "hello, world")
)
```

You can now analyze the parts of this function. Its name is hello-world, its parameter list is empty so it takes no arguments, it has no documentation string, and its body consists of one expression.

```c
(format t "hello, world")
```

The following is a slightly more complex function:

```c
(defun verbose-sum (x y) 
  "Sum any two numbers after printing a message." 
  (format t "Summing ~d and ~d.~%" x y) 
  (+ x y)
)
```

This function is named verbose-sum, takes two arguments that will be bound to the parameters x and y, has a documentation string, and has a body consisting of two expressions. The value returned by the call to + becomes the return value of verbose-sum.

2 Well, almost any symbol. It’s undefined what happens if you use any of the names defined in the language standard as a name for one of your own functions. However, as you’ll see in Chapter 21, the Lisp package system allows you to create names in different namespaces, so this isn’t really an issue.

3 Parameter lists are sometimes also called lambda lists because of the historical relationship between Lisp’s notion of functions and the lambda calculus.

4 For example, the following:

```c
(documentation 'foo 'function)
```

returns the documentation string for the function foo. Note, however, that documentation strings are intended for human consumption, not programmatic access. A Lisp implementation isn’t required to store them and is allowed to discard them at any time, so portable programs shouldn’t depend on their presence. In some implementations an implementation-defined variable needs to be set before it will store documentation strings.

### 5.2 Function Parameter Lists

There's not a lot more to say about function names or documentation strings, and it will take a good portion of the rest of this book to describe all the things you can do in the body of a function, which leaves us with the parameter list.

The basic purpose of a parameter list is, of course, to declare the variables that will receive the arguments passed to the function. When a parameter list is a simple list of variable names -- as in verbose-sum -- the parameters are called required parameters. When a function is called, it must be supplied with one argument for every required parameter. Each parameter is bound to the corresponding argument. If a function is called with too few or too many arguments, Lisp will signal an error.

However, Common Lisp's parameter lists also give you more flexible ways of mapping the arguments in a function call to the function's parameters. In addition to required parameters, a function can have optional parameters. Or a function can have a single parameter that's bound to a list containing any extra arguments. And, finally, arguments can be mapped to parameters using keywords rather than position. Thus, Common Lisp's parameter lists provide a convenient solution to several common coding problems.

### 5.3 Optional Parameters

While many functions, like verbose-sum, need only required parameters, not all functions are quite so simple. Sometimes a function will have a parameter that only certain callers will care about, perhaps because there's a reasonable default value. An example is a function that creates a data structure that can grow as needed. Since the data structure can grow, it doesn't matter -- from a correctness point of view -- what the initial size is. But callers who have a good idea how many items they're going to put into the data structure may be able to improve performance by specifying a specific initial size. Most callers, though, would probably rather let the code that implements the data structure pick a good general-purpose value. In Common Lisp you can accommodate both kinds of callers by using an optional parameter; callers who don't care will get a reasonable default, and other callers can provide a specific value. 5

To define a function with optional parameters, after the names of any required parameters, place the symbol `&optional` followed by the names of the optional parameters. A simple example looks like this:

```c
(defun foo (a b &optional c d) 
  (list a b c d)
)
```

When the function is called, arguments are first bound to the required parameters. After all the required parameters have been given values, if there are any arguments left, their values are assigned to the optional parameters. If the arguments run out before the optional parameters do, the remaining optional parameters are bound to the value NIL. Thus, the function defined previously gives the following results:

```c
(foo 1 2) ==> (1 2 NIL NIL) 
(foo 1 2 3) ==> (1 2 3 NIL) 
(foo 1 2 3 4) ==> (1 2 3 4)
```

Lisp will still check that an appropriate number of arguments are passed to the function -- in this case between two and four, inclusive -- and will signal an error if the function is called with too few or too many.

Of course, you'll often want a different default value than NIL. You can specify the default value by replacing the parameter name with a list containing a name and an expression. The expression will be evaluated only if the caller doesn't pass enough arguments to provide a value for the optional parameter. The common case is simply to provide a value as the expression.

```c
(defun foo (a &optional (b 10)) 
  (list a b)
)
```

1『默认值都能实现，赞！（2020-10-28）』

This function requires one argument that will be bound to the parameter a. The second parameter, b, will take either the value of the second argument, if there is one, or 10.

```c
(foo 1 2) ==> (1 2) 
(foo 1) ==> (1 10)
```

Sometimes, however, you may need more flexibility in choosing the default value. You may want to compute a default value based on other parameters. And you can -- the default-value expression can refer to parameters that occur earlier in the parameter list. If you were writing a function that returned some sort of representation of a rectangle and you wanted to make it especially convenient to make squares, you might use an argument list like this:

```c
(defun make-rectangle (width &optional (height width)) ...)
```

which would cause the height parameter to take the same value as the width parameter unless explicitly specified.

Occasionally, it's useful to know whether the value of an optional argument was supplied by the caller or is the default value. Rather than writing code to check whether the value of the parameter is the default (which doesn't work anyway, if the caller happens to explicitly pass the default value), you can add another variable name to the parameter specifier after the default-value expression. This variable will be bound to true if the caller actually supplied an argument for this parameter and NIL otherwise. By convention, these variables are usually named the same as the actual parameter with a "-supplied-p" on the end. For example:

```c
(defun foo (a b &optional (c 3 c-supplied-p)) 
  (list a b c c-supplied-p)
)
```

This gives results like this:

```c
(foo 1 2) ==> (1 2 3 NIL) 
(foo 1 2 3) ==> (1 2 3 T) 
(foo 1 2 4) ==> (1 2 4 T)
```

5 In languages that don’t support optional parameters directly, programmers typically find ways to simulate them. One technique is to use distinguished “no-value” values that the caller can pass to indicate they want the default value of a given parameter. In C, for example, it’s common to use NULL as such a distinguished value. However, such a protocol between the function and its callers is ad hoc — in some functions or for some arguments NULL may be the distinguished value while in other functions or for other arguments the magic value may be -1 or some #defined constant. In languages such as Java that support overloading a single method name with multiple definitions, optional parameters can also be simulated by providing methods with the same name but different numbers of arguments and having the methods with fewer arguments call the “real” method with default values for the missing arguments.

1『上面教你如何来模拟可选形参，在 autolisp 那边试验过，同样的函数名不同个数的形参，系统会自动根据参数个数正确的匹配到对应的函数调用，当时就想利用这个特点来模拟函数的多态行为。（2020-10-28）』

### 5.4 Rest Parameters

Optional parameters are just the thing when you have discrete parameters for which the caller may or may not want to provide values. But some functions need to take a variable number of arguments. Several of the built-in functions you've seen already work this way. FORMAT has two required arguments, the stream and the control string. But after that it needs a variable number of arguments depending on how many values need to be interpolated into the control string. The + function also takes a variable number of arguments -- there's no particular reason to limit it to summing just two numbers; it will sum any number of values. (It even works with zero arguments, returning 0, the identity under addition.) The following are all legal calls of those two functions:

```c
(format t "hello, world") 
(format t "hello, ~a" name) 
(format t "x: ~d y: ~d" x y) 
(+) 
(+ 1) 
(+ 1 2) 
(+ 1 2 3)
```

Obviously, you could write functions taking a variable number of arguments by simply giving them a lot of optional parameters. But that would be incredibly painful -- just writing the parameter list would be bad enough, and that doesn't get into dealing with all the parameters in the body of the function. To do it properly, you'd have to have as many optional parameters as the number of arguments that can legally be passed in a function call. This number is implementation dependent but guaranteed to be at least 50. And in current implementations it ranges from 4,096 to 536,870,911.6 Blech. That kind of mind-bending tedium is definitely not The Lisp Way.

Instead, Lisp lets you include a catchall parameter after the symbol &rest. If a function includes a &rest parameter, any arguments remaining after values have been doled out to all the required and optional parameters are gathered up into a list that becomes the value of the &rest parameter. Thus, the parameter lists for FORMAT and + probably look something like this:

```c
(defun format (stream string &rest values) ...) 
(defun + (&rest numbers) ...)
```

6 The constant CALL-ARGUMENTS-LIMIT tells you the implementation-specific value.

### 5.5 Keyword Parameters

Optional and rest parameters give you quite a bit of flexibility, but neither is going to help you out much in the following situation: Suppose you have a function that takes four optional parameters. Now suppose that most of the places the function is called, the caller wants to provide a value for only one of the four parameters and, further, that the callers are evenly divided as to which parameter they will use.

The callers who want to provide a value for the first parameter are fine -- they just pass the one optional argument and leave off the rest. But all the other callers have to pass some value for between one and three arguments they don't care about. Isn't that exactly the problem optional parameters were designed to solve?

Of course it is. The problem is that optional parameters are still positional -- if the caller wants to pass an explicit value for the fourth optional parameter, it turns the first three optional parameters into required parameters for that caller. Luckily, another parameter flavor, keyword parameters, allow the caller to specify which values go with which parameters.

To give a function keyword parameters, after any required, &optional, and &rest parameters you include the symbol &key and then any number of keyword parameter specifiers, which work like optional parameter specifiers. Here's a function that has only keyword parameters:

```c
(defun foo (&key a b c) 
  (list a b c)
)
```

When this function is called, each keyword parameters is bound to the value immediately following a keyword of the same name. Recall from Chapter 4 that keywords are names that start with a colon and that they're automatically defined as self-evaluating constants.

If a given keyword doesn't appear in the argument list, then the corresponding parameter is assigned its default value, just like an optional parameter. Because the keyword arguments are labeled, they can be passed in any order as long as they follow any required arguments. For instance, foo can be invoked as follows:

```c
(foo) ==> (NIL NIL NIL) 
(foo :a 1) ==> (1 NIL NIL) 
(foo :b 1) ==> (NIL 1 NIL) 
(foo :c 1) ==> (NIL NIL 1) 
(foo :a 1 :c 3) ==> (1 NIL 3) 
(foo :a 1 :b 2 :c 3) ==> (1 2 3) 
(foo :a 1 :c 3 :b 2) ==> (1 2 3)
```

As with optional parameters, keyword parameters can provide a default value form and the name of a supplied-p variable. In both keyword and optional parameters, the default value form can refer to parameters that appear earlier in the parameter list.

```c
(defun foo (&key (a 0) (b 0 b-supplied-p) (c (+ a b))) 
  (list a b c b-supplied-p)
) 

(foo :a 1) ==> (1 0 1 NIL) 
(foo :b 1) ==> (0 1 1 T) 
(foo :b 1 :c 4) ==> (0 1 4 T) 
(foo :a 2 :b 1 :c 4) ==> (2 1 4 T)
```

Also, if for some reason you want the keyword the caller uses to specify the parameter to be different from the name of the actual parameter, you can replace the parameter name with another list containing the keyword to use when calling the function and the name to be used for the parameter. The following definition of foo:

```c
(defun foo (&key ((:apple a)) ((:box b) 0) ((:charlie c) 0 c-supplied-p)) 
  (list a b c c-supplied-p)
)
```

lets the caller call it like this:

```c
(foo :apple 10 :box 20 :charlie 30) ==> (10 20 30 T)
```

This style is mostly useful if you want to completely decouple the public API of the function from the internal details, usually because you want to use short variable names internally but descriptive keywords in the API. It's not, however, very frequently used.

2『经验证 autolisp 里没法实现 key 的形参。（2020-10-28）』

### 5.6 Mixing Different Parameter Types

It's possible, but rare, to use all four flavors of parameters in a single function. Whenever more than one flavor of parameter is used, they must be declared in the order I've discussed them: first the names of the required parameters, then the optional parameters, then the rest parameter, and finally the keyword parameters. Typically, however, in functions that use multiple flavors of parameters, you'll combine required parameters with one other flavor or possibly combine &optional and &rest parameters. The other two combinations, either &optional or &rest parameters combined with &key parameters, can lead to somewhat surprising behavior.

Combining &optional and &key parameters yields surprising enough results that you should probably avoid it altogether. The problem is that if a caller doesn't supply values for all the optional parameters, then those parameters will eat up the keywords and values intended for the keyword parameters. For instance, this function unwisely mixes &optional and &key parameters:

```c
(defun foo (x &optional y &key z) 
  (list x y z)
)
```

If called like this, it works fine:

```c
(foo 1 2 :z 3) ==> (1 2 3)
```

And this is also fine:

```c
(foo 1) ==> (1 nil nil)
```

But this will signal an error:

```c
(foo 1 :z 3) ==> ERROR
```

This is because the keyword :z is taken as a value to fill the optional y parameter, leaving only the argument 3 to be processed. At that point, Lisp will be expecting either a keyword/value pair or nothing and will complain. Perhaps even worse, if the function had had two &optional parameters, this last call would have resulted in the values :z and 3 being bound to the two &optional parameters and the &key parameter z getting the default value NIL with no indication that anything was amiss.

In general, if you find yourself writing a function that uses both &optional and &key parameters, you should probably just change it to use all &key parameters -- they're more flexible, and you can always add new keyword parameters without disturbing existing callers of the function. You can also remove keyword parameters, as long as no one is using them. 7 In general, using keyword parameters helps make code much easier to maintain and evolve -- if you need to add some new behavior to a function that requires new parameters, you can add keyword parameters without having to touch, or even recompile, any existing code that calls the function.

You can safely combine &rest and &key parameters, but the behavior may be a bit surprising initially. Normally the presence of either &rest or &key in a parameter list causes all the values remaining after the required and &optional parameters have been filled in to be processed in a particular way -- either gathered into a list for a &rest parameter or assigned to the appropriate &key parameters based on the keywords. If both &rest and &key appear in a parameter list, then both things happen -- all the remaining values, which include the keywords themselves, are gathered into a list that's bound to the &rest parameter, and the appropriate values are also bound to the &key parameters. So, given this function:

```c
(defun foo (&rest rest &key a b c) 
  (list rest a b c)
)
```

you get this result:

```c
(foo :a 1 :b 2 :c 3) ==> ((:A 1 :B 2 :C 3) 1 2 3)
```

7 Four standard functions take both &optional and &key arguments — READ-FROM-STRING, PARSE-NAMESTRING, WRITE-LINE, and WRITE-STRING. They were left that way during standardization for backward compatibility with earlier Lisp dialects. READ-FROM-STRING tends to be the one that catches new Lisp programmers most frequently — a call such as (read-from-string s :start 10) seems to ignore the :start keyword argument, reading from index 0 instead of 10. That’s because READ-FROM-STRING also has two &optional parameters that swallowed up the arguments :start and 10.

### 5.7 Function Return Values

All the functions you've written so far have used the default behavior of returning the value of the last expression evaluated as their own return value. This is the most common way to return a value from a function.

However, sometimes it's convenient to be able to return from the middle of a function such as when you want to break out of nested control constructs. In such cases you can use the RETURN-FROM special operator to immediately return any value from the function.

1-2『

在 autolisp 里总算找到了替代函数 [vl-exit-with-value (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-80622A39-A5E8-4E68-824E-E66BD8D3E9DE)。通过它可以实现函数的多个出口。

```c

```

函数多出口的实现，做一张任意卡片。（2021-01-05）——已完成

』

You'll see in Chapter 20 that RETURN-FROM is actually not tied to functions at all; it's used to return from a block of code defined with the BLOCK special operator. However, DEFUN automatically wraps the whole function body in a block with the same name as the function. So, evaluating a RETURN-FROM with the name of the function and the value you want to return will cause the function to immediately exit with that value. RETURN-FROM is a special operator whose first "argument" is the name of the block from which to return. This name isn't evaluated and thus isn't quoted.

The following function uses nested loops to find the first pair of numbers, each less than 10, whose product is greater than the argument, and it uses RETURN-FROM to return the pair as soon as it finds it:

```c
(defun foo (n) 
  (dotimes (i 10) 
    (dotimes (j 10) 
      (when (> (* i j) n) 
        (return-from foo (list i j))
      )
    )
  )
)
```

Admittedly, having to specify the name of the function you're returning from is a bit of a pain -- for one thing, if you change the function's name, you'll need to change the name used in the RETURN-FROM as well. 8 But it's also the case that explicit RETURN-FROMs are used much less frequently in Lisp than return statements in C-derived languages, because all Lisp expressions, including control constructs such as loops and conditionals, evaluate to a value. So it's not much of a problem in practice.

8 Another macro, RETURN, doesn’t require a name. However, you can’t use it instead of RETURN-FROM to avoid having to specify the function name; it’s syntactic sugar for returning from a block named NIL. I’ll cover it, along with the details of BLOCK and RETURN-FROM, in Chapter 20.

### 5.8 Functions As Data, a.k.a. Higher-Order Functions

While the main way you use functions is to call them by name, a number of situations exist where it's useful to be able treat functions as data. For instance, if you can pass one function as an argument to another, you can write a general-purpose sorting function while allowing the caller to provide a function that's responsible for comparing any two elements. Then the same underlying algorithm can be used with many different comparison functions. Similarly, callbacks and hooks depend on being able to store references to code in order to run it later. Since functions are already the standard way to abstract bits of code, it makes sense to allow functions to be treated as data. 9

1-2『编程语言里，能把函数当作数据，个人感觉太有必要了，将函数作为参数传进另一个函数，构建复杂的模型。函数作为数据，做一张主题卡。（2020-10-28）』 —  — 已完成

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

FUNCALL is the one to use when you know the number of arguments you're going to pass to the function at the time you write the code. The first argument to FUNCALL is the function object to be invoked, and the rest of the arguments are passed onto that function. Thus, the following two expressions are equivalent:

```c
(foo 1 2 3) === (funcall #'foo 1 2 3)
```

However, there's little point in using FUNCALL to call a function whose name you know when you write the code. In fact, the previous two expressions will quite likely compile to exactly the same machine instructions.

The following function demonstrates a more apt use of FUNCALL. It accepts a function object as an argument and plots a simple ASCII-art histogram of the values returned by the argument function when it's invoked on the values from min to max, stepping by step.

```c
(defun plot (fn min max step) 
  (loop for i from min to max by step do 
    (loop repeat (funcall fn i) do (format t "*")) 
    (format t "~%")
  )
)
```

The FUNCALL expression computes the value of the function for each value of i. The inner LOOP uses that computed value to determine how many times to print an asterisk to standard output.

Note that you don't use FUNCTION or `#'` to get the function value of fn; you want it to be interpreted as a variable because it's the variable's value that will be the function object. You can call plot with any function that takes a single numeric argument, such as the built-in function EXP that returns the value of e raised to the power of its argument.

```c
CL-USER> (plot #'exp 0 4 1/2) 
*
*
**
****
*******
NIL
```

FUNCALL, however, doesn't do you any good when the argument list is known only at runtime. For instance, to stick with the plot function for another moment, suppose you've obtained a list containing a function object, a minimum and maximum value, and a step value. In other words, the list contains the values you want to pass as arguments to plot. Suppose this list is in the variable plot-data. You could invoke plot on the values in that list like this:

```c
(plot 
  (first plot-data) 
  (second plot-data) 
  (third plot-data) 
  (fourth plot-data)
)
```

This works fine, but it's pretty annoying to have to explicitly unpack the arguments just so you can pass them to plot.

That's where APPLY comes in. Like FUNCALL, the first argument to APPLY is a function object. But after the function object, instead of individual arguments, it expects a list. It then applies the function to the values in the list. This allows you to write the following instead:

```c
(apply #'plot plot-data)
```

As a further convenience, APPLY can also accept "loose" arguments as long as the last argument is a list. Thus, if plot-data contained just the min, max, and step values, you could still use APPLY like this to plot the EXP function over that range:

```c
(apply #'plot #'exp plot-data)
```

APPLY doesn't care about whether the function being applied takes &optional, &rest, or &key arguments -- the argument list produced by combining any loose arguments with the final list must be a legal argument list for the function with enough arguments for all the required parameters and only appropriate keyword parameters.

9 Lisp, of course, isn’t the only language to treat functions as data. C uses function pointers, Perl uses subroutine references, Python uses a scheme similar to Lisp, and C# introduces delegates, essentially typed function pointers, as an improvement over Java’s rather clunky reflection and anonymous class mechanisms.

10 The exact printed representation of a function object will differ from implementation to implementation.

11 The best way to think of FUNCTION is as a special kind of quotation. QUOTEing a symbol prevents it from being evaluated at all, resulting in the symbol itself rather than the value of the variable named by that symbol. FUNCTION also circumvents the normal evaluation rule but, instead of preventing the symbol from being evaluated at all, causes it to be evaluated as the name of a function, just the way it would if it were used as the function name in a function call expression.

12 There’s actually a third, the special operator MULTIPLE-VALUE-CALL, but I’ll save that for when I discuss expressions that return multiple values in Chapter 20.

### 5.9 Anonymous Functions

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

Anonymous functions can be useful when you need to pass a function as an argument to another function and the function you need to pass is simple enough to express inline. For instance, suppose you wanted to plot the function 2x. You could define the following function:

```c
(defun double (x) (* 2 x))
```

which you could then pass to plot.

```c
CL-USER> (plot #'double 0 10 1) 
** 
**** 
****** 
******** 
********** 
************ 
************** 
**************** 
****************** 
******************** 
NIL
```

But it's easier, and arguably clearer, to write this:

```c
CL-USER> (plot #'(lambda (x) (* 2 x)) 0 10 1) 
** 
**** 
****** 
******** 
********** 
************ 
************** 
**************** 
****************** 
******************** 
NIL
```

The other important use of LAMBDA expressions is in making closures, functions that capture part of the environment where they're created. You used closures a bit in Chapter 3, but the details of how closures work and what they're used for is really more about how variables work than functions, so I'll save that discussion for the next chapter.

## 0601. Variables

The next basic building block we need to look at are variables. Common Lisp supports two kinds of variables: lexical and dynamic. 1 These two types correspond roughly to "local" and "global" variables in other languages. However, the correspondence is only approximate. On one hand, some languages' "local" variables are in fact much like Common Lisp's dynamic variables. 2 And on the other, some languages' local variables are lexically scoped without providing all the capabilities provided by Common Lisp's lexical variables. In particular, not all languages that provide lexically scoped variables support closures.

To make matters a bit more confusing, many of the forms that deal with variables can be used with both lexical and dynamic variables. So I'll start by discussing a few aspects of Lisp's variables that apply to both kinds and then cover the specific characteristics of lexical and dynamic variables. Then I'll discuss Common Lisp's general-purpose assignment operator, SETF, which is used to assign new values to variables and just about every other place that can hold a value.

1『晕死，这里才突然意识到，command lisp 里的 `setf` 如同 autolisp 里的 `setq`。（2020-11-03）』

1 Dynamic variables are also sometimes called special variables for reasons you’ll see later in this chapter. It’s important to be aware of this synonym, as some folks (and Lisp implementations) use one term while others use the other.

2 Early Lisps tended to use dynamic variables for local variables, at least when interpreted. Elisp, the Lisp dialect used in Emacs, is a bit of a throwback in this respect, continuing to support only dynamic variables. Other languages have recapitulated this transition from dynamic to lexical variables — Perl’s local variables, for instance, are dynamic while its my variables, introduced in Perl 5, are lexical. Python never had true dynamic variables but only introduced true lexical scoping in version 2.2. (Python’s lexical variables are still somewhat limited compared to Lisp’s because of the conflation of assignment and binding in the language’s syntax.)

### 6.1 Variable Basics

As in other languages, in Common Lisp variables are named places that can hold a value. However, in Common Lisp, variables aren't typed the way they are in languages such as Java or C++. That is, you don't need to declare the type of object that each variable can hold. Instead, a variable can hold values of any type and the values carry type information that can be used to check types at runtime. Thus, Common Lisp is dynamically typed -- type errors are detected dynamically. For instance, if you pass something other than a number to the + function, Common Lisp will signal a type error. On the other hand, Common Lisp is a strongly typed language in the sense that all type errors will be detected -- there's no way to treat an object as an instance of a class that it's not. 3

1-2『这里又见「动态语言」的概念，做一张术语卡片。』 —  — 已完成

All values in Common Lisp are, conceptually at least, references to objects. 4 Consequently, assigning a variable a new value changes what object the variable refers to but has no effect on the previously referenced object. However, if a variable holds a reference to a mutable object, you can use that reference to modify the object, and the modification will be visible to any code that has a reference to the same object.

One way to introduce new variables you've already used is to define function parameters. As you saw in the previous chapter, when you define a function with DEFUN, the parameter list defines the variables that will hold the function's arguments when it's called. For example, this function defines three variables -- x, y, and z -- to hold its arguments.

```c
(defun foo (x y z) 
  (+ x y z)
)
```

Each time a function is called, Lisp creates new bindings to hold the arguments passed by the function's caller. A binding is the runtime manifestation of a variable. A single variable -- the thing you can point to in the program's source code -- can have many different bindings during a run of the program. A single variable can even have multiple bindings at the same time; parameters to a recursive function, for example, are rebound for each call to the function.

As with all Common Lisp variables, function parameters hold object references. 5 Thus, you can assign a new value to a function parameter within the body of the function, and it will not affect the bindings created for another call to the same function. But if the object passed to a function is mutable and you change it in the function, the changes will be visible to the caller since both the caller and the callee will be referencing the same object.

1『看到这里提到的「可变」，渐渐对「不可变性」有那么一点点感觉了。（2020-11-03）』

Another form that introduces new variables is the LET special operator. The skeleton of a LET form looks like this:

```c
(let (variable*) 
  body-form*
)
```

where each variable is a variable initialization form. Each initialization form is either a list containing a variable name and an initial value form or -- as a shorthand for initializing the variable to NIL -- a plain variable name. The following LET form, for example, binds the three variables x, y, and z with initial values 10, 20, and NIL:

```c
(let ((x 10) (y 20) z) 
  ...
)
```

When the LET form is evaluated, all the initial value forms are first evaluated. Then new bindings are created and initialized to the appropriate initial values before the body forms are executed. Within the body of the LET, the variable names refer to the newly created bindings. After the LET, the names refer to whatever, if anything, they referred to before the LET.

The value of the last expression in the body is returned as the value of the LET expression. Like function parameters, variables introduced with LET are rebound each time the LET is entered. 6

The scope of function parameters and LET variables -- the area of the program where the variable name can be used to refer to the variable's binding -- is delimited by the form that introduces the variable. This form -- the function definition or the LET -- is called the binding form. As you'll see in a bit, the two types of variables -- lexical and dynamic -- use two slightly different scoping mechanisms, but in both cases the scope is delimited by the binding form.

If you nest binding forms that introduce variables with the same name, then the bindings of the innermost variable shadows the outer bindings. For instance, when the following function is called, a binding is created for the parameter x to hold the function's argument. Then the first LET creates a new binding with the initial value 2, and the inner LET creates yet another binding, this one with the initial value 3. The bars on the right mark the scope of each binding.

```c
(defun foo (x) ; x is argument
  (format t "Parameter: ~a~%" x) 
  (let ((x 2)) ; x is 2 
    (format t "Outer LET: ~a~%" x) 
    (let ((x 3)) ; x is 3 
      (format t "Inner LET: ~a~%" x)
    ) 
    (format t "Outer LET: ~a~%" x)
  )
  (format t "Parameter: ~a~%" x)
) 
```

Each reference to x will refer to the binding with the smallest enclosing scope. Once control leaves the scope of one binding form, the binding from the immediately enclosing scope is unshadowed and x refers to it instead. Thus, calling foo results in this output:

```c
CL-USER> (foo 1) 
Parameter: 1 
Outer LET: 2 
Inner LET: 3 
Outer LET: 2 
Parameter: 1 
NIL
```

In future chapters I'll discuss other constructs that also serve as binding forms -- any construct that introduces a new variable name that's usable only within the construct is a binding form.

For instance, in Chapter 7 you'll meet the DOTIMES loop, a basic counting loop. It introduces a variable that holds the value of a counter that's incremented each time through the loop. The following loop, for example, which prints the numbers from 0 to 9, binds the variable x:

```c
(dotimes (x 10) 
  (format t "~d " x)
)
```

Another binding form is a variant of LET, `LET*.` The difference is that in a LET, the variable names can be used only in the body of the LET -- the part of the LET after the variables list -- but in a `LET*`, the initial value forms for each variable can refer to variables introduced earlier in the variables list. Thus, you can write the following:

```c
(let* ((x 10) 
       (y (+ x 10))) 
  (list x y)
)
```

but not this:

```c
(let ((x 10) 
      (y (+ x 10))) 
  (list x y)
)
```

However, you could achieve the same result with nested LETs.

```c
(let ((x 10)) 
  (let ((y (+ x 10))) 
    (list x y)
  )
)
```

3 Actually, it’s not quite true to say that all type errors will always be detected — it’s possible to use optional declarations to tell the compiler that certain variables will always contain objects of a particular type and to turn off runtime type checking in certain regions of code. However, declarations of this sort are used to optimize code after it has been developed and debugged, not during normal development.

4 As an optimization certain kinds of objects, such as integers below a certain size and characters, may be represented directly in memory where other objects would be represented by a pointer to the actual object. However, since integers and characters are immutable, it doesn’t matter that there may be multiple copies of “the same” object in different variables. This is the root of the difference between EQ and EQL discussed in Chapter 4.

1『这里又见到「不可变性」，函数式编程里核心的一个概念。上面提到的，整数和字符串在 lisp 里是不可变型的数据类型，但作为变量，整数是可以赋值不同的数的啊，难道是分配给整数的内存空间只能放整数的意思？所以说目前还是不太明白其不变性。（2020-11-03）』

5 In compiler-writer terms Common Lisp functions are “pass-by-value.” However, the values that are passed are references to objects. This is similar to how Java and Python work.

6 The variables in LET forms and function parameters are created by exactly the same mechanism. In fact, in some Lisp dialects — though not Common Lisp — LET is simply a macro that expands into a call to an anonymous function. That is, in those dialects, the following:

```c
(let ((x 10)) (format t "~a" x))
```

is a macro form that expands into this:

```c
((lambda (x) (format t "~a" x)) 10)
```

### 6.2 Lexical Variables and Closures

By default all binding forms in Common Lisp introduce lexically scoped variables. Lexically scoped variables can be referred to only by code that's textually within the binding form. Lexical scoping should be familiar to anyone who has programmed in Java, C, Perl, or Python since they all provide lexically scoped "local" variables. For that matter, Algol programmers should also feel right at home, as Algol first introduced lexical scoping in the 1960s.

However, Common Lisp's lexical variables are lexical variables with a twist, at least compared to the original Algol model. The twist is provided by the combination of lexical scoping with nested functions. By the rules of lexical scoping, only code textually within the binding form can refer to a lexical variable. But what happens when an anonymous function contains a reference to a lexical variable from an enclosing scope? For instance, in this expression:

```c
(let ((count 0)) #'(lambda () (setf count (1+ count))))
```

the reference to count inside the LAMBDA form should be legal according to the rules of lexical scoping. Yet the anonymous function containing the reference will be returned as the value of the LET form and can be invoked, via FUNCALL, by code that's not in the scope of the LET. So what happens? As it turns out, when count is a lexical variable, it just works. The binding of count created when the flow of control entered the LET form will stick around for as long as needed, in this case for as long as someone holds onto a reference to the function object returned by the LET form. The anonymous function is called a closure because it "closes over" the binding created by the LET.

1-2『又见闭包 closure，不过这里目前介绍的闭包概念没弄明白。做一张术语卡片。（2020-11-03）』 —  — 已完成

The key thing to understand about closures is that it's the binding, not the value of the variable, that's captured. Thus, a closure can not only access the value of the variables it closes over but can also assign new values that will persist between calls to the closure. For instance, you can capture the closure created by the previous expression in a global variable like this:

```c
(defparameter *fn* 
  (let ((count 0)) 
       #'(lambda () (setf count (1+ count)))
  )
)
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

### 6.3 Dynamic, a.k.a. Special, Variables

Lexically scoped bindings help keep code understandable by limiting the scope, literally, in which a given name has meaning. This is why most modern languages use lexical scoping for local variables. Sometimes, however, you really want a global variable -- a variable that you can refer to from anywhere in your program. While it's true that indiscriminate use of global variables can turn code into spaghetti nearly as quickly as unrestrained use of goto, global variables do have legitimate uses and exist in one form or another in almost every programming language. 7 And as you'll see in a moment, Lisp's version of global variables, dynamic variables, are both more useful and more manageable.

Common Lisp provides two ways to create global variables: DEFVAR and DEFPARAMETER. Both forms take a variable name, an initial value, and an optional documentation string. After it has been DEFVARed or DEFPARAMETERed, the name can be used anywhere to refer to the current binding of the global variable. As you've seen in previous chapters, global variables are conventionally named with names that start and end with `*`. You'll see later in this section why it's quite important to follow that naming convention. Examples of DEFVAR and DEFPARAMETER look like this:

```c
(defvar *count* 0 "Count of widgets made so far.") 
(defparameter *gap-tolerance* 0.001 "Tolerance to be allowed in widget gaps.")
```

The difference between the two forms is that DEFPARAMETER always assigns the initial value to the named variable while DEFVAR does so only if the variable is undefined. A DEFVAR form can also be used with no initial value to define a global variable without giving it a value. Such a variable is said to be unbound.

Practically speaking, you should use DEFVAR to define variables that will contain data you'd want to keep even if you made a change to the source code that uses the variable. For instance, suppose the two variables defined previously are part of an application for controlling a widget factory. It's appropriate to define the `*count*` variable with DEFVAR because the number of widgets made so far isn't invalidated just because you make some changes to the widget-making code. 8

On the other hand, the variable `*gap-tolerance*` presumably has some effect on the behavior of the widget-making code itself. If you decide you need a tighter or looser tolerance and change the value in the DEFPARAMETER form, you'd like the change to take effect when you recompile and reload the file.

After defining a variable with DEFVAR or DEFPARAMETER, you can refer to it from anywhere. For instance, you might define this function to increment the count of widgets made:

```c
(defun increment-widget-count () 
  (incf *count*)
)
```

The advantage of global variables is that you don't have to pass them around. Most languages store the standard input and output streams in global variables for exactly this reason -- you never know when you're going to want to print something to standard out, and you don't want every function to have to accept and pass on arguments containing those streams just in case someone further down the line needs them.

However, once a value, such as the standard output stream, is stored in a global variable and you have written code that references that global variable, it's tempting to try to temporarily modify the behavior of that code by changing the variable's value.

For instance, suppose you're working on a program that contains some low-level logging functions that print to the stream in the global variable `*standard-output*`. Now suppose that in part of the program you want to capture all the output generated by those functions into a file. You might open a file and assign the resulting stream to `*standard-output*`. Now the low-level functions will send their output to the file.

This works fine until you forget to set `*standard-output*` back to the original stream when you're done. If you forget to reset `*standard-output*`, all the other code in the program that uses `*standard-output*` will also send its output to the file. 9

What you really want, it seems, is a way to wrap a piece of code in something that says, "All code below here -- all the functions it calls, all the functions they call, and so on, down to the lowest-level functions -- should use this value for the global variable `*standard-output*`." Then when the high-level function returns, the old value of `*standard-output*` should be automatically restored.

It turns out that that's exactly what Common Lisp's other kind of variable -- dynamic variables -- let you do. When you bind a dynamic variable -- for example, with a LET variable or a function parameter -- the binding that's created on entry to the binding form replaces the global binding for the duration of the binding form. Unlike a lexical binding, which can be referenced by code only within the lexical scope of the binding form, a dynamic binding can be referenced by any code that's invoked during the execution of the binding form.10 And it turns out that all global variables are, in fact, dynamic variables.

1『上面信息目前的理解，在 Common Lisp 里 dynamic variables 是结合了局部变量和全局变量的优点，而且还能避免全局变量时常忘记重置的缺点。（2020-11-08）』

Thus, if you want to temporarily redefine `*standard-output*`, the way to do it is simply to rebind it, say, with a LET.

```c
(let ((*standard-output* *some-other-stream*)) (stuff))
```

In any code that runs as a result of the call to stuff, references to `*standard-output*` will use the binding established by the LET. And when stuff returns and control leaves the LET, the new binding of `*standard-output*` will go away and subsequent references to `*standard-output*` will see the binding that was current before the LET. At any given time, the most recently established binding shadows all other bindings. Conceptually, each new binding for a given dynamic variable is pushed onto a stack of bindings for that variable, and references to the variable always use the most recent binding. As binding forms return, the bindings they created are popped off the stack, exposing previous bindings. 11

A simple example shows how this works.

```c
(defvar *x* 10) 
(defun foo () (format t "X: ~d~%" *x*))
```

The DEFVAR creates a global binding for the variable `*x*` with the value 10. The reference to `*x*` in foo will look up the current binding dynamically. If you call foo from the top level, the global binding created by the DEFVAR is the only binding available, so it prints 10.

```c
CL-USER> (foo) 
X: 10 
NIL
```

But you can use LET to create a new binding that temporarily shadows the global binding, and foo will print a different value.

```c
CL-USER> (let ((*x* 20)) (foo)) 
X: 20 
NIL
```

Now call foo again, with no LET, and it again sees the global binding.

```c
CL-USER> (foo) 
X: 10 
NIL
```

Now define another function.

```c
(defun bar () (foo) (let ((*x* 20)) (foo)) (foo))
```

Note that the middle call to foo is wrapped in a LET that binds `*x*` to the new value 20. When you run bar, you get this result:

```c
CL-USER> (bar) 
X: 10 
X: 20 
X: 10 
NIL
```

As you can see, the first call to foo sees the global binding, with its value of 10. The middle call, however, sees the new binding, with the value 20. But after the LET, foo once again sees the global binding.

As with lexical bindings, assigning a new value affects only the current binding. To see this, you can redefine foo to include an assignment to `*x*`.

```c
(defun foo () 
  (format t "Before assignment~18tX: ~d~%" *x*) 
  (setf *x* (+ 1 *x*)) 
  (format t "After assignment~18tX: ~d~%" *x*)
)
```

Now foo prints the value of `*x*`, increments it, and prints it again. If you just run foo, you'll see this:

```c
CL-USER> (foo) 
Before assignment X: 10 
After assignment X: 11 
NIL
```

Not too surprising. Now run bar.

```c
CL-USER> (bar) 
Before assignment X: 11 
After assignment X: 12 
Before assignment X: 20 
After assignment X: 21 
Before assignment X: 12 
After assignment X: 13 
NIL
```

Notice that `*x*` started at 11 -- the earlier call to foo really did change the global value. The first call to foo from bar increments the global binding to 12. The middle call doesn't see the global binding because of the LET. Then the last call can see the global binding again and increments it from 12 to 13.

So how does this work? How does LET know that when it binds `*x*` it's supposed to create a dynamic binding rather than a normal lexical binding? It knows because the name has been declared special. 12 The name of every variable defined with DEFVAR and DEFPARAMETER is automatically declared globally special. This means whenever you use such a name in a binding form -- in a LET or as a function parameter or any other construct that creates a new variable binding -- the binding that's created will be a dynamic binding. This is why the `*naming*` `*convention*` is so important -- it'd be bad news if you used a name for what you thought was a lexical variable and that variable happened to be globally special. On the one hand, code you call could change the value of the binding out from under you; on the other, you might be shadowing a binding established by code higher up on the stack. If you always name global variables according to the `*` naming convention, you'll never accidentally use a dynamic binding where you intend to establish a lexical binding.

2『目前还是没弄明白，`*` 命名全局变量，与普通命名全局变量的本质区别。（2020-11-08）』

It's also possible to declare a name locally special. If, in a binding form, you declare a name special, then the binding created for that variable will be dynamic rather than lexical. Other code can locally declare a name special in order to refer to the dynamic binding. However, locally special variables are relatively rare, so you needn't worry about them.13

Dynamic bindings make global variables much more manageable, but it's important to notice they still allow action at a distance. Binding a global variable has two at a distance effects -- it can change the behavior of downstream code, and it also opens the possibility that downstream code will assign a new value to a binding established higher up on the stack. You should use dynamic variables only when you need to take advantage of one or both of these characteristics.

7 Java disguises global variables as public static fields, C uses extern variables, and Python’s module-level and Perl’s package-level variables can likewise be accessed from anywhere.

8 If you specifically want to reset a DEFVARed variable, you can either set it directly with SETF or make it unbound using MAKUNBOUND and then reevaluate the DEFVAR form.

9 The strategy of temporarily reassigning `*standard-output*` also breaks if the system is multithreaded — if there are multiple threads of control trying to print to different streams at the same time, they’ll all try to set the global variable to the stream they want to use, stomping all over each other. You could use a lock to control access to the global variable, but then you’re not really getting the benefit of multiple concurrent threads, since whatever thread is printing has to lock out all the other threads until it’s done even if they want to print to a different stream.

10 The technical term for the interval during which references may be made to a binding is its extent. Thus, scope and extent are complementary notions — scope refers to space while extent refers to time. Lexical variables have lexical scope but indefinite extent, meaning they stick around for an indefinite interval, determined by how long they’re needed. Dynamic variables, by contrast, have indefinite scope since they can be referred to from anywhere but dynamic extent. To further confuse matters, the combination of indefinite scope and dynamic extent is frequently referred to by the misnomer dynamic scope.

11 Though the standard doesn’t specify how to incorporate multithreading into Common Lisp, implementations that provide multithreading follow the practice established on the Lisp machines and create dynamic bindings on a per-thread basis. A reference to a global variable will find the binding most recently established in the current thread, or the global binding.

12 This is why dynamic variables are also sometimes called special variables.

13 If you must know, you can look up DECLARE, SPECIAL, and LOCALLY in the HyperSpec.

### 6.4 Constants

One other kind of variable I haven't mentioned at all is the oxymoronic "constant variable." All constants are global and are defined with DEFCONSTANT. The basic form of DEFCONSTANT is like DEFPARAMETER.

```c
(defconstant name initial-value-form [ documentation-string ])
```

As with DEFVAR and DEFPARAMETER, DEFCONSTANT has a global effect on the name used -- thereafter the name can be used only to refer to the constant; it can't be used as a function parameter or rebound with any other binding form. Thus, many Lisp programmers follow a naming convention of using names starting and ending with + for constants. This convention is somewhat less universally followed than the *-naming convention for globally special names but is a good idea for the same reason. 14

Another thing to note about DEFCONSTANT is that while the language allows you to redefine a constant by reevaluating a DEFCONSTANT with a different initial-value-form, what exactly happens after the redefinition isn't defined. In practice, most implementations will require you to reevaluate any code that refers to the constant in order to see the new value since the old value may well have been inlined. Consequently, it's a good idea to use DEFCONSTANT only to define things that are really constant, such as the value of NIL. For things you might ever want to change, you should use DEFPARAMETER instead.

14 Several key constants defined by the language itself don’t follow this convention — not least of which are T and NIL. This is occasionally annoying when one wants to use t as a local variable name. Another is PI, which holds the best long-float approximation of the mathematical constant π.

### 6.5 Assignment

Once you've created a binding, you can do two things with it: get the current value and set it to a new value. As you saw in Chapter 4, a symbol evaluates to the value of the variable it names, so you can get the current value simply by referring to the variable. To assign a new value to a binding, you use the SETF macro, Common Lisp's general-purpose assignment operator. The basic form of SETF is as follows:

```c
(setf place value)
```

Because SETF is a macro, it can examine the form of the place it's assigning to and expand into appropriate lower-level operations to manipulate that place. When the place is a variable, it expands into a call to the special operator SETQ, which, as a special operator, has access to both lexical and dynamic bindings.15 For instance, to assign the value 10 to the variable x, you can write this:

```c
(setf x 10)
```

As I discussed earlier, assigning a new value to a binding has no effect on any other bindings of that variable. And it doesn't have any effect on the value that was stored in the binding prior to the assignment. Thus, the SETF in this function:

```c
(defun foo (x) 
  (setf x 10)
)
```

will have no effect on any value outside of foo. The binding that was created when foo was called is set to 10, immediately replacing whatever value was passed as an argument. In particular, a form such as the following:

```c
(let ((y 20)) 
  (foo y) 
  (print y)
)
```

will print 20, not 10, as it's the value of y that's passed to foo where it's briefly the value of the variable x before the SETF gives x a new value. SETF can also assign to multiple places in sequence. For instance, instead of the following:

```c
(setf x 1) 
(setf y 2)
```

you can write this:

```c
(setf x 1 y 2)
```

SETF returns the newly assigned value, so you can also nest calls to SETF as in the following expression, which assigns both x and y the same random value:

```c
(setf x (setf y (random 10)))
```

15 Some old-school Lispers prefer to use SETQ with variables, but modern style tends to use SETF for all assignments.

1『怪不得 autolisp 里用 `setq` 给变量赋值，果然是老古董，哈哈。（2020-11-08）』

### 6.6 Generalized Assignment

Variable bindings, of course, aren't the only places that can hold values. Common Lisp supports composite data structures such as arrays, hash tables, and lists, as well as user-defined data structures, all of which consist of multiple places that can each hold a value.

I'll cover those data structures in future chapters, but while we're on the topic of assignment, you should note that SETF can assign any place a value. As I cover the different composite data structures, I'll point out which functions can serve as "SETFable places." The short version, however, is if you need to assign a value to a place, SETF is almost certainly the tool to use. It's even possible to extend SETF to allow it to assign to user-defined places though I won't cover that. 16

In this regard SETF is no different from the = assignment operator in most C-derived languages. In those languages, the = operator assigns new values to variables, array elements, and fields of classes. In languages such as Perl and Python that support hash tables as a built-in data type, = can also set the values of individual hash table entries. Table 6-1 summarizes the various ways = is used in those languages.

Table 6-1. Assignment with = in Other Languages

|  Assigning to ... |  Java, C, C++  |  Perl  | Python  |
| --- | --- | --- | --- |
|  ... variable |  x = 10; |  `$x = 10;` |  x = 10 |
|  ... array element |  a[0] = 10;   |  `$a[0] = 10;` |  a[0] = 10 |
|  ... hash table entry |  |  `$hash{'key'} = 10;` |  hash['key'] = 10 |
|  ... field in object |   o.field = 10; | ` $o->{'field'} = 10;` |  o.field = 10 |

1『发现 Perl 的语法跟 PHP 一样的，突然间想起来，PHP 语言本身就是用 Perl 写的。（2020-11-08）』

SETF works the same way -- the first "argument" to SETF is a place to store the value, and the second argument provides the value. As with the = operator in these languages, you use the same form to express the place as you'd normally use to fetch the value. 17 Thus, the Lisp equivalents of the assignments in Table 6-1 -- given that AREF is the array access function, GETHASH does a hash table lookup, and field might be a function that accesses a slot named field of a user-defined object -- are as follows:

```c
Simple variable: 
(setf x 10) 

Array: 
(setf (aref a 0) 10) 

Hash table: 
(setf (gethash 'key hash) 10) 

Slot named 'field': 
(setf (field o) 10)
```

Note that SETFing a place that's part of a larger object has the same semantics as SETFing a variable: the place is modified without any effect on the object that was previously stored in the place. Again, this is similar to how = behaves in Java, Perl, and Python. 18

16 Look up DEFSETF, DEFINE-SETF-EXPANDER for more information.

17 The prevalence of Algol-derived syntax for assignment with the “place” on the left side of the = and the new value on the right side has spawned the terminology lvalue, short for “left value,” meaning something that can be assigned to, and rvalue, meaning something that provides a value. A compiler hacker would say, “SETF treats its first argument as an lvalue.”

18 C programmers may want to think of variables and other places as holding a pointer to the real object; assigning to a variable simply changes what object it points to while assigning to a part of a composite object is similar to indirecting through the pointer to the actual object. C++ programmers should note that the behavior of = in C++ when dealing with objects — namely, a memberwise copy — is quite idiosyncratic.

### 6.7 Other Ways to Modify Places

While all assignments can be expressed with SETF, certain patterns involving assigning a new value based on the current value are sufficiently common to warrant their own operators. For instance, while you could increment a number with SETF, like this:

```c
(setf x (+ x 1))
```

or decrement it with this:

```c
(setf x (- x 1))
```

it's a bit tedious, compared to the C-style ++x and  -- x. Instead, you can use the macros INCF and DECF, which increment and decrement a place by a certain amount that defaults to 1.

```c
(incf x) === (setf x (+ x 1)) 
(decf x) === (setf x (- x 1)) 
(incf x 10) === (setf x (+ x 10))
```

INCF and DECF are examples of a kind of macro called modify macros. Modify macros are macros built on top of SETF that modify places by assigning a new value based on the current value of the place. The main benefit of modify macros is that they're more concise than the same modification written out using SETF. Additionally, modify macros are defined in a way that makes them safe to use with places where the place expression must be evaluated only once. A silly example is this expression, which increments the value of an arbitrary element of an array:

```c
(incf (aref *array* (random (length *array*))))
```

A naive translation of that into a SETF expression might look like this:

```c
(setf (aref *array* (random (length *array*))) 
  (1+ (aref *array* (random (length *array*))))
)
```

However, that doesn't work because the two calls to RANDOM won't necessarily return the same value -- this expression will likely grab the value of one element of the array, increment it, and then store it back as the new value of a different element. The INCF expression, however, does the right thing because it knows how to take apart this expression:

```c
(aref *array* (random (length *array*)))
```

to pull out the parts that could possibly have side effects to make sure they're evaluated only once. In this case, it would probably expand into something more or less equivalent to this:

```c
(let ((tmp (random (length *array*)))) 
  (setf (aref *array* tmp) (1+ (aref *array* tmp)))
)
```

In general, modify macros are guaranteed to evaluate both their arguments and the subforms of the place form exactly once each, in left-to-right order.

The macro PUSH, which you used in the mini-database to add elements to the `*db*` variable, is another modify macro. You'll take a closer look at how it and its counterparts POP and PUSHNEW work in Chapter 12 when I talk about how lists are represented in Lisp.

Finally, two slightly esoteric but useful modify macros are ROTATEF and SHIFTF. ROTATEF rotates values between places. For instance, if you have two variables, a and b, this call:

```c
(rotatef a b)
```

swaps the values of the two variables and returns NIL. Since a and b are variables and you don't have to worry about side effects, the previous ROTATEF expression is equivalent to this:

```c
(let ((tmp a)) 
  (setf a b b tmp) 
  nil
)
```

With other kinds of places, the equivalent expression using SETF would be quite a bit more complex.

SHIFTF is similar except instead of rotating values it shifts them to the left -- the last argument provides a value that's moved to the second-to-last argument while the rest of the values are moved one to the left. The original value of the first argument is simply returned. Thus, the following:

```c
(shiftf a b 10)
```

is equivalent -- again, since you don't have to worry about side effects -- to this:

```c
(let ((tmp a)) 
  (setf a b b 10) 
  tmp
)
```

Both ROTATEF and SHIFTF can be used with any number of arguments and, like all modify macros, are guaranteed to evaluate them exactly once, in left to right order. With the basics of Common Lisp's functions and variables under your belt, now you're ready to move onto the feature that continues to differentiate Lisp from other languages: macros.

## 0701. Macros: Standard Control Constructs

While many of the ideas that originated in Lisp, from the conditional expression to garbage collection, have been incorporated into other languages, the one language feature that continues to set Common Lisp apart is its macro system. Unfortunately, the word macro describes a lot of things in computing to which Common Lisp's macros bear only a vague and metaphorical similarity. This causes no end of misunderstanding when Lispers try to explain to non-Lispers what a great feature macros are. 1 To understand Lisp's macros, you really need to come at them fresh, without preconceptions based on other things that also happen to be called macros. So let's start our discussion of Lisp's macros by taking a step back and looking at various ways languages support extensibility.

All programmers should be used to the idea that the definition of a language can include a standard library of functionality that's implemented in terms of the "core" language -- functionality that could have been implemented by any programmer on top of the language if it hadn't been defined as part of the standard library. C's standard library, for instance, can be implemented almost entirely in portable C. Similarly, most of the ever-growing set of classes and interfaces that ship with Java's standard Java Development Kit (JDK) are written in "pure" Java.

One advantage of defining languages in terms of a core plus a standard library is it makes them easier to understand and implement. But the real benefit is in terms of expressiveness -- since much of what you think of as "the language" is really just a library -- the language is easy to extend. If C doesn't have a function to do some thing or another that you need, you can write that function, and now you have a slightly richer version of C. Similarly, in a language such as Java or Smalltalk where almost all the interesting parts of the "language" are defined in terms of classes, by defining new classes you extend the language, making it more suited for writing programs to do whatever it is you're trying to do.

While Common Lisp supports both these methods of extending the language, macros give Common Lisp yet another way. As I discussed briefly in Chapter 4, each macro defines its own syntax, determining how the s-expressions it's passed are turned into Lisp forms. With macros as part of the core language it's possible to build new syntax -- control constructs such as WHEN, DOLIST, and LOOP as well as definitional forms such as DEFUN and DEFPARAMETER -- as part of the "standard library" rather than having to hardwire them into the core. This has implications for how the language itself is implemented, but as a Lisp programmer you'll care more that it gives you another way to extend the language, making it a better language for expressing solutions to your particular programming problems.

Now, it may seem that the benefits of having another way to extend the language would be easy to recognize. But for some reason a lot of folks who haven't actually used Lisp macros -- folks who think nothing of spending their days creating new functional abstractions or defining hierarchies of classes to solve their programming problems -- get spooked by the idea of being able to define new syntactic abstractions. The most common cause of macrophobia seems to be bad experiences with other "macro" systems. Simple fear of the unknown no doubt plays a role, too. To avoid triggering any macrophobic reactions, I'll ease into the subject by discussing several of the standard control-construct macros defined by Common Lisp. These are some of the things that, if Lisp didn't have macros, would have to be built into the language core. When you use them, you don't have to care that they're implemented as macros, but they provide a good example of some of the things you can do with macros. 2 In the next chapter, I'll show you how you can define your own macros.

2『这里有关 lisp 宏的信息补充进宏的术语卡片里。』——已完成

1 To see what this misunderstanding looks like, find any longish Usenet thread cross-posted between comp.lang.lisp and any other comp.lang.* group with macro in the subject. A rough paraphrase goes like this: Lispnik: “Lisp is the best because of its macros!” Othernik: “You think Lisp is good because of macros?! But macros are horrible and evil; Lisp must be horrible and evil.”

2 Another important class of language constructs that are defined using macros are all the definitional constructs such as DEFUN, DEFPARAMETER, DEFVAR, and others. In Chapter 24 you’ll define your own definitional macros that will allow you to concisely write code for reading and writing binary data.

### 7.1 WHEN and UNLESS

As you've already seen, the most basic form of conditional execution -- if x, do y; otherwise do z -- is provided by the IF special operator, which has this basic form:

```c
(if condition then-form [else-form])
```

The condition is evaluated and, if its value is non-NIL, the then-form is evaluated and the resulting value returned. Otherwise, the else-form, if any, is evaluated and its value returned. If condition is NIL and there's no else-form, then the IF returns NIL.

```
(if (> 2 3) "Yup" "Nope") ==> "Nope" 
(if (> 2 3) "Yup") ==> NIL 
(if (> 3 2) "Yup" "Nope") ==> "Yup"
```

However, IF isn't actually such a great syntactic construct because the then-form and else-form are each restricted to being a single Lisp form. This means if you want to perform a sequence of actions in either clause, you need to wrap them in some other syntax. For instance, suppose in the middle of a spam-filtering program you wanted to both file a message as spam and update the spam database when a message is spam. You can't write this:

```c
(if (spam-p current-message) 
  (file-in-spam-folder current-message) 
  (update-spam-database current-message))
```

because the call to update-spam-database will be treated as the else clause, not as part of the then clause. Another special operator, PROGN, executes any number of forms in order and returns the value of the last form. So you could get the desired behavior by writing the following:

```c
(if (spam-p current-message) 
  (progn 
    (file-in-spam-folder current-message) 
    (update-spam-database current-message)))
```

That's not too horrible. But given the number of times you'll likely have to use this idiom, it's not hard to imagine that you'd get tired of it after a while. "Why," you might ask yourself, "doesn't Lisp provide a way to say what I really want, namely, 'When x is true, do this, that, and the other thing'?" In other words, after a while you'd notice the pattern of an IF plus a PROGN and wish for a way to abstract away the details rather than writing them out every time.

This is exactly what macros provide. In this case, Common Lisp comes with a standard macro, WHEN, which lets you write this:

```c
(when (spam-p current-message) 
  (file-in-spam-folder current-message) 
  (update-spam-database current-message))
```

But if it wasn't built into the standard library, you could define WHEN yourself with a macro such as this, using the backquote notation I discussed in Chapter 3: 3

```c
(defmacro when (condition &rest body) 
  `(if ,condition (progn ,@body)))
```

A counterpart to the WHEN macro is UNLESS, which reverses the condition, evaluating its body forms only if the condition is false. In other words:

```c
(defmacro unless (condition &rest body) 
  `(if (not ,condition) (progn ,@body)))
```

Admittedly, these are pretty trivial macros. There's no deep black magic here; they just abstract away a few language-level bookkeeping details, allowing you to express your true intent a bit more clearly. But their very triviality makes an important point: because the macro system is built right into the language, you can write trivial macros like WHEN and UNLESS that give you small but real gains in clarity that are then multiplied by the thousands of times you use them. In Chapters 24, 26, and 31 you'll see how macros can also be used on a larger scale, creating whole domain-specific embedded languages. But first let's finish our discussion of the standard control-construct macros.

1『直觉告诉我这是 lisp 的一个关键知识点。难道 lisp 语言内部可以自有的定制「宏」？回复：可惜了，经测试，autolisp 里是没有内置宏 `when`，连 `defmacro` 都没有，哎。不过总觉得还可以通过其他途径来实现同样的目的，待挖掘。（2020-11-08）』

3 You can’t actually feed this definition to Lisp because it’s illegal to redefine names in the COMMON-LISP package where WHEN comes from. If you really want to try writing such a macro, you’d need to change the name to something else, such as my-when.

### 7.2 COND

Another time raw IF expressions can get ugly is when you have a multibranch conditional: if a do x, else if b do y; else do z. There's no logical problem writing such a chain of conditional expressions with just IF, but it's not pretty.

```c
(if a 
  (do-x) 
  (if b 
    (do-y) 
      (do-z)))
```
And it would be even worse if you needed to include multiple forms in the then clauses, requiring PROGNs. So, not surprisingly, Common Lisp provides a macro for expressing multibranch conditionals: COND. This is the basic skeleton:

```c
(cond 
  (test-1 form*) 
  .
  .
  . 
  (test-N form*))
```

Each element of the body represents one branch of the conditional and consists of a list containing a condition form and zero or more forms to be evaluated if that branch is chosen. The conditions are evaluated in the order the branches appear in the body until one of them evaluates to true. 

At that point, the remaining forms in that branch are evaluated, and the value of the last form in the branch is returned as the value of the COND as a whole. If the branch contains no forms after the condition, the value of the condition is returned instead. 

By convention, the branch representing the final else clause in an if/else-if chain is written with a condition of T. Any non-NIL value will work, but a T serves as a useful landmark when reading the code. Thus, you can write the previous nested IF expression using COND like this:

```c
(cond (a (do-x)) 
          (b (do-y)) 
          (t (do-z)))
```

2『在 autolisp 里 `cond` 语句是有效的，真不错。（2020-11-08）』

### 7.3 AND, OR, and NOT

When writing the conditions in IF, WHEN, UNLESS, and COND forms, three operators that will come in handy are the boolean logic operators, AND, OR, and NOT.

NOT is a function so strictly speaking doesn't belong in this chapter, but it's closely tied to AND and OR. It takes a single argument and inverts its truth value, returning T if the argument is NIL and NIL otherwise.

AND and OR, however, are macros. They implement logical conjunction and disjunction of any number of subforms and are defined as macros so they can short-circuit. That is, they evaluate only as many of their subforms -- in left-to-right order -- as necessary to determine the overall truth value. Thus, AND stops and returns NIL as soon as one of its subforms evaluates to NIL. If all the subforms evaluate to non-NIL, it returns the value of the last subform. OR, on the other hand, stops as soon as one of its subforms evaluates to non-NIL and returns the resulting value. If none of the subforms evaluate to true, OR returns NIL. Here are some examples:

```c
(not nil) ==> T 
(not (= 1 1)) ==> NIL 
(and (= 1 2) (= 3 3)) ==> NIL 
(or (= 1 2) (= 3 3)) ==> T
```

### 7.4 Looping

Control constructs are the other main kind of looping constructs. Common Lisp's looping facilities are -- in addition to being quite powerful and flexible -- an interesting lesson in the have-your-cake-and-eat-it-too style of programming that macros provide.

As it turns out, none of Lisp's 25 special operators directly support structured looping. All of Lisp's looping control constructs are macros built on top of a pair of special operators that provide a primitive goto facility. 4 Like many good abstractions, syntactic or otherwise, Lisp's looping macros are built as a set of layered abstractions starting from the base provided by those two special operators.

At the bottom (leaving aside the special operators) is a very general looping construct, DO. While very powerful, DO suffers, as do many general-purpose abstractions, from being overkill for simple situations. So Lisp also provides two other macros, DOLIST and DOTIMES, that are less flexible than DO but provide convenient support for the common cases of looping over the elements of a list and counting loops. While an implementation can implement these macros however it wants, they're typically implemented as macros that expand into an equivalent DO loop. Thus, DO provides a basic structured looping construct on top of the underlying primitives provided by Common Lisp's special operators, and DOLIST and DOTIMES provide two easier-to-use, if less general, constructs. And, as you'll see in the next chapter, you can build your own looping constructs on top of DO for situations where DOLIST and DOTIMES don't meet your needs.

Finally, the LOOP macro provides a full-blown mini-language for expressing looping constructs in a non-Lispy, English-like (or at least Algol-like) language. Some Lisp hackers love LOOP; others hate it. LOOP's fans like it because it provides a concise way to express certain commonly needed looping constructs. Its detractors dislike it because it's not Lispy enough. But whichever side one comes down on, it's a remarkable example of the power of macros to add new constructs to the language.

4 The special operators, if you must know, are TAGBODY and GO. There’s no need to discuss them now, but I’ll cover them in Chapter 20.

### 7.5 DOLIST and DOTIMES

I'll start with the easy-to-use DOLIST and DOTIMES macros.

DOLIST loops across the items of a list, executing the loop body with a variable holding the successive items of the list. 5 This is the basic skeleton (leaving out some of the more esoteric options):

```c
(dolist (var list-form) body-form*)
```

When the loop starts, the list-form is evaluated once to produce a list. Then the body of the loop is evaluated once for each item in the list with the variable var holding the value of the item. For instance:

```c
CL-USER> 
(dolist (x '(1 2 3)) 
  (print x)
)
1 2 3 
NIL
```

Used this way, the DOLIST form as a whole evaluates to NIL. If you want to break out of a DOLIST loop before the end of the list, you can use RETURN.

```c
CL-USER> 
(dolist (x '(1 2 3)) 
  (print x) 
  (if (evenp x) (return))
)
1 2 
NIL
```

DOTIMES is the high-level looping construct for counting loops. The basic template is much the same as DOLIST's.

```c
(dotimes (var count-form) body-form*)
```

The count-form must evaluate to an integer. Each time through the loop var holds successive integers from 0 to one less than that number. For instance:

```c
CL-USER> 
(dotimes (i 4) (print i)) 
0 1 2 3 
NIL
```

As with DOLIST, you can use RETURN to break out of the loop early.

Because the body of both DOLIST and DOTIMES loops can contain any kind of expressions, you can also nest loops. For example, to print out the times tables from `1 × 1 = 1` to `20 × 20 = 400,` you can write this pair of nested DOTIMES loops:

```c
(dotimes (x 20) 
  (dotimes (y 20) 
    (format t "~3d " (* (1+ x) (1+ y)))
  ) 
  (format t "~%")
)
```

1『试了下，上面的代码跑出来是一个矩阵。（2020-11-08）』

5 DOLIST is similar to Perl’s foreach or Python’s for. Java added a similar kind of loop construct with the “enhanced” for loop in Java 1.5, as part of JSR-201. Notice what a difference macros make. A Lisp programmer who notices a common pattern in their code can write a macro to give themselves a source-level abstraction of that pattern. A Java programmer who notices the same pattern has to convince Sun that this particular abstraction is worth adding to the language. Then Sun has to publish a JSR and convene an industry-wide “expert group” to hash everything out. That process — according to Sun — takes an average of 18 months. After that, the compiler writers all have to go upgrade their compilers to support the new feature. And even once the Java programmer’s favorite compiler supports the new version of Java, they probably still can’t use the new feature until they’re allowed to break source compatibility with older versions of Java. So an annoyance that Common Lisp programmers can resolve for themselves within five minutes plagues Java programmers for years.

1『

这时才发现，dolist 与 autolisp 里的函数 `mapcar` 以及 `foreach` 语句功能相当。（2021-01-07）

在 autolisp 里也是使用的 `foreach` 语句。

```c
(defun StrListToListListUtils (strList / resultList)
  (foreach item strList 
    (setq resultList (append resultList (list (StrToListUtils item ","))))
  )
  resultList
)
```

』

### 7.6 DO

While DOLIST and DOTIMES are convenient and easy to use, they aren't flexible enough to use for all loops. For instance, what if you want to step multiple variables in parallel? Or use an arbitrary expression to test for the end of the loop? If neither DOLIST nor DOTIMES meet your needs, you still have access to the more general DO loop.

Where DOLIST and DOTIMES provide only one loop variable, DO lets you bind any number of variables and gives you complete control over how they change on each step through the loop. You also get to define the test that determines when to end the loop and can provide a form to evaluate at the end of the loop to generate a return value for the DO expression as a whole. The basic template looks like this:

```c
(do (variable-definition*) (end-test-form result-form*) statement*)
```

Each variable-definition introduces a variable that will be in scope in the body of the loop. The full form of a single variable definition is a list containing three elements.

```c
(var init-form step-form)
```

The init-form will be evaluated at the beginning of the loop and the resulting values bound to the variable var. Before each subsequent iteration of the loop, the step-form will be evaluated and the new value assigned to var. The step-form is optional; if it's left out, the variable will keep its value from iteration to iteration unless you explicitly assign it a new value in the loop body. As with the variable definitions in a LET, if the init-form is left out, the variable is bound to NIL. Also as with LET, you can use a plain variable name as shorthand for a list containing just the name.

At the beginning of each iteration, after all the loop variables have been given their new values, the end-test-form is evaluated. As long as it evaluates to NIL, the iteration proceeds, evaluating the statements in order.

When the end-test-form evaluates to true, the result-forms are evaluated, and the value of the last result form is returned as the value of the DO expression. At each step of the iteration the step forms for all the variables are evaluated before assigning any of the values to the variables. This means you can refer to any of the other loop variables in the step forms. 6 That is, in a loop like this:

```c
(do ((n 0 (1+ n)) 
     (cur 0 next) 
     (next 1 (+ cur next))
    ) 
  ((= 10 n) cur)
)
```

the step forms (1+ n), next, and (+ cur next) are all evaluated using the old values of n, cur, and next. Only after all the step forms have been evaluated are the variables given their new values. (Mathematically inclined readers may notice that this is a particularly efficient way of computing the eleventh Fibonacci number.)

This example also illustrates another characteristic of DO -- because you can step multiple variables, you often don't need a body at all. Other times, you may leave out the result form, particularly if you're just using the loop as a control construct. This flexibility, however, is the reason that DO expressions can be a bit cryptic. Where exactly do all the parentheses go? The best way to understand a DO expression is to keep in mind the basic template.

```c
(do (variable-definition*) (end-test-form result-form*) statement*)
```

The six parentheses in that template are the only ones required by the DO itself. You need one pair to enclose the variable declarations, one pair to enclose the end test and result forms, and one pair to enclose the whole expression. Other forms within the DO may require their own parentheses -- variable definitions are usually lists, for instance. And the test form is often a function call. But the skeleton of a DO loop will always be the same. Here are some example DO loops with the skeleton in bold:

```c
(do ((i 0 (1+ i))) ((>= i 4)) (print i))
```

Notice that the result form has been omitted. This is, however, not a particularly idiomatic use of DO, as this loop is much more simply written using DOTIMES. 7

```c
(dotimes (i 4) (print i))
```

As another example, here's the bodiless Fibonacci-computing loop:

```c
(do ((n 0 (1+ n)) (cur 0 next) (next 1 (+ cur next))) ((= 10 n) cur))
```

Finally, the next loop demonstrates a DO loop that binds no variables. It loops while the current time is less than the value of a global variable, printing "Waiting" once a minute. Note that even with no loop variables, you still need the empty variables list.

```c
(do () 
  ((> (get-universal-time) *some-future-date*)) 
  (format t "Waiting~%") 
  (sleep 60)
)
```

6 A variant of DO, DO*, assigns each variable its value before evaluating the step form for subsequent variables. For more details, consult your favorite Common Lisp reference.

7 The DOTIMES is also preferred because the macro expansion will likely include declarations that allow the compiler to generate more efficient code.

### 7.7 The Mighty LOOP

For the simple cases you have DOLIST and DOTIMES. And if they don't suit your needs, you can fall back on the completely general DO. What more could you want?

Well, it turns out a handful of looping idioms come up over and over again, such as looping over various data structures: lists, vectors, hash tables, and packages. Or accumulating values in various ways while looping: collecting, counting, summing, minimizing, or maximizing. If you need a loop to do one of these things (or several at the same time), the LOOP macro may give you an easier way to express it.

The LOOP macro actually comes in two flavors -- simple and extended. The simple version is as simple as can be -- an infinite loop that doesn't bind any variables. The skeleton looks like this:

```c
(loop body-form*)
```

The forms in body are evaluated each time through the loop, which will iterate forever unless you use RETURN to break out. For example, you could write the previous DO loop with a simple LOOP.

```c
(loop 
  (when (> (get-universal-time) *some-future-date*) 
    (return)
  ) 
  (format t "Waiting~%") 
  (sleep 60)
)
```

The extended LOOP is quite a different beast. It's distinguished by the use of certain loop keywords that implement a special-purpose language for expressing looping idioms. It's worth noting that not all Lispers love the extended LOOP language. At least one of Common Lisp's original designers hated it. LOOP's detractors complain that its syntax is totally un-Lispy (in other words, not enough parentheses). LOOP's fans counter that that's the point: complicated looping constructs are hard enough to understand without wrapping them up in DO's cryptic syntax. It's better, they say, to have a slightly more verbose syntax that gives you some clues what the heck is going on.

For instance, here's an idiomatic DO loop that collects the numbers from 1 to 10 into a list:

```c
(do ((nums nil) (i 1 (1+ i))) ((> i 10) (nreverse nums)) (push i nums)) 
==> (1 2 3 4 5 6 7 8 9 10)
```

A seasoned Lisper won't have any trouble understanding that code -- it's just a matter of understanding the basic form of a DO loop and recognizing the PUSH/NREVERSE idiom for building up a list. But it's not exactly transparent. The LOOP version, on the other hand, is almost understandable as an English sentence.

```c
(loop for i from 1 to 10 collecting i) 
==> (1 2 3 4 5 6 7 8 9 10)
```

The following are some more examples of simple uses of LOOP. This sums the first ten squares:

```c
(loop for x from 1 to 10 summing (expt x 2)) 
==> 385
```

This counts the number of vowels in a string:

```c
(loop for x across "the quick brown fox jumps over the lazy dog" counting (find x "aeiou")) 
==> 11
```

This computes the eleventh Fibonacci number, similar to the DO loop used earlier:

```c
(loop for i below 10 and a = 0 then b and b = 1 then (+ b a) finally (return a))
```

The symbols across, and, below, collecting, counting, finally, for, from, summing, then, and to are some of the loop keywords whose presence identifies these as instances of the extended LOOP. 8

I'll save the details of LOOP for Chapter 22, but it's worth noting here as another example of the way macros can be used to extend the base language. While LOOP provides its own language for expressing looping constructs, it doesn't cut you off from the rest of Lisp. The loop keywords are parsed according to loop's grammar, but the rest of the code in a LOOP is regular Lisp code.

And it's worth pointing out one more time that while the LOOP macro is quite a bit more complicated than macros such as WHEN or UNLESS, it is just another macro. If it hadn't been included in the standard library, you could implement it yourself or get a third-party library that does.

With that I'll conclude our tour of the basic control-construct macros. Now you're ready to take a closer look at how to define your own macros.

8 Loop keywords is a bit of a misnomer since they aren’t keyword symbols. In fact, LOOP doesn’t care what package the symbols are from. When the LOOP macro parses its body, it considers any appropriately named symbols equivalent. You could even use true keywords if you wanted:for, :across, and so on — because they also have the correct name. But most folks just use plain symbols. Because the loop keywords are used only as syntactic markers, it doesn’t matter if they’re used for other purposes — as function or variable names.
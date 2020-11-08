# 2019117Practical-Common-LispR02

## 记忆时间

## 0701. Macros: Standard Control Constructs

While many of the ideas that originated in Lisp, from the conditional expression to garbage collection, have been incorporated into other languages, the one language feature that continues to set Common Lisp apart is its macro system. Unfortunately, the word macro describes a lot of things in computing to which Common Lisp's macros bear only a vague and metaphorical similarity. This causes no end of misunderstanding when Lispers try to explain to non-Lispers what a great feature macros are. 1 To understand Lisp's macros, you really need to come at them fresh, without preconceptions based on other things that also happen to be called macros. So let's start our discussion of Lisp's macros by taking a step back and looking at various ways languages support extensibility.

All programmers should be used to the idea that the definition of a language can include a standard library of functionality that's implemented in terms of the "core" language--functionality that could have been implemented by any programmer on top of the language if it hadn't been defined as part of the standard library. C's standard library, for instance, can be implemented almost entirely in portable C. Similarly, most of the ever-growing set of classes and interfaces that ship with Java's standard Java Development Kit (JDK) are written in "pure" Java.

One advantage of defining languages in terms of a core plus a standard library is it makes them easier to understand and implement. But the real benefit is in terms of expressiveness--since much of what you think of as "the language" is really just a library--the language is easy to extend. If C doesn't have a function to do some thing or another that you need, you can write that function, and now you have a slightly richer version of C. Similarly, in a language such as Java or Smalltalk where almost all the interesting parts of the "language" are defined in terms of classes, by defining new classes you extend the language, making it more suited for writing programs to do whatever it is you're trying to do.

While Common Lisp supports both these methods of extending the language, macros give Common Lisp yet another way. As I discussed briefly in Chapter 4, each macro defines its own syntax, determining how the s-expressions it's passed are turned into Lisp forms. With macros as part of the core language it's possible to build new syntax--control constructs such as WHEN, DOLIST, and LOOP as well as definitional forms such as DEFUN and DEFPARAMETER--as part of the "standard library" rather than having to hardwire them into the core. This has implications for how the language itself is implemented, but as a Lisp programmer you'll care more that it gives you another way to extend the language, making it a better language for expressing solutions to your particular programming problems.

Now, it may seem that the benefits of having another way to extend the language would be easy to recognize. But for some reason a lot of folks who haven't actually used Lisp macros--folks who think nothing of spending their days creating new functional abstractions or defining hierarchies of classes to solve their programming problems--get spooked by the idea of being able to define new syntactic abstractions. The most common cause of macrophobia seems to be bad experiences with other "macro" systems. Simple fear of the unknown no doubt plays a role, too. To avoid triggering any macrophobic reactions, I'll ease into the subject by discussing several of the standard control-construct macros defined by Common Lisp. These are some of the things that, if Lisp didn't have macros, would have to be built into the language core. When you use them, you don't have to care that they're implemented as macros, but they provide a good example of some of the things you can do with macros. 2 In the next chapter, I'll show you how you can define your own macros.

1 To see what this misunderstanding looks like, find any longish Usenet thread cross-posted between comp.lang.lisp and any other comp.lang.* group with macro in the subject. A rough paraphrase goes like this: Lispnik: “Lisp is the best because of its macros!” Othernik: “You think Lisp is good because of macros?! But macros are horrible and evil; Lisp must be horrible and evil.”

2 Another important class of language constructs that are defined using macros are all the definitional constructs such as DEFUN, DEFPARAMETER, DEFVAR, and others. In Chapter 24 you’ll define your own definitional macros that will allow you to concisely write code for reading and writing binary data.

### 7.1 WHEN and UNLESS

As you've already seen, the most basic form of conditional execution--if x, do y; otherwise do z--is provided by the IF special operator, which has this basic form:

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

AND and OR, however, are macros. They implement logical conjunction and disjunction of any number of subforms and are defined as macros so they can short-circuit. That is, they evaluate only as many of their subforms--in left-to-right order--as necessary to determine the overall truth value. Thus, AND stops and returns NIL as soon as one of its subforms evaluates to NIL. If all the subforms evaluate to non-NIL, it returns the value of the last subform. OR, on the other hand, stops as soon as one of its subforms evaluates to non-NIL and returns the resulting value. If none of the subforms evaluate to true, OR returns NIL. Here are some examples:

```c
(not nil) ==> T 
(not (= 1 1)) ==> NIL 
(and (= 1 2) (= 3 3)) ==> NIL 
(or (= 1 2) (= 3 3)) ==> T
```

### 7.4 Looping

Control constructs are the other main kind of looping constructs. Common Lisp's looping facilities are--in addition to being quite powerful and flexible--an interesting lesson in the have-your-cake-and-eat-it-too style of programming that macros provide.

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

5 DOLIST is similar to Perl’s foreach or Python’s for. Java added a similar kind of loop construct with the “enhanced” for loop in Java 1.5, as part of JSR-201. Notice what a difference macros make. A Lisp programmer who notices a common pattern in their code can write a macro to give themselves a source-level abstraction of that pattern. A Java programmer who notices the same pattern has to convince Sun that this particular abstraction is worth adding to the language. Then Sun has to publish a JSR and convene an industry-wide “expert group” to hash everything out. That process—according to Sun—takes an average of 18 months. After that, the compiler writers all have to go upgrade their compilers to support the new feature. And even once the Java programmer’s favorite compiler supports the new version of Java, they probably still can’t use the new feature until they’re allowed to break source compatibility with older versions of Java. So an annoyance that Common Lisp programmers can resolve for themselves within five minutes plagues Java programmers for years.

1『

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

This example also illustrates another characteristic of DO--because you can step multiple variables, you often don't need a body at all. Other times, you may leave out the result form, particularly if you're just using the loop as a control construct. This flexibility, however, is the reason that DO expressions can be a bit cryptic. Where exactly do all the parentheses go? The best way to understand a DO expression is to keep in mind the basic template.

```c
(do (variable-definition*) (end-test-form result-form*) statement*)
```

The six parentheses in that template are the only ones required by the DO itself. You need one pair to enclose the variable declarations, one pair to enclose the end test and result forms, and one pair to enclose the whole expression. Other forms within the DO may require their own parentheses--variable definitions are usually lists, for instance. And the test form is often a function call. But the skeleton of a DO loop will always be the same. Here are some example DO loops with the skeleton in bold:

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

The LOOP macro actually comes in two flavors--simple and extended. The simple version is as simple as can be--an infinite loop that doesn't bind any variables. The skeleton looks like this:

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

A seasoned Lisper won't have any trouble understanding that code--it's just a matter of understanding the basic form of a DO loop and recognizing the PUSH/NREVERSE idiom for building up a list. But it's not exactly transparent. The LOOP version, on the other hand, is almost understandable as an English sentence.

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

8 Loop keywords is a bit of a misnomer since they aren’t keyword symbols. In fact, LOOP doesn’t care what package the symbols are from. When the LOOP macro parses its body, it considers any appropriately named symbols equivalent. You could even use true keywords if you wanted:for, :across, and so on—because they also have the correct name. But most folks just use plain symbols. Because the loop keywords are used only as syntactic markers, it doesn’t matter if they’re used for other purposes—as function or variable names.a

## 0901. Practical: Building a Unit Test Framework

In this chapter you'll return to cutting code and develop a simple unit testing framework for Lisp. This will give you a chance to use some of the features you've learned about since Chapter 3, including macros and dynamic variables, in real code.

The main design goal of the test framework will be to make it as easy as possible to add new tests, to run various suites of tests, and to track down test failures. For now you'll focus on designing a framework you can use during interactive development.

The key feature of an automated testing framework is that the framework is responsible for telling you whether all the tests passed. You don't want to spend your time slogging through test output checking answers when the computer can do it much more quickly and accurately. Consequently, each test case must be an expression that yields a boolean value--true or false, pass or fail. For instance, if you were writing tests for the built-in + function, these might be reasonable test cases: 1

```c
(= (+ 1 2) 3) 
(= (+ 1 2 3) 6) 
(= (+ -1 -3) -4)
```

Functions that have side effects will be tested slightly differently--you'll have to call the function and then check for evidence of the expected side effects. 2 But in the end, every test case has to boil down to a boolean expression, thumbs up or thumbs down.

1 This is for illustrative purposes only--obviously, writing test cases for built-in functions such as + is a bit silly, since if such basic things aren't working, the chances the tests will be running the way you expect is pretty slim. On the other hand, most Common Lisps are implemented largely in Common Lisp, so it's not crazy to imagine writing test suites in Common Lisp to test the standard library functions.

2 Side effects can include such things as signaling errors; I’ll discuss Common Lisp’s error handling system in Chapter 19. You may, after reading that chapter, want to think about how to incorporate tests that check whether a function does or does not signal a particular error in certain situations.

### 9.1 Two First Tries

If you were doing ad hoc testing, you could enter these expressions at the REPL and check that they return T. But you want a framework that makes it easy to organize and run these test cases whenever you want. If you want to start with the simplest thing that could possibly work, you can just write a function that evaluates the test cases and ANDs the results together.

```c
(defun test-+ ()
  (and 
    (= (+ 1 2) 3)
    (= (+ 1 2 3) 6)
    (= (+ -1 -3) -4)
  )
)
```

Whenever you want to run this set of test cases, you can call test-+.

```c
CL-USER> (test-+) 
T
```

As long as it returns T, you know the test cases are passing. This way of organizing tests is also pleasantly concise--you don't have to write a bunch of test bookkeeping code. However, as you'll discover the first time a test case fails, the result reporting leaves something to be desired. When test-+ returns NIL, you'll know something failed, but you'll have no idea which test case it was.

So let's try another simple--even simpleminded--approach. To find out what happens to each test case, you could write something like this:

```c
(defun test-+ () 
  (format t "~:[FAIL~;pass~] ... ~a~%" (= (+ 1 2) 3) '(= (+ 1 2) 3)) 
  (format t "~:[FAIL~;pass~] ... ~a~%" (= (+ 1 2 3) 6) '(= (+ 1 2 3) 6)) 
  (format t "~:[FAIL~;pass~] ... ~a~%" (= (+ -1 -3) -4) '(= (+ -1 -3) -4))
)
```

1-3『

`'(= (+ 1 2) 3))` 表示仅仅以字面量的形式展示 `(= (+ 1 2) 3))`，那么 `'` 在这的作用就很明确了，使后面的函数表达式丧失作用，仅显示字面量。

编译器自带的说明：（详见原文）

经过试验，以写成函数语句后，重新加载进 emacs 里，`format` 函数会报错，直接把语句 `(format t "~:[FAIL~;pass~] ... ~a~%" (= (+ 1 2) 3) '(= (+ 1 2) 3))` 拷到 emacs 里运行没问题，目前不知道为啥。（2020-10-24）回复：完全是自己的问题，封装完函数，在 emacs 里调用的时候漏掉了函数名外面的括号，之前一直是用 `test-+`，应该是 `(test-+)`，真是蠢。（2020-10-24）

』

Now each test case will be reported individually. The` ~:[FAIL~;pass~]` part of the FORMAT directive causes FORMAT to print "FAIL" if the first format argument is false and "pass" otherwise. 3 Then you label the result with the test expression itself. Now running test-+ shows you exactly what's going on.

```c
CL-USER> (test-+) 
pass ... (= (+ 1 2) 3) 
pass ... (= (+ 1 2 3) 6) 
pass ... (= (+ -1 -3) -4) NIL
```

This time the result reporting is more like what you want, but the code itself is pretty gross. The repeated calls to FORMAT as well as the tedious duplication of the test expression cry out to be refactored. The duplication of the test expression is particularly grating because if you mistype it, the test results will be mislabeled.

Another problem is that you don't get a single indicator whether all the test cases passed. It's easy enough, with only three test cases, to scan the output looking for "FAIL"; however, when you have hundreds of test cases, it'll be more of a hassle.

3 I’ll discuss this and other FORMAT directives in more detail in Chapter 18.

### 9.2 Refactoring

What you'd really like is a way to write test functions as streamlined as the first test-+ that return a single T or NIL value but that also report on the results of individual test cases like the second version. Since the second version is close to what you want in terms of functionality, your best bet is to see if you can factor out some of the annoying duplication.

The simplest way to get rid of the repeated similar calls to FORMAT is to create a new function.

```c
(defun report-result (result form) 
  (format t "~:[FAIL~;pass~] ... ~a~%" result form)
)
```

Now you can write test-+ with calls to report-result instead of FORMAT. It's not a huge improvement, but at least now if you decide to change the way you report results, there's only one place you have to change.

```c
(defun test-+ () 
  (report-result (= (+ 1 2) 3) '(= (+ 1 2) 3)) 
  (report-result (= (+ 1 2 3) 6) '(= (+ 1 2 3) 6)) 
  (report-result (= (+ -1 -3) -4) '(= (+ -1 -3) -4))
)
```

Next you need to get rid of the duplication of the test case expression, with its attendant risk of mislabeling of results. What you'd really like is to be able to treat the expression as both code (to get the result) and data (to use as the label). Whenever you want to treat code as data, that's a sure sign you need a macro. Or, to look at it another way, what you need is a way to automate writing the error-prone report-result calls. You'd like to be able to say something like this:

```c
(check (= (+ 1 2) 3))
```

and have it mean the following:

```c
(report-result (= (+ 1 2) 3) '(= (+ 1 2) 3))
```

Writing a macro to do this translation is trivial.

```c
(defmacro check (form) 
  `(report-result ,form ',form)
)
```

1『

改成了自己习惯的格式：

```c
(defmacro check (form) 
  `(report-result, form', form)
)
```
』


Now you can change test-+ to use check.

```c
(defun test-+ () 
  (check (= (+ 1 2) 3)) 
  (check (= (+ 1 2 3) 6)) 
  (check (= (+ -1 -3) -4))
)
```

Since you're on the hunt for duplication, why not get rid of those repeated calls to check? You can define check to take an arbitrary number of forms and wrap them each in a call to report-result.

```c
(defmacro check (&body forms) 
  `(progn 
     ,@(loop for f in forms collect `(report-result ,f ',f))
   )
)
```

This definition uses a common macro idiom of wrapping a PROGN around a series of forms in order to turn them into a single form. Notice also how you can use ,@ to splice in the result of an expression that returns a list of expressions that are themselves generated with a backquote template.

With the new version of check you can write a new version of test-+ like this:

```c
(defun test-+ () 
  (check 
    (= (+ 1 2) 3) 
    (= (+ 1 2 3) 6) 
    (= (+ -1 -3) -4)
  )
)
```

that is equivalent to the following code:

```c
(defun test-+ () 
  (progn 
    (report-result (= (+ 1 2) 3) '(= (+ 1 2) 3)) 
    (report-result (= (+ 1 2 3) 6) '(= (+ 1 2 3) 6)) 
    (report-result (= (+ -1 -3) -4) '(= (+ -1 -3) -4))
  )
)
```

Thanks to check, this version is as concise as the first version of test-+ but expands into code that does the same thing as the second version. And now any changes you want to make to how test-+ behaves, you can make by changing check.

### 9.3 Fixing the Return Value

You can start with fixing test-+ so its return value indicates whether all the test cases passed. Since check is responsible for generating the code that ultimately runs the test cases, you just need to change it to generate code that also keeps track of the results.

As a first step, you can make a small change to report-result so it returns the result of the test case it's reporting.

```c
(defun report-result (result form) 
  (format t "~:[FAIL~;pass~] ... ~a~%" result form)
  result
)
```

Now that report-result returns the result of its test case, it might seem you could just change the PROGN to an AND to combine the results. Unfortunately, AND doesn't do quite what you want in this case because of its short-circuiting behavior: as soon as one test case fails, AND will skip the rest. On the other hand, if you had a construct that worked like AND without the short-circuiting, you could use it in the place of PROGN, and you'd be done. Common Lisp doesn't provide such a construct, but that's no reason you can't use it: it's a trivial matter to write a macro to provide it yourself.

Leaving test cases aside for a moment, what you want is a macro--let's call it combine-results--that will let you say this:

```c
(combine-results 
  (foo) 
  (bar) 
  (baz)
)
```

and have it mean something like this:

```c
(let ((result t)) 
  (unless (foo) (setf result nil)) 
  (unless (bar) (setf result nil)) 
  (unless (baz) (setf result nil)) 
  result
)
```

The only tricky bit to writing this macro is that you need to introduce a variable--result in the previous code--in the expansion. As you saw in the previous chapter, using a literal name for variables in macro expansions can introduce a leak in your macro abstraction, so you'll need to create a unique name. This is a job for with-gensyms. You can define combine-results like this:

```c
(defmacro combine-results (&body forms) 
  (with-gensyms (result) 
    `(let ((,result t)) 
       ,@(loop for f in forms collect `(unless ,f (setf ,result nil))) 
       ,result
     )
  )
)
```

Now you can fix check by simply changing the expansion to use combine-results instead of PROGN.

```c
(defmacro check (&body forms) 
  `(combine-results 
     ,@(loop for f in forms collect `(report-result ,f ',f))
   )
)
```

With that version of check, test-+ should emit the results of its three test expressions and then return T to indicate that everything passed. 4

```c
CL-USER> (test-+) 
pass ... (= (+ 1 2) 3)
pass ... (= (+ 1 2 3) 6)  
pass ... (= (+ -1 -3) -4) 
T
```

1『目前用原书里的代码，没跑通。（2020-10-27）』

And if you change one of the test cases so it fails, 5 the final return value changes to NIL.

```c
CL-USER> (test-+) 
pass ... (= (+ 1 2) 3) 
pass ... (= (+ 1 2 3) 6) 
FAIL ... (= (+ -1 -3) -5) NIL
```

4 If test-+ has been compiled—which may happen implicitly in certain Lisp implementations—you may need to reevaluate the definition of test-+ to get the changed definition of check to affect the behavior of test-+. Interpreted code, on the other hand, typically expands macros anew each time the code is interpreted, allowing the effects of macro redefinitions to be seen immediately.

5 You have to change the test to make it fail since you can’t change the behavior of +.

### 9.4 Better Result Reporting

As long as you have only one test function, the current result reporting is pretty clear. If a particular test case fails, all you have to do is find the test case in the check form and figure out why it's failing. But if you write a lot of tests, you'll probably want to organize them somehow, rather than shoving them all into one function. For instance, suppose you wanted to add some test cases for the * function. You might write a new test function.

```c
(defun test-* () 
  (check 
    (= (* 2 2) 4) 
    (= (* 3 5) 15)
  )
)
```

Now that you have two test functions, you'll probably want another function that runs all the tests. That's easy enough.

```c
(defun test-arithmetic () 
  (combine-results 
    (test-+) 
    (test-*)
  )
)
```

In this function you use combine-results instead of check since both test-+ and test-* will take care of reporting their own results. When you run test-arithmetic, you'll get the following results:

```c
CL-USER> (test-arithmetic) 
pass ... (= (+ 1 2) 3) 
pass ... (= (+ 1 2 3) 6) 
pass ... (= (+ -1 -3) -4) 
pass ... (= (* 2 2) 4) 
pass ... (= (* 3 5) 15) T
```

Now imagine that one of the test cases failed and you need to track down the problem. With only five test cases and two test functions, it won't be too hard to find the code of the failing test case. But suppose you had 500 test cases spread across 20 functions. It might be nice if the results told you what function each test case came from.

Since the code that prints the results is centralized in report-result, you need a way to pass information about what test function you're in to report-result. You could add a parameter to report-result to pass this information, but check, which generates the calls to report-result, doesn't know what function it's being called from, which means you'd also have to change the way you call check, passing it an argument that it simply passes onto report-result.

This is exactly the kind of problem dynamic variables were designed to solve. If you create a dynamic variable that each test function binds to the name of the function before calling check, then report-result can use it without check having to know anything about it.

Step one is to declare the variable at the top level.

```c
(defvar *test-name* nil)
```

Now you need to make another tiny change to report-result to include `*test-name*` in the FORMAT output.

```c
(format t "~:[FAIL~;pass~] ... ~a: ~a~%" result *test-name* form)
```

With those changes, the test functions will still work but will produce the following output because `*test-name*` is never rebound:

```c
CL-USER> (test-arithmetic) 
pass ... NIL: (= (+ 1 2) 3) 
pass ... NIL: (= (+ 1 2 3) 6) 
pass ... NIL: (= (+ -1 -3) -4) 
pass ... NIL: (= (* 2 2) 4) 
pass ... NIL: (= (* 3 5) 15) 
T
```

For the name to be reported properly, you need to change the two test functions.

```c
(defun test-+ () 
  (let ((*test-name* 'test-+)) 
    (check 
      (= (+ 1 2) 3) 
      (= (+ 1 2 3) 6) 
      (= (+ -1 -3) -4)
    )
  )
) 

(defun test-* () 
  (let ((*test-name* 'test-*)) 
    (check 
      (= (* 2 2) 4) 
      (= (* 3 5) 15)
    )
  )
)
```

Now the results are properly labeled.

```c
CL-USER> (test-arithmetic) 
pass ... TEST-+: (= (+ 1 2) 3) 
pass ... TEST-+: (= (+ 1 2 3) 6) 
pass ... TEST-+: (= (+ -1 -3) -4)
pass ... TEST-*: (= (* 2 2) 4) 
pass ... TEST-*: (= (* 3 5) 15) 
T
```

### 9.5 An Abstraction Emerges

In fixing the test functions, you've introduced several new bits of duplication. Not only does each function have to include the name of the function twice--once as the name in the DEFUN and once in the binding of `*test-name*`--but the same three-line code pattern is duplicated between the two functions. You could remove the duplication simply on the grounds that duplication is bad. But if you look more closely at the root cause of the duplication, you can learn an important lesson about how to use macros.

The reason both these functions start the same way is because they're both test functions. The duplication arises because, at the moment, test function is only half an abstraction. The abstraction exists in your mind, but in the code there's no way to express "this is a test function" other than to write code that follows a particular pattern.

Unfortunately, partial abstractions are a crummy tool for building software. Because a half abstraction is expressed in code by a manifestation of the pattern, you're guaranteed to have massive code duplication with all the normal bad consequences that implies for maintainability. More subtly, because the abstraction exists only in the minds of programmers, there's no mechanism to make sure different programmers (or even the same programmer working at different times) actually understand the abstraction the same way. To make a complete abstraction, you need a way to express "this is a test function" and have all the code required by the pattern be generated for you. In other words, you need a macro.

Because the pattern you're trying to capture is a DEFUN plus some boilerplate code, you need to write a macro that will expand into a DEFUN. You'll then use this macro, instead of a plain DEFUN to define test functions, so it makes sense to call it deftest.

```c
(defmacro deftest (name parameters &body body) 
  `(defun ,name ,parameters (let ((*test-name* ',name)) ,@body))
)
```

With this macro you can rewrite test-+ as follows:

```c
(deftest test-+ () 
  (check 
    (= (+ 1 2) 3) 
    (= (+ 1 2 3) 6) 
    (= (+ -1 -3) -4)
  )
)
```

### 9.6 A Hierarchy of Tests

Now that you've established test functions as first-class citizens, the question might arise, should test-arithmetic be a test function? As things stand, it doesn't really matter--if you did define it with deftest, its binding of `*test-name*` would be shadowed by the bindings in test-+ and test-* before any results are reported.

But now imagine you've got thousands of test cases to organize. The first level of organization is provided by test functions such as test-+ and test-* that directly call check. But with thousands of test cases, you'll likely need other levels of organization. Functions such as test-arithmetic can group related test functions into test suites. Now suppose some low-level test functions are called from multiple test suites. It's not unheard of for a test case to pass in one context but fail in another. If that happens, you'll probably want to know more than just what low-level test function contains the test case.

If you define the test suite functions such as test-arithmetic with deftest and make a small change to the `*test-name*` bookkeeping, you can have results reported with a "fully qualified" path to the test case, something like this:

```
pass ... (TEST-ARITHMETIC TEST-+): (= (+ 1 2) 3)
```

Because you've already abstracted the process of defining a test function, you can change the bookkeeping details without modifying the code of the test functions.6 To make `*test-name*` hold a list of test function names instead of just the name of the most recently entered test function, you just need to change this binding form:

```c
(let ((*test-name* ',name))
```

to the following:

```c
(let ((*test-name* (append *test-name* (list ',name))))
```

Since APPEND returns a new list made up of the elements of its arguments, this version will bind `*test-name*` to a list containing the old contents of `*test-name* `with the new name tacked onto the end.7 When each test function returns, the old value of `*test-name*` will be restored.

Now you can redefine test-arithmetic with deftest instead of DEFUN.

```c
(deftest test-arithmetic () 
  (combine-results 
    (test-+) 
    (test-*)
  )
)
```

The results now show exactly how you got to each test expression.

```c
CL-USER> (test-arithmetic) 
pass ... (TEST-ARITHMETIC TEST-+): (= (+ 1 2) 3) 
pass ... (TEST-ARITHMETIC TEST-+): (= (+ 1 2 3) 6) 
pass ... (TEST-ARITHMETIC TEST-+): (= (+ -1 -3) -4) 
pass ... (TEST-ARITHMETIC TEST-*): (= (* 2 2) 4) 
pass ... (TEST-ARITHMETIC TEST-*): (= (* 3 5) 15) 
T
```

As your test suite grows, you can add new layers of test functions; as long as they're defined with deftest, the results will be reported correctly. For instance, the following:

```c
(deftest test-math () 
  (test-arithmetic)
)
```

would generate these results:

```c
CL-USER> (test-math)
pass ... (TEST-MATH TEST-ARITHMETIC TEST-+): (= (+ 1 2) 3) 
pass ... (TEST-MATH TEST-ARITHMETIC TEST-+): (= (+ 1 2 3) 6) 
pass ... (TEST-MATH TEST-ARITHMETIC TEST-+): (= (+ -1 -3) -4) 
pass ... (TEST-MATH TEST-ARITHMETIC TEST-*): (= (* 2 2) 4) 
pass ... (TEST-MATH TEST-ARITHMETIC TEST-*): (= (* 3 5) 15) 
T
```

6 Though, again, if the test functions have been compiled, you'll have to recompile them after changing the macro.

7 As you'll see in Chapter 12, APPENDing to the end of a list isn't the most efficient way to build a list. But for now this is sufficient--as long as the test hierarchies aren't too deep, it should be fine. And if it becomes a problem, all you'll have to do is change the definition of deftest.

### 9.7 Wrapping Up

You could keep going, adding more features to this test framework. But as a framework for writing tests with a minimum of busywork and easily running them from the REPL, this is a reasonable start. Here's the complete code, all 26 lines of it:

```c
(defvar *test-name* nil) 

(defmacro deftest (name parameters &body body) 
  "Define a test function. Within a test function we can call other test functions or use 'check' to run individual test cases." 
  `(defun ,name ,parameters 
     (let ((*test-name* (append *test-name* (list ',name)))) 
      ,@body
     )
   )
) 

(defmacro check (&body forms) 
  "Run each expression in 'forms' as a test case." 
  `(combine-results 
     ,@(loop for f in forms collect `(report-result ,f ',f))
   )
) 

(defmacro combine-results (&body forms) 
  "Combine the results (as booleans) of evaluating 'forms' in order." 
  (with-gensyms (result) 
    `(let ((,result t)) 
       ,@(loop for f in forms collect `(unless ,f (setf ,result nil))) 
       ,result
     )
  )
) 

(defun report-result (result form) 
  "Report the results of a single test case. Called by 'check'." 
  (format t "~:[FAIL~;pass~] ... ~a: ~a~%" result *test-name* form) 
  result
)
```

1『目前没跑通，还是需要研读前面几章的内容才能找出问题所在。（2020-10-27）』

It's worth reviewing how you got here because it's illustrative of how programming in Lisp often goes.

You started by defining a simple version of your problem--how to evaluate a bunch of boolean expressions and find out if they all returned true. Just ANDing them together worked and was syntactically clean but revealed the need for better result reporting. So you wrote some really simpleminded code, chock-full of duplication and error-prone idioms that reported the results the way you wanted.

The next step was to see if you could refactor the second version into something as clean as the former. You started with a standard refactoring technique of extracting some code into a function, report-result. Unfortunately, you could see that using report-result was going to be tedious and error-prone since you had to pass the test expression twice, once for the value and once as quoted data. So you wrote the check macro to automate the details of calling report-result correctly.

While writing check, you realized as long as you were generating code, you could make a single call to check to generate multiple calls to report-result, getting you back to a version of test-+ about as concise as the original AND version.

At that point you had the check API nailed down, which allowed you to start mucking with how it worked on the inside. The next task was to fix check so the code it generated would return a boolean indicating whether all the test cases had passed. Rather than immediately hacking away at check, you paused to indulge in a little language design by fantasy. What if--you fantasized--there was already a non-short-circuiting AND construct. Then fixing check would be trivial. Returning from fantasyland you realized there was no such construct but that you could write one in a few lines. After writing combine-results, the fix to check was indeed trivial.

At that point all that was left was to make a few more improvements to the way you reported test results. Once you started making changes to the test functions, you realized those functions represented a special category of function that deserved its own abstraction. So you wrote deftest to abstract the pattern of code that turns a regular function into a test function.

With deftest providing an abstraction barrier between the test definitions and the underlying machinery, you were able to enhance the result reporting without touching the test functions.

Now, with the basics of functions, variables, and macros mastered, and a little practical experience using them, you're ready to start exploring Common Lisp's rich standard library of functions and data types.
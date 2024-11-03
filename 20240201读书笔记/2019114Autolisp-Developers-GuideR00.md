## 记忆时间

2020-10-06 | 2021-03-08 | 2021-10-12

## 资源汇总

[Pomoc: Introduction (AutoLISP)](http://help.autodesk.com/view/OARX/2018/PLK/?guid=GUID-A0E9D801-8BE9-4BF1-85E8-3807E15F3B71)

[AutoLISP | AfraLISP](https://www.afralisp.net/autolisp/)

[Forums - AutoCAD Forums](https://www.cadtutor.net/forum/)

[Tutorials | Lee Mac Programming](http://lee-mac.com/tutorials.html)

[Free LISP Programs | Lee Mac Programming](http://lee-mac.com/programs.html)

[Dynamic Block Functions | Lee Mac Programming](http://lee-mac.com/dynamicblockfunctions.html)

## 卡片

### 0101. 主题卡 —— list 数据类型常用的操作函数

A list is a group of related values separated by spaces and enclosed in parentheses. Lists provide an efficient method of storing numerous related values. After all, LISP is so-named because it is the LISt Processing language. Once you understand the power of lists, you will find that you can create more powerful and flexible applications. Lists are used to represent 2D and 3D coordinate values, and entity data.

Examples of lists are (1.0 1.0 0.0), ("this" "that" "the other"), and (1 . "ONE"). AutoLISP provides many functions for working with lists. The following are some of the most commonly used functions:

1 list - Creates a new list with any number of values.

2 append - Appends values to an existing list, and returns a new list.

3 cons - Adds an element to the beginning of a list, or constructs a dotted list.

4 length - Returns an integer indicating the number of elements in a list.

5 assoc - Searches an association list for an element and returns that association list entry.

6 car - Returns the first element of a list.

7 cdr - Returns a list containing all but the first element of the specified list.

8 nth - Returns the nth element of a list.

9 subst - Searches a list for an old item and returns a copy of the list with a new item substituted in place of every occurrence of the old item.

创建 list 数据相关的函数：

The list function provides a simple method of grouping related items. These items do not need to be of similar data types and can even be other lists. The following code groups three items as a list:

```c
(setq lst1 (list 1.0 "One" 1))

// out
(1.0 "One" 1)
```

1『试验过，list 函数后面的元素不能直接用 () 括起来。如果想简单用 () 声明的话，可以用下面讲到的 ' 符号，替代 list 函数名。回复：' 符号替代 list 函数名，经常看到，必须牢记。（2020-10-06）』

A list can also be created using the quote (or ' ) function.

```c
(setq lst1 '(1.0 "One" 1))

// out
(1.0 "One" 1)
```

修改 list 数据相关的函数：

The append function allows you to add new items to the end of a list, and the cons function allows you to add new items to the beginning of a list. The subst function can be used to substitute a new item for every occurrence of an old item. These functions do not modify the original list; they return a modified list. If you need to modify the original list, you explicitly replace the old list with the new list.

1『函数式编程的思想，数据的不变性，反正不会修改原来的值，只是返回一个新值。（2020-10-06）』

The append function takes any number of lists and runs them together as one list. Therefore, all arguments to this function must be lists. The following code adds another "One" to the list stored in lst1.

```c
(setq lst2 (append lst1 '("One")))

// out
(1.0 "One" 1 "One")
```

1『

注意，append 函数的参数都必须是 list 数据类型。而 cons 函数的参数一个是单个元素，一个是 list 类型。（2020-10-06）

补充：这里真的很容易弄错，append 的参数都是数组，而且自己之前存在一个误区，以为只能传 2 个数组作为参数拼接，看官方文档的说明（`(append [list ...])`），可以传多个数组的。这样的话其实就可以对一个大数组（包含多个小数组）直接调用 `apply` 函数，经试验可行的。下面的代码跑通了，这样的话之前自己很多功能的实现可以更加简洁。（2021-03-08）

```c
(defun c:foo ()
  (apply 'append (list '(1 2 3) '(11 12 13) '(21 22 23)))
)
```

』

The cons function combines a single element with a list. You can add another string "One" to the beginning of a list, lst2, with the cons function.

```c
(setq lst3 (cons "One" lst2 ))

// out
("One" 1.0 "One" 1 "One")
```

You can substitute all occurrences of an item in a list with a new item using the subst function. The following code replaces all strings "One" with the string "one".

```c
(setq lst4 (subst "one" "One" lst3))

// out
("one" 1.0 "one" 1 "one")
```

获取 list 数据中某些元素：

You can retrieve a specific item from a list with the nth function. This function accepts two arguments. The first argument is an integer that specifies which item to return. Lists start with a 0 index. A 0 specifies the first item in a list, 1 specifies the second item, and so on. The second argument is the list itself. The following code returns the second item in lst1.

```c
(nth 1 lst1)

// out
"One"
```

The car function returns the first item of a list. For example:

```c
(car lst1)

// out
1.0
```

The cdr function returns all items from a list as a new list, except the first item. For example:

```c
(cdr lst1)

// out
("One" 1)
```

AutoLISP also offers a number of additional functions that are variations of the car and cdr functions. For example, the cadr function returns the second element of a list and the caddr function returns the third item of a list. The cadr function is like using the cdr function on a list and then car on the resulting list.

```c
(cadr lst1)

// out
"One"

(car (cdr lst1))
// out
"One"
```

1『

list 元素排序：[vl-sort (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-F3B27BD2-27FA-4185-B22C-85509175C171)

Sorts the elements in a list according to a given compare function.

```c
(vl-sort lst comparison-function)
```

comparison-function. Type: Subroutine or Symbol. A comparison function. This can be any function that accepts two arguments and returns T (or any non-nil value). if the first argument precedes the second in the sort order. The comparison-function value can take one of the following forms:

```
A symbol (function name)
'(LAMBDA (A1 A2) ...)
(FUNCTION (LAMBDA (A1 A2) ...))
```

Return Values. Type: List. A list containing the elements of lst in the order specified by comparison-function. Duplicate elements may be eliminated from the list.

注意这里会自动去重的。

```c
(vl-sort '(3 2 1 3) '<)
(1 2 3)
```

Sort a list of 2D points by Y coordinate:

```c
(vl-sort '((1 3) (2 2) (3 1))
             (function (lambda (e1 e2)
                         (< (cadr e1) (cadr e2)))))
((3 1) (2 2) (1 3))
```

Sort a list of symbols:

```c
(vl-sort
   '(a d c b a)
   '(lambda (s1 s2)
    (< (vl-symbol-name s1) (vl-symbol-name s2))))
(A B C D)       ;  Note that only one A remains in the result list
```

vl-sort-i (AutoLISP). Sorts the elements in a list according to a given compare function, and returns the element index numbers.

设备位号按位号排序的代码实现：

```c
(defun c:foo (/ ss ss2)
  (setq ss '("R1101" "E1103" "E1102" "R1201" "P1201"))
  (setq ss2 '("甲醇反应釜" "换热器1" "换热器2" "反应釜1" "泵"))
  (setq ss (mapcar '(lambda (x y) (list x y)) ss ss2))
  (vl-sort ss '(lambda (x y) (< (car x) (car y))))
)
```

』

### 0102. 主题卡 —— 字符串数据的操作函数

A string is a group of characters surrounded by quotation marks. Within quoted strings the backslash (\) character allows control characters (or escape codes) to be included. When you explicitly use a quoted string in AutoLISP, that value is known as a literal string or a string constant. Examples of valid strings are “string 1” and “\nEnter first point:”.

AutoLISP provides many functions for working with string values. The following are some of the most commonly used functions:

1 strcat – Returns a string that is the concatenation of multiple strings.

2 strcase – Returns a string where all alphabetic characters have been converted to uppercase or lowercase.

3 strlen – Returns an integer that is the number of characters in a string.

4 substr – Returns a substring of a string.

5 vl-string-search – Searches for the specified pattern in a string.

6 vl-string-subst – Substitutes one string for another, within a string.

### 0103. 主题卡 —— lisp 中的多态

With AutoLISP, many functions require you to pass them values. These values are known as arguments. There are functions that also accept no arguments, and some in which accept optional arguments. User-defined functions cannot have optional arguments. When you call a user-defined function that accepts arguments, you must provide values for all arguments.

1『注意：自定义的函数是没法使用默认形参的，必须明确掉。回复：之前的理解有误，optional arguments 是指可选参数，而非默认参数。下面的信息也说明了，可以通过同一个函数名结合不同参数来实现「可选参数」。（2021-03-08）』

Note: You can define multiple user functions with the same name, but have each definition accept a different number or type of arguments.

1-2『同一个名字定义多个函数，每个函数设不同的形参。这倒是个折中的办法。回复：这不就是函数重载么，哈哈。（2020-07-03）回复：这个可以实现多态了，模拟面向对象范式，太 NB 了。做一张主题卡片。（2020-10-06）』—— 已完成

### 0104. 主题卡 —— 处理选择集的操作函数

Selection sets are groups of one or more selected objects (entities). You can interactively add objects to, remove objects from, or list objects in a selection set. The following example code uses the ssget function to return a selection set containing all the objects in a drawing.

```c
(ssget "X")
```

AutoLISP provides a number of functions for handling selection sets. The following lists some of the functions available for working with selection sets:

1 ssget - Prompts the user to select objects (entities), and returns a selection set;

2 ssadd - Adds an object (entity) to a selection set, or creates a new selection set;

3 ssdel - Removes an object (entity) from a selection set;

4 ssname - Returns the object (entity) name of the indexed element of a selection set;

5 sslength - Returns an integer containing the number of objects (entities) in a selection set.

1『获得选择集之后，需要靠 ssname，比如获取块选择集里第一个块的实体信息：`(setq ent (entget (ssname ss 0)))`。』

The ssget function provides the most general means of creating a selection set. It can create a selection set in one of the following ways: 1) Explicitly specifying the objects to select, using the Last, Previous, Window, Implied, Window Polygon, Crossing, Crossing Polygon, or Fence options; 2) Specifying a single point; 3) Selecting all objects in the database; 4) Prompting the user to select objects. With any option, you can use filtering to specify a list of properties and conditions that the selected objects must match.

### 0105. 主题卡 —— lisp 里数组过滤函数的实现

1『太重要了，升级为主题卡，哈哈。这张主题卡摘自数据「2019117Practical-Common-LispR00.md」（2020-10-27）』

Now suppose you want to wrap that whole expression in a function that takes the name of the artist as an argument. You can write that like this:

```c
(defun select-by-artist (artist)
  (remove-if-not
    #'(lambda (cd) (equal (getf cd :artist) artist))
    *db*
  )
)
```

Note how the anonymous function, which contains code that won't run until it's invoked in REMOVE-IF-NOT, can nonetheless refer to the variable artist. In this case the anonymous function doesn't just save you from having to write a regular function — it lets you write a function that derives part of its meaning — the value of artist — from the context in which it's embedded.

1-2-3『

看到这里才意识到 `remove-if-not` 就是用来构造过滤函数的啊，这正式自己之前 PHP 里用的最多的 `array_filter` 函数，试着在 autolisp 的文档里搜了下，发现果然有 `vl-remove-if-not`，有了它的话，自己很多很多的功能开发都可以基于它变得简洁优雅，简直是捡到金子了，哈哈。做一张术语卡片。（2020-10-22）

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

1『

函数 `vl-member-if-not` 目前没吃透，不过直觉上感觉有大用途。（2020-10-22）

补充：现在弄明白了。对一个数组里的各个元素用断言函数去判断，比如到第 3 个元素断言才为假，那么返回的数组是从第 3 个元素之后所有元素组成的数据。如果从头到尾断言均为真，那么返回 nil。那么这个函数就能够判断一个数组里的各个元素是否全部符合某个断言，只需判断结果是不是 nil，是的话即全部符合某个条件，印象中 JS 里也有一个这个函数。下面举了 2 个例子。（2021-03-08）

```c
(defun c:foo ()
  (vl-member-if-not '(lambda (x)
                       (= x 1)
                     )
                     (list 1 1 2 1 3)
  )
)

; 反的数组为 '(2 1 3)

(defun c:foo ()
  (vl-member-if-not '(lambda (x)
                       (= x 1)
                     )
                     (list 1 1 1 1)
  )
)
; 返回 nil
```

补充：其实用函数 vl-some/vl-every 可以达到同样的效果。（2021-10-12）

』

### 0106. 主题卡 —— list 映射处理的几个函数

[lambda (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-3B8BB020-1E1A-4FA3-B7B3-B5B20BA04CD9)

Defines an anonymous function.

```c
(lambda arguments expr ...)
```

arguments. Type: List. Arguments passed to an expression.

expr. Type: List. An AutoLISP expression.

Return Values. Type: Integer, Real, String, List, Symbol, Ename (entity name), T, or nil. Value of the last expr.

Remarks. Use the lambda function when the overhead of defining a new function is not justified. It also makes your intention more apparent by laying out the function at the spot where it is to be used. This function returns the value of its last expr, and is often used in conjunction with apply and/or mapcar to perform a function on a list.

```c
(apply '(lambda (x y z)
          (* x (- y z))
        )
        '(5 20 14)
)
30

(setq counter 0)
(mapcar '(lambda (x)
          (setq counter (1+ counter))
          (* x 5)
        )
        '(2 4 -6 10.2)
)
(10 20 -30 51.0)
```

[mapcar (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-8802AE73-1A05-457E-8A51-09677C23E26E)

Returns a list that is the result of executing a function with a list (or lists) supplied as arguments to the function.

```c
(mapcar function list1... listn)
```

function. Type: Subroutine. A function.

list1... listn. Type: List. One or more lists. The number of lists must match the number of arguments required by function.

Return Values. Type: List. A list.

```c
(setq a 10 b 20 c 30)
30

(mapcar '1+ (list a b c))
(11 21 31)
```

This is equivalent to the following series of expressions, except that mapcar returns a list of the results:

```c
(1+ a)
(1+ b)
(1+ c)
```

The lambda function can specify an anonymous function to be performed by mapcar. This is useful when some of the function arguments are constant or are supplied by some other means. The following example demonstrates the use of lambda with mapcar:

```c
(mapcar '(lambda (x)
          (+ x 3)
          )
         '(10 20 30)
)
(13 23 33)
```

[apply (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-0574ADA0-0950-456A-9330-A2518421536E)

Passes a list of arguments to, and executes, a specified function.

```c
(apply 'function list)
```
'function. Type: Symbol. A function. The function argument can be either a symbol identifying a defun, or a lambda expression.

list. Type: List or nil. A list. If the function accepts no arguments, the value can be nil.

Return Values. Type: String, Integer, Real, List, T, or nil. The result of the function call.

```
(apply '+ '(1 2 3))
6

(apply 'strcat '("a" "b" "c"))
"abc"
```

### Mapcar & Lambda

Lee Mac 上有关映射函数的知识：[Mapcar & Lambda | Lee Mac Programming](http://www.lee-mac.com/mapcarlambda.html)。

In my experience, the mapcar and lambda functions are two of the least understood functions in the AutoLISP programming language, however, when understood and used correctly, they can replace superfluous code and are powerful functions for dealing with lists.

1『个人对此深有感触，映射函数用的好，基本可以取代原来的循环函数。』

#### The Mapcar Function

Put simply, mapcar will evaluate a function on every element of one or more lists and return a list of the result of each such evaluation. The mapcar function is used in the following way:

```c
(mapcar <function> <list-1> <list-2> ... <list-n>)
```

Where function is a function to be evaluated on each item in the supplied list(s); this can be any function, user-defined or otherwise, taking any number of arguments.

list-1 ... list-n are a number of lists equal to the number of arguments required by the function to be evaluated. Hence if used with a function requiring a single argument, such as strcase (without the case flag), only one list need be supplied. Let me clarify this explanation with an example.

Example 1

Assume we have the following list of strings:

```c
("adam" "ben" "claire" "david")
```

Suppose we wish to convert each of these strings into uppercase (capitals). We could approach this task in a number of ways, for example, using the foreach function to shuffle through the list and create a new list of uppercase strings:

```c
(foreach str (reverse '("adam" "ben" "claire" "david"))
    (setq lst (cons (strcase str) lst))
)
```

The resultant value of the lst variable would then be:

```c
_$ lst
("ADAM" "BEN" "CLAIRE" "DAVID")
```

However this same task can be accomplished with more concision using the mapcar function:

```c
_$ (mapcar 'strcase '("adam" "ben" "claire" "david"))
("ADAM" "BEN" "CLAIRE" "DAVID")
```

Since the strcase function requires a single argument (a string) when converting to uppercase, only one list is supplied: the list of strings to be converted to uppercase.

The result: mapcar evaluates the strcase function on each element of the supplied list - this is equivalent to:

```c
_$ (list (strcase "adam") (strcase "ben") (strcase "claire") (strcase "david"))
("ADAM" "BEN" "CLAIRE" "DAVID")
```

1『有点悟到，`mapcar` 函数的本质实现途径了。』

Notice also that mapcar has been supplied with the function strcase prefixed with an apostrophe so that the strcase symbol is not evaluated, but rather treated as an argument for the mapcar function. This could also be achieved using the quote function in the following way:

```
_$ (mapcar (quote strcase) (quote ("adam" "ben" "claire" "david")))
("ADAM" "BEN" "CLAIRE" "DAVID")
```

Or using the function function to declare strcase as a function:

```c
_$ (mapcar (function strcase) (quote ("adam" "ben" "claire" "david")))
("ADAM" "BEN" "CLAIRE" "DAVID")
```

1『这里收获了好几个知识点：1）the function strcase prefixed with an apostrophe so that the strcase symbol is not evaluated，理解了很多地方看到的 symbol 概念，`'strcase` 就是一个 symbol。2）函数名加了撇号后就不会执行该函数了，形成第一个知识点的 symbol。3）撇号也可以用函数 `quote` 或者 `function` 来代替。（2021-03-08）』

Functions with More than One Argument

In the example above, the strcase function is demonstrated, and only one list is supplied as strcase only requires a single argument when converting to uppercase; but what if we want to use a function that requires multiple arguments?

Example 2

Consider the following example to add the items of two lists:

```c
_$ (mapcar '+ '(1 2 3 4 5) '(3 4 5 6 7))
(4 6 8 10 12)
```

Here mapcar is supplied with the + function, which takes any number of numerical arguments and adds them together. Hence in the above example, mapcar will evaluate the + function on each member of each list and return a list of the results:

```c
(4 6 8 10 12) = ((+ 1 3) (+ 2 4) (+ 3 5) (+ 4 6) (+ 5 7))
```

If the supplied lists are unequal in length, mapcar will cease evaluation when the shortest list has been processed, e.g.:

```c
_$ (mapcar '+ '(1 2 3 4 5) '(3 4 5))
(4 6 8)
```

1『哈哈，终于在这里找到了参数列表数量不一致时，系统默认处理的方式。（2020-10-26）』

#### The Lambda Function

Let's go back to our original list of strings:

```c
("adam" "ben" "claire" "david")
```

Suppose that we wish to convert each string to 'Titlecase' such that the first letter of each word is capitalised, for example:

```c
("Adam" "Ben" "Claire" "David")
```

We could again implement a method using the foreach function, and shuffle through our list:

```c
(foreach str (reverse '("adam" "ben" "claire" "david"))
    (setq lst (cons (strcat (strcase (substr str 1 1)) (substr str 2)) lst))
)
```

But we could also use mapcar to avoid the need to reverse the list and involve the extra variables. However, there is no function in LISP that allows us to capitalise the first letter of a word, so how to can we provide mapcar with a function to evaluate? Since the function supplied to mapcar is arbitrary, one possible solution could be to define a function ourselves and supply it:

```c
(defun titlecase ( str )
    (strcat (strcase (substr str 1 1)) (substr str 2))
)

_$ (mapcar 'titlecase '("adam" "ben" "claire" "david"))
("Adam" "Ben" "Claire" "David")
```

Here we have defined a function titlecase which takes a single argument str, and returns the value of this argument with the first letter capitalised. But this means that we now have an extra function definition in our code that may only be used once and could potentially be located elsewhere in the code, making it far less readable. A far better way to accomplish this task would be to use the lambda function.

The lambda function defines an anonymous function (a defun without a name if you like) and is usually used when the overhead of defining a new function is not justified - as in our case.

```
(mapcar '(lambda (s) (strcat (strcase (substr s 1 1)) (substr s 2)))
        '("adam" "ben" "claire" "david")
)
```

The code is now far more comprehensible since the operations performed by the anonymous lambda function are in-line with the flow of the code.

1『这里突然领悟到，匿名函数实现了「重构」里的「内联函数」经典手法。（2020-10-26）』

Further Examples

The mapcar and lambda functions are best illustrated and understood using examples, so here are a few more for you to study:

Adding one to each element of a list:

```c
_$ (mapcar '1+ '(1 2 3 4 5))
(2 3 4 5 6)
```

Adding two to each element of a list, using a defined function:

```c
(defun addtwo ( x ) (+ x 2))

_$ (mapcar 'addtwo '(1 2 3 4 5))
(3 4 5 6 7)
```

Using an anonymous lambda function:

```
_$ (mapcar '(lambda ( x ) (+ x 2)) '(1 2 3 4 5))
(3 4 5 6 7)
```

Concatenating a string with an integer, using a defined function taking two arguments:

```c
(defun join (str int)
  (strcat str (itoa int))
)

_$ (mapcar 'join '("a" "b" "c") '(1 2 3))
("a1" "b2" "c3")
```

Using an anonymous lambda function taking two arguments:

```c
_$ (mapcar '(lambda (str int) (strcat str (itoa int))) '("a" "b" "c") '(1 2 3))
("a1" "b2" "c3")
```

One final example to scramble the brain: a function to return the average point of a list of points:

```c
(defun averagepoint (lst / n)
    (setq n (float (length lst)))
    (mapcar '/ (apply 'mapcar (cons '+ lst)) (list n n n))
)
```

Notice that the above function exploits the fact that mapcar will cease evaluation when the shortest list is exhausted, since calling the function with 3D points will result in a 3D average point, and supplying 2D points will result in a 2D average point:

```c
_$ (averagepoint '((2 3 1) (2 4 1) (1 5 1)))
(1.66667 4.0 1.0)

_$ (averagepoint '((2 3) (2 1) (5 1)))
(3.0 1.66667)
```

Observe that this behaviour could also be obtained by using a lambda function to perform the division:

```c
(defun averagepoint (lst / n)
    (setq n (float (length lst)))
    (mapcar (function (lambda ( x ) (/ x n))) (apply 'mapcar (cons '+ lst)))
)
```

1『这个函数确实很烧脑，目前还是没有绕明白。但这个函数（多个数组取平均数）可以作为一个基础函数封装起来用。mark 一下。（2021-03-08）』

Further Reading

If this tutorial has sparked your interest in all things mapcar and lambda, the following publication from the Autodesk University written by Darren Young also provides an outline of mapcar, lambda and the apply function: LISP: Advance Yourself Beyond A Casual Programmer.

1-2『感觉又捡到金子了，已下载「附件1-CP401-1-Lisp-Advance-Yourself」作为本书的附件。』

### 0201. 术语卡 —— DXF group codes

CAD 里实体对象的唯一标识。重新打开文件，里面实体的名称会变，但它的 handle 是不会变的，是唯一的；一个实体的 handle，其 Group Code 为 5；handent 函数，通过传入实体的 handent 来获得实体的名称。

The DXF Reference describes the drawing interchange format (DXF™) and the DXF group codes that identify attributes of AutoCAD objects. You might need to refer to the DXF Reference when working with association lists describing entity data.

1-2-3『多次见到「association lists」这个概念，印象中，书籍「2019117Practical-Common-Lisp」里也有相关介绍。查了下书籍第 11 章的章名就是「Collections」，后面详细去研究。（2021-03-08）』—— 未完成

### 0202. 术语卡 —— Entity Names

An entity name is a numeric label assigned to objects in a drawing. It is actually a pointer into a file maintained by AutoCAD, and can be used to find the object's database record and its vectors (if they are displayed). This label can be referenced by AutoLISP functions to allow selection of objects for processing in various ways. Internally, AutoCAD refers to objects as entities.

Note: You can use the `vlax-ename->vla-object` function to convert an entity name to a VLA-object when working with ActiveX functions. The `vlax-vla-object->ename` function converts a VLA-object to an entity name. The following functions are useful when working with entity names: 1) entget - Retrieves an object's (entity's) definition data. 2) entlast - Returns the name of the last non-deleted main object (entity) in the drawing. 3) ssname - Returns the object (entity) name of the indexed element of a selection set. 4) entsel - Prompts the user to select a single object (entity) by specifying a point. 5) nentsel - Prompts the user to select an object (entity) by specifying a point, and provides access to the definition data contained within a complex object. 6) nentselp - Provides similar functionality to that of the nentsel function without the need for user input. 7) handent - Returns an object (entity) name based on its handle.

Entity names assigned to objects in a drawing are only in effect during the current editing session. The next time you open the drawing, AutoCAD assigns new entity names to the objects. You can use an object's handle to refer to it from one editing session to another.

1『实体名重新打开图纸会刷新掉，handle 则不会。』

Objects in a drawing can be represented as ActiveX (VLA) objects. When working with ActiveX methods and properties, you must refer to VLA-objects, not the ename pointer returned by functions such as entlast. VLA-objects can be converted to an ename pointer with `vlax-vla-object->ename`. You can also use `vlax-ename->vla-object` to convert an ename pointer to a VLA-object.

### 0203. 术语卡 —— cons 函数

[cons (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-33B418E7-DB3D-4CBE-954E-F070F0A7CB2B)

```c
(cons new-first-element list-or-atom)
```

new-first-element. Type: Integer, Real, String, List, T, or nil. Element to be added to the beginning of a list. This element can be an atom or a list.

list-or-atom. Type: Integer, Real, String, List, or T. A list or an atom.

Return Values. Type: List. The value returned depends on the data type of list-or-atom. If list-or-atom is a list, cons returns that list with new-first-element added as the first item in the list. If list-or-atom is an atom, cons returns a dotted pair consisting of new-first-element and list-or-atom.

```c
(cons 'a '(b c d))
(A B C D)

(cons '(a) '(b c d))
((A) B C D)

(cons 'a 2)
(A . 2)
```

替换块内某一个属性值的源码里有一片段，这里的 cons 形成的就是一个 dotted pair。3.8.2 小结里有 dotted pair 的相关知识。（2020-10-06）——做一张术语卡片—— 已完成

```c
(setq a (cons 1 "17.03.10"))
(setq b (assoc 1 entx))
(entmod (subst a b entx))
```

[列表构造函数 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E5%88%97%E8%A1%A8%E6%A7%8B%E9%80%A0%E5%87%BD%E6%95%B8)

列表构造函数是用来构造列表的基本函数，在大多数 LISP 体系的计算机编程语言中，使用的函数名称是 cons。cons 构成了存放两个变量与其指针的内存物件，这个物件被称为 CONS 单元、非原子的 S 表达式或 cons 对。LISP 编程中表达要把 x 加入 y 的语法：(cons x y)，构造了一个新物件。产生的结果具备了左半部，称为 CAR（第一元素或暂存器位址的内容）；以及右半部称为 CDR（其余元素或递减暂存器的内容）。

以上约略与面向对象的构造器概念相关，即产生一个给定参数的新物件，而其与代数数据类型系统的构造函数，更密切相关。「cons」和诸如「cons onto」的词句，也是函数编程的通用术语。有时运算子有类似作用，特别是在列表处理的情况下，被读作「CONS」。（例如 ML，Scala，F＃和 Elm 编程的：运算符，或 Haskell 编程的：运算符，都是向列表的开头添加一个元素。）

使用。虽然 cons 单元可用于储存有序的数据对，但它们更常用于组合为更复杂的复合数据结构，特别是列表和二叉树；有序对。例如 LISP 表达式 (cons 1 2) 产生一个有序的单元，在左半部存放 1，而右半部存放 2。左右次序不能互换（`(1 2)` 跟 `(2 1)` 不同）。在 LISP 表示法中，(cons 1 2) 结果会印出如下。须注意 1 和 2 之间的句点；这个 S 表达式是特殊的「点对」（所谓的 cons 对），并不是普通的「列表」。

1『关键信息：cons 点对，不是简单的列表。（2021-03-08）』

```c
(1 . 2)
```

列表。列表 (42 69 613) 的 Cons 单元图，以 cons 构造函数写成：

```c
(cons 42 (cons 69 (cons 613 nil)))
```

此外可用 list 函数写成：

```c
(list 42 69 613)
```

LISP 编程中的列表实作在「cons 对」之上。具体地说，每个列表的结构都是：一个空列表 ()，通常被称为 nil 的特殊物件；一个 cons 单元，car 代表这列表的第一个元素，而 cdr 则是包含其余元素的一个子列表。这形成了简单基本的列表，而 cons，car 和 cdr 函数可以操作列表的内容。注意，nil 是个特殊的空列表，并不是「cons 对」。考虑元素为 1, 2 和 3 的列表为例。这样的列表经由三个步骤产生：CONS 3 到 nil 空列表之上；CONS 2 到上一步的结果之上；CONS 1 到上一步的结果，产生最后的结果。这相当于单一表达式：

```c
(cons 1 (cons 2 (cons 3 nil)))
```

或可用 list 函数节略如下：

```c
(list 1 2 3)
```

最终结果是一个列表，形式如右：

```c
(1 . (2 . (3 . nil)))
```

通常结果会被打印为：(1 2 3)，因此 cons 操作会在既有列表的最前头，添加一个元素。例如，如果 x 是上面定义的列表，那么 (cons 5 x) 将产生列表：(5 1 2 3) 。另一个有用的函数是 append，用于合并两个列表。

树。cons 也容易建构出在叶片中储存数据的二叉树。例如以下代码： (cons (cons 1 2) (cons 3 4)) 产生了一棵树：

```c
((1 . 2) . (3 . 4))
```

技术上，前例中的列表（1 2 3）恰巧是不平衡的二叉树。要看到这点，只需重新排列图。

### 0204. 术语卡 —— dotted pair

Dotted pair lists must always contain two members and is the method AutoLISP uses to maintain entity definition data. When representing a dotted pair, members of the list are separated by a period ( . ). Most list-handling functions do not accept a dotted pair as an argument, so you should be sure you are passing the right kind of list to a function.

1『关键信息：很多 lisp 原生函数，传参是不支持 dotted pair 的。（2021-03-08）』

Dotted pairs are an example of an 'improper list'. An improper list is one in which the last cdr is not nil. In addition to adding an item to the beginning of a list, the cons function can create a dotted pair. If the second argument to the cons function is anything other than another list or nil, it creates a dotted pair.

```c
(setq sublist (cons 'lyr "WALLS"))
// out
(LYR . "WALLS")
```

The following functions are useful for handling dotted pairs:

1 car - Returns the first member of the specified dotted pair.

2 cdr - Returns the second member of the specified dotted pair.

3 assoc - Searches an association list for a member and returns that association list entry.

4 nth - Returns the nth element of a list.

The following code creates an association list of dotted pairs:

```c
(setq wallinfo (list sublist (cons 'len 240.0) (cons 'hgt 96.0)))
// out
((LYR . "WALLS") (LEN . 240.0) (HGT . 96.0))
```

The assoc function returns a specified list from within an association list regardless of the specified list's location within the association list. The assoc function searches for a specified key element in the lists and returns the first instance, as follows:

```c
(assoc 'len wallinfo)
// out
(LEN . 240.0)

(cdr (assoc 'lyr wallinfo))
// out
"WALLS"

(nth 1 wallinfo)
// out
(LEN . 240.0)

(car (nth 1 wallinfo))
// out
LEN
```

1『

醍醐灌顶。dotted pairs 就是 lisp 语言里的对象、「键-值」对、字典，哈哈。通过 assoc 函数可以提取特定「键」的值，这么一来，批量替换块内某一属性那边的源码片段渐渐看明白了。（2020-10-06）

```c
(setq a (cons 1 "17.03.10"))
(setq b (assoc 1 entx))
(entmod (subst a b entx))
```

autolisp 里一个高频操作 `cdr (assoc -1 ent)`，其中 -1 是 DXF group codes，表示 entity name，ent 是通过实体名获取的实体数据列表。

』

### 0205. 术语卡 —— Wild-Card Matching

通配符的使用说明：

1、`*` 相当于任意数量的任意字符。比如：1） `VT*` 会匹配到任意以 VT 开头的管道；2）`VT-25-*` 会匹配任意管径为 25 的管道。3）`VT*-50-*2J1*` 会匹配任意管径为 50 的、等级号为 2J1 的管道。等等。

2、`[]` 范围描述符。1）`[a-z]` 表示从 a 到 z 之间的任意一个。2）`[1-6]` 表示 1 到 6 之间的任意数据。

3、`?` 会相当于任何一个字符。

A string can be compared to a wild-card pattern with the wcmatch function. This can be helpful when needing to build a dynamic selection set (in conjunction with ssget) or to retrieve extended entity data by application name (in conjunction with entget). The wcmatch function compares a single string to a pattern. The function returns T if the string matches the pattern, and nil if it does not. The wild-card patterns are similar to the regular expressions used by many system and application programs.

1-2『直觉这里又是一个关键点。讲的应该就是通配符的知识点。回复：通配符与选择集（ssget）配合构建动态选择集，还可以与 entget 配合，结合实体名筛选。其实跟正则的功能差不多。回复：通配符的用处实在太大了，数据流开发中，批量修改块内某一属性前，要做的过滤功能可以通过这个来实现。（2020-10-06）做一张术语卡片。』—— 已完成

The following rules apply to wild-card patterns:

1 Alphabetic characters and numerals are treated literally in the pattern.

2 Brackets can be used to specify optional characters or a range of letters or digits.

3 A question mark ( ? ) matches a single character.

4 An asterisk ( * ) matches a sequence of characters; and, certain other special characters have special meanings within the pattern. When you use the * character at the beginning and end of the search pattern, you can locate the desired portion anywhere in the string.

1『注意，通配符里直接用 `*` 表示任意多个字符，正则里是用 `.*` 表示的，有时候会混淆掉。牢记调用 `wcmath` 时用通配符，掉正则时用正则模式。（2021-03-08）』

In the following examples, a string variable called matchme has been declared and initialized:

```c
(setq matchme "this is a string - test1 test2 the end")
// out
"this is a string - test1 test2 the end"
```

The following code checks whether or not matchme begins with the four characters "this":

```c
(wcmatch matchme "this*")
// out
T
```

The following code illustrates the use of brackets in the pattern. In this case, wcmatch returns T if matchme contains "test4", "test5", "test6" (4-6), or "test9" (note the use of the * character):

```c
(wcmatch matchme "*test[4-69]*")
// out
nil
```

In this case, wcmatch returns nil because matchme does not contain any of the strings indicated by the pattern. However, using the pattern "test[4-61]" does match the string because it contains “test1”.

```c
(wcmatch matchme "*test[4-61]*")
// out
T
```

The pattern string can specify multiple patterns, separated by commas. The following code returns T if matchme equals "ABC", or if it begins with "XYZ", or if it ends with "end".

```c
(wcmatch matchme "ABC,XYZ*,*end")
// out
T
```

About Wild-Card Patterns in Selection Set Filter Lists (AutoLISP). Symbol names specified in filtering lists can include wild-card patterns. The wild-card patterns recognized by ssget are the same as those recognized by the wcmatch function. When filtering for anonymous blocks, you must precede the `*` character with a reverse single quotation mark ( ` ), also known as an escape character, because the * is read by ssget as a wild-card character. For example, you can retrieve an anonymous block named *U2 with the following:

```c
(ssget "X" '((2 . "`*U2")))
```

1-2『选择特定名称块的实现方式，mark 一下。可以用来提取块里的基本信息用，做设备表的一个环节。wild-card 是指通配符。\` 应该是转义用的。回复：很棒啊，这样的话数据流里筛选仪表块只需要使用 `"Instrument*"` 过滤即可。合并到之前已经做好的通配符术语卡片。（2020-10-07）补充：SB 了，这里通配符可以直接在选择集里过滤，仪表块的例子很好，但自己之前实现的时候，竟然用的是「逻辑或」筛选出 3 大类仪表块。受此启发，布置图里的设备块，我应该都加上 `GsBzEquip` 做前缀，方便以后刷选。（2021-03-08）』

### 0206. 术语卡 —— lisp 里的函数

You can define your own functions. Once defined, these functions can be used at the AutoCAD Command prompt, the Visual LISP Console prompt, or within other AutoLISP expressions, just as you use the standard functions.

You can also create your own commands, because commands are just a special type of function. The defun function combines a multiple expressions into a function or command. This function requires at least three arguments: 1) Name of the function (symbol name). 2) Argument list (a list of arguments and local variables used by the function). The argument list can be nil or an empty list (). 3) AutoLISP expressions to execute with the function or command. There must be at least one expression in a function definition.

```c
(defun symbol_name ( arguments / local_variables )
  expressions
)
```

1『 / 后面的就代表是局部变量。arguments 准确的翻译即为函数的形参。』

The following example code defines a simple function that accepts no arguments and displays the message “bye” at the AutoCAD Command prompt. Note that the argument list is defined as an empty list (()):

```c
(defun DONE ( ) (prompt "\nbye! "))
// out
DONE
```

Once the DONE function is defined, you can use it as you would any other function. For example, the following code prints a message, then says “bye” at the AutoCAD Command prompt:

```c
(prompt "The value is 127.") (DONE) (princ)

The value is 127

bye!
```

1『这种代码定义出的命令跟我之前想的有出入，只能在源码里调用，在 CAD 里的话必须使用命令：`(DONE)`；正巧发现，lisp 的函数名是不分大小写的，用命令 (done) 也可以跑。』

Note how the previous example invokes the princ function without an argument to suppress an ending nil and achieves a quiet exit.

1『正巧弄明白了为什么语句最后要加 (princ)，是为了消除字符串尾部的「nil」，否则显示出来的尾部就是 bye!nil 了。』

Functions that accept no arguments may seem useless. However, you might use this type of function to query the state of certain system variables or conditions and to return a value that indicates those values.

1-2『这应该也是个关键点。回复：上面的信息直觉上很有用，但目前还是没看懂。lisp 里的函数做一张术语卡片。（2020-10-06）补充：这里目前来看没什么价值大点，只是说「无参数函数」的几个用途。（2021-03-09）』—— 已完成

If an AutoLISP function is defined with a name of the form C:xxx, it can be issued at the AutoCAD Command prompt in the same manner as a built-in AutoCAD command. This is true regardless of whether you define and load the function in VLISP or at the AutoCAD Command prompt. You can use this feature to add new commands to AutoCAD or to redefine existing commands.

1『解答了前面的疑问。这样的话就可以在 CAD 里跟常规命令一样使用了。』

To use functions as AutoCAD commands, be sure they adhere to the following rules:

1 The function name must use the form C:xxx (upper- or lowercase characters). The C: portion of the name must always be present; the XXX portion is a command name of your choice. C:xxx functions can be used to override built-in AutoCAD commands. (See About Redefining AutoCAD Commands [AutoLISP].)

2 The function must be defined with no arguments. However, local variables are permitted and it is a good programming practice to use them.

1『不能有参数，但可以使用局部变量。』

### 0207. 术语卡 —— cond 语句

Let's start looking at some code. To begin with, we'll write code that returns the factorial of the number 4. If you're unfamiliar with factorials, it's the mathematical process where you take a number, multiply it by a number one less, multiplied by a number one less until you get to 1. So, the factorial for the number 4 is the following formula 4 * 3 * 2 * 1 =  24.

```c
(defun factorial (n)
  (cond
    ((= n 0) 1)
    (T (* n (factorial (1- n))))
  )
)
```

1『这里递归实现阶乘的代码很值得借鉴。（2021-03-09）』

[cond (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-7BA45202-D95F-4F2D-8D83-965024826074)

The cond function accepts any number of lists as arguments. It evaluates the first item in each list (in the order supplied) until one of these items returns a value other than nil. It then evaluates those expressions that follow the test that succeeded.

```c
(cond
   ((minusp a) (- a))
   (t a)
)
```

If the variable a is set to the value -10, this returns 10. As shown, cond can be used as a case type function. It is common to use T as the last (default) test expression. Here's another simple example. Given a user response string in the variable s, this function tests the response and returns 1 if it is Y or y, 0 if it is N or n; otherwise nil.

```c
(cond
   ((= s "Y") 1)
   ((= s "y") 1)
   ((= s "N") 0)
   ((= s "n") 0)
   (t nil)
)
```

1-2『

cond 语句感觉还是很有用的，类似于其他语言里的 case 语句，多个不同的场景返回不同的值，这个场景可以通过 cond 来实现。看到这些例子，发现一般最后一条语句采用 `T` 结合默认结果来收尾。做一张术语卡片。（2020-10-27）—— 已完成

补充：cond 语句里，条件为真执行一个函数（而且条件为真时后面可以接多个执行语句，超级赞），多个 cond 语句应该可以实现之前自己一直想实现的卫语句。经测试，可行。（2021-03-09）

```c
(defun c:foo (/ testNum)
  (setq testNum 2)
  (cond
    ((= testNum 1)
     (princ "\ndalong11")
     (princ "\ndalong12")
     (princ))
    ((= testNum 2)
     (princ "\ndalong21")
     (princ "\ndalong22")
     (princ))
    ((= testNum 3)
     (princ "\ndalong31")
     (princ "\ndalong32")
     (princ))  
  )
)
```

』

### 0208. 术语卡 —— 递归

Recursion in programming is essentially the same thing, it's when a program calls itself. Of course, unlike the television picture that goes on and on forever, with recursive programming, you need to have an 'out' or your program would just go on forever and ever in an endless loop until your software or computer ran out of memory.

It's a difficult concept to grasp beyond the basic definition of 'a program that calls itself'. Anyone can understand that, but wrapping your head around how you'd use such a technique in your programs is a little more mind numbing. So to get you thinking about it and understanding it, let's look at a few examples, which might get you thinking about how you can apply this from a programming perspective.

Suppose you built a machine that has one conveyor that fed into it, and one that fed out of it. The machine, removes cardboard boxes to reveal the contents of the box. Boxes move down the in feed conveyor, into the machine, the cardboard box is removed, and the contents come out on the exit conveyor. Now, what would happen if one of the boxes contained more cardboard boxes? As the machine processed the big box that had more, smaller cardboard boxes inside, it stopped accepting big boxes from the feed conveyor. It then took the smaller boxes, and fed those back into the machine again. The machine then stripped the cardboard off the small boxes, except one of those contained even more tiny boxes. The small boxes stopped feeding into the machine, and the tiny boxes went back in. When all the tiny boxes finished going into the machine, the small boxes started again, and when all those were done, the large boxes started again. This process that the machine we built was performing, can be thought of as recursion.

Now instead of a conveyor of boxes, think of data in a List. Maybe the List has strings, integers, real numbers. Maybe some of the items are Lists and some of those may or may not contain Lists. How would you process this data not knowing how deep it was nested? you'd build a recursive function that processed the List, and when it encountered a nested List inside of the List, it would halt processing the List (temporarily), while it called itself and handled the nested List and when finished with the nested List, it would continue with the main list.

Another good example is a program that processes folders on your hard drive and finds files. You can point it to a folder, but does that folder contain more folders? And do those folders contain more folders? And are files scattered through out at all levels within those 'unknown' levels of sub-folders? This would be a good case for using recursion. This is the essence of recursive programming. Anytime you have an unknown set of potentially nested conditions or processes you need to perform, or data you need to examine, recursive programming can come to the rescue.

Calling the above code (factorial4 4) will do the same thing as the recursive example. Except in this case, instead of calling itself, it calls a completely different function that's almost identical. As you can see, a lot of the code is the same. And the 'unknown' nature of not knowing how many times (how deep is it nested) makes this a good application for recursion.

1『判断何时应该使用递归的办法，遇到那种自己都不知道要计算多少次的场景时，自己要有意识的想想能不能用递归函数来实现。（2020-10-27）』

Now that you've seen a couple examples, it's really not that hard. In fact, the hardest part of writing a program that uses recursion, is to make sure the program has an 'out' or at some point stops processing and doesn't just blindly call itself forever. But it takes a while; you won't be an expert just by reading this. You'll become and expert only after using this technique many times. To help you with this, Here's a little sample code. This code was posted to the AutoCAD's Customization discussion group. It was created by Owen Wengerd ([ManuSoft Home](http://www.manusoft.com/) & [Cadlock.com](http://ww1.cadlock.com/)) and is a very good example of short, well-written recursive program.

```c
(defun Str+ (source / prefix rchar)
  (cond
    ((= source "") "A")
    ((= (setq prefix (substr source 1 (1- (strlen source)))
              rchar (substr source (strlen source))
        )
        "Z"
     )
     (strcat (Str+ prefix) "A")
    )
    ((strcat prefix (chr (1+ (ascii rchar)))))
  )
)
```

What this codes does, it takes a string character and increments it. Its intent is to generate the next revision letter based in the current revision. So Let's say your drawing is at revision 'B', calling the function (str+ "B") would return 'C'. Calling the program with (str+ "C") would return 'D' and so on. that's not that hard in itself, and you wouldn't need recursion to perform it. But what happens when you get to revision "Z" and need to go to 'AA' or you're at revision 'AZ' and need to go to 'BA'. This program handles that and that's where the recursion comes in. So your homework when you get back to your office is to slice and dice this program up and see how it works. Play with it a little and see if you can truly understand what it's doing. And if you're really ambitious, try modifying the program so that it works as described, but does Not use the letters 'O' (oh) and 'I' (eye) which resemble 0 (zero) and 1 (one). Use the following lines to make notes on recursion, this class or how you might use it in your own environment.

### 0209. 术语卡 —— vl-some 和 vl-every 函数

The fact that we're dealing with numbers in this example, means that it would really not be that hard to create a loop with a few counter variables to perform this same calculation. But not all cases would be that easy. Let's look at another example that deals with nested lists…

```c
(setq mylist '(1 2 3 (4 5 (6 7 (8 9) 10) 11) 12 13 (14 15 (16))))

(defun item-in-list (L I)
  (vl-some '(lambda (x)
              (cond
                ((= x I) T)
                ((= (type x) 'LIST) (item-in-list x I))
                (T nil))
            )
            L
  )
)
```

The code in this example looks for a user specified item within a list. The AutoLISP function (member) typically handles this type of need. But if the list contains other nested lists, (member) just doesn't do it anymore. In this case, we're using a function called (vl-some). This function takes a quoted function, just like (apply) or (mapcar). The purpose of (vl-some) is to return T if the function evaluates to T for at least 1 (one) item in the list. If the function evaluates to NIL for all items, it returns NIL. it's the perfect function for our needs. Next, we build our function. Just like (mapcar), (vl-some) will be handed each item in the list, one at a time. Your function then needs to check if that item matches what we're looking for. that's not hard. But what if the list item, is another list? Our function must also check for that, and if the list item is another list, it calls itself again to process the nested list. Now, (vl-some) itself isn't looking for our item, our (lambda) function is doing that. What (vl-some) does is looks for T or NIL and it returns T or NIL. (lambda) is pasting the T and/or NILs to (vl-some).

1-2-3『

看到 `vl-some` 后印象中「JS 忍者秘籍」讲数组操作的那章有一个函数功能相同，去查了下是 `some` 函数，顺带看到 JS 里配套的一个 `every` 函数，果然又在 autolisp 里查到 `vl-every` 函数，哈哈。相关知识做一张术语卡。（2020-10-27） —— 已完成

忍者秘籍里：

测试数组，元素处理集合的元素时，常常遇到需要知道数组的全部元素或部分元素是否满足某些条件。为了尽可能有效地编写这段代码，JavaScript 数组具有内置的 every 和 some 方法，如清单 9.8 所示。1）every 方法接收回调函数，对集合中的每个 ninja 对象检查是否含有 name 属性。当且仅当全部的回调函数都返回 true 时，every 方法才返回 true，否则返回 false。

```js
var allNinjasAreNamed = ninjas
(ninja => "name" in ninja);
```

some 方法从数组的第 1 项开始执行回调函数，直到回调函数返回 true。如果有一项元素执行回调函数时，返回 true，some 方法返回 true；否则，some 方法返回 false。

```js
const someNinjasAreArmed = ninjas.some(ninja => "weapon" in ninja);
```

[vl-every (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-8BF61C9E-1382-4168-A778-FEA394A361CC)

Checks whether the predicate is true for every element combination.

```c
(vl-every predicate-function list [list ...])
```

predicate-function. Type: Subroutine or Symbol. The test function. This can be any function that accepts as many arguments as there are lists provided with vl-every, and returns T on any user-specified condition. The predicate-function value can take one of the following forms:

```c
A symbol (function name)
'(LAMBDA (A1 A2) ...)
(FUNCTION (LAMBDA (A1 A2) ...))
```

list. Type: List. A list to be tested.

Return Values. Type: T or nil. T, if predicate-function returns a non-nil value for every element combination; otherwise nil.

Remarks. The `vl-every` function passes the first element of each supplied list as an argument to the test function, followed by the next element from each list, and so on. Evaluation stops as soon as one of the lists runs out.

Examples

Check whether there are any empty files in the current directory:

```c
(vl-every
'(lambda (fnm) (> (vl-file-size fnm) 0))
   (vl-directory-files nil nil 1))
T
```

Check whether the list of numbers in nlst is ordered by `'<=`:

```
(setq nlst (list 0 2 pi pi 4))
(0 2 3.14159 3.14159 4)

(vl-every '<= nlst (cdr nlst))
T
```

1『这个实现好，判断一个数组是否排好了序，直觉上以后肯定会遇到这个功能。（2020-10-27）』

Compare the results of the following expressions:

```c
(vl-every '= '(1 2) '(1 3))
nil

(vl-every '= '(1 2) '(1 2 3))
T
```

The first expression returned nil because vl-every compared the second element in each list and they were not numerically equal. The second expression returned T because vl-every stopped comparing elements after it had processed all the elements in the shorter list (1 2), at which point the lists were numerically equal. If the end of a list is reached, vl-every returns a non-nil value.

The following example demonstrates the result when vl-every evaluates one list that contains integer elements and another list that is nil:

```c
(setq alist (list 1 2 3 4))
(1 2 3 4)

(setq junk nil)
nil

(vl-every '= junk alist)
T
```

The return value is T because vl-every responds to the nil list as if it has reached the end of the list (even though the predicate has not yet been applied to any elements). And since the end of a list has been reached, vl-every returns a non-nil value.

[vl-some (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-2840F793-DA88-4140-8A9D-EBAC47B62F9D)

Checks whether the predicate is not nil for one element combination.

```c
(vl-some predicate-function lst [lst ...])
```

predicate-function. Type: Subroutine or Symbol. The test function. This can be any function that accepts as many arguments as there are lists provided with vl-some, and returns T on a user-specified condition. The predicate-function value can take one of the following forms:

lst. Type: List. A list to be tested.

Return Values. Type: List or nil.

The predicate value, if predicate-function returned a value other than nil; otherwise nil.

Remarks. The vl-some function passes the first element of each supplied list as an argument to the test function, then the next element from each list, and so on. Evaluation stops as soon as the predicate function returns a non-nil value for an argument combination, or until all elements have been processed in one of the lists.

Examples

The following example checks whether nlst (a number list) has equal elements in sequence:

```c
(setq nlst (list 0 2 pi pi 4))
(0 2 3.14159 3.14159 4)

(vl-some '= nlst (cdr nlst))
T
```

自己写了一个例子：

```c
(defun foo ()
  (vl-some '(lambda (x) (= x 2))
    '(1 3 4 5 2)
  )
)
```

』

### 0301. 任意卡 —— MNL 源文件

AutoLISP source code can also be stored in files with a .mnl extension. A Menu AutoLISP (MNL) file contains custom functions and commands that are required for the elements defined in a customization (CUIx) file. A MNL file is loaded automatically when it has the same name as a customization (CUIx) file that is loaded into the AutoCAD-based product.

1-2『

MNL 应该就是可以显示的自定义菜单，后面需要自己实现的。（2020-07-02）回复：数据流实现了菜单，新建了一个 dataflow.cuix 文件，使用的过程中自动生成了一个 dataflow.mnr 文件。受这里的信息启发，D 盘下的 dataflowcad 文件夹里，把原来的 lsp 文件更改为 dataflow.mnl，这样的话 cuix 文件底下的不用手动加载 lsp 文件了，经验证，可行，哈哈。做一张任意卡片。（2020-10-06）

补充：之前源码直接改成 mnl 后用户还是能看到源码，次方法就一直没用。但后来发现可以做一个总启动的文件，那么只需把总启动的文件名更改为「dataflow.mnl」就可以满足自己的需求。（2021-03-09）

```c
(defun s::startup ()
  (vl-load-all "D:\\dataflowcad\\dataflow.VLX")
)
(princ "\n数据流一体化开发者：冯大龙、谢雨东、华雷、曾涵卫、徐骋、郑飞宏、靳淳，版本号V2.0")
```

』

For example, on Windows, when acad.cuix is loaded, the file named acad.mnl is also loaded if it is found in one of the folders listed as part of the AutoCAD Support File Search Path. If a CUIx file does not have a corresponding MNL file, no error is displayed, the product just moves and loading other support files.

### 0302. 任意卡 —— quote (') 与使用 list 函数创建 list 数据的区别

The latter uses the value of variable abc as the X component of the point list. If all members of a list are constant values, you can use the quote function to explicitly define the list, rather than the list function. The quote function returns an expression without evaluation, as follows:

1『只有 list 元素是 constant 值是才可以用 quote。』

```c
(setq pt1 (quote (4.5 7.5)))

// out
(4.5 7.5)
```

The single quotation mark ( ' ) can be used as shorthand for the quote function. The following code produces the same result as the preceding code.

```c
(setq pt1 '(4.5 7.5))

// out
(4.5 7.5)
```

The quote and (') functions cannot be used to create a list using values that are stored in a variable. The following code does not return the excepted results:

```c
(setq abc 3.45)
// out
3.45

(setq pt4 (quote abc 1.23))
// out
; error: syntax error
```

1-2『这里终于弄明白 quote (') 与使用 list 的区别，简化函数是有条件的，只能是常数，而不能传入变量。做一张任意卡片。』—— 已完成

### 0303. 任意卡 —— 获取 CAD 数据的选择集

ssget 的官方文档：[Pomoc: ssget (AutoLISP)](http://help.autodesk.com/view/OARX/2018/PLK/?guid=GUID-0F37CC5E-1559-4011-B8CF-A3BA0973B2C3)

```c
(ssget [sel-method] [pt1 [pt2]] [pt-list] [filter-list])
```

By specifying filters, you can obtain a selection set that includes all objects of a given type, on a given layer, or of a given color. The following example returns a selection set that consists only of blue lines that are part of the implied selection set .

```c
(ssget "_I" '((0 . "LINE") (62 . 5)))

// 获取特定块名称的块实体
(setq ss (ssget '((0 . "INSERT") (2. "InstrumentP"))))
```

找到一个获取实体类型（entity type）的办法，比如获取块的类型（2020-10-07）。

```c
// 选择一个实体对象
(setq ss (ssget))
// 获取该实体对象的数据列表
(setq ent (entget (ssname ss 0)))
// 查看数据列表，列表里是一个个 dotted pairs，键是 0 的即为该实体对象的类型，块的是 "INSERT"，单行文字的是 "TEXT"
!ent
```

1『目前发现直接用「entsel」获取实体数据更方便，获得的数据也更简洁。』

### 0304. 任意卡 —— Relational Tests in Filter Lists

About Relational Tests in Filter Lists for Selection Sets (AutoLISP). Unless otherwise specified, an equivalency is implied for each item in the filter-list. For numeric group codes (integers, reals, points, and vectors), you can specify other relations by including a special -4 group code that specifies a relational operator. The value of a -4 group code is a string indicating the test operator to be applied to the next group in the filter-list. The following selects all circles with a radius (group code 40) greater than or equal to 2.0:

```c
(ssget "X" '((0 . "CIRCLE") (-4 . ">=") (40 . 2.0)))
```

3『 group code 0, Text string indicating the entity type (fixed); group code -4, APP: conditional operator (used only with ssget); group code 40, Floating-point values. (text height, scale factors, and so on)』

1-2『这个过滤集中增加条件语句实在是赞，`(-4 . ">=")`。Relational Tests in Filter Lists 做一张任意卡片。（2020-10-07）补充：这里选择集过滤的手段比我之前想象的更「深」，可以再深挖。（2021-03-09）』

The grouping operators are specified by -4 dxf group codes, like the relational operators. They are paired and must be balanced correctly in the filter list or the ssget call will fail.

```c
(ssget "X"
  '(
    (-4 . "<OR")
      (-4 . "<AND")
        (0 . "CIRCLE")
        (40 . 1.0)
      (-4 . "AND>")
      (-4 . "<AND")
        (0 . "LINE")
        (8 . "ABC")
      (-4 . "AND>")
    (-4 . "OR>")
  )
)
```

This filter list allows the selection of all circles with a radius of 1.0 plus all lines on layer "ABC". The grouping operators are not case-sensitive; for example, you can specify "and>", "<or", instead of "AND>", "<OR". Grouping operators are not allowed within the -3 dxf group code. Multiple application names specified in a -3 dxf group code use an implied AND operator. If you want to test for extended data using other grouping operators, specify separate -3 dxf group codes and group them as desired.

The following example code demonstrates how to select all circles having extended data for either application "APP1" or "APP2" but not both:

```c
(ssget "X"
  '((0 . "CIRCLE")
    (-4 . "<XOR")
      (-3 ("APP1"))
      (-3 ("APP2"))
    (-4 . "XOR>")
  )
)
```

1『经验证，上面的代码里的 `XOR` 得改成 `OR` 才有效。』

### 0305. 任意卡 —— autolisp 中的逻辑判断

AND returns true if all arguments are true.

OR returns true if any of the arguments are true.

NOT returns true if it's argument is false and returns false if it's argument is true. Let's look at some.

### 0306. 任意卡 —— handle 与实体名之间的切换

直接在 CAD 里用 `list` 命令选中一个实体，在显示的信息里，句柄即为 handle。

1、通过实体名获取实体的 handle：借用任意卡 0303 里的信息，可以直接获取一个实体的数据信息，举个例子，里面的 `(5 . "59DAA")` 这个即为 handle。那么获取这个数据的办法就显而易见了，跟获取它的坐标 `(10 xx yy)`，图层 `(0 . "0")`，块名称 `(2 . "PipeArrowLeft")` 等等的信息一模一样。

```
(cdr (assoc 5 (entget ename)))
```

2、通过 handle 获取实体名。

```
(setq ename (handent "5a2"))
```

### 0307. 任意卡 —— AutoLisp 历史

AutoLISP is based on the LISP programming language but was written by Autodesk specifically for AutoCAD. It was introduced with AutoCAD version 2.18 (a minor version update of AutoCAD 2.1) in January 1986. Autodesk continued to enhance and extend AutoLISP up to and including AutoCAD Release 13 in November 1994. From Release 14 onwards, Autodesk have not developed AutoLISP, choosing to focus efforts on the then new Visual LISP version of the language. Despite the fact that AutoLISP has not changed in almost two decades, it remains incredibly popular with AutoCAD users. This is mainly due to its ease of use and the massive productivity gains that can be earned through its implementation. See the AutoLISP Wikipedia article for more information.

### 0308. 任意卡 —— 启动加载命令

```c
(defun s::startup ()
  (vl-load-all "D:\\dataflowcad\\dataflow.VLX")
)
```

```
(load "D:\\dataflowcad\\dataflow.VLX")
```

## 0101Introduction.md

可以搜索问题的官方地址，可以按 Google 搜索的规则来：

[Search - Autodesk Community](https://forums.autodesk.com/t5/forums/searchpage/tab/message?advanced=false&allow_punctuation=false&inactive=false)

[主页 | Autodesk Knowledge Network](https://knowledge.autodesk.com/zh-hans)

Visual LISP isn't just an extension of AutoLISP, but is also a complete and integrated development environment (IDE) that includes a compiler, debugger, and other tools to increase productivity when developing custom programs.

They can also be very complex, extracting and formatting information from blocks, and constructing the extracted information into a table. When you first get started, keep things simple and then once you feel comfortable with AutoLISP then start looking at conditional and looping statements.

When you begin to develop an AutoLISP program, you should keep the following steps in mind: Think about which tasks you want to accomplish; Design the program; Write the code; Add comments and format the code for readability; Test and debug the program.

AutoLISP is a programming language designed for extending and customizing AutoCAD product functionality. It is based on the LISP programming language, whose origins date back to the late 1950s. LISP was originally designed for use in Artificial Intelligence (AI) applications, and is still the basis for many AI applications.

Autodesk introduced AutoLISP as an application programming interface (API) in Release 2.1, in the mid-1980s. LISP was chosen as the initial AutoCAD API because it was uniquely suited for the unstructured design process of AutoCAD projects, which involved repeatedly trying different solutions to design problems.

AutoLISP programs are developed using a basic ASCII text editor, such as NotePad on Windows or TextEdit on Mac OS, or the Visual LISP (VLISP) integrated development environment (IDE) on Windows only. The Visual LISP integrated development environment (IDE) provides features to help ease the tasks of source-code creation and modification, program testing, and debugging.

After an AutoLISP program is written, it must loaded into the product before it can be used or debugged. Debugging your program allows you to evaluate and verify the code is working as expected, and if not identify what might be going wrong. The basics of debugging involve adding statements to the code and reviewing the contents of variables at strategic points in the program. If you discover you still do not have enough information to determine the error, you change the code again by adding additional debugging points. And finally, when you get the program working, you can either comment out or remove the debugging code.

This documentation introduces the constructs of the AutoLISP language, and explains how to write and run AutoLISP programs. If you have developed AutoLISP programs in earlier releases of AutoCAD, it is important that you refer to the "New and Changed AutoLISP Functions Reference (AutoLISP)" topic for information on additions and changes to AutoLISP that may affect your programs.

The AutoLISP documentation is broken down into three types of content: Reference documentation describes what every AutoLISP function does and provides basic samples to see how a function can be used; Tutorial documentation contains step-by-step instructions guiding you toward writing a working AutoLISP program; Developer's documentation assumes you have some experience with AutoCAD. Prior experience with AutoLISP is not required.

2『上面的这 3 个大文档要去看完。』

The following is covered by the AutoLISP Developer's documentation: Details on the concepts and structures of the AutoLISP language; Provides a summary of all AutoLISP functions by category and information on AutoLISP error codes; Describes how to develop and test AutoLISP programs; Explains how to design and implement dialog boxes with AutoLISP applications. (Windows only)

1『最终目标是要熟练使用 AutoLISP applications 构造图形窗口（dialog boxes）的自定义命令。』

In addition to the AutoLISP reference and tutorial topics, several other AutoCAD documentation resources might be required for building and deploying applications. You might need to use these resources when working with AutoLISP:

1 AutoCAD ActiveX Reference and Developer's Guides contain information on accessing ActiveX methods, properties, objects, and events. If you develop AutoLISP applications that use ActiveX automation to reference AutoCAD objects, you will need to refer to these guides. The help files can be accessed from %ProgramFiles%\Common Files\Autodesk Shared. (AutoCAD for Mac does not support ActiveX)
AutoCAD Customization topics contain basic information on creating and modifying customizable files. For example, they include information on customizing the user interface, and creating custom linetypes and hatch patterns. These topics can be found in the AutoCAD product help.

2 The DXF Reference describes the drawing interchange format (DXF™) and the DXF group codes that identify attributes of AutoCAD objects. You might need to refer to the DXF Reference when working with association lists describing entity data. The DXF Reference is available through the AutoCAD product help or the Autodesk website (www.autodesk.com/dxf).

4 The ObjectARX Reference and Developer's Guides contain information on using ObjectARX® to develop custom AutoCAD applications. AutoCAD reactor functionality is implemented through ObjectARX. If you develop AutoLISP applications that implement reactor functions, you may want to refer to the ObjectARX Reference . The ObjectARX Reference and Developer's Guides are not installed with the AutoCAD program. To obtain this documentation, download the ObjectARX SDK (Software Development Kit) from the www.autodesk.com/objectarx.

5 The Managed .NET Reference and Developer's Guides contain information on using the Managed .NET API to develop custom AutoCAD applications. The Managed .NET Reference is not installed with the AutoCAD program. To obtain this documentation, download the ObjectARX SDK (Software Development Kit) from the www.autodesk.com/objectarx. The Managed .NET Developer's Guide is available from the AutoCAD product help. (AutoCAD for Mac does not support Managed .NET development)

2-3『

hatch patterns 的概念；DXF group codes 的概念做一张术语卡片；已下载书籍「2020038dxf-reference2012」。

[Free AutoCAD Hatch Patterns | CADHatch](http://www.cadhatch.com/)

[DXF Group Codes | AfraLISP](https://www.afralisp.net/reference/dxf-group-codes.php)

』

1『原文中有各版本的主要更新信息。』

## 0106. Error Codes and FQA

### 6.1 Error Codes Reference (AutoLISP)

The following table shows the values of error codes generated by AutoLISP. The ERRNO system variable is set to one of these values when an AutoLISP function call causes an error that AutoCAD detects. AutoLISP applications can inspect the current value of ERRNO with (getvar "errno").

The ERRNO system variable is not always cleared to zero. Unless it is inspected immediately after an AutoLISP function has reported an error, the error that its value indicates may be misleading. This variable is always cleared when starting or opening a drawing.

Note: The possible values of ERRNO, and their meanings, are subject to change.

### 6.2 FAQ: What is the Difference Between Lightweight Polylines and Old-Style Polylines? (AutoLISP)

A lightweight polyline (lwpolyline) is defined in the drawing database as a single graphic entity unlike the old-style polyline, which is defined as a group of subentities.

Lwpolylines display faster and consume less disk space and RAM. As of AutoCAD Release 14, 3D polylines are always created as old-style polyline entities, and 2D polylines are created as lwpolyline entities, unless they are curved or fitted with the AutoCAD PEDIT command. When a drawing from an earlier release is opened in AutoCAD Release 14 or a later release, all 2D polylines convert to lwpolylines automatically, unless they have been curved or fitted or contain extended data (xdata).

### 6.3 FAQ: What Symbol Table Entries Cannot Be Renamed or Modified? (AutoLISP)

Most entries in the symbol tables can be renamed or modified with a few exceptions.

The following table shows which symbol table entries cannot be modified or renamed, except that most LAYER symbol table entries can be renamed and xdata can be modified on all symbol table entries.

### 6.4 FAQ: How Do I Process Curve-Fit and Spline-Fit Polylines? (AutoLISP)

An old-style polyline might contain vertices that were not created explicitly; these auxiliary vertices were inserted automatically by the AutoCAD PEDIT command's Fit and Spline options.

You can safely ignore these additional vertices when stepping through a polyline with entnext because changes to these vertices will be discarded the next time the AutoCAD PEDIT command is used to fit or convert the polyline to a spline. The old-style polyline entity's group code 70 flags indicate whether the polyline has been curve-fit (bit value 2) or spline-fit (bit value 4). If neither bit is set, all the polyline's vertices are regular user-defined vertices.

However, if the curve-fit bit (2) is set, alternating vertices of the polyline have the bit value 1 set in their 70 group code to indicate that they were inserted by the curve-fitting process. If you use entmod to move the vertices of such a polyline with the intent of refitting the curve by means of the AutoCAD PEDIT command, ignore these vertices.

Likewise, if the old-style polyline entity's spline-fit flag bit (bit 4) is set, an assortment of vertices will be found—some with flag bit 1 (inserted by curve fitting if the AutoCAD SPLINESEGS system variable was negative), some with bit value 8 (inserted by spline fitting), and all others with bit value 16 (spline frame-control point). Here again, if you use entmod to move the vertices and you intend to refit the spline afterward, move only the control-point vertices.

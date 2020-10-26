# 2019114Autolisp-Developers-GuideR00

## 记忆时间

2020-10-06

## 资源汇总

[Pomoc: Introduction (AutoLISP)](http://help.autodesk.com/view/OARX/2018/PLK/?guid=GUID-A0E9D801-8BE9-4BF1-85E8-3807E15F3B71)

[Forums - AutoCAD Forums](https://www.cadtutor.net/forum/)

[Tutorials | Lee Mac Programming](http://lee-mac.com/tutorials.html)

[Free LISP Programs | Lee Mac Programming](http://lee-mac.com/programs.html)

[Dynamic Block Functions | Lee Mac Programming](http://lee-mac.com/dynamicblockfunctions.html)

[AutoLisp 选择对象函数 ssget 用法 - 钉钉铛铛 - 博客园](https://www.cnblogs.com/chenjiafeng/p/7537786.html)

[COND vs. IF | AfraLISP](https://www.afralisp.net/autolisp/tutorials/cond-vs-if.php)

## 卡片

### 0101. 主题卡——list 数据类型常用的操作函数

A list is a group of related values separated by spaces and enclosed in parentheses. Lists provide an efficient method of storing numerous related values. After all, LISP is so-named because it is the LISt Processing language. Once you understand the power of lists, you will find that you can create more powerful and flexible applications. Lists are used to represent 2D and 3D coordinate values, and entity data.

Examples of lists are (1.0 1.0 0.0), ("this" "that" "the other"), and (1 . "ONE"). AutoLISP provides many functions for working with lists. The following are some of the most commonly used functions:

1. list - Creates a new list with any number of values.

2. append - Appends values to an existing list, and returns a new list.

3. cons - Adds an element to the beginning of a list, or constructs a dotted list.

4. length - Returns an integer indicating the number of elements in a list.

5. assoc - Searches an association list for an element and returns that association list entry.

6. car - Returns the first element of a list.

7. cdr - Returns a list containing all but the first element of the specified list.

8. nth - Returns the nth element of a list.

9. subst - Searches a list for an old item and returns a copy of the list with a new item substituted in place of every occurrence of the old item.

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

1『注意，append 函数的参数都必须是 list 数据类型。而 cons 函数的参数一个是单个元素，一个是 list 类型。（2020-10-06）』

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

### 0102. 主题卡——字符串数据的操作函数

A string is a group of characters surrounded by quotation marks. Within quoted strings the backslash (\) character allows control characters (or escape codes) to be included. When you explicitly use a quoted string in AutoLISP, that value is known as a literal string or a string constant. Examples of valid strings are “string 1” and “\nEnter first point:”.

AutoLISP provides many functions for working with string values. The following are some of the most commonly used functions:

1. strcat – Returns a string that is the concatenation of multiple strings.

2. strcase – Returns a string where all alphabetic characters have been converted to uppercase or lowercase.

3. strlen – Returns an integer that is the number of characters in a string.

4. substr – Returns a substring of a string.

5. vl-string-search – Searches for the specified pattern in a string.

6. vl-string-subst – Substitutes one string for another, within a string.

### 0103. 主题卡——lisp 中的多态

With AutoLISP, many functions require you to pass them values. These values are known as arguments. There are functions that also accept no arguments, and some in which accept optional arguments. User-defined functions cannot have optional arguments. When you call a user-defined function that accepts arguments, you must provide values for all arguments.

1『注意：自定义的函数是没法使用默认形参的，必须明确掉。』

Note: You can define multiple user functions with the same name, but have each definition accept a different number or type of arguments.

1-2『同一个名字定义多个函数，每个函数设不同的形参。这倒是个折中的办法。回复：这不就是函数重载么，哈哈。（2020-07-03）回复：这个可以实现多态了，模拟面向对象范式，太 NB 了。做一张主题卡片。（2020-10-06）』——已完成

### 0104. 主题卡——处理选择集的操作函数

Selection sets are groups of one or more selected objects (entities). You can interactively add objects to, remove objects from, or list objects in a selection set. The following example code uses the ssget function to return a selection set containing all the objects in a drawing.

```c
(ssget "X")
```

AutoLISP provides a number of functions for handling selection sets. The following lists some of the functions available for working with selection sets: 

1. ssget - Prompts the user to select objects (entities), and returns a selection set; 

2. ssadd - Adds an object (entity) to a selection set, or creates a new selection set; 

3. ssdel - Removes an object (entity) from a selection set; 

4. ssname - Returns the object (entity) name of the indexed element of a selection set; 

5. sslength - Returns an integer containing the number of objects (entities) in a selection set.

1『获得选择集之后，需要靠 ssname，比如获取块选择集里第一个块的实体信息：`(setq ent (entget (ssname ss 0)))`。』

The ssget function provides the most general means of creating a selection set. It can create a selection set in one of the following ways: 1) Explicitly specifying the objects to select, using the Last, Previous, Window, Implied, Window Polygon, Crossing, Crossing Polygon, or Fence options; 2) Specifying a single point; 3) Selecting all objects in the database; 4) Prompting the user to select objects. With any option, you can use filtering to specify a list of properties and conditions that the selected objects must match.

### 0105. 主题卡——修改 CAD 实体数据的基本思路

### 0106. 主题卡——list 映射处理的几个函数

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
0
(10 20 -30 51.0)
```

[mapcar (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-8802AE73-1A05-457E-8A51-09677C23E26E)

Returns a list that is the result of executing a function with a list (or lists) supplied as arguments to the function.

```
(mapcar function list1... listn)
```

function. Type: Subroutine. A function.

list1... listn. Type: List. One or more lists. The number of lists must match the number of arguments required by function.

Return Values. Type: List. A list.

```
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

Further Reading

If this tutorial has sparked your interest in all things mapcar and lambda, the following publication from the Autodesk University written by Darren Young also provides an outline of mapcar, lambda and the apply function: LISP: Advance Yourself Beyond A Casual Programmer.

1-2『感觉又捡到金子了，已下载「附件1-CP401-1-Lisp-Advance-Yourself」作为本书的附件。』

### 0201. 术语卡——DXF group codes

CAD 里实体对象的唯一标识。重新打开文件，里面实体的名称会变，但它的 handle 是不会变的，是唯一的；一个实体的 handle，其 Group Code 为 5；handent 函数，通过传入实体的 handent 来获得实体的名称。

The DXF Reference describes the drawing interchange format (DXF™) and the DXF group codes that identify attributes of AutoCAD objects. You might need to refer to the DXF Reference when working with association lists describing entity data. 

### 0202. 术语卡——Entity Names

An entity name is a numeric label assigned to objects in a drawing. It is actually a pointer into a file maintained by AutoCAD, and can be used to find the object's database record and its vectors (if they are displayed). This label can be referenced by AutoLISP functions to allow selection of objects for processing in various ways. Internally, AutoCAD refers to objects as entities.

Note: You can use the vlax-ename->vla-object function to convert an entity name to a VLA-object when working with ActiveX functions. The vlax-vla-object->ename function converts a VLA-object to an entity name. The following functions are useful when working with entity names: 1) entget - Retrieves an object's (entity's) definition data. 2) entlast - Returns the name of the last non-deleted main object (entity) in the drawing. 3) ssname - Returns the object (entity) name of the indexed element of a selection set. 4) entsel - Prompts the user to select a single object (entity) by specifying a point. 5) nentsel - Prompts the user to select an object (entity) by specifying a point, and provides access to the definition data contained within a complex object. 6) nentselp - Provides similar functionality to that of the nentsel function without the need for user input. 7) handent - Returns an object (entity) name based on its handle.

Entity names assigned to objects in a drawing are only in effect during the current editing session. The next time you open the drawing, AutoCAD assigns new entity names to the objects. You can use an object's handle to refer to it from one editing session to another.

1『实体名重新打开图纸会刷新掉，handle 则不会。』

Objects in a drawing can be represented as ActiveX (VLA) objects. When working with ActiveX methods and properties, you must refer to VLA-objects, not the ename pointer returned by functions such as entlast. VLA-objects can be converted to an ename pointer with vlax-vla-object->ename. You can also use vlax-ename->vla-object to convert an ename pointer to a VLA-object.

### 0203. 术语卡——cons 函数

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

替换块内某一个属性值的源码里有一片段，这里的 cons 形成的就是一个 dotted pair。3.8.2 小结里有 dotted pair 的相关知识。（2020-10-06）——做一张术语卡片——已完成

```c
(setq a (cons 1 "17.03.10"))
(setq b (assoc 1 entx))
(entmod (subst a b entx))
```

[列表构造函数 - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/%E5%88%97%E8%A1%A8%E6%A7%8B%E9%80%A0%E5%87%BD%E6%95%B8)

列表构造函数是用来构造列表的基本函数，在大多数 LISP 体系的计算机编程语言中，使用的函数名称是 cons。cons 构成了存放两个变量与其指针的内存物件，这个物件被称为 CONS 单元、非原子的 S 表达式或 cons 对。LISP 编程中表达要把 x 加入 y 的语法：(cons x y)，构造了一个新物件。产生的结果具备了左半部，称为 CAR（第一元素或暂存器位址的内容）；以及右半部称为 CDR（其余元素或递减暂存器的内容）。

以上约略与面向对象的构造器概念相关，即产生一个给定参数的新物件，而其与代数数据类型系统的构造函数，更密切相关。「cons」和诸如「cons onto」的词句，也是函数编程的通用术语。有时运算子有类似作用，特别是在列表处理的情况下，被读作「CONS」。（例如 ML，Scala，F＃和 Elm 编程的：运算符，或 Haskell 编程的：运算符，都是向列表的开头添加一个元素。）

使用。虽然 cons 单元可用于储存有序的数据对，但它们更常用于组合为更复杂的复合数据结构，特别是列表和二叉树；有序对。例如 LISP 表达式 (cons 1 2) 产生一个有序的单元，在左半部存放 1，而右半部存放 2。左右次序不能互换（`(1 2)` 跟 `(2 1)` 不同）。在 LISP 表示法中，(cons 1 2) 结果会印出如下。须注意 1 和 2 之间的句点；这个 S 表达式是特殊的「点对」（所谓的 cons 对），并不是普通的「列表」。

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

LISP 编程中的列表实作在「cons 对」之上。具体地说，每个列表的结构都是：一个空列表 ()，通常被称为 nil 的特殊物件；一个 cons 单元，car 代表这列表的第一个元素，而 cdr 则是包含其余元素的一个子列表。这形成了简单基本的列表，而 cons，car 和 cdr 函数可以操作列表的内容。注意，nil 是个特殊的空列表，并不是「cons 对」。考虑元素为 1,2 和 3 的列表为例。这样的列表经由三个步骤产生：CONS 3 到 nil 空列表之上；CONS 2 到上一步的结果之上；CONS 1 到上一步的结果，产生最后的结果。这相当于单一表达式：

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

### 0204. 术语卡——dotted pair

Dotted pair lists must always contain two members and is the method AutoLISP uses to maintain entity definition data. When representing a dotted pair, members of the list are separated by a period ( . ). Most list-handling functions do not accept a dotted pair as an argument, so you should be sure you are passing the right kind of list to a function.

Dotted pairs are an example of an "improper list." An improper list is one in which the last cdr is not nil. In addition to adding an item to the beginning of a list, the cons function can create a dotted pair. If the second argument to the cons function is anything other than another list or nil, it creates a dotted pair.

```c
(setq sublist (cons 'lyr "WALLS"))
// out
(LYR . "WALLS")
```

The following functions are useful for handling dotted pairs:

1. car - Returns the first member of the specified dotted pair.

2. cdr - Returns the second member of the specified dotted pair.

3. assoc - Searches an association list for a member and returns that association list entry.

4. nth - Returns the nth element of a list.

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

醍醐灌顶。dotted pairs 就是 lisp 语言里的对象、「键-值」对、字典，哈哈。通过 assoc 函数可以提前特定「键」的值，这么一来，批量替换块内某一属性那边的源码片段渐渐看明白了。（2020-10-06）

```c
(setq a (cons 1 "17.03.10"))
(setq b (assoc 1 entx))
(entmod (subst a b entx))
```

autolisp 里一个高频操作 `cdr (assoc -1 ent)`，其中 -1 是 DXF group codes，表示 entity name，ent 是通过实体名获取的实体数据列表。

』

### 0205. 术语卡——Wild-Card Matching

通配符的使用说明：

1、`*` 相当于任意数量的任意字符。比如：1） `VT*` 会匹配到任意以 VT 开头的管道；2）`VT-25-*` 会匹配任意管径为 25 的管道。3）`VT*-50-*2J1*` 会匹配任意管径为 50 的、等级号为 2J1 的管道。等等。

2、`[]` 范围描述符。1）`[a-z]` 表示从 a 到 z 之间的任意一个。2）`[1-6]` 表示 1 到 6 之间的任意数据。

3、`?` 会相当于任何一个字符。

A string can be compared to a wild-card pattern with the wcmatch function. This can be helpful when needing to build a dynamic selection set (in conjunction with ssget) or to retrieve extended entity data by application name (in conjunction with entget). The wcmatch function compares a single string to a pattern. The function returns T if the string matches the pattern, and nil if it does not. The wild-card patterns are similar to the regular expressions used by many system and application programs.

1-2『直觉这里又是一个关键点。讲的应该就是通配符的知识点。回复：通配符与选择集（ssget）配合构建动态选择集，还可以与 entget 配合，结合实体名筛选。其实跟正则的功能差不多。回复：通配符的用处实在太大了，数据流开发中，批量修改块内某一属性前，要做的过滤功能可以通过这个来实现。（2020-10-06）做一张术语卡片。』——已完成

The following rules apply to wild-card patterns:

1. Alphabetic characters and numerals are treated literally in the pattern.

2. Brackets can be used to specify optional characters or a range of letters or digits.

3. A question mark ( ? ) matches a single character.

4. An asterisk ( * ) matches a sequence of characters; and, certain other special characters have special meanings within the pattern. When you use the * character at the beginning and end of the search pattern, you can locate the desired portion anywhere in the string.

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

About Wild-Card Patterns in Selection Set Filter Lists (AutoLISP). Symbol names specified in filtering lists can include wild-card patterns. The wild-card patterns recognized by ssget are the same as those recognized by the wcmatch function. When filtering for anonymous blocks, you must precede the * character with a reverse single quotation mark ( ` ), also known as an escape character, because the * is read by ssget as a wild-card character. For example, you can retrieve an anonymous block named *U2 with the following:

```c
(ssget "X" '((2 . "`*U2")))
```

1-2『选择特定名称块的实现方式，mark 一下。可以用来提取块里的基本信息用，做设备表的一个环节。wild-card 是指通配符。\` 应该是转义用的。回复：很棒啊，这样的话数据流里筛选仪表块只需要使用 `"Instrument*"` 过滤即可。合并到之前已经做好的通配符术语卡片。（2020-10-07）』

### 0206. 术语卡——lisp 里的函数

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

1『这种代码定义出的命令跟我之前想的有出入，只能在源码里调用，在 CAD 里的话必须使用命令：(DONE)；正巧发现，lisp 的函数名是不分大小写的，用命令 (done) 也可以跑。』

Note how the previous example invokes the princ function without an argument to suppress an ending nil and achieves a quiet exit.

1『正巧弄明白了为什么语句最后要加 (princ)，是为了消除字符串尾部的「nil」，否则显示出来的尾部就是 bye!nil 了。』

Functions that accept no arguments may seem useless. However, you might use this type of function to query the state of certain system variables or conditions and to return a value that indicates those values.

1-2『这应该也是个关键点。回复：上面的信息直觉上很有用，但目前还是没看懂。lisp 里的函数做一张术语卡片。（2020-10-06）』——已完成

If an AutoLISP function is defined with a name of the form C:xxx, it can be issued at the AutoCAD Command prompt in the same manner as a built-in AutoCAD command. This is true regardless of whether you define and load the function in VLISP or at the AutoCAD Command prompt. You can use this feature to add new commands to AutoCAD or to redefine existing commands.

1『解答了前面的疑问。这样的话就可以在 CAD 里跟常规命令一样使用了。』

To use functions as AutoCAD commands, be sure they adhere to the following rules:

1. The function name must use the form C:xxx (upper- or lowercase characters). The C: portion of the name must always be present; the XXX portion is a command name of your choice. C:xxx functions can be used to override built-in AutoCAD commands. (See About Redefining AutoCAD Commands [AutoLISP].)

2. The function must be defined with no arguments. However, local variables are permitted and it is a good programming practice to use them.

1『不能有参数，但可以使用局部变量。』

### 0301. 任意卡——MNL 源文件

AutoLISP source code can also be stored in files with a .mnl extension. A Menu AutoLISP (MNL) file contains custom functions and commands that are required for the elements defined in a customization (CUIx) file. A MNL file is loaded automatically when it has the same name as a customization (CUIx) file that is loaded into the AutoCAD-based product.

1-2『 MNL 应该就是可以显示的自定义菜单，后面需要自己实现的。（2020-07-02）回复：数据流实现了菜单，新建了一个 dataflow.cuix 文件，使用的过程中自动生成了一个 dataflow.mnr 文件。受这里的信息启发，D 盘下的 dataflowcad 文件夹里，把原来的 lsp 文件更改为 dataflow.mnl，这样的话 cuix 文件底下的不用手动加载 lsp 文件了，经验证，可行，哈哈。做一张任意卡片。（2020-10-06）』

For example, on Windows, when acad.cuix is loaded, the file named acad.mnl is also loaded if it is found in one of the folders listed as part of the AutoCAD Support File Search Path. If a CUIx file does not have a corresponding MNL file, no error is displayed, the product just moves and loading other support files.

### 0302. 任意卡——quote (‘) 与使用 list 函数创建 list 数据的区别

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

The quote and (‘) functions cannot be used to create a list using values that are stored in a variable. The following code does not return the excepted results:

```c
(setq abc 3.45)
// out
3.45

(setq pt4 (quote abc 1.23))
// out
; error: syntax error
```

1-2『这里终于弄明白 quote (‘) 与使用 list 的区别，简化函数是有条件的，只能是常数，而不能传入变量。做一张任意卡片。』——已完成

### 0303. 任意卡——获取实体类型（entity type）

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

### 0304. 任意卡——Relational Tests in Filter Lists

About Relational Tests in Filter Lists for Selection Sets (AutoLISP). Unless otherwise specified, an equivalency is implied for each item in the filter-list. For numeric group codes (integers, reals, points, and vectors), you can specify other relations by including a special -4 group code that specifies a relational operator. The value of a -4 group code is a string indicating the test operator to be applied to the next group in the filter-list. The following selects all circles with a radius (group code 40) greater than or equal to 2.0:

```c
(ssget "X" '((0 . "CIRCLE") (-4 . ">=") (40 . 2.0)))
```

3『 group code 0, Text string indicating the entity type (fixed); group code -4, APP: conditional operator (used only with ssget); group code 40, Floating-point values. (text height, scale factors, and so on)』

1-2『这个过滤集中增加条件语句实在是赞，`(-4 . ">=")`。Relational Tests in Filter Lists 做一张任意卡片。（2020-10-07）』

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

### 0305. 任意卡——autolisp 中的逻辑判断

AND returns true if all arguments are true.

OR returns true if any of the arguments are true.

NOT returns true if it's argument is false and returns false if it's argument is true. Let's look at some.

### 0306. 任意卡——handle 与实体名之间的切换

直接在 CAD 里用 `list` 命令选中一个实体，在显示的信息里，句柄即为 handle。

1、通过实体名获取实体的 handle：借用任意卡 0303 里的信息，可以直接获取一个实体的数据信息，举个例子，里面的 `(5 . "59DAA")` 这个即为 handle。那么获取这个数据的办法就显而易见了，跟获取它的坐标 `(10 xx yy)`，图层 `(0 . "0")`，块名称 `(2 . "PipeArrowLeft")` 等等的信息一模一样。

```
(cdr (assoc 5 (entget ename)))
```

2、通过 handle 获取实体名。

```
(setq ename (handent "5a2"))
```


## 实战经验汇总

### 01. 函数返回值的问题

场景：获取仪表、设备、管道等选择集的时候想把这些选择集封装在一起，通过传入一个参数来返回特定的选择集。结果发现多个 if 语句后，导致一直返回 nil。

解决方法：印象中是在书籍里「2019116AutoCAD-Platform-CustomizationR00」里看到过，可以人为的设置一个变量作为该函数的返回值。一个小插曲，开始的时候把该变量放在每个 if 语句内的，发现无效，还是要拿到 if 语句之外来。

```c
; get the select set
(defun GetBlockSS (blockSSName / ss)
  ; need to refactor
  (if (= blockSSName "Pipe")
    (progn
      (setq ss (ssget '((0 . "INSERT") 
            (-4 . "<OR")
              (2 . "PipeArrowLeft")
              (2 . "PipeArrowUp")
            (-4 . "OR>")
          )
        )
      )
    )
  )
  (if (= blockSSName "Instrument")
    (progn
      (setq ss (ssget '((0 . "INSERT") 
            (-4 . "<OR")
              (2 . "InstrumentP")
              (2 . "InstrumentL")
            (-4 . "OR>")
          )
        )
      )
    )
  )
  ss
)
```

### 02. 弹窗里下拉列表的第一个默认值自动获取不了数据

场景：数据流开发时，发现弹窗里下拉列表的第一个默认值（流程图号），自动获取不了数据，必须切换到其他选项后再切换回来才行。

解决方法：发现 `list_box` 或者 `popup_list` 这两个 tile，默认值不做任何动作时，它就是返回 nil，目前不知道是啥原因。加了一个 if 语句，是 nil 的话人为返回第一个选项的值（即 `"0"`）。

```c
(defun modifyBlockProperty (tileName blockSSName / dcl_id property_name property_value status selectedName ss)
  (setq dcl_id (load_dialog (strcat "D:\\dataflowcad\\" "dataflow.dcl")))
  (if (not (new_dialog tileName dcl_id))
    (exit)
  )
  ; optional setting for the popup_list tile
  (set_tile "property_name" "0")
  ;the default value of input box
  (set_tile "property_value" "")
  (mode_tile "property_name" 2)
  (mode_tile "property_value" 2)
  (action_tile "property_name" "(setq property_name $value)")
  (action_tile "property_value" "(setq property_value $value)")
  ; the solution code for the bug
  (if (= nil property_name)
    (setq property_name "0")
  )

  (setq status (start_dialog))
  (unload_dialog dcl_id)
  
  (if (= status 1)
    (progn 
      (setq selectedName (GetPropertyName property_name blockSSName))
      (setq ss (GetBlockSS blockSSName))
      (ModifyPropertyValue ss selectedName property_value)
      (alert "更新数据成功")(princ)
    )
    ;(alert "取消选择")
  )
)
```

### 03. 选择集按坐标排序

[Sort Selectionset by X coord](https://forums.augi.com/showthread.php?137837-Sort-Selectionset-by-X-coord)

[Selection Set Processing | Lee Mac Programming](http://www.lee-mac.com/selsetprocessing.html)

1. Create list of enames.

2. (vl-sort lst (function (lambda (a b) (> (cadr (assoc 10 (entget a))) (cadr (assoc 10 (entget b)))))))

3. Create new selection set with ssadd.

4. Step (foreach) through sorted (#2) list and ssadd enames to newly created selection set.

Thanks for the direction, I'm still having issues though. Perhaps I'm not building my list properly, but for some reason the lambda function grabs the first item, then tries to grab the entire rest of the list as the second item, That obviously doesnt work, as it cant grab the entdata from a list of entities. How do you suggest creating the list, I know that there are multiple ways of doing it, I'm using (setq lst (list ss lst)) which based on my results isnt the proper way to do it.
here is the error I'm receiving

```c
; error: bad argument type: lentityp (nil)
```

Nevermind, I figured it out. I had to set each item as a list, then append my lists together. Works great!

```c
(setq ss (ssget '((0 . "TEXT") (8 . "C-ROAD-STAN-OFFS")))) ;_ select all objects
  (setvar "osmode" 64)
  (setq stp (getpoint "\nSelect insert point of first text obj")) ;_ select start point
  (setq    count1 (sslength ss)
    count  1
    xcoord (- (car stp) 0.135)
    ss1    (ssadd)
    ss4    (list (ssname ss (1- count)))
    ss6    (ssadd)
  ) ;_ end of setq
  (while (<= (1+ count) count1)        ;SORT LIST BY X COORD LOW TO HIGH
    (setq ss3 (list (ssname ss count)))
    (setq ss4 (append ss4 ss3))
    (setq count (1+ count))
  ) ;_ end of while
  (vl-sort ss4
       (function (lambda (a b) (> (cadr (assoc 11 (entget a))) (cadr (assoc 11 (entget b))))))
  ) ;_ end of vl-sort
  (setq    count 0
    counta 1
  ) ;_ end of setq
  (foreach ss5 (reverse ss4)
    (setq ss6 (ssadd ss5 ss6))
  )
```

I like to segregate the functionality of each step of the function so that I can build very general toolbox functions that allow me to make changes. Like here I convert a selection set to a list, change the list into a list of sublists ivgncluding the xyz coordinates of the entities, sort by the x y and z coordinates (either up or down), convert the list of sublists back to a list of entities and then into a selection set. I like the list of sublists structure and use this sort function all the time.I also like storing selections sets as lists of entities or objects.

```c
(defun sortListofSublistsbyItemX (lstOfSublists intItem intDirection)
 (if (> intDirection 0)
  (vl-sort lstOfSublists '(lambda (X Y) (< (nth intItem X) (nth intItem Y))))
  (vl-sort lstOfSublists '(lambda (X Y) (> (nth intItem X) (nth intItem Y))))
 )
)

(defun SelectionSetToList (ssSelections / intCount lstReturn)
 (if (and ssSelections 
          (= (type ssSelections) 'PICKSET)
     )
  (repeat (setq intCount (sslength ssSelections))
   (setq intCount  (1- intCount)
         lstReturn (cons (ssname ssSelections intCount) lstReturn)
   )
  )
 )
 (reverse lstReturn)
)

(defun ListToSelectionSet (lstOfEntities / ssReturn)
 (if lstOfEntities      
  (foreach entItem lstOfEntities
   (if (= (type entItem) 'ENAME)
    (if ssReturn 
     (setq ssReturn (ssadd entItem ssReturn))
     (setq ssReturn (ssadd entItem))
    )
   )
  )
 )
 ssReturn
)

(defun SortSelectionSetByXYZ (ssSelections /  lstOfSelections lstOfSublists lstSelections)
 (if
  (and 
   (setq lstSelections (SelectionSetToList ssSelections))
   (setq lstOfSublists (mapcar '(lambda (X)(cons X (cdr (assoc 10 (entget X))))) lstSelections))
   (setq lstOfSublists (sortlistofsublistsbyitemX lstOfSublists 3 1))
   (setq lstOfSublists (sortlistofsublistsbyitemX lstOfSublists 2 1))
   (setq lstOfSublists (sortlistofsublistsbyitemX lstOfSublists 1 1))
   (setq ssSelections  (listtoselectionset (mapcar 'car lstOfSublists)))
  )
  ssSelections
 )
)
```

## 函数库收集

### 01. 替换字符串

This subfunction will substitute all occurrences of a string for another string within a string. The functionality is similar to the Visual LISP vl-string-subst (and indeed uses this function), however, this subfunction performs a global replacement, hence all occurrences of the pattern string are replaced.

```c
;;--------------------=={ String Subst }==--------------------;;
;;                                                            ;;
;;  Substitutes a string for all occurrences of another       ;;
;;  string within a string.                                   ;;
;;------------------------------------------------------------;;
;;  Author: Lee Mac, Copyright © 2011 - www.lee-mac.com       ;;
;;------------------------------------------------------------;;
;;  Arguments:                                                ;;
;;  new - string to be substituted for 'old'                  ;;
;;  old - string to be replaced                               ;;
;;  str - the string to be searched                           ;;
;;------------------------------------------------------------;;
;;  Returns:  String with 'old' replaced with 'new'           ;;
;;------------------------------------------------------------;;

(defun StringSubst (new old str / inc len)
    (setq len (strlen new)
          inc 0
    )
    (while (setq inc (vl-string-search old str inc))
        (setq str (vl-string-subst new old str inc)
              inc (+ inc len)
        )
    )
    str
)
```

1『代码里 `inc (+ inc len)` 是有讲究的，替换一次后，往后移动一个步长 `strlen new` 是明智的。哈哈。（2020-10-12）』

## 细节汇总

1、if 判断，结果为真后的语句有多个，经常忘记写 `progn` 语句。

## 搭建测试框架的记录

找到一个 autolisp 大牛的相关资料：

[jdsandifer/ALUnit: The only unit testing framework for AutoLISP available on GitHub (as of its publication).](https://github.com/jdsandifer/ALUnit)

[jdsandifer/AutoLISP: Programs written to help drafters work faster and automate common tasks in AutoCAD. (Professional Experience)](https://github.com/jdsandifer/AutoLISP)

[jdsandifer/Reading-List: See if I've read your favorite software development book or get ideas for your next read!](https://github.com/jdsandifer/Reading-List)

fork 了他 2 个仓库，里面的代码值得仔细研读，感觉是个宝藏。

### 2020-10-24

直接用成品「ALUnit」一直没有跑通。幸好在作者的第二个项目仓库「jdsandifer/AutoLISP」里看到一个「TEST.lsp」文件，直接借鉴里面的代码。但作者的 `DL:CountBooleans` 有问题，自己重写后跑通了基本测试。同时把失败案例的提示单独拎出来了。

### 2020-10-26

遇到的一个问题：断言的传参列表里如果还嵌入列表，就有报错。

比如 `(AssertEqual 'GetIndexforSearchMemberInListUtils (list "PL1101" (list "PL1101" "PL1102")) 0)` 报错：`函数错误："PL1101"`。如果改成 `(AssertEqual 'GetIndexforSearchMemberInListUtils '("PL1101" '("PL1101" "PL1102")) 0)`，跑测试后会出现 `failed...return nil instead of 1` 信息，还是报错 `错误：参数类型错误`。

早上看成品「ALUnit」里「Assert.lsp」的代码，发现一个关键信息：作者用 `vl-catch-all-apply` 取代了原来的 `eval` 函数，原来测试代码里最关键的语句就是：

```c
(equal (setq actualReturn (eval (cons functionName argumentList)))
			  expectedReturn)
```

作者替换成了：

```c
(equal (setq actualReturn (vl-catch-all-apply functionName argumentList))
			  expectedReturn)
```

接着去官方文档了解了下该函数：[vl-catch-all-apply (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-E08CC2A6-787A-422F-8BD3-18812996794C)。

Passes a list of arguments to a specified function and traps any exceptions.

```c
(vl-catch-all-apply 'function list)
```

'function. Type: Symbol. A function. The function argument can be either a symbol identifying a defun or lambda expression.

list. Type: List. A list containing arguments to be passed to the function.

Return Values. Type: Integer, Real, String, List, Ename (entity name), T, nil, or catch-all-apply-error.

The result of the function call, if successful. If an error occurs, vl-catch-all-apply returns an error object.

Examples:

If the function invoked by vl-catch-all-apply completes successfully, it is the same as using apply, as the following examples show:

```c
(setq catchit (apply '/ '(50 5)))
10

(setq catchit (vl-catch-all-apply '/ '(50 5)))
10
```

The benefit of using vl-catch-all-apply is that it allows you to intercept errors and continue processing. See what happens when you try to divide by zero using apply:

```c
(setq catchit (apply '/ '(50 0)))
; error: divide by zero
```

When you use apply, an exception occurs and an error message displays. Here is the same operation using vl-catch-all-apply:

```c
(setq catchit (vl-catch-all-apply '/ '(50 0)))
#<%catch-all-apply-error%>
```

The vl-catch-all-apply function traps the error and returns an error object. Use vl-catch-all-error-message to see the error message contained in the error object:

```c
(vl-catch-all-error-message catchit)
"divide by zero"
```

1『看到这里基本上也理解了 `apply` 函数的用法，哈哈。（2020-10-26）』

测试框架里用 `vl-catch-all-apply` 重构后，再使用 `(AssertEqual 'GetIndexforSearchMemberInListUtils (list "PL1101" (list "PL1101" "PL1102")) 0)` 跑测试就 OK 了。

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

1. AutoCAD ActiveX Reference and Developer's Guides contain information on accessing ActiveX methods, properties, objects, and events. If you develop AutoLISP applications that use ActiveX automation to reference AutoCAD objects, you will need to refer to these guides. The help files can be accessed from %ProgramFiles%\Common Files\Autodesk Shared. (AutoCAD for Mac does not support ActiveX)
AutoCAD Customization topics contain basic information on creating and modifying customizable files. For example, they include information on customizing the user interface, and creating custom linetypes and hatch patterns. These topics can be found in the AutoCAD product help.

2. The DXF Reference describes the drawing interchange format (DXF™) and the DXF group codes that identify attributes of AutoCAD objects. You might need to refer to the DXF Reference when working with association lists describing entity data. The DXF Reference is available through the AutoCAD product help or the Autodesk website (www.autodesk.com/dxf).

4. The ObjectARX Reference and Developer's Guides contain information on using ObjectARX® to develop custom AutoCAD applications. AutoCAD reactor functionality is implemented through ObjectARX. If you develop AutoLISP applications that implement reactor functions, you may want to refer to the ObjectARX Reference . The ObjectARX Reference and Developer's Guides are not installed with the AutoCAD program. To obtain this documentation, download the ObjectARX SDK (Software Development Kit) from the www.autodesk.com/objectarx.

5. The Managed .NET Reference and Developer's Guides contain information on using the Managed .NET API to develop custom AutoCAD applications. The Managed .NET Reference is not installed with the AutoCAD program. To obtain this documentation, download the ObjectARX SDK (Software Development Kit) from the www.autodesk.com/objectarx. The Managed .NET Developer's Guide is available from the AutoCAD product help. (AutoCAD for Mac does not support Managed .NET development)

2『hatch patterns 的概念；DXF group codes 的概念做一张术语卡片；已下载书籍「2020038dxf_reference2012」。』——已完成

3『

[Free AutoCAD Hatch Patterns | CADHatch](http://www.cadhatch.com/)

[DXF Group Codes | AfraLISP](https://www.afralisp.net/reference/dxf-group-codes.php)

』

1『原文中有各版本的主要更新信息。』

## 0102. About Namespaces (AutoLISP)

[Pomoc: Introduction (AutoLISP)](http://help.autodesk.com/view/OARX/2018/PLK/?guid=GUID-A0E9D801-8BE9-4BF1-85E8-3807E15F3B71)

A namespace is a LISP environment containing a set of symbols (for example, variables and functions).

The concept of namespaces was introduced to prevent applications running in one drawing window from unintentionally affecting applications running in other windows. Each open AutoCAD drawing document has its own namespace. Variables and functions defined in one document namespace are isolated from variables and functions defined in other namespaces.

### 2.1 About Referencing Variables in Document Namespaces (AutoLISP)

Variables defined in a separate-namespace VLX are not known to the document namespace associated with the VLX. However, a separate-namespace VLX can access variables defined in a document namespace using the vl-doc-ref and vl-doc-set functions. The vl-doc-set function is the same as using the setq function.

The vl-doc-ref function copies the value of a variable from a document namespace. The function requires a single argument, a symbol identifying the variable to be copied. For example, the following copies the value of a variable named aruhu:

```
(vl-doc-ref 'aruhu)
```

If executed within a document namespace, vl-doc-ref is equivalent to the eval function. The vl-doc-set function sets the value of a variable in a document namespace. The function requires two arguments: a symbol identifying the variable to be set, and the value to set for the variable. For example, the following sets the value of a variable named ulus:

```
(vl-doc-set 'ulus "Go boldly to noone")
```

If executed within a document namespace, vl-doc-set is equivalent to the setq function. Use the vl-propagate function to set the value of a variable in all open document namespaces. For example, the following sets a variable named fooyall in all open document namespaces:

```
(setq fooyall "Go boldly and carry a soft stick")

(vl-propagate 'fooyall)
```

1『确实，使用函数 vl-propagate 后，变量在任何打开的图纸里都能够访问了。（2020-10-06）』

The vl-propagate function not only copies the value of fooyall into all currently open document namespaces, but also causes fooyall to automatically be copied to the namespace of any new drawings opened during the current AutoCAD session.

To set and retrieve variables from a document namespace (AutoLISP). Values can be stored and retrieved from AutoLISP variables while a drawing remains open. At the AutoCAD Command prompt or in an AutoLISP program, enter an AutoLISP statement that uses the setq function and press Enter. Enter the name of the variable you assigned a value to and prefix it with an ! (exclamation point) to return the value assigned to the variable and press Enter.

1『

setq 是基本的赋值函数，可以赋，值、字符串等。获取变量的命令，前面要加个 ！。比如，在命令窗口里先给一个变量赋值，然后提取：

```
(setq foo "dalong")

// 提取变量
!foo
```

』

To set and retrieve variables in the blackboard namespace (AutoLISP). Variables can be stored and retrieved across multiple open drawings using the blackboard namespace. At the AutoCAD Command prompt or from an AutoLISP program, use the vl-bb-set function to set the value of a variable in the blackboard. Use the vl-bb-ref function to retrieve the value of a variable from the blackboard.

1『原文里有一个有关 vl-bb-set 函数的例子。』

The blackboard variable named \*example* is still set to the value assigned in Step 1; setting the document variable of the same name in Step 4 had no effect on the variable in the blackboard. You can also the vl-doc-set and vl-doc-ref functions to set and retrieve document namespace variables from a separate-namespace VLX, and vl-propagate to set the value of a variable in all open document namespaces.

### 2.3 To load functions across all document namespaces (AutoLISP)

Normally, loading an application file loads it in the current drawing only, but the vl-load-all function can be used to load a file in all drawings. At the AutoCAD Command prompt, enter an AutoLISP statement that uses the vl-load-all function and press Enter.

Note: The vl-load-all function is useful for testing new functions in multiple documents, but in general you should use acaddoc.lsp to load files that are needed in every document.

1. At the AutoCAD Command prompt, enter (load "yinyang.lsp") and press Enter.

2. Invoke a function defined in the AutoLISP source (LSP) file. The function should work as expected.

3. Create a new or open an existing drawing.

4. With the second drawing window active, try invoking the function again. The response will be an error message saying the function is not defined.

5. At the AutoCAD Command prompt, enter (vl-load-all "yinyang.lsp") and press Enter.

6. Create a new or open an existing drawing.

7. Invoke the function again. This time the function will work correctly because the vl-load-all function loads the contents of an AutoLISP file into all open documents, and into any documents opened later in the session.

1『

这个知识点很有用，我将公司的提取程序「line-index.lsp」和贱人工具「cad_tools.vlx」放到 D 根目录下。在 CAD 里输入加载命令：

```
(vl-load-all "D:line-index.lsp")
    
(vl-load-all "D:cad_tools.vlx")
```

加载完后，之后打开的程序这些插件都可以用。

』

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
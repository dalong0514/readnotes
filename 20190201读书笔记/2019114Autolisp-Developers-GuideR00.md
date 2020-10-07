# 2019114Autolisp-Developers-GuideR00

## 记忆时间

2020-10-06

## 资源汇总

[Pomoc: Introduction (AutoLISP)](http://help.autodesk.com/view/OARX/2018/PLK/?guid=GUID-A0E9D801-8BE9-4BF1-85E8-3807E15F3B71)

[Forums - AutoCAD Forums](https://www.cadtutor.net/forum/)

[Tutorials | Lee Mac Programming](http://lee-mac.com/tutorials.html)

[Free LISP Programs | Lee Mac Programming](http://lee-mac.com/programs.html)

[Dynamic Block Functions | Lee Mac Programming](http://lee-mac.com/dynamicblockfunctions.html)

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

### 0204. 术语卡——Wild-Card Matching

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

1-2『选择特定名称块的实现方式，mark 一下。可以用来提取块里的基本信息用，做设备表的一个环节。wild-card 是指通配符。\` 应该是转义用的。回复：很棒啊，这样的话数据流里筛选仪表块只需要使用 "Instrument`*" 过滤即可。合并到之前已经做好的通配符术语卡片。（2020-10-07）』

### 0205. 术语卡——lisp 里的函数

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

## 实战源码解析

### 01. 批量替换特定块内的某一属性值




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

## 0103. About AutoLISP Basics (AutoLISP)

You can use number, string, and list-handling functions to customize AutoCAD. The following links introduce the basic concepts of the AutoLISP ® programming language. It describes the core components and data types used in AutoLISP, and presents examples of simple number-, string-, output-, and list-handling functions. AutoLISP code does not need to be compiled, so you can enter the code at a Command line and immediately see the results.

### 3.1 About Expressions (AutoLISP)

An expression is the basic structure that is used when working with AutoLISP. AutoLISP expressions have the following form:

```
(function arguments)
```

1『典型的函数式编程。』

Each expression:

1. Begins with an open (left) parenthesis.

2. Consists of a function name and optional arguments for that function. Each argument can also be an expression.

3. Ends with a close (right) parenthesis.

4. Returns a value that can be used by a surrounding expression. The value of the last interpreted expression is returned to the calling expression.

For example, the following code example involves three functions:

```c
(fun1 (fun2 arguments)(fun3 arguments))
```

The first function, fun1, has two arguments, which in this example are expressions. The values returned by the expressions are used by fun1. The other functions, fun2 and fun3, each have one argument. AutoLISP evaluates the innermost expression first, working its way outward. For this example, expressions containing fun2 and fun3 are evaluated before fun1.

1『 AutoLISP 先执行最里层的表达式。』

The following example shows the use of the * (multiplication) function, which accepts one or more numbers as arguments:

```c
(* 2 27)

// out
54
```

Because this code example has no surrounding expression, AutoLISP returns the result to the window from which you entered the code. Expressions nested within other expressions return their result to the surrounding expression. The following example uses the result from the + (addition) function as one of the arguments for the * (multiplication) function.

```c
(* 2 (+ 5 10))

// out
30
```

In the previous example, (+ 5 10) returns a value of 15. After the innermost expression is evaluated, the AutoLISP interpreter sees the following:

```c
(* 2 15)

// out
30
```

1『有个技巧。现在 autolisp 编辑器里编写代码，点菜单里的「加载活动编辑窗口」，下面的控制台会出现该文件的路径。接着在 CAD 里的 command prompt 里输入加载该文件的命名：(load "D:/xx.lsp") 即可。』

#### Entering AutoLISP Expressions

AutoLISP expressions can be entered directly at the AutoCAD Command prompt, loaded with an AutoLISP source (LSP) file, or the Visual LISP Editor (Windows only). When you type an open (left) parenthesis, you indicate to AutoCAD that the following text should be passed to the AutoLISP interpreter for evaluation.

If you enter the incorrect number of close (right) parentheses, AutoLISP displays the following prompt:

```c
(_>
```

1『只要有开始符号 ( 就必定对应一个 ) 闭合符号，而且不写闭合符号的话在 command prompt 里命令就一直不会结束。』

The number of open parentheses in this prompt indicates how many levels of open parentheses remain unclosed. If this prompt appears, you must enter the required number of close parentheses for the expression to be evaluated.

```c
(* 2 (+ 5 10
((_> ) )

// out
30
```

A common mistake is to omit the closing quotation mark (") in a text string, in which case the close parentheses are interpreted as part of the string and have no effect in resolving the open parentheses. To correct this condition, press Shift+Esc to cancel the function, then re-enter it correctly.

### 3.2 About Function Syntax (AutoLISP)

Reference topics in the documentation use a consistent convention to describe the proper syntax for an AutoLISP function. The syntax used is as follows:

In this example, the foo function has one required argument, string of the string data type, and one or more optional arguments of numeric value for number. The number arguments can be of the integer or real data types. Frequently, the name of the argument indicates the expected data type. The examples in the following table show both valid and invalid calls to the foo function.

### 3.3 About Data Types (AutoLISP)

AutoLISP expressions are processed according to the order and data type of the code within the parentheses. Before you can fully utilize AutoLISP, you must understand the differences among the data types and how to use them.

#### 3.3.1 About Integers (AutoLISP)

Integers are whole numbers; numbers that do not contain a decimal point. AutoLISP integers are 32-bit signed numbers with values ranging from +2,147,483,647 to -2,147,483,648. Some functions through, only accept 16-bit numbers ranging from +32767 to -32678. When you explicitly use an integer, that value is known as a constant. Numbers such as 2, -56, and 1,200,196 are valid integers.

If you enter a number that is greater than the maximum integer allowed (resulting in integer overflow), AutoLISP converts the integer to a real number. However, if you perform an arithmetic operation on two valid integers, and the result is greater than the maximum allowable integer, the resulting number will be invalid.

The following examples demonstrate how AutoLISP handles integer overflow. The largest positive integer value retains its specified value:

```c
(setq int1 2147483647)

// out
2147483647
```

If you enter an integer that is greater than the largest allowable value, AutoLISP returns the value as a real:

```c
(setq int2 2147483648)

// out
2.14748e+009
```

An arithmetic operation involving two valid integers, but resulting in integer overflow, produces an invalid result:

```c
(setq int3 (+ 2147483646 3))

// out
-2147483647
```

In the previous example the result is clearly invalid, as the addition of two positive numbers results in a negative number. But note how the following operation produces a valid result:

```c
(setq int4 (+ 2147483648 2))

// out
2.14748e+009
```

In this instance, AutoLISP converts 2147483648 to a valid real before adding 2 to the number. The result is a valid real. The largest negative integer value retains its specified value:

```c
(setq int5 -2147483647)

// out
-2147483647
```

If you enter a negative integer larger than the greatest allowable negative value, AutoLISP returns the value as a real:

```c
(setq int6 -2147483648)

// out
-2.14748e+009
```

The following operation concludes successfully, because AutoLISP first converts the overflow negative integer to a valid real:

```c
(setq int7 (- -2147483648 1))

// out
-2.14748e+009
```

#### 3.3.2 About Reals (AutoLISP)

A real is a number containing a decimal point. Numbers between -1 and 1 must contain a leading zero. Real numbers are stored in double-precision floating-point format, providing at least 14 significant digits of precision. Note that AutoLISP does not show you all the significant digits.

Reals can be expressed in scientific notation, which has an optional e or E followed by the exponent of the number (for example, 0.0000041 is the same as 4.1e-6). Numbers such as 3.1, 0.23, -56.123, and 21,000,000.0 are all valid AutoLISP real numbers.

#### 3.3.3 About Strings (AutoLISP)

A string is a group of characters surrounded by quotation marks. Within quoted strings the backslash (\) character allows control characters (or escape codes) to be included. When you explicitly use a quoted string in an AutoLISP expression, that value is known as a literal string or a string constant. Examples of valid strings are “string 1” and “\nEnter first point:”.

#### 3.3.4 About Lists (AutoLISP)

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

1『以上都是一些常用的数组操作函数，牢记哦。』

#### 3.3.4.1 Creating a List

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

#### 3.3.4.2 Adding to or Changing an Item in a List

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

#### 3.3.4.3 Retrieving an Item from a List

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

#### 3.3.5 About Selection Sets (AutoLISP)

Selection sets are groups of one or more objects (entities). You can interactively add objects to, or remove objects from, selection sets with AutoLISP routines. The following example uses the ssget function to return a selection set containing all the objects in a drawing.

```c
(ssget "X")

// out
<Selection set: 1>
```

1『上面的命名目前没有弄清楚。回复：现在看这个命令很简单啊，ssget 函数，接受一个参数 "X" 表示返回一个包含当前图纸里所有实体的选择集。（2020-07-03）』

#### 3.3.6 About Entity Names (AutoLISP)

An entity name is a numeric label assigned to objects in a drawing. It is actually a pointer into a file maintained by AutoCAD, and can be used to find the object's database record and its vectors (if they are displayed). This label can be referenced by AutoLISP functions to allow selection of objects for processing in various ways. Internally, AutoCAD refers to objects as entities.

2『实体名（About Entity Names）做一张术语卡片。』

Note: You can use the vlax-ename->vla-object function to convert an entity name to a VLA-object when working with ActiveX functions. The vlax-vla-object->ename function converts a VLA-object to an entity name. The following functions are useful when working with entity names:

1. entget - Retrieves an object's (entity's) definition data.

2. entlast - Returns the name of the last non-deleted main object (entity) in the drawing.

3. ssname - Returns the object (entity) name of the indexed element of a selection set.

4. entsel - Prompts the user to select a single object (entity) by specifying a point.

5. nentsel - Prompts the user to select an object (entity) by specifying a point, and provides access to the definition data contained within a complex object.

6. nentselp - Provides similar functionality to that of the nentsel function without the need for user input.

7. handent - Returns an object (entity) name based on its handle.

The following example uses the entlast function to get the name of the last object created in the drawing.

```c
(entlast)

// out
<Entity name: 27f0540>
```

Entity names assigned to objects in a drawing are only in effect during the current editing session. The next time you open the drawing, AutoCAD assigns new entity names to the objects. You can use an object's handle to refer to it from one editing session to another.

1『实体名重新打开图纸会刷新掉，handle 则不会。』

#### 3.3.7 About VLA-objects (AutoLISP/ActiveX)

Objects in a drawing can be represented as ActiveX (VLA) objects. When working with ActiveX methods and properties, you must refer to VLA-objects, not the ename pointer returned by functions such as entlast. VLA-objects can be converted to an ename pointer with vlax-vla-object->ename. You can also use vlax-ename->vla-object to convert an ename pointer to a VLA-object.

Note: AutoCAD for Mac does not support ActiveX.

2『 VLA-object 的概念去多了解下。』

#### 3.3.8 About File Descriptors (AutoLISP)

A file descriptor is a pointer to a file opened by the AutoLISP open function. The open function returns this pointer as an alphanumeric label. You supply the file descriptor as an argument to other AutoLISP functions that read, write, or close the file.

You use the following functions when working with a file:

1. open - Opens a file for access by the AutoLISP I/O functions.

2. write-line - Writes a string to the screen or to an open file.

3. write-char - Writes one character to the screen or to an open file.

4. read-line - Reads a string from the keyboard or from an open file, until an end-of-line marker is encountered.

5. read-char - Returns the decimal ASCII code representing the character read from the keyboard input buffer or from an open file.

6. print – Prints an expression to the command line or writes an expression to an open file.

7. prin1 – Prints an expression to the command line or writes an expression to an open file.

8. close – Closes a file opened with the open function.

1『

要实现读写数据就得靠上面的这些函数，读取块属性里的实现肯定得结合这些。实现写数据方法：[Pomoc: write-line (AutoLISP)](http://help.autodesk.com/view/OARX/2018/PLK/?guid=GUID-CB4F3ABC-F0F6-41DA-A911-75B90D9F974A)

```c
# open a file first
(setq f (open "d:\\test.txt" "w"))
(write-line "dalong" f)
# close the file
(close file)
```

回复：数据流开发直接用 princ 函数写数据进文件，比如 `(princ propertyValue f)`。（2020-10-06）


』

The following example opens the myinfo.dat file for reading. The open function returns a file descriptor which is stored in the file1 variable:

```c
(setq file1 (open "c:\\myinfo.dat" "r"))
#<file "c:\\myinfo.dat">
```

Files remain open until you explicitly close them in your AutoLISP program. The close function closes a file. The following code closes the file whose file descriptor is stored in the file1 variable:

```c
(close file1)
// out
nil
```

1『果然所有语言都是一个套路，打开文件记得关掉。』

### 3.4 About Source Code Files (AutoLISP)

Although you can enter AutoLISP code at the AutoCAD Command prompt or Visual LISP Console window prompt (Windows only), any functions you define are lost when you close the drawing or session they were created in. AutoLISP source code can be saved to an ASCII text file with a .lsp extension. Saving AutoLISP source code to a file has the following advantages: 1) Programs are not lost when the drawing they are defined in is closed. 2) Programs can be used in more than one drawing and can be executed on multiple machines. 3) Programs can be shared with others in your organization. 4) Testing and debugging multiple expressions is considerably easier.

AutoLISP source code can also be stored in files with a .mnl extension. A Menu AutoLISP (MNL) file contains custom functions and commands that are required for the elements defined in a customization (CUIx) file. A MNL file is loaded automatically when it has the same name as a customization (CUIx) file that is loaded into the AutoCAD-based product.

1-2『 MNL 应该就是可以显示的自定义菜单，后面需要自己实现的。（2020-07-02）回复：数据流实现了菜单，新建了一个 dataflow.cuix 文件，使用的过程中自动生成了一个 dataflow.mnr 文件。受这里的信息启发，D 盘下的 dataflowcad 文件夹里，把原来的 lsp 文件更改为 dataflow.mnl，这样的话 cuix 文件底下的不用手动加载 lsp 文件了，经验证，可行，哈哈。做一张任意卡片。（2020-10-06）』——已完成

For example, on Windows, when acad.cuix is loaded, the file named acad.mnl is also loaded if it is found in one of the folders listed as part of the AutoCAD Support File Search Path. If a CUIx file does not have a corresponding MNL file, no error is displayed, the product just moves and loading other support files.

Note: While AutoLISP source code is commonly saved in files with a .lsp or .mnl extension, AutoLISP code can be loaded from any ASCII text file.

#### Topics in this section

1. About Formatting and Spaces in Code (AutoLISP). AutoLISP code can span multiple lines, and contain empty lines and extra spaces. Empty lines and extra spaces do not have any significant meaning, but can make your code easier to read.

2. About Comments in AutoLISP Program Files (AutoLISP). Comments are useful to both the programmer and future users who may need to revise a program to suit their needs.

3. To Create and Open AutoLISP Source Code Files (AutoLISP). AutoLISP source code files can be created and edited using a plain ASCII text editor.

#### 3.4.1 About Formatting and Spaces in Code (AutoLISP)

AutoLISP code can span multiple lines, and contain empty lines and extra spaces. Empty lines and extra spaces do not have any significant meaning, but can make your code easier to read. Multiple spaces between function and variable names, and constants are equivalent to a single space. The end of a line and tab is also treated as a single space. The following two expressions produce the same result:

```c
(setq test1 123 test2 456)

(setq
  test1 123
  test2 456
)
```

The extensive use of parentheses in AutoLISP code can make it difficult to read. The traditional techniques for combatting this confusion is indentation, and to align the open and close parentheses of a function. The more deeply nested a line of code is, the farther to the right the line is positioned. The following two functions are the same code, but the second one is much easier to read and determine visually if the parentheses of the AutoLISP expressions are balanced.

```c
(defun c:mycmd ()
(setq old_clayer (getvar "clayer"))
(setq insPt (getpoint "\nSpecify text insertion: "))
(if (/= insPt nil)
(progn
(command "_.UNDO" "_BE")
(command "._-LAYER" "_M" "Text" "_C" "3" "" "")
(command "_.-TEXT" insPt "" "0" "Sample Text")
(command "_.UNDO" "_E")))
(setvar "clayer" old_clayer)
(princ)
)

(defun c:mycmd ()
  (setq old_clayer (getvar "clayer"))

  (setq insPt (getpoint "\nSpecify text insertion: "))

  (if (/= insPt nil)
    (progn
      (command "_.UNDO" "_BE")
      (command "._-LAYER" "_M" "Text" "_C" "3" "" "")
      (command "_.-TEXT" insPt "" "0" "Sample Text")
      (command "_.UNDO" "_E")
    )
  )

  (setvar "clayer" old_clayer)
 (princ)
)
```

1『上面的例子值得好好吸收消化。回复：这原来是一个插入单行文本的代码，借鉴过来开发插入「块」的功能，哈哈。（2020-10-06）』

#### 3.4.2 About Comments in AutoLISP Program Files (AutoLISP)

Comments are useful to both the programmer and future users who may need to revise a program to suit their needs. It is good coding practice to include comments in all AutoLISP program files, small and large. Use comments to do the following: 1) Give a title, authorship, and creation date. 2) Provide instructions on using a routine. 3) Make explanatory notes throughout the body of a routine. 4) Make notes to yourself during debugging.

Comments begin with one or more semicolons ( ; ) and continue through the end of the line.

```c
; This entire line is a comment
(setq area (* pi r r)) ; Compute area of circle
```

Any text within ;| ... |; is ignored. Therefore, comments can be included within a line of code or extend for multiple lines. This type of comment is known as an in-line comment.

```c
(setq tmode ;|some note here|; (getvar "tilemode"))
```

The following example shows a comment that continues across multiple lines:

```c
(setvar "orthomode" 1) ;|comment starts here
and continues to this line,
but ends way down here|; (princ "\nORTHOMODE set On.")
```

#### 3.4.3 To Create and Open AutoLISP Source Code Files (AutoLISP)

AutoLISP source code files can be created and edited using a plain ASCII text editor.

### 3.5 About Variables (AutoLISP)

Variables are used to store a value or list of values in memory. The data type of a variable is determined when a value is assigned. Variables retain their value until a new value is assigned or the variable goes out of scope. The scope of a variable can either be global or local. Global variables are accessible by any AutoLISP program that is loaded into a drawing, while local variables are only available within a specific function or command. You use the AutoLISP setq function to assign values to variables. The syntax of the setq function is as follows:

```c
(setq variable_name1 value1 [variable_name2 value2 ...])
```

The setq function assigns the specified value to the variable name given, and returns the last assigned value as its function result. The following example creates two variables: val and abc. val is assigned the value of 3, while abc is assigned the value of 3.875.

```c
(setq val 3 abc 3.875)

// out
3.875
```

The following example creates a variable named layr and assigns it the value of “EXTERIOR-WALLS”.

```
(setq layr "EXTERIOR-WALLS")

// out
"EXTERIOR-WALLS"
```

#### Using a Variable with a Function

Once a value is assigned to a variable, it can be used in an expression as the value for an argument of a function. The following uses two of the previously created variables in a few AutoLISP expressions to create a layer and draw a line with a specific length at 0 degrees.

```c
(command "_.-layer" "_make" layr "")
(command "_.line" PAUSE (strcat "@" (itoa val) "<0") "")
```

#### Checking the Value of a Variable

You can use the following methods to determine the current value of a variable:

At the AutoCAD Command prompt, add an ! (exclamation point) in front of the variable and press Enter.

```c
(setq val 3 abc 3.875)
// out
3.875

!val
// out
3
```

At the Visual LISP Console Window prompt, enter the name of the variable and press Enter. (Windows only).

```c
_$ (setq val 3 abc 3.875)
// out
3.875

_$ val
// out
3
```

At the AutoCAD Command prompt or Visual LISP Console Window prompt (Windows only), or in an AutoLISP program, create an expression that uses the princ function and pass it the name of the variable. You should also follow the first expression with a second expression that uses the princ function, but do not pass it an argument to suppress the return value of the first princ function.

```c
(setq val 3 abc 3.875)
// out
3.875

(princ val)(princ)
// out
3
```

1『上面的打印语句下面有详细的解释。』

Note: If you do not add the second expression in the above example, a value of 33 appears to be returned. The first 3 is the desired output of the princ function, while the second 3 is the result of the value returned by the princ function. Remember that AutoLISP returns the value of the last function evaluated. In the previous example, no value is returned by the second princ because no argument was provided.

1『 autolisp 必定返回最后一个函数计算后的值。』

#### 3.5.1 About Nil Variables (AutoLISP)

A variable that has not been assigned a value has a default value of nil. This is different from blank, which is considered a character string, and different from 0, which is a number. So, in addition to checking a variable for its current value, you can test to determine if the variable has been assigned a value.

1『类似于 JavaScript 里的 undefined 的，哈哈。回复：nil 用的地方超级多，很多地方会先判断该变量（比如选择集）是否为空，非空的后再做相关的逻辑处理，`(if (/= nil (ssname ss i)) (......))`。（2020-10-06）』

Each variable consumes a small amount of memory, so it is good programming practice to reuse variable names or set variables to nil when their values are no longer needed. Setting a variable to nil releases the memory used to store that variable's value. If you no longer need the val variable, you can release its value from memory with the following expression:

```c
(setq val nil)
// out
nil
```

Another efficient programming practice is to use local variables whenever possible.

1『养成 2 个好习惯：1）释放不用的变量；2）尽量用不要用全局变量。』

#### 3.5.2 About Predefined Variables (AutoLISP)

AutoLISP has several predefined variables that can be used with your custom functions and commands. You can change the value of these variables with the setq function. However, other applications might rely on their values being consistent; therefore, it is recommended that you do not modify these variables. The following variables are predefined for use with AutoLISP applications:

1. PAUSE - Defined as a constant string of a double backslash (\\) character. This variable is used with the command function to pause for user input.

2. PI - Defined as the constant p (pi). It evaluates to approximately 3.14159.

3. T - Defined as the constant T. This is used as a non-nil value.

Note: Visual LISP, by default, protects these variables from redefinition. You can override this protection through the Visual LISP Symbol Service feature or by setting a Visual LISP environment option. Visual LISP is available on Windows only.

### 3.6 About Number Handling (AutoLISP)

AutoLISP provides functions for working with integers and real numbers. In addition to performing basic and complex mathematical computations, you can use the number-handling functions to help you in your daily use of AutoCAD. If you are drawing a steel connection detail that uses a 2.5" bolt with a diameter of 0.5" and has 13 threads per inch, you could calculate the total number of threads for the bolt by multiplying 2.5 by 13. In AutoLISP, this is done with the multiplication ( * ) function. Remember, the name of a function comes before the arguments you are passing to a function.

```c
(* 2.5 13)

// out
32.5
```

The arithmetic functions that have a number argument (as opposed to num or angle, for example) return different values if you provide integers or reals as arguments. If all arguments are integers, the value returned is an integer. However, if one or all the arguments are reals, the value returned is a real.

```c
(/ 12 5)
// out
2

(/ 12.0 5)
// out
2.4
```

### 3.7 About Strings and String Handling (AutoLISP)

A string is a group of characters surrounded by quotation marks. Within quoted strings the backslash (\) character allows control characters (or escape codes) to be included. When you explicitly use a quoted string in AutoLISP, that value is known as a literal string or a string constant. Examples of valid strings are “string 1” and “\nEnter first point:”.

AutoLISP provides many functions for working with string values. The following are some of the most commonly used functions:

1. strcat – Returns a string that is the concatenation of multiple strings.

2. strcase – Returns a string where all alphabetic characters have been converted to uppercase or lowercase.

3. strlen – Returns an integer that is the number of characters in a string.

4. substr – Returns a substring of a string.

5. vl-string-search – Searches for the specified pattern in a string.

6. vl-string-subst – Substitutes one string for another, within a string.

1『字符串的常用操作函数，跟数组的一样，得牢记，哈哈。』

#### 3.7.1 Convert the Case of a String

The alphabetic characters of a string can be converted to uppercase or lowercase with the strcase function. It accepts two arguments: a string and an optional argument that specifies the case in which the characters are returned. If the optional second argument is omitted, it evaluates to nil and strcase returns the characters converted to uppercase.

```c
(strcase "This is a TEST.")

// out
"THIS IS A TEST."
```

If you provide a second argument of T, the characters are returned as lowercase.

```c
(strcase "This is a TEST." T)

// out
"this is a test."
```

Note: The predefined variable T is often used to represent a True value when a function returns or excepts a True/False value. A nil value is used to represent a False value in these conditions.

1『 strcase 函数，一般是传递进 2 个参数，第一个参数是要处理的字符串；第二个参数决定如何处理，不输入的话默认为 nil，全大写，输入 T 的话代表 True，全小写。』

#### 3.7.2 Combine Multiple Strings

You can combine multiple strings into a single string value with the strcat function. This is useful for placing a variable string within a constant string, such as an error message or note in a drawing. The following code example sets a variable to a string value and then uses strcat to insert that string between two other strings.

```c
(setq str "BIG")

(setq bigstr (strcat "This is a " str " test."))

// out
"This is a BIG test."
```

#### 3.7.3 Return a Substring of a String

The substr function allows you to return a portion of a string. This function requires two arguments and has one optional argument. The first argument is a string and the second argument is an integer that represents the start character of the string that you want to return as the substring. If the third argument is not provided, substr returns all characters including and following the specified start character.

```c
(substr "Welcome to AutoLISP" 12)

// out
"AutoLISP"
```

If want to return a substring that is at the beginning or middle of the string provided to the substr function, you can specify an integer for the third argument that represents the number of characters that should be returned. For example, the following example code returns the first 7 characters of the provided string:

```c
(substr "Welcome to AutoLISP" 1 7)

// out
"Welcome"
```

Often, when working with a string you might not know how long it is but might know the start position of the substring you want to return. The strlen function returns the number of characters (including spaces) in a string.

```c
(setq filnam "bigfile.txt")
(strlen filnam)

// out
11
```

The following example code returns all the characters in a filename except the last four (the period and the three-letter extension). This is done by using strlen to get the length of the string and subtract 4 from that value. Then substr is used to specify the first character of the substring and its length.

```c
(setq newlen (- (strlen filnam) 4))
// out
7

(substr filnam 1 newlen)

"bigfile"
```

1『

上面的方法可以获得一个文件的文件名。应该也可以直接用字符串函数来实现，待实现。（2020-07-03）

回复：在 autolisp 里确实可以直接通过内置的函数来实现获取文件名，数据流开发过程中用到的（2020-10-06）。

```c
(set fn filename)
(set currentDir (getvar "dwgprefix"))
(set fn (strcat currentDir fn ".txt"))
```

』

You can combine the two previous lines of code into one if you do not need the length of the string stored in the newlen variable for other functions.

```c
(substr filnam 1 (- (strlen filnam) 4))

// out
"bigfile"
```

#### 3.7.4 Find and Replace Text in a String

Finding and replacing text can be helpful in updating notes or part numbers. The vl-string-search function allows you to locate a pattern within a string, and return the start position as an integer of the first instance of the specified pattern. If the function returns an integer, you can then use that as the starting position for another search to make sure there is not more than one instance of the pattern in the string.

The vl-string-subst function can be used to replace text within a string. Similar to the vl-string-search function, it can only identify the first instance of a specified pattern. You can use the vl-string-search function after replacing a text string to see if another instance of a pattern is contained in the string returned by vl-string-subst.

1『可以两个函数结合起来用遍历的方法全部替换。』

The following code examples find and replace the text [WIDTH] in a string.

```c
(setq note "All door openings are [WIDTH] unless otherwise noted.")
// out
"All door openings are [WIDTH] unless otherwise noted."

(setq position (vl-string-search "[WIDTH]" note))
// out
22

(setq revised-note (vl-string-subst "36\"" "[WIDTH]" note position))
// out
"All door openings are 36\" unless otherwise noted."

(prompt revised-note)(princ)
// out
All door openings are 36" unless otherwise noted.
```

### 3.8 About List Handling (AutoLISP)

AutoLISP provides functions for working with lists. This section provides examples of the append, assoc, car, cons, list, nth, and subst functions. A summary of all list-handling functions is in AutoLISP Function Synopsis (AutoLISP), under the heading List Manipulation Functions(AutoLISP).

Lists provide an efficient and powerful method of storing numerous related values. After all, LISP is so-named because it is the LISt Processing language. Once you understand the power of lists, you'll find that you can create more powerful and flexible applications.

Several AutoLISP functions provide a basis for programming two-dimensional and three-dimensional graphics applications. These functions return point values in the form of a list. The list function provides a simple method of grouping related items. These items do not need to be of similar data types. The following code groups three related items as a list:

```c
(setq lst1 (list 1.0 "One" 1))

// out
(1.0 "One" 1)
```

You can retrieve a specific item from the list in the lst1 variable with the nth function. This function accepts two arguments. The first argument is an integer that specifies which item to return. A 0 specifies the first item in a list, 1 specifies the second item, and so on. The second argument is the list itself. The following code returns the second item in lst1.

```c
(nth 1 lst1)

// out
"One"
```

The cdr function returns all elements, except the first, from a list. For example:

```c
(cdr lst1)

// out
("One" 1)
```

The car function provides another way to extract items from a list. For more examples using car and cdr, and combinations of the two, see About Point Lists (AutoLISP).

Three functions let you modify an existing list. The append function returns a list with new items added to the end of it, and the cons function returns a list with new items added to the beginning of the list. The subst function returns a list with a new item substituted for every occurrence of an old item. These functions do not modify the original list; they return a modified list. To modify the original list, you must explicitly replace the old list with the new list.

The append function takes any number of lists and runs them together as one list. Therefore, all arguments to this function must be lists. The following code adds another "One" to the list lst1. Note the use of the quote (or ' ) function as an easy way to make the string "One" into a list.

```c
(setq lst2 (append lst1 '("One")))

// out
(1.0 "One" 1 "One")
```

The cons function combines a single element with a list. You can add another string "One" to the beginning of this new list, lst2, with the cons function.

```c
(setq lst3 (cons "One" lst2 ))

// out
("One" 1.0 "One" 1 "One")
```

You can substitute all occurrences of an item in a list with a new item with the subst function. The following code replaces all strings "One" with the string "one".

```c
(setq lst4 (subst "one" "One" lst3))

// out
("one" 1.0 "one" 1 "one")
```

3『[帮助: cons (AutoLISP)](http://help.autodesk.com/view/OARX/2018/CHS/?guid=GUID-33B418E7-DB3D-4CBE-954E-F070F0A7CB2B)

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

』


#### 3.8.1 About Point Lists (AutoLISP)

AutoLISP utilizes the list data type to represent graphical coordinate values. Points are expressed as lists with either two or three numerical values. 1) 2D point - List with two integer or real numbers, (X and Y, respectively), as in (3.4 7.52). 2) 3D point – List with three integer or real numbers, (X, Y, and Z, respectively), as in (3.4 7.52 1.0). You can use the list function to form point lists, as shown in the following examples:

```c
(list 3.875 1.23)
// out
(3.875 1.23)

(list 88.0 14.77 3.14)
// out
(88.0 14.77 3.14)
```

To assign particular coordinates to a point variable, you can use one of the following expressions:

```c
(setq pt1 (list 3.875 1.23))
// out
(3.875 1.23)

(setq pt2 (list 88.0 14.77 3.14))
// out
(88.0 14.77 3.14)

(setq abc 3.45)
// out
3.45

(setq pt3 (list abc 1.23))
// out
(3.45 1.23)
```

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

Retrieve the X, Y, and Z components of a point list. You can retrieve the X, Y, and Z components of a point list using three additional built-in functions; car, cadr, and caddr. The following code examples show how to retrieve values from a 3D point list. The pt variable is set to the point `1.5,3.2,2`:

```c
(setq pt '(1.5 3.2 2.0))
// out
(1.5 3.2 2.0)
```

The car function returns the first member of a list. In this example, it returns the X value of the point list to the x_val variable.

```c
(setq x_val (car pt))
// out
1.5
```

The cadr function returns the second member of a list. In this example it returns the Y value of the point list to the y_val variable.

```c
(setq y_val (cadr pt))
// out
3.2
```

The caddr function returns the third member of a list. In this example it returns the Z value of the point list to the z_val variable.

```c
(setq z_val (caddr pt))
// out
2.0
```

You can use the following code to define the lower-left and upper-right (pt1 and pt2) corners of a rectangle, as follows:

```c
(setq pt1 '(1.0 2.0) pt2 '(3.0 4.0))
// out
(3.0 4.0)
```

You can use the car and cadr functions to set the pt3 variable to the upper-left corner of the rectangle, by extracting the X component of pt1 and the Y component of pt2, as follows:

```c
 (setq pt3 (list (car pt1) (cadr pt2)))
// out
(1.0 4.0)
```

The preceding statement sets pt3 equal to point (1.0, 4.0).

AutoLISP supports combinations of the car and cdr functions up to four levels deep. Some examples of these functions are caaaar and cadr. Each a represents a call to car and each d represents a call to cdr. For example:

```c
(caar x)    is equivalent to  (car (car x)) 
(cdar x)    is equivalent to  (cdr (car x)) 
(cadar x)   is equivalent to  (car (cdr (car x)))
(cadr x)    is equivalent to  (car (cdr x)) 
(cddr x)    is equivalent to  (cdr (cdr x)) 
(caddr x)   is equivalent to  (car (cdr (cdr x)))
```

#### 3.8.2 About Dotted Pairs (AutoLISP)

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

』


### 3.9 About Basic Output Functions (AutoLISP)

AutoLISP includes functions for controlling the AutoCAD display, including both text and graphics windows. Some functions also display information in the Visual LISP Console window. The major text display functions are: 1) prin1. 2) princ. 3) print. 4) prompt.

These functions are discussed in the following linked topics. The remaining display functions are covered in About Using AutoLISP to Communicate with AutoCAD (AutoLISP), beginning with the About Display Control (AutoLISP) topic.

#### 3.9.1 About Displaying Messages (AutoLISP)

AutoLISP programs often need to inform the user of an error or request for input. Messages that are displayed should try and not interrupt the flow of a command, and when they do the text displayed should be short and precise as to what the problem is or the input that is being requested. AutoLISP offers the following functions to display messages to the user:

1. prompt - Displays string at the AutoCAD Command prompt.

2. princ - Displays a value at the AutoCAD Command prompt or to an open file. Strings are displayed without the enclosing quotation marks.

3. prin1 - Displays a value at the AutoCAD Command prompt or to an open file. Strings are enclosed in quotation marks.

4. print - Displays a value at the AutoCAD Command prompt or to an open file, but a blank line is placed before the value and a space is placed after the value. Strings are enclosed in quotation marks.

5. alert - Displays a dialog box containing an error or warning message.

6. terpri - Prints a newline to the AutoCAD Command prompt.

The write-char, write-line, getXXX, and entsel functions can also display messages at the AutoCAD Command prompt.

When entered from the Visual LISP Console window prompt, the prompt function displays a message (a string) in the AutoCAD Command window and returns nil to the Visual LISP Console window. The princ, prin1, and print functions all display a value (not necessarily a string) in the AutoCAD Command prompt and returns the value to the Visual LISP Console window.

The following examples demonstrate the differences between the basic output functions and how they handle the same string of text.

```c
(setq str "The \"allowable\" tolerance is \261 \274\"")
(prompt str)
// out
outputs The "allowable" tolerance is 1/4"
returns nil

(princ str)
// out
outputs The "allowable" tolerance is 1/4"
returns "The \"allowable\" tolerance is 1/4\""

(prin1 str)
// out
outputs "The \"allowable\" tolerance is 1/4""
returns "The \"allowable\" tolerance is 1/4\""

(print str)
// out
outputs<blank line> "The \"allowable\" tolerance is 1/4""<space>
returns "The \"allowable\" tolerance is 1/4\""
```

#### 3.9.2 About Exiting a Function Quietly (AutoLISP)

If you invoke the princ function without passing an expression to it, it displays nothing and has no value to return. So if you add a call to princ without any arguments, after an expression, there is no return value. This is a great way to suppress the nil that is often returned by the last expression within a custom function. This practice is called exiting quietly.

1『这里解释了为啥那么多语句是以 `(princ)` 收尾的。（2020-10-06）』

#### 3.9.3 About Control Characters in Strings (AutoLISP)

Within quoted string values, the backslash (\) character allows control characters (or escape codes) to be included. The following lists the currently recognized control characters:

The prompt, princ, and getXXX functions expand the control characters in a string and display the expanded string at the AutoCAD Command prompt. The following example shows displaying a backslash character (\) and quotation mark (") within a quoted string:

```c
(princ "The \"filename\" is: D:\\ACAD\\TEST.TXT.")
// out
The "filename" is: D:\ACAD\TEST.TXT
```

Text can be forced across multiple lines with the newline character (\n).

```c
(prompt "An example of the \nnewline character. ")
// out
An example of the
newline character.
```

You can also use the terpri function to cause a line break. The Return character (\r) returns to the beginning of the current line. This is useful for displaying incremental information (for example, a counter showing the number of objects processed during a loop).

1『

这里直觉是一个关键点，因为跟循环有关，等遇到应用点的时候在反馈回这里。

回复：做计数器用的。（2020-07-02）

[Pomoc: terpri (AutoLISP)](http://help.autodesk.com/view/OARX/2018/PLK/?guid=GUID-16FB5411-7563-4FB9-AB59-A73457B092C5)

Prints a newline to the command line

```
(terpri)
```
No arguments.

Return Values. Type: nil. Always returns nil.

Remarks: The terpri function is not used for file I/O. To write a newline to a file, use prin1, princ, or print.

』

A Tab character (\t) can be used in strings to indent or to provide alignment with other tabbed text strings. In this example, note the use of the princ function to suppress the ending nil.

```c
(prompt "\nName\tOffice\n- - - - -\t- - - - -
(_> \nSue\t101\nJoe\t102\nSam\t103\n")(princ)

Name Office
- - - - - - - - - -
Sue 101
Joe 102
Sam 103
```

#### 3.9.4 About Wild-Card Matching (AutoLISP)

A string can be compared to a wild-card pattern with the wcmatch function. This can be helpful when needing to build a dynamic selection set (in conjunction with ssget) or to retrieve extended entity data by application name (in conjunction with entget). The wcmatch function compares a single string to a pattern. The function returns T if the string matches the pattern, and nil if it does not. The wild-card patterns are similar to the regular expressions used by many system and application programs.

1-2『直觉这里又是一个关键点。讲的应该就是通配符的知识点。回复：通配符与选择集（ssget）配合构建动态选择集，还可以与 entget 配合，结合实体名筛选。其实跟正则的功能差不多。做一张术语卡片。』——已完成

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

### 3.10. About Equality and Conditional (AutoLISP)

AutoLISP includes functions that provide equality verification as well as conditional branching and looping. The equality and conditional functions are listed in AutoLISP Function Synopsis (AutoLISP), under the heading Equality and Conditional Functions (AutoLISP).

When writing code that checks string and symbol table names, keep in mind that AutoLISP automatically converts symbol table names to upper case in some instances. When testing symbol names for equality, you need to make the comparison insensitive to the case of the names. Use the strcase function to convert strings to the same case before testing them for equality.

1『确实，CAD 很多地方会自动把字符转成大写的，比如块里面的属性名。所以在做匹配的时候记得先用字符串函数 strcase 将要匹配的字符转成大写的。』

### 3.11. About Symbol and Function Handling (AutoLISP)

AutoLISP provides a number of functions for handling symbols and variables. The symbol-handling functions are listed in AutoLISP Function Synopsis (AutoLISP), under the heading Symbol-Handling Functions (AutoLISP).

AutoLISP provides functions for handling one or more groups of functions. The links in this topic provides examples of the defun function. The remaining function-handling functions are listed in AutoLISP Function Synopsis (AutoLISP), under the heading Symbol-Handling Functions (AutoLISP).

#### 3.11.1 About Defining a Function (AutoLISP)

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

#### 3.11.2 About Compatibility of Defun with Earlier Releases of AutoCAD (AutoLISP)

The internal implementation of defun changed in AutoCAD 2000. This change is transparent to the great majority of AutoLISP users upgrading from earlier AutoCAD releases. The change only affects AutoLISP code that manipulated defun definitions as a list structure, such as by appending one function to another, as in the following code:

```c
(append s::startup (cdr mystartup))
```

For situations like this, you can use defun-q to define your functions. An attempt to use a defun function as a list results in an error. The following example illustrates the error:

```c
(defun foo (x) 4)
// out
foo

(append foo '(3 4))
; error: Invalid attempt to access a compiled function definition.
You may want to define it using defun-q: #<SUBR @024bda3c FOO>
```

The error message alerts you to the possibility of using defun-q instead of defun. The defun-q function is provided strictly for backward compatibility with earlier releases and should not be used for other purposes.

#### 3.11.3 About C:XXX Functions (AutoLISP)

If an AutoLISP function is defined with a name of the form C:xxx, it can be issued at the AutoCAD Command prompt in the same manner as a built-in AutoCAD command. This is true regardless of whether you define and load the function in VLISP or at the AutoCAD Command prompt. You can use this feature to add new commands to AutoCAD or to redefine existing commands.

1『解答了前面的疑问。这样的话就可以在 CAD 里跟常规命令一样使用了。』

To use functions as AutoCAD commands, be sure they adhere to the following rules:

1. The function name must use the form C:xxx (upper- or lowercase characters). The C: portion of the name must always be present; the XXX portion is a command name of your choice. C:xxx functions can be used to override built-in AutoCAD commands. (See About Redefining AutoCAD Commands [AutoLISP].)

2. The function must be defined with no arguments. However, local variables are permitted and it is a good programming practice to use them.

1『不能有参数，但可以使用局部变量。』

A function defined in this manner can be issued transparently from within any prompt of any built-in AutoCAD command, provided the function issued transparently does not call the command function. When issuing a C:xxx defined command transparently, you must precede the XXX portion with a single quotation mark (').

You can issue a built-in command transparently while a C:xxx command is active by preceding it with a single quotation mark ('), as you would with all commands that are issued transparently. However, you cannot issue a C:xxx command transparently while a C:xxx command is active.

Note: When calling a function defined as a command from the code of another AutoLISP function, you must use the whole name, including the parentheses; for example, (C:HELLO). You also must use the whole name and the parentheses when you invoke the function from the VLISP Console prompt.

1『什么情况下用全称命令 (C:DONE) 还需确认。』

#### 3.11.3.1 About Defining Commands (AutoLISP)

New commands can be defined with the defun function and by prefixing a function name with c:. Functions prefixed with c: can be accessed directly from the AutoCAD Command prompt and used to redefine an AutoCAD command.

Functions that are defined as commands should not accept arguments directly, instead input for a command should be obtained using one of the getXXX functions. The following defines a function named HELLO. This function displays a simple message.

```c
(defun HELLO () (princ "\nHello world.") (princ))
// out
HELLO
```

Functions can be issued from the AutoCAD Command prompt or an AutoLISP program. The HELLO function can be called from the AutoCAD Command prompt by entering the following:

```c
Command: (hello)
// out
Hello world.
```

The HELLO function must be wrapped in parentheses since it is not defined as a command. Entering HELLO without the parentheses at the AutoCAD Command prompt, returns the following error message:

```c
Unknown command "HELLO". Press F1 for help.
```

Adding c: to the front of the HELLO function name results in the function being declared as a command, and can then be entered at the AutoCAD Command prompt without being wrapped with parentheses. For example:

```c
(defun C:HELLO () (princ "\nHello world.") (princ))
// out
C:HELLO
```

While HELLO is declared as a command, it is also an AutoLISP function as well. The command can now be entered at the AutoCAD Command prompt, as follows:

```c
Command: hello
// out
Hello world.
```

The HELLO command can also be used transparently because it does not make a call the command function. At the AutoCAD Command prompt, you could do the following:

```c
Command: line

From point: 'hello

Hello world.

From point:
```

If an AutoLISP function is declared as a command, you can call the command from an AutoLISP program by wrapping the whole function name with parentheses. For example:

```c
(c:hello)
```

Note: If you are using the Visual LISP Editor in the Windows release, the Console window does not recognize AutoCAD commands. You must wrap the function name with parentheses.

You cannot usually use an AutoLISP statement to respond to prompts from an AutoLISP-implemented command. However, if your AutoLISP routine makes use of the initget function, you can use arbitrary keyboard input with certain functions. This allows an AutoLISP-implemented command to accept an AutoLISP statement as a response. Also, the values returned by a DIESEL expression can perform some evaluation of the current drawing and return these values to AutoLISP.

1『直觉上这里的信息重要的，目前看不懂。（2020-10-06）』

#### 3.11.3.2 About Redefining AutoCAD Commands (AutoLISP)

Using AutoLISP, you can undefine and replace the functionality of a built-in AutoCAD command. The UNDEFINE command allows you to disable a built-in AutoCAD command, and then using AutoLISP it can be replaced by defining a user-defined command of the same name with the defun function. A command remains undefined for the current editing session only. The built-in definition of a command can be restored with the REDEFINE command.

You can execute the built-in definition of a command after it has been undefined by specifying its name prefixed with a period (.). For example, if you undefine QUIT, you can access the command by entering .quit at the AutoCAD Command prompt. This is also the syntax that should be used within the AutoLISP command function to make sure your user-defined functions and commands work predictably even if a built-in command has been undefined.

1『命令失效后，如果在命令前面加个 . 还是可以接着用的。』

It is recommended that you protect your menus, scripts, and AutoLISP programs by using the period-prefixed forms of all commands. This ensures that your applications use the built-in command definitions rather than a redefined command.

Consider the following example. Whenever you use the LINE command, you want AutoCAD to remind you about using the PLINE command. You can define the AutoLISP function C:LINE to substitute for the normal LINE command as follows:

```c
(defun C:LINE ( )
  (princ "Shouldn't you be using PLINE?\n")
  (command ".LINE")
 (princ)
)

// out
C:LINE
```

In this example, the function C:LINE is designed to issue its message and then to execute the standard LINE command (using .LINE with the command function). Before AutoCAD can use your definition of the LINE command, you must undefine the built-in LINE command. Enter the following to undefine the built-in LINE command:

```c
(command ".undefine" "line")
```

1『先要让原始命令失效。』

After undefining the command and entering line at the AutoCAD Command prompt, AutoCAD uses the C:LINE AutoLISP function:

```c
Command: line

// out
Shouldn't you be using PLINE?
```

.LINE Specify first point: Specify first point:

The previous code example assumes the CMDECHO system variable is set to 1 (On). If CMDECHO is set to 0 (Off), AutoCAD does not echo prompts during a command function call. The following code uses the CMDECHO system variable to prevent the LINE command prompt from repeating:

```c
(defun C:LINE ( / cmdsave )
  (setq cmdsave (getvar "cmdecho"))
  (setvar "cmdecho" 0)
  (princ "Shouldn't you be using PLINE?\n")
  (command ".LINE")
  (setvar "cmdecho" cmdsave)
 (princ)
)

// out
C:LINE
```

3『[Pomoc: getvar (AutoLISP)](http://help.autodesk.com/view/OARX/2018/PLK/?guid=GUID-9C56BEA8-D473-4305-9E17-BEF7630C334D)

Retrieves the value of an AutoCAD system variable.

```c
(getvar varname)
```

varname. Type: String. Names of a system variable. See the product's Help system for a list of current AutoCAD system variables.

Return Values. Type: Integer, Real, String, List, or nil. The value of the system variable; otherwise nil, if varname is not a valid system variable.

Examples. Get the current value of the fillet radius:

```c
(getvar 'FILLETRAD)

// out
0.25
```

』

Now if you enter line at the AutoCAD Command prompt, the following text is displayed:

```c
Shouldn't you be using PLINE?

Specify first point:
```

You can undefined and redefine commands to create a drawing management system, for example. You can redefine the NEW, OPEN, and QUIT commands to write billing information to a log file after a drawing is created and before you terminate an editing session.

#### 3.11.4 About Local Variables in Functions (AutoLISP)

AutoLISP provides a method for defining a list of symbols (variables) that are available only to your function. These are known as local variables.

#### 3.11.4.1 About Local and Global Variables (AutoLISP)

Variables can be local or global in scope based on how they are defined. The use of local variables ensures that the variables in your functions are unaffected by other user-defined functions and custom applications. These variables do not remain available after the calling function has completed its task.

When you define a function or a command, any variables that you want to remain local must be added after the forward slash ( / ) in the arguments and local variables list. For example, the following example defines a function named ARGTEST which combines a constant string with other strings values. arg1 and arg2 are populated by the arguments you provide when using the function, but ccc is defined as a local variable for this function.

```c
(defun ARGTEST ( arg1 arg2 / ccc )
  (setq ccc "Constant string")
  (strcat ccc ", " arg1 ", " arg2)
)

// out
ARGTEST
```

```c
(ARGTEST "String 1" "String 2")

// out
"Constant string, String 1, String 2"
```

Once the function is done, the value of ccc is lost. You can test this by entering the following at the AutoCAD Command prompt:

```c
!ccc

// out
nil
```

Tip: Do not make your variables local until after you have done most of the debugging for your function. By not declaring your variables as local right away, you can check the last values assigned to a variable after the function has finished.

Another advantage of using local variables is that AutoCAD can recycle the memory space used by these variables, whereas global variables keep accumulating within AutoCAD memory space.

Global variables can be helpful if you want to retain values in between the uses of a function or command while the function remains loaded, or to use a value across many functions. However, if all or many of your variables are global it becomes increasingly possible that you could end up changing the value of a variable so it is incompatible with another function. This can lead to unpredictable behavior and it can be very difficult to identify the source of a problem. When declaring a global variable, it is good practice to indicate that you intend a variable to be global. A common way of doing this is to add an opening and closing asterisk to the variable name, for example, \*default-layer*.

1『前后加星号代表是全局变量。』

All variables when they are initially declared are global. The following code demonstrates the use of both global and local variables.

```c
(setq *dr-layer* "Doors")
(defun list-layers ( / cur-layer)
  (setq cur-layer (getvar "clayer"))
  (prompt (strcat "\nCurrent layer: " cur-layer "\nDoor layer: " *dr-layer*))
 (princ)
)

// out
LIST-LAYERS
```

```c
(list-layers)

Current layer: 0

Door layer: Doors
```

You can test the values stored in the variables by doing the following:

```c
!cur-layer

nil

!*dr-layer*

"Doors"
```

While a variable can be declared as local in a function, a variable with the same name can also be declared as global. If a variable name is added to the local variables list of a function, the global variable with the same name is ignored. The following example code demonstrates this behavior:

```c
(setq var-scope "Global")
(defun list-scope ( / var-scope)
  (if (/= var-scope nil)
    (prompt (strcat "\nScope: " var-scope))
    (prompt (strcat "\nvar-scope is nil"))
  )

  (setq var-scope "Local")
  (prompt (strcat "\nScope: " var-scope))
 (princ)
)
```

```c
(list-scope)

// out
var-scope is nil
Scope: Local

!var-scope
//out
"Global"
```

1『之前没注意到，这里的「!var-scope」是不用加括号的。』

When the function is started, the variable var-scope is declared with a value of nil within the scope of the function. This is why the message var-scope is nil is returned when checking to see if the variable is nil. If var-scope was not added to the local variables list for the function, the message Scope: Global would have been displayed and the value of var-scope changed to "Local".

```c
(setq var-scope "Global")
(defun list-scope ( / )
  (if (/= var-scope nil)
    (prompt (strcat "\nScope: " var-scope))
    (prompt (strcat "\nvar-scope is nil"))
  )

  (setq var-scope "Local")
  (prompt (strcat "\nScope: " var-scope))
 (princ)
)
```

```c
(list-scope)
// out
Scope: Global
Scope: Local

!var-scope
// out
"Local"
```

To declare local variables (AutoLISP). Local variables are only accessible within the user-defined function that they are defined in. In the arguments and variables list of the defun function, add a forward slash ( / ) delimiter to the list. After the forward slash, list each local variable. Be certain there is at least one space between the slash and each local variable.

1『声明局部变量时，/ 与变量名后面得有个空格。』

#### 3.11.4.2 Example Using Local Variables (AutoLISP)

The LOCAL function in the following example defines two local variables: aaa and bbb. At the AutoCAD Command prompt, enter the following code:

```c
(defun LOCAL ( / aaa bbb)
  (setq aaa "A" bbb "B")
  (princ (strcat "\naaa has the value " aaa ))
  (princ (strcat "\nbbb has the value " bbb))
  (princ)
)

// out
LOCAL
```

Note: You can also add the example code to an existing or create a new LSP file. Then load the LSP file with the APPLOAD command.

Enter the following code to define two global variables before using the LOCAL function:

```c
(setq aaa 1 bbb 2)
// out
2
```

Enter the following code to check the value of the two global variables:

```c
!aaa
// out
1

!bbb
// out
2
```

Enter the following code to check the value of the two local variables:

```c
(local)

// out
aaa has the value A
bbb has the value B
```

You will notice the function used the values for aaa and bbb that are local within the function. The current values for aaa and bbb are still set to their global values and can be verified with the following statements:

```c
!aaa
// out
1

!bbb
// out
2
```

#### 3.11.5 About Functions with Arguments (AutoLISP)

With AutoLISP, many functions require you to pass them values. These values are known as arguments. There are functions that also accept no arguments, and some in which accept optional arguments. User-defined functions cannot have optional arguments. When you call a user-defined function that accepts arguments, you must provide values for all arguments.

1『注意：自定义的函数是没法使用默认形参的，必须明确掉。』

Note: You can define multiple user functions with the same name, but have each definition accept a different number or type of arguments.

1-2『同一个名字定义多个函数，每个函数设不同的形参。这倒是个折中的办法。回复：这不就是函数重载么，哈哈。（2020-07-03）回复：这个可以实现多态了，模拟面向对象范式，太 NB 了。做一张主题卡片。（2020-10-06）』——已完成

The symbols used as arguments are defined in the argument list before the local variables. Arguments are treated as a special type of local variable; argument variables are not available outside the function. You cannot define a function with multiple arguments of the same name. If you do use the same name for multiple arguments, the following error message is displayed at the AutoCAD Command prompt:

```c
duplicate argument name:
```

The following code defines a function that accepts two arguments. The code expects the arguments to both be of the string data type. The arguments are combined and returned as the resulting string.

```c
(defun ARGTEST ( arg1 arg2 / ccc )
  (setq ccc "Constant string")
  (strcat ccc ", " arg1 ", " arg2)
)

// out
ARGTEST
```

The ARGTEST function returns the desired value because AutoLISP always returns the results of the last expression it evaluates. The last line in ARGTEST uses strcat to concatenate the strings, and the resulting value is returned. This is one example where you should not use the princ function to suppress the return value from your program. This type of function can be used a number of times within an application to combine two variable strings with one constant string in a specific order. Because it returns a value, you can save the value to a variable for use later in the application.

```c
(setq newstr (ARGTEST "String 1" "String 2"))
// out
"Constant string, String 1, String 2"
```

The newstr variable is now set to the value of the three strings combined. Note that the ccc variable was defined locally within the ARGTEST function. Once the function runs to completion, AutoLISP recaptures the memory allocated to the variable. You can use the following code to check the value assigned to ccc.

```c
!ccc
// out
nil
```

If string values are not passed to the ARGTEST function, the strcat function will return the following error:

```c
; error: bad argument type: stringp 1
```

You can use the type function to verify the data type of an argument and respond appropriately. The vl-catch-apply-all function could also be helpful in catching the error returned by the strcat function. The following example code uses the type function to make sure that the ARGTEST function was passed two string values before trying to combine and return the resulting string.

1『 vl-catch-apply-all 是获取错误类型的函数，那么在写测试程序的时候应该很有用。』

```c
(defun ARGTEST (arg1 arg2 / ccc retVal)
  (setq ccc "Constant string")

  (if (= (type arg1) 'STR)
    (if (= (type arg2) 'STR)
      (setq retVal (strcat ccc ", " arg1 ", " arg2))
      (prompt "bad argument: arg2 not a string\n")
    )
    (prompt "bad argument: arg1 not a string\n")
  )
  (if retVal
    retVal
    (princ)
  )
)
```

#### 3.11.6 About Special Forms (AutoLISP)

Certain AutoLISP functions are considered special forms because they evaluate arguments in a different manner than most AutoLISP function calls. A typical function evaluates all arguments passed to it before acting on those arguments. Special forms either do not evaluate all their arguments, or only evaluate some arguments under certain conditions. The following AutoLISP functions are considered special forms:

### 3.12 About Error Handling (AutoLISP)

The AutoLISP language provides several functions for handling errors. The proper handling of errors allows your program to exit gracefully and with an expected result. Using the error handling functions of the AutoLISP programming language allows you to do the following: 1) Provide information to users when an error occurs during the execution of a program. 2) Restore the AutoCAD environment to a known state. 3) Intercept errors and continue program execution.

The following functions are useful to handle errors encountered by your programs:

1. \*error* - A user-definable error-handling function.

2. \*pop-error-mode* - Error-handling function that ends the previous call to \*push-error-using-command* or \*push-error-using-stack*.

3. \*push-error-using-command* - Error-handling function that indicates the use of the command function within a custom \*error* handler.

4. \*push-error-using-stack* - Error-handling function that indicates the use of variables from the AutoLISP stack within a custom \*error* handler.

5. vl-catch-all-apply - Passes a list of arguments to a specified function and traps any exceptions.

If your program contains more than one error in the same expression, you cannot depend on the order in which AutoLISP detects the errors. For example, the inters function requires several arguments, each of which must be either a 2D or 3D point list. A call to inters like the following:

```c
(inters 'a)
```

Two errors are encountered: too few arguments and invalid argument type. You will receive either of the following error messages:

```c
; *** ERROR: too few arguments
; *** ERROR: bad argument type: 2D/3D point
```

Your program should be designed to handle either error.

Note: AutoLISP evaluates all arguments before checking the argument types. In earlier releases of AutoCAD, AutoLISP evaluated and checked the type of each argument sequentially. To see the difference, look at the following code examples:

```c
(defun foo ()
  (print "Evaluating foo")
  '(1 2))

(defun bar ()
  (print "Evaluating bar")
  'b)

(defun baz ()
  (print "Evaluating baz")
  'c)
```

Observe how an expression using the inters function is evaluated in AutoCAD:

```c
Command: (inters (foo) (bar) (baz))

"Evaluating foo"

"Evaluating bar"

"Evaluating baz"

; *** ERROR: too few arguments
```

Each argument was evaluated successfully before AutoLISP passed the results to inters and discovered that too few arguments were specified. In AutoCAD R14 and earlier, the same expression evaluated as follows:

```c
Command: (inters (foo) (bar) (baz))

"Evaluating foo"

"Evaluating bar" error: bad argument type
```

AutoLISP evaluated (foo), then passed the result to inters. Since the result was a valid 2D point list, AutoLISP proceeds to evaluate (bar), where it determines that the evaluated result is a string, an invalid argument type for inters.

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
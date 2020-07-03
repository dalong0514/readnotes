# 2019114Autolisp-Developers-GuideR00

## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——DXF group codes

CAD 里实体对象的唯一标识。重新打开文件，里面实体的名称会变，但它的 handle 是不会变的，是唯一的；一个实体的 handle，其 Group Code 为 5；handent 函数，通过传入实体的 handent 来获得实体的名称。

The DXF Reference describes the drawing interchange format (DXF™) and the DXF group codes that identify attributes of AutoCAD objects. You might need to refer to the DXF Reference when working with association lists describing entity data. 

### 0202. 术语卡——Entity Names

An entity name is a numeric label assigned to objects in a drawing. It is actually a pointer into a file maintained by AutoCAD, and can be used to find the object's database record and its vectors (if they are displayed). This label can be referenced by AutoLISP functions to allow selection of objects for processing in various ways. Internally, AutoCAD refers to objects as entities.

Note: You can use the vlax-ename->vla-object function to convert an entity name to a VLA-object when working with ActiveX functions. The vlax-vla-object->ename function converts a VLA-object to an entity name. The following functions are useful when working with entity names: 1)entget - Retrieves an object's (entity's) definition data. 2) entlast - Returns the name of the last non-deleted main object (entity) in the drawing. 3) ssname - Returns the object (entity) name of the indexed element of a selection set. 4) entsel - Prompts the user to select a single object (entity) by specifying a point. 5) nentsel - Prompts the user to select an object (entity) by specifying a point, and provides access to the definition data contained within a complex object. 6) nentselp - Provides similar functionality to that of the nentsel function without the need for user input. 7) handent - Returns an object (entity) name based on its handle.

Entity names assigned to objects in a drawing are only in effect during the current editing session. The next time you open the drawing, AutoCAD assigns new entity names to the objects. You can use an object's handle to refer to it from one editing session to another.

1『实体名重新打开图纸会刷新掉，handle 则不会。』

Objects in a drawing can be represented as ActiveX (VLA) objects. When working with ActiveX methods and properties, you must refer to VLA-objects, not the ename pointer returned by functions such as entlast. VLA-objects can be converted to an ename pointer with vlax-vla-object->ename. You can also use vlax-ename->vla-object to convert an ename pointer to a VLA-object.

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

## 0101Introduction.md

[Pomoc: Introduction (AutoLISP)](http://help.autodesk.com/view/OARX/2018/PLK/?guid=GUID-A0E9D801-8BE9-4BF1-85E8-3807E15F3B71)

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

```
(fun1 (fun2 arguments)(fun3 arguments))
```

The first function, fun1, has two arguments, which in this example are expressions. The values returned by the expressions are used by fun1. The other functions, fun2 and fun3, each have one argument. AutoLISP evaluates the innermost expression first, working its way outward. For this example, expressions containing fun2 and fun3 are evaluated before fun1.

1『 AutoLISP 先执行最里层的表达式。』

The following example shows the use of the * (multiplication) function, which accepts one or more numbers as arguments:

```
(* 2 27)

// out
54
```

Because this code example has no surrounding expression, AutoLISP returns the result to the window from which you entered the code. Expressions nested within other expressions return their result to the surrounding expression. The following example uses the result from the + (addition) function as one of the arguments for the * (multiplication) function.

```
(* 2 (+ 5 10))

// out
30
```

In the previous example, (+ 5 10) returns a value of 15. After the innermost expression is evaluated, the AutoLISP interpreter sees the following:

```
(* 2 15)

// out
30
```

1『有个技巧。现在 autolisp 编辑器里编写代码，点菜单里的「加载活动编辑窗口」，下面的控制台会出现该文件的路径。接着在 CAD 里的 command prompt 里输入加载该文件的命名：(load "D:/xx.lsp") 即可。』

#### Entering AutoLISP Expressions

AutoLISP expressions can be entered directly at the AutoCAD Command prompt, loaded with an AutoLISP source (LSP) file, or the Visual LISP Editor (Windows only). When you type an open (left) parenthesis, you indicate to AutoCAD that the following text should be passed to the AutoLISP interpreter for evaluation.

If you enter the incorrect number of close (right) parentheses, AutoLISP displays the following prompt:

```
(_>
```

1『只要有开始符号 ( 就必定对应一个 ) 闭合符号，而且不写闭合符号的话在 command prompt 里命令就一直不会结束。』

The number of open parentheses in this prompt indicates how many levels of open parentheses remain unclosed. If this prompt appears, you must enter the required number of close parentheses for the expression to be evaluated.

```
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

```
(setq int1 2147483647)

// out
2147483647
```

If you enter an integer that is greater than the largest allowable value, AutoLISP returns the value as a real:

```
(setq int2 2147483648)

// out
2.14748e+009
```

An arithmetic operation involving two valid integers, but resulting in integer overflow, produces an invalid result:

```
(setq int3 (+ 2147483646 3))

// out
-2147483647
```

In the previous example the result is clearly invalid, as the addition of two positive numbers results in a negative number. But note how the following operation produces a valid result:

```
(setq int4 (+ 2147483648 2))

// out
2.14748e+009
```

In this instance, AutoLISP converts 2147483648 to a valid real before adding 2 to the number. The result is a valid real. The largest negative integer value retains its specified value:

```
(setq int5 -2147483647)

// out
-2147483647
```

If you enter a negative integer larger than the greatest allowable negative value, AutoLISP returns the value as a real:

```
(setq int6 -2147483648)

// out
-2.14748e+009
```

The following operation concludes successfully, because AutoLISP first converts the overflow negative integer to a valid real:

```
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

```
(setq lst1 (list 1.0 "One" 1))

// out
(1.0 "One" 1)
```

1『试验过，list 函数后面的元素不能直接用 () 括起来。如果想简单用 () 声明的话，可以用下面讲到的 ' 符号，替代 list 函数名。』

A list can also be created using the quote (or ' ) function.

```
(setq lst1 '(1.0 "One" 1))

// out
(1.0 "One" 1)
```

#### 3.3.4.2 Adding to or Changing an Item in a List

The append function allows you to add new items to the end of a list, and the cons function allows you to add new items to the beginning of a list. The subst function can be used to substitute a new item for every occurrence of an old item. These functions do not modify the original list; they return a modified list. If you need to modify the original list, you explicitly replace the old list with the new list.

The append function takes any number of lists and runs them together as one list. Therefore, all arguments to this function must be lists. The following code adds another "One" to the list stored in lst1.

```
(setq lst2 (append lst1 '("One")))

// out
(1.0 "One" 1 "One")
```

The cons function combines a single element with a list. You can add another string "One" to the beginning of a list, lst2, with the cons function.

```
(setq lst3 (cons "One" lst2 ))

// out
("One" 1.0 "One" 1 "One")
```

You can substitute all occurrences of an item in a list with a new item using the subst function. The following code replaces all strings "One" with the string "one".

```
(setq lst4 (subst "one" "One" lst3))

// out
("one" 1.0 "one" 1 "one")
```

#### 3.3.4.3 Retrieving an Item from a List

You can retrieve a specific item from a list with the nth function. This function accepts two arguments. The first argument is an integer that specifies which item to return. Lists start with a 0 index. A 0 specifies the first item in a list, 1 specifies the second item, and so on. The second argument is the list itself. The following code returns the second item in lst1.

```
(nth 1 lst1)

// out
"One"
```

The car function returns the first item of a list. For example:

```
(car lst1)

// out
1.0
```

The cdr function returns all items from a list as a new list, except the first item. For example:

```
(cdr lst1)

// out
("One" 1)
```

AutoLISP also offers a number of additional functions that are variations of the car and cdr functions. For example, the cadr function returns the second element of a list and the caddr function returns the third item of a list. The cadr function is like using the cdr function on a list and then car on the resulting list.

```
(cadr lst1)

// out
"One"

(car (cdr lst1))
// out
"One"
```

#### 3.3.5 About Selection Sets (AutoLISP)

Selection sets are groups of one or more objects (entities). You can interactively add objects to, or remove objects from, selection sets with AutoLISP routines. The following example uses the ssget function to return a selection set containing all the objects in a drawing.

```
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

```
(entlast)

// out
<Entity name: 27f0540>
```

Entity names assigned to objects in a drawing are only in effect during the current editing session. The next time you open the drawing, AutoCAD assigns new entity names to the objects. You can use an object's handle to refer to it from one editing session to another.

1『实体名重新打开图纸会刷新掉，handle 则不会。』

#### 3.3.7 About VLA-objects (AutoLISP/ActiveX)

Objects in a drawing can be represented as ActiveX (VLA) objects. When working with ActiveX methods and properties, you must refer to VLA-objects, not the ename pointer returned by functions such as entlast. VLA-objects can be converted to an ename pointer with vlax-vla-object->ename. You can also use vlax-ename->vla-object to convert an ename pointer to a VLA-object.

Note: AutoCAD for Mac does not support ActiveX.

2『VLA-object 的概念去多了解下。』

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

```
# open a file first
(setq f (open "d:\\test.txt" "w"))
(write-line "dalong" f)
# close the file
(close file)
```

』

The following example opens the myinfo.dat file for reading. The open function returns a file descriptor which is stored in the file1 variable:

```
(setq file1 (open "c:\\myinfo.dat" "r"))
#<file "c:\\myinfo.dat">
```

Files remain open until you explicitly close them in your AutoLISP program. The close function closes a file. The following code closes the file whose file descriptor is stored in the file1 variable:

```
(close file1)
// out
nil
```

1『果然所有语言都是一个套路，打开文件记得关掉。』

### 3.4 About Source Code Files (AutoLISP)

Although you can enter AutoLISP code at the AutoCAD Command prompt or Visual LISP Console window prompt (Windows only), any functions you define are lost when you close the drawing or session they were created in. AutoLISP source code can be saved to an ASCII text file with a .lsp extension. Saving AutoLISP source code to a file has the following advantages: 1) Programs are not lost when the drawing they are defined in is closed. 2) Programs can be used in more than one drawing and can be executed on multiple machines. 3) Programs can be shared with others in your organization. 4) Testing and debugging multiple expressions is considerably easier.

AutoLISP source code can also be stored in files with a .mnl extension. A Menu AutoLISP (MNL) file contains custom functions and commands that are required for the elements defined in a customization (CUIx) file. A MNL file is loaded automatically when it has the same name as a customization (CUIx) file that is loaded into the AutoCAD-based product.

1『 MNL 应该就是可以显示的自定义菜单，后面需要自己实现的。（2020-07-02）』

For example, on Windows, when acad.cuix is loaded, the file named acad.mnl is also loaded if it is found in one of the folders listed as part of the AutoCAD Support File Search Path. If a CUIx file does not have a corresponding MNL file, no error is displayed, the product just moves and loading other support files.

Note: While AutoLISP source code is commonly saved in files with a .lsp or .mnl extension, AutoLISP code can be loaded from any ASCII text file.

#### Topics in this section

1. About Formatting and Spaces in Code (AutoLISP). AutoLISP code can span multiple lines, and contain empty lines and extra spaces. Empty lines and extra spaces do not have any significant meaning, but can make your code easier to read.

2. About Comments in AutoLISP Program Files (AutoLISP). Comments are useful to both the programmer and future users who may need to revise a program to suit their needs.

3. To Create and Open AutoLISP Source Code Files (AutoLISP). AutoLISP source code files can be created and edited using a plain ASCII text editor.

#### 3.4.1 About Formatting and Spaces in Code (AutoLISP)

AutoLISP code can span multiple lines, and contain empty lines and extra spaces. Empty lines and extra spaces do not have any significant meaning, but can make your code easier to read. Multiple spaces between function and variable names, and constants are equivalent to a single space. The end of a line and tab is also treated as a single space. The following two expressions produce the same result:

```
(setq test1 123 test2 456)

(setq
  test1 123
  test2 456
)
```

The extensive use of parentheses in AutoLISP code can make it difficult to read. The traditional techniques for combatting this confusion is indentation, and to align the open and close parentheses of a function. The more deeply nested a line of code is, the farther to the right the line is positioned. The following two functions are the same code, but the second one is much easier to read and determine visually if the parentheses of the AutoLISP expressions are balanced.

```
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

1『上面的例子值得好好吸收消化。』

#### 3.4.2 About Comments in AutoLISP Program Files (AutoLISP)

Comments are useful to both the programmer and future users who may need to revise a program to suit their needs. It is good coding practice to include comments in all AutoLISP program files, small and large. Use comments to do the following: 1) Give a title, authorship, and creation date. 2) Provide instructions on using a routine. 3) Make explanatory notes throughout the body of a routine. 4) Make notes to yourself during debugging.

Comments begin with one or more semicolons ( ; ) and continue through the end of the line.

```
; This entire line is a comment
(setq area (* pi r r)) ; Compute area of circle
```

Any text within ;| ... |; is ignored. Therefore, comments can be included within a line of code or extend for multiple lines. This type of comment is known as an in-line comment.

```
(setq tmode ;|some note here|; (getvar "tilemode"))
```

The following example shows a comment that continues across multiple lines:

```
(setvar "orthomode" 1) ;|comment starts here
and continues to this line,
but ends way down here|; (princ "\nORTHOMODE set On.")
```

#### 3.4.3 To Create and Open AutoLISP Source Code Files (AutoLISP)

AutoLISP source code files can be created and edited using a plain ASCII text editor.

### 3.5 About Variables (AutoLISP)

Variables are used to store a value or list of values in memory. The data type of a variable is determined when a value is assigned. Variables retain their value until a new value is assigned or the variable goes out of scope. The scope of a variable can either be global or local. Global variables are accessible by any AutoLISP program that is loaded into a drawing, while local variables are only available within a specific function or command. You use the AutoLISP setq function to assign values to variables. The syntax of the setq function is as follows:

```
(setq variable_name1 value1 [variable_name2 value2 ...])
```

The setq function assigns the specified value to the variable name given, and returns the last assigned value as its function result. The following example creates two variables: val and abc. val is assigned the value of 3, while abc is assigned the value of 3.875.

```
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

```
(command "_.-layer" "_make" layr "")
(command "_.line" PAUSE (strcat "@" (itoa val) "<0") "")
```

#### Checking the Value of a Variable

You can use the following methods to determine the current value of a variable:

At the AutoCAD Command prompt, add an ! (exclamation point) in front of the variable and press Enter.

```
(setq val 3 abc 3.875)
// out
3.875

!val
// out
3
```

At the Visual LISP Console Window prompt, enter the name of the variable and press Enter. (Windows only).

```
_$ (setq val 3 abc 3.875)
// out
3.875

_$ val
// out
3
```

At the AutoCAD Command prompt or Visual LISP Console Window prompt (Windows only), or in an AutoLISP program, create an expression that uses the princ function and pass it the name of the variable. You should also follow the first expression with a second expression that uses the princ function, but do not pass it an argument to suppress the return value of the first princ function.

```
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

1『类似于 JavaScript 里的 undefined 的，哈哈。』

Each variable consumes a small amount of memory, so it is good programming practice to reuse variable names or set variables to nil when their values are no longer needed. Setting a variable to nil releases the memory used to store that variable's value. If you no longer need the val variable, you can release its value from memory with the following expression:

```
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

```
(* 2.5 13)

// out
32.5
```

The arithmetic functions that have a number argument (as opposed to num or angle, for example) return different values if you provide integers or reals as arguments. If all arguments are integers, the value returned is an integer. However, if one or all the arguments are reals, the value returned is a real.

```
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

```
(strcase "This is a TEST.")

// out
"THIS IS A TEST."
```

If you provide a second argument of T, the characters are returned as lowercase.

```
(strcase "This is a TEST." T)

// out
"this is a test."
```

Note: The predefined variable T is often used to represent a True value when a function returns or excepts a True/False value. A nil value is used to represent a False value in these conditions.

1『 strcase 函数，一般是传递进 2 个参数，第一个参数是要处理的字符串；第二个参数决定如何处理，不输入的话默认为 nil，全大写，输入 T 的话代表 True，全小写。』

#### 3.7.2 Combine Multiple Strings

You can combine multiple strings into a single string value with the strcat function. This is useful for placing a variable string within a constant string, such as an error message or note in a drawing. The following code example sets a variable to a string value and then uses strcat to insert that string between two other strings.

```
(setq str "BIG")

(setq bigstr (strcat "This is a " str " test."))

// out
"This is a BIG test."
```

#### 3.7.3 Return a Substring of a String

The substr function allows you to return a portion of a string. This function requires two arguments and has one optional argument. The first argument is a string and the second argument is an integer that represents the start character of the string that you want to return as the substring. If the third argument is not provided, substr returns all characters including and following the specified start character.

```
(substr "Welcome to AutoLISP" 12)

// out
"AutoLISP"
```

If want to return a substring that is at the beginning or middle of the string provided to the substr function, you can specify an integer for the third argument that represents the number of characters that should be returned. For example, the following example code returns the first 7 characters of the provided string:

```
(substr "Welcome to AutoLISP" 1 7)

// out
"Welcome"
```

Often, when working with a string you might not know how long it is but might know the start position of the substring you want to return. The strlen function returns the number of characters (including spaces) in a string.

```
(setq filnam "bigfile.txt")
(strlen filnam)

// out
11
```

The following example code returns all the characters in a filename except the last four (the period and the three-letter extension). This is done by using strlen to get the length of the string and subtract 4 from that value. Then substr is used to specify the first character of the substring and its length.

```
(setq newlen (- (strlen filnam) 4))
// out
7

(substr filnam 1 newlen)

"bigfile"
```

1『上面的方法可以获得一个文件的文件名。应该也可以直接用字符串函数来实现，待实现。（2020-07-03）』

You can combine the two previous lines of code into one if you do not need the length of the string stored in the newlen variable for other functions.

```
(substr filnam 1 (- (strlen filnam) 4))

// out
"bigfile"
```

#### 3.7.4 Find and Replace Text in a String

Finding and replacing text can be helpful in updating notes or part numbers. The vl-string-search function allows you to locate a pattern within a string, and return the start position as an integer of the first instance of the specified pattern. If the function returns an integer, you can then use that as the starting position for another search to make sure there is not more than one instance of the pattern in the string.

The vl-string-subst function can be used to replace text within a string. Similar to the vl-string-search function, it can only identify the first instance of a specified pattern. You can use the vl-string-search function after replacing a text string to see if another instance of a pattern is contained in the string returned by vl-string-subst.

1『可以两个函数结合起来用遍历的方法全部替换。』

The following code examples find and replace the text [WIDTH] in a string.

```
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


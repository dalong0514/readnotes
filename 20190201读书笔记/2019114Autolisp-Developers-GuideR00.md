# 2019114Autolisp-Developers-GuideR00

## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——DXF group codes

CAD 里实体对象的唯一标识。重新打开文件，里面实体的名称会变，但它的 handle 是不会变的，是唯一的；一个实体的 handle，其 Group Code 为 5；handent 函数，通过传入实体的 handent 来获得实体的名称。

The DXF Reference describes the drawing interchange format (DXF™) and the DXF group codes that identify attributes of AutoCAD objects. You might need to refer to the DXF Reference when working with association lists describing entity data. 

### 0202. 术语卡——

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


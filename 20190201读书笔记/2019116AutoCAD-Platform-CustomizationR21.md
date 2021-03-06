# 2019116AutoCAD-Platform-CustomizationR21

## 记忆时间

## 目录

Part II AutoLISP: Productivity through Programming

0201 —— Chapter 11: Quick Start for New AutoLISP Programmers

0202 —— Chapter 12: Understanding AutoLISP

0203 —— Chapter 13: Calculating and Working with Values

## 0201. Quick Start for New AutoLISP Programmers

The AutoLISP® language and programming in general are two subjects that I have enjoyed for over 15 years now, but the same subjects make some people cringe and want to run in the opposite direction. I am not going to claim AutoLISP is easy to learn, but it can be learned by anyone, whether or not they have a programming background. When I first set out to learn AutoLISP, I didn't have any programming experience, but I wanted the benefits that AutoLISP could offer.

I understand if you have some hesitation at the thought of learning AutoLISP, but you don't need to feel that way—I will help you. This chapter will ease you into some core programming concepts and the AutoLISP programming language by exposing you to a variety of functions that are available.

To complete the exercises in this chapter and be able to create and edit LSP files, you must have the following: 1) For Windows users: Autodesk® AutoCAD® 2006 or later and the Notepad program. 2) For Mac OS users: Autodesk® AutoCAD® 2011 or later and the TextEdit program.

NOTE: Although I mention AutoCAD 2006 or later, everything covered in this chapter should work without any problems going all the way back to AutoCAD® 2000 and even possibly earlier releases.

### 1.1 Working with AutoLISP Expressions

AutoLISP is a natural extension of AutoCAD, as it can be used seamlessly from the AutoCAD Command prompt. You can enter AutoLISP when no commands are active or when AutoCAD prompts you for a value. The programming statements used in AutoLISP are known as expressions. You can type expressions at the Command prompt as long as they start with an opening parenthesis [( ] or an exclamation point (! ). Follow those symbols with the functions you wish to execute and the arguments that provide data or further instruction.

Each AutoLISP expression that starts with an opening parenthesis must also end with a closing parenthesis. AutoLISP expressions must contain the same number of opening and closing parentheses—this is sometimes referred to as balancing parentheses. You can enter the opening and closing parentheses on separate lines, though.

Use these steps to gain a basic understanding of entering AutoLISP expressions at the AutoCAD Command prompt: ...... In this exercise, you did the following:

1 Entered AutoLISP expressions at the AutoCAD Command prompt and stored values in a user-defined variable (see Chapter 12,「Understanding AutoLISP,」for more information)

2 Used functions to perform basic math calculations (see Chapter 13,「Calculating and Working with Values,」for more information)

3 Created a list that represented a 2D coordinate (see Chapter 14,「Working with Lists,」for more information)

### 1.2 Working with Commands and Input

In addition to calculating values with AutoLISP and passing those values to a command, you can execute a command as part of an AutoLISP expression using the command function. Input can also be requested and passed to a command or saved to a user-defined variable.

The following steps demonstrate how to create a layer named Circles with an AutoCAD Color Index (ACI) of 30 using the -layer command. You'll then draw a circle on the new layer with a user-specified center point and radius.

......

Now that you've entered some short expressions, let's look at creating long expressions—expressions that can span multiple lines. Using the following steps, you will also see how to give feedback to the user based on values they provided in the form of the center point and radius of the circle.

......

1『学到了几个新函数：1）`vl-princ-to-string` 将 list 数据类型转化为字符串。2）`rtos` 将数字转化为字符串。（2020-10-08）』

In these exercises, you did the following:

1 Used standard AutoCAD commands to create a layer and draw a circle (see Chapter 12 for more information)

2 Requested input from the user and displayed information back to the user (see Chapter 15,「Requesting Input and Using Conditional and Looping Expressions,」for more information)

3 Converted values from one type of data to another (see Chapters 13 and 14 for more information)

### 1.3 Conditionalizing and Repeating Expressions

Complex programs often contain branches (different sets of expressions that are used to handle different conditions or choices by the user), and they might loop (execute a set of expressions multiple times). Conditional expressions allow your programs to use a programming concept known as branching. Branching gives your programs the ability to execute different expressions based on the input a user provides or the current value of a system variable. When modifying large sets of data or even prompting a user for input, you can use looping expressions to repeat a set of expressions while a condition is met.

This exercise demonstrates some of the conditional and looping expressions that are available in AutoLISP:

1 At the AutoCAD Command prompt, type `(if (= (tblsearch "layer" "Circles") nil)` and press Enter. The if function is used to test whether a condition is true or false. If the = comparison operator returns T, then the first expression is evaluated; otherwise, the second expression is. The tblsearch function is used to check to see if a layer, linetype, or some other nongraphical object already exists in a drawing.

2 Type `(command "-layer" "m" "Circles" "c" "30" " " " ")` and press Enter. This command creates the new Circles layer if it doesn't exist in the drawing.

3 Type `(prompt "\nLayer already exists.")` and press Enter.

4 Type `)` and press Enter. The closing parenthesis ends the if function. Either the Circles layer is created or the message Layer already exists. is displayed. Entering the four expressions again results in the displaying of the message.

5 Type `(setq cnt 0)` and press Enter. The setq function defines a user-defined variable named cnt and assigns it the value of 0.

6 Type `(command "circle" (list 0 0) 1)` and press Enter. This command draws a circle at 0,0 with a radius of 1 on the「Circles」layer.

    TIP: If the new circle is not visible on the screen, pan and/or zoom to make it visible.

7 Type `(repeat 7` and press Enter. The repeat function is used to repeat a set of AutoLISP expressions a specific number of times.

8 Type `(setq cnt (1+ cnt))` and press Enter. The `1+` function increments the current value of cnt by 1 each time the expression is evaluated.

9 Type `(command "circle" (list 0 0) (* (getvar "circlerad") 1.5))` and press Enter. Once you enter the expressions within the repeat loop and add the final closing parenthesis to complete the expression, AutoCAD draws a new circle at 0,0 with a radius that is 1.5 times larger than the previous circle that was drawn. The previous radius used to create a circle with the circle command is stored in the circlerad system variable. The getvar function returns the current value of a system variable.

10 Type `(command "change" (entlast) " " "p" "c" cnt " ")` and press Enter. The change command modifies the color of the recently drawn circle, or more specifically the last object in the drawing. The entlast function returns the last object added to the drawing.

11 Type `)` and press Enter. The closing parenthesis ends the repeat function. Seven concentric circles, as shown in Figure 11.2, are drawn around the circle that was drawn outside of the repeat loop. Each circle drawn inside the repeat loop is assigned a different color, and the radius of each circle is 1.5 times larger than the next inner circle.

In the previous exercise, you did the following:

1 Used comparison operators and conditional functions to evaluate different expressions based on the results of a test condition (see Chapter 15 for more information)

2 Used math-based functions to calculate the radius of a circle and to increment a counter used in a looping expression (see Chapter 13 for more information)

3 Checked to see if a layer existed in the drawing (see Chapter 17,「Creating and Modifying Nongraphical Objects,」for more information)

4 Repeated a set of AutoLISP expressions until a condition was met (see Chapter 15 for more information)

1『变量自增 1 的简化版写法：`(setq cnt (1+ cnt))`，其中 `1+` 也是一个函数。（2020-10-08）』

### 1.4 Grouping Expressions

Entering individual expressions can be helpful when you are first learning AutoLISP or when you are developing a new program, but it isn't ideal for you to do each time you want to execute a set of AutoLISP expressions. The AutoLISP programming language allows you to define a custom function that can be executed at the Command prompt or from a command macro assigned to a user-interface element, such as a ribbon or toolbar button.

The following steps demonstrate how to define a custom function named RectangularRevCloud that can be entered at the AutoCAD Command prompt:

......

In the previous exercise, you did the following:

1 Grouped a set of AutoLISP expressions into a custom function to make it easier to execute the expressions (see Chapter 12 for more information).

2 Accessed the value of a system variable (see Chapter 12 for more information).

### 1.5 Storing and Loading AutoLISP Expressions

AutoLISP expressions entered at the AutoCAD Command prompt are accessible from that drawing and only while that drawing remains open. You can store AutoLISP expressions in an LSP file that, once saved, can then be loaded into and executed from any drawing file that is opened in AutoCAD. The following exercise explains how to create and load an LSP file named `acp_qs.lsp`.

......

In the previous exercise, you did the following:

1 Created an LSP file to store AutoLISP expressions (see Chapter 20,「Authoring, Managing, and Loading AutoLISP Programs,」for more information).

2 Loaded an LSP file into AutoCAD (see Chapter 20 for more information).

## 0202. Understanding AutoLISP

The AutoLISP® programming language allows you to automate workflows in the Autodesk® AutoCAD® drawing environment. At first glance, AutoLISP can feel more than a bit intimidating because of its syntax and use of parentheses. This is not an uncommon feeling for those who are new to AutoLISP and it's why some claim that LISP stands for「Lost in Stupid Parentheses」instead of its true meaning,「LISt Processing.」Although AutoLISP and even programming in general can take time to learn and understand, venturing down a path that is often less traveled can prove to be the difference that makes you and the company you work for stand out from others.

Here are some of the reasons I recommend AutoLISP: 1) The programs can be entered directly at the AutoCAD Command prompt and can be used in a script or CUI/CUIx files. 2) AutoLISP leverages your existing understanding of AutoCAD commands and system variables. 3) AutoLISP programs can be executed on Windows or Mac OS with no changes based on the functions used. 4) AutoLISP programs are low maintenance; programs written last week or even a decade ago often run with few to no changes in the latest release.

### 2.1 Getting Started with AutoLISP

I recommend that anyone who wants to create custom programs for AutoCAD consider AutoLISP as their first language to learn unless they have previous experience with another supported programming language, such as Visual Basic, VB.NET, C#, or C++. Even if you do know a programming language, you can use AutoLISP to quickly create a new custom program.

AutoLISP was the first programming language I learned, and it took me a bit of time to grasp not only AutoLISP but general computation logic as well. However, once I got some traction with AutoLISP and programming concepts, things started to click for me. Even to this day, AutoLISP is still very near and dear to me as a programming option when it comes to creating custom programs for AutoCAD.

When learning a programming language like AutoLISP, consider approaching it how you might learn a spoken language. First you need to learn some key fundamentals about the language and then spend time practicing to get good at it. As you start to learn AutoLISP, you will want to learn how to do the following: 1) Construct an AutoLISP expression. 2) Execute an AutoLISP expression. 3) Select an environment to create and edit AutoLISP programs. 4) Store AutoLISP expressions in a file to reuse.

I have no doubt that with time and practice you too can be successful in leveraging AutoLISP to be more productive in your daily work.

#### 2.1.1 Understanding the Syntax of an Expression

An AutoLISP expression is the formation of one or more items known as atoms. An atom represents a function or variable name, operator, or value. A valid AutoLISP expression must start with one of the following characters:

1 ( —Opening Parenthesis. An opening parenthesis indicates the beginning of an AutoLISP expression and must be paired with a closing parenthesis `)` to indicate the end of an AutoLISP expression. The opening and closing parentheses do not need to be on the same lines in an AutoLISP program, but each AutoLISP program must contain the same number of opening and closing parentheses.

2 ! —Exclamation Point. An exclamation point is used to retrieve the current value assigned to a variable. The exclamation point must be placed in front of the variable's name and can only be used at the AutoCAD Command prompt. I discuss variables later, in the「Storing and Retrieving Values」section.

Table 12.1 shows various AutoLISP expressions and a description of what happens when the expression is evaluated at the AutoCAD Command prompt.

`!cenPT` Returns the current value of a user-defined variable named cenPT, which by default is nil.

`(setq cenPT '(5 5 0))` Defines a user-defined variable named cenPT and assigns it a list that represents a coordinate point of 5,5,0 in a drawing.

`(command "._circle" cenPT 6.25)` Executes the AutoCAD circle command with the AutoLISP command function and draws a circle at the coordinate point assigned to the user-defined variable cenPT with a radius of 6.25 units.

`(- 10 (/ 6 3))` Returns a value of 8. When AutoLISP expressions are nested, the AutoLISP interpreter evaluates the innermost expression first. Then the next expression works its way to the outermost expression. (/ 6 3) is evaluated first and returns a value of 2. The outermost expression is then seen as being (- 10 2), which evaluates to the final value of 8.

`(setq msg (strcat "Hello " "World!"))` The AutoLISP strcat function concatenates multiple string values into a single string value. The value of「Hello World!」is returned by the strcat function and assigned to the user-defined variable msg.

Now that you have a basic understanding of what an AutoLISP expression looks like, the next step is to look at the inner workings of an AutoLISP expression's structure. A valid AutoLISP expression must start with an opening parenthesis and end with a closing one. Typically, between the two parentheses you will find the atoms that should be evaluated; remember that an atom represents a function name and the values that a function should perform an action on. There are two exceptions to this, though. The first exception is an exclamation point, which I mentioned earlier. The other exception is when an apostrophe is used instead of the AutoLISP list function. Figure 12.1 explains the structure of an AutoLISP expression.

When you type an AutoLISP expression, make sure that you have at least one space between each atom. You can have more than one space, but at least one space must be present. A space lets AutoCAD know where the name of the function or operator ends and the first value (if one is provided) begins. The following expression demonstrates what happens when a space after an operator is missing; the space is missing after the / operator.

```c
(- 10 (/6 3))
```

When the function is evaluated by AutoLISP, it thinks you are trying to use a function named /6 instead of the / operator. You'll see this error:

```
; error: no function definition:

/6 is displayed as a result of the missing space.
```

NOTE: The AutoLISP programming language, unlike other popular programming languages such as C# or C++, is not case sensitive. This means that the functions and user-defined variables are evaluated in exactly the same way, regardless of how you enter them—uppercase, lowercase, or mixed case. For example, COMMAND and command have the same meaning. The only time case matters is when you're using string values, which must start and end with quotation marks (").

1『 AutoLISP 里变量不区分大小写的。』

#### 2.1.2 Executing Expressions

AutoCAD supports a variety of ways to execute an AutoLISP expression. When first learning AutoLISP, you'll find being able to enter an AutoLISP expression directly at the AutoCAD Command prompt a huge benefit; you can see in real time the results of an entered expression. When you type an opening parenthesis or exclamation point at the Command prompt, AutoCAD passes control to the AutoLISP interpreter, which carries out the evaluation of the expression. After the expression is evaluated, control is then returned to AutoCAD and the standard Command prompt is displayed.

The following exercise creates a circle with a center point of 5,5,0 and a radius of 6.25 units using AutoLISP expressions at the Command prompt:

......

In addition to executing AutoLISP expressions at the AutoCAD Command prompt, you can use the following:

1 Scripts and Command Macros AutoLISP expressions can be used in script (SCR) files and command macros that are defined for use with a user-interface element in a customization (CUIx/CUI) file, just as you enter expressions at the Command prompt. I discussed SCR files in Chapter 8,「Automating Repetitive Tasks,」and you learned about CUIx/CUI files in Chapter 5,「Customizing the AutoCAD User Interface for Windows,」and Chapter 6,「Customizing the AutoCAD User Interface for Mac.」

2 A File You can store AutoLISP expressions in an ASCII text file and then load that file into AutoCAD. Entering expressions at the Command prompt is a great way to learn AutoLISP and is useful when only a few expressions need to be executed, but it is not ideal for complex programs or when you want to reuse the same expressions several times. I explain how to create and manage AutoLISP files in Chapter 20,「Authoring, Managing, and Loading AutoLISP Programs.」

#### 2.1.3 Accessing the AutoLISP Documentation

The AutoLISP documentation is part of the AutoCAD Help system. The help system includes the AutoLISP Reference and AutoLISP Developer's Guide topics. Although this book is designed to make it easy to learn the AutoLISP programming language and doubles as a reference that you can refer to time and time again when working with AutoLISP, it just is not possible to cover every function and technique here.

The AutoLISP Reference topics explain what each function does in the AutoLISP programming language. The AutoLISP Developer's Guide topics explore advanced techniques and features that are not covered in this book.

### 2.2 Storing and Retrieving Values

Programs—and programming languages, for that matter—are typically designed with one of two basic concepts in mind: to receive/consume or return/give. Most AutoLISP functions are designed to receive one or more values in the form of arguments, and then return a single value that can then be used by another function or returned to the user. When a function returns a value, you can store that value for future use—in the current custom function that is executing or even between different AutoCAD sessions. After a value has been stored, you can then retrieve the value for use by your program when it is needed.

You can store and retrieve values using these techniques:

1 User-Defined Variables. User-defined variables allow you to temporarily store a value within a function or globally while a drawing remains open. A variable is defined using the AutoLISP setq function. For example, you can use the expression `(setq msg "Hello AutoLISP! ")` to define a variable named msg and assign it the text string「Hello AutoLISP!」I discuss user-defined variables in the next section.

2 System Variables. System variables store values that are often used to control the behavior of AutoCAD commands or the drawing environment, and even allow access to the values that are calculated by some AutoCAD commands, such as area or distance. Unlike with user-defined variables, you can't create your own system variables. The system variable might represent a value that is stored in the current drawing or as part of the current AutoCAD user profile. See the section「Working with System Variables」later in this chapter.

3 Environment Variables. Similar to system variables, environment variables are used to control the behavior of AutoCAD commands or the drawing environment. You can access the values of environment variables that are defined by AutoCAD or even create your own as needed. Environment variables are stored as part of the AutoCAD user profile and as part of the Windows Registry or as a property list (Plist) file on Mac OS. I discuss accessing environment variables later in this chapter in the「Accessing Environment Variables」section.

4 Windows Registry (Windows Only). The Windows Registry is used to store settings that can be retrieved across different drawings and between application sessions. You can access the settings that AutoCAD reads and writes, and the Windows Registry is also a perfect place to store your own settings for your custom programs. I explain how to work with the Windows Registry in Chapter 18,「Working with the Operating System and External Files.」

5 Property List File (Mac OS Only). Similar to the Windows Registry, Plist files are used to store settings that can be retrieved across different drawings and between application sessions. As with the Window Registry, you can access the settings that AutoCAD reads and writes, and the Plist files are also a perfect place to store your own settings for your custom programs. I explain in Chapter 18 how to work with the Plist files.

6 Extended Data and Records. Extended data (XData) and records (XRecords) allow you to attach custom information to a graphical object or create a custom dictionary in a drawing that can be used to store multiple entries containing custom information. XData is a great way to add unique information to an object in a drawing. AutoCAD uses XData to help facilitate dimension overrides, implement some multiline text features, and provide other features. You'll learn about XData in Chapter 16,「Creating and Modifying Graphical Objects,」and XRecords in Chapter 17,「Creating and Modifying Nongraphical Objects.」

7 External Data Files. AutoLISP allows you to write values to and read values from an ASCII text file that can be stored outside of AutoCAD on a local or network drive. I explain how to access external files in Chapter 18. If you are using Windows and have Microsoft Office installed, you can also access information that can be created and modified using an application that is part of Microsoft Office—ActiveX/COM. I discuss using COM with AutoLISP in Chapter 22,「Working with ActiveX/COM Libraries (Windows Only).」

8 Configuration Files. Configuration (CFG) files are used to store settings that can be retrieved across different drawings and between application sessions. Storing values in a CFG file is not as common as it once was, but you should be familiar with storing and retrieving values from a CFG file just in case you are working on an older program. I recommend using one of the other techniques for storing values that can be accessed across multiple drawings or between application sessions, such as the Windows Registry, Plist files, or even external data files. You'll learn how to work with CFG files in Chapter 18.

1『汇总：1）第 6 点里，感觉 Extended Data and Records 有大用处，目前没遇到应用点，相关的知识也没去研读。2）妙啊，第 7 点提到，可以读取本地文件和网络文件作为输入数据，去看第 18 章的内容。（2020-10-08）』

#### 2.2.1 Setting and Using Variables

In an AutoLISP program, it is not uncommon to want to use the same value more than once or to use a value returned by one function as a value for an argument in another function. Variables allow you to define a named location in memory to temporarily store a value. AutoLISP supports two types of variables: user-defined and predefined. 1) User-defined variables are those that you or another developer create for use in an AutoLISP program. 2) Predefined variables are those that are automatically defined and assigned a specific value by the AutoLISP environment for each drawing that is created or opened.

#### Defining and Using User-Defined Variables

You can define a variable, called a user-defined variable, by using the AutoLISP setq function. By default each user-defined variable exists only in the context of the drawing in which it is defined; once the drawing is closed, the variable and its value are lost.

NOTE: If you need to retain the value assigned to a variable beyond the drawing it was defined in, consider using a custom dictionary object to store the value in a drawing, or use the Registry (Windows) or Plist file (Mac OS). I discussed these and other ways of storing values earlier, in the「Storing and Retrieving Values」section.

1『上面的知识点以后肯定会用到，用「custom dictionary object」或者「Registry」来存储数据，这样的数据可以在不同的图纸之间使用了。』

The following shows the syntax of the setq function:

```c
(setq var_name value)
```

`var_name`. The `var_name` argument represents the name of the user-defined variable you want to define and assign a value to.

value. The value argument represents the data that you want to assign to the variable specified by `the var_name` argument.

The setq function always returns the value that is assigned to the last variable in the expression.

The following AutoLISP expressions assign a coordinate value of 2,2,0 and numeric value of 6.25 to user-defined variables named pt and dia:

```c
(setq pt '(2 2 0)) (setq dia 6.25)
```

Although the setq function is commonly used to define a variable and then assign that variable a value, it can also be used to define multiple variable and value pairings. The following AutoLISP expression defines multiple variables and then assigns them a value:

```c
(setq pt '(2 2 0) dia 6.25)
```

Once a variable has been defined and a value assigned, you can use it as an argument with another AutoLISP expression or return its current value at the AutoCAD Command prompt. There is nothing special you need to do in order to use a variable in an AutoLISP expression, but you need to include an exclamation point before the variable name in order to return its current value at the AutoCAD Command prompt. For example, to return the value of the variable dia at the AutoCAD Command prompt you would type !dia and press Enter. (The exclamation point isn't necessary when you're using the variable inside an AutoLISP expression that begins and ends with parentheses.)

The following exercise demonstrates how to define two variables and use their values at the AutoCAD Command prompt:

1 At the AutoCAD Command prompt, type !cenpt and press Enter. nil should be returned, unless the variable was previously defined.

2 Type (setq cenpt '(1 2 0)) and press Enter. The variable cenpt is defined and assigned the coordinate value 1,2,0. (1 2 0) is returned by the setq function.

3 Type !cenpt and press Enter. The value of the cenpt variable is returned, which should be (1 2 0).

4 Type (setq rad 3.125) and press Enter. The variable rad is defined and assigned the real numeric value 3.125.

5 Type circle and press Enter. The circle command is started.

6 At the Specify center point for circle or [3P/2P/Ttr (tan tan radius)]: prompt, type !cenpt and press Enter. The value of the cenpt variable is returned and used for the circle's center point.

7 At the Specify radius of circle or [Diameter]: prompt, type !rad and press Enter. The value of the rad variable is returned and used for the circle's radius. The circle command ends and the circle is drawn.

#### Using Predefined Variables

In addition to the user-defined variables that you might create and use in AutoLISP expressions, the AutoLISP environment defines three variables that are assigned a specific value and are accessible from all drawing files that are opened. The variables that are predefined by the AutoLISP environment are as follows:

1 PI. The PI variable is assigned the value of 3.141592653589793, which is a constant value that represents the ratio of a circle's diameter to its circumference.

2 T. The T variable always returns a value. This variable is commonly used when you test whether a condition returns True.

3 PAUSE. The PAUSE variable is assigned the string「\\」. The PAUSE variable is used in combination with the command function to suspend the execution of an AutoLISP expression and allow the user to respond to a command's request for input.

WARNING: You should never change the value of a predefined variable; doing so could affect the execution of the AutoLISP programs that use them.

#### 2.2.3 Controlling the Scope of a Variable

Variables can be accessed from the global or local scope of the AutoLISP environment. By default, all variables defined with the setq function are accessible globally. Each of the predefined variables that are defined by the AutoLISP environment are accessible from the global scope of the AutoLISP environment. However, you typically want to limit the number of such variables in the current drawing. Variables that are defined with the global scope continue to consume system resources until you set the variable to the value of nil, whereas those defined as local variables have their system resources freed up when the execution of the function in which they are defined ends.

Another reason to limit global variables is what I refer to as unexpected data. Unexpected data occurs when a variable is assigned one value by your program and changed to another value by a different program. For example, say you assigned a global variable the value of 6.25, but another program (one written by you or even a third-party program) is using that same variable name and assigns the variable the value of (1「A」). Based on how your program is designed, it might be using the variable as a way to persist the last value chosen by the user, much the same way the AutoCAD circle command remembers the last radius used. When your program goes to use the value, it gets a list instead of a numeric value, which must be handled differently and doesn't even hold a value that is useful to you any longer.

---

#### Unique Function and Global Variable Names

AutoLISP is kind of like the Wild West—at times it can feel lawless since you have the ability to stake a claim to a name and still have someone come in and take it from you. For example, you can create a function named MakeLayer or a user-defined global variable named pt. A third party could do the same. If the third-party LSP file contains the same function or it defines a variable with the same name, your loaded function and defined variable are replaced.

To help protect your functions and variables, I recommend adding a unique prefix to their names. Typically, the unique prefix you create is derived from a company name. For example, you might use the unique prefix of mc3 if your company was My Cool CAD Company. In addition to adding the unique prefix to a variable name, I recommend prefixing and suffixing the names of any global variables with an asterisk to make it easier to identify which variables are defined globally.

Instead of creating a function named MakeLayer, you would use the name `mc3_MakeLayer` and for a variable named size (which might store the size of a bolt) you would use `*mc3_size*.` Another consideration when naming global variables is whether they need to be program or function specific. For function-specific global variables, consider including the name of the function that defines the variable. For example, the two functions DrawBolt and DrawScrew were originally written to use a global variable named `*mc3_size*`, which stores the recent size the user selects when using either of the functions. The size is then used the next time the function is executed; AutoLISP offers users their previous selection, which (based on the current naming of the variable) would be a potential problem. By using the variable names `*mc3_drawbolt_size*` and `*mc3_drawscrew_size*`, you ensure that both functions have their own global variable.

---

The following explains the differences between global and local variables, and shows you how to define a variable in the local scope of a custom function:

1 A global variable is accessible to all AutoLISP programs that are loaded into the drawing and to those expressions that are executed in the drawing from which the variable was defined. By default, all variables are defined with a global scope.

2 A local variable is accessible only from the function in which it is defined. You define the variable using the setq function, but the name of the variable is also added to the `local_var` argument of the defun function to restrict its use to just that function. I discuss the defun function later in this chapter in the section「Defining and Using Custom Functions.」If a variable is not added to this argument, it remains a global variable.

Although a variable can be defined with a global scope, a variable with the same name can exist in the local scope of a function. When this happens, the expressions inside your function are aware only of the local variable. The following steps show how a variable defined in the local scope of a custom function takes precedence over a variable defined with a global scope:

1 At the AutoCAD Command prompt, type the following and press Enter: `(setq *apc_var* "Global")`

2 Type the following and press Enter to define the GlobalVar function: `(defun c:GlobalVar ( / )(alert *apc_var*))`

3 Type the following and press Enter to define the LocalVar function: `(defun c:LocalVar ( / *apc_var*) (setq *apc_var* "Local") (alert *apc_var*) )`

4 Type globalvar and press Enter. Click OK to exit the alert message box. The alert message box displays the text string assigned to the `*apc_var* `variable in the global scope, which is the value Global.

5 Type localvar and press Enter. Click OK to exit the alert message box. The variable `*apc_var*` is assigned the value of the string "Local" and then an alert message box displays the text string assigned to the `*apc_var*` variable in the local scope, which is the value Local.

6 Type globalvar and press Enter. Click OK to exit the alert message box. The alert message box displays the text string assigned to the `*apc_var*` variable in the global scope, which is the value Global. When the localvar function was executed in step 5, the`*apc_var*` variable was assigned a value that existed only while the function was executing; it did not overwrite the value of the globally defined `*apc_var*` variable.

TIP: User-defined variables are normally accessible only from the drawing in which they are defined, but you can use the AutoLISP vl-bb-ref and vl-bb-set functions to define variables on what is known as the blackboard. The blackboard is a centralized location for defining variables that can be accessed from any open drawing. The AutoLISP vl-propagate function can also be used to define a variable with a specific value in all open drawings and any drawings that are subsequently opened in the AutoCAD session. You can learn more about these functions in the AutoCAD Help system.

1-2『上面的几个函数，可以实现把一些数据放到公共变量（内存）中，保证所有打开的图纸空间都可以访问到。这个可以帮助实现把数据从流程图迁移到设备布置图，功能待开发，哈哈。做一张任意卡片。（2020-10-08）』—— 已完成

#### 2.2.4 Working with System Variables

System variables are used to alter the way commands work, describe the current state of a drawing or AutoCAD environment, and even specify where the support files are for your custom programs. Many of the settings that are exposed by system variables are associated with controls in dialog boxes and palettes; other settings are associated with various command options. For example, many of the settings in the Options (Windows) or Application Preferences (Mac OS) dialog box are accessible from system variables and even environment variables (which I discuss in the next section).

A system variable can store any one of the basic data types that AutoLISP supports (see「Exploring Data Types」later in this chapter). You can see the hundreds of system variables and the type of data each system variable holds by using the AutoCAD Help system. Whereas you might normally use the setvar command to list or change the value of a system variable at the AutoCAD Command prompt, with AutoLISP you use the getvar and setvar functions to query and set the value of a system variable. Here's the syntax of the getvar and setvar functions:

```c
(getvar sysvar_name) (setvar sysvar_name value)
```

`sysvar_name`. The `sysvar_name` argument represents the name of the system variable you want to query or set.

`value`. The value argument represents the data that you want to assign to the system variable.

The next exercise demonstrates how to query and set the value of the osmode system variable, which controls the running object snap drafting aid. This setting is available in the Drafting Settings dialog box (dsettings command).

1 At the AutoCAD Command prompt, type `(setq *apc_cur_osmode* (getvar "osmode"))` and press Enter. The function returns the current value of the osmode system variable and assigns it to the user-defined variable `*apc_cur_osmode*` with the setq function.

2 Type `(setvar "osmode" 33)` and press Enter. The osmode system variable is assigned the integer value of 33, which represents the Endpoint and Intersection running object snap modes.

3 Type osnap and press Enter. In the Drafting Settings dialog box, select the Object Snap tab and verify that the Endpoint and Intersection options are checked and all other options are unchecked. Click Cancel to return to the Command prompt.

4 Type `(setvar "osmode" *apc_cur_osmode*)` and press Enter. The previous value of the system variable is restored.

5 Type osnap and press Enter. In the Drafting Settings dialog box, you will notice that the options checked will represent those of the restored running object snap settings value. Click Cancel to return to the Command prompt.

TIP: The AutoCAD Help system is a great resource for learning about system variables. However, if you need to support multiple AutoCAD releases you will need to reference the documentation for each release. To make it easier to identify which system variables are supported in the recent and past AutoCAD releases, I created a list of system variables that spans a large number of AutoCAD releases; you can view the list here: [HyperPics: AutoCAD System Variable References for AutoCAD R12 through AutoCAD 2013](http://www.hyperpics.com/system_variables/).

3『顺藤摸瓜，找到这个好网站：[HyperPics: Resources for the AutoCAD and AutoCAD LT Programs](http://www.hyperpics.com/)。』

#### 2.2.5 Accessing Environment Variables

Environment variables allow you to access settings that are, at times, accessible only from the Options (Windows) or Application Preferences (Mac OS) dialog box and not through system variables or from the Command prompt. Unlike with system variables, though, there is no official documentation that explains which environment variables are available or what values they can be assigned.

Many of the environment variables that I am aware of can be found stored in the Windows Registry or a Plist file on Mac OS. Both of these storage locations include a General Configurations section for the AutoCAD program, and it is in this section that you will find the environment variables you can manipulate. You use the AutoLISP getenv and setenv functions to retrieve and set the value of an environment variable.

WARNING: Unlike system variables, environment variable names are case sensitive. For example, MaxHatch is not the same as maxhatch or MAXHATCH.

The following shows the syntax of the getenv and setenv functions:

```c
(getenv envvar_name) (setenv envvar_name "value")
```

`envvar_name`. The `envvar_name` argument represents the name of the environment variable you want to query or set.

`value`. The value argument represents the string value that you want to assign to the environment variable. Environment variables can only be assigned a string value, but that string could contain a number or even a list of values.

Both the getenv and setenv functions return the current value of the environment variable or the value that was successfully assigned to an environment variable.

The following steps show how to retrieve and set the value of the DefaultFormatForSave environment variable, which controls the default format for saving drawings. This setting is available in the Options dialog box on Windows, but not in the Application Preferences dialog box on AutoCAD 2013 and earlier on Mac OS. It does affect the behavior of saving a drawing file on both Windows and Mac OS.

1 At the AutoCAD Command prompt, type `(setq *apc_cur_val* (getenv "DefaultFormatForSave"))` and press Enter. The function returns the current value of the environment variable and assigns it to the user-defined variable `*apc_cur_val*` with the setq function.

2 Type `(setenv "DefaultFormatForSave" "48")` and press Enter. The DefaultFormatForSave environment variable is assigned the value of 48, which represents the AutoCAD 2010 drawing file format. If you are using an earlier release, you may need to use a different value to set a previous drawing file format as current.

3 Type saveas and press Enter. In the SaveAs dialog box, notice that the Files Of Type drop-down list will list AutoCAD 2010/LT2010 Drawing (*.dwg) as the current option. Click Cancel to return to the Command prompt.

4 Type `(setenv "DefaultFormatForSave" *apc_cur_val*)` and press Enter. The previous value of the environment variable is restored.

5 Type saveas and press Enter. In the SaveAs dialog box, notice that the Files Of Type drop-down list now lists the previous default drawing file format. Click Cancel to return to the Command prompt.

TIP: I created a list (though not complete or up to date) of the environment variables available in a number of earlier releases of AutoCAD. You can find this list here: http://www.hyperpics.com/downloads/resources/customization/autolisp/AutoCAD%20Environment%20Variables.pdf

2『已下载「附件1201AutoCAD-Environment-Variables」作为本书的附件。』

### 2.3 Exploring Data Types

Programming languages use data types to help you identify the following: 1) The type of data required by a function's argument. 2) The type of data that might be returned by a function.

AutoLISP on Windows and Mac OS support the following data types:

1 Integer. An integer is a numeric value without a decimal point. The numeric value must be in the range of –32,768 to 32,767 and can be optionally prefixed with a plus sign (+) for positive numbers. You can use an integer value to represent an angular or linear distance or the number of columns or rows in an array or table, or to specify whether a system variable is enabled or disabled. Examples include -10, 0, 1, +45, and 400. You'll learn about using integer values with mathematical functions in Chapter 13,「Calculating and Working with Values.」

2 Real. A real value is numeric with a decimal point. The numeric value must be in the range of 1.80 × 10308 to –4.94 × 10–324 for negative numbers and 4.94 × 10–324 to 1.80 × 10308 for positive numbers. A positive number can optionally be prefixed with a plus sign and be expressed in exponential notation; 10e4 is the same as 100000.0. When using a value between –1.0 and 1.0, you must use a leading zero before the decimal;.5 is not a valid real number but 0.5 is. You might use a real number to represent an angular or linear distance or part of a coordinate. Examples of a real number are –10.01, 0.0, 1.125, +45.0, and 400.00001. Chapter 13 discusses using real values with mathematical functions.

NOTE: The real data type in AutoLISP is commonly referred to as a double or float in other programming languages.

3 String. A string is a value that contains one or more characters enclosed in quotation marks. You might use a string value for a command or system variable name, a file path and name, messages and prompts that are displayed to the user, or even a real or integer number converted to a string. Examples of a string value are「Hello AutoLISP!", "._line", "\nSpecify next point: ", and "6.25". You'll learn more about working with string values in Chapter 13.

4 List. A list is an expression of one or more atoms enclosed in parentheses. All AutoLISP expressions are known as lists, but lists often represent 2D points, 3D points, and data groupings. Examples of a list are `(1.5 2.75)`, `(1.5 2.75 0.5)`, `("Model" "Layout1" "Layout2")`, `(1 "A" 2 "B")`, and `()`. () represents an empty list. When you're assigning a list to a variable, either the list must be preceded by an apostrophe, as in `(setq pt '(1 2 0))`, or you must use the AutoLISP list function, as in `(setq pt (list 1 2 0))`. Chapter 14,「Working with Lists,」explores creating and manipulating lists.

NOTE: The list data type in AutoLISP is similar to an array in other programming languages.

5 Dotted Pair. A dotted pair is a list of two values separated by a period. Dotted pairs are commonly used to represent property values for an object. The first value of a dotted pair is sometimes referred to as a DXF group code. For example, `(40 . 2.0)` represents the radius of a circle; DXF group code value 40 indicates the radius property, and 2.0 is the actual radius value for the circle. When you're assigning a dotted pair to a variable, either the pair must be preceded by an apostrophe, as in `(setq dxf_40 '(40 . 2))`, or you must use the AutoLISP cons function, as in `(setq dxf_40 (cons 40 2))`. You'll learn more about creating and manipulating dotted pairs in Chapter 16.

6 Entity Name. An entity name is an in-memory numeric label used to reference an object stored in a drawing. You will often work with an entity name to modify an object's properties or after a request to select objects in a drawing has been completed. See Chapters 16 and 17 to learn how to work with entity names.

2『 Dotted Pair 做一张术语卡片。』—— 已完成

AutoLISP on Windows supports a few additional data types, and I discuss these additional data types in depth and how they are used in Chapter 22. The data types that are specifically used for working with ActiveX libraries are as follows:

1  VLA-Object. A VLA-Object represents an ActiveX object that is used when working with methods and properties imported from the AutoCAD Object Library or another ActiveX library. An ActiveX object can be an object stored in a drawing, an open drawing, or the AutoCAD application itself.

2 Variant. A variant is a generic data type that can hold any type of data supported by the Component Object Model (COM) interface.

3 Safearray. A safearray is not really a data type, but rather a data structure that can contain multiple values similar to the list data type. You use a safearray when you need to represent a coordinate value, specify the objects used to define a closed boundary when creating a Region or Hatch object, or specify the data types and values that make up the XData attached to an object.

You can use the AutoLISP type function to identify the type of data retuned by a function or assigned to a variable. The following shows the syntax of the type function:

```c
(type value)
```

value. The value argument represents any valid atom; an AutoLISP expression, a value, or a variable.

The type function returns a symbol that can be used to determine if the value returned by a function or assigned to a variable is the type of data you are expecting. The following AutoLISP expressions define a custom function named IsString, which uses the type function to determine whether a value is of the string data type:

```c
(defun IsString (val / ) 
  (if (= (type val) 'STR) T nil) 
)
```

You can use the IsString function by entering it at the AutoCAD Command prompt or loading it as part of an AutoLISP (LSP) file. When the function is executed, it will return T if the value it is passed is a string data type or nil for all other data types. The following shows several examples of the IsString function along with the values they return:

```c
(IsString "2") 
// out 
T 

(IsString 2) 
// out
nil 

(IsString PAUSE) 
// out
T 

(IsString PI) 
// out
nil
```

1-2『完全可以自己做一些判断数据类型的函数，封装起来自己用，真切的感觉到，一切语法即为语法糖。封装判断数据类型的函数，做一张主题卡片。』—— 已完成

### 2.4 Leveraging AutoCAD and Third-Party Commands

The AutoLISP command and command-s functions allow you to leverage the functionality of a standard AutoCAD command or a command defined by a loaded third-party application. Because these functions allow you to use a command, they are often some of the first functions that many new to AutoLISP learn.

NOTE: When using the command and command-s functions, keep in mind that the command being executed in most cases behaves similar to when you use it from the AutoCAD Command prompt. That means you can use many system variables to control a command's behavior or outcome. For example, you can use the clayer system variable to set a layer as current before an object is drawn or even disable running object snaps with the osmode system variable before using the line and circle commands. After you make a call to the last command and command-s function in your AutoLISP programs, be sure to restore any changed system variables to their previous values.

In Chapters 5 and 6 you learned about creating command macros. Some of the special characters used in command macros also apply to the command and command-s functions. Table 12.2 lists the special characters that can prefix a command name.

Table 12.2 Special characters that can prefix a command name

1 `.` (period). Accesses an AutoCAD command's standard definition even when a command might have been undefined with the undefine command.

2 `_` (underscore). Instructs AutoCAD to use the global command name or option value instead of the localized name or value provided. This allows the macro to function as expected when used with a different language of the AutoCAD release.

#### 2.4.1 Using the command Function

The command function passes each argument it receives to the AutoCAD Command prompt. The first argument is the name of the command to execute. After the command name are the arguments that reflect the options and values that should be executed by the command. If a command is already active when the command function is evaluated, the arguments are passed to the current command.

TIP: Before using the command function, you should test to see if a command is active by querying the current value of the cmdactive system variable with the AutoLISP getvar function. A value greater than 0 indicates a command is active. You can issue the command function without any arguments to simulate pressing Esc to get to a clean Command prompt.

1『查看一个命令是否在「激活」状态的方法，mark 一下。（2020-10-08）』

The following shows the syntax of the command function:

```c
(command [cmdname [argN …]])
```

cmdname. The cmdname argument represents the name of the command to execute. cmdname is optional.

argN. The argN argument represents the options and values that should be executed at the AutoCAD Command prompt. argN is optional. Arguments are also known as command tokens.

The following AutoLISP example assigns the coordinate values of 2,2,0 and 5,6,0 to the user-defined variables named `*apc_pt1*` and `*apc_pt2*`. The line command is then used to draw a line between the coordinate values assigned to the user-defined variables `*apc_pt1*` and `*apc_pt2*.`

```c
(setq *apc_pt1* '(2 2 0) 
    *apc_pt2* '(5 6 0)) 
(command "._line" *apc_pt1* *apc_pt2* "")
```

NOTE: The arguments that you might pass to the command function can span multiple expressions. The following produces the same results as the previous AutoLISP example code:

```c
(setq *apc_pt1* '(2 2 0) 
    *apc_pt2* '(5 6 0)) 
(command "._line") 
(command *apc_pt1* *apc_pt2* "")
```

When the command function is used, you can suspend the execution of an AutoLISP program and allow the user to provide input at the Command prompt. You use the predefined PAUSE variable or the "\\" ASCII character sequence to allow the user to provide a value. The following AutoLISP expression starts the circle command and then allows the user to specify a center point. Once a center point is specified, the circle's diameter is set to 3 units.

```c
(command "._circle" PAUSE "_d" 3)
```

2『宏命令里的悬停，做一张任意卡片。（2020-10-08）』—— 已完成

---

#### Controlling a Command's Version

Internally each standard AutoCAD command is assigned a new version number when a change is made that affects an AutoLISP program, script, or command macro. You use the initcommandversion function to control which version of a command is used by the next use of the command or command-s function. The initcommandversion function doesn't require a value, but when one is provided it must be an integer value that represents the version of the command you want to use.

The following example uses version 1 of the color command:

```c
(initcommandversion 1) 
(command "._color")
```

Version 1 of the color command displays options at the Command prompt; version 2 or later displays the Select Color dialog box instead. The -insert command is another command that is affected by the initcommandversion function. When using version 2 of the -insert command, the user can interact with the AutoCAD Properties palette in Windows while a preview of the block is being dragged in the drawing area.

1-2『真是巧了，昨天实现自动批量插入设备位号的时候才发现这个问题。当时是通过 `(setvar "ATTREQ" 1)` 实现插入块的时候交互输入属性值，插完后再将系统变量 ATTREQ 重置为 0。不过试验了下，改用 `(initcommandversion 2)` 实现了不了自动插入设备位号，目前原因不知。命令的版本号，做一张术语卡片。（2020-10-08）』—— 已完成

---

#### 2.4.2 Using the command-s Function

The command-s function is similar to the command function, with a few differences. Like the command function, the command-s function passes each argument it receives to the AutoCAD Command prompt. The first argument that is passed to the command-s function is the name of the command you want to execute. This is followed by the arguments that reflect the options and values you want executed.

When you use the command-s function, you must supply all values to complete the command that you want to execute. Unlike with the command function, you can't do either of these things:

1 Suspend the execution of an AutoLISP program and allow the user to provide input at the Command prompt with the predefined PAUSE variable.

2 Start the execution of a command in one expression and finish the command in another expression. The following is not a valid use of the command-s function: `(command-s "._circle") (command-s '(5 5) 2)`.

The following shows the syntax of the command-s function:

```c
(command-s [cmdname [argN …]])
```

cmdname. The cmdname argument represents the name of the command to execute. cmdname is optional.

argN. The argN argument represents the options and values that should be executed at the AutoCAD Command prompt. argN is optional. Arguments are also known as command tokens.

The following AutoLISP example assigns the coordinate value of 5,5,0 to the user-defined variable named `*apc_cpt*`. The circle command is then used to draw a circle using the coordinate value assigned to the user-defined variables `*apc_cpt*` and a radius of 5.

```c
(setq *apc_cpt* '(5 5 0)) (command-s "._circle" *apc_cpt* 5)
```

#### 2.4.3 Working with Commands That Display a Dialog Box

When using the command and command-s functions, avoid commands that display a dialog box because doing so can lead to inconsistencies when your AutoLISP program is executed. Instead, you should use the alternative command-line equivalent of a command, or use the system and environment variables that might be changed with the dialog box. In most cases, adding a hyphen (-) in front of a command that normally displays a dialog box will cause the command to display a series of command prompts instead. For more information, see Chapter 8 or the AutoCAD Help system.

If you need to use the dialog box that a command normally displays, you must use the AutoLISP initdia function. This function indicates to AutoCAD that the next command executed with the command or command-s function should display a dialog box, if it is supported. Using the initdia function before a command that doesn't display a dialog box has no effect on the command. The initdia function doesn't accept any arguments.

The following exercise demonstrates how the initdia function affects the use of the command function when using the plot command:

1 At the AutoCAD Command prompt, type (command "._plot") and press Enter. The plot command starts and the Detailed plot configuration? [Yes/No] <No>: prompt is displayed.

2 Press Esc to end the plot command.

3 Type `(initdia)` and press Enter. It will seem like nothing happens, but rest assured a flag has been set in the background for AutoCAD to check with the next use of the command function.

4 Type `(command "._plot")` and press Enter. The plot command starts and the Plot dialog box is displayed.

5 When the Plot dialog box opens, click Cancel.

### 2.5 Defining and Using Custom Functions

Although you can execute AutoLISP expressions one at a time at the Command prompt, doing so makes it hard to repeat or use more than a few AutoLISP expressions at a time. You can group AutoLISP expressions together into a new custom function and then execute all of the expressions in the group by using the function name you specify.

#### 2.5.1 Defining a Custom Function

The AutoLISP defun function is used to define a custom function. A custom function defined with defun behaves similar to a standard AutoLISP function, but it can also mimic a command that can be entered directly at the AutoCAD Command prompt or used in a script or command macro. Typically, a function is defined when you want to make it easier to execute and repeat a specific set of AutoLISP expressions.

The following shows the syntax of the defun function that you should follow when defining a function that doesn't need to mimic an AutoCAD command:

```c
(defun function_name ([argN] / [local_varN]) expressionN )
```

`function_name`. The `function_name` argument represents the name of the function you want to define.

argN. The argN argument represents a list of arguments that the function can accept and then act upon. argN is optional.

`local_varN`. The `local_varN` argument represents a list of user-defined variables defined in the function that should be restricted to the local scope of the function. `local_varN` is optional. Variables defined within a function have a global scope if they aren't added to the `local_varN` argument.

expressionN. The expressionN argument represents the AutoLISP expressions that should be executed by the function when it is used.

The following shows the syntax of the defun function when you want to define a function that can be accessed from the AutoCAD Command prompt, similar to a standard AutoCAD command:

```c
(defun c:function_name ( / [local_varN]) expressionN )
```

NOTE: Custom functions that have the C: prefix shouldn't accept any arguments. If your function requires any values, those values should be requested from the user with the getxxx functions. Chapter 15,「Requesting Input and Using Conditional and Looping Expressions,」discusses getting input from the user.

The following steps show how to define two custom functions: a function named dtr that converts an angular value in degrees to radians, and another named c:zw, which executes the zoom command with the Window option. These functions can be executed at the AutoCAD Command prompt.

1 At the AutoCAD Command prompt, type `(defun dtr (deg / )` and press Enter. The defun function defines a function named dtr, which accepts a single argument named deg. In this example the dtr function will use no local user-defined variables, but if you decided to, you'd list them after the forward slash.

2 Type `(* deg (/ PI 180))` and press Enter. The value assigned to the variable PI will be divided by 180 and then multiplied by the value passed into the dtr function that is assigned to the deg variable.

3 Type ) and press Enter. The AutoLISP interpreter returns the name of the function that is defined; in this case DTR is returned. This parenthesis closes the AutoLISP expression that was started with the defun function.

4 Type `(dtr 45)` and press Enter. The value 0.785398 is returned.

5 Type `(defun c:zw ( / )` and press Enter. The defun function defines a function named zw and it is prefixed with C:, indicating it can be entered at the AutoCAD Command prompt. This function doesn't accept any arguments and there are no variables that should be limited locally to this function.

6 Type `(command "._zoom" "_w"))` and press Enter. The AutoLISP interpreter returns C:ZW. The AutoLISP expression that uses the command function will be executed when the zw function is used. The command function starts the zoom command and then uses the Window option. The last closing parenthesis ends the AutoLISP expression that was started with the defun function.

7 Type zw and press Enter. You will be prompted to specify the corners of the window in which the drawing should be zoomed.

#### 2.5.2 Using a Custom Function

After you define a custom AutoLISP function with the defun function, you can execute it at either the AutoCAD Command prompt or from an AutoLISP program. Chapter 20 discusses creating AutoLISP programs. In the previous section, you defined two functions: dtr and c:zw. The following rules explain how you can execute a custom AutoLISP function defined with the defun function:

If a function name does not have the C: prefix, you must place the name of the function and any arguments that it accepts between opening and closing parentheses. It doesn't matter whether you are calling the function from the AutoCAD Command prompt or an AutoLISP program. For example, to call the dtr function defined in the previous section you would use `(dtr 45)` to call the dtr function with an argument value of 45.

If a function name has the C: prefix, you can enter the name of the function directly at the AutoCAD Command prompt without entering the C: prefix first. However, if you want to use a function that has the C: prefix from an AutoLISP program, you don't use the command or command-s function since it is not a true, natively defined AutoCAD command. Instead you must place the name of the function along with the C: prefix between opening and closing parentheses. For example, to call the C:ZW function defined in the previous section you would use (c:zw).

Functions used in a script or command macro for a user-interface element must follow the same syntax that can be entered at the AutoCAD Command prompt.

TIP: Although custom AutoLISP functions that have the C: prefix aren't recognized as native AutoCAD commands, you can use the AutoLISP vlax-add-cmd and vlax-remove-cmd functions to register a custom AutoLISP function as a built-in AutoCAD command. (These functions are available only on Windows.) There are a couple reasons you might want to do so. The first is so that your custom functions trigger events or reactors related to when a command starts or ends. The other reason is so that your custom function can be called with the command or command-s function. You can learn more about these functions in the AutoCAD Help system.

2『自定义命令变为内置命令的实现手段，做一张任意卡片。』—— 已完成

### 2.6 Example: Drawing a Rectangle

I don't introduce any new functions or techniques in this section, but I want to explain how to use many of the AutoLISP functions explored in this chapter to define a custom function that creates a new layer and draws a rectangle. I will break down each AutoLISP expression of the function in more detail in Table 12.3.

1 Create a new AutoCAD drawing.

2 At the AutoCAD Command prompt, type the following and press Enter after eac. The drawplate function draws a rectangle that is 5 × 2.75 units in size, starting at the coordinate 0,0,0.

3 Type drawplate and press Enter. Once the drawplate function completes, you'll have a rectangular object made up of four line segments on a new layer named Plate; see Figure 12.2.

4 Create a new AutoCAD drawing.

6 At the AutoCAD Command prompt, type drawplate and press Enter. The message Unknown command "DRAWPLATE". Press F1 for help. is displayed. This message is the expected result because AutoLISP entered or loaded into one drawing is accessible only to that drawing. Chapter 20 shows you how to create and load AutoLISP files.

```c
(defun c:drawplate ( / old_osmode pt1 pt2 pt3 pt4) 
  (setq old_osmode (getvar "osmode")) 
  (setvar "osmode" 0) 
  (command "._-layer" "_m" "Plate" "_c" 5 "" "") 
  (setq pt1 '(0 0 0)) 
  (setq pt2 '(5 0 0)) 
  (setq pt3 '(5 2.75 0)) 
  (setq pt4 '(0 2.75 0)) 
  (command "._line" pt1 pt2 pt3 pt4 "_c") 
  (setvar "osmode" old_osmode) 
)
```

Table 12.3 AutoLISP expressions used to define the drawplate function

`(defun c:drawplate ( / old_osmode pt1 pt2 pt3 pt4)` Uses the defun function to define the custom function drawplate, which has the prefix C: and can be executed directly at the AutoCAD Command prompt. The argument list of the defun function is empty because a function that can be entered directly at the Command prompt should not accept arguments. The forward slash character separates the argument and local variable lists. The local variable list contains five variables; these variables are added to the list so they aren't defined as global variables.

`(setq old_osmode (getvar "osmode"))` Assigns the current value of the osmode system variable to the variable named `old_osmode`.

`(setvar "osmode" 0)` Sets the osmode system variable to a value of 0.

`(command "._-layer" "_m" "Plate" "_c" 5 "" "")` Executes the -layer command with the Make option to create a layer with the name Plate. Once the layer is created (or if it already existed), the Make option sets the layer as current. The layer is also assigned the AutoCAD Color Index (ACI) value of 5.

`(setq pt1 '(0 0 0))` Assigns a list of three values that represent the coordinate value 0,0,0 to the variable named pt1.

`(setq pt2 '(5 0 0))` Assigns a list of three values that represent the coordinate value 5,0,0 to the variable named pt2.

`(setq pt3 '(5 2.75 0))` Assigns a list of three values that represent the coordinate value 5,2.75,0 to the variable named pt3.

`(setq pt4 '(0 2.75 0))` Assigns a list of three values that represent the coordinate value 0,2.75,0 to the variable named pt4.

`(command "._line" pt1 pt2 pt3 pt4 "_c")` Executes the line command and uses the values assigned to the variables pt1, pt2, pt3, and pt4 to draw three sides of a rectangle. Once the first three segments are drawing, the Close option draws the fourth and final line segment to create a closed object.

`(setvar "osmode" old_osmode)` Sets the osmode system variable to the current value of the `old_osmode` variable.

`)` Closes the defun function.

Now that you have seen the drawplate function in action, Table 12.3 provides a breakdown of what each expression is doing in the function.

## 0203. Calculating and Working with Values

Many of the standard AutoCAD® commands perform a lot of calculations as they are used from the user interface, but much of this work is shifted to you as a programmer when you work with AutoLISP®. AutoLISP supports a variety of functions that allow you to perform basic and complex math calculations, manipulate numeric or string values, and work with the elements contained in a list. I cover working with lists in Chapter 14,「Working with Lists.」

Although many of the math and data-manipulation functions in AutoLISP provide a solid foundation for working with values, you might need to combine many of these functions to create custom functions that return a value. In Chapter 12,「Understanding AutoLISP,」you learned how to create custom functions, but I didn't explain how to return a value like standard AutoLISP functions do. Later in this chapter, we'll explore how to define a custom function that returns a value using the defun function.

### 3.1 Calculating Values with Math Functions

When working with AutoCAD, you must consider the accuracy with which objects are placed and the precision with which objects are created in a drawing. The same is true with AutoLISP; you must consider both accuracy and precision when creating and modifying objects. The AutoLISP math functions allow you to perform a variety of basic and complex calculations. You can add or multiply numbers together, or even calculate the sine or arctangent of an angle.

#### 3.1.1 Performing Basic Math Calculations

When manipulating geometric properties of an object in a drawing, you often need to perform a math operation on the current value of an object and then assign that value back to the object — or even apply it to another object. Using math operations, you can manipulate an object's location, decrease a text object's height, increase an object's length or radius, and much more. The basic math functions that AutoLISP supports allow you to:

1 Add, subtract, multiply, or divide numbers.

2 Get the remainder after dividing two numbers.

3 Calculate bitwise values.

4 Get the minimum or maximum value in a range of values.

5 Determine if a value is 0 or negative.

This exercise demonstrates how to add and subtract values in AutoLISP:

1 At the AutoCAD Command prompt, type `(setq sum (+ 2 3 0.5 4))` and press Enter. All the values are added together for a final value of 9.5.

2 Type `(setq val (+ 2 (1- sum)))` and press Enter. 1 is subtracted from the value assigned to the sum user-defined variable, for a value of 8.5. Then, 2 is added to the value of 8.5 for a final value of 10.5, which is assigned to the val user-defined variable.

3 Type `(command "._circle" PAUSE val)` and press Enter. The AutoLISP command function starts the circle command and then prompts for a center point. After you provide a center point, the current value of the val user-defined variable is used for the radius of the circle.

1-3『这里宏命令里的 `PAUSE` 也可以用空字符串来替代。（2021-03-05）』

4 At the Specify radius of circle or [Diameter]: prompt, pick a point in the drawing area. The new circle is drawn.

#### 3.1.2 Adding and Subtracting Numeric Values

Adding and subtracting numbers in AutoLISP works just like you might have learned in elementary school, with one slight difference: Instead of placing a + or – operator symbol between each number as you normally would, the AutoLISP + or - function must be the first atom in a list. An atom is an element or item within a list. The + and - functions can add or subtract any number of integer or real numeric values, and they return an integer or real numeric value. An integer is returned when all the values passed to the function are integers; otherwise, a real value is returned.

The following shows the syntax of the + and - functions:

```c
(+ [numberN …]) (- [numberN …])
```

The numberN argument represents the numeric values you want to add together or subtract from each other. The numberN argument is optional and can be more than one value. If no value is passed to the + or - functions, 0 is returned. Here are some examples of adding and subtracting numbers with the + and - functions, along with the values that are returned:

```c
(+ 5 2 3) 
10 
(+ 5.0 2 3) 
10.0 
(+ 5.0 2.25 0.25) 
7.5 
(- 2 3) 
-1 
(+ (- 1.625 0.125) 1) 
2.5
```

In addition to the + and - functions, you can use the 1+ function to increment (or 1- to decrement) a value by 1. If you need to increment or decrement a value by more than 1, you will need to use the + and - functions. The 1+ and 1- functions are a great way to create a counter in a looping expression. I explain how to use looping expressions in Chapter 15,「Requesting Input and Using Conditional and Looping Expressions.」

The following shows the syntax of the 1+ and 1- functions:

```c
(1+ number) 
(1- number)
```

The number argument represents the numeric value that should be incremented or decremented by 1. Here are examples of incrementing or decrementing a number with the 1+ and 1- functions, along with the values that are returned:

```c
(setq cnt 0) 
0 
(1+ cnt) 
1 
(1- cnt) 
-1
```

#### 3.1.3 Multiplying and Dividing Numeric Values

Multiplying and dividing numeric values is an effective way to calculate a new scale factor to increase or decrease the scale factor of an object, or even to figure out how many objects of a specific size might fit into an area or along a linear path. Use the `*` function to multiply any number of integer or real numeric values and return the resulting product. Using the `/` function returns the quotient after dividing any number of numeric values. The `*` and `/` functions return an integer or real numeric value. An integer is returned by the functions when all the values passed to the function are integers; otherwise, a real numeric value is returned.

NOTE: If you divide several integer values, the value returned is an integer even if the returned value would normally have a remainder. Use at least one real number with the `/` function to return a real number with the remainder. The following shows the syntax of the `*` and `/` functions:

```c
(* [numberN …]) 
(/ [numberN …])
```

The numberN argument represents the numeric values you want to multiply or divide by each other. The numberN argument is optional and can be more than one value. If no value is passed to the `*` or `/` function, 0 is returned. Here are examples of multiplying and dividing numbers with the `*` and `/` functions, along with the values that are returned:

```c
(* 5 3) 
15 
(* 5.0 2 3) 
30.0 
(/ 5 2) 
2 
(/ 5.0 2) 
2.5
```

NOTE: Dividing a number by 0 causes an error and returns this message: `; error: divide by zero`. If the error is not handled, the custom function that contains the error is terminated. You can use the `vl-catch-all-apply` function to keep the function from being terminated. I discuss the `vl-catch-all-apply` function in Chapter 19,「Catching and Handling Errors.」

When dividing numbers, you can use the AutoLISP `rem` function to return the remainder of the first number after it has been divided by all the other numbers supplied to the function. The `rem` function can take any number of numeric values; the function returns 0 when no values are passed to it. The following demonstrates the rem function:

```c
(/ 10.0 3) 
3.33333 
(rem 10.0 3.0) 
1.0
```

AutoLISP includes a function named `gcd` that can be used to return the greatest common denominator of two integer values. The gcd function requires two integer values, and it returns an integer that represents the greatest common denominator of the provided values. Here are two examples:

1-2『这不是就是求最大公约数嘛，数学应用很广的，以后应该可以用到。函数 rem 和 gcd 收录进主题卡片「函数收藏」中。（2021-03-06）』—— 已完成

```c
(gcd 5 2) 
1 
(gcd 54 81) 
27
```

#### 3.1.4 Using Other Basic Math Functions

Most of your math function needs should be met with the basic math functions that I previously covered, but you should be aware of some other basic math functions. These other functions allow you to get the minimum or maximum number in a range of values or determine if a numeric value is equal to 0 or is negative.

The following explains some of the other basic math functions that are available as part of AutoLISP:

1 min and max.

The min and max functions accept any integer or real numeric values. The min function returns the smallest numeric value from those that are passed to it, whereas the max function returns the largest numeric value. A real value is returned by the function, except when the function is passed only integer values — in that case, an integer value is returned. If no numeric value is passed to either function, 0 is returned. The following are examples of the min and max functions:

```c
(min 9 1 1976 0.25 100 -25) 
-25.0
(max 9 1 1976 0.25 100 -25) 
1976.0 
(max 9 1 1976 100 -25) 
1976
```

2 minusp and zerop.

The minusp and zerop functions accept an integer or real numeric value. The minusp function returns T if the value that it was passed is negative, or it returns nil if the value was positive. The zerop function also returns T or nil; T is returned if the value passed is equal to 0. The zerop function can help you avoid dividing a number by 0 or seeing if a system variable is set to 0. The following are examples of the minusp and zerop functions:

```c
(minusp 25) 
nil 
(minusp -25) 
T 
(zerop 25) 
nil 
(zerop 0) 
T
```

For more information on the minusp and zerop functions, see the AutoCAD Help system.

2『求最大最小值函数、判断负值、判断零值函数，收录进主题卡片「函数收藏」。（2021-03-06）』—— 已完成

#### 3.1.5 Performing Advanced Math Calculations

In addition to basic math functions, AutoLISP offers a range of advanced math functions that aren't used as frequently. These advanced functions allow you to work with angular, exponential, natural logarithm, or square root numeric values. AutoLISP supports the advanced math functions listed in Table 13.1.

1-2『真没想到，autolisp 里原生数学函数这么丰富。这些高阶函数都收录进主题卡片「函数收藏」。（2021-03-06）』—— 已完成

Table 13.1 AutoLISP advanced math functions

| Function | Description |
| --- | --- |
| sin | Returns the sine of an angular value expressed in radians. |
| atan | Calculates the arctangent of an angular value expressed in radians. |
| cos | Returns the cosine of an angular value expressed in radians. |
| exp | Returns a numeric value that has been raised to its natural antilogarithm. |
| expt | Returns a numeric value after it has been raised by a specified power. |
| log | Calculates the natural logarithm of a numeric value. |
| sqrt | Gets the square root of a numeric value. |
| - | - |

For more information on these functions, see the AutoCAD Help system.

#### 3.1.6 Working with Bitwise Operations

Integer values can be used to represent what is known as a bit pattern or bit-coded value. A bit-coded value is the sum of one or more bits. A bit is a binary value; when one or more bits are combined they create a unique sum. AutoCAD uses bit-coded values for many different object properties (DXF group codes) and system variables.

2『这里的 bit-coded values 做一张术语卡片。（2021-03-06）』—— 已完成

For example, the layer status property (DXF group code 70) of a layer is a bit-coded value that contains various flags used to specify whether the layer is frozen (1 bit), locked (4 bit), or dependent on an xref (16 bit). The osmode system variable is another example of a bit-coded value in AutoCAD. In the osmode system variable, the value indicates which running object snaps are currently enabled. Refer to the AutoCAD Help system to determine whether an object property or system variable is an integer or bit-coded value.

1『这里意外获取到，图层锁定状态的 DXF 码，哈哈。收入进主题卡片「常用 DXF 码」。（2021-03-06）』

Because a bit-coded value is represented by the integer data type, you can use the `+` and `–` functions to add or remove a bit value for the overall sum of a bit-coded value. AutoLISP also provides several useful functions that you can use when working with bit-coded values. The logior and logand functions help combine several bit-coded values and determine whether a bit is part of a bit-coded value. Let's take a closer look at the logior and logand functions.

2『函数 logior、函数 logand，收录进主题卡片「函数收藏」。（2021-03-06）』—— 已完成

1 logior. The logior function allows you to combine several bits into a single bit-coded value and ensures that a bit is added only once to the resulting bit-coded value. Although you can use the `+` function to add several bits together, that function simply adds several values together and returns the resulting value, which might return a bit-coded value with a different meaning. For example, the bits 1 and 4 are equal to the bit-coded value of 5:

```c
; Final result is a bit-coded value of the bits 1 and 4 
(logior 1 4) 
5 
; Final result is an integer of 5 
(+ 1 4) 
5
```

Adding the bits 1, 2, and 5 with the logior function results in the bit-coded value of 7.

```c
; Final result is a bit-coded value of the bits 1, 2, and 4 
(logior 1 2 5) 
7
```

Were you expecting a value of 8 maybe? The 1 bit is added only once because the logior function recognizes that the 1 bit is provided individually and as part of the bit-coded value of 5 in the previous example. If you were to add the same numbers (1, 2, and 5) together with the `+` function, the result would be 8 and would mean something different. A value of 8 is a bit in and of itself.

```c
; Final result is an integer of 8 and not a bit-coded value of the bits 1, 2, and 4 
(+ 1 2 5) 
8
```

Here is the syntax of the logior function:

```c
(logior [bitN …])
```

The bitN argument represents the bits you want to combine. If no bit is passed to the function, 0 is returned.

The following examples add the provided bits together into a bit-coded value of 35 with the logior function. The bits 1, 2, and 32 represent the ENDpoint, MIDpoint, and INTersection running object snap settings. The second expression returns a value of 35 as well, and because 3 is a bit-coded value that represents both bits 1 and 2, the logior function will add a bit only once to the bit-coded value it returns. If you used the `+` function instead, it would be easy to add a bit more than once to a bit-coded value.

```c
; Returns the sum of the bits 1, 2, and 32 
(setq new_osmode (logior 1 2 32)) 
35 
; Returns the sum of the bits 1, 2, 3, and 32 
; Bit 3 is a bit-coded value containing 1 and 2 
(logior 1 2 3 32) 35
```

2 logand. The logand function is used to determine whether a specific bit or bit-coded value is part of another bit-coded value. This type of comparison in a program can be helpful when you need to handle specific conditions in the AutoCAD environment, such as making sure that the current layer is not frozen or locked when you're creating or selecting objects, or making sure a specific running object snap is set. Here is the syntax of the logand function:

1-2『这里提供了实现自动锁图层的实现线索，待研究。之前开发建筑底图迁移功能时，已经通过 activeX 实现了，这里的信息如果实现，应该是另外一条途径。（2021-03-06）』

```c
(logand [bitN …])
```

The bitN argument represents the bits you want to test for comparison. If no value is passed to the function, 0 is returned.

The following examples use the logand function to determine if a bit is common with the provided bits or bit-coded values. Bit 2 represents the MIDpoint running object snap; a bit-coded value of 12 represents the CENter and QUAdrant running object snaps; and the bit-coded value of 34 represents the running object snaps MIDpoint and INTersection. The first example returns 0 because the bit 2 value is not part of the bit-coded value 12 (bit codes 4 and 8), whereas 2 is returned for the second example because bit 2 is part of the bit-coded value of 34 (bit codes 1, 2, and 32).

```c
; Returns 0 because no bit codes are in 
; common with the two numbers 
(logand 2 12) 
0 
; Returns 2 because it is the common bit code 
; in common with both numbers 
(logand 2 34) 
2s
```

If you want to add or remove a bit to or from a bit-coded value, you can use logand to verify whether a bit is already part of the bit-coded value. If 0 is returned by logand, the bit code is not part of the bit-coded value, so the bit could safely be added with the `+` function. If the bit is returned instead of 0, the bit is part of the bit-coded value and can be safely removed using the `-` function.

#### 3.1.7 Other Bitwise Functions

In addition to the AutoLISP logior and logand functions, you can use these functions when working with bit-coded values:

1 `˜` (Bitwise NOT). The `˜` (bitwise NOT) function accepts a bit (integer) value and converts it into a binary number before performing a bitwise negation. The negation changes any 1 in the binary value to a 0, and any 0 to a 1. For example, an integer value of 32 expressed as a binary value is as follows:

```
0000 0000 0000 0000 0000 0000 0000 0000 
0000 0000 0000 0000 0000 0000 0010 0000
```

The binary value is read from lower right to upper left. When the ˜ (bitwise NOT) function is applied to a bit value of 32, it becomes a bit value of –33 and is expressed as the binary value

```
1111 1111 1111 1111 1111 1111 1111 1111 
1111 1111 1111 1111 1111 1111 1101 1111
```

The following is an example of the ˜ (bitwise NOT) function:

```c
(˜ 32) 
-33
```

2『竟然还有这个取负数的函数，这样以后不用自己用 0 减生成负数了。收录进主题卡片「函数收藏」。（2021-03-06）』—— 已完成

2 boole. The AutoLISP boole function is used to perform a Boolean operation on two bit-coded (integer) values. The Boolean operations that can be performed are `AND(1)`, `XOR(6)`, `OR(7)`, and `NOR(8)`. For example, the AND Boolean operation can be used to see which bits are common between two bit-coded values. If an AND Boolean operation is performed on the bit-coded values 55 and 4135, a bit-coded value of 39 is returned.

The following is an example of the boole function:

```c
(boole 1 55 4135) 
39
```

1-2『选择器过滤条件的实现，底层原理应该靠的就是它，但目前没吃透。收录进主题卡片「函数收藏」。（2021-03-06』—— 已完成

3 lsh. The AutoLISP lsh function accepts a bit (integer) value and converts it into a binary number before performing a bitwise shift by a specified number of bits. For example, you can shift the bit value of 1 by 3 bits to return the 8 bit value. A bit value of 1 is expressed as the binary value 1000 0000 (read left to right); the bitwise shift moves the 1 three bits to the right and it becomes a binary value of 0001 0000, or a bit value of 8.

The following is an example of the lsh function:

```c
(lsh 1 3) 
8
```

For more information on the `˜` (bitwise NOT), boole, and lsh functions, see the AutoCAD Help system.

#### 3.1.8 Working with Bit-Coded Values

The following exercise demonstrates how to work with bit-coded values. You'll create a custom function that allows you to toggle the state of the INTersection object snap. The current running object snap modes are stored in the osmode system variable, which contains a bit-coded value. The INTersection object snap is represented by the bit code 32.

1 At the AutoCAD Command prompt, type `(setq cur_osmode (getvar "osmode"))` and press Enter. The current value of the osmode system variable is assigned to the `cur_osmode` user-defined variable.

2 Type `(logand 32 cur_osmode)` and press Enter. The value 32 or 0 is returned. If 32 is returned, then the INTersection object snap mode is enabled.

3 Type osnap and press Enter.

4 When the Drafting Settings dialog box opens, verify the current state of the Intersection check box based on the results you got in step 2. Click Cancel. If 32 is returned by the logand function in step 2, the Intersection check box should be checked; otherwise it will be unchecked.

5 Type the following and press Enter: 

```c
(defun c:ToggleINT ( / cur_osmode) 
  (setq cur_osmode (getvar "osmode")) 
  (if (= (logand 32 cur_osmode) 0) 
    (setvar "osmode" (logior 32 cur_osmode)) 
    (setvar "osmode" (- cur_osmode 32)) 
  ) 
  (princ) 
)
```

6 Type toggleint and press Enter. The custom function checks the bit-coded value of the osmode system variable to see if bit code 32 is part of the value. If bit code 32 is not part of the bit-coded value, 32 is added to the current value of the osmode system variable with the logior function. Otherwise, 32 is subtracted from the osmode system variable.

7 Open the Drafting Settings dialog box and verify that the state of the Intersection check box has been changed. Click Cancel.

8 Type toggleint and press Enter. The previous state of the INTersection object snap mode is restored.

### 3.2 Manipulating Strings

Strings are used for a variety of purposes in AutoLISP, from displaying command prompts and messages to creating annotations in a drawing. The string values in an AutoLISP program can have a static or fixed value that never changes during execution, or a value that is more dynamic and is changed by the use of string-manipulation functions. You can manipulate a string by:

1 Concatenating two or more strings together.

2 Getting the number of characters or their position in a string.

3 Replacing characters in a string.

4 Removing characters from or truncating a string.

5 Trimming empty spaces or other characters from the ends of a string.

6 Changing the case of and evaluating the values of a string.

This exercise demonstrates how to concatenate and manipulate strings in AutoLISP:

1 At the AutoCAD Command prompt, type `(setq str1 "String:")` and press Enter. The string "String:" is assigned to the str1 user-defined variable.

2 Type `(setq str2 "\"Sample\"")` and press Enter. The string "\"Sample\""" is assigned to the str2 user-defined variable.

3 Type `(setq mtline1 (strcat str1 " " str2))` and press Enter. A new string value of "String:\"Sample\"" is returned and assigned to the mtline1 user-defined variable.

4 Type `(setq mtline2 (strcat "Length: " (itoa (strlen str2))))` and press Enter. A new string value of "Length: 8" is returned and assigned to the mtline2 user-defined variable.

5 Type `(command "mtext" PAUSE PAUSE (strcat mtline1 "\\P" mtline2) "")` and press Enter. The mtext command is started and you are prompted for the two corners of the multiline text boundary.

6 At the Specify first corner: prompt, pick a point in the drawing.

7 At the Specify opposite corner or [Height/Justify/Line spacing/Rotation/Style/Width/Columns]: prompt, pick a point in the drawing. The new multiline text object is created and should look like Figure 13.1.

Figure 13.1 Multiline text object created from multiple string values

I discuss the strcat and strlen functions in the following sections, along with many other functions related to working with strings. The section「Converting Data Types」later in this chapter explores the itoa function used to convert an integer to a string.

#### 3.2.1 Concatenating Strings

Two or more strings can be concatenated (combined) into a string value that can then be presented to the user or used by another function. There are many different reasons why you might combine two or more strings. Some of the most common reasons follow:

1 To define an absolute file location based on a path and filename.

2 To write a string value out to a file.

3 To create a prompt based on a fixed string value and a recently entered string or numeric value that was converted to a string.

4 To build a field or multiline text value using special characters that can then be displayed using an MText object.

5 The AutoLISP strcat (short for string concatenation) function is used to concatenate multiple strings together. The following shows the syntax of the strcat function:

```c
(strcat [stringN …])
```

The stringN argument represents the strings that should be concatenated together to form the resulting string. The stringN argument is optional. If no argument is provided, an empty string represented by a pair of quotation marks ("") is returned.

The following demonstrates the strcat function and the values that are returned:

```c
(setq str1 "Hello" str2 "AutoLISP!") 
(strcat str1 str2) 
"HelloAutoLISP!" 
(strcat str1 " from " str2) 
"Hello from AutoLISP!" 
(setq kwd1 "Plate" kwd2 "Bolt" *prev_kwd* "Plate") 
(strcat "\nEnter object to place [" kwd1 "/" kwd2 "] <" *prev_kwd* ">: ") 
"\nEnter object to place [Plate/Bolt] <Plate>: "
```

### 3.2.2 Getting the Length of and Searching for Strings

When working with strings, you may want to know the number of characters in a string or the position in which a text pattern begins. You can use the length of a string to make sure a string doesn't exceed a specific number of characters, to remove characters from the end of a string, or to insert a string at a known location.

#### Returning the Length of a String

The AutoLISP strlen (short for string length) function returns the number of characters in a string. The following shows the syntax of the strlen function:

```c
(strlen [string])
```

The string argument represents the string for which you want to know the length; the length is returned as an integer. Spaces in a string are counted as one character. The string argument is optional, and a length of 0 is returned if no argument is provided. The following are examples of the strlen function and the values that are returned:

```c
(strlen "Hello") 
5 
(strlen " Hello ") 
9 
(strlen "Product: %product%") 
18
```

#### Searching for a Text Pattern in a String

In addition to wanting to know the number of characters in a string, you might want to know if a specific text pattern is contained in a string. This can be helpful if you want to create a custom find and replace program for text contained in an annotation object. The AutoLISP `vl-string-search` function takes a text pattern and compares that pattern to a string. The position at which the text pattern begins in the string is returned as an integer. If the text pattern is not found, nil is returned. The first character in a string is located in the 0 position. A string can contain multiple instances of the text pattern, but the `vl-string-search` function only returns the start position of the first instance of the text pattern. The following shows the syntax of the `vl-string-search` function:

```c
(vl-string-search pattern string [start])
```

The arguments are as follows:

1 pattern. The pattern argument represents the text pattern that you want to search for in the string argument. The text pattern is case sensitive.

2 string. The string argument represents the string that you want to search.

3 start. The start argument represents the starting position in the string argument where you want to begin searching for the text pattern specified by the pattern argument. The start argument is optional. If no argument is provided, searching for the text pattern starts at the 0 position.

The following are examples of the vl-string-search function and the values that are returned:

```c
(vl-string-search "product" "Product: %product%") 
10 
(vl-string-search "Product" "Product: %product%") 
0 
(vl-string-search "program" "Product: %product%") 
nil
```

Although the `vl-string-search` function can be used to search a string for a text pattern, the function is limited to searching only for that text pattern and in the case specified. If you have a need to search a string for multiple text patterns, the `vl-string-search` function is not very efficient by itself. You can use the `wcmatch` (short for wildcard match) function to help search a string for more complex text patterns with the use of wildcard pattern matching.

However, unlike the `vl-string-search` function, the `wcmatch` function returns T only if the wildcard pattern matches part or all of the string; otherwise, nil is returned if no match is found. If a match is found, it is up to you to try to find the text in the string that was matched. You can use the AutoLISP `substr` function along with a looping expression to get down to the substring that is a match. You'll learn more about the `substr` function in the「Replacing and Trimming Strings」section later in this chapter, and more about looping expressions in Chapter 15.

The following shows the syntax of the wcmatch function:

```c
(wcmatch string pattern)
```

The arguments are as follows:

1 string. The string argument represents the string that you want to search.

2 pattern. The pattern argument represents the wildcard text pattern that you want to search for in the string argument. For information on the wildcard characters that are supported, see the「wcmatch」topic in the AutoCAD Help system.

Here are examples of the wcmatch function and the values that are returned:

```c
(wcmatch "W6X12" "W#X12") 
T 
(wcmatch "W*6" "W#X12") 
nil
```

The AutoLISP `strlen`, `vl-string-search`, and `wcmatch` functions are all helpful in learning more about the length or characters in a string. Here are two additional functions that can be useful in finding out what characters are in a string:

`vl-string-position` Returns the position of a character in a string.

`vl-string-mismatch` Returns the length of the characters that are at the beginning of and in common between two strings.

For more information on these functions, see the AutoCAD Help system.

#### 3.2.3 Replacing and Trimming Strings

In the previous section, I mentioned how the vl-string-search and wcmatch functions can be used to determine whether a text pattern exists in a string. After you know that the text pattern is in a string, you can use that information to split a string into two strings based on the text pattern's location, replace a matching text pattern with a new string, or remove the string that matches a text pattern. Along with working with a string based on the results of a matched text pattern, you can trim spaces or specific characters off the ends of a string.

3『

数据流里的一个功能函数：

```c
; Changes all "pattern"s to "newSubst". Like vl-string-subst, but replaces
; ALL instances of pattern instead of just the first one.
; Argument: String to alter.
; Return: Altered string.
(defun DL:ReplaceAllSubst (newSubst pattern string / pattern)
	(while (vl-string-search pattern string)
		(setq
			string
			(vl-string-subst newSubst pattern string)))
	string
)
```

』

#### Replacing a Text Pattern in a String

A text pattern or set of characters in a string can be replaced with a new string or set of characters, making it easy to update an out-of-date part number or even a basic implementation of inline variable expansion. For additional information on inline variable expansion, see the「What Is Inline Variable Expansion?」sidebar.

#### What Is Inline Variable Expansion?

Inline variable expansion is the process of defining a variable and then adding the name of the variable using the format `%VARIABLE_NAME%` (Windows) or `${VARIABLE_NAME}` (Mac OS) in a string. The name of the variable is then replaced with the variable's actual value when the expression containing the string is used. Inline variable expansion is not native functionality in AutoLISP, but it can be simulated. Inline variable expansion is supported by other programming languages and is often used with values that are defined by the operating system. Listing 13.1 in this section demonstrates one possible implementation of inline variable expansion in AutoLISP.

1『太惊喜了，autolisp 里竟然也能模拟内联变量，那种很常用的，嵌入在字符串里的变量，感谢作者的源码，哈哈。做一张术语卡片。（2021-03-06）』

The AutoLISP `vl-string-subst` (short for string substitution) function is commonly used to replace a text pattern in a string. Only the first instance of the matching text pattern is replaced, so you might need to run the `vl-string-subst` function several times on a string.

The following shows the syntax of the vl-string-subst function:

```c
(vl-string-subst new_string pattern string [start])
```

The arguments are as follows:

1 `new_string`. The `new_string` argument represents the string that you want to use as the replacement value if the text pattern specified by the pattern argument is found in the string argument.

2 pattern. The pattern argument represents the text pattern that you want to search for in the string argument.

3 string. The string argument represents the string that you want to search.

4 start. The start argument represents the starting position in the string argument that you want to begin searching for the text pattern specified by the pattern argument. The start argument is optional. If no argument is provided, searching for the text pattern starts at the first position.

The following are examples of the vl-string-subst function and the values that are returned:

```c
(vl-string-subst "career" "hobby" "Programming is my hobby.") 
"Programming is my career." 
(vl-string-subst "_" " " "Project 123 - ABC") 
"Project_123 - ABC"
```

Listing 13.1 is a custom function that mimics the use of inline variable expansion. When the function is executed, it attempts to match the text between % (percent) signs with a user-defined variable. If the variable is found, the inline variable is replaced by its current value.

Listing 13.1: The ExpandVariable function

```c
; Custom implementation of expanding variables in AutoLISP 
; To use: 
; 1. Define a variable with the setq function. 
; 2. Add the variable name with % symbols on both sides of the variable name. 
; For example, the variable named *program* would appear as %*program*% in the string. 
; 3. Use the function on the string that contains the variable. 
(defun expandvariableUtils (string / start_pos next_pos var2expand expand_var) 
  (while (wcmatch string "*%*%*") 
         (progn 
          (setq start_pos (1+ (vl-string-search "%" string))) 
          (setq next_pos (vl-string-search "%" string start_pos)) 
          (setq var2expand (substr string start_pos (- (+ next_pos 2) start_pos))) 
          (setq expand_var (vl-princ-to-string (eval (read (vl-string-trim "%" var2expand))))) 
          (if (/= expand_var nil) 
            (setq string (vl-string-subst expand_var var2expand string)) 
          ) 
         ) 
  ) 
  string 
) 

; Define a global variable and string to expand 
(setq *program* (getvar "PROGRAM") str2expand "PI=%PI% Program=%*program*%" ) 
; Execute the custom function to expand the variables defined in the string 
(expandvariable str2expand) 
"PI=3.14159 Program=acad"
```

Along with the `vl-string-subst` function, you can use the `vl-string-translate` function to replace all instances of a character anywhere in a string with another character. Since the `vl-string-translate` function works with single characters, it provides much less control over using a text pattern that contains multiple characters.

The following example demonstrates how the `vl-string-translate` function can be used to replace all of the spaces in a string with underscores:

```c
(vl-string-translate " " "_" "Project 123 - ABC") 
"Project_123_-_ABC"
```

For more information on the `vl-string-translate` function, see the AutoCAD Help system.

#### Trimming a String

A string can be trimmed to a specific length by specifying a starting position and the number of characters to keep, resulting in what is known as a substring. The AutoLISP substr (short for substring) function allows you to keep a set of characters from a given string. The following shows the syntax of the substr function:

```c
(substr string start [length])
```

The arguments are as follows:

1 string. The string argument represents the string that contains the substring you want to return.

2 start. The start argument represents the starting position in the string argument that the substring begins. A string starts at the first position.

3 length. The length argument represents the number of characters the substring should contain. The length argument is optional. If no argument is provided, the substring contains all of the characters from the starting position specified by the start argument to the end of the string.

The following are examples of the substr function and the values that are returned:

```c
(substr "Programming is my hobby." 12) 
" is my hobby." 
(substr "Programming is my hobby." 1 11) 
"Programming" 
(substr "Programming is my hobby." 19 5) 
"hobby"
```

Although the substr function is very helpful in pulling a string apart, it is not the most efficient function to use if you need to remove or trim specific characters from the left or right ends of a string. The AutoLISP `vl-string-trim`, `vl-string-left-trim`, and `vl-string-right-trim` functions are better suited to trimming specific characters, such as extra spaces or zeroes, from the ends of a string. The `vl-string-trim` function trims both ends of a string, whereas the `vl-string-left-trim` and `vl-string-right-trim` functions trim only the left and right ends of a string, respectively. Characters that are part of the `character_set` argument are trimmed from the respective ends of the string until a character that isn't a part of the `character_set` argument is encountered.

1『每个语言都看到这 3 个剔除函数，底层的实现原理应该都一样。每个语言都有说明应用场景肯定多。（2021-03-06）』

The following shows the syntax of the `vl-string-trim`, `vl-string-left-trim`, and `vl-string-right-trim` functions:

```c
(vl-string-trim character_set string) 
(vl-string-left-trim character_set string) 
(vl-string-right-trim character_set string)
```

The arguments are as follows:

1 `character_set`. The `character_set` argument represents the characters on the end or ends of the string specified by the string argument that should be trimmed off.

2 string. The string argument represents the string that should be trimmed based on the characters specified by the `character_set` argument.

The following are examples of the `vl-string-trim`, `vl-string-right-trim` and `vl-string-left-trim`, functions and the values that are returned:

```c
(vl-string-trim " " " Extra spaces ")
 "Extra spaces" 
 (vl-string-right-trim ".0" "Trailing Zeroes and Spaces 0.10000 ") 
 "Trailing Zeroes and Spaces 0.1" 
 (vl-string-right-trim ".0" "Trailing Zeroes and Spaces 1.0000 ") 
 "Trailing Zeroes and Spaces 1" 
 (vl-string-left-trim " 0" " 001005 Leading Zeroes and Spaces") 
 "1005 Leading Zeroes and Spaces"
```

1『结合文档的例子，发现 `character_set` 几个有趣的地方：1）可以是多个字符组成的字符串，最右侧字符只要有满足的，都会剔除。2）没有顺序要求。（2021-03-06）』

#### 3.2.4 Changing the Case of a String

The text in most annotation objects of a drawing file is in all uppercase letters. However, the text that a user might enter at a Command prompt might be in uppercase, lowercase, or even mixed-case letters. The AutoLISP strcase (short for string case) function can be used to convert all of the letters in a string to either uppercase or lowercase. The following shows the syntax of the strcase function:

```c
(strcase string [lowercase])
```

The arguments are as follows:

1 string. The string argument represents the string that you want to convert to all uppercase or lowercase letters.

2 lowercase. The lowercase argument, when provided, indicates that all the letters should be converted to lowercase. T is typically provided as the value for this argument. Using a value of T indicates that the string argument should be converted to all lowercase letters.

The following are examples of the strcase function and the values that are returned:

```c
(setq str_convert "StRiNg") 
(strcase str_convert) 
"STRING" 
(strcase str_convert T) 
"string"
```

The strcase function can't be used to convert specific letters of a string to sentence or title case. However, if you need that type of functionality, you can use the subst and strcase functions to do get the desired results. For example, in the case of wanting to convert a string to sentence case, you can use the substr function to get the first character of a string and then get the remaining characters of a string. After you get the two parts of the string you can then change their case with the strcase function and concatenate the two strings back together with the strcat function.

Listing 13.2 is an example of a custom AutoLISP function that could be used to convert a text string to sentence case.

Listing 13.2: The sentencecase function

```c
; Converts a string to sentence case 
; (sentencecase "string") 
(defun sentencecase (string / ) 
  (strcat 
    (strcase (substr string 1 1)) 
    (strcase (substr string 2 (1- (strlen string))) T) 
  ) 
) 
(sentencecase "THIS IS A SAMPLE SENTENCE.") 
"This is a sample sentence."
```

#### 3.2.5 Evaluating Values to Strings

When working with strings, you may also want to concatenate a numeric value as part of a prompt string or response to the user. Before you can concatenate a nonstring value to a string, you must convert the nonstring value to a string. The quickest way to do so is to use the AutoLISP `vl-princ-to-string` and `vl-prin1-to-string` functions.

The difference between the two functions is how quotation marks, backslashes, and other control characters are represented in the string that is returned. The `vl-prin1-to-string` function expands all control characters, whereas the `vl-princ-to-string` function doesn't. For more information on control characters that can be used in strings, search on the keywords「control characters」in the AutoCAD Help system.

The following shows the syntax of the `vl-princ-to-string` and `vl-prin1-to-string` functions:

```c
(vl-princ-to-string atom) 
(vl-prin1-to-string atom)
```

The atom argument represents the expression, variable, or value that should be converted to and returned as a string. The following are examples of the `vl-princ-to-string` and `vl-prin1-to-string` functions, and the values that are returned:

```c
(vl-princ-to-string 1.25) 
"1.25" 
(vl-princ-to-string (findfile (strcat (getvar "PROGRAM") ".exe"))) 
"C:\\Program Files\\Autodesk\\AutoCAD 2014\\acad.exe" 
(vl-prin1-to-string 1.25) 
"1.25" 
(vl-prin1-to-string (findfile (strcat (getvar "PROGRAM") ".exe"))) 
"\"C:\\\\Program Files\\\\Autodesk\\\\AutoCAD 2014\\\\acad.exe\""
```

I discuss other AutoLISP functions that can be used to convert nonstring values to strings and strings to nonstring values next.

### 3.3 Converting Data Types

Variables in AutoLISP aren't defined to hold a specific data type, which allows the variable to be flexible and hold any valid type of data. However, data types are used by AutoLISP as a way to enforce data integrity and communicate the types of values an argument expects or a function might return. As your programs become more complex and you start requesting input from the user, there will be times when a function returns a value of one data type and you want to use that value with a function that expects a different data type.

I explained the use of the `vl-princ-to-string` and `vl-prin1-to-string` functions earlier, but those functions simply convert most values to a string. AutoLISP also contains many other conversion functions that allow you to convert the following:

1 Numeric values to strings.

2 Strings to numeric values.

3 Numeric values to other number types.

4 Lists to strings and strings to lists.

You'll learn how to convert lists to strings and strings to lists in Chapter 14.

#### 3.3.1 Converting Numeric Values to Strings

Numbers are the most commonly used data type in AutoLISP because you are often working with the size of any object, positioning an object in a drawing, or counting objects to generate a bill of materials. The reason you might want to convert a numeric value to a string is to add a value to a prompt string, create a text string for an annotation object, or write a value out to an external file.

Table 13.2 lists the available functions for converting a numeric value to a string.

Table 13.2 AutoLISP functions for converting numeric values to strings

| Function | Description |
| --- | --- |
| angtos | The angtos function accepts a numeric value, integer or real number, which represents an angle in radians. Optionally, you can specify the unit that the angle should be converted into along with a precision. The function returns a string based on the angular value, unit, and precision arguments specified. You can use the AutoLISP angtof function to reverse the conversion. |
| rtos | The rtos function accepts a numeric value, integer or real number, which represents a distance. Optionally, you can specify the linear unit that the distance should be converted into along with a precision. The function returns a string based on the linear value, unit, and precision arguments specified. You can use the AutoLISP atof function to reverse the conversion. |
| itoa | The itoa function accepts an integer and returns a string value of the converted integer value. If a real number is passed to the function, the ; error: bad argument type: fixnump: error message is displayed. You can use the AutoLISP atoi function to reverse the conversion. |
| chr | The chr function accepts an ASCII code, which is an integer value, and returns the character equivalent of the ASCII code value. If a real number is passed to the function, the ; error: bad argument type: fixnump: error message is displayed. You can use the AutoLISP ascii function to reverse the conversion. |

The following are examples of the angtos, rtos, itoa, and chr functions, and the values they return:

```c
(angtos (/ PI 2)) 
"90" 
(angtos (/ PI 6) 0 5) 
"30.00000" 
(rtos 1.375) 
"1.3750" 
(rtos 1.375 4) 
"1 3/8\"" 
(rtos 1.375 3 4) 
"1.3750\"" 
(itoa -25) 
"-25" 
(itoa 5) 
"5" 
(chr 32) 
" " 
(chr 65) 
"A"
```

1『竟然还能控制精度的，不错。（2021-03-06）』

For more information on these functions, see the AutoCAD Help system.

#### 3.3.2 Converting Strings to Numeric Values

You can use string values for prompts and messages to the user, as you saw earlier. You can store string values with annotation objects, and you can also read a part number from an external data file and assign that value to an attribute in a block. Even though a string value is between quotation marks, it can still represent a numeric value. Before you use a string that contains a number with a function that expects a numeric value, you must convert that string to a numeric value.

Table 13.3 lists the AutoLISP functions that can be used to convert a string to a numeric value.

Table 13.3 AutoLISP functions for converting strings to numeric values

| Function | Description |
| --- | --- |
| angtof  | Accepts a string that represents an angular value. Optionally, you can specify the unit that defines the formatting of the number in the string. The function returns a real number based on the value in the string and the unit argument that is specified. You can use the AutoLISP angtos function to reverse the conversion. |
| atof | Accepts a string that represents a numeric value and returns a real number based on the value in the string. You can use the AutoLISP rtos function to reverse the conversion. |
| distof | Accepts a string that represents a distance value. Optionally, you can specify the unit that defines the formatting of the number in the string. The function returns a real number based on the value in the string and the unit argument that is specified. You can use the AutoLISP rtos function to reverse the conversion. |
| atoi | Accepts a string that represents a numeric value and returns an integer based on the value in the string. You can use the AutoLISP itoa function to reverse the conversion. |
| ascii | Accepts a string and returns an integer that represents the ASCII code value of the first character in the string. Although the string can be more than one character, only the first character is converted. You can use the AutoLISP chr function to reverse the conversion. |
| vl-string-elt | Accepts a string and returns an integer that represents the ASCII code value of the character at the specified position in the string. You can use the AutoLISP chr function to reverse the conversion. |

The following are examples of the angtof, atof, distof, atoi, ascii, and vl-string-elt functions, and the values they return:

```c
(angtof "90") 
1.5708 
(angtof "30.00000" 0) 
0.523599 
(atof "1.3750") 
1.375 
(distof "1 3/8\"" 4) 
1.375 
(distof "1.3750\"" 3) 
1.375 (atoi "-25") 
-25 
(atoi "5") 
5 
(atoi "5th Place") 
5 (ascii " ") 
32 
(ascii "A") 
65 
(vl-string-elt "Programming" 4) 
114
```

For more information on these functions, see the AutoCAD Help system.

#### 3.3.3 Converting Numeric Values to Other Number Types

There are times when you have to work with an integer or a real number, even if a function returns a different numeric data type. In addition to converting integers to reals or reals to integers, you can also convert a negative number to a positive number.

Table 13.4 explains the functions that can be used to convert one numeric value to another.

Table 13.4 AutoLISP functions for converting numeric values

| Function | Description |
| --- | --- |
| fix | Accepts a numeric value, integer or real number, and returns the nearest integer after discarding the value after the decimal place. |
| float | Accepts a numeric value, integer or real number, and returns a real number. |
| abs | Accepts a numeric value, integer or real number, and returns the absolute value of the numeric value. The absolute value is a positive value, never negative. You can also multiply a numeric value by –1 to convert a positive to a negative numeric value or a negative to a positive numeric value. The AutoLISP minusp function can be used to determine whether a numeric value is negative. |

The following are examples of the fix, float, and abs functions, and the values they return:

```c
(fix -25) 
-25 
(fix 25.5) 
25 
(float -25) 
-25.0
(float 25.5) 
25.5 
(abs -25) 
25 
(abs 25.5) 
25.5
```

For more information on these functions, see the AutoCAD Help system.

### 3.4 Returning a Value from a Custom Function

Almost all AutoLISP functions return some sort of value—a number, string, or even nil. In Chapter 12 you learned how to create custom functions, but I didn't explain how you can specify a return value for a custom function. The value a custom AutoLISP function returns is always based on the last expression that is evaluated, which doesn't need to be an AutoLISP expression in the traditional sense; it doesn't need to contain a function and be surrounded by parentheses.

Listing 13.3 contains a custom AutoLISP function that divides two numbers and will return either nil or a numeric value. nil is returned instead of the resulting quotient when a zero is passed as an argument value. The reason for the nil is because there is no Else statement to the if function and the if function is the last function to be evaluated.

Listing 13.3: The /s function—dividing by 0 returns nil

```c
; Safely divides two numbers 
; Checks to make sure that one or both of the numbers are not zero 
; (/s 0 2) 
(defun /s (num1 num2 / quotient) 
  (setq quotient 0) 
  (if (and (not (zerop num1)) 
        (not (zerop num2)) 
      ) 
    (setq quotient (/ num1 num2)) 
  ) 
) 

(/s 0 3) 
nil 
(/s 3 0) 
nil 
(/s 2 3) 
0 
(/s 2.0 3) 
0.666667
```

Without the if function to verify that it is safe to divide the two numbers, there would be no point in creating the custom function, as it would be the same as the regular / (divide) function. However, it is valid to add a variable as the last expression in a function. The variable is then evaluated and its value is returned. Listing 13.4 contains a custom AutoLISP function similar to the one shown in Listing 13.3, but the resulting quotient is returned instead.

Listing 13.4: The /s function—dividing by 0 returns 0

```c
; Safely divides two numbers 
; Checks to make sure that one or both of the numbers are not zero 
; (/s 0 2) 
(defun /s (num1 num2 / quotient) 
  (setq quotient 0) 
  (if (and (not (zerop num1)) 
        (not (zerop num2)) 
      ) 
    (setq quotient (/ num1 num2)) 
  )
  quotient
) 

(/s 0 3) 
0
(/s 3 0) 
0
(/s 2 3) 
0 
(/s 2.0 3) 
0.666667
```

1『哈哈，这个知识点很重要，可以直接函数结尾直接写这个变量名即可返回该变量，赞啊。（2020-10-08）』

Listing 13.5 demonstrates how adding an Else statement to the /s custom function would have also solved the problem of nil being returned when a zero is passed as an argument to the function.

Listing 13.5: The /s function—dividing by 0 returns 0 (revised)

```c
; Safely divides two numbers 
; Checks to make sure that one or both of the numbers are not zero 
; (/s 0 2) 
(defun /s (num1 num2 / quotient) 
  (setq quotient 0) 
  (if (and (not (zerop num1)) 
        (not (zerop num2)) 
      ) 
    (/ num1 num2)
    0
  )
) 

(/s 0 3) 
0
(/s 3 0) 
0
(/s 2 3) 
0 
(/s 2.0 3) 
0.666667
```

TIP: Using the AutoLISP princ function in the last statement of a custom AutoLISP function allows that function to「exit quietly」and not return a value. This technique is commonly used when a function's name is prefixed with c:. I cover the princ function in Chapter 15.

1『汇总：1）上面的写法更简洁，写条件语句的时候值得借鉴。2）算是搞明白函数结尾用 `(princ)` 的真正用途了，阻止返回最后一条语句返回的值。做一张任意卡片。（2020-10-08）』

### 3.5 Exercise: Drawing a Rectangle (Revisited)

In this section, I take another look at the drawplate function from Chapter 12, and apply some of the concepts that have been introduced in this chapter. The key concepts that are covered in this exercise are as follows:

1 Using Math Functions Numeric values can be changed using basic math functions.

2 Converting Values AutoLISP functions return different values, and those values can be converted to be used with functions that accept other types of data.

3 Manipulating Strings String values can be manipulated to create a new string value.

4 Storing AutoLISP Expressions You can store AutoLISP expressions in an LSP file so they can be used in more than one drawing or shared with others.

5 Identifying the Locations of Your LSP Files AutoCAD needs to know where your LSP files are so it can locate them and know which locations are trusted.

6 Loading LSP Files LSP files can be loaded into AutoCAD for use by the user or an AutoLISP program.

You can learn more about working with LSP files in Chapter 20,「Authoring, Managing, and Loading AutoLISP Programs.」

#### 3.5.1 Creating the drawplate.lsp File

In Chapter 12, you entered the drawplate function at the AutoCAD Command prompt and executed the function from the current drawing. However, once you created a new drawing or closed the drawing that the function was typed in, it was lost unless you entered the function again. The following steps explain how to create a file named drawplate.lsp that can be used to store the drawplate function:

1 Do one of the following: 1) On Windows XP or Windows 7, click the Start button [All] Programs Accessories Notepad. 2) On Windows 8, on the Start Screen, type note and then click Notepad on the Search bar.

2 In Notepad, click File Save As.

3 In the Save As dialog box, browse to the MyCustomFiles folder that you created under the Documents (or My Documents) folder, or the location in which you want to store the LSP file.

4 In the File Name text box, type drawplate.lsp.

5 Click the Save As Type drop-down list and select All Files (`*.*`).

6 Click the Encoding drop-down list and select ANSI. Click Save.

7 In Notepad, click File Save As. Don't close Notepad.

If you are running AutoCAD on Mac OS, use the following steps to create the drawplate.lsp file:

1 In the Mac OS Finder, click Go Applications. In the Finder window, double-click TextEdit.

2 In TextEdit, click TextEdit Preferences. In the Preferences dialog box, on the New Document tab, click Plain Text and deselect Smart Quotes. Close the dialog box.

3 Click File New to create a plain ASCII text file.

4 Click File Save and type DrawPlate.lsp in the Save As text box. From the sidebar on the left, click Documents MyCustomFiles, or select the location in which you want to store the LSP file. Click Save.

5 If prompted to use the .lsp extension, click Use.lsp.

6 Don't close the TextEdit window for the drawplate.lsp file.

#### 3.5.2 Revising the drawplate Function

In Chapter 12, you defined the drawplate function as a single function with the following expressions:

```c
(defun c:drawplate ( / old_osmode pt1 pt2 pt3 pt4) 
  (setq old_osmode (getvar "osmode")) 
  (setvar "osmode" 0) 
  (command "._-layer" "_m" "Plate" "_c" 5 "" "") 
  (setq pt1 '(0 0 0)) 
  (setq pt2 '(5 0 0)) 
  (setq pt3 '(5 2.75 0)) 
  (setq pt4 '(0 2.75 0)) 
  (command "._line" pt1 pt2 pt3 pt4 "_c") 
  (setvar "osmode" old_osmode) 
)
```

If you look at the drawplate function, it contains expressions that are used to create a layer and draw objects that form a rectangle. Creating or setting a layer is a common task that you will want to perform each time you add objects to a drawing; the same could be true about drawing rectangles, depending on the type of drawings you create. The following two functions are the result of modularizing the expressions of the drawplate function that were used to create a layer and draw a rectangle:

```c
(defun createlayer (name color / ) 
  (command "._-layer" "_m" name "_c" color "" "") 
) 

(defun createrectangle (pt1 pt2 pt3 pt4 / old_osmode) 
  (setq old_osmode (getvar "osmode")) 
  (setvar "osmode" 0) 
  (command "._line" pt1 pt2 pt3 pt4 "_c") 
  (setvar "osmode" old_osmode) 
)
```

If you look at the createlayer and createrectangle functions, you'll see that they both accept values in the form of arguments that are used by the expressions that make up the function. Arguments allow a function to be more flexible and perform the same task in different situations. For example, createlayer could be used to create a Door layer, which is green, or the Plate layer, which is blue. I discussed how to create functions that accept arguments in Chapter 12.

A revised version of the drawplate function using the separate functions that create a layer and draw a rectangle might look like this:

```c
(defun c:drawplate_rev ( / pt1 pt2 pt3 pt4) 
  (createLayer "Plate" 5) 
  (setq width 5 height (/ width 2)) 
  (setq pt1 '(0 0 0) pt2 (list width 0 0) pt3 (list width height 0) pt4 (list 0 height 0)) 
  (createRectangle pt1 pt2 pt3 pt4) 
)
```

Along with breaking code down into smaller functions, thereby making the code modular, you can take the same approach to how the functions are stored. Using this approach, let's you store the three functions in two files: drawplate.lsp and utility.lsp.

1 drawplate.lsp will contain the functions that will be exposed to the user: the original and revised versions of the drawplate function.

2 utility.lsp will contain the createlayer and createrectangle functions, making it easier to reuse the functions with other programs if needed.

#### 3.5.3 Adding the Revised drawplate Function to drawplate.lsp

Now that you have seen how the drawplate function can be broken down into smaller functions, it is time to add the revised function to the drawplate.lsp file and use it in AutoCAD. The following steps explain how to update the drawplate.lsp file:

1 In NotePad or TextEdit, open the file drawplate.lsp.

2 In the text editor area, position the cursor in front of the first expression of the original drawplate function. Hold down the Shift key and click after the last expression of the function.

3 With the expressions of the function highlighted, type the following:

```c
; Draws a rectangular plate that is 5x2.75 
(defun c:drawplate ( / pt1 pt2 pt3 pt4 width height insPt textValue) 
  ; Create the layer named Plate or set it current 
  (createlayer "Plate" 5) 
  ; Define the width and height for the plate 
  (setq width 5 height 2.75) 
  ; Set the coordinates to draw the rectangle 
  (setq 
    pt1 '(0 0 0) ;| lower-left corner |;
    pt2 (list width 0 0) ;| lower-right corner |; 
    pt3 (list width height 0) ;| upper-right corner |; 
    pt4 (list 0 height 0)) ;| upper-left corner |; 
  ; Draw the rectangle 
  (createrectangle pt1 pt2 pt3 pt4) 
  ; Set the insertion point for the text label 
  (setq insPt (list (/ width 2.0) (+ height 1.0) 0)) 
  ; Define the label to add 
  (setq textValue 
    (strcat "Plate Size: " 
            (vl-string-right-trim ".0" (rtos width 2 2)) 
            "x" 
            (vl-string-right-trim ".0" (rtos height 2 2))
    ) 
  ) 
  ; Create label 
  (createlayer "Label" 7) 
  (createtext insPt "_c" 0.5 0.0 textValue) 
)
```

4 Click File Save.

#### 3.5.4 Creating the utility.lsp File

Now that you have the revised version of the drawplate function in the drawplate.lsp file, you need to create the utility.lsp file that will store the functions createlayer and createrectangle. You will also define a function named createtext. That function will be used to place a single-line text object below the plate that is drawn with the createrectangle function.

Follow these steps to create the utility.lsp file, and add the createlayer, createrectangle, and createtext functions:

1 Open Notepad or TextEdit, and create a file named utility.lsp. Use the steps from the「Creating the drawplate.lsp File」section if you need additional information.

2 In NotePad or TextEdit, in the text editor area, type the following:

```c
; CreateLayer function creates/modifies a layer and 
; expects to argument values. 
(defun createlayer (name color / ) 
  (command "._-layer" "_m" name "_c" color "" "") 
) 

; Createrectangle function draws a four-sided closed object. 
(defun createrectangle (pt1 pt2 pt3 pt4 / old_osmode) 
  ; Store and change the value of the OSMODE system variable 
  (setq old_osmode (getvar "osmode")) 
  (setvar "osmode" 0) 
  ; Draw a closed object with the LINE command 
  (command "._line" pt1 pt2 pt3 pt4 "_c") 
  ; Restore the value of the OSMODE system variable 
  (setvar "osmode" old_osmode) 
) 

; Createtext function creates a single-line text object. 
(defun createtext (insertionPoint alignment height rotation textString / old_osmode) 
  ; Store and change the value of the OSMODE system variable 
  (setq old_osmode (getvar "osmode")) 
  (setvar "osmode" 0) 
  ; Creates a single-line text object with the -TEXT command 
  (command "._-text" "_j" alignment insertionPoint height rotation textString) 
  ; Restore the value of the OSMODE system variable 
  (setvar "osmode" old_osmode) 
)
```

3 Click File Save.

#### 3.5.5 Loading the LSP Files into AutoCAD

Before the AutoLISP expressions in the drawplate.lsp and utility.lsp files can be used, the files must be loaded into AutoCAD. The Load/Unload Applications dialog box (appload command) can be used for this purpose. The following steps explain how to load the LSP files into AutoCAD:

1 Make AutoCAD the active program and do one of the following: 1) On the ribbon, click the Manage tab Customization panel Load Application (Windows). 2) On the menu bar, click Tools Load Application (Mac OS). 3) At the Command prompt, type appload and press Enter (Windows and Mac OS).

2 When the Load/Unload Applications dialog box (see Figure 13.2) opens, browse to the MyCustomFiles folder and select the drawplate.lsp file. Click Load.

3 If the File Loading - Security Concerns message box is displayed, click Load.

4 Repeat steps 2 and 3, but select the utility.lsp file to load this time.

5 Click Close to return to the drawing area.

6 At the Command prompt, type drawplate press Enter.

7 Type zoom and press Enter, and then type e to use the Extents option and press Enter.

Figure 13.2 Loading the LSP files

The rectangle that represents the plate is drawn with a single-line text object drawn above it, as shown in Figure 13.3.

Figure 13.3 Results of the custom drawplate function
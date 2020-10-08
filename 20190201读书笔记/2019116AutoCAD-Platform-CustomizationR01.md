# 2019116AutoCAD-Platform-CustomizationR01

## 记忆时间

## 目录

Part II AutoLISP: Productivity through Programming

Chapter 11: Quick Start for New AutoLISP Programmers

Chapter 12: Understanding AutoLISP

Chapter 13: Calculating and Working with Values

Chapter 14: Working with Lists

Chapter 15: Requesting Input and Using Conditional and Looping Expressions

Chapter 16: Creating and Modifying Graphical Objects

Chapter 17: Creating and Modifying Nongraphical Objects

Chapter 18: Working with the Operating System and External Files

Chapter 19: Catching and Handling Errors

Chapter 20: Authoring, Managing, and Loading AutoLISP Programs

Chapter 21: Using the Visual LISP Editor (Windows only)

Chapter 22: Working with ActiveX/COM Libraries (Windows only)

Chapter 23: Implementing Dialog Boxes (Windows only)

## 0201. Quick Start for New AutoLISP Programmers

The AutoLISP® language and programming in general are two subjects that I have enjoyed for over 15 years now, but the same subjects make some people cringe and want to run in the opposite direction. I am not going to claim AutoLISP is easy to learn, but it can be learned by anyone, whether or not they have a programming background. When I first set out to learn AutoLISP, I didn't have any programming experience, but I wanted the benefits that AutoLISP could offer.

I understand if you have some hesitation at the thought of learning AutoLISP, but you don't need to feel that way—I will help you. This chapter will ease you into some core programming concepts and the AutoLISP programming language by exposing you to a variety of functions that are available.

To complete the exercises in this chapter and be able to create and edit LSP files, you must have the following: 1) For Windows users: Autodesk® AutoCAD® 2006 or later and the Notepad program. 2) For Mac OS users: Autodesk® AutoCAD® 2011 or later and the TextEdit program.

NOTE: Although I mention AutoCAD 2006 or later, everything covered in this chapter should work without any problems going all the way back to AutoCAD® 2000 and even possibly earlier releases.

### 1.1 Working with AutoLISP Expressions

AutoLISP is a natural extension of AutoCAD, as it can be used seamlessly from the AutoCAD Command prompt. You can enter AutoLISP when no commands are active or when AutoCAD prompts you for a value. The programming statements used in AutoLISP are known as expressions. You can type expressions at the Command prompt as long as they start with an opening parenthesis [( ] or an exclamation point (! ). Follow those symbols with the functions you wish to execute and the arguments that provide data or further instruction.

Each AutoLISP expression that starts with an opening parenthesis must also end with a closing parenthesis. AutoLISP expressions must contain the same number of opening and closing parentheses—this is sometimes referred to as balancing parentheses. You can enter the opening and closing parentheses on separate lines, though.

Use these steps to gain a basic understanding of entering AutoLISP expressions at the AutoCAD Command prompt: ......

In this exercise, you did the following:

1. Entered AutoLISP expressions at the AutoCAD Command prompt and stored values in a user-defined variable (see Chapter 12,「Understanding AutoLISP,」for more information)

2. Used functions to perform basic math calculations (see Chapter 13,「Calculating and Working with Values,」for more information)

3. Created a list that represented a 2D coordinate (see Chapter 14,「Working with Lists,」for more information)

### 1.2 Working with Commands and Input

In addition to calculating values with AutoLISP and passing those values to a command, you can execute a command as part of an AutoLISP expression using the command function. Input can also be requested and passed to a command or saved to a user-defined variable.

The following steps demonstrate how to create a layer named Circles with an AutoCAD Color Index (ACI) of 30 using the -layer command. You'll then draw a circle on the new layer with a user-specified center point and radius.

......

Now that you've entered some short expressions, let's look at creating long expressions—expressions that can span multiple lines. Using the following steps, you will also see how to give feedback to the user based on values they provided in the form of the center point and radius of the circle.

......

1『学到了几个新函数：1）`vl-princ-to-string` 将 list 数据类型转化为字符串。2）`rtos` 将数字转化为字符串。（2020-10-08）』

In these exercises, you did the following:

1. Used standard AutoCAD commands to create a layer and draw a circle (see Chapter 12 for more information)

2. Requested input from the user and displayed information back to the user (see Chapter 15,「Requesting Input and Using Conditional and Looping Expressions,」for more information)

3. Converted values from one type of data to another (see Chapters 13 and 14 for more information)

### 1.3 Conditionalizing and Repeating Expressions

Complex programs often contain branches (different sets of expressions that are used to handle different conditions or choices by the user), and they might loop (execute a set of expressions multiple times). Conditional expressions allow your programs to use a programming concept known as branching. Branching gives your programs the ability to execute different expressions based on the input a user provides or the current value of a system variable. When modifying large sets of data or even prompting a user for input, you can use looping expressions to repeat a set of expressions while a condition is met.

This exercise demonstrates some of the conditional and looping expressions that are available in AutoLISP:

1. At the AutoCAD Command prompt, type `(if (= (tblsearch "layer" "Circles") nil)` and press Enter. The if function is used to test whether a condition is true or false. If the = comparison operator returns T, then the first expression is evaluated; otherwise, the second expression is. The tblsearch function is used to check to see if a layer, linetype, or some other nongraphical object already exists in a drawing.

2. Type `(command "-layer" "m" "Circles" "c" "30" " " " ")` and press Enter. This command creates the new Circles layer if it doesn't exist in the drawing.

3. Type `(prompt "\nLayer already exists.")` and press Enter.

4. Type `)` and press Enter. The closing parenthesis ends the if function. Either the Circles layer is created or the message Layer already exists. is displayed. Entering the four expressions again results in the displaying of the message.

5. Type `(setq cnt 0)` and press Enter. The setq function defines a user-defined variable named cnt and assigns it the value of 0.

6. Type `(command "circle" (list 0 0) 1)` and press Enter. This command draws a circle at 0,0 with a radius of 1 on the「Circles」layer.

    TIP: If the new circle is not visible on the screen, pan and/or zoom to make it visible.

7. Type `(repeat 7` and press Enter. The repeat function is used to repeat a set of AutoLISP expressions a specific number of times.

8. Type `(setq cnt (1+ cnt))` and press Enter. The `1+` function increments the current value of cnt by 1 each time the expression is evaluated.

9. Type `(command "circle" (list 0 0) (* (getvar "circlerad") 1.5))` and press Enter. Once you enter the expressions within the repeat loop and add the final closing parenthesis to complete the expression, AutoCAD draws a new circle at 0,0 with a radius that is 1.5 times larger than the previous circle that was drawn. The previous radius used to create a circle with the circle command is stored in the circlerad system variable. The getvar function returns the current value of a system variable.

10. Type `(command "change" (entlast) " " "p" "c" cnt " ")` and press Enter. The change command modifies the color of the recently drawn circle, or more specifically the last object in the drawing. The entlast function returns the last object added to the drawing.

11. Type `)` and press Enter. The closing parenthesis ends the repeat function. Seven concentric circles, as shown in Figure 11.2, are drawn around the circle that was drawn outside of the repeat loop. Each circle drawn inside the repeat loop is assigned a different color, and the radius of each circle is 1.5 times larger than the next inner circle.

In the previous exercise, you did the following:

1. Used comparison operators and conditional functions to evaluate different expressions based on the results of a test condition (see Chapter 15 for more information)

2. Used math-based functions to calculate the radius of a circle and to increment a counter used in a looping expression (see Chapter 13 for more information)

3. Checked to see if a layer existed in the drawing (see Chapter 17,「Creating and Modifying Nongraphical Objects,」for more information)

4. Repeated a set of AutoLISP expressions until a condition was met (see Chapter 15 for more information)

1『变量自增 1 的简化版写法：`(setq cnt (1+ cnt))`，其中 `1+` 也是一个函数。（2020-10-08）』

### 1.4 Grouping Expressions

Entering individual expressions can be helpful when you are first learning AutoLISP or when you are developing a new program, but it isn't ideal for you to do each time you want to execute a set of AutoLISP expressions. The AutoLISP programming language allows you to define a custom function that can be executed at the Command prompt or from a command macro assigned to a user-interface element, such as a ribbon or toolbar button.

The following steps demonstrate how to define a custom function named RectangularRevCloud that can be entered at the AutoCAD Command prompt:

......

In the previous exercise, you did the following:

1. Grouped a set of AutoLISP expressions into a custom function to make it easier to execute the expressions (see Chapter 12 for more information).

2. Accessed the value of a system variable (see Chapter 12 for more information).

### 1.5 Storing and Loading AutoLISP Expressions

AutoLISP expressions entered at the AutoCAD Command prompt are accessible from that drawing and only while that drawing remains open. You can store AutoLISP expressions in an LSP file that, once saved, can then be loaded into and executed from any drawing file that is opened in AutoCAD. The following exercise explains how to create and load an LSP file named `acp_qs.lsp`.

......

In the previous exercise, you did the following:

1. Created an LSP file to store AutoLISP expressions (see Chapter 20,「Authoring, Managing, and Loading AutoLISP Programs,」for more information).

2. Loaded an LSP file into AutoCAD (see Chapter 20 for more information).

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

1. ( —Opening Parenthesis. An opening parenthesis indicates the beginning of an AutoLISP expression and must be paired with a closing parenthesis `)` to indicate the end of an AutoLISP expression. The opening and closing parentheses do not need to be on the same lines in an AutoLISP program, but each AutoLISP program must contain the same number of opening and closing parentheses.

2. ! —Exclamation Point. An exclamation point is used to retrieve the current value assigned to a variable. The exclamation point must be placed in front of the variable's name and can only be used at the AutoCAD Command prompt. I discuss variables later, in the「Storing and Retrieving Values」section.

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

1. Scripts and Command Macros AutoLISP expressions can be used in script (SCR) files and command macros that are defined for use with a user-interface element in a customization (CUIx/CUI) file, just as you enter expressions at the Command prompt. I discussed SCR files in Chapter 8,「Automating Repetitive Tasks,」and you learned about CUIx/CUI files in Chapter 5,「Customizing the AutoCAD User Interface for Windows,」and Chapter 6,「Customizing the AutoCAD User Interface for Mac.」

2. A File You can store AutoLISP expressions in an ASCII text file and then load that file into AutoCAD. Entering expressions at the Command prompt is a great way to learn AutoLISP and is useful when only a few expressions need to be executed, but it is not ideal for complex programs or when you want to reuse the same expressions several times. I explain how to create and manage AutoLISP files in Chapter 20,「Authoring, Managing, and Loading AutoLISP Programs.」

#### 2.1.3 Accessing the AutoLISP Documentation

The AutoLISP documentation is part of the AutoCAD Help system. The help system includes the AutoLISP Reference and AutoLISP Developer's Guide topics. Although this book is designed to make it easy to learn the AutoLISP programming language and doubles as a reference that you can refer to time and time again when working with AutoLISP, it just is not possible to cover every function and technique here.

The AutoLISP Reference topics explain what each function does in the AutoLISP programming language. The AutoLISP Developer's Guide topics explore advanced techniques and features that are not covered in this book.

### 2.2 Storing and Retrieving Values

Programs—and programming languages, for that matter—are typically designed with one of two basic concepts in mind: to receive/consume or return/give. Most AutoLISP functions are designed to receive one or more values in the form of arguments, and then return a single value that can then be used by another function or returned to the user. When a function returns a value, you can store that value for future use—in the current custom function that is executing or even between different AutoCAD sessions. After a value has been stored, you can then retrieve the value for use by your program when it is needed.

You can store and retrieve values using these techniques:

1. User-Defined Variables. User-defined variables allow you to temporarily store a value within a function or globally while a drawing remains open. A variable is defined using the AutoLISP setq function. For example, you can use the expression `(setq msg "Hello AutoLISP! ")` to define a variable named msg and assign it the text string「Hello AutoLISP!」I discuss user-defined variables in the next section.

2. System Variables. System variables store values that are often used to control the behavior of AutoCAD commands or the drawing environment, and even allow access to the values that are calculated by some AutoCAD commands, such as area or distance. Unlike with user-defined variables, you can't create your own system variables. The system variable might represent a value that is stored in the current drawing or as part of the current AutoCAD user profile. See the section「Working with System Variables」later in this chapter.

3. Environment Variables. Similar to system variables, environment variables are used to control the behavior of AutoCAD commands or the drawing environment. You can access the values of environment variables that are defined by AutoCAD or even create your own as needed. Environment variables are stored as part of the AutoCAD user profile and as part of the Windows Registry or as a property list (Plist) file on Mac OS. I discuss accessing environment variables later in this chapter in the「Accessing Environment Variables」section.

4. Windows Registry (Windows Only). The Windows Registry is used to store settings that can be retrieved across different drawings and between application sessions. You can access the settings that AutoCAD reads and writes, and the Windows Registry is also a perfect place to store your own settings for your custom programs. I explain how to work with the Windows Registry in Chapter 18,「Working with the Operating System and External Files.」

5. Property List File (Mac OS Only). Similar to the Windows Registry, Plist files are used to store settings that can be retrieved across different drawings and between application sessions. As with the Window Registry, you can access the settings that AutoCAD reads and writes, and the Plist files are also a perfect place to store your own settings for your custom programs. I explain in Chapter 18 how to work with the Plist files.

6. Extended Data and Records. Extended data (XData) and records (XRecords) allow you to attach custom information to a graphical object or create a custom dictionary in a drawing that can be used to store multiple entries containing custom information. XData is a great way to add unique information to an object in a drawing. AutoCAD uses XData to help facilitate dimension overrides, implement some multiline text features, and provide other features. You'll learn about XData in Chapter 16,「Creating and Modifying Graphical Objects,」and XRecords in Chapter 17,「Creating and Modifying Nongraphical Objects.」

7. External Data Files. AutoLISP allows you to write values to and read values from an ASCII text file that can be stored outside of AutoCAD on a local or network drive. I explain how to access external files in Chapter 18. If you are using Windows and have Microsoft Office installed, you can also access information that can be created and modified using an application that is part of Microsoft Office—ActiveX/COM. I discuss using COM with AutoLISP in Chapter 22,「Working with ActiveX/COM Libraries (Windows Only).」

8. Configuration Files. Configuration (CFG) files are used to store settings that can be retrieved across different drawings and between application sessions. Storing values in a CFG file is not as common as it once was, but you should be familiar with storing and retrieving values from a CFG file just in case you are working on an older program. I recommend using one of the other techniques for storing values that can be accessed across multiple drawings or between application sessions, such as the Windows Registry, Plist files, or even external data files. You'll learn how to work with CFG files in Chapter 18.

1『汇总：1）第 6 点里，感觉 Extended Data and Records 有大用处，目前没遇到应用点，相关的知识也没去研读。2）妙啊，第 7 点提到，可以读取本地文件和网络文件作为输入数据，去看第 18 章的内容。（2020-10-08）』

#### 2.2.1 Setting and Using Variables

In an AutoLISP program, it is not uncommon to want to use the same value more than once or to use a value returned by one function as a value for an argument in another function. Variables allow you to define a named location in memory to temporarily store a value. AutoLISP supports two types of variables: user-defined and predefined. 1) User-defined variables are those that you or another developer create for use in an AutoLISP program. 2) Predefined variables are those that are automatically defined and assigned a specific value by the AutoLISP environment for each drawing that is created or opened.

#### 2.2.1.1 Defining and Using User-Defined Variables

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

1. At the AutoCAD Command prompt, type !cenpt and press Enter. nil should be returned, unless the variable was previously defined.

2. Type (setq cenpt '(1 2 0)) and press Enter. The variable cenpt is defined and assigned the coordinate value 1,2,0. (1 2 0) is returned by the setq function.

3. Type !cenpt and press Enter. The value of the cenpt variable is returned, which should be (1 2 0).

4. Type (setq rad 3.125) and press Enter. The variable rad is defined and assigned the real numeric value 3.125.

5. Type circle and press Enter. The circle command is started.

6. At the Specify center point for circle or [3P/2P/Ttr (tan tan radius)]: prompt, type !cenpt and press Enter. The value of the cenpt variable is returned and used for the circle's center point.

7. At the Specify radius of circle or [Diameter]: prompt, type !rad and press Enter. The value of the rad variable is returned and used for the circle's radius. The circle command ends and the circle is drawn.

#### 2.2.1.2 Using Predefined Variables

In addition to the user-defined variables that you might create and use in AutoLISP expressions, the AutoLISP environment defines three variables that are assigned a specific value and are accessible from all drawing files that are opened. The variables that are predefined by the AutoLISP environment are as follows:

1. PI. The PI variable is assigned the value of 3.141592653589793, which is a constant value that represents the ratio of a circle's diameter to its circumference.

2. T. The T variable always returns a value. This variable is commonly used when you test whether a condition returns True.

3. PAUSE. The PAUSE variable is assigned the string「\\」. The PAUSE variable is used in combination with the command function to suspend the execution of an AutoLISP expression and allow the user to respond to a command's request for input.

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

1. A global variable is accessible to all AutoLISP programs that are loaded into the drawing and to those expressions that are executed in the drawing from which the variable was defined. By default, all variables are defined with a global scope.

2. A local variable is accessible only from the function in which it is defined. You define the variable using the setq function, but the name of the variable is also added to the `local_var` argument of the defun function to restrict its use to just that function. I discuss the defun function later in this chapter in the section「Defining and Using Custom Functions.」If a variable is not added to this argument, it remains a global variable.

Although a variable can be defined with a global scope, a variable with the same name can exist in the local scope of a function. When this happens, the expressions inside your function are aware only of the local variable. The following steps show how a variable defined in the local scope of a custom function takes precedence over a variable defined with a global scope:

1. At the AutoCAD Command prompt, type the following and press Enter: `(setq *apc_var* "Global")`

2. Type the following and press Enter to define the GlobalVar function: `(defun c:GlobalVar ( / )(alert *apc_var*))`

3. Type the following and press Enter to define the LocalVar function: `(defun c:LocalVar ( / *apc_var*) (setq *apc_var* "Local") (alert *apc_var*) )`

4. Type globalvar and press Enter. Click OK to exit the alert message box. The alert message box displays the text string assigned to the `*apc_var* `variable in the global scope, which is the value Global.

5. Type localvar and press Enter. Click OK to exit the alert message box. The variable `*apc_var*` is assigned the value of the string "Local" and then an alert message box displays the text string assigned to the `*apc_var*` variable in the local scope, which is the value Local.

6. Type globalvar and press Enter. Click OK to exit the alert message box. The alert message box displays the text string assigned to the `*apc_var*` variable in the global scope, which is the value Global. When the localvar function was executed in step 5, the`*apc_var*` variable was assigned a value that existed only while the function was executing; it did not overwrite the value of the globally defined `*apc_var*` variable.

TIP: User-defined variables are normally accessible only from the drawing in which they are defined, but you can use the AutoLISP vl-bb-ref and vl-bb-set functions to define variables on what is known as the blackboard. The blackboard is a centralized location for defining variables that can be accessed from any open drawing. The AutoLISP vl-propagate function can also be used to define a variable with a specific value in all open drawings and any drawings that are subsequently opened in the AutoCAD session. You can learn more about these functions in the AutoCAD Help system.

1-2『上面的几个函数，可以实现把一些数据放到公共变量（内存）中，保证所有打开的图纸空间都可以访问到。这个可以帮助实现把数据从流程图迁移到设备布置图，功能待开发，哈哈。做一张任意卡片。（2020-10-08）』——已完成

#### 2.2.4 Working with System Variables

System variables are used to alter the way commands work, describe the current state of a drawing or AutoCAD environment, and even specify where the support files are for your custom programs. Many of the settings that are exposed by system variables are associated with controls in dialog boxes and palettes; other settings are associated with various command options. For example, many of the settings in the Options (Windows) or Application Preferences (Mac OS) dialog box are accessible from system variables and even environment variables (which I discuss in the next section).

A system variable can store any one of the basic data types that AutoLISP supports (see「Exploring Data Types」later in this chapter). You can see the hundreds of system variables and the type of data each system variable holds by using the AutoCAD Help system. Whereas you might normally use the setvar command to list or change the value of a system variable at the AutoCAD Command prompt, with AutoLISP you use the getvar and setvar functions to query and set the value of a system variable. Here's the syntax of the getvar and setvar functions:

```c
(getvar sysvar_name) (setvar sysvar_name value)
```

`sysvar_name`. The `sysvar_name` argument represents the name of the system variable you want to query or set.

`value`. The value argument represents the data that you want to assign to the system variable.

The next exercise demonstrates how to query and set the value of the osmode system variable, which controls the running object snap drafting aid. This setting is available in the Drafting Settings dialog box (dsettings command).

1. At the AutoCAD Command prompt, type `(setq *apc_cur_osmode* (getvar "osmode"))` and press Enter. The function returns the current value of the osmode system variable and assigns it to the user-defined variable `*apc_cur_osmode*` with the setq function.

2. Type `(setvar "osmode" 33)` and press Enter. The osmode system variable is assigned the integer value of 33, which represents the Endpoint and Intersection running object snap modes.

3. Type osnap and press Enter. In the Drafting Settings dialog box, select the Object Snap tab and verify that the Endpoint and Intersection options are checked and all other options are unchecked. Click Cancel to return to the Command prompt.

4. Type `(setvar "osmode" *apc_cur_osmode*)` and press Enter. The previous value of the system variable is restored.

5. Type osnap and press Enter. In the Drafting Settings dialog box, you will notice that the options checked will represent those of the restored running object snap settings value. Click Cancel to return to the Command prompt.

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

1. At the AutoCAD Command prompt, type `(setq *apc_cur_val* (getenv "DefaultFormatForSave"))` and press Enter. The function returns the current value of the environment variable and assigns it to the user-defined variable `*apc_cur_val*` with the setq function.

2. Type `(setenv "DefaultFormatForSave" "48")` and press Enter. The DefaultFormatForSave environment variable is assigned the value of 48, which represents the AutoCAD 2010 drawing file format. If you are using an earlier release, you may need to use a different value to set a previous drawing file format as current.

3. Type saveas and press Enter. In the SaveAs dialog box, notice that the Files Of Type drop-down list will list AutoCAD 2010/LT2010 Drawing (*.dwg) as the current option. Click Cancel to return to the Command prompt.

4. Type `(setenv "DefaultFormatForSave" *apc_cur_val*)` and press Enter. The previous value of the environment variable is restored.

5. Type saveas and press Enter. In the SaveAs dialog box, notice that the Files Of Type drop-down list now lists the previous default drawing file format. Click Cancel to return to the Command prompt.

TIP: I created a list (though not complete or up to date) of the environment variables available in a number of earlier releases of AutoCAD. You can find this list here: http://www.hyperpics.com/downloads/resources/customization/autolisp/AutoCAD%20Environment%20Variables.pdf

2『已下载「AutoCAD-Environment-Variables.pdf」作为本书的附件。』

### 2.3 Exploring Data Types

Programming languages use data types to help you identify the following: 1) The type of data required by a function's argument. 2) The type of data that might be returned by a function.

AutoLISP on Windows and Mac OS support the following data types:

1. Integer. An integer is a numeric value without a decimal point. The numeric value must be in the range of –32,768 to 32,767 and can be optionally prefixed with a plus sign (+) for positive numbers. You can use an integer value to represent an angular or linear distance or the number of columns or rows in an array or table, or to specify whether a system variable is enabled or disabled. Examples include -10, 0, 1, +45, and 400. You'll learn about using integer values with mathematical functions in Chapter 13,「Calculating and Working with Values.」

2. Real. A real value is numeric with a decimal point. The numeric value must be in the range of 1.80 × 10308 to –4.94 × 10–324 for negative numbers and 4.94 × 10–324 to 1.80 × 10308 for positive numbers. A positive number can optionally be prefixed with a plus sign and be expressed in exponential notation; 10e4 is the same as 100000.0. When using a value between –1.0 and 1.0, you must use a leading zero before the decimal;.5 is not a valid real number but 0.5 is. You might use a real number to represent an angular or linear distance or part of a coordinate. Examples of a real number are –10.01, 0.0, 1.125, +45.0, and 400.00001. Chapter 13 discusses using real values with mathematical functions.

    NOTE: The real data type in AutoLISP is commonly referred to as a double or float in other programming languages.

3. String. A string is a value that contains one or more characters enclosed in quotation marks. You might use a string value for a command or system variable name, a file path and name, messages and prompts that are displayed to the user, or even a real or integer number converted to a string. Examples of a string value are「Hello AutoLISP!", "._line", "\nSpecify next point: ", and "6.25". You'll learn more about working with string values in Chapter 13.

4. List. A list is an expression of one or more atoms enclosed in parentheses. All AutoLISP expressions are known as lists, but lists often represent 2D points, 3D points, and data groupings. Examples of a list are `(1.5 2.75)`, `(1.5 2.75 0.5)`, `("Model" "Layout1" "Layout2")`, `(1 "A" 2 "B")`, and `()`. () represents an empty list. When you're assigning a list to a variable, either the list must be preceded by an apostrophe, as in `(setq pt '(1 2 0))`, or you must use the AutoLISP list function, as in `(setq pt (list 1 2 0))`. Chapter 14,「Working with Lists,」explores creating and manipulating lists.

    NOTE: The list data type in AutoLISP is similar to an array in other programming languages.

5. Dotted Pair. A dotted pair is a list of two values separated by a period. Dotted pairs are commonly used to represent property values for an object. The first value of a dotted pair is sometimes referred to as a DXF group code. For example, `(40 . 2.0)` represents the radius of a circle; DXF group code value 40 indicates the radius property, and 2.0 is the actual radius value for the circle. When you're assigning a dotted pair to a variable, either the pair must be preceded by an apostrophe, as in `(setq dxf_40 '(40 . 2))`, or you must use the AutoLISP cons function, as in `(setq dxf_40 (cons 40 2))`. You'll learn more about creating and manipulating dotted pairs in Chapter 16.

6. Entity Name. An entity name is an in-memory numeric label used to reference an object stored in a drawing. You will often work with an entity name to modify an object's properties or after a request to select objects in a drawing has been completed. See Chapters 16 and 17 to learn how to work with entity names.

2『 Dotted Pair 做一张术语卡片。』——已完成

AutoLISP on Windows supports a few additional data types, and I discuss these additional data types in depth and how they are used in Chapter 22. The data types that are specifically used for working with ActiveX libraries are as follows:

1. VLA-Object. A VLA-Object represents an ActiveX object that is used when working with methods and properties imported from the AutoCAD Object Library or another ActiveX library. An ActiveX object can be an object stored in a drawing, an open drawing, or the AutoCAD application itself.

2. Variant. A variant is a generic data type that can hold any type of data supported by the Component Object Model (COM) interface.

3. Safearray. A safearray is not really a data type, but rather a data structure that can contain multiple values similar to the list data type. You use a safearray when you need to represent a coordinate value, specify the objects used to define a closed boundary when creating a Region or Hatch object, or specify the data types and values that make up the XData attached to an object.

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

1-2『完全可以自己做一些判断数据类型的函数，封装起来自己用，真切的感觉到，一切语法即为语法糖。封装判断数据类型的函数，做一张主题卡片。』——已完成


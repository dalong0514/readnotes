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


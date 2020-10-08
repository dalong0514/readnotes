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


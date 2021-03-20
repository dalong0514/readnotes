statements, they can consist of anything you want. You can insert a comment to

remind yourself why you did something or to clarify some particularly elegant

code you wrote.

CHAPTER 7  Essential VBA Language Elements    93

Use comments liberally and extensively to describe what the code does (which isn’t always obvious from reading the code itself). Often, code that makes perfect

sense today mystifies you tomorrow. Been there. Done that.

You begin a comment with an apostrophe (’). VBA ignores any text that follows an

apostrophe in a line of code. You can use a complete line for your comment or

insert your comment at the end of a line of code. The following example shows a

VBA procedure with four comments:

Sub FormatCells()

'  Exit if a range is not selected

If TypeName(Selection) <> "Range" Then

MsgBox "Select a range."

Exit Sub

End If

'  Format the cells

With Selection

.HorizontalAlignment = xlRight

.WrapText = False ' no wrap

.MergeCells = False ' no merged cells

End With

End Sub

The「apostrophe indicates a comment」rule has one exception: VBA doesn’t inter-

pret an apostrophe inside a set of quotation marks as a comment indicator. For

example, the following statement doesn’t contain a comment, even though it has

an apostrophe:

Msg = "Can't continue"

When you’re writing code, you may want to test a procedure by  excluding a

particular statement or group of statements. You  could delete the statements and then retype them later. But that’s a waste of time. A better solution is to simply

turn those statements into comments by inserting apostrophes. VBA ignores

statements beginning with apostrophes when executing a routine. To reactivate

those「commented」statements, just remove the apostrophes.

Here’s a quick way to convert a block of statements to comments. In the VBE,

choose View ➪ Toolbars ➪ Edit to display the Edit toolbar. To convert a block of

statements to comments, select the statements and click the Comment Block

button. To remove the apostrophes, select the statements and click the Uncom-

ment Block button.

94    PART 3  Programming Concepts

Everyone develops his or her own style of commenting. To be useful, however, comments should convey information that’s not immediately obvious from

reading the code.

The following tips can help you make effective use of comments:

» Identify yourself as the author. This can be useful when you get promoted and the person who takes over your job has some questions.

» Briefly describe the purpose of each Sub or Function procedure you write.

» Use comments to keep track of changes you make to a procedure.

» Use a comment to indicate that you’re using a function or a construct in an unusual or nonstandard manner.

» Use comments to describe the variables you use, especially if you don’t use meaningful variable names.

» Use a comment to describe any workarounds you develop to overcome bugs

in Excel.

» Write comments as you develop code instead of saving the task for a final

step.

» Depending on your work environment, consider adding a joke or two as a

comment. The person who takes over your job when you get promoted might

appreciate the humor.

Using Variables, Constants,

and Data Types

VBA’s main purpose is to manipulate data. VBA stores the data in your computer’s

memory, and the data may or may not end up on disk. Some data, such as work-

sheet ranges, resides in objects. Other data is stored in variables that you create.

Understanding variables

A  variable is simply a named storage location in your computer’s memory that’s used by a program. You have lots of flexibility in naming your variables, so make

the variable names as descriptive as possible. You assign a value to a variable by

using the equal-sign operator. (More about this later in the「Using Assignment

Statements」section.)

CHAPTER 7  Essential VBA Language Elements    95

Here are some examples of variables being assigned values. Note that the last example uses two variables.

x = 1

InterestRate = 0.075

LoanPayoffAmount = 243089

DataEntered = False

x = x + 1

UserName = "Bob Johnson"

Date_Started = #3/14/2019#

MyNum = YourNum * 1.25

VBA enforces a few rules regarding variable names:

» You can use letters, numbers, and some punctuation characters, but the first character must be a letter.

» VBA doesn’t distinguish between uppercase and lowercase letters.

» You can’t use any spaces, periods, or mathematical operators in a variable

name.

» You can’t use the following characters in a variable name: #, $, %, &, or !.

» Variable names can be no longer than 255 characters. But nobody even gets

close to that limit.

To make variable names more readable, programmers often use mixed case (for

example, InterestRate) or the underscore character (interest_rate).

VBA has many reserved words that you can’t use for variable names or procedure

names. These include words such as Sub, Dim, With, End, Next, and For. If you

attempt to use one of these words as a variable, you may get a compile error

(which means your code won’t run). So if an assignment statement produces an

error message, double-check to make sure that the variable name isn’t a reserved

word. An easy way to do that is to select the variable name and press F1. If your

variable name is a reserved word, it will have an entry in the Help system.

VBA does allow you to create variables with names that match names in Excel’s

object model, such as Workbook and Range. But obviously, using names like that

just increases the possibility of getting confused. Here’s a perfectly valid (but very confusing) macro that declares Range as a variable name and works with a cell

named Range in a worksheet named Range:

96    PART 3  Programming Concepts

Sub RangeConfusion()

Dim Range As Double

Range = Sheets("Range").Range("Range").Value

MsgBox Range

End Sub

So resist the urge to use a variable named Workbook or Range, and use something

like MyWorkbook or MyRange instead.

What are VBA’s data types?

When discussing programming languages, the term  data type refers to the manner in which a program stores data in memory — for example, as integers, real numbers, or strings. Although VBA can take care of these details automatically, it does so at a cost. (There’s no free lunch.) Letting VBA handle your data typing results

in slower execution and inefficient memory use. For small applications, this usu-

ally doesn’t present much of a problem. But for large or complex applications, which may be slow or need to conserve every last byte of memory, you need to be

on familiar terms with data types.

VBA automatically handles all the data details, which makes life easier for

programmers. Not all programming languages provide this luxury. For example,

some languages are  strictly typed,  which means the programmer must explicitly define the data type for every variable used.

VBA doesn’t require that you declare the variables that you use, but it’s definitely a good practice. You see why later in this chapter.

VBA has a variety of built-in data types. Table 7-1 lists the most common types of

data that VBA can handle.

In general, choose the data type that uses the smallest number of bytes but can

still handle all the data you want to store in the variable.

An exception to the「smallest number of bytes」rule is Long. Most VBA programmers

use Long instead of Integer because doing so offers a slight performance increase.

But for small procedures, you would never notice any difference between Integer

and Long data types.

CHAPTER 7  Essential VBA Language Elements    97

TABLE 7-1

VBA’s Built-In Data Types

Data Type

Bytes Used

Range of Values

Byte

1

0 to 255

Boolean

2

True or False

Integer

2

–32,768 to 32,767

Long

4

–2,147,483,648 to 2,147,483,647

Single

4

–3.40E38 to –1.40E-45 for negative values;

1.40E-45 to 3.40E38 for positive values

Double

8

–1.79E308 to –4.94E-324 for negative values;

4.94E-324 to 1.79E308 for positive values

Currency

8

–922,337,203,685,477 to 922,337,203,685,477

Date

8

1/1/0100 to 12/31/9999

Object

4

Any object reference

String

1 per character

Varies

Variant

Varies

Varies

Declaring and scoping variables

If you read the preceding sections, you know a bit about variables and data types.

In this section, you discover how to declare a variable as a certain data type.

If you don’t declare the data type for a variable you use in a VBA routine, VBA uses the default data type: Variant. Data stored as a variant acts like a chameleon; it

changes type depending on what you do with it. For example, if a variable is a

Variant data type and contains a text string that looks like a number (such as「143」), you can use this variable for string manipulations as well as numeric calculations.

VBA automatically handles the conversion. Letting VBA handle data types may

seem like an easy way out — but remember that you sacrifice speed and increase

memory used.

Before you use variables in a procedure, it’s an excellent practice to  declare your variables — that is, tell VBA each variable’s data type. Declaring your variables

makes your macro run faster and use memory more efficiently. The default data

type, Variant, causes VBA to repeatedly perform time-consuming checks and

98    PART 3  Programming Concepts

reserve more memory than necessary. If VBA knows a variable’s data type, it doesn’t have to investigate and can reserve just enough memory to store the data.

To force yourself to declare all the variables you use, include these two words as

the first statement in your VBA module:

Option Explicit

When this statement is present, you won’t be able to run your code if it contains

any undeclared variables.

You need to use Option Explicit only once: at the beginning of your module, before

the declaration of any procedures in the module. Keep in mind that the Option

Explicit statement applies only to the module in which it resides. If you have more

than one VBA module in a project, you need an Option Explicit statement for each

module.

Suppose that you use an undeclared variable (that is, a Variant) named Current-

Rate. At some point in your routine, you insert the following statement:

CurentRate = .075

The variable name is misspelled (missing an r) and can be very difficult to spot.

If you don’t notice it, Excel interprets it as a  different variable, and it will probably cause your routine to give incorrect results. If you use Option Explicit at the

beginning of your module (forcing you to declare the CurrentRate variable), Excel

generates an error if it encounters a misspelled variation of that variable.

To ensure that the Option Explicit statement is inserted automatically whenever

you insert a new VBA module, turn on the Require Variable Definition option.

You find it on the Editor tab of the Options dialog box (in the VBE, choose Tools ➪ Options).

Declaring your variables also allows you to take advantage of a shortcut that can

save some typing. Just type the first two or three characters of the variable name

and then press Ctrl+space bar. The VBE either completes the entry for you or — if

the choice is ambiguous — shows you a list of matching words to choose among.

In fact, this slick trick works with reserved words and functions, too. Figure 7-1

shows an example of how this works.

CHAPTER 7  Essential VBA Language Elements    99

FIGURE 7-1:

Pressing

Ctrl+space bar

displays a list of

variable names,

reserved words,

and functions.

You now know the advantages of declaring variables, but  how do you do it? The most common way is to use a Dim statement. Here are some examples of variables

being declared:

Dim YourName As String

Dim January_Inventory As Double

Dim AmountDue As Double

Dim RowNumber As Long

Dim X

The first four variables are declared as a specific data type. The last variable, X, is not declared as a specific data type, so it’s treated as a Variant (it can be anything).

Besides Dim, VBA has three keywords that are used to declare variables:

» Static

» Public

» Private

The Dim, Static, Public, and Private keywords later are discussed later, but first,

two other topics are relevant here: a variable’s scope and a variable’s life.

A workbook can have any number of VBA modules, and a VBA module can have

any number of Sub and Function procedures. A variable’s  scope determines which modules and procedures can use the variable. Table 7-2 has the details.

Confused? Keep turning the pages; some examples make this stuff crystal clear.

100    PART 3  Programming Concepts

TABLE 7-2

Variable’s Scope

Scope

How the Variable Is Declared

Procedure only

By using a Dim or a Static statement in the procedure that uses the

variable

Module only

By using a Dim or a Private statement before the first Sub or Function

statement in the module

All procedures in all modules

By using a Public statement before the first Sub or Function statement

in a module

Procedure-only variables

The lowest level of scope for a variable is at the procedure level. (A  procedure is either a Sub or a Function procedure.) Variables declared with this scope can be

used only in the procedure in which they’re declared. When the procedure ends,

the variable no longer exists, and Excel frees up its memory. If you execute the

procedure again, the variable comes back to life, but its previous value is lost.

The most common way to declare a procedure-only variable is with a Dim

statement. Dim doesn’t refer to the mental capacity of the VBA designers. Rather,

it’s an old programming term that’s short for  dimension,  which simply means you’re setting aside memory for a particular variable. You usually place Dim statements immediately after the Sub or Function statement and before the

procedure’s code.

The following example shows some procedure-only variables declared by using

Dim statements:

Sub MySub()

Dim x As Integer

Dim First As Long

Dim InterestRate As Single

Dim TodaysDate As Date

Dim UserName As String

Dim MyValue

' ...   [The procedure's code goes here] ...

End Sub

Notice that the last Dim statement in the preceding example doesn’t declare a data

type for the MyValue variable; it declares only the variable itself. The effect is that the variable MyValue is a Variant data type.

CHAPTER 7  Essential VBA Language Elements    101

Unlike some languages, VBA doesn’t allow you to declare a group of variables to be

a particular data type by separating the variables with commas. For example,

though valid, the following statement does  not declare all the variables as Integers: Dim i, j, k As Integer

In this example, only k is declared to be an Integer; the other variables default to the Variant data type.

If you declare a variable with procedure-only scope, other procedures in the same

module can use the same variable name, but each instance of the variable is unique

to its own procedure. In general, variables declared at the procedure level are the

most efficient because VBA frees up the memory they use when the procedure ends.

Module-only variables

Sometimes, you want a variable to be available to all procedures in a module. If so, just declare the variable (using Dim or Private)  before the module’s first Sub or Function statement — outside any procedures. You do this in the Declarations section, at the beginning of your module. (This is also where the Option Explicit

statement is located.)

Figure 7-2 shows how you know when you’re working with the Declarations

section. Use the drop-down menu on the right, and go directly to the Declarations

section. Do not pass Go, and do not collect $200.

FIGURE 7-2:

Each VBA

module has a

Declarations

section, which

appears before

any Sub or

Function

procedures.

Suppose that you want to declare the CurrentValue variable so that it’s available to all the procedures in your module. All you need to do is use the Dim statement in

the Declarations section:

Dim CurrentValue As Double

With this declaration in place — and in the proper place — the CurrentValue variable can be used from any other procedure within the module, and it retains

its value from one procedure to another.

102    PART 3  Programming Concepts

Public variables

If you need to make a variable available to all the procedures in all your VBA mod-

ules in a workbook, declare the variable at the module level (in the Declarations

section) by using the Public keyword. Here’s an example:

Public CurrentRate As Long

The Public keyword makes the CurrentRate variable available to any procedure in

the workbook — even those in other VBA modules. You must insert this statement

before the first Sub or Function statement in a module.

If you’d like a variable to be available to modules in other workbooks, you must

declare the variable as Public and establish a reference to the workbook that contains the variable declaration. Set up a reference by choosing Tools ➪ References in the VBE. In practice, sharing a variable across workbooks is hardly ever done.

But it’s nice to know that it can be done, in case it ever comes up as a  Jeopardy!

question.

Static variables

Normally, when a procedure ends, all the procedure’s variables are reset.  Static  variables are special cases because they retain their value even when the procedure ends. You declare a static variable at the procedure level. A static variable may be useful if you need to track the number of times you execute a procedure. You can

declare a static variable and increment it each time you run the procedure.

As shown in the following example, you declare static variables by using the Static

keyword:

Sub MySub()

Static Counter As Integer

Dim Msg As String

Counter = Counter + 1

Msg = "Number of executions: " & Counter

MsgBox Msg

End Sub

The code keeps track of the number of times the procedure was executed and

displays the number in a message box. The value of the Counter variable isn’t

reset when the procedure ends, but it’s reset when you close and reopen the

workbook.

CHAPTER 7  Essential VBA Language Elements    103

Even though the value of a variable declared as Static is retained after a variable ends, that variable is unavailable to other procedures. In the preceding MySub

procedure example, the Counter variable and its value are available only within

the MySub procedure. In other words, it’s a procedure-level variable.

Life of variables

Nothing lives forever, including variables. The scope of a variable not only

determines where that variable may be used, but also affects the circumstances

under which the variable is removed from memory.

You can purge all variables from memory by using three methods:

» Click the Reset toolbar button (the little blue square button on the Standard toolbar in the VBE).

» Click End when a runtime error message dialog box shows up.

» Include an End statement anywhere in your code. This is not the same as an

End Sub or End Function statement.

Otherwise, only procedure-level variables will be removed from memory when

the macro code has completed running. Static variables, module-level variables,

and global (public) variables all retain their values in between runs of your code.

If you use module-level or global-level variables, make sure they have the values

you expect them to have. You never know whether one of the situations just men-

tioned may have caused your variables to lose their content!

Working with constants

A variable’s value may (and usually does) change while your procedure is execut-

ing. That’s why they call it a  variable . Sometimes, you need to refer to a value or string that never changes. In such a case, you need a  constant — a named element whose value doesn’t change.

As shown in the following examples, you declare constants by using the Const

statement. The declaration statement also gives the constant its value:

Const NumQuarters As Integer = 4

Const Rate = .0725, Period = 12

Const ModName As String = "Budget Macros"

Public Const AppName As String = "Budget Application"

104    PART 3  Programming Concepts

Using constants in place of hard-coded values or strings is an excellent programming practice. For example, if your procedure needs to refer to a specific

value (such as an interest rate) several times, it’s better to declare the value as a constant and refer to its name rather than the value. This makes your code more

readable and easier to change. And if the interest rate changes, you have to change

only one statement rather than several.

Like variables, constants have a scope. Keep these points in mind:

» To make a constant available within only a single procedure, declare the

constant after the procedure’s Sub or Function statement.

» To make a constant available to all procedures in a module, declare the

constant in the Declarations section for the module.

» To make a constant available to all modules in the workbook, use the Public keyword and declare the constant in the Declarations section of any module.

Unlike a variable, the value of a constant doesn’t vary. If you attempt to change

the value of a constant in a VBA routine, you get an error. This isn’t too surprising because the value of a constant must remain constant. If you need to change the

value of a constant while your code is running, what you really need is a variable.

Premade constants

Excel and VBA contain many predefined constants, which you can use without the

need to declare them yourself. The macro recorder usually uses constants rather

than actual values. In general, you don’t need to know the value of these constants

to use them. The following simple procedure uses a built-in constant (xlCalculation

Manual) to change the Calculation property of the Application object (in other

words, to change the Excel recalculation mode to manual):

Sub CalcManual()

Application.Calculation = xlCalculationManual

End Sub

If you look in Excel’s Help system for calculation modes, you’ll find this:

Name

Value

Description

xlCalculationAutomatic

–4105

Excel controls recalculation.

xlCalculationManual

–4135

Calculation is done when the user requests it.

xlCalculationSemiautomatic

2

Excel controls recalculation but ignores changes

in tables.

CHAPTER 7  Essential VBA Language Elements    105

So the actual value of the built-in xlCalculationManual constant is –4135.

Obviously, it’s easier to use the constant’s name than try to remember such an

odd value. As you can see, many of the built-in constants are just arbitrary

numbers that have special meaning to VBA.

To find the actual value of a built-in constant, use the Immediate window in the

VBE and execute a VBA statement such as the following:

? xlCalculationAutomatic

If the Immediate window isn’t visible, press Ctrl+G. The question mark is a short-

cut for typing Print.

Working with strings

Excel can work with both numbers and text, so it should come as no surprise that

VBA has this same power. Text is often referred to as a  string.  You can work with two types of strings in VBA:

» Fixed-length strings are declared with a specified number of characters. The maximum length is 65,526 characters. That’s a lot of characters! As a point of

reference, this chapter contains about half that many characters.

» Variable-length strings theoretically can hold as many as two billion characters.

If you type 5 characters per second, it would take you about 760 days to bang out

2 billion characters — assuming you don’t take any breaks to eat or sleep.

When declaring a string variable with a Dim statement, you can specify the maximum length if you know it (it’s a fixed-length string) or let VBA handle it

dynamically (it’s a variable-length string). The following example declares the

MyString variable as a string with a maximum length of 50 characters. (Use an

asterisk to specify the number of characters, up to the 65,526-character limit.)

YourString is also declared as a string, but its length is unspecified:

Dim MyString As String * 50

Dim YourString As String

When declaring a fixed-length string that exceeds 999, don’t use a comma in the

number that specifies the string size. In fact, never use commas when entering a

numeric value in VBA. VBA doesn’t like that.

106    PART 3  Programming Concepts

Working with dates

Another data type you may find useful is Date. You can use a string variable to

store dates, but then you can’t perform date calculations. Using the Date data type

gives your routines greater flexibility. For example, you might need to calculate

the number of days between two dates. This would be impossible (or at least

extremely challenging) if you used strings to hold your dates.

A variable defined as a Date can hold dates ranging from January 1, 0100, to December 31, 9999. That’s a span of nearly 10,000 years and more than enough

for even the most aggressive financial forecast. You can also use the Date data type to work with time data. (VBA lacks a Time data type.)

These examples declare variables and constants as a Date data type:

Dim Today As Date

Dim StartTime As Date

Const FirstDay As Date = #1/1/2019#

Const Noon = #12:00:00#

In VBA, place dates and times between two hash marks, as shown in the preceding

examples.

Date variables display dates according to your system’s short date format, and they display times according to your system’s time format (either 12- or 24-hour

formatting). The Windows Registry stores these settings, and you can modify

them via the Regional and Language Settings dialog box in the Windows Control

Panel. Therefore, the VBA-displayed date or time format may vary, depending on

the settings for the system on which the application is running.

When writing VBA code, however, you must use one of the U.S. date formats (such

as mm/dd/yyyy). So the following statement assigns a day in October (not

November) to the MyDate variable (even if your system is set to use dd/mm/yyyy

for dates):

MyDate = #10/11/2019#

When you display the variable (with the MsgBox function, for example), VBA

shows MyDate using your system settings. So if your system uses the dd/mm/yyyy

date format, MyDate is displayed as 11/10/2019.

CHAPTER 7  Essential VBA Language Elements    107

Using Assignment Statements

An  assignment statement is a VBA statement that assigns the result of an expression to a variable or an object. Excel’s Help system defines the term expression as

. . . a combination of keywords, operators, variables, and constants that yields a

string, number, or object. An expression can be used to perform a calculation,

manipulate characters, or test data.

Much of your work in VBA involves developing (and debugging) expressions. If

you know how to create formulas in Excel, you’ll have no trouble creating expres-

sions. With a worksheet formula, Excel displays the result in a cell. A VBA expres-

sion, on the other hand, can be assigned to a variable.

Assignment statement examples

In the assignment statement examples that follow, the expressions are to the

right of the equal sign:

x = 1

x = x + 1

x = (y * 2) / (z * 2)

HouseCost = 375000

FileOpen = True

Range("TheYear").Value = 2019

Expressions can be as complex as you need them to be; use the line continuation

character (a space followed by an underscore) to make lengthy expressions easier

to read.

Often, expressions use functions: VBA’s built-in functions, Excel’s worksheet

functions, or functions that you develop with VBA. Functions are discussed in Chapter 9.

About that equal sign

As you can see in the preceding example, VBA uses the equal sign as its assign-

ment operator. You’re probably accustomed to using an equal sign as a mathe-

matical symbol for equality. Therefore, an assignment statement like the following

may cause you to raise your eyebrows:

z = z + 1

108    PART 3  Programming Concepts

In what crazy universe is z equal to itself plus 1? Answer: No known universe. In this case, the assignment statement (when executed) increases the value of z by 1.

So if z is 12, executing the statement makes z equal to 13. Just remember that an

assignment uses the equal sign as an operator, not a symbol of equality.

Smooth operators

Operators play major roles in VBA. Besides the equal-sign operator (discussed in

the previous section), VBA provides several operators. Table 7-3 lists these operators. These should be familiar to you because they’re the same operators

used in worksheet formulas (except for the Mod operator).

TABLE 7-3

VBA’s Operators

Function

Operator Symbol

Addition

+

Multiplication

*

Division

/

Subtraction

–

Exponentiation

^

String concatenation

&

Integer division (the result is always an integer)

\

Modulo arithmetic (returns the remainder of a division operation)

Mod

When you’re writing an Excel formula, you do modulo arithmetic by using the

MOD function. For example, the following formula returns 2 (the remainder when

you divide 12 by 5):

=MOD(12,5)

In VBA, the Mod operator is used like this (and z has a value of 2):

z = 12 Mod 5

The term  concatenation is programmer speak for「join together.」Thus, if you concatenate strings, you’re combining strings to make a new and improved string.

CHAPTER 7  Essential VBA Language Elements    109

As shown in Table 7-4, VBA also provides a full set of logical operators.

TABLE 7-4

VBA’s Logical Operators

Operator

What It Does

Not

Performs a logical negation on an expression

And

Performs a logical conjunction on two expressions

Or

Performs a logical disjunction on two expressions

Xor

Performs a logical exclusion on two expressions

Eqv

Performs a logical equivalence on two expressions

Imp

Performs a logical implication on two expressions

The precedence order for operators in VBA is exactly the same as in Excel formulas.

Exponentiation has the highest precedence. Multiplication and division come

next, followed by addition and subtraction. You can use parentheses to change the natural precedence order, making whatever’s sandwiched in parentheses

come before any operator. Take a look at this code:

x = 3

y = 2

z = x + 5 * y

When the preceding code is executed, what’s the value of z? If you answered 13,

you get a gold star that proves you understand the concept of operator precedence.

If you answered 16, read this: The multiplication operation (5 * y) is performed

first, and that result is added to x.

If you have trouble remembering the correct operator precedence, add parenthesis

around the parts that get calculated first. For example, the previous assignment

statement looks like this with parethesis:

z = x + (5 * y)

Don’t be shy about using parentheses even when they aren’t required — especially

if doing so makes your code easier to understand. VBA doesn’t care if you use extra

parentheses.

110    PART 3  Programming Concepts

Working with Arrays

Like most programming languages, VBA supports arrays. An  array is a group of variables that share a name. You refer to a specific variable in the array by using

the array name and an index number in parentheses. For example, you can define

an array of 12 string variables to hold the names of the months of the year. If you

name the array  MonthNames , you can refer to the first element of the array as MonthNames (1), the second element as MonthNames (2), and so on.

Declaring arrays

Before you can use an array, you  must declare it. No exceptions. Unlike with normal variables, VBA is very strict about this rule. You declare an array with a

Dim statement, just as you declare a regular variable. However, you also need to

specify the number of elements in the array. You do this by specifying the first

index number, the keyword To, and the last index number — all inside parentheses.

The following example shows how to declare an array of 100 integers:

Dim MyArray(1 To 100) As Integer

When you declare an array, you can choose to specify only the upper index. If you

omit the lower index, VBA assumes that it’s 0. Therefore, both of the following

statements declare the same 101-element array:

Dim MyArray (0 To 100) As Integer

Dim MyArray (100) As Integer

If you want VBA to assume that 1 (rather than 0) is the lower index for your arrays, include the following statement in the Declarations section at the top of your module:

Option Base 1

This statement forces VBA to use 1 as the first index number for arrays that declare only the upper index. If this statement is present, the following statements are

identical, both declaring a 100-element array:

Dim MyArray (1 To 100) As Integer

Dim MyArray (100) As Integer

CHAPTER 7  Essential VBA Language Elements    111

Multidimensional arrays

The arrays created in the previous examples are all one-dimensional arrays. Think

of one-dimensional arrays as a single line of values. Arrays you create in VBA can

have as many as 60 dimensions — although you rarely need more than two or

three dimensions in an array. The following example declares an 81-integer array

with two dimensions:

Dim MyArray (1 To 9, 1 To 9) As Integer

You can think of this array as occupying a 9 x 9 matrix — perfect for storing all

numbers in a Sudoku puzzle.

To refer to a specific element in this array, you need to specify two index numbers

(similar to its「row」and its「column」in the matrix). The following example

shows how you can assign a value to an element in this array:

MyArray (3, 4)= 125

This statement assigns a value to a single element in the array. If you’re thinking

of the array in terms of a 9 x 9 matrix, this assigns 125 to the element located in

the third row and fourth column of the matrix.

Here’s how to declare a three-dimensional array, with 1,000 elements:

Dim My3DArray (1 To 10, 1 To 10, 1 To 10) As Integer

You can think of a three-dimensional array as a cube. Visualizing an array of more

than three dimensions is more difficult.

Dynamic arrays

You can also create  dynamic arrays. A dynamic array doesn’t have a preset number of elements. Declare a dynamic array with an empty set of parentheses:

Dim MyArray () As Integer

Before you can use this array, you must use the ReDim statement to tell VBA how

many elements the array has. Usually, the number of elements in the array is

determined while your code is running. You can use the ReDim statement any number of times, changing the array’s size as often as needed. The following example demonstrates how to change the number of elements in a dynamic array.

112    PART 3  Programming Concepts

It assumes that the NumElements variable contains a value, which your code calculated.

ReDim MyArray (1 To NumElements)

When you redimension an array by using ReDim, you wipe out any values

currently stored in the array elements. You can avoid destroying the old values by

using the Preserve keyword. The following example shows how you can preserve

an array’s values when you redimension the array:

ReDim Preserve MyArray (1 To NumElements)

If MyArray currently has ten elements, and you execute the preceding statement

with NumElements equaling 12, the first ten elements remain intact, and the array

has room for two additional elements (up to the number contained in the variable

NumElements). If NumElements equals 7 however, the first seven elements are

retained but the remaining three elements meet their demise.

The topic of arrays comes up again in Chapter 10, when you explore the concept of

looping.

Using Labels

In early versions of BASIC, every line of code required a line number. For example,

if you had written a BASIC program in the ’70s (dressed, of course, in your bell

bottoms), it may have looked something like this:

010: LET X=5

020: LET Y=3

030: LET Z=X*Y

040: PRINT Z

050: END

VBA permits the use of such line numbers, and it even permits text labels. You

don’t typically use a label for each line, but you may occasionally need to use a

label. For example, insert a label if you use a GoTo statement (discussed in Chapter 10). A label must begin with the first nonblank character in a line and end

with a colon.

CHAPTER 7  Essential VBA Language Elements    113

IN THIS CHAPTER

» Finding out why Range objects are so

important

» Understanding the various ways of

referring to ranges

» Discovering some of the most useful

Range object properties

» Uncovering some of the most useful

Range object methods

Chapter 8

Working with Range

Objects

T his chapter digs a bit deeper into Excel’s dungeons and takes a closer look

at Range objects. Excel is all about cells, and the Range object is a container


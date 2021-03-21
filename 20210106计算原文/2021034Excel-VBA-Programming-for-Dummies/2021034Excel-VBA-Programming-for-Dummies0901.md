T here are three flavors of functions: those built into VBA (vanilla), those built into Excel (strawberry), and other functions written in VBA (chocolate).

Previous chapters mention how you can use functions in your VBA expres-

sions, and this chapter provides a full explanation. Functions can make your VBA

code perform some powerful feats, with little or no programming effort required.

If you like that idea, this chapter's for you.

What Is a Function?

Except for a few people who think Excel is a word processor, all Excel users incor-

porate worksheet functions in their formulas. The most common worksheet func-

tion is the SUM function, and you have more than 500 others at your disposal.

A  function essentially performs a calculation and returns a single value. The SUM

function, of course, returns the sum of a range of values. The same holds true for

functions used in your VBA expressions: Each function does its thing and returns

a single value.

CHAPTER 9  Using VBA and Worksheet Functions    131

The functions you use in VBA can come from three sources:

» Built-in functions provided by VBA

» Worksheet functions provided by Excel

» Custom functions that you (or someone else) write, using VBA

The rest of this chapter clarifies the differences.

Using Built-In VBA Functions

VBA provides numerous built-in functions. Some of these functions take argu-

ments, and some do not.

VBA function examples

This section presents a few examples of using VBA functions in code. In many of

these examples, the MsgBox function displays a value in a message box. Yes, MsgBox is a VBA function — a rather unusual one, but a function nonetheless.

This useful function displays a message in a dialog box and also returns a value.

For more details about the MsgBox function, see Chapter 15.

A workbook that contains all the examples is available at this book's website.

Displaying the system date or time

The first example uses VBA's Date function to display the current system date in

a message box:

Sub ShowDate()

MsgBox "Today is: " & Date

End Sub

Notice that the Date function doesn't use an argument. Unlike worksheet func-

tions, a VBA function with no argument doesn't require an empty set of parenthe-

ses. In fact, if you type an empty set of parentheses, the VBE promptly removes

them.

To get the system time, use the Time function. And if you want it all, use the Now

function to return both the date and the time.

132    PART 3  Programming Concepts

Finding a string length

The following procedure uses the VBA Len function, which returns the length of a

text string. The Len function takes one argument: the string. When you execute

this procedure, the message box displays your name, and the number of charac-

ters in your name (see Figure 9-1).

Sub GetLength()

Dim MyName As String

Dim StringLength As Long

MyName = Application.UserName

StringLength = Len(MyName)

MsgBox MyName & " has " & StringLength & " characters."

End Sub

FIGURE 9-1:

Calculating the

length of your

name.

Excel also has a LEN function, which you can use in your worksheet formulas. The

Excel version and the VBA function work the same.

Displaying the name of a month

The following procedure uses the MonthName function, which returns the name

of a month. MonthName uses one argument: an integer between 1 and 12.

Sub ShowMonthName()

Dim ThisMonth As Long

ThisMonth = Month(Date)

MsgBox MonthName(ThisMonth)

End Sub

This procedure uses the Month function to get the current month (as a value), and

this value is assigned to the ThisMonth variable. The MonthName function then

converts the value to text. So if you run this procedure in April, the message box

displays the text April.

CHAPTER 9  Using VBA and Worksheet Functions    133

Actually, the ThisMonth variable isn't required. You can get the same effect with this expression, which uses three VBA functions:

MonthName(Month(Date))

Here, the current date is passed as an argument to the Month function, which returns a value that's passed as an argument to the MonthName function.

Determining a file size

The following Sub procedure displays the size, in bytes, of the Excel executable

file. It finds this value by using the FileLen function:

Sub GetFileSize()

Dim TheFile As String

TheFile = "C:\Program Files (x86)\Microsoft Office\root\Office16\EXCEL.EXE"

MsgBox FileLen(TheFile)

End Sub

Notice that this routine  hard-codes the filename (that is, explicitly states the path).

This isn't a good idea. The file may not be on the C drive, or the Excel folder may

have a different name. The following statement shows a better approach:

TheFile = Application.Path & "\EXCEL.EXE"

Path is a property of the Application object. It simply returns the name of the folder in which the application (that is, Excel) is installed (without a trailing backslash).

Identifying the type of a selected object

The following procedure uses the TypeName function, which returns the type of

the selection on the worksheet (as a string):

Sub ShowSelectionType()

Dim SelType As String

SelType = TypeName(Selection)

MsgBox SelType

End Sub

The selection could be a Range, a Picture, a Rectangle, a ChartArea, or any other

type of object that can be selected.

134    PART 3  Programming Concepts

The TypeName function is very versatile. You can also use this function to deter-

mine the data type of a variable.

VBA functions that do more

than return a value

A few VBA functions go above and beyond the call of duty. Rather than simply

return a value, these functions have some useful side effects. Table 9-1 lists them.

TABLE 9-1

VBA Functions with Useful Side Benefits

Function

What It Does

MsgBox

Displays a handy dialog box containing a message and buttons. The function returns a code that identifies which button the user clicks. See Chapter 15 for details.

InputBox

Displays a simple dialog box that asks the user for some input. The function returns whatever the user enters in the dialog box. Chapter 15 explores the InputBox function.

Shell

Executes another program. The function returns the  task ID (a unique identifier) of the other program (or an error if the function can't start the other program).

Discovering VBA functions

How do you find out which functions VBA provides? Good question. The best source is the Excel VBA system. Another way is to type VBA , followed by a period.

You get a list of items, as shown in Figure 9-2. Those with a green icon are functions. If this feature isn't working, choose VBE's Tools ➪ Options, click the Editor tab, and place a check next to Auto List Members.

FIGURE 9-2:

A way to display

a list of VBA

functions.

There are over 140 different functions available in VBA. Some are so specialized

and obscure, you'll never need them. Others, however, are quite useful for many

applications. Table 9-2 lists some of the more useful functions.

CHAPTER 9  Using VBA and Worksheet Functions    135

TABLE 9-2

VBA's Most Useful Built-In Functions

Function

What It Does

Abs

Returns a number's absolute value

Array

Returns a variant containing an array

Choose

Returns a value from a list of items

Chr

Converts an ANSI value to a string

CurDir

Returns the current path

Date

Returns the current system date

DateAdd

Returns a date to which a specified time interval has been added — for example, one

month from a particular date

DateDiff

Returns an integer showing the number of specified time intervals between two dates —

for example, the number of months between now and your birthday

DatePart

Returns an integer containing the specified part of a given date — for example, a date's day of the year

DateSerial

Converts a date to a serial number

DateValue

Converts a string to a date

Day

Returns the day of the month from a date value

Dir

Returns the name of a file or directory that matches a pattern

Err

Returns the error number of an error condition

Error

Returns the error message that corresponds to an error number

Exp

Returns the base of the natural logarithm (e) raised to a power

FileLen

Returns the number of bytes in a file

Fix

Returns a number's integer portion

Format

Displays an expression in a particular format

GetSetting

Returns a value from the Windows registry

Hour

Returns the hour portion of a time

InputBox

Displays a box to prompt a user for input

InStr

Returns the position of a string within another string (counting from the start)

InStrRev

Returns the position of a string within another string (counting from the end)

Int

Returns the integer portion of a number

IsArray

Returns True if a variable is an array

IsDate

Returns True if an expression is a date

136    PART 3  Programming Concepts

Function

What It Does

IsEmpty

Returns True if a variable has not been initialized

IsError

Returns True if an expression is an error value

IsMissing

Returns True if an optional argument was not passed to a procedure

IsNull

Returns True if an expression contains no valid data

IsNumeric

Returns True if an expression can be evaluated as a number

LBound

Returns the smallest subscript for a dimension of an array

LCase

Returns a string converted to lowercase

Left

Returns a specified number of characters from the left of a string

Len

Returns the number of characters in a string

Mid

Returns a specified number of characters from a string

Minute

Returns the minutes portion of a time value

Month

Returns the month from a date value

MsgBox

Displays a message box and (optionally) returns a value

Now

Returns the current system date and time

Replace

Replaces a substring in a string with another substring

RGB

Returns a numeric RGB value representing a color

Right

Returns a specified number of characters from the right of a string

Rnd

Returns a random number between 0 and 1

Second

Returns the seconds portion of a time value

Shell

Runs an executable program

Space

Returns a string with a specified number of spaces

Split

Splits a string into parts, using a delimiting character

Sqr

Returns a number's square root

String

Returns a repeating character or string

Time

Returns the current system time

Timer

Returns the number of seconds since midnight

TimeSerial

Returns the time for a specified hour, minute, and second

TimeValue

Converts a string to a time serial number

(continued)

CHAPTER 9  Using VBA and Worksheet Functions    137

TABLE 9-2  (continued)

Function

What It Does

Trim

Returns a string without leading or trailing spaces

TypeName

Returns a string that describes a variable's data type

UBound

Returns the largest available subscript for an array's dimension

UCase

Converts a string to uppercase

Val

Returns the numbers contained in a string

Weekday

Returns a number representing a day of the week

Year

Returns the year from a date value

For complete details on a particular function, type the function name in a VBA

module, move the cursor anywhere in the text, and press F1.

Using Worksheet Functions in VBA

Although VBA offers a decent assortment of built-in functions, you might not always find exactly what you need. Fortunately, you can also use most of Excel's

worksheet functions in your VBA procedures. The only worksheet functions that

you can't use are those that have an equivalent VBA function. For example, you

can't use Excel's RAND function (which generates a random number) because VBA

has an equivalent function: Rnd.

VBA makes Excel's worksheet functions available through the WorksheetFunction

object, which is contained in the Application object. Here's an example of how you

can use Excel's SUM function in a VBA statement:

Total = Application.WorksheetFunction.SUM(Range("A1:A12"))

You can omit either the Application part or the WorksheetFunction part of the expression. In either case, VBA figures out what you're doing. In other words, these three expressions all work exactly the same:

Total = Application.WorksheetFunction.SUM(Range("A1:A12"))

Total = WorksheetFunction.SUM(Range("A1:A12"))

Total = Application.SUM(Range("A1:A12"))

138    PART 3  Programming Concepts

Worksheet function examples

Many of Excel's worksheet functions can be used in your VBA expressions. Think

of worksheet functions as plug-ins you can use to extend the utility of your own

procedures. In this section, you discover how to incorporate Excel worksheet functions into your VBA code.

Finding the maximum value in a range

Here's an example that shows how to use Excel's MAX worksheet function in a

VBA procedure. This procedure displays the maximum value in column A of the

active worksheet (see Figure 9-3):

Sub ShowMax()

Dim TheMax As Double

TheMax = WorksheetFunction.MAX(Range("A:A"))

MsgBox TheMax

End Sub

FIGURE 9-3:

Using a

worksheet

function in

your VBA

code.

You can use the MIN function to get the smallest value in a range. And as you

might expect, you can use other worksheet functions in a similar manner. For example, you can use the LARGE function to determine the  k th-largest value in a range. The following expression demonstrates this:

SecondHighest = WorksheetFunction.LARGE(Range("A:A"),2)

Notice that the LARGE function uses two arguments. The second argument repre-

sents the  k th part — 2, in this case (the second-largest value).

CHAPTER 9  Using VBA and Worksheet Functions    139

Calculating a mortgage payment

The next example uses the PMT worksheet function to calculate a mortgage pay-

ment. This procedure uses three variables to store the data that's passed to the

PMT function as arguments. A message box displays the calculated payment.

Sub PmtCalc()

Dim IntRate As Double

Dim LoanAmt As Double

Dim Periods As Long

IntRate = 0.0625 / 12

Periods = 30 * 12

LoanAmt = 150000

MsgBox WorksheetFunction.PMT(IntRate, Periods, -LoanAmt)

End Sub

As the following statement shows, you can also insert the values directly as the

function arguments:

MsgBox WorksheetFunction.PMT(0.0625 /12, 360, -150000)

However, using variables to store the parameters makes the code easier to read

and modify, if necessary.

Using a lookup function

The following example uses VBA's InputBox and MsgBox functions, plus Excel's

VLOOKUP function. It prompts for a part number and then gets the price from a

lookup table. In Figure 9-4, range A1:B13 is named PriceList.

Sub GetPrice()

Dim PartNum As Variant

Dim Price As Double

PartNum = InputBox("Enter the Part Number")

Sheets("Prices").Activate

Price = WorksheetFunction.VLOOKUP(PartNum, Range("PriceList"), 2, False)

MsgBox PartNum & " costs " & Price

End Sub

You can download this workbook from the book's website.

140    PART 3  Programming Concepts

FIGURE 9-4:

The range,

named PriceList,

contains prices

for parts.

Here's how the GetPrice procedure works:

1. VBA's InputBox function asks the user for a part number.

2. The part number the user enters is assigned to the PartNum variable.

3. The next statement activates the Prices worksheet, just in case it's not already the active sheet.

4. The code uses the VLOOKUP function to find the part number in the table.

Notice that the arguments you use in this statement are the same as those you

would use with the function in a worksheet formula. This statement assigns

the result of the function to the Price variable.

5. The code displays the price for the part via the MsgBox function.

This procedure doesn't have any error handling, and it fails miserably if you enter

a nonexistent part number. (Try it.) If this were an actual application that's used

in an actual business, you would want to add some statements that deal with errors more gracefully. Chapter 12 discusess error handling.

Entering worksheet functions

You can't use the Excel Paste Function dialog box to insert a worksheet function

into a VBA module. Instead, enter such functions the old-fashioned way: by hand.

However, you  can use the Paste Function dialog box to identify the function you want to use and find out about its arguments.

CHAPTER 9  Using VBA and Worksheet Functions    141

You can also take advantage of the VBE's Auto List Members option, which dis-

plays a drop-down list of all worksheet functions. Just type Application.Work-

sheetFunction , followed by a period. Then you see a list of the functions you can use, as shown in Figure 9-5. If this feature isn't working, choose the VBE's Tools ➪ Options, click the Editor tab, and place a check next to Auto List Members.

FIGURE 9-5:

Getting a list of

worksheet

functions that

you can use in

your VBA code.

More about using worksheet functions

Newcomers to VBA often confuse VBA's built-in functions and Excel's workbook

functions. A good rule to remember is that VBA doesn't try to reinvent the wheel.

For the most part, VBA doesn't duplicate Excel worksheet functions.

For most worksheet functions that are unavailable as methods of the Worksheet-

Function object, you can use an equivalent VBA built-in operator or function. For

example, the MOD worksheet function is not available in the WorksheetFunction

object because VBA has an equivalent: its built-in Mod operator.

Bottom line? If you need to use a function, first determine whether VBA has some-

thing that meets your needs. If not, check out the worksheet functions. If all else

fails, you may be able to write a custom function by using VBA.

Using Custom Functions

After you know how to handle VBA functions and Excel worksheet functions, you

can dive into the third category of functions you can use in your VBA procedures:

custom functions. A  custom function (also known as a User Defined Function, or UDF) is one you develop yourself by using (what else?) VBA. To use a custom function, you must define it in the workbook in which you use it — or else define the

functions in an add-in (see Chapter 21).

142    PART 3  Programming Concepts

Here's an example of defining a simple Function procedure (MultiplyTwo) and then using it in a VBA Sub procedure (ShowResult):

Function MultiplyTwo(num1, num2) As Double

MultiplyTwo = num1 * num2

End Function

Sub ShowResult()

Dim n1 As Double, n2 As Double

Dim Result As Double

n1 = 123

n2 = 544

Result = MultiplyTwo(n1, n2)

MsgBox Result

End Sub

The custom function MultiplyTwo has two arguments. The ShowResult Sub pro-

cedure uses this Function procedure by passing two arguments to it (in parenthe-

ses). The ShowResult procedure then displays a message box showing the value

returned by the MultiplyTwo function.

Of course, most custom functions aren't as trivial as the MultiplyTwo function.

But this example should give you an idea of how a Sub procedure can make use of

a custom function.

You can also use custom functions in your worksheet formulas. For example, if

MultiplyTwo is defined in your workbook, you can write a formula such as this one:

=MultiplyTwo(A1,A2)

This formula returns the product of the values in cells A1 and A2.

Creating custom worksheet functions is an important (and very useful) topic. So

important (and useful) that Chapter 20 includes examples that are actually useful.

CHAPTER 9  Using VBA and Worksheet Functions    143

IN THIS CHAPTER

» Discovering methods for controlling

the flow of your VBA procedures

» Finding out about the dreaded GoTo

statement

» Using If-Then and Select Case

structures

» Performing looping in your

procedures

Chapter 10

Controlling Program

Flow and Making

Decisions

S ome VBA procedures start at the code's beginning and progress line by line

to the end, never deviating from this top-to-bottom program flow. Macros


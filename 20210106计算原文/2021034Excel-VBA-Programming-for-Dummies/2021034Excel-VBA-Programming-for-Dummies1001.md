that you record always work like this. In many cases, however, you need to

control the flow of your code by skipping some statements, executing some state-

ments multiple times, and testing conditions to determine what the procedure does next. Hang on to your hat and enjoy the ride, because you're about to discover the essence of programming.

Going with the Flow, Dude

Some programming newbies can't understand how a dumb computer can make

intelligent decisions. The secret is in several programming constructs that most

programming languages support. Table 10-1 provides a sneak preview of these constructs. (These are explained later in this chapter.)

CHAPTER 10  Controlling Program Flow and Making Decisions    145

TABLE 10-1

Programming Constructs for Making Decisions

Construct

How It Works

GoTo statement

Jumps to a particular statement

If-Then structure

Does something if something else is true

Select Case

Does any of several things, depending on something's value

For-Next loop

Executes a series of statements a specified number of times

Do-While loop

Does something as long as something else remains true

Do-Until loop

Does something until something else becomes true

The GoTo Statement

A GoTo statement offers the most straightforward means for changing a

program's flow. The GoTo statement simply transfers program execution to a new statement, which is preceded by a label.

Your VBA procedures can contain as many labels as you like. A  label is just a text string followed by a colon.

The following procedure shows how a GoTo statement works:

Sub CheckUser()

UserName = InputBox("Enter Your Name: ")

If UserName <> "Satya Nadella" Then GoTo WrongName

MsgBox ("Welcome Satya...")

'   ...[More code here] ...

Exit Sub

WrongName:

MsgBox "Sorry. Only Satya Nadella can run this."

End Sub

The procedure uses the InputBox function to get the user's name. Then a decision

is made: If the user enters a name other than Satya Nadella, the program flow

jumps to the WrongName label, displays an apologetic message, and the proce-

dure ends. On the other hand, if Mr. Nadella runs this macro and uses his real

name, the procedure displays a welcome message and then executes some

additional code (not shown in the example).

Notice that the Exit Sub statement ends the procedure before the second MsgBox

function has a chance to work. Without that Exit Sub statement, both MsgBox statements would be executed.

146    PART 3  Programming Concepts

WHAT IS STRUCTURED PROGRAMMING?

DOES IT MATTER?

If you hang around with programmers, sooner or later you hear the term  structured  programming . This term has been around for decades, and programmers generally agree that structured programs are superior to unstructured programs. So what is

structured programming? And can you do that using VBA?

The basic premise of structured programming is that a procedure or code segment

should have only one entry point and one exit point. In other words, a block of code should be a stand-alone unit. A program cannot jump into the middle of this unit;

neither can it exit at any point except the single exit point. When you write structured code, your program progresses in an orderly manner and is easy to follow — unlike a

program that jumps around in a haphazard fashion. This pretty much rules out using

the GoTo statement.

In general, a structured program is easier to read and understand. More important,

it's also easier to modify when the need arises.

VBA is indeed a structured language. It offers standard structured constructs such

as If-Then-Else, For-Next loops, Do-Until loops, Do-While loops, and Select Case

structures. Furthermore, it fully supports module code constructions. If you're new

to programming, you should try to develop good structure-programming habits

early on. End of lecture.

This simple procedure works, but VBA provides several better (and more

structured) alternatives than GoTo. In general, you should use GoTo only when

you have no other way to perform an action. In real life, the only time you  must use a GoTo statement is for trapping errors. (You get a detailed review of error

handling in Chapter 12.)

By the way, the CheckUser procedure simply demonstrates the GoTo statement.

It's not intended to demonstrate an effective security technique!

Many hard-core programming types have a deep-seated hatred for GoTo state-

ments because using them tends to result in difficult-to-read (and difficult-to-

maintain)「spaghetti code.」Therefore, you should never admit that you use GoTo

statements when talking with other programmers.

CHAPTER 10  Controlling Program Flow and Making Decisions    147

Decisions, Decisions

As in many other aspects of life, effective decision-making is the key to success

in writing Excel macros. This section reviews two programming structures

that can empower your VBA procedures with some impressive decision-making

capabilities: If-Then and Select Case.

The If-Then structure

The If-Then structure is VBA's most important control structure. You'll probably

use this command on a daily basis.

Use the If-Then structure when you want to execute one or more statements conditionally. The optional Else clause, if included, lets you execute one or more

statements if the condition you're testing is  not true. Here's the simple CheckUser procedure presented earlier in this chapter, recoded to use the If-Then-Else structure:

Sub CheckUser2()

UserName = InputBox("Enter Your Name: ")

If UserName = "Satya Nadella" Then

MsgBox ("Welcome Satya...")

'    ...[More code here] ...

Else

MsgBox "Sorry. Only Satya Nadella can run this."

End If

End Sub

You would probably agree that this version is much easier to follow.

A workbook that contains this section's examples can be downloaded from this

book's website.

If-Then examples

The following procedure demonstrates the If-Then structure without the optional

Else clause:

Sub GreetMe()

If Time < 0.5 Then MsgBox "Good Morning"

End Sub

148    PART 3  Programming Concepts

The GreetMe procedure uses VBA's Time function to get the system time. If the current time is less than .5 (in other words, before noon), the procedure displays

a friendly greeting. If Time is greater than or equal to .5, the procedure ends, and nothing happens.

To display a different greeting if Time is greater than or equal to .5, you can add

another If-Then statement after the first one:

Sub GreetMe2()

If Time < 0.5 Then MsgBox "Good Morning"

If Time >= 0.5 Then MsgBox "Good Afternoon"

End Sub

Notice that the second If-Then statement uses >= (greater than or equal to). This ensures that the entire day is covered. Had it used > (greater than), no message

would appear if this procedure were executed at precisely 12:00 noon. That's pretty unlikely, but with an important program like this, you don't want to take

any chances.

An If-Then-Else example

Another approach to the preceding problem uses the Else clause. Here's the same

procedure recoded to use the If-Then-Else structure:

Sub GreetMe3()

If Time < 0.5 Then MsgBox "Good Morning" Else _

MsgBox "Good Afternoon"

End Sub

Notice the line continuation character (underscore) in the preceding example. The

If-Then-Else statement is actually a single statement. VBA provides a slightly dif-

ferent way of coding If-Then-Else constructs that use an End If statement. There-

fore, the GreetMe procedure can be rewritten as

Sub GreetMe4()

If Time < 0.5 Then

MsgBox "Good Morning"

Else

MsgBox "Good Afternoon"

End If

End Sub

CHAPTER 10  Controlling Program Flow and Making Decisions    149

In fact, you can insert any number of statements under the If part and any number of statements under the Else part. This syntax is easier to read and makes the statements shorter.

What if you need to expand the GreetMe procedure to handle three conditions:

morning, afternoon, and evening? You have two options: Use three If-Then

statements or use a  nested  If-Then-Else structure.  Nesting means placing an If-Then-Else structure within another If-Then-Else structure. The first approach,

using three If-Then statements, is simpler:

Sub GreetMe5()

Dim Msg As String

If Time < 0.5 Then Msg = "Morning"

If Time >= 0.5 And Time < 0.75 Then Msg = "Afternoon"

If Time >= 0.75 Then Msg = "Evening"

MsgBox "Good " & Msg

End Sub

Now, you can get fancy by using a variable. The Msg variable gets a different text

value, depending on the time of day. The MsgBox statement displays the greeting:

Good Morning, Good Afternoon, or Good Evening.

The following procedure performs the same action but uses an If-Then-End If

structure:

Sub GreetMe6()

Dim Msg As String

If Time < 0.5 Then

Msg = "Morning"

End If

If Time >= 0.5 And Time < 0.75 Then

Msg = "Afternoon"

End If

If Time >= 0.75 Then

Msg = "Evening"

End If

MsgBox "Good " & Msg

End Sub

Using ElseIf

In the previous examples, every statement in the procedure is executed — even in

the morning. A slightly more efficient structure would exit the procedure as soon

as a condition is found to be true. In the morning, for example, the procedure should display the Good Morning message and then exit — without evaluating the

other superfluous conditions.

150    PART 3  Programming Concepts

With a tiny procedure like this, you don't have to worry about execution speed. But for larger applications in which speed is critical, you should know about another

syntax for the If-Then structure: ElseIf.

Here's how you can rewrite the GreetMe procedure by using this syntax:

Sub GreetMe7()

Dim Msg As String

If Time < 0.5 Then

Msg = "Morning"

ElseIf Time >= 0.5 And Time < 0.75 Then

Msg = "Afternoon"

Else

Msg = "Evening"

End If

MsgBox "Good " & Msg

End Sub

When a condition is true, VBA executes the conditional statements, and the If structure ends. In other words, VBA doesn't waste time evaluating the extraneous

conditions, which makes this procedure a bit more efficient than the previous examples. The trade-off (there are always trade-offs) is that the code is more difficult to understand. (Of course, you already knew that.)

Another If-Then example

Here's another example that uses the simple form of the If-Then structure. This

procedure prompts the user for a quantity and then displays the appropriate discount, based on the quantity the user enters:

Sub ShowDiscount()

Dim Quantity As Long

Dim Discount As Double

Quantity = InputBox("Enter Quantity:")

If Quantity > 0 Then Discount = 0.1

If Quantity >= 25 Then Discount = 0.15

If Quantity >= 50 Then Discount = 0.2

If Quantity >= 75 Then Discount = 0.25

MsgBox "Discount: " & Discount

End Sub

Notice that each If-Then statement in this procedure is executed, and the value

for Discount can change as the statements are executed. However, the procedure

ultimately displays the correct value for Discount because the If-Then statements

are in order of ascending Discount values.

CHAPTER 10  Controlling Program Flow and Making Decisions    151

The following procedure performs the same tasks by using the alternative ElseIf syntax. In this case, the procedure ends immediately after executing the statements for a true condition:

Sub ShowDiscount2()

Dim Quantity As Long

Dim Discount As Double

Quantity = InputBox("Enter Quantity: ")

If Quantity > 0 And Quantity < 25 Then

Discount = 0.1

ElseIf Quantity >= 25 And Quantity < 50 Then

Discount = 0.15

ElseIf Quantity >= 50 And Quantity < 75 Then

Discount = 0.2

ElseIf Quantity >= 75 Then

Discount = 0.25

End If

MsgBox "Discount: " & Discount

End Sub

As important as the If-Then structure is to VBA, they become cumbersome when

a decision involves three or more choices. Fortunately, the Select Case structure,

discussed in the next section, offers a simpler and more efficient approach.

The Select Case structure

The Select Case structure is useful for decisions involving three or more options

(although it also works with two options, providing an alternative to the If-Then-

Else structure).

The examples in this section are available at this book's website.

A Select Case example

The following example shows how to use the Select Case structure. This also shows another way to code the examples presented in the previous section:

Sub ShowDiscount3()

Dim Quantity As Long

Dim Discount As Double

Quantity = InputBox("Enter Quantity: ")

Select Case Quantity

Case 0 To 24

Discount = 0.1

152    PART 3  Programming Concepts

Case 25 To 49

Discount = 0.15

Case 50 To 74

Discount = 0.2

Case Is >= 75

Discount = 0.25

End Select

MsgBox "Discount: " & Discount

End Sub

In this example, the Quantity variable is being evaluated. The procedure checks for

four different cases (0–24, 25–49, 50–74, and 75 or greater).

Any number of statements can follow each Case statement, and they all are executed if the case is true. If you use only one statement, as in this example,

you can put the statement on the same line as the Case keyword, preceded by a

colon — the VBA statement separator character. This tends to make your code more compact and a bit clearer. Here's how the procedure looks in this format:

Sub ShowDiscount4 ()

Dim Quantity As Long

Dim Discount As Double

Quantity = InputBox("Enter Quantity: ")

Select Case Quantity

Case 0 To 24: Discount = 0.1

Case 25 To 49: Discount = 0.15

Case 50 To 74: Discount = 0.2

Case Is >= 75: Discount = 0.25

End Select

MsgBox "Discount: " & Discount

End Sub

When VBA executes a Select Case structure, the structure is exited as soon as VBA

finds a true case and executes the statements for that case.

A nested Select Case example

As demonstrated in the following example, you can nest Select Case structures.

This procedure examines the active cell and displays a message describing the cell's contents. Notice that the procedure has three Select Case structures, and each has its own End Select statement:

Sub CheckCell()

Dim Msg As String

Select Case IsEmpty(ActiveCell)

CHAPTER 10  Controlling Program Flow and Making Decisions    153

Case True

Msg = "is blank."

Case Else

Select Case ActiveCell.HasFormula

Case True

Msg = "has a formula"

Case Else

Select Case IsNumeric(ActiveCell)

Case True

Msg = "has a number"

Case Else

Msg = "has text"

End Select

End Select

End Select

MsgBox "Cell " & ActiveCell.Address & " " & Msg

End Sub

The logic goes something like this:

1. Find out whether the cell is empty.

2. If it's not empty, see whether it contains a formula.

3. If there's no formula, find out whether it contains a numeric value or text.

When the procedure ends, the Msg variable contains a string that describes the

cell's contents. As shown in Figure 10-1, the MsgBox function displays that message.

You can nest Select Case structures as deeply as you need to, but make sure that

each Select Case statement has a corresponding End Select statement.

FIGURE 10-1:

A message

displayed by the

CheckCell

procedure.

154    PART 3  Programming Concepts

If you're still not convinced that indenting code is worth the effort, the previous listing serves as a good example. The indentations really make the nesting levels

clear. Take a look at the same procedure without any indentation:

Sub CheckCell()

Dim Msg As String

Select Case IsEmpty(ActiveCell)

Case True

Msg = "is blank."

Case Else

Select Case ActiveCell.HasFormula

Case True

Msg = "has a formula"

Case Else

Select Case IsNumeric(ActiveCell)

Case True

Msg = "has a number"

Case Else

Msg = "has text"

End Select

End Select

End Select

MsgBox "Cell " & ActiveCell.Address & " " & Msg

End Sub

Fairly incomprehensible, eh?

Knocking Your Code for a Loop

The term  looping refers to repeating a block of VBA statements numerous times.

Why use loops? Your code can . . .

» Loop through a range of cells, working with each cell individually.

» Loop through all open workbooks (the Workbooks collection) and do some-

thing with each one.

» Loop through all worksheets in a workbook (the Worksheets collection) and

do something with each one.

» Loop through all the elements in an array.

CHAPTER 10  Controlling Program Flow and Making Decisions    155

» Loop through all characters in a cell.

» Loop through all charts on a worksheet (the ChartObjects collection) and do something with each chart.

VBA supports several types of loops, and the examples that follow demonstrate a

few ways that you can use them.

For-Next loops

The examples in this section are all available at this book's website.

The simplest type of loop is a For-Next loop. The looping is controlled by a counter variable, which starts at one value and stops at another value. The statements between the For statement and the Next statement are the statements that get

repeated in the loop. To see how this works, keep reading.

A For-Next example

The following example uses a For-Next loop to sum the first 1,000 positive numbers. The Total variable starts out as zero. Then the looping occurs. The variable Cnt is the loop counter. It starts out as 1 and is incremented by 1 each time

through the loop. The loop ends when Cnt is 1,000.

This example has only one statement inside the loop. This statement adds the value of Cnt to the Total variable. When the loop finishes, a MsgBox displays the

sum of the numbers.

Sub AddNumbers()

Dim Total As Double

Dim Cnt As Long

Total = 0

For Cnt = 1 To 1000

Total = Total + Cnt

Next Cnt

MsgBox Total

End Sub

Because the loop counter is a normal variable, you can write code to change its

value within the block of code between the For and the Next statements. This, however, is a  very bad practice. Changing the counter within the loop can have unpredictable results. Take special precautions to ensure that your code doesn't

change the value of the loop counter.

156    PART 3  Programming Concepts

For-Next examples with a Step

You can use a Step value to skip some counter values in a For-Next loop. Here's the

previous example, rewritten to sum only the odd numbers between 1 and 1,000:

Sub AddOddNumbers()

Dim Total As Double

Dim Cnt As Long

Total = 0

For Cnt = 1 To 1000 Step 2

Total = Total + Cnt

Next Cnt

MsgBox Total

End Sub

This time, Cnt starts out as 1 and then takes on values of 3, 5, 7, and so on. The

Step value determines how the counter is incremented. Notice that the upper loop

value (1000) is not actually used because the highest value of Cnt will be 999.

Here's another example that uses a Step value of 3. This procedure works with the

active sheet and applies light gray shading to every third row, from row 1 to row 100.

Sub ShadeEveryThirdRow()

Dim i As Long

For i = 1 To 100 Step 3

Rows(i).Interior.Color = RGB(200, 200, 200)

Next i

End Sub

Figure 10-2 shows the result of running this macro.

FIGURE 10-2:

Using a loop to

apply background

shading to rows.

CHAPTER 10  Controlling Program Flow and Making Decisions    157

A For-Next example with an Exit For statement

A For-Next loop can also include one or more Exit For statements within the loop.

When VBA encounters this statement, the loop terminates immediately.

The following example, available on the book's website, demonstrates the Exit For

statement. This procedure is a Function procedure, intended to be used in a work-

sheet formula. The function accepts one argument (a variable named Str) and returns the characters to the left of the first numeric digit. For example, if the

argument is「KBR98Z,」the function returns「KBR.」

Function TextPart(Str)

Dim i As Long

TextPart = ""

For i = 1 To Len(Str)

If IsNumeric(Mid(Str, i, 1)) Then

Exit For

Else

TextPart = TextPart & Mid(Str, i, 1)

End If

Next i

End Function

The For-Next loop starts with 1 and ends with the number that represents the

number of characters in the string. The code uses VBA's Mid function to extract a

single character within the loop. If a numeric character is found, the Exit For statement is executed, and the loop ends prematurely. If the character is not numeric, it's appended to the returned value (which is the same as the function's

name). The only time the loop will examine every character is if the string passed

as the argument contains no numeric characters.

Now, you might shout,「Hey, but you said something about always using a single

point of exit!」Well, you're right, and obviously, you're getting the hang of this

structured programming business. But in some cases, ignoring that rule is a wise

decision. In this example, it greatly speeds up your code because there's no reason

to continue the loop after the first numeric digit is found.

A nested For-Next example

So far, all this chapter's examples use relatively simple loops. However, you can

have any number of statements in the loop and nest For-Next loops inside other

For-Next loops.

The following example uses a nested For-Next loop to insert random numbers

into a 12-row-by-5-column range of cells, as shown in Figure 10-3. Notice that

the procedure executes the  inner loop (the loop with the Row counter) once for 158    PART 3  Programming Concepts

each iteration of the  outer loop (the loop with the Col counter). In other words, the procedure executes the Cells(Row, Col) = Rnd statement 60 times.

Sub FillRange()

Dim Col As Long

Dim Row As Long

For Col = 1 To 5

For Row = 1 To 12

Cells(Row, Col) = Rnd

Next Row

Next Col

End Sub

FIGURE 10-3:

These cells were

filled using a

nested For-Next

loop.

The next example uses nested For-Next loops to initialize a three-dimensional

array with the value 100. This procedure executes the statement in the middle of

all the loops (the assignment statement) 1,000 times (10 * 10 * 10), each time with

a different combination of values for i, j, and k:

Sub NestedLoops()

Dim MyArray(10, 10, 10)

Dim i As Long

Dim j As Long

Dim k As Long

For i = 1 To 10

For j = 1 To 10

For k = 1 To 10

MyArray(i, j, k) = 100

Next k

Next j

Next i

' Other statements go here

End Sub

CHAPTER 10  Controlling Program Flow and Making Decisions    159

Refer to Chapter 7 for information about arrays.

Here's a final example that uses nested For-Next loops, with a Step value. This

procedure creates a checkerboard (or chessboard, if you prefer) by changing the

background color of alternating cells (see Figure 10-4).

FIGURE 10-4:

Using loops to

create a

checkerboard

pattern.

The Row counter loops from 1 to 8. An If-Then construct determines which nested

For-Next structure to use. For odd-numbered rows, the Col counter begins with 2.

For even-numbered rows, the Col counter begins with 1. Both loops use a Step

value of 2, so alternate cells are affected. Two additional statements make the cells square (just like a real checkerboard).

Sub MakeCheckerboard()

Dim R As Long, C As Long

For R = 1 To 8

If WorksheetFunction.IsOdd(R) Then

For C = 2 To 8 Step 2

Cells(R, C).Interior.Color = 255

Next C

Else

For C = 1 To 8 Step 2

Cells(R, C).Interior.Color = 255

Next C

End If

Next R

Rows("1:8").RowHeight = 35

Columns("A:H").ColumnWidth = 6.5

End Sub

160    PART 3  Programming Concepts

Do-While loop

VBA supports another type of looping structure known as a Do-While loop. Unlike

a For-Next loop, a Do-While loop continues until a specified condition is met.

The following example uses a Do-While loop. This procedure uses the active cell

as a starting point and then travels down the column, multiplying each cell's value by 2. The loop continues until the procedure encounters an empty cell.

Sub DoWhileDemo()

Do While ActiveCell.Value <> Empty

ActiveCell.Value = ActiveCell.Value * 2

ActiveCell.Offset(1, 0).Select

Loop

End Sub

Do-Until loop

The Do-Until loop structure is similar to the Do-While structure. The two struc-

tures differ in their handling of the tested condition. A program continues to exe-

cute a Do-While loop  while the condition remains true. In a Do-Until loop, the program executes the loop  until the condition is true.

The following example is the same one presented for the Do-While loop but recoded to use a Do-Until loop:

Sub DoUntilDemo()

Do Until IsEmpty(ActiveCell.Value)

ActiveCell.Value = ActiveCell.Value * 2

ActiveCell.Offset(1, 0).Select

Loop

End Sub

Using For Each-Next Loops

with Collections

VBA supports yet another type of looping: looping through each object in a collec-

tion of objects. A collection, as you may know, consists of a number of objects of

the same type. For example, Excel has a collection of all open workbooks (the Workbooks collection), and each workbook has a collection of worksheets (the Worksheets collection).

CHAPTER 10  Controlling Program Flow and Making Decisions    161

The examples in this section are all available at this book's website.

When you need to loop through each object in a collection, use the For Each-Next

structure. The following example loops through each worksheet in the active workbook and deletes the worksheet if it's empty:

Sub DeleteEmptySheets()

Dim WkSht As Worksheet

Application.DisplayAlerts = False

For Each WkSht In ActiveWorkbook.Worksheets

If WorksheetFunction.CountA(WkSht.Cells) = 0 Then

WkSht.Delete

End If

Next WkSht

Application.DisplayAlerts = True

End Sub

In this example, the variable WkSht is an object variable that represents each worksheet in the workbook. Nothing is special about the variable name WkSht;

you can use any variable name that you like.

The code loops through each worksheet and determines an empty sheet by count-

ing the nonblank cells. If that count is zero, the sheet is empty, and it's deleted.

Notice that the DisplayAlerts setting is turned off while the loop is doing its thing.

Without that statement, Excel displays a warning every time a sheet is about to be

deleted.

If all the worksheets in the workbook are empty, you get an error when Excel attempts to delete the only sheet. Normally, you would write code to handle that

situation.

Here's another For Each-Next example. This procedure uses a loop to hide all worksheets in the active workbook except the active sheet.

Sub HideSheets()

Dim Sht As Worksheet

For Each Sht In ActiveWorkbook.Worksheets

If Sht.Name <> ActiveSheet.Name Then

Sht.Visible = xlSheetHidden

End If

Next Sht

End Sub

162    PART 3  Programming Concepts

The HideSheets procedure checks the sheet name. If it's not the same as the active sheet's name, the sheet is hidden. Notice that the Visible property isn't Boolean.

This property can actually take on any of  three values, and Excel provides three built-in constants. If you're curious about the third possibility (xlVeryHidden),

check the Help system.

What gets hidden must eventually get unhidden, so here's a macro that unhides

all worksheets in the active workbook:

Sub UnhideSheets()

Dim Sht As Worksheet

For Each Sht In ActiveWorkbook.Worksheets

Sht.Visible = xlSheetVisible

Next Sht

End Sub

Not surprisingly, you can create nested For Each-Next loops. The CountBold pro-

cedure loops through every cell in the used range on each worksheet in every open

workbook and displays a count of the number of cells that are formatted as bold:

Sub CountBold()

Dim WBook As Workbook

Dim WSheet As Worksheet

Dim Cell As Range

Dim Cnt As Long

For Each WBook In Workbooks

For Each WSheet In WBook.Worksheets

For Each Cell In WSheet.UsedRange

If Cell.Font.Bold = True Then Cnt = Cnt + 1

Next Cell

Next WSheet

Next WBook

MsgBox Cnt & " bold cells found"

End Sub

CHAPTER 10  Controlling Program Flow and Making Decisions    163

IN THIS CHAPTER

» Knowing the event types that can

trigger an execution

» Finding out where to place your

event-handler VBA code

» Executing a macro when a workbook

is opened or closed

» Executing a macro when a workbook

or worksheet is activated

Chapter 11

Automatic Procedures

and Events

Y ou have a number of ways to execute a VBA Sub procedure. One way is to


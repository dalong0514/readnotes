T o err is human. To anticipate errors is divine. When working with VBA, you

should be aware of two broad classes of errors: programming errors and

runtime errors .  This chapter is all about runtime errors.

A well-written program handles errors the way Fred Astaire danced: gracefully.

Fortunately, VBA includes several tools to help you identify errors — and then

handle them gracefully.

Types of Errors

If you’ve tried any of the examples in this book, you have probably encountered

one or more error messages. Some of these errors result from bad VBA code. For

example, you may spell a keyword incorrectly or type a statement with the wrong

syntax. If you make such an error, you won’t even be able to execute the procedure

until you correct it.

CHAPTER 12  Error-Handling Techniques    187

This chapter doesn’t deal with those types of errors. Instead, it focuses on runtime errors — the errors that occur while Excel executes your VBA code. More specifically, this chapter covers the following fascinating topics:

» Identifying errors

» Doing something about the errors that occur

» Recovering from errors

» Creating intentional errors (Yes, sometimes an error can be a good thing.)

The ultimate goal of error handling is to write code that avoids displaying Excel’s

error messages as much as possible. In other words, you want to anticipate poten-

tial errors and deal with them before Excel has a chance to rear its ugly head with

a (usually) less-than-informative error message.

An Erroneous Example

To get things started, take a look at the following macro. A macro this simple

couldn’t produce any errors, right?

Activate the VBE, insert a module, and enter the following code:

Sub EnterSquareRoot()

Dim Num As Double

'  Prompt for a value

Num = InputBox("Enter a value")

'  Insert the square root

ActiveCell.Value = Sqr(Num)

End Sub

As shown in Figure 12-1, this procedure asks the user for a value. It then performs

a magical calculation and enters the square root of that value into the active cell.

FIGURE 12-1:

The InputBox

function displays

a dialog box

that asks the

user for a value.

188    PART 3  Programming Concepts

You can execute this procedure directly from the VBE by pressing F5. Alternatively, you may want to add a button to a worksheet (choose Developer ➪

Controls ➪ Insert and select the button in the Form Controls group to do this) and

then assign the macro to the button. (Excel prompts you for the macro to assign.)

Then you can run the procedure by simply clicking the button.

The macro’s not quite perfect

Execute the code a couple of times to try it out. It works pretty well, doesn’t it?

Now try entering a negative number when you’re prompted for a value. Oops.

Trying to calculate the square root of a negative number is illegal on this planet.

Excel responds to the request to calculate the square root of a negative number by

displaying the runtime error message shown in Figure 12-2. For now, just click

the End button. If you click the Debug button, Excel suspends the macro so that

you can use the debugging tools to help track down the error. (Debugging tools are

covered in Chapter 13.)

FIGURE 12-2:

Excel displays

this error

message when

the procedure

attempts to

calculate the

square root

of a negative

number.

Most folks don’t find the Excel error messages (for example,  Invalid procedure call  or argument) particularly helpful. To improve the procedure, you need to anticipate this error and handle it more gracefully. In other words, you need to add some

error-handling code.

Here’s a modified version of EnterSquareRoot:

Sub EnterSquareRoot2()

Dim Num As Double

'  Prompt for a value

Num = InputBox("Enter a value")

CHAPTER 12  Error-Handling Techniques    189

'  Make sure the number is nonnegative

If Num < 0 Then

MsgBox "You must enter a positive number."

Exit Sub

End If

'  Insert the square root

ActiveCell.Value = Sqr(Num)

End Sub

An If-Then structure checks the value contained in the Num variable. If Num is

less than 0, the procedure displays a message box containing information that

humans can actually understand. Then the procedure ends with the Exit Sub statement, so the runtime error never has a chance to occur.

The macro is still not perfect

So the modified EnterSquareRoot procedure is perfect, right? Not really. Try entering text rather than a value. Or click the Cancel button in the input box. Both of these actions generate an error  (Type mismatch).  This simple little procedure needs still more error-handling code.

The following modified code uses the IsNumeric function to make sure that Num

contains a numeric value. If the user doesn’t enter a number, the procedure

displays a message and then stops. Also, notice that the Num variable is now

declared as a Variant. If it were declared as a Double, the code would generate an

unhandled error if the user entered a nonnumeric value into the input box.

Sub EnterSquareRoot3()

Dim Num As Variant

'  Prompt for a value

Num = InputBox("Enter a value")

'  Make sure Num is a number

If Not IsNumeric(Num) Then

MsgBox "You must enter a number."

Exit Sub

End If

'  Make sure the number is nonnegative

If Num < 0 Then

MsgBox "You must enter a positive number."

Exit Sub

End If

190    PART 3  Programming Concepts

'  Insert the square root

ActiveCell.Value = Sqr(Num)

End Sub

Is the macro perfect yet?

Now this code is absolutely perfect, right? Not quite. Try running the procedure

while the active sheet is a chart sheet. Yikes — another runtime error, this time

the dreaded Number 91 (see Figure 12-3). This error occurs because there is no

active cell when a chart sheet is active or when something other than a range is

selected.

FIGURE 12-3:

Running the

procedure

when a chart

is selected

generates

this error.

The following procedure uses the TypeName function to make sure that the selec-

tion is a range. If anything other than a range is selected, this procedure displays a message and then exits:

Sub EnterSquareRoot4()

Dim Num As Variant

'  Make sure a worksheet is active

If TypeName(Selection) <> "Range" Then

MsgBox "Select a cell for the result."

Exit Sub

End If

'  Prompt for a value

Num = InputBox("Enter a value")

'  Make sure Num is a number

If Not IsNumeric(Num) Then

MsgBox "You must enter a number."

Exit Sub

End If

CHAPTER 12  Error-Handling Techniques    191

'  Make sure the number is nonnegative

If Num < 0 Then

MsgBox "You must enter a positive number."

Exit Sub

End If

'  Insert the square root

ActiveCell.Value = Sqr(Num)

End Sub

Giving up on perfection

By now, this procedure simply  must be perfect. Think again, pal.

Protect the worksheet (choose Review ➪ Changes ➪ Protect Sheet) and then run the

code. Yep, attempting to write to a protected worksheet generates yet another

error. And there are probably another half-dozen errors that are impossible to

predict. Keep reading for another way to deal with errors — even those you can’t

anticipate.

Handling Errors Another Way

How can you identify and handle every possible error? Often, you can’t. Fortu-

nately, VBA provides another way to deal with errors.

Revisiting the EnterSquareRoot procedure

The following code is a modified version of the procedure from the previous section. Here, an all-purpose On Error statement traps all errors and then checks

to see whether the InputBox was canceled.

Sub EnterSquareRoot5()

Dim Num As Variant

Dim Msg As String

'  Set up error handling

On Error GoTo BadEntry

'  Prompt for a value

Num = InputBox("Enter a value")

192    PART 3  Programming Concepts

'  Exit if cancelled

If Num = "" Then Exit Sub

'  Insert the square root

ActiveCell.Value = Sqr(Num)

Exit Sub

BadEntry:

Msg = "An error occurred." & vbNewLine & vbNewLine

Msg = Msg & "Make sure a range is selected, "

Msg = Msg & "the sheet is not protected, "

Msg = Msg & "and you enter a nonnegative value."

MsgBox Msg, vbCritical

End Sub

This routine traps  any type of runtime error. After trapping a runtime error, the revised EnterSquareRoot procedure displays the message box shown in Figure 12-4.

This message box describes the most likely causes of the error.

FIGURE 12-4:

A runtime error in

the procedure

generates this

semihelpful error

message.

ON ERROR NOT WORKING?

If an On Error statement isn’t working as advertised, you need to change one of your settings:

1. Activate the VBE.

2. Choose Tools  ➪ Options.

3. Click the General tab of the Options dialog box.

4. Make sure that the Break on All Errors setting is deselected.

If this setting is selected, Excel essentially ignores any On Error statements. You

normally want to keep the Error Trapping options set to Break on Unhandled Errors.

CHAPTER 12  Error-Handling Techniques    193

About the On Error statement

Using an On Error statement in your VBA code allows you to bypass Excel’s built-in

error handling and use your own error-handling code. In the previous example, a

runtime error causes macro execution to jump to the statement labeled BadEntry.

As a result, you avoid Excel’s unfriendly error messages, and you can display your

own message to the user.

Notice that the example uses an Exit Sub statement right before the BadEntry label. This statement is necessary because you don’t want to execute the error-handling code if an error does  not occur.

Handling Errors: The Details

You can use the On Error statement in three ways, as shown in Table 12-1.

TABLE 12-1

Using the On Error Statement

Syntax

What It Does

On Error GoTo  label

After executing this statement, VBA resumes execution at the statement following

the specified label. You must include a colon after the label so that VBA recognizes it as a label.

On Error GoTo 0

After executing this statement, VBA resumes its normal error-checking behavior.

Use this statement after using one of the other On Error statements or when

you want to remove error handling in your procedure.

On Error Resume Next

After executing this statement, VBA simply ignores all errors and resumes

execution with the next statement.

Resuming after an error

In some cases, you simply want the routine to end gracefully when an error occurs.

For example, you may display a message describing the error and then exit the

procedure. (The EnterSquareRoot5 example shown earlier uses this technique.) In

other cases, you want to recover from the error, if possible.

To recover from an error, you must use a Resume statement. This clears the error

condition and allows you to continue execution at some location. You can use the

Resume statement in three ways, as shown in Table 12-2.

194    PART 3  Programming Concepts

TABLE 12-2

Using the Resume Statement

Syntax

What It Does

Resume

Execution resumes with the statement that caused the error. Use this if your error-handling code corrects the problem and it’s okay to continue.

Resume Next

Execution resumes with the statement immediately following the statement that caused the error. This essentially ignores the error.

Resume  label

Execution resumes at the  label you specify.

The following example uses a Resume statement after an error occurs:

Sub EnterSquareRoot6()

Dim Num As Variant

Dim Msg As String

Dim Ans As Integer

TryAgain:

'  Set up error handling

On Error GoTo BadEntry

'  Prompt for a value

Num = InputBox("Enter a value")

If Num = "" Then Exit Sub

'  Insert the square root

ActiveCell.Value = Sqr(Num)

Exit Sub

BadEntry:

Msg = Err.Number & ": " & Error(Err.Number)

Msg = Msg & vbNewLine & vbNewLine

Msg = Msg & "Make sure a range is selected, "

Msg = Msg & "the sheet is not protected, "

Msg = Msg & "and you enter a nonnegative value."

Msg = Msg & vbNewLine & vbNewLine & "Try again?"

Ans = MsgBox(Msg, vbYesNo + vbCritical)

If Ans = vbYes Then Resume TryAgain

End Sub

This procedure has another label: TryAgain. If an error occurs, execution contin-

ues at the BadEntry label, and the code displays the message shown in Figure 12-5.

If the user responds by clicking Yes, the Resume statement kicks in, and execution

jumps back to the TryAgain label. If the user clicks No, the procedure ends.

CHAPTER 12  Error-Handling Techniques    195

FIGURE 12-5:

If an error occurs,

the user can

decide whether

to try again.

Notice that the error message also includes the error number, along with the

「official」error description.

The Resume statement clears the error condition before continuing. To under-

stand what this means, try substituting the following statement for the second-

to-last statement in the preceding example:

If Ans = vbYes Then GoTo TryAgain

The code doesn’t work correctly if you use GoTo rather than Resume. To demon-

strate, enter a negative number. You get the error prompt. Click Yes to try again

and then enter  another negative number. This second error is not trapped because the original error condition was not cleared.

This example is available on this book’s website.

Error handling in a nutshell

To help you keep all this error-handling business straight, here’s a quick-and-

dirty summary. A block of error-handling code has the following characteristics:

» It begins immediately after the label specified in the On Error statement.

» It should be reached by your macro only if an error occurs. This means that you must use a statement such as Exit Sub or Exit Function immediately

before the label.

» It may require a Resume statement. If you choose not to abort the procedure when an error occurs, you must execute a Resume statement before returning to the main code.

196    PART 3  Programming Concepts

Knowing when to ignore errors

In some cases, it’s perfectly okay to ignore errors. That’s when the On Error Resume Next statement comes into play.

The following example loops through each cell in the selected range and converts

the value to its square root. This procedure generates an error message if any cell

in the selection contains a negative number or text:

Sub SelectionSqrt()

Dim cell As Range

If TypeName(Selection) <> "Range" Then Exit Sub

For Each cell In Selection

cell.Value = Sqr(cell.Value)

Next cell

End Sub

In this case, you may want to simply skip any cell that contains a value you can’t

convert to a square root. You can create all sorts of error-checking capabilities by using If-Then structures, but you can devise a better (and simpler) solution by

simply ignoring the errors that occur.

The following routine accomplishes this by using the On Error Resume Next statement:

Sub SelectionSqrt()

Dim cell As Range

If TypeName(Selection) <> "Range" Then Exit Sub

On Error Resume Next

For Each cell In Selection

cell.Value = Sqr(cell.Value)

Next cell

End Sub

In general, you can use an On Error Resume Next statement if you consider the

errors to be harmless or inconsequential to your task.

Identifying specific errors

All errors are not created equal. Some are serious, and some are less serious.

Although you may ignore errors you consider to be inconsequential, you must deal

with other, more serious errors. In some cases, you need to identify the specific

error that occurs.

CHAPTER 12  Error-Handling Techniques    197

Every type of error has an official number. When an error occurs, Excel stores the error number in an Error object named Err. This object’s Number property contains the error number, and its Description property contains a description of the

error. For example, the following statement displays the error number, a colon,

and a description of the error:

MsgBox Err.Number & ": " & Err.Description

Figure 12-5, earlier in this chapter, shows an example. Keep in mind, however,

that the Excel error messages are not always very useful — but you already know

that.

The following procedure demonstrates how to determine which error occurred. In

this case, you can safely ignore errors caused by trying to get the square root of a nonpositive number (that is, error 5) or errors caused by trying to get the square

root of a nonnumeric value (error 13). On the other hand, you need to inform the

user if the worksheet is protected and the selection contains one or more locked

cells. (Otherwise, the user may think the macro worked when it really didn’t.)

Attempting to write to a locked cell in a protected worksheet causes error 1004.

Sub SelectionSqrt()

Dim cell As Range

Dim ErrMsg As String

If TypeName(Selection) <> "Range" Then Exit Sub

On Error GoTo ErrorHandler

For Each cell In Selection

cell.Value = Sqr(cell.Value)

Next cell

Exit Sub

ErrorHandler:

Select Case Err.Number

Case 5 'Negative number

Resume Next

Case 13 'Type mismatch

Resume Next

Case 1004 'Locked cell, protected sheet

MsgBox "Cell is locked. Try again.", vbCritical, cell.Address

Exit Sub

Case Else

ErrMsg = Error(Err.Number)

MsgBox "ERROR: " & ErrMsg, vbCritical, cell.Address

Exit Sub

End Select

End Sub

198    PART 3  Programming Concepts

When a runtime error occurs, execution jumps to the code beginning at the ErrorHandler label. The Select Case structure (discussed in Chapter 10) tests for

three common error numbers. If the error number is 5 or 13, execution resumes at

the next statement. (In other words, the error is ignored.) But if the error number

is 1004, the routine advises the user and then ends. The last case, a catch-all for

unanticipated errors, traps all other errors and displays the actual error message.

An Intentional Error

Sometimes, you can use an error to your advantage. Suppose that you have a

macro that works only if a particular workbook is open. How can you determine

whether that workbook is open? One way is to write code that loops through the

Workbooks collection, checking to determine whether the workbook you’re inter-

ested in is in that collection.

Here’s an easier way: using a general-purpose function that accepts one argu-

ment (a workbook name) and returns True if the workbook is open or False if

it’s not.

Here’s the function:

Function WorkbookIsOpen(book As String) As Boolean

Dim WBName As String

On Error GoTo NotOpen

WBName = Workbooks(book).Name

WorkbookIsOpen = True

Exit Function

NotOpen:

WorkbookIsOpen = False

End Function

This function takes advantage of the fact that Excel generates an error if you refer to a workbook that isn’t open. For example, the following statement generates an

error if a workbook named MyBook.xlsx isn’t open:

WBName = Workbooks("MyBook.xlsx").Name

In the WorkbookIsOpen function, the On Error statement tells VBA to continue the

macro at the NotOpen statement if an error occurs. Therefore, an error means that

the workbook isn’t open, and the function returns False. If the workbook  is open, no error occurs, and the function returns True.

CHAPTER 12  Error-Handling Techniques    199

Here’s another variation on the WorkbookIsOpen function. This version uses On Error Resume Next to ignore the error. But the code checks Err’s Number property. If Err.Number is 0, no error occurred, and the workbook is open. If Err.Number is anything else, it means that an error occurred (and the workbook

isn’t open).

Function WorkbookIsOpen(book) As Boolean

Dim WBName As String

On Error Resume Next

WBName = Workbooks(book).Name

If Err.Number = 0 Then WorkbookIsOpen = True _

Else WorkbookIsOpen = False

End Function

The following example demonstrates how to use this function in a Sub

procedure:

Sub UpdatePrices()

If Not WorkbookIsOpen("Prices.xlsx") Then

MsgBox "Please open the Prices workbook first!"

Exit Sub

End If

'  [Other code goes here]

End Sub

The UpdatePrices procedure (which must be in the same workbook as

WorkbookIsOpen) calls the WorkbookIsOpen function and passes the workbook

name (Prices.xlsx) as an argument. The WorkbookIsOpen function returns either

True or False. Therefore, if the workbook is not open, the procedure informs the

user of that fact. If the workbook is open, the macro continues.

Error handling can be a tricky proposition. After all, many errors can occur, and

you can’t anticipate all of them. In general, you should trap errors and correct the situation before Excel intervenes, if possible. Writing effective error-trapping code requires a thorough knowledge of Excel and a clear understanding of how

VBA error handling works. Subsequent chapters contain more examples of error

handling.

200    PART 3  Programming Concepts

IN THIS CHAPTER

» Defining a bug and knowing why you

should squash it

» Recognizing types of program bugs

you may encounter

» Using techniques for debugging

your code

» Using the VBE’s built-in debugging

tools

» Presenting a handy list of bug

reduction tips

Chapter 13

Bug Extermination

Techniques

I f the word  bugs conjures up an image of a cartoon rabbit, this chapter can set you straight. Simply put, a bug is an error in your programming. Here, you take

a look at the topic of programming bugs — how to identify them and how to

wipe them off the face of your module.

Species of Bugs

Welcome to Entomology 101. The term  program bug,  as you probably know, refers to a problem with software. In other words, if software doesn’t perform as

expected, it has a bug. Fact is, all major software programs have bugs — lots of

bugs. Excel itself has hundreds (if not thousands) of bugs. Fortunately, the vast

majority of these bugs are relatively obscure and appear in only very specific circumstances.

CHAPTER 13  Bug Extermination Techniques    201

When you write nontrivial VBA programs, your code probably will have bugs. This is a fact of life and not necessarily a reflection of your programming ability.

The bugs may fall into any of the following categories:

» Logic flaws in your code: You can often avoid these bugs by carefully

thinking through the problem your program addresses.

» Incorrect context bugs: This type of bug surfaces when you attempt to do

something at the wrong time. For example, your code may try to write data to

cells in the active sheet when the active sheet is actually a chart sheet (which

has no cells).

» Extreme-case bugs: These bugs rear their ugly heads when you encounter

data you didn’t anticipate, such as very large or very small numbers.

» Wrong data-type bugs: This type of bug occurs when you try to process data

of the wrong type, such as attempting to take the square root of a text string.

» Wrong version bugs: This type of bug involves incompatibilities between

different Excel versions. For example, you may develop a workbook with Excel

2019 and then find out that the workbook doesn’t work with Excel 2003. You

can usually avoid such problems by not using version-specific features. Often,

the easiest approach is to develop your application by using the lowest

version number of Excel that users might have. In all cases, however, you

should test your work on all versions you expect it will be used with.

» Beyond-your-control bugs: These are the most frustrating. An example

occurs when Microsoft upgrades Excel and makes a minor, undocumented

change that causes your macro to bomb. Even security updates have been

known to cause problems.

Debugging is the process of identifying and correcting bugs in your program.

Developing debugging skills takes time, so don’t be discouraged if this process is

difficult at first.

It’s important to understand the distinction between  bugs and  syntax errors.  A syntax error is a language error. For example, you might misspell a keyword, omit the

Next statement in a For-Next loop, or have a mismatched parenthesis. Before you

can even execute the procedure, you must correct these syntax errors. A program

bug is much subtler. You can execute the routine, but it doesn’t perform as expected.

Identifying Bugs

Before you can do any debugging, you must determine whether a bug actually

exists. You can tell that your macro contains a bug if it doesn’t work the way

202    PART 3  Programming Concepts

it should. (Gee, this book is just filled with insight, isn’t it?) Usually, but not always, you can easily discern this.

A bug often (but not always) becomes apparent when Excel displays a runtime

error message. Figure 13-1 shows an example. Notice that this error message includes a button labeled Debug. More about this later in the「About the Debugger」

section.

FIGURE 13-1:

An error message

like this often

means that your

VBA code

contains a bug.

A key fact known to all programmers is that bugs often appear when you least

expect them. For example, just because your macro works fine with one data set

doesn’t mean you can assume it works equally as well with all data sets.

The best debugging approach is to start with thorough testing, under a variety of

real-life conditions. And because any workbook changes made by your VBA code

can’t be undone, it’s always a good idea to use a backup copy of the workbook that

you use for testing.

Debugging Techniques

In this section, you explore the four most common methods for debugging Excel

VBA code:

» Examining the code

» Inserting MsgBox functions at various locations in your code

» Inserting Debug.Print statements

» Using the Excel built-in debugging tools

CHAPTER 13  Bug Extermination Techniques    203

Examining your code

Perhaps the most straightforward debugging technique is simply taking a close

look at your code to see whether you can find the problem. This method, of course,

requires knowledge and experience. In other words, you have to know what you’re

doing. If you’re lucky, the error jumps right out, and you slap your forehead and

say,「D’oh!」But often times, you discover errors when you have been working on

your program for eight hours straight, it’s 2 a.m., and you’re running on caffeine

and willpower. At times like that, you’re lucky if you can even see your code, let

alone find the bugs. Thus, don’t be surprised if simply examining your code isn’t

enough to make you find and expunge all the bugs it contains.

Using the MsgBox function

A common problem in many programs involves one or more variables not taking

on the values you expect. In such cases, monitoring the variable(s) while your

code runs is a helpful debugging technique. One way to do this is by inserting

temporary MsgBox functions into your routine. For example, if you have a variable

named CellCount, you can insert the following statement:

MsgBox CellCount

When you execute the routine, the MsgBox function displays CellCount’s value.

It’s often helpful to display the values of two or more variables in the message

box. The following statement displays the current value of two variables:

LoopIndex (1) and CellCount (72), separated by a space.

MsgBox LoopIndex & " " & CellCount

Notice that the two variables are combined with the concatenation operator (&)

and a space character inserted between them. Otherwise, the message box strings

the two values together, making them look like a single value. You can also use the

built-in constant, vbNewLine, in place of the space character. vbNewLine inserts

a line-feed break, which displays the text on a new line. The following statement

displays three variables, each on a separate line (see Figure 13-2):

MsgBox LoopIndex & vbNewLine & CellCount & vbNewLine & MyVal

This technique isn’t limited to monitoring variables. You can use a message box to

display all sorts of useful information while your code is running. For example, if

your code loops through a series of sheets, the following statement displays the

name and type of the active sheet:

MsgBox ActiveSheet.Name & " " & TypeName(ActiveSheet)

204    PART 3  Programming Concepts

FIGURE 13-2:

Using a message

box to display

the value of

three variables.

If your message box shows something unexpected, press Ctrl+Break, and you see

a dialog box that tells you Code execution has been interrupted; as shown in

Figure 13-3, you have four choices:

» Click the Continue button. The code continues executing.

» Click the End button. Execution stops.

» Click the Debug button. The VBE goes into Debug mode (explained a bit later in the section「About the Debugger」).

» Click the Help button. A help screen tells you that you pressed Ctrl+Break. In other words, it’s not very helpful.

FIGURE 13-3:

Pressing

Ctrl+Break halts

execution of your

code and gives

you some

choices.

If your keyboard doesn’t have a Break key, try pressing Ctrl+ScrollLock.

Feel free to use MsgBox functions frequently when you debug your code. Just

make sure that you remove them after you identify and correct the problem.

CHAPTER 13  Bug Extermination Techniques    205

Inserting Debug.Print statements

As an alternative to using MsgBox functions in your code, you can insert one or

more temporary Debug.Print statements. Use these statements to print the value

of one or more variables in the Immediate window. Here’s an example that dis-

plays the values of three variables:

Debug.Print LoopIndex, CellCount, MyVal

Notice that the variables are separated with commas. You can display as many

variables as you like with a single Debug.Print statement.

Debug.Print sends output to the Immediate window even if that window is hidden.

If VBE’s Immediate window is not visible, press Ctrl+G (or choose View ➪ Immediate

Window). Figure 13-4 shows some output in the Immediate window.

FIGURE 13-4:

A Debug.Print

statement sends

output to the

Immediate

window.

Unlike MsgBox, Debug.Print statements don’t halt your code. So you need to keep

an eye on the Immediate window to see what’s going on.

After you’ve debugged your code, be sure to remove or comment out all the Debug.

Print statements. Even big companies like Microsoft occasionally forget to remove

their Debug.Print statements. In several previous versions of Excel, every time the

Analysis ToolPak add-in was opened, you’d see several strange messages in

the Immediate window. That problem was finally fixed in Excel 2007.

Using the VBA debugger

The Excel designers are intimately familiar with the concept of bugs. Conse-

quently, Excel includes a set of debugging tools that can help you correct problems

in your VBA code. The VBA debugger is the topic of the next section.

206    PART 3  Programming Concepts

About the Debugger

This section discusses the gory details of using the Excel debugging tools. These

tools are much more powerful than the techniques discussed in the previous

section. But along with power comes responsibility. Using the debugging tools takes a bit of setup work.

Setting breakpoints in your code

You can use MsgBox functions in your code to monitor the values of certain vari-

ables. (See the earlier section,「Using the MsgBox function.」) Displaying a mes-

sage box essentially halts your code in mid-execution, and clicking the OK button

resumes execution.

Wouldn’t it be nice if you could halt a routine’s execution, take a look at the value of  any of your variables, and then continue execution? Well, that’s exactly what you can do by setting a breakpoint. You can set a breakpoint in your VBA code in

several ways:

» Move the cursor to the statement at which you want execution to stop;

then press F9.

» Click the gray margin to the left of the statement at which you want execution to stop.

» Position the insertion point in the statement at which you want execution to stop. Then choose Debug ➪  Toggle Breakpoint.

» Right-click a statement and choose Toggle ➪  Breakpoint from the shortcut

menu.

The results of setting a breakpoint are shown in Figure 13-5. Excel highlights the

line to remind you that you set a breakpoint there; it also inserts a large dot in the margin.

When you execute the procedure, Excel goes into  Break mode before the line with the breakpoint is executed. In Break mode, the word [break] is displayed in the

VBE’s title bar. To get out of Break mode and continue execution, press F5 or click

the Run Sub/UserForm button on the VBE’s toolbar. See「Stepping through your

code」later in this chapter to find out more.

To quickly remove a breakpoint, click the large dot in the gray margin or move

the cursor to the highlighted line and press F9. To remove all breakpoints in the

module, press Ctrl+Shift+F9.

CHAPTER 13  Bug Extermination Techniques    207

FIGURE 13-5:

The highlighted

statement marks

a breakpoint in

this procedure.

VBA also has a keyword, which you can insert as a statement, that forces Break

mode:

Stop

When your code reaches the Stop keyword, VBA enters Break mode.

What is Break mode? You can think of it as a state of suspended animation. Your

VBA code stops running, and the current statement is highlighted in bright yellow.

In Break mode, you can

» Type VBA statements in the Immediate window. (See the next section

for details.)

» Press F8 to step through your code one line at a time to check various things while the program is paused.

» Move the mouse pointer over a variable to display its value in a small pop-up window.

» Skip the next statement(s) and continue execution there (or even go back a

couple of statements).

» Edit a statement and then continue.

Figure 13-6 shows some debugging action. A breakpoint is set (notice the big dot),

and the F8 key is used to step through the code line by line (notice the arrow that

points to the current statement).

208    PART 3  Programming Concepts

FIGURE 13-6:

A typical scene in

Break mode.

Using the Immediate window

The Immediate window may not be visible in the VBE. You can display the VBE’s

Immediate window at any time by pressing Ctrl+G.

In Break mode, the Immediate window is particularly useful for finding the cur-

rent value of any variable in your program. For example, if you want to know the

current value of a variable named CellCount, enter the following in the Immediate

window and press Enter:

Print CellCount

You can save a few milliseconds by using a question mark in place of the word

Print, like this:

? CellCount

The Immediate window allows you to do other things besides check variable val-

ues. For example, you can change the value of a variable, activate a different sheet, or even open a new workbook. Just make sure that the command you enter is a

valid VBA statement.

You can also use the Immediate window when Excel is not in Break mode. The

Immediate window makes for a handy place to add small code snippets before

incorporating them into your procedures.

Stepping through your code

While in Break mode, you can also step through your code line by line. One state-

ment is executed each time you press F8. Throughout this line-by-line execution

of your code, you can activate the Immediate window at any time to check the

status of your variables.

CHAPTER 13  Bug Extermination Techniques    209

You can use your mouse to change which statement VBA executes next. If you put

your mouse pointer in the margin to the left of the currently highlighted state-

ment (which is usually yellow), your pointer changes to a right-pointing arrow.

Simply drag your mouse to the statement you want to execute next and watch that

statement turn yellow.

Using the Watches window

In some cases, you may want to know whether a certain variable or expression

takes on a particular value. Suppose that a procedure loops through 1,000 cells.

You notice that a problem occurs during the 900th iteration of the loop. Well, you

could insert a breakpoint into the loop, but that would mean responding to 899

prompts before the code finally gets to the iteration you want to see (and that gets boring real fast). A more efficient solution involves setting a  watch expression.

For example, you can create a watch expression that puts the procedure into Break

mode whenever a certain variable takes on a specific value — for example, Counter=900. To create a watch expression, choose Debug ➪  Add Watch to display

the Add Watch dialog box (see Figure 13-7).

FIGURE 13-7:

The Add Watch

dialog box lets

you specify a

condition that

causes a break.

The Add Watch dialog box has three parts:

» Expression: Enter a valid VBA expression or a variable here — for example,

Counter=900 or just Counter.

» Context: Select the procedure and the module you want to watch. Note that

you can select All Procedures and All Modules.

210    PART 3  Programming Concepts

» Watch Type: Select the type of watch by clicking an option button. Your

choice here depends on the expression you enter. The first choice, Watch

Expression, doesn’t cause a break; it simply displays the expression’s value

when a break occurs.

Execute your procedure after setting up your watch expression(s). Things run

normally until your watch expression is satisfied (based on the Watch Type you

specified). When that happens, Excel enters Break mode (you did set the Watch

Type to Break When Value Is True, didn’t you?). From there, you can step through

the code or use the Immediate window to debug your code.

When you create a watch, the VBE displays the Watches window, shown in

Figure 13-8. This window displays the value of all watches that you’ve defined. In

this figure, the value of the Counter variable hit 900, which caused Excel to enter

Break mode.

FIGURE 13-8:

The Watches

window displays

all watches.

To remove a watch, right-click it in the Watches window, and choose Delete Watch

from the shortcut menu.

The best way to understand how this Watch business works is to use it and

try various options. Before long, you’ll probably wonder how you ever got along

without it.

Using the Locals window

Another useful debugging aid is the Locals window. You can show this window by

choosing View ➪  Locals Window in the VBE. When you are in Break mode, this window shows a list of all variables that are local to the current procedure (see

Figure 13-9). The nice thing about this window is that you don’t have to add a load

of watches manually if you want to look at the content of many variables. The VBE

has done all the hard work for you.

CHAPTER 13  Bug Extermination Techniques    211

FIGURE 13-9:

The Locals

window displays

all local variables

and their content.

Bug Reduction Tips

There is no sure-fire way to completely eliminate bugs in your VBA programs. But

here are a few tips to help you keep those bugs to a minimum:

» Use an Option Explicit statement at the beginning of your modules.  This

statement requires you to define the data type for every variable you use.

This creates a bit more work for you, but you avoid the common error of

misspelling a variable name. And it has a nice side benefit: Your routines run

a bit faster.

» Format your code with indentation.  Using indentations helps delineate

different code segments. If your program has several nested For-Next loops,

for example, consistent indentation helps you keep track of them all.

» Be careful with the On Error Resume Next statement.  This statement

causes Excel to ignore any errors and continue executing the routine. In some

cases, using this statement causes Excel to ignore errors that it shouldn’t

ignore. Your code may have bugs, and you may not even realize it.

» Use comments.  Nothing is more frustrating than revisiting code you wrote

six months ago and not having a clue as to how it works. By adding a few

comments to describe your logic, you can save lots of time down the road.

» Keep your Sub and Function procedures simple.  By writing your code in

small modules, each of which has a single, well-defined purpose, you simplify

the debugging process.

» Use the macro recorder to help identify properties and methods.  When

you can’t remember the name or the syntax of a property or method, simply

record a macro and look at the recorded code.

» Understand Excel’s debugger.  Although it can be a bit daunting at first, the Excel debugger is a useful tool. Invest some time and get to know it.

212    PART 3  Programming Concepts

IN THIS CHAPTER

» Working with ranges in your

VBA code

» Changing Boolean and non-Boolean

settings

» Manipulating charts with VBA

» Making your VBA code run as fast as

possible

Chapter 14

VBA Programming


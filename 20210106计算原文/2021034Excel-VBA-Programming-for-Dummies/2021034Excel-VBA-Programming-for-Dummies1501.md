Simple Dialog Boxes

Y ou can't use Excel very long without being exposed to dialog boxes. They

seem to pop up all the time. Excel — like most Windows programs — uses

dialog boxes to obtain information, clarify commands, and display

messages. If you develop VBA macros, you can create your own dialog boxes that

work just like those built into Excel. Those custom dialog boxes are called UserForms in VBA.

This chapter doesn't tell you anything about creating UserForms. Rather, it

describes some very useful techniques you might be able to use in  place of

UserForms. Chapters 16 through 18, however, do cover UserForms.

UserForm Alternatives

Some of the VBA macros you create behave the same every time you execute them.

For example, you may develop a macro that enters a list of your employees into a

worksheet range. This macro always produces the same result and requires no additional user input.

CHAPTER 15  Simple Dialog Boxes    239

You might develop other macros, however, that behave differently under various circumstances or that offer the user options. In such cases, the macro may benefit

from a custom dialog box. A custom dialog box provides a simple means for getting

information from the user. Your macro then uses that information to determine

what it should do.

UserForms can be quite useful, but creating them takes time. Before delving into

the topic of creating UserForms in the next chapter, you need to know about some

potentially timesaving alternatives.

VBA allows you to display several types of dialog boxes that you can sometimes

use in place of a handcrafted UserForm. You can customize these built-in dialog

boxes in some ways, but they certainly don't offer the options available in a UserForm. In some cases, however, they're just what the doctor ordered.

In this chapter, you read about

» The MsgBox function

» The InputBox function

» The GetOpenFilename method

» The GetSaveAsFilename method

» The FileDialog method

Also in this chapter, you discover how to use VBA to display some of the Excel

built-in dialog boxes — the dialog boxes that Excel uses to get information from you.

The MsgBox Function

By now, you're probably familiar with the VBA MsgBox function; several of the

examples in the preceding chapters make use of the MsgBox function. The MsgBox

function, whose main arguments are shown in Table 15-1, is handy for displaying

information and getting simple user input. It's able to accept user input because

it's a function. A function, as you probably know, returns a value. In the case of

the MsgBox function, it uses a dialog box to get the value that it returns. Keep

reading to see exactly how it works.

240    PART 4  Communicating with Your Users

TABLE 15-1

MsgBox Function Arguments

Argument

What It Affects

Prompt

The text Excel displays in the message box

Buttons

A number that specifies which buttons (along with what icon) appear in

the message box (optional)

Title

The text that appears in the message box's title bar (optional)

Here's a simplified version of the syntax of the MsgBox function:

MsgBox(prompt[, buttons][, title])

Displaying a simple message box

You can use the MsgBox function in two ways:

» To simply show a message to the user: In this case, you don't care about the result returned by the function.

» To get a response from the user: In this case, you do care about the result returned by the function. The result depends on the button that the user clicks.

If you use the MsgBox function by itself, don't include parentheses around the

arguments. The following example simply displays a message and doesn't return

a result. When the message is displayed, the code stops until the user clicks OK.

Sub MsgBoxDemo()

MsgBox "Click OK to begin printing."

Sheets("Results").PrintOut

End Sub

Figure 15-1 shows how this message box looks. In this case, printing commences

when the user clicks OK. Do you notice that there is no way to cancel the printing?

The next section describes how to fix that.

Getting a response from a message box

If you display a message box that has more than just an OK button, you'll probably

want to know which button the user clicks. You're in luck. The MsgBox function

returns a value that represents which button is clicked. You can assign the result

of the MsgBox function to a variable.

CHAPTER 15  Simple Dialog Boxes    241

FIGURE 15-1:

A simple

message box.

The following code uses some of the built-in constants (outlined in Table 15-2)

that make it easy to work with the values returned by MsgBox:

Sub GetAnswer()

Dim Ans As Long

Ans = MsgBox("Start printing?", vbYesNo)

Select Case Ans

Case vbYes

ActiveSheet.PrintOut

Case vbNo

MsgBox "Printing canceled"

End Select

End Sub

TABLE 15-2

Constants Used in the MsgBox Function

Constant

Value

What It Does

vbOKOnly

0

Displays OK button only.

vbOKCancel

1

Displays OK and Cancel buttons.

vbAbortRetryIgnore

2

Displays Abort, Retry, and Ignore buttons.

vbYesNoCancel

3

Displays Yes, No, and Cancel buttons.

vbYesNo

4

Displays Yes and No buttons.

vbRetryCancel

5

Displays Retry and Cancel buttons.

vbCritical

16

Displays Critical Message icon.

vbQuestion

32

Displays Warning Query icon.

vbExclamation

48

Displays Warning Message icon.

vbInformation

64

Displays Information Message icon.

242    PART 4  Communicating with Your Users

Constant

Value

What It Does

vbDefaultButton1

0

First button is default.

vbDefaultButton2

256

Second button is default.

vbDefaultButton3

512

Third button is default.

vbDefaultButton4

768

Fourth button is default.

Figure 15-2 shows how it looks. When you execute this procedure, the Ans variable

is assigned a value of either vbYes or vbNo, depending on which button the user

clicks. The Select Case statement uses the Ans value to determine which action the

code should perform.

FIGURE 15-2:

A simple message

box, with two

buttons.

You can also use the MsgBox function result without using a variable, as the

following example demonstrates:

Sub GetAnswer2()

If MsgBox("Start printing?", vbYesNo) = vbYes Then

'    ...[code if Yes is clicked]...

Else

'    ...[code if Yes is not clicked]...

End If

End Sub

Customizing message boxes

The flexibility of the buttons argument makes it easy to customize your message

boxes. You can choose which buttons to display, determine whether an icon

appears, and decide which button is the default (the default button is「clicked」if

the user presses Enter).

CHAPTER 15  Simple Dialog Boxes    243

To use more than one of these constants as an argument, just connect them with

a + operator. For example, to display a message box with Yes and No buttons and

an exclamation icon, use the following expression as the second MsgBox argument:

vbYesNo + vbExclamation

Or, if you prefer to make your code less understandable, use a value of 52 (that is, 4 + 48).

The following example uses a combination of constants to display a message box

with a Yes button and a No button (vbYesNo) as well as a question-mark icon (vbQuestion). The constant vbDefaultButton2 designates the second button (No)

as the default button — that is, the button that is clicked if the user presses Enter.

For simplicity, you can assign these constants to the Config variable and then use

Config as the second argument in the MsgBox function:

Sub GetAnswer3()

Dim Config As Long

Dim Ans As Integer

Config = vbYesNo + vbQuestion + vbDefaultButton2

Ans = MsgBox("Process the monthly report?", Config)

If Ans = vbYes Then RunReport

End Sub

Figure 15-3 shows the message box Excel displays when you execute the

GetAnswer3 procedure. If the user clicks the Yes button, the routine executes the

procedure named RunReport (which is not shown). If the user clicks the No button (or presses Enter), the routine ends with no action. Because the procedure

omits the title argument in the MsgBox function, Excel uses the default title,

Microsoft Excel.

FIGURE 15-3:

The MsgBox

function's buttons

argument

determines what

appears in the

message box.

244    PART 4  Communicating with Your Users

The following routine provides another example of using the MsgBox function:

Sub GetAnswer4()

Dim Msg As String, Title As String

Dim Config As Integer, Ans As Integer

Msg = "Do you want to process the monthly report?"

Msg = Msg & vbNewLine & vbNewLine

Msg = Msg & "Processing the monthly report will "

Msg = Msg & "take approximately 15 minutes. It "

Msg = Msg & "will generate a 30-page report for "

Msg = Msg & "all sales offices for the current "

Msg = Msg & "month."

Title = "XYZ Marketing Company"

Config = vbYesNo + vbQuestion

Ans = MsgBox(Msg, Config, Title)

If Ans = vbYes Then RunReport

End Sub

This example demonstrates an efficient way to specify a longer message in a message box. Here, the variable (Msg) and the concatenation operator (&) build

the message in a series of statements. The vbNewLine constant inserts a line-break

character that starts a new line (use it twice to insert a blank line). The Title argument displays a different title in the message box.

Figure 15-4 shows the message box Excel displays when you execute this

procedure.

FIGURE 15-4:

This dialog box,

displayed by the

MsgBox function,

displays a title, an

icon, and two

buttons.

Previous examples use constants (such as vbYes and vbNo) for the return value of

a MsgBox function. Table 15-3 lists a few other constants.

CHAPTER 15  Simple Dialog Boxes    245

TABLE 15-3

Constants Used as Return Values for the MsgBox Function

Constant

Value

What It Means

vbOK

1

User clicked OK.

vbCancel

2

User clicked Cancel.

vbAbort

3

User clicked Abort.

vbRetry

4

User clicked Retry.

vbIgnore

5

User clicked Ignore.

vbYes

6

User clicked Yes.

vbNo

7

User clicked No.

And that's pretty much all you need to know about the MsgBox function. Use message boxes with caution, though. There's usually no reason to display message

boxes that serve no purpose. For example, people tend to get annoyed when they

see a message box every day that reads Good morning. Thanks for loading the

Budget Projection workbook.

The InputBox Function

The VBA InputBox function is useful for obtaining a single piece of information

typed by the user. That information could be a value, a text string, or even a range address. This is a good alternative to developing a UserForm when you need to get

only one value.

InputBox syntax

Here's a simplified version of the syntax of the InputBox function:

InputBox(prompt[, title][, default])

Table 15-4 shows the key arguments for the InputBox function.

TABLE 15-4

InputBox Function Arguments

Argument

What It Affects

Prompt

The text displayed in the input box

Title

The text displayed in the input box's title bar (optional)

Default

The default value for the user's input (optional)

246    PART 4  Communicating with Your Users

An InputBox example

Here's a statement that shows how you can use the InputBox function:

TheName = InputBox("What is your name?", "Greetings")

When you execute this VBA statement, Excel displays the dialog box shown in Figure 15-5. Notice that this example uses only the first two arguments and doesn't supply a default value. When the user enters a value and clicks OK, the

code assigns the value to the variable TheName.

FIGURE 15-5:

The InputBox

function displays

this dialog box.

The following example uses the third argument and provides a default value. The

default value is the username stored by Excel (the Application object's UserName

property).

Sub GetName()

Dim TheName As String

TheName = InputBox("What is your name?", _

"Greetings", Application.UserName)

End Sub

The InputBox always displays a Cancel button. If the user clicks Cancel, the InputBox function returns an empty string.

VBA's InputBox function always returns a string, so if you need to get a value, your code needs to do some additional checking. The following example uses the InputBox function to get a number. It uses the IsNumeric function to check whether

the string is a number. If the string does contain a number, all is fine. If the user's entry cannot be interpreted as a number, the code displays a message box.

Sub AddSheets()

Dim Prompt As String

Dim Caption As String

Dim DefValue As Long

Dim NumSheets As String

CHAPTER 15  Simple Dialog Boxes    247

Prompt = "How many sheets do you want to add?"

Caption = "Tell me..."

DefValue = 1

NumSheets = InputBox(Prompt, Caption, DefValue)

If NumSheets = "" Then Exit Sub ';Canceled

If IsNumeric(NumSheets) Then

If NumSheets > 0 Then Sheets.Add Count:=NumSheets

Else

MsgBox "Invalid number"

End If

End Sub

Figure 15-6 shows the dialog box that this routine produces.

FIGURE 15-6:

Another example

of using the

InputBox

function.

Another type of InputBox

The information presented in this section applies to VBA's InputBox function.

Microsoft seems to love confusion, so you also have access to the InputBox  method , which is a method of the Application object.

One big advantage of using the Application InputBox method is that your code can

prompt for a range selection. The user can then select the range in the worksheet

by highlighting the cells. Here's a quick example that prompts the user to select a

range:

Sub GetRange()

Dim Rng As Range

On Error Resume Next

Set Rng = Application.InputBox _

(prompt:="Specify a range:", Type:=8)

If Rng Is Nothing Then Exit Sub

MsgBox "You selected range " & Rng.Address

End Sub

248    PART 4  Communicating with Your Users

Figure 15-7 shows how it looks.

FIGURE 15-7:

Using the

Application

InputBox method

to get a range.

In this simple example, the code tells the user the address of the range that was

selected. In real life, your code would actually do something useful with the

selected range. A nice thing about this example is that Excel takes care of the error handling. If you enter something that's not a range, Excel tells you about it and

lets you try again.

The Application.InputBox method is similar to VBA's InputBox function, but it

also has some differences. Check the Help system for complete details.

The GetOpenFilename Method

If your VBA procedure needs to ask the user for a filename, you  could use the InputBox function and have the user do some typing. An input box usually isn't

the best tool for this job, however, because most users find it difficult to remem-

ber paths, backslashes, filenames, and file extensions. In other words, it's far too easy to screw up when typing a filename.

For a better solution to this problem, use the GetOpenFilename method of the Application object, which ensures that your code gets its hands on a valid filename, including its complete path. The GetOpenFilename method displays the

familiar Open dialog box (a dead ringer for the dialog box Excel displays when you

choose File ➪ Open ➪ Browse).

CHAPTER 15  Simple Dialog Boxes    249

The GetOpenFilename method doesn't actually open the specified file. This method simply returns the user-selected filename as a string. Then you can write

code to do whatever you want with the filename.

The syntax for the GetOpenFilename

method

The official syntax of the GetOpenFilename method is as follows:

object.GetOpenFilename ([fileFilter], [filterIndex],

[title],[buttonText], [multiSelect])

GetOpenFilename method takes the optional arguments shown in Table 15-5.

TABLE 15-5

GetOpenFilename Method Arguments

Argument

What It Does

FileFilter

Determines the types of files that appear in the dialog box (for example,

*.TXT). You can specify several filters for the user to choose from.

FilterIndex

Determines which of the file filters the dialog box displays by default.

Title

Specifies the caption for the dialog box's title bar.

ButtonText

Ignored (used only for the Macintosh version of Excel).

MultiSelect

If True, the user can select multiple files.

A GetOpenFilename example

The FileFilter argument determines what appears in the dialog box's Files of Type

drop-down list. This argument consists of pairs of file filter strings followed by

the wildcard file filter specification, with commas separating each part and pair.

If omitted, this argument defaults to the following:

All Files (*.*), *.*

Notice that this string consists of two parts, separated by a comma:

All Files (*.*)

and

*.*

250    PART 4  Communicating with Your Users

The first part of this string is the text displayed in the Files of Type drop-down list. The second part determines which files the dialog box displays. For example,

*.* means  all files.

The code in the following example opens a dialog box that asks the user for a filename. The procedure defines five file filters. Notice that the VBA line-continuation sequencesets up the Filter variable; doing so helps simplify this

rather complicated argument.

Sub GetImportFileName()

Dim Finfo As String

Dim FilterIndex As Long

Dim Title As String

Dim FileName As Variant

'  Set up list of file filters

FInfo = "Text Files (*.txt),*.txt," & _

"Lotus Files (*.prn),*.prn," & _

"Comma Separated Files (*.csv),*.csv," & _

"ASCII Files (*.asc),*.asc," & _

"All Files (*.*),*.*"

'  Display *.* by default

FilterIndex = 5

'  Set the dialog box caption

Title = "Select a File to Import"

'  Get the filename

FileName = Application.GetOpenFilename (FInfo, _

FilterIndex, Title)

'  Handle return info from dialog box

If FileName = False Then

MsgBox "No file was selected."

Else

MsgBox "You selected " & FileName

End If

End Sub

Figure 15-8 shows the dialog box Excel displays when you execute this procedure.

The appearance may vary, depending on the version of Windows you use and the

display options you've set.

CHAPTER 15  Simple Dialog Boxes    251

FIGURE 15-8:

The GetOpen

Filename method

displays a

customizable

dialog box and

returns the

selected file's

path and name.

It does not

open the file.

In a real application, you would do something more meaningful with the filename.

For example, you might want to open it by using a statement such as this:

Workbooks.Open FileName

Notice that the FileName variable is declared as a Variant data type. If the user

clicks Cancel, that variable contains a Boolean value (False). Otherwise, FileName

is a string. Therefore, using a Variant data type handles both possibilities.

The GetSaveAsFilename Method

The Excel GetSaveAsFilename method works just like the GetOpenFilename

method, but it displays the Excel Save As dialog box rather than its Open dialog

box. The GetSaveAsFilename method gets a path and filename from the user but

doesn't do anything with that information. It's up to you to write code that actu-

ally saves the file.

The syntax of this method follows:

object.GetSaveAsFilename ([InitialFilename], [FileFilter],

[FilterIndex],[Title], [ButtonText])

252    PART 4  Communicating with Your Users

The GetSaveAsFilename method takes Table 15-6's arguments, all of which are optional.

TABLE 15-6

GetSaveAsFilename Method Arguments

Argument

What It Does

InitialFileName

Specifies a default filename that appears in the File Name box.

FileFilter

Determines the types of files Excel displays in the dialog box

(for example, *.TXT). You can specify several filters for the user

to choose among.

FilterIndex

Determines which of the file filters Excel displays by default.

Title

Defines a caption for the dialog box's title bar.

Getting a Folder Name

Sometimes, you don't need to get a filename; you just need to get a folder name.

If that's the case, the FileDialog object is just what the doctor ordered.

The following procedure displays a dialog box that allows the user to select a

directory. The selected directory name (or「Canceled」) is displayed by the MsgBox

function.

Sub GetAFolder()

With Application.FileDialog(msoFileDialogFolderPicker)

.InitialFileName = Application.DefaultFilePath & "\"

.Title = "Please select a location for the backup"

.Show

If .SelectedItems.Count = 0 Then

MsgBox "Canceled"

Else

MsgBox .SelectedItems(1)

End If

End With

End Sub

The FileDialog object lets you specify the starting directory by specifying a value

for the InitialFileName property. In this case, the code uses Excel's default file

path as the starting directory.

CHAPTER 15  Simple Dialog Boxes    253

Displaying Excel's Built-in Dialog Boxes

One way to look at VBA is that it's a tool that lets you mimic Excel commands. For

example, consider this VBA statement:

Range("A1:A12").Name = "MonthNames"

Executing this VBA statement has the same effect as choosing Formulas ➪ Defined

Names ➪ Define Name to display the New Name dialog box, typing MonthNames

in the Name box and A1:A12 in the Refers to box, and clicking OK.

When you execute the VBA statement, the New Name dialog box doesn't appear.

This is almost always what you want to happen; you don't want dialog boxes

flashing across the screen while your macro executes.

In some cases, however, you may want your code to display one of Excel's many

built-in dialog boxes and let the user make the choices in the dialog box. You can

do this by using VBA to execute a Ribbon command. Here's an example that

displays the New Name dialog box. The address in the Refers To box represents

the range that's selected when the command is executed (see Figure 15-9).

Application.CommandBars.ExecuteMso "NameDefine"

FIGURE 15-9:

Displaying one of

Excel's dialog

boxes by

using VBA.

Your VBA code can't get any information from the dialog box. For example, if you

execute the code to display the New Name dialog box, your code can't get the

name entered by the user or the range that's being named.

The ExecuteMso is a method of the CommandBars object and accepts one

argument: an idMso parameter that represents a Ribbon control. Unfortunately,

these parameters aren't listed in the Help system. And because the Ribbon hasn't

254    PART 4  Communicating with Your Users

been around forever, code that uses the ExecuteMso method is not compatible

with versions before Excel 2007.

Here's another example of using the ExecuteMso method. This statement, when

executed, displays the Font tab of the Format Cells dialog box:

Application.CommandBars.ExecuteMso "FormatCellsFontDialog"

If you try to display a built-in dialog box in an incorrect context, Excel displays an error message. For example, here's a statement that displays the Format Number

dialog box:

Application.CommandBars.ExecuteMso "NumberFormatsDialog"

If you execute this statement when it's not appropriate (for example, a Shape is

selected), Excel displays an error message because that dialog box is appropriate

only for worksheet cells.

Excel has thousands of commands. How can you find the name of the one you

need? One way is to use the Customize Ribbon tab of the Excel Options dialog box.

The quick way to get there is to right-click any Ribbon control and choose Customize the Ribbon from the shortcut menu. Virtually every command available

in Excel is listed in the left panel. Find the command you need and hover your

mouse over it, and you see its secret command name in the tooltip (it's the part in

parentheses). Figure 15-10 shows an example.

FIGURE 15-10:

Using the

Customize

Ribbon tab to

identify a

command name.

CHAPTER 15  Simple Dialog Boxes    255

IN THIS CHAPTER

» Finding out when to use UserForms

» Understanding UserForm objects

» Displaying a UserForm

» Creating a UserForm that works with

a useful macro

Chapter 16


arrange for the Sub to be executed automatically. In this chapter, you

explore the ins and outs of this potentially useful feature, explaining how

to set things up so that a macro is executed automatically when a particular event

occurs. (No, this chapter is not about capital punishment.)

Preparing for the Big Event

An  event is basically something that happens Excel. Following are a few examples of the types of events that Excel can recognize:

» A workbook is opened or closed.

» A window is activated or deactivated.

» A worksheet is activated or deactivated.

» Data is entered into a cell or the cell is edited.

CHAPTER 11  Automatic Procedures and Events    165

» A workbook is saved.

» An object, such as a button, is clicked.

» A particular key or key combination is pressed.

» A particular time of day occurs.

» An error occurs.

Dozens of different types of events are associated with all kinds of Excel objects,

such as workbooks, worksheets, pivotTables, and even charts. To simplify things,

you can use two other more common types of events: workbook events and work-

sheet events.

Table 11-1 lists some useful workbook-related events. If, for some reason, you need to see the complete list of workbook-related events, check out the Help system.

TABLE 11-1

Workbook Events

Event

When It's Triggered

Activate

The workbook is activated.

BeforeClose

The command to close the workbook is given.

BeforePrint

The command to print is given.

BeforeSave

The command to save the workbook is given.

Deactivate

The workbook is deactivated.

NewSheet

A new sheet is added to the workbook.

Open

The workbook is opened.

SheetActivate

A sheet in the workbook is activated.

SheetBeforeDoubleClick

A cell in the workbook is double-clicked.

SheetBeforeRightClick

A cell in the workbook is right-clicked.

SheetChange

A change is made to a cell in the workbook.

SheetDeactivate

A sheet in the workbook is deactivated.

SheetSelectionChange

The selection is changed.

WindowActivate

The workbook window is activated.

WindowDeactivate

The workbook window is deactivated.

166    PART 3  Programming Concepts

Table 11-2 lists some useful worksheet-related events.

TABLE 11-2

Worksheet Events

Event

When It's Triggered

Activate

The worksheet is activated.

BeforeDoubleClick

A cell in the worksheet is double-clicked.

BeforeRightClick

A cell in the worksheet is right-clicked.

Change

A change is made to a cell in the worksheet.

Deactivate

The worksheet is deactivated.

SelectionChange

The selection is changed.

Are events useful?

At this point, you may be wondering how these events can be useful. Here's a quick example.

Suppose you have a workbook in which you enter values in column A. Your boss, a

very compulsive person, tells you that he needs to know exactly when each num-

ber was entered. Entering data is an event: a WorksheetChange event. You can write a macro that responds to this event. That macro kicks in whenever the worksheet is changed. If the change was made in column A, the macro puts the

date and time in column B, next to the data point that was entered.

In case you're curious, here's what such a macro would look like. Probably a lot

simpler than you thought it would be, eh?

Private Sub Worksheet_Change(ByVal Target As Range)

If Target.Column = 1 Then

Target.Offset(0, 1) = Now

End If

End Sub

By the way, macros that respond to events are very picky about where they are

stored. For example, this Worksheet_Change macro  must be in the Code module

for that worksheet. Put it somewhere else, and it won't work. More about this later

(see「Where Does the VBA Code Go?」).

CHAPTER 11  Automatic Procedures and Events    167

Just because your workbook contains procedures that respond to events doesn't guarantee that those procedures will actually run. As you know, it's possible to

open a workbook with macros disabled. In such a case, all macros (even proce-

dures that respond to events) are turned off. Keep this fact in mind when you create workbooks that rely on event-handler procedures.

Programming event-handler procedures

A VBA procedure that executes in response to an event is called an  event-handler  procedure . These are always Sub procedures (as opposed to Function procedures).

Writing these event-handlers is relatively straightforward after you understand

how the process works.

Creating event-handler procedures boils down to a few steps:

1. Identify the event you want to trigger the procedure.

2. Press Alt+F11 to activate the Visual Basic Editor.

3. In the VBE Project window, double-click the appropriate object listed

under Microsoft Excel Objects.

For workbook-related events, the object is ThisWorkbook. For a worksheet-

related event, the object is a Worksheet object (such as Sheet1).

4. In the Code window for the object, write the event-handler procedure

that is executed when the event occurs.

This procedure will have a special name that identifies it as an event-handler

procedure.

These steps become clearer as you progress through the chapter.

Where Does the VBA Code Go?

It's very important to understand where your event-handler procedures go. They

must reside in the Code window of an Object module. They do not go in a standard

VBA module. If you put your event-handler procedure in the wrong place, it simply

won't work. And you won't see any error messages, either.

Figure 11-1 shows the VBE window with one project displayed in the Project window. (Refer to Chapter 3 for some background on the VBE.) Notice that the VBA

project for Book1 is fully expanded and consists of several objects:

168    PART 3  Programming Concepts

» One object for each worksheet in the workbook (in this case, three

Sheet objects)

» An object labeled ThisWorkbook

» A VBA module inserted manually (Choose Insert ➪ Module.)

FIGURE 11-1:

The Project

window displays

items for a single

project.

Double-clicking any of these objects displays the code associated with the item,

if any.

The event-handler procedures that you write go into the Code window for the ThisWorkbook item (for workbook-related events) or one of the Sheet objects (for

worksheet-related events).

In Figure 11-1, the Code window for the Sheet1 object is displayed, and it happens

to have a single event-handler procedure defined. Notice the two drop-down con-

trols at the top of the Code module? Keep reading to find out why those are useful.

Writing an Event-Handler Procedure

The VBE helps you out when you're ready to write an event-handler procedure; it

displays a list of all events for the selected object.

At the top of each Code window, you find two drop-down lists:

» The Object drop-down list (the one on the left)

» The Procedure drop-down list (the one on the right)

By default, the Object drop-down list in the Code window displays General.

If you're writing an event-handler for the ThisWorkbook object, you need to click

ThisWorkbook in the Project window and then choose Workbook from the Object

drop-down (it's the only other choice).

CHAPTER 11  Automatic Procedures and Events    169

If you're writing an event-handler for a Sheet object, you need to click the specific Sheet in the Project window and then choose Worksheet from the Object drop-down list (again, the only other choice).

After you've made your choice from the Object drop-down list, you can choose the

event from the Procedure drop-down list. Figure 11-2 shows some of the choices

for a workbook-related event.

FIGURE 11-2:

Choosing an

event in the Code

window for the

ThisWorkbook

object.

When you select an event from the list, the VBE automatically starts creating an

event-handler procedure for you. This is a very useful feature, because it tells you exactly what the proper arguments are.

Here's a little quirk. When you first select Workbook from the Object list, the VBE

always assumes that you want to create an event-handler procedure for the Open

event and creates it for you. If you're actually creating a Workbook_Open proce-

dure, that's fine. But if you're creating a different event-procedure, you need to

delete the empty Workbook_Open Sub that was created.

The VBE's help goes only so far, however. It writes the Sub statement and the End Sub statement. Writing the VBA code that goes between these two statements is your job.

You don't really have to use those two drop-down lists, but doing so makes your

job easier because the name of the event-handler procedure is critically impor-

tant. If you don't get the name exactly right, the procedure won't work. Also, some event-handler procedures use one or more arguments in the Sub statement.

There's no way you can remember what those arguments are. For example, if you

select SheetActivate from the event list for a Workbook object, the VBE writes the

following Sub statement:

Private Sub Workbook_SheetActivate(ByVal Sh As Object)

In this case, Sh is the argument passed to the procedure and is a variable that

represents the sheet in the activated workbook. Examples in this chapter clarify

this point.

170    PART 3  Programming Concepts

Introductory Examples

In this section, you find a few examples so that you can get the hang of this event-

handling business.

The Open event for a workbook

One of the most commonly used events is the Workbook Open event. Assume that

you have a workbook that you use every day. The Workbook_Open procedure in

this example is executed every time the workbook is opened. The procedure checks

the day of the week; if it's Friday, the code displays a reminder message for you.

To create the procedure that is executed whenever the Workbook Open event occurs, follow these steps:

1. Open the workbook.

Any workbook will do.

2. Press Alt+F11 to activate the VBE.

3. Locate the workbook in the Project window.

4. Double-click the project name to display its items, if necessary.

5. Double-click the ThisWorkbook item.

The VBE displays an empty Code window for the ThisWorkbook object.

6. In the Code window, select Workbook from the Object (left) drop-down

list.

The VBE enters the beginning and ending statements for a Workbook_Open

procedure.

7. Enter the following statements, so the complete event-procedure looks

like this:

Private Sub Workbook_Open()

Dim Msg As String

If Weekday(Now) = 6 Then

Msg = "Today is Friday. Don't forget to "

Msg = Msg & "submit the TPS Report!"

MsgBox Msg

End If

End Sub

The Code window should look like Figure 11-3.

CHAPTER 11  Automatic Procedures and Events    171

FIGURE 11-3:

This event-

handler

procedure is

executed when

the workbook

is opened.

Workbook_Open is executed automatically whenever the workbook is opened. It

uses the VBA's WeekDay function to determine the day of the week. If it's Friday

(day 6), a message box reminds the user to submit a report. If it's not Friday, nothing happens.

If today isn't Friday, you might have a hard time testing this procedure. You can

just change the 6 to correspond to today's actual day number.

And of course, you can modify this procedure any way you like. For example, the

following version displays a message every time the workbook is opened. This gets annoying after a while.

Private Sub Workbook_Open()

Msg = "This is Frank's cool workbook!"

MsgBox Msg

End Sub

A Workbook_Open procedure can do almost anything. These event-handlers are

often used for the following:

» Displaying welcome messages (such as in Frank's cool workbook)

» Opening other workbooks

» Activating a particular worksheet in the workbook

» Setting up custom shortcut menus

Here's a final example of a Workbook_Open procedure that uses the GetSetting

and SaveSetting functions to keep track of how many times the workbook has been opened. The SaveSetting function writes a value to the Windows registry, and

the GetSetting function retrieves that value (see the Help system for details).

The following example retrieves the count from the registry, increments it, and

then saves it back to the registry. It also tells the user the value of Cnt that corresponds to the number of times the workbook has been opened (see Figure 11-4).

172    PART 3  Programming Concepts

Private Sub Workbook_Open()

Dim Cnt As Long

Cnt = GetSetting("MyApp", "Settings", "Open", 0)

Cnt = Cnt + 1

SaveSetting "MyApp", "Settings", "Open", Cnt

MsgBox "This workbook has been opened " & Cnt & " times."

End Sub

FIGURE 11-4:

Using a

Workbook_Open

event-handler to

keep track of how

many times a

workbook has

been opened.

The BeforeClose event for a workbook

Here's an example of the Workbook_BeforeClose event-handler procedure, which

is executed automatically immediately before the workbook is closed. This proce-

dure is located in the Code window for a ThisWorkbook object:

Private Sub Workbook_BeforeClose(Cancel As Boolean)

Dim Msg As String

Dim Ans As Long

Dim FName As String

Msg = "Would you like to make a backup of this file?"

Ans = MsgBox(Msg, vbYesNo)

If Ans = vbYes Then

FName = "F:\BACKUP\" & ThisWorkbook.Name

ThisWorkbook.SaveCopyAs FName

End If

End Sub

This routine uses a message box to ask the user whether he would like to make a

backup copy of the workbook. If the answer is yes, the code uses the SaveCopyAs

method to save a backup copy of the file on drive F. If you adapt this procedure for your own use, you need to change the drive and path.

CHAPTER 11  Automatic Procedures and Events    173

Excel programmers often use a Workbook_BeforeClose procedure to clean up after themselves. For example, if you use a Workbook_Open procedure to change

some settings when you open a workbook (hiding the status bar, for example), it's

only appropriate that you return the settings to their original state when you close the workbook. You can perform this electronic housekeeping with a Workbook_

BeforeClose procedure.

When using the Workbook_BeforeClose event, keep this in mind: If you close Excel and any open file has been changed since the last save, Excel shows its usual

「Do you want to save your changes」 message box. Clicking the Cancel button cancels the entire closing process. But the Workbook_BeforeClose event will have

been executed anyway.

The BeforeSave event for a workbook

The BeforeSave event, as its name implies, is triggered before a workbook is saved.

This event occurs when you choose File ➪ Save or File ➪ Save As.

The following procedure, which is placed in the Code window for a ThisWorkbook

object, demonstrates the BeforeSave event. The routine updates the value in a cell

(cell A1 on Sheet1) every time the workbook is saved. In other words, cell A1 serves as a counter to keep track of the number of times the file was saved.

Private Sub Workbook_BeforeSave(ByVal SaveAsUI _

As Boolean, Cancel As Boolean)

Dim Counter As Range

Set Counter = Sheets("Sheet1").Range("A1")

Counter.Value = Counter.Value + 1

End Sub

Notice that the Workbook_BeforeSave procedure has two arguments: SaveAsUI

and Cancel. To demonstrate how these arguments work, examine the following

macro, which is executed before the workbook is saved. This procedure attempts

to prevent the user from saving the workbook with a different name. If the user

chooses File ➪ Save As, the SaveAsUI argument is True.

When the code executes, it checks the SaveAsUI value. If this variable is True, the

procedure displays a message and sets Cancel to True, which cancels the Save operation.

174    PART 3  Programming Concepts

Private Sub Workbook_BeforeSave(ByVal SaveAsUI _

As Boolean, Cancel As Boolean)

If SaveAsUI Then

MsgBox "You cannot save a copy of this workbook!"

Cancel = True

End If

End Sub

Note that this procedure won't really prevent anyone from saving a copy with a

different name. If someone really wants to do it, he or she can just open the work-

book with macros disabled. When macros are disabled, event-handler procedures

are also disabled, which makes sense because they are, after all, macros.

Examples of Activation Events

Another category of events consists of activating and deactivating objects —

specifically, sheets and workbooks.

Activate and deactivate events in a sheet

Excel can detect when a particular sheet is activated or deactivated and execute a

macro when either of these events occurs. These event-handler procedures go in

the Code window for the Sheet object.

You can quickly access a sheet's Code window by right-clicking the sheet's tab

and selecting View Code.

The following example shows a simple procedure that is executed whenever a particular sheet is activated. This code simply pops up an annoying message box

that displays the name of the active sheet:

Private Sub Worksheet_Activate()

MsgBox "You just activated " & ActiveSheet.Name

End Sub

Here's another example that activates cell A1 whenever the sheet is activated:

Private Sub Worksheet_Activate()

Range("A1").Activate

End Sub

CHAPTER 11  Automatic Procedures and Events    175

Although the code in these two procedures is about as simple as it gets, event-handler procedures can be as complex as you like.

The following procedure (which is stored in the Code window for the Sheet1 object)

uses the Deactivate event to prevent a user from activating any other sheet in the

workbook. If Sheet1 is deactivated (that is, another sheet is activated), the user

gets a message and Sheet1 is activated.

Private Sub Worksheet_Deactivate()

MsgBox "You must stay on Sheet1"

Sheets("Sheet1").Activate

End Sub

By the way, it's not a great idea to use VBA procedures, such as this one, to attempt to take over Excel. These so-called「dictator」applications can be very frustrating and confusing for the user. And of course, they can be defeated easily by disabling macros.

Activate and deactivate events

in a workbook

The previous examples use events associated with a specific worksheet. The ThisWorkbook object also handles events that deal with sheet activation and deactivation. The following procedure, which is stored in the Code window for the

ThisWorkbook object, is executed when  any sheet in the workbook is activated.

The code displays a message with the name of the activated sheet.

Private Sub Workbook_SheetActivate(ByVal Sh As Object)

MsgBox Sh.Name

End Sub

The Workbook_SheetActivate procedure uses the Sh argument. Sh is a variable

that represents the active Sheet object. The message box displays the Sheet object's Name property.

The next example is contained in a ThisWorkbook Code window. It consists of two

event-handler procedures:

» Workbook_SheetDeactivate: Executed when any sheet in the workbook is

deactivated. It stores the sheet that is deactivated in an object variable — but

only if the sheet is a worksheet. The Set keyword creates an object variable,

which is available to all procedures in the module.

176    PART 3  Programming Concepts

» Workbook_SheetActivate: Executed when any sheet in the workbook

is activated. It checks the type of sheet that is activated (using the

TypeName function). If the sheet is a chart sheet, the user gets a message

(see Figure 11-5). When the OK button in the message box is clicked, the

previous worksheet (which is stored in the OldSheet variable) is reactivated.

FIGURE 11-5:

When a chart

sheet is activated,

the user sees a

message like this.

A workbook that contains this code is available at this book's website.

Dim OldSheet As Object

Private Sub Workbook_SheetDeactivate(ByVal Sh As Object)

If TypeName(Sh) = "Worksheet" Then Set OldSheet = Sh

End Sub

Private Sub Workbook_SheetActivate(ByVal Sh As Object)

Dim Msg As String

If TypeName(Sh) = "Chart" Then

Msg = "This chart contains "

Msg = Msg & ActiveChart.SeriesCollection(1).Points.Count

Msg = Msg & " data points." & vbNewLine

Msg = Msg & "Click OK to return to " & OldSheet.Name

MsgBox Msg

OldSheet.Activate

End If

End Sub

CHAPTER 11  Automatic Procedures and Events    177

Workbook activation events

Excel also recognizes the event that occurs when you activate or deactivate a

particular workbook. The following code, which is contained in the Code window

for the ThisWorkbook object, is executed whenever the workbook is activated. The

procedure simply maximizes the workbook's window.

Private Sub Workbook_Activate()

ActiveWindow.WindowState = xlMaximized

End Sub

An example of Workbook_Deactivate code appears next. This procedure is executed

when a workbook is deactivated. This procedure copies the selected range whenever

the workbook is deactivated. It might be useful if you're copying data from lots of

areas and pasting them into a different workbook. When this event-procedure is

in place, you can select the range to be copied, activate the other workbook, select the destination, and press Ctrl+V (or Enter) to paste the copied data.

Private Sub Workbook_Deactivate()

ThisWorkbook.Windows(1).RangeSelection.Copy

End Sub

Other Worksheet-Related Events

The preceding section illustrated examples for worksheet activation and deactiva-

tion events. In this section, you find additional events that occur in worksheets:

double-clicking a cell, right-clicking a cell, and changing a cell.

The BeforeDoubleClick event

You can set up a VBA procedure to be executed when the user double-clicks a cell.

In the following example (which is stored in the Code window for a Sheet object),

double-clicking a cell in that sheet makes the cell bold (if it's not bold) or not bold (if it is bold):

Private Sub Worksheet_BeforeDoubleClick _

(ByVal Target As Excel.Range, Cancel As Boolean)

Target.Font.Bold = Not Target.Font.Bold

Cancel = True

End Sub

178    PART 3  Programming Concepts

The Worksheet_BeforeDoubleClick procedure has two arguments: Target and Cancel. Target represents the cell (a Range object) that was double-clicked. If Cancel is set to True, the default double-click action doesn't occur.

The default action for double-clicking a cell is to put Excel in cell edit mode. In

this case, you don't necessarily want to edit the cell when double-clicking the cells, so set Cancel to True.

The BeforeRightClick event

The BeforeRightClick event is similar to the BeforeDoubleClick event except that it

consists of right-clicking a cell. The following procedure checks to see whether

the cell that was right-clicked contains a numeric value. If so, the code displays

the Format Number dialog box and sets the Cancel argument to True (avoiding the

normal shortcut menu display). If the cell doesn't contain a numeric value, noth-

ing special happens; the shortcut menu is displayed as usual.

Private Sub Worksheet_BeforeRightClick _

(ByVal Target As Excel.Range, Cancel As Boolean)

If IsNumeric(Target) And Not IsEmpty(Target) Then

Application.CommandBars.ExecuteMso ("NumberFormatsDialog")

Cancel = True

End If

End Sub

Notice that the code, which is available on this book's website, makes an addi-

tional check to see if the cell isn't empty. This is because VBA considers empty

cells to be numeric.

The Change event

The Change event occurs whenever any cell in the worksheet is changed. In the

following example, the Worksheet_Change procedure effectively prevents a user

from entering a nonnumeric value in cell A1. This code is stored in the Code window for a Sheet object.

Private Sub Worksheet_Change(ByVal Target As Range)

If Target.Address = "$A$1" Then

If Not IsNumeric(Target) Then

MsgBox "Enter a number in cell A1."

CHAPTER 11  Automatic Procedures and Events    179

Range("A1").ClearContents

Range("A1").Activate

End If

End If

End Sub

The single argument for the Worksheet_Change procedure (Target) represents

the range that was changed. The first statement checks whether the cell's address

is $A$1. If so, the code uses the IsNumeric function to determine whether the cell

contains a numeric value. If not, a message appears, and the cell's value is erased.

Cell A1 is then activated — useful if the cell pointer moved to a different cell after the entry was made. If the change occurs in any cell except A1, nothing happens.

Why not use data validation?

You may be familiar with Data ➪ Data Tools ➪ Data Validation. This handy feature

makes it easy to ensure that only data of the proper type is entered into a particular cell or range. Although Data ➪ Data Tools ➪ Data Validation is useful, it's definitely not foolproof.

Try adding data validation to a cell. For example, you can set it up so the cell accepts only a numerical value. It works fine — until you copy another cell and

paste it to the data validation cell. Pasting removes the data validation. It's as if it was never there. The severity of this flaw depends on your application.

Pasting wipes out data validation because Excel considers validation to be a format

for a cell. Therefore, it's in the same classification as font size, color, or other similar attributes. When you paste a cell, you're replacing the formats in the target cell with those of the source cell. Unfortunately, those formats also include your

validation rules.

Preventing data validation from being destroyed

The procedure in this section demonstrates how to prevent users from copying

data and wiping out data validation rules. This example assumes that the work-

sheet has a range named InputArea, and this input area contains data validation

rules (set up by choosing Data ➪ Data Tools ➪ Data Validation). The range can have

any validation rules you want.

A workbook that contains this code is available at this book's website:

Private Sub Worksheet_Change(ByVal Target As Range)

Dim VT As Long

'Do all cells in the validation range

'still have validation?

180    PART 3  Programming Concepts

On Error Resume Next

VT = Range("InputRange").Validation.Type

If Err.Number <> 0 Then

Application.Undo

MsgBox "Your last operation was canceled. " & _

"It would have deleted data validation rules.", vbCritical

End If

End Sub

The procedure is executed whenever a cell is changed. It checks the validation type

of the range (named InputRange) that is  supposed to contain the data validation rules. If the VT variable contains an error, one or more cells in the InputRange no

longer have data validation. (The user probably copied some data over it.) If that's the case, the code executes the Undo method of the Application object and reverses

the user's action. Then it displays a message box, as shown in Figure 11-6. See

Chapter 12 for more information about using On Error Resume Next.

FIGURE 11-6:

Performing data

validation with an

event procedure.

The net effect? It's impossible to wipe out the validation rules by copying data.

When Excel is broken, sometimes you can use VBA to fix it.

Events Not Associated with Objects

The events discussed previously in this chapter are associated with either a work-

book object or a worksheet object. This section focuses on two types of events that

aren't associated with objects: time and keypresses.

Because time and keypresses aren't associated with a particular object such as a

workbook or a worksheet, you program these events in a normal VBA module (unlike the other events discussed in this chapter).

CHAPTER 11  Automatic Procedures and Events    181

The OnTime event

The OnTime event occurs when a particular time of day occurs. The following example demonstrates how to get Excel to execute a procedure when the 3 p.m.

event occurs. In this case, a robot voice tells you to wake up, accompanied by a

message box:

Sub SetAlarm()

Application.OnTime 0.625, "DisplayAlarm"

End Sub

Sub DisplayAlarm()

Application.Speech.Speak ("Hey, wake up")

MsgBox " It's time for your afternoon break!"

End Sub

In this example, you use the OnTime method of the Application object. This method takes two arguments: the time (0.625, which is 3:00 p.m.) and the name

of the Sub procedure to execute when the time event occurs (DisplayAlarm).

This procedure is quite useful if you tend to get so wrapped up in your work that

you forget about meetings and appointments. Just set an OnTime event to remind

yourself.

Most people find it difficult to think of time in terms of the Excel numbering system. Therefore, you may want to use the VBA TimeValue function to represent

the time. TimeValue converts a string that looks like a time into a value that Excel can handle. The following statement shows an easier way to program an event for 3 p.m.:

Application.OnTime TimeValue("3:00:00 pm"), "DisplayAlarm"

If you want to schedule an event relative to the current time (for example,

20 minutes from now), you can use a statement like this:

Application.OnTime Now + TimeValue("00:20:00"), "DisplayAlarm"

You can also use the OnTime method to run a VBA procedure on a particular day.

You must make sure that your computer keeps running and that the workbook

with the procedure is kept open. The following statement runs the DisplayAlarm

procedure at 5 p.m. on December 31, 2019:

Application.OnTime DateValue("12/31/2019 5:00 pm"), "DisplayAlarm"

This particular code line could come in handy to warn you that you need to go

home and get ready for the New Year's Eve festivities.

182    PART 3  Programming Concepts

Here's another example that uses the OnTime event. Executing the UpdateClock procedures writes the time to cell A1 and also programs another event five seconds

later. This event reruns the UpdateClock procedure. The net effect is that cell A1 is updated with the current time every five seconds. To stop the events, execute the

StopClock procedure (which cancels the event). Note that NextTick is a module-

level variable that stores the time for the next event.

Dim NextTick As Date

Sub UpdateClock()

'  Updates cell A1 with the current time

ThisWorkbook.Sheets(1).Range("A1") = Time

'  Set up the next event five seconds from now

NextTick = Now + TimeValue("00:00:05")

Application.OnTime NextTick, "UpdateClock"

End Sub

Sub StopClock()

'  Cancels the OnTime event (stops the clock)

On Error Resume Next

Application.OnTime NextTick, "UpdateClock", , False

End Sub

The OnTime event persists even after the workbook is closed. In other words, if

you close the workbook without running the StopClock procedure, the workbook

reopens itself in five seconds (assuming that Excel is still running). To prevent

this, use a Workbook_BeforeClose event procedure that contains the following statement:

Call StopClock

The OnTime method has two additional arguments. If you plan to use this method,

you should refer to the Help system for complete details.

The OnTime method has a ton of utility for all kinds of applications. Figure 11-7

illustrates an analog-clock workbook that uses the OnTime method to tick every

second. The clock face is actually a chart, and the chart is updated every second to display the time of day.

Keypress events

While you work, Excel constantly monitors what you type. Because of this, you can

set up things so a keystroke or a key combination executes a procedure.

CHAPTER 11  Automatic Procedures and Events    183

FIGURE 11-7:

An analog-clock

application.

Here's an example that reassigns the PgDn and PgUp keys:

Sub Setup_OnKey()

Application.OnKey "{PgDn}", "PgDn_Sub"

Application.OnKey "{PgUp}", "PgUp_Sub"

End Sub

Sub PgDn_Sub()

On Error Resume Next

ActiveCell.Offset(1, 0).Activate

End Sub

Sub PgUp_Sub()

On Error Resume Next

ActiveCell.Offset(-1, 0).Activate

End Sub

After setting up the OnKey events by executing the Setup_OnKey procedure,

pressing PgDn moves you down one row. Pressing PgUp moves you up one row.

Notice that the key codes are enclosed in braces, not in parentheses. For a com-

plete list of keyboard codes, consult the Help system. Search for  OnKey.

In this example, On Error Resume Next ignores any errors that are generated. For

example, if the active cell is in the first row, trying to move up one row causes an error that can safely be ignored. And if a chart sheet is active, there is no active cell.

184    PART 3  Programming Concepts

By executing the following routine, you cancel the OnKey events:

Sub Cancel_OnKey()

Application.OnKey "{PgDn}"

Application.OnKey "{PgUp}"

End Sub

Using an empty string as the second argument for the OnKey method does  not

cancel the OnKey event. Rather, it causes Excel to simply ignore the keystroke. For

example, the following statement tells Excel to ignore Alt+F4. The percent sign

represents the Alt key:

Application.OnKey "%{F4}", ""

Although you can use the OnKey method to assign a shortcut key for executing a

macro, you should use the Macro Options dialog box for this task. For more details,

see Chapter 5.

If you close the workbook that contains the code and leave Excel open, the OnKey

method doesn't reset. As a consequence, pressing the shortcut key causes Excel

to automatically open the file with the macro. To prevent this from happening,

you should include code in your Workbook_BeforeClose event code (shown earlier

in this chapter) to reset the OnKey event.

CHAPTER 11  Automatic Procedures and Events    185

IN THIS CHAPTER

» Understanding the difference

between programming errors and

runtime errors

» Trapping and handling runtime

errors

» Using On Error and Resume

statements

» Finding out how you can use an error

to your advantage

Chapter 12

Error-Handling

Techniques


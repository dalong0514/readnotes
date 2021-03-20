and Tricks

T he previous chapters show you how to insert a UserForm (which contains a

custom dialog box), add controls to the UserForm, and adjust some of the

control’s properties. These skills, however, won’t do you much good unless

you understand how to make use of UserForms in your VBA code. This chapter

provides these missing details and presents some useful techniques and tricks in

the process.

CHAPTER 18  UserForm Techniques and Tricks    295

Using Dialog Boxes

When you use a custom dialog box in your application, you normally write VBA

code that does the following:

» Initializes the UserForm controls. For example, you may write code that sets the default values for the controls.

» Displays the dialog box by using the UserForm object’s Show method.

» Responds to the events that occur for the various controls — such as clicking a CommandButton.

» Validates the information provided by the user (if the user didn’t cancel the dialog box). This step is not always necessary.

» Takes some action with the information provided by the user (if the information is valid).

» Closes the UserForm by using the Unload method.

A UserForm Example

This example demonstrates the five points described in the preceding section. In

this example, you use a dialog box to get two pieces of information: a person’s

name and sex. The dialog box uses a TextBox control to get the name, and it uses

three OptionButtons to get the sex (Male, Female, or Unknown). The information

collected in the dialog box is then sent to the next blank row in a worksheet.

Creating the dialog box

Figure 18-1 shows the finished UserForm for this example. For best results, start

with a new workbook with only one worksheet in it. Then follow these steps:

1. Press Alt+F11 to activate the VBE.

2. In the Project window, select the empty workbook and choose

Insert  ➪ UserForm.

An empty UserForm is added to the project.

3. Change the UserForm’s Caption property to Get Name and Sex.

If the Properties window isn’t visible, press F4.

296    PART 4  Communicating with Your Users

FIGURE 18-1:

This dialog box

asks the user to

enter a Name and

choose a Sex.

This dialog box has eight controls with properties that were adjusted:

» Label

Property

Value

Accelerator

N

Caption

Name

TabIndex

0

» TextBox

Property

Value

Name

TextName

TabIndex

1

» Frame object

Property

Value

Caption

Sex

TabIndex

2

» OptionButton

Property

Value

Accelerator

M

Caption

Male

Name

OptionMale

TabIndex

0

CHAPTER 18  UserForm Techniques and Tricks    297

» Another OptionButton

Property

Value

Accelerator

F

Caption

Female

Name

OptionFemale

TabIndex

1

» Another OptionButton

Property

Value

Accelerator

U

Caption

Unknown

Name

OptionUnknown

TabIndex

2

Value

True

» CommandButton

Property

Value

Caption

Enter

Default

True

Name

EnterButton

TabIndex

b

» CommandButton

Property

Value

Caption

Close

Cancel

True

Name

CloseButton

TabIndex

4

If you’re following along on your computer (and you should be), take a few min-

utes to create this UserForm by using the preceding information. Make sure to

create the Frame object before adding the OptionButtons to it.

298    PART 4  Communicating with Your Users

In some cases, you may find copying an existing control easier than creating a new one. To copy a control, press Ctrl while you drag the control.

If you prefer to cut to the chase, you can download the example from this book’s

website.

Writing code to display the dialog box

After you’ve added the controls to the UserForm, your next step is to develop some

VBA code to display this dialog box:

1. In the VBE window, choose Insert  ➪ Module to insert a VBA module.

2. Enter the following macro:

Sub GetData()

UserForm1.Show

End Sub

This short procedure uses the UserForm object’s Show method to display the

dialog box.

Making the macro available

The next set of steps gives the user an easy way to execute the procedure:

1. Activate Excel.

2. Choose Developer  ➪ Controls  ➪ Insert, and click the Button icon in the  Form Controls section.

3. Drag in the worksheet to create the button.

The Assign Macro dialog box appears.

4. Assign the GetData macro to the button.

5. Edit the button’s caption so that it reads Data Entry.

If you want to get really fancy, you can add an icon to your Quick Access toolbar.

Then click the icon to run the GetData macro. To set this up, right-click your Quick Access toolbar and choose Customize Quick Access Toolbar, which displays the Quick Access Toolbar tab of the Excel Options dialog box. From the Choose Commands From drop-down menu, select Macros. Then select the GetData macro and

click Add. If you like, you can click the Modify button and change the icon. You can also make the Quick Access Toolbar icon visible only when the appropriate CHAPTER 18  UserForm Techniques and Tricks    299

workbook is activated. Before you add the macro, use the drop-down control at

the top-right of the Excel Options dialog box to specify the workbook name, rather

than For All Documents (Default).

Trying out your dialog box

Follow these steps to test your dialog box:

1. Click the Data Entry button on the worksheet, or click the Quick Access

toolbar icon if you set one up.

The dialog box appears, as shown in Figure 18-2.

2. Enter some text in the edit box.

3. Click Enter or Close.

Nothing happens — which is understandable because you haven’t created any

procedures yet.

4. Click the X button on the dialog box’s title bar to dismiss the dialog box.

FIGURE 18-2:

Executing the

GetData

procedure

displays the

dialog box.

Adding event-handler procedures

You’ill often want certain procedures to trigger when certain events occur with

your dialog boxes. For example, you may want to run a procedure when a dialog

box opens. Or maybe you want to force Excel to save the workbook each time the

dialog box closes.

This section walks you through an example of writing procedures that handle

dialog box events.

Start by following these steps:

1. Press Alt+F11 to activate the VBE and then make sure that the UserForm

is displayed.

300    PART 4  Communicating with Your Users

2. Double-click the Close button on the UserForm.

The VBE activates the Code window for the UserForm and provides an empty

procedure named CloseButton_Click.

3. Modify the procedure as follows:

Private Sub CloseButton_Click()

Unload UserForm1

End Sub

This procedure, which is executed when the user clicks the Close button,

simply unloads the dialog box from memory.

4. Press Shift+F7 to redisplay UserForm1.

5. Double-click the Enter button, and enter the following procedure:

Private Sub EnterButton_Click()

Dim NextRow As Long

'  Make sure Sheet1 is active

Sheets("Sheet1").Activate

'  Determine the next empty row

NextRow = Application.WorksheetFunction. _

CountA(Range("A:A")) + 1

'  Transfer the name

Cells(NextRow, 1) = TextName.Text

'  Transfer the sex

If OptionMale Then Cells(NextRow, 2) = "Male"

If OptionFemale Then Cells(NextRow, 2) = "Female"

If OptionUnknown Then Cells(NextRow, 2) = "Unknown"

'  Clear the controls for the next entry

TextName.Text = ""

OptionUnknown = True

TextName.SetFocus

End Sub

6. Activate Excel and run the procedure again by clicking the Data Entry

button.

The dialog box works just fine. Figure 18-3 shows how this looks in action.

While the figure shows column headers in row 1, that step is not necessary.

CHAPTER 18  UserForm Techniques and Tricks    301

FIGURE 18-3:

Use the custom

dialog box for

data entry.

Here’s how the EnterButton_Click procedure works:

1. The code makes sure that the proper worksheet (Sheet1) is active.

2. It then uses the Excel COUNTA function to count the number of entries in

column A and to determine the next blank cell in the column.

3. The procedure transfers the text from the TextBox to column A.

4. It uses a series of If statements to determine which OptionButton was selected and writes the appropriate text (Male, Female, or Unknown) to column B.

5. The dialog box is reset to make it ready for the next entry.

Notice that clicking the Enter button doesn’t close the dialog box, because the user will probably want to enter more data. To end data entry, click the Close button.

Validating the data

Play around with this routine some more, and you’ll find that the macro has a

small problem: It doesn’t ensure that the user actually enters a name in the Text-

Box. The following code — which is inserted into the EnterButton_Click proce-

dure before the text is transferred to the worksheet — ensures that the user enters

some text in the TextBox. If the TextBox is empty, a message appears, and the

routine stops. The dialog box remains open, however, so the user can correct the

problem.

' Make sure a name is entered

If TextName.Text = "" Then

MsgBox "You must enter a name."

Exit Sub

End If

302    PART 4  Communicating with Your Users

Now the dialog box works

After making these modifications, the dialog box works flawlessly. In real life, you’d probably need to collect more information than just name and sex. However, the

same basic principles apply. You just have to deal with more UserForm controls.

One more thing to remember: If the data doesn’t begin in row 1 or if the data area

contains any blank rows, the counting for the NextRow variable will be wrong.

The COUNTA function is counting the number of cells in column A, and the

assumption is that there are no blank cells above the last name in the column.

Here’s another way of determining the next empty row:

NextRow = Cells(Rows.Count, 1).End(xlUp).Row + 1

The statement simulates activating the last cell in column A, pressing End, press-

ing the up-arrow key, and then moving down one row. If you do that manually,

the cell pointer will be in the next empty cell in column A — even if the data area

doesn’t begin in row 1 and contains blank rows.

A ListBox Example

ListBoxes are useful controls, but working with them can be a bit tricky. Before displaying a dialog box that uses a ListBox, you need to fill the ListBox with items. Then, when the dialog box is closed, you need to determine which item(s) the user selected.

When dealing with ListBoxes, you need to know about the following properties

and methods:

» AddItem: You use this method to add an item to a ListBox.

» ListCount: This property returns the number of items in the ListBox.

» ListIndex: This property returns the index number of the selected item or

sets the item that’s selected (single selections only). The first item has a

ListIndex of 0 (not 1).

» MultiSelect: This property determines whether the user can select more than one item from the ListBox.

» RemoveAllItems: Use this method to remove all items from a ListBox.

» Selected: This property returns an array indicating selected items (applicable only when multiple selections are allowed).

» Value: This property returns the selected item in a ListBox.

CHAPTER 18  UserForm Techniques and Tricks    303

Most of the methods and properties that work with ListBoxes also work with ComboBoxes. So after you’ve figured out how to handle ListBoxes, you can transfer that knowledge to your work with ComboBoxes.

Filling a ListBox

To keep things simple, start with an empty workbook. The example in this section

assumes the following:

» You’ve added a UserForm.

» The UserForm contains a ListBox control named ListBox1 .

» The UserForm has a CommandButton named OKButton.

» The UserForm has a CommandButton named CancelButton, which has the

following event-handler procedure:

Private Sub CancelButton_Click()

Unload UserForm1

End Sub

The following procedure is stored in the Initialize procedure for the UserForm.

Follow these steps:

1. Select your UserForm, and press F7 to activate its Code window.

The VBE displays the Code window for your form and is ready for you to input

the code for the Initialize event.

2. From the Procedure drop-down list at the top of the Code window,

choose Initialize.

3. Add the initialization code for the form:

Sub UserForm_Initialize()

'  Fill the list box

With ListBox1

.AddItem "January"

.AddItem "February"

.AddItem "March"

.AddItem "April"

.AddItem "May"

.AddItem "June"

.AddItem "July"

.AddItem "August"

304    PART 4  Communicating with Your Users

.AddItem "September"

.AddItem "October"

.AddItem "November"

.AddItem "December"

End With

'  Select the first list item

ListBox1.ListIndex = 0

End Sub

This initialization routine runs automatically whenever your UserForm is

loaded. So when you use the Show method for the UserForm, the code is

executed and your ListBox is populated with 12 items, each added via the

AddItem method.

4. Insert a VBA module, and type this short Sub procedure to display the

dialog box:

Sub ShowList()

UserForm1.Show

End Sub

Determining the selected item

The preceding code merely displays a dialog box with a ListBox filled with month

names. What’s missing is a procedure to determine which item in the ListBox is

selected.

Double-click the OKButton, and add the following OKButton_Click procedure:

Private Sub OKButton_Click()

Dim Msg As String

Msg = "You selected item # "

Msg = Msg & ListBox1.ListIndex

Msg = Msg & vbNewLine

Msg = Msg & ListBox1.Value

MsgBox Msg

Unload UserForm1

End Sub

This procedure displays a message box with the selected item number and the

selected item.

CHAPTER 18  UserForm Techniques and Tricks    305

If no item in the ListBox is selected, the ListIndex property returns –1. However,

this will never be the case for this particular ListBox, because code in the

UserForm_Initialize procedure selected the first item. It’s impossible to unselect

an item without selecting another item. So there will  always be a selected item, if the user doesn’t actually select a month.

Figure 18-4 shows how this looks.

FIGURE 18-4:

Determining

which item

in a ListBox

is selected.

The first item in a ListBox has a ListIndex of 0, not 1 (as you might expect). This

is always the case, even if you use an Option Base 1 statement to change the default lower bound for arrays.

This example is available at this book’s website.

Determining multiple selections

If your ListBox is set up so that the user can select more than one item, you find

that the ListIndex property returns only the  last item selected. To determine all selected items, you need to use the Selected property, which contains an array.

To allow multiple selections in a ListBox, set the MultiSelect property to either 1

or 2. You can do so at design time by using the Properties window or at runtime by

using a VBA statement such as this:

UserForm1.ListBox1.MultiSelect = 1

The MultiSelect property has three possible settings. The meaning of each is

shown in Table 18-1.

306    PART 4  Communicating with Your Users

TABLE 18-1

Settings for the MultiSelect Property

Value

VBA Constant

Meaning

0

fmMultiSelectSingle

Only a single item can be selected.

1

fmMultiSelectMulti

Clicking an item or pressing the space bar selects or

deselects an item in the list.

2

fmMultiSelectExtended

Items are added to or removed from the selection

set by holding down the Shift or Ctrl key as you

click items.

The following procedure displays a message box that lists all selected items in a

ListBox. Figure 18-5 shows an example.

Private Sub OKButton_Click()

Dim Msg As String

Dim i As Long

Dim Counter As Long

Msg = "You selected:" & vbNewLine

For i = 0 To ListBox1.ListCount - 1

If ListBox1.Selected(i) Then

Counter = Counter + 1

Msg = Msg & ListBox1.List(i) & vbNewLine

End If

Next i

If Counter = 0 Then Msg = Msg & "(nothing)"

MsgBox Msg

Unload UserForm1

End Sub

FIGURE 18-5:

Determining the

selected items in

a ListBox that

allows multiple

selections.

CHAPTER 18  UserForm Techniques and Tricks    307

This routine uses a For-Next loop to cycle through each item in the ListBox. Notice

that the loop starts with item 0 (the first item) and ends with the last item ( determined by the value of the ListCount property minus 1). If an item’s Selected

property is True, it means that the list item was selected. The code also uses a

variable (Counter) to keep track of how many items are selected. An If-Then statement modifies the message if nothing is selected.

This example is available at this book’s website.

Selecting a Range

In some cases, you may want the user to select a range while a dialog box is displayed. An example of this type of range selection occurs in the Create Table

dialog box, which is displayed when you choose Home ➪ Insert ➪ Tables ➪ Table.

The Create Table dialog box has a range selector control that contains Excel’s guess regarding the range to be converted — but you can use this control to change the range by selecting cells in the worksheet.

To allow a range selection in your dialog box, add a RefEdit control. The following

example displays a dialog box with the current region’s range address displayed

in a RefEdit control, as shown in Figure 18-6. The current region is the block of

nonempty cells that contains the active cell. The user can accept or change this

range. When the user clicks OK, the procedure makes the range bold.

FIGURE 18-6:

This dialog box

lets the user

select a range.

308    PART 4  Communicating with Your Users

This example assumes the following:

» You have a UserForm named UserForm1.

» The UserForm contains a CommandButton control named OKButton.

» The UserForm contains a CommandButton control named CancelButton.

» The UserForm contains a RefEdit control named RefEdit1.

The code is stored in a VBA module and shown here. This code does two things:

initializes the dialog box by assigning the current region’s address to the RefEdit

control and displays the UserForm.

Sub BoldCells()

'  Exit if worksheet is not active

If TypeName(ActiveSheet) <> "Worksheet" Then Exit Sub

'  Select the current region

ActiveCell.CurrentRegion.Select

'  Initialize RefEdit control

UserForm1.RefEdit1.Text = Selection.Address

'  Show dialog

UserForm1.Show

End Sub

The following procedure is executed when the OK button is clicked. This procedure

does some simple error checking to make sure that the range specified in the RefEdit control is valid.

Private Sub OKButton_Click()

On Error GoTo BadRange

Range(RefEdit1.Text).Font.Bold = True

Unload UserForm1

Exit Sub

BadRange:

MsgBox "The specified range is not valid."

End Sub

If an error occurs (most likely an invalid range specification in the RefEdit con-

trol), the code jumps to the BadRange label, and a message box is displayed. The

dialog box remains open so the user can select another range.

CHAPTER 18  UserForm Techniques and Tricks    309

If getting a user selected range is the  only function performed by your UserForm, you can simplify things by using the Application InputBox method (see

Chapter 15).

Using Multiple Sets of OptionButtons

Figure 18-7 shows a custom dialog box with three sets of OptionButtons. If your

UserForm contains more than one set of OptionButtons, make sure that each set

of OptionButtons works as a group. You can do so in either of two ways:

» Enclose each set of OptionButtons in a Frame control. This approach is easier and also makes the dialog box look more organized. It’s easier to add the

Frame before adding the OptionButtons. You can, however, also drag existing

OptionButtons into a Frame.

» Make sure that each set of OptionButtons has a unique GroupName property

(which you specify in the Properties box). If the OptionButtons are in a Frame,

you don’t have to be concerned with the GroupName property.

FIGURE 18-7:

This dialog

box contains

three sets of

OptionButton

controls.

Only one OptionButton in a group can have a value of True. To specify a default

option for a set of OptionButtons, just set the Value property for the default item

to True. You can do this directly in the Properties box or by using VBA code:

UserForm1.OptionButton1.Value = True

310    PART 4  Communicating with Your Users

This example is available at this book’s website. It also has code that displays the selected options when the user clicks OK.

Using a SpinButton and a TextBox

A SpinButton control lets the user specify a number by clicking arrows. This con-

trol consists only of arrows (no text), so you usually want a method to display the

selected number. One option is to use a Label control, but this has a disadvantage:

The user can’t type text in a Label. A better choice is to use a TextBox.

A SpinButton control and TextBox control form a natural pair, and Excel uses them

frequently. For example, check out Excel’s Page Setup dialog box for a few exam-

ples. Ideally, the SpinButton and its TextBox are always in sync: If the user clicks the SpinButton, the SpinButton’s value should appear in the TextBox. And if the

user enters a value directly into the TextBox, the SpinButton should take on that

value. Figure 18-8 shows a custom dialog box with a SpinButton and a TextBox.

FIGURE 18-8:

A UserForm with

a SpinButton and

a companion

TextBox.

This UserForm contains the following controls:

» A SpinButton named SpinButton1, with its Min property set to 1 and its Max

property set to 100

» A TextBox named TextBox1, positioned to the left of the SpinButton

» A CommandButton named OKButton

The event-handler procedure for the SpinButton follows. This procedure handles

the Change event, which is triggered whenever the SpinButton value is changed.

When the SpinButton’s value changes (when it’s clicked), this procedure assigns

the SpinButton’s value to the TextBox. To create this procedure, double-click the

SpinButton to activate the Code window for the UserForm. Then enter this code:

Private Sub SpinButton1_Change()

TextBox1.Text = SpinButton1.Value

End Sub

CHAPTER 18  UserForm Techniques and Tricks    311

The event-handler for the TextBox, which is listed next, is a bit more complicated.

To create this procedure, double-click the TextBox to activate the Code window

for the UserForm. This procedure is executed whenever the user changes the text

in the TextBox.

Private Sub TextBox1_Change()

Dim NewVal As Long

NewVal = Val(TextBox1.Text)

If NewVal >= SpinButton1.Min And _

NewVal <= SpinButton1.Max Then _

SpinButton1.Value = NewVal

End Sub

This procedure uses a variable, which stores the text in the TextBox (converted to

a value with the Val function). It then checks to ensure that the value is within the proper range. If so, the SpinButton is set to the value in the TextBox. The net effect is that the SpinButton’s value is always equal to the value in the TextBox (assuming that the SpinButton’s value is in the proper range).

If you press F8 to single-step through the code in debugging mode, you’ll notice

that when the line SpinButton1.Value = NewVal is executed, the change event of

the SpinButton immediately fires. In turn, the SpinButton1_Change event sets the

value of TextBox1. Luckily, this in turn doesn’t fire the TextBox1_Change event,

because its value is not actually changed by the SpinButton1_Change event. But

you can imagine that this effect can cause surprising results in your UserForm.

Confused? Just remember that if your code changes the Value of a control, the

Change event of that control will fire.

This example is available at this book’s website. It also has a few other bells and

whistles that you may find useful.

Using a UserForm as a Progress Indicator

If you have a macro that takes a long time to run, you might want to display a

progress meter so people won’t think Excel has crashed. You can use a UserForm

to create an attractive progress indicator, as shown in Figure 18-9. Such a use of

dialog boxes does, however, require a few tricks.

312    PART 4  Communicating with Your Users

FIGURE 18-9:

This UserForm

functions as a

progress

indicator for a

lengthy macro.

Creating the progress-indicator dialog box

The first step is to create your UserForm. In this example, the dialog box displays

the progress while a macro inserts random numbers into 100 columns and

1,000 rows of the active worksheet. To create the dialog box, follow these steps:

1. Activate the VBE, and insert a new UserForm.

2. Change the UserForm’s caption to Progress.

3. Add a Frame object, and set the following properties:

Property

Value

Caption

0%

Name

FrameProgress

SpecialEffect

2 — fmSpecialEffectSunken

Width

204

Height

28

4. Add a Label object inside the Frame, and set the following properties:

Property

Value

Name

LabelProgress

BackColor

&H0000C000& (green)

Caption

(no caption)

SpecialEffect

1 — fmSpecialEffectRaised

Width

20

CHAPTER 18  UserForm Techniques and Tricks    313

Property

Value

Height

13

Top

5

Left

2

5. Add another Label above the frame, and change its caption to Entering

random numbers. . .

The UserForm should resemble Figure 18-10.

FIGURE 18-10:

The progress-

indicator

UserForm.

The procedures

This example uses two procedures and a module-level variable:

» The module-level variable: Located in a VBA module, this variable holds

the copy of the UserForm:

Dim ProgressIndicator as UserForm1

» Ente.rRandomNumbers: This procedure does all the work and is executed

when the UserForm is shown. Notice that it calls the UpdateProgress proce-

dure, which updates the progress indicator in the dialog box:

Sub EnterRandomNumbers()

'  Inserts random numbers on the active worksheet

Dim Counter As Long

Dim RowMax As Long, ColMax As Long

Dim r As Long, c As Long

Dim PctDone As Single

314    PART 4  Communicating with Your Users

'  Create a copy of the form in a variable

Set ProgressIndicator = New UserForm1

'  Show ProgressIndicator in modeless state

ProgressIndicator.Show vbModeless

If TypeName(ActiveSheet) <> "Worksheet" Then

Unload ProgressIndicator

Exit Sub

End If

'  Enter the random numbers

Cells.Clear

Counter = 1

RowMax = 200

ColMax = 50

For r = 1 To RowMax

For c = 1 To ColMax

Cells(r, c) = Int(Rnd * 1000)

Counter = Counter + 1

Next c

PctDone = Counter / (RowMax * ColMax)

Call UpdateProgress(PctDone)

Next r

Unload ProgressIndicator

Set ProgressIndicator = Nothing

End Sub

» UpdateProgress: This procedure accepts one argument and updates the

progress indicator in the dialog box:

Sub UpdateProgress(pct)

With ProgressIndicator

.FrameProgress.Caption = Format(pct, "0%")

.LabelProgress.Width = pct * (.FrameProgress _

.Width - 10)

End With

'  The DoEvents statement is responsible for the form updating

DoEvents

End Sub

CHAPTER 18  UserForm Techniques and Tricks    315

How this example works

When the EnterRandomNumbers procedure is executed, it loads a copy of

UserForm1 into the module variable named ProgressIndicator. Then it sets the width of the LabelProgress label to 0 and displays the UserForm in modeless state

(so the code will continue to run).

The EnterRandomNumber procedure checks the active sheet. If it’s not a work-

sheet, the UserForm (ProgressIndicator) is closed, and the procedure ends with no

action. If the active sheet is a worksheet, the procedure does the following:

1. Erases all cells on the active worksheet.

2. Loops through the rows and columns (specified by the RowMax and ColMax

variables) and inserts a random number in each cell.

3. Increments the Counter variable and calculates the percentage completed

(which is stored in the PctDone variable).

4. Calls the UpdateProgress procedure, which displays the percentage completed by changing the width of the LabelProgress label and updating the caption of

the frame control.

5. Unloads the UserForm.

Using a progress indicator will, of course, make your macro run a bit slower

because the code is doing additional work updating the UserForm. If speed is absolutely critical, think twice about using a progress indicator.

If you adapt this technique for your own use, you need to figure out how to deter-

mine the macro’s progress, which varies depending on your macro. Then call the

UpdateProgress procedure at periodic intervals while your macro is executing.

This example is available at this book’s website.

Creating a Modeless Tabbed Dialog Box

Tabbed dialog boxes are useful because they let you present information in small,

organized chunks. Excel’s Format Cells dialog box (which is displayed when you

right-click a cell and choose Format Cells) is a good example. The dialog box in

this example uses three tabs to help organize some of Excel’s display options.

Creating your own tabbed dialog boxes is relatively easy, thanks to the MultiPage

control. Figure 18-11 shows a custom dialog box that uses a MultiPage control with

316    PART 4  Communicating with Your Users

three  pages,  or  tabs.  When the user clicks a tab, a new page is activated, and only the controls on that page are displayed.

FIGURE 18-11:

The three tabs

of a MultiPage

control.

Notice that this is a modeless dialog box. In other words, the user can keep it displayed while working. Each of the controls has an immediate effect, so there is

no need to have an OK button. Here’s the procedure that displays the UserForm so

it stays on top:

Sub ShowDialog()

UserForm1.Show vbModeless

End Sub

Keep the following points in mind when using the MultiPage control to create a

tabbed dialog box:

» Use only one MultiPage control per dialog box.

» To make some controls (such as OK, Cancel, and Close buttons) visible at all times, place these controls outside the MultiPage control.

» Right-click a tab on the MultiPage control to display a shortcut menu that lets you add, remove, rename, or move a tab.

» At design time, click a tab to activate the page. After it’s activated, add other controls to the page by using normal procedures.

CHAPTER 18  UserForm Techniques and Tricks    317

» To select the MultiPage control itself (rather than a page on the control), click the border of the MultiPage control. Keep your eye on the Properties window,

which displays the name and type of the selected control. You can also select

the MultiPage control by selecting its name from the drop-down list in the

Properties window.

» You can change the look of the MultiPage control by changing the Style and

TabOrientation properties.

» The Value property of a MultiPage control determines which page is displayed.

For example, if you write code to set the Value property to 0, the first page of

the MultiPage control is displayed.

This example is available at this book’s website.

Displaying a Chart in a UserForm

If you need to display a chart in a UserForm, you find that Excel doesn’t provide

any direct way to do so. Therefore, you need to get creative. This section describes a technique that allows you to display one or more charts in a UserForm.

Figure 18-12 shows an example that displays three charts. The UserForm has an

Image control. The trick is to use VBA code to save the chart as a GIF file and then specify that file as the Image control’s Picture property (which loads the image

from your disk). The Previous and Next buttons switch the displayed chart.

FIGURE 18-12:

Displaying a chart

in a UserForm.

318    PART 4  Communicating with Your Users

In this example, which is also available on this book’s website, the three charts are on a sheet named Charts. The Previous and Next buttons determine which chart to

display, and this chart number is stored as a Public variable named ChartNum,

which is accessible to all procedures. A procedure named UpdateChart, which is

listed here, does the actual work.

Private Sub UpdateChart()

Dim CurrentChart As Chart

Dim Fname As String

Set CurrentChart = _

Sheets("Charts").ChartObjects(ChartNum).Chart

CurrentChart.Parent.Width = 300

CurrentChart.Parent.Height = 150

'  Save chart as GIF

Fname = ThisWorkbook.Path & "\temp.gif"

CurrentChart.Export FileName:=Fname, FilterName:="GIF"

'  Show the chart

Image1.Picture = LoadPicture(Fname)

End Sub

This procedure determines a name for the saved chart and then uses the Export

method to export the GIF file. Finally, it uses the VBA LoadPicture function to specify the Picture property of the Image object.

A Dialog Box Checklist

Remember that a dialog box is essentially your only way to communicate with

your end user. After all, dialog boxes are user interfaces.

As you start designing you own user interfaces, run down this checklist to ensure

you’re building dialog boxes that are both functional and intuitive:

» Are the controls aligned with one another?

» Are similar controls the same size?

» Are the controls evenly spaced?

» Does the dialog box have an appropriate caption?

CHAPTER 18  UserForm Techniques and Tricks    319

» Is the dialog box overwhelming? If so, you may want to use a series of dialog boxes or divide them over a MultiPage control.

» Can the user access every control with an accelerator key?

» Are any accelerator keys duplicated?

» Are the controls grouped logically, by function?

» Is the tab order set correctly? The user should be able to tab through the

dialog box and access the controls sequentially.

» If you plan to store the dialog box in an add-in, did you test it thoroughly after creating the add-in?

» Will your VBA code take appropriate action if the user cancels the dialog box, presses Esc, or uses the Close button?

» Does the text contain any misspellings? Unfortunately, the Excel spell checker doesn’t work with UserForms, so you’re on your own when it comes to spelling.

» Will your dialog box fit on the screen in the lowest resolution to be used

(usually, 1024×768 mode)? In other words, if you develop your dialog box by

using a high-resolution video mode, your dialog box may be too big to fit on a

lower-resolution screen.

» Do all TextBox controls have the appropriate validation setting?

» If you intend to use the WordWrap property, is the MultiLine property also set to True?

» Do all ScrollBars and SpinButtons allow valid values only?

» Do all ListBoxes have their MultiSelect property set properly?

Start simply and experiment with the controls and their properties. And don’t

forget about the Help system; it’s your best source for details about every control

and property.

320    PART 4  Communicating with Your Users

IN THIS CHAPTER

» Getting to know ways to customize

the Ribbon

» Adding icons to the Quick Access

toolbar

» Modifying shortcut menus

Chapter 19

Accessing Your

Macros through

the User Interface

B efore Office 2007, there was no such thing as a Ribbon. Back then, people


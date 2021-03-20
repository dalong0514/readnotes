UserForm Basics

A UserForm is useful if your VBA macro needs to pause and get some

information from a user. For example, your macro may have some options

that can be specified in a UserForm. If only a few pieces of information are

required (for example, a Yes/No answer or a text string), one of the techniques in

Chapter 15 may do the job. But if you need to obtain more information, you must

create a UserForm. That’s what this chapter is all about.

Knowing When to Use a UserForm

This section describes a situation in which a UserForm is useful. The following

macro changes the text in each cell in the selection to uppercase letters. It does

this by using the VBA built-in UCase function.

Sub ChangeCase()

Dim WorkRange As Range, cell As Range

'  Exit if a range is not selected

If TypeName(Selection) &lt;&gt; "Range" Then Exit Sub

'  Process only text cells, no formulas

On Error Resume Next

Set WorkRange = Selection.SpecialCells _

(xlCellTypeConstants, xlCellTypeConstants)

CHAPTER 16  UserForm Basics    257

For Each cell In WorkRange

cell.Value = UCase(cell.Value)

Next cell

End Sub

You can make this macro even more useful. For example, it would be nice if the

macro could also change the text in the cells to either lowercase or proper case

(capitalizing the first letter in each word). One approach is to create two additional macros — one for lowercase and one for proper case. Another approach is to modify the macro to handle the other options. If you use the second approach, you

need some method of asking the user which type of change to make to the cells.

The solution is to display a dialog box like the one shown in Figure 16-1. You create this dialog box on a UserForm in the VBE and display it by using a VBA macro. The

next section offers step-by-step instructions for creating this dialog box.

FIGURE 16-1:

You can get

information from

the user by

displaying a

UserForm.

In VBA, the official name for a dialog box is a UserForm. But a UserForm is really

an object that contains what’s commonly known as a  dialog box.  This distinction isn’t important, so you’ll often here these terms used interchangeably.

Creating UserForms: An Overview

When creating a UserForm, you usually take the following general steps:

1. Determine how the dialog box will be used and at what point it will be

displayed in your VBA macro.

2. Press Alt+F11 to activate the VBE and insert a new UserForm object.

A UserForm object holds a single UserForm.

258    PART 4  Communicating with Your Users

3. Add controls to the UserForm.

Controls include items such as text boxes, buttons, check boxes, and list boxes.

4. Use the Properties window to modify the properties for the controls or

for the UserForm itself.

5. Write event-handler procedures for the controls (for example, a macro

that executes when the user clicks a button in the dialog box).

These procedures are stored in the Code window for the UserForm object.

6. Write a procedure (stored in a VBA module) that displays the dialog box

to the user.

Don’t worry if some of these steps seem foreign. The following sections provide

more details, along with step-by-step instructions for creating a UserForm.

When you’re designing a UserForm, you’re creating what developers call the Graphical User Interface (GUI) to your application. GUI also stands for Gaming Under the Influence, but that’s not relevant here.

Take some time to consider what your form should look like and how your users

are likely to want to interact with the elements on the UserForm. Try to guide

them through the steps they need to take on the form by carefully considering

the arrangement and wording of the controls. Like most things VBA-related, the

more you do it, the easier it gets.

Working with UserForms

Each dialog box that you create is stored in its own UserForm object — one dialog

box per UserForm. You create and access these UserForms in the Visual Basic

Editor.

Inserting a new UserForm

Insert a UserForm object by following these steps:

1. Activate the VBE by pressing Alt+F11.

2. Select the workbook that will hold the UserForm in the Project window.

3. Choose Insert  ➪ UserForm.

The VBE inserts a new UserForm object, which contains an empty dialog box.

CHAPTER 16  UserForm Basics    259

Figure 16-2 shows a UserForm — an empty dialog box. Your job, if you choose to

accept it, is to add some controls to this UserForm.

FIGURE 16-2:

A new UserForm

object.

Adding controls to a UserForm

When you activate a UserForm, the VBE displays the Toolbox in a floating window

(refer to Figure 16-2). You use the tools in the Toolbox to add controls to your

UserForm. If, for some reason, the Toolbox doesn’t appear when you activate your

UserForm, choose View ➪ Toolbox.

To add a control, just click the desired control in the Toolbox and drag it into the dialog box to create the control. After you add a control, you can move and resize

it by using standard techniques.

Table 16-1 lists the various tools, as well as their capabilities. To determine which tool is which, hover your mouse pointer over the control and read the small pop-up description.

TABLE 16-1

Toolbox Controls

Control

What It Does

Label

Shows text

TextBox

Allows the user to enter text

ComboBox

Displays a drop-down list

ListBox

Displays a list of items

CheckBox

Provides options such as on/off or yes/no

OptionButton

Allows the user to select one of several options; used in

groups of two or more

260    PART 4  Communicating with Your Users

Control

What It Does

ToggleButton

Enables the user to switch a button on or off

Frame

Contains other controls

CommandButton

Adds a clickable button

TabStrip

Displays tabs

MultiPage

Creates a tabbed container for other objects

ScrollBar

Enables the user to drag a bar to establish a setting

SpinButton

Enables the user to click a button to change a value

Image

Holds an image

RefEdit

Allows the user to select a range

Changing properties for a UserForm control

Every control you add to a UserForm has properties that determine how the control

looks or behaves. In addition, the UserForm itself has its own set of properties.

You can change these properties with the aptly named Properties window.

Figure 16-3 shows the Properties window when a CommandButton control is

selected.

FIGURE 16-3:

Use the

Properties

windows to

change the

properties of

UserForm

controls.

The Properties window appears when you press F4. Alternatively, you can choose

View ➪ Properties Window. The properties shown in this window depend on what

is selected. If you select a different control, the properties change to those appropriate for that control. To hide the Properties window and get it out of the

way, click the Close button in its title bar. Pressing F4 always brings it back when you need it.

CHAPTER 16  UserForm Basics    261

Properties for controls include the following:

» Name

» Width

» Height

» Value

» Caption

Each control has its own set of properties (although many controls have some common properties). To change a property using the Properties window, follow

these steps:

1. Make sure that the correct control is selected in the UserForm.

2. Make sure the Properties window is visible. (Press F4 if it’s not.)

3. In the Properties window, click the property that you want to change.

4. Make the change in the right portion of the Properties window.

If you select the UserForm itself (not a control on the UserForm), you can use the

Properties window to adjust UserForm properties.

Chapter 17 tells you everything you need to know about working with dialog box

controls.

Some of the UserForm properties serve as default settings for new controls you

drag onto the UserForm. For example, if you change the Font property for the

UserForm itself, controls that you subsequently add use that same font. Controls

that are already on the UserForm aren’t affected.

Viewing the UserForm Code window

Every UserForm object has a Code module that holds the VBA code (the event-

handler procedures) that is executed when the user works with the dialog box.

To view the Code module, press F7. The Code window is empty until you add some

procedures. Press Shift+F7 to return to the UserForm.

Here’s another way to switch between the Code window and the UserForm display:

Use the View Code and View Object buttons in the Project window’s title bar. Or

right-click the UserForm and choose View Code. If you’re viewing code, double-

click the UserForm name in the Project window to return to the UserForm.

262    PART 4  Communicating with Your Users

Displaying a UserForm

You display a UserForm by using the UserForm’s Show method in a VBA

procedure.

The macro that displays the dialog box must be in a VBA module — not in the Code

window for the UserForm.

The following procedure displays the dialog box named UserForm1:

Sub ShowDialogBox()

UserForm1.Show

'  Other statements can go here

End Sub

When Excel displays the dialog box, the ShowDialogBox macro halts until the user closes the dialog box. Then VBA executes any remaining statements in the

procedure. Most of the time, you won’t have any more code in the procedure. As

you later see, you put your event-handler procedures in the Code window for the

UserForm. These procedures kick in when the user works with the controls on the

UserForm.

Using information from a UserForm

The VBE provides a name for each control you add to a UserForm. The control’s

name corresponds to its Name property. Use this name to refer to a particular

control in your code. For example, if you add a CheckBox control to a UserForm

named UserForm1, the CheckBox control is named CheckBox1 by default. You can

use the Properties box to make this control appear with a check mark. Or you can

write code to do it:

UserForm1.CheckBox1.Value = True

Most of the time, you write the code for a UserForm in the UserForm’s code mod-

ule. If that’s the case, you can omit the UserForm object qualifier and write the

statement like this:

CheckBox1.Value = True

Your VBA code can also check various properties of the controls and take appro-

priate actions. The following statement executes a macro named PrintReport if

the check box (named CheckBox1) is checked:

If CheckBox1.Value = True Then Call PrintReport

CHAPTER 16  UserForm Basics    263

It’s usually a good idea to change the default name the VBE gives to your controls to something more meaningful. You might consider naming the check box

something like cbxPrintReport. Note the three-letter prefix (cbx). There is no technical reason for using cbx as the prefix. This is just one example of using a

naming convention to differentiate objects in VBA. Using a naming convention like this makes your code easier to read. In the end, the convention you choose is

a matter of what you’re comfortable with.

A UserForm Example

This section’s UserForm example is an enhanced version of the ChangeCase macro

from the beginning of the chapter. The original version of this macro changes the

text in the selected cells to uppercase. This modified version uses a UserForm to

ask the user which type of change to make: uppercase, lowercase, or proper case.

This dialog box needs to obtain one piece of information from the user: the type of

change to make to the text. Because the user has three choices, your best bet is a

dialog box with three OptionButton controls. The dialog box also needs two more

buttons: an OK button and a Cancel button. Clicking the OK button runs the code

that does the work. Clicking the Cancel button causes the macro to finish without

doing anything.

This workbook is available at the book’s website. However, you get more out of

this exercise if you follow the steps provided here and create it yourself.

Creating the UserForm

These steps create the UserForm. Start with an empty workbook, and follow these

steps:

1. Press Alt+F11 to activate the VBE.

2. If multiple projects are in the Project window, select the project that

corresponds to the workbook you’re using.

3. Choose Insert  ➪ UserForm.

The VBE inserts a new UserForm object with an empty dialog box.

4. Press F4 to display the Properties window.

5. In the Properties window, change the dialog box’s Caption property to

Change Case.

264    PART 4  Communicating with Your Users

6. (Optional) The dialog box is a bit too large, so you may want to click it and  use the handles (on the right and bottom sides) to make it smaller.

You can do Step 6 after you position all the controls in the dialog box.

Adding the CommandButtons

Ready to add two CommandButtons — OK and Cancel — to the dialog box? Follow

along:

1. Make sure that the Toolbox is displayed; if it isn’t, choose View  ➪ Toolbox.

2. If the Properties window isn’t visible, press F4 to display it.

3. In the Toolbox, drag a CommandButton into the dialog box to create a

button.

As you see in the Properties box, the button has a default name and caption:

CommandButton1.

4. Make sure that the CommandButton is selected; then activate the

Properties window and change the following properties:

Property

Change To

Name

OKButton

Caption

OK

Default

True

5. Add a second CommandButton object to the UserForm and change the

following properties:

Property

Change To

Name

CancelButton

Caption

Cancel

Cancel

True

6. Adjust the size and position of the controls so your dialog box looks

something like Figure  16-4.

CHAPTER 16  UserForm Basics    265

FIGURE 16-4:

The UserForm

with two

CommandButton

controls.

Adding the OptionButtons

In this section, you add three OptionButtons to the dialog box. Before adding the

OptionButtons, you add a Frame object that contains the OptionButtons. The Frame isn’t necessary, but it makes the dialog box look a bit more professional so

users won’t think it was designed by an amateur.

To add the OptionButtons, follow these steps:

1. In the Toolbox, click the Frame tool and drag it into the dialog box.

This step creates a frame to hold the options buttons.

2. Use the Properties window to change the frame’s caption to Options.

3. In the Toolbox, click the OptionButton tool and drag it into the dialog box

(within the Frame).

Doing this creates an OptionButton control.

4. Select the OptionButton and use the Properties window to change the

following properties:

Property

Change To

Name

OptionUpper

Caption

Upper Case

Accelerator

U

Value

True

Setting the Value property to True makes this OptionButton the default.

266    PART 4  Communicating with Your Users

5. Add another OptionButton and use the Properties window to change the

following properties:

Property

Change To

Name

OptionLower

Caption

Lower Case

Accelerator

L

6. Add a third OptionButton and use the Properties window to change the

following properties:

Property

Change To

Name

OptionProper

Caption

Proper Case

Accelerator

P

7. Adjust the size and position of the OptionButtons, Frame, and dialog box.

Your UserForm should look something like Figure 16-5.

FIGURE 16-5:

This is the

UserForm after

adding three

OptionButton

controls inside a

Frame control.

If you’d like a sneak preview to see what the UserForm looks like when it’s dis-

played, press F5. None of the controls work yet, so you need to click the red X in

the title bar to close the dialog box.

The Accelerator property determines which letter in the caption is underlined —

and more important, it determines what Alt+key combination selects that control.

For example, you can select the Lower Case option by pressing Alt+L because the

L is underlined. Accelerator keys are optional, but some users prefer to use the

keyboard to navigate dialog boxes.

CHAPTER 16  UserForm Basics    267

You may wonder why the OptionButtons have accelerator keys but the CommandButtons lack such a feature. Generally, OK and Cancel buttons never have accelerator keys because they can be accessed from the keyboard. Pressing

Enter is equivalent to clicking OK because the control’s Default property is True.

Pressing Esc is equivalent to clicking Cancel because the control’s Cancel property

is True.

Adding event-handler procedures

Now it’s time to make the UserForm actually do something. Here’s how to add an

event-handler procedure for the Cancel and OK buttons:

1. Double-click the Cancel button.

The VBE activates the Code window for the UserForm and inserts an empty

procedure:

Private Sub CancelButton_Click()

End Sub

The procedure named CancelButton_Click is executed when the Cancel button

is clicked, but only when the dialog box is displayed. In other words, clicking the

Cancel button when you’re designing the dialog box won’t execute the

procedure. Because the Cancel button’s Cancel property is set to True, pressing

Esc also triggers the CancelButton_Click procedure.

2. Insert the following statement inside the procedure (before the End Sub

statement):

Unload UserForm1

This statement closes the UserForm when the Cancel button is clicked.

3. Press Shift+F7 to return to the UserForm.

4. Double-click the OK button.

The VBE activates the Code window for the UserForm and inserts an empty

Sub procedure called OKButton_Click.

When the UserForm is displayed, clicking OK executes this procedure. Because

this button has its Default property set to True, pressing Enter also executes

the OKButton_Click procedure.

268    PART 4  Communicating with Your Users

5. Enter the following code so the procedure looks like this:

Private Sub OKButton_Click()

Dim WorkRange As Range

Dim cell As Range

'  Process only text cells, no formulas

On Error Resume Next

Set WorkRange = Selection.SpecialCells _

(xlCellTypeConstants, xlCellTypeConstants)

'  Upper case

If OptionUpper Then

For Each cell In WorkRange

cell.Value = UCase(cell.Value)

Next cell

End If

'  Lower case

If OptionLower Then

For Each cell In WorkRange

cell.Value = LCase(cell.Value)

Next cell

End If

'  Proper case

If OptionProper Then

For Each cell In WorkRange

cell.Value = Application. _

WorksheetFunction.Proper(cell.Value)

Next cell

End If

Unload UserForm1

End Sub

The preceding code is an enhanced version of the original ChangeCase macro

presented at the beginning of the chapter. The macro consists of three separate

blocks of code. This code uses three If-Then structures; each one has a For Each-Next loop. Only one block is executed, determined by which OptionButton

the user selects. The last statement  unloads (closes) the dialog box after the work is finished.

CHAPTER 16  UserForm Basics    269

Creating a macro to display the dialog box

You’re almost finished with this project. The only thing missing is a way to dis-

play the dialog box. Follow these steps to create the procedure that makes the dialog box appear:

1. In the VBE window, choose Insert  ➪ Module.

The VBE adds an empty VBA module (named Module1) to the project.

2. Enter the following code:

Sub ChangeCase()

If TypeName(Selection) = "Range" Then

UserForm1.Show

Else

MsgBox "Select a range.", vbCritical

End If

End Sub

This procedure is pretty simple. It checks to make sure that a range is selected. If so, the dialog box is displayed (using the Show method). The user then interacts

with the dialog box, and the code stored in the UserForm’s Code pane is executed.

If a range is not selected, the user sees a MsgBox with the text Select a range.

Making the macro available

At this point, everything should be working properly. But you still need an easy

way to execute the macro. Assign a shortcut key (Ctrl+Shift+C) that executes the

ChangeCase macro by following these steps:

1. Activate the Excel window by pressing Alt+F11.

2. Choose Developer  ➪ Code  ➪ Macros or press Alt+F8.

3. In the Macros dialog box, select the ChangeCase macro.

4. Click the Options button.

Excel displays its Macro Options dialog box.

5. Enter C for the Shortcut key (see Figure  16-6).

6. Enter a description of the macro in the Description field.

7. Click OK.

8. Click Cancel when you return to the Macro dialog box.

270    PART 4  Communicating with Your Users

FIGURE 16-6:

Assign a shortcut

key to execute

the ChangeCase

macro.

After you perform this operation, pressing Ctrl+Shift+C executes the ChangeCase

macro, which displays the UserForm if a range is selected.

You can also make this macro available from the Quick Access toolbar. Right-click

the Quick Access toolbar and choose Customize Quick Access Toolbar. The Excel

Options dialog box appears, and the ChangeCase macro is listed below Macros (see

Figure 16-7).

FIGURE 16-7:

Adding the

ChangeChase

macro to the

Quick Access

toolbar.

CHAPTER 16  UserForm Basics    271

Testing the macro

Finally, you need to test the macro and dialog box to make sure they work properly, as follows:

1. Activate a worksheet (any worksheet in any workbook).

2. Select some cells that contain text.

You can even select entire rows or columns.

3. Press Ctrl+Shift+C.

The UserForm appears. Figure 16-8 shows how it should look.

4. Make your choice, and click OK.

If you did everything correctly, the macro makes the specified change to the

text in the selected cells.

FIGURE 16-8:

The UserForm is

in action.

If you test this procedure when only one cell is selected, you’ll find that  all the cells on the worksheet are processed. That behavior is a byproduct of using the SpecialCells method. If you prefer to be able to process just one cell, change

the first block of code to this:

If Selection.Count = 1 Then

Set WorkRange = Selection

Else

Set WorkRange = Selection.SpecialCells _

(xlCellTypeConstants, xlCellTypeConstants)

End If

272    PART 4  Communicating with Your Users

Figure 16-9 shows the worksheet after converting the text to uppercase. Notice

that the formula in cell B16 and the date in cell B17 were not changed. The macro

works only with cells that contain text.

FIGURE 16-9:

The text has been

converted to

uppercase.

As long as the workbook is open, you can execute the macro from any other workbook. If you close the workbook that contains your macro, Ctrl+Shift+C no

longer has any function.

If the macro doesn’t work properly, double-check the preceding steps to locate

and correct the error. Don’t be alarmed; debugging is a normal part of developing

macros. As a last resort, download the completed workbook from this book’s website and try to figure out where you went wrong.

CHAPTER 16  UserForm Basics    273

IN THIS CHAPTER

» Understanding each type of dialog

box control

» Changing each control’s properties

» Manipulating dialog box controls in

your UserForm object

Chapter 17

Using UserForm Controls

A user responds to a custom dialog box (also known as a  UserForm ) by using the various controls (buttons, edit boxes, option buttons, and so on) that


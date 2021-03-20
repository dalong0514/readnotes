dures, and make them part of your Excel interface. Best of all, you can

share these packages with others so that they get the benefit of your VBA prowess.

In this chapter, you explore how to create add-ins by using only the tools built

into Excel.

Okay . . . So What’s an Add-In?

Glad you asked. An Excel  add-in is something you add to enhance Excel’s functionality. Some add-ins provide new worksheet functions you can use in formulas;

other add-ins provide new commands or utilities. If the add-in is designed prop-

erly, the new features blend in well with the original interface so they appear to be part of the program.

Excel ships with several add-ins, including the Analysis ToolPak and Solver. You

can also get Excel add-ins from third-party suppliers or as shareware.

Any knowledgeable user can create add-ins, but VBA programming skills are

required. An Excel add-in is basically a different form of an XLSM workbook file.

CHAPTER 21  Creating Excel Add-Ins    355

More specifically, an add-in is a normal XLSM workbook with the following differences:

» The IsAddin property of the Workbook object is True.

» The workbook window is hidden and can’t be unhidden by choosing View ➪

Window ➪ Unhide.

» The workbook isn’t a member of the Workbooks collection. Rather, it’s in the AddIns collection.

You can convert any workbook file to an add-in, but not all workbooks are good

candidates. Because add-ins are always hidden, you can’t display worksheets or

chart sheets contained in an add-in. However, you can access an add-in’s VBA Sub

and Function procedures and display dialog boxes contained on UserForms.

Excel add-ins usually have an XLAM file extension to distinguish them from XLSM worksheet files. Add-ins from pre-2007 versions of Excel have an XLA extension.

Why Create Add-Ins?

You might decide to convert your Excel application to an add-in for any of the

following reasons:

» Make it more difficult to access your code.  When you distribute an application as an add-in (and you protect its VBA project), casual users can’t view the

sheets in the workbook. If you use proprietary techniques in your VBA code,

you can make it more difficult for others to copy the code. Excel’s protection

features aren’t perfect, though, and password-cracking utilities are available.

» Avoid confusion.  If a user loads your application as an add-in, the file is invisible and therefore less likely to confuse novice users or get in the way.

Unlike a hidden workbook, the contents of an add-in can’t be revealed.

» Simplify access to worksheet functions.  Custom worksheet functions that

you store in an add-in don’t require the workbook name qualifier. For

example, if you store a custom function named MOVAVG in a workbook

named NEWFUNC.XLSM, you must use syntax like the following to use this

function in a different workbook:

=NEWFUNC.XLSM!MOVAVG(A1:A50)

356    PART 5  Putting It All Together

But if this function is stored in an add-in file that’s open, you can use much simpler syntax because you don’t need to include the file reference:

=MOVAVG(A1:A50)

» Provide easier access for users.  After you identify the location of your

add-in, it appears in the Add-Ins dialog box, with a friendly name and a

description of what it does. The user can easily enable or disable your add-in.

» Gain better control over loading.  Add-ins can be opened automatically

when Excel starts, regardless of the directory in which they’re stored.

» Avoid displaying prompts when unloading.  When an add-in is closed, the

user never sees the dialog box prompt asking whether to save changes in

the file.

Working with Add-Ins

You load and unload add-ins by using the Add-Ins dialog box. To display this

dialog box, choose File ➪ Options ➪ Add-Ins. Then select Excel Add-Ins from the

drop-down list at the bottom of this dialog box and click Go. Or take the fast track and choose Developer ➪ Add-Ins ➪ Add-Ins. But the easiest method is to just press

Alt+TI (the old Excel 2003 keyboard shortcut).

Any of these methods displays the Add-Ins dialog box, shown in Figure 21-1. The

list box contains the names of all add-ins that Excel knows about. In this list,

check marks identify any currently open add-ins. You can open and close add-ins

from the Add-Ins dialog box by selecting or deselecting the check boxes.

To add a new add-in to the list, click Browse and then locate the XLAM file.

You can also open most add-in files (as though they were workbook files) by choosing File ➪ Open ➪ Browse. An add-in opened in this manner doesn’t appear in

the Add-Ins dialog box. In addition, if you open the add-in by choosing the Open

command, you can’t close it by choosing File ➪ Close. You can remove the add-in

only by exiting and restarting Excel or by writing a macro to close the add-in.

When you open an add-in, you may or may not notice anything different. In many

cases, however, the Ribbon changes in some way; Excel displays a new tab or one

or more new groups on an existing tab. For example, opening the Analysis ToolPak

add-in gives you a new item on the Data tab: Analysis ➪ Data Analysis. If the add-in contains only custom worksheet functions, the new functions appear in the Insert

Function dialog box, and you see no change in Excel’s user interface.

CHAPTER 21  Creating Excel Add-Ins    357

FIGURE 21-1:

The Add-Ins

dialog box lists

all the add-ins

known to Excel.

Understanding Add-In Basics

Although you can convert any workbook to an add-in, not all workbooks benefit

from this conversion. A workbook with no macros makes a useless add-in. In fact,

the only types of workbooks that benefit from being converted to an add-in are

those with macros. For example, a workbook that consists of general-purpose

macros (Sub and Function procedures) makes an ideal add-in.

Creating an add-in isn’t difficult, but it does require a bit of extra work. Follow

these steps to create an add-in from a normal workbook file:

1. Develop your application, and make sure that everything works properly.

Don’t forget to include a method for executing the macro or macros. You might

want to define a shortcut key or customize the user interface in some way

(see Chapter 19). If the add-in consists only of functions, there’s no need to

include a method to execute them because they appear in the Insert Function

dialog box.

2. Test the application by executing it when a  different workbook is active.

Doing so simulates the application’s behavior when it’s used as an add-in

because an add-in is never the active workbook.

358    PART 5  Putting It All Together

3. Activate the VBE and select the workbook in the Project window; choose  Tools  ➪  VBAProject Properties and click the Protection tab; select the Lock  Project for Viewing check box and enter a password (twice); then click OK.

This step is necessary only if you want to prevent others from viewing or

modifying your macros or UserForms.

4. Back in Excel, choose File  ➪ Info, and select Show All Properties at the  bottom of the right panel.

Excel expands the list of properties displayed.

5. Enter a brief descriptive title in the Title field and a longer description in  the Comments field.

Steps 4 and 5 aren’t required but make the add-in easier to use, because the

descriptions you enter appear in the Add-Ins dialog box when your add-in is

selected.

6. Still in Backstage, click Save As in the left pane.

7. Click Browse on the Save As screen. In the Save As dialog box, select Excel

Add-in (*.xlam) from the Save as Type drop-down list.

8. Specify the folder that will store the add-in.

Excel proposes its default add-ins folder (named AddIns), but you can save the

file in any folder you like.

9. Click Save.

A copy of your workbook is converted to an add-in and saved with an XLAM exten-

sion. Your original workbook remains open.

Looking at an Add-In Example

This section discusses the basic steps involved in creating a useful add-in.

The example is based on the Change Case text conversion utility described in Chapter 16.

The XLSM version of this example is available at this book’s website. You can create an add-in from this workbook.

Setting up the workbook

The workbook consists of one blank worksheet, a VBA module, and a UserForm.

Chapter 19 shows how to implement code that adds a new item to the Cell shortcut

menu.

CHAPTER 21  Creating Excel Add-Ins    359

The original version of the utility includes options for uppercase, lowercase, and

proper case. The add-in version includes two options to the UserForm so it has the

same options as the built-in tool in Microsoft Word:

» Sentence Case: Makes the first letter uppercase and all other letters

lowercase.

» Toggle Case: All uppercase characters are converted to lowercase, and vice

versa.

Figure 21-2 shows UserForm1. The five OptionButton controls are inside a Frame

control. In addition, the UserForm has a Cancel button (named CancelButton) and

an OK button (named OKButton).

FIGURE 21-2:

The UserForm

for the Change

Case add-in.

The code executed when the Cancel button is clicked is very simple. This proce-

dure unloads the UserForm with no action:

Private Sub CancelButton_Click()

Unload UserForm1

End Sub

The code that’s executed when the OK button is clicked follows. This code does all

the work:

Private Sub OKButton_Click()

Dim TextCells As Range

Dim cell As Range

Dim Text As String

Dim i As Long

'  Create an object with just text constants

On Error Resume Next

Set TextCells = Selection.SpecialCells(xlConstants, xlTextValues)

360    PART 5  Putting It All Together

' Turn off screen updating

Application.ScreenUpdating = False

'  Loop through the cells

For Each cell In TextCells

Text = cell.Value

Select Case True

Case OptionLower 'lowercase

cell.Value = LCase(cell.Value)

Case OptionUpper 'UPPERCASE

cell.Value = UCase(cell.Value)

Case OptionProper 'Proper Case

cell.Value = WorksheetFunction.Proper(cell.Value)

Case OptionSentence 'Sentence case

Text = UCase(Left(cell.Value, 1))

Text = Text & LCase(Mid(cell.Value, 2, Len(cell.Value)))

cell.Value = Text

Case OptionToggle 'tOGGLE CASE

For i = 1 To Len(Text)

If Mid(Text, i, 1) Like "[A-Z]" Then

Mid(Text, i, 1) = LCase(Mid(Text, i, 1))

Else

Mid(Text, i, 1) = UCase(Mid(Text, i, 1))

End If

Next i

cell.Value = Text

End Select

Next

'  Unload the dialog box

Unload UserForm1

End Sub

In addition to the two new options, this version of the Change Case utility differs

from the version in Chapter 16 in two other ways:

» The SpecialCells method creates an object variable that consists of the cells in the selection that contain a text constant (not a formula). This technique

makes the routine run a bit faster if the selection contains many formula cells.

See Chapter 14 for more information on this technique.

» Because of the Change Case menu item to the Row and the Column shortcut

menus, you can now execute the utility by right-clicking a range selection, a

complete row selection, or a complete column selection. Each of these actions

displays the Change Case item on the shortcut menu.

CHAPTER 21  Creating Excel Add-Ins    361

Testing the workbook

Test the add-in before converting this workbook. To simulate what happens when

the workbook is an add-in, you should test the workbook when a different work-

book is active. Because an add-in is never the active sheet or workbook, testing it

when a different workbook is open may help you identify some potential errors.

1. Open a new workbook and enter information in some cells.

For testing purposes, enter various types of information, including text, values,

and formulas. Or just open an existing workbook and use it for your tests.

Remember that any changes to the workbook cannot be undone, so you may

want to use a copy.

2. Select one or more cells (or entire rows and columns).

3. Execute the ChangeCase macro by choosing the new Change Case

command from your Cell (or Row or Column) shortcut menu.

If the Change Case command doesn’t appear on your shortcut menu, the most

likely reason is that you didn’t enable macros when you opened the change case.

xlsm workbook. Close the workbook and then reopen it — and make sure that you

enable macros.

Adding descriptive information

Although not required, it’s considered to be a best practice to enter a description

of your add-in. Follow these steps to add a description:

1. Activate the change case.xlsm workbook.

2. Choose File  ➪ Info, and click Show All Properties at the bottom right.

Excel expands the Properties list.

3. Enter a title for the add-in in the Title field.

This text appears in the list of add-ins in the Add-Ins dialog box. For this

example, enter Change Case.

4. In the Comments field, enter a description.

This information appears at the bottom of the Add-Ins dialog box when the

add-in is selected. For this example, enter Changes the case of text in

selected cells.  Access this utility by using the shortcut menu.

Figure 21-3 shows the Properties section with the Title and Comments fields filled out.

362    PART 5  Putting It All Together

FIGURE 21-3:

Use the

Properties

section to enter

descriptive

information

about your

add-in.

Protecting the VBA code

If you want to add a password to prevent others from viewing the VBA code, follow

these steps:

1. Activate the VBE, and select the change case.xlsm workbook in the

Project window.

2. Choose Tools  ➪ VBAProject Properties, and click the Protection tab on the  dialog box that appears.

3. Select the Lock Project for Viewing check box, and enter a password

(twice).

4. Click OK.

5. Save the workbook by choosing File  ➪ Save in the VBE or by going back to  the Excel window and choosing File  ➪ Save.

Creating the add-in

At this point, you’ve tested the change case.xlsm file, and it’s working correctly.

The next step is creating the add-in. Follow these steps:

1. If needed, reactivate Excel.

2. Activate the change case.xlsm workbook, and choose File  ➪ Save

As  ➪ Browse.

Excel displays its Save As dialog box.

3. From the Save as Type drop-down menu, choose Add-In (*.xlam).

4. Specify the location, and click Save.

A new add-in file (with an .xlam extension) is created, and the original XLSM

version remains open.

CHAPTER 21  Creating Excel Add-Ins    363

Opening the add-in

To avoid confusion, close the XLSM workbook before opening the add-in that you

created from that workbook.

Open the add-in by following these steps:

1. Choose Developer  ➪ Add-Ins  ➪ Add-Ins (or press Alt+TI).

Excel displays the Add-Ins dialog box.

2. Click the Browse button.

3. Locate and select the add-in you just created.

4. Click OK to close the Browse dialog box.

After you find your new add-in, the Add-Ins dialog box lists the add-in.

As shown in Figure 21-4, the Add-Ins dialog box also displays the descriptive

information you provided in the Document Properties panel.

5. Make sure that your new add-in is selected in the Add-Ins dialog box.

6. Click OK to close the dialog box.

Excel opens the add-in. Now you can use it with all your workbooks. As long as

it remains selected in the Add-Ins dialog box, the add-in opens every time you

start Excel.

FIGURE 21-4:

The Add-Ins

dialog box has

the new add-in

selected.

Distributing the add-in

If you’re in a generous mood, you can distribute this add-in to other Excel users

simply by giving them a copy of the XLAM file. (They don’t need the XLSM

version.) When they open the add-in, the new Change Case command appears on

the shortcut menu when they select a range, one or more rows, or one or more

364    PART 5  Putting It All Together

columns. If you lock the VBA project with a password, others cannot view your

macro code unless they know the password.

Modifying the add-in

An add-in can be edited just like any other workbook. You can edit the XLAM file

directly (you don’t need to work with the original XLSM version) by following these steps:

1. Open your XLAM file, if it’s not already open.

2. Activate the VBE.

3. Double-click the project’s name in the Project window.

If you protected the code, you’re prompted for the password.

4. Enter your password, and click OK.

5. Make your changes to the code.

6. Save the file by choosing File  ➪ Save.

If you create an add-in that stores information in a worksheet, you must set the

workbook’s IsAddIn property to False to view the workbook. You do this in the

Properties window when the ThisWorkbook object is selected (see Figure 21-5).

After you’ve made your changes to the workbook, make sure that you set the

IsAddIn property back to True before you save the file.

FIGURE 21-5:

Making an add-in

not an add-in.

CHAPTER 21  Creating Excel Add-Ins    365

6The Part of Tens

IN THIS PART . . .

Discover tips on using the VBE.

Expand your knowledge with Excel resources.

Find out what you should and shouldn’t do in Excel VBA.

IN THIS CHAPTER

» Applying block comments

» Copying multiple lines of code at once

» Jumping between modules and

procedures

» Teleporting to your functions

» Staying in the right procedure

» Stepping through your code

» Stepping to a specific line in

your code

» Stopping your code at a predefined

point

» Seeing the beginning and end of

variable values

» Turning off auto syntax check

Chapter 22

Ten Handy Visual Basic

Editor Tips


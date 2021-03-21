# 0601. Using the Excel

In This Chapter: 1) Recording your actions by using the Excel built-in macro recorder. 2) Understanding the types of macros you can record. 3) Setting the appropriate options for macro recording. 4) Evaluating the efficiency of recorded macros.

Macro Recorder

Y  ou can use two methods to create an Excel macro:

» Record it by using the Excel macro recorder.


» Write it manually.

This chapter deals specifically with the ins and outs of using the Excel macro recorder. Recording a macro isn't always the best approach, and some macros simply can't be recorded, no matter how hard you try. You'll see, however, that

the Excel macro recorder is very useful. Even if your recorded macro isn't quite

what you want, the macro recorder can almost always lead you in the right direction.

CHAPTER 6  Using the Excel Macro Recorder    79

Recording Basics

You take the following basic steps when recording a macro.

1. Determine what you want the macro to do.

2. Get things set up properly.

This step determines how well your macro works.

3. Determine whether you want cell references in your macro to be relative

or absolute.

4. Click the Record Macro button on the left side of the status bar

(or choose Developer ➪ Code ➪ Record Macro).

Excel displays its Record Macro dialog box.

5. Enter a name, shortcut key, macro location, and description.

Each of these items — with the exception of the name — is optional.

6. Click OK in the Record Macro dialog box.

Excel automatically inserts a VBA module in the workbook specified in the

Store Macro In box. From this point, Excel converts your actions to VBA code.

It also displays a square Stop Recording button on your status bar.

7. Perform the actions you want to record by using the mouse or the

keyboard.

8. When you finish, click the Stop Recording button on the status bar

(or choose Developer ➪ Code ➪ Stop Recording).

Excel stops recording your actions.

9. Test the macro to make sure it works correctly.

10. (Optional) Clean up the code by removing extraneous statements or

add some comments to your code to explain what it does.

The macro recorder is best suited for simple, straightforward macros. For example,

you may want a macro that applies formatting to a selected range of cells or that

sets up row and column headings for a new worksheet.

The macro recorder is for Sub procedures only. You can't use the macro recorder

to create Function procedures.

You may also find the macro recorder helpful for developing more complex

macros. That is to say, you can record some actions and then copy the recorded

code into another, more complex macro. In most cases, you need to edit the recorded code and add some new VBA statements.

80    PART 2  How VBA Works with Excel

The macro recorder  cannot generate code for any of the following tasks, which are described later in the book:

» Performing any type of repetitive looping

» Performing any type of conditional actions (using an If-Then statement)

» Assigning values to variables

» Specifying data types

» Displaying pop-up messages

» Displaying custom dialog boxes

The macro recorder's limited capability certainly doesn't diminish its importance.

Recording your actions is perhaps the best way to master VBA .  When in doubt, try recording. Although the result may not be exactly what you want, viewing the recorded code may reveal some objects, properties, and methods that you weren't

aware of and steer you in the right direction.

Preparing to Record

Before you take the big step and turn on the macro recorder, spend a minute or

two thinking about what you're going to do. You record a macro so that Excel can

automatically repeat the actions you record, so you'll want those actions to be accurate.

Ultimately, the success of a recorded macro depends on five factors:

» How the workbook is set up while you record the macro

» What is selected when you start recording

» Whether you use absolute or relative recording mode

» The accuracy of your recorded actions

» The context in which you play back the recorded macro

The importance of these factors becomes more clear as you go through the recording process.

CHAPTER 6  Using the Excel Macro Recorder    81

Relative or Absolute?

When recording your actions, Excel normally records absolute references to cells.

(This is the default recording mode.) But quite often, this is the  wrong recording mode. If you use absolute recording mode, Excel records actual cell references.

If you use relative recording, Excel records  relative references to cells. Keep reading to see the difference.

Recording in absolute mode

Open a new workbook and follow these steps to record a simple macro in absolute

mode. This macro simply enters three month names in a worksheet:

1. Make sure that the Developer ➪ Code ➪ Use Relative References button is

not highlighted and then choose Developer ➪ Code ➪ Record Macro.

2. Type Absolute as the name for this macro.

3. Click OK to begin recording.

4. Activate cell B1, and type Jan in that cell.

5. Move to cell C1, and type Feb.

6. Move to cell D1, and type Mar.

7. Click cell B1 to activate it again.

8. Stop the macro recorder.

9. Press Alt+F11 to activate the VBE.

10. Examine the Module1 module.

Excel generates the following code:

Sub Absolute()

'

' Absolute Macro

'

Range("B1").Select

ActiveCell.FormulaR1C1 = "Jan"

Range("C1").Select

ActiveCell.FormulaR1C1 = "Feb"

Range("D1").Select

82    PART 2  How VBA Works with Excel

ActiveCell.FormulaR1C1 = "Mar"

Range("B1").Select

End Sub

When executed, this macro selects cell B1 and inserts the three month names

into the range B1:D1. Then the macro reactivates cell B1.

These same actions occur regardless of which cell is active when you execute the

macro. A macro recorded by using absolute references always produces the same

results when it's executed. In this case, the macro always enters the names of the first three months in the range B1:D1 on the active worksheet.

Recording in relative mode

In some cases, you want your recorded macro to work with cell locations in a relative manner. You may want the macro to start entering the month names in the active cell. In such a case, you need to use relative recording.

You can change the manner in which Excel records your actions by clicking the

Use Relative References button in the Code group of the Developer tab. This button

is a toggle button. When the button appears highlighted in a different color, the

recording mode is relative. When the button appears normally, you're recording in

absolute mode.

You can change the recording method at any time, even in the middle of recording.

To see how relative mode recording works, delete the contents of range B1:D1 and

then perform the following steps:

1. Activate cell B1.

2. Choose Developer ➪ Code ➪ Record Macro.

3. Name this macro Relative.

4. Click OK to begin recording.

5. Click the Use Relative References button to change the recording mode

to relative.

When you click this button, it changes to a different color from the rest of the

ribbon.

6. Type Jan in cell B1.

7. Move to cell C1, and type Feb.

CHAPTER 6  Using the Excel Macro Recorder    83

8. Move to cell D1, and type Mar.

9. Select cell B1.

10. Stop the macro recorder.

Notice that this procedure differs slightly from the previous example. In this example, you activate the beginning cell  before  you start recording. This is an important step when you record macros that use the active cell as a base.

This macro always starts entering text in the active cell. Try it. Move the cell pointer to any cell and then execute the Relative macro. The month names are

always entered beginning at the active cell.

With the recording mode set to relative, the code that Excel generates is quite different from the code generated in absolute mode:

Sub Relative()

'

' Relative Macro

'

ActiveCell.FormulaR1C1 = "Jan"

ActiveCell.Offset(0, 1).Range("A1").Select

ActiveCell.FormulaR1C1 = "Feb"

ActiveCell.Offset(0, 1).Range("A1").Select

ActiveCell.FormulaR1C1 = "Mar"

ActiveCell.Offset(0, -2).Range("A1").Select

End Sub

To test this macro, activate any cell except B1. The month names are entered in

three cells, beginning with the cell that you activated.

Notice that the code generated by the macro recorder refers to cell A1. This may

seem strange because you never used cell A1 during the recording of the macro.

This is simply a byproduct of the way the macro recorder works. (This is discussed

in more detail in Chapter 8, where you explore the Offset property.)

What Gets Recorded?

When you turn on the macro recorder, Excel converts your mouse and keyboard

actions to valid VBA code. The best way to understand the process is to watch the

macro recorder in action. (See Figure 6-1.)

84    PART 2  How VBA Works with Excel

FIGURE 6-1:

A convenient

window

arrangement for

watching the

macro recorder

do its thing.

Follow these steps:

1. Start with a blank workbook.

2. Make sure that the Excel window is not maximized.

3. Press Alt+F11 to activate the VBE (and make sure that  this program  window is not maximized).

4. Resize and arrange the Excel window and the VBE window so that both

are visible.

For best results, position the Excel window above the VBE window and

minimize any other applications that are running.

5. Activate Excel, and choose Developer ➪ Code ➪ Record Macro.

6. Click OK to start the macro recorder.

Excel inserts a new module (named Module1) and starts recording in that

module.

7. Activate the VBE program window.

8. In the Project Explorer window, double-click Module1 to display that

module in the Code window.

Jump back to Excel and play around for a while. Choose various Excel commands

and watch the code being generated in the VBE window. Select cells, enter data,

CHAPTER 6  Using the Excel Macro Recorder    85

format cells, use the Ribbon commands, create a chart, change column widths,

manipulate graphics objects, and so on — go crazy! You'll be enlightened as you

watch Excel spit out the VBA code before your very eyes.

If you happen to have a system with dual monitors, you might find it helpful to

keep Excel on one monitor and the VBE window on the other one.

Recording Options

When recording your actions to create VBA code, you have several options. Recall

that Developer ➪ Code ➪ Record Macro displays the Record Macro dialog box before

recording begins, as shown in Figure 6-2.

FIGURE 6-2:

The Record

Macro dialog

box provides

several options.

The Record Macro dialog box allows you to specify a few aspects of your macro.

The following sections dive into these options.

Macro name

You can enter a name for the Sub procedure that you're recording. By default, Excel uses the names Macro1, Macro2, and so on for each macro you record. Don't

worry if you don't give your macro a friendly name in Record Macro dialog box.

You can always give it a more descriptive name later by editing the recorded code

in the VBE.

86    PART 2  How VBA Works with Excel

Shortcut key

The Shortcut key option allows you to execute the macro by pressing a shortcut

key combination. For example, if you enter w (lowercase), you can execute the macro by pressing Ctrl+W. If you enter  W  (uppercase), the macro comes alive when you press Ctrl+Shift+W.

You can add or change a shortcut key at any time, so there's no real reason to set

this option when recording a macro. For instructions on assigning a shortcut key

to an existing macro, see Chapter 5.

Store Macro In option

The Store Macro In option tells Excel where to store the macro that it's recording.

By default, Excel puts the recorded macro in a module in the active workbook. If

you prefer, you can record it in a new workbook (Excel opens a blank workbook)

or in your Personal Macro Workbook.

Your Personal Macro Workbook is a hidden workbook that opens automatically

when Excel starts. This is a good place to store macros that you'll use with mul-

tiple workbooks. The Personal Macro Workbook is named PERSONAL.XLSB. This

file doesn't exist until you specify it as the location for a recorded macro. If you've made any changes to this file, Excel prompts you to save it when you exit.

Description

If you'd like to add some descriptive comments to your macro, enter it in the Description box. You can put anything you like here, or nothing at all.

Is This Thing Efficient?

You might think that recording a macro would generate some award-winning VBA

code — better than you could ever write manually. Think again. Because the macro

recorder has to be generic enough to record virtually every combination of actions,

it often generates extraneous code that works, but is less than efficient.

To demonstrate just how inefficient the macro recorder's code can be, try this:

1. Turn on the macro recorder.

2. Choose Page Layout ➪ Page Setup ➪ Orientation ➪ Landscape.

3. Turn off the macro recorder.

CHAPTER 6  Using the Excel Macro Recorder    87

To take a look at the macro, activate the Module1 sheet. This single (very simple) command generates the following code:

Sub Macro1()

Application.PrintCommunication = False

With ActiveSheet.PageSetup

.PrintTitleRows = ""

.PrintTitleColumns = ""

End With

Application.PrintCommunication = True

ActiveSheet.PageSetup.PrintArea = ""

Application.PrintCommunication = False

With ActiveSheet.PageSetup

.LeftHeader = ""

.CenterHeader = ""

.RightHeader = ""

.LeftFooter = ""

.CenterFooter = ""

.RightFooter = ""

.LeftMargin = Application.InchesToPoints(0.7)

.RightMargin = Application.InchesToPoints(0.7)

.TopMargin = Application.InchesToPoints(0.75)

.BottomMargin = Application.InchesToPoints(0.75)

.HeaderMargin = Application.InchesToPoints(0.3)

.FooterMargin = Application.InchesToPoints(0.3)

.PrintHeadings = False

.PrintGridlines = False

.PrintComments = xlPrintNoComments

.PrintQuality = 600

.CenterHorizontally = False

.CenterVertically = False

.Orientation = xlLandscape

.Draft = False

.PaperSize = xlPaperLetter

.FirstPageNumber = xlAutomatic

.Order = xlDownThenOver

.BlackAndWhite = False

.Zoom = 100

.PrintErrors = xlPrintErrorsDisplayed

.OddAndEvenPagesHeaderFooter = False

.DifferentFirstPageHeaderFooter = False

.ScaleWithDocHeaderFooter = True

88    PART 2  How VBA Works with Excel

.AlignMarginsHeaderFooter = True

.EvenPage.LeftHeader.Text = ""

.EvenPage.CenterHeader.Text = ""

.EvenPage.RightHeader.Text = ""

.EvenPage.LeftFooter.Text = ""

.EvenPage.CenterFooter.Text = ""

.EvenPage.RightFooter.Text = ""

.FirstPage.LeftHeader.Text = ""

.FirstPage.CenterHeader.Text = ""

.FirstPage.RightHeader.Text = ""

.FirstPage.LeftFooter.Text = ""

.FirstPage.CenterFooter.Text = ""

.FirstPage.RightFooter.Text = ""

End With

Application.PrintCommunication = True

End Sub

You may be surprised by the amount of code generated by this single command.

Although you changed only one print setting, Excel generated code that set many

other print-related properties.

This is a good example of macro-recording overkill. If you want a macro that just

switches the page setup to landscape mode, you can simplify this macro consider-

ably by deleting the extraneous code. This makes the macro a bit faster and a lot

easier to read. Here's how the macro looks after deleting the irrelevant lines:

Sub Macro1()

With ActiveSheet.PageSetup

.Orientation = xlLandscape

End With

End Sub

The only line necessary is the one that sets the Orientation property. Actually, you can simplify this macro even more because you don't really need the With-End

With construct (you find out more about this construct in Chapter 14):

Sub Macro1()

ActiveSheet.PageSetup.Orientation = xlLandscape

End Sub

In this case, the macro changes the Orientation property of the PageSetup object

on the active sheet. All other properties are unchanged. By the way, xlLandscape

CHAPTER 6  Using the Excel Macro Recorder    89

is a built-in constant that makes your code easier to read. This constant has a value of 2, so the following statement works exactly the same (but isn't as easy

to read):

ActiveSheet.PageSetup.Orientation = 2

Stay tuned for the built-in constants explanations in Chapter 7.

Rather than record this macro, you can enter it directly in a VBA module. To do so,

you have to know which objects, properties, and methods to use. Although the

recorded macro isn't all that great, by recording it, you realize that the PageSetup object is contained in a Worksheet object and that the PageSetup object has an

Orientation property. Armed with this knowledge and a quick trip to the Help system (and probably some experimentation), you can write the macro manually.

This chapter nearly sums it up when it comes to using the macro recorder. The

only thing missing is experience. Eventually, you discover which recorded

statements you can safely delete. Better yet, you discover how to modify a recorded

macro to make it more useful.

90    PART 2  How VBA Works with Excel

3Programming

Concepts

IN THIS PART . . .

Discover the essential elements of Excel programming:

variables, constants, data types, operators, arrays, and

so on.

Get acquainted with Range objects; you'll be glad

you did.

Find out why VBA functions (and also Excel worksheet

functions) are important.

Discover the essence of programming: decision-making

and looping.

See how to run code automatically when certain things

occur.

Find out about the different types of errors and why

error handling is important.

Know what to do when good code does bad things: Get

initiated into the bug extermination club.

IN THIS CHAPTER

» Knowing when, why, and how to use

comments in your code

» Using variables and constants

» Telling VBA what type of data you're

using

» Getting familiar with arrays

» Knowing why you may need to use

labels in your procedures

Chapter 7

Essential VBA Language

Elements

B ecause VBA is a real, live programming language, it uses many elements

common to all programming languages. In this chapter, you're introduced

to several of these elements: comments, variables, constants, data types,

arrays, and a few other goodies. If you've programmed with other languages,

some of this material will be familiar. If you're a programming newbie, it's time

to roll up your sleeves and get busy.

Using Comments in Your VBA Code

A  comment is the simplest type of VBA statement. Because VBA ignores these
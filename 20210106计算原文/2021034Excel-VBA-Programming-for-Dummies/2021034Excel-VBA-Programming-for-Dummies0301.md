# 0201. Jumping Right In

T he best way to get into a cold body of water is to jump right in — no sense

prolonging the agony. By wading through this chapter, you can get your feet

wet immediately but avoid getting in over your head.

By the time you reach the end of this chapter, you may start feeling better about

this Excel programming business, and you’ll be glad you took the plunge. This

chapter provides a step-by-step demonstration of how to develop a simple but

useful VBA macro.

First Things First

Before you can call yourself an Excel programmer, you must go through the initi-

ation rites. That means you need to make a small change so Excel will display a

new tab at the top of the screen: Developer. Getting Excel to display the Developer

tab is easy (and you only have to do it one time). Just follow these steps:

1. Right-click any part of the Ribbon and choose Customize the Ribbon from

the shortcut menu.

2. In the Customize Ribbon tab of the Excel Options dialog box, locate

Developer in the box on the right.

CHAPTER 2  Jumping Right In    17

3. Put a check mark next to Developer.

4. Click OK.

You’re back to Excel with a brand-new tab: Developer.

When you click the Developer tab, the Ribbon displays information that is of

interest to programmers (that’s you!). Figure 2-1 shows how the Ribbon looks when the Developer tab is selected in Excel 2019.

FIGURE 2-1:

The Developer

tab is normally

hidden, but it’s

easy to unhide.

What You’ll Be Doing

In this chapter, you create your first macro. The macro that you’re about to create

does this:

» Types your name in a cell

» Enters the current date and time in the cell below

» Formats both cells to display bold

» Changes the font size of both cells to 16 point

This macro won’t be winning any prizes in the Annual VBA Programmer’s

Competition, but everyone must start somewhere. The macro accomplishes all

these steps in a single action. As described in the following sections, you start by recording your actions as you go through these steps. Then you test the macro to

see whether it works. Finally, you edit the macro to add some finishing touches.

Ready?

Taking the First Steps

This section describes the steps you take prior to recording the macro. In other

words, you need to make a few preparations before the fun begins:

18    PART 1  Getting Started with Excel VBA Programming

1. Start Excel, if it’s not already running.

2. If necessary, create a new, empty workbook.

Pressing Ctrl+N is a quick favorite way to do that.

3. Click the Developer tab, and take a look at the Use Relative References

button in the Code group.

If the color of that button is different from the other buttons, you’re in good

shape. If the Use Relative References button is the same color as the other

buttons, you need to click it to enable this option.

You explore the Relative References button in Chapter 6. For now, just make sure

that the option is turned on. When it’s turned on, the Use Relative References but-

ton will be a different color.

Recording the Macro

Here comes the hands-on part. Follow these instructions carefully:

1. Select a cell.

Any cell will do.

2. Choose Developer  ➪ Code  ➪ Record Macro or click the macro recording  button on the status bar.

The Record Macro dialog box appears, as shown in Figure 2-2.

3. Enter a name for the macro.

Excel provides a default name (something like  Macro1 ), but it’s better to use a more descriptive name.  NameAndTime (with no spaces) is a good name for this

macro.

4. Click the Shortcut Key box, and enter Shift+N (for an uppercase N) as the

shortcut key.

Specifying a shortcut key is optional. If you do specify one, you can execute the

macro by pressing a key combination — in this case, Ctrl+Shift+N. Be aware

that if you assign a common shortcut key (for instance Ctrl+C), you lose the

normal functionality for that shortcut key; Excel will trigger your macro instead.

5. Make sure the Store Macro In setting is This Workbook.

6. You can enter some text in the Description box, if you like.

This step is optional. Some people like to describe what the macro does (or is

supposed to do).

CHAPTER 2  Jumping Right In    19

7. Click OK.

The Record Macro dialog box closes, and Excel’s macro recorder is turned on.

From this point, Excel monitors everything you do and converts it to VBA code.

8. Type your name in the active cell.

9. Move the cell pointer to the cell below and enter this formula:

=NOW()

The formula displays the current date and time.

10. Select the formula cell, and press Ctrl+C to copy that cell to the Clipboard.

11. Choose Home  ➪ Clipboard  ➪ Paste  ➪ Values (V).

This command converts the formula to its value.

12. With the date cell selected, press Shift+up arrow to select that cell and

the one above it (which contains your name).

13. Use the controls in the Home  ➪ Font group to change the formatting to

Bold and make the font size 16 point.

14. Choose Developer  ➪ Code  ➪ Stop Recording.

The macro recorder is turned off.

FIGURE 2-2:

The Record

Macro dialog box

appears when

you’re about to

record a macro.

Congratulations! You just created your first Excel VBA macro. You may want to

phone your mother and tell her the good news.

20    PART 1  Getting Started with Excel VBA Programming

Testing the Macro

Now you can try this macro and see whether it works properly. To test your macro,

move to an empty cell and press Ctrl+Shift+N (or whatever shortcut you assigned).

In a flash, Excel executes the macro. Your name and the current date and time are

displayed in large, bold letters.

Another way to execute the macro is to choose Developer ➪ Code ➪ Macros (or

press Alt+F8) to display the Macros dialog box. Select the macro from the list (in

this case, NameAndTime), and click Run. Make sure you select the cell that will

hold your name before executing the macro.

Examining the Macro

You’ve recorded a macro, and you’ve tested it. If you’re a curious type, you’re

probably wondering what this macro looks like. And you might even wonder

where it’s stored.

Remember when you started recording the macro? You indicated that Excel should

store the macro in This Workbook. The macro is stored in the workbook, but you

need to activate the Visual Basic Editor (VBE, for short) to see it.

Follow these steps to see the macro:

1. Choose Developer  ➪ Code  ➪ Visual Basic (or press Alt+F11).

The Visual Basic Editor program window appears, as shown in Figure 2-3. This

window is highly customizable, so your VBE window may look a bit different.

The VBE window contains several other windows and is probably very intimi-

dating. Don’t fret; you’ll get used to it.

2. In the VBE window, locate the window called Project.

The Project window (also known as the Project Explorer window) contains a list

of all workbooks and add-ins that are currently open. Each project is arranged

as a  tree and can be expanded (to show more information) or contracted (to

show less information).

The VBE uses quite a few different windows, any of which can be open or

closed. If a window isn’t immediately visible in the VBE, you can choose an

option from the View menu to display the window. For instance, if the Project

window is not visible, you can choose View ➪ Project Explorer (or press Ctrl+R)

CHAPTER 2  Jumping Right In    21

to display it. You can display any other VBE window in a similar manner. The

components of the VBE are covered in Chapter 3.

3. Select the project that corresponds to the workbook in which you

recorded the macro.

If you haven’t saved the workbook, the project is probably called VBAProject

(Book1).

4. Click the plus sign (+) to the left of the folder named Modules.

The tree expands to show Module1, which is the only module in the project.

5. Double-click Module1.

The VBA code in that module is displayed in a Code window (see Figure 2-3).

Your screen may not look exactly the same as Figure 2-3. The code that’s

recorded depends on the specific actions you made while recording the macro.

FIGURE 2-3:

The VBE displays

the VBA code in

Module1 of

Book1.

At this point, the macro probably looks like Greek to you. Don’t worry. Travel a

few chapters down the road, and all will be as clear as the view from Olympus.

The NameAndTime macro consists of several statements. Excel executes the

statements one by one, from top to bottom. A statement that’s preceded by an

apostrophe (’) is a comment. Comments are included only for your information

and are ignored by Excel. In other words, Excel skips right over comments.

22    PART 1  Getting Started with Excel VBA Programming

HEY, I DIDN’T RECORD THAT!

The macro recorder is like recording sound on a recorder. When you play back a recording and listen to your own voice, you invariably say,「I don’t sound like that.」And when you look at your recorded macro, you may see some actions that you didn’t think you

recorded.

When you recorded the NameAndTime example, you changed only the font size, yet the

recorded code shows all sorts of font-changing statements (Strikethrough, Superscript, Shadow, and so on). Don’t worry; it happens all the time. Excel often records lots of seemingly useless code. In later chapters, you find out how to remove the extra stuff from a recorded macro.

The first VBA statement (which begins with the word  Sub) identifies the macro as a Sub procedure and gives its name; you provided this name before you started

recording the macro. If you read through the code, you may be able to make sense

of some of it. You see your name, the formula you entered, and lots of additional

code that changes the font. The Sub procedure ends with the End Sub statement.

Modifying the Macro

As you might expect, you not only view your macro in the VBE, but can also change

it. Even though you probably have no idea what you’re doing at this point, these

changes are easy to make:

» Change the name that’s entered in the active cell. If you have a dog, use your dog’s name.

» Change the font name or size.

» See if you can figure out the appropriate location for this new statement that makes the cells italic:

Selection.Font.Italic = True

Working in a VBA code module is much like working in a word-processing docu-

ment (except there’s no word wrap, and you can’t format the text). On second

thought, it’s more like working in Windows Notepad. You can press Enter to start

a new line, and the familiar editing keys work as expected.

CHAPTER 2  Jumping Right In    23

After you’ve made your changes, jump back to Excel and try the revised macro to

see how it works. Just as you can press Alt+F11 in Excel to display the VBE, you can press Alt+F11 in the VBE to switch back to Excel.

Saving Workbooks That Contain Macros

If you store one or more macros in a workbook, the file must be saved as a macro-enabled  file type. In other words, the file must be saved with an XLSM

extension rather than the normal XLSX extension.

For example, when you save the workbook that contains your NameAndTime

macro, the file format in the Save As dialog box defaults to XLSX (a format that

cannot contain macros). Unless you change the file format to XLSM, Excel dis-

plays the warning shown in Figure 2-4. You need to click No and then choose Excel Macro-Enabled Workbook (*.xlsm) from the Save As Type drop-down list.

FIGURE 2-4:

If your workbook

contains macros,

and you attempt

to save it in a

macro-free file

format, Excel

warns you.

Understanding Macro Security

Macro security is a key feature in Excel. The reason is that VBA is a powerful

language — so powerful that it’s possible to create a macro that can do serious

damage to your computer. A macro can delete files, send information to other computers, and even destroy Windows so that you can’t even start your system.

The macro security features introduced in Excel 2007 were created to help prevent

these types of problems.

Figure 2-5 shows the Macro Settings section of the Trust Center dialog box. To

display this dialog box, choose Developer ➪ Code ➪ Macro Security.

24    PART 1  Getting Started with Excel VBA Programming

FIGURE 2-5:

The Macro

Settings

section of the

Trust Center

dialog box.

By default, Excel uses the Disable All Macros with Notification option. With this

setting in effect, if you open a workbook that contains macros (and the file is not

digitally「signed」or stored in a trusted location), Excel displays a warning like

the one in Figure 2-6. If you are certain that the workbook comes from a trusted

source, click Enable Macros, and the macros will be enabled.

FIGURE 2-6:

Excel’s warning

that the file to be

opened contains

macros.

You see the pop-up box in Figure 2-6 only when the VBE is open. Otherwise, Excel

displays an eye-catching Security Warning above the Formula bar, as shown in

Figure 2-7. If you know the workbook is safe, click the Enable Content button to

enable the macros. To use the workbook without macros, click the X to dismiss the

warning.

Excel remembers when you’ve designated a workbook to be safe. So the next time

you open it, you won’t see the Security Warning.

CHAPTER 2  Jumping Right In    25

FIGURE 2-7:

Excel’s warning

that the

workbook just

opened contains

macros. You see

this warning

when the VBE

isn’t open.

Perhaps the best way to handle macro security is to designate one or more folders

as  trusted locations.  All the workbooks in a trusted location are opened without a macro warning. You designate trusted folders in the Trusted Locations section of

the Trust Center dialog box.

If you want to find out what the other macro security settings imply, press F1

while the Macro Settings section of the Trust Center dialog box is in view. You get

a Help screen that describes the security settings.

Revealing More about the

NameAndTime Macro

By the time you finish this book, you should completely understand how the NameAndTime macro works — and you’ll be able to develop more sophisticated

macros. For now, this chapter ends with a few additional points about the macro:

» For this macro to work, its workbook must be open. If you close the workbook, the macro isn’t available so it can’t work (and its shortcut keys have no effect).

» As long as the workbook containing the macro is open, you can run the macro while any workbook is active. In other words, the macro’s own workbook

doesn’t have to be active.

» The macro isn’t「pro-quality」code. It will overwrite existing text with no warning — and its effects can’t be undone.

» Before you started recording the macro, you assigned it a new shortcut key.

This is just one of several ways to execute the macro. (You discover other

ways in Chapter 5.)

26    PART 1  Getting Started with Excel VBA Programming

» You can create this macro manually rather than record it. To do so, you need a good understanding of VBA. (Be patient; you’ll get there.)

» You can store this macro in your Personal Macro Workbook. If you do so, the macro is available automatically whenever you start Excel. (See Chapter 6 for

details about your Personal Macro Workbook.)

» You can also convert the workbook to an add-in file. (More about this in

Chapter 21.)

Congratulations. You’ve been initiated into the world of Excel programming.

(Sorry, there’s no secret handshake or decoder ring.)

CHAPTER 2  Jumping Right In    27

2How VBA Works

with Excel

IN THIS PART . . .

See how to access the important part of the Visual

Basic Editor.

Discover VBA code modules (where you store your

VBA code).

Get an overview of the Excel object model.

Discover a bit about two key concepts: object

properties and methods.

Find out the differences between Sub procedures and

Function procedures.

Get a crash course in using the Excel macro recorder.

IN THIS CHAPTER

» Understanding the Visual Basic Editor

» Discovering the Visual Basic Editor

parts

» Knowing what goes into a VBA

module

» Understanding three ways to get VBA

code into a module

» Customizing the VBA environment

Chapter 3

Working in the Visual

Basic Editor

A s a more experienced-than-average Excel user, you probably know a good


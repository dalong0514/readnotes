## 记忆时间

2021-04-22

## 目录

0101 What Is VBA?

0201 Jumping Right In

0301 Working in the Visual Basic Editor

0401 Introducing the Excel Object Model

0501 VBA Sub and Function

In This Part: 1) Get to know Visual Basic for Applications. 2) See examples of some of the things you can do with VBA. 3) Work through a real-live Excel programming session. 4) Get a handle on how Excel deals with macro security.

## 0101. What Is VBA?

In This Chapter: 1) Getting a conceptual overview of VBA. 2) Finding out what you can do with VBA. 3) Discovering the advantages and disadvantages of using VBA. 4) Getting the lowdown on what VBA is. 5) Staying Excel compatible.

If you're eager to jump into VBA programming, hold your horses. This chapter is completely devoid of any hands-on training material. It does, however, contain some essential background information that assists you in becoming an Excel programmer. In other words, this chapter paves the way for everything else that follows and gives you a feel for how Excel programming fits into the overall scheme of the universe. It's not as boring as you might think, so please try to resist the urge to jump to Chapter 2.

Okay, So What Is VBA?

VBA, which stands for Visual Basic for Applications, is a programming language developed by Microsoft — you know, the company that tries to get you to buy a new version of Windows every few years. Excel, along with the other members of Microsoft Office, includes the VBA language (at no extra charge). In a nutshell, VBA is the tool that people use to develop programs that control Excel.

Imagine an intelligent robot that knows all about Excel. This robot can read instructions, and it can also operate Excel very fast and accurately. When you want the robot to do something in Excel, you write a set of robot instructions by using special codes. Then you tell the robot to follow your instructions while you sit back and drink a glass of lemonade. That's kind of what VBA is all about — a code language for robots. Note, however, that Excel does not come with a robot or lemonade.

A Few Words About Terminology

Excel programming terminology can be a bit confusing. For example, VBA is a programming language, but it also serves as a macro language. In this context, a macro is a set of instructions Excel performs to imitate keystrokes and mouse actions. What do you call something written in VBA and executed in Excel? Is it a macro, or is it a program? Excel's Help system often refers to VBA procedures as macros, so that terminology is used in this book. But you can also call this stuff a program.

You'll see the term automate throughout this book. This term means that a series of steps are completed automatically. For example, if you write a macro that adds color to some cells, prints the worksheet, and then removes the color, you have automated those three steps.

By the way, macro doesn't stand for Messy And Confusing Repeated Operation. Rather, it comes from the Greek makros, which means large — which also describes your pay-check after you become an expert macro programmer.

### 1.1 What Can You Do with VBA?

You're probably aware that people use Excel for thousands of different tasks. Here are just a few examples: 1) Analyzing scientific data. 2) Budgeting and forecasting. 3) Creating invoices and other forms. 4) Developing charts from data. 5) Keeping lists of things such as customers' names, students' grades, or holiday gift ideas (a nice fruitcake would be lovely). 6) Yadda, yadda, yadda.

The list could go on and on, but you get the idea. The point is simply that Excel is used for a wide variety of tasks, and everyone reading this book has different needs and expectations regarding Excel. One thing virtually every reader has in common is the need to automate some aspect of Excel. That, dear reader, is what VBA is all about.

For example, you might create a VBA program to import some numbers and then format and print your month-end sales report. After developing and testing the program, you can execute the macro with a single command, causing Excel to automatically perform many time-consuming procedures. Rather than struggle through a tedious sequence of commands, you can click a button and then hop on over to Facebook and kill some time while your macro does the work.

The following sections briefly describe some common uses for VBA macros. One or two of these may push your button.

#### 1.1.1 Inserting a bunch of text

If you often need to enter your company name, address, and phone number in your worksheets, you can create a macro to do the typing for you. You can extend this concept as far as you like. For example, you might develop a macro that auto-matically enters a list of all salespeople who work for your company.

#### 1.1.2 Automating a task you perform frequently

Assume you're a sales manager and you need to prepare a month-end sales report to keep your boss happy. If the task is straightforward, you can develop a VBA program to do it for you. Your boss will be impressed by the consistently high quality of your reports, and you'll be promoted to a new job for which you are highly unqualified.

#### 1.1.3 Automating repetitive operations

If you need to perform the same action on, say, 12 different Excel workbooks, you can record a macro while you perform the task on the first workbook and then let the macro repeat your action on the other workbooks. The nice thing about this is that Excel never complains about being bored. Excel's macro recorder is similar to recording live action on a video recorder. But it doesn't require a camera, and the battery never needs to be recharged.

#### 1.1.4 Creating a custom command

Do you often issue the same sequence of Excel commands? If so, save yourself a few seconds by developing a macro that combines these commands into a single custom command, which you can execute with a single keystroke or button click.

You probably won't save that much time, but you'll probably be more accurate. And the guy in the next cubicle will be really impressed.

#### 1.1.5 Creating a custom button

You can customize your Quick Access toolbar with your own buttons that execute the macros you write. Office workers tend to be very impressed by buttons that perform magic. And if you really want to impress your fellow employees, you can even add new buttons to the Ribbon.

#### 1.1.6 Developing new worksheet functions

Although Excel includes hundreds of built-in functions (such as SUM and AVERAGE), you can create custom worksheet functions that can greatly simplify your formulas. You'll be surprised by how easy this is. (You can explore how to do this in Chapter 20.) Even better, the Insert Function dialog box displays your custom functions, making them appear built-in. Very snazzy stuff.

#### 1.1.7 Creating custom add-ins for Excel

You're probably familiar with some of the add-ins that ship with Excel. For example, the Analysis ToolPak is a popular add-in. You can use VBA to develop your own special-purpose add-ins.

### 1.2 Advantages and Disadvantages of VBA

This section outlines the good things about VBA — and also its darker side.

#### 1.2.1 VBA advantages

You can automate almost anything you do in Excel. To do so, you write instructions that Excel carries out. Automating a task by using VBA offers several advantages:

1 Excel always executes the task in exactly the same way. (In most cases, consistency is a good thing.)

2 Excel performs the task much faster than you can do it manually. (Unless, of course, you're Clark Kent.)

3 If you're a good macro programmer, Excel always performs the task with-out errors (which probably can't be said about you, no matter how careful you are).

4 If you set up things properly, someone who doesn't know anything about Excel can perform the task by running the macro.

5 You can do things in Excel that are otherwise impossible — which can make you a very popular person around the office.

6 For long, time-consuming tasks, you don't have to sit in front of your computer and get bored. Excel does the work while you hang out at the water cooler.

#### 1.2.2 VBA disadvantages

It's only fair to give equal time to the disadvantages (or potential disadvantages) of VBA:

1 You have to know how to write programs in VBA (but that's why you bought this book, right?). Fortunately, it's not as difficult as you might expect.

2 Other people who need to use your VBA programs must have their own copies of Excel. It would be nice if you could press a button that transforms your Excel/VBA application into a stand-alone program, but that isn't possible.(And probably never will be.)

3 Sometimes, things go wrong. In other words, you can't blindly assume that your VBA program will always work correctly under all circumstances. Welcome to the world of debugging and, if others are using your macros, technical support.

4 VBA is a moving target. As you know, Microsoft is continually upgrading Excel. Even though Microsoft puts great effort into compatibility between versions, you may discover that the VBA code you've written doesn't work properly with older versions or with a future version of Excel.

### 1.3 VBA in a Nutshell

Just to let you know what you're in for, here's a quick-and-dirty summary of what VBA is all about.

1 You perform actions in VBA by writing (or recording) code in a VBA module. You view and edit VBA modules by using the Visual Basic Editor (VBE).

2 A VBA module consists of Sub procedures. A Sub procedure has nothing to do with underwater vessels or tasty sandwiches. Rather, it's a chunk of computer code that performs some action on or with objects (discussed in a moment). The following example shows a simple Sub procedure called AddEmUp. This amazing program, when executed, displays the result of 1 plus 1:

```c
Sub AddEmUp()
  Sum = 1 + 1
  MsgBox "The answer is " & Sum
End Sub
```

A Sub procedure that doesn't perform properly is said to be substandard.

3 A VBA module can also have Function procedures. A Function procedure returns a single value. You can call it from another VBA procedure or even use it as a function in a worksheet formula. An example of a Function procedure (named AddTwo) follows. This Function accepts two numbers (called arguments) and returns the sum of those values:

```c
Function AddTwo(arg1, arg2)
  AddTwo = arg1 + arg2
End Function
```

A Function procedure that doesn't work correctly is said to be dysfunctional.

4 VBA manipulates objects. Excel provides dozens and dozens of objects that you can manipulate. Examples of objects include a workbook, a worksheet, a cell range, a chart, and a shape. You have many more objects at your disposal, and you can manipulate them by using VBA code.

5 Objects are arranged in a hierarchy. Objects can act as containers for other objects. At the top of the object hierarchy is Excel. Excel itself is an object called Application. The Application object contains other objects, such as Workbook objects and Add-In objects. The Workbook object can contain other objects, such as Worksheet objects and Chart objects. A Worksheet object can contain objects such as Range objects and PivotTable objects. The term object model refers to the arrangement of these objects. (Object-model mavens can find out more in Chapter 4.)

6 Objects of the same type form a collection. For example, the Worksheets collection consists of all the worksheets in a particular workbook. The Charts collection consists of all Chart objects in a workbook. Collections are themselves objects.

7 You refer to an object by specifying its position in the object hierarchy, using a dot (aka a period) as a separator. For example, you can refer to the workbook Book1.xlsx as 

```c
Application.Workbooks("Book1.xlsx")
```

This refers to the workbook Book1.xlsx in the Workbooks collection. The Workbooks collection is contained in the Application object (that is, Excel).

Extending this to another level, you can refer to Sheet1 in Book1.xlsx as

```c
Application.Workbooks("Book1.xlsx").Worksheets("Sheet1")
```

You can take this to still another level and refer to a specific cell (in this case, cell A1): 

```c
Application.Workbooks("Book1.xlsx").Worksheets("Sheet1").Range("A1")
```

8 If you omit specific references, Excel uses the active objects. If Book1.xlsx is the active workbook, you can simplify the preceding reference as follows:

```c
Worksheets("Sheet1").Range("A1")
```

If you know that Sheet1 is the active sheet, you can simplify the reference even more:

```c
Range("A1")
```

9 Objects have properties. You can think of a property as a setting for an object. For example, a Range object has such properties as Value and Address. A Chart object has such properties as HasTitle and Type. You can use VBA to determine object properties and also to change properties.

10 You refer to a property of an object by combining the object name with the property name, separated by a dot. For example, you can refer to the Value property in cell A1 on Sheet1 as follows:

```c
Worksheets("Sheet1").Range("A1").Value
```

11 You can assign values to variables. A variable is a named element that stores information. You can use variables in your VBA code to store such things as values, text, and property settings. To assign the value in cell A1 on Sheet1 to a variable called Interest, use the following VBA statement:

```c
Interest = Worksheets("Sheet1").Range("A1").Value
```

12 Objects have methods. A method is an action Excel performs with an object. For example, one of the methods for a Range object is ClearContents. This aptly named method clears the contents of the range.

13 You specify a method by combining the object with the method, separated by a dot. For example, the following statement clears the contents of cell A1:

```c
Worksheets("Sheet1").Range("A1").ClearContents
```

14 VBA includes all the constructs of modern programming languages, including variables, arrays, and looping. In other words, if you're willing to spend a little time learning the ropes, you can write code that does some incredible things.

Believe it or not, the preceding list pretty much describes VBA in a nutshell. Now you just have to find out the details. That's why this book has more pages.

### 1.4 Excel Compatibility

This book is written for the desktop versions of Excel 2016 and Excel 2019. If you don't have one of those versions, you run the risk of getting confused in a few places.

If you plan to distribute your Excel/VBA files to other users, it's vitally important that you understand which versions of Excel they use. People using older versions won't be able to take advantage of features introduced in later versions. For example, if you write VBA code that references cell XFD1048576 (the last cell in a work-book), those who use a version prior to Excel 2007 will get an error because those pre-Excel 2007 worksheets had only 65,536 rows and 255 columns (the last cell is IV65536).

Excel 2010 and later also have some new objects, methods, and properties. If you use these in your code, users with an older version of Excel will get an error when they run your macro — and you'll get the blame.

## 0201. Jumping Right In

In This Chapter: 1) Developing a useful VBA macro: A hands-on, step-by-step example. 2) Recording your actions by using Excel's macro recorder. 3) Examining and testing recorded code. 4) Changing a recorded macro. 5) Dealing with macro security issues

The best way to get into a cold body of water is to jump right in — no sense prolonging the agony. By wading through this chapter, you can get your feet wet immediately but avoid getting in over your head.

By the time you reach the end of this chapter, you may start feeling better about this Excel programming business, and you'll be glad you took the plunge. This chapter provides a step-by-step demonstration of how to develop a simple but useful VBA macro.

### 2.1 First Things First

Before you can call yourself an Excel programmer, you must go through the initiation rites. That means you need to make a small change so Excel will display a new tab at the top of the screen: Developer. Getting Excel to display the Developer tab is easy (and you only have to do it one time). Just follow these steps:

1 Right-click any part of the Ribbon and choose Customize the Ribbon from the shortcut menu.

2 In the Customize Ribbon tab of the Excel Options dialog box, locate Developer in the box on the right.

3 Put a check mark next to Developer.

4 Click OK.

You're back to Excel with a brand-new tab: Developer.

When you click the Developer tab, the Ribbon displays information that is of interest to programmers (that's you!). Figure 2-1 shows how the Ribbon looks when the Developer tab is selected in Excel 2019.

FIGURE 2-1: The Developer tab is normally hidden, but it's easy to unhide.

### 2.2 What You'll Be Doing

In this chapter, you create your first macro. The macro that you're about to create does this:

1 Types your name in a cell.

2 Enters the current date and time in the cell below.

3 Formats both cells to display bold.

4 Changes the font size of both cells to 16 point.

This macro won't be winning any prizes in the Annual VBA Programmer's Competition, but everyone must start somewhere. The macro accomplishes all these steps in a single action. As described in the following sections, you start by recording your actions as you go through these steps. Then you test the macro to see whether it works. Finally, you edit the macro to add some finishing touches.

Ready?

### 2.3 Taking the First Steps

This section describes the steps you take prior to recording the macro. In other words, you need to make a few preparations before the fun begins:

1 Start Excel, if it's not already running.

2 If necessary, create a new, empty workbook. Pressing Ctrl+N is a quick favorite way to do that.

3 Click the Developer tab, and take a look at the Use Relative References button in the Code group. If the color of that button is different from the other buttons, you're in good shape. If the Use Relative References button is the same color as the other buttons, you need to click it to enable this option.

You explore the Relative References button in Chapter 6. For now, just make sure that the option is turned on. When it's turned on, the Use Relative References button will be a different color.

### 2.4 Recording the Macro

1『开始录制宏了。（2021-03-21）』

Here comes the hands-on part. Follow these instructions carefully:

1 Select a cell. Any cell will do.

2 Choose Developer => Code => Record Macro or click the macro recording button on the status bar. The Record Macro dialog box appears, as shown in Figure 2-2.

3 Enter a name for the macro. Excel provides a default name (something like Macro1 ), but it's better to use a more descriptive name. NameAndTime (with no spaces) is a good name for this macro.

4 Click the Shortcut Key box, and enter Shift+N (for an uppercase N) as the shortcut key. Specifying a shortcut key is optional. If you do specify one, you can execute the macro by pressing a key combination — in this case, Ctrl+Shift+N. Be aware that if you assign a common shortcut key (for instance Ctrl+C), you lose the normal functionality for that shortcut key; Excel will trigger your macro instead.

5 Make sure the Store Macro In setting is This Workbook.

6 You can enter some text in the Description box, if you like. This step is optional. Some people like to describe what the macro does (or is supposed to do).

7 Click OK. The Record Macro dialog box closes, and Excel's macro recorder is turned on. From this point, Excel monitors everything you do and converts it to VBA code.

8 Type your name in the active cell.

9 Move the cell pointer to the cell below and enter this formula:

```c
=NOW()
```

The formula displays the current date and time.

10 Select the formula cell, and press Ctrl+C to copy that cell to the Clipboard.

11 Choose Home  => Clipboard => Paste => Values(V).

This command converts the formula to its value.

12 With the date cell selected, press Shift+up arrow to select that cell and the one above it (which contains your name).

13 Use the controls in the Home => Font group to change the formatting to Bold and make the font size 16 point.

14 Choose Developer => Code  => Stop Recording. The macro recorder is turned off.

Congratulations! You just created your first Excel VBA macro. You may want to phone your mother and tell her the good news.

1『看到这里突然意识到，有时候如果不知道如何用 VBA 代码实现某个功能，可以自己录制一个宏，然后去看宏的源码。（2021-03-21）』

### 2.5 Testing the Macro

Now you can try this macro and see whether it works properly. To test your macro, move to an empty cell and press Ctrl+Shift+N (or whatever shortcut you assigned).

In a flash, Excel executes the macro. Your name and the current date and time are displayed in large, bold letters. Another way to execute the macro is to choose Developer => Code => Macros (or press Alt+F8) to display the Macros dialog box. Select the macro from the list (in this case, NameAndTime), and click Run. Make sure you select the cell that will hold your name before executing the macro.

### 2.6 Examining the Macro

You've recorded a macro, and you've tested it. If you're a curious type, you're probably wondering what this macro looks like. And you might even wonder where it's stored.

Remember when you started recording the macro? You indicated that Excel should store the macro in This Workbook. The macro is stored in the workbook, but you need to activate the Visual Basic Editor (VBE, for short) to see it.

Follow these steps to see the macro:

1 Choose Developer => Code => Visual Basic (or press Alt+F11). The Visual Basic Editor program window appears, as shown in Figure 2-3. This window is highly customizable, so your VBE window may look a bit different. The VBE window contains several other windows and is probably very intimi-dating. Don't fret; you'll get used to it.

2 In the VBE window, locate the window called Project. The Project window (also known as the Project Explorer window) contains a list of all workbooks and add-ins that are currently open. Each project is arranged as a tree and can be expanded (to show more information) or contracted (to show less information).

The VBE uses quite a few different windows, any of which can be open or closed. If a window isn't immediately visible in the VBE, you can choose an option from the View menu to display the window. For instance, if the Project window is not visible, you can choose View => Project Explorer (or press Ctrl+R) to display it. You can display any other VBE window in a similar manner. The components of the VBE are covered in Chapter 3.

3 Select the project that corresponds to the workbook in which you recorded the macro. If you haven't saved the workbook, the project is probably called VBAProject(Book1).

4 Click the plus sign (+) to the left of the folder named Modules. The tree expands to show Module1, which is the only module in the project.

5 Double-click Module1. The VBA code in that module is displayed in a Code window (see Figure 2-3). Your screen may not look exactly the same as Figure 2-3. The code that's recorded depends on the specific actions you made while recording the macro.

FIGURE 2-3: The VBE displays the VBA code in Module1 of Book1.

At this point, the macro probably looks like Greek to you. Don't worry. Travel a few chapters down the road, and all will be as clear as the view from Olympus.

The NameAndTime macro consists of several statements. Excel executes the statements one by one, from top to bottom. A statement that's preceded by an apostrophe (') is a comment. Comments are included only for your information and are ignored by Excel. In other words, Excel skips right over comments.

HEY, I DIDN'T RECORD THAT!

The macro recorder is like recording sound on a recorder. When you play back a recording and listen to your own voice, you invariably say,「I don't sound like that.」And when you look at your recorded macro, you may see some actions that you didn't think you recorded.

When you recorded the NameAndTime example, you changed only the font size, yet the recorded code shows all sorts of font-changing statements (Strikethrough, Superscript, Shadow, and so on). Don't worry; it happens all the time. Excel often records lots of seemingly useless code. In later chapters, you find out how to remove the extra stuff from a recorded macro.

The first VBA statement (which begins with the word Sub) identifies the macro as a Sub procedure and gives its name; you provided this name before you started recording the macro. If you read through the code, you may be able to make sense of some of it. You see your name, the formula you entered, and lots of additional code that changes the font. The Sub procedure ends with the End Sub statement.

### 2.7 Modifying the Macro

As you might expect, you not only view your macro in the VBE, but can also change it. Even though you probably have no idea what you're doing at this point, these changes are easy to make:

1 Change the name that's entered in the active cell. If you have a dog, use your dog's name.

2 Change the font name or size.

3 See if you can figure out the appropriate location for this new statement that makes the cells italic:

```c
Selection.Font.Italic = True
```

Working in a VBA code module is much like working in a word-processing document (except there's no word wrap, and you can't format the text). On second thought, it's more like working in Windows Notepad. You can press Enter to start a new line, and the familiar editing keys work as expected.

After you've made your changes, jump back to Excel and try the revised macro to see how it works. Just as you can press Alt+F11 in Excel to display the VBE, you can press Alt+F11 in the VBE to switch back to Excel.

### 2.8 Saving Workbooks That Contain Macros

If you store one or more macros in a workbook, the file must be saved as a macro-enabled file type. In other words, the file must be saved with an XLSM extension rather than the normal XLSX extension.

1『这个之前深有体会，压根没去看提示，一直不另存为 xlsm 文件，导致一直没保存宏，想想当时真 2。（2021-04-21）』

For example, when you save the workbook that contains your NameAndTime macro, the file format in the Save As dialog box defaults to XLSX (a format that cannot contain macros). Unless you change the file format to XLSM, Excel displays the warning shown in Figure 2-4. You need to click No and then choose Excel Macro-Enabled Workbook (*.xlsm) from the Save As Type drop-down list.

FIGURE 2-4: If your workbook contains macros, and you attempt to save it in a macro-free file format, Excel warns you.

### 2.9 Understanding Macro Security

Macro security is a key feature in Excel. The reason is that VBA is a powerful language — so powerful that it's possible to create a macro that can do serious damage to your computer. A macro can delete files, send information to other computers, and even destroy Windows so that you can't even start your system.

The macro security features introduced in Excel 2007 were created to help prevent these types of problems.

Figure 2-5 shows the Macro Settings section of the Trust Center dialog box. To display this dialog box, choose Developer => Code => Macro Security.

FIGURE 2-5: The Macro Settings section of the Trust Center dialog box.

By default, Excel uses the Disable All Macros with Notification option. With this setting in effect, if you open a workbook that contains macros (and the file is not digitally「signed」or stored in a trusted location), Excel displays a warning like the one in Figure 2-6. If you are certain that the workbook comes from a trusted source, click Enable Macros, and the macros will be enabled.

FIGURE 2-6: Excel's warning that the file to be opened contains macros.

You see the pop-up box in Figure 2-6 only when the VBE is open. Otherwise, Excel displays an eye-catching Security Warning above the Formula bar, as shown in Figure 2-7. If you know the workbook is safe, click the Enable Content button to enable the macros. To use the workbook without macros, click the X to dismiss the warning.

Excel remembers when you've designated a workbook to be safe. So the next time you open it, you won't see the Security Warning.

FIGURE 2-7: Excel's warning that the workbook just opened contains macros. You see this warning when the VBE isn't open.

Perhaps the best way to handle macro security is to designate one or more folders as trusted locations. All the workbooks in a trusted location are opened without a macro warning. You designate trusted folders in the Trusted Locations section of the Trust Center dialog box.

1『获取到的知识点：指定某一个特定的文件夹为「信任」级别，这里面的宏打开无需验证。（2021-04-21）』

If you want to find out what the other macro security settings imply, press F1 while the Macro Settings section of the Trust Center dialog box is in view. You get a Help screen that describes the security settings.

### 2.10 Revealing More about the NameAndTime Macro

By the time you finish this book, you should completely understand how the NameAndTime macro works — and you'll be able to develop more sophisticated macros. For now, this chapter ends with a few additional points about the macro:

1 For this macro to work, its workbook must be open. If you close the workbook, the macro isn't available so it can't work (and its shortcut keys have no effect).

2 As long as the workbook containing the macro is open, you can run the macro while any workbook is active. In other words, the macro's own workbook doesn't have to be active.

3 The macro isn't「pro-quality」code. It will overwrite existing text with no warning — and its effects can't be undone.

4 Before you started recording the macro, you assigned it a new shortcut key. This is just one of several ways to execute the macro. (You discover other ways in Chapter 5.)

5 You can create this macro manually rather than record it. To do so, you need a good understanding of VBA. (Be patient; you'll get there.)

6 You can store this macro in your Personal Macro Workbook. If you do so, the macro is available automatically whenever you start Excel. (See Chapter 6 for details about your Personal Macro Workbook.)

7 You can also convert the workbook to an add-in file. (More about this in Chapter 21.)

Congratulations. You've been initiated into the world of Excel programming. (Sorry, there's no secret handshake or decoder ring.)

In This Part: 1) See how to access the important part of the Visual Basic Editor. 2) Discover VBA code modules (where you store your VBA code). 3) Get an overview of the Excel object model. 4) Discover a bit about two key concepts: object properties and methods. 5) Find out the differences between Sub procedures and Function procedures. 6) Get a crash course in using the Excel macro recorder.

## 0301. Working in the Visual Basic Editor

In This Chapter: 1) Understanding the Visual Basic Editor. 2) Discovering the Visual Basic Editor parts. 3) Knowing what goes into a VBA module. 4) Understanding three ways to get VBA code into a module 5) Customizing the VBA environment.

As a more experienced-than-average Excel user, you probably know a good deal about workbooks, formulas, charts, and other Excel goodies. Now it's time to expand your horizons and explore an entirely new aspect of Excel: the Visual Basic Editor. In this chapter, you find out how to work with the Visual Basic Editor, and you get down to the nitty-gritty of writing some VBA code.

### 3.1 What Is the Visual Basic Editor?

The Visual Basic Editor (often refered to as the VBE) is a separate application where you write and edit your VBA macros. Beginning with Excel 2013, every workbook displays in a separate window. However, there is only one VBE window, and it works with all open Excel windows.

You can't run the VBE separately; Excel must be running for the VBE to run.

1『小知识点：VBE 不能独立运行，必须 Excel 打开的时候跑。（2021-03-21）』

#### 3.1.1 Activating the VBE

The quickest way to activate the VBE is to press Alt+F11 when Excel is active. To return to Excel, press Alt+F11 again. Or you can just click the Close button on the VBE's title bar. When the VBE window closes, Excel is activated.

You can also activate the VBE by choosing Developer => Code => Visual Basic. If you don't have a Developer tab at the top of your Excel window, refer to Chapter 2, where you learn how to get that handy Developer tab to show up.

#### 3.1.2 Understanding VBE components

Figure 3-1 shows the VBE program, with some of the key parts identified.

Chances are that your VBE program window won't look exactly like what you see in Figure 3-1. The VBE contains several windows, and it's highly customizable. You can hide windows, rearrange windows, dock windows, and so on.

Menu bar: The VBE menu bar works just like every other menu bar you've encountered. It contains commands that you use to do things with the various components in the VBE. You also find that many of the menu commands have shortcut keys associated with them. The VBE also features shortcut menus. You can right-click virtually anything in the VBE and get a shortcut menu of common commands.

Toolbar: The Standard toolbar, which is directly below the menu bar by default (refer to Figure 3-1), is one of the four VBE toolbars available. You can customize the toolbars, move them around, display other toolbars, and so on. If you're so inclined, choose View => Toolbars to work with the VBE toolbars. Most people just leave them as they are.

Project window: The Project window displays a tree diagram that shows every workbook currently open in Excel (including add-ins and hidden workbooks). Double-click items to expand or contract them within the outline. See the upcoming「Working with the Project Window」section for more detail.

If the Project window is not visible, press Ctrl+R or choose View => Project Explorer. To hide the Project window, click the Close button on its title bar. Or right-click anywhere in the Project window and choose Hide from the shortcut menu.

Code window: A Code window is where you put your VBA code. Every object in a project has an associated Code window. To view an object's Code window, double-click the object in the Project window. For example, to view the Code window for the Sheet1 object in Book1, double-click Sheet1 in the VBAProject for Book1. Unless you've added some VBA code, the Code window is empty.

You find out more about Code windows later in this chapter's「Working with a Code Window」section.

Immediate window: The Immediate window may or may not be visible. If it isn't visible, press Ctrl+G or choose View => Immediate Window. To close the Immediate window, click the Close button on its title bar (or right-click anywhere in the Immediate window and choose Hide from the shortcut menu).

WHAT'S NEW IN THE VISUAL BASIC EDITOR?

Excel 2007 introduced a brand-new user interface. Menus and toolbars were replaced with a slick new Ribbon user interface (UI). But the VBE never got the facelift and has kept the old-school menu and toolbar UI. The VBA programming language has been updated to accommodate the new Excel features, but nothing else has changed.

One thing that has changed is the Help system. In the past, help information was stored on your computer, and you had the option of accessing Help via the Internet. Beginning with Excel 2013, all help information is on the Internet and is displayed in your web browser. In other words, you must be connected to the Internet to access the Help system. You can, however, download your very own copy of the Help system from Microsoft's site. Do a web search for download excel vba documentation , and you'll find it.

The Immediate window is most useful for executing VBA statements directly and for debugging your code. If you're just starting out with VBA, this window won't be all that useful, so feel free to hide it and free some screen space for other things.

Chapter 13 covers the Immediate window in detail. It may just become your good friend!

### 3.2 Working with the Project Window

When you're working in the VBE, each Excel workbook and add-in that's open is a project. You can think of a project as a collection of objects arranged as an outline.

You can expand a project by clicking the plus sign (+) at the left of the project's name in the Project window. Collapse a project by clicking the minus sign (–) to the left of a project's name. Or you can double-click the items to expand them.

If a project is password-protected, you're prompted for the password when you double-click a project name. If you don't know the password, you can't expand the project — which means that you can't view or modify any part of the project.

Figure 3-2 shows a Project window with four projects listed: an add-in named pup7.xlam, an unsaved workbook named Book1, a workbook named investments. xlsm, and the Personal Macro Workbook (which is always named PERSONAL. XLSB). Of the four, only the investments.xlsm project is expanded to show all of its objects.

FIGURE 3-2: This Project window lists four projects. One of them is expanded to show its objects.

Every project expands to show at least one node called Microsoft Excel Objects. This node expands to show an item for each sheet in the workbook (each sheet is considered an object) and another object called ThisWorkbook (which represents the Workbook object). If the project has any VBA modules, the project listing also shows a Modules node. And as you find out in Part 4, a project may also contain a node called Forms, which contains UserForm objects (which hold custom dialog boxes).

The concept of objects may be a bit fuzzy for you. But don't worry. Things become much clearer in subsequent chapters. Don't be too concerned if you don't understand what's going on at this point.

#### 3.2.1 Adding a new VBA module

Follow these steps to add a new VBA module to a project:

1 In the VBE, select the project's name in the Project window.

2 Choose Insert ➪ Module.

Or

1 Right-click the project's name.

2 Choose Insert => Module from the shortcut menu.

When you record a macro, Excel automatically inserts a VBA module to hold the recorded code. Which workbook holds the module for the recorded macro depends on where you chose to store the recorded macro, just before you started recording.

#### 3.2.2 Removing a VBA module

Sometimes, you need to remove a VBA module from a project. For example, it may contain code that you no longer need, or it's empty because you inserted the module and then changed your mind. To remove a VBA module from a project:

1 Select the module's name in the Project window.

2 Choose File => Remove xxx , where xxx is the module name.

Or

1 Right-click the module's name.

2 Choose Remove xxx from the shortcut menu.

Excel, always trying to keep you from doing something you'll regret, asks whether you want to export the code in the module before you delete it. Almost always, you don't. (If you do want to export the module, see the next section.) You can remove VBA modules, but there is no way to remove the other code modules — those for the Sheet objects or ThisWorkbook.

#### 3.2.3 Exporting and importing objects

1『竟然还能导入导出模块，之前看 VBA 的那边中文书籍里没看到过。（2021-03-21）』

Every object in a VBA project can be saved to a separate file. Saving an individual object in a project is known as exporting. It stands to reason that you can also import objects into a project. Exporting and importing objects might be useful if you want to use a particular object (such as a VBA module or a UserForm) in a different project. Or maybe you want to send a co-worker a copy of a VBA module, which she can then import into her project.

Follow these steps to export an object:

1 Select an object in the Project window.

2 Choose File => Export File or press Ctrl+E.

You get a dialog box that asks for a filename. Note that the object remains in the project; only a copy of it is exported. Excel provides the file extension for you, and the extension depends on what type of object you're exporting. In all cases, the result is a text file. If you're so inclined, you can open it with a text editor and take a look.

Importing a file to a project goes like this:

1 Select the project's name in the Explorer window.

2 Choose File => Import File or press Ctrl+M. You get a dialog box that asks for a file.

3 Locate the file, and click Open.

You should import VBA object files only if you know who it came from. Otherwise, you could be introducing macros that perform malicious actions.

### 3.3 Working with a Code Window

As you become proficient with VBA, you spend lots of time working in Code windows. Macros that you record are stored in a module, and you can type VBA code directly in a VBA module.

#### 3.3.1 Minimizing and maximizing windows

If you have several projects open, the VBE may have lots of Code windows at any given time. Figure 3-3 shows an example.

FIGURE 3-3: Code window overload isn't a pretty sight.

Code windows are much like workbook windows in Excel. You can minimize them, maximize them, resize them, hide them, rearrange them, and so on. Most people find it much easier to maximize the Code window that they're working on. Doing so lets you see more code and keeps you from getting distracted.

To maximize a Code window, click the Maximize button on its title bar (right next to the X). Or just double-click its title bar to maximize it. To restore a Code window to its original size, click the Restore button. When a window is maximized, its title bar isn't visible, so you'll find the Restore button below the VBE title bar.

Sometimes, you may want to have two or more Code windows visible. For example, you may want to compare the code in two modules or copy code from one module to another. You can arrange the windows manually or choose Window => Tile Horizontally or Window => Tile Vertically to arrange them automatically.

You can quickly switch among Code windows by pressing Ctrl+F6. If you repeat that key combination, you keep cycling through all the open Code windows. Pressing Ctrl+Shift+F6 cycles through the windows in reverse order.

Minimizing a Code window gets it out of the way. You can also click the window's Close button (which displays X) on a Code window's title bar to close the window. (Closing a window just hides it; you won't lose anything.) To open it again, just double-click the appropriate object in the Project window. By the way, working with these Code windows sounds more difficult than it really is.

#### 3.3.2 Creating a module

In general, a VBA module can hold three types of code:

1 Declarations: One or more information statements that you provide to VBA. For example, you can declare the data type for variables you plan to use or set some other module-wide options. Declarations are basically house-keeping statements. They aren't actually executed.

2 Sub procedures: A set of programming instructions that, when executed, performs some action.

3 Function procedures: A set of programming instructions that returns a single value (similar in concept to a worksheet function, such as SUM).

1-2『这里第一次认识到 Sub 和 Function 的区别。Sub 是一系列「语句」的集合，而 Function 往往针对会返回一个「结果值」的场景。那么是不是可以理解：只有返回「结果值」的情况下才封装成 Function，其他情况都封装成 Sub。Sub 和 Function 的区别，做一张主题卡片。（2021-04-21）』—— 已完成

A single VBA module can store any number of Sub procedures, Function procedures, and declarations. Well, there is a limit — about 64,000 characters per module. It's unlikely you'll even get close to reaching the 64,000-character limit. But if you did, the solution is simple: Just insert a new module.

How you organize a VBA module is completely up to you. Some people prefer to keep all their VBA code for an application in a single VBA module; others like to split the code into several modules. It's a personal choice, just like arranging furniture.

#### 3.3.3 Getting VBA code into a module

An empty VBA module is like the fake food you see in the windows of some Chinese restaurants; it looks good but it doesn't really do much for you. Before you can do anything meaningful, you must have some VBA code in the VBA module. You can get VBA code into a VBA module in three ways:

1 Enter the code directly.

2 Use the Excel macro recorder to record your actions and convert those actions to VBA code (see Chapter 6).

3 Copy the code from one module and paste it into another.

#### 3.3.4 Entering code directly

Sometimes, the best route is the most direct one. Entering code directly involves......well, entering the code directly. In other words, you type the code by using your keyboard. Entering and editing text in a VBA module works as you might expect. You can select, copy, cut, paste, and do other things to the text.

Use the Tab key to indent some of the lines to make your code easier to read. Indenting isn't necessary, but it's a good habit to acquire. As you study the code in this book, you'll understand why indenting code lines is helpful.

PAUSE FOR A TERMINOLOGY BREAK

Throughout this book, you'll see the terms Sub procedure, routine, program, procedure , and macro. These terms are a bit confusing. Programming folks usually use the word procedure to describe an automated task. Technically, a procedure can be a Sub procedure or a Function procedure — both of which are sometimes called routines — or even programs. All these terms are used interchangeably. As detailed in later chapters, however, there is an important difference between Sub and Function procedures. For now, don't worry about the terminology. Just try to understand the concepts.

A single line of VBA code can be as long as you need it to be. However, you may want to use the line-continuation characters to break up lengthy lines of code. To continue a single line of code (also known as a statement) from one line to the next, end the first line with a space followed by an underscore (_). Then continue the statement on the next line. And don't forget the space. An underscore character that's not preceded by a space won't do the job.

1-2『第二次看到了换行写法的注意点：`_` 前面的空格一定不定漏，否则换行无效。做一张任意卡片。（2021-04-21）』—— 已完成

Here's an example of a single statement split into three lines:

```c
Selection.Sort Key1:=Range("A1"), _
  Order1:=xlAscending, Header:=xlGuess, _
  Orientation:=xlTopToBottom
```

This statement would perform exactly the same way if it were entered in a single line (with no line-continuation characters). Notice that the second and third lines of this statement are indented. Indenting is optional, but it helps clarify the fact that these lines are not separate statements.

The white-coated engineers who designed the VBE anticipated that people like us would be making mistakes. Therefore, the VBE has multiple levels of undo and redo. If you deleted a statement that you shouldn't have, click the Undo button on the toolbar (or press Ctrl+Z) until the statement shows up again. After undoing,

you can click the Redo button to perform the changes you've undone. Are you ready to enter some real-live code? Try the following steps:

1 Create a new workbook in Excel.

2 Press Alt+F11 to activate the VBE.

3 Click the new workbook's name in the Project window.

4 Choose Insert => Module to insert a VBA module into the project.

5 Type the following code in the module:

```c
Sub GuessName()
  Msg = "Is your name " & Application.UserName & "?"
  Ans = MsgBox(Msg, vbYesNo)
  If Ans = vbNo Then MsgBox "Oh, never mind."
  If Ans = vbYes Then MsgBox "I must be psychic!"
End Sub
```

1『上面的 if 语句的写法就很简介，值得借鉴。（2021-04-21）』

6 Position the cursor anywhere within the text you typed and press F5 to execute the procedure.

F5 is a shortcut for Run => Run Sub/UserForm. If you entered the code correctly, Excel executes the procedure, and you can respond to the simple dialog box shown in Figure 3-4. The text in the dialog box will be different from the text shown in the figure.

2『跑 Sub 的快捷键 F5，收录入主题卡片「快捷键」。（2021-04-21）』—— 已完成

FIGURE 3-4: The GuessName procedure displays this dialog box.

When you enter the code listed in Step 5, you might notice that the VBE makes some adjustments to the text you enter. For example, after you type the Sub statement, the VBE automatically inserts the End Sub statement. And if you omit the space before or after an equal sign, the VBE inserts the space for you. Also, the VBE changes the color and capitalization of some text. This is all perfectly normal.

It's just the VBE's way of keeping things neat and readable.

COMPILE ERROR?

There's a chance that the GuessName macro won't work. When you try to run it, Excel may complain and pop up an error message: Compile Error: Variable Not Defined. Don't worry; there's an easy fix for that.

If you get that error, look at the top of your module, and you'll see this text: Option Explicit. Just delete that line, and the macro should work. That line, when present at the top of a module, means that you must「declare」all your variables. (See Chapter 7 for more about variables). If that line was added, it means that your VBE is set up to add the line automatically. For now, don't worry about it. Just delete the line and forget about the rude interruption.

1『个人建议保留那行语句，强制声明变量，VBA 还是按静态语言方式编程比较好。（2021-04-21）』

If you followed the previous steps, you just wrote a VBA Sub procedure, also known as a macro. When you press F5, Excel executes the code and follows the instructions. In other words, Excel evaluates each statement and does what you told it to do. (Don't let this newfound power go to your head.) You can execute this macro any number of times — although it tends to lose its appeal after a few dozen times.

For the record, this simple macro uses the following concepts, all of which are covered later in this book:

1 Defining a Sub procedure (the first line).

2 Assigning values to variables (Msg and Ans).

3 Concatenating (joining) a string (using the & operator).

4 Using a built-in VBA function (MsgBox).

5 Using built-in VBA constants (vbYesNo, vbNo, and vbYes).

6 Using an If-Then construct (twice).

7 Ending a Sub procedure (the last line).

Not bad for a beginner, eh?

#### 3.3.5 Using the macro recorder

Another way you can get code into a VBA module is by recording your actions, using the Excel macro recorder. If you worked through the hands-on exercise in Chapter 2, you already have some experience with this technique.

By the way, there is absolutely no way you can record the GuessName procedure shown in the preceding section. You can record only things that you can do directly in Excel. Displaying a message box is not in Excel's normal repertoire. (It's a VBA thing.) The macro recorder is useful, but in many cases, you'll probably need to enter at least some code manually.

Here's a step-by-step example that shows how to record a macro that inserts a new worksheet and hides all but the first ten rows and all but the first ten columns. If you want to try this example, start with a new, blank workbook and follow these steps:

1 Activate a worksheet in the workbook. Any worksheet will do.

2 Click the Developer tab, and make sure that Use Relative References is not highlighted. This macro is recorded using Absolute References.

3 Choose Developer => Code => Record Macro, or click the icon next to the Ready indicator on the left end of the status bar. Excel displays its Record Macro dialog box.

4 In the Record Macro dialog box, name the macro TenByTen, specify that you want the macro stored in This Workbook, and press Shift+T for the shortcut key. The macro can be executed when you press Ctrl+Shift+T.

5 Click OK to start recording. Excel automatically inserts a new VBA module into the project that corresponds to the active workbook. From this point on, Excel converts your actions to VBA code. While you're recording, the icon in the status bar turns into a small square. This is a reminder that the macro recorder is running. You can also click that icon to stop the macro recorder.

6 Click the New Sheet icon to the right of the last sheet tab. Excel inserts a new worksheet.

7 Select the entire Column K (the 11th column) and press Ctrl+Shift+right arrow; then right-click any selected column and choose Hide from the shortcut menu. Excel hides all of the selected columns.

8 Select the entire Row 11 and press Ctrl+Shift+down arrow; then right-click any selected row and choose Hide from the shortcut menu. Excel hides all of the selected columns.

9 Select cell A1.

10 Choose Developer => Code => Stop Recording, or click the Stop Recording button on the status bar (the small square). Excel stops recording your actions.

To view this newly recorded macro, press Alt+F11 to activate the VBE. Locate the workbook's name in the Project window. You see that the project has a new module listed. The name of the module depends on whether you had any other modules in the workbook when you started recording the macro. If you didn't, the module is named Module1. You can double-click the module to view the Code window for the module.

Here's the code generated by your actions:

```c
Sub TenByTen()
'
' TenByTen Macro
'
' Keyboard Shortcut: Ctrl+Shift+T
'
  Sheets.Add After:=ActiveSheet
  Columns("K:K").Select
  Range(Selection, Selection.End(xlToRight)).Select
  Selection.EntireColumn.Hidden = True
  Rows("11:11").Select
  Range(Selection, Selection.End(xlDown)).Select
  Selection.EntireRow.Hidden = True
  Range("A1").Select
End Sub
```

To try this macro, activate any worksheet and press the shortcut key that you assigned in Step 4: Ctrl+Shift+T.

If you didn't assign a shortcut key to the macro, don't worry. Here's how to display a list of all macros available and run the one you want:

1 Choose Developer =>  Code => Macros.

Keyboard fans can press Alt+F8. Either of these methods displays a dialog box that lists all the available macros.

2 Select the macro in the list (in this case, TenByTen).

3 Click the Run button. Excel executes the macro, and you get a new worksheet with ten visible rows and ten visible columns.

You can execute any number of commands and perform any number of actions while the macro recorder is running. Excel dutifully translates your mouse actions and keystrokes to VBA code.

And, of course, you can also edit the macro after you record it. To test your new skills, try editing the macro so that it inserts a worksheet with nine visible rows and columns — perfect for a Sudoku puzzle.

#### 3.3.6 Copying VBA code

The final method for getting code into a VBA module is to copy it from another module or from some other place (such as a website). For example, a Sub or Function procedure that you write for one project might also be useful in another project. Instead of wasting time reentering the code, you can activate the module and use the normal Clipboard copy-and-paste procedures. (You're probably rather fond of the keyboard shortcuts Ctrl+C to copy and Ctrl+V to paste.) After pasting the code into a VBA module, you can modify the code if necessary.

By the way, you'll find lots of VBA code examples on the web. If you'd like to try them, select the code in your browser and press Ctrl+C to copy it. Then activate a module and press Ctrl+V to paste it.

When you copy code from a website, it sometimes requires some fixing. For example, quote characters may be「smart quotes」and they must be converted to simple quote characters. And sometimes, long lines wrap around. Erroneous statements are easy to spot in the VBE because they appear in red.

### 3.4 Customizing the VBA Environment

If you're serious about becoming an Excel programmer, you'll spend a lot of time with VBA modules on your screen. To help make things as comfortable as possible (no, please keep your shoes on), the VBE provides quite a few customization options.

When the VBE is active, choose Tools => Options. You'll see a dialog box with four tabs: Editor, Editor Format, General, and Docking. Some of the most useful options are discussed in the sections that follow.

#### 3.4.1 Using the Editor tab

Figure 3-5 shows the options you can access by clicking the Editor tab of the Options dialog box. Use the options in the Editor tab to control how certain things work in the VBE.

Auto Syntax Check option:

The Auto Syntax Check setting determines whether the VBE pops up a dialog box if it discovers a syntax error while you're entering your VBA code. The dialog box tells roughly what the problem is. If you don't choose this setting, the VBE flags syntax errors by displaying them in a different color from the rest of the code, and you don't have to deal with any dialog boxes popping up on your screen.

FIGURE 3-5: The Editor tab of the Options dialog box.

Require Variable Declaration option: If the Require Variable Declaration option is set, VBE inserts the following statement at the beginning of each new VBA module you insert:

```c
Option Explicit
```

Changing this setting affects only new modules, not existing modules. If this statement appears in your module, you must explicitly define each variable you use. Chapter 7 goes into the details why you should develop this habit.

Auto List Members option: If the Auto List Members option is set, the VBE provides some help when you're entering your VBA code. It displays a list that would logically complete the statement you're typing. This bit of magic is sometimes called IntelliSense. This is one of the best features of the VBE. Figure 3-6 shows an example (which will make lots more sense when you start writing VBA code).

Auto Quick Info option: If the Auto Quick Info option is set, the VBE displays information about functions and their arguments as you type. This can be very helpful. Figure 3-7 shows this feature in action, telling you about the arguments for the MsgBox function.

FIGURE 3-6: An example of Auto List Members.

FIGURE 3-7: Auto Quick Info offers help about the MsgBox function.

Auto Data Tips option: If the Auto Data Tips option is set, the VBE displays the value of the variable over which your cursor is placed when you're debugging code. When you enter the wonderful world of debugging, as described in Chapter 13, you'll appreciate this option.

Auto Indent setting:

The Auto Indent setting determines whether the VBE automatically indents each new line of code the same as the previous line. Use the Tab key to indent your code, not the space bar. Also, you can press Shift+Tab to「unindent」a line of code. If you want to indent more than just one line, select all the lines you want to indent. Then press the Tab key.

The VBE's Edit toolbar (which is hidden by default) contains two useful buttons: Indent and Outdent. These buttons let you quickly indent or「unindent」a block of code. Select the code and click one of these buttons to change the block's indenting.

Drag-and-Drop Text Editing option: The Drag-and-Drop Text Editing option, when enabled, lets you copy and move text by dragging and dropping with your mouse.

Default to Full Module View option: The Default to Full Module View option sets the default state for new modules. (It doesn't affect existing modules.) If this option is set, procedures in the Code window appear as a single scrollable list. If this option is turned off, you can see only one procedure at a time.

Procedure Separator option: When the Procedure Separator option is turned on, separator bars appear between procedures in a Code window.

Using the Editor Format tab: Figure 3-8 shows the Editor Format tab of the Options dialog box. With this tab, you can customize the way the VBE looks.

FIGURE 3-8: Change the VBE's looks with the Editor Format tab.

Code Colors option: The Code Colors option lets you set the text color and background color displayed for various elements of VBA code. This is largely a matter of personal preference.

Font option: The Font option lets you select the font that's used in your VBA modules. For best results, stick with a fixed-width font such as Courier New. In a fixed-width font, all characters are exactly the same width. This makes your code more readable because the characters are nicely aligned vertically, and you can easily distinguish multiple spaces (which is sometimes useful).

Size setting: The Size setting specifies the point size of the font in the VBA modules. This setting is a matter of personal preference determined by your video display resolution and how many carrots you've been eating.

Margin Indicator Bar option: This option controls the display of the vertical margin indicator bar in your modules. You should keep this turned on; otherwise, you won't be able to see the helpful graphical indicators when you're debugging your code.

#### 3.4.2 Using the General tab

Figure 3-9 shows the options available on the General tab of the Options dialog box. In almost every case, the default settings are just fine.

FIGURE 3-9: The General tab of the Options dialog box.

The most important setting is Error Trapping. It's considered a best practice to use the Break on Unhandled Errors setting (which is the default). If you use a different setting, your error-handling code won't work. You can read more about this in Chapter 12.

If you're really interested in these options, click the Help button for details.

#### 3.4.3 Using the Docking tab

Figure 3-10 shows the Docking tab. These options determine how the various windows in the VBE behave. When a window is docked, it's fixed in place along one of the edges of the VBE program window. This makes it much easier to identify and locate a particular window. If you turn off all docking, you have a big, confusing mess of windows. Generally, the default settings work fine.

FIGURE 3-10: The Docking tab of the Options dialog box.

Sometimes the VBE seems to have a mind of its own when you're trying to dock a window. If docking doesn't seem to work correctly, just stick with it, and you'll get the hang of things.

## 0401. Introducing the Excel Object Model

In This Chapter: 1) Introducing the concept of objects. 2) Finding out about the Excel object hierarchy. 3) Understanding object collections. 4) Referring to specific objects in your VBA code. 5) Accessing or changing an object's properties. 6) Performing actions with an object's methods.

Everyone is familiar with the word object. Well, folks, forget the definition you think you know. In the world of programming, the word object has a different meaning. You often see it used as part of the expression object-oriented programming, or OOP for short. OOP is based on the idea that software deals with distinct objects that have attributes (or properties) and can be manipulated. These objects are not material things. Rather, they exist in the form of bits and bytes.

In this chapter, you'll be introduced to the Excel object model, which is a hierarchy of objects contained in Excel. By the time you finish this chapter, you'll have a pretty good feel for what OOP is all about — and why you need to understand this concept to become a VBA programmer. After all, Excel programming really boils down to manipulating the objects that make up Excel. It's as simple as that.

### 4.1 Excel Is an Object?

You've used Excel for quite a while, but you probably never thought of it as an object. The more you work with VBA, the more you view Excel in those terms. You'll understand that Excel is an object and that it contains other objects. Those objects, in turn, contain still more objects. In other words, VBA programming involves working with an object hierarchy.

At the top of this hierarchy is the Application object — in this case, Excel itself (the mother of all objects).

### 4.2 Climbing Down the Object Hierarchy

The Application object contains other objects. The following are some of the more useful objects contained in the Excel application: 1) Addin. 2) Window. 3) Workbook. 4) WorksheetFunction.

Each object contained in the Application object can contain other objects. For example, the following are some objects that can be contained in a Workbook object: 1) Chart (which is a chart sheet). 2) Name. 3) VBProject. 4) Window. 5) Worksheet.

In turn, each of these objects can contain still other objects. Consider a Worksheet object, which is contained in a Workbook object, which is contained in the Application object. Some of the objects that can be contained in a Worksheet object are: 1) Comment. 2) Hyperlink. 3) Name. 4) PageSetup. 5) PivotTable. 6) Range.

Put another way, if you want to do something with a range on a particular worksheet, you may find it helpful to visualize that range in the following manner:

Range => contained in Worksheet => contained in Workbook => contained in Excel

Is this beginning to make sense?

When you start digging around, you'll find that Excel has more objects than you can shake a stick at. Even power users can get overwhelmed. The good news is that you'll never have to actually deal with most of these objects. When you're working on a problem, you can just focus on a few relevant objects — which you can often discover by recording a macro.

### 4.3 Wrapping Your Mind around Collections

Collections are another key concept in VBA programming. A collection is a group of objects of the same type. And to add to the confusion, a collection is itself an object. Here are a few examples of commonly used collections:

1 Workbooks: A collection of all currently open Workbook objects.

2 Worksheets: A collection of all Worksheet objects contained in a particular Workbook object.

3 Charts: A collection of all Chart objects (chart sheets) contained in a particular Workbook object.

4 Sheets: A collection of all sheets (regardless of their type) contained in a particular Workbook object.

1-2『 Sheets 和 Worksheets 是 2 个对象集合，印象中 Sheets 的概念更大，Sheet 包含 Worksheet 对象。做一张任意卡片。（2021-04-22）』—— 已完成

You may notice that collection names are all plural, which makes sense.

「What are collections for?」you may rightfully ask. Well, for example, they're very useful when you want to work with not just one worksheet, but with a couple of them or all of them. As you'll see, your VBA code can loop through all members of a collection and do something to each one.

### 4.4 Referring to Objects

Referring to an object is important because you must identify the object that you want to work with. After all, VBA can't read your mind — yet.

You can work with an entire collection of objects in one fell swoop. More often, however, you need to work with a specific object in a collection (such as a particular worksheet in a workbook). To reference a single object from a collection, you put the object's name or index number in parentheses after the name of the collection, like this:

```c
Worksheets("Sheet1")
```

Notice that the sheet's name is in quotation marks. If you omit the quotation marks, Excel won't be able to identify the object (and will assume that it's a variable name). If you want to work with the first worksheet in the collection, you can also use the following reference:

```c
Worksheets(1)
```

In this case, the number is not in quotation marks. Bottom line? If you refer to an object by using its name, use quotation marks. If you refer to an object by using its index number, use a plain number without quotation marks. What about chart sheets? A chart sheet contains a single chart. It has a sheet tab, but it's not a worksheet. Well, as it turns out, the object model has a collection called Charts. This collection contains all the chart sheet objects in a workbook (and does not include charts embedded in a worksheet). And just to keep things logical, there's another collection called Sheets. The Sheets collection contains all sheets (worksheets and chart sheets) in a workbook. The Sheets collection is handy if you want to work with all sheets in a workbook and don't care if they are worksheets or chart sheets.

So, a single worksheet named Sheet1 is a member of two collections: the Worksheets collection and the Sheets collection. You can refer to it in either of two ways:

```c
Worksheets("Sheet1")
Sheets("Sheet1")
```

#### 4.4.1 Navigating through the hierarchy

If you want to work with Excel objects, they are all under the Application object. So start by typing Application.

Every other object in Excel's object model is under the Application object. You get to these objects by moving down the hierarchy and connecting each object on your way with the dot (`.`) operator. To get to the Workbook object named Book1.xlsx, start with the Application object and navigate down to the Workbooks collection object:

```c
Application.Workbooks("Book1.xlsx")
```

To navigate to a specific worksheet, add a dot operator and access the Worksheets collection object:

```c
Application.Workbooks("Book1.xlsx").Worksheets(1)
```

Not far enough yet? If you really want to get the value from cell A1 on the first Worksheet of the Workbook named Book1.xlsx, you need to navigate one more level to the Range object:

```c
Application.Workbooks("Book1.xlsx").Worksheets(1).Range("A1").Value
```

When you refer to a Range object in this way, it's called a fully qualified reference. You've told Excel exactly which range you want, on which worksheet and in which workbook, and have left nothing to the imagination. Imagination is good in people but not so good in computer programs.

By the way, workbook names also have a dot to separate the filename from the extension (for example, Book1.xlsx). That's just a coincidence. The dot in a filename has nothing at all to do with the dot operator referred to a few paragraphs ago.

#### 4.4.2 Simplifying object references

If you were required to fully qualify every object reference you make, your code would get quite long, and it might be more difficult to read. Fortunately, Excel provides some shortcuts that can improve the readability (and save you some typing). For starters, the Application object is always assumed. There are only a few cases when it makes sense to type it. Omitting the Application object reference shortens the example from the previous section to

```c
Workbooks("Book1.xlsx").Worksheets(1).Range("A1").Value
```

That's a pretty good improvement. But wait, there's more. If you're sure that Book1. xlsx is the active workbook, you can omit that reference, too. Now you're down to

```c
Worksheets(1).Range("A1").Value
```

Now you're getting somewhere. Have you guessed the next shortcut? That's right. If you know the first worksheet is the currently active worksheet, Excel assumes that reference and allows you to just type

```c
Range("A1").Value
```

Contrary to what some people may think, Excel does not have a Cell object. A cell is simply a Range object that consists of just one element.

2『 Excel 里没有 cell 对象，做一张数据信息卡片。（2021-04-22）』—— 已完成

The shortcuts described here are great, but they can also be dangerous. What if you only think Book1.xlsx is the active workbook? You could get an error, or worse, you could get the wrong value and not even realize it's wrong. For that reason, it's often best to fully qualify your object references.

Chapter 14 discusses the With-End With structure, which helps you fully qualify your references but also helps to make the code more readable and cuts down on the typing. The best of both worlds!

### 4.5 Diving into Object Properties and Methods

Although knowing how to refer to objects is important, you can't do anything useful by simply referring to an object (as in the examples in the preceding sections). To accomplish anything meaningful, you must do one of two things:

Read or modify an object's properties.

Specify a method of action to be used with an object.

ANOTHER SLANT ON MCPROPERTIES, AND MCOBJECTS, MCMETHODS

Here's an analogy, comparing Excel to a fast-food chain, that may help you understand the relationships among objects, properties, and methods in VBA.

The basic unit of Excel is a Workbook object. In a fast-food chain, the basic unit is an individual restaurant. With Excel, you can add a workbook and close a workbook, and all the open workbooks are known as Workbooks (a collection of Workbook objects). Similarly, the management of a fast-food chain can add a restaurant and close a restaurant, and all the restaurants in the chain can be viewed as the Restaurants collection (a collection of Restaurant objects).

An Excel workbook is an object, but it also contains other objects such as worksheets, chart sheets, VBA modules, and so on. Furthermore, each object in a workbook can contain its own objects. For example, a Worksheet object can contain Range objects, PivotTable objects, Shape objects, and so on.

Continuing with the analogy, a fast-food restaurant (like a workbook) contains objects such as the Kitchen, DiningArea, and Tables (a collection). Furthermore, management can add or remove objects from the Restaurant object. For example, management may add more tables to the Tables collection. Each of these objects can contain other objects. For example, the Kitchen object has a Stove object, VentilationFan object, Chef object, Sink object, and so on.

So far, so good. This analogy seems to work.

Excel's objects have properties. For example, a Range object has properties such as Value and Name, and a Shape object has properties such as Width, Height, and so on. Not surprisingly, objects in a fast-food restaurant also have properties. The Stove object, for example, has properties such as Temperature and NumberofBurners. The VentilationFan has its own set of properties (TurnedOn, RPM, and so on).

Besides properties, Excel's objects also have methods, which perform an operation on an object. For example, the ClearContents method erases the contents of a Range object. An object in a fast-food restaurant also has methods. You can easily envision a ChangeThermostat method for a Stove object or a SwitchOn method for a VentilationFan object.

In Excel, methods sometimes change an object's properties. The ClearContents method for a Range changes the Range's Value property. Similarly, the ChangeThermostat method on a Stove object affects its Temperature property. With VBA, you can write procedures to manipulate Excel's objects. In a fast-food restaurant, the management can give orders to manipulate the objects in the restaurants (“Turn the stove on and switch the ventilation fan to high”).

The next time you visit your favorite fast-food joint, just say, “Use the Grill method on a Burger object with the Onion property set to False.”

#### 4.5.1 Object properties

Every object has properties. You can think of properties as attributes that describe the object. An object's properties determine how it looks, how it behaves, and even whether it's visible. Using VBA, you can do two things with an object's properties: 1) Examine the current setting for a property. 2) Change the property's setting.

For example, a single-cell Range object has a property called Value. The Value property stores the value contained in the cell. You can write VBA code to display the Value property, or you may write VBA code to set the Value property to a specific value. The following macro uses the VBA built-in MsgBox function to bring up a box that displays the value in cell A1 on Sheet1 of the active workbook (see Figure 4-1):

```c
Sub ShowValue() 
  Contents = Worksheets("Sheet1").Range("A1").Value 
  MsgBox Contents 
End Sub
```

FIGURE 4-1: This message box displays a Range object's Value property.

By the way, MsgBox is a very useful function. You can use it to display results while Excel executes your VBA code. You find out more about this function in Chapter 15, so be patient (or just flip ahead and read all about it).

The code in the preceding example displays the current setting of a cell's Value property. What if you want to change the setting for that property? The following macro changes the value in cell A1 by changing the cell's Value property:

```c
Sub ChangeValue()
  Worksheets("Sheet1").Range("A1").Value = 994.92
End Sub
```

After Excel executes this procedure, cell A1 on Sheet1 of the active workbook contains the value 994.92. If the active workbook doesn't have a sheet named Sheet1, the result of executing that macro is an error message. VBA just follows instructions, and it can't work with a sheet that doesn't exist.

Each object has its own set of properties, although some properties are common to many objects. For example, many (but not all) objects have a Visible property. Most objects also have a Name property.

Some object properties are read-only properties, which means that your code can get the property's value, but it can't change it. For example, the Application object has a property called Version that returns the version number of the Excel that's running. You can't change the Version property index; it's read-only.

As mentioned earlier in this chapter, a collection is also an object. This means that a collection also has properties. For example, you can determine how many workbooks are open by accessing the Count property of the Workbooks collection. The following VBA procedure displays a message box that tells you how many workbooks are open:

```c
Sub CountBooks()
  MsgBox Workbooks.Count
End Sub
```

#### 4.5.2 Object methods

In addition to properties, objects have methods. A method is an action you perform with an object. A method can change an object's properties or make the object do something.

This simple example uses the ClearContents method on a Range object to erase the contents of 12 cells on the active sheet:

```c
Sub ClearRange()
  Range("A1:A12").ClearContents
End Sub
```

Some methods take one or more arguments. An argument is a value that further specifies the action to perform. You place the arguments for a method after the method, separated by a space. Multiple arguments are separated by a comma.

The following example activates Sheet1 (in the active workbook) and then copies the contents of cell A1 to cell B1 by using the Range object's Copy method. In this example, the Copy method has one argument, which is the destination range for the copy operation:

```c
Sub CopyOne() 
  Worksheets("Sheet1").Activate 
  Range("A1").Copy Range("B1") 
End Sub
```

Notice that the worksheet reference is omitted when referring to the Range objects. You can do this safely due to the statement to activate Sheet1 (using the Activate method).

Another way to specify an argument for a method is to use the official name of the argument followed by a colon and an equal sign. Using named arguments is optional, but doing so can often make your code easier to understand. The second statement in the CopyOne procedure could be written like this:

```c
Range("A1").Copy Destination:=Range("B1")
```

In Figure 4-2, notice the little prompt as the statement is being typed. That prompt shows the official name of the argument.

FIGURE 4-2: The VBE displays a list of arguments while you type.

Because a collection is also an object, collections have methods. The following macro uses the Add method for the Workbooks collection:

```c
Sub AddAWorkbook()
  Workbooks.Add
End Sub
```

As you may expect, this statement creates a new workbook. In other words, it adds a new workbook to the Workbooks collection. After you execute this macro, a fresh workbook is the active workbook.

#### 4.5.3 Object events

This section briefly touches on one more topic that you need to know about: events. Objects respond to various events that occur. For example, when you're working in Excel and you activate a different workbook, a Workbook Activate event occurs. You could, for example, have a VBA macro that is designed to execute whenever an Activate event occurs for a particular Workbook object.

Excel supports many events, but not all objects can respond to all events. And some objects don't respond to any events. The only events you can use are those made available by the programmers of Microsoft Excel. The concept of an event becomes clear in Chapter 11 and also in Part 4.

### 4.6 Finding Out More

Consider yourself initiated into the wonderful world of objects, properties, methods, and events. You find out more about these concepts in the chapters that follow. If you just can't get enough, you may also be interested in three other excellent tools: 1) VBA's Help system. 2) The Object Browser. 3) Auto List Members.

#### 4.6.1 Using VBA's Help system

The VBA Help system describes every object, property, and method available to you, and also provides sample code. This is an excellent resource for finding out about VBA, and it's more comprehensive than any book on the market. But it's also very boring to read.

If you're using Excel 2013 or later, you must be connected to the Internet to use the VBA Help system (previous versions don't have this requirement). You can, however, download the VBA Help system from Microsoft's website. Do a web search for download excel vba documentation, and you'll find it.

If you're working in a VBA module and want information about a particular object, method, or property, move the cursor to the word you're interested in and press F1. In a few seconds, you see the appropriate Help topic displayed in your web browser, complete with cross-references and perhaps even an example or two.

Figure 4-3 shows part of a screen from the VBA Help system — in this case, for a Worksheet object.

FIGURE 4-3: An example from VBA's Help system.

#### 4.6.2 Using the Object Browser

The VBE includes another tool known as the Object Browser. As the name implies, this tool lets you browse through the objects available to you. To access the Object Browser, press F2 when the VBE is active (or choose View => Object Browser). You see a window like the one shown in Figure 4-4.

The drop-down list at the top contains a list of all currently available object libraries. Figure 4-4 shows All Libraries. If you want to browse through Excel's objects, select Excel from the drop-down list.

FIGURE 4-4: Browsing for objects with the Object Browser.

The second drop-down list is where you enter a search string. For example, if you want to look at all Excel objects that deal with comments, type comment in the second field and click the Search button. (It has a pair of binoculars on it.) The Search Results window displays everything in the object library that contains the text comment. If you see something that looks like it may be of interest, select it and press F1 for more information online.

#### 4.6.3 Automatically listing properties and methods

Chapter 3 introduces you to a handy feature called Auto List Members. This feature provides a list of properties and methods as you type. Figure 4-5 shows an example for the Workbooks collection.

FIGURE 4-5: The Auto List Members feature helps you identify properties and methods for an object.

After typing the dot after workbooks, the VBE volunteers to help by displaying a list of properties and methods for that collection. Typing the letter (like the letter c), narrows the list to items that begin with that letter. With each letter you type, the VBE further narrows the list of choices. Highlight the item you need, press Tab, and voilà! You've eliminated some typing — and also ensured that the property or method was spelled correctly.

## 0501. VBA Sub and Function

In This Chapter: 1) Understanding the difference between Sub procedures and Function procedures. 2) Executing Sub procedures (many ways). 3) Executing Function procedures (two ways).

In the preceding chapters, you've seen the term Sub procedures and Function procedures. The differences between the two kinds of procedures are probably still a mystery to you at this point, but fear not. This chapter clears up any confusion you may have about these concepts.

### 5.1 Understanding Subs versus Functions

The VBA code that you write in the Visual Basic Editor is known as a procedure. The two most common types of procedures are Sub procedures and Function procedures.

A Sub procedure is a group of VBA statements that performs an action (or a sequence of actions) with Excel.

A Function procedure is a group of VBA statements that performs a calculation and returns a single value (or, sometimes, an array).

Most of the macros you write in VBA are Sub procedures. You can think of a Sub procedure as being like a command: Execute the Sub procedure, and something happens. (Of course, exactly what happens depends on the Sub procedure's VBA code.)

A Function is also a procedure, but it's quite different from a Sub. You're already familiar with the concept of a function. Excel includes many worksheet functions that you use every day (well, at least every weekday). Examples include SUM, PMT, and VLOOKUP. You use these worksheet functions in formulas. Each function takes one or more arguments (although a few functions don't use any arguments). The function does some behind-the-scenes calculations using those arguments and then returns a single value. Function procedures that you develop with VBA work the same way.

2『上面的信息补充进主题卡片「Sub 和 Function 的区别」。』—— 已完成

#### 5.1.1 Looking at Sub procedures

Every Sub procedure starts with the keyword Sub and ends with an End Sub statement. Here's an example:

```c
Sub ShowMessage()
  MsgBox "That's all folks!"
End Sub
```

This example shows a procedure named ShowMessage. A set of parentheses follows the procedure's name. In most cases, these parentheses are empty. However, you may pass arguments to Sub procedures from other procedures. If your Sub uses arguments, list them between the parentheses.

When you record a macro with the Excel macro recorder, the result is always a Sub procedure that takes no arguments.

As you see later in this chapter, Excel provides quite a few ways to execute a VBA Sub procedure.

#### 5.1.2 Looking at Function procedures

Every Function procedure starts with the keyword Function and ends with an End Function statement. Here's a simple example:

```c
Function CubeRoot(number) 
  CubeRoot = number ^ (1 / 3) 
End Function
```

This function, named CubeRoot, takes one argument (a variable named number), which is enclosed in parentheses. Functions can have as many as 255 arguments or none at all. When you execute this function, it returns a single value — the cube root of the argument passed to the function.

VBA allows you to specify what type of information (also known as data type) is returned by a Function procedure. For example, a value can be a currency, date, or text string. Chapter 7 contains more information on specifying data types.

You can execute a Function procedure in only two ways: You can execute it from another procedure (a Sub or another Function procedure) or use it in a worksheet formula.

No matter how hard you try, you can't use the Excel macro recorder to record a Function procedure. You must manually enter every Function procedure that you create.

### 5.2 Naming Subs and Functions

Like humans, pets, and hurricanes, every Sub and Function procedure must have a name. Although it's perfectly acceptable to name your dog Hairball Harris, it's usually not a good idea to use such a freewheeling attitude when naming procedures. When naming procedures, you must follow a few rules:

1 You can use letters, numbers, and some punctuation characters, but the first character must be a letter.

2 You can't use any spaces or periods in the name.

3 VBA does not distinguish between uppercase and lowercase letters.

4 You can't use any of the following characters in a procedure name: #, $, %, &, @, ^, *, or !. In other words, your procedure name can't look like comic-strip curse words.

5 If you write a Function procedure for use in a formula, avoid using a name that looks like a cell address (for example, A1 or B52). Actually, Excel allows such function names, but why make things more confusing than they are already?

6 Procedure names can be no longer than 255 characters. (Of course, you would never make a procedure name this long.)

Ideally, a procedure's name describes the routine's purpose. A good practice is to create a name by combining a verb and a noun — for example, ProcessData, PrintReport, Sort_Array, or CheckFilename.

Some programmers prefer using sentencelike names that provide a complete description of the procedure. Some examples include WriteReportToTextFile and Get_Print_Options_and_Print_Report. The use of such lengthy names has pros and cons. On the one hand, such names are descriptive and usually unambiguous. On the other hand, they take longer to type. Everyone develops a naming style, but if your macro isn't just a quick-and-dirty temporary macro, it's a good idea to be descriptive and to avoid meaningless names such as DoIt, Update, Fix, and the ever-popular Macro1.

#### 5.2.1 Executing Sub procedures

Although you may not know much about developing Sub procedures at this point, it's important to know how to execute these procedures. A Sub procedure is worthless unless you know how to execute it.

By the way, executing a Sub procedure means the same thing as running or calling a Sub procedure. You can use whatever terminology you like.

You can execute a VBA Sub in many ways; that's one reason you can do so many useful things with Sub procedures. Here's an exhaustive list of the ways to execute a Sub procedure:

1 Choose Run => Run Sub/UserForm (in the VBE). Excel executes the Sub procedure in which the cursor is located. This menu command has two alternatives: the F5 key and the Run Sub/UserForm button on the Standard toolbar in the VBE. These methods don't work if the procedure requires one or more arguments.

2 Use Excel's Macro dialog box. You open this box by choosing Developer => Code => Macros or by choosing View => Macros => Macros. Or bypass the Ribbon and just press Alt+F8. When the Macro dialog box appears, select the Sub procedure you want and click Run. This dialog box lists only the procedures that don't require an argument.

3 Press Ctrl+key (or Ctrl+Shift+key) assigned to the Sub procedure (assuming you assigned one).

4 Click a button or a shape on a worksheet. The button or shape must have a Sub procedure assigned to it — which is very easy to do.

5 From another Sub procedure that you write.

6 Click a button that you've added to the Quick Access toolbar. (See Chapter 19.) From a custom item you've added to the Ribbon. (See Chapter 19.)

7 When an event occurs. As explained later in Chapter 11, these events include opening the workbook, closing the workbook, saving the workbook, making a change to a cell, activating a sheet, and other things.

8 From the Immediate window in the VBE. Just type the name of the Sub procedure and press Enter.

Some of these techniques are covered in the following sections. To follow along, you need to enter a Sub procedure in a VBA module:

1 Start with a new workbook.

2 Press Alt+F11 to activate the VBE.

3 Select the workbook in the Project window.

4 Choose Insert => Module to insert a new module.

5 Enter the following in the module:

```c
Sub ShowCubeRoot()
  Num = InputBox("Enter a positive number")
  MsgBox Num ^ (1/3) & " is the cube root."
End Sub
```

This procedure asks the user for a number and then displays that number's cube root in a message box. Figures 5-1 and 5-2 show what happens when you execute this procedure.

FIGURE 5-1: Using the built-in VBA InputBox function to get a number.

FIGURE 5-2: Displaying the cube root of a number via the MsgBox function.

By the way, ShowCubeRoot is not an example of a good macro. It doesn't check for errors, so it fails easily. Try clicking the Cancel button in the input box or entering a negative number. Either action results in an error message. Chapter 12 describes how to deal with these types of errors.

#### 5.2.2 Executing the Sub procedure directly

One way to execute this procedure is by doing so directly from the VBA module in which you defined it. Follow these steps:

1 Activate the VBE, and select the VBA module that contains the procedure.

2 Move the cursor anywhere in the procedure's code.

3 Press F5 (or choose Run => Run Sub/UserForm).

4 Respond to the input box, and click OK.

The procedure displays the cube root of the number you entered.

You can't use Run => Run Sub/UserForm to execute a Sub procedure that uses arguments, because you have no way to pass the arguments to the procedure. If the procedure contains one or more arguments, the only way to execute it is to call it from another procedure — which must supply the argument(s).

#### 5.2.3 Executing the procedure from the Macro dialog box

Most of the time, you execute Sub procedures from Excel, not from the VBE. The following steps describe how to execute a macro by using Excel's Macro dialog box:

1 If you're working in the VBE, activate Excel. Pressing Alt+F11 is the express route.

2 Choose Developer => Code => Macros (or press Alt+F8). Excel displays the dialog box shown in Figure 5-3.

3 Select the macro.

4 Click Run (or double-click the macro's name in the list box).

FIGURE 5-3: The Macro dialog box lists all available Sub procedures.

The Macro dialog box doesn't display Sub procedures that use arguments. That's because there is no way for you to specify the arguments.

#### 5.2.4 Executing a macro by using a shortcut key

Another way to execute a macro is to press its shortcut key. But before you can use this method, you must assign a shortcut key to the macro.

You have the opportunity to assign a shortcut key in the Record Macro dialog box when you begin recording a macro. If you create the procedure without using the macro recorder, you can assign a shortcut key (or change an existing shortcut key) by using the following steps:

1 Choose Developer => Code => Macros.

2 Select the Sub procedure name from the list box. In this example, the procedure is named ShowCubeRoot.

3 Click the Options button. Excel displays the Macro Options dialog box shown in Figure 5-4.

4 Click the Shortcut Key option and enter a letter in the box labeled Ctrl.

The letter you enter corresponds to the key combination you want to use for executing the macro. For example, if you enter the lowercase letter c, you can execute the macro by pressing Ctrl+C. If you enter an uppercase letter, you need to add the Shift key to the key combination. For example, if you enter C, you can execute the macro by pressing Ctrl+Shift+C.

5 Click OK to close the Macro Options dialog box and then click Cancel to close the Macro dialog box.

FIGURE 5-4: The Macro Options dialog box lets you set options for your macros.

After you've assigned a shortcut key, you can press that key combination to execute the macro. A shortcut key doesn't work if it's assigned to a macro that uses an argument.

The shortcut keys you assign to macros override Excel's built-in shortcut keys. For example, Ctrl+C is the standard shortcut key to copy data. If you assign Ctrl+C to a macro, you can't use Ctrl+C to copy. This is usually not a big deal because Excel almost always provides other ways to execute commands.

#### 5.2.5 Executing the procedure from a button or shape

Sometimes, you might like the idea of assigning the macro to a button (or any other shape) on a worksheet. To assign the macro to a button, follow these steps:

1 Activate a worksheet.

2 Add a button from the Form Controls group. To display the Form Controls group, choose Developer ➪ Controls ➪ Insert (see Figure 5-5).

3 Click the Button tool in the Form Controls group. It's the first button in the first row of controls.

4 Drag in the worksheet to create the button. After you add the button to your worksheet, Excel reads your mind and displays the Assign Macro dialog box shown in Figure 5-6.

5 Select the macro you want to assign to the button.

6 Click OK.

FIGURE 5-5: The Ribbon, showing the controls available when you click Insert on the Developer tab.

FIGURE 5-6: When you add a button to a worksheet, Excel automatically displays the Assign Macro dialog box.

After you've made the assignment, clicking the button executes the macro — just like magic.

When you add a button, note that the drop-down box shows two sets of controls: Form Controls and ActiveX Controls. These two groups of controls look similar, but they are actually very different. In practice, the Form Controls are easier to use.

You can also assign a macro to any other shape or object. For example, assume you'd like to execute a macro when the user clicks a Rectangle object. Follow these steps:

1 Add the rectangle to the worksheet. Insert a rectangle by choosing Insert ➪ Illustrations ➪ Shapes.

2 Right-click the rectangle.

3 Choose Assign Macro from its shortcut menu.

4 Select the macro in the Assign Macro dialog box.

5 Click OK.

After you've performed these steps, clicking the rectangle executes the assigned macro.

#### 5.2.6 Executing the procedure from another procedure

You can also execute a procedure from another procedure. Follow these steps if you want to give this a try:

1 Activate the VBA module that holds the ShowCubeRoot routine.

2 Enter this new procedure (either above or below ShowCubeRoot code it makes no difference):

```c
Sub NewSub()
  Call ShowCubeRoot
End Sub
```

3 Execute the NewSub macro. The easiest way to do this is to move the cursor anywhere within the NewSub code and press F5. Notice that this NewSub procedure simply executes the ShowCubeRoot procedure. By the way, the keyword Call is optional. The statement can consist of only the Sub procedure's name. However, using the Call keyword makes it perfectly clear that a procedure is being called.

#### 5.2.7 Executing Function procedures

Functions, unlike Sub procedures, can be executed in only two ways: 1) By calling the function from another Sub procedure or Function procedure By using the function in a worksheet formula. 2) Try this simple function. Enter it in a VBA module:

```c
Function CubeRoot(number)
  CubeRoot = number ^ (1 / 3)
End Function
```

This function is pretty wimpy; it merely calculates the cube root of the number passed to it as its argument. It does, however, provide a starting point for understanding functions. It also illustrates an important concept about functions: how to return the value. (You do remember that a function returns a value, right?)

Notice that the single line of code that makes up this Function procedure performs a calculation. The result of the math (number to the power of 1 ⁄3) is assigned to the variable CubeRoot. Not coincidentally, CubeRoot is also the name of the function. To tell the function what value to return, you assign that value to the name of the function.

#### 5.2.8 Calling the function from a Sub procedure

Because you can't execute a function directly, you must call it from another procedure. Enter the following simple procedure in the same VBA module that contains the CubeRoot function:

```c
Sub CallerSub()
  Ans = CubeRoot(125)
  MsgBox Ans
End Sub
```

When you execute the CallerSub procedure (using any of the methods described earlier in this chapter), Excel displays a message box that contains the value of the Ans variable, which is 5.

Here's what's going on: The CubeRoot function is executed, and it receives an argument of 125. The calculation is performed by the function's code (using the value passed as an argument), and the function's returned value is assigned to the Ans variable. The MsgBox function then displays the value of the Ans variable.

Try changing the argument that's passed to the CubeRoot function and run the CallerSub macro again. It works just like it should — assuming that you give the function a valid argument (a positive number).

By the way, the CallerSub procedure could be simplified a bit. The Ans variable is not really required unless your code will use that variable later. You could use this single statement to obtain the same result:

```c
MsgBox CubeRoot(125)
```

#### 5.2.9 Calling a function from a worksheet formula

Now it's time to call this VBA Function procedure from a worksheet formula. Activate a worksheet in the same workbook that holds the CubeRoot function definition. Then enter the following formula in any cell:

```c
=CubeRoot(1728)
```

The cell displays 12, which is indeed the cube root of 1,728.

As you might expect, you can use a cell reference as the argument for the CubeRoot function. For example, if cell A1 contains a value, you can enter =CubeRoot(A1). In this case, the function returns the number obtained by calculating the cube root of the value in A1.

You can use this function any number of times in the worksheet. Like Excel's built-in functions, your custom functions appear in the Insert Function dialog box. Click the Insert Function toolbar button, and choose the User Defined category. As shown in Figure 5-7, the Insert Function dialog box lists your very own function.

2『自定义函数作为内置函数的设置，做一张主题卡片。（2021-04-22）』—— 已完成

If you want the Insert Function dialog box to display a description of the function, follow these steps:

1 Choose Developer => Code => Macros.

Excel displays the Macro dialog box, but CubeRoot doesn't appear in the list. (CubeRoot is a Function procedure, and this list shows only Sub procedures.) Don't fret.

FIGURE 5-7: The CubeRoot function appears in the User Defined category of the Insert Function dialog box.

2 Type the word CubeRoot in the Macro Name box.

3 Click the Options button.

4 Enter a description of the function in the Description box.

5 Click OK to close the Macro Options dialog box.

6 Close the Macro dialog box by clicking the Cancel button.

This descriptive text now appears in the Insert Function dialog box.

Figure 5-8 shows the CubeRoot function being used in worksheet formulas.

By now, things may be starting to come together for you. You've found out lots about Sub and Function procedures. You start creating macros in Chapter 6, which discusses the ins and outs of developing macros by using the Excel macro recorder. And Chapter 20 reveals even more about Function procedures.
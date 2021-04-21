# 0501. VBA Sub and Function

In This Chapter: 1) Understanding the difference between Sub procedures and Function procedures. 2) Executing Sub procedures (many ways). 3) Executing Function procedures (two ways).

In the preceding chapters, you’ve seen the term Sub procedures and Function procedures. The differences between the two kinds of procedures are probably still a mystery to you at this point, but fear not. This chapter clears up any confusion you may have about these concepts.

## 5.1 Understanding Subs versus Functions

The VBA code that you write in the Visual Basic Editor is known as a procedure. The two most common types of procedures are Sub procedures and Function procedures.

A Sub procedure is a group of VBA statements that performs an action (or a sequence of actions) with Excel.

A Function procedure is a group of VBA statements that performs a calculation and returns a single value (or, sometimes, an array).

Most of the macros you write in VBA are Sub procedures. You can think of a Sub procedure as being like a command: Execute the Sub procedure, and something happens. (Of course, exactly what happens depends on the Sub procedure’s VBA code.)

A Function is also a procedure, but it’s quite different from a Sub. You’re already familiar with the concept of a function. Excel includes many worksheet functions that you use every day (well, at least every weekday). Examples include SUM, PMT, and VLOOKUP. You use these worksheet functions in formulas. Each function takes one or more arguments (although a few functions don’t use any arguments). The function does some behind-the-scenes calculations using those arguments and then returns a single value. Function procedures that you develop with VBA work the same way.

### 5.1.1 Looking at Sub procedures

Every Sub procedure starts with the keyword Sub and ends with an End Sub statement. Here’s an example:

Sub ShowMessage()

MsgBox "That's all folks!"

End Sub

This example shows a procedure named ShowMessage. A set of parentheses follows the procedure’s name. In most cases, these parentheses are empty. However, you may pass arguments to Sub procedures from other procedures. If your Sub uses arguments, list them between the parentheses.

When you record a macro with the Excel macro recorder, the result is always a Sub procedure that takes no arguments.

As you see later in this chapter, Excel provides quite a few ways to execute a VBA Sub procedure.

### 5.1.2 Looking at Function procedures

Every Function procedure starts with the keyword Function and ends with an End Function statement. Here’s a simple example:

Function CubeRoot(number) CubeRoot = number ^ (1 / 3) End Function

This function, named CubeRoot, takes one argument (a variable named number), which is enclosed in parentheses. Functions can have as many as 255 arguments or none at all. When you execute this function, it returns a single value — the cube root of the argument passed to the function.

VBA allows you to specify what type of information (also known as data type) is returned by a Function procedure. For example, a value can be a currency, date, or text string. Chapter 7 contains more information on specifying data types.

You can execute a Function procedure in only two ways: You can execute it from another procedure (a Sub or another Function procedure) or use it in a worksheet formula.

No matter how hard you try, you can’t use the Excel macro recorder to record a Function procedure. You must manually enter every Function procedure that you create.

## 5.2 Naming Subs and Functions

Like humans, pets, and hurricanes, every Sub and Function procedure must have a name. Although it’s perfectly acceptable to name your dog Hairball Harris, it’s usually not a good idea to use such a freewheeling attitude when naming procedures. When naming procedures, you must follow a few rules:

»

You can use letters, numbers, and some punctuation characters, but the first character must be a letter.

» » »

You can’t use any spaces or periods in the name.

VBA does not distinguish between uppercase and lowercase letters.

You can’t use any of the following characters in a procedure name: #, $, %, &, @, ^, *, or !. In other words, your procedure name can’t look like comic-strip curse words.

»

If you write a Function procedure for use in a formula, avoid using a name that looks like a cell address (for example, A1 or B52). Actually, Excel allows such function names, but why make things more confusing than they are already?

»

Procedure names can be no longer than 255 characters. (Of course, you would never make a procedure name this long.)

Ideally, a procedure’s name describes the routine’s purpose. A good practice is to create a name by combining a verb and a noun — for example, ProcessData, PrintReport, Sort_Array, or CheckFilename.

Some programmers prefer using sentencelike names that provide a complete description of the procedure. Some examples include WriteReportToTextFile and Get_Print_Options_and_Print_Report. The use of such lengthy names has pros and cons. On the one hand, such names are descriptive and usually unambiguous. On the other hand, they take longer to type. Everyone develops a naming style, but if your macro isn’t just a quick-and-dirty temporary macro, it’s a good idea to be descriptive and to avoid meaningless names such as DoIt, Update, Fix, and the ever-popular Macro1.

### 5.2.1 Executing Sub procedures

Although you may not know much about developing Sub procedures at this point, it’s important to know how to execute these procedures. A Sub procedure is worthless unless you know how to execute it.

By the way, executing a Sub procedure means the same thing as running or calling a Sub procedure. You can use whatever terminology you like.

You can execute a VBA Sub in many ways; that’s one reason you can do so many useful things with Sub procedures. Here’s an exhaustive list of the ways to execute a Sub procedure:

»

Choose Run ➪ Run Sub/UserForm (in the VBE). Excel executes the Sub procedure in which the cursor is located. This menu command has two alternatives: the F5 key and the Run Sub/UserForm button on the Standard toolbar in the VBE. These methods don’t work if the procedure requires one or more arguments.

»

Use Excel’s Macro dialog box. You open this box by choosing Developer ➪ Code ➪ Macros or by choosing View ➪ Macros ➪ Macros. Or bypass the Ribbon and just press Alt+F8. When the Macro dialog box appears, select the Sub procedure you want and click Run. This dialog box lists only the procedures that don’t require an argument.

» »

Press Ctrl+key (or Ctrl+Shift+key) assigned to the Sub procedure (assuming you assigned one).

Click a button or a shape on a worksheet. The button or shape must have a Sub procedure assigned to it — which is very easy to do.

From another Sub procedure that you write.

Click a button that you’ve added to the Quick Access toolbar. (See Chapter 19.) From a custom item you’ve added to the Ribbon. (See Chapter 19.)

When an event occurs. As explained later in Chapter 11, these events include opening the workbook, closing the workbook, saving the workbook, making a change to a cell, activating a sheet, and other things.

»

From the Immediate window in the VBE. Just type the name of the Sub procedure and press Enter.

Some of these techniques are covered in the following sections. To follow along, you need to enter a Sub procedure in a VBA module:

1. Start with a new workbook.

2. Press Alt+F11 to activate the VBE.

3. Select the workbook in the Project window.

4. Choose Insert ➪ Module to insert a new module.

5. Enter the following in the module:

Sub ShowCubeRoot()

Num = InputBox("Enter a positive number")

MsgBox Num ^ (1/3) & " is the cube root."

End Sub

This procedure asks the user for a number and then displays that number’s cube root in a message box. Figures 5-1 and 5-2 show what happens when you execute this procedure.

FIGURE 5-1:

Using the built-in VBA InputBox function to get a number.

FIGURE 5-2:

Displaying the cube root of a number via the MsgBox function.

By the way, ShowCubeRoot is not an example of a good macro. It doesn’t check for errors, so it fails easily. Try clicking the Cancel button in the input box or entering a negative number. Either action results in an error message. Chapter 12 describes how to deal with these types of errors.

### 5.2.2 Executing the Sub procedure directly

One way to execute this procedure is by doing so directly from the VBA module in which you defined it. Follow these steps:

1. Activate the VBE, and select the VBA module that contains the procedure.

2. Move the cursor anywhere in the procedure’s code.

3.

4.

Press F5 (or choose Run ➪ Run Sub/UserForm).

Respond to the input box, and click OK.

The procedure displays the cube root of the number you entered.

You can’t use Run ➪ Run Sub/UserForm to execute a Sub procedure that uses arguments, because you have no way to pass the arguments to the procedure. If the procedure contains one or more arguments, the only way to execute it is to call it from another procedure — which must supply the argument(s).

### 5.2.3 Executing the procedure from the Macro dialog box

Most of the time, you execute Sub procedures from Excel, not from the VBE. The following steps describe how to execute a macro by using Excel’s Macro dialog box:

1. If you’re working in the VBE, activate Excel.

Pressing Alt+F11 is the express route.

2.

3.

4.

Choose Developer ➪ Code ➪ Macros (or press Alt+F8).

Excel displays the dialog box shown in Figure 5-3.

Select the macro.

Click Run (or double-click the macro’s name in the list box).

FIGURE 5-3:

The Macro dialog box lists all available Sub procedures.

The Macro dialog box doesn’t display Sub procedures that use arguments. That’s because there is no way for you to specify the arguments.

Executing a macro by using a shortcut key

Another way to execute a macro is to press its shortcut key. But before you can use this method, you must assign a shortcut key to the macro.

You have the opportunity to assign a shortcut key in the Record Macro dialog box when you begin recording a macro. If you create the procedure without using the macro recorder, you can assign a shortcut key (or change an existing shortcut key) by using the following steps:

1. Choose Developer ➪ Code ➪ Macros.

2. Select the Sub procedure name from the list box.

In this example, the procedure is named ShowCubeRoot.

3. Click the Options button.

Excel displays the Macro Options dialog box shown in Figure 5-4.

4. Click the Shortcut Key option and enter a letter in the box labeled Ctrl.

The letter you enter corresponds to the key combination you want to use for executing the macro. For example, if you enter the lowercase letter c, you can execute the macro by pressing Ctrl+C. If you enter an uppercase letter, you need to add the Shift key to the key combination. For example, if you enter C, you can execute the macro by pressing Ctrl+Shift+C.

5. Click OK to close the Macro Options dialog box and then click Cancel to close the Macro dialog box.

FIGURE 5-4:

The Macro Options dialog box lets you set options for your macros.

After you’ve assigned a shortcut key, you can press that key combination to execute the macro. A shortcut key doesn’t work if it’s assigned to a macro that uses an argument.

The shortcut keys you assign to macros override Excel’s built-in shortcut keys. For example, Ctrl+C is the standard shortcut key to copy data. If you assign Ctrl+C to a macro, you can’t use Ctrl+C to copy. This is usually not a big deal because Excel almost always provides other ways to execute commands.

Executing the procedure from a button or shape

Sometimes, you might like the idea of assigning the macro to a button (or any other shape) on a worksheet. To assign the macro to a button, follow these steps:

1. Activate a worksheet.

2. Add a button from the Form Controls group.

To display the Form Controls group, choose Developer ➪ Controls ➪ Insert (see Figure 5-5).

Click the Button tool in the Form Controls group.

It’s the first button in the first row of controls.

Drag in the worksheet to create the button.

After you add the button to your worksheet, Excel reads your mind and displays the Assign Macro dialog box shown in Figure 5-6.

Select the macro you want to assign to the button.

Click OK.

FIGURE 5-5:

The Ribbon, showing the controls available when you click Insert on the Developer tab.

FIGURE 5-6:

When you add a button to a worksheet, Excel automatically displays the Assign Macro dialog box.

After you’ve made the assignment, clicking the button executes the macro — just like magic.

When you add a button, note that the drop-down box shows two sets of controls: Form Controls and ActiveX Controls. These two groups of controls look similar, but they are actually very different. In practice, the Form Controls are easier to use.

You can also assign a macro to any other shape or object. For example, assume you’d like to execute a macro when the user clicks a Rectangle object. Follow these steps:

1. Add the rectangle to the worksheet.

Insert a rectangle by choosing Insert ➪ Illustrations ➪ Shapes.

2. Right-click the rectangle.

3. Choose Assign Macro from its shortcut menu.

4. Select the macro in the Assign Macro dialog box.

5. Click OK.

After you’ve performed these steps, clicking the rectangle executes the assigned macro.

### 5.2.4 Executing the procedure from another procedure

You can also execute a procedure from another procedure. Follow these steps if you want to give this a try:

1. Activate the VBA module that holds the ShowCubeRoot routine.

2. Enter this new procedure (either above or below ShowCubeRoot code it makes no difference):

Sub NewSub()

Call ShowCubeRoot

End Sub

3. Execute the NewSub macro.

The easiest way to do this is to move the cursor anywhere within the NewSub code and press F5. Notice that this NewSub procedure simply executes the ShowCubeRoot procedure.

By the way, the keyword Call is optional. The statement can consist of only the Sub procedure’s name. However, using the Call keyword makes it perfectly clear that a procedure is being called.

### 5.2.5 Executing Function procedures

Functions, unlike Sub procedures, can be executed in only two ways:

» »

By calling the function from another Sub procedure or Function procedure By using the function in a worksheet formula

Try this simple function. Enter it in a VBA module:

Function CubeRoot(number)

CubeRoot = number ^ (1 / 3)

End Function

This function is pretty wimpy; it merely calculates the cube root of the number passed to it as its argument. It does, however, provide a starting point for understanding functions. It also illustrates an important concept about functions: how to return the value. (You do remember that a function returns a value, right?)

Notice that the single line of code that makes up this Function procedure performs a calculation. The result of the math (number to the power of 1 ⁄3) is assigned to the variable CubeRoot. Not coincidentally, CubeRoot is also the name of the function. To tell the function what value to return, you assign that value to the name of the function.

### 5.2.6 Calling the function from a Sub procedure

Because you can’t execute a function directly, you must call it from another procedure. Enter the following simple procedure in the same VBA module that contains the CubeRoot function:

Sub CallerSub()

Ans = CubeRoot(125)

MsgBox Ans

End Sub

When you execute the CallerSub procedure (using any of the methods described earlier in this chapter), Excel displays a message box that contains the value of the Ans variable, which is 5.

Here’s what’s going on: The CubeRoot function is executed, and it receives an argument of 125. The calculation is performed by the function’s code (using the value passed as an argument), and the function’s returned value is assigned to the Ans variable. The MsgBox function then displays the value of the Ans variable.

Try changing the argument that’s passed to the CubeRoot function and run the CallerSub macro again. It works just like it should — assuming that you give the function a valid argument (a positive number).

By the way, the CallerSub procedure could be simplified a bit. The Ans variable is not really required unless your code will use that variable later. You could use this single statement to obtain the same result:

MsgBox CubeRoot(125)

### 5.2.7 Calling a function from a worksheet formula

Now it’s time to call this VBA Function procedure from a worksheet formula. Activate a worksheet in the same workbook that holds the CubeRoot function definition. Then enter the following formula in any cell:

=CubeRoot(1728)

The cell displays 12, which is indeed the cube root of 1,728.

As you might expect, you can use a cell reference as the argument for the CubeRoot function. For example, if cell A1 contains a value, you can enter =CubeRoot(A1). In this case, the function returns the number obtained by calculating the cube root of the value in A1.

You can use this function any number of times in the worksheet. Like Excel’s built-in functions, your custom functions appear in the Insert Function dialog box. Click the Insert Function toolbar button, and choose the User Defined category. As shown in Figure 5-7, the Insert Function dialog box lists your very own function.

If you want the Insert Function dialog box to display a description of the function, follow these steps:

1. Choose Developer ➪ Code ➪ Macros.

Excel displays the Macro dialog box, but CubeRoot doesn’t appear in the list. (CubeRoot is a Function procedure, and this list shows only Sub procedures.) Don’t fret.

FIGURE 5-7:

The CubeRoot function appears in the User Defined category of the Insert Function dialog box.

2. Type the word CubeRoot in the Macro Name box.

3. Click the Options button.

4. Enter a description of the function in the Description box.

5. Click OK to close the Macro Options dialog box.

6. Close the Macro dialog box by clicking the Cancel button.

This descriptive text now appears in the Insert Function dialog box.

Figure 5-8 shows the CubeRoot function being used in worksheet formulas.

FIGURE 5-8:

Using the CubeRoot function in formulas.

By now, things may be starting to come together for you. You’ve found out lots about Sub and Function procedures. You start creating macros in Chapter 6, which discusses the ins and outs of developing macros by using the Excel macro recorder. And Chapter 20 reveals even more about Function procedures.



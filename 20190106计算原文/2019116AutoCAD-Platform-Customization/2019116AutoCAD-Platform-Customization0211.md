# 0211. Using the Visual LISP Editor (Windows only)

Up until now, when working with LSP files you have been using Notepad, which is designed primarily for creating and editing plain ASCII text files—not LSP files. The Autodesk® AutoCAD® program on Windows supports an integrated development environment (IDE) used to develop custom AutoLISP® applications. The IDE used to work with AutoLISP is called the Visual LISP® Editor and is often referred to as the VLIDE. Unlike Notepad, the Visual LISP Editor offers a range of tools that are designed specifically for working with LSP files.

In this chapter, you'll learn how to create and manage LSP files with the Visual LISP Editor. You'll also learn how to format AutoLISP statements in the editor and debug a loaded program. After a program has been debugged, it can be compiled into an FAS or VLX file to prevent someone from making changes to the original LSP file.

NOTE

If you are using Mac OS, I recommend installing Windows and AutoCAD on Boot Camp or Parallels so that you can use the Visual LISP Editor when creating or editing LSP files.

Accessing the Visual LISP Editor

You access the Visual LISP Editor from within AutoCAD by entering vlide at the Command prompt. You can also start the vlide command by clicking the Manage tab Applications panel Visual LISP Editor. Figure 21.1 shows the initial state of the Visual LISP Editor after the vlide command is started.

Figure 21.1 The Visual LISP Editor with a new LSP file open in an editor window

The Visual LISP Editor is similar to many Windows-based applications. It has a menu bar displayed along the top with toolbars placed below it that allow access to many of the tools commonly used to create, format, and debug LSP files. The large area in the middle is where you access windows for editing open LSP files and other tool-related windows.

When you display the Visual LISP Editor, any files not closed during the previous editing session are reopened automatically. The reopening of files makes it easy to pick up where you left off working on custom programs. Along with previously opened files, the Visual LISP Console and Trace windows are also displayed in a minimized state near the bottom of the Visual LISP Editor. The Visual LISP Console and Trace windows might be hidden behind one of the other opened editor windows and can be brought to the foreground using the Window pull-down menu.

Managing AutoLISP Files with the Visual LISP Editor

Creating new files in the Visual LISP Editor is similar to creating a new file in many other Windows-based programs. You create a new file by clicking the New button on the Standard toolbar or by choosing File New File. The new file is a general text file and is not assigned a specific file extension, so the new file could be used to store custom linetype definitions, hatch patterns, or AutoLISP programs. An extension is added to the filename when it is saved the first time.

You can save the file by clicking Save File on the Standard toolbar or by choosing File Save or File Save As. If the Save-as dialog box is displayed, you can specify a name and location for the file and append the desired file extension to the filename. As an alternative, you can choose a file format from the Save As Type drop-down list. Click Save to store the file to disk. Choose File Save All to save any open and changed files back to disk.

If you want to edit an existing file, click Open on the Standard toolbar or choose File Open File. When the Open File To Edit/View dialog box is displayed, browse to and select the file you want to open, and then click Open. You can use the File Of Types drop-down list to filter the files that are displayed in the Files list. Choose File Reopen and then an item from the menu to reopen a file that was previously opened.

NOTE

Choose File Revert if you want to reload a file based on the content that is in the version of the file on disk instead of in memory.

When you are done working with a file, save any changes and then click the Close button in the upper-right corner of the editor window or choose File Close. Choose File Close All to close all open files in the current editing session.

TIP

If you think you might want to continue to work with a LSP file later, leave it open in the Visual LISP Editor and simply close the editor without first closing the file. The next time the Visual LISP Editor is loaded, it reopens the file for you if it is found in its previous known location.

As you work in the Visual LISP Editor, you can take advantage of the tools on the Edit and Search menus to assist in editing and finding code in the current editor window. Many of the available tools are similar to those found in Notepad, with the exception of the Parentheses Matching and Extra Commands options on the Edit menu. I'll explain some of the items on these two submenus later in this chapter.

Although the Visual LISP Editor offers many tools that differentiate it from Notepad, one of my favorite tools is the Apropos window (see Figure 21.2, on the left). The Apropos window allows you to obtain a listing of the AutoLISP functions and variables that are defined in the current drawing. Display the Apropos window by clicking Apropos on the View toolbar or by choosing View Apropos Window. After the window is displayed, enter a text string that matches part of the function or variable names you want to list and click OK. The matching results are displayed in the Apropos Results window (see Figure 21.2, on the right).

Figure 21.2 Searching for defined functions and variables

Formatting an AutoLISP File

Editor formatting is one of the key advantages of using the Visual LISP Editor over Notepad. The Visual LISP Editor supports the following features that help you to author and format code:

Color syntax

Automatic indenting

Ability to format code by selection or in the editor window

Comments

Coloring Syntax

The Visual LISP Editor supports color syntax, which helps to distinguish function names from argument values. Color is also used to help distinguish values based on the data type; strings are displayed in magenta, integers are displayed in green, and real numbers are displayed in teal. Many modern development environments, such as Microsoft Visual Studio, also support color syntax. Figure 21.3 shows the badcode function from Chapter 19,「Catching and Handling Errors,」open in the Visual LISP Editor.

Figure 21.3 Color syntax allows you to quickly identify functions, argument values, and problems in a program.

Although the color of the characters doesn't come through in black and white, you should notice that the second statement shown in Figure 21.3 is a comment and its background is shaded to help you visually distinguish it from other statements in the program. When the Visual LISP Editor detects an error in the syntax within an open LSP file, the color syntax applied to code can be affected. The change in the color syntax indicates an error.

In Figure 21.3, a quotation mark is missing from the (princ "DEBUG: Inside IF) statement. The missing quotation mark affects the color syntax of all the statements that are after it. Notice most of the statements after the missing quotation mark are also displayed in a gray color, such as the string of the (setq str (getstring "\nEnter a string: ")) statement. As you can see, color syntax can also be helpful in identifying problems in a program and thereby it reduces the amount of debugging that you have to perform.

You can adjust the colors that the Visual LISP Editor applies to the editor window by choosing Tools Window Attributes Configure Current. In the Window Attributes dialog box (see Figure 21.4), click the element drop-down list and choose the element you want to format. Then select a foreground (top row) and background (bottom row) color to apply to the element. Choose Transparent FG or Transparent BG to match the background color of the editor window. Clear the Lexical Colors check box to remove the color from all text elements.

Figure 21.4 Setting element colors to be used in the editor window

You can also set the number of characters that a tab character represents and the left margin of the editor window (in pixels) by changing the values of the Tab Width and Left Margin text boxes in the Window Attributes dialog box.

Formatting Code

Code formatting isn't something you have to do; AutoCAD and AutoLISP don't care whether all code is placed on a single line or is nicely formatted. Formatting code is a benefit for you, the programmer, because it makes code easier to read and helps you identify missing or extra parentheses. When writing code in Notepad, you have to manually add spaces and indents to make your code easier to follow.

The Visual LISP Editor provides several features designed to format code as you type it in the editor window, or you can specify that you'd like to base the formatting on the code that was previously entered. When you start a statement by typing an opening parenthesis and then press Enter without adding the closing parenthesis on the same line, the Visual LISP Editor indents the next line to signal that the new line is a continuation of the current expression. You can specify the size of the indent with the Narrow Style Indentation value in the Format Options dialog box (see Figure 21.5). To open this dialog box, choose Tools Environment Options Visual LISP Format Options.

Figure 21.5 Specifying the settings to format code in the editor window

In the Format Options dialog box, specify the settings for the Visual LISP Editor formatting tools. Click the More Options button to access additional formatting settings. Once the formatting options are set, click Format Edit Window on the Tools toolbar or choose Tools Format Code In Editor to format all the code in the current editor window. If you want to format only some of the code, select the code you want to format and click Format Selection on the Tools toolbar or choose Tools Format Code In Selection.

NOTE

When you format all of the code in the editor window, the Visual LISP Editor will notify you if it finds a problem with a missing or extra parenthesis.

Commenting Code

Comments are commonly added by you as the programmer, as I explained in Chapter 20,「Authoring, Managing, and Loading AutoLISP Programs.」The Visual LISP Editor can format the comments that have been added to an AutoLISP program based on the settings in the Format Options dialog box, and it can also add what are called form-closing comments.

Form-closing comments are added after the closing parentheses of specific functions, such as defun, if, and progn. The comments let you know the location in the code of the closing parenthesis for functions to assist you in the debugging of a program. Select the Insert Form-Closing Comment option and type the prefix for the comment in the Form-Closing Comment Prefix text box of the Format Options dialog box (choose Tools Environment Options Visual LISP Format Options). Form-closing comments are added when you use the Format Edit Window or Format Selection tool discussed in the previous section.

In addition to adding form-closing comments, you can mark selected statements in the current window as comments. Select the statements to be marked as comments, and then click Comment Block on the Tools toolbar or choose Edit Extra Commands Comment Block. The Visual LISP Editor places three semicolons (;;;) in front of each of the selected statements. Click Uncomment Block or choose Edit Extra Commands Comment Block to uncomment selected statements. The Uncomment Block tool removes only the semicolons that are located at the left margin of the editor window—indented comments are ignored.

Validating and Debugging Code

The benefits of the Visual LISP Editor extend beyond being able to view code in color, use automatic formatting, and insert comments based on the way your code was written. Since the Visual LISP Editor was designed to be a proper development environment, it offers the following functionality that can be used to validate, load, and debug code:

Execute AutoLISP statements without returning to the AutoCAD Command prompt

Load and check the code in a LSP file

Debug the code in the current editor window

Executing Code from the Visual LISP Editor

The Console window (see Figure 21.6) is an extension of the AutoCAD Command prompt; it allows AutoLISP statements to be executed in real time from the Visual LISP Editor. When you type an AutoLISP statement in the Console window and press Enter, the value of the last evaluated function is returned to the Console window and not the AutoCAD Command prompt. AutoLISP statements entered in the Console window follow the same rules as statements entered at the AutoCAD Command prompt, with one exception: user-defined variables don't need to be prefixed with an exclamation point to get the current value.

Figure 21.6 Use the Console window to execute AutoLISP statements.

The Console window is opened in a minimized state by default, but you can choose Window Visual LISP Console to bring the window to the foreground. At the _$ prompt, type the statement you want to execute and press Enter. You can press Shift+Enter to move input to the next line, but the statements won't be executed until you press Enter. Right-click in the Console window to clear the window or to enable logging.

NOTE

Focus is shifted away from the Visual LISP Editor and to AutoCAD when you execute a function from the Console window that requires user input.

Checking and Loading Code in the Current Editor Window

The ability to check code and perform parentheses matching in code is an important feature that makes the Visual LISP Editor more efficient than Notepad. Once you are done checking the code in your programs, you can load all the code or just the code that is selected in the current editor window.

Checking Code

The code-checking tool validates that the code in the current editor window will load successfully into AutoCAD and even checks for too many or too few arguments being passed to the functions used in the code. However, the argument values being passed to a function aren't checked. You can use code checking in one of two ways:

To check the code in the current editor window, click Check Edit Window on the Tools toolbar or choose Tools Check Text In Editor.

If you don't want to check all of the code in the current editor, select the code you want to check and click Check Selection on the Tools toolbar or choose Tools Check Selection.

Checking stops when an error is encountered or when the file has been successfully checked. The Visual LISP Editor then displays the Build Output window. If an error was encountered during checking, an error message and the faulty code are displayed in highlighted text (see Figure 21.7). Double-clicking the highlighted text in the Build Output window causes Visual LISP to highlight the faulty code in the editor window as well.

Figure 21.7 The Build Output window indicates the type of error encountered during checking.

Matching Parentheses

Keeping parentheses balanced in AutoLISP programs is an ongoing challenge. The Visual LISP parentheses-matching tools can help you identify a missing parenthesis. You can either select code between two balanced parentheses or move the cursor between matching parentheses. If you suspect you are missing a parenthesis, you can step through the code, matching parentheses to see if (and where) an opening or closing parenthesis is missing. When you select a Parentheses Match option, Forward moves the cursor toward the end of the file, whereas Backward moves the cursor toward the beginning of the file. If Parentheses Match or Parentheses Select cannot find the balancing parenthesis, Visual LISP sounds an audible bing. The cursor is not moved; no code is selected.

Playground Disaster to Incomplete Code

To save time and typos, you are copying and pasting partial code statements from another program when you get a call from your child's school. Your daughter fell off the monkey bars and needs stitches. You save your work, go pick up your child, rush off to the emergency room, soothe her while she's being stitched up, take her home, and don't get back to work until the next day.

The fact that you pasted partial code statements and didn't get to adding balancing parentheses (or removing the excess ones) before the call came in has completely slipped your mind. Out of habit, you open Visual LISP and, before adding any more code, you select the code block you added last and run Check Selection. Since the copy and paste left your program with three extra closing parentheses, an error message appears in the Build Output window. Starting at the end of the new code block, the Parentheses Match tools allow you to quickly step backward through the code, identify the partial code statements, and repair your code to working order.

Here's how you can use the Visual LISP parentheses-matching tools:

To Find the Balancing Parenthesis for a Closing Parenthesis Click immediately before a closing parenthesis that you want to match. With the cursor positioned within the code in the current editor window, choose Edit Parentheses Match Match Backward. Visual LISP identifies the matching opening parenthesis.

To Find the Balancing Parenthesis for an Opening Parenthesis Click immediately after an opening parenthesis that you want to match. With the cursor positioned within the code in the current editor window, choose Edit Parentheses Match Match Forward. Visual LISP identifies the matching closing parenthesis.

To View the Code between Matching Parentheses Click immediately after a closing parenthesis and then choose Edit Parentheses Match Select Backward. Or click immediately before an opening parenthesis and then choose Edit Parentheses Match Select Forward. Visual LISP selects the matching parentheses and the code between.

TIP

You can double-click in front of or after a parenthesis to have the Visual LISP Editor select the code between the adjacent parenthesis and the balancing parenthesis (the same as choosing Edit Parentheses Select Forward or Select Backward).

Loading Code

You can load the code in the current Visual LISP Editor window directly into AutoCAD. There is no need to use one of the methods for loading LSP files that I discussed in Chapter 20; you don't need to copy and paste the code to the AutoCAD Command prompt. Click Load Active Edit Window on the Tools toolbar or choose Tools Load Text In Editor to load all of the code in the current editor window.

If you want to load only specific statements from the current editor window, select the code you want to load and click Load Selection on the Tools toolbar or choose Tools Load Selection. After the code is loaded, switch to AutoCAD and use the loaded code. You can switch to AutoCAD from the Visual LISP Editor by clicking Activate AutoCAD on the View toolbar, by choosing Window Activate AutoCAD, or by clicking the AutoCAD icon on the Windows taskbar.

Debugging Code

In addition to the formatting and checking tools that I have already covered in this chapter, the Visual LISP Editor supports a variety of debugging tools that can make locating and resolving problems easier within a program. The following explains several of the debugging tools that are available:

Breakpoints Breakpoints allow you to interrupt the execution of a program that is loaded into the Visual LISP Editor and being executed in AutoCAD. When execution is interrupted, you can evaluate the values that have been assigned to variables and step through the remainder of the statements in the program to identify problems in real time. Position the cursor where you want to insert a breakpoint (typically immediately before an opening parenthesis), right-click, and choose Toggle Breakpoint from the context menu. The parenthesis is highlighted in red at the point where the program will be interrupted. After the breakpoint is set, execute the program in AutoCAD. Breakpoints set by the Visual LISP Editor work only while the program is open in the Visual LISP Editor window.

Once execution is interrupted, you can use Step Into, Step Over, and Step Out on the Debug toolbar to step through a program statement by statement.

Choose Step Into when you want to step through and evaluate all expressions of a code statement, even nested expressions.

Use Step Over when you want to evaluate a code statement as a whole and are not interested in stepping through each nested expression one at a time.

The Step Out tool resumes normal execution and ignores any further breakpoints that are set.

When you are finished, click Continue to resume normal execution until the next breakpoint is set, if one has been set, or click Reset to stop execution and abort the function that is currently interrupted. Continue and Reset are also located on the Debug toolbar. The Step Into, Step Over, Step Out, Continue, and Reset (Quit) options can also be found on the Debug menu.

Watch Window The Watch window allows you to see the current value assigned to a global or local variable while code is being executed from the Visual LISP Editor. You can see only the current value of a local variable when execution is paused by a breakpoint. You can add to the Watch window the variables or statements, known as watches, for which you want to see the current value by selecting and right-clicking the code in the editor window and then choosing Add Watch. A watch can be added before execution is started or while execution is paused by a breakpoint. If the Watch window isn't displayed, click Watch Window on the View toolbar or choose View Watch Window.

Error Trace and Last Error Source Often when you are trying to debug a program, you aren't always sure where an error occurred. The Visual LISP Editor can help you identify the code that caused the error. Choose View Error Trace to get information about the last error that occurred. In the Error Trace window, double-click each entry in the window to learn more about the error that occurred. Use the Last Error Source option on the Debug menu to select the code that caused the error.

You will have a chance to use all three of these debugging features later in this chapter in the「Exercise: Working with the Visual LISP Editor」section.

Table 21.1 lists some of the other debugging tools that the Visual LISP Editor offers. You can learn more about these debugging tools in the AutoCAD Help system.

Table 21.1 Additional Visual LISP Editor debugging tools

Tool Description

Break On Error Suspends execution when an error occurs and allows you to evaluate variable values and code statements to identify the origin of the error. Choose Debug Break On Error to toggle the option.

Animate Slows the execution of a custom program so it can be watched in real time. Choose Debug Animate to toggle the option. You can adjust the delay between statements by choosing Tools Environment Options General Options, clicking the Diagnostics tab, and specifying a new value in the Animation Delay text box. When the program is executed, the execution is similar to what happens if you manually click Step Into all the way through a program.

Inspect Window Displays additional information about a symbol, value, or expression in a window.

Trace Stack Window Traces the use of a function during the execution of a program. Trace Stack Window is a modernized version of the trace and untrace functions discussed in Chapter 19.

Browsing the Objects in a Drawing

The Visual LISP Editor also provides a few tools that allow you to step through and evaluate the graphical and nongraphical objects in a current drawing. Access these tools by choosing View Browse Drawing Database and then selecting the option that lets you work with the objects you are interested in.

Creating a Visual LISP Project

The Visual LISP Editor supports a concept known as projects. Projects are a means of grouping related program and data files. Projects are optional, but they can make opening and managing multiple LSP and other resource files easy. You create a project by choosing Project New Project and then specifying a location and name for the project in the New Project dialog box.

In the Project Properties dialog box (see Figure 21.8), on the Project Files tab, you specify the files that you want to be part of the project and the order in which they should be loaded. Click the ellipsis button next to the Look In text box to specify the folder that contains the files you want to add to the project. Select a file from the list and click the > button to add the file to the project, or click the < button to remove a file from the project. Use the Top, Up, Down, and Bottom buttons to set the load order of the files in the project when compiled.

Figure 21.8 Organizing LSP files into a project

The Build Options tab allows you to control compilation, merge files, and specify message modes along with the output locations for the project when it is compiled into an FAS file. An FAS file is a secure and faster-loading alternative to LSP files that doesn't allow editing. AutoCAD will always try to load an FAS file in place of a LSP file, unless the LSP file is newer. A project can also be built into a standalone AutoCAD application known as a VLX file.

A VLX file is secure, like an FAS file, but it can also be used to combine multiple program and resource files in a single file that can be loaded into AutoCAD. (You can learn more about creating VLX files in the next section.) I recommend leaving the settings alone since they are the best options for most programs, but feel free to experiment with them. You can learn more about these settings in the AutoCAD Help system. Click OK to create the new project (PRJ) file. Once you create a new project or open one (by choosing Project Open Project), the project window opens (see Figure 21.9) with the name of the project displayed in the window's title bar.

Figure 21.9 Accessing files from the project window

The project window allows you to do the following:

Change the properties of a project

Open a file by double-clicking it from the Files list in the main area of the project window

Add files to a project

Load and check the syntax of a file

Load a selected LSP or FAS file

Build FAS files for each LSP file in the current project

Close and save a project

The toolbar displayed along the top of the project window gives you access to commonly used tools. Additional tools are available via context menus that open when you right-click a file or an empty area in the project window.

Once you've added files to your project and specified the project's settings, choose Project Build Project FAS to compile the LSP files into FAS files—one FAS file for each LSP file by default. Then, review the output locations in the Build Output window to determine where the generated files were placed. The Visual LISP Editor places the FAS files in the same folder as the PRJ file unless you specified a different location in the Project Properties dialog box. Once an FAS file has been built, you can load the file using the same methods described in Chapter 20 for loading a LSP file.

Compiling LSP and PRJ Files into a VLX File

You've seen that a LSP file can be compiled into an FAS file after it has been added to a PRJ file. You can also combine and compile LSP and PRJ files into a VLX file by using the New Application wizard. Unlike FAS files, VLX files can also contain the resource files that the LSP or FAS files require. Resource files can be TXT files (data sources) or DCL files, which are used to implement dialog boxes with an AutoLISP program. I cover creating dialog boxes for AutoLISP in Chapter 23,「Implementing Dialog Boxes (Windows only).」

NOTE

Check with your company's IT department before compiling and distributing your LSP files and projects as VLX files. Some companies don't allow VLX files on their network simply because of the associations they have with some computer viruses and the inability to see the code in the files. However, LSP and FAS files have also been known to be used to spread computer viruses. Use the security features Autodesk offers in the latest releases of AutoCAD, such as the Trusted Locations option in the Options dialog box, to help prevent the loading and execution of malicious code.

To generate a VLX file, choose File New Application Wizard. The New Application wizard offers two modes: Simple and Expert. The following steps describe how to create a VLX file using the Expert mode:

Start the New Application wizard in Expert mode.

On the Application Directory page, specify a location and name for the application. Click Next.

If you wish to protect your application's namespace, select the Separate Namespace option on the Application Options page. If not, leave the option unchecked. Click Next. When you select the Separate Namespace option, the wizard will create a separate namespace for the functions and variables in your custom program. That way, when you load the VLX file they are not overwritten by AutoCAD-defined functions and variables that have the same name.

On the LISP Files To Include page, select the LSP, FAS, or PRJ files that you want to add to the application and set the load order for the files. Click Next.

If you have LSP, FAS, PRJ, DCL, or TXT files that you want to add as resources for the application, select them on the Resource Files To Include page. Resources are optional; you do not need to select any files. When you are finished, click Next.

On the Application Compilation Options page, select Standard. Optionally, you can choose Optimize and Link, which might provide your program with better performance. When you are finished, click Next.

On the Review Selections/Build Applications page, select the Build Application check box and click Finish. The wizard saves the application make (PRV) file and builds the VLX file.

You can use the other options under File Make Application to load and rebuild a VLX file from an existing PRV file. The original files that were added to the PRV file must still be available, though. Once you've built a VLX file, you can load it using the same methods described in Chapter 20 for loading a LSP file.

Exercise: Working with the Visual LISP Editor

In this section, you will take another look at the badcode function from Chapter 19 to demonstrate some of the AutoLISP functions for debugging a program. You will also have an opportunity to continue to work with the drawplate function originally introduced in Chapter 12,「Understanding AutoLISP.」The key concepts I cover in this exercise are:

Formatting, Checking, and Debugging Code The Visual LISP Editor provides many great features that assist you in formatting and checking code. The formatting and checking tools also provide a basic level of debugging tools to ensure the structure of your code is sound.

Stepping Through and Inspecting Code Although the debugging techniques I described in Chapter 19 are essential, breakpoints—which allow you to interrupt and then step through your code—can be great time-saving tools. While a program is interrupted, the Visual LISP Editor also lets you inspect code and variable values in real time.

Organizing LSP Files into a Project Projects make accessing your LSP files much easier compared to having to browse for and open each file that you want to access. Files added to a project can also be compiled to secure your custom programs from users who shouldn't be making changes to them.

NOTE

The steps in this exercise depend on the completion of the steps in the「Exercise: Handling Errors in the drawplate Function」section of Chapter 19. If you didn't complete the steps, do so now or start with the ch21_drawplate.lsp and ch21_utility.lsp sample files available for download from www.sybex.com/go/autocadcustomization. Place these sample files in the MyCustomFiles folder within the Documents (or My Documents) folder or in the location you are using to store the LSP files. Once you've stored the sample files on your system, remove the characters ch21_ from each filename.

Formatting, Checking, and Debugging the badcode Function

Often when you start a new project, formatting code takes a backseat to the actual problem you are trying to solve. However, once you encounter a problem within your code, you will understand why accomplished programmers spend time formatting their code. Once the code is formatted, checking it is much easier since you can visually determine where a parenthesis or quotation mark is missing.

The following steps explain how to format, check, and debug the badcode function for problems, and then fix those problems:

At the AutoCAD Command prompt, type vlide and press Enter.

In the Visual LISP Editor, choose File Open File.

When the Open File To Edit/View dialog box is displayed, browse to either the MyCustomFiles folder within the Documents (or My Documents) folder or the location of the exercise files for this book. Select the ch21_debuggingex.lsp file and click Open. The code in the editor window should look like the code shown on the left side of Figure 21.10. By the end of this exercise, it will look like the code on the right—and you won't have had to format each line one at a time.

Choose Tools Format Code In Editor. An Info message box appears with the message Formatting stopped:Unbalanced token. This is the result of a missing closing parenthesis. Click OK to close the message.

Figure 21.10 Unformatted and formatted code

The formatting tools available through the Visual LISP Editor work only with code that has valid structure and can be loaded into AutoCAD. Use the next steps to troubleshoot and repair the code so it can be properly formatted:

With the ch21_debuggingex.lsp file open in the current editor window, choose Tools Check Text In Editor.

In the Build Output window, double-click the highlighted error message ; error: malformed string on input. You are returned to the badcode function editor window, but the text it highlights is not exactly near the problem since the Visual LISP Editor simply counts quotation marks to determine balance. Most of the text in the editor window is displayed in the color (magenta is the default) applied to the string data type as a result of a missing quotation mark.

Find the code (getstring "\nEnter a string: ) and change it to (getstring "\nEnter a string: "). Notice that the text color changes as a result of adding the missing quotation mark.

Choose File Save.

In the next steps, you'll locate and add a missing parenthesis:

Choose Tools Check Text In Editor.

In the Build Output window, double-click the highlighted error message ; error: malformed list on input. You are returned to the badcode function editor window, and now all of the text is highlighted, indicating a closing parenthesis is missing.

Click after the last parenthesis of the badcode function and then choose Edit Parentheses Matching Select Forward. Notice the code is selected backward to the statement that starts with (if str instead of balancing the defun function. The missing parenthesis is somewhere inside the highlighted text.

Double-click to the right of the closing parenthesis that is located above the (princ) code statement. Notice the code is selected backward to the statement that starts with (progn instead of balancing the (if str statement.

Double-click to the right of the closing parenthesis that is located above the one you clicked to the right of in step 4. The (if int (prompt (strcat "\nDivisor: " (rtos (/ 2.0 int)))) code statement and the closing parenthesis are selected.

Double-click to the right of the (if int (prompt (strcat "\nDivisor: " (rtos (/ 2.0 int)))) code statement. Only part of the code statement is highlighted now: (prompt (strcat "\nDivisor: " (rtos (/ 2.0 int)))).

Add a closing parenthesis at the end of the (if int (prompt (strcat "\nDivisor" (rtos (/ 2.0 int)))) statement to balance out the statement.

Choose File Save.

In the next steps, you'll identify and address a problem related to passing too many arguments to a function:

Choose Tools Check Text In Editor.

In the Build Output window, double-click the highlighted error message ; warning: too many arguments: (PROMPT "\nValue entered: " STR). You are returned to the badcode function editor window and the bad statement is now selected.

Change (prompt "\nValue entered: " str) to (prompt (strcat "\nValue entered: " str)).

Choose Tools Check Text In Editor. No error is returned this time, so the code can now be formatted.

Close the Build Output window and choose Tools Format Code In Editor.

Choose File Save. The results you get should be similar to those shown on the right side of Figure 21.10.

Stepping Through and Inspecting the badcode Function

In this exercise, you'll continue to work with the ch21_debuggingex.lsp file that you checked, formatted, and performed some basic debugging on already in the previous section. Stepping through code line by line allows you to visually identify what is happening in your code, whether it is executing as expected or if an error occurs, and see which branches of a program are being followed based on the results of the logical tests. Additionally, you can view the current values of the variables in the program at specific times to ensure they have the correct data before they are passed to a function.

The following steps explain how to set a breakpoint, step through code, and view the current value of a variable:

Open the Visual LISP Editor and the ch21_debuggingex.lsp file if they are not already open.

In the editor window, locate and click immediately before the statement that starts with (setq str.

Right-click and choose Toggle Breakpoint to add a breakpoint to the opening parenthesis of the statement. The opening parenthesis should change color and appear in a colored background (white text on a red background is the default); this indicates that a breakpoint has been set (see Figure 21.11).

Locate and add a breakpoint to the opening parenthesis of the statement that starts with (if int.

Choose Tools Load Text In Editor.

Switch to AutoCAD.

At the Command prompt, type badcode and press Enter. Execution of the function starts and the Visual LISP Editor is brought back to the foreground when execution is interrupted at the first breakpoint. You can tell execution has been interrupted because the line of code with the first breakpoint is selected, but also because the tools on the left side of the Debug toolbar are now enabled, as shown in Figure 21.12.

Select the text str in the statement that starts with (setq str. Right-click and choose Add Watch. If the Add Watch dialog box is displayed, click OK. The Watch window is displayed and lists the str variable and its current value (see Figure 21.13).

NOTE

You can remove variables from the Watch window. Select the variable in the Watch window that you wish to remove, right-click, and choose Remove From Watch.

Select the text int in the statement that starts with (setq int and right-click. Choose Add Watch. If the Add Watch dialog box is displayed, click OK.

On the Debug toolbar, click Step Into (or choose Debug Step Into) twice. Evaluation of the statement is moved to the inner list, (getstring "\nEnter a string: "), and then the statement is evaluated. Focus shifts to AutoCAD; if it doesn't, you might not have clicked Step Into enough times.

At the Enter a string: prompt, type debug and press Enter.

The Visual LISP Editor becomes the focus. Click Step Into again. In the Watch window, the value of the str variable is now shown as debug instead of its previous value of nil.

On the Debug toolbar, click Continue (or choose Debug Continue).

At the Enter an integer: prompt, type 0 and press Enter.

On the Debug toolbar, click Step Over (or choose Debug Step Over). As a result of trying to divide 2 by 0, an error occurred and the program stopped executing. You can tell an error occurred because the text _1$ is displayed in the Visual LISP Console window. _1$ indicates that the program was left in debugging. The Reset button on the Debug toolbar is also still activated, another sign that debugging is still available and that the program didn't end successfully.

NOTE

Remember that Step Over evaluates all nested statements as a whole and doesn't step you through each nested statement one at a time. You could have clicked Step Into in the previous step, but it would take using Step Into more than 10 times to get through the code.

Choose View Error Trace. When the Error Trace window opens, information about the most recent error that occurred in AutoLISP is displayed (see Figure 21.14). Typically, the first entry represents the error message; it is followed by the statement and function name where the error occurred.

In the Error Trace window, double-click the first entry. A message box with the message :ERROR-BREAK: divide by zero is displayed. This is similar to the message you would see at the AutoCAD Command prompt. Click OK.

TIP

To resolve this problem, you should add an if statement to the code to ensure that the program never tries to divide by 0. Adding this code to the program is beyond the scope of this exercise.

In the Error Trace window, right-click the second entry; (/ 2.0 0). Choose Call Point Source. The statement that caused the error is highlighted.

Choose View Breakpoints Window. When the Breakpoints window is displayed, click Delete All. All the breakpoints you set earlier are removed.

Choose Window Activate AutoCAD and execute the badcode function again. Enter the values debug and 2 this time. The function completes as expected and the output from the function is displayed in the command-line window.

Figure 21.11 Breakpoint set in the editor window

Figure 21.12 Execution paused as a result of a breakpoint

Figure 21.13 Watching variable values with the Watch window

Figure 21.14 Viewing information about the recent error

Creating and Compiling a Project

Projects make it easy to access your LSP files or those that are related to a set of functions. Although creating a project is optional, doing so can save you some time managing complex programs by making everything available from a single place, especially since files need to be opened in the Visual LISP Editor to take advantage of the editor's debugging tools.

The following steps explain how to create a project for the drawplate function:

At the AutoCAD Command prompt, type vlide and press Enter.

In the Visual LISP Editor, choose Project New Project.

When the New Project dialog box is displayed, browse to either the MyCustomFiles folder within the Documents (or My Documents) folder or the location where you stored the exercise files for this book.

In the File Name text box, type drawplate and click Save.

When the Project Properties dialog box is displayed, click the ellipsis button to the right of the Look In text box. Browse to the folder you specified in step 3.

Choose Drawplate and Utility from the Files list box (located on the left, below the Look In text box) and click >.

Click OK.

In the DrawPlate project window, double-click the DrawPlate item. Notice the file is opened in an editor window and is ready for you to make changes.

In the editor window, change (load "utility.lsp") to (load "utility") so that AutoCAD loads the FAS or LSP file if either is found. You will remember that AutoCAD will always try to load an FAS file in place of a LSP file, unless the LSP file is newer.

On the toolbar of the DrawPlate project window, click Build Project FAS.

Switch to AutoCAD and create a new drawing. Load the drawplate.fas file with the appload command.

TIP

The FAS file should be placed in the same folder as the project. If you cannot find the file, return to the Visual LISP Editor and review the path location of the FAS file in the Build Output window.

At the Command prompt, type drawplate and press Enter. Follow the prompts that are displayed. The plate should be created as expected.
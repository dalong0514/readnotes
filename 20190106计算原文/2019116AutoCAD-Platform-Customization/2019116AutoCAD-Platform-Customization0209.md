# 0209. Catching and Handling Errors

As a veteran AutoLISP® programmer looking back over the past 15 years, I realize writing a custom program wasn't always the difficult part for me. The part of application development that didn't come so naturally was predicting the unexpected. Programs are written based on a set of known criteria, which might include the current values assigned to system variables when the program was created, a specific set of steps that the user should follow, and what the end result should be. However, as in life, your program will have to handle a curve ball every now and then.

As a programmer, you must learn to locate problems—errors or bugs, as programmers commonly refer to them. If you hang around programmers, you might have heard the term debugging, which is the industry-standard term used for the process of locating and resolving problems in a program. Conditional statements can be used to identify and work around potential problems by validating values and data types used in a program. As a last resort, a custom error handler can be used to catch an error and exit a program cleanly.

Identifying and Tracking Down Errors

Writing a program takes time, but what can often take more time is identifying why a program is not working correctly—or at all. Figuring out a problem within a custom program can drive you crazy; after all, the problem is right there in the code you wrote.

NOTE

Sometimes finding a peer, or someone else in the industry, who can review your code can be helpful in finding the problem. If you don't know a specific individual who is willing to review your code, try visiting sites such as www.theswamp.org, www.augi.com, and forums.autodesk.com for some help.

Debugging is a skill that is honed over time, and it is something you start learning on your first day of writing AutoLISP—or any programming language, for that matter. These basic techniques can be useful in debugging an AutoLISP program:

Executing a program one line at a time by pasting code at the Command prompt

Displaying messages at the command line during execution

Tracing a function and the values it is passed

TIP

On Windows, the Visual LISP Integrated Development Environment (VLIDE) that comes with AutoCAD provides additional tools that can be helpful when debugging an AutoLISP program. I cover the VLIDE in Chapter 21,「Using the Visual LISP Editor (Windows only).」

Putting Your Code Under the Microscope

Errors in an AutoLISP program aren't specific to any particular type of programmer; even the most veteran AutoLISP programmer can miss something in their code. The advantage a veteran programmer does have over those who are new to AutoLISP programming is an understanding of what to look for. When your program won't load, there are several things you should look at to try to fix the error. The following common errors are often responsible when your program does not load:

Missing Closing Parenthesis It is common to miss one or more closing parentheses when you are working on a program. AutoLISP displays (_> or ; error: malformed list on input at the Command prompt to let you know you have more opening than closing parentheses. One opening parenthesis is displayed for each closing parenthesis that is needed when(_> is displayed. For example, (((_> indicates you need to add three closing parentheses to your program. The closing parentheses that are missing might or might not be together in the code. The resolution is to go through your code line by line, add the correct number of missing closing parentheses, and then try reloading the program.

Missing Opening Parenthesis Much less common is a missing opening parenthesis, but it can happen. If you move lines of code around, a parenthesis could be overlooked. AutoLISP displays the error message ; error: extra right paren on input when there are more closing parentheses than opening in your program. The resolution again is to go through your code line by line, add the missing opening parentheses or remove the extra closing parentheses, and then try reloading the program.

Missing Quotation Mark Strings that are missing a beginning or ending quotation mark will cause a problem when trying to load a program. AutoLISP will display (("_> at the Command prompt when this condition is encountered. If you are trying to display a quotation mark in a string, make sure you add the correct control sequence of \". The resolution is to find and add the missing quotation mark and then try reloading the program.

Bad Argument Type One of the most obscure problems to track down in an AutoLISP program that won't load is related to a bad value. Typically, AutoLISP displays the error message ; error: bad argument type: consp or ; error: extra cdrs in dotted pair on input when you have dotted pairs in your program that aren't structured correctly. The resolution is to locate the dotted pairs in your program and verify that they are structured correctly.

TIP

When adding a new function or line of code to an AutoLISP program, consider adding an opening and closing parenthesis right away before typing a function or argument value. If you are adding a string, add both the beginning and ending quotation marks to ensure you don't forget one of them. Following these tips will help to keep your parentheses and quotation marks balanced and avoid some of the errors I previously described.

Figure 19.1 shows a logic tree or analysis flowchart that you can refer to when troubleshooting and debugging problems in an AutoLISP file that won't load.

Figure 19.1 Troubleshooting and debugging loading problems

Once your program is loaded, you might still encounter problems. AutoLISP doesn't validate whether a function exists or is being passed an appropriate value when it loads a program; it just checks for a valid structure and proper syntax. The following are common problems that you might encounter when executing a program:

Bad Function AutoLISP displays the message ; error: bad function: <function_name> at the Command prompt when it encounters a function name it doesn't understand. This could be the result of a misspelled name or a space missing between a function name and the first argument. The resolution is to search on the value after the colon in the AutoLISP program to locate the bad function name, and fix the name before reloading the program. If the function name is spelled correctly and the syntax is correct (no missing spaces), make sure that the program file that defines the function is loaded into AutoCAD.

Bad Argument Type Unlike when you load an AutoLISP program and get the ; error: bad argument type message, this problem is often the result of trying to pass a function an unexpected value. The best technique to use is to display multiple messages throughout your custom program to isolate just where the error occurs. I explain how to add messages to a program for debugging purposes in the next section.

Too Few/Too Many Arguments Functions expect a specific number of arguments; too few or too many results in an error. When AutoLISP displays the message ; error: too few arguments or ; error: too many arguments, check the number of arguments that is being passed to each function. Adding messages to a program can be helpful in identifying which statement is causing the error. I explain how to add messages to a program for debugging purposes in the next section.

Figure 19.2 shows a logic tree or analysis flowchart that you can refer to when troubleshooting and debugging problems in an AutoLISP file that loads, but doesn't execute.

Figure 19.2 Troubleshooting and debugging execution problems

Displaying Messages During Execution

Using messaging functions to locate which statements in a custom program might be causing an error during execution may not make sense at first, but you can think of it like a game of Marco Polo between you and the program. Adding messaging functions is the equivalent of you calling out「Marco」and when a function is executed, the program calls back to you with「Polo.」You know when you are near the statement producing the error because the program doesn't display the next debugging message.

Place the message functions used for debugging about every 5 to 10 statements in a program; place them too frequently or infrequently, and they will not be as useful. The following is an example of a custom program that contains two errors that will cause some problems and shows how messaging functions can be used to help identify the bad statements:

(defun c:BadCode ( / ) ; Prompt for string (setq str (getstring "\nEnter a string: ")) ; If str is not nil, continue (if str (progn (princ "DEBUG: Inside IF") (prompt "\nValue entered: " str) ; Error 1, too many arguments ; Prompt for integer (setq int (getint "\nEnter an integer: ")) (princ "DEBUG: Ready to divide") ; Divide number by 2 (if int (prompt (strcat "\nDivisor" (itoa (/ 2 int))))) ; Error 2 (possible) if user types 0 ) (princ "DEBUG: IF ELSE") ) (princ "DEBUG: Inside IF") (princ) )

The princ function in the previous example is used to display debugging-related messages during the execution of the program. The statement containing the prompt function causes an error because it doesn't accept two arguments, and the / function causes an error if it tries to divide 2 by 0.

TIP

I recommend starting debugging messages with \nDEBUG: to make it easy to locate them in a program. By doing so, you can use the Find and Replace tools of Notepad (Windows) or TextEdit (Mac OS) to comment out debugging messages before you publish the finished program. Replace (princ "\nDEBUG: with ;(princ "\nDEBUG: to comment the statement out.

The following functions can be used to display messages during the execution of a custom program:

alert

prin1

princ

print

prompt

These message functions were covered in Chapter 15,「Requesting Input and Using Conditional and Looping Expressions.」

NOTE

The steps in the following exercise depend on the ch19_debuggingex.lsp sample file available for download from www.sybex.com/go/autocadcustomization. The sample file should be placed in the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store the LSP files.

In this exercise, you will look at a custom program that has seen better days; it contains several errors that need to be identified and fixed. Some of the errors prevent the program from loading, whereas others cause the program to generate errors during execution. The following steps explain how to fix the errors in the file:

Load Ch19_DebuggingEx.lsp into AutoCAD with the appload command. If the File Loading - Security Concern warning message is displayed, click Load to continue. AutoLISP displays the error message ; error: malformed string on input at the Command prompt.

Open the Ch19_DebuggingEx.lsp file in Notepad (Windows) or TextEdit (Mac OS). In the text editor area, you see the following code:

(defun c:BadCode ( / str int) ; Prompt for string (setq str (getstring "\nEnter a string: )) ; If str is not nil, continue (if str (progn (prompt "\nValue entered: " str) ; Prompt for integer (setq int (getint "\nEnter an integer: ")) ; Divide 2 by a number (if int (prompt (strcat "\nDivisor: " (rtos (/ 2.0 int)))) ) ) (princ) )

Scan the code for the missing quotation mark (「). Do you see it? It is missing at the end of the prompt string in the getstring function.

Change "\nEnter a string: to "\nEnter a string: ".

Save the file and reload it into AutoCAD.

Scan the code line by line and count the number of opening and closing parentheses. Do you see it? A missing closing parenthesis can be much harder to locate than a missing quotation mark, but there is a technique you can use.

Copy and paste one line at a time from the LSP file to the AutoCAD Command prompt and look to the left side of the command-line window. Evaluate the number of open parentheses each time you paste a new line until you see an extra open parenthesis.

NOTE

Instead of copying one line at a time, you can copy a whole AutoLISP function and paste it at the Command prompt as well; just don't paste a command as the first line.

The following shows the results of pasting each code statement to the Command prompt. The problem is not that there's an extra opening parenthesis, but rather that a closing parenthesis is missing (as the last line here makes clear). The statement that is causing the error is (if int (prompt (strcat "\nDivisor: " (rtos (/ 2.0 int)))).

Command: (defun c:BadCode ( / str int) (_> ; Prompt for string (_> (setq str (getstring "\nEnter a string: ")) (_> (_> ; If str is not nil, continue (_> (if str ((_> (progn (((_> (prompt "\nValue entered: " str) (((_> (((_> ; Prompt for integer (((_> (setq int (getint "\nEnter an integer: ")) (((_> (((_> ; Divide 2 by a number (((_> (if int (prompt (strcat "\nDivisor: " (rtos (/ 2.0 int)))) ((((_> ) (((_> ) ((_> ((_> (princ) ((_> )

In the text editor area, add the missing closing parenthesis to the end of the following statement: (if int (prompt (strcat "\nDivisor: " (rtos (/ 2.0 int))))

Save the file and reload it into AutoCAD. The file loads without any problems.

In this exercise, you will test the custom program and fix any problems that might be encountered:

At the Command prompt, type badcode and press Enter.

At the Enter a string: prompt, type test and press Enter. AutoCAD displays the error message ; error: too many arguments at the Command prompt.

In the text editor area, add the statements in bold to the file:(defun c:BadCode ( / ) ; Prompt for string (setq str (getstring "\nEnter a string: ")) ; If str is not nil, continue (if str (progn (princ "\nDEBUG: Inside IF") (prompt "\nValue entered: " str) ; Prompt for integer (setq int (getint "\nEnter an integer: ")) (princ "\nDEBUG: Ready to divide") ; Divide 2 by a number (if int (prompt (strcat "\nDivisor: " (rtos (/ 2 int))))) ) (princ "\nDEBUG: IF ELSE") ) (princ "\nDEBUG: Inside IF") (princ) )

Save the file and reload it into AutoCAD. The last message that AutoCAD displays before the error message is DEBUG: Inside IF. Look at the next statement after the message that contains the prompt function. Do you see the problem? The prompt function accepts only a single argument.

Change the statement containing the prompt function to the following:(prompt (strcat "\nValue entered: " str))

Save the file and reload it into AutoCAD.

At the Command prompt, type badcode and press Enter.

At the Enter a string: prompt, type test and press Enter.

At the Enter an integer: prompt, type 4 and press Enter. The custom function completes as expected and the following messages are displayed at the Command prompt.

Command: BADCODE Enter a string: test DEBUG: Inside IF Value entered: test Enter an integer: 4 DEBUG: Ready to divide Divisor: 0.5000 DEBUG: Inside IF

Run the badcode function again. When prompted for an integer value, type 0 and press Enter. The last message that is displayed is DEBUG: Ready to divide before the error message ; error: divide by zero. To avoid the error related to dividing by 0, you should add a test condition to the program.

The previous exercises demonstrate how the AutoLISP error messages are helpful in figuring out why a program doesn't load or what is happening during execution. You also saw how adding messages to a function can be helpful in figuring out where an error is occurring in a custom program.

Tracing Functions

AutoLISP provides a feature known as function tracing that allows you to be notified when a function is about to be executed and what it returns. You use the trace function to enable the tracing of a function and the untrace function to stop tracing a function. When tracing is enabled for a function, a message stating that the function is about to be executed is displayed at the Command prompt along with the arguments it was passed. Once the function is done executing, a message with the function's return value is displayed at the Command prompt. You can trace both custom and standard AutoLISP functions.

The following shows the syntax of the trace and untrace functions:

(trace [function_name …]) (untrace [function_name …])

The function_name argument is the name of the function you want to enable tracing for (or that you no longer want to trace). The argument is optional, and when no function name is provided, the function doesn't do anything. If you want to trace more than one function, enter additional function names and separate them with a space; don't provide the function names in a list.

Here is an example of tracing a custom function named OddOrEven:

; Function returns ODD or EVEN based on the number it is passed (defun OddOrEven (cnt / ) (if (= (rem cnt 2) 1) "ODD" "EVEN" ) ) ; Enable tracing of the OddorEven function (trace OddOrEven) ; Function that loops 5 times and calls the OddOrEven function (defun c:TraceUntrace ( / ) (setq cnt 5) (while (> cnt 0) (OddOrEven cnt) (setq cnt (1- cnt)) ) (princ) ) ; Output from the tracing of the OddOrEven function Entering (ODDOREVEN 5) Result: "ODD" Entering (ODDOREVEN 4) Result: "EVEN" Entering (ODDOREVEN 3) Result: "ODD" Entering (ODDOREVEN 2) Result: "EVEN" Entering (ODDOREVEN 1) Result: "ODD" ; Disable tracing of the OddorEven function (untrace OddOrEven)

Catching Errors in a Program

Even with all the effort put into identifying and locating errors in a custom program, an error can still occur during the execution. It is just in the nature of some functions to always return an error instead of nil when something unexpected happens. For example, dividing a number by 0 always produces an error; the same goes for times when a custom function isn't loaded when your program tries to call it.

The vl-catch-all-apply function can be used to catch and then handle the error without it causing your program to suddenly end. The arguments passed to the vl-catch-all-apply function are evaluated before the function returns a value. If no error occurs, either the expected value or a value of the Catch-All-Apply-Error data type is returned.

The following shows the syntax of the vl-catch-all-apply function:

(vl-catch-all-apply 'function_name 'argument_list)

Here are its arguments:

function_name The function_name argument is the name of the function you want to execute. The name must be prefixed with an apostrophe.

argument_list The argument_list argument is a list that contains the arguments that should be passed to the function specified by the function_name argument. The argument list must be prefixed with an apostrophe.

Here's an example that shows how to catch an error with the vl-catch-all-apply function:

; Divide 2 by 0 (setq div (/ 2 0)) ; error: divide by zero !div nil ; Divide 2 by 1 (setq div (vl-catch-all-apply '/ '(2 1))) 2 ; Divide 2 by 0 (setq div (vl-catch-all-apply '/ '(2 0))) #<%catch-all-apply-error%> !div #<%catch-all-apply-error%>

When you use the vl-catch-all-apply function, you can use the vl-catch-all-error-p function to determine if an error was returned.

The following shows the syntax of the vl-catch-all-error-p function:

(vl-catch-all-error-p value)

The value argument is a value of any supported data type. If the value is of the Catch-All-Apply-Error data type, T is returned and indicates that the return contains an error and not an expected data type, or nil if a value other than an error was returned.

Here are examples of the vl-catch-all-error-p function:

; Divide 2 by 1 (vl-catch-all-error-p (setq div (vl-catch-all-apply '/ '(2 1)))) nil ; Divide 2 by 0 (vl-catch-all-error-p (setq div (vl-catch-all-apply '/ '(2 0)))) T

The type of error returned by the vl-catch-all-apply function can be obtained with the vl-catch-all-error-message function. The vl-catch-all-error-message function returns a string value that represents the error, which you can use in a conditional statement to determine how the program should continue. Perhaps you will ask the user for a new value, substitute a default value, or not execute any further statements.

The following shows the syntax of the vl-catch-all-error-message function:

(vl-catch-all-error-message value)

The value argument should contain a value of the Catch-All-Apply-Error data type. If an error is passed to the function, a string containing the error type is returned. Any value passed to the function results in the return of a new error.

Here's an example of the vl-catch-all-error-message function:

; Divide 2 by 0 (vl-catch-all-error-message (setq div (vl-catch-all-apply '/ '(2 0)))) "divide by zero"

NOTE

The apply function is similar to vl-catch-all-apply; you can pass a single function a list of values to use as the function's arguments. However, the apply function will still result in the ending of the program if an error occurs. For more information on the apply function, see the AutoCAD Help system.

Defining and Using a Custom Error Handler

Debugging and eradicating errors in a custom program (and catching those errors that might happen during execution) helps to ensure a great experience for the end user. However, even with all of this planning there are some situations you can't handle using the techniques described so far in this chapter. As a last-ditch effort to handle any errors that might come up, AutoLISP provides the ability to implement a custom error handler that will give you a chance to clean up any changes to the AutoCAD environment.

No! Not the Esc Key!

Here's a situation that will always end with an error. You can't catch it while you're programming because nobody is supposed to do that. When an end user presses Esc while being prompted for a value, AutoLISP cancels the current function and starts the current error handler. The standard AutoLISP error handler simply returns a message about the most recent error, but you can override the standard AutoLISP error handler with your own error handler. I'll show you how to use a custom error handler to catch the error and then respond accordingly.

A custom error handler is a function defined with the defun function and should accept a single argument. The argument passed to the error handler is of the string data type, and it represents the error that occurred.

The standard error handler is represented by the function named *error*. You don't directly call this function, but you do override it with your own custom error handler once it is defined. The *error* function is overwritten using the setq function, but before you do override it, I recommend that you store the current *error* function so it can be restored after your custom program ends. If you don't restore the previous *error* function, it might cause problems with other custom AutoLISP programs.

The following is an example of a basic custom error handler that doesn't return an error message when the user presses Esc while being prompted for input with one of the getxxx functions:

(defun *my_error* ( msg / ) (if (/= (strcase msg T) "function cancelled") (alert (strcat "\nERROR: " msg)) ) (setq *error* old_err) )

The following stores the current *error* function in the old_err variable, and then sets the *my_error* function as the current error handler that AutoLISP calls when an error occurs:

(setq old_err *error* *error* *my_error*)

This statement restores the previous error handler that was assigned to the old_err variable:

(setq *error* old_err)

The following function prompts the user for an integer and then divides 2 by that number. This is designed to deal with errors that occur if the user presses Esc instead of entering a number or if 0 is entered.

(defun c:TestEsc ( / int) (setq int (getint "\nEnter a whole number: ")) (alert (strcat "Value: " (itoa (/ 2 int)))) )

As an alternative to the previous example, you could use a custom error handler to catch the error that might be generated by the function and then respond accordingly. The following function implements a custom error handler and displays an error message only when the user doesn't press Esc:

(defun c:TestEscErr ( / int) ; Define the custom error handler (defun *my_error* ( msg / ) (if (/= (strcase msg T) "function cancelled") (alert (strcat "\nERROR: " msg)) ) (setq *error* old_err) ) ; Store the current error handler and set the custom error handler (setq old_err *error* *error* *my_error*) (setq int (getint "\nEnter a whole number: ")) (alert (strcat "Value: " (itoa (/ 2 int)))) ; Restore the previous error handler (setq *error* old_err) (princ) )

NOTE

A custom error handler has access to the local variables of the function in which the error occurred.

Grouping Functions into a Single Undo Action

Standard AutoCAD commands support the ability to be undone with a single action using the u or undo command. Using the undo command, you can wrap all the functions in a custom AutoLISP program to act like a single operation. This makes it easier to roll back changes that are made by a custom program and restore the drawing to the state it was in before the program was executed when an error is encountered or for the end user's convenience.

If you don't use the undo command to wrap the functions in a custom AutoLISP program, the undo command might need to be executed several (maybe even hundreds of) times to roll back the changes that were made. Objects created or modified with the command function would need to be rolled back one command at a time. However, objects created or modified without the use of the command function don't support individual undoing, but rather are undone only after the changes made by the last individual command are undone.

Figure 19.3 illustrates how commands are undone by default—one at a time—and also shows how objects created with the entmake function are undone when undo grouping is not used. The top of the illustration shows the circle command used twice and the line command used once; executing the u command three times would get you back to the drawing's previous state. The bottom of the illustration shows the creation of a circle with the circle command, and then a line and circle created with the entmake function. Notice that the objects created with entmake are grouped with the previous command; in this case it was the circle command. Executing the u command will undo the line and circle created with the entmake function, along with the circle command.

Figure 19.3 Rolling back changes made with commands and the entmake function

The BEgin suboption of the undo command is used to start a new undo grouping, whereas the End suboption marks the end of the undo grouping. Once a grouping is defined, the u or undo command will then roll back all the changes that were made as part of that grouping. Figure 19.4 illustrates the same object-creation operations shown in Figure 19.3, but here the operations are wrapped in undo groupings. Undoing the changes now requires the end user to execute the u command only once to roll back all the changes included in the undo grouping.

Figure 19.4 Wrapping functions with undo groupings to create a single undo action

The following example demonstrates how to begin and end an undo grouping:

; Create concentric circles (defun c:CCircs ( / cenPt rad) ; Start the undo grouping (command "._undo" "_be") ; Prompt for center point (setq cenPt (getpoint "\nSpecify center point: ")) (entmake (list (cons 0 "CIRCLE") (cons 10 cenPt) (cons 40 0.75))) ; Prompt for radius (setq rad (getdist cenPt "\nSpecify radius of second circle: ")) (entmake (list (cons 0 "CIRCLE") (cons 10 cenPt) (cons 40 rad))) ; End the undo grouping (command "._undo" "_e") (princ) )

Here's an example of using undo grouping with a custom error handler:

; Create concentric circles (defun c:CCircs ( / cenPt rad) ; Custom error handler (defun *my_error* ( msg / ) ; Ends the previous undo grouping (command "._undo" "_e") ; Roll back the changes (command "._u") (setq *error* old_err) ) ; Store the current error handler and set the custom error handler (setq old_err *error* *error* *my_error*) ; Start the undo grouping (command "._undo" "_be") ; Prompt for center point (setq cenPt (getpoint "\nSpecify center point: ")) (entmake (list (cons 0 "CIRCLE") (cons 10 cenPt) (cons 40 0.75))) ; Prompt for radius (setq rad (getdist cenPt "\nSpecify radius of second circle: ")) (entmake (list (cons 0 "CIRCLE") (cons 10 cenPt) (cons 40 rad))) ; End the undo grouping (command "._undo" "_e") ; Restore the previous error handler (setq *error* old_err) (princ) )

With the previous example, if the user presses Esc while being prompted for the radius, the program ends and undoes the drawing of the first circle.

Starting with AutoCAD 2012, the way commands are called within a custom error handler was changed. If you are using the command-s function within a custom error handler, you must call the *push-error-using-stack* function before the *error* handler might be called. Then, after the last use of the command-s function, you must call the *pop-error-mode* function.

The *push-error-using-command* function is similar to *push-error-using-stack*, but should be called when the command function is used in a custom error handler. When neither is called, AutoLISP assumes it is using *push-error-using-command* and it is okay to use the command function; this is the legacy behavior of AutoCAD 2011 and earlier releases.

The *push-error-using-command*, *push-error-using-stack*, and *pop-error-mode* functions don't accept any arguments. I show how to use the *push-error-using-command* and *pop-error-mode* functions in the next section. For an example of the *push-error-using-stack* function, see the AutoCAD Help system.

TIP

Examples of custom error handlers using the command and command-s functions can be found in the ch19_errhandlers.lsp sample file available for download from www.sybex.com/go/autocadcustomization.

Exercise: Handling Errors in the drawplate Function

In this section, you will continue to work with the drawplate function that was originally introduced in Chapter 12,「Understanding AutoLISP.」The key concepts I cover in this exercise are as follows:

Using Undo Grouping Wrapping functions into an undo grouping allows any changes that are made by a custom program to be rolled back and restores the drawing to the state it was in before it was executed.

Adding a Custom *error* Handler Custom *error* handlers make it easy to determine when a program encounters an error and then to respond accordingly.

NOTE

The steps in this exercise depend on the completion of the steps in the「Exercise: Creating, Querying, and Modifying Objects」section of Chapter 16,「Creating and Modifying Graphical Objects.」If you didn't complete the steps, do so now or start with the ch19_drawplate.lsp and ch19_utility.lsp sample files available for download from www.sybex.com/go/autocadcustomization. These sample files should be placed in the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store the LSP files. Once the sample files are stored on your system, remove the characters ch19_ from the name of each file.

Using the drawplate Function

Chapter 16 was the last chapter in which any changes were made to the drawplate function. At that time, the function drew a plate and added holes based on user input, which defined the overall size of the plate. But what if you made a mistake? Did you try to undo the changes that were made by the drawplate function or press Esc to cancel the function when being prompted for input? If you did, you found that the plate that was drawn remained in the drawing or the changes that were made to the drawing didn't exactly roll back as expected. Typically when you cancel a command before it completes, all of the changes are undone, but not so with the drawplate function. Use the following steps to see for yourself:

Create a new drawing.

Start the appload command. Load the LSP files drawplate.lsp and utility.lsp. If the File Loading - Security Concerns message box is displayed, click Load.

At the Command prompt, type drawplate and press Enter.

At the Specify base point for the plate or [Width/Height]: prompt, pick a point in the drawing area to draw the plate and holes based on the width and height values specified.

At the Specify label insertion point: prompt, press Esc. The plate that was drawn remains in the drawing. Typically, when you cancel a command before it completes all of its changes are undone.

Run the drawplate function again. Specify a point for the plate and the label.

At the Command prompt, type u and press Enter. Both the incomplete and complete plates are undone, not just the most recently drawn objects.

Implementing a Custom *error* Handler and Undo Grouping

As you revise the functions, notice how easy it can be to change the underlying functionality of your programs when they are divided into several smaller functions. Smaller functions are easier not only to change, but to retest if a problem is encountered.

The following steps explain how to update the drawplate function to include a custom *error* handler and undo grouping:

Open the drawplate.lsp file in Notepad (Windows) or TextEdit (Mac OS).

In the text editor area, add the text in bold:; Custom error handler with command functions (defun err_drawplate (msg) (if (/= msg "Function cancelled") (alert (strcat "\nError: " msg)) ) (command "._undo" "_e") (command "._u") ; Restore previous error handler (setq *error* old_err) (princ) ) ; Draws a rectangular plate that is 5x2.75 (defun c:drawplate ( / pt1 pt2 pt3 pt4 width height insPt textValue cenPt1 cenPt2 cenPt3 cenPt4 old_vars hole_list) (setq old_err *error* *error* err_drawplate) ; Command function being used in custom error handler (*push-error-using-command*) (command "._undo" "_be") ; Store and change the value of the system variables (setq old_vars (get-sysvars '("osmode" "clayer" "cmdecho"))) (set-sysvars '("osmode" "clayer" "cmdecho") '(0 "0" 0)) ; <Code break…> ; Save previous values to global variables (setq *drawplate_width* width) (setq *drawplate_height* height) (command "._undo" "_e") ; Restore previous error handler (setq *error* old_err) ; End using *push-error-using-command* (*pop-error-mode*) ; Exit "quietly" (princ) )

Click File Save.

Testing the Changes to the drawplate Function

The following steps explain how to test the changes that were made to the drawplate function:

Create a new drawing.

Start the appload command. Load the LSP files drawplate.lsp and utility.lsp. If the File Loading - Security Concerns message box is displayed, click Load.

At the Command prompt, type drawplate and press Enter.

At the Specify base point for the plate or [Width/Height]: prompt, pick a point in the drawing area to draw the plate and holes based on the width and height values specified.

At the Specify label insertion point: prompt, press Esc. The plate that was drawn is removed from the drawing, thereby restoring the drawing to its previous state.

Run the drawplate function again. Specify a point for the plate and label.

At the Command prompt, type u and press Enter. The completed plate is undone as expected.

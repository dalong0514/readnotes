# Getting Started with DCL

[Dialog Control Language (DCL) | AfraLISP](https://www.afralisp.net/dialog-control-language/)

[Getting Started with DCL - Part 1 | AfraLISP](https://www.afralisp.net/dialog-control-language/tutorials/getting-started-part-1.php)

[Dialog Boxes & AutoLISP - Part 1 | AfraLISP](https://www.afralisp.net/dialog-control-language/tutorials/dialog-boxes-and-autolisp-part-1.php)

What is Dialog Control Language? Dialog Control Language or DCL for short is a simple markup language that enables programmers in AutoLISP and Visual LISP to create dialog boxes that can be integrated into their routines. This means that an AutoLISP routine can gather a range of input data from a user through a familiar and logical interface. Without DCL, AutoLISP can only take user input from the command line.

AutoLISP includes a number of special functions that allow routines to load, interact with and unload dialog boxes written in DCL. DCL is specifically for use with AutoCAD in conjunction with AutoLISP and Visual LISP. See the DCL Wikipedia article for more information.

## Getting Started with DCL - Part 1

by Kenny Ramage

Dialog Control Language, or DCL, always seems to frighten off a lot of Lispers. I admit, it did me too until I was forced into a situation were I had to learn it and quickly. (make it work, or you're out boy!)

Well, I would hate for any of you to be in the same situation, so for the next few issues, I'll be taking you step by step, hand in hand, through the minefield of the DCL language. I will share your pain and misery, and will wipe away your tears, I will… ("Hey Kenny, get on with it!"). Oops, sorry!

As I was saying before I got this black eye, there are a few terms that you need to familiarise yourself with before we get stuck into some coding. Firstly, the dialog box itself is known as a "dialog definition". Secondly, each "control" on the dialog is known as a "tile definition". Thirdly, each "property" of a "tile" is known as a dialog "attribute". And fourthly, each "method" of a "tile" is known as an "action expression". Why? Who knows? Who cares? All I know is that it will help you immensely in understanding the AutoCAD DCL reference book if you have a basic knowledge of these terms. Right, enough waffle, I'm bored and my eye's sore. Let's have a look at some DCL coding and design ourselves a simple dialog box.

Copy and paste this into Notepad and save it as test_dcl1.dcl. Oh, before I forget, please ensure that you save this file, and it's namesake AutoLisp file, into a directory that is within your AutoCAD search path.

```
//DCL CODING

: dialog
 
{
label = "Test Dialog No 1";
 
	: text
	{
	label = "This is a Test Message";
	alignment = centered;
	}
 
	: button
	{
	key = "accept";
	label = "Close";
	is_default = true;
	fixed_width = true;
	alignment = centered;
	}
 
}
```

We'll have a closer look at what this all means a bit later. First, let's load some AutoLisp coding and try out our new dialog box. Copy and paste this into Notepad and save it as test_dcl1.lsp.

```
;AUTOLISP CODING

(prompt "\nType TEST_DCL1 to run...")
 
(defun C:TEST_DCL1 (/ dcl_id)
 
(setq dcl_id (load_dialog "test_dcl1.dcl"))
 
     (if (not (new_dialog "test_dcl1" dcl_id))
	 (exit )
     );if
 
(action_tile "accept"
    "(done_dialog)"
);action_tile
 
(start_dialog)
(unload_dialog dcl_id)
 
(princ)
 
);defun
(princ)
```

Now load and run your program.

A very simple dialog box containing a message should appear on your screen. It did? Good, well done! Right, let's dissect the DCL coding.

```
//DCL CODING
Anything starting with "//" in DCL is regarded as a comment.

test_dcl1
The name of the dialog.

: dialog
The start of the dialog definition.

{
The opening bracket for the dialog definition.

label = "Test Dialog No 1";
The Label of the dialog definition.
This is what appears in the title bar of the dialog.

: text
The start of a text tile definition.

{
The opening bracket for the text tile definition.

label = "This is a Test Message";
The label attribute of the text tile.

alignment = centered;
The alignment attribute of the text tile.

}
The closing bracket of the text tile.

: button
The start of a button tile definition.

{
The opening bracket for the button tile definition.

key = "accept";
The key, or name of the button tile.
You will use this name to reference this button in your AutoLisp coding.

label = "Close";
The label attribute. What appears on it.

is_default = true;
The default attribute. If this is true, this button will automatically be selected if the <Enter> key is pressed.

fixed_width = true;
Forces the button to be just large enough for the label attribute.

alignment = centered;
The alignment attribute.

}
The closing bracket for the button tile.

}
The closing bracket for the dialog definition.
```

OK, that was easy hey? By the way, did you notice that each of the attribute lines finished with a semicolon(;)? Another important thing that you must remember when dealing with attributes is that their values are case sensitive. (e.g. "True" does not equal "true".)

Now let's have a wee look at the AutoLisp coding that puts this whole thing together. Again, we'll take it line by line :

```
(prompt "\nType TEST_DCL1 to run...") Inform the user how to start the program. Just good manners.
(defun C:TEST_DCL1 (/ dcl_id)
Define the function and declare variables.

(setq dcl_id (load_dialog "test_dcl1.dcl"))
Load the dialog file and set a reference to it.

(if (not (new_dialog "test_dcl1" dcl_id))
Load the dialog definition and check for it's existence.
Remember, a dialogue file can hold various dialogue definitions.

(exit)
Exit the program if the dialog definition is not found.

);if
End if

(action_tile "accept"
If the user selects the tile who's name is "accept", then do the following :

"(done_dialog)"
Close the dialog

);action_tile End of action_tile

(start_dialog)
Start the dialog

(unload_dialog dcl_id)
Unload the dialog from memory

(princ)
finish clean

);defun
End of function

(princ)
Load clean
```

Many people get confused in regards to the order of AutoLisp statements when dealing with DCL files. I don't blame 'em really. I mean look at the coding above! 1) First we load the dialog file. 2) Then we load the dialog definition. 3) Then we run an action_tile statement. 4) Then we start the dialog. 5) And right after that, we unload the dialog.

Where's the logic in that? Haha. But did you notice that the action\_tile statement was quoted? e.g. "(done_dialog)". In effect, what we are telling the tile is this:

"Remember this string, then pass it back to me when the user activates you.". "So, in other words, coding is pre-stored within a particular tile. When I select that tile the coding runs?"

Yep, that's it. But remember, no values will be returned until (done\_dialog) is called, which is also quoted. So, the sequence is like this : 1) First we load the dialog file. 2) Then we load the dialog definition. 3) Then we run AND REMEMBER all theaction\_tile statements. 4) Then we start the dialog. 5) The dialog is displayed. 6) Any action\_tile statement is processed IF the relevant tile is selected.

When a tile that contains the (done\_dialog) function is selected, we unload the dialog and return all tile values.

And that's it. Easy hey? In Part 2, we'll have a look at some predefined tiles, how to enter and retrieve values from a dialog, and how to validate these values.

## Getting Started with DCL - Part 2

OK, tea break over, back to work! Copy and paste this into Notepad and save it as test_dcl2.dcl.

```
//DCL CODING
test_dcl2
 
: dialog
 
{
 
label = "Test Dialog No 2";
		
	: edit_box
	{
	label = "Enter Your Name :";
	mnemonic = "N";
	key = "name";
	alignment = centered;
	edit_limit = 30;
	edit_width = 30;
	value = "";
	}
 
	: edit_box
	{
	label = "Enter Your Age :";
	mnemonic = "A";
	key = "age";
	alignment = centered;
	edit_limit = 3;
	edit_width = 3;
	value = "";
	}
 
	: button	
	{
	key = "accept";
	label = "OK";
	is_default = true;
	fixed_width = true;
	alignment = centered;
	}
 
	: errtile
	{
	width = 34;
	}
}
```

And now the AutoLisp coding. Copy and paste this and save it as test_dcl2.lsp and then load and run it.

```
;AUTOLISP CODING
(prompt "\nType TEST_DCL2 to run.....")
 
(defun C:TEST_DCL2 ( / dcl_id)
 
(setq dcl_id (load_dialog "test_dcl2.dcl"))
     (if (not (new_dialog "test_dcl2" dcl_id))
	 (exit)
     );if
 
(set_tile "name" "Enter Name Here")
(mode_tile "name" 2)
(action_tile "name" "(setq name $value)")
(action_tile "age" "(setq age $value)")
(action_tile "accept" "(val1)")
 
(start_dialog)
(unload_dialog dcl_id)
 
(alert (strcat "Your name is " name
               "\nand you are " age " years of age."))
 
(princ)
 
);defun
 
-----------------------
 
(defun val1 ()
 
(if (= (get_tile "name") "Enter Name Here")
	(progn
	   (set_tile "error" "You must enter a name!")
	   (mode_tile "name" 2)
	);progn
	(val2)
);if
 
);defun
 
-------------------
 
(defun val2 ()
 
(if (< (atoi (get_tile "age")) 1)
	(progn
	  (set_tile "error" "Invalid Age - Please Try Again!!")
	  (mode_tile "age" 2)
	);progn
	(done_dialog)
);if
 
);defun
 
(princ)
```

The dialog that is displayed contains two edit boxes. One to enter your name into, and one your age. After entering the relevant information select the "OK" button. An alert box will display showing your details.

1『原来用 alert 函数可以直接弹窗显示信息，收获到了。（2020-09-14）』

Now run the program again, but do not enter your name. An error message will display informing you that you must enter your name. Fill in your name but leave your age blank. Press enter again. Another error message will inform you that you have entered an invalid age. Try it with a zero or a negative number. The same error message will display until you enter a number equal or greater than 1. Both of these examples are know as validation. Let's have a look at the DCL coding.

```
:edit_box
This is a predefined tile that allows the user to enter or edit a single line of text.

There are a few new attributes defined in this tile :

mnemonic = "N";
This defines the mnemonic character for the tile.

edit_limit = 30;
This limits the size of the edit box to 30 characters.

edit_width = 30;
This limits the user to typing a maximum of 30 characters.

value = "";
This sets the intial value of the edit box, in this case nothing.
```

Now let's have a look at the AutoLisp coding. First the "action expressions" :

```
(set_tile "name" "Enter Name Here")
This sets the runtime (initial) value of a tile who's "key" attribute is "name".

(mode_tile "name" 2)
This sets the mode of the tile who's "key" attribute is "name". In this example, we have used a mode of "2" that allows for overwriting of what is already in the edit box.

(action_tile "name" "(setq name $value)")
Associates the specied tile with the action expression or call back function. In this case we are saying "If the tile who's key attribute is name is selected, store the value of this tile in the variable name."
; 这是关键操作，绑定输入框的值到变量上

(get_tile "name")
Retrieve the value of the tile who's "key" attribute is "name".

Did you notice that we wrote :
(action_tile "accept" "(val1)")
instead of :
(action_tile "accept" "(done_dialog)")

Instead of closing the dialog when OK is selected, we initiate a subroutine that checks (validates) that the name information is exceptable. If it is not, the error tile is displayed.

(set_tile "error" "You must enter a name!")
Once the name has been validated, this routine then initiates a second subroutine that validates the age value. If this not correct, the error tile is again displayed, this time with a different message.

(set_tile "error" "Invalid Age - Please Try Again!!")
If everything is correct, (done_dialog) is called, all values are returned and the alert box is displayed with the relevant information.
```

## 自己的代码

```
// DCL code
test_dcl
:dialog

{
label = "Test Dialog No 1";
    :text {
    label = "This is a Test Message";
    alignment = centered;
    }

    :button {
    key = "accept";
    label = "Close";
    is_default = true;
    fixed_width = true;
    alignment = centered;
    }
}

// autolisp code
(prompt "\nType TEST_DCL to run...")

(defun c:TEST_DCL (/ dcl_id)
    (setq dcl_id (load_dialog "test_dcl.dcl"))
    (if (not (new_dialog "test_dcl" dcl_id))
        (exit)
    )
    (action_tile "accept" "(done_dialog)")
    (start_dialog)
    (unload_dialog dcl_id)
    (princ)
)
(princ)
```

```
// DCL code
test_dcl
:dialog {
    label = "Test Dialog No 2";
    :edit_box {
        label = "Enter your name: ";
        mnemonic = "N";
        key = "name";
        alignment = centered;
        edit_limit = 30;
        edit_width = 30;
        value = "";
    }
    :edit_box {
        label = "Enter your age: ";
        mnemonic = "A";
        key = "age";
        alignment = centered;
        edit_limit = 3;
        edit_width = 3;
        value = "";
    }

    :button {
        key = "accept";
        label = "OK";
        is_default = true;
        fixed_width = true;
        alignment = centered;
    }

    :errtile {
        width = 34;
    }
}

;autolisp code
(prompt "\nType TEST_DCL to run...")

(defun c:test_dcl (/ dcl_id)
    (setq dcl_id (load_dialog "test_dcl.dcl"))
    (if (not (new_dialog "test_dcl" dcl_id))
        (exit)
    )
    (set_tile "name" "Enter name here")
    (mode_tile "name" 2)
    (action_tile "name" "(setq name $value)")
    (action_tile "age" "(setq age $value)")
    (action_tile "accept" "(val1)")
    (start_dialog)
    (unload_dialog dcl_id)
    (alert (strcat "your name is: " name "\nand your age is: " age))
    (princ)
)

(defun val1 ()
    (if (= (get_tile "name") "Enter Name Here")
        (progn 
            (set_tile "error" "You must enter a name!")
            (mode_tile "name" 2)
        )
        (val2)
    )
)

(defun val2 ()
    (if (< (atoi (get_tile "age")) 1)
        (progn
            (set_tile "error" "Invalid Age!")
            (mode_tile "name" 2)
        )
        (done_dialog)
    )
) 

(princ)
```

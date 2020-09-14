# 0202Dialog Box Programming Concepts

[Dialog Box Programming Concepts | Cadalyst](https://www.cadalyst.com/cad/autocad/dialog-box-programming-concepts-4829)

30 Apr, 1999
By: Bill Kramer

Dialog-box interfaces can make a world of difference in how well the user community accepts an application. This month, we'll look at a simple dialog box and how to program it. First, we will create a basic version that does nothing more for the user than place all the input in a dialog box. Then, we'll improve that dialog box into something much more user friendly. Along the way we'll investigate how dialog boxes are defined and programmed in AutoLISP and Visual LISP.
Both Visual LISP and AutoLISP are the same when it comes to programming a dialog box. First, you have to create a Dialog Control Language (DCL) file that contains the definition of the dialog box. These are essentially the property definitions for the dialog-box objects. A DCL file can contain multiple-dialog box definitions as well.

Listing 1 contains a dialog definition of the dialog box. (All listings are at the bottom of this page.) Each item in the dialog box has an optional name that is followed by a colon. The name is typically used in the Dialog item only, such as the use of CHANGENOTE1 in the beginning of Listing 1. Following the colon is the type of item or tile. You can use a set of predefined tiles (you can also define your own) that can build the dialog box. The most common are the EDIT_BOX and Button. There are also grouping-tile types, such as Row and Column, that define where in the dialog box the tile is to appear. Following the tile type are the properties of the tile inside of a set of squiggle brackets.

When being defined, most tiles contain the Label and Key properties. The Label appears when called for by the tile type. In the dialog tile, the Label appears at the top of the dialog box; in an EDIT_BOX tile, the label appears next to the input field. The Key property is used by the application to gain access to the dialog box or tile. As such, the Key is used in the AutoLISP code to place data into the tile properties and to get the information from the dialog box as it is running.

Some simple rules exist for the use of Key properties inside a dialog box. First off, each Key value must be a string, and it must be unique inside the dialog box. In other words, there should not be any other keys of the same value in the same dialog box. Key names are case sensitive and should be consistent within an application. In Listing 1 all of the Key names are uppercase as a standard.

Dialog Boxes as Objects
Another way to think of dialog boxes is to consider them to be objects. We won't go into the nuances of object-oriented programming, but similar programming concepts apply. From a programming perspective, an object is something that can be manipulated by setting and changing properties or data values. The properties are typically manipulated using functions or methods that take outside information and put it into the object or expose the information in the object to the outside world. When the properties of an object are changed, the object changes accordingly. In the case of AutoLISP, the outside world is our application, and the methods used to manipulate the dialog box are a set of functions available to our application. As we change the properties of the tile objects, the dialog box changes in one way or another.

The coding required to manipulate a basic dialog box, can be found in Listing 2. This function performs all of the essential work required for input via a dialog box. It uses the dialog box definition found in Listing 1, which it assumes is located in the file cdnc3-99.dcl somewhere in the current file system. The (LOAD_DIALOG) subr loads an entire DCL file into memory, and it returns a dialog handle. The dialog handle is used later in the program to access the dialog box definitions. Since a single DCL file can contain multiple dialog-box definitions, a dialog handle can be used to address more than one dialog box.

This is the very minimum application that will support a dialog box. After loading the dialog, the variables are initialized to default or reset values. Next, a WHILE loop is started, and it iterates as long as the symbol ALLDONE is nil and the dialog box named CHANGENOTE1 can be loaded. The dialog handle is used with the name of the dialog box to access the name as defined in the DCL file. CHANGENOTE1 is the name of the dialog object, and a call to (NEW_DIALOG) draws the dialog box on the screen.

Using (NEW_DIALOG) only draws the dialog box; it does not start the dialog box for the user. When (NEW_DIALOG) is done and has returned a non-nil answer, the dialog box is visible on the screen, but the system is still under the control of the application program. We can now use tile manipulation subrs such as (SET_TILE), (ACTION_TILE) and (MODE_TILE) to change the properties of the tiles that make up the dialog box.

Obviously, one does not want to have the program spend too much time setting up the dialog box once it appears on the screen. If the application needs to open a large library and read it (or do something that takes a sizable fraction of a second or more), then this should be done before the (NEW_DIALOG) subr is called. This is as a courtesy to the user who will think the application has bombed or has a problem.

So, exactly which properties would you want to set once the dialog box is active? Most of the time, there are only two properties you will want to manipulate at runtime-when the dialog box is visible on the screen and your control program is running. The remaining properties are typically set at design time-when you are defining the DCL file.

The two properties typically manipulated at runtime are the Value and Action properties. The Value property is the actual value or data stored in a tile, and it typically changes during a run as the user changes data elsewhere in the dialog box or program. The subr (SET_TILE) can be used to set the default values into the Value property of a tile object. When (SET_TILE) runs, the value appears in the dialog box at the tile specified.

Another property that is set in many applications at runtime is the Action property. The Action of a tile is an AutoLISP expression that will be run when the tile is manipulated. The expression defined for the Action property is often called the callback expression or function. Actions can be simple, such as setting the tile value into a local variable, or they can be calls to your own function definitions that are as complex as the application requires.

Once the dialog box has been prepared, the (START_DIALOG) subr is run. At this time, the control is turned over to the dialog-box interaction (that is, the user is driving the pointing device, and the dialog box is reacting).

How the Program Takes Control
There are two ways that your program gets control once (START_DIALOG) is running. The first is for the dialog box to be finished. When the user hits a retirement button, such as OK or Cancel, the (START_DIALOG) subr returns. This subr always returns an integer amount. If the value returned is one, then the OK button was selected. Cancel results in a return value of zero. Your callback functions can also force a return of the (START_DIALOG) subr through the use of (DONE_DIALOG). In that case, you supply the integer parameter to (DONE_DIALOG) that will be returned as a result of the (START_DIALOG).

The other way your program gets control from the dialog-box system is when a callback function is invoked. Callback functions defined in the Action properties of the tiles can result in your own functions being run as the result of the user manipulating the tile. When a callback function is running, your application can service the input, check it or change other tile settings.

Listing 2 does not contain any callback-function requests, just simple SETQ assignments to local variables. After an OK result is returned from the dialog box, the values in the local variables are checked to see if the user made entries for them. If not, the user is told that the data is not complete and the dialog box WHILE loop will repeat. Otherwise, if data was supplied for all of the fields, then a list is created from the data to be returned as a result of the function. The (UNLOAD_DIALOG) removes the DCL definitions from memory, and then the list is returned to the calling function.

If the value returned from (START_ DIALOG) is not one (meaning that the cancel button has been hit), the ALLDONE flag is set to true in order to stop the WHILE loop. After stopping the WHILE loop, the dialog is unloaded from memory and a nil result sent back to the calling function.

Making It Better
The example in Listing 2 demonstrates the basic principles involved in programming a dialog box in AutoLISP, and it has a lot of lines of code when compared to simply asking the user for the input in a series of (GETSTRING) type entries. Additionally, this function does not run in a very user-friendly manner (other than to provide a dialog box entry mechanism). So, what can be done to improve it?

First off, we can provide the system date in the date field as default. When asking for a date, it is a good idea to fill in the field with the system date. Not only does this save the user time in having to enter the date, it also provides a clue as to the date format expected. Another improvement is the use of pop-up lists for the initials of the engineer, the checker and the drafter. The use of the list items will ensure that the entry is proper as well as save on keystrokes needed to enter the information. These improvements make the interface much more satisfying for the user, and they also increase the integrity of the data entry.

Listings 3 and 4 are the DCL and AutoLISP code for the improved interface, respectfully. In the DCL file, the EDIT_ BOX tiles for the initials have been replaced with POPUP_LIST tiles. The AutoLISP code has the most changes in order to accommodate the dialog box. The program startup is the same except that three lists containing the Engineers', the Checkers' and the Drafters' initials have been created. Obviously, these values could come from elsewhere in the system or from a data file of valid choices. To keep the code simple, they are just defined at the beginning of the function.

The function CNOTE2_DIALOG also demonstrates a programming style I highly recommend when developing dialog-box functions, which is to put the runtime-property-setup-function calls in a separate function. Listing 5 contains the code for initializing the dialog box. The function CNOTE2_PREP contains the ACTION_TILE and SET_TILE calls used to initialize the dialog box. The reason for placing them in a separate function is to make it easier to add or change things in the future. It also makes the main-processing program shorter and easier to read (something you will be grateful for if you ever have to change the code in the future).

List Box Setup
You have three subrs to fill in the popup-list values. START_LIST identifies the exact list tile to fill in; using it you can start at the beginning and define all the entries, append to the end or replace a single entry in the middle. ADD_LIST adds a value to the list at the place specified. And, END_LIST terminates the list update sequence. MAPCAR is often used with ADD_LIST to place the contents of a list of strings into the list tile. Also, you must maintain the list separately from the list box. When users manipulate or select a list member, the value of the tile only gives the location in the list box that is affected.

After the call to CNOTE2_PREP (back in Listing 4), there is a call to the MODE_TILE subr. Not only can MODE_TILE be used to enable or disable tiles, but it can also be used to set the focus to the tile. Setting the focus means that the tile specified is the active tile for edits-as if the user had picked it with the mouse. In this application, the only keyboard entry required is the description, and, thus, the focus is set there initially. If a dialog box contains a mixture of mouse and keyboard entry, then set the focus to the first keyboard entry when starting the dialog box. That way the user can enter the data and return to the pointing device for the remainder of the dialog box. Keeping the user's comfort in mind when designing dialog boxes is important because it will improve the acceptance of the application.

Finally, in Listing 4 we check to see what the value returned from START_DIALOG is. Similar to the earlier version, we are interested in the OK result. When OK has been selected, START_DIALOG returns a value of one, and the program then checks to see if the description field has been filled in. It doesn't need to check the initials because a default entry has already been selected, so the user can only select from the choices provided in the program. The date entry was checked using a callback function. At the end of Listing 5, the callback function, CNOTE2_DATE, was attached to the DATE tile. In Listing 6, CNOTE2_ DATE checks the date entry to see if it is a recognizable date. As a consequence, the user cannot enter a bad date while the dialog box is running. Thus, our main program in Listing 4 only has to check to see if the description entry is empty or not.

Callback Functions
Callback functions provide a way for the program to perform error checking in a realtime fashion-as the user enters the data it is checked to see if it is valid. If not, an error message can be flashed to users informing them of the problem so that corrective action can take place right away. Callback functions should be short and to the point. They cannot perform (COMMAND) expressions, and they should not attempt to communicate with the user through the command line. Instead, callback functions can be set up to start nested dialog boxes and to create graphic objects using (ENTMAKE).

The callback function in Listing 6 is very short, and it simply checks the date format. If the date format is not correct, the user is informed of that through an Alert dialog box. The date tile value is set to the currently saved value in the variable cdate. It is important to note that the date-check mechanism in Listing 6 uses some code borrowed from a previous Programmer's Toolbox column (CADENCE, March 1996, "The Dating Game," pp. 111-116). The function (IS_A_ DATE) is not printed here, but it can be found online at www.cadence-mag.com as part of the code associated with this article.

In order to set up the default date to today's date, the function TODAY-DATE is used, as shown in Listing 7. This function retrieves the value of the system date from the AutoCAD cdate system variable, and then it reformats the value into a string. The resulting string has a form of "YYYYMMDD" where YYYY is the year value, MM is the month and DD the day number. Just for fun, this version does not require that the year value be four digits. It will accurately parse the AutoCAD date string for years before 1000 and after 9999.

The functions shown here are just the input functions for a bigger application that would take the change-note information and create a block entry for placement into a drawing title block. Listing 8 contains the starting code for each of these functions but nothing else. One nice feature of dialog-box programming is that it does reward structured-programming design. As seen in Listing 8, the entire input is reduced to a single function call that results in a list of input values that are very easy to test. Once you are happy with the results of the dialog box, you can move deeper into the application by tackling the database update of the change note. Until next time, keep on programmin'!

```c
Listing 1. Dialog Box Code for Version 1

CHANGENOTE1 : dialog { label = "Change note";
  : edit_box {key="DESC";
    label="Describe";
  }
  : edit_box {key="DATE";
      label="Change date MM/DD/YY";
  }
  : boxed_row { label="Initials";
    : edit_box {key="ENG";
      label="Engineer"; edit_width=3;
    }
    : edit_box {key="CHK";
      label="Checker"; edit_width=3;
    }
    : edit_box {key="DFT";
      label="Drafter"; edit_width=3;
    }
  }
  ok_cancel;
}
Listing 2. Change Request Input Version 1

;;
(defun CNOTE1_DIALOG ( /
     DH
     CDate
     CDesc
     CEng
     CChk
     CDft
     AllDone
     )
  (setq DH (load_dialog "CDNC3-99")
        CDesc ""
        CEng ""
        CChk ""
        CDft ""
        CDate ""
  )
  (if DH (progn
     (while (and (null AllDone)
                 (new_dialog "CHANGENOTE1" DH))
       ;;
       ;;Prepare dialog box contents
       (set_tile "DESC" CDesc)
       (set_tile "ENG" CEng)
       (set_tile "CHK" CChk)
       (set_tile "DFT" CDft)
       (set_tile "DATE" CDate)
       (action_tile "DESC" "(setq CDesc $value)")
       (action_tile "DATE" "(setq CDate $value)")
       (action_tile "ENG" "(setq CEng $value)")
       (action_tile "CHK" "(setq CChk $value)")
(continued from previous column)
       (action_tile "DFT" "(setq CDft $value)")
       ;;
       ;;Hand control over to the user
       (if (= (start_dialog) 1)
         ;;okay was selected, check input
         (if (and (/= CDesc "")
                  (/= CEng "")
                  (/= CChk "")
                  (/= CDft "")
                  (/= CDate ""))
             (setq AllDone  ;result list
               (list
                CDesc
                CDate
                CEng
                CChk
                CDft
             ))
             ;;else, error detected.
             (alert "Data is not complete!")
         )
         ;; else, CANCEL was checked
         (setq AllDone 'T)
       ) ;;end IF check of start_dialog return
     ) ;;end WHILE Loop
     (unload_dialog DH)
  ))
  (if (listp AllDone) AllDone) ;;send back ;;resulting list
)
Listing 3. Dialog Box Code for Version 2

CHANGENOTE2 : dialog { label = "Change note";
  : edit_box {key="DESC";
    label="Description";}
  : edit_box {key="DATE";
    label="Date MM/DD/YYYY"; edit_width=12;}
  : boxed_row {
    : popup_list {key="ENG";
      label="Engineer";}
    : popup_list {key="CHK";
      label="Checker";}
    : popup_list {key="DFT";
      label="Drafter";}
  }
  ok_cancel;
}
Listing 4. Change Request Input Version 2

;;
(defun CNOTE2_DIALOG ( /
     DH CDesc CDate
     CEng CChk CDft
     Engs Chks Dfts
     AllDone
     )
   (setq DH (load_dialog "CDNC3-99")
         CDesc ""
         CDate (Today-date)
         CEng "0"
         CChk "0"
         CDft "0"
         Engs (list "EN1" "EN2")
         Chks (list "CH1" "CH2" "CH3" "CH4")
         Dfts (list "ME!" "DF2" "DF3")
   )
   (while (and DH
               (null AllDone)
               (new_dialog "CHANGENOTE2" DH)) 
      ;;
      (CNOTE2_PREP)
      (mode_tile "DESC" 2)
      ;;
      (if (= (start_dialog) 1) ;;okay pressed
         (if (/= CDesc "")
          (setq AllDone
           (list
             CDesc
             CDate
             (nth (atoi CEng) Engs)
             (nth (atoi CChk) Chks)
             (nth (atoi CDft) Dfts)
           )
          )
          (alert "Description required!")
         )
         ;; cancel pressed
         (setq AllDone 'T)
      )
   )
   (if DH (unload_dialog DH))
   (if (listp AllDone) AllDone)
)
Listing 5. Prepare Dialog Version 2

;;
(defun CNOTE2_PREP ()
   (start_list "ENG")
      (mapcar 'add_list Engs)
   (end_list)
   (start_list "CHK")
      (mapcar 'add_list Chks)
   (end_list)
   (start_list "DFT")
      (mapcar 'add_list Dfts)
   (end_list)
   (set_tile "ENG" CEng)
   (set_tile "CHK" CChk)
   (set_tile "DFT" CDft)
   (set_tile "DESC" CDesc)
   (set_tile "DATE" CDate)
   (action_tile "DESC" "(setq CDesc $value)")
   (action_tile "ENG" "(setq CEng $value)")
   (action_tile "CHK" "(setq CChk $value)")
   (action_tile "DFT" "(setq CDft $value)")
   (action_tile "DATE" "(CNOTE2_DATE $value)")
)
Listing 6. Date Entry Check

;;
(defun CNOTE2_DATE (Val)
   ;; This function uses the Programmer's    ;; Toolbox
   ;; function (IS_A_DATE) from the March 
   ;; 1996 issue of CADENCE.
   (if (IS_A_DATE Val)
      (setq CDate Val)
      (progn
        (alert "Date string entry invalid!")
        (set_tile "DATE" CDate)
      )
   )
)
Listing 7. Today's Date as a String

;;
(defun Today-Date ( / S L)
  (setq S (rtos (getvar "CDATE") 2 0)
        L (strlen S)
        S (strcat
            (substr S (- L 3) 2) "/" ;;month
            (substr S (- L 1) 2) "/" ;;day
            (substr S 1 (- L 4)) ;;year
          )
  )
)
Listing 8. Command Functions to Test Input

;;
(defun C:CNOTE1 ( / CHNG)
  (setq CHNG (CNOTE1_DIALOG))
)
(defun C:CNOTE2 ( / CHNG)
  (setq CHNG (CNOTE2_DIALOG))
)
```
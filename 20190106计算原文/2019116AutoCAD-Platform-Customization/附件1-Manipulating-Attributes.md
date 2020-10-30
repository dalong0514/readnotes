# Manipulating Attributes

29 Feb, 2000

By: Bill Kramer

[Manipulating Attributes | Cadalyst](https://www.cadalyst.com/management/manipulating-attributes-4817)

AutoCAD drawings are more than just graphics. Obviously they are intended to convey information to designers, manufacturers, builders and so forth, but they can do much more as well. AutoCAD drawings can contain data that can be used by other computer programs to perform a variety of tasks such as creating a bill of materials, validating a design, interfacing to a machine tool or any number of activities. To accomplish this, the AutoCAD drawing must store more than just the graphical data and dimensions. It must also store information that is specific to the interface involved. Sometimes this information will be visible in the drawing, and other times it will not be visible. Visibility depends on the application and nature of the data. There are a couple of ways to store information in a drawing that meets these needs.
One way is through the use of block attributes. Attributes are independent entities attached to block inserts. They can be used to hold text in a visible or invisible fashion. As a result, they offer a wonderful way for AutoCAD to interface with other applications.

In order to facilitate the access of attributes by external systems, they are tagged, which means that the attributes contain not only variable text information but also have tags or names attached to them so that they can be extracted into an external text file for manipulation by another system using a common reference. For example, suppose you had a library of blocks that represented standard building objects such as windows, doors or bolts. These blocks can have tags (and associated data) that describe the objects in a way that can be used by another program. For bolts, the tagged text might contain sizing information. For windows and doors, the text may contain manufacturer, costs, delivery schedules and so forth.

Perhaps the most common uses of attributes are in a title block that is attached to a drawing. The attributes of a title block can contain project data, revision histories and anything else that might be important to a reader of the document. A program can then read the tags of the project block and create a report for a drawing information system. In fact, at a recent Autodesk University an attendee asked me about manipulating the tags that are found in attributes for just this purpose. As a consequence, this month we'll explore some very useful utilities that facilitate that sort of activity in a drawing.

## How Attributes are Stored

First, it's important to understand how attributes are stored in a drawing. Attributes exist at two levels in a drawing. They are initially created using the attribute definition command (ATTDEF) in which the default, prompt, visibility and tag values are defined. Attributes are defined when you create the graphics that will comprise a block. When defined in a drawing, the attributes are drawn using the tag name where the text will appear relative to the block being constructed. When the block is created, either through the use of the BLOCK command or by saving the drawing to disk, the attribute definition objects are included along with the graphics.

As a simple example, draw a circle in a new drawing and then use the ATTDEF command to define an attribute. Use whatever text values you desire for the prompt, default and tag values. Place the text for the attribute at the center point of the circle (use the middle alignment option). Next, use the BLOCK command, and select both the circle and attribute definition objects for the graphics that represent the new block. When the block is inserted into the drawing, the attribute prompt will appear in a dialog box (if the AutoCAD system variable ATTDIA is set to 1) or at the command prompt. The text used for the prompt string will be displayed along with the default value for each attribute defined in the block.

After the block has been inserted, an INSERT object will be added to the drawing. When the block contains attributes, the group code 66 will appear in the entity list of the block with a value of one (1). This means that attribute objects follow the insert object. Using (ENTNEXT), the programs can then navigate to the objects that have the name ATTRIB. Since a variable number of attributes can be associated with a block, the SEQEND object denotes the end. Thus, inside a drawing the sequence of entity objects will be an INSERT object followed by any number of ATTRIB objects followed by a SEQEND object. If the block insert does not have any attributes, ATTRIB or SEQEND objects will not follow the INSERT.

In the block definition you will find the ATTDEF objects for any given block. If there are no attributes for the block, then the ATTDEF objects will not be found in the definition. This leads you to think that the number of attribute objects must match the number of attribute definitions, and, for most blocks, this is true. However, using the utilities shown in Listings 1-4, you can redefine the attribute objects to be whatever you need.

The listings are shown at the bottom of this page. Or Click here to download the source code.
Listing 1 shows a utility that will retrieve the tags for a particular block in a drawing. The utility can get the tags from the block table, a specific block insert instance or the first occurrence of the block in the drawing. There are two parameters passed to the function. The first is either a string containing the block name or an entity name. The second is a flag that is non-nil when a block name is provided and you want to search the block definition table. The flag is nil if you want the first occurrence of the block inserted into the drawing or if you supply an entity name for the block insert of interest.

The utility function BLOCKTAGS reads the attributes (or attribute definitions) and returns a list of the tag names found. A WHILE loop reads through the entities in either the block definition or the attribute objects following the insertion of the block. In the case of reading the block definition, the WHILE loop will iterate until it has looked at each object in the definition. In this case, it looks for the ATTDEF objects and gets the tag values from the group code 2 elements of each ATTDEF object found. For inserted blocks the routine reads each of the ATTRIB objects and saves the tag names.

BLOCKTAGS is useful when writing programs that work with attributes, you are not sure what is stored in the block definitions and this information differs from what is actually found in the drawing database. Plus, BLOCKTAGS demonstrates the basic process of reading attributes from either location.

(Get_Attribs)
Listing 2 contains another very useful utility function, (Get_Attribs). You can use it with block inserts to get the tags plus values stored in the inserted block. Given a block insertion entity name, the function moves forward to the attributes that are attached following the insert object. Once again, use a WHILE loop to iterate through the ATTRIB objects and return the requested data. In this case, the list returned is a nested list that contains the tag name followed by the value for each ATTRIB found.

For example, suppose you have a block insert containing two attributes named A1 and A2 with values Value1 and Value2, respectively. Calling the function in Listing 2 with the entity name of the block insert will return the list (("A1" "Value1") ("A2" "Value2")), which is in the format of an association list and gives you easy access to your program so you can get specific values.

Following the same basic logic, Listing 3 shows a utility that updates the values for specific attributes in a block insert. The (Put_Attribs) function has two parameters: the block insert entity name and a nested list of the same format-as returned by (Get_Attribs)-that contains the tags and values you want to update. You do not have to supply the complete set of attributes nor do the attributes have to be in the same order as found in the drawing database. This function loops through the attribute objects and matches the tag name against the list of tags to be updated. When a match is found, the entity list of the attribute is written back to the drawing with the modified value stashed inside.

Using Listings 2 and 3 you can write powerful applications that manipulate the attribute values in a set of block insertions. At the Web site listed at the end of this column, you can find a simple application example that uses the put and get functions to write and read attributes in a file with the handles of the block inserts. You can manipulate the file created with a spreadsheet program or some other program to update the appropriate values. Then, an import utility (part of the example provided online) can be used to read the data file and update the appropriate attributes.

## Changing Tag Names

Now, here's the actual question that the attendee asked me at Autodesk University: How do you change the tag names in a block that has already been inserted into the drawing database? Listing 4 contains a utility that does just this. The function (Rename_Tags) will accept a block name, a tag name to replace and the new tag name to use. It then searches the entire drawing for occurrences of the inserted block using a filtered selection set. Once those blocks are isolated into a selection set named SS1, the function loops through each member in the selection set (starting at the back of the set). Moving from the specific block insert objects, the routine goes into a WHILE loop that reads each of the attribute objects attached to the block and updates the tag value when it encounters the name to replace.

Although the attributes inserted into the drawing no longer match the original block definition, the drawing is not considered corrupt in any way. You can still use the attribute extraction functions or command to get the data from the blocks and manipulate the drawing as normal. Just remember that the tag names have changed. Do note that if the block is inserted again, the original tag names will be used. I've left it as an exercise for you to adapt this utility to update the block table by changing the ATTDEF tag names in the block definitions. If the ATTDEF tag names are changed, then future insertions of the block will use the updated tag names for the attached attributes.

Along the same lines, you can shift the locations of the attributes under program control by changing the appropriate group code values for the insertion point, rotation, size and so forth. A regeneration of the drawing will not change these locations or values back to match the block definition because the attributes exist as independent objects in the drawing database. They are just attached to a block insert; the details inside the attributes themselves are their own.

Do note that an attribute object can't exist in the drawing database unless it is attached to a block insertion. Attempting to use ENTMAKE to create an attribute object that is not part of a block insert sequence will not work, and there is no command that allows you to just create an attribute. All attribute objects will be found between an INSERT and SEQEND object set. But the contents of these attribute objects can vary to be whatever your drawing or application requirements need to be. This example set of utilities will help you work with AutoCAD drawings that contain attributes and are not an application by themselves.

## GetAttributes for VBA

VBA programmers will find that the task of obtaining attributes associated with a block reference is much easier. There is a method called GetAttributes associated with the BlockRef object that will return a variant array of AttributeRef objects. Changing the properties TextString and TagString can modify each AttributeRef object as needed. Additional properties are in the AttributeRef that can be modified just as the entity list manipulations have demonstrated. You can learn more about the AttributeRef and BlockRef objects via the Object Browser in the VBA editor (VBAIDE).

Listing 5 shows how to update the tag names using VBA. The subroutine has three parameters with the first being the block reference (insert object) to change. The next two parameters are the old tag name to find and the new tag name to insert in its place. This function uses the GetAttributes method of the block reference object to obtain a variant array of the attribute reference objects. A FOR loop is then used to access each attribute and place it in a variable typed as an attribute reference. If the tag string property matches the old tag parameter, the tag string is updated with the newer value. Once again, VBA appears to show an easier way to obtain similar results. The difference is that the example starts with an entity object already being selected while the AutoLISP example provided in Listing 4 changes all blocks that have the same name. You can modify the VBA example to accomplish the same thing by building a selection set with filter for the block name. Interestingly enough you will find that the number of lines of code will be just about the same for each language!

Whether you use AutoLISP or VBA to customize AutoCAD, you need an understanding of how data is stored in the drawing-especially so when attributes and blocks are involved. These utilities are meant to point you in the right direction and to be added to your programming toolbox. You may want to expand them to meet specific application requirements or simply use them as supplied. If so, please download the source code and do not type in the code as printed in the magazine. Until next time, keep on programmin'.


Listing 1. Access Tags for a Block 

(defun BlockTags (BlckName ;;Master block name
Flg ;;flag; T=from table / EL ;;entity data list Tags ;;list of tags found ) (cond (Flg ;; ;; When FLG is non-nil, get data from ;; the block definitions table. ;; (setq EL (tblsearch "BLOCK" BlckName) EL (entget (cdr (assoc -2 EL))) ) ) ((= (type BlckName) 'STR) ;; ;; If name, get tag information from ;; first item found in selection set. ;; (setq EL (ssget "X" (list '(0 . "INSERT") (cons 2 BlckName))) EL (if EL ;;get ATTRIB object. (entget (entnext (ssname EL 0)))) ) ) ;; ;; If ename, get tag from insert ((= (type BlckName) 'EName) (setq EL (entget BlckName)) (if (and (= (cdr (assoc 0 EL)) "INSERT") (continued from previous column) (= (cdr (assoc 66 EL)) 1)) (setq EL (entget (entnext BlckName)))) ) ) ;; ;; Loop through objects, ;; If FLG is set, read through table ;; otherwise read through the ATTRIB set. ;; (while (and EL (if FLG EL (= (cdr (assoc 0 EL)) "ATTRIB"))) ;; ;; If FLG is set, look for ATTDEF objects. (if (and FLG (= (cdr (assoc 0 EL)) "ATTDEF")) ;;Add ATTDEF tag name to return list (setq Tags (cons (cdr (assoc 2 EL)) Tags))) ;; ;; If Null FLG, get tag from ATTRIB object. (if (null FLG) (setq Tags (cons (cdr (assoc 2 EL)) Tags))) ;; ;; Get the next entity data list. (setq EL (entnext (cdr (assoc -1 EL)))) (if EL (setq EL (entget EL))) ) ;; ;; Reverse response list for return. (reverse Tags) )
Listing 2. Return List of Tags and Values

(defun Get_Attribs (BlckIns ;;entity name
		    /
		    EL  ;;entity data list
		    Attribs ;;return attribs
		    )
  ;;
  ;; Get attribute object data list
  (setq EL (entget (entnext BlckIns)))
  ;;
  ;; Loop through attribute objects
  (while (= (cdr (assoc 0 EL)) "ATTRIB")
    ;;
    ;; Add tag and value to return list
    (setq Attribs
	   (cons
	     (list (cdr (assoc 2 EL))
		   (cdr (assoc 1 EL)))
	     Attribs)
	  ;; Get next attribute object
	  EL (entget
	       (entnext
		 (cdr (assoc -1 EL)))))
  )
  ;; Return values in order found.
  (reverse Attribs)
)
Listing 3. Store Revised Attributes List

 (defun Put_Attribs (BlckIns ;;ename of insert
		    Attribs ;;update values
		    /
		    EL ;;entity data list
		    )
  ;;
  ;; Advance from insert to attribute object
  (setq EL (entget (entnext BlckIns)))
  ;;
  ;; Loop through attribute objects
  (while (= (cdr (assoc 0 EL)) "ATTRIB")
    ;;
    ;; See if attribute object tag name
    ;; is in the update list.
    ;;
    (if (assoc (cdr (assoc 2 EL))
	       Attribs)
      (progn
	;; It is, so update the value in
	;; the entity data list with the
	;; value from the parameter list.
	(setq EL (subst
		   (cons 1 ;;new value
			 (cadr
			   ;;locate new value
			   (assoc
			     (cdr
			       (assoc 2 EL))
			   Attribs)))
		   (assoc 1 EL) ;;old value
		   EL)
	)
	(entmod EL) ;;regen needed for display
      )
    )
    ;; Get the next attribute object
    (setq EL (entget
	       (entnext
		 (cdr (assoc -1 EL)))))
Listing 4. Rename Tags for Block Inserts

(defun Rename_Tags (BlckName ;;master block name
		    TagOld ;;Old tag name
		    TagNew ;;New tag name
		    /
		    SS1 ;;set of inserts
		    CNT ;;number of blocks
		    EL  ;;entity data list
		   )
  ;; Get instances of block insert from DWG.
  (setq SS1 (ssget "X" ;;use filtered search
		   (list
		     '(0 . "INSERT")
		     (cons 2 BlckName))))
  ;;
  ;; Did SSGET find anything?
  (if SS1
    (progn
      ;; Yes, loop through selection set
      (setq Cnt (sslength SS1))
      (repeat Cnt
	;;
	;; Get the entity data list of the
	;; first attribute attached.
	;;
	(setq EL (entget
		   (entnext
		     ;; Get entity name of block
		     ;; insert from SS1.
		     (ssname SS1
			     (SETQ Cnt (1- Cnt))
		     ))))(continued from previous column)
	;;
	;; Loop through Attribute objects
	(while (= (cdr (assoc 0 EL)) "ATTRIB")
	  ;;
	  ;; Does tag name equal "old tag" value?
	  (if (= (cdr (assoc 2 EL)) TagOld)
	    (progn
	      ;;
	      ;;Yes, update tag value in Elist.
	      (setq EL (subst
			 (cons 2 TagNew)
			 (assoc 2 EL)
			 EL))
	      ;;
	      ;;Write modified Elist to drawing.
	      (entmod EL)
	    )
	  )
	  ;;
	  ;;Get next entity 
			  ;;in chain.
	  (setq EL (entget
		     (entnext
		       (cdr (assoc -1 EL)))))
	)
      )
    )
  )
)
;;  
Listing 5. Change Attribute Tag Names in VBA

Sub Change_Attribute_Tags
(Blk As AcadBlockReference, OldTag As String, NewTag As String)
   Dim Attribs As Variant
   Dim Attrib As AcadAttributeReference
   Attribs = Blk.GetAttributes
   For I = LBound(Attribs) To UBound(Attribs)
     Set Attrib = Attribs(I)
     If Attrib.TagString = OldTag Then
        Attrib.TagString = NewTag
     End If
   Next I
End SubC

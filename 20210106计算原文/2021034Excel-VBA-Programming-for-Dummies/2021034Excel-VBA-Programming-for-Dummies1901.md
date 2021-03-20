used drop-down menus and toolbars. Now the Ribbon is the user interface

for Microsoft Office — and Ribbon mania has even spread to other software,

including Windows.

You might expect to be able to create custom Ribbon commands using VBA. The

bad news is that you can’t use VBA to modify the Ribbon. The good news is that

you’re not completely out of luck. This chapter describes some of the ways to work

with Excel’s user interface.

Customizing the Ribbon

This section describes ways to customize the Ribbon. You can modify the Ribbon

manually, but you can’t make changes to the Ribbon by using VBA. Sad, but true.

For example, if you write an application and you’d like to add a few new buttons

CHAPTER 19  Accessing Your Macros through the User Interface    321

to the Ribbon, you need to program those changes outside Excel, using something called RibbonX.

Customizing the Ribbon manually

It’s very easy to make changes to the Ribbon manually, but you must be using

Excel 2010 or later. If you use Excel 2007, you should just skip this section because it doesn’t apply to you.

You can customize the Ribbon in these ways:

» Tabs

•  Add a new custom tab.

•  Delete custom tabs.

•  Add a new group to a tab.

•  Change the order of the tabs.

•  Change the name of a tab.

•  Hide built-in tabs.

» Groups

•  Add new custom groups.

•  Add commands to a custom group.

•  Remove commands from custom groups.

•  Remove groups from a tab.

•  Move a group to a different tab.

•  Change the order of the groups within a tab.

•  Change the name of a group.

That’s a fairly comprehensive list of customization options, but there are some

actions that you  can’t do (no matter how hard you try):

» Remove built-in tabs — but you  can hide them.

» Remove commands from built-in groups.

» Change the order of commands in a built-in group.

322    PART 4  Communicating with Your Users

You make manual changes to the Ribbon in the Customize Ribbon panel of the

Excel Options dialog box (see Figure 19-1). The quickest way to display this dialog

box is to right-click anywhere in the Ribbon and choose Customize the Ribbon

from the shortcut menu.

FIGURE 19-1:

The Customize

Ribbon tab of the

Excel Options

dialog box.

The process of customizing the Ribbon is very similar to customizing the Quick

Access toolbar, which is described later in this chapter. The only difference is that you need to decide where to put the command within the Ribbon. Follow this general procedure:

1. Use the drop-down list on the left (labeled Choose Commands From) to

display various groups of commands.

2. Locate the command in the list box on the left and select it.

3. Use the drop-down list on the right (labeled Customize the Ribbon) to

choose a group of tabs.

Main tabs refer to the tabs that are always visible; Tool tabs refer to the context

tabs that appear when a particular object is selected.

CHAPTER 19  Accessing Your Macros through the User Interface    323

4. In the list box on the right, select the tab and the group where you would

like to put the command.

You need to click the plus-sign controls to expand the hierarchical lists.

5. Click the Add button in the middle to add the selected command from

the left to the group on the right.

Keep in mind that you can click the New Tab button to create a new tab and the

New Group button to create a new group within a tab. New tabs and groups are

given generic names, so you probably want to give them more meaningful names.

Use the Rename button to rename the selected tab or group. You can also rename

built-in tabs and groups.

Figure 19-2 shows a custom group, named Text To Speech, added to the View tab

(to the right of the Zoom group). This new group has four commands.

FIGURE 19-2:

The View tab

with a new

group named

Text To Speech.

Although you can’t remove a built-in tab, you can hide the tab by clearing the

check box next to its name on the Customize Ribbon tab.

Adding a macro to the Ribbon

Fortunately, you can also add macros to the Ribbon. Follow the instructions in the

previous section, but in Step 1, choose Macros from the drop-down list on the left.

All the currently available macros are listed, ready to be added to the Ribbon. You

just need to decide on a tab and group for the macro.

If you customize the Ribbon to include a macro, the macro command on the Ribbon is visible even when the workbook that contains the macro is not open.

Clicking the command opens the workbook that contains the macro and then

executes the macro.

324    PART 4  Communicating with Your Users

If you add a button to the Ribbon that executes a macro, that Ribbon modification applies to your copy of Excel only. The Ribbon modifications are not part of the

workbook. In other words, if you give your workbook to a colleague, the Ribbon

customizations you made won’t appear on the colleague’s system.

Customizing the Ribbon with XML

In some situations, you may want to modify the Ribbon automatically when a workbook or add-in is opened. Doing so makes it easy for the user to access your

macro. It also eliminates the need for the user to modify the Ribbon manually by

using the Excel Options dialog box.

You can make automatic changes to the Ribbon with Excel 2007 and later versions,

but it’s not a simple task. Modifying the Ribbon involves writing XML code in a

text editor, copying that XML file into the workbook file, editing a bunch of XML

files (which also are stashed away inside the Excel file, which in reality is nothing more than a zipped container of individual files), and then writing VBA procedures

to handle the clicking of the controls you put in the XML file.

Fortunately, software is available to assist you with customizing the Ribbon — but

you still need to be on familiar terms with XML.

GETTING THE SOFTWARE

If you’d like to follow along with the Ribbon customization example, you need to download a small program called Custom UI Editor for Microsoft Office. This free program greatly simplifies the process of customizing the Ribbon in Microsoft Office applications.

Using this software still requires a lot of work, but it’s a lot easier than doing it manually.

The download location tends to change, so search the web for  "Custom UI Editor for  Microsoft Office"  to find the software. It’s a small download, and it’s free.

Explaining all the intricate details involved in customizing the Ribbon is well beyond the scope of this book. However, this chapter does walk you through a quick example that demonstrates the steps required to add a new Ribbon group to the Home tab. The new

Ribbon group is named Excel VBA For Dummies, and it contains one button, labeled

Click Me. Clicking that button runs a VBA macro named ShowMessage.

CHAPTER 19  Accessing Your Macros through the User Interface    325

You can download a sample file from this book’s website, which contains this customization. If you’d like to create it yourself, follow these steps exactly:

1. Create a new Excel workbook.

2. Save the workbook, and name it ribbon modification.xlsm.

3. Close the workbook.

4. Launch the Custom UI Editor for Microsoft Office.

If you don’t have this software, you need to find it and install it. Refer to the

nearby sidebar「Getting the software.」

5. In the Custom UI Editor, choose File  ➪ Open and find the workbook you

saved in Step 2.

6. Choose Insert  ➪ Office 2007 Custom UI Part.

Choose this command even if you’re using a Excel 2010 or a later version.

7. Type the following code in the code panel (named customUI.xml)

displayed in the Custom UI Editor (see Figure  19-3):

<customUI xmlns='http://schemas.microsoft.com/office/2006/01/customui'>

<ribbon>

<tabs>

<tab idMso='TabHome'>

<group id'Group1' label='Excel VBA For Dummies'>

<button id='Button1'

label='Click Me'

size='large'

onAction='ShowMessage'

imageMso='FileStartWorkflow'/>

</group>

</tab>

</tabs>

</ribbon>

</customUI>

8. Click the Validate button on the toolbar.

If the code has any syntax errors, you get a message that describes the

problem. If any errors are identified, you must correct them.

326    PART 4  Communicating with Your Users

FIGURE 19-3:

RibbonX code

displayed in the

Custom UI Editor.

9. Click the Generate Callback button.

The Custom UI Editor creates a VBA Sub procedure that is executed when the

button is clicked (see Figure 19-4). This procedure is not actually inserted into

the workbook, so you need to copy it for later use (or memorize it, if you have

a good memory).

FIGURE 19-4:

The VBA callback

procedure that is

executed by

clicking the

Ribbon button.

10. Go back to the customUI.xml module and choose File  ➪ Save (or click the  Save icon on the toolbar).

11. Close the file by choosing File  ➪ Close.

12. Open the workbook in Excel, and click the Home tab.

You should see the new Ribbon group and Ribbon button. But it doesn’t

work yet.

CHAPTER 19  Accessing Your Macros through the User Interface    327

13. Press Alt+F11 to activate the VBE.

14. Insert a new VBA module; paste (or type) the callback procedure that was

generated in Step 9; and add a MsgBox statement, so you’ll know whether

the procedure is actually being executed.

The procedure is

Sub ShowMessage(control As IRibbonControl)

MsgBox "Congrats. You found the new ribbon command."

End Sub

15. Press Alt+F11 to jump back to Excel, and click the new button on the

Ribbon.

If all goes well, you see the MsgBox shown in Figure 19-5.

FIGURE 19-5:

Proof that adding

a new Ribbon

command using

XML is actually

possible.

In the Custom UI Editor, when you choose Insert ➪ Office 2007 Custom UI Part, you

insert a UI part for Excel 2007. The Custom UI Editor also has an option to insert

a UI part for Excel 2010 (this software hasn’t been updated for subsequent versions

of Office). For maximum compatibility, use the Excel 2007 Custom UI Part.

You probably realize that modifying the Ribbon using XML is not exactly intuitive.

Even with a good tool to help (such as the Custom UI Editor), you still need to

understand XML. If that sounds appealing to you, search the web or find a book

devoted exclusively to customizing the Ribbon interface in Microsoft Office. This

book isn’t one of them.

328    PART 4  Communicating with Your Users

ADDING A BUTTON TO THE

QUICK ACCESS TOOLBAR

If you create a macro that you use frequently, you may want to add a new button to the Quick Access toolbar. Doing so is easy, but you must do it manually. The Quick Access toolbar is intended to be customized by end users only — not programmers. Here’s

how to do it:

1. Right-click the Quick Access toolbar and select Customize Quick Access

toolbar from the shortcut menu to display the Quick Access toolbar tab

of the Excel Options dialog box.

2. From the drop-down list labeled Choose Commands From, select Macros.

3. Select your macro from the list.

4. Click the Add button to add the macro to the Quick Access toolbar list on the  right.

5. If you like, click the Modify button to change the icon and (optionally) the

display name.

When you click a macro button on the Quick Access toolbar, the workbook that con-

tains the macro is opened (if it’s not already open). And the macro can be executed

when any workbook is open.

You’ll also find an option to display the Quick Access toolbar button only when a

particular workbook is open. Before you add the macro, use the drop-down control at

the top-right of the Excel Options dialog box and specify the workbook name rather

than For All Documents (Default).

If you have macros that are useful for many workbooks, storing them in your Personal Macro Workbook is a good idea.

Because this XML stuff is way too complex for the beginner VBA programmer, the

remainder of this chapter focuses on UI customization that uses the  old method (VBA only): specifically, how to customize shortcut menus. It’s not as slick as the

Ribbon, but it’s a lot easier, and it still provides quick access to your macros.

Customizing Shortcut Menus

Before Excel 2007, VBA programmers used the CommandBar object for creating

custom menus, custom toolbars, and custom shortcut (right-click) menus.

CHAPTER 19  Accessing Your Macros through the User Interface    329

Beginning with Excel 2007, the CommandBar object is in a rather odd position.

If you write code to customize a menu or a toolbar, Excel intercepts that code and

ignores many of your commands. Instead of displaying your well-thought-out

interface enhancement, Excel 2007 (like later versions) simply dumps your

customized menus and toolbars into a catch-all Ribbon tab named Add-Ins.

Menu and toolbar customizations end up in the Add-Ins ➪ Menu Commands or the

Add-Ins ➪ Custom Toolbars group. But customizing shortcut menus (which also

uses the CommandBar object) still works as it always has — well, sort of. See

「What’s different since Excel 2007?」later in this chapter.

Bottom line? The CommandBar object is not very useful anymore, but it remains

the only way to customize shortcut menus.

Adding a new item to the

Cell shortcut menu

This section contains sample code that adds a new item to the shortcut menu that

appears when you right-click a cell. Although the technical details are out of the

scope for this book, you should be able to adapt these examples to your needs.

Chapter 16 describes the Change Case utility. You can enhance that utility a bit by

making it available from the Cell shortcut menu.

This example is available at this book’s website.

The AddToShortcut procedure adds a new menu item to the Cell shortcut menu.

You can adapt it to point to your own macros by changing the Caption and OnAction properties of the object named NewControl.

Sub AddToShortCut()

Dim Bar As CommandBar

Dim NewControl As CommandBarButton

DeleteFromShortcut

Set Bar = Application.CommandBars("Cell")

Set NewControl = Bar.Controls.Add _

(Type:=msoControlButton, ID:=1, _

temporary:=True)

With NewControl

.Caption = "&Change Case"

.OnAction = "ChangeCase"

.Style = msoButtonIconAndCaption

End With

End Sub

330    PART 4  Communicating with Your Users

When you modify a shortcut menu, that modification remains in effect until you

restart Excel. In other words, modified shortcut menus don’t reset themselves when you close the workbook that contains the VBA code. Therefore, if you write

code to modify a shortcut menu, you almost always write code to reverse the effect

of your modification.

The DeleteFromShortcut procedure removes the new menu item from the Cell

shortcut menu:

Sub DeleteFromShortcut()

On Error Resume Next

Application.CommandBars("Cell").Controls _

("&Change Case").Delete

End Sub

Figure 19-6 shows the new menu item displayed after you right-click a cell.

FIGURE 19-6:

The Cell shortcut

menu showing

a custom

menu item:

Change Case.

The first actual command after the declaration of a couple of variables calls the

DeleteFromShortcut procedure. This statement ensures that only one Change Case

menu item appears on the shortcut Cell menu. Try commenting out that line (put

an apostrophe at the start of the line) and running the procedure a few times — but

don’t get carried away! Right-click a cell, and you can see multiple instances of the CHAPTER 19  Accessing Your Macros through the User Interface    331

Change Case menu item. Get rid of all the entries by running DeleteFromShortcut multiple times (once for each extra menu item).

Finally, you need a way to add the shortcut menu item when the workbook is opened and to delete the menu item when the workbook is closed. Doing this is

easy . . . if you’ve read Chapter 11. Just add these two event procedures to the ThisWorkbook code module:

Private Sub Workbook_Open()

Call AddToShortCut

End Sub

Private Sub Workbook_BeforeClose(Cancel As Boolean)

Call DeleteFromShortcut

End Sub

The Workbook_Open procedure is executed when the workbook is opened, and

the Workbook_BeforeClose procedure is executed before the workbook is closed.

Just what the doctor ordered.

What’s different since Excel 2007?

If you’ve used VBA to work with shortcut menus in Excel 2007 or earlier, you need

to be aware of a significant change.

In the past, if your code modified a shortcut menu, that modification was in effect

for all workbooks. For example, if you added a new item to the Cell right-click

menu, that new item would appear when you right-clicked a cell in  any workbook (plus other workbooks that you open later on). In other words, shortcut menu modifications were made at the  application level.

Excel 2013 and later versions use a single document interface, and that affects shortcut menus. Changes that you make to shortcut menus affect only the active

workbook window. When you execute the code that modifies the shortcut menu,

the shortcut menu for windows other than the active window aren’t changed. This

is a radical departure from how things used to work.

Another twist: If the user opens a workbook (or creates a new workbook) when the

active window displays the modified shortcut menu, the new workbook also dis-

plays the modified shortcut menu. In other words, new windows display the same

shortcut menus as the window that was active when the new windows were opened.

Bottom line: In the past, if you opened a workbook or add-in that modified shortcut menus, you could be assured that the modified shortcut menus would be

available in all workbooks. You no longer have that assurance.

332    PART 4  Communicating with Your Users

5Putting It All

Together

IN THIS PART . . .

Find out why you might want to create custom

worksheet functions.

Make your custom functions work just like Excel’s

built-in functions.

Discover Excel add-ins.

Create simple add-ins.

IN THIS CHAPTER

» Knowing why custom worksheet

functions are so useful

» Understanding the basics of custom

worksheet functions

» Writing your own functions

» Exploring functions that use various

types of arguments

» Examining function examples

» Understanding the Insert Function

dialog box

Chapter 20

Creating Worksheet

Functions — and Living

to Tell about It

F or many macro mavens, VBA’s main attraction is the capability to create

customworksheetfunctions —functionsthatlook,work,andfeeljustlikethose that Microsoft built into Excel. A  custom function offers the addedadvantageofworkingexactlyhowyouwantitto(because you wroteit).Chapter 5introducestheconceptofcustomfunctions.Inthischapter,youtakeadeeperdivewithsomereal-worldexamples.

CHAPTER 20  Creating Worksheet Functions — and Living to Tell about It    335

Why Create Custom Functions?

You’reundoubtedlyfamiliarwithExcel’sworksheetfunctions;evenExcelnovicesknow how to use common worksheet functions such as SUM, AVERAGE, and

IF. Excelcontainsmorethan450predefinedworksheetfunctions.Andifthat’snotenough,youcancreatefunctionsbyusingVBA.

WHAT CUSTOM WORKSHEET

FUNCTIONS CAN’T DO

As you develop custom functions for use in your worksheet formulas, it’s important that you understand a key point. VBA worksheet Function procedures are essentially  passive.

For example, code within a Function procedure cannot manipulate ranges, change

formatting, or do many of the other things that are possible with a Sub procedure.

An example may help.

It might be useful to create a function that changes the color of text in a cell based on the cell’s value. Try as you might, however, you can’t write such a function. It always returns an error value.

Just remember this: A function used in a worksheet formula returns a value. It doesn’t perform actions with objects.

That said, this rule has a few exceptions. For example, here’s a Function procedure that changes the text in a cell comment:

Function ChangeComment(cell, NewText)

cell.Comment.Text NewText

End Function

And here’s a formula that uses the function. It works only if cell A1 already has a

comment. When the formula is calculated, the comment is changed.

=ChangeComment(A1,"I changed the comment!")

It’s unclear whether this is an oversight or a feature. But it’s a rare example of a VBA function that changes something in a worksheet.

336    PART 5  Putting It All Together

WithallthefunctionsavailableinExcelandVBA,youmaywonderwhyyouwouldeverneedtocreatefunctions.Theanswer:tosimplifyyourwork.Withabitofplanning, custom functions are very useful in worksheet formulas and VBA

procedures.Often,forexample,youcansignificantlyshortenaformulabycreat-

ingacustomfunction.Afterall,shorterformulasaremorereadableandeasiertowork with.

Understanding VBA Function Basics

A VBA  function isaprocedurethat’sstoredinaVBAmodule.YoucanusethesefunctionsinotherVBAproceduresorinyourworksheetformulas.Customfunctionscan’tbecreatedwiththemacrorecorder,althoughthemacrorecordercanhelpyouidentifyrelevantpropertiesandmethods.

A  module can contain any number of functions. You can use a custom function in aformulajustasthoughitwereabuilt-infunction.Ifthefunctionisdefinedin adifferentworkbook,however,youmustprecedethefunctionnamewiththeworkbook name. Suppose that you develop a function called DiscountPrice

(which takes one argument) and the function is stored in a workbook namedpricing.xlsm.

Tousethisfunctioninthepricing.xlsmworkbook,enteraformulasuchasthis:

=DiscountPrice(A1)

Ifyouwanttousethisfunctionina different workbook, enter a formula such as this(andmakesurethepricing.xlsmfileisopen):

=pricing.xlsm!discountprice(A1)

If the custom function is stored in an add-in, you don’t need to precede the

function name with the workbook name. Chapter 21 provides an overview ofadd-ins.

CustomfunctionsappearintheInsertFunctiondialogbox,intheUserDefinedcategory.PressingShift+F3isonewaytodisplaytheInsertFunctiondialogbox.

CHAPTER 20  Creating Worksheet Functions — and Living to Tell about It    337

Writing Functions

Rememberthatafunction’snameactslikeavariable.Thefinalvalueofthisvari-

ableisthevaluereturnedbythefunction.Todemonstrate,examinethefollowingfunction,whichreturnstheuser’sfirstname: Function FirstName()

Dim FullName As String

Dim FirstSpace As Long

FullName = Application.UserName

FirstSpace = InStr(FullName, " ")

If FirstSpace = 0 Then

FirstName = FullName

Else

FirstName = Left(FullName, FirstSpace - 1)

End If

End Function

ThisfunctionstartsbyassigningtheUserNamepropertyoftheApplicationobjecttoavariablenamedFullName.Next,itusestheVBAInStrfunctiontolocatethepositionofthefirstspaceinthename.Ifthereisnospace,FirstSpaceisequalto 0,andFirstNameisequaltotheentirename.IfFullName does have a space, the Left functionextractsthetexttotheleftofthespaceandassignsittoFirstName.

NoticethatFirstNameisthenameofthefunctionandisalsousedasavariablename  in thefunction.ThefinalvalueofFirstNameisthevaluethat’sreturnedbythefunction.Severalintermediatecalculationsmaybegoingoninthefunction,butthefunctionalwaysreturnsthelastvalueassignedtothevariablethatisthesame as the function’s name.

All the examples in this chapter are available at this book’s website.

Working with Function Arguments

Toworkwithfunctions,youneedtounderstandhowtoworkwitharguments.Anargumentisnotadisagreementbetweenvariables.Rather,it’sinformationthatispassedtothefunctionandthenusedbythefunctiontodoitsthing.

ThefollowingpointsapplytotheargumentsforExcelworksheetfunctionsandcustomVBAfunctions: 338    PART 5  Putting It All Together

»  Arguments can be cell references, variables (including arrays), constants, literal values, or expressions.

» Some functions have no arguments.

» Some functions have a fixed number of required arguments.

» Some functions have a combination of required and optional arguments.

The examples in this section demonstrate how to work with various types ofarguments.

A function with no argument

Somefunctionsdon’tuseanyarguments.Forexample,Excelhasafewbuilt-inworksheet functions that don’t use arguments. These include RAND, TODAY,andNOW.

Here’sanexampleofacustomfunctionwithnoarguments.Thefollowingfunc-

tionreturnstheUserNamepropertyoftheApplicationobject.ThisnameappearsintheGeneraltaboftheExcelOptionsdialogbox.Thissimplebutusefulexampleshowstheonlywayyoucangettheuser’snametoappearinaworksheetcell: Function User()

'  Returns the name of the current user

User = Application.UserName

End Function

Whenyouenterthefollowingformulaintoaworksheetcell,thecelldisplaysthecurrentuser’sname:

=User()

AswiththeExcelbuilt-infunctions,youmustincludeasetofemptyparentheseswhenusingafunctionwithnoarguments.Otherwise,Exceltriestointerpretthefunctionasanamedrange.

A function with one argument

Thesingle-argumentfunctioninthissectionisdesignedforsalesmanagerswhoneedtocalculatethecommissionsearnedbytheirsalespeople.Thecommissionrate depends on the monthly sales volume; those who sell more earn a highercommission rate. The function returns the commission amount based on themonthlysales(whichisthefunction’sonlyargument —arequiredargument).

ThecalculationsinthisexamplearebasedonTable 20-1.

CHAPTER 20  Creating Worksheet Functions — and Living to Tell about It    339

TABLE 20-1

Commission Rates by Sales

Monthly Sales

Commission Rate

$0–$9,999

8.0%

$10,000–$19,999

10.5%

$20,000–$39,999

12.0%

$40,000+

14.0%

Youcanuseseveralapproachestocalculatecommissionsforsalesamountsenteredinto a worksheet. You  could writealengthyworksheetformulasuchasthis:

=IF(AND(A1>=0,A1<=9999.99),A1*0.08,IF(AND(A1>=10000,

A1<=19999.99),A1*0.105,IF(AND(A1>=20000,A1<=39999.99),

A1*0.12,IF(A1>=40000,A1*0.14,0))))

Acoupleofreasonsmakethisabadapproach.First,theformulaisoverlycomplex.

Second,thevaluesarehard-codedintotheformula,makingtheformuladifficulttomodifyifthecommissionstructurechanges.

A better approach is to create a table of commission values and use a LOOKUPtablefunctiontocomputethecommissions:

=VLOOKUP(A1,Table,2)*A1

Anotherapproach,whichdoesn’trequireatableofcommissions,istocreateacustomfunction: Function Commission(Sales)

'  Calculates sales commissions

Const Tier1 As Double = 0.08

Const Tier2 As Double = 0.105

Const Tier3 As Double = 0.12

Const Tier4 As Double = 0.14

Select Case Sales

Case 0 To 9999.99: Commission = Sales * Tier1

Case 10000 To 19999.99: Commission = Sales * Tier2

Case 20000 To 39999.99: Commission = Sales * Tier3

Case Is >= 40000: Commission = Sales * Tier4

End Select

Commission = Round(Commission, 2)

End Function

340    PART 5  Putting It All Together

Notice that the four commission rates are declared as constants rather than

hard-codedinthestatements.Thismakesitveryeasytomodifythefunctionifthecommissionrateschange.

After you define this function in a VBA module, you can use it in a worksheet

formula.Enteringthefollowingformulaintoacellproducesaresultof3,000.Theamountof25,000qualifiesforacommissionrateof12percent:

=Commission(25000)

Figure 20-1showsaworksheetthatusestheCommissionfunctioninformulasincolumn C.

FIGURE 20-1:

Using the

Commission

function in a

worksheet.

A function with two arguments

Thenextexamplebuildsontheprecedingone.Imaginethatthesalesmanagerimplementsanewpolicytorewardlong-termemployees:Thetotalcommissionpaid increases by 1 percent for every year the salesperson has been with thecompany.

YoucanmodifytheCommissionfunction(definedintheprecedingsection)sothatittakestwoarguments,bothofwhicharerequiredarguments.CallthisnewfunctionCommission2: Function Commission2(Sales, Years)

'  Calculates sales commissions based on years in service

Const Tier1 As Double = 0.08

Const Tier2 As Double = 0.105

Const Tier3 As Double = 0.12

Const Tier4 As Double = 0.14

CHAPTER 20  Creating Worksheet Functions — and Living to Tell about It 341

Select Case Sales

Case 0 To 9999.99: Commission2 = Sales * Tier1

Case 10000 To 19999.99: Commission2 = Sales * Tier2

Case 20000 To 39999.99: Commission2 = Sales * Tier3

Case Is >= 40000: Commission2 = Sales * Tier4

End Select

Commission2 = Commission2 + (Commission2 * Years / 100)

Commission2 = Round(Commission2, 2)

End Function

Theproceduresimplyaddsthesecondargument(Years)totheFunctionstate-

mentandincludesanadditionalcomputationthatadjuststhecommissionbeforeexitingthefunction.Thisadditionalcomputationmultipliestheoriginalcommissionbythenumberofyearsinservices,dividesby100,andthenaddstheresulttotheoriginalcomputation.

Here’s an example of how you can write a formula by using this function. (ItassumesthatthesalesamountisincellA1;cellB1specifiesthenumberofyearsthesalespersonhasworked.)

=Commission2(A1,B1)

Figure 20-2showsaworksheetthatusestheCommission2function.

FIGURE 20-2:

Using the

Commission2

function, which

takes two

arguments.

A function with a range argument

Usingaworksheetrangeasanargumentisnotatalltricky;Exceltakescareofthebehind-the-scenesdetails.

342    PART 5  Putting It All Together

Here’sasimplebutusefulfunctionthatconcatenatesthecontentsofarange.Ittakes two arguments: InRange (the worksheet range to be concatenated), and

Delim(oneormoredelimitercharacters,tobeinsertedbetweencells).

Function JoinText(InRange, Delim)

Dim Cell As Range

For Each Cell In InRange

JoinText = JoinText & Cell.Value & Delim

Next Cell

JoinText = Left(JoinText, Len(JoinText) - Len(Delim))

End Function

ItusesaForEach-Nextconstructtoloopthrougheachcellintherange.Itcon-

catenatesthecellcontents,followedbytheDelimcharacter(s).Thelaststatementremovesthefinaldelimiter,whichisnotneededbecausetherearenomoreitems.

Figure 20-3showsanexample.Thesecondargumentisatwo-characterstring(acommafollowedbyaspace).

FIGURE 20-3:

Using the JoinText

function to

concatenate cells.

Here’sanotherexampleofafunctionthatusesarangeargument.AssumethatyouwanttocalculatetheaverageofthefivelargestvaluesinarangenamedData.

Excel doesn’t have a function that can do this, so you would probably write aformula:

=(LARGE(Data,1)+LARGE(Data,2)+LARGE(Data,3)+

LARGE(Data,4)+LARGE(Data,5))/5

ThisformulausesExcel’sLARGEfunction,whichreturnsthe n thlargestvalueinarange.TheformulaaddsthefivelargestvaluesintherangenamedDataandthendividestheresultby5.Theformulaworksfine,butit’sratherunwieldy.Andwhatifyoudecidethatyouneedtocomputetheaverageofthetopsixvalues?Youwouldneedtorewritetheformula —andmakesurethatyouupdateallcopiesofthe formula.

CHAPTER 20  Creating Worksheet Functions — and Living to Tell about It 343

Wouldn’tthisbeeasierifExcelhadafunctionnamedTopAvg?Thenyoucouldcomputetheaveragebyusingthefollowing(nonexistent)function:

=TopAvg(Data,5)

Thisexampleshowsacaseinwhichacustomfunctioncanmakethingsmucheasierforyou.ThefollowingcustomVBAfunction,namedTopAvg,returnstheaverageofthe N largestvaluesinarange: Function TopAvg(InRange, N)

'  Returns the average of the highest N values in InRange

Dim Sum As Double

Dim i As Long

Sum = 0

For i = 1 To N

Sum = Sum + WorksheetFunction.Large(InRange, i)

Next i

TopAvg = Sum / N

End Function

Thisfunctiontakestwoarguments:InRange(whichisaworksheetrange)andN

(thenumberofvaluestoaverage).ItstartsbyinitializingtheSumvariableto0.ItthenusesaFor-Nextlooptocalculatethesumofthe N largestvaluesintherange.

NotetheExcelLARGEfunctionwithintheloop.Finally,TopAvgisassignedthevalueoftheSumdividedby N .

You can use all Excel worksheet functions in your VBA procedures  except those that haveequivalentsinVBA. Forexample,VBAhasaRndfunctionthatreturnsa random number. Therefore, you can’t use the Excel RAND function in a VBAprocedure.

A function with an optional argument

Many Excel built-in worksheet functions use optional arguments. An exampleis theLEFTfunction,whichreturnscharactersfromtheleftsideofastring.Itsofficialsyntaxfollows: LEFT(text[,num_chars])

Thefirstargumentisrequired,butthesecond(insquarebrackets)isoptional.Ifyouomittheoptionalargument,Excelassumesavalueof1.Therefore,thefollowingformulasreturnthesameresult:

=LEFT(A1,1)

=LEFT(A1)

344    PART 5  Putting It All Together

ThecustomfunctionsyoudevelopinVBAalsocanhaveoptionalarguments.Youspecifyanoptionalargumentbyprecedingtheargument’snamewiththekeywordOptional.Theargument’snameisthenfollowedbyanequalsignandthedefaultvalue.Iftheoptionalargumentismissing,thecodeusesthedefaultvalue.

One caveat: If you use optional arguments, they must always come after allrequiredargumentsintheargumentlist.

Thefollowingexampleshowsacustomfunctionthatusesanoptionalargument:

Function DrawOne(InRange, Optional Recalc = 0)

'  Chooses one cell at random from a range

Randomize

'  Make function volatile if Recalc is 1

If Recalc = 1 Then Application.Volatile True

'  Determine a random cell

DrawOne = InRange(Int((InRange.Count) * Rnd + 1))

End Function

DEBUGGING CUSTOM FUNCTIONS

Debugging a Function procedure can be a bit more challenging than debugging a Sub

procedure. If you develop a function for use in worksheet formulas, you find that an error in the Function procedure simply results in an error display in the formula cell (usually, #VALUE!). In other words, you don’t receive the normal runtime error message that helps you locate the offending statement.

You can choose among three methods for debugging custom functions:

• Place MsgBox functions at strategic locations to monitor the value of specific variables. Fortunately, message boxes in Function procedures pop up when you exe-

cute the procedure. Make sure that only one formula in the worksheet uses your

function. Otherwise, the message boxes appear for each formula that’s evaluated —

which could get very annoying.

• Test the procedure by calling it from a Sub procedure. Runtime errors normally appear in a pop-up window, and you can either correct the problem (if you know it)

or jump right into the debugger.

• Set a breakpoint in the function and then use the Excel debugger to step through the function. You can then access all the usual debugging tools. Refer to Chapter 13

to find out about the debugger.

CHAPTER 20  Creating Worksheet Functions — and Living to Tell about It 345

Thisfunctionrandomlychoosesonecellfromaninputrange.Therangepassedasanargumentisactuallyanarray,andthefunctionselectsoneitemfromthearrayatrandom.(SeeChapter 7forarefresheronarrays.)Ifthesecondargumentis1,theselectedvaluechangeswhenevertheworksheetisrecalculated.(Thefunctionismade volatile. )Ifthesecondargumentis0(orisomitted),thefunctionisnotrecalculatedunlessoneofthecellsintheinputrangeismodified.

The Randomize statement ensures that a different random number「seed」is

chosen each time the workbook is opened. Without this statement, the same

randomnumbersaregeneratedeachtimetheworkbookisopened.

Youcanusethisfunctionforchoosinglotterynumbers,selectingawinnerfromalistofnames,andsoon.

Introducing Wrapper Functions

Thissectioncontainssomerelativelysimplewrapperfunctionsthatcanbeusefulinawidearrayoftasks.

Wrapperfunctionsconsistofcodethat’swrappedaroundintrinsicVBAelements.

Inotherwords,theyallowyoutouseVBAfunctionsinworksheetformulas.

The earlier section in this chapter,「A function with no argument,」shows anexampleofawrapperfunction: Function User()

'  Returns the name of the current user

User = Application.UserName

End Function

Thisfunction,inessence,letsyourformulasaccesstheUserNamepropertyofthe

Applicationobject.

Theremainderofthissectioncontainssomeadditionalwrapperfunctions.

The NumberFormat function

Thisfunctionsimplydisplaysthenumberformatforacell.Itcanbeusefulifyouneedtoensurethatagroupofcellsallhavethesamenumberformat.

346    PART 5  Putting It All Together

Function NumberFormat(Cell)

'  Returns the cell's number format

NumberFormat = Cell(1).NumberFormat

End Function

NoticetheuseofCell (1)?Ifamulticellrangeisusedasanargument,onlythefirstcellisused.

Youcaneasilywritesimilarfunctionsthatreturnacell’stextcolor,backgroundcolor,font,andsoon.

The ExtractElement function

Thiswrapperfunctionreturnsasubstringfromatextstringthatcontainsmul-

tiple elements, separated by a separator character. For example, this formulareturns cow,whichisthethirdelementinastringthatusesaspaceasaseparator.

Thearguments,ofcourse,couldbecellreferences.

=ExtractElement("dog horse cow cat", 3, " ")

Here’sthecode,whichisawrapperforVBA’sSplitfunction:

Function ExtractElement(Txt, n, Sep)

'  Returns the nth element of a text string, where the

'  elements are separated by a specified separator character

ExtractElement = Split(Application.Trim(Txt), Sep)(n - 1)

End Function

Figure 20-4 shows the ExtractElement function used in worksheet formulas.

Column A contains the text string, Column B contains the element number tobe extracted,andColumnCcontainsthedelimiter(cellsthatappeartobeblankcontain a space character).

FIGURE 20-4:

Using the

ExtractElement

function to

return an

element from

a string.

CHAPTER 20  Creating Worksheet Functions — and Living to Tell about It 347

The SayIt function

ThissimplefunctionisawrapperfortheSpeakmethodoftheApplication.Speechobject.Itusesasynthesizedvoiceto「speak」theargument.

Function SayIt(txt)

'  Speaks the argument

Application.Speech.Speak txt, True

End Function

Here’sanexample:

=IF(C10>10000,SayIt("Over budget"),"OK")

The formula checks cell C10. If the value is greater than 10,000, the functionspeaksthetext:「Overbudget.」Ifthevalueislessthan10,000,thefunctiondisplaysthetextOK(anddoesn’tsayanything).

Usesparingly.Ifyouusethisfunctionmorethanonetime,itcanbeveryconfusing.

Also,rememberthatthisfunctionisevaluatedeachtimetheworksheetiscalculated,sothevoicemaygetveryannoyingifyou’remakingmanychanges.Thisfunctionisprobablymoresuitedforamusementpurposes.

The IsLike function

VBA’sLikeoperatorisaveryflexiblewaytocomparetextstrings.Checkitoutinthe VBA Help system. This function brings that power to your worksheetformulas: Function IsLike(text, pattern)

'  Returns true if the first argument is like the second

IsLike = text Like pattern

End Function

Working with Functions That

Return an Array

ArrayformulasareoneofExcel’smostpowerfulfeatures.Ifyou’refamiliarwitharray formulas, you’ll be happy to know that you can create VBA functions that return an array.

348    PART 5  Putting It All Together

Returning an array of month names

AsimpleexampleofanarrayistheMonthNamesfunction.Itreturnsa12-elementarrayof —youguessedit —monthnames.

Function MonthNames()

MonthNames = Array("January", "February", "March", _

"April", "May", "June", "July", "August", _

"September", "October", "November", "December") End Function

TousetheMonthNamesfunctioninaworksheet,youmustenteritasa12-cellarrayformula.Forexample,selectrangeA2:L2andenter =MonthNames() .Thenpress Ctrl+Shift+Entertoenterthearrayformulainall12selectedcells.Figure 20-5shows the result.

FIGURE 20-5:

Using the

MonthNames

function to

return a

12-element

array.

Ifyouwantthemonthnamestodisplayinacolumn,select12cellsinacolumnandusethisarrayformula.(Don’tforgettoenteritbypressingCtrl+Shift+Enter.)

=TRANSPOSE(MonthNames())

Youcanalsopickoutasinglemonthfromthearray.Here’saformula(notanarrayformula)thatdisplaysthefourthelementofthearray:April.

=INDEX(MonthNames(),4)

Returning a sorted list

Supposethatyouhavealistofnamesyouwanttoshowinsortedorderinanotherrangeofcells.Wouldn’titbenicetohaveaworksheetfunctiondothatforyou?

Thecustomfunctioninthissectiondoesjustthat:Ittakesasingle-columnrangeofcellsasitsargumentandthenreturnsanarrayofthosecellssorted.Figure 20-6showshowitworks.RangeA2:A13containssomenames.RangeC2:C13contains

CHAPTER 20  Creating Worksheet Functions — and Living to Tell about It 349

this multicell array formula. (Remember that you must enter the formula bypressingCtrl+Shift+Enter.)

=Sorted(A2:A13)

FIGURE 20-6:

Using a custom

function to return

a sorted range.

Here’sthecodefortheSortedfunction:

Function Sorted(Rng As Range)

Dim SortedData() As Variant

Dim Cell As Range

Dim Temp As Variant, i As Long, j As Long

Dim NonEmpty As Long

'  Transfer data to SortedData

For Each Cell In Rng

If Not IsEmpty(Cell) Then

NonEmpty = NonEmpty + 1

ReDim Preserve SortedData(1 To NonEmpty)

SortedData(NonEmpty) = Cell.Value

End If

Next Cell

'  Sort the array

For i = 1 To NonEmpty

For j = i + 1 To NonEmpty

If SortedData(i) > SortedData(j) Then

Temp = SortedData(j)

SortedData(j) = SortedData(i)

SortedData(i) = Temp

350    PART 5  Putting It All Together

End If

Next j

Next i

'  Transpose the array and return it

Sorted = Application.Transpose(SortedData)

End Function

The Sorted function starts by creating an array named SortedData. This array

contains all the nonblank values in the argument range. Next, the SortedDataarrayissorted,usingabubble-sortalgorithm.Becausethearrayisahorizontalarray,itmustbetransposedbeforeit’sreturnedbythefunction.

TheSortedFunctionworkswitharangeofanysize,aslongasit’sinasinglecol-

umnorrow.Iftheunsorteddataisinarow,yourformulaneedstouseExcel’s

TRANSPOSEfunctiontodisplaythesorteddatahorizontally.Forexample:

=TRANSPOSE(Sorted(A16:L16))

Using the Insert Function Dialog Box

TheExcelInsertFunctiondialogboxisahandytoolthatallowsyoutochooseaworksheet function from a list and prompts you for the function’s arguments.

As notedearlierinthischapter,yourcustomworksheetfunctionsalsoappearinthe Insert Function dialog box. Custom functions appear in the User Definedcategory.

FunctionproceduresdefinedwiththePrivatekeyworddon’tappearintheInsert

Functiondialogbox.Therefore,ifyouwriteaFunctionprocedurethat’sdesignedtobeusedonlybyotherVBAprocedures(butnotinformulas),youshoulddeclarethefunctionasPrivate.

Displaying the function’s description

TheInsertFunctiondialogboxdisplaysadescriptionofeachbuilt-infunction.

ButasshowninFigure 20-7,acustomfunctiondisplaysthefollowingtextasitsdescription:No help available.

CHAPTER 20  Creating Worksheet Functions — and Living to Tell about It 351

FIGURE 20-7:

By default, the

Insert Function

dialog box

doesn’t provide a

description for

custom functions.

TodisplayameaningfuldescriptionofyourcustomfunctionintheInsertFunc-

tiondialogbox,performafewadditional(nonintuitive)steps:

1. Activate a worksheet in the workbook that contains the custom function.

2. Choose Developer  ➪   Code  ➪   Macros (or press Alt+F8).

The Macro dialog box appears.

3. In the Macro Name field, type the function’s name.

Note that the function doesn’t appear in the list of macros; you must type the

name.

4. Click the Options button.

The Macro Options dialog box appears.

5. In the Description field, type a description of the function.

6. Click OK.

7. Click Cancel.

NowtheInsertFunctiondialogboxdisplaysthedescriptionofyourfunction(see

Figure 20-8).

Customfunctions,bydefault,arelistedintheUserDefinedcategory.Toaddafunctiontoadifferentcategory,youneedtouseVBA. Thisstatement,whenexecuted,addstheTopAvgfunctiontotheMath&Trigcategory(whichiscategory3): Application.MacroOptions Macro:="TopAvg", Category:=3

352    PART 5  Putting It All Together

FIGURE 20-8:

The custom

function now

displays a

description.

ChecktheHelpsystemforothercategorynumbers.

Youneedtoexecutethisstatementonlyonetime.Afteryouexecuteit(andsavetheworkbook),thecategorynumberispermanentlyassignedtothefunction.

Adding argument descriptions

When you access a built-in function from the Insert Function dialog box, the

Function Arguments dialog box displays descriptions of the arguments (see

Figure 20-9).

FIGURE 20-9:

By default,

the Function

Arguments

dialog box

displays

Function

argument

descriptions

for built-in

functions only.

CHAPTER 20  Creating Worksheet Functions — and Living to Tell about It    353

Inthepast,itwasnotpossibletoaddargumentdescriptions.Butbeginningwith

Excel 2010, Microsoft finally implemented this feature. You provide argumentdescriptions by using the MacroOptions method. Here’s an example that addsdescriptionsfortheargumentsusedbytheTopAvgfunction: Sub AddArgumentDescriptions()

Application.MacroOptions Macro:="TopAvg", _

ArgumentDescriptions:= _

Array("Range that contains the values", _

"Number of values to average")

End Sub

Youneedtoexecutethisprocedureonlyonetime.Afteryouexecuteit,theargu-

mentdescriptionsarestoredintheworkbookandareassociatedwiththefunction.

NoticethattheargumentdescriptionsappearasargumentsfortheArrayfunction.

You must use the Array function even if you’re assigning a description for a

functionthathasonlyoneargument.

This chapter provides lots of information about creating custom worksheet

functions.Usetheseexamplesasmodelswhenyoucreatefunctionsforyourownwork.Asusual,theonlinehelpprovidesadditionaldetails.TurntoChapter 21ifyou want to find out how to make your custom functions more accessible by

storingtheminanadd-in.

354    PART 5  Putting It All Together

IN THIS CHAPTER

» Using add-ins: What a concept!

» Knowing why you might want to

create your own add-ins

» Creating custom add-ins

» Reviewing an add-in example

Chapter 21

Creating Excel Add-Ins

O ne of the slickest features of Excel is the capability to create add-ins.

Excel add-ins make it possible for you to package up your VBA proce-


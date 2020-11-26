NOTE

The Ch26_ExSamples.dvb sample file, which you can download from www.sybex.com/go/autocadcustomization, contains two procedures—named AssignSumInfo and QuerySumInfo—that demonstrate a more comprehensive solution for working with drawing properties. Place the file in the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store the DVB files. Then load the VBA project into the AutoCAD drawing environment to use it.

Manipulating a Drawing Window

In addition to getting information about a drawing file, you can query and manipulate the window in which a drawing file is displayed. The Active property and the Activate method are helpful when you are working with the AcadDocuments collection object. You can use the Active property to determine whether a document is the current object, and the Activate method lets you set a document as current.

Table 26.4 lists the AcadDocument object properties that can be used to resize and get information about a drawing window.

Table 26.4 Drawing window–related properties

Property Description

Height Specifies the height of the drawing window. The value is an integer and represents the window height in pixels.

Width Specifies the width of the drawing window. The value is an integer and represents the window width in pixels.

WindowState Returns an integer value that represents the current state of the drawing window. The integer values allowed are defined as part of the AcWindowState enumerator. A value of 1 (or acNorm) indicates the window is neither minimized nor maximized, whereas a value of 2 (or acMin) or 3 (or acMax) indicates the window is minimized or maximized, respectively.

WindowTitle Returns a string that contains the title of the drawing window. This property is read-only.

For more information on these properties and methods, use the Object Browser in the VBA Editor or check the AutoCAD Help system.

Working with System Variables

System variables are used to alter the way commands work, describe the current state of a drawing or AutoCAD environment, and specify where support files are stored. Many of the settings that are exposed by system variables are associated with controls in dialog boxes and palettes; other settings are associated with various command options. For example, many of the settings in the Drafting Settings dialog box (which you display using the dsettings command) are accessible from system variables.

A system variable can store any one of the basic data types that VBA supports (see「Exploring Data Types」in Chapter 25). You can see the hundreds of system variables and the type they hold by using the AutoCAD Help system. Whereas you might normally use the setvar command to list or change the value of a system variable at the AutoCAD Command prompt, with the AutoCAD Object library you use the GetVariable and SetVariable methods of an AcadDocument object to query and set the value of a system variable, respectively.

Here's the syntax of the SetVariable and GetVariable methods:

document.SetVariable sysvar_name, value retVal = document.GetVariable(sysvar_name)

The arguments are as follows:

sysvar_name The sysvar_name argument specifies the name of the system variable you want to query or set.

value The value argument specifies the data that you want to assign to the system variable.

retVal The retVal argument specifies the user-defined variable that you want to assign the current value of the system variable.

The next exercise demonstrates how to query and set the value of the osmode system variable, which controls the object snap drafting aid that is currently running. This setting is available in the Drafting Settings dialog box:

Create a new VBA project or use the empty VBA project that is available by default when the VBA Editor is started.

In the Project Explorer, double-click the ThisDrawing component.

In the code editor window, type the following:Sub WorkingWithSysVars() ' Get and store the current value of osmode Dim nCurOsmode As Integer nCurOsmode = ThisDrawing.GetVariable("osmode") MsgBox "Current value of osmode: " & CStr(nCurOsmode) ' Set osmode to a value of 33 ThisDrawing.SetVariable "osmode", 33 MsgBox "Current value of osmode: " & _ CStr(ThisDrawing.GetVariable("osmode")) ' Restore osmode to its previous value ThisDrawing.SetVariable "osmode", nCurOsmode MsgBox "Current value of osmode: " & _ CStr(ThisDrawing.GetVariable("osmode")) End Sub

Switch to the AutoCAD application window.

On the ribbon, click the Manage tab Applications panel Run VBA Macro.

When the Macros dialog box opens, select the macro name that ends with WorkingWithSysVars. Click Run.

Review the value in the message box and click OK to continue the execution of the procedure. The current value of the osmode system variable is displayed after the colon in the message box.

Review the message and click OK in the next two message boxes. The value of the osmode system variable is changed to 33, and the change is reflected after the colon in the message box. The final message box reflects the original value.

TIP

The AutoCAD Help system is a great resource for learning about system variables. However, if you need to support multiple AutoCAD releases, you will need to reference the documentation for each release. To make it easier to identify which system variables are supported in the current and previous AutoCAD releases, Shaan Hurley (http://autodesk.blogs.com/between_the_lines/) and I compiled a list of system variables that spans AutoCAD releases from 2004 through the present; you can view the list here: www.hyperpics.com/system_variables/.

Querying and Setting Application and Document Preferences

System variables provide access to many application and document settings, but there are some settings that are not accessible using system variables. The AcadApplication and AcadDocument objects both offer a property named Preferences that allows you to access additional settings that are not accessible using system variables. The Preferences property of the AcadApplication object contains a reference to an AcadPreferences object. The AcadPreferences object provides access to 10 properties that provide access to different preference objects that are used to organize the available preferences. The 10 preference objects represent many of the tabs in the Options dialog box (which you open using the option command).

Table 26.5 lists the preference objects that are used to organize application preferences.

Table 26.5 Preference objects accessible from the application

Class/Object Description

AcadPreferencesDisplay Provides access to settings that control the display and color of user-interface elements, scroll bars, drawing windows, and crosshairs.

AcadPreferencesDrafting Provides access to the AutoSnap and AutoTracking settings.

AcadPreferencesFiles Provides access to the support-file locations, such as Support File Search Path and Drawing Template File Location.

AcadPreferencesOpenSave Provides access to the default drawing format used when saving a drawing with the save and qsave commands, in addition to settings used to control the loading of Xrefs and ObjectARX applications.

AcadPreferencesOutput Provides access to settings that control the plotting and publishing of drawing files.

AcadPreferencesProfiles Provides access to methods used to manage profiles defined in the AutoCAD drawing environment, as well as a property used to get or switch the active profile.

AcadPreferencesSelection Provides access to settings that control the display of grips and the pickbox.

AcadPreferencesSystem Provides access to application settings that control the display of message boxes and whether the acad.lsp file is loaded once per AutoCAD session or into each drawing.

AcadPreferencesUser Provides access to settings that control the default insertion units used with the insert command and the behavior of the shortcut menus in the drawing area.

The Preferences property of the AcadDocument object doesn't provide access to a reference of an AcadPreferences object but instead provides access to an AcadDatabasePreferences object. The AcadDatabasePreferences object can be used to control the display of lineweights, object selection sorting, and the number of contour lines per surface, among many other settings.

The following examples show how to query and set application and drawing preferences:

' Sample used to control Application preferences With ThisDrawing.Application.Preferences ' Displays a message box with the current support file search paths MsgBox.Files.SupportPath ' Displays a message box with all available profiles Dim vName As Variant, vNames As Variant, strNames As String .Profiles.GetAllProfileNames vNames For Each vName In vNames strNames = strNames & vName & "," Next vName MsgBox "Available profile names: " & strNames ' Sets the crosshairs to 100 .Display.CursorSize = 100 ' Sets the background color of model space color to light gray .Display.GraphicsWinModelBackgrndColor = 12632256 End With ' Sample used to control Document preferences With ThisDrawing.Preferences ' Turns off solid fill mode .SolidFill = False ' Turns on quick text display mode .TextFrameDisplay = True End With

Executing Commands

The AutoCAD Object library allows you to automate most common tasks without the use of a command, but there might be times when you will need to use an AutoCAD or third-party command. A command can be executed using the SendCommand method of the AcadDocument object.

NOTE

While using a command might seem like a quick and easy choice over using the methods and properties of the objects in the AutoCAD Object library, you should avoid using commands whenever possible. The execution of an AutoCAD command can be slower and more limited than using the same approach with the AutoCAD Object library and VBA. The behavior of commands is affected by system variables, and ensuring system variables are set to specific values before calling a command can result in you having to write additional code statements that can complicate your programs.

The SendCommand method expects a single string that represents the command, options, and values that would be entered at the Command prompt. A space in the string represents the single press of the Enter key. When the Enter key must be pressed, such as when providing a string value that supports spaces, use the vbCr constant.

The following statements show how to draw a rectangle and a single-line text object using commands:

' Draws a rectangle 0,0 to 10,4 ThisDrawing.SendCommand "._rectang 0,0 10,4 " ' Draws a single line text object with middle center justification ' at 5,2 with a height of 2.5 units and the text string D101 ThisDrawing.SendCommand "._-text _j _mc 5,2 2.5 0 D101" & vbCr

Figure 26.1 shows the result of drawing a rectangle with the rectang command and single-line text placed inside the rectangle with the -text command.

Figure 26.1 Rectangle and text drawn using commands

The string sent by the SendCommand method to the AcadDocument object is executed immediately in most cases. Typically, the string isn't executed immediately when the SendCommand method is called from an event handler. I discuss event handlers in Chapter 33.

Starting with AutoCAD 2015, you can postpone the execution of the commands and options in the string until after the VBA program finishes by using the PostCommand method instead of the SendCommand method. Unlike with the SendCommand method, you don't need to have all commands, options, and values in a single string.

The following statements show how to draw a rectangle with the PostCommand method:

' Draws a rectangle 0,0 to 10,4 ThisDrawing.PostCommand "._rectang " ThisDrawing.PostCommand "0,0 10,4 "

Exercise: Setting Up a Project

Before a product is manufactured or a building is constructed, it starts as an idea that must be documented. In AutoCAD, documenting is known as drafting or modeling. Similar to a Microsoft Word document, a drawing must be set up to ensure that what you want to design appears and outputs as intended. Although you can create a number of drawing template (DWT) files to use when creating a new drawing, it can be better and more flexible to design an application that can adapt to your company's needs instead of creating many DWT files to try to cover every type of drawing your company might create.

In this section, you will create and set up a new drawing file using some of the concepts that have been introduced in this chapter. The key concepts that are covered in this exercise are as follows:

Managing Documents Create and save a new drawing file.

Assigning and Creating Drawing Properties Assign values to standard drawing properties and create custom drawing properties that can be used to populate text in a title block.

Setting System Variables and Preferences Changes can be made to system variables and preferences that are stored with the application or a drawing to affect the behavior of drafting aids and other AutoCAD features.

Performing Tasks with a Command AutoCAD commands can be used to create and modify graphical and nongraphical objects in a drawing.

Creating the DrawingSetup Project

A project is used to store any and all VBA code that is to be executed in the AutoCAD drawing environment. The following steps explain how to create a project named DrawingSetup and save it to a file named drawingsetup.dvb:

On the ribbon, click the Manage tab Applications panel title bar and then click VBA Manager (or at the Command prompt, type vbaman and press Enter).

When the VBA Manager opens, select the first project in the Projects list and click Unload. If prompted to save the changes, click Yes if you wish to save the changes, or click No to discard the changes.

Repeat step 2 for each VBA project in the list.

Click New. The new project is added to the list with a default name of ACADProject and a location of Global1, Global2, and so on based on how many projects have been created in the current AutoCAD session.

Select the new project from the Projects list and click Save As.

When the Save As dialog box opens, browse to the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store custom program files.

In the File Name text box, type drawingsetup and click Save.

In the VBA Manager dialog box, click Visual Basic Editor.

The next steps explain how to change the project name from ACADProject to DrawingSetup and add a new code module named basDrawingSetup:

When the VBA Editor opens, select the project node labeled ACADProject (shown in Figure 26.2) from the Project Explorer. If the Project Explorer isn't displayed, click View Project Explorer on the menu bar in the VBA Editor.

In the Properties window, select the field named (Name) and double-click in the text box adjacent to the field. If the Properties window isn't displayed, click View Properties Window on the menu bar in the VBA Editor.

In the text box, type DrawingSetup and press Enter.

On the menu bar, click Insert Module.

In the Project Explorer, select the new module named Module1.

In the Properties window, change the current value of the (Name) property to basDrawingSetup.

On the menu bar, click File Save.

Figure 26.2 Navigating the new project with the Project Explorer

Creating and Saving a New Drawing from Scratch

Designs created with the AutoCAD drawing environment are stored in a DWG file, which can then be shared with others in your organization or external vendors and clients. The New method of the AcadDocuments collection object gives you the most flexibility in creating a new drawing file.

In the following steps, you define a procedure named newDWGFromScratch, which will be used to create a drawing from scratch with imperial units and return the AcadDocument object that represents the new drawing. Once the drawing is created, the SaveAs method of the new AcadDocument object is used to save the drawing with the name of ACP-D1.B.dwg to the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store files from this book.

In the Project Explorer, double-click the code module named basDrawingSetup.

When the code editor opens, type the following:' Creates a new drawing from scratch ' Function accepts an optional value of: ' 0 - Creates an imperial units based drawing ' 1 - Creates a metric units based drawing Private Function newDWGFromScratch _ (Optional nMeasureInit As Integer = 0) As AcadDocument ' Get the current value of the MEASUREINIT system variable Dim curMInit As Integer curMInit = ThisDrawing.GetVariable("measureinit") ' Set the measurement system for new drawings to metric ThisDrawing.SetVariable "measureinit", nMeasureInit ' Create a new drawing from scratch Dim newDWGFromScratch As AcadDocument Set newDWGFromScratch = Application.Documents.Add ' Restore the previous value ThisDrawing.SetVariable "measureinit", curMInit End Function

On the menu bar, click File Save.

Since the procedure newDWGFromScratch is designated as private, it can't be executed from the AutoCAD user interface with the vbarun command. In the next steps, you will create a public procedure named Main that will be used to execute the various procedures that will make up the final functionality of the DrawingSetup project.

In the code editor, click after the End Function code statement of the newDWGFromScratch procedure and press Enter twice.

Type the following:Public Sub Main() ' Executes the newDWGFromScratch to create a new drawing from sratch Dim newDWG As AcadDocument Set newDWG = newDWGFromScratch ' Saves the new drawing ThisDrawing.SaveAs ThisDrawing.GetVariable("mydocumentsprefix") & _ "\MyCustomFiles\acp-d1_b.dwg" End Sub

On the menu bar, click File Save.

In the code editor, click after the code statement that starts with Public Sub Main.

On the menu bar, click Run Run Sub/UserForm. If the Macros dialog box opens, select Main and click Run. If you clicked inside the Main procedure definition, the Macro dialog box will not be displayed. The new drawing is created and saved to the file named acp-d1_b.dwg. If an error message is displayed, make sure that the MyCustomFiles folder exists under the Documents (or My Documents) folder, or update the code to reflect the folder you are using to store the files for this book.

On the Windows taskbar, click the AutoCAD application icon and verify that the new drawing was created.

Try executing the Main procedure again. This time an error message is displayed, as shown in Figure 26.3, which indicates that the drawing couldn't be saved. The drawing couldn't be saved because it was already open in AutoCAD and the file was locked on the local disc. I cover how to handle errors in Chapter 36.

In the Microsoft Visual Basic error message box, click End to terminate the execution of the code.

Figure 26.3 Error message generated as a result of AutoCAD not being able to save the drawing

Inserting a Title Block with the insert Command

The next steps insert a title block into the current drawing. The insert command is sent to the current drawing with the SendCommand method.

NOTE

From www.sybex.com/go/autocadcustomization you can download the drawing file b-tblk.dwg used by the insert command in the following steps. Place the file in the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store custom program files. If you are storing the files for this book in a different folder other than MyCustomFiles under the Documents (or My Documents) folder, update the code in the following steps as needed.

In the code editor, click after the End Sub code statement of the Main procedure and press Enter twice.

Type the following:Private Sub insertTitleBlock() With ThisDrawing ' Gets the current layer name Dim sLyrName As String sLyrName =.GetVariable("clayer") ' Creates a new layer named TBlk with the ACI value 8 .SendCommand "._-layer _m " & "TBlk" & vbCr & "_c 8 " & "TBlk" & vbCr & vbCr ' Inserts the title block drawing .SendCommand "._-insert " &.GetVariable("mydocumentsprefix") & _ "\MyCustomFiles\b-tblk" & vbCr & "0,0 1 1 0" & vbCr ' Zooms to the extents of the drawing .SendCommand "._zoom _e" & vbCr ' Restores the previous layer .SetVariable "clayer", sLyrName End With End Sub

Scroll up and add the statements shown in bold to the Main procedure:Public Sub Main() ' Executes the newDWGFromScratch to create a new drawing from scratch Dim newDWG As AcadDocument Set newDWG = newDWGFromScratch ' Saves the new drawing ThisDrawing.SaveAs ThisDrawing.GetVariable("mydocumentsprefix") & _ "\MyCustomFiles\acp-d1_b.dwg" ' Insert the title block insertTitleBlock End Sub

On the menu bar, click File Save.

Close all open drawing files and then create a new drawing file.

Execute the Main procedure with the vbarun command or by clicking Run Run Sub/UserForm from the VBA Editor menu bar. A new drawing should be created and the title block drawing b-tblk is inserted on the TBlk layer, as shown in Figure 26.4.

Switch to the AutoCAD application to view the new drawing and title block.

Figure 26.4 New drawing with a title block

Adding Drawing Properties

Drawing properties can be a great way to populate values of a title block using fields or even to help you locate a drawing file years later. (You will remember that drawing properties can be searched using the Search field in Windows Explorer and File Explorer, making it possible to find a drawing based on an assigned property value.) Drawing properties are stored with a DWG file and are accessible with the dwgprops command or the AcadSummaryInfo object of the AutoCAD Object library.

In the following steps, you will define a procedure named addDWGProps, which adds some static values to some of the standard drawing properties and creates a few custom drawing properties. A few of the values are used by the fields in the title block that was inserted with the insertTitleBlock procedure added in the previous section.

In the AutoCAD drawing window, zoom into the lower-right area of the title block. You should notice a few values with the text ----. This text is the default value of a field value that can't be resolved.

In the code editor, click after the End Sub code statement of the insertTitleBlock procedure and press Enter twice.

Type the following:Private Sub addDWGProps() With ThisDrawing.SummaryInfo ' Set the author and comment properties .Author = "[Replace this text with your initials here]" .Comments = "Phase 1: 1st Floor Furniture Plan" ' Add custom properties to a drawing Dim sProject As String Dim sPhase As String On Error Resume Next .GetCustomByKey "ProjectName", sProject If Err.Number <> 0 Then ' Property doesn't exist .AddCustomInfo "ProjectName", "ACP Renovation" Err.Clear Else ' Property exists, so update the value .SetCustomByKey "ProjectName", "ACP Renovation" End If End With ' Regen the drawing to update the fields ThisDrawing.Regen acActiveViewport End Sub

Scroll up and add the statements shown in bold to the Main procedure:Public Sub Main() ' Executes the newDWGFromScratch to create a new drawing from scratch Dim newDWG As AcadDocument Set newDWG = newDWGFromScratch ' Saves the new drawing ThisDrawing.SaveAs ThisDrawing.GetVariable("mydocumentsprefix") & _ "\MyCustomFiles\acp-d1_b.dwg" ' Insert the title block insertTitleBlock ' Add the drawing properties addDWGProps End Sub

On the menu bar, click File Save.

Close all open drawing files and then create a new drawing file.

Execute the Main procedure. The「project name」and「drafted by」values are populated in the title block by the property values assigned to the drawing. The property values of the drawing are assigned using the methods and properties of the AcadSummaryInfo object, as shown in Figure 26.5.

Figure 26.5 Field values populated by drawing properties

Setting the Values of Drafting-Related System Variables and Preferences

System variables and the preferences of the application or drawing can be used to affect many of the commands and drafting aids in the AutoCAD drawing environment.

In the following steps, you define a procedure named setDefDraftingAids, which specifies the values of system variables and application preferences.

In the code editor, click after the End Sub code statement of the addDWGProps procedure and press Enter twice.

Type the following:Private Sub setDefDraftingAids() ' Set the values of drafting-related system variables With ThisDrawing .SetVariable "orthomode", 1 .SetVariable "osmode", 35 .SetVariable "gridmode", 0 .SetVariable "snapmode", 0 .SetVariable "blipmode", 0 End With ' Set display-related preferences With ThisDrawing.Application.Preferences.Display .CursorSize = 100 End With ' Set drafting-related preferences With ThisDrawing.Application.Preferences.Drafting .AutoSnapAperture = True .AutoSnapApertureSize = 10 End With ' Set selection-related preferences With ThisDrawing.Application.Preferences.Selection .DisplayGrips = True .PickFirst = True End With End Sub

Scroll up and add the statements shown in bold to the Main procedure:Public Sub Main() ' Executes the newDWGFromScratch to create a new drawing from scratch Dim newDWG As AcadDocument Set newDWG = newDWGFromScratch ' Saves the new drawing ThisDrawing.SaveAs ThisDrawing.GetVariable("mydocumentsprefix") & _ "\MyCustomFiles\acp-d1_b.dwg" ' Insert the title block insertTitleBlock ' Add the drawing properties addDWGProps ' Sets the values of system variables and application preferences setDefDraftingAids ' Saves the changes to the drawing ThisDrawing.Save End Sub

On the menu bar, click File Save.

Close all open drawing files and then create a new drawing file.

Execute the Main procedure. The system variables and application preferences are changed, and the changes to the drawing file are saved.

Chapter 27

Creating and Modifying Drawing Objects

All drawings start off as an idea. Maybe it's just in your head, or maybe it became a sketch done on a napkin over lunch. The idea or sketch is then handed over to a drafter or engineer, who creates a set of drawings that will be used to communicate the final design. The final design is then used to manufacture the parts or construct the building. A drafter or engineer completes a design using a variety of objects, from lines to circles, and even splines and hatch patterns.

Although adding objects to a drawing is how most designs start off, those objects are often used to create new objects or are modified to refine a design. Most users of the AutoCAD® program, on average, spend more time modifying objects than creating new objects. When automating tasks with VBA, be sure to look at tasks related not only to creating objects but also to modifying objects.

In this chapter, you will learn to create 2D graphical objects and how to work with nongraphical objects, such as layers and linetypes. Along with creating objects, you will learn how to modify objects.

Due to limitations on the number of pages available for this book, additional content that covers working with 2D and 3D objects is presented in the bonus chapters available on the companion website. The companion website is located here: www.sybex.com/go/autocadcustomization.

Understanding the Basics of a Drawing-Based Object

Each drawing contains two different types of objects: nongraphical and graphical. Nongraphical objects represent the layers, block definitions, named styles, and other objects that are stored in a drawing but aren't present in model space or on a named layout. Nongraphical objects can, and typically do, affect the display of graphical objects.

Although model space and named layouts are typically not thought of as nongraphical objects, they are. Model space is a special block definition, whereas a layout is an object that is based on a plot configuration—commonly called a page setup—with a reference to a block definition. Graphical objects are those objects that are added to model space or a named layout, such as lines, circles, and text. Every graphical object added to a drawing references at least one nongraphical object and is owned by one nongraphical object. The nongraphical object that each graphical object references is a layer, and each graphical object is owned by model space or a named layout.

In the AutoCAD Object library, any object that can be added to a drawing is derived from or based on the AcadObject object type. For example, an AcadLine object that represents a line segment and an AcadLayer object that represents a layer have the same properties and methods as the AcadObject object type. You can think of the AcadObject as a more general or generic object in the terms of AutoCAD objects, much like you might use the term automobile to describe a vehicle with four wheels. Figure 27.1 shows the object hierarchy of nongraphical and graphical objects.

Figure 27.1 Drawing object hierarchy

Table 27.1 lists the properties of the AcadObject object that you use to get information about an object in a drawing.

Table 27.1 Properties related to the AcadObject object

Property Description

Application Returns the AcadApplication object that represents the current AutoCAD session. I discussed working with the AcadApplication object in Chapter 26,「Interacting with the Application and Documents Objects.」

Document Returns the AcadDocument object that represents the drawing in which the object is stored. I discussed working with the AcadDocument object in Chapter 26.

Handle Returns a string that represents a unique hexadecimal value that differentiates one object from another in a drawing; think of it along the lines of a database index. An object's handle persists between drawing sessions. A handle, while unique to a drawing, can be assigned to another object in a different drawing.

HasExtensionDictionary Returns True if an extension dictionary has been attached to the object. I discuss extension dictionaries in Chapter 32,「Storing and Retrieving Custom Data.」

ObjectID Returns a unique integer that differentiates one object from another in a drawing; think of it along the lines of a database index. Unlike a handle, the object ID of an object might be different each time a drawing is loaded into memory.

ObjectID32 Same as the ObjectID property, but must be used on 64-bit releases of Windows. This property is only valid with AutoCAD 2009 through 2014. Use the ObjectID property for earlier releases and AutoCAD 2015.

ObjectName Returns a string that represents the object's internal classname. This value can be used to distinguish one object type from another as part of a conditional statement.

OwnerID Returns the object ID of the object's parent. For example, the parent of a line might be model space or a named layout whereas the text style symbol table is the parent of a text style.

OwnerID32 Same as the OwnerID property, but must be used on 64-bit releases of Windows. This property is only valid with AutoCAD 2009 through 2014. Use the OwnerID property for earlier releases and AutoCAD 2015.

Determining a Drawing Object's Type

The ObjectName property and VBA TypeOf statement can be used to determine an object's type. The following code statements demonstrate how to display an object's name in a message box and use the TypeOf statement to determine whether an object is based on the AcadCircle class:

' Gets the first object in model space Dim oFirstEnt As AcadEntity Set oFirstEnt = ThisDrawing.ModelSpace(0) ' Display an object's name in a message box MsgBox "ObjectName: " & oFirstEnt.ObjectName ' Check to see if the object is a circle, and ' display a message based on the results If TypeOf oFirstEnt Is AcadCircle Then MsgBox "Object is a circle." Else MsgBox "The object isn't a circle." End If

In addition to the properties that are shared across all drawing-based objects, several methods are shared. The Delete method is used to remove an object from a drawing; it is the AutoCAD Object library equivalent of the erase command. The other three shared methods are used to work with extension dictionaries and extended data (Xdata). These three methods are GetExtensionDictionary, GetXData, and SetXData, and I cover them in Chapter 32.

All graphical objects in a drawing are represented by the AcadEntity object. The AcadEntity object inherits the properties and methods of the AcadObject object and adds additional properties and methods that all graphical objects have in common. For example, all graphical objects can be assigned a layer and moved in the drawing. The Layer property of the AcadEntity object is used to specify the layer in which an object is placed, and the Move method is used to relocate an object in the drawing. Objects based on the AcadEntity object can be added to model space, a named layout, or a block definition.

Table 27.2 lists the properties of the AcadEntity object that you can use to get information about and control the appearance of a graphical object in a drawing.

Table 27.2 Properties related to the AcadEntity object

Property Description

EntityTransparency Specifies the transparency for an object. See Bonus Chapter 1,「Working with 2D Objects and Object Properties.」

Hyperlinks Returns the AcadHyperlinks collection object assigned to an object. See Bonus Chapter 1.

Layer Specifies the layer for an object. See Bonus Chapter 1.

Linetype Specifies the linetype for an object. See Bonus Chapter 1.

LinetypeScale Specifies the linetype scale for an object. See Bonus Chapter 1.

Lineweight Specifies the lineweight for an object. See Bonus Chapter 1.

Material Specifies the name of the material to use when an object is rendered. See Bonus Chapter 2,「Modeling in 3D Space.」

PlotStyleName Specifies the name of the plot style for an object. See Bonus Chapter 1.

TrueColor Specifies the color assigned to an object. See Bonus Chapter 1.

Visible Specifies the visibility for an object. See Bonus Chapter 1.

Inheriting Default Property Values

When new objects are added to a drawing, they inherit many of their default property values from system variables; this occurs whether you are using an AutoCAD command or the AutoCAD Object library. For example, the clayer system variable holds the name of the layer that is assigned to the Layer property of each new graphical object. If your functions need to create multiple objects on a specific layer, it is best to set that layer current before adding new graphical objects and then restore the previous layer after the objects have been added.

The following lists other system variables that affect the default properties of new graphical objects:

cecolor: Color assigned to the TrueColor property celtype: Linetype assigned to the Linetype property celweight: Lineweight assigned to the Lineweight property celtscale: Linetype scale assigned to the LinetypeScale property cetransparency: Transparency assigned to the EntityTransparency property cmaterial: Material assigned to the Material property cplotstyle: Plot style name assigned to the PlotStyleName property

Table 27.3 lists the methods that all graphical objects inherit from the AcadEntity object.

Table 27.3 Methods related to the AcadEntity object

Method Description

ArrayPolar Creates a polar array from an object. See Bonus Chapter 1.

ArrayRectangular Creates a rectangular array from an object. See Bonus Chapter 1.

Copy Duplicates an object. See the「Copying and Moving Objects」section.

GetBoundingBox Returns an array of doubles that represents the lower and upper points of an object's extents. See Bonus Chapter 1.

Highlight Highlights or unhighlights an object. See Bonus Chapter 1.

IntersectWith Returns an array of doubles that represents the intersection points between two objects. See Bonus Chapter 1.

Mirror Mirrors an object along a vector. See Bonus Chapter 1.

Mirror3D Mirrors an object about a plane. See Bonus Chapter 2.

Move Moves an object. See the「Copying and Moving Objects」section.

Rotate Rotates an object around a base point. See the「Rotating Objects」section.

Rotate3D Rotates an object around a vector. See Bonus Chapter 2.

ScaleEntity Uniformly increases or decreases the size of an object. See Bonus Chapter 1.

TransformBy Applies a transformation matrix to an object. A transformation matrix can be used to scale, rotate, move, and mirror an object in a single operation. See Bonus Chapter 1.

Update Instructs AutoCAD to recalculate the display of an object; similar to the regen command but it only affects the object in which the method is executed. See the「Modifying Objects」section.

Accessing Objects in a Drawing

Before working with nongraphical and graphical objects, you must understand where objects are located in the AutoCAD Object hierarchy. Nongraphical objects are stored in collection objects that are accessed from an AcadDocument or ThisDrawing object. Even graphical objects displayed in model space, on named layouts, or in a block definition require you to work with a collection object. I explained how to work with the AcadDocument object in Chapter 26.

To access the collection objects of a drawing, use the properties of an AcadDocument object. Collection objects may also be referred to as symbol tables or dictionaries the AutoLISP and Managed.NET programming languages (Table 27.4).

NOTE

Not all named styles are accessible from a property of the AcadDocument object. For example, table and multileader styles are stored as dictionaries and accessed from the Dictionaries property.

Table 27.4 Properties used to access the collection objects of an AcadDocument object

Property Description

Blocks Returns an AcadBlocks collection object that contains the block definitions stored in a drawing, even model space, paper space, and those used for named layouts. See Chapter 30,「Working with Blocks and External References,」for more information.

Dictionaries Returns an AcadDictionaries collection object that contains the named dictionaries stored in a drawing. See Chapter 32 for more information.

DimStyles Returns an AcadDimStyles collection object that contains the dimension styles stored in a drawing. See Chapter 29,「Annotating Objects,」for more information.

FileDependencies Returns an Acad FileDependencies collection object that contains the external file dependencies used by a drawing. See Chapter 30 for more information.

Groups Returns an AcadGroups collection object that contains the named groups defined in a drawing. See Bonus Chapter 1.

Layers Returns an AcadLayers collection object that contains the layers stored in a drawing. See Bonus Chapter 1.

Layouts Returns an AcadLayouts collection object that contains the named layouts stored in a drawing. See Chapter 31,「Outputting Drawings,」for more information.

Linetypes Returns an AcadLinetypes collection object that contains the linetypes stored in a drawing. See Bonus Chapter 1.

Materials Returns an AcadMaterialss collection object that contains the names of the materials stored in a drawing. See Bonus Chapter 2.

ModelSpace Returns an AcadBlock object that is a reference to model space in the drawing. See the「Working with Model or Paper Space」section.

PaperSpace Returns an AcadBlock object that is a reference to paper space in the drawing. See the「Working with Model or Paper Space」section.

PlotConfigurations Returns an Acad PlotConfigurations collection object that contains the named plot configurations stored in a drawing. See Chapter 31 for more information.

RegisteredApplications Returns an AcadRegisteredApplications collection object that contains the names of all registered applications that store custom data in a drawing. See Chapter 32 for more information.

TextStyles Returns an AcadTextStyles collection object that contains the text styles stored in a drawing. See Chapter 29 for more information.

UserCoordinateSystems Returns an AcadUCSs collection object that contains the user coordinate systems saved in a drawing. See Bonus Chapter 2.

Viewports Returns an AcadViewports collection object that contains the named arrangements of tiled viewports for use in model space. See Chapter 28,「Interacting with the User and Controlling the Current View,」for more information.

Working with Model or Paper Space

Graphical objects created by the end user or with the AutoCAD Object library are all added to a block definition. Although this might seem a bit confusing at first, model space is nothing more than a block definition that is edited using the drawing area displayed in the drawing window. The same is true with paper space and the named layouts stored in a drawing. Before you can add or modify an object in a drawing file, you must determine which block definition to work with.

Model space and paper space are accessed using the ModelSpace and PaperSpace properties of an AcadDocument or ThisDrawing object. You use the ModelSpace property to get a reference to an AcadModelSpace object, which is actually a reference to the block definition named *MODEL_SPACE. The PaperSpace property returns a reference to an AcadPaperSpace object, which is a reference to the most recently accessed paper space block. The initial paper space block is named *PAPER_SPACE or *PAPER_SPACE0. Switching named layouts changes which paper space block is returned by the PaperSpace property.

You use the AcadModelSpace and AcadPaperSpace objects to access the graphical objects in a drawing. A majority of the methods that these two objects support are related to adding new graphical objects. To add new graphical objects to a drawing, use the methods whose names start with the prefix Add. I explain how to add graphical objects to model space in the next section and I cover how to access the objects already in model space in the「Getting an Object in the Drawing」section. You can learn more about the properties and methods specific to block definitions in Chapter 30 and the properties and methods specific to named layouts in Chapter 31.

The standard commands of AutoCAD typically work in the current context of the drawing. If model space is active and the line command is started, the line object is added to model space. However, if the line command is started when a named layout is current, the line is added to the named layout. The AutoCAD Object library isn't concerned with the active space. Model space might be active, but objects can be added to paper space and vice versa. The active space can be bypassed with the AutoCAD Object library and VBA because you have direct access to the objects in a drawing's database.

The active space doesn't matter so much when adding and modifying objects with the AutoCAD Object library, but users still expect macros to be executed in the current context of the drawing. The ActiveSpace property can be used to determine which space is active. A constant value of acModelSpace or acPaperSpace is returned by the ActiveSpace property; acModelSpace is returned when model space is current. You can also use the ActiveSpace property to switch the active space; assign the constant value of acPaperSpace to switch to paper space when model space is current.

The following code statements display a message containing the number of objects in the current space:

Dim nCnt As Integer nCnt = 0 Select Case ThisDrawing.ActiveSpace Case acModelSpace nCnt = ThisDrawing.ModelSpace.Count Case acPaperSpace nCnt = ThisDrawing.PaperSpace.Count End Select MsgBox "Number of objects in current space: " & CStr(nCnt)

TIP

As an alternative to specifying model space or paper space, you can use the ActiveLayout property of an AcadDocument or ThisDrawing object. The ActiveLayout property can be helpful when you want to draw objects on the current layout. Using the Block property of the AcadLayout object that is returned by the ActiveLayout property, you can get a reference to model space or paper space. When the Model layout is current, ActiveLayout.Block returns a reference to the AcadModelSpace object. I discuss more about layouts in Chapter 31.

Creating Graphical Objects

Graphical objects are used to communicate a design, whether a mechanical fastener or a new football stadium. AutoCAD supports two types of graphical objects: straight and curved. Straight objects, such as lines, rays, and xlines, contain only straight segments. Curved objects can have curved segments, but as an option can have straight segments, too. Arcs, circles, splines, and polylines with arcs are considered examples of curved objects. I cover commonly used straight and curved objects in the「Adding Straight Line Segments」and「Working with Curved Objects」sections. Polylines are discussed in the「Working with Polylines」section.

NOTE

As a reminder, graphical objects inherit many of their properties and methods from the AcadEntity object. For that reason, I only focus on the properties and methods specific to an object as they are introduced going forward. I covered the AcadEntity object in the「Understanding the Basics of a Drawing-Based Object」section earlier in this chapter.

Adding Straight Line Segments

Straight objects are used in a variety of drawings created by drafters and engineers. You can use a straight object to represent the following:

The top of a bolt head

The tooth of a gear

A wire in a wiring diagram

The edge of a student desk

The face of a wall for a building

Lines are straight objects with a defined start point and endpoint and are represented by the AcadLine object. The AddLine function allows you to create a line object drawn between two points. The following shows the syntax of the AddLine function:

retVal = object.AddLine(startPoint, endPoint)

Its arguments are as follows:

retVal The retVal argument represents the new AcadLine object returned by the AddLine function.

object The object argument represents the AcadModelSpace collection object.

startPoint The startPoint argument is an array of three doubles that defines the start point of the new line.

endPoint The endPoint argument is an array of three doubles that defines the endpoint of the new line.

The following code statements add a new line object to model space (see Figure 27.2):

' Defines the start and endpoint for the line Dim dStartPt(2) As Double, dEndPt(2) As Double dStartPt(0) = 0: dStartPt(1) = 0: dStartPt(2) = 0 dEndPt(0) = 5: dEndPt(1) = 5: dEndPt(2) = 0 Dim oLine As AcadLine Set oLine = ThisDrawing.ModelSpace.AddLine(dStartPt, dEndPt)

Figure 27.2 Definition of a line

Using the AcadLine object returned by the AddLine function, you can obtain information about and modify the line's properties. In addition to the properties that the AcadLine object shares in common with the AcadEntity object, you can use the properties listed in Table 27.5 when working with an AcadLine object.

Table 27.5 Properties related to an AcadLine object

Property Description

Angle Returns a double that represents the angle of the line expressed in radians. All angles are stored in a drawing file as radians.

Delta Returns an array of three double values that represent the delta of the line: the difference between the line's start and endpoints.

EndPoint Specifies the endpoint of the line.

Length Returns a double that represents the length of the line.

Normal Specifies the normal vector of the line. The normal vector is an array of three double values, which defines the positive Z-axis of the line.

StartPoint Specifies the start point of the line.

Thickness Specifies the thickness assigned to the line; the value must be numeric. The default is 0; anything greater than 0 results in the creation of a 3D planar object.

Working with Curved Objects

Straight objects are used in many designs, but they aren't the only objects. Curved objects are used to soften the edges of a design and give a design a more organic look. You can use a curved object to represent any of the following:

A hole in a plate

A fillet on a metal bracket

A round edge on the top of a desk

A cross section of a shaft or hub

I discuss how to create and modify circles in the upcoming sections.

NOTE

Ellipse and spline objects are covered in Bonus Chapter 1.

Creating and Modifying Circles

Circles are one of the most commonly used curved objects in mechanical designs, but they are less frequently used in architectural and civil designs. Drill holes in the top view of a model, the center of a gear, or the grommet in the side of a desk are typically circular and are drawn using circles. Circles in a drawing are represented by the AcadCircle object in the AutoCAD Object library. The AddCircle function allows you to create a circle object based on a center point and radius value, and the function returns an AcadCircle object that represents the new circle. The following shows the syntax of the AddCircle function:

retVal = object.AddCircle(centerPoint, radius)

Its arguments are as follows:

retVal The retVal argument represents the new AcadCircle object returned by the AddCircle function.

object The object argument represents the AcadModelSpace collection object.

centerPoint The centerPoint argument is an array of three doubles that defines the center point of the new circle.

radius The radius argument is a double that specifies the radius of the new circle. If you know the diameter of the circle you want to create, divide that value in half to get the radius for the circle.

The following code statements add a new circle object to model space (see Figure 27.3):

' Defines the center point for the circle object Dim dCenPt(2) As Double dCenPt(0) = 2.5: dCenPt(1) = 1: dCenPt(2) = 0 ' Adds the circle object to model space with a radius of 4 Dim oCirc As AcadCircle Set oCirc = ThisDrawing.ModelSpace.AddCircle(dCenPt, 4)

Figure 27.3 Definition of a circle

The properties and methods of the AcadCircle object returned by the AddCircle function can be used to obtain information about and modify the circle. An AcadCircle object shares properties and methods in common with the AcadEntity object, but it has additional properties that describe the circle object. Table 27.6 lists the properties specific to the AcadCircle object.

Table 27.6 Properties related to an AcadCircle object

Property Description

Area Returns a double that represents the calculated area of the circle.

Center Specifies the center point of the circle. That value is expressed as an array of three doubles.

Circumference Returns a double that represents the circumference of the circle.

Diameter Specifies the diameter of the circle; the value is a double.

Normal Specifies the normal vector of the line. The normal vector is an array of three doubles that defines the positive Z-axis for the circle.

Radius Specifies the radius of the circle; the value is a double.

Thickness Specifies the thickness assigned to the circle; the value must be numeric. The default is 0; anything greater than 0 results in the creation of a 3D cylinder object.

Adding and Modifying Arcs

Fillets and rounded corners are common in many types of designs, and they are drawn using arcs. Arcs are partial circles represented by the AcadArc object. An arc is added to a drawing with the AddArc function. Unlike drawing arcs with the arc command, which offers nine options, the AddArc function offers only one approach to adding an arc, and that is based on a center point, two angles (start and end), and a radius. The AddArc function returns an AcadArc object that represents the new arc added to the drawing. The following shows the syntax of the AddArc function:

retVal = object.AddArc(centerPoint, radius, startAngle, endAngle)

Its arguments are as follows:

retVal The retVal argument represents the new AcadArc object returned by the AddArc function.

object The object argument represents the AcadModelSpace collection object.

centerPoint The centerPoint argument is an array of three doubles that defines the center point of the new arc.

radius The radius argument is a double that specifies the radius of the new arc.

startAngle and endAngle The startAngle and endAngle arguments are doubles that specify the starting and end angle of the new arc, respectively. A start angle larger than the end angle results in the arc being drawn in a counterclockwise direction. Angles are measured in radians.

The following code statements add a new arc object to model space (see Figure 27.4):

' Defines the center point for the arc object Dim dCenPt(2) As Double dCenPt(0) = 2.5: dCenPt(1) = 1: dCenPt(2) = 0 ' Sets the value of PI Dim PI As Double PI = 3.14159265 ' Adds the arc object to model space with a radius of 4 Dim oArc As AcadArc Set oArc = ThisDrawing.ModelSpace.AddArc(dCenPt, 4, PI, 0)

Figure 27.4 Definition of an arc

The AcadArc object returned by the AddArc function can be used to obtain information about and modify the object's properties and methods. In addition to the properties that the AcadArc object shares in common with the AcadEntity object, you can use the properties listed in Table 27.7 when working with an AcadArc object.

Table 27.7 Properties related to an AcadArc object

Property Description

ArcLength Returns a double that represents the length along the arc.

Area Returns a double that represents the calculated area of the arc.

Center Specifies the center point of the arc. The value is expressed as an array of three doubles.

EndAngle Specifies a double that represents the end angle of the arc.

EndPoint Returns an array of doubles that represents the endpoint of the arc.

Normal Specifies the normal vector of the line. The normal vector is an array of three doubles that defines the positive Z-axis for the arc.

Radius Specifies the radius of the arc; the value is a double.

StartAngle Specifies a double that represents the start angle of the arc.

StartPoint Returns an array of doubles that represents the start point of the arc.

Thickness Specifies the thickness assigned to the circle; the value must be numeric. The default is 0; anything greater than 0 results in the creation of a curved 3D object.

TotalAngle Returns a double that represents the angle of the arc: the end angle minus the start angle.

Working with Polylines

Polylines are objects that can be made up of multiple straight and/or curved segments. Although lines and arcs drawn end to end can look like a polyline, polylines are more efficient to work with. Because a polyline is a single object made up of multiple segments, it is easier to modify. For example, all segments of a polyline are offset together instead of individually. If you were to offset lines and arcs that were drawn end to end, the resulting objects wouldn't be drawn end to end like the original objects (see Figure 27.5).

Figure 27.5 Offset polylines and lines

There are two types of polylines that you can create and modify:

Polyline Legacy polylines were available in AutoCAD R13 and earlier releases, and they are still available in AutoCAD R14 and later releases. This type of polyline object supports 3D coordinate values, but it uses more memory and increase the size of a drawing file.

Lightweight Polyline Lightweight polylines, or LWPolylines, were first introduced in AutoCAD R14. They are more efficient in memory and require less space in a drawing file. Lightweight polylines support only 2D coordinate values.

NOTE

Autodesk recommends using lightweight polylines in a drawing instead of legacy polylines when possible.

Legacy polylines are represented by the AcadPolyline object type and can be added to a drawing with the AddPolyline function. LWPolylines are represented by the AcadLWPolyline object type and can be added to a drawing with the AddLightWeightPolyline function. The AddPolyline and AddLightWeightPolyline functions both require you to specify a list of vertices.

A vertices list is defined using an array of doubles. The number of elements in the array varies by the type of polyline you want to create or modify. To create an AcadPolyline object, you define an array of doubles in multiples of three, whereas an array of doubles must be in multiples of two to create an AcadLWPolyline object. For example, an AcadPolyline object with three vertices would require an array with nine elements (three elements × three vertices). For an LWPolyline, each vertex requires two elements in an array, so an AcadLWPolyline object with three vertices would require a vertices list with six elements (two elements × three vertices).

The following shows an example of a six-element array that defines three 2D points representing the corners of a triangle:

' Defines a six element array of doubles Dim dVecList(5) As Double ' Sets the first corner dVecList(0) = 0#: dVecList(1) = 0# ' Sets the second corner dVecList(2) = 3#: dVecList(3) = 0# ' Sets the third corner dVecList(4) = 1.5: dVecList(5) = 2.5981

The following shows the syntax of the AddLightWeightPolyline and AddPolyline functions:

retVal = object.AddLightWeightPolyline(vecList) retVal = object.AddPolyline(vecList)

The arguments are as follows:

retVal The retVal argument represents the new AcadLWPolyline or AcadPolyline object returned by the AddLightWeightPolyline or AddPolyline function.

object The object argument represents the AcadModelSpace collection object.

vecList The vecList argument is an array of doubles that defines the vectors of the polyline. For the AddLightWeightPolyline function, the array must contain an even number of elements since each vertex is defined by two elements. Specify an array in three-element increments when using the AddPolyline function since each vertex is defined by three elements.

The following code statements add a new lightweight polyline object to model space (see Figure 27.6):

' Adds a lightweight polyline Dim oLWPoly As AcadLWPolyline Set oLWPoly = ThisDrawing.ModelSpace.AddLightWeightPolyline(dVecList)

Figure 27.6 Polyline with three vertices

Using the AcadLWPolyline or AcadPolyline object returned by the AddLightWeightPolyline or AddPolyline function, you can obtain information about and modify the polyline's properties. In addition to the properties that the AcadLWPolyline or AcadPolyline object share in common with the AcadEntity object, you can use the properties listed in Table 27.8 when working with an AcadLWPolyline or AcadPolyline object.

Table 27.8 Properties related to an AcadLWPolyline or AcadPolyline object

Property Description

Area Returns a double that represents the calculated area of the polyline.

Closed Specifies whether the polyline is open or closed. A value of True closes the polyline if the object contains more than two vertices.

ConstantWidth Specifies the global width for all segments of the polyline.

Coordinate Specifies the coordinate value of a specific vertex in the polyline.

Coordinates Specifies the coordinate values for all vertices of the polyline.

Elevation Specifies the elevation at which the polyline is drawn.

Length Returns a double that represents the length of the polyline.

LinetypeGeneration Specifies whether the linetype pattern assigned to the polyline is generated across the polyline as one continuous pattern, or whether the pattern begins and ends at each vertex. A value of True indicates that the linetype pattern should be generated across the polyline as one continuous pattern.

Normal Specifies the normal vector of the polyline. The normal vector is an array of three doubles that defines the positive Z-axis for the polyline.

Thickness Specifies the thickness assigned to the polyline; the value must be numeric. The default is 0; anything greater than 0 results in the creation of a 3D planar object.

In addition to the properties listed in Table 27.8, an AcadLWPolyline or AcadPolyline object contains methods that are specific to polylines. Table 27.9 lists the methods that are unique to polylines.

TIP

You use the AddVertex or AppendVertex method to add a new vertex to a polyline, but it isn't exactly obvious how you might remove a vertex. To remove a vertex from a polyline, use the Coordinates property to get the vertices of the polyline. Then create a new vertices list of the points you want to keep and assign the new vertices list to the Coordinates property.

Table 27.9 Methods related to an AcadLWPolyline or AcadPolyline object

Method Description

AddVertex Adds a new 2D point at the specified vertex in the LWPolyline (supported by AcadLWPolyline objects only).

AppendVertex Appends a new 3D point to the polyline (supported by AcadPolyline objects only).

Explode Explodes the polyline and returns an array of the objects added to the drawing as a result of exploding the polyline.

GetBulge Gets the bulge–curve–value at the specified vertex. The bulge is a value of the double data type.

GetWidth Gets the width of the segment at the specified vertex. The width is a value of the double data type.

SetBulge Sets the bulge–curve–value at the specified vertex.

SetWidth Sets the width of the segment at the specified vertex.

Defining Parallel Line Segments

Polylines make it easy to create parallel straight and curved segments. Parallel line segments can also be created with an AcadMLine object. Multilines (or mlines) allow you to create multiple parallel line segments and each parallel line can have a different format. The formatting of an mline is inherited from an mline style. You can use mlines to draw the walls of a building and even the foundation in plan view where the outermost lines might represent the footing and the inner lines represent the actual foundation walls. Although mlines have their use, they aren't common in drawings because they can be hard to edit. Mlines are added to a drawing with the AddMLine function. You can learn more about the AddMLine function and AcadMLine object in the AutoCAD Help system.

Getting an Object in the Drawing

Modifying an object after it has been added to a drawing is fairly straightforward; you use the properties and methods of the object that is returned by one of the Add* functions described in the previous sections. If you want to modify an existing object in a drawing, you must locate it in the AcadModelSpace or AcadPaperSpace collection object or a block definition represented by an AcadBlock object. I explain how to work with block definitions in Chapter 30 and with paper space in Chapter 31.

The Item method and a For statement are the most common ways to access an object in the AcadModelSpace collection object. I explained how to use the Item method and For statement in Chapter 25,「Understanding Visual Basic for Applications.」Use the Item method when you want to access a specific object in model space based on its index value; the first object in model space has an index of 0. Here are example code statements that get the handle and object type name of the first object in model space:

Dim oEnt As AcadEntity Set oEnt = ThisDrawing.ModelSpace(0) MsgBox "Handle: " & oEnt.Handle & vbLf & _ "ObjectID: " & CStr(oEnt.ObjectID) & vbLf & _ "Object Name: " & oEnt.ObjectName

The values displayed in the message box by the example code will vary from drawing to drawing. Figure 27.7 shows an example of a message box with the values from a first object in model space; the values reflected are of a point object.

Figure 27.7 Message box containing the handle and object ID of an object

A For statement is the most efficient way to step through all the objects in model space or any other collection object you might need to work with. The following code statements step through model space and return the center point and radius of each circle object:

Dim oEnt As AcadEntity Dim oCircle As AcadCircle ' Displays a general message ThisDrawing.Utility.Prompt vbLf & "Circles in model space" ' Steps through model space For Each oEnt In ThisDrawing.ModelSpace ' Checks to see if the object is a circle If TypeOf oEnt Is AcadCircle Then Set oCircle = oEnt ' outputs the center point and radius of the circle ThisDrawing.Utility.Prompt vbLf & "Center point: " & _ CStr(oCircle.Center(0)) & "," & _ CStr(oCircle.Center(1)) & "," & _ CStr(oCircle.Center(2)) & _ vbLf & "Radius: " & _ CStr(oCircle.Radius) End If Next oEnt ThisDrawing.Utility.Prompt vbLf

Here is an example of the output created by the previous code statements:

Circles in model space Center point: 5,2,0 Radius: 2.5 Center point: 6,2.5,0 Radius: 0.125 Center point: 3,1,0 Radius: 5

NOTE

The Item method and For statement are useful when stepping through all objects in model space or paper space, but they don't allow the user to interactively select an object. I discuss how to prompt a user for objects in Chapter 28.

Modifying Objects

Adding new objects is critical to completing a design, but more time is often spent by a drafter or engineer modifying existing objects than adding new objects. The AutoCAD Object library contains methods that are similar to many of the standard AutoCAD commands used to modify objects. The modifying methods of the AutoCAD Object library can be used to erase, move, scale, mirror, and rotate objects, among other tasks. I explain how to erase, copy, move, and rotate graphical objects in the following sections using the methods that are inherited by the AcadEntity object. I discuss how to scale, mirror, offset, array, and control the visibility of objects in Bonus Chapter 1 on the companion website at .www.sybex.com/go/autocadcustomization.

When a change is made to an object, I recommend that you update the display of that object. The AutoCAD command regen is used to regenerate the display of all objects in the current space, but with the AutoCAD Object library you can update the display of a single graphical object or all objects in a drawing. Use the Update method to update the display of a single graphical object. The Update method doesn't accept any argument values.

If you want to update the display of all objects in a drawing, use the Regen method of the AcadDocument or ThisDrawing object. The Regen method expects a constant value from the AcRegenType enumerator. You use the acActiveViewport constant to regenerate the objects in the current viewport or the acAllViewports constant to regenerate all objects in a drawing.

The following code statements show how to update the display of the first object in model space and all objects in the current viewport:

' Update the first object in model space ThisDrawing.ModelSpace(0).Update ' Update all objects in the current viewport Thisdrawing.Regen acActiveViewport

Deleting Objects

All graphical and most nongraphical objects can be removed from a drawing when they are no longer needed. The only objects that can't be removed are any nongraphical objects that are referenced by a graphical object, such as a text or dimension style, and nongraphical objects that represent symbol tables, such as the Layers and Blocks symbol tables. The Delete method is used to remove—or erase—an object. The method doesn't accept any arguments. If an object can't be removed, an error is generated. I explain how to trap and handle errors in Chapter 36,「Handling Errors and Deploying VBA Projects.」

The following code statement removes the first object in model space:

' Removes the first object in model space ThisDrawing.ModelSpace(0).Delete

Removing All Unreferenced Nongraphical Objects

Although the Delete method can be used to remove a nongraphical object that isn't currently being referenced by a graphical object in a drawing, the PurgeAll method can be used to purge all unreferenced nongraphical objects. The PurgeAll method is a member of the AcadDocument or ThisDrawing object, and it doesn't accept any argument values.

Here's an example of the PurgeAll method:

ThisDrawing.PurgeAll

Copying and Moving Objects

The copy and move commands are used to duplicate and relocate objects in a drawing. When working with the AutoCAD Object library, use the Copy function to duplicate an object. The Copy function doesn't accept any arguments, but it does return a reference to the new duplicate object. The Move method can be used to relocate an object. It expects two arrays of three doubles that define the base and destination points to control the distance and angle at which the object should be moved.

The following code statements draw a circle, duplicate the circle, and then move the duplicated circle 5 units along the X-axis in the positive direction:

' Defines the center point for the circle Dim dCenPt(2) As Double dCenPt(0) = 5: dCenPt(1) = 5: dCenPt(2) = 0 ' Adds a new circle to model space Dim oCirc As AcadCircle Set oCirc = ThisDrawing.ModelSpace.AddCircle(dCenPt, 2) ' Creates a copy of the circle Dim oCircCopy As AcadCircle Set oCircCopy = oCirc.Copy ' Moves the circle 5 units along the X axis Dim dToPt(2) As Double dToPt(0) = oCircCopy.Center(0) + 5 dToPt(1) = oCircCopy.Center(1) dToPt(2) = oCircCopy.Center(2) oCircCopy.Move dCenPt, dToPt

Rotating Objects

The angle and orientation of an object can be changed by rotating the object around a base point or axis. Rotating an object around a base point is performed with the Rotate method, whereas rotating an object around an axis is performed with the Rotate3D method. I discuss the Rotate3D method in Bonus Chapter 2 on the companion website. The base point you pass to the Rotate method must be defined as an array of three doubles. The angle in which the object is rotated must be expressed in radians.

The following code statements draw a line from 5,5 to 7,9 and then create a copy of the line. The new line object that is copied is then rotated 90 degrees to a value of 1.570796325 radians (see Figure 27.8):

' Defines the start and endpoints of the line Dim dStartPt(2) As Double, dEndPt(2) As Double dStartPt(0) = 5: dStartPt(1) = 5: dStartPt(2) = 0 dEndPt(0) = 7: dEndPt(1) = 9: dEndPt(2) = 0 ' Adds a new line to model space Dim oLine As AcadLine Set oLine = ThisDrawing.ModelSpace.AddLine(dStartPt, dEndPt) ' Copies the line Dim oLineCopy As AcadLine Set oLineCopy = oLine.Copy ' Rotates the copied line by 1.570796325 radians oLineCopy.Rotate dStartPt, 1.570796325

Figure 27.8 Rotated line object around a base point

The angular measurement of radians isn't as frequently used as degrees, but all angular values in a drawing are stored as radians; this is why the Rotate method expects radians. Radians are also expected or returned by most methods or properties in the AutoCAD Object library. Listing 27.1 shows two custom functions that can be used to convert degrees to radians and radians to degrees.

Listing 27.1: Converting angular measurements

Const PI As Double = 3.14159265 Private Function Degrees2Radians(dDegrees As Double) Degrees2Radians = dDegrees * PI / 180 End Function Private Function Radians2Degrees(dRadians As Double) Radians2Degrees = dRadians * 180 / PI End Function

Here are a few examples of using the custom functions in Listing 27.1:

Dim dAngle As Double ' Converts 1.570796325 radians to 90 degrees dAngle = Radians2Degrees(PI / 2) ' Converts 180 degrees to 3.14159265 radians dAngle = Degrees2Radians(180)

Changing Object Properties

All graphical objects are derived from the AcadEntity object—that is, all graphical objects inherit the properties and methods of the AcadEntity object. For example, even though the AcadLine object represents a single line segment and the AcadCircle object represents a circle, they share the properties named Layer and Linetype, among many others.

The properties that all graphical objects have in common are known as the general properties of an object. In the AutoCAD user interface, an object's general properties can be modified from the Properties panel on the ribbon or the Properties palette (displayed with the properties command). The general properties shared by all graphical objects were listed in Table 27.2.

The following code statements assign the layer named TitleBlk to the first object in model space and override the color of the layer by directly assigning the color 3 (green) to the object:

' Assigns the TitleBlk layer to the first object in model space ThisDrawing.ModelSpace(0).Layer = "TitleBlk" ' Assigns the ACI color Green to the first object in model space Dim oClr As AcadAcCmColor Set oClr = ThisDrawing.ModelSpace(0).TrueColor oClr.ColorMethod = acColorMethodByACI oClr.ColorIndex = acGreen ThisDrawing.ModelSpace(0).TrueColor = oClr

I explain how to work with and manage layers and linetypes in Bonus Chapter 1 on the companion website. In addition to working with layers and linetypes, I explain how to work with true and color book colors, along with assigning a plot style and transparency to a layer or object.

Exercise: Creating, Querying, and Modifying Objects

In this section, you will create two new projects that create, query, and modify objects. One project will define a macro that allows you to draw a mounting plate with 2D objects, and the second project will use a similar set of logic to create a 3D model of a mounting plate. Along with the two projects, you will create a utility class that contains common functions that can be used across both projects and even in other projects later in this book.

The key concepts I cover in this exercise are as follows:

Creating and Modifying Graphical Objects Graphical objects are the backbone of any design; they are used to communicate what the building or product should look like when built or manufactured. When you want to add or modify graphical objects, you must decide whether to work with model space or paper space, or even a custom block definition.

Working with Layers All graphical objects are placed on a layer. Layers are used to organize graphical objects and control many of the general properties that all graphical objects have in common.

Creating and Using a Custom Class The VBA programming language supports the ability to create a custom class. Custom classes can be used to organize functions and manage global variables. A custom class when created in a project can be exported and used across many projects.

NOTE

The steps in this exercise don't rely on the completion of an earlier exercise in this book. Later exercises in this book will rely on the completion of this exercise, though. If you don't complete this exercise, you can obtain the completed files from www.sybex.com/go/autocadcustomization.

Creating the DrawPlate Project

The following steps explain how to create a project named DrawPlate and to save it to a file named drawplate.dvb:

On the ribbon, click Manage tab Applications panel title bar and then click VBA Manager (or at the Command prompt, type vbaman and press Enter).

When the VBA Manager opens, click New. The new project is added to the list with a default name of ACADProject and a location of Global1, Global2, and so on based on how many projects have been created in the current AutoCAD session.

Select the new project from the Projects list and click Save As.

When the Save As dialog box opens, browse to the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store custom program files.

In the File Name text box, type drawplate and click Save.

In the VBA Manager dialog box, click Visual Basic Editor.

The next steps explain how to change the project name from ACADProject to DrawPlate:

When the VBA Editor opens, select the project node labeled ACADProject from the Project Explorer.

In the Properties window, select the field named (Name) and double-click in the text box adjacent to the field.

In the text box, type DrawPlate and press Enter.

On the menu bar, click File Save.

Creating the Utilities Class

Separating the custom functions you create into logical groupings can make debugging code statements easier and allow you to reuse code in other products. Custom classes are one way of sharing functions and protecting global variables from the functions of your main project. One of the benefits of using a custom class over just a code module is that you gain the advantage of type-ahead in the Visual Basic Editor, which reduces the amount of text you need to type.

In these steps, you add a new custom class module named clsUtilities to the DrawPlate project:

On the menu bar, click Insert Class Module.

In the Project Explorer, select the new module named Class1.

In the Properties window, change the current value of the (Name) property to clsUtilities.

On the menu bar, click File Save.

The clsUtilities class module will contain functions that define common and reusable functions for use with the main function of the DrawPlate project along with other projects later in this book. The following steps add two functions to the clsUtilities class that are used to work with system variables.

Working with one system variable at a time isn't always efficient when you need to set or restore the values of multiple system variables. You will define two functions named GetSysvars and SetSysvars. The GetSysvars function will return an array of the current values for multiple system variables, and the SetSysvars function will be used to set the values of multiple system variables.

The following steps explain how to add the GetSysvars and SetSysvars functions:

In the Project Explorer, double-click the clsUtilities component.

In the text editor area of the clsUtilities component, type the following. (The comments are here for your information and don't need to be typed.)' GetSysvars function returns an array of the current values ' for each system variable in the array it is passed. Public Function GetSysvars(sysvarNames) As Variant Dim nIdxTotal As Integer nIdxTotal = UBound(sysvarNames) Dim aVals() As Variant ReDim aVals(UBound(sysvarNames) - LBound(sysvarNames)) Dim nCnt As Integer For nCnt = LBound(sysvarNames) To UBound(sysvarNames) aVals(nCnt) = ThisDrawing.GetVariable(sysvarNames(nCnt)) Next GetSysvars = aVals End Function ' SetSysvars function sets the values of the system variables ' in the array that the function is passed. ' Function expects two arrays. Public Sub SetSysvars(sysvarNames, sysvarValues) Dim nCnt As Integer For nCnt = LBound(sysvarNames) To UBound(sysvarNames) ThisDrawing.SetVariable sysvarNames(nCnt), sysvarValues(nCnt) Next End Sub

Click File Save.

New graphical objects must be added to model space, paper space, or a block definition. In most situations, you want to add new objects to the current layout. You can create custom functions to combine multiple code statements and reduce the amount of code that needs to be otherwise entered. The following steps add three functions to the clsUtilities class that can be used to create a closed polyline and circle in the current layout, and a new layer.

In the text editor area of the clsUtilities component, type the following. (The comments are here for your information and don't need to be typed.)' CreateRectangle function draws a closed LWPolyline object. ' Function expects an array that represents four points, ' but can accept more points. Public Function CreateRectangle(ptList As Variant) As AcadLWPolyline Set CreateRectangle = ThisDrawing.ActiveLayout.Block. _ AddLightWeightPolyline(ptList) CreateRectangle.Closed = True End Function ' CreateCircle function draws a Circle object. ' Function expects a center point and radius. Public Function CreateCircle(cenPt As Variant, circRadius) As AcadCircle Set CreateCircle = ThisDrawing.ActiveLayout.Block. _ AddCircle(cenPt, circRadius) End Function ' CreateLayer function creates a layer and returns an AcadLayer object. ' Function expects a layer name and color. Public Function CreateLayer(sName As String, _ nClr As ACAD_COLOR) As AcadLayer On Error Resume Next ' Try to get the layer first and return it if it exists Set CreateLayer = ThisDrawing.Layers(sName) ' If layer doesn't exist create it If Err Then Err.Clear Set CreateLayer = ThisDrawing.Layers.Add(sName) CreateLayer.color = nClr End If End Function

Click File Save.

Defining the CLI_DrawPlate Function

The main function of the DrawPlate project draws a rectangular mounting plate with four bolt holes. The outside edge of the mounting plate is defined using a closed lightweight polyline that is drawn using the CreateRectangle function defined in the clsUtilities class. Each of the bolt holes is drawn using the CreateCircle function of the clsUtilities class. Since objects in a drawing are organized using layers, you will place the rectangle and circles on different layers; the layers will be added to the drawing with the CreateLayer function.

In these steps, you add a new custom module named basDrawPlate to the DrawPlate project:

On the menu bar, click Insert Module.

In the Project Explorer, select the new module named Module1.

In the Properties window, change the current value of the (Name) property to basDrawPlate.

On the menu bar, click File Save.

The following steps explain how to add the CLI_DrawPlate function, which is the macro users will use to create the mounting plate:

In the Project Explorer, double-click the basDrawPlate component.

In the text editor area of the basDrawPlate component, type the following: Private myUtilities As New clsUtilities

The clsUtilities.cls file code statement defines a global variable named myUtilities. The myUtilities variable is then assigned a new instance of the clsUtilities class that you defined earlier. When you want to reference a function defined in the clsUtilities class, you will use the myUtilities variable.

In the text editor area of the basDrawPlate component, press Enter and type the following. (The comments are here for your information and don't need to be typed.)Public Sub CLI_DrawPlate() Dim oLyr As AcadLayer On Error Resume Next ' Store the current value of the system variables to be restored later Dim sysvarNames As Variant, sysvarVals As Variant sysvarNames = Array("nomutt", "clayer", "textstyle") sysvarVals = myUtilities.GetSysvars(sysvarNames) ' Set the current value of system variables myUtilities.SetSysvars sysvarNames, Array(0, "0", "STANDARD") ' Define the width and height for the plate Dim dWidth As Double, dHeight As Double dWidth = 5# dHeight = 2.75 Dim basePt(2) As Double basePt(0) = 0: basePt(1) = 0: basePt(2) = 0 ' Create the layer named Plate or set it current Set oLyr = myUtilities.CreateLayer("Plate", acBlue) ThisDrawing.ActiveLayer = oLyr ' Create the array that will hold the point list ' used to draw the outline of the plate Dim dPtList(7) As Double dPtList(0) = basePt(0): dPtList(1) = basePt(1) dPtList(2) = basePt(0) + dWidth: dPtList(3) = basePt(1) dPtList(4) = basePt(0) + dWidth: dPtList(5) = basePt(1) + dHeight dPtList(6) = basePt(0): dPtList(7) = basePt(1) + dHeight ' Draw the rectangle myUtilities.CreateRectangle dPtList ' Create the layer named Holes or set it current Set oLyr = myUtilities.CreateLayer("Holes", acRed) ThisDrawing.ActiveLayer = oLyr ' Define the center points of the circles Dim cenPt1(2) As Double, cenPt2(2) As Double Dim cenPt3(2) As Double, cenPt4(2) As Double cenPt1(0) = 0.5: cenPt1(1) = 0.5: cenPt1(2) = 0 cenPt2(0) = 4.5: cenPt2(1) = 0.5: cenPt2(2) = 0 cenPt3(0) = 0.5: cenPt3(1) = 2.25: cenPt3(2) = 0 cenPt4(0) = 4.5: cenPt4(1) = 2.25: cenPt4(2) = 0 ' Draw the four circles myUtilities.CreateCircle cenPt1, 0.1875 myUtilities.CreateCircle cenPt2, 0.1875 myUtilities.CreateCircle cenPt3, 0.1875 myUtilities.CreateCircle cenPt4, 0.1875 ' Restore the saved system variable values myUtilities.SetSysvars sysvarNames, sysvarVals End Sub

Click File Save.

Running the CLI_DrawPlate Function

Now that the CLI_DrawPlate function has been defined with the necessary code statements to draw the mounting plate, it can be executed from the AutoCAD user interface. In these steps, you run the CLI_DrawPlate function from the Macros dialog box.

Switch to AutoCAD by clicking on its icon in the Windows taskbar or by clicking View AutoCAD from the menu bar in the Visual Basic Editor.

In AutoCAD, at the Command prompt, type vbarun and press Enter.

When the Macros dialog box opens, select the DrawPlate.dvb!basDrawPlate.CLI_DrawPlate macro from the list and click Run. The new mounting plate is drawn, as shown in Figure 27.9. The mounting plate measures 5×2.75, which was defined in the CLI_DrawPlate function. In Chapter 28, you will learn to accept user input to control the size of the mounting plate that should be drawn.

If you don't see the mounting plate, use the zoom command and zoom to the extents of the drawing area.

Figure 27.9 New mounting plate

Exporting the Utilities Class

The functions in the clsUtilities class can be used in other projects. By exporting the class module out of the DrawPlate project, you can then import it into other projects. Class modules aren't the only components that can be exported from a project; you can export code modules and User Forms that define dialog boxes in a project as well.

The following steps explain how to export the clsUtilities class module from the drawplate.dvb file:

In the VBA Editor, in the Project Explorer, right-click the clsUtilities component and choose Export File.

When the Export File dialog box opens, browse to the MyCustomFiles folder.

Keep the default filename of clsUtilities.cls and click Save. The clsUtilities.cls file is exported from the DrawPlate project.
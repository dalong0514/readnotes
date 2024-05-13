# 0303. Interacting with the Application and Documents Objects

The top object in the AutoCAD® Object library is the AcadApplication object, which allows you to access and manipulate the AutoCAD application window. From the AcadApplication object, you can also access the AcadDocuments collection, which allows you to work with not only the current drawing but all open drawings in the current AutoCAD session. As mentioned in earlier chapters, the ThisDrawing object can be used to access the current drawing.

Working with the Application

The AcadApplication object is the topmost object in the AutoCAD Object library. Although it isn't the most used object, it does provide access to the many features that you will use in VBA projects. All objects in the AutoCAD Object library provide access to the AcadApplication object with the object's Application property. You can access the AcadApplication object from the ThisDrawing object with the following code statement in the VBA Editor:

ThisDrawing.Application

You can also use the following code statement to access the AcadApplication object from a code, class, or UserForm module:

AcadApplication.Application

The following tasks can be performed once you have a reference to the AcadApplication object:

Get the current drawing or the AcadDocuments collection object to work with all open drawings (see the section「Managing Documents」later in this chapter for more information).

List, load, and unload ObjectARX® applications.

Load and unload VBA project files and execute a macro (see Chapter 36,「Handling Errors and Deploying VBA Projects」).

Manipulate the menus on the menu bar and toolbars in the user interface (see Chapter 33,「Modifying the Application and Working with Events」).

Monitor changes to the application, system variables, commands, and more using event handlers (see Chapter 36).

Update the display in the drawing window or zoom in the current viewport (see Chapter 28,「Interacting with the User and Controlling the Current View」).

Access application preferences (see the section「Querying and Setting Application and Document Preferences」later in this chapter for more information).

Get the name of and path to an application executable.

Manipulate the size and position of the application window.

The following shows a few code statements that allow you to query or manipulate an application:

' Gets and displays the caption of the application window MsgBox ThisDrawing.Application.Caption ' Zooms to the extents of all drawing objects in the current viewport AcadApplication.Application.ZoomExtents ' Maximizes the application window ThisDrawing.Application.WindowState = acMax

For a full list of the methods and properties that the AcadApplication object supports, look up the AcadApplication class in the Object Browser of the VBA Editor and the AutoCAD Help system.

Getting Information about the Current AutoCAD Session

The properties of the AcadApplication object can be used to access information about the current instance of the application. You can learn the application name and where the executable is stored, as well as which drawing is current or which drawings are open.

Table 26.1 lists the properties of the AcadApplication object that can be used to get information about the AutoCAD executable.

Table 26.1 Application-related properties

Property Description

FullName Returns a string that contains the full name of the executable file used to start the application. This property is read-only.

HWND Returns a long integer that contains the handle of the application in memory. A handle is a unique value assigned to an application by Windows while it is executing in memory. A different number is assigned to the application each time it is started. This property is read-only.

HWND32 Returns a long integer that contains the handle of the application in memory on a Windows 64-bit platform. This property is read-only and is available in AutoCAD 2014 and earlier releases that didn't support a true implementation of VBA 64-bit on the Windows 64-bit platform.

LocaleId Returns an integer that represents the locale or language being used in the current session. This property is read-only.

Name Returns a string that contains the name and file extension of the executable file used to start the application. This property is read-only.

Path Returns a string that contains the path of the executable file used to start the application. This property is read-only.

Version Returns a string that contains the version number of the application. This property is read-only.

The following demonstrates how to display a message box containing the name, path, and version number of the application:

Sub DisplayAppInfo() MsgBox "Name: " & ThisDrawing.Application.Name & vbLf & _ "Path: " & ThisDrawing.Application.Path & vbLf & _ "FullName : " & ThisDrawing.Application.FullName & vbLf & _ "Version : " & ThisDrawing.Application.Version, _ vbInformation, "Application Info" End Sub

TIP

The FullName and Path properties can be helpful in identifying whether the current AutoCAD session was started from a plain or from a vertical AutoCAD installation. For example, the installation path might be C:\Program Files\Autodesk\AutoCAD 2015\ACA, which lets you know that instance of AutoCAD 2015 should have access to the AutoCAD® Architecture features. You can also use the product system variable to check whether the current AutoCAD instance is a vertical-based product. I discuss working with system variables in the「Working with System Variables」section later in this chapter.

Manipulating the Placement of the Application Window

Some properties of the AcadApplication object can be used to resize, reposition, or even hide the AutoCAD application window from the user.

Table 26.2 lists the AcadApplication object properties that can be used to resize and get information about the application window.

Table 26.2 Application window–related properties

Property Description

Caption Returns a string that contains the title of the application window. This property is read-only.

Height Specifies the height of the application window. The value returned is an integer and represents the window height in pixels.

Visible Specifies the visibility of the application window. The value returned is Boolean. True indicates that the application window is visible, whereas False indicates the window is hidden.

Width Specifies the width of the application window. The value is an integer and represents the window width in pixels.

WindowLeft Specifies the location of the application window's left edge. The value is an integer. 0 sets the window to the leftmost visible position. A negative value moves the window to the left and off the screen, whereas a value greater than 0 moves the window to the right.

WindowState Returns an integer value that represents the current state of the application window. The integer values allowed are defined as part of the AcWindowState enumerator. A value of 1 (or acNorm) indicates the window is neither minimized nor maximized, whereas a value of 2 (or acMin) or 3 (or acMax) indicates the window is minimized or maximized, respectively.

WindowTop Specifies the location of the application window's top edge. The value is an integer. 0 sets the window to the topmost visible position. A negative value moves the window up and off the screen, whereas a value greater than 0 moves the window down.

For more information on these properties, use the Object Browser in the VBA Editor or check the AutoCAD Help system.

Managing Documents

When a drawing file is opened in the AutoCAD drawing environment, it is presented in a drawing window. A drawing window in the AutoCAD Object library is referred to as a document and is represented by an AcadDocument object. The AcadDocument object provides access to the objects in a drawing file and the window in which the drawing is displayed.

The AcadDocuments collection object is used to manage all the drawings open in the current AutoCAD session. You can access the AcadDocuments collection object with the Documents property of the AcadApplication object. In addition to working with drawings in the current session, you can create new and open existing drawing files, save and close open drawings, and get information from an open drawing.

NOTE

As I explained in Chapter 25,「Understanding Visual Basic for Applications,」the For statement can be used to step through and get each drawing in the AcadDocuments collection object. The Item method can also be used to get a specific document in the AcadDocuments collection object.

Working with the Current Drawing

The ThisDrawing object is the most common way to access the current drawing from a VBA project. ThisDrawing is equivalent to using the code statement AcadApplication.ActiveDocument.

From the current drawing, you can perform the following tasks:

Add, query, and modify graphical and nongraphical objects (see Chapter 27,「Creating and Modifying Drawing Objects,」Chapter 29,「Annotating Objects,」and Chapter 30,「Working with Blocks and External References」).

Set a nongraphical object as current (see Chapter 27, Chapter 29, and Chapter 30).

Use utility functions to get user input and perform geometric calculations (see Chapter 28).

Monitor changes to the drawing, commands, objects, and more using event handlers (see Chapter 36).

Select objects using selection sets (see Chapter 27).

Get the name and path to the drawing file stored on disc.

Access and modify drawing properties.

The following shows a few example code statements that access the properties of a current drawing:

' Sets the model space elevation to 10.0 ThisDrawing.ElevationModelSpace = 10# ' Displays a message box with the name of the current layer MsgBox ThisDrawing.ActiveLayer.Name ' Maximizes the drawing window ThisDrawing.WindowState = acMax

For a full list of the methods and properties that the ThisDrawing object supports, look up the AcadDocument class in the Object Browser of the VBA Editor or check the AutoCAD Help system.

Creating and Opening Drawings

Not only can you work with the current drawing, but you can create a new drawing or open an existing drawing file that had been stored on disc. The Add method of the AcadDocuments collection object can be used to create a new drawing from scratch or based on a drawing template (DWT) file. If you don't pass the name of a drawing template file to the Add method, the measurement units of the new drawing is determined by the current value of the measureinit system variable. A value of 0 for the measureinit system variable indicates the new drawing will use imperial units, whereas a value of 1 indicates the use of metric units. The Add method returns an AcadDocument object that represents the new drawing file that has been created in memory.

The following example code statements show how to create a new drawing that uses metric units from scratch or based on the Tutorial-iArch.dwt file that is installed with AutoCAD:

' Set the measurement system for new drawings to metric ThisDrawing.SetVariable "measureinit", 1 ' Create a new drawing from scratch Dim newDWG1 As AcadDocument Set newDWG1 = Application.Documents.Add ' Create a new drawing based on Tutorial-iArch.dwt Dim newDWG2 As AcadDocument Set newDWG2 = Application.Documents.Add("Tutorial-iArch.dwt")

NOTE

If the DWT file passed to the Add method isn't located in a path listed under the Drawing Template File Location node on the Files tab of the Options dialog box, you must specify the full path to the DWT file. The TemplateDwgPath property of the AcadPreferencesFiles object can be used to add additional paths for AutoCAD to look in for DWT files. I discuss application preferences later, in the「Querying and Setting Application and Document Preferences」section.

The New method of an AcadDocument object can also be used to create a new drawing file when the AutoCAD drawing environment is in single document interface (SDI) mode. Autodesk doesn't recommend using SDI mode; it affects the functionality of some features in the AutoCAD drawing environment. You can determine whether AutoCAD is in SDI mode by checking the value of the sdimode system variable or checking the SingleDocumentMode property of the AcadPreferencesSystem object. The New method returns an AcadDocument object that represents the new drawing file that has been created in memory.

When you want to work with an existing drawing file that is stored on a local or network drive, use the Open method of the AcadDocument or AcadDocuments collection object. Here's the syntax of the Open methods:

retVal = document.Open(fullname [, password]) retVal = documents.Open(fullname [, read-only] [, password])

The arguments are as follows:

fullname The fullname argument is a string that represents the DWG file you want to open. You can also open a DWS or DWT file.

password The password argument is an optional string that represents the password that is required to open a password-protected DWG file.

read-only The read-only argument is an optional Boolean that specifies whether the drawing should be open for read-write or read-only. A value of True indicates the drawing should be open for read-only access.

retVal The retVal argument specifies a user-defined variable that you want to assign the AcadDocument object that is returned by the Open method.

The following example code statements show how to open a DWG file named Building_Plan.dwg stored at C:\Drawings, first for read-write and then for read-only access:

' Open Building_Plan.dwg for read-write Dim objDoc1 As AcadDocument set objDoc1 = ThisDrawing.Open("c:\drawings\building_plan.dwg") ' Open Building_Plan.dwg for read-only Dim objDoc2 As AcadDocument set objDoc2 = Application.Documents.Open("c:\drawings\building_plan.dwg", True)

NOTE

Before you try to use a DWT file or open a DWG file, you should make sure the file exists on your workstation. The VBA Dir method can be used to check for the existence of a file or folder. I explain how to work with files in Windows in Chapter 35,「Communicating with Other Applications.」

Saving and Closing Drawings

After you create a new drawing or make changes to an existing drawing file, you most likely will want to save the drawing to a file. Saving a drawing can be accomplished with the Save or SaveAs method of the AcadDocument object. Similar to the user interface, the Save method should be used to save a drawing file that was opened from disc or was previously saved with the SaveAs method.

The Save method accepts no arguments and saves a drawing to the location it was opened from. If you use the Save method on a new drawing that wasn't previously saved, the Save method saves the drawing to the location stored in the Path property of the AcadDocument object. You can determine whether the drawing was previously saved by checking the FullName property of the AcadDocument object; if the property returns an empty string, the drawing hasn't been saved to disc yet.

When you want to save a new drawing, save an existing drawing with a new name or location or in a different file format, or change the password protection, save the drawing with the SaveAs method. Here's the syntax of the SaveAs method:

document.SaveAs(fullname [, SaveAsType] [,SecurityParams])

The arguments are as follows:

fullname The fullname argument is a string that represents the name and path of the drawing or drawing interchange file on disc.

SaveAsType The SaveAsType argument is an optional integer that represents one of the supported file formats. The supported values can be found in the Object Browser of the VBA Editor under the enumerator named AcSaveAsType or in the SaveAs Method topic in the AutoCAD Help system. When not provided, the default format (the native drawing file format for the AutoCAD release you are using) is used. For AutoCAD 2013 and later, the default file format is the AutoCAD 2013 DWG file format.

SecurityParams The SecurityParams argument is an optional AcadSecurityParams object that specifies the password or digital signature settings to apply to the drawing. For information on the AcadSecurityParams object, see the AutoCAD Help system.

Before saving a drawing, you should check to see if the file was opened as read-only or if the drawing already has been saved. The ReadOnly property returns a Boolean value of True when the drawing is opened for read-only access, and the Saved property returns a Boolean value of True if the drawing doesn't need to be saved.

The following example demonstrates how to save a DWG file named SampleVBASave.dwg to the Documents (or My Documents) folder:

' Check to see if the drawing is read-write If ThisDrawing.ReadOnly = False Then ' Check to see if the drawing file was previously saved If ThisDrawing.FullName = "" Then ' Drawing wasn't previously saved ThisDrawing.SaveAs ThisDrawing.GetVariable("MyDocumentsPrefix") & _ "\SampleVBASave.dwg" Else ' Drawing was previously saved to disc ' Check to see if the drawing has been modifed If ThisDrawing.Saved = False Then ThisDrawing.Save End If End If End If

Once a drawing file no longer needs to remain open in the AutoCAD drawing environment, you can close it using the Close method of the AcadDocument object. Alternatively, you can use the Close method of the AcadDocuments collection object, which will close all open drawings and ignore any changes that haven't previously been saved.

Here's the syntax of the Close methods:

document.Close([SaveChanges] [, fullname]) documents.Close

Here are the arguments:

SaveChanges The SaveChanges argument is an optional Boolean that specifies whether the changes made to the drawing should be saved or discarded.

fullname The fullname argument is an optional string that represents a new name and path to use when saving the drawing file if SaveChanges was passed a value of True.

TIP

If you want to close all open drawings, I recommend using the For statement with the AcadDocuments collection object and then close each drawing one at a time with the Close method of the AcadDocument object returned by the For statement. This approach will give you a chance to specify how changes are handled for each drawing as it is closed.

The following example demonstrates a procedure that mimics some of the functionality available with the AutoCAD closeall command:

Sub CloseAll() Dim oDoc As AcadDocument For Each oDoc In Application.Documents ' Activates the document window oDoc.Activate ' Close the drawing if no changes have been made since last save If oDoc.Saved = True Then oDoc.Close False Else Dim nRetVal As Integer nRetVal = MsgBox("Save changes to " & _ oDoc.Path & "\" & oDoc.Name & "?", vbYesNoCancel) Select Case nRetVal Case vbYes ' Save the drawing using its default name or last saved name ' if not open as read-only. If oDoc.ReadOnly = False Then oDoc.Save ' Close the drawing oDoc.Close Else ' Close file and discard changes if file is read-only If vbYes = MsgBox("File is read-only." & vbLf & vbLf & _ "Discard changes and close file?", vbYesNo) Then oDoc.Close False End If End If ' You should prompt the user here if the file was not previously ' saved to disc for a file name and path, or how read-only files ' should be handled. Case vbNo ' Close file and discard changes oDoc.Close False Case vbCancel ' Exit the procedure and return to AutoCAD Exit Sub End Select End If Next oDoc End Sub

NOTE

The previous example doesn't handle all situations that might be encountered when closing and saving changes to a drawing. The Ch26_ExSamples.dvb file, which you can download from www.sybex.com/go/autocadcustomization, contains a more comprehensive and complete solution. Place the file in the MyCustomFiles folder within the Documents (or My Documents) folder, or the location you are using to store the DVB files. Then load the VBA project into the AutoCAD drawing environment to use it. This sample file also contains a custom class that wraps two functions that can be used to display an open or save file-navigation dialog box.

Accessing Information about a Drawing

The properties of an AcadDocument object can be used to access information about the drawing file it represents. You can learn where the drawing file is stored, identify the graphical and nongraphical objects stored in a drawing file, and access the drawing properties that are used to identify a drawing file. I discuss how to access graphical and nongraphical objects later in this book.

Table 26.3 lists the properties of the AcadDocument object that can be used to get the name, location, and drawing properties of a drawing file open in the current AutoCAD session.

NOTE

Use the SaveAs method of the AcadDocument object to save a drawing file with a new name or location.

Table 26.3 Drawing file–related properties

Property Description

FullName Returns a string that contains the full name of the drawing file when it is stored on disc. If the drawing has not been saved yet, this property returns an empty string. This property is read-only.

Name Returns a string that contains the name and file extension of the drawing file. If the drawing has not been saved yet, it returns the default name assigned to the drawing file (that is, Drawing1.dwg, Drawing2.dwg, …). This property is read-only.

Path Returns a string that contains the path of the drawing file when it is stored on disc or the Documents (or My Documents) folder by default if the drawing has not been saved. This property is read-only.

SummaryInfo Returns a reference to an AcadSummaryInfo object, which represents the drawing properties that can be displayed and modified using the AutoCAD dwgprops command. This property is read-only.

The following demonstrates how to display a message box containing the path and name of the current drawing:

Sub DisplayDWGName() MsgBox "Name: " & ThisDrawing.Name & vbLf & _ "Path: " & ThisDrawing.Path & vbLf & _ "FullName : " & ThisDrawing.FullName, _ vbInformation, "File Name and Path" End Sub

To query and set the Author and Comments properties of the AcadSummaryInfo object for the current drawing, you'd use this code:

Sub DWGSumInfo() Dim oSumInfo As AcadSummaryInfo Set oSumInfo = ThisDrawing.SummaryInfo MsgBox "Author: " & oSumInfo.Author & vbLf & _ "Comments: " & oSumInfo.Comments, _ vbInformation, "Drawing Properties" oSumInfo.Author = "Drafter" oSumInfo.Comments = "Phase 1: Demolishion of first floor" MsgBox "Author: " & oSumInfo.Author & vbLf & _ "Comments: " & oSumInfo.Comments, _ vbInformation, "Drawing Properties" End Sub

For more information on the AcadSummaryInfo object, use the Object Browser in the VBA Editor or check the AutoCAD Help system.

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
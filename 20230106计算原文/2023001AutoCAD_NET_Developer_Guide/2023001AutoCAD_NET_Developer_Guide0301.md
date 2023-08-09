## 0301. Basics of the AutoCAD .NET API (.NET)

To use the AutoCAD® .NET API effectively you should be familiar with the AutoCAD entities, objects, and features related to the tasks you want to automate. The greater your knowledge of an object's graphical and non-graphical properties, the easier it is for you to manipulate them through the AutoCAD .NET API.

### 3.1 Understand the AutoCAD Object Hierarchy (.NET)

An object is the main building block of the AutoCAD .NET API. Each exposed object represents a precise part of AutoCAD. There are many different types of objects in the AutoCAD .NET API. Some of the objects represented in the AutoCAD .NET API are:

1 Graphical objects such as lines, arcs, text, and dimensions

2 Style settings such as layers, linetypes, and dimension styles

3 Organizational structures such as layers, groups, and blocks

4 The drawing display such as view and viewport

5 Even the drawing and the AutoCAD application

The objects are structured in a hierarchical fashion, with the AutoCAD Application object at the root. This hierarchical structure is often referred to as the Object Model. The following illustration shows the basic relationships between the Application object and an entity that is in a BlockTableRecord, such as Model space. There are many more objects in the AutoCAD .NET API that are not represented here.

#### The Application Object (.NET)

The Application object is the root object of the AutoCAD .NET API. From the Application object, you can access the main window as well as any open drawing. Once you have a drawing, you can then access the objects in the drawing.

For example, the Application object has a DocumentManager property that returns the DocumentCollection object. This object provides access to the drawings that are currently open in AutoCAD and allows you to create, save and open drawing files. Other properties of the Application object provide access to the application-specific data such as InfoCenter, the main window, and the status bar. The MainWindow property allows access to the application name, size, location, and visibility.

While most of the properties of the Application object allow access to objects in the AutoCAD .NET API, there are some that reference objects in the AutoCAD ActiveX® Automation. These properties include a COM version of the application object (AcadApplication), the menubar (MenuBar), loaded menugroups (MenuGroups), and preferences (Preferences).

DocumentManager

Container for all the document objects (there is a document object for each drawing that is open).

DocumentWindowCollection

Container for all the document window objects (there is a document window object for each document object in the DocumentManager).

InfoCenter

Contains a reference to the InfoCenter toolbar.

MainWindow

Contains a reference to the application window object of AutoCAD.

MenuBar

Contains a reference to the MenuBar COM object for the menubar in AutoCAD.

MenuGroups

Contains a reference to the MenuGroups COM object which contains the customization group name for each loaded CUIx file.

Preferences

Contains a reference to the Preferences COM object which allows you to modify many of the settings in the Options dialog box.

Publisher

Contains a reference to the Publisher object which is used for publishing drawings.

StatusBar

Contains a reference to the StatusBar object for the application window.

UserConfigurationManager

Contains a reference to the UserConfigurationManager object which allows you to work with user saved profiles.

#### The Document Object (.NET)

The Document object, which is actually an AutoCAD drawing, is part of the DocumentCollection object. You use the DocumentExtension and DocumentCollectionExtention objects to create, open, and close drawing files. A Document object provides access to the Database object which contains all of the graphical and most of the non-graphical AutoCAD objects.

Along with the Database object, the Document object provides access to the status bar, the window the document is opened in, the Editor and TransactionManager objects. The Editor object provides access to functions used to obtain input from the user in the form of a point or an entered string or numeric value.

The TransactionManager object is used to access multiple database objects under a single operation known as a transaction. Transactions can be nested, and when you are done with a transaction you can commit or abort the changes made.

#### The Database Object (.NET)

The Database object contains all of the graphical and most of the non-graphical AutoCAD objects. Some of the objects contained in the database are entities, symbol tables, and named dictionaries. Entities in the database represent graphical objects within a drawing. Lines, circles, arcs, text, hatch, and polylines are examples of entities. A user can see an entity on the screen and can manipulate it.

You access the Database object for the current document by the Document object’s Database member property.

Application.DocumentManager.MdiActiveDocument.Database

Symbol Tables and Dictionaries

Symbol table and dictionary objects provide access to non-graphical objects (blocks, layers, linetypes, layouts, and so forth). Each drawing contains a set of nine fixed symbol tables, whereas the number of dictionaries in a drawing can vary based on the features and types of applications used in AutoCAD. New symbol tables cannot be added to a database.

Examples of symbol tables are the layer table (LayerTable), which contains layer table records, and the block table (BlockTable), which contains block table records. All graphical entities (lines, circles, arcs, and so forth) are owned by a block table record. By default, every drawing contains predefined block table records for Model and Paper space. Each Paper space layout has its own block table record.

A dictionary is a container object which can contain any AutoCAD object or an XRecord. Dictionaries are stored either in the database under the named object dictionary or as an extension dictionary of a table record or graphical entity. The named object dictionary is the master table for all of the dictionaries associated with a database. Unlike symbol tables, new dictionaries can be created and added to the named object dictionary.

Note: Dictionary objects cannot contain drawing entities.

VBA/ActiveX Cross Reference

The Database object in the AutoCAD .NET API is similar to the Document object in the ActiveX Automation library. To access most of the properties that are available in the Document object of the ActiveX Automation library, you will need to work with the Document and Database objects of the AutoCAD .NET API.

#### Graphical and Non-graphical Objects (.NET)

Graphical objects, also known as entities, are the visible objects (lines, circles, raster images, and so forth) that make up a drawing. Adding graphical objects to a drawing is done by referencing the correct block table record, and then using the AppendEntity method with the new object to append it to the drawing.

To modify or query objects, obtain a reference to the object from the appropriate block table record, and then use the methods or properties of the object itself. Each graphical object has methods that perform most of the same functionality as the AutoCAD editing commands such as Copy, Erase, Move, Mirror, and so forth.

These objects also have methods to retrieve the extended data (xdata), highlight and unhighlight, and set the properties from another entity. Most graphical objects have some properties in common with each other such as LayerId, LinetypeId, Color, and Handle. Each graphical object also has specific properties, such as Center, StartPoint, Radius, and FitTolerance.

Non-graphical objects are the invisible (informational) objects that are part of a drawing, such as Layers, Linetypes, Dimension styles, Table styles, and so forth. To create a new symbol table records, use the Add method on the owner table or use the SetAt method to add a dictionary to the named object dictionary. To modify or query these objects, use the methods or properties of the object itself. Each non-graphical object has methods and properties specific to its purpose; all have methods to retrieve extended data (xdata), and erase themselves.

#### The Collection Objects (.NET)

AutoCAD groups most graphical and non-graphical objects into collections or container objects. Although collections contain different types of data, they can be processed using similar techniques. Each collection has a method for adding an object to or obtaining an item from a collection. Most collections use the Add or SetAt methods to add an object to a collection.

Most collections offer similar methods and properties to make them easy to use and learn. The Count property returns a zero-based count of the objects in a collection, while the Item function returns an object from a collection. Examples of collection members in the AutoCAD .NET API are:

1 Layer table record in the Layers symbol table

2 Layout in the ACAD_LAYOUT dictionary

3 Document in the DocumentCollection

4 Attributes in a block reference

#### Non-Native Graphical and Nongraphical Objects (.NET)

The AutoCAD .NET API is a cross implementation of ObjectARX and ActiveX Automation. While you can use ActiveX Automation from an ObjectARX application, the AutoCAD .NET API provides direct access to the objects of the ActiveX Automation library. As you work with objects using the native AutoCAD .NET API, you can also access the equivalent COM object from a property. In some cases, the COM object is the only way to access an AutoCAD feature programmatically. Some examples of properties that expose COM objects through the AutoCAD .NET API are, Preferences, Menubar, MenuGroups, AcadObject and AcadApplication.

Note: When working with COM objects, you will want to make sure you reference the AutoCAD type library.
The Preferences property of the Application object provides access to a set of COM objects, each corresponding to a tab in the Options dialog box. Together, these objects provide access to all the registry-stored settings in the Options dialog box. You can also set and modify options (and system variables that are not part of the Options dialog box) with the SetSystemVariable and GetSystemVariable methods of the Application object.

Accessing COM objects is useful if you are working with existing code that might have been originally developed for VB or VBA, or even when working with a third-party library that might work with the AutoCAD ActiveX Automation library with the AutoCAD .NET API. Like the Preferences object, you can also access utilities which translate coordinates or define a new point based on an angle and distance using the Utility object which can be accessed from the AcadApplication COM object which is the equivalent of the Application object in the AutoCAD .NET API.

Note: When working with both the AutoCAD .NET API and ActiveX Automation, and you create custom functions that might need to return an object, it is recommended to return an ObjectId instead of the object itself.

### 3.2 Access the Object Hierarchy (.NET)

While the Application is the root object in the AutoCAD .NET API, you commonly will be working with the database of the current drawing. The DocumentManager property of the Application object allows you to access the current document with the MdiActiveDocument property. From the Document object returned by the MdiActiveDocument property, you can access its database with the Database property.

VB.NET

Application.DocumentManager.MdiActiveDocument.Database.Clayer

C#

Application.DocumentManager.MdiActiveDocument.Database.Clayer;

VBA/ActiveX Code Reference

ThisDrawing.ActiveLayer

#### Reference Objects in the Object Hierarchy (.NET)

When you work with objects in the AutoCAD .NET API, you can reference some objects directly or through a user-defined variable based on the object you are working with. To reference an objects directly, include the object in the calling hierarchy. For example, the following statement attaches a drawing file to the database of the current drawing. Notice that the hierarchy starts with the Application and then goes to the Database object. From the Database object, the AttachXref method is called:

To reference the objects through a user-defined variable, define the variable as the desired type, then set the variable to the appropriate object. For example, the following code defines a variable (acCurDb) of type Autodesk.AutoCAD.DatabaseServices.Database and sets the variable equal to the current database:

The following statement then attaches a drawing file to the database using the acCurDb user-defined variable:

Retrieve entities from Model space
The following example returns the first entity object in Model space. Similar code can do the same for Paper space entities. Note that all graphical objects are defined as an Entity object:

#### Access the Application Object (.NET)

The Application object is at the root of the object hierarchy and it provides access to the main window of AutoCAD. For example, the following line of code updates the application:

VB.NET

Autodesk.AutoCAD.ApplicationServices.Application.UpdateScreen()

C#

Autodesk.AutoCAD.ApplicationServices.Application.UpdateScreen();

VBA/ActiveX Code Reference

ThisDrawing.Application.Update

### 3.3 Collection Objects (.NET)

A collection is a type of object that contains many instances of similar objects. The following list contains some of the collection objects that are found in the AutoCAD .NET API:

Block Table Record

Contains all entities within a specific block definition.

Block Table

Contains all blocks in the drawing.

Named Objects Dictionary 

Contains all dictionaries in the drawing.

Dimension Style Table 

Contains all dimension styles in the drawing.

Document Collection

Contains all open drawings in the current session.

Group Dictionary

Contains all groups in the drawing.

Hyperlink Collection

Contains all hyperlinks for a given entity.

Layer Table

Contains all layers in the drawing.

Layout Dictionary

Contains all layouts in the drawing.

Linetype Table

Contains all linetypes in the drawing.

MenuBar Collection

Contains all menus currently displayed in AutoCAD.

MenuGroup Collection

Contains all customization groups currently loaded in AutoCAD. A customization group represents a loaded CUIx file which can contain menus, toolbars, and ribbon tabs among other elements that define the user interface.

Plot Configuration Dictionary

Contains named plot settings in the drawing.

Registered Application Table

Contains all registered applications in the drawing.

Text Style Table

Contains all text styles in the drawing.

UCS Table

Contains all user coordinate systems (UCS's) in the drawing.

View Table

Contains all views in the drawing.

Viewport Table

Contains all viewports in the drawing.

#### Access a Collection (.NET)

Most collection and container objects are accessed through the Document or Database objects. The Document and Database objects contain a property to access an object or object id for most of the available Collection objects. For example, the following code defines a variable and retrieves the LayersTable object which represents the collection of Layers in the current drawing:

```cs
// Get the current document and start the Transaction Manager
Database acCurDb = Application.DocumentManager.MdiActiveDocument.Database;
using (Transaction acTrans = acCurDb.TransactionManager.StartTransaction())
{
    // This example returns the layer table for the current database
    LayerTable acLyrTbl;
    acLyrTbl = acTrans.GetObject(acCurDb.LayerTableId,
                                 OpenMode.ForRead) as LayerTable;
 
     // Dispose of the transaction
}
```

#### Add a New Member to a Collection Object (.NET)

To add a new member to the collection, use the Add method. For example, the following code creates a new layer and adds it to the Layer table:

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
 
[CommandMethod("AddMyLayer")]
public static void AddMyLayer()
{
  // Get the current document and database, and start a transaction
  Document acDoc = Application.DocumentManager.MdiActiveDocument;
  Database acCurDb = acDoc.Database;
 
  using (Transaction acTrans = acCurDb.TransactionManager.StartTransaction())
  {
      // Returns the layer table for the current database
      LayerTable acLyrTbl;
      acLyrTbl = acTrans.GetObject(acCurDb.LayerTableId,
                                   OpenMode.ForRead) as LayerTable;
 
      // Check to see if MyLayer exists in the Layer table
      if (acLyrTbl.Has("MyLayer") != true)
      {
          // Open the Layer Table for write
          acTrans.GetObject(acCurDb.LayerTableId, OpenMode.ForWrite);
 
          // Create a new layer table record and name the layer "MyLayer"
          using (LayerTableRecord acLyrTblRec = new LayerTableRecord())
          {
              acLyrTblRec.Name = "MyLayer";
 
              // Add the new layer table record to the layer table and the transaction
              acLyrTbl.Add(acLyrTblRec);
              acTrans.AddNewlyCreatedDBObject(acLyrTblRec, true);
          }

          // Commit the changes
          acTrans.Commit();
      }
 
      // Dispose of the transaction
  }
}
```





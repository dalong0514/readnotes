## 0501. Create and Edit AutoCAD Entities (.NET)

你是一名精通 AutoCAD、AutoCAD .NET 二次开发的编程人员。我想让你充当英文翻译员、拼写纠正员和改进员。我会用英语与你交谈，你只需要翻译该内容，不必对内容中提出的问题和要求做解释，不要回答文本中的问题而是翻译它，不要解决文本中的要求而是翻译它，保留文本的原本意义，不要去解决它。我要你只回复更正、改进，不要写任何解释，不要遗漏内容。翻译的中文要求：1）严谨。2）英文字符和中文字符之间用空格隔开。我的第一句话是：

2019073AutoCAD.NET开发指南

You can create a range of objects, from simple lines and circles to spline curves, ellipses, and associative hatch areas. In general, you add objects to a BlockTableRecord object using the AppendEntity function. Once an object is created, you can change its properties such as layer, color, and linetype.

The drawing database is similar to other database programs, you can think of a Line object in Model space as table record and Model space as its database table. When working with a database, you must open and close records before working with them. The objects stored in the Database object are no different, you use the GetObject function to retrieve an object from the database and define how you want to work with the object.

### 5.1 Open and Close Objects (.NET)

Whether you are working with objects such as lines, circles and polyline or a symbol table and its records, you need to open the object for read or write. When querying an object you want to open the object for read, but if you are going to make changes to the object you will want to open it for write.

#### Work With ObjectIds (.NET)

Each object contained within a database is assigned several unique ids. The unique ways you can access objects are:

Entity handle

ObjectId

Instance pointer

The most common way to access an object is by its ObjectId. ObjectIds work well if your projects utilize both COM interop and the managed AutoCAD .NET API. If you create custom AutoLISP functions, you may need to work with entity handles.

Handles are persistent between AutoCAD sessions, so they are the best way of accessing objects if you need to export drawing information to an external file which might later need to be used to update the drawing. The ObjectId of an object in a database exists only while the database is loaded into memory. Once the database is closed, the ObjectId assigned to an object no longer exist and maybe different the next time the database is opened.

Obtain an ObjectId

As you work with objects, you will need to obtain an ObjectId first before you can open the object to query or edit it. An ObjectId is assigned to an existing object in the database when the drawing file is opened, and new objects are assigned an ObjectId when they are first created. An ObjectId is commonly obtained for an existing object in the database by:

1 Using a member property of the Database object, such as Clayer which retrieves the Object ID for the current layer

2 Iterating a symbol table, such as the Layer symbol table

Open an Object

Once an Object Id is obtained, the GetObject function is used to open the object assigned the given Object Id. An object can be opened in one of the following modes:

Read. Opens an object for read.

Write. Opens an object for write if it is not already open.

Notify. Opens an object for notification when it is closed, open for read, or open for write, but not when it is already open for notify. This mode is intended for use when an object might modify itself from within its own code, such as when defining a custom object which is not supported with the AutoCAD Managed .NET API.

You should open an object in the mode that is best for the situation in which the object will be accessed. Opening an object for write introduces additional overhead than you might need due to the creation of undo records. If you are unsure if the object you are opening is the one you want to work with, you should open it for read and then upgrade the object from read to write mode. For more information on upgrading an object, see "Upgrade and Downgrade Open Objects (.NET)."

Both the GetObject and Open functions return an object. When working with some programming languages, you will need to cast the returned value based on the variable the value is being assigned to. If you are using VB.NET, you do not need to worry about casting the return value as it is done for you.

When working with the Dynamic Runtime Language (DLR), you do not need to worry about opening an object for read or write. The opening of an object is handled transparently for you, and so is the process of committing the changes made to an object without using transactions.

The following examples show how to obtain the LayerTableRecord for Layer Zero of the current database.

The following example manually disposes of the transaction after it is no longer needed.

```cs
Document acCurDb = Application.DocumentManager.MdiActiveDocument.Database;
Transaction acTrans = acCurDb.TransactionManager.StartTransaction();
 
LayerTableRecord acLyrTblRec;
acLyrTblRec = acTrans.GetObject(acCurDb.LayerZero,
                                OpenMode.ForRead) as LayerTableRecord;
 
acTrans.Dispose();
```

The following example uses the Using statement to dispose of the transaction after it is no longer needed. The Using statement is the preferred coding style.

```cs
Document acCurDb = Application.DocumentManager.MdiActiveDocument.Database;
using (Transaction acTrans = acCurDb.TransactionManager.StartTransaction())
{
    LayerTableRecord acLyrTblRec;
    acLyrTblRec = acTrans.GetObject(acCurDb.LayerZero,
                                    OpenMode.ForRead) as LayerTableRecord;
}
```

#### Use Transactions With the Transaction Manager (.NET)

Transactions are used to group multiple operations on multiple objects together as a single operation. Transactions are started and managed through the Transaction Manager. Once a transaction is started, you can then use the GetObject function to open an object.

As you work with objects opened with GetObject, the Transaction manager keeps track of the changes that are being made to the object. Any new objects that you create and add to the database should be added to a transaction as well with the AddNewlyCreatedDBObject function. Once the objects have been edited or added to the database, you can save the changes made to the database and close all the open objects with the Commit function on the Transaction object created with the Transaction Manager. Once you are finished with a transaction, call the Dispose function close the transaction.

01 Use Transactions to Access and Create Objects (.NET)

The Transaction Manager is accessed from the TransactionManager property of the current database. Once a reference to the Transaction Manager is made, you can use one of the following methods to start or obtain a transaction:

1 StartTransaction – Starts a new transaction by creating a new instance of a Transaction object. Use this method when you need to write to an object multiple times and control how the changes can be rolled back through the use of different nesting levels.

2 StartOpenCloseTransation – Creates an OpenCloseTransaction object, which behaves similar to a Transaction object, that wraps the Open and Close methods of an object making it easier to close all opened objects instead of having to explicitly close each opened object. Recommended for use in support or utility functions that might be called an unknown number of times, and used when working with most event handlers.

Once you have a Transaction or OpenCloseTransaction object, use the GetObject method to open an object stored in the database for read or write. The GetObject method returns a DBObject which can be cast to the actual object type it represents.

All open objects opened during a transaction are closed at the end of the transaction. To end a transaction, call the Dispose method of a transaction object. If you use the Using and End Using keywords to indicate the start and end of a transaction, you do not need to call the Dispose method.

Prior to disposing of a transaction, you should commit any changes made with the Commit method. If the changes are not committed before a transaction is disposed, any changes made are rolled back to the state they were in prior to the start of the transaction.

More than one transaction can be started. The number of active transactions can be retrieved with the NumberOfActiveTransactions property of the TransactionManager object while the top most or latest transaction can be retrieved with the TopTransaction property.

Transactions can be nested one inside of another in order to roll back some of the changes made during the execution of a routine.

Query objects

The following example demonstrates how to open and read objects within using a transaction. You use the GetObject method to first open the BlockTable and then the Model space record.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
 
[CommandMethod("StartTransactionManager")]
public static void StartTransactionManager()
{
    // Get the current document and database
    Document acDoc = Application.DocumentManager.MdiActiveDocument;
    Database acCurDb = acDoc.Database;
 
    // Start a transaction
    using (Transaction acTrans = acCurDb.TransactionManager.StartTransaction())
    {
        // Open the Block table for read
        BlockTable acBlkTbl;
        acBlkTbl = acTrans.GetObject(acCurDb.BlockTableId,
                                     OpenMode.ForRead) as BlockTable;
 
        // Open the Block table record Model space for read
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForRead) as BlockTableRecord;
 
        // Step through the Block table record
        foreach (ObjectId asObjId in acBlkTblRec)
        {
            acDoc.Editor.WriteMessage("\nDXF name: " + asObjId.ObjectClass.DxfName);
            acDoc.Editor.WriteMessage("\nObjectID: " + asObjId.ToString());
            acDoc.Editor.WriteMessage("\nHandle: " + asObjId.Handle.ToString());
            acDoc.Editor.WriteMessage("\n");
        }
 
        // Dispose of the transaction
    }
}
```

Add a new object to the database

The following example demonstrates how to add a circle object to the database with in a transaction. You use the GetObject method to first open the BlockTable for read and then the Model space record for write. After Model space is opened for write, you use the AppendEntity and AddNewlyCreatedDBObject function to append the new Circle object to Model space as well as the transaction.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("AddNewCircleTransaction")]
public static void AddNewCircleTransaction()
{
    // Get the current document and database
    Document acDoc = Application.DocumentManager.MdiActiveDocument;
    Database acCurDb = acDoc.Database;

    // Start a transaction
    using (Transaction acTrans = acCurDb.TransactionManager.StartOpenCloseTransaction())
    {
        // Open the Block table for read
        BlockTable acBlkTbl;
        acBlkTbl = acTrans.GetObject(acCurDb.BlockTableId,
                                        OpenMode.ForRead) as BlockTable;

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForWrite) as BlockTableRecord;

        // Create a circle with a radius of 3 at 5,5
        using (Circle acCirc = new Circle())
        {
            acCirc.Center = new Point3d(5, 5, 0);
            acCirc.Radius = 3;

            // Add the new object to Model space and the transaction
            acBlkTblRec.AppendEntity(acCirc);
            acTrans.AddNewlyCreatedDBObject(acCirc, true);
        }

        // Commit the changes and dispose of the transaction
        acTrans.Commit();
    }
}
```

02 Commit and Rollback Changes (.NET)

When using transactions, you are able to decide when changes to objects are saved to the drawing database. You use the Commit method to save the changes made to the objects opened within a transaction. If your program encounters an error you can rollback any changes made within a transaction with the Abort method.

If Commit is not called before Dispose is called, all changes made within the transaction are rolled back. Whether Commit or Abort is called, you need to call Dispose to signal the end of the transaction. If the transaction object is started with the Using statement, you do not have to call Dispose.

```cs
// Commit the changes made within the transaction
<transaction>.Commit();
 
// Abort the transaction and rollback to the previous state
<transaction>.Abort();
```

03 Dispose Objects (.NET)

When creating new objects in .NET, you must properly free the objects from memory through the disposal process and garbage collection. You use the Dispose method or the Using statement to signal when an object is ready for garbage collection. The Using statement in most cases is the preferred method, as it makes the proper calls to close and dispose of the object when it is no longer needed.

You need to dispose of an object under the following conditions:

Always with a Transaction or DocumentLock object

Always with newly created database objects, objects derived from DBObject, that are being added to a transaction

Always with newly created database objects, objects derived from DBObject, that are not added to the database

Do not have to with existing database objects, objects derived from DBObject, opened with a transaction object and the GetObject method

```cs
// Dispose an object with the using statement
using (<dataType> <object>  = <value>)
    // Do something here
}
 
// Manually dispose of an object with the Dispose method
<object>. Dispose ();
```

04 Nest Transactions (.NET)

Transactions can be nested one inside another. You might have an outer transaction to undo all the changes made by your routine and inner transactions to undo just portions of the changes made. When you work with nested transactions, you start with a top transaction which is also the outer most transaction.

As you start new transactions, they are added into the previous transaction. Nested transactions must be committed or aborted in the opposite order in which they are created. So if you have three transactions, you must close the third or innermost one before the second and finally the first. If you abort the first transaction, the changes made by all three transactions are undone.

The following illustration shows how transactions appear when nested.

Use nested transactions to create and modify objects

The following example demonstrates using three transactions to create a Circle and Line object, and then change their colors. The color of the circle is changed in the second and third transaction, but since the third transaction is aborted only the changes made in the first and second transactions are saved to the database. Additionally, the number of active transactions is printed in the Command Line window as they are created and closed.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
using Autodesk.AutoCAD.EditorInput;
 
[CommandMethod("NestedTransactions")]
public static void NestedTransactions()
{
    // Get the current document and database
    Document acDoc = Application.DocumentManager.MdiActiveDocument;
    Database acCurDb = acDoc.Database;

    // Create a reference to the Transaction Manager
    Autodesk.AutoCAD.DatabaseServices.TransactionManager acTransMgr;
    acTransMgr = acCurDb.TransactionManager;

    // Create a new transaction
    using (Transaction acTrans1 = acTransMgr.StartTransaction())
    {
        // Print the current number of active transactions
        acDoc.Editor.WriteMessage("\nNumber of transactions active: " +
                                    acTransMgr.NumberOfActiveTransactions.ToString());

        // Open the Block table for read
        BlockTable acBlkTbl;
        acBlkTbl = acTrans1.GetObject(acCurDb.BlockTableId,
                                        OpenMode.ForRead) as BlockTable;

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans1.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                            OpenMode.ForWrite) as BlockTableRecord;

        // Create a circle with a radius of 3 at 5,5
        using (Circle acCirc = new Circle())
        {
            acCirc.Center = new Point3d(5, 5, 0);
            acCirc.Radius = 3;

            // Add the new object to Model space and the transaction
            acBlkTblRec.AppendEntity(acCirc);
            acTrans1.AddNewlyCreatedDBObject(acCirc, true);

            // Create the second transaction
            using (Transaction acTrans2 = acTransMgr.StartTransaction())
            {
                acDoc.Editor.WriteMessage("\nNumber of transactions active: " +
                                            acTransMgr.NumberOfActiveTransactions.ToString());

                // Change the circle's color
                acCirc.ColorIndex = 5;

                // Get the object that was added to Transaction 1 and set it to the color 5
                using (Line acLine = new Line(new Point3d(2, 5, 0), new Point3d(10, 7, 0)))
                {
                    acLine.ColorIndex = 3;

                    // Add the new object to Model space and the transaction
                    acBlkTblRec.AppendEntity(acLine);
                    acTrans2.AddNewlyCreatedDBObject(acLine, true);
                }

                // Create the third transaction
                using (Transaction acTrans3 = acTransMgr.StartTransaction())
                {
                    acDoc.Editor.WriteMessage("\nNumber of transactions active: " +
                                                acTransMgr.NumberOfActiveTransactions.ToString());

                    // Change the circle's color
                    acCirc.ColorIndex = 3;

                    // Update the display of the drawing
                    acDoc.Editor.WriteMessage("\n");
                    acDoc.Editor.Regen();

                    // Request to keep or discard the changes in the third transaction
                    PromptKeywordOptions pKeyOpts = new PromptKeywordOptions("");
                    pKeyOpts.Message = "\nKeep color change ";
                    pKeyOpts.Keywords.Add("Yes");
                    pKeyOpts.Keywords.Add("No");
                    pKeyOpts.Keywords.Default = "No";
                    pKeyOpts.AllowNone = true;

                    PromptResult pKeyRes = acDoc.Editor.GetKeywords(pKeyOpts);

                    if (pKeyRes.StringResult == "No")
                    {
                        // Discard the changes in transaction 3
                        acTrans3.Abort();
                    }
                    else
                    {
                        // Save the changes in transaction 3
                        acTrans3.Commit();
                    }

                    // Dispose the transaction
                }

                acDoc.Editor.WriteMessage("\nNumber of transactions active: " +
                                            acTransMgr.NumberOfActiveTransactions.ToString());

                // Keep the changes to transaction 2
                acTrans2.Commit();
            }
        }

        acDoc.Editor.WriteMessage("\nNumber of transactions active: " +
                                    acTransMgr.NumberOfActiveTransactions.ToString());

        // Keep the changes to transaction 1
        acTrans1.Commit();
    }
}
```

#### Open and Close Objects Without the Transaction Manager (.NET)

Transactions make it easier to open and work with multiple objects, but they are not the only way to open and edit objects. Other than using a transaction, you can open and close objects using the Open and Close methods. You still need to obtain an object Id to use the Open method. Like the GetObject method used with transactions, you need to specify an open mode and the return value is an object.

If you make changes to an object after you opened it with the Open method, you can use the Cancel method to rollback all the changes made since it was opened. Cancel must be called on each object in which you want to rollback. Objects must also be properly disposed of with the Dispose method after an object is closed or you can use the Using statement to close and dispose of an object.

Note: Objects must be paired with an open and close operation. If you use the Open method without the Using statement, you must call either the Close or Cancel method on an opened object. Failure to close an object will lead to read access violations and cause AutoCAD to become unstable.
If you need to work with a single object, using the Open and Close methods can reduce the number of lines of code that you might otherwise have to write compared to working with the Transaction Manager. However, using transactions is the recommended way of opening and closing objects.

Caution: You should not directly use the Open and Close methods when using transactions, as objects might not get opened or closed properly by the Transaction Manager which could cause AutoCAD to become unstable. Instead, use the StartOpenCloseTransation method to create an OpenCloseTransaction object which wraps the Open and Close methods.

Query objects (manually open and close objects)

This example demonstrates how to manually open and close objects without using a transaction and the GetObject method.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
 
[CommandMethod("OpenCloseObjectId")]
public static void OpenCloseObjectId()
{
    // Get the current document and database
    Document acDoc = Application.DocumentManager.MdiActiveDocument;
    Database acCurDb = acDoc.Database;

    // Open the Block table for read
    BlockTable acBlkTbl = null;

    try
    {
        acBlkTbl = acCurDb.BlockTableId.Open(OpenMode.ForRead) as BlockTable;

        // Open the Block table record Model space for read
        BlockTableRecord acBlkTblRec = null;

        try
        {
            acBlkTblRec = acBlkTbl[BlockTableRecord.ModelSpace].Open(OpenMode.ForRead) as BlockTableRecord;

            // Step through the Block table record
            foreach (ObjectId acObjId in acBlkTblRec)
            {
                acDoc.Editor.WriteMessage("\nDXF name: " + acObjId.ObjectClass.DxfName);
                acDoc.Editor.WriteMessage("\nObjectID: " + acObjId.ToString());
                acDoc.Editor.WriteMessage("\nHandle: " + acObjId.Handle.ToString());
                acDoc.Editor.WriteMessage("\n");
            }
        }
        catch (Autodesk.AutoCAD.Runtime.Exception es)
        {
            System.Windows.Forms.MessageBox.Show(es.Message);
        }
        finally
        {
            // Close the Block table
            if (!acBlkTblRec.ObjectId.IsNull)
            {
                // Close the Block table record
                acBlkTblRec.Close();
                acBlkTblRec.Dispose();
            }
        }
    }
    catch (Autodesk.AutoCAD.Runtime.Exception es)
    {
        System.Windows.Forms.MessageBox.Show(es.Message);
    }
    finally
    {
        // Close the Block table
        if (!acBlkTbl.ObjectId.IsNull)
        {
            acBlkTbl.Close();
            acBlkTbl.Dispose();
        }
    }
}
```

Query objects (Using statement)

The following example demonstrates how to open and close objects with the Using statement instead of manually closing and disposing of objects.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
 
[CommandMethod("OpenCloseObjectIdWithUsing")]
public static void OpenCloseObjectIdWithUsing()
{
    // Get the current document and database
    Document acDoc = Application.DocumentManager.MdiActiveDocument;
    Database acCurDb = acDoc.Database;

    // Open the Block table for read
    using (BlockTable acBlkTbl = acCurDb.BlockTableId.Open(OpenMode.ForRead) as BlockTable)
    {
        // Open the Block table record Model space for read
        using (BlockTableRecord acBlkTblRec = acBlkTbl[BlockTableRecord.ModelSpace].Open(OpenMode.ForRead)
                                                as BlockTableRecord)
        {
            // Step through the Block table record
            foreach (ObjectId acObjId in acBlkTblRec)
            {
                acDoc.Editor.WriteMessage("\nDXF name: " + acObjId.ObjectClass.DxfName);
                acDoc.Editor.WriteMessage("\nObjectID: " + acObjId.ToString());
                acDoc.Editor.WriteMessage("\nHandle: " + acObjId.Handle.ToString());
                acDoc.Editor.WriteMessage("\n");
            }

        // Close the Block table record
        }

        // Close the Block table
    }
}
```

Add a new object to the database

This example demonstrates how to create a new object and append it to Model space without using the Transaction Manager.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("AddNewCircleOpenClose")]
public static void AddNewCircleOpenClose()
{
    // Get the current document and database
    Document acDoc = Application.DocumentManager.MdiActiveDocument;
    Database acCurDb = acDoc.Database;

    // Open the Block table for read
    using (BlockTable acBlkTbl = acCurDb.BlockTableId.Open(OpenMode.ForRead) as BlockTable)
    {
        // Open the Block table record Model space for write
        using (BlockTableRecord acBlkTblRec = acBlkTbl[BlockTableRecord.ModelSpace].Open(OpenMode.ForWrite)
                                                as BlockTableRecord)
        {
            // Create a circle with a radius of 3 at 5,5
            using (Circle acCirc = new Circle())
            {
                acCirc.Center = new Point3d(5, 5, 0);
                acCirc.Radius = 3;

                // Add the new object to Model space and the transaction
                acBlkTblRec.AppendEntity(acCirc);

                // Close and dispose the circle object
            }

            // Close the Block table record
        }

        // Close the Block table
    }
}
```

#### Upgrade and Downgrade Open Objects (.NET)

An object's current open mode can be changed from read to write or write to read by upgrading or downgrading the object.

These methods can be used to upgrade or downgrade a previously opened object:

Transaction.GetObject method – If the object was opened with the Transaction.GetObject method, use the method to reopen the object with the desired new open mode.

UpgradeOpen and DowngradeOpen methods – If the object was opened with the Open method, or the OpenCloseTransaction.GetObject, use the UpgradeOpen method to change the object’s open mode from read to write or DowngradeOpen method to change the object’s open mode from write to read. You do not need to pair a call to DowngradeOpen with each UpgradeOpen, since closing of an object or disposing of a transaction will sufficiently cleanup the open state of an object.

It is recommended to open an object with the mode that best matches how the object will be used, as it is more efficient to open an object for read and query the object’s properties than it is to open the object for write and query the object’s properties. If you are uncertain whether an object might need to be modified, it is best to open the object for read and then upgrade it for write as this helps to reduce the overhead of your program.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
 
[CommandMethod("FreezeDoorLayer")]
public static void FreezeDoorLayer()
{
    // Get the current document and database
    Document acDoc = Application.DocumentManager.MdiActiveDocument;
    Database acCurDb = acDoc.Database;

    // Start a transaction
    using (Transaction acTrans = acCurDb.TransactionManager.StartTransaction())
    {
        // Open the Layer table for read
        LayerTable acLyrTbl;
        acLyrTbl = acTrans.GetObject(acCurDb.LayerTableId,
                                        OpenMode.ForRead) as LayerTable;

        // Step through each layer and update those that start with 'Door'
        foreach (ObjectId acObjId in acLyrTbl)
        {
            // Open the Layer table record for read
            LayerTableRecord acLyrTblRec;
            acLyrTblRec = acTrans.GetObject(acObjId,
                                            OpenMode.ForRead) as LayerTableRecord;

            // Check to see if the layer's name starts with 'Door' 
            if (acLyrTblRec.Name.StartsWith("Door",
                                            StringComparison.OrdinalIgnoreCase) == true)
            {
                // Check to see if the layer is current, if so then do not freeze it
                if (acLyrTblRec.ObjectId != acCurDb.Clayer)
                {
                    // Change from read to write mode
                    acTrans.GetObject(acObjId, OpenMode.ForWrite);

                    // Freeze the layer
                    acLyrTblRec.IsFrozen = true;
                }
            }
        }

        // Commit the changes and dispose of the transaction
        acTrans.Commit();
    }
}
```

#### About Using the Dynamic Language Runtime (.NET)

The AutoCAD Managed .NET API allows you to utilize the Dynamic Language Runtime (DLR) that was introduced with .NET 4.0.

Using DLR allows you to access objects directly without having to:

Open an object for read or write, and then close the object once you are done.

Utilize transactions to commit the changes made.

You can access the properties and methods of an object directly once you have obtained its ObjectId when using DLR. After you have obtained an ObjectId, you can assign the ObjectId to a variable of the data type:

Object in VB.NET

dynamic in C#

Obtaining an ObjectId varies by how the object is saved to the database. For objects stored in a table or dictionary, you can access its ObjectId by:

Using the Item method of an ObjectId to access an element in the collection.

Creating a reference to the ObjectId of the table or dictionary and assigning it to a variable, and then accessing the element of the array.

The following sample code shows both options for accessing an object that is stored in a table or dictionary with DLR:

```cs
C#
// Item method
dynamic acCurDb = HostApplicationServices.WorkingDatabase;
dynamic acMSpace = acCurDb.BlockTableId.Item(BlockTableRecord.ModelSpace);

// Reference an element directly from a collection
dynamic acCurDb = HostApplicationServices.WorkingDatabase;
dynamic acBlkTbl = acCurDb.BlockTableId;
dynamic acMSpace = acBlkTbl[BlockTableRecord.ModelSpace];
```

Important: When working with DLR and C#, you will need to reference the Microsoft.CSharp library.

Working with the GetEnumerator Method

When using the GetEnumerator method with DLR, you need to explicitly dispose of the enumerator object once you are done working with it. The following sample demonstrates how to dispose of the enumerator when you are done with it.

```cs
C#
dynamic acCurDb = HostApplicationServices.WorkingDatabase;
var acLtypeTbl = acCurDb.LinetypeTableId;
var acTblEnum = acLtypeTbl.GetEnumerator();
...
acTblEnum.Dispose();
```

Using LINQ Queries

You can utilize LINQ queries to query the contents of a table or dictionary in a drawing with DLR. The following sample demonstrates the use of LINQ queries to query which layers have certain states assigned to them in the current drawing.

```cs
C#
[CommandMethod("LINQ")]
public static void LINQExample()
{
    dynamic db = HostApplicationServices.WorkingDatabase;
    dynamic doc = Application.DocumentManager.MdiActiveDocument;

    var layers = db.LayerTableId;
    for (int i = 0; i < 2; i++)
    {
        var newrec = layers.Add(new LayerTableRecord());
        newrec.Name = "Layer" + i.ToString();
        if (i == 0)
            newrec.IsFrozen = true;
        if (i == 1)
            newrec.IsOff = true;
    }

    var OffLayers = from l in (IEnumerable<dynamic>)layers
                    where l.IsOff
                    select l;

    doc.Editor.WriteMessage("\nLayers Turned Off:");

    foreach (dynamic rec in OffLayers)
        doc.Editor.WriteMessage("\n - " + rec.Name);

    var frozenOrOffNames = from l in (IEnumerable<dynamic>)layers
                            where l.IsFrozen == true || l.IsOff == true
                            select l;

    doc.Editor.WriteMessage("\nLayers Frozen or Turned Off:");

    foreach (dynamic rec in frozenOrOffNames)
        doc.Editor.WriteMessage("\n - " + rec.Name);
}
```

Sample Code

The sample code on this page uses the following name spaces:

```cs
Autodesk.AutoCAD.Runtime
Autodesk.AutoCAD.ApplicationServices
Autodesk.AutoCAD.DatabaseServices
Autodesk.AutoCAD.Colors
Autodesk.AutoCAD.Geometry
```

The following sample code demonstrates how to add a Line to the current space; with and without DLR.

```cs
[CommandMethod("ADDLINE")]
public static void AddLine()
{
    // Get the current database
    Database acCurDb = HostApplicationServices.WorkingDatabase;

    // Start a transaction
    using (Transaction acTrans = acCurDb.TransactionManager.StartTransaction())
    {
        // Open the Block table for read
        BlockTable acBlkTbl;
        acBlkTbl = acTrans.GetObject(acCurDb.BlockTableId,
                                     OpenMode.ForRead) as BlockTable;

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForWrite) as BlockTableRecord;

        // Create a line that starts at 5,5 and ends at 12,3
        using (Line acLine = new Line(new Point3d(5, 5, 0),
                                      new Point3d(12, 3, 0)))
        {
            // Add the new object to the block table record and the transaction
            acBlkTblRec.AppendEntity(acLine);
            acTrans.AddNewlyCreatedDBObject(acLine, true);
        }

        // Save the new object to the database
        acTrans.Commit();
    }
}
```

C# with Dynamic Language Runtime (DLR)

```cs
[CommandMethod("ADDLINE")]
public static void AddLine()
{
    // Get the current database
    dynamic acCurDb = HostApplicationServices.WorkingDatabase;

    // Create a dynamic reference to model or paper space
    dynamic acSpace = acCurDb.CurrentSpaceId;

    // Create a line that starts at 5,5 and ends at 12,3
    dynamic acLine = new Line(new Point3d(5, 5, 0),
                              new Point3d(12, 3, 0));

    // Add the new object to the current space
    acSpace.AppendEntity(acLine);
}
```

The following sample code demonstrates how to add a Layer to the current database; with and without DLR.

```cs
[CommandMethod("ADDLAYER")]
public static void AddLayer()
{
    // Get the current database
    Database acCurDb = HostApplicationServices.WorkingDatabase;

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

            // Create a new layer named "MyLayer"
            using (LayerTableRecord acLyrTblRec = new LayerTableRecord())
            {
                acLyrTblRec.Name = "MyLayer";

                // Assign the ACI color 3 to the new layer
                Color acClr = Color.FromColorIndex(ColorMethod.ByAci, 3);
                acLyrTblRec.Color = acClr;

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

C# with Dynamic Language Runtime (DLR)

```cs
[CommandMethod("ADDLAYER")]
public static void AddLayer()
{
    // Get the current database
    dynamic acCurDb = HostApplicationServices.WorkingDatabase;

    dynamic acLyrTbl = acCurDb.LayerTableId;

    // Check to see if MyLayer exists in the Layer table
    if (acLyrTbl.Has("MyLayer") != true)
    {
        // Create a new layer named "MyLayer"
        dynamic acLyrTblRec = new LayerTableRecord();
        acLyrTblRec.Name = "MyLayer";

        // Assign the ACI color 3 to the new layer
        dynamic acClr = Color.FromColorIndex(ColorMethod.ByAci, 3);
        acLyrTblRec.Color = acClr;

        // Add the new layer table record to the layer table
        acLyrTbl.Add(acLyrTblRec);
    }
}
```

The following demonstrates how to step through and list all the objects in the current space; with and without DLR.

```cs
[CommandMethod("LISTOBJECTS")]
public static void ListObjects()
{
    // Get the current document and database
    Document acDoc = Application.DocumentManager.MdiActiveDocument;
    Database acCurDb = HostApplicationServices.WorkingDatabase;

    using (Transaction acTrans = acCurDb.TransactionManager.StartTransaction())
    {
        // Open the Block table record Model space for write
        BlockTableRecord acSpace;
        acSpace = acTrans.GetObject(acCurDb.CurrentSpaceId,
                                    OpenMode.ForRead) as BlockTableRecord;

        // Step through the current space
        foreach (ObjectId objId in acSpace)
        {
            // Display the class and current layer of the object
            Entity acEnt = (Entity)acTrans.GetObject(objId, OpenMode.ForRead);
            acDoc.Editor.WriteMessage("\nObject Class: " + acEnt.GetRXClass().Name +
                                      "\nCurrent Layer: " + acEnt.Layer + 
                                       "\n");
        }
        acTrans.Commit();
    }
}
```

C# with Dynamic Language Runtime (DLR)

```cs
[CommandMethod("LISTOBJECTS")]
public static void ListObjects()
{
    // Get the current document and database
    dynamic acDoc = Application.DocumentManager.MdiActiveDocument;
    dynamic acCurDb = HostApplicationServices.WorkingDatabase;

    // Create a dynamic reference to model or paper space
    dynamic acSpace = acCurDb.CurrentSpaceId;

    // Step through the current space
    foreach (dynamic acEnt in acSpace)
    {
        // Display the class and current layer of the object
        acDoc.Editor.WriteMessage("\nObject Class: " + acEnt.GetRXClass().Name +
                                  "\nCurrent Layer: " + acEnt.Layer +
                                  "\n");
    }
}
```
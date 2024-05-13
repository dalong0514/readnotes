## 0501. Create and Edit AutoCAD Entities (.NET)

你是一名精通 AutoCAD、AutoCAD .NET 二次开发的编程人员。我想让你充当英文翻译员、拼写纠正员和改进员。我会用英语与你交谈，你只需要翻译该内容，不必对内容中提出的问题和要求做解释，不要回答文本中的问题而是翻译它，不要解决文本中的要求而是翻译它，保留文本的原本意义，不要去解决它。我要你只回复更正、改进，不要写任何解释，不要遗漏内容。翻译的中文要求：1）严谨。2）英文字符和中文字符之间用空格隔开。我的第一句话是：

2019073AutoCAD.NET开发指南

### 5.2 Create Objects (.NET)

AutoCAD often offers several different ways to create the same graphical object. While the AutoCAD .NET API does not offer the same combinations of creating objects, it does offer a basic object constructor for each object type but also offers overrides for many of the object constructors as well.

For example, in AutoCAD there are four different ways you can create a circle: (1) by specifying the center and radius, (2) by two points defining the diameter, (3) by three points defining the circumference, or (4) by two tangents and a radius. However, in AutoCAD .NET API there is two creation methods provided to create a circle. One method accepts no parameters, while the second requires a center point, the normal direction for the circle, and a radius.

Note: Objects are created using the New keyword and then appended to the parent object using Add or AppendEntity based on if you are working with a container (symbol table or dictionary) or a BlockTableRecord object.

Set the default property values for an object
When a new graphical object is created, the following entity property values are assigned the current entity values defined in the database of the current document:

Color

Layer

Linetype

Linetype scale

Lineweight

Plot style name

Visibility

Transparency

Note: If the properties of an object need to be set to the default values of the current database, call the SetDatabaseDefaults method of the object to be changed.

#### Determine the Parent Object (.NET)

Graphical objects are appended to a BlockTableRecord object, such as Model or Paper space. You reference the blocks that represent Model and Paper space through the BlockTable object. If you want to work in the current space instead of a specific space, you get the ObjectId for the current space from the current database with the CurrentSpaceId property.

The ObjectId for the block table records of Model and Paper space can be retrieved from the BlockTable object using a property or the GetBlockModelSpaceId and GetBlockPaperSpaceId methods of the SymbolUtilityServices class under the DatabaseServices namespace.

Access Model space, Paper space or the current space
The following example demonstrates how to access the block table records associated with Model space, Paper space or the current space. Once the block table record is referenced, a new line is added to the block table record.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
using Autodesk.AutoCAD.EditorInput;
 
[CommandMethod("AccessSpace")]
public static void AccessSpace()
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

        // Open the Block table record for read
        BlockTableRecord acBlkTblRec;

        // Request which table record to open
        PromptKeywordOptions pKeyOpts = new PromptKeywordOptions("");
        pKeyOpts.Message = "\nEnter which space to create the line in ";
        pKeyOpts.Keywords.Add("Model");
        pKeyOpts.Keywords.Add("Paper");
        pKeyOpts.Keywords.Add("Current");
        pKeyOpts.AllowNone = false;
        pKeyOpts.AppendKeywordsToMessage = true;

        PromptResult pKeyRes = acDoc.Editor.GetKeywords(pKeyOpts);

        if (pKeyRes.StringResult == "Model")
        {
            // Get the ObjectID for Model space from the Block table
            acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                            OpenMode.ForWrite) as BlockTableRecord;
        }
        else if (pKeyRes.StringResult == "Paper")
        {
            // Get the ObjectID for Paper space from the Block table
            acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.PaperSpace],
                                            OpenMode.ForWrite) as BlockTableRecord;
        }
        else
        {
            // Get the ObjectID for the current space from the database
            acBlkTblRec = acTrans.GetObject(acCurDb.CurrentSpaceId,
                                            OpenMode.ForWrite) as BlockTableRecord;
        }

        // Create a line that starts at 2,5 and ends at 10,7
        using (Line acLine = new Line(new Point3d(2, 5, 0),
                                new Point3d(10, 7, 0)))
        {
            // Add the new object to the block table record and the transaction
            acBlkTblRec.AppendEntity(acLine);
            acTrans.AddNewlyCreatedDBObject(acLine, true);
        }

        // Save the new line to the database
        acTrans.Commit();
    }
}
```

#### Create Lines (.NET)

The line is the most basic object in AutoCAD. You can create a variety of lines—single lines, and multiple line segments with and without arcs. In general, you draw lines by specifying coordinate points. Lines when created, inherit the current settings from the drawing database, such as layer, linetype and color.

To create a line, you create a new instance of one of the following objects:

Line

Creates a line.

Polyline

Creates a 2D lightweight polyline.

MLine

Creates a multiline.

Polyline2D

Creates a 2D polyline.

Polyline3D

Creates a 3D polyline.

Note: Polyline2D objects are the legacy polyline objects that were in AutoCAD prior to Release 14, and the Polyline object represents the new optimized polyline that was introduced with AutoCAD Release 14.

Create a Line Object (.NET)

This example adds a line that starts at (5,5,0) and ends at (12,3,0) to Model space.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("AddLine")]
public static void AddLine()
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

Create a Polyline Object (.NET)

This example adds a lightweight polyline with two straight segments using the 2D coordinates (2,4), (4,2), and (6,4) to Model space.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("AddLightweightPolyline")]
public static void AddLightweightPolyline()
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

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForWrite) as BlockTableRecord;

        // Create a polyline with two segments (3 points)
        using (Polyline acPoly = new Polyline())
        {
            acPoly.AddVertexAt(0, new Point2d(2, 4), 0, 0, 0);
            acPoly.AddVertexAt(1, new Point2d(4, 2), 0, 0, 0);
            acPoly.AddVertexAt(2, new Point2d(6, 4), 0, 0, 0);

            // Add the new object to the block table record and the transaction
            acBlkTblRec.AppendEntity(acPoly);
            acTrans.AddNewlyCreatedDBObject(acPoly, true);
        }

        // Save the new object to the database
        acTrans.Commit();
    }
}
```

#### Create Curved Objects (.NET)

You can create a variety of curved objects with AutoCAD, including splines, helixes, circles, arcs, and ellipses. All curves are created on the XY plane of the current UCS.

To create a curve, you create a new instance of one of the following objects:

Arc

Creates an arc given the center point, radius, start and end angles.

Circle

Creates a circle given the center point and radius.

Ellipse

Creates an ellipse given the center point, a point on the major axis, and the radius ratio.

Spline

Creates a quadratic or cubic NURBS (nonuniform rational B-spline) curve.

Helix

Creates a 2D or 3D helix object.

Create a Circle Object (.NET)

This example creates a circle in Model space with a center point of (2,3,0) and a radius of 4.25.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("AddCircle")]
public static void AddCircle()
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

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForWrite) as BlockTableRecord;

        // Create a circle that is at 2,3 with a radius of 4.25
        using (Circle acCirc = new Circle())
        {
            acCirc.Center = new Point3d(2, 3, 0);
            acCirc.Radius = 4.25;

            // Add the new object to the block table record and the transaction
            acBlkTblRec.AppendEntity(acCirc);
            acTrans.AddNewlyCreatedDBObject(acCirc, true);
        }

        // Save the new object to the database
        acTrans.Commit();
    }
}
```

Create an Arc Object (.NET)

This example creates an arc in Model space with a center point of (6.25,9.125,0), a radius of 6, start angle of 1.117 (64 degrees), and an end angle of 3.5605 (204 degrees).

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("AddArc")]
public static void AddArc()
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

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForWrite) as BlockTableRecord;

        // Create an arc that is at 6.25,9.125 with a radius of 6, and
        // starts at 64 degrees and ends at 204 degrees
        using (Arc acArc = new Arc(new Point3d(6.25, 9.125, 0),
                            6, 1.117, 3.5605))
        {

            // Add the new object to the block table record and the transaction
            acBlkTblRec.AppendEntity(acArc);
            acTrans.AddNewlyCreatedDBObject(acArc, true);
        }

        // Save the new line to the database
        acTrans.Commit();
    }
}
```

Create a Spline Object (.NET)

This example creates a circle in Model space using three points (0, 0, 0), (5, 5, 0), and (10, 0, 0). The spline has start and end tangents of (0.5, 0.5, 0.0).

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("AddSpline")]
public static void AddSpline()
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

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForWrite) as BlockTableRecord;

        // Define the fit points for the spline
        Point3dCollection ptColl = new Point3dCollection();
        ptColl.Add(new Point3d(0, 0, 0));
        ptColl.Add(new Point3d(5, 5, 0));
        ptColl.Add(new Point3d(10, 0, 0));

        // Get a 3D vector from the point (0.5,0.5,0)
        Vector3d vecTan = new Point3d(0.5, 0.5, 0).GetAsVector();

        // Create a spline through (0, 0, 0), (5, 5, 0), and (10, 0, 0) with a
        // start and end tangency of (0.5, 0.5, 0.0)
        using (Spline acSpline = new Spline(ptColl, vecTan, vecTan, 4, 0.0))
        {
            // Add the new object to the block table record and the transaction
            acBlkTblRec.AppendEntity(acSpline);
            acTrans.AddNewlyCreatedDBObject(acSpline, true);
        }

        // Save the new line to the database
        acTrans.Commit();
    }
}
```

#### Create Point Objects (.NET)

Point objects can be useful, for example, as node or reference points that you can snap to and offset objects from. You can set the style of the point and its size relative to the screen or in absolute units.

The Pdmode and Pdsize properties of the Database object control the appearance of Point objects. A value of 0, 2, 3, and 4 for Pdmode specify a figure to draw through the point. A value of 1 selects nothing to be displayed.

Adding 32, 64, or 96 to the previous value selects a shape to draw around the point in addition to the figure drawn through it:

Pdsize controls the size of the point figures, except for when Pdmode is 0 and 1. A 0 setting generates the point at 5 percent of the graphics area height. Setting Pdsize to a positive value specifies an absolute size for the point figures. A negative value is interpreted as a percentage of the viewport size. The size of all points is recalculated when the drawing is regenerated.

After you change Pdmode and Pdsize, the appearance of existing points changes the next time the drawing is regenerated.

Create a Point object and change its appearance

The following example creates a Point object in Model space at the coordinate (5, 5, 0). The Pdmode and Pdsize properties are then updated.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("AddPointAndSetPointStyle")]
public static void AddPointAndSetPointStyle()
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

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForWrite) as BlockTableRecord;

        // Create a point at (4, 3, 0) in Model space
        using (DBPoint acPoint = new DBPoint(new Point3d(4, 3, 0)))
        {
            // Add the new object to the block table record and the transaction
            acBlkTblRec.AppendEntity(acPoint);
            acTrans.AddNewlyCreatedDBObject(acPoint, true);
        }

        // Set the style for all point objects in the drawing
        acCurDb.Pdmode = 34;
        acCurDb.Pdsize = 1;

        // Save the new object to the database
        acTrans.Commit();
    }
}
```

#### Create Solid-Filled Areas (.NET)

You can create triangular and quadrilateral areas filled with a color. When creating filled areas, set the FILLMODE system variable to off to improve performance and back on once the fills have been created.

When you create a quadrilateral solid-filled area, the sequence of the third and fourth points determines its shape. Compare the following illustrations:


The first two points define one edge of the polygon. The third point is defined diagonally opposite from the second. If the fourth point is set equal to the third point, then a filled triangle is created.

Create a solid-filled object

The following example creates a quadrilateral solid (bow-tie) in Model space using the coordinates (0, 0, 0), (5, 0, 0), (5, 8, 0), and (0, 8, 0). It also creates a quadrilateral solid in a rectangular shape using the coordinates (10, 0, 0), (15, 0, 0), (10, 8, 0), and (15, 8, 0).

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("Add2DSolid")]
public static void Add2DSolid()
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

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForWrite) as BlockTableRecord;

        // Create a quadrilateral (bow-tie) solid in Model space
        using (Solid ac2DSolidBow = new Solid(new Point3d(0, 0, 0),
                                        new Point3d(5, 0, 0),
                                        new Point3d(5, 8, 0),
                                        new Point3d(0, 8, 0)))
        {
            // Add the new object to the block table record and the transaction
            acBlkTblRec.AppendEntity(ac2DSolidBow);
            acTrans.AddNewlyCreatedDBObject(ac2DSolidBow, true);
        }

        // Create a quadrilateral (square) solid in Model space
        using (Solid ac2DSolidSqr = new Solid(new Point3d(10, 0, 0),
                                        new Point3d(15, 0, 0),
                                        new Point3d(10, 8, 0),
                                        new Point3d(15, 8, 0)))
        {
            // Add the new object to the block table record and the transaction
            acBlkTblRec.AppendEntity(ac2DSolidSqr);
            acTrans.AddNewlyCreatedDBObject(ac2DSolidSqr, true);
        }

        // Save the new object to the database
        acTrans.Commit();
    }
}
```

#### Work With Regions (.NET)

Regions are two-dimensional enclosed areas you create from closed shapes called loops. A loop is a closed boundary that is made up of straight and curved objects which do not intersect themselves. Loops can be combinations of lines, lightweight polylines, 2D and 3D polylines, circles, arcs, ellipses, elliptical arcs, splines, 3D faces, traces, and solids.

The objects that make up the loops must either be closed or form closed areas by sharing endpoints with other objects. They must also be coplanar (on the same plane). The loops that make up a region must be defined as an array of objects.

Create Regions (.NET)

Regions are added to a BlockTableRecord object by creating an instance of a Region object and then appending it to a BlockTableRecord. Before you can add it to a BlockTableRecord object, a region needs to be calculated based on the objects that form the closed loop. The CreateFromCurves function creates a region out of every closed loop formed by the input array of objects. The CreateFromCurves method returns and requires a DBObjectCollection object.

AutoCAD converts closed 2D and planar 3D polylines to separate regions, then converts polylines, lines, and curves that form closed planar loops. If more than two curves share an endpoint, the resulting region might be arbitrary. Because of this, several regions may actually be created with the CreateFromCurves method. You need to append each region created to a BlockTableRecord object.

Create a simple region

The following example creates a region from a single circle.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("AddRegion")]
public static void AddRegion()
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

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForWrite) as BlockTableRecord;

        // Create an in memory circle
        using (Circle acCirc = new Circle())
        {
            acCirc.Center = new Point3d(2, 2, 0);
            acCirc.Radius = 5;

            // Adds the circle to an object array
            DBObjectCollection acDBObjColl = new DBObjectCollection();
            acDBObjColl.Add(acCirc);

            // Calculate the regions based on each closed loop
            DBObjectCollection myRegionColl = new DBObjectCollection();
            myRegionColl = Region.CreateFromCurves(acDBObjColl);
            Region acRegion = myRegionColl[0] as Region;

            // Add the new object to the block table record and the transaction
            acBlkTblRec.AppendEntity(acRegion);
            acTrans.AddNewlyCreatedDBObject(acRegion, true);

            // Dispose of the in memory circle not appended to the database
        }

        // Save the new object to the database
        acTrans.Commit();
    }
}
```

Create Composite Regions (.NET)

You can create composite regions by subtracting, combining, or finding the intersection of regions or 3D solids. You can then extrude or revolve composite regions to create complex solids. To create a composite region, use the BooleanOperation method.

Subtract regions

When you subtract one region from another, you call the BooleanOperation method from the first region. This is the region from which you want to subtract. For example, to calculate how much carpeting is needed for a floor plan, call the BooleanOperation method from the outer boundary of the floor space and use the non-carpeted areas, such as pillars and counters, as the object in the Boolean parameter list.

Unite regions

To unite regions, call the BooleanOperation method and use the constant BooleanOperationType.BoolUnite for the operation instead of BooleanOperationType.BoolSubtract. You can combine regions in any order to unite them.

Find the intersection of two regions

To find the intersection of two regions, use the constant BooleanOperationType.BoolIntersect. You can combine regions in any order to intersect them.

Create a composite region

The following example creates two regions from two circles and then subtracts the smaller region from the large one to create a wheel.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("CreateCompositeRegions")]
public static void CreateCompositeRegions()
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

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForWrite) as BlockTableRecord;

        // Create two in memory circles
        using (Circle acCirc1 = new Circle())
        {
            acCirc1.Center = new Point3d(4, 4, 0);
            acCirc1.Radius = 2;

            using (Circle acCirc2 = new Circle())
            {
                acCirc2.Center = new Point3d(4, 4, 0);
                acCirc2.Radius = 1;

                // Adds the circle to an object array
                DBObjectCollection acDBObjColl = new DBObjectCollection();
                acDBObjColl.Add(acCirc1);
                acDBObjColl.Add(acCirc2);

                // Calculate the regions based on each closed loop
                DBObjectCollection myRegionColl = new DBObjectCollection();
                myRegionColl = Region.CreateFromCurves(acDBObjColl);
                Region acRegion1 = myRegionColl[0] as Region;
                Region acRegion2 = myRegionColl[1] as Region;

                // Subtract region 1 from region 2
                if (acRegion1.Area > acRegion2.Area)
                {
                    // Subtract the smaller region from the larger one
                    acRegion1.BooleanOperation(BooleanOperationType.BoolSubtract, acRegion2);
                    acRegion2.Dispose();

                    // Add the final region to the database
                    acBlkTblRec.AppendEntity(acRegion1);
                    acTrans.AddNewlyCreatedDBObject(acRegion1, true);
                }
                else
                {
                    // Subtract the smaller region from the larger one
                    acRegion2.BooleanOperation(BooleanOperationType.BoolSubtract, acRegion1);
                    acRegion1.Dispose();

                    // Add the final region to the database
                    acBlkTblRec.AppendEntity(acRegion2);
                    acTrans.AddNewlyCreatedDBObject(acRegion2, true);
                }

                // Dispose of the in memory objects not appended to the database
            }
        }

        // Save the new object to the database
        acTrans.Commit();
    }
}
```

##### Create Hatches (.NET)

Closed boundaries can be filled with a pattern.

When creating hatch, you do not initially specify the area to be filled. First you must create the Hatch object. Once this is done, you can specify the outer loop, which is the outermost boundary for the hatch. You can then continue to specify any inner loops that may exist in the hatch.

Create a Hatch Object (.NET)

When creating a Hatch object, you specify the hatch pattern type, the hatch pattern name, and the associativity. Once a Hatch object has been created, you will not be able to change the hatch associativity.

To create a Hatch object, you create a new instance of the object and then use the AppendEntity method to add it to a BlockTableRecord object.

Associate a Hatch (.NET)

You can create associative or nonassociative hatches. Associative hatches are linked to their boundaries and updated when the boundaries are modified. Nonassociative hatches are independent of their boundaries.

To make a hatch associative, set the Associative property of the hatch object created to TRUE. To make a hatch nonassociative, set the Associative property to FALSE.

Associativity for hatch must be set before appending the hatch loop. If a hatch object is nonassociative, you can make it associative again by setting the Associative property to TRUE and re-appending the hatch loop.

Assign the Hatch Pattern Type and Name (.NET)
AutoCAD supplies a solid-fill and more than fifty industry-standard hatch patterns. Hatch patterns highlight a particular feature or area of a drawing. For example, patterns can help differentiate the components of a 3D object or represent the materials that make up an object.

You can use a pattern supplied with AutoCAD or one from an external pattern library.

To specify a unique pattern, you must specify both a pattern type and name for the Hatch object. The pattern type specifies where to look up the pattern name. When entering the pattern type, use one of the following constants:

HatchPatternType.PreDefined

Selects the pattern name from those defined in the acad.pat or acadiso.pat files.

HatchPatternType.UserDefined

Defines a pattern of lines using the current linetype.

HatchPatternType.CustomDefined

Selects the pattern name from a PAT other than the acad.pat or acadiso.pat files.

When entering the pattern name, use a name that is valid for the file specified by the pattern type.

Define the Hatch Boundaries (.NET)

Once the Hatch object is created, the hatch boundaries can be added. Boundaries can be any combination of lines, arcs, circles, 2D polylines, ellipses, splines, and regions.

The first boundary added must be the outer boundary, which defines the outermost limits to be filled by the hatch. To add the outer boundary, use the AppendLoop method with the HatchLoopTypes.Outermost constant for the type of loop to append.

Once the outer boundary is defined, you can continue adding additional boundaries. Add inner boundaries using the AppendLoop method with the HatchLoopTypes.Default constant.

Inner boundaries define islands within the hatch. How these islands are handled by the Hatch object depends on the setting of the HatchStyle property. The HatchStyle property can be set to one of the following conditions:

When you have finished defining the hatch it must be evaluated before it can be displayed. Use the EvaluateHatch method to do this.

Create a Hatch object

The following example creates an associated hatch in Model space. Once the hatch has been created, you can change the size of the circle that the hatch is associated with. The hatch will change to match the size of the circle.

```cs
using Autodesk.AutoCAD.Runtime;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.Geometry;
 
[CommandMethod("AddHatch")]
public static void AddHatch()
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

        // Open the Block table record Model space for write
        BlockTableRecord acBlkTblRec;
        acBlkTblRec = acTrans.GetObject(acBlkTbl[BlockTableRecord.ModelSpace],
                                        OpenMode.ForWrite) as BlockTableRecord;

        // Create a circle object for the closed boundary to hatch
        using (Circle acCirc = new Circle())
        {
            acCirc.Center = new Point3d(3, 3, 0);
            acCirc.Radius = 1;

            // Add the new circle object to the block table record and the transaction
            acBlkTblRec.AppendEntity(acCirc);
            acTrans.AddNewlyCreatedDBObject(acCirc, true);

            // Adds the circle to an object id array
            ObjectIdCollection acObjIdColl = new ObjectIdCollection();
            acObjIdColl.Add(acCirc.ObjectId);

            // Create the hatch object and append it to the block table record
            using (Hatch acHatch = new Hatch())
            {
                acBlkTblRec.AppendEntity(acHatch);
                acTrans.AddNewlyCreatedDBObject(acHatch, true);

                // Set the properties of the hatch object
                // Associative must be set after the hatch object is appended to the 
                // block table record and before AppendLoop
                acHatch.SetHatchPattern(HatchPatternType.PreDefined, "ANSI31");
                acHatch.Associative = true;
                acHatch.AppendLoop(HatchLoopTypes.Outermost, acObjIdColl);
                acHatch.EvaluateHatch(true);
            }
        }

        // Save the new object to the database
        acTrans.Commit();
    }
}
```
# Chapter 30 Working with Blocks and External References

Most designs created with the AutoCAD® program start off with simple geometric objects, such as lines, circles, and arcs. The geometric objects are used to represent holes, bolts, motors, and even the outside of a building. As a design grows in complexity, elements often are repeated many times. For example, you might use several lines and circles to represent a bolt head or a desk with a grommet.

AutoCAD allows you to reuse geometry by creating what is known as a block. A block is a named grouping of objects that can be inserted in a drawing multiple times. Each insertion creates a block reference that displays the objects stored in the block at the insertion point. If the block is changed, each block reference based on that block is updated.

Blocks aren't the only method for reusing geometry or other data in a drawing. A drawing file can also include external references (xrefs) to geometry stored in another drawing file. External references can include blocks, raster images, and other documents. When you reference another document, such as a PDF or DWF file, it is known as an underlay. In this chapter, I explain how to use VBA to work with blocks and external referenced files.

Managing Block Definitions

Blocks make it possible to logically group basic geometry together with a unique name and then create instances of that geometry within a drawing. Blocks are implemented as two separate objects: block definitions and block references. Block definitions are nongraphical objects that are stored in the AcadBlocks collection object. Each block definition is represented by an AcadBlock object, which contains the geometry and attribute definitions that define how the block should appear and behave when it is inserted into the drawing area. A block definition can contain either static or dynamic properties.

Figure 30.1 shows the relationship between a block definition and a block reference and how the attributes of the block are used to bring the geometry into model space.

Figure 30.1 Block-definition-to-block-reference relationship

You can think of a block definition much like a cookie recipe. The recipe lists the ingredients (which determines how the cookie should taste) and provides instructions for combining those ingredients and baking the dough. What the recipe doesn't control is how much dough is placed on any particular spot on the cookie sheet before baking. The exact placement and amount of the cookie dough on the tray is determined by the baker. Similarly, an end user uses a block reference in a drawing to determine the exact placement, size, and number of geometries to be displayed. I explain how to insert and work with block references in the「Inserting and Working with Block References」section later in this chapter.

Creating a Block Definition

A new block definition can be added to a drawing using the Add function of the AcadBlocks collection object. The Add function expects two argument values and returns an AcadBlock object. Before adding a new block definition, you should use the Item method with an error handler to check to see if a block definition with the specific name you want to use already exists in the drawing. The Item method can also be used to get a specific block definition in the AcadBlocks collection object and, as with other collections, a For statement can be used to step through the block definitions in a drawing.

The following shows the syntax of the Add function:

retVal = object.Add(origin, blockName)

Its arguments are as follows:

retVal The retVal argument represents the new AcadBlock collection object returned by the Add function.

object The object argument specifies the AcadBlocks collection object that is used to add a new block definition.

origin The origin argument is an array of three doubles that defines the origin of the new block definition; think insertion point for the block reference.

blockName The blockName argument is a string that specifies the unique name to be assigned to the new block definition.

The following code statements add a new block definition named RoomNum:

' Defines the origin of the block Dim dOrigin(2) As Double dOrigin(0) = 5: dOrigin(1) = 2.5: dOrigin(2) = 0 Dim oBlkDef As AcadBlock Set oBlkDef = ThisDrawing.Blocks.Add(dOrigin, "RoomNum")

Here is an example that checks for the existence of a block definition named RoomNum:

On Error Resume Next Dim oBlkDef As AcadBlock Set oBlkDef = ThisDrawing.Blocks("RoomNum") If Err Then MsgBox "Block definition doesn't exist." Else MsgBox "Block definition exists." End If

After an AcadBlock object has been obtained using the Item or Add method of the AcadBlocks collection object, you can step through the objects of the block using a For statement or the Item method of the AcadBlock object. You can use the same functions to add new objects to a block definition as you would to add objects to model space or paper space. I explained how to add objects to and step through the objects of model space in Chapter 27,「Creating and Modifying Drawing Objects.」

The following code statements add a closed lightweight polyline to the block definition named RoomNum:

On Error Resume Next ' Gets the RoomNum block definition Dim oBlkDef As AcadBlock Set oBlkDef = ThisDrawing.Blocks("RoomNum") ' If the block doesn't exist, an error is generated If Err Then ' Defines the origin of the block Dim dOrigin(2) As Double dOrigin(0) = 5: dOrigin(1) = 2.5: dOrigin(2) = 0 ' Adds the block definition Set oBlkDef = ThisDrawing.Blocks.Add(dOrigin, "RoomNum") ' Defines the vertex points for the ' lightweight polyline Dim dPts(7) As Double dPts(0) = 0: dPts(1) = 0 dPts(2) = 10: dPts(3) = 0 dPts(4) = 10: dPts(5) = 5 dPts(6) = 0: dPts(7) = 5 ' Adds a new lightweight polyline to the block Dim oLWPoly As AcadLWPolyline Set oLWPoly = oBlkDef.AddLightWeightPolyline(dPts) ' Closes the lightweight polyline oLWPoly.Closed = True ' Sets the layer of the lightweight polyline to 0 oLWPoly.Layer = "0" End If

NOTE

I recommend placing objects in a block definition on layer 0 when the object should inherit its properties from the layer that the block reference is inserted onto. The appearance of objects in a block definition can be controlled ByBlock or ByLayer when you insert a block definition as a block reference. For information on the ByBlock and ByLayer values, see the AutoCAD Help system.

When a block definition is no longer needed, it can be removed from the drawing using the Delete method of an AcadBlock object. A block definition can't be deleted if a block reference associated with the block definition is inserted into the drawing.

NOTE

Dynamic blocks—block definitions with dynamic properties—can't be created with the AutoCAD Object library. However, you can modify the dynamic properties of a block reference using the AutoCAD Object library. I explain how to work with blocks that contain dynamic properties in the「Working with Dynamic Properties」section later in this chapter.

Adding Attribute Definitions

A block definition can contain what is known as an attribute. An attribute is similar to a text object, except its value can be changed after a block reference has been inserted into a drawing. Attributes allow you to store string values and then extract their values later. There are two types of attributes that are part of the block creation and insertion process: attribute definitions and attribute references. Attribute definitions can be added to a block definition, and attribute references are part of each block reference inserted into a drawing that is associated with a block definition that has one or more attribute definitions.

The AddAttribute function is used to add an attribute definition to a block definition and returns an AcadAttribute object. The following shows the syntax of the AddAttribute function:

retVal = object.AddAttribute(height, mode, prompt, insertionPoint, tag, value)

Its arguments are as follows:

retVal The retVal argument represents the new AcadAttribute object returned by the AddAttribute function.

object The object argument specifies the AcadBlock object to add the attribute definition.

height The height argument is a double that represents the height of the attribute.

mode The mode argument is an integer that represents the behavior of the attribute reference added to a block reference when the block is inserted into the drawing. Instead of using an integer value, I recommend that you use the constant values of the AcAttributeMode enumerator. Table 30.1 lists each of the constant values of the AcAttributeMode enumerator. You can specify more than one constant by separating each constant with a plus symbol, such as acAttributeModeInvisible + acAttributeModeNormal.

prompt The prompt argument is a string that represents the text that provides a hint for the value that's expected when the block reference is inserted.

insertionPoint The insertionPoint argument is an array of three doubles that defines the insertion point of the attribute definition.

tag The tag argument is a string that represents the text that's displayed in the drawing if the block reference is exploded after being inserted and the value used to extract the attribute's value from a block reference. A tag cannot contain spaces.

value The value argument is a string that represents the default value of the attribute when the block reference is inserted.

Table 30.1 Constant values of the AcAttributeMode enumerator

Constant Description

acAttributeModeConstant Indicates the value of the attribute can't be changed.

acAttributeModeInvisible Attribute is marked as invisible. The attmode system variable controls the display of all invisible attributes.

acAttributeModeLockPosition Position of the attribute can't be adjusted using grip editing.

acAttributeModeMultipleLine Attribute supports multiple lines of text instead of the standard single line of text.

acAttributeModeNormal Default display behavior of the attribute is maintained when the block is inserted using the insert command.

acAttributeModePreset Value of the attribute is preset. When the block is inserted using the insert command, the user isn't prompted to enter a value for the attribute.

acAttributeModeVerify User is prompted to verify the value they provide for the attribute when inserting the block reference with the insert command.

Table 30.1 lists the constant values of the AcAttributeMode enumerator that can be passed to the mode argument of the AddAttribute function or assigned to the Mode property of an AcadAttribute object.

The following code statements add an attribute definition to the block definition assigned to the oBlkDef variable:

' Defines the insertion point of the attribute definition Dim dInsPt(2) As Double dInsPt(0) = 5: dInsPt(1) = 2.5: dInsPt(2) = 0 ' Adds the attribute definition to the block Dim oAttDef As AcadAttribute Set oAttDef = oBlkDef.AddAttribute(2.5, acAttributeModeNormal, _ "Room#", dInsPt, "Room#", "101") ' Sets the alignment for the attribute's text oAttDef.Alignment = acAlignmentMiddleCenter oAttDef.TextAlignmentPoint = dInsPt

After adding an attribute definition to a block definition, you can modify its appearance and behavior using the properties and methods of the AcadAttribute object. The properties and methods of an AcadAttribute object are similar to those of an AcadText object. I discussed the AcadText object in Chapter 29,「Annotating Objects.」

Table 30.2 lists the properties of the AcadAttribute object that are unique to the object and are different from those of an AcadText object.

NOTE

If you change the MTextAttributeContent, MTextBoundaryWidth, or MTextDrawingDirection property, you must execute the UpdateMTextAttribute method of the AcadAttribute object. The UpdateMTextAttribute method updates the display of the multiline attribute in the drawing.

Table 30.2 Properties related to an AcadAttribute object

Property Description

Constant Returns True if the attribute is set to the constant mode.

Invisible Returns True if the attribute should be invisible when the block reference is inserted.

LockPosition Returns True if the attribute can't be modified using grip editing when the block reference is inserted.

MTextAttribute Returns True if the attribute should be multiline instead of single-line text.

MTextAttributeContent Specifies the content for the multiline text when the MTextAttribute property is True.

MTextBoundaryWidth Specifies the width of the multiline text when the MTextAttribute property is True.

MTextDrawingDirection Specifies the direction in which the text should be drawn when the MTextAttribute property is True.

Preset Returns True if the user shouldn't be prompted to enter a value for the attribute when the block is inserted.

PromptString Specifies the prompt string that is displayed for the attribute when the block is inserted.

TagString Specifies the tag for the attribute that is displayed in the drawing if the block reference is exploded after being inserted. The tag can also be useful when trying to identify which attribute's value to extract when generating a BOM.

TextString Specifies the default text for the attribute to use when the block is inserted.

Verify Returns True if the user should be prompted to verify the value of the attribute when the block is inserted.

Modifying and Redefining a Block Definition

You can add new objects or modify existing objects of a block definition, much like you can in model space or paper space. The Item method of the AcadBlock object can be used to get a specific object or a For statement to step through all objects in a block definition.

In addition to modifying the objects in a block definition, the origin—the insertion point of a block—can be modified using the Origin property. The Origin property of an AcadBlock object allows you to get or set the origin for the block definition. The origin of a block definition is defined as a double array with three elements.

Besides modifying the objects and origin of a block, you can specify whether a block reference created from a block can be exploded, set the units that control the scaling of a block, and make other changes. Table 30.3 lists the properties that control the behavior of and provide information about an AcadBlock object.

Table 30.3 Properties related to an AcadBlock object

Property Description

BlockScaling Specifies if the block can only be scaled uniformly (acUniform) or the block can be assigned a different scale factor for each axis (acAny).

Comments Specifies a string that describes the block definition.

Count Returns an integer value that contains the number of block references that have been inserted into the drawing based on the block definition.

Explodable Returns True if the block reference inserted into the drawing can be exploded.

Name Specifies a string that contains the name of the block definition.

Units Specifies the units of measurement for the block. A constant value from the AcInsertUnits enumerator is returned by or can be assigned to this property. See the Object Browser in the VBA Editor for a list of possible values. The units specified affect the insertion scale of the block.

After a block definition has been updated, you should use the Regen method of the AcadApplication object to regenerate the display of the drawing. You can also update the display of an individual block reference using the Update method. I explained the Regen and Update methods in Chapter 27. If you add or remove an AcadAttribute object in a block definition, the block references inserted into model space or paper space aren't updated to reflect the change unless the attribute being changed is defined as a constant.

To reflect the changes in the attributes between a block definition and the block references inserted into a drawing, you will need to do the following:

Insert a new block reference into the drawing.

Update the attribute values of the new block reference with those from the existing block reference.

Remove the old block reference.

I discuss more about working with block references in the「Inserting and Working with Block References」section later in this chapter.

Determining the Type of Block Definition

Block definitions stored in the AcadBlocks collection object of a drawing aren't only used to insert block references. Model space and paper space are also block definitions with special names along with external references (xrefs) and layouts. You can determine a block definition's type using the properties in Table 30.4. I discuss xrefs in the「Working with Xrefs」section later in this chapter and layouts in Chapter 31,「Outputting Drawings.」

Table 30.4 Properties used to determine a block definition's type

Property Description

IsDynamicBlock Returns True if the block definition contains dynamic properties.

IsLayout Returns True if the block definition is for a layout. You can use the Layout property of an AcadBlock, AcadModelSpace, or AcadPaperSpace object to get the object's associated AcadLayout object.

IsXref Returns True if the block definition is for an external reference.

Inserting and Working with Block References

A block reference is an instance—not a copy—of the geometry from a block definition; the geometry only exists as part of the block definition, with the exception of attributes. Attribute definitions that are part of a block definition are added to a block reference as attribute references unless the attribute definition is defined as a constant attribute. Constant attributes are part of the geometry that is inherited from a block definition and are not part of the block reference.

Inserting a Block Reference

The InsertBlock function is used to insert a reference of a block definition in model space, paper space, or another block definition and expects seven argument values that define the block definition you want to insert, as well as the placement and size of the block reference. After a block reference has been inserted, an AcadBlockReference object is returned.

The following shows the syntax of the InsertBlock function:

retVal = object.InsertBlock(insertionPoint, blockName, xScale, yScale, zScale, rotation [, password])

Its arguments are as follows:

retVal The retVal argument represents the new AcadBlockReference object returned by the InsertBlock function.

object The object argument specifies the AcadBlock, AcadModelSpace, or AcadPaperSpace object where the block reference is to be inserted.

insertionPoint The insertionPoint argument is an array of doubles that represents the insertion point of the block reference.

blockName If you wish to insert the reference into a block definition, use the blockName argument (a string) to specify the name of that block definition. The block must already be defined in the drawing before the insertion can be executed. If you wish to insert a DWG file as a reference into a drawing, specify the full path of a DWG file. When a DWG file is specified, an AcadBlock object based on the objects in model space of the DWG file specified is created, and then the block reference is inserted.

NOTE

An error is generated if the block definition being inserted doesn't already exist in the drawing. You can catch the error and use the Add method to create the block definition or specify a DWG file to insert that might contain the objects for the block you want to use.

For example, the following inserts a block named grid.dwg from the location c:\symbols:

Set oBlkRef = ThisDrawing.ModelSpace.InsertBlock( _ insPt, "c:\symbols\grid.dwg", 1, 1, 1, 0)

xScale, yScale, and zScale The xScale, yScale, and zScale arguments are doubles that represent the scale factors of the block reference.

rotation The rotation argument is a double that represents the rotation angle of the block reference. The rotation angle must be expressed in radians.

password The password argument is an optional string that represents the password assigned to restrict the drawing file from being opened or inserted into by unapproved users. This argument is only required if you are inserting a block based on a DWG file that is password protected.

The following code statements insert a block reference based on a block named RoomNum at 15,27. (Remember, the block you name in code like this must already be defined in your drawing before the code can be executed. Be sure to use an error handler to add the block if it doesn't exist.)

' Defines the insertion point Dim insPt(2) As Double insPt(0) = 15: insPt(1) = 27: insPt(2) = 0 ' Defines the name of the block Dim blkName As String blkName = "RoomNum" ' Inserts the block reference Dim oBlkRef As AcadBlockReference Set oBlkRef = ThisDrawing.ModelSpace.InsertBlock( _ insPt, blkName, 1, 1, 1, 0)

Modifying a Block Reference

Once a block reference, an AcadBlockReference object, is inserted into a drawing, you can modify it using the methods and properties inherited from the AcadEntity object and those specific to the AcadBlockReference object. I explained how to use the methods and properties of the AcadEntity object in Chapter 27. Table 30.5 lists the properties that are used to change the placement, rotation, and scale of a block reference.

Table 30.5 Properties used to affect a block reference

Property Description

InsertionPoint Specifies the insertion point of the block reference in the drawing and is an array of doubles

InsUnits Returns a string that represents the insertion units saved with the block

InsUnitsFactor Returns the insertion factor that is based on the insertion units of the block and those of the drawing

Rotation Specifies the rotation of the block reference

XEffectiveScaleFactor Specifies the effective scale factor along the X-axis for the block reference

XScaleFactor Specifies the scale factor along the X-axis for the block reference

YEffectiveScaleFactor Specifies the effective scale factor along the Y-axis for the block reference

YScaleFactor Specifies the scale factor along the Y-axis for the block reference

ZEffectiveScaleFactor Specifies the effective scale factor along the Z-axis for the block reference

ZScaleFactor Specifies the scale factor along the Z-axis for the block reference

Block references also support the ability to be exploded. The Explode method is used to explode a block reference and it returns an array of the objects added to the drawing as a result of exploding the block reference. The objects in the array are copies of the objects from the block definition associated with the block reference. When the Explode method is executed, the block reference isn't removed from the drawing. You must decide what to do with the block reference. Typically, the block reference is removed using the Delete method, while the objects from the Explode method are kept.

The following code statements explode the first block reference located in model space and then list the block definition name and the objects that make up the block definition:

Sub ExplodeFirstBlkRef() Dim oBlkRef As AcadBlockReference Dim oObj As Object ' Step through model space For Each oObj In ThisDrawing.ModelSpace ' If a block reference is found, explode it If TypeOf oObj Is AcadBlockReference Then Set oBlkRef = oObj ' Explode the block reference Dim vObjArray As Variant vObjArray = oBlkRef.Explode ' List the objects that were added ThisDrawing.Utility.Prompt vbLf & "Block exploded: " & _ oBlkRef.Name & vbLf ThisDrawing.Utility.Prompt vbLf & "Objects added: " & _ vbLf ' Remove the block reference oBlkRef.Delete Dim oAcadObj As AcadObject Dim oObjFromBlkRef As Variant For Each oObjFromBlkRef In vObjArray Set oAcadObj = oObjFromBlkRef ThisDrawing.Utility.Prompt " " & oAcadObj.ObjectName & _ vbLf Next oObjFromBlkRef ' Exit the For statement since we are interested ' in the first block reference only Exit For End If Next oObj End Sub

Here is an example of the output from the previous example code:

Block exploded: 2x4x8 Objects added: AcDbPolyline AcDbLine AcDbLine

Accessing the Attributes of a Block

When a block reference is first inserted into a drawing, the default values of all attributes are used. The value of each nonconstant attribute of a block reference can be changed. Before you access the attributes of a block reference, you should make sure the block reference has attributes. The HasAttributes property of an AcadBlockReference object returns True if a block reference has attributes, either constant or nonconstant.

The GetAttributes and GetConstantAttributes functions of an AcadBlockReference object are used to access the attributes of a block reference. Neither function accepts any arguments. The GetAttributes function returns an array of AcadAttributeReference objects that aren't defined as constant attributes attached to a block reference, whereas the GetConstantAttributes function returns an array of AcadAttribute objects.

Listing 30.1 is a custom procedure that demonstrates how to get both the attributes and constant attributes attached to a block reference.

Listing 30.1: Lists attribute tags and values of a block reference

Sub ListBlockAtts() ' Prompt the user to select a block reference Dim oObj As Object Dim vPtPicked As Variant ThisDrawing.Utility.GetEntity oObj, vPtPicked, vbLf & _ "Select a block reference: " ' Check to see if the entity selected is a ' block reference If TypeOf oObj Is AcadBlockReference Then Dim oBlkRef As AcadBlockReference Set oBlkRef = oObj ' Output information about the block ThisDrawing.Utility.Prompt vbLf & "*Block Reference*" & _ vbLf & " Block name: " & _ oBlkRef.Name & vbLf ' Check to see if the block reference has attributes If oBlkRef.HasAttributes = True Then Dim oAttRef As AcadAttributeReference Dim oAttDef As AcadAttribute Dim vObj As Variant ' Gets the nonconstant attributes ThisDrawing.Utility.Prompt vbLf & "*Nonconstant Attributes*" Dim vArAtts As Variant vArAtts = oBlkRef.GetAttributes ' Steps through the nonconstant attributes If UBound(vArAtts) > -1 Then For Each vObj In vArAtts Set oAttRef = vObj ' Outputs the tag and text of the attribute ThisDrawing.Utility.Prompt vbLf & " Tag: " & _ oAttRef.TagString & _ vbLf & " Value: " & _ oAttRef.TextString Next vObj Else ThisDrawing.Utility.Prompt vbLf & " None" End If ' Gets the nonconstant attributes ThisDrawing.Utility.Prompt vbLf & "*Constant Attributes*" ' Gets the constant attributes vArAtts = oBlkRef.GetConstantAttributes ' Steps through the constant attributes If UBound(vArAtts) > -1 Then For Each vObj In vArAtts Set oAttDef = vObj ' Outputs the tag and text of the attribute ThisDrawing.Utility.Prompt vbLf & " Tag: " & _ oAttDef.TagString & _ vbLf & " Value: " & _ oAttDef.TextString Next vObj Else ThisDrawing.Utility.Prompt vbLf & " None" End If ThisDrawing.Utility.Prompt vbLf End If End If End Sub

Here is an example of the output generated by the custom ListBlockAtts procedure from Listing 30.1:

*Block Reference* Block name: RoomNumber *Nonconstant Attributes* Tag: ROOM# Value: 101 *Constant Attributes* None

In addition to listing the values of the attributes attached to a block reference, you can modify the appearance and placement of the attribute references returned by the GetAttributes function. If you make changes to an attribute reference, make sure to execute the Update method and regenerate the display of the object. The AcadAttributeReference and AcadAttribute objects are nearly identical. However, the AcadAttributeReference object doesn't support the Mode, Preset, PromptString, or Verify property.

Working with Dynamic Properties

Most block references display a single set of geometry, meaning that the objects that are included in the block definition are the only ones that can be shown in the drawing. Starting with AutoCAD 2006, block definitions were extended to support what are known as dynamic properties. Block definitions with dynamic properties are known as dynamic blocks. You can't create dynamic blocks with the AutoCAD Object library, but you can modify the custom properties of a dynamic block after it is inserted into a drawing. For information on how to create a dynamic block, see the topic「About Dynamic Blocks」in the AutoCAD Help system.

The IsDynamicBlock property of the AcadBlockReference object can be used to determine whether a block reference has dynamic properties. When the IsDynamicBlock property returns True, the block reference has dynamic properties that can be queried and modified.

Once you have verified that a block reference has dynamic properties, you use the GetDynamicBlockProperties function to get an array of AcadDynamicBlockReferenceProperty objects. The Value property of an AcadDynamicBlockReferenceProperty object is used to get and set the value of a dynamic property, whereas the PropertyName property returns a string that represents the name of the dynamic property.

Listing 30.2 is a custom procedure that demonstrates how to get the custom properties and their values of a block reference named Door - Imperial. You can insert the Door - Imperial block reference using the block tool on the Architectural tab of the Tool Palettes window (displayed using the toolpalettes command).

Listing 30.2: Listing custom properties and values of a block reference

Sub ListCustomProperties() ' Prompt the user to select a block reference Dim oObj As Object Dim vPtPicked As Variant ThisDrawing.Utility.GetEntity oObj, vPtPicked, vbLf & _ "Select a block reference: " ' Check to see if the entity selected is a ' block reference If TypeOf oObj Is AcadBlockReference Then Dim oBlkRef As AcadBlockReference Set oBlkRef = oObj ' Output information about the block ThisDrawing.Utility.Prompt vbLf & "*Block Reference*" & _ vbLf & " Block name: " & _ oBlkRef.Name & vbLf ' Check to see if the block reference has dynamic properties If oBlkRef.IsDynamicBlock = True Then Dim oDynProp As AcadDynamicBlockReferenceProperty Dim vObj As Variant ' Gets the block reference's dynamic properties ThisDrawing.Utility.Prompt vbLf & "*Dynamic Properties*" Dim vDynProps As Variant vDynProps = oBlkRef.GetDynamicBlockProperties ' Steps through the dynamic properties If UBound(vDynProps) > -1 Then For Each vObj In vDynProps Set oDynProp = vObj ' Outputs the property name and value Dim sValue As String If IsArray(oDynProp.Value) = False Then sValue = CStr(oDynProp.Value) Else For Each vVal In oDynProp.Value If sValue <> "" Then sValue = sValue & "," sValue = sValue & CStr(vVal) Next vVal End If ThisDrawing.Utility.Prompt vbLf & " Property Name: " & _ oDynProp.PropertyName & _ vbLf & " Value: " & _ sValue sValue = "" Next vObj Else ThisDrawing.Utility.Prompt vbLf & " None" End If ThisDrawing.Utility.Prompt vbLf End If End If End Sub

Here is an example of the output generated by the custom ListCustomProperties procedure from Listing 30.2:

*Block Reference* Block name: *U3 *Dynamic Properties* Property Name: Door Size Value: 40 Property Name: Origin Value: 0,0 Property Name: Wall Thickness Value: 6 Property Name: Origin Value: 0,0 Property Name: Hinge Value: 0 Property Name: Swing Value: 0 Property Name: Opening Angle Value: Open 30°

When a user manipulates a grip associated with a dynamic property, onscreen it looks like the user is manipulating the block reference through a stretching, arraying, moving, or other action. The action that is performed by the user results in the creation of a new anonymous block definition. An anonymous block is a block that can't be inserted into a drawing but that is used as a way to let AutoCAD create and manage unique blocks.

NOTE

The name of a block reference is typically obtained using the Name property, but with dynamic blocks the Name property might return an anonymous block name such as *U8. An anonymous block name is created as a result of manipulating one of the grips associated with a dynamic property on a block reference. To get the original name of the block definition for a dynamic block, you use the EffectiveName property.

You can convert a dynamic block to an anonymous block without dynamic properties using the ConvertToAnonymousBlock method or a new block definition using the ConvertToStaticBlock method. The ConvertToStaticBlock method expects a string that represents the name of the new block definition.

The appearance and custom properties of a dynamic block can be reset to their default values. To reset the appearance and custom properties of a dynamic block, you use the ResetBlock method of an AcadBlockReference object. The ResetBlock method doesn't accept any argument values and doesn't return a value.

Managing External References

AutoCAD allows you to create what is known as an external reference. An external reference is a reference to a file that is stored outside of a drawing file. The contents in an external file can be another drawing, a raster or vector image, or even a file that supports Object Linking and Embedding (OLE). OLE allows you to embed, among other things, a Word document or an Excel spreadsheet into a drawing file. In addition to referencing a file, you can import objects into a drawing using OLE. An OLE object is represented by the AcadOle object in the AutoCAD Object library. You can modify, but not create, an OLE object with the AutoCAD Object library. I discuss how to import objects or a file in Chapter 31.

You can see which files are externally referenced to a file by accessing the items of the AcadFileDependencies collection object. Each file that a drawing is dependent on to correctly display objects is part of the AcadFileDependencies collection object. I mention the AcadFileDependencies collection object in the「Listing File Dependencies」section later in this chapter.

Working with Xrefs

An external drawing file referenced into a drawing is known as an xref. Xrefs are similar to blocks because they allow for the reuse of geometry in any drawing with one distinct difference. The difference that sets blocks and xrefs apart is that any changes made to the objects in the external drawing file are reflected in any drawings that reference the file. Xrefs are frequently used in architectural and civil engineering drawings to reference a floor plan or survey drawing. An xref is represented by an AcadExternalReference object and is similar to an AcadBlockReference object except in the way that the object can be modified and managed.

Attaching an Xref

An xref is attached to a drawing, not inserted like a block or added like other graphical objects. The AttachExternalReference function returns an AcadExternalReference object and expects nine argument values that define which file to attach, as well as the placement and size of the xref. When an xref is attached to a drawing, an AcadBlock object is created. The AcadBlock object contains the geometry that is in the referenced drawing file, but objects can't be added or modified in that AcadBlock object. Figure 30.2 shows the flow of data that takes place when a drawing file is attached to a drawing and an xref is placed in model space.

Figure 30.2 Xref attachment flow

The following shows the syntax of the AttachExternalReference function:

retVal = object.AttachExternalReference(fileName, xrefName, insertionPoint, xScale, yScale, zScale, rotation, overlay [, password])

Its arguments are as follows:

retVal The retVal argument represents the new AcadExternalReference object returned by the AttachExternalReference function.

object The object argument specifies the AcadBlock, AcadModelSpace, or AcadPaperSpace object where you wish to attach the xref.

fileName The fileName argument is a string that represents the name of the external DWG file you want to reference.

xrefName The xrefName argument is a string that represents the name you want to assign to the AcadBlock object that is added to the drawing.

insertionPoint The insertionPoint argument is an array of doubles that represents the insertion point of the xref.

xScale, yScale, zScale The xScale, yScale, and zScale arguments are doubles that represent the scale factors of the xref.

rotation The rotation argument is a double that represent the rotation angle of the xref. The rotation angle must be expressed in radians.

overlay The overlay argument is a Boolean that represents the reference type for the xref. There are two reference types: attachment and overlay. The reference types don't affect the current drawing unless the drawing is referenced into another drawing. An attachment reference type allows the xref to be displayed in other drawings that reference the drawing that contains the xref, whereas an overlay reference restricts the xref to be displayed only in the drawing to which it is attached. Use a value of True to specify an overlay reference type.

password The password argument is an optional string that represents the password assigned to restrict the drawing file from being opened or referenced by unapproved users.

The following code statements add an xref based on the Ch30_Building_Plan.dwg file at 0,0 and set the reference type to attachment:

' Defines the insertion point Dim insPt(2) As Double insPt(0) = 0: insPt(1) = 0: insPt(2) = 0 ' Defines the path to the drawing file Dim dwgName As String dwgName = ThisDrawing.GetVariable("MyDocumentsPrefix") & _ "\MyCustomFiles\Ch30_Building_Plan.dwg" ' Adds the xref Dim oXref As AcadExternalReference Set oXref = ThisDrawing.ModelSpace.AttachExternalReference( _ dwgName, "Building_Plan", insPt, 1, 1, 1, 0, False)

TIP

The objects of all attached xrefs can be faded using the xdwgfadectl and xfadectl system variables. Use the SetVariable method of an AcadDocument or ThisDrawing object to change the values of the system variables, or the GetVariable function to get their current values.

Getting Information About and Modifying an Xref

Once an xref has been attached to a drawing, you can access information about the instance of the xref. As I previously mentioned, an xref is similar to a block reference that has been inserted into a drawing, and even the AcadExternalReference and AcadBlockReference objects share many of the same properties and methods. For information on how to access information about and modify a block reference, see the「Modifying a Block Reference」section earlier in this chapter.

Although an AcadExternalReference and AcadBlockReference object have much in common, there are a few differences:

Xrefs do not support attributes.

Xrefs do not support dynamic block properties.

Xrefs can't be exploded unless they have been bound to the drawing first.

The path to the external file can be modified.

The objects in the external referenced file can be accessed.

Although there are a number of differences between xrefs and block references, in the AutoCAD Object library the AcadExternalReference and AcadBlockReference objects are similar. The only difference between the two object types is the Path property. The Path property of an AcadExternalReference object can be used to get and specify the path that AutoCAD should look in for the externally referenced drawing file. I show an example of using the Path property in the next section.

For each externally referenced file that is attached to a drawing, AutoCAD creates an in-memory database for that file. The database is represented by an AcadDatabase object and contains access to the nongraphical and graphical objects stored in the externally referenced file. The database of an xref can be accessed with the XRefDatabase property of an AcadBlock object.

Objects in the database of an xref returned by the XRefDatabase property can't be directly modified. However, it is possible to open the externally referenced drawing file into memory with the AutoCAD/ObjectDBX Common Type library. After a drawing file is opened in memory with the AutoCAD/ObjectDBX Common Type library, the objects in the file can then be modified. Once changes have been made to the drawing, you use the Reload method of an AcadBlock object in the drawing to which the xref is attached to update its display. I mention the Reload method in the next section and how to reference other object libraries in Chapter 35,「Communicating with Other Applications.」

Changing the Layers of an Xref

Although you can't make changes to the geometry of an AcadBlock object that references an external file, you can affect the layers of an xref. To change a layer in an xref, set the visretain system variable to 1 with the SetVariable method of an AcadDocument or ThisDrawing object. After the visretain system variable has been enabled, you can use the XRefDatabase property of the AcadBlock object and access its AcadLayers collection, which contains the layers used by the objects of the xref. Any changes made to the layers are maintained in the drawing file that contains the xref and not the externally referenced file.

When locating an item in a collection object of the xref database, you must add the name of the xref with a pipe symbol as a prefix to the item's name. For example, to get the Surfaces layer in the xref named Building_Plan, you use the value Building_Plan|Surfaces.

The following code statements change the color of the layer named Surfaces to yellow:

' Enable the visretain system variable ThisDrawing.SetVariable "visretain", 1 ' Defines the name of the xref to locate Dim sXrefName As String sXrefName = "Building_Plan" ' Gets the name of the block Dim oBlkDef As AcadBlock Set oBlkDef = ThisDrawing.Blocks(sXrefName) ' Change the Surface layer in the xref to yellow oBlkDef.XRefDatabase.Layers(sXrefName & "|" _ & "Surfaces").color = acYellow

Managing an Attached Xref

The management of the reference between an external drawing file and an xref is handled through an AcadBlock object. The name of the AcadBlock object used by an xref can be obtained with the Name property of the AcadExternalReference object. Once the name of the block has been obtained, you can use the Item method of the AcadBlocks collection object to get the AcadBlock object associated with the xref.

In addition to using the Item method, you can use a For statement to step through all the blocks in a drawing and see which ones are associated with an external file. While stepping through the AcadBlocks collection object, the IsXref property of the AcadBlock object returns True if the block represents an external referenced file.

The following code statements get the AcadBlock object for a block named Building_Plan and then use the IsXref property to see if it is an xref. If the block is an xref, a message box with the path to the external referenced file is displayed.

' Defines the name of the xref to locate Dim sXrefName As String sXrefName = "Building_Plan" ' Gets the name of the block Dim oBlkDef As AcadBlock Set oBlkDef = ThisDrawing.Blocks(sXrefName) ' Check to see if the block is an xref If oBlkDef.IsXRef Then ' Display information about the xref MsgBox "Block name: " & sXrefName & _ vbLf & "Path: " & oBlkDef.Path End If

The Path property shown in the previous sample code is used to get the current path to the external referenced file, but it can also be used to update the default location for the externally referenced drawing file. After an AcadBlock object containing an external reference has been obtained, you can then manage the reference between the drawing and the external referenced file stored outside of AutoCAD. Table 30.6 lists the four functions that can be used to manage an xref.

Table 30.6 Methods used to manage an xref

Method Description

Bind Removes the reference to the external file, and all xrefs attached to the drawing are converted to blocks and stored as part of the drawing. Changes made to the external file no longer affect the objects in the drawing. The method expects a Boolean value; use True if you do not want to add a prefix to the symbol names that are created from the external reference or use False to add a prefix to the symbol name. Use a value of False to maintain the appearance of objects in the xref. Specifying a value of True indicates that the objects from the xref being merged will use the nongraphical objects defined in the drawing to which the xref is attached. If the nongraphical objects don't exist in the drawing to which the xref is attached and True is specified, the nongraphical object is copied from the xref's database.

Detach Removes the reference to the external referenced file, and all xrefs attached to the drawing are removed. This method doesn't accept any arguments.

Reload Updates the geometry in the drawing by reading the objects from the external referenced file. This method doesn't accept any arguments.

Unload Maintains the reference to the external referenced file, and all xrefs remain in the drawing. The file isn't loaded into the drawing, which results in the objects contained in the file not being displayed. This method doesn't accept any arguments.

The following code statements reload the external reference named Building_Plan:

' Defines the name of the xref to locate Dim sXrefName As String sXrefName = "Building_Plan" ' Gets the name of the block Dim oBlkDef As AcadBlock Set oBlkDef = ThisDrawing.Blocks(sXrefName) ' Reload the xref oBlkDef.Reload

Attaching and Modifying Raster Images

A raster image stored in an external file can be attached to a drawing. You might want to reference an external image file to place a company logo on a title block, display a watermark, or reference a topography map. An image file that has been added to a drawing is represented by an AcadRasterImage object.

NOTE

Before attaching an image to a drawing file, keep in mind that large image files can increase the amount of time it takes to open a drawing and even change the display of a drawing.

A raster image can be added to model space or paper space using the AddRaster function. The AddRaster function returns an AcadRasterImage object and expects four argument values that specify the image file you want to add and then the placement and size of the image.

The following shows the syntax of the AddRaster function:

retVal = object.AddRaster(fileName, insertionPoint, scaleFactor, rotation)

Its arguments are as follows:

retVal The retVal argument represents the new AcadRasterImage object returned by the AddRaster function.

object The object argument specifies the AcadBlock, AcadModelSpace, or AcadPaperSpace object and indicates where you want to add the raster image.

fileName The fileName argument is a string that represents the name of the image file.

insertionPoint The insertionPoint argument is an array of doubles that represents the insertion point of the raster image.

scaleFactor The scaleFactor argument is a double that represents the scale factor of the raster image.

rotation The rotation argument is a double that represents the rotation angle of the raster image. The rotation angle must be expressed in radians.

The following code statements add a raster image based on the acp_logo.png filename to 5,5 and set the background of the image to transparent:

' Defines the insertion point Dim insPt(2) As Double insPt(0) = 5: insPt(1) = 5: insPt(2) = 0 ' Defines the path to the image Dim imageName As String imageName = ThisDrawing.GetVariable("MyDocumentsPrefix") & _ "\MyCustomFiles\acp_logo.png" ' Adds the raster image Dim oRaster As AcadRasterImage Set oRaster = ThisDrawing.ModelSpace. _ AddRaster(imageName, insPt, 1, 0) ' Sets the background of the image to transparent oRaster.Transparency = True

After a raster image has been added to a drawing, you can control its appearance using the object properties and methods. A raster image supports the same general properties and methods as all graphical objects in a drawing, along with additional object-specific properties. Table 30.7 lists the properties that are specific to a raster image.

Table 30.7 Raster image–related properties and methods

Property/Method Description

Brightness Specifies the brightness applied to the raster image; the valid range is 0 to 100.

ClippingEnabled Returns True if the raster image is clipped.

ClipBoundary Specifies the clipping boundary of the raster image. The ClipBoundary method expects an array of doubles that form a closed region. The array must contain a minimum of six elements; each element pairing specifies a 2D coordinate value.

Contrast Specifies the contrast applied to the raster image; the valid range is 0 to 100.

Fade Specifies the fade value applied to the raster image; the valid range is 0 to 100. The greater the value, the more transparent the object.

Height Returns the height, in pixels, for the raster image. This property is read-only.

ImageFile Specifies the full path to the external file for the raster image.

ImageHeight Specifies the height, in pixels, for the raster image.

ImageVisibility Returns True if the raster image is visible.

ImageWidth Specifies the width, in pixels, for the raster image.

Name Specifies the name of the raster image.

Origin Specifies the insertion point of the raster image in the drawing and is an array of doubles.

Rotation Specifies the rotation of the raster image.

ScaleFactor Specifies the scale factor applied to the raster image.

ShowRotation Returns True if the raster image is displayed at its specified rotation.

Transparency Returns True if the background of the raster image is displayed as transparent.

Width Returns the width, in pixels, for the underlay. This property is read-only.

Masking Objects with Wipeouts

A wipeout object is used to mask or hide other objects in a drawing. For example, you can place a wipeout behind the text or extension line of a dimension to make the text easier to read and make it easier to identify the objects that are dimensioned. An AcadWipeout object is used to represent a wipeout object that was created in a drawing.

There is no method to create a new wipeout, but you can use the wipeout command with the SendCommand or PostCommand method. The properties of an AcadWipeout object are the same as an AcadRasterImage object. I explained how to work with raster images in the「Attaching and Modifying Raster Images」section earlier in this chapter.

Working with Underlays

Underlays consist of geometry and annotation that is referenced into a drawing file from a drawing web (DWF/DWFx) file, MicroStation design (DGN) file, or an Adobe portable document (PDF) file. The geometry in an underlay is less accurate than that of a drawing because of the source applications that created the objects. Even though an underlay is less accurate, the accuracy might be enough for many designs created in the architectural and civil engineering industries.

When an underlay is attached to a drawing, its objects can be controlled using the layer information embedded in the underlay. As users create new objects in a drawing, they can use object snaps to snap to geometry that is part of an underlay.

The AutoCAD Object library doesn't provide support for attaching or detaching an underlay, but it does provide some support for querying and modifying an underlay that has already been attached to a drawing. If you want to attach an underlay, you can use the -dgnattach, -dwfattach, or -pdfattach commands with the SendCommand or PostCommand method.

The following objects represent the underlays that can be attached to a drawing:

AcadDgnUnderlay—DGN underlay

AcadDwfUnderlay—DWF/DWFx underlay

AcadPdfUnderlay—PDF underlay

The following code statements demonstrate how the ObjectName property can be used to determine the type of an underlay object. The first two code statements get the first object in model space and expect the object to be an underlay.

Dim oEnt As AcadEntity Set oEnt = ThisDrawing.ModelSpace(0) Select Case oEnt.ObjectName Case "AcDbDgnReference" MsgBox "Underlay is a DGN file." Case "AcDbDwfReference" MsgBox "Underlay is a DWF file." Case "AcDbPdfReference" MsgBox "Underlay is a PDF file." End Select

An underlay shares many properties in common with an AcadRaster object. The following properties are shared between underlays and raster images:

ClippingEnabled

Contrast

FadeHeight

Rotation

ScaleFactor

Width

Table 30.8 lists the properties specific to an underlay. These properties can be used to control the display of the object and get information about the referenced file.

Table 30.8 Underlay-related properties

Property Description

AdjustForBackground Returns True if the colors in the underlay are adjusted for the current background color of the viewport.

File Specifies the full path to the external file that contains the objects for the underlay.

ItemName Specifies the sheet or design model name in the underlay file you want to display. A sheet or design model is one of the pages or designs stored in the underlay file. For example, a PDF file can contain several pages, and you use ItemName to specify which page you want to display.

Monochrome Returns True if the colors of the underlay are displayed as monochromatic.

Position Specifies the insertion point of the underlay in the drawing and is an array of doubles.

UnderlayLayerOverrideApplied Specifies whether layer overrides are applied to the underlay; a constant value of acNoOverrides means no overrides are applied, whereas acApplied indicates overrides are applied.

UnderlayName Specifies the name of the underlay file.

UnderlayVisibility Returns True if the objects in the underlay should be visible.

Listing File Dependencies

A drawing file relies on a number of support files to display objects accurately. These support files might be font files, plot styles, external referenced files, and much more. You can use the AcadFileDependencies collection object to access a listing of the files that need to be included when sharing your files with a subcontractor or archiving your designs. Each dependency in the AcadFileDependencies collection object is represented by an AcadFileDependency object.

Although it is possible to directly add new entries for file dependencies to a drawing, I recommend letting the AutoCAD application and AutoCAD Object library do the work for you. Incorrectly defining a file dependency could have unexpected results on a drawing; objects might not display correctly or at all. Methods such as AttachExternalReference and AddRaster will add the appropriate file dependency entries to a drawing.

If you want, you can use the CreateEntry, RemoveEntry, and UpdateEntry methods to manage the file dependencies of a drawing. See the AutoCAD Help system for information on the methods used to manage file dependencies. In most cases, you will simply want to query the file dependencies of a drawing to learn which files might be missing and help the user locate them if possible. Use the Item method or a For statement to step through the file dependencies of the AcadFileDependencies collection object.

The following code statements display information about each file dependency at the Command prompt:

Sub ListDependencies() Dim oFileDep As AcadFileDependency For Each oFileDep In ThisDrawing.FileDependencies ThisDrawing.Utility.Prompt _ vbLf & "Affects graphics: " & CStr(oFileDep.AffectsGraphics) & _ vbLf & "Feature: " & oFileDep.Feature & _ vbLf & "File name: " & oFileDep.FileName & _ vbLf & "File size (Bytes): " & CStr(oFileDep.FileSize) & _ vbLf & "Found path: " & oFileDep.FoundPath & _ vbLf Next oFileDep End Sub

NOTE

A drawing file must have been saved once before you access its file dependency entries with the AcadFileDependencies collection object. Using the file path returned by the FileName and FoundPath properties of an AcadFileDependency object, you can use the FileSystemObject object to get more information about the referenced file. I explain how to use the FileSystemObject object in Chapter 35.

Here is an example of the output produced for a file dependency:

Affects graphics: True Feature: Acad:Text File name: arial.ttf File size (Bytes): 895200 Found path: C:\WINDOWS\FONTS\

Exercise: Creating and Querying Blocks

In this section, you will create several new procedures that create and insert room label blocks into a drawing, move the blocks to specific layers based on their names, and extract the attributes of the blocks to produce a bill of materials (BOM). Room labels and blocks with attributes are often used in architectural drawings, but the same concepts can be applied to callouts and parts in mechanical drawings.

As you insert a room label block with the custom program, a counter increments by 1 so you can place the next room label without needing to manually enter a new value. The last calculated value is stored in a custom dictionary so it can be retrieved the next time the program is started. The key concepts I cover in this exercise are:

Creating and Modifying Block Definitions Block definitions are used to store a grouping of graphical objects that can be inserted into a drawing. Inserting a block definition creates a block reference that creates an instance of the objects defined in a block definition and not a copy of the objects.

Modify and Extracting Attributes The attributes attached to a block reference can be modified to hold different values per block reference, and those values can be extracted to a database or even a table within the drawing. Attribute values can represent project information, part numbers and descriptions of the parts required to assemble a new project, and so on.

NOTE

The steps in this exercise depend on the completion of the steps in the「Exercise: Creating, Querying, and Modifying Objects」section of Chapter 27. If you didn't complete the steps, do so now or start with the ch30_clsUtilities.cls sample file available for download from www.sybex.com/go/autocadcustomization. Place these sample files in the MyCustomFiles folder under the Documents (or My Documents) folder, or the location you are using to store the DVB files. Also, remove the ch30_ prefix from the name of the CLS file. You will also be working with the ch30_building_plan.dwg from this chapter's sample files.

Creating the RoomLabel Project

The RoomLabel project will contain functions and a main procedure that allow you to create and insert a room label block based on end-user input. The number applied to the block is incremented each time the block is placed in the current drawing. The following steps explain how to create a project named RoomLabel and to save it to a file named roomlabel.dvb:

Create a new VBA project with the name RoomLabel. Make sure to change the default project name (ACADProject) to RoomLabel in the VBA Editor.

In the VBA Editor, in the Project Explorer, right-click the new project and choose Import File.

When the Import File dialog box opens, browse to and select the clsUtilities.cls file in the MyCustomFiles folder. Click Open.The clsUtilities.cls file contains the utility procedures that you created as part of the DrawPlate project.

In the Project Explorer, right-click the new project and choose Insert Module. Change the default name of the new module to basRoomLabel.

On the menu bar, click File Save.

Creating the RoomLabel Block Definition

Creating separate drawing files that your custom programs depend on has advantages and disadvantages. One advantage of creating a separate drawing file is that you can use the AutoCAD user interface to create the block file. However, AutoCAD must be able to locate the drawing file so that the custom program can use the file. If AutoCAD can't locate the file, the custom program will have problems. Creating a block definition through code allows you to avoid the need of maintaining separate files for your blocks, thus making it easier to share a custom application with your clients or subcontractors. A disadvantage of using code to create your blocks is the time it takes to write the code for all your blocks and then having to maintain the code once it has been written.

In these steps, you create a custom function named roomlabel_createblkdef that will be used to create the block definition for the room label block if it doesn't already exist in the drawing.

In the Project Explorer, double-click the basRoomLabel component.

In the text editor area of the basRoomLabel component, type the following. (The comments are here for your information and don't need to be typed.)Private myUtilities As New clsUtilities ' Constant for the removal of the "Command: " prompt msg Const removeCmdPrompt As String = vbBack & vbBack & vbBack & _ vbBack & vbBack & vbBack & _ vbBack & vbBack & vbBack & vbLf Private g_nLastNumber As Integer Private g_sLastPrefix As String ' Creates the block definition roomlabel Private Sub RoomLabel_CreateBlkDef() On Error Resume Next ' Check for the existence of the roomlabel block definition Dim oBlkDef As AcadBlock Set oBlkDef = ThisDrawing.Blocks("roomlabel") ' If an error was generated, create the block definition If Err Then Err.Clear ' Define the block's origin Dim dInsPt(2) As Double dInsPt(0) = 18: dInsPt(1) = 9: dInsPt(2) = 0 ' Create the block definition Set oBlkDef = ThisDrawing.Blocks.Add(dInsPt, "roomlabel") ' Add a rectangle to the block Dim dPtList(7) As Double dPtList(0) = 0: dPtList(1) = 0 dPtList(2) = 36: dPtList(3) = 0 dPtList(4) = 36: dPtList(5) = 18 dPtList(6) = 0: dPtList(7) = 18 Dim oLWPline As AcadLWPolyline Set oLWPline = oBlkDef.AddLightWeightPolyline(dPtList) oLWPline.Closed = True ' Add the attribute definition to the block Dim oAttDef As AcadAttribute Set oAttDef = oBlkDef.AddAttribute(9, acAttributeModeLockPosition, _ "ROOM#", dInsPt, "ROOM#", "L000") oAttDef.Layer = "Plan_RoomLabel_Anno" ' Set the alignment of the attribute oAttDef.Alignment = acAlignmentMiddleCenter oAttDef.TextAlignmentPoint = dInsPt End If End Sub

Click File Save.

Figure 30.3 shows the block definition that is created by this procedure. To see the contents of the block definition, use the bedit command and select the RoomLabel block. As an alternative, you can insert the RoomLabel block into the drawing and explode it.

Figure 30.3 RoomLabel block definition

Inserting a Block Reference Based on the RoomLabel Block Definition

Once you've created the block definition and added it to the AcadBlocks collection object, you can insert it into the drawing by using the insert command or the InsertBlock function in the AutoCAD Object library.

In these steps, you create two custom functions named changeattvalue and roomlabel_insertblkref. The changeattvalue function allows you to revise the insertion point and value of an attribute reference attached to a block reference based on the attribute's tag. The roomlabel_insertblkref function creates a block reference based on the RoomLabel block definition that was created with the roomlabel_createblkdef function.

In the text editor area of the basRoomLabel component, scroll to the bottom of the last procedure and press Enter a few times. Then, type the following. (The comments are here for your information and don't need to be typed.)' Changes the value of an attribute reference in a block reference Private Sub ChangeAttValue(oBlkRef As AcadBlockReference, _ vInsPt As Variant, sAttTag As String, _ sNewValue As String) ' Check to see if the block reference has attribute references If oBlkRef.HasAttributes Then ' Get the attributes of the block reference Dim vAtts As Variant vAtts = oBlkRef.GetAttributes Dim nCnt As Integer ' Step through the attributes in the block reference Dim oAttRef As AcadAttributeReference For nCnt = 0 To UBound(vAtts) Set oAttRef = vAtts(nCnt) ' Compare the attributes tag with the tag ' passed to the function If UCase(oAttRef.TagString) = UCase(sAttTag) Then oAttRef.InsertionPoint = vInsPt oAttRef.TextAlignmentPoint = vInsPt oAttRef.textString = sNewValue ' Exit the For statement Exit For End If Next End If End Sub ' Creates the block definition roomlabel Private Sub RoomLabel_InsertBlkRef(vInsPt As Variant, _ sLabelValue As String) ' Add the layer Plan_RoomLabel_Anno myUtilities.CreateLayer "Plan_RoomLabel_Anno", 150 ' Create the "roomlabel" block definition RoomLabel_CreateBlkDef ' Insert the block into model space Dim oBlkRef As AcadBlockReference Set oBlkRef = ThisDrawing.ModelSpace. _ InsertBlock(vInsPt, "roomlabel", _ 1, 1, 1, 0) ' Changes the attribute value of the "ROOM#" ChangeAttValue oBlkRef, vInsPt, "ROOM#", sLabelValue End Sub

Click File Save.

Prompting the User for an Insertion Point and a Room Number

Now that you have defined the functions to create the block definition and inserted the block reference into a drawing, the last function creates the main procedure that will prompt the user for input. The roomlabel procedure will allow the user to specify a point in the drawing, provide a new room number, or provide a new prefix. The roomlabel procedure uses the default number of 101 and prefix of L. As you use the roomlabel procedure, it increments the counter by 1 so that you can continue placing room labels.

In these steps, you create the custom procedure named roomlabel that uses all of the functions that you defined in this exercise to place a RoomLabel block each time you specify a point in the drawing.

In the text editor area of the basRoomLabel component, scroll to the bottom of the last procedure and press Enter a few times. Then, type the following. (The comments are here for your information and don't need to be typed.)' Prompts the user for an insertion point and room number Public Sub RoomLabel() On Error Resume Next ' Set the default values Dim nLastNumber As Integer, sLastPrefix As String If g_nLastNumber <> 0 Then nLastNumber = g_nLastNumber sLastPrefix = g_sLastPrefix Else nLastNumber = 101 sLastPrefix = "L" End If ' Display current values ThisDrawing.Utility.Prompt removeCmdPrompt & _ "Prefix: " & sLastPrefix & _ vbTab & "Number: " & CStr(nLastNumber) Dim basePt As Variant ' Continue to ask for input until a point is provided Do Dim sKeyword As String sKeyword = "" basePt = Null ' Setup default keywords ThisDrawing.Utility.InitializeUserInput 0, "Number Prefix" ' Prompt for a base point, number, or prefix value basePt = ThisDrawing.Utility.GetPoint(, _ removeCmdPrompt & "Specify point for room label (" & _ sLastPrefix & CStr(nLastNumber) & _ ") or change [Number/Prefix]: ") ' If an error occurs, the user entered a keyword or pressed Enter If Err Then Err.Clear sKeyword = ThisDrawing.Utility.GetInput Select Case sKeyword Case "Number" nLastNumber = ThisDrawing.Utility. _ GetInteger(removeCmdPrompt & _ "Enter new room number <" & _ CStr(nLastNumber) & ">: ") Case "Prefix" sLastPrefix = ThisDrawing.Utility. _ GetString(False, removeCmdPrompt & _ "Enter new room number prefix <" & _ sLastPrefix & ">: ") End Select End If ' If a base point was specified, then insert a block reference If IsNull(basePt) = False Then RoomLabel_InsertBlkRef basePt, sLastPrefix & CStr(nLastNumber) ' Increment number by 1 nLastNumber = nLastNumber + 1 End If Loop Until IsNull(basePt) = True And sKeyword = "" ' Store the latest values in the global variables g_nLastNumber = nLastNumber g_sLastPrefix = sLastPrefix End Sub

Click File Save.

Adding Room Labels to a Drawing

The roomlabel.dvb file contains the main roomlabel procedure and some helper functions defined in the clsUtilities.cls file to define new layers.

NOTE

The following steps require a drawing file named ch30_building_plan.dwg. If you didn't download the sample files previously, download them now from www.sybex.com/go/autocadcustomization. Place these sample files in the MyCustomFiles folder under the Documents (or My Documents) folder.

The following steps explain how to use the roomlabel procedure that is in the roomlabel.lsp file:

Open Ch30_Building_Plan.dwg. Figure 30.4 shows the plan drawing of the office building.

At the Command prompt, type vbarun and press Enter.

When the Macros dialog box opens, select the RoomLabel.dvb!basRoomLabel.RoomLabel macro from the list and click Run.

At the Specify point for room label (L101) or change [Number/Prefix]: prompt, specify a point inside the room in the lower-left corner of the building.The room label definition block and Plan_RoomLabel_Anno layer are created the first time the roomlabel procedure is used. The RoomLabel block definition should look like Figure 30.5 when inserted into the drawing.

At the Specify point for room label (L101) or change [Number/Prefix]: prompt, type n and press Enter.

At the Enter new room number <102>: prompt, type 105 and press Enter.

At the Specify point for room label (L105) or change [Number/Prefix]: prompt, type p and press Enter.

At the Enter new room number prefix <L>: prompt, type R and press Enter.

At the Specify point for room label (R105) or change [Number/Prefix]: prompt, specify a point in the large open area in the middle of the building.

Press Enter to end roomlabel.

Close and discard the changes to the drawing file.

Figure 30.4 Plan view of the office building

Figure 30.5 Inserted RoomLabel block

Creating the FurnTools Project

The FurnTools project will contain several functions and main procedures that modify the properties and extract the attribute values of block references that have been inserted into a drawing. The following steps explain how to create a project named FurnTools and save it to a file named furntools.dvb:

Create a new VBA project with the name FurnTools. Make sure to also change the default project name (ACADProject) to FurnTools in the VBA Editor.

In the VBA Editor, in the Project Explorer, right-click the new project and choose Import File.

When the Import File dialog box opens, browse to and select the clsUtilities.cls file in the MyCustomFiles folder. Click Open.The clsUtilities.cls file contains the utility procedures that you created as part of the DrawPlate project.

In the Project Explorer, right-click the new project and choose Insert Module. Change the name of the new module to basFurnTools.

On the menu bar, click File Save.

Moving Objects to Correct Layers

Not everyone will agree on the naming conventions, plot styles, and other various aspects of layers, but there are two things drafters can agree on when it comes to layers:

Objects should inherit their properties, for the most part, from the objects in which they are placed.

Objects should only be placed on layer 0 when creating blocks.

Although I would like to think that all of the drawings I have ever created are perfect, I know they aren't. Rushed deadlines, changing project parameters, and other distractions impede perfection. Objects may have been placed on the wrong layer, or maybe it wasn't my fault and standards simply changed during the course of a project. With VBA and the AutoCAD Object library, you can identify potential problems in a drawing and let the user know about them so they can be fixed. You might even be able to fix the problems automatically without user input.

In these steps, you will create a custom procedure named furnlayers that will be used to identify objects by type and value to ensure they are placed on the correct layer. This is achieved by using selection sets and entity data lists, along with looping and conditional statements.

In the Project Explorer, double-click the basFurnTools component.

In the text editor area of the basFurnTools component, type the following. (The comments are here for your information and don't need to be typed.)Private myUtilities As New clsUtilities ' Constants for PI Const PI As Double = 3.14159265358979 ' Moves objects to the correct layers based on a set of established rules Sub FurnLayers() On Error Resume Next ' Get the blocks to extract Dim oSSFurn As AcadSelectionSet Set oSSFurn = ThisDrawing.SelectionSets.Add("SSFurn") ' If an error is generated, selection set already exists If Err Then Err.Clear Set oSSFurn = ThisDrawing.SelectionSets("SSFurn") End If ' Define the selection set filter to select only blocks Dim nDXFCodes(3) As Integer, nValue(3) As Variant nDXFCodes(0) = -4: nValue(0) = "<OR": nDXFCodes(1) = 0: nValue(1) = "INSERT" nDXFCodes(2) = 0: nValue(2) = "DIMENSION" nDXFCodes(3) = -4: nValue(3) = "OR>" Dim vDXFCodes As Variant, vValues As Variant vDXFCodes = nDXFCodes vValues = nValue ' Allow the user to select objects in the drawing oSSFurn.SelectOnScreen vDXFCodes, vValues ' Proceed if oSSFurn is greater than 0 If oSSFurn.Count > 0 Then ' Step through each object in the selection set Dim oEnt As AcadEntity For Each oEnt In oSSFurn ' Check to see if the object is a block reference If oEnt.ObjectName = "AcDbBlockReference" Then Dim oBlkRef As AcadBlockReference Set oBlkRef = oEnt ' Get the name of the block, use EffectiveName because ' the block could be dynamic Dim sBlkName As String sBlkName = oBlkRef.EffectiveName ' If the block name starts with RD or CD, ' then place it on the surfaces layer If sBlkName Like "RD*" Or _ sBlkName Like "CD*" Then oBlkRef.Layer = "Surfaces" ' If the block name starts with PNL, PE, and PX, ' then place it on the panels layer ElseIf sBlkName Like "PNL*" Or _ sBlkName Like "PE*" Or _ sBlkName Like "PX*" Then oBlkRef.Layer = "Panels" ' If the block name starts with SF, ' then place it on the panels layer ElseIf sBlkName Like "SF*" Or _ sBlkName Like "FF*" Then oBlkRef.Layer = "Storage" End If ElseIf oEnt.ObjectName Like "AcDb*Dim*" Then oEnt.Layer = "Dimensions" End If Next oEnt ' Remove the selection set oSSFurn.Delete End If End Sub

Click File Save.

Creating a Basic Block Attribute Extraction Program

The designs you create take time and often are a source of income or savings for your company. Based on the types of objects in a drawing, you can step through a drawing and get attribute information from blocks or even geometric values such as lengths and radii of circles. You can use the objects in a drawing to estimate the potential cost of a project or even provide information to manufacturing.

In these steps, you create four custom functions named ExtAttsFurnBOM, SortArray, TableFurnBOM, and RowValuesFurnBOM. The ExtAttsFurnBOM function extracts the values of the attributes in the selected blocks and then uses the SortArray function to sort the attribute values before quantifying them. The TableFurnBOM and RowValuesFurnBOM functions are used to create a grid of lines containing the extracted values.

In the text editor area of the basFurnTools component, scroll to the bottom of the last procedure and press Enter a few times. Then, type the following. (The comments are here for your information and don't need to be typed.)' ExtAttsFurnBOM - Extracts, sorts, and quantifies the attribute information Private Function ExtAttsFurnBOM(oSSFurn As AcadSelectionSet) As Variant Dim sList() As String Dim sPart As String, sLabel As String ' Step through each block in the selection set Dim oBlkRef As AcadBlockReference Dim nListCnt As Integer nListCnt = 0 For Each oBlkRef In oSSFurn ' Step through the objects that appear after ' the block reference, looking for attributes Dim vAtts As Variant vAtts = oBlkRef.GetAttributes ' Check to see if the block has attributes If oBlkRef.HasAttributes = True Then ' Get the attributes of the block reference Dim vAttRefs As Variant vAttRefs = oBlkRef.GetAttributes Dim oAttRef As AcadAttributeReference Dim nAttCnt As Integer For nAttCnt = LBound(vAttRefs) To UBound(vAttRefs) Set oAttRef = vAttRefs(nAttCnt) If UCase(oAttRef.TagString) = "PART" Then sPart = oAttRef.textString ElseIf UCase(oAttRef.TagString) = "LABEL" Then sLabel = oAttRef.textString End If Next End If ' Resize the array ReDim Preserve sList(nListCnt) ' Add the part and label values to the array sList(nListCnt) = sLabel & vbTab & sPart ' Increment the counter nListCnt = nListCnt + 1 Next oBlkRef ' Sort the array of parts and labels Dim vFurnListSorted As Variant vFurnListSorted = SortArray(sList) ' Quantify the list of parts and labels ' Step through each value in the sorted array Dim sFurnList() As String Dim vCurVal As Variant, sPreVal As String Dim sItems As Variant nCnt = 0: nListCnt = 0 For Each vCurVal In vFurnListSorted ' Check to see if the previous value is the same as the current value If CStr(vCurVal) = sPreVal Or sPreVal = "" Then ' Increment the counter by 1 nCnt = nCnt + 1 ' Values weren't the same, so record the quantity Else ' Split the values of the item sItems = Split(sPreVal, vbTab) ' Resize the array ReDim Preserve sFurnList(nListCnt) ' Add the part and label values to the array sFurnList(nListCnt) = CStr(nCnt) & vbTab & sItems(0) & vbTab & sItems(1) ' Increment the array counter nListCnt = nListCnt + 1 ' Reset the counter nCnt = 1 End If sPreVal = CStr(vCurVal) Next vCurVal ' Append the last item ' Split the values of the item sItems = Split(sPreVal, vbTab) ' Resize the array ReDim Preserve sFurnList(nListCnt) ' Add the part and label values to the array sFurnList(nListCnt) = CStr(nCnt) & vbTab & sItems(0) & vbTab & sItems(1) ' Return the sorted and quantified array ExtAttsFurnBOM = sFurnList End Function ' Performs a basic sort on the string values in an array, ' and returns the newly sorted array. Private Function SortArray(vArray As Variant) As Variant Dim nFIdx As Integer, nLIdx As Integer nFIdx = LBound(vArray): nLIdx = UBound(vArray) Dim nOuterCnt As Integer, nInnerCnt As Integer Dim sTemp As String For nOuterCnt = nFIdx To nLIdx - 1 For nInnerCnt = nOuterCnt + 1 To nLIdx If vArray(nOuterCnt) > vArray(nInnerCnt) Then sTemp = vArray(nInnerCnt) vArray(nInnerCnt) = vArray(nOuterCnt) vArray(nOuterCnt) = sTemp End If Next nInnerCnt Next nOuterCnt SortArray = vArray End Function ' Create the bill of materials table/grid Private Sub TableFurnBOM(vQtyList As Variant, dInsPt() As Double) ' Define the sizes of the table and grid Dim dColWidths(3) As Double dColWidths(0) = 0: dColWidths(1) = 15 dColWidths(2) = 45: dColWidths(3) = 50 Dim dTableWidth As Double, dTableHeight As Double dTableWidth = 0: dTableHeight = 0 Dim nRow As Integer nRow = 1 Dim dRowHeight As Double, dTextHeight As Double dRowHeight = 4: dTextHeight = dRowHeight - 1 ' Get the table width by adding all column widths Dim vColWidth As Variant For Each vColWidth In dColWidths dTableWidth = dTableWidth + CDbl(vColWidth) Next vColWidth ' Define the standard table headers Dim sHeaders(2) As String sHeaders(0) = "QTY": sHeaders(1) = "LABELS": sHeaders(2) = "PARTS" ' Create the top of the table Dim vInsPtRight As Variant vInsPtRight = ThisDrawing.Utility.PolarPoint( _ dInsPt, 0, dTableWidth) Dim oLine As AcadLine Set oLine = ThisDrawing.ModelSpace.AddLine(dInsPt, vInsPtRight) ' Get the bottom of the header row Dim vBottomRow As Variant vBottomRow = ThisDrawing.Utility.PolarPoint( _ dInsPt, ((PI / 2) * -1), dRowHeight) ' Add headers to the table RowValuesFurnBOM sHeaders, vBottomRow, dColWidths, dTextHeight ' Step through each item in the list Dim vItem As Variant For Each vItem In vQtyList nRow = nRow + 1 vBottomRow = ThisDrawing.Utility.PolarPoint( _ dInsPt, ((PI / 2) * -1), dRowHeight * nRow) RowValuesFurnBOM Split(vItem, vbTab), vBottomRow, dColWidths, dTextHeight Next vItem ' Create the vertical lines for each column dColWidthTotal = 0 For Each vColWidth In dColWidths ' Calculate the placement of each vertical line (left to right) dColWidthTotal = CDbl(vColWidth) + dColWidthTotal Dim vColBasePt As Variant vColBasePt = ThisDrawing.Utility.PolarPoint( _ dInsPt, 0, dColWidthTotal) Dim vColBottomPt As Variant vColBottomPt = ThisDrawing.Utility.PolarPoint( _ vColBasePt, ((PI / 2) * -1), _ myUtilities.Calc2DDistance(dInsPt(0), _ dInsPt(1), _ vBottomRow(0), _ vBottomRow(1))) ' Draw the vertical line Set oLine = ThisDrawing.ModelSpace.AddLine(vColBasePt, vColBottomPt) Next vColWidth End Sub ' Create a row and populate the data for the table Private Sub RowValuesFurnBOM(vItems As Variant, _ vBottomRow As Variant, _ vColWidths As Variant, _ dTextHeight As Double) ' Calculate the insertion point for the header text Dim dRowText(2) As Double dRowText(0) = 0.5 + vBottomRow(0) dRowText(1) = 0.5 + vBottomRow(1) dRowText(2) = vBottomRow(2) Dim dTableWidth As Double dTableWidth = 0 ' Get the table width by adding all column widths Dim vColWidth As Variant For Each vColWidth In vColWidths dTableWidth = dTableWidth + CDbl(vColWidth) Next vColWidth ' Lay out the text in each row Dim nCol As Integer, dColWidthTotal As Double nCol = 0: dColWidthTotal = 0 Dim vItem As Variant For Each vItem In vItems ' Calculate the placement of each text object (left to right) dColWidthTotal = dColWidthTotal + vColWidths(nCol) Dim vInsTextCol As Variant vInsTextCol = ThisDrawing.Utility.PolarPoint( _ dRowText, 0, dColWidthTotal) ' Draw the single-line text object Dim oText As AcadText Set oText = ThisDrawing.ModelSpace.AddText(CStr(vItem), _ vInsTextCol, dTextHeight) ' Create the row line Dim vBottomRowRight As Variant vBottomRowRight = ThisDrawing.Utility.PolarPoint( _ vBottomRow, 0, dTableWidth) Dim oLine As AcadLine Set oLine = ThisDrawing.ModelSpace.AddLine(vBottomRow, vBottomRowRight) ' Increment the counter nCol = nCol + 1 Next vItem End Sub ' Extracts, aggregates, and counts attributes from the furniture blocks Sub FurnBOM() On Error Resume Next ' Get the blocks to extract Dim oSSFurn As AcadSelectionSet Set oSSFurn = ThisDrawing.SelectionSets.Add("SSFurn") ' If an error is generated, selection set already exists If Err Then Err.Clear Set oSSFurn = ThisDrawing.SelectionSets("SSFurn") End If ' Define the selection set filter to select only blocks Dim nDXFCodes(0) As Integer, nValue(0) As Variant nDXFCodes(0) = 0 nValue(0) = "INSERT" Dim vDXFCodes As Variant, vValues As Variant vDXFCodes = nDXFCodes vValues = nValue ' Allow the user to select objects in the drawing oSSFurn.SelectOnScreen vDXFCodes, vValues ' Use the ExtAttsFurnBOM to extract and quantify the attributes in the blocks ' If a selection set was created, then look for attributes If oSSFurn.Count > 0 Then ' Extract and quantify the parts in the drawing Dim vAttList As Variant vAttList = ExtAttsFurnBOM(oSSFurn) ' Create the layer named BOM and set it current Dim oLayer As AcadLayer Set oLayer = myUtilities.CreateLayer("BOM", 8) Set ThisDrawing.ActiveLayer = oLayer.Name ' Prompt the user for the point to create the BOM Dim vInsPt As Variant vInsPt = ThisDrawing.Utility.GetPoint(, vbLf & _ "Specify upper-left corner of BOM: ") ' Start the function that creates the table grid Dim dInsPt(2) As Double dInsPt(0) = vInsPt(0): dInsPt(1) = vInsPt(1): dInsPt(2) = vInsPt(2) TableFurnBOM vAttList, dInsPt ' Remove the selection set oSSFurn.Delete End If End Sub

Click File Save.

Using the Procedures of the FurnTools Project

The procedures you added to FurnTools project leverage some of the functions defined in clsUtilities.cls. These tools allow you to change the layers of objects in a drawing and extract information from the objects in a drawing as well. More specifically, they allow you to work with blocks that represent an office furniture layout.

Although you might be working in a civil engineering– or mechanical design–related field, these concepts can and do apply to the work you do—just in different ways. Instead of extracting information from a furniture block, you could get and set information in a title block, a callout, or even an elevation marker. Making sure hatching is placed on the correct layers along with dimensions can improve the quality of output for the designs your company creates.

NOTE

The following steps require a drawing file named ch30_building_plan.dwg. If you didn't download the sample files previously, download them now from www.sybex.com/go/autocadcustomization. Place these sample files in the MyCustomFiles folder under the Documents (or My Documents) folder.

The following steps explain how to use the FurnLayers procedure:

Open ch30_building_plan.dwg.

At the Command prompt, type vbarun and press Enter.

When the Macros dialog box opens, select the FurnTools.dvb!basFurnTools.FurnLayers macro from the list and click Run.

At the Select objects: prompt, select all the objects in the drawing and press Enter. The objects in the drawing are placed on the correct layers, and this can be seen as the objects were all previously placed on layer 0 and had a color of white (or black based on the background color of the drawing area).

The following steps explain how to use the FurnBom procedure:

At the Command prompt, type vbarun and press Enter.

When the Macros dialog box opens, select the FurnTools.dvb!basFurnTools.FurnBOM macro from the list and click Run.

At the Select objects: prompt, select all the objects in the drawing. Don't press Enter yet. Notice that the dimension objects aren't highlighted. As a result of the selection set filter being applied with the SelectOnScreen function, the SelectOnScreen function only allows block references (insert object types) to be selected.

Press Enter to end the object selection.

At the Specify upper-left corner of BOM: prompt, specify a point to the right of the furniture layout in the drawing. The bill of materials that represents the furniture blocks is placed in a table grid, as shown Figure 30.6.

Close and discard the changes to the drawing file.

Figure 30.6 Bill of materials generated from the office furniture layout
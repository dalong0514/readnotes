# 2901. Annotating Objects

Annotation plays an important role in most designs; it is used to communicate measurements and design features that might require explanation. The Autodesk® AutoCAD® program offers a variety of annotation objects that include stand-alone text, dimensions, leaders, and tables. Each annotation object type is affected by specially named styles that control its appearance. Blocks can also include attributes, which are a form of annotation that can be updated when an instance of a block reference is inserted into a drawing. I discuss blocks and attributes in Chapter 30,「Working with Blocks and External References.」

In this chapter, you will learn to create and modify stand-alone text objects and other types of annotation objects, such as dimensions, leaders, and tables. Along with creating and modifying annotation objects, you will also learn to control the appearance of annotation objects with named styles and create field values that can be used in multiline text objects and table cells.

Working with Text

Stand-alone text is often used for adding labels below a viewport and detail, general disclaimers, and revision comments. You can create two types of stand-alone text: single-line and multiline. Single-line text (Text) is used when you only need to add a few words or a short comment to a drawing, whereas multiline text (MText) is used when you want to create a bullet list or a paragraph of text.

MText supports a wider range of formatting options and features than single-line text. Even though MText is designed for formatting text in paragraphs, it can be used in place of single-line text. The appearance of stand-alone text is controlled by its assigned text style.

Creating and Modifying Text

Single-line text and MText is represented by the AcadText and AcadMText objects. The AddText function allows you to create a single-line text object based on a text string, an insertion point, and text height. The text height passed to the AddText function is used only if the Height property of the text style assigned to the text object is set to 0. I discuss text styles in the「Controlling Text with Text Styles」section later in this chapter. You use the AddMText function to create a new MText. The AddMText function is similar to the AddText function with one exception: the AddMText function expects a value that defines the width of the bounding box of the text area instead of a value that defines the height of the text object. The following shows the syntax of the AddText and AddMText functions:

retVal = object.AddText(textString, insertionPoint, height) retVal = object.AddMText(insertionPoint, width, textString)

Their arguments are as follows:

retVal The retVal argument represents the new AcadText or AcadMText object returned by the function.

object The object argument represents an AcadModelSpace, AcadpaperSpace, or AcadBlock collection object.

textString The textString argument is a string that contains the text that should be added to the text object. The text string can contain special character sequences to format text and insert special characters; see the「Formatting a Text String」section later in this chapter for some of the supported character sequences.

insertionPoint The insertionPoint argument is an array of three doubles that defines the insertion point of the text object.

height or width The height and width arguments are doubles that define the height of the text for an AcadText object or overall width of the boundary box of an AcadMText object.

The following code statements add two new single-line text objects to model space (see Figure 29.1):

' Defines the insertion point and height for the text object Dim dInsPt(2) As Double, dHeight As Double dInsPt(0) = 0: dInsPt(1) = 0: dInsPt(2) = 0 dHeight = 0.25 ' Creates a new text object Dim oText As AcadText Set oText = ThisDrawing.ModelSpace.AddText( _ "NOTE: ADA requires a minimum turn radius of", dInsPt, dHeight) ' Adjusts the insertion point for the second text object dInsPt(0) = 0: dInsPt(1) = dHeight * -1.6065: dInsPt(2) = 0 Set oText = ThisDrawing.ModelSpace.AddText( _ "60"" (1525mm) diameter for wheelchairs.", dInsPt, dHeight)

Figure 29.1 Basic note created with single-line text

The following code statements add an MText object to model space (see Figure 29.2):

' Defines the insertion point and width for the text object Dim dInsPt(2) As Double, dWidth As Double dInsPt(0) = 0: dInsPt(1) = 0: dInsPt(2) = 0 dWidth = 5.5 ' Creates a new text object Dim oMText As AcadMText Set oMText = ThisDrawing.ModelSpace.AddMText(dInsPt, dWidth, _ "NOTE: ADA requires a minimum turn radius of " & _ "60"" (1525mm) diameter for wheelchairs.")

Figure 29.2 Basic note created with an MText object

The properties of the AcadText and AcadMText objects can be used to adjust the justification of the text, the direction in which the text is drawn, and much more. For information on the properties of the two text objects, see the AutoCAD Help system or the Object Browser in the VBA Editor. Like other graphical objects, the AcadText and AcadMText objects also inherit the properties and methods of an AcadEntity object, which I discussed in Chapter 27,「Creating and Modifying Drawing Objects.」

The following code statements add a new single-line text object to model space and center the text:

' Defines the insertion point and height for the text object Dim dInsPt(2) As Double, dHeight As Double dInsPt(0) = 5: dInsPt(1) = 5: dInsPt(2) = 0 dHeight = 0.25 ' Creates a new text object Dim oText As AcadText Set oText = ThisDrawing.ModelSpace.AddText( _ "Center Justified", dInsPt, dHeight) ' Sets the justification of the text to middle center oText.Alignment = acAlignmentMiddleCenter ' Moves the alignment point of the justified text ' to the original insertion point oText.TextAlignmentPoint = dInsPt

NOTE

After changing the justification of an AcadText object, you will need to update the TextAlignmentPoint property to move the location to the correct position.

In addition to the methods the AcadText and AcadMText objects inherit from an AcadEntity object, the objects also support a function named FieldCode. I explain the FieldCode function in the「Creating Fields」section later in this chapter.

Formatting a Text String

Alphanumeric characters are used to create the text string that an AcadText object displays, but how those characters are arranged can impact how the text appears. The use of the percent symbol has a special meaning in a text string. You use a percent symbol to indicate the use of special control codes and field values. Special control codes can be used to toggle underlining or overscoring for part or all of a text string and to insert special symbols. Table 29.1 lists the control codes that are supported in the text string of an AcadText object.

Table 29.1 Control codes for AcadText objects

Control code Description

%%c Adds a diameter symbol to the text.

%%d Adds a degree symbol to the text.

%%nnn Adds the ASCII character represented by the character value nnn. For example, %%169 adds the Copyright symbol.

%%o Toggles the use of overscoring. The first instance of %%o in a text string turns overscoring on, and the second turns it off.

%%p Adds a plus or minus symbol ( ± ) to the text.

%%u Toggles the use of underscoring. The first instance of %%u in a text string turns underscoring on, and the second turns it off.

%%% Adds a percent symbol to the text.

%< and >% Defines the start and end of a field value. I discuss working with field values in in the「Creating Fields」section later in this chapter.

The text string of an AcadMText object can be very basic, but it can be very complex as well. You can control the formatting of each character in a text string with special control codes. Unlike the special control codes that are supported by an AcadText object, those used by an AcadMText object are much more complicated and harder to figure out at first. However, the AutoCAD list command will be your friend if you want to create complexly formatted text strings.

The best process for learning how to format the text string of an AcadMText object is to use the mtext command in AutoCAD and create a sample text string that you want to create with your VBA macro. Once the MText object is added to the drawing, use the list command and look at the value after the Contents label in the output. For example, the following is an example of the output displayed by the list command for an MText object that contains a numbered list with three items (see Figure 29.3):

Contents: Numbered List\P\pxi-3,l3,t3;1. Item 1\P2. Item 2\P3. Item 3

Figure 29.3 Numbered list in an MText object

The long spaces in the example are actually tab characters. To create the numbered list shown in Figure 29.3 with VBA, the code statements would look like the following:

' Defines the insertion point and width for the MText object Dim dInsPt(2) As Double, dWidth As Double dInsPt(0) = 0: dInsPt(1) = 0: dInsPt(2) = 0 dWidth = 5.5 ' Creates a new MText object with a numbered list Dim oMText As AcadMText Set oMText = ThisDrawing.ModelSpace.AddMText(dInsPt, dWidth, _ "Numbered List\P\pxi-3,l3,t3;1." & vbTab & _ "Item 1\P2." & vbTab & "Item 2\P3." & vbTab & "Item 3")

Most of the control codes you will need to use take a combination of the list and mtext commands to initially figure out, but there a few control codes that are much easier to add to the text string of MText. The AcadMText object supports the %%d, %%c, and %%p control codes that are also supported by the AcadText object. If you want to add a special character to a text string of an AcadMText object, use the control sequence of \U+nnn, which adds a character based on its Unicode value instead of the %%nnn that an AcadText object supports. For example, to insert the Copyright symbol you would use the sequence of \U+00A9.

TIP

You can use the Windows Character Map to get the Unicode value of a character for a specific font. If you need to use a character from the font that isn't assigned to the text style applied to the MText object, you must provide the proper control codes to indicate the font you want to use for that character. For example, the following indicates that the Copyright symbol of the Arial font should be added:

{\fArial|b0|i0|c186|p34;\U+00A9}

As I mentioned before, it is best to use the mtext command to first create an MText object and then use the list command to see the contents of that object. Then you will know the code control codes and sequences required.

Checking Spelling

The AutoCAD Object library doesn't support the ability to check the spelling or grammar of a text string. However, with some help from the Microsoft Word Object library you can check the spelling and grammar of a text string. The following outlines an approach you can take using the Word Object library to check the spelling or grammar of a text string:

Create a Word Document object.

Add the text you want to check.

Perform the spelling and grammar check.

Update the text in the drawing.

Close and discard the changes to the Word Document object.

I introduce how to work with the Word Object library in Chapter 35,「Communicating with Other Applications.」

Controlling Text with Text Styles

Text styles are used to control the appearance of the characters in a text string for an AcadText or AcadMText object. Some of the characteristics that are controlled by a text style are font filename, bold and italic font faces, and character sets. A text style is represented by the AcadTextStyle object, and the text styles stored in a drawing are accessed from the AcadTextStyles collection object. Use the TextStyles property of an AcadDocument or ThisDrawing object to get a reference to the AcadTextStyles collection object.

Creating and Managing Text Styles

New text styles are created with the Add method of the AcadTextStyles collection object. The Add method of the AcadTextStyles collection object requires you to provide the name of the new text style and returns an AcadTextStyle object. The Item method of the AcadTextStyles collection object is used to get an existing text style in the drawing; if the text style doesn't exist, an error is generated. I discuss how to handle errors in Chapter 36,「Handling Errors and Deploying VBA Projects.」

The Item method accepts a string that represents the name of the text style you want to work with or an integer value. The integer value represents the index of the text style in the AcadTextStyles collection object you want to return. The index of the first text style in the drawing starts with 0, and the highest index is one less than the number of text styles in the AcadTextStyles collection object returned by the Count property. If you want to step through all the text styles in the drawing, you can use a For statement.

The following sample code statements check for the existence of a text style named General; if the text style doesn't exist, it is created:

On Error Resume Next ' Gets the TextStyles collection Dim oStyles As AcadTextStyles Set oStyles = ThisDrawing.TextStyles ' Gets the text style named General Dim oStyle As AcadTextStyle Set oStyle = oStyles("General") ' If an error is returned, create the text style If Err Then Err.Clear ' Creates a new text style Set oStyle = oStyles.Add("General") End If

NOTE

Although the Add method won't return an error if a text style with the same name already exists, I recommend using the Item method of the AcadTextStyles collection object to check whether a text style already exists.

After you have an AcadTextStyle object, you can get its current font and character set with the GetFont method. The SetFont method is used to set the font and character set among other settings of the text style. In addition to the GetFont and SetFont methods, you can use the fontFile and BigFontFile properties of the AcadTextStyle object to specify the TrueType font (TTF) and Shape (SHX) file that should be used by the text style. The BigFontFile property is helpful if you need to support the double-byte characters that are used mainly for Asian languages.

If you want text to be drawn at a specific height each time the text style is used, you set the height value to the Height property of the text style. Other properties of a text style allow you to specify the oblique angle and direction in which the text should be drawn, among other settings with the properties of the AcadTextStyle object. For information on the properties of the two text objects, see the AutoCAD Help system or the Object Browser in the VBA Editor.

NOTE

Text styles are used by dimension, mleader, and table styles. If a text style will be used by other named annotation styles, I recommend that you set the Height property of the text style to 0. When you use a height of 0, the referencing named annotation style has control over the final text height.

If you don't need a text style anymore, remove it from a drawing with the Delete method of the AcadTextStyle object and not the Delete method of the AcadTextStyles collection object. The PurgeAll method of an AcadDocument or ThisDrawing object can also be used to remove all unused text styles from a drawing. I discussed the PurgeAll method in Chapter 27.

The following sample code statements set the font of the text style assigned to the oStyle variable, enable boldface, and set the oblique angle to 10:

Dim sFont As String Dim bBold As Boolean, bItalic As Boolean Dim nCharSet As Long Dim nPitchandFamily As Long ' Sets the font, enables boldface, and assigns an ' oblique angle to the style based on the active style ThisDrawing.ActiveTextStyle.GetFont sFont, bBold, _ bItalic, nCharSet, nPitchandFamily oStyle.SetFont "Arial", True, False, nCharSet, nPitchandFamily oStyle.ObliqueAngle = 10

Assigning a Text Style

A text style can be assigned to an object directly or inherited by the active text style of the drawing. You assign a text style to an AcadText or AcadMText object with the StyleName property. The StyleName property returns or accepts a string that represents the name of current or the text style to be assigned. When a new text object is created, the text style applied is inherited from the ActiveTextStyle property of the AcadDocument or ThisDrawing object. The ActiveTextStyle property returns and expects an AcadTextStyle object.

NOTE

As an alternative to the ActiveTextStyle property, you can use the textstyle system variable. The textstyle system variable accepts a string that represents the name of the text style to be inherited by each newly created text object.

The following code statements assign the text style named General to the ActiveTextStyle property:

' Sets the General text style as the active text style Dim oStyle As AcadTextStyle Set oStyle = ThisDrawing.TextStyles("GENERAL") ThisDrawing.ActiveTextStyle = oStyle

Dimensioning Objects

Dimensions are annotation objects that show a measurement value in a drawing. The value in which a dimension displays depends on the type of dimension object created. A dimension can measure the linear distance between two points, the radial value of a circle or an arc, the X or Y value of a coordinate, the angle between two vectors, or the length of an angle. Similar to text objects, the appearance of a dimension is controlled by a dimension style. Dimension objects are graphical objects just like lines and circles, so they inherit properties and methods from AcadEntity. Dimensions also inherit properties from a class named AcadDimension.

Creating Dimensions

Nine types of dimensions can be created with the AutoCAD Object library and VBA. When you want to add a dimension object to a drawing, use one of the functions that begin with the name AddDim. The functions used to add a dimension object can be accessed from an AcadModelSPace, AcadPaperSpace, or AcadBlock collection object. Table 29.2 lists the functions that can be used to add a new dimension object.

Table 29.2 Functions used to create new dimensions

Function Description

AddDim3PointAngular Adds an angular dimension based on three points; same as that created with the dimangular command.

AddDimAligned Adds a linear dimension that is parallel to the two points specified; same as the dimaligned command.

AddDimAngular Adds an angular dimension based on two vectors; same as that created with the dimangular command.

AddDimArc Adds an arc length dimension based on the center of an arc and two points along the arc; same as that created with the dimarc command.

AddDimDiametric Adds a diametric dimension that reflects the diameter of a circle or an arc; same as that created with the dimdiameter command.

AddDimOrdinate Adds an ordinate dimension that displays the X or Y value of a coordinate; same as that created with the dimordinate command.

AddDimRadial Adds a radial dimension that reflects the radius of a circle or an arc; same as that created with the dimradius command.

AddDimRadialLarge Adds a radial dimension with a jogged line that indicates the radius of a circle or arc, but the dimension doesn't start at the center of the object dimensioned; same as that created with the dimjogged command.

AddDimRotated Adds a linear dimension that measures the distance between two points, but the dimension line of the dimension is rotated at a specified value; same as that created with the dimrotated command.

For specifics on the arguments that are required to add a dimension object, see the AutoCAD Help system or the Object Browser in the VBA Editor.

The following code statements add two circles, add a linear dimension between the center points of the two circles with the AddDimRotated function, and finally, add a diameter dimension to one of the circles with the AddDiametric function (see Figure 29.4):

' Defines the center point of the circles Dim dCenPt1(2) As Double, dCenPt2(2) As Double dCenPt1(0) = 2.5: dCenPt1(1) = 1: dCenPt1(2) = 0 dCenPt2(0) = 5.5: dCenPt2(1) = 2: dCenPt2(2) = 0 ' Adds the two circles ThisDrawing.ModelSpace.AddCircle dCenPt1, 0.5 ThisDrawing.ModelSpace.AddCircle dCenPt2, 0.5 ' Adds the linear dimension Dim dDimPlace(2) As Double dDimPlace(0) = dCenPt2(0) - dCenPt1(0) dDimPlace(1) = dCenPt2(1) + 1: dDimPlace(2) = 0 Dim oDimRot As AcadDimRotated Set oDimRot = ThisDrawing.ModelSpace.AddDimRotated( _ dCenPt1, dCenPt2, dDimPlace, 0) ' Adds the diametric dimension Dim vDimChordPt1 As Variant vDimChordPt1 = ThisDrawing.Utility.PolarPoint( _ dCenPt1, -0.7854, 0.5) Dim vDimChordPt2 As Variant vDimChordPt2 = ThisDrawing.Utility.PolarPoint( _ dCenPt1, 0.7854 * 3, 0.5) Dim oDimDia As AcadDimDiametric Set oDimDia = ThisDrawing.ModelSpace.AddDimDiametric( _ vDimChordPt2, vDimChordPt1, 1)

Figure 29.4 Aligned and diametric dimensions showing the measurement values of two circles

After you create a dimension object, you can modify its properties. However, based on the properties that you modify, a dimension override might be applied. For example, if you change the value of the DimensionLineColor property and later make a change to the dimension style applied to the dimension, the color of the dimension line will not be updated unless you remove the override from the dimension.

NOTE

Dimensions created with the AutoCAD Object library are not associative; the dimension isn't updated if the objects that the dimension measures are changed. If you want to create associative dimensions, consider using the SendCommand or PostCommand method with the appropriate command sequence.

Formatting Dimensions with Styles

Dimension styles are stored in and accessed from the AcadDimStyles collection object. Each dimension style in a drawing is represented by an AcadDimStyle object. A new dimension style can be added to a drawing with the Add method of the collection object. The Add method expects a string that contains the name of the new dimension type to be created and returns an AcadDimStyle object. The Item method of the AcadDimStyles collection object is used to get an existing dimension style in the drawing; if the dimension style doesn't exist, an error is generated. I discuss how to handle errors in Chapter 36.

The Item method accepts a string that represents the name of the dimension style you want to work with or an integer value. The integer value represents the index of the dimension style in the AcadDimStyles collection object you want to return. The index of the first dimension style in the drawing starts with 0, and the highest index is one less than the number of dimension styles in the AcadDimStyles collection object returned by the Count property. If you want to step through all the dimension styles in the drawing, you can use a For statement.

The following sample code statements check for the existence of a dimension style named Arch24; if the dimension style doesn't exist, it is created:

On Error Resume Next ' Gets the DimStyles collection Dim oStyles As AcadDimStyles Set oStyles = ThisDrawing.DimStyles ' Gets the dimension style named Arch24 Dim oStyle As AcadDimStyle Set oStyle = oStyles("Arch24") ' If an error is returned, create the dimension style If Err Then Err.Clear ' Creates a new dimension style Set oStyle = oStyles.Add("Arch24") End If

NOTE

Although the Add method won't return an error if a text style with the same name already exists, I recommend using the Item method of the AcadDimStyles collection object to check to see whether a dimension style already exists.

After you create or decide to modify an AcadDimStyle object, how to go about modifying the dimension style might not be immediately obvious. From the AutoCAD user interface, you commonly would use the Dimension Style Manager (displayed with the ddim command), but at the Command prompt, you could use the -dimstyle command.

Although you could use the -dimstyle command, the workflow with VBA is to modify the values of dimension-related system variables with the SetVariable method of an AcadDocument or a ThisDrawing object, and then use the CopyFrom method of the AcadDimStyle object to copy the values of the dimension system variables to the dimension style. Modifying the dimension system variables of a drawing will result in the creation of drawing-level dimension overrides. When creating a new dimension variable, I recommend storing the name of the current dimension style so it can be restored after you modify your dimension style.

Now, there is a problem that isn't easy to resolve: the preservation of drawing-level dimension overrides when modifying an existing dimension style. The reason is that when a dimension style is set as active, the previous drawing-level dimension variable overrides are lost. It is always best to restore the previous state of a drawing if you don't want to affect the current settings for the user.

The only way to preserve drawing-level dimension variable overrides is to create an array containing the current value of all dimension variables and then restore the values after the previous style has been set as active. An example of storing and restoring system variables for a number of system variables is shown in the「Setting the Values of Drafting-Related System Variables and Preferences」section of Chapter 26,「Interacting with the Application and Documents Objects.」

Here are code statements that demonstrate how to change the values of the dimblk and dimscale dimension system variables, copy the values of the dimension variables of the drawing to the dimension style named Arch24, and then restore the previous dimension style and dimension values:

' Store the current dimension style Dim oCurDimStyle As AcadDimStyle Set oCurDimStyle = ThisDrawing.ActiveDimStyle ' Store current values to override Dim vValues(1) As Variant vValues(0) = ThisDrawing.GetVariable("DIMBLK") vValues(1) = ThisDrawing.GetVariable("DIMSCALE") ' Change the DIMBLK and DIMSCALE system variable for the drawing ThisDrawing.SetVariable "DIMBLK", "ARCHTICK" ThisDrawing.SetVariable "DIMSCALE", 24# ' Create the new dimension style and copy the variable values from the drawing oStyle.CopyFrom ThisDrawing ' Restore the previous style Set ThisDrawing.ActiveDimStyle = oCurDimStyle ' Restore the values of the overridden variables If vValues(0) = "" Then ThisDrawing.SetVariable "DIMBLK", "." Else ThisDrawing.SetVariable "DIMBLK", vValues(0) End If ThisDrawing.SetVariable "DIMSCALE", vValues(1)

If you don't need a dimension style anymore, remove it from a drawing with the Delete method of the AcadDimStyle object and not the Delete method of the AcadDimStyles collection object. The PurgeAll method of an AcadDocument or ThisDrawing object can also be used to remove all unused dimension styles from a drawing. I discussed the PurgeAll method in Chapter 27.

Assigning a Dimension Style

You can change the dimension style of a dimension object after it has been added to a drawing with the StyleName property. The StyleName property returns or accepts a string that represents the name of the current or dimension style to be assigned. When a new dimension object is created, the dimension style applied is inherited from the ActiveDimStyle property of the AcadDocument or ThisDrawing object. The ActiveDimStyle property returns and expects an AcadDimStyle object.

NOTE

Unlike other Active* properties, the ActiveDimStyle property doesn't have a system variable alternative that can be used to set the default dimension style for new dimension objects. The dimstyle system variable can be used to get the name of the current dimension style.

The following code statements assign the dimension style named Arch24 to the ActiveDimStyle property:

' Sets the Arch24 text style as the active dimension style Dim oStyle As AcadDimStyle Set oStyle = ThisDrawing.DimStyles("ARCH24") ThisDrawing.ActiveDimStyle = oStyle

Creating and Modifying Geometric Tolerances

Geometric tolerances, also referred to as control frames, are used to display acceptable deviations of a form, location, or other measurements in mechanical designs. A geometric tolerance is represented by an AcadTolerance object. Similar to AcadMText objects, AcadTolerance objects accept text strings with control codes in them to define the appearance of the final object that is displayed in the drawing. The control codes that an AcadTolerance object accepts define the symbols, tolerance, and datum values that are displayed in the geometric tolerance object. I recommend using the AutoCAD tolerance and list commands to learn the control codes and text sequences that go into defining a geometric tolerance object.

The following is an example of the output displayed by the list command for a geometric tolerance object that contains a Parallelism symbol, with a tolerance value of 0.00125 and a datum value of B (see Figure 29.5).

Text {\Fgdt;f}%%v{\Fgdt;n}.00125%%v%%vB%%v%%v

Figure 29.5 Geometric tolerance object created with the AddTolerance function

To create a geometric tolerance value, use the AddTolerance function of an AcadModelSpace, AcadPaperSpace, or AcadBlock collection object. The geometric tolerance object shown in Figure 29.5 can be created with the following code statements:

' Defines the insertion point and direction vector ' for the Tolerance object Dim dInsPt(2) As Double, dDirVec(2) As Double dInsPt(0) = 2.5: dInsPt(1) = 2.5: dInsPt(2) = 0 dDirVec(0) = 1: dDirVec(1) = 0: dDirVec(2) = 0 ' Creates a new Tolerance object Dim oTol As AcadTolerance Set oTol = ThisDrawing.ModelSpace.AddTolerance( _ "{\Fgdt;f}%%v{\Fgdt;n}.00125%%v%%vB%%v%%v", dInsPt, dDirVec)

The text string, insertion point, and direction among other characteristics of a geometric object can be queried or modified using the properties and methods of the AcadTolerance object. Like AcadDimension objects, an AcadTolerance object inherits the way it looks by the dimension style it is assigned. When initially created, the geometric tolerance object is assigned the dimension style that is assigned to the ActiveDimStyle property, and the StyleName property of an AcadTolerance object can be used to assign the object a specific dimension style.

If you need to use geometric tolerance objects in your drawings, see the AutoCAD Help system or Object Browser in the VBA Editor for more information.

Adding Leaders

Leaders, also known as callouts, are used to bring attention to a feature in a drawing. A leader starts with an arrowhead that is connected to multiple straight segments or a spline. The end of a leader often includes an attachment: a text object that contains a label or descriptive text. An attachment could also be a geometric tolerance object or block reference. AutoCAD supports two types of leaders: multileader and legacy.

Multileaders are leaders that can be made up of multiple leader lines and one or more attachments. The attachment and leader lines behave as a single object with multileaders. Legacy leaders don't provide as much flexibility as multileaders. Leader lines and the attachment of a legacy leader can be connected to or separate from the leader object.

Working with Multileaders

Multileaders were introduced in AutoCAD 2008 to improve the workflow when working with leaders. A multileader object is represented by the AcadMLeader object in a drawing file. Their initial appearance is controlled by a multileader style. The methods and properties of an AcadMLeader object allow you to add and modify leader lines and the content of a multileader object.

In addition to modifying a multileader object as a whole, you can modify the appearance of each leader line attached to the multileader object. Along with methods and properties specific to the AcadMLeader object, an AcadMLeader object inherits properties and methods from an AcadEntity.

Placing and Modifying Multileaders

A multileader object is created with the AddMLeader function. The AddMLeader method is available from an AcadModelSpace, AcadPaperSpace, or AcadBlock collection object and returns an AcadMLeader object. When you create a leader with the AddMLeader function, you specify the vertices of the initial leader line for the multileader. The AddMLeader function also returns an index for the leader line. which is represented by an AcadMLeaderLeader.

When a multileader is added to a drawing, its appearance is inherited by the active multileader style. I explain how to define and manage multileader styles in the next section,「Defining Multileader Styles.」You will learn to apply a named multileader style in the「Assigning a Multileader Style」section.

The following code statements add a multileader with two leader lines and an attachment object of MText (see Figure 29.6):

' Defines the points of the first leader Dim dLeader1Pts(0 To 5) As Double dLeader1Pts(0) = 0.1326: dLeader1Pts(1) = 0.1326: dLeader1Pts(2) = 0 dLeader1Pts(3) = 1.1246: dLeader1Pts(4) = 2.1246: dLeader1Pts(5) = 0 ' Defines the points of the second leader Dim dLeader2Pts(0 To 5) As Double dLeader2Pts(0) = 0.1847: dLeader2Pts(1) = 1.7826: dLeader2Pts(2) = 0 dLeader2Pts(3) = 1.1246: dLeader2Pts(4) = 2.1246: dLeader2Pts(5) = 0 ' Adds the new multileader object Dim lLeaderIdx As Long Dim oMLeader As AcadMLeader Set oMLeader = ThisDrawing.ModelSpace.AddMLeader(dLeader1Pts, lLeaderIdx) ' Adds the second leader line oMLeader.AddLeaderLine lLeaderIdx, dLeader2Pts ' Attaches the MText object oMLeader.ContentType = acMTextContent oMLeader.TextString = "3/16""R"

Figure 29.6 Multileader with two leader lines

After placing a multileader object, you can refine the leader lines, content, and appearance of the object using its methods and properties. However, depending on the properties that you modify, a style override might be applied. For example, if you change the value of the ArrowheadBlock property and later make a change to the multileader style applied to the object, the arrowhead of the leader lines will not be updated unless you remove the Xdata attached to the multileader that represents the data associated with the override. I explain more about Xdata in Chapter 32,「Storing and Retrieving Custom Data.」

Defining Multileader Styles


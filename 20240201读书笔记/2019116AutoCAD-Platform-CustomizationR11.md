## 记忆时间

## 目录

0101 Establishing the Foundation for Drawing Standards

0103 Building the Real World One Block at a Time

## 0101. Establishing the Foundation for Drawing Standards

Well-established drawing standards ensure that your drawings all look the same when they are presented to the client, and they can make it easier to: Train new drafters and other professionals on your company's standards that use AutoCAD; Identify which drawing and externally referenced files are associated with a project; Determine the purpose of a named object in a drawing; Share project files with clients and contractors because your standards are well defined.

## 0103. Building the Real World One Block at a Time

定义块、修改块；提取块内的数据信息。

3『

在 18 章看到这么一段话。然后在 17 章里找到一小节「Creating the Room Label Block Definition」。

In Chapter 17, you created a set of functions that allowed you to extract the attributes of a block and then quantify the results before creating the BOM in the drawing. Here, you will create a function named furnbomexport that allows you to export the BOM data generated with the extAttsFurnBOM function output to an external file instead of adding it to the drawing as a table grid as you did with the furnbom function.

』

Instead of dedicating time to re-create the geometry each time, you can create the objects once and store them as a block definition. Block definitions are another type of nongraphical object that can be in a drawing, much like text and dimension styles.

3『[AutoCAD 2019 帮助: 关于定义块](http://help.autodesk.com/view/ACD/2019/CHS/?guid=GUID-F81D7F1E-1F0A-45AD-AC7E-891A85A0033A)』

In addition to geometric objects, block definitions can contain attribute definitions, which allow you to embed information into a block. The information stored in attributes can be extracted to an external file or added to a table in a drawing.

Block definitions must be defined in a drawing before you can create (or, as commonly known, insert) a block reference. A block reference object specifies where and how the objects from a block definition should be drawn onscreen or plotted. You typically create block definitions by first adding the geometry for your block in model space and then using the block command to define which objects will make up the block definition. AutoCAD also offers a special environment called the Block Editor (bedit command) for working with block definitions. Once a block definition is defined, you can use the insert command to create a block reference of a block definition. when defining a block you must consider the following:

1 Name. The name of a block definition is used to differentiate one from another; each block definition in a drawing must have a unique name. Drawings can easily contain hundreds and even thousands of block definitions. When naming block definitions, use descriptive names, but don't make them so long that the user must carefully read a sentence-long name. I discussed naming blocks and other nongraphical objects in Chapter 2,「Working with Nongraphical Objects.」

2 Base (or Insertion). Point The base point for a block definition is similar to a drawing's origin. This point is used as a block reference's insertion point, the same point that is used to drag a preview of the block onscreen with the insert command. You typically specify the base point of a block on one of the objects in the block definition, such as an endpoint or intersection of two objects.

3 Objects. The objects that make up the block definition determine how the block references inserted into a drawing will look and behave. Objects within a drawing include geometry objects such as lines, circles, arcs, and even other blocks. Blocks can also include special objects known as attribute definitions, which allow you to add to a block information such as a project name or part number. I discuss attributes in the section「Embedding Information in a Block Definition with Attributes」later in this chapter.

Block definitions can contain attributes that allow you to add custom information to a block reference when it is inserted into a drawing. Using attributes allows you to use a single block definition but represent several items that might be the same size and a different color or style. A common use for attributes is to store project, date, and revision information in a title block, or a model number and description with a window or bolt block. After you insert a block reference with attributes, you can extract the values stored in the attributes to an external file or table object.

There are two types of attributes in a drawing. Those in a block definition are known as attribute definitions. The other type of attribute is known as an attribute reference, which can be found attached to a block reference that has been inserted into a drawing whose block definition contains attribute definitions.

1『两类属性，attribute definitions 和 attribute reference。』

You can create attribute definitions by using the Attribute Definition dialog box (attdef command). You can add an attribute definition to model space or paper space before you define your block definition by using the Block Definition (Windows) or Define Block (Mac OS) dialog box (block command), or after a block definition is created in the Block Editor (bedit command). The following steps explain how to add an attribute definition, whether you are working in the drawing window or the Block Editor:

Invisible: The attribute is invisible when a block reference is inserted into the drawing. All invisible attributes can be displayed by setting the attmode system variable to a value of 2;  Constant: The text string entered in the Value text box of the attribute is fixed and is the same for all block references that are inserted based on the block definition that contains this type of attribute;  Verify: You are prompted to verify the value of the attribute when the block reference is inserted.

Preset: The Default value is assigned to the attribute when the block reference is inserted, and you are not prompted to change the value. You can change the value using the attedit or eattedit command or the Properties palette (Windows) or Properties Inspector (Mac OS); Lock Position: Restricts the attribute from being moved using grips. This mode is helpful if you want to control the placement of an attribute with parameters and actions in a dynamic block.

NOTE: While AutoCAD remains open, the Mode options you choose are stored as a sum of different bitcode values in the aflags system variable. The value of aflags is used as the default option for the next attribute definition you create.

NOTE: When you are selecting objects to define a block definition, the order in which you select your attribute definitions affects how AutoCAD prompts for each attribute value. I recommend selecting all your graphical objects first, and then selecting each attribute definition in the order you want its value to be prompted for. Prompting order can have an impact on your block's usage with scripts, menu macros, and other custom programs. You can also change the prompting order of the attributes in a block by using the Block Attribute Manager (battman command).

1『这点很重要，定义块的时候，选择顺序先选图形元素，然后再选属性。作者的意思这对后面使用 autolisp 有好处。』

Just as it is not uncommon to make changes to the way a block looks over time, you might decide to update the attribute definitions in a block definition. There are a few things you need to consider when adding, modifying, or removing attribute definitions from a block definition. Although it is true that the geometry of a block definition is the same for each and every block reference that uses a specific block definition, the same is not true for attribute definitions and references unless all your attribute definitions are defined as Constant.

Some blocks based on the same block definition may not have all the attributes defined in that block definition. This situation often occurs when attributes in a block definition are updated but the block references themselves are not synchronized to include the same changes, or when a custom application has decided not to add an attribute reference to a block reference for some reason.

After you update the attributes of a block definition, you want to run the attredef or attsync command or use the Block Attribute Manager (battman command). These utilities synchronize the attribute definitions in a block definition with the attribute references in each of the block references that have been inserted in a drawing by adding and removing attributes as needed. Those attributes in the block reference that are contained in the block definition are not changed; their current values are retained.

The Block Attribute Manager (battman command) can also be helpful in updating the properties and prompting order of the attribute definitions in a block definition, as well as editing and removing attribute definitions. These three commands can also affect any formatting or property changes made to attributes in a block reference with the attedit and eattedit commands. If you need to just change the prompting order of the attributes within a block definition, you can use the battorder command while the block definition is open in the Block Editor (bedit command).

1『修改块属性可以用命令 attredef 或者 attsync。』

Using Fields with Attributes. Fields allow you to place information in your drawing based on a graphical or nongraphical drawing object, the current value of a system variable, a property of a sheet set or project, the current date or the date when the current drawing was created, and much more. Fields can be used to construct the string value of a single-line or multiline text object, which can be a standalone object or in another object such as a table or dimension. In addition to text objects, attributes can use fields to define the value that they hold. Use the following steps to define an attribute definition with a field:

2『 Fields 感觉是在定义属性时看到的「字段」，待确认。』

When you insert a block reference with an attribute, you can specify a field value in the Edit Attributes dialog box by right-clicking in the text box to the right of the attribute prompt and clicking Insert Field. You can edit an existing field by double-clicking the shaded text in the text box, or you can convert it to static text by selecting and right-clicking the shaded text that represents the field and clicking Convert Field To Text.

BlockPlaceholder Field Type. In AutoCAD on Windows while the Block Editor is active, you have access to an additional field type: BlockPlaceholder. The BlockPlaceholder field type allows you to access the properties of the block reference when it is placed in a drawing. For example, you could list the name of the block as part of a description in an attribute field or even access the current value of one of the parameters used for a custom dynamic property.

Dynamic properties when added to a block definition allow you to rotate, move, stretch, and perform other actions on the objects within a block reference. A block definition that contains dynamic properties is known as a dynamic block. Parameters and actions are used to implement dynamic properties. You can only add dynamic properties to a block definition using the Block Editor in AutoCAD on Windows. Although you can't create or modify dynamic properties in AutoCAD for Mac OS, you can insert blocks that have these properties already implemented.

When a block with dynamic properties is inserted into a drawing, additional grips are displayed for the block reference when it is selected. These additional grips allow you to interactively change the values of the custom actions rather than selecting values from a predefined list. Figure 3.7 shows a block reference selected in the drawing and a linear distance being modified with grips.

One of the benefits of using attributes with your blocks is that you can extract the information and then use it in your drawing or an external program. If all of your blocks contain attributes, you could generate a bill of materials on demand or even help prepare an estimate for a project. The attribute values and the properties of the blocks containing attributes can be extracted from a drawing using the Attribute Extraction dialog box (attext command) or Data Extraction Wizard (attext command) (in AutoCAD on Windows only) or by using the -attext command at the command prompt in AutoCAD both on Windows and Mac OS. The following steps explain how to extract the attributes from a drawing using the Data Extraction Wizard in AutoCAD on Windows:

1『 dataextraction 命令可以提取实体对象里的各个数据，可以筛选出块的属性信息，可以导出成 csv、txt 等格式。可以说这个命令可以满足我想要做数据分析所需的数据源了，哈哈；用命令 -attext 可以直接提取属性信息，但需要一个模板，没有 dataextraction 方便。』

NOTE: After you place a table using the Data Extraction Wizard, a Data Link icon that looks like two chain links appears in the application's status-bar tray. Right-click the icon or the table in the drawing, and click Update All Data Links to ensure the information displayed in the table is up to date.
# 2019116AutoCAD-Platform-CustomizationR00

## 记忆时间

## 卡片

### 0101. 反常识卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## Introduction

In 1996, Lee began learning the core concepts of customizing the AutoCAD user interface and AutoLISP. The introduction of VBA in AutoCAD R14 would once again redefine how Lee approached programming solutions for AutoCAD. VBA made it much easier to communicate with external databases and other applications that supported VBA. It transformed the way information could be moved between project management and manufacturing systems.

Not being content with VBA, in 1999 Lee attended his first Autodesk University and began to learn ObjectARX®. Autodesk University had a lasting impression on him. In 2001, he started helping as a lab assistant. He began presenting on customizing and programming AutoCAD at the event in 2004. Along the way he learned how to use the AutoCAD Managed.NET API.

Customization is one of the feature areas that sets AutoCAD apart from many other CAD programs. Even though the product can be used out of the box, configuring the user interface and modifying the support files that come with the product can greatly improve your productivity. By customizing AutoCAD, you can streamline product workflows and create new ones that are a better fit with the way your company works. These workflows might range from importing layers and styles into a drawing to the extraction of drawing-based information into a spreadsheet or database.

The AutoLISP programming language can be used to: Create custom functions that can be executed from the AutoCAD Command prompt; Create and manipulate graphical objects in a drawing, such as lines, circles, and arcs; Create and manipulate nongraphical objects in a drawing, such as layers, dimension styles, and named views; Perform mathematical and geometric calculations; Request input from or display messages to the user at the Command prompt; Interact with files and directories in the operating system; Read from and write to external files; Connect to applications that support ActiveX and COM; Display dialog boxes and get input from the end user.

AutoLISP code can be entered directly at the Command prompt or loaded using a LSP file. Once an AutoLISP program has been loaded, you can execute the custom functions from the Command prompt. Functions executed from the Command prompt can be similar to standard AutoCAD commands, but the programmer determines the prompts that should be displayed. It is also possible to use AutoLISP code with a command macro that is activated from the AutoCAD user interface or a tool on a tool palette.

1『VBA 能实现的功能同上。』

VBA code statements are entered into the Visual Basic Editor and stored in a DVB file. Once a VBA project has been loaded, you can execute the macros through the Macros dialog box. Unlike standard AutoCAD commands, macros cannot be executed from the Command prompt, but once executed, a macro can prompt users for values at the Command prompt or with a user form. It is possible to execute a macro from a command macro that is activated with a command button displayed in the AutoCAD user interface or as a tool on a tool palette.

Part I: AutoCAD Customization: Increasing Productivity through Personalization

Chapter 1: Establishing the Foundation for Drawing Standards In this chapter, you'll learn how to establish drawing standards. Drawing standards allow you to enforce consistency across multiple drawings. By enforcing a set of standards, you can easily share your drawings and make them look the same when plotting them.

Chapter 2: Working with Nongraphical Objects In this chapter, you'll learn how nongraphical objects affect display and output of objects in a drawing. Nongraphical objects such as layers and text styles make it easy to update the look of all the objects that reference them.

Chapter 3: Building the Real World One Block at a Time In this chapter, you'll learn how to create and manage blocks. Blocks allow you to logically create object groupings that can be used several times in the same drawing. For example, you could create a small assembly of parts and insert it more than once in a drawing. If the assembly changes, you just need to update the block and all instances of that block are changed.

Chapter 4: Manipulating the Drawing Environment In this chapter, you'll learn how to change the AutoCAD drawing environment. During start up, you can control several of the settings that affect the AutoCAD program. These settings can affect the display of the user interface, behavior of tools in the drawing environment, and where AutoCAD looks for support files.

Chapter 5: Customizing the AutoCAD User Interface for Windows In this chapter, you'll learn how to customize the elements and display of the AutoCAD user interface on Windows. The Customize User Interface (CUI) Editor allows you to create and manage the tools that are displayed by the AutoCAD user interface.

Chapter 6: Customizing the AutoCAD User Interface for Mac In this chapter, you'll learn how to customize the elements and display of the AutoCAD user interface on Mac OS. The Customize dialog box allows you to create and manage the tools displayed by the AutoCAD user interface.

Chapter 7: Creating Tools and Tool Palettes In this chapter, you'll learn how to create and customize tool palettes in AutoCAD on Windows. Tool palettes allow you to create a visual set of tools that can be used to insert blocks, start commands, or even hatch a closed area. Tool palettes are available on Windows only.

Chapter 8: Automating Repetitive Tasks In this chapter, you will learn how to create scripts and action macros to automate repetitive tasks. Script files and action macros allow you to combine multiple commands into simple logical sequences without needing to know a programming language. Action macros are supported on Windows only.

Chapter 9: Defining Shapes, Linetypes, and Hatch Patterns In this chapter, you will learn how to create custom shapes, linetypes, and hatch patterns that you can use to control the way line work appears in a drawing. The AutoCAD install provides a limited number of standard shapes, linetypes, and hatch patterns. You can extend the standard definitions by creating your own shapes, linetypes, and hatch patterns for use in your drawings.

Chapter 10: Using, Loading, and Managing Custom Files In this chapter, you will learn how to use, manage, and migrate custom files. After you have spent the time customizing AutoCAD, all you have left to do is deploy and manage your files.

Part II: AutoLISP: Productivity through Programming

Chapter 11: Quick Start for New AutoLISP Programmers In this chapter, you'll get an introduction to the AutoLISP programming language. I begin by showing you how to enter AutoLISP expressions at the Command prompt and execute standard AutoCAD commands. After that, you are eased into some basic programming concepts that allow you to perform conditional tests and repeat expressions. The chapter wraps up with creating and loading an AutoLISP file into the AutoCAD program.

Chapter 12: Understanding AutoLISP In this chapter, you'll learn the fundamentals of the AutoLISP programming language. AutoLISP fundamentals include a look at the syntax and structure of an expression, how to use a function, and how to work with variables. Beyond just syntax and variables, you learn to use AutoCAD commands and group multiple AutoLISP expressions into custom functions.

Chapter 13: Calculating and Working with Values In this chapter, you'll learn to work with mathematical and string manipulation functions. Math functions allow you to perform basic and advanced calculations based on object values or a value that the user might provide, whereas string manipulation functions allow you to work with text-based values. Both numeric and textual values are used when creating or manipulating objects, adding annotations to a drawing, or displaying a message to the end user. Based on how the values are used, numeric values can be converted to strings and strings can be converted to numeric values.

Chapter 14: Working with Lists In this chapter, you'll learn to work with the list data type. Lists are used throughout AutoLISP to provide 2D or 3D coordinate values or to define an object stored in a drawing.

Chapter 15: Requesting Input, and Using Conditional and Looping Expressions In this chapter, you'll learn to request input from the user, use conditional statements, and repeat expressions. Requesting input allows you to get values from the user and then use those values to determine the end result of the program. Conditional statements enable a program to make choices based on known conditions in a drawing or input from a user. After you understand conditional statements, you will learn to use them in conjunction with looping expressions to execute a set of expressions until a condition is met.

Chapter 16: Creating and Modifying Graphical Objects In this chapter, you'll learn how to create, modify, and attach extended data to graphical objects using AutoCAD commands and AutoLISP functions. Graphical objects represent the drawing objects, such as a line, an arc, or a circle, that are displayed in model space or on a named layout. When modifying objects, you can choose to step through all the objects in a drawing or let the user select the objects to be modified. Extended data allows you to store information with an object that can be used to identify the objects your program creates or link objects to external database records.

Chapter 17: Creating and Modifying Nongraphical Objects In this chapter, you'll learn how to create and modify nongraphical objects using AutoCAD commands and AutoLISP functions. Nongraphical objects are used to control the appearance of graphical objects and store settings that affect the behavior of features in the AutoCAD program. Drawings support two different types of nongraphical objects: symbol table objects and dictionaries.

Chapter 18: Working with the Operating System and External Files In this chapter, you will learn how to work with settings and files stored outside of the AutoCAD program. Settings can be stored in the Windows Registry and Plist files on Mac OS, and they can be used to affect the behavior of the AutoCAD program or persist values for your custom programs between AutoCAD sessions. Files and folders stored in the operating system can be accessed and manipulated from the AutoCAD program, which allows you to set up project folders or populate project information in the title block of a drawing from an external file.

2『 16 和18 章里应该有，将数据导出的相关信息。结果发现 17 章里也有这方面的信息。最终竟然在第 3 章里找到解决办法，直接用命令 dataextraction 就可以提取块里面的属性信息，以 csv 或 txt 格式导出来。』

Chapter 19: Catching and Handling Errors In this chapter, you will learn how to catch and handle errors that are caused by an AutoLISP function and keep an AutoLISP program from terminating early. AutoLISP provides functions that allow you to trace a function, see arguments as they are passed, catch an error and determine how it should be handled, and group functions together so all the actions performed can be rolled back as a single operation.

Chapter 20: Authoring, Managing, and Loading AutoLISP Programs In this chapter, you will learn how to store AutoLISP code statements in a file, load and manage AutoLISP files, and deploy custom programs with plug-in bundles. Storing AutoLISP code in a file allows for its reuse in multiple drawings. When you load an AutoLISP file, all of the functions defined in the file are made available while the drawing remains open. Based on how you load or deploy an AutoLISP file, you might need to let the AutoCAD program know where your AutoLISP files are stored.

Chapter 21: Using the Visual LISP Editor (Windows only) In this chapter, you will learn how to use the Visual LISP® Editor. The editor provides tools for writing, formatting, validating, and debugging code in an AutoLISP file. Using the Visual LISP Editor, you can group AutoLISP files into project files, which make them easy to manage and compile. Compiling an AutoLISP file secures the source code contained in the file so that it can't be altered by others.

Chapter 22: Working with ActiveX/COM Libraries (Windows only) In this chapter, you will learn how to use ActiveX/COM libraries with AutoLISP. ActiveX provides access to additional functions, which allow for the creation and manipulation of drawing objects and AutoCAD application settings that aren't easily accessible with standard AutoLISP functions. External applications, such as Microsoft Word and Excel, can also be accessed from the AutoCAD program when using ActiveX.

Chapter 23: Implementing Dialog Boxes (Windows only) In this chapter, you will learn how to create and use dialog boxes with an AutoLISP program. Dialog boxes provide an alternative method of requesting input from the user and are implemented using Dialog Control Language (DCL).

Part III: AutoCAD VBA: Programming with VBA and ActiveX (Windows only)

Chapter 24: Understanding the AutoCAD VBA Environment In this chapter, you'll get an introduction to the Visual Basic Editor. I begin by showing you how to verify whether the VBA environment for AutoCAD has been installed and, if not, how to install it. After that, you are eased into navigating the Visual Basic Editor and managing VBA programs. The chapter wraps up with learning how to execute macros and access the help documentation.

Chapter 25: Understanding Visual Basic for Applications In this chapter, you'll learn the fundamentals of the VBA programming language and how to work with objects. VBA fundamentals include a look at the syntax and structure of a statement, how to use a function, and how to work with variables. Beyond syntax and variables, you learn to group multiple statements into custom procedure.

Chapter 26: Interacting with the Application and Documents Objects In this chapter, you'll learn to work with the AutoCAD application and manage documents. Many of the tasks you perform with an AutoCAD VBA program require you to work with either the application or a document. For example, you can get the objects in a drawing and even access end-user preferences. Although you typically work with the current document, VBA allows you to work with all open documents and create new documents. From the current document, you can execute commands and work with system variables from within a VBA program, which allows you to leverage and apply your knowledge of working with commands and system variables.

Chapter 27: Creating and Modifying Drawing Objects In this chapter, you'll learn to create and modify graphical objects in model space with VBA. Graphical objects represent the drawing objects, such as a line, an arc, or a circle. The methods and properties of an object are used to modify and obtain information about the object. When working with the objects in a drawing, you can get a single object or step through all objects in a drawing.

Chapter 28: Interacting with the User and Controlling the Current View In this chapter, you'll learn to request input from an end-user and manipulate the current view of a drawing. Based on the values provided by the end-user, you can then determine the end result of the program. You can evaluate the objects created or consider how a drawing will be output, and use that information to create named views and adjust the current view in which objects are displayed.

Chapter 29: Annotating Objects In this chapter, you'll learn how to create and modify annotation objects. Typically, annotation objects are not part of the final product that is built or manufactured based on the design in the drawing. Rather, annotation objects are used to communicate the features and measurements of a design. Annotation can be a single line of text that is used as a callout for a leader, a dimension that indicates the distance between two drill holes, or a table that contains quantities and information about the windows and doors in a design.

Chapter 30: Working with Blocks and External References In this chapter, you'll learn how to create, modify, and manage block definitions. Model space in a drawing is a special named block definition, so working with block definitions will feel familiar. Once you create a block definition, you will learn how to insert a block reference and work with attributes along with dynamic properties. You complete the chapter by learning how to work with externally referenced files.

Chapter 31: Outputting Drawings In this chapter, you will learn how to output the graphical objects in model space or on a named layout to a printer, plotter, or electronic file. Named layouts will be used to organize graphical objects for output, including title blocks, annotation, floating viewports, and many others. Floating viewports will be used to control the display of objects from model space on a layout at a specific scale. After you define and configure a layout, you learn to plot and preview a layout. The chapter wraps up with learning how to export and import file formats.

Chapter 32: Storing and Retrieving Custom Data In this chapter, you will learn how to store custom information in a drawing or in the Windows Registry. Using extended data (Xdata), you will be able to store information that can be used to identify a graphical object created by your program or define a link to a record in an external database. In addition to attaching information to an object, you can store data in a custom dictionary that isn't attached to a specific graphical object in a drawing. Both Xdata and custom dictionaries can be helpful in making information available between drawing sessions; the Windows Registry can persist data between sessions.

Chapter 33: Modifying the Application and Working with Events In this chapter, you will learn how to customize and manipulate the AutoCAD user interface. You also learn how to load and access externally defined custom programs and work with events. Events allow you to respond to an action that is performed by the end-user or the AutoCAD application. There are three main types of events that you can respond to: application, document, and object.

Chapter 34: Creating and Displaying User Forms In this chapter, you will learn how to create and display user forms. User forms provide a more visual approach to requesting input from the user.

Chapter 35: Communicating with Other Applications In this chapter, you will learn how to work with libraries provided by other applications. These libraries can be used to access features of the Windows operating system, read and write content in an external text or XML file, and even work with the applications that make up Microsoft Office.

1『这章涉及与其他 app 的交互，那么有提取 cad 数据直接进服务器的实现线索。（2020-06-25）』

Chapter 36: Handling Errors and Deploying VBA Projects In this chapter, you will learn how to catch and handle errors that are caused by the incorrect use of a function or the improper handling of a value that is returned by a function. The Visual Basic Editor provides tools that allow you to debug code statements, evaluate values assigned to user-defined variables, identify where within a program an error has occurred, and determine how errors should be handled. The chapter wraps everything up with learning how to deploy a VBA project on other workstations for use by individuals at your company.

Bonus Chapter 1: Working with 2D Objects and Object Properties In this chapter, you build on the concepts covered in Chapter 27,「Creating and Modifying Drawing Objects.」You will learn to create additional types of 2D objects and use advanced methods of modifying objects, you also learn to work with complex 2D objects, such as regions and hatch fills. The management of layers and linetypes and the control of the appearance of objects are also covered.

Bonus Chapter 2: Modeling in 3D Space In this chapter, you learn to work with objects in 3D space, and 3D objects. 3D objects can be used to create a model of a drawing which can be used to help visualize a design or detect potential design problems. 3D objects can be viewed from different angles and used to generate 2D views of a model that can be used to create assembly directions or shop drawings.

Bonus Chapter 3: Development Resources In this chapter, you discover resources that can help expand the skills you develop from this book or locate an answer to a problem you might encounter. I cover development resources, places you might be able to obtain instructor-led training, and interact with fellow users on extending AutoCAD. The online resources sites listed cover general customization, AutoLISP, and VBA programming in AutoCAD.

## 01. Establishing the Foundation for Drawing Standards

Well-established drawing standards ensure that your drawings all look the same when they are presented to the client, and they can make it easier to: Train new drafters and other professionals on your company's standards that use AutoCAD; Identify which drawing and externally referenced files are associated with a project; Determine the purpose of a named object in a drawing; Share project files with clients and contractors because your standards are well defined.

## 03. Building the Real World One Block at a Time

### 1. 逻辑脉络

定义块、修改块；提取块内的数据信息。

### 2. 摘录及评论

3『

在 18 章看到这么一段话。然后在 17 章里找到一小节「Creating the Room Label Block Definition」。

In Chapter 17, you created a set of functions that allowed you to extract the attributes of a block and then quantify the results before creating the BOM in the drawing. Here, you will create a function named furnbomexport that allows you to export the BOM data generated with the extAttsFurnBOM function output to an external file instead of adding it to the drawing as a table grid as you did with the furnbom function.

』

Instead of dedicating time to re-create the geometry each time, you can create the objects once and store them as a block definition. Block definitions are another type of nongraphical object that can be in a drawing, much like text and dimension styles.

3『[AutoCAD 2019 帮助: 关于定义块](http://help.autodesk.com/view/ACD/2019/CHS/?guid=GUID-F81D7F1E-1F0A-45AD-AC7E-891A85A0033A)』

In addition to geometric objects, block definitions can contain attribute definitions, which allow you to embed information into a block. The information stored in attributes can be extracted to an external file or added to a table in a drawing.

Block definitions must be defined in a drawing before you can create (or, as commonly known, insert) a block reference. A block reference object specifies where and how the objects from a block definition should be drawn onscreen or plotted. You typically create block definitions by first adding the geometry for your block in model space and then using the block command to define which objects will make up the block definition. AutoCAD also offers a special environment called the Block Editor (bedit command) for working with block definitions. Once a block definition is defined, you can use the insert command to create a block reference of a block definition. when defining a block you must consider the following:

1. Name . The name of a block definition is used to differentiate one from another; each block definition in a drawing must have a unique name. Drawings can easily contain hundreds and even thousands of block definitions. When naming block definitions, use descriptive names, but don't make them so long that the user must carefully read a sentence-long name. I discussed naming blocks and other nongraphical objects in Chapter 2,「Working with Nongraphical Objects.」

2. Base (or Insertion) . Point The base point for a block definition is similar to a drawing's origin. This point is used as a block reference's insertion point, the same point that is used to drag a preview of the block onscreen with the insert command. You typically specify the base point of a block on one of the objects in the block definition, such as an endpoint or intersection of two objects.

3. Objects. The objects that make up the block definition determine how the block references inserted into a drawing will look and behave. Objects within a drawing include geometry objects such as lines, circles, arcs, and even other blocks. Blocks can also include special objects known as attribute definitions, which allow you to add to a block information such as a project name or part number. I discuss attributes in the section「Embedding Information in a Block Definition with Attributes」later in this chapter.

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

2『Fields 感觉是在定义属性时看到的「字段」，待确认。』

When you insert a block reference with an attribute, you can specify a field value in the Edit Attributes dialog box by right-clicking in the text box to the right of the attribute prompt and clicking Insert Field. You can edit an existing field by double-clicking the shaded text in the text box, or you can convert it to static text by selecting and right-clicking the shaded text that represents the field and clicking Convert Field To Text.

BlockPlaceholder Field Type. In AutoCAD on Windows while the Block Editor is active, you have access to an additional field type: BlockPlaceholder. The BlockPlaceholder field type allows you to access the properties of the block reference when it is placed in a drawing. For example, you could list the name of the block as part of a description in an attribute field or even access the current value of one of the parameters used for a custom dynamic property.

Dynamic properties when added to a block definition allow you to rotate, move, stretch, and perform other actions on the objects within a block reference. A block definition that contains dynamic properties is known as a dynamic block. Parameters and actions are used to implement dynamic properties. You can only add dynamic properties to a block definition using the Block Editor in AutoCAD on Windows. Although you can't create or modify dynamic properties in AutoCAD for Mac OS, you can insert blocks that have these properties already implemented.

When a block with dynamic properties is inserted into a drawing, additional grips are displayed for the block reference when it is selected. These additional grips allow you to interactively change the values of the custom actions rather than selecting values from a predefined list. Figure 3.7 shows a block reference selected in the drawing and a linear distance being modified with grips.

One of the benefits of using attributes with your blocks is that you can extract the information and then use it in your drawing or an external program. If all of your blocks contain attributes, you could generate a bill of materials on demand or even help prepare an estimate for a project. The attribute values and the properties of the blocks containing attributes can be extracted from a drawing using the Attribute Extraction dialog box (attext command) or Data Extraction Wizard (attext command) (in AutoCAD on Windows only) or by using the -attext command at the command prompt in AutoCAD both on Windows and Mac OS. The following steps explain how to extract the attributes from a drawing using the Data Extraction Wizard in AutoCAD on Windows:

1『 dataextraction 命令可以提取实体对象里的各个数据，可以筛选出块的属性信息，可以导出成 csv、txt 等格式。可以说这个命令可以满足我想要做数据分析所需的数据源了，哈哈；用命令 -attext 可以直接提取属性信息，但需要一个模板，没有 dataextraction 方便。』

NOTE: After you place a table using the Data Extraction Wizard, a Data Link icon that looks like two chain links appears in the application's status-bar tray. Right-click the icon or the table in the drawing, and click Update All Data Links to ensure the information displayed in the table is up to date.


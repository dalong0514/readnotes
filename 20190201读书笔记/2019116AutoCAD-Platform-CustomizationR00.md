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

### 0501. 任意卡——生成 VLX 文件

VLX 文件是 LSP 文件编译后的成品文件。在 Visual LISP 编译器里，「文件 -> 生成应用程序 -> 新建应用程序向导」，按步骤一步步来。

## Introduction

In 1996, Lee began learning the core concepts of customizing the AutoCAD user interface and AutoLISP. The introduction of VBA in AutoCAD R14 would once again redefine how Lee approached programming solutions for AutoCAD. VBA made it much easier to communicate with external databases and other applications that supported VBA. It transformed the way information could be moved between project management and manufacturing systems.

Not being content with VBA, in 1999 Lee attended his first Autodesk University and began to learn ObjectARX®. Autodesk University had a lasting impression on him. In 2001, he started helping as a lab assistant. He began presenting on customizing and programming AutoCAD at the event in 2004. Along the way he learned how to use the AutoCAD Managed.NET API.

Customization is one of the feature areas that sets AutoCAD apart from many other CAD programs. Even though the product can be used out of the box, configuring the user interface and modifying the support files that come with the product can greatly improve your productivity. By customizing AutoCAD, you can streamline product workflows and create new ones that are a better fit with the way your company works. These workflows might range from importing layers and styles into a drawing to the extraction of drawing-based information into a spreadsheet or database.

The AutoLISP programming language can be used to: Create custom functions that can be executed from the AutoCAD Command prompt; Create and manipulate graphical objects in a drawing, such as lines, circles, and arcs; Create and manipulate nongraphical objects in a drawing, such as layers, dimension styles, and named views; Perform mathematical and geometric calculations; Request input from or display messages to the user at the Command prompt; Interact with files and directories in the operating system; Read from and write to external files; Connect to applications that support ActiveX and COM; Display dialog boxes and get input from the end user.

AutoLISP code can be entered directly at the Command prompt or loaded using a LSP file. Once an AutoLISP program has been loaded, you can execute the custom functions from the Command prompt. Functions executed from the Command prompt can be similar to standard AutoCAD commands, but the programmer determines the prompts that should be displayed. It is also possible to use AutoLISP code with a command macro that is activated from the AutoCAD user interface or a tool on a tool palette.

1『 VBA 能实现的功能同上。』

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

2『 Fields 感觉是在定义属性时看到的「字段」，待确认。』

When you insert a block reference with an attribute, you can specify a field value in the Edit Attributes dialog box by right-clicking in the text box to the right of the attribute prompt and clicking Insert Field. You can edit an existing field by double-clicking the shaded text in the text box, or you can convert it to static text by selecting and right-clicking the shaded text that represents the field and clicking Convert Field To Text.

BlockPlaceholder Field Type. In AutoCAD on Windows while the Block Editor is active, you have access to an additional field type: BlockPlaceholder. The BlockPlaceholder field type allows you to access the properties of the block reference when it is placed in a drawing. For example, you could list the name of the block as part of a description in an attribute field or even access the current value of one of the parameters used for a custom dynamic property.

Dynamic properties when added to a block definition allow you to rotate, move, stretch, and perform other actions on the objects within a block reference. A block definition that contains dynamic properties is known as a dynamic block. Parameters and actions are used to implement dynamic properties. You can only add dynamic properties to a block definition using the Block Editor in AutoCAD on Windows. Although you can't create or modify dynamic properties in AutoCAD for Mac OS, you can insert blocks that have these properties already implemented.

When a block with dynamic properties is inserted into a drawing, additional grips are displayed for the block reference when it is selected. These additional grips allow you to interactively change the values of the custom actions rather than selecting values from a predefined list. Figure 3.7 shows a block reference selected in the drawing and a linear distance being modified with grips.

One of the benefits of using attributes with your blocks is that you can extract the information and then use it in your drawing or an external program. If all of your blocks contain attributes, you could generate a bill of materials on demand or even help prepare an estimate for a project. The attribute values and the properties of the blocks containing attributes can be extracted from a drawing using the Attribute Extraction dialog box (attext command) or Data Extraction Wizard (attext command) (in AutoCAD on Windows only) or by using the -attext command at the command prompt in AutoCAD both on Windows and Mac OS. The following steps explain how to extract the attributes from a drawing using the Data Extraction Wizard in AutoCAD on Windows:

1『 dataextraction 命令可以提取实体对象里的各个数据，可以筛选出块的属性信息，可以导出成 csv、txt 等格式。可以说这个命令可以满足我想要做数据分析所需的数据源了，哈哈；用命令 -attext 可以直接提取属性信息，但需要一个模板，没有 dataextraction 方便。』

NOTE: After you place a table using the Data Extraction Wizard, a Data Link icon that looks like two chain links appears in the application's status-bar tray. Right-click the icon or the table in the drawing, and click Update All Data Links to ensure the information displayed in the table is up to date.

## 0105. Customizing the AutoCAD User Interface for Windows

You customize the user interface through a combination of direct manipulation and the Customize User Interface Editor—or CUI Editor, as it is commonly known. Direct manipulation can make it fast and easy to reorganize elements, but there are limitations, as not all elements are supported and new user-interface elements can't be added. The CUI Editor provides the most control over the elements of the user interface.

As you make changes to the user interface, the changes are stored as part of the Windows Registry or in the main customization (CUIx) file. CUIx files contain the definitions for many of the elements that are displayed in the AutoCAD application window, such as the buttons on a ribbon panel, items on the menu bar, or even shortcut key combinations.

### 5.1 Getting Started with the CUI Editor

The CUI Editor is the tool that you will need to become familiar with to customize the AutoCAD user interface. Figure 5.1 shows the CUI Editor and highlights some of the areas that I will discuss. The editor might appear a bit overwhelming at first—and to be honest it can be because of everything it does—but there is nothing to be afraid of; I will guide you one step at a time. The CUI Editor is a much better solution for those new to customizing the AutoCAD user interface than what was available in the releases prior to AutoCAD 2006. In those versions, a dialog box offered only limited customization options. You needed to use an ASCII text editor like Notepad to customize all available elements.

Not that I have anything against Notepad; it just does not know what needs to be done to create a toolbar, add a toolbar button, or define a pull-down menu with a series of items. If you forget a character, attempting to load the miscoded menu/customization file often results in a cryptic message from AutoCAD. The CUI Editor lowers the learning curve for creating and modifying user-interface elements.

You can display the CUI Editor using one of the following methods: 1) On the ribbon, click Manage tab Customization panel User Interface. 2) Right-click a button on the Quick Access toolbar or a standard toolbar and click Customize Quick Access Toolbar or Customize, respectively. 3) At the command prompt, type cui and press Enter.

When the CUI Editor is displayed, notice that there are two tabs. Each tab is divided into areas called panes. The two tabs in the CUI Editor and their purpose are as follows:

Customize Tab. Use the Customize tab to create, modify, and organize the user-interface elements that come with AutoCAD or those that you create. You will also use this tab to create workspaces that allow you to control when and where specific user-interface elements are displayed. This tab is divided into three panes: 

1. Customizations In Pane. Here you will find a listing of the CUIx files that are currently loaded and the user-interface elements that they contain. When a user-interface element is expanded, you see each of the items that make up that particular element, such as the buttons on a ribbon panel or the items on a pull-down menu. When you select a user-interface element, command, or control in this pane, its properties can be changed in the Dynamic pane.

2. Command List Pane. Here you'll find a list of the commands and controls that you can add to the user-interface elements in the Customizations In pane. New custom commands for use in the user-interface are created in this pane. Selecting a command from this pane displays its properties in the Dynamic pane, where you can change the image, name, macro, and other settings that define how a command appears in the user interface.

3. Dynamic Pane. Displays the properties of an item selected from either the Customizations In or Command List pane. Based on the item selected, one or more of eight different subpanes could be displayed. I cover each of these panes later in this chapter as I explain how to customize the elements of the user interface.

Transfer Tab. Use the Transfer tab to copy user-interface elements between customization (CUIx) files, migrate user-interface elements from an earlier release, and create new or save existing CUIx files.

1『是在「Transfer Tab」面板里，新建一个 cuix 文件的。』

TIP: You can resize a pane by positioning the cursor between two panes and dragging when the cursor changes to two arrows that point in opposite directions. The panes on the Customize tab can also be collapsed by clicking a pane's title bar.

### 5.2 Creating Commands and Defining Command Macros

Commands are the primary component of elements in the AutoCAD user interface, and they are created in the Command List pane of the CUI Editor. The properties of a command in a CUIx file define the sequence of AutoCAD commands and options that will be executed when the command is used, and how the command should appear on a user-interface element. The sequence of AutoCAD commands and options that are assigned to a command are contained in a macro. The macro is the most significant property of a command in a CUIx file.

#### 5.2.1 Understanding the Basics of a Command Macro

A macro defines the input that is sent to the AutoCAD command prompt when a user-interface element is used; it can, but does not necessarily need to, start and complete a command in a single command macro. You could start a command with one macro and then click another button to send an expected value to the active command. An example might be where one macro starts a custom AutoLISP® routine that prompts you for a bolt or window size, and rather than typing a size each time, you use a second macro to pass a value to the routine.

For the most part, a macro is similar to the input that you enter at the command prompt to start and complete an AutoCAD command, but it can also contain special characters that control its execution. For example, the following might be what you normally would do to draw a circle with a diameter of one-eighth of an inch:

1. At the command prompt, type circle and press Enter.

2. At the Specify center point for circle or [3P/2P/Ttr (tan tan radius)]: prompt, specify a point with the input device or type a value at the command prompt.

3. At the Specify radius of circle or [Diameter] <0.1875>: prompt, type d and press Enter.

4. At the Specify diameter of circle <0.3750>: prompt, type 0.125 and press Enter.

An example of a command macro using the same input as the previous example might look something like this:

```
^C^C._circle;\_d;0.125;
```

As you can see, I used five special characters in the example macro that were not present as part of the original input entered at the command prompt: 

```
^ (caret), . (period), _ (underscore), ; (semicolon), and \ (backslash). 
```

Table 5.1 explains the significance of each macro component.

```
Macro Component Description

^C^C Simulates the pressing of the Esc key twice.

._circle Passes the circle command to the command prompt.

; Simulates the pressing of the Enter key to start the circle command.

\ Pauses for the user to specify the center point of the circle.

_d Indicates that the Diameter option of the circle command will be used.

; Simulates the pressing of the Enter key to accept the Diameter option.

0.125 Specifies the value for the Diameter option.

; Simulates the pressing of the Enter key to accept the diameter value. Since this is the last expected value, the circle command ends too.
```

Table 5.2 lists the most common special characters used in a command macro.

TIP: To learn about other special and control characters that can be used in a command macro, search the AutoCAD Help system using the keywords characters in macros.

Table 5.2 Special characters that can be used in macros

```
Special Character Description

^C Equivalent to pressing Esc.

; Equivalent to pressing Enter.

[blank space] Equivalent to pressing Enter or spacebar based on the expected input of the current prompt.

\ Allows the user to provide input.

. Instructs AutoCAD to use the command's standard definition even when a command might have been undefined with the undefine command.

_ Instructs AutoCAD to use the global command name or option value instead of the local name or value provided. This allows the macro to function as expected when used with a different language of the AutoCAD release.

* Repeats the AutoCAD command after the asterisk character until the user cancels the command.

Example macro from the Point, Multiple Point command in the acad.cuix file:

*^C^C_point

$M= Indicates the start of a DIESEL expression.

Example expression from the UCS Icon, On command in the acad.cuix file:

$M=$(if,$(and,$(getvar,ucsicon),1),^C^C_ucsicon _off,^C^C_ucsicon _on)
```

When combining multiple commands into a single menu macro, you will want to first step through the sequence at the command prompt. Doing this can help you identify which commands, options, and values you want to use. The following example demonstrates the commands and options you might use to create and set as current a layer named Notes and then draw a multiline text object:

```
At the command prompt, type -layer and press Enter.

At the Enter an option prompt, type m and press Enter.

At the Enter name for new layer (becomes the current layer) <0>: prompt, type Notes and press Enter.

At the Ente0r an option prompt, type c and press Enter.

At the New color [Truecolor/COlorbook]: prompt, type 8 and press Enter.

At the Enter name list of layer(s) for color 8 <Notes>: prompt, press Enter.

At the Enter an option prompt, press Enter.

At the command prompt, type -mtext and press Enter.

At the Specify first corner: prompt, specify a point in the drawing area.

At the Specify opposite corner or [Height/Justify/Line spacing/Rotation/Style/Width/Columns]: prompt, type j and press Enter.

At the Enter justification [TL/TC/TR/ML/MC/MR/BL/BC/BR] <TL>: prompt, type tl and press Enter.

At the Specify opposite corner or [Height/Justify/Line spacing/Rotation/Style/Width/Columns]: prompt, type h and press Enter.

At the Specify height <0.2000>: prompt, type 0.25 and press Enter.

At the Specify opposite corner or [Height/Justify/Line spacing/Rotation/Style/Width/Columns]: prompt, type r and press Enter.

At the Specify rotation angle <0>: prompt, type 0 and press Enter.

At the Specify opposite corner or [Height/Justify/Line spacing/Rotation/Style/Width/Columns]: prompt, type w and press Enter.

At the Specify width: prompt, type 7.5 and press Enter.

At the MText: prompt, type NOTE: ADA requires a minimum turn radius of and press Enter.

At the MText: prompt, type 60" (1525mm) for wheelchairs. and press Enter.

Press Enter again to end the mtext command and leave the command-line window open.
```

What's That Hyphen? As I discussed earlier, commands that display dialog boxes or palettes should be avoided in macros when you want to use specific values. Adding a leading hyphen to many commands that normally display a dialog box or palette starts an alternate command that displays a series of prompts instead. For example, use -layer instead of layer when you want to create a layer from a command macro, or -insert instead of insert to insert a block. See Chapter 8,「Automating Repetitive Tasks,」for a listing of alternative commands and system variables that allow you to avoid opening dialog boxes and palettes.

After you've worked through the process at the command prompt, you can use that information to convert the process to a macro. The next steps walk you through the process of converting input entered at the command prompt into a command macro:

```
Press F2 to expand the command-line history or display the AutoCAD Text Window.

In the History area, select the command prompts that were displayed and input that you entered (see Figure 5.2). Right-click and click Copy.

At the command prompt, enter notepad and press Enter twice to launch Notepad.

In Notepad, click in the editor window and press Ctrl+V to paste the copied text from the command-line history.

From the pasted text, remove the two informational lines Current layer: and Current text style: and their values.

Replace the Specify first corner: prompt with a \ (single backslash character).

Remove all the other prompts before the input you entered.

After each line, add a ; (semicolon), with the exception of the line that contains the backslash. After this and the previous three steps you should have the following left in Notepad: -layer; m; Notes; c; 8; ; ; -mtext; \ j; tl; h; 0.25; r; 0; w; 7.5; NOTE: ADA requires a minimum turn radius of; 60" (1525mm) diameter for wheelchairs.; ;

Enter ^C^C before the first line to make sure no other command is active when the macro is used.

Place the cursor at the end of each line and press Delete to move all input to a single line. Your finished macro should look like this: ^C^C-layer;m;Notes;c;8;;;-mtext;\j;tl;h;0.25;r;0;w;7.5; NOTE: ADA requires a minimum turn radius of;60" (1525mm) for wheelchairs.;;

Click File Save As.

In the Save As dialog box, browse to the MyCustomFiles folder that you created under the Documents (or My Documents) folder, or the location where you want to store the text file.

In the File Name text box, type mynotemacro.txt and click Save.

Do not close Notepad; you will use the macro you just created in the next section, when you create a command for use in the user interface.
```

```
TIP

Add the text ._ (period underscore) in front of each command name and an _ (underscore) in front of the values that represent an option name. This ensures that your macro works correctly if a command is undefined or the command macro is used on a non-English AutoCAD release.

Here's how the macro you just created would look after prefixing commands with ._ and options with _:

^C^C._-layer;_m;Notes;_c;8;;;._-mtext;\_j;_tl;_h;0.25;_r;0;_w;7.5; NOTE: ADA requires a minimum turn radius of;60" (1525mm) for wheelchairs.;;
```

Figure 5.2 Command-line history of the input you previously entered

#### 5.2.2 Creating and Modifying Commands

Before you can use your macro, you first need to learn how to create a new command in a CUIx file. Commands are created under the Command List pane of the CUI Editor. You can also locate and modify existing commands in the CUIx files that are currently loaded.

The following example explains how to create a command for the macro that you created in the previous section in a current CUIx file. If you did not complete the steps for the previous example, you can open the NoteMacro.txt exercise file that is available for download from www.sybex.com/go/autocadcustomization. If you did complete the previous example but closed Notepad, launch Notepad and open the file MyNoteMacro.txt from the MyCustomFiles subfolder under the Documents (or My Documents) folder, or the location you used.

```
On the ribbon, click Manage tab Customization panel User Interface (or at the command prompt, type cui and press Enter).

In the CUI Editor, from the Command List pane select Create A New Command.

NOTE

When you create a new command, it is added to the customization (CUIx) file that is selected from the drop-down list at the top of the Customizations In pane. If you want to add a command to a partial customization file, make sure it is selected before creating the command. I discuss the types of customization files later in this chapter in the「Working with Customization Files」section.

In the Properties pane (see Figure 5.3), type Wheelchair Note in the Name field. The Name field is used to identify the command in the Command List pane and is part of the tooltip (shown in Figure 5.12, later in this chapter) that is displayed when the cursor hovers over the command in the user interface.

Click in the Macro field and then click the ellipsis […] button. In the Long String Editor, clear the current value in the text box. Enter the macro that you created in the previous exercise or copy/paste the contents of the MyNoteMacro.txt or NoteMacro.txt file into the text box. Click OK. The macro defines the actions that AutoCAD will perform when the command is used from the user interface.

Optionally, in the Description field enter ADA Wheelchair minimum radius note. The text entered in this field helps to describe what the command is used for and is part of the tooltip that is displayed when the cursor hovers over the command in the user interface.

Optionally in the Extended Help File field, specify an XAML file that contains additional text and images that describe what the command does. I do not cover creating extended help files in this book; search on the keywords extended help in the AutoCAD Help system to learn more.

Optionally in the Command Display Name field, enter -LAYER, TEXT. The text entered in this field helps the user to identify which AutoCAD commands are used as part of the macro, and is part of the tooltip displayed when the cursor is over the command in the user interface.

Optionally, click in the Tags field and then click the ellipsis […] button. In the Tag Editor, click in the Tags text box and enter Wheelchair,Note. Click OK.

NOTE

Tags make it easier to locate a command without looking for it in the user interface. You can search for a command that is assigned a tag using the Search field of the Application menu; the Search field is accessed by clicking the Application button located near the upper-left corner of the AutoCAD application window.

Click Apply to save the changes you made to the properties of the new command (see Figure 5.4).
```

Figure 5.3 Defining the properties of a command

Figure 5.4 The properties of the completed command

A command can be edited by selecting it from the Command List pane and then making changes to it in the Properties pane, just as you did when you created the new command.

TIP: Click the Filter The Command List By Category drop-down list under the Command List pane and select Custom Commands to list only the custom commands that have been added to any of the loaded CUIx files.

#### 5.2.3 Creating and Assigning an Image to a Command

While using images with your commands is optional, you should consider adding an image to each of the commands that you create in a CUIx file to provide the most flexibility. Although not all user-interface elements display an image, most of the common user-interface elements do. AutoCAD provides a basic image editor that allows you to create images for your commands right inside the CUI Editor. However, if you or someone else in your company has experience with a different image editor, you can use that software.

Here are the basic requirements your images need to meet:

```
Small images should be 16×16 pixels in size.

Large images should be 32×32 pixels in size.

Images need to be in the BMP file format.
```

If an image is created using the Button Editor inside the CUI Editor, that image is saved as part of the CUIx file. You can export an image file if you want to edit the image outside of AutoCAD. You also can import into a CUIx file images that you created or edited outside of AutoCAD and then assign those images to a command. An alternative to importing images into the CUIx file is to create a resource DLL file that has the same name as the CUIx file being loaded into AutoCAD. This method is more common with third-party utilities that use CUIx files for their user-interface elements.

The following example explains how to create a custom image for the Wheelchair Note command you created in the previous section:

```
Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the CUI Editor, from the Command List pane select the Wheelchair Note command.

Under the Button Image pane, select one of the images from the Image list. It does not matter which image you select unless there is an image that is similar to the image you want to create. If there is a similar image, select it.

Under the Apply To section, select Both.

Click Edit.

In the Button Editor (see Figure 5.5), click Clear.

Click the Grid check box to display a grid of pixel squares over the image canvas.

Click the Pencil drawing tool located above the image canvas to edit the image.

Click one of the color swatches from the left side or click More to display the Select Color dialog box. If you click More, choose a color that is different from the standard colors.

Click (or drag over) the image canvas to create your image. Draw an image that you feel conveys the idea of a Wheelchair Note. Figure 5.6 shows an example of an image that I created. It can be found in the files available for download from this book's web page; the file is named WheelchairNote.bmp.

After you have created your image, click Save.

In the Save Image dialog box, in the Image Name text box enter WheelchairNote. Click OK.

Click Close to return to the main dialog of the CUI Editor. The image you created should now be assigned to both the Small Image and Large Image fields of the command.

Click Apply to save the changes to the command.
```

Figure 5.5 Creating a custom image

Figure 5.6 Example custom image

If you have an externally saved file that you want to use for a command, you can do the following:

```
In the CUI Editor, from the Command List pane select the command that you want to assign a button image to.

In the Button Image pane, right-click the Image list, and then click Import Image.

In the Open dialog box, browse to and select the image to import. Click Open.

In the Apply To section, select Both.

Scroll to the bottom of the Image list and select the image you just imported. The image you selected should now be assigned to both the Small Image and Large Image fields of the command.

Click Apply to save the changes to the command.
```

As I mentioned earlier, the images used for your commands are stored in the CUIx file. You can manage the images stored in a CUIx file using the CUI Editor - Image Manager (see Figure 5.7). Click the Image Manager button in the Customizations In pane to display the CUI Editor - Image Manager. Here you can perform the following tasks:

```
View the images and their sizes

Import externally stored BMP files

Export selected images in the CUIx file and save them as individual BMP files

Remove the images that you are not currently using
```

Figure 5.7 Managing images in the loaded CUIx files

### 5.3 Customizing User-Interface Elements

Out of the box, the AutoCAD user interface is designed for everyone, but not to accommodate the needs of any specific industry or any one single company's workflow. Many of the common user-interface elements in the AutoCAD application window can be customized, and you should take the time to customize them to get the most out of AutoCAD. You can add new elements that execute command macros and custom applications you create, remove or hide those that you do not use, or reorganize those that you use frequently to make them easier to access. You use the CUI Editor to modify the elements defined in a CUIx file.

The following elements of the user interface can be edited with the CUI Editor:

```
Quick Access toolbar (QAT)

Ribbon; panels and tabs

Pull-down and shortcut menus

Toolbars

Double-click actions

Shortcut and temporary override keys

Mouse buttons

Properties displayed as part of the Quick Properties palette or rollover tooltips

Legacy elements; tablet menus and buttons; image tile and screen menus
```

#### 5.3.1 Quick Access Toolbar

The Quick Access toolbar (QAT), shown in Figure 5.8, is part of the AutoCAD title bar area along the top of the application window. The tools commonly placed in the toolbar are for managing drawing files, plotting or publishing layouts, undoing or redoing recent actions, and setting a workspace current that is defined in the main CUIx file.

Figure 5.8 Accessing the customization options for the Quick Access toolbar

You can customize the QAT using one of the following methods:

1. QAT Customize Menu. Clicking the Customize button on the far right side of the QAT displays the Customize menu. From this menu, you can toggle the display of several additional select commands, click More Commands to display the CUI Editor, or click Show Below/Above The Ribbon to change the placement of the QAT.

2. QAT Shortcut Menu Right-clicking a command or control on the QAT displays a shortcut menu that allows you to remove the element below the cursor, add a vertical separator bar to the right of the element under the cursor, click Customize Quick Access Toolbar to display the CUI Editor, or click Show Quick Access Toolbar Below/Above The Ribbon to change its placement.

3. Ribbon Button Right-clicking a command on the ribbon displays a shortcut that contains the Add To Quick Access Toolbar item. This item adds the command to the QAT.

4. CUI Editor The CUI Editor provides you with the same functionality that is found on the QAT's Customize and shortcut menus, and a few additional options as well. With the CUI Editor, you can choose to customize the default QAT or create a new one, and you can also change the order in which commands and controls are displayed.

1『

到了这里，算是把数据流的各个命令弄成图标了。

1、cui 命令进入「自定义用户界面」。在右侧「传输」面板那边，新建一个 cuix 文件，命名为 dataflow.cuix。

2、回到左侧的「自定义」面板，打开刚刚新建的「dataflow.cuix」。右键「LISP 文件」，加载数据流的插件。

3、在左下角的「命令列表」面板里，点「创建新命令」。选好图标，名称写「导出设备表数据」，宏写插件里的命令「gsequipment」。

4、在左上角的面板里，菜单栏下新建子菜单「数据流」，把一个个命令拖到「数据流」子菜单下即可。当然，也可以放到「快速访问工具栏」里，我个人更倾向于放到「菜单栏」。

』

#### 5.3.2 Customizing the Default QAT

The next example explains how to customize the default QAT. You will add the Wheelchair Note command that you created earlier in this chapter.

```
Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the Customizations In pane of the CUI Editor, expand the Quick Access Toolbars node. Expand the Quick Access Toolbar 1 node, or any other QAT you want to customize.

In the Command List pane, select Custom Commands from the Filter The Command List By Category drop-down list.

From the Command list, drag the Wheelchair Note command below the Ribbon Combo Box - Workspace control. Release the mouse button when the horizontal bar is displayed below the control (see Figure 5.9). After a command or control is added to the QAT, you can change how it is displayed by changing its properties under the Properties pane.

Click Apply to save the changes.
```

Figure 5.9 Adding a command to the QAT

Now that the Wheelchair Note command has been added, let's add a separator and Layer controls to the QAT that we are customizing in this exercise:

```
Use the command-list filter to access the Ribbon Control Elements. In the Command List pane, open the Filter The Command List By Category drop-down list and select Ribbon Control Elements (see Figure 5.10).

In the Search Command List text box (located just above the Filter The Command List By Category drop-down list), type layer.

In the command list, right-click Layer List Combo Box and select Copy.

In the Customizations In pane, right-click the Wheelchair Note command you added in Step 4. Click Paste. The Layer List Combo Box control is added to the QAT.

Right-click the Ribbon Combo Box - Workspace control under the QAT node and click Insert Separator. A separator element is added to the end of the toolbar.

Click Apply to save the changes.
```

Figure 5.10 Accessing the controls that can be placed on the QAT

There will be times when you want to remove access to particular commands. The next steps in this exercise explain how to remove the SaveAs command from the QAT and how to test the customized QAT:

```
Right-click the SaveAs element under the QAT and click Remove. In the message box, click Yes to remove the element.

Click and drag the Layer List Combo Box above the Wheelchair Note command in the tree view to reorder it on the QAT.

Click Apply to see the changes in the application window. The QAT and the elements under the QAT node in the CUI Editor should now look like Figure 5.11.

Click OK to save the changes to the CUIx file and return to the drawing window.

On the QAT, position the cursor over Wheelchair Note. Notice the contents of the tooltip, shown in Figure 5.12; you should see the information you entered when you created the command earlier in this exercise.

Click Wheelchair Note and specify a point in the drawing window. The layer Notes is created and set as current, and two single-line text objects are created with the note (see Figure 5.13).
```

NOTE: You can create drop-down menus on the QAT that allow you to group multiple commands, not controls, into a single button. To create a drop-down menu, right-click the node of the QAT to which you want to add a drop-down menu in the CUI Editor and click New Drop-Down. Then, add commands to it from the Command List pane just as you did when you added commands to the QAT itself.

Figure 5.11 Results of the customization to the QAT

Figure 5.12 Tooltip for the custom Wheelchair Note command

Figure 5.13 The results of using the Wheelchair Note command

#### 5.3.3 Creating a New QAT

While AutoCAD can display only a single QAT at a time, you could create your own QAT that contains the commands and controls you want to use instead of modifying the default toolbar that is defined in the acad.cuix file. Not only could you create your own new QAT, but you could define multiple QATs that contain different commands and controls for each department in your company or for each discipline of drawings that you work on. If you create a new QAT, you must assign it to a workspace to display it in the user interface.

These steps explain the overall process for creating a new QAT and displaying it within a workspace:

```
Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the Customizations In pane of the CUI Editor, right-click the Quick Access Toolbars node and select New Quick Access Toolbar.

Enter a name for the new QAT or press Enter to accept the default name.

Customize the QAT as needed using the techniques introduced in the「Customizing the Default QAT」section.

Click OK to save the changes made. The new QAT must be added to a workspace before it can be displayed in the application window; see the「Organizing the User Interface with Workspaces」section later in this chapter for details on how to customize a workspace.
```

#### 5.3.4 Ribbon

The main AutoCAD user-interface feature that you most likely have interacted with is the ribbon. The ribbon follows Microsoft's design concept called「fluent user interface」(or FUI) and is similar in concept to the one found in the Microsoft Office products. The idea behind the design is that it makes it easier to discover and access the commands and options that a user is looking for with a rich visual user experience.

Pull-down menus and toolbars, which most applications still use to this day, provide a tried-and-true user experience, but they work best with a somewhat limited selection of commands. Pull-down menus and toolbars can handle hundreds of commands, but these elements lack the ability to start an operation and then give you additional choices while the operation is active.

Sure, you could show and hide menus and toolbars dynamically, but that introduces an element of inconsistency in the design. Where those items might appear this or next time becomes unpredictable. Dialog boxes are also a great way to allow the user to control the way a command or control might function, but that does not mean a user will always discover the most helpful settings. Instead of hiding useful settings and options, the design of the ribbon makes it easier to place them adjacent to a command or on a contextual tab. There is no doubt that the ribbon introduces an initial learning curve, but what doesn't when you are new to using it or after something you have done for a decade or two changes?

Commands and controls on the ribbon are organized by task through the use of tabs and panels, as shown in Figure 5.14. Each task is represented by a tab, which can hold different panels. A ribbon tab can be static—displayed all the time—or contextual, which means the tab is displayed only when a specific condition is met. If you have created a hatch or multiline text object in AutoCAD, chances are you worked with the Hatch Creation and Text Editor tabs that are displayed while you were using the hatch and mtext commands. Those tabs are contextual and are available only while the commands are active; ending the commands hides the tabs once again.

Figure 5.14 Command and control organization using the ribbon

The ribbon is divided into panels, which are used to organize and display commands and controls to the user. Panels have two different display states: normal and expanded. Not all panels are configured to be expanded, but when a panel offers additional commands or controls that are not displayed by default, you see a down arrow to the right of the ribbon's title. Clicking the panel's title bar expands the panel.

When a panel is expanded, it can be pinned (forced to remain expanded until you switch tabs or unpin it) using the Pin button, shown in Figure 5.14. Some panels show a panel dialog-box launcher button, also shown in Figure 5.14, which can start a command that commonly displays a dialog box or palette that is related to the commands and controls on the ribbon panel.

When customizing the ribbon, you can control the display of ribbon tabs with a workspace. Workspaces are also used to control the order in which tabs appear on the ribbon in the user interface. For more information on workspaces, see the section「Organizing the User Interface with Workspaces」later in this chapter. From the AutoCAD application window, you can also show and hide ribbon panels and tabs by right-clicking a panel or tab on the ribbon. Then, from the shortcut menu, click the element you want to show or hide. You can also modify the order in which ribbon panels and tabs are displayed by clicking and dragging an element on the ribbon.

#### 5.3.5 Ribbon Panels

Ribbon panels are containers for the commands and controls that you eventually want to display on the ribbon. Each ribbon panel is divided into two areas; the upper area is always displayed, and the lower area is displayed only when the panel is expanded by clicking a panel title bar. The lower area is known as the slideout.

The commands and controls on a panel must be placed in a row. A panel can contain more than one row, but a panel must always have at least one row in order to contain commands or controls. A row can be divided into one or more rows with the use of a subpanel. A row can also contain a Fold panel, which can contain commands and controls as well. A fold panel differs from a subpanel in that it can't contain any rows; however, it can be assigned a collapse priority and resizing considerations. Separators and drop-down menus allow you to further organize related commands and controls on the panel. Figure 5.15 shows the Draw panel on the ribbon and how it is defined in the CUI Editor using rows and a single subpanel.

Figure 5.15 Structure of the Home 2D - Draw panel

The following example explains how to create a new panel named My Tools:

```
Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the Customizations In pane of the CUI Editor, expand the Ribbon node.

Right-click the Panels node and select New Panel.

In the in-place text editor, type My Tools for the name of the panel and press Enter.

Click Apply to save the new ribbon panel.
```

Now, let's add structure to organize commands and controls:

```
Right-click the My Tools panel and click New Row. The new row is added below <SLIDEOUT>, which is the element that separates the rows that are displayed by default and those that are displayed when the panel is expanded.

Right-click Row 1 under the My Tools panel node and click New Sub-Panel.

Right-click Sub-Panel 1 under the Row 1 node and click New Row.

Under Sub-Panel 1, right-click the first row node and click New Drop-Down. Your ribbon panel should now look like Figure 5.16.

Select the New Drop-Down node under Row 1 of Sub-Panel 1, and in the Properties pane, click the Button Style field. Select SmallWithText from the drop-down list that appears. Once a command or drop-down menu is added to a ribbon panel, you can customize how it will look using the properties available in the Properties pane.
```

Figure 5.16 Structure for the new My Tools panel

The next steps explain how to add commands and controls to the rows of the ribbon panel:

```
In the Command List pane, click the Filter The Command List By Category drop-down list and select All Commands Only.

Locate the Wheelchair Note command and add it to Row 1 under the My Tools panel. (Type Wheelchair in the Search Command List text box to make it easier to locate the command.) Click and drag the Wheelchair Note command to the My Tools panel. When the cursor is over Row 1, release the mouse button. Then, drag the command so it is placed above Sub-Panel 1 and under Row 1.

Select the Wheelchair Note command under Row 1, and in the Properties pane, click the Button Style field. Select Large With Text (Vertical) from the drop-down list that appears. Once a command is added to a ribbon panel, you can customize how it will look using the new properties available in the Properties pane.

In the Command List pane, locate and add the Multileader, Multileader Edit, and Multileader Edit Remove commands to the New Drop-Down node under Row 1 of Sub-Panel 1. Remember, you can use the Search Command List text box to filter the Command List pane.

TIP: You can press and hold the Ctrl key to select multiple commands. The order in which the commands are selected determines the order in which they are added to the panel.

Add the Multileader Style Manager command to the Panel Dialog Box Launcher node under the My Tools panel.

Add the other five multileader-related commands to Row 2 (located under the <SLIDEOUT> item).

Click the Filter The Command List By Category drop-down list and select Ribbon Control Elements. Add the Ribbon Combo Box - Multileader Style control to Row 2 under Sub-Panel 1.

Add some of your favorite commands and controls that you use often to the ribbon panel, if you want.

Click Apply to save the new panel. The new panel should appear in the CUI Editor, as shown in Figure 5.17.
```

Figure 5.17 The completed My Tools panel

Once you have created a panel, you must add it to a tab in order for it to be displayed on the ribbon. I cover customizing ribbon tabs in the next section. You can modify an existing panel by selecting it from the Panels node under the Ribbons node of the Customizations In pane. The process for modifying a panel is similar to the process you used when you created the My Tools panel.

#### 5.3.6 Ribbon Tabs

Ribbon tabs are used to control the display and organization of ribbon panels in the user interface. You can add and remove ribbon panels to or from one of the standard ribbon tabs or create your own. Often, if you create your own panels you will want to create your own ribbon tabs as well. Several conditions determine whether a tab displays in the user interface:

Is the tab part of the current workspace?

Is the tab enabled?

Has the tab been assigned to a contextual state?

Has a contextual condition been met?

#### 5.3.7 Creating a New Ribbon Tab

The following example explains how to create a new tab named Favorites and how to add several ribbon panels to the new tab:

```
Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the Customizations In pane of the CUI Editor, expand the Ribbon node.

Right-click the Tabs node and select New Tab.

Using the in-place text editor, type My Favorites Tab for the name of the new tab and press Enter.

Select the My Favorites Tab from the Ribbon Tabs node, and in the Properties pane, change the value in the Display Name field to Favorites. The Display Name field controls the text that appears in the user interface as the tab label.

In the Customizations In pane, go to the Ribbon node and expand Panels. Select the My Tools node and right-click. Click Copy.

Under the Tabs node, select the Favorites node and right-click. Click Paste. A reference to the My Tools panel is added to the Favorites tab. Figure 5.18 shows what the Favorites tab should look like in the Customizations In pane, and the tab's settings in the Properties pane.

Click Apply to save the new tab. The new tab is not added to the ribbon until it has been added to a workspace or a contextual tab state.
```

Figure 5.18 Favorites tab with the My Tools panel

#### 5.3.8 Displaying Ribbon Tabs

After a ribbon tab has been created, you have two options for displaying it in the user interface: 1) Add the ribbon tab to a workspace. 2) Add the ribbon tab to a contextual tab state.

When you choose to add it to a workspace, you can control the location in which the tab appears on the ribbon and its default display state: shown or hidden. If you add the tab to a contextual tab state, you can control the tab's display type: full or merged.

Use the following steps to add the Favorites tab to the ribbon for the current workspace:

```
In the Customizations In pane, expand the Workspaces node and select the workspace that ends with the text (current).

In the Workspace Controls pane, click Customize Workspace, as shown in Figure 5.19.

In the Customizations In pane, expand Ribbon Tabs and click My Favorites Tab (shown in Figure 5.20). The My Favorites Tab check box should be selected.

In the Workspace Contents pane, click Done.

Expand the Ribbon Tabs node and drag Favorites above Home - 2D (shown in Figure 5.21).

Click OK to save the changes and close the CUI Editor.

On the ribbon, click the Favorites tab (shown in Figure 5.22). Test the various parts of the ribbon panel; click the panel's title bar to expand the panel and display the dialog box launcher button.
```

Figure 5.19 Customizing the current workspace

Figure 5.20 Adding the ribbon tab to the current workspace

Figure 5.21 Controlling the order of the ribbon tab with the workspace

Figure 5.22 The Favorites tab displayed on the ribbon

Any ribbon tab can be added to a contextual tab, but typically the scope of the commands and controls on the panels of the tab are limited to editing objects only. Contextual tab states are not workspace specific, so there is no need to add contextual tabs to a current workspace.

The following example explains how to create a new ribbon tab that contains the Annotate - Text panel, and adds the new ribbon tab to the Text, Multiline Selected contextual tab state.

```
In the drawing window, use the mtext command to create a multiline text object. Now, select the text object. Notice that no contextual tab is displayed unless the multiline text object is being edited in the in-place text editor.

In the CUI Editor, create a new ribbon tab named Text Contextual tab.

Select the Text Contextual tab from the Ribbon Tabs node, and then in the Properties pane, change the value of the Display Text field to Edit Text.

Click the Contextual Display type field, and select Full from the drop-down list. Full designates that the panels associated with the tab are displayed on their own tab, while Merged designates that the panels associated with the tab are displayed no matter which ribbon tab is current.

In the Customizations In pane, go to the Ribbon node and expand Panels. Select and then right-click the Annotate - Text panel. Click Copy.

Under the Ribbon Tabs node, select the Text Contextual tab and right-click. Click Paste.

In the Customizations In pane, expand Ribbon Contextual Tab States.

From the Ribbon Tabs node, drag the Text Contextual tab to the Text, Multiline Selected contextual tab state.

Click OK to save the changes and close the CUI Editor.

In the drawing window, select the multiline text object. The Edit Text tab is displayed with the Text panel, as shown in Figure 5.23. By default, tabs that are assigned to contextual tab states are added to the right side of the ribbon, but in Figure 5.23 the Edit Text tab was dragged to the left side directly in the application window.
```

Figure 5.23 The custom Edit Text tab displayed when the multiline text object was selected

#### 5.3.9 Pull-Down Menus

The menu bar is an area commonly found along the top of an application window. It contains a number of menus, which are also referred to as pull-down menus. You click a label on the menu bar to display the associated pull-down menu. When displayed, you can click one of the items on the pull-down menu to start a command. A pull-down menu can contain separators and submenus to group related commands together.

The menu bar and pull-down menus were the primary method for accessing commands before the introduction of the ribbon. They are still used for corporate customization and are displayed by default with the AutoCAD Classic workspace. It is possible to display both the ribbon and menu bar. When the menubar system variable is set to 1, the menu bar is displayed just below the title bar of the AutoCAD application window.

Like the QAT and ribbon, you can customize the pull-down menus that come with AutoCAD or create your own. Pull-down menus can contain the commands that can be added to other user-interface elements but can't contain a drop-down list, check box, text box, or other common Windows controls that can be found on the ribbon or some toolbars. You can, however, use DIESEL to enable, disable, and/or display a check mark next to a menu item. For information on DIESEL and how to use it, refer to the AutoCAD Help system.

As you have seen with other user-interface elements, workspaces are also used to control the display of a pull-down menu on the menu bar and in which order all pull-down menus should be displayed. For more information on workspaces, see the「Organizing the User Interface with Workspaces」section later in this chapter.

The following explains how to create a new pull-down menu, add commands, and organize the commands with a separator and submenu:

```
Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the Customizations In pane of the CUI Editor, right-click the Menus node and select New Menu.

In the in-place text editor, type Favorites for the name of the new pull-down menu and press Enter.

In the Command List pane, locate the Wheelchair Note command. (Type wheelchair in the Search Command List text box.) Click the command name and then drag the Wheelchair Note command to the Favorites pull-down menu under the Menus node in the Customizations In pane. When the cursor is over Favorites, release the mouse button.

In the Customizations In pane, under the Menus node, right-click the Favorites pull-down menu and click New Sub-menu. In the in-place text editor, type Annotation Tools for the name of the new submenu and press Enter.

In the Command List pane, locate the Multiline Text and Single Line Text commands and drag them to the Annotation Tools submenu. (If you have difficulty finding the commands, type line text in the Search Command List text box.)

In the Customizations In pane, under the Menus node, right-click the Annotation Tools submenu under the Favorites pull-down menu and click Insert Separator.

In the Command List pane, locate the Multileader command and drag it below the separator on the Annotation Tools submenu. (If you have difficulty finding the command, type multileader in the Search Command List text box.)

Click Apply to save the new pull-down menu. Figure 5.24 shows what the completed pull-down menu should look like under the Menus node.
```

Figure 5.24 Structure of the Favorites pull-down menu in the CUI Editor

While a new pull-down menu is added to all the workspaces currently defined in the main customization (CUIx) file, you will want to make changes to each workspace to ensure the pull-down menu is in the correct position on the menu bar.

Use the following steps to add the pull-down menu if it is not displayed in the current workspace. I will also show you how to change the menu's position.

```
In the Customizations In pane, expand the Workspaces node and select the workspace that ends with the text (current).

In the Properties pane, click the Menu Bar field and select On from the drop-down list. Enabling this property ensures that the menu bar is displayed when the workspace is set as current; this sets the menubar system variable to a value of 1.

In the Workspace Contents pane, click Customize Workspace.

In the Customizations In pane, expand Menus and click Favorites if it is not already checked.

In the Workspace Contents pane, expand the Menus node and drag Favorites above Window. Click Done.

Click OK to save the changes and close the CUI Editor.

On the menu bar, click Favorites. Test the various menu items and the subpanel pull-down menu. Figure 5.25 shows what the Favorites pull-down menu looks like on the menu bar.
```

Figure 5.25 Favorites pull-down menu on the menu bar

#### 5.3.10 Shortcut Menus

Shortcut menus make it easy to access the commands that you need when you need them—and near the cursor, so you don't have to leave the drawing area. You display a shortcut menu by right-clicking or secondary-clicking on the input device. The commands that you can access from a shortcut menu are often determined by the context in which the menu is displayed, which is why shortcut menus are sometimes referred to as context or contextual menus. Table 5.3 lists the shortcut menus that you can customize and the contexts in which they are displayed.

NOTE: The shortcutmenu system variable controls the display of the shortcut menus related to the Default, Command, and Edit modes. These settings can also be controlled from the Windows Standard Behavior section of the User Preferences tab in the Options dialog box (options command). In addition to controlling which menus are displayed, you can control the duration for which the right pointer device button needs to be held before the shortcut menu is displayed. You can change the duration by using the Options dialog box or the shortcutmenuduration system variable.

Table 5.3 Customizable shortcut menus

```
Context Description

Hot Grip Displayed when a grip has been selected and is ready for editing, and you right-click in the drawing area

Object Snap Displayed when the Shift key is held and you right-click in the drawing area

Default Mode Displayed when no command is active, an object is selected, grip editing is not active, and you right-click in the drawing area

Command Mode Displayed when a command is active and you right-click in the drawing area

Edit Mode Displayed when an object is selected and you right-click in the drawing area
```

Shortcut menus are customized with the CUI Editor using techniques that are nearly identical to those used for customizing pull-down menus. You add commands to the shortcut menu and use separators and submenus to organize related commands. Shortcut menus are not displayed as part of the main user interface, but are called on based on the current context. AutoCAD uses a special property value called an alias to determine which shortcut menu should be displayed. Each alias must be unique inside a customization (CUIx) file.

Table 5.4 lists the unique aliases and alias naming conventions that AutoCAD uses for displaying specific shortcut menus.

Table 5.4 Aliases and alias naming conventions for shortcut menus

```
Alias Description

GRIPS Hot Grip Cursor menu

SNAP,POP0 Object Snap Cursor menu

CMDEFAULT Default Mode menu

CMCOMMAND Command Mode menu

CMEDIT Edit Mode menu

COMMAND_cmdname Command-specific menu; cmdname represents the name of the command that the shortcut menu should be associated with.

OBJECT_objectname or

OBJECTS_objectname Single or multiple selected objects menu; objectname represents the type of the object that the shortcut menu should be associated with.
```

The next example explains how to create a new object shortcut menu that adds items to the Edit Mode menu when a line is selected:

```
Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the Customizations In pane in the CUI Editor, right-click the Shortcut Menus node and select New Shortcut Menu.

In the in-place text editor, type Line Objects Menu for the name of the new shortcut menu and press Enter.

Select the Line Objects Menu from the Shortcuts Menus node, and then go to the Properties pane and click the Aliases field. Click the ellipsis […] button to display the Aliases dialog box. Click after the alias in the text box and press Enter. Type OBJECTS_LINE and click OK. For information on defining command- and object-related shortcut menus, see the「Command Mode Shortcut Menus」and「Object Mode Shortcut Menus」sections later in this chapter.

In the Command List pane, locate the Stretch, Trim, and Extend commands and drag them to the Line Objects Menu item in the Shortcut Menus node.

Click OK to save the new shortcut menu.

In the drawing window, create a few lines.

Select the lines you create and right-click. The shortcut menu with the CMEDIT alias is displayed and the items in the Line Objects Menu shortcut menu are merged with it, as you can see in Figure 5.26.

Figure 5.26 Line Objects Menu in the drawing window
```

#### 5.3.11 Command Mode Shortcut Menus

Command-specific menus insert additional items into the shortcut menu with the CMCOMMAND alias. You use the COMMAND_cmdname alias to specify which command the shortcut menu should be associated with. cmdname must match the name of a command defined with ObjectARX® or Managed.NET, not one that has been defined with AutoLISP. For example, to associate items with the LINE command's shortcut menu you would create a shortcut menu with the alias COMMAND_LINE.

#### 5.3.12 Object Mode Shortcut Menus

Single or multiple selected object menus insert additional items into the shortcut menu with the CMEDIT alias. You use the OBJECT_objectname and OBJECTS_objectname aliases to specify which object type the shortcut menu should be associated with. OBJECT_objectname is used when you select a single object of a specific object type and right-click in the drawing area; OBJECTS_objectname is used when multiple objects of a single object type are selected.

For example, to associate items with the Edit Mode shortcut menu when a single arc object is selected, you would create a shortcut menu with the alias OBJECT_ARC.

If a shortcut menu with the alias OBJECT_objectname is not defined but a shortcut menu with the alias OBJECTS_objectname is, OBJECTS_objectname applies to the context of when one or more objects of the specified object type are selected. objectname must match a valid DXF Code 0 value. You can search the product Help system on the keywords DXF Entities to locate a listing of values for standard AutoCAD objects.

There are some additional names, though, that do not match a DXF Code 0 value. These exceptions apply to block references that have the value INSERT. Table 5.5 lists the additional names that are used to identify types of block reference objects.

TIP: If you are unsure what the DXF Code 0 value is for an object, place the object in the drawing window and enter the AutoLISP expression (cdr (assoc 0 (entget (car (entsel))))) at the AutoCAD command prompt. When prompted, select the object and the DXF name and the entity will be displayed.

Table 5.5 Special names used to identify types of block reference objects

```
Name Description

ATTBLOCKREF Block reference containing attribute references

ATTDYNBLOCKREF Dynamic block reference containing attribute references

BLOCKREF Block reference without attribute references

DYNBLOCKREF Dynamic block reference without attribute references

XREF External drawing reference (xref)
```

#### 5.3.13 Toolbars

Toolbars can be found in most Windows applications. Before the ribbon or even the dashboard, which was the predecessor to the ribbon, toolbars were one of the earliest visual user-interface elements. Buttons on a toolbar can be clicked to start a command or pressed and held to display a flyout. A flyout on a toolbar is similar to a submenu on a pull-down menu or even a drop-down menu on the ribbon, but flyouts are based on other toolbars, as defined in a loaded customization (CUIx) file. Toolbars can also contain controls, such as drop-down lists or text boxes, and separators to organize commands and controls.

While toolbars for the most part are no longer one of the primary user-interface elements in AutoCAD, they are still useful for corporate customization and are displayed by default with the AutoCAD Classic workspace. It is possible to display toolbars and the ribbon at the same time; this can be helpful if you want access to specific commands and controls no matter which ribbon tab is active. For example, you might consider displaying the Layers toolbar so you can change the current layer without switching to the Home tab on the ribbon.

Workspaces are used to control the display of toolbars, as well as their position in the user interface. For more information on workspaces, see the「Organizing the User Interface with Workspaces」section later in this chapter.

The following example explains how to create a new toolbar and add an existing toolbar as a flyout:

```
Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the Customizations In pane of the CUI Editor, right-click the Toolbars node and select New Toolbar.

In the in-place text editor, type Favorites for the name of the new toolbar and press Enter.

In the Command List pane, locate and add the Wheelchair Note command to the Favorites toolbar. (Type wheelchair in the Search Command List text box to make it easier to find the command.) Click and drag the Wheelchair Note command to the Favorites toolbar under the Toolbars node in the Customizations In pane. When the cursor is over Favorites, release the mouse button.

Locate and add the Multileader command below the Wheelchair command. (Type multileader in the Search Command List text box to make it easier to find the command.)

In the Customizations In pane, under the Toolbars node click and drag the Text toolbar between the Wheelchair and Multileader commands in the Favorites toolbar. This creates a flyout on the Favorites toolbar containing the commands of the Text toolbar. A toolbar can contain controls, but when used as a flyout, the controls are not displayed.

Click Apply to save the new toolbar. Figure 5.27 shows what the completed toolbar should look like under the Toolbars node.
```

Figure 5.27 Structure of the Favorites toolbar in the CUI Editor and how it appears in the user interface

When a toolbar is created, it is added to all the workspaces currently defined in the customization (CUIx) file. Use the following steps to add the Favorites and Layers toolbars to the current workspace:

```
Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the Customizations In pane, expand the Workspaces node and select the workspace that ends with the text (current).

In the Workspace Contents pane, click Customize Workspace.

In the Customizations In pane, expand Toolbars and click Favorites if it is not already checked. Click Layers as well if it is not already checked.

In the Workspace Controls pane, expand the Toolbars node and select Favorites.

In the Properties pane, you can edit the Orientation, Location, and Rows properties of the toolbar. Click Done.

TIP: Rather than controlling the orientation and location of toolbars using the CUI Editor, you can drag and position toolbars in the application window. Once the toolbars are positioned, use the wssave command to save the changes to a workspace.

Click OK to save the changes and close the CUI Editor.

Click the Wheelchair Note and Multileader to start the command macros. Click and hold the mouse button over the Text button in the middle of the toolbar that represents the Text toolbar you added in the previous exercise. Then drag the cursor on the flyout and release the mouse button when it is over the button of the macro to start.
```

#### 5.3.14 Shortcut and Temporary Override Keys

Shortcut and temporary override key combinations are used to execute a command macro. A temporary override key combination can also execute a second macro when the key combination is released. Both key types require you to define a key combination that includes at least the Shift, Ctrl, or Alt key and, in almost all combinations, one or more of the standard and virtual keys on the keyboard.

Discovering Existing Shortcut and Temporary Override Keys

The CUI Editor allows you to print or copy a list of all the shortcut and temporary override keys to your default printer or the Windows Clipboard. Both of these operations can be helpful to let users know which key combinations are available to them and can be performed by doing the following:

```
Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the Customizations In pane of the CUI Editor, select the Keyboard Shortcuts node.

In the Shortcut Keys pane, click the Type drop-down list and choose the type of keys you want to list: All keys

Accelerator (shortcut) keys

Temporary Override Keys

Click the Status drop-down list and choose the status of the keys you want to list: All

Active

Inactive

Unassigned

Do one of the following: Click Copy To Clipboard to copy a tab-delimited list of all the keys currently displayed in the list.

Click Print to output a list of all the keys currently displayed in the list.

Click OK to exit the CUI Editor.

Not all key combinations are included in the list. Those that are common Windows shortcut keys are not defined as part of a customization (CUIx) file. You can search the product's Help on the keywords shortcut keys reference and temporary keys reference to locate listings of both keyboard-shortcut types.
```

The following example explains how to create a shortcut key that starts the Wheelchair Note command created earlier in this chapter:

```
Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the Customizations In pane of the CUI Editor, expand the Keyboard Shortcuts node.

Go to the Command List pane, locate the Wheelchair Note command, and drag it to the Shortcut Keys node in the Customizations In pane. (If you have difficulty locating the command, type wheelchair in the Search Command List text box.)

With the Wheelchair Note command highlighted under the Shortcut Keys node in the Properties pane, and click in the Key(s) field. Click the ellipsis […] button to display the Shortcut Keys dialog box. Click in the Press The New Shortcut Key text box, and then press and hold the Ctrl, Shift, and N keys. CTRL+SHIFT+N should now appear in the text box. Click OK.

Click OK to save the changes and close the CUI Editor.

In the drawing window, press the key combination Ctrl+Shift+N.

When prompted, specify a point in the drawing.

You can use these steps to create a new temporary override key that toggles the current setting of the osnapz system variable:

Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

In the Customizations In pane, right-click the Keyboard Shortcuts node and click New Temporary Override.

In the in-place text editor, type Object Snap Z Toggle as the name of the new temporary override and press Enter.

Select the Object Snap Z Toggle temporary override under the Temporary Override Keys node in the Properties pane, and click in the Key(s) field. Click the ellipsis […] button to display the Shortcut Keys dialog box. Click in the Press The New Shortcut Key text box, and then press and hold the Shift and F keys. SHIFT+F should now appear in the text box. Ctrl and Alt cannot be used when defining the key combination for a temporary override key. Click OK.

Click in the Macro 1 (Key Down) field and replace the default text by typing the following: ^P'_.osnapz $M=$(if,$(and,$(getvar,osnapz),1),0,1). The macro toggles the current value of the osnapz system variable when the key combination is held and then changes it again when the key combination is released.

Click OK to save the changes and close the CUI Editor.

In the drawing window, draw a 3D box with the box command.

Enable the Endpoint running object snap.

Start the line command and position the crosshairs close to the top corner of the 3D box. The Endpoint marker should appear. Click, and the line should start from that endpoint. Cancel the line command.

Start the line command again. This time press and hold the key combination Shift+F and position the crosshairs close to the top corner of the 3D box. The Endpoint object snap marker should appear on the work plane. If the toggle does not seem to work correctly, you might need to disable Dynamic UCS in order for the temporary override key to work properly.

TIP: The tempoverride system variable needs to be set to a value of 1 in order to use temporary override keys.
```

#### 5.3.15 Double-Click Actions

Double-click actions, as the name implies, are actions performed when you double-click something; in this case, that something happens to be a drawing object in the drawing window. While a double-click action starts a command macro that is defined in the Command List pane, all of the commands assigned to the default double-click actions edit the drawing object that was double-clicked.

When possible, a specific object-related editing command is started. For example, mtedit is started when you double-click a multiline text object, or pedit is started for a polyline object. If an object does not have a double-click action defined in the main customization (CUIx) file, the Properties palette is displayed. As a double-click action is defined, you must specify the type of object that the double-click action should be performed on using the object's DXF Code 0 value. You can figure out the DXF 0 Code value for an object by using the information I mentioned earlier, in the「Object Mode Shortcut Menus」section.

The following explains how to create a double-click action for an RTEXT object that is created with the rtext command that is part of Express Tools:

```
On the ribbon, click Express Tools tab Text panel, click the panel's title bar, and then click Remote Text. You can also enter rtext at the command prompt and press Enter.

At the Enter an option [Style/Height/Rotation/File/Diesel] <Diesel>: prompt, enter d and press Enter.

In the Edit RText dialog box, type Filename: $(getvar,dwgname) and click OK.

At the Specify start point of RText: prompt, specify a point in the drawing window.

At the Enter an option [Style/Height/Rotation/Edit]: prompt, press Enter to exit the command.

Double-click the new remote text object; you should see the Properties palette displayed even though there is a command named rtedit that allows you to edit remote text.

At the command prompt, enter (cdr (assoc 0 (entget (car (entsel))))) and press Enter. Select the remote text object, and the text RTEXT is returned. RTEXT is the object name of a remote text object; this will be needed to create the double-click action.

On the ribbon, click Manage tab Customization panel User Interface.

In the CUI Editor, from the Command List pane select Create A New Command.

In the Properties pane, type Remote Text Edit in the Name field.

In the Macro field, type ._rtedit;_e;. If you opened the Long String Editor, click OK.

In the Customizations In pane, right-click the Double Click Actions node and click New Double Click Action.

In the in-place text editor, type Rtext for the name of the new double-click action and press Enter.

Select the Rtext item under the Double Click Actions node; in the Properties pane, click in the Object Name field and type RTEXT.

In the Command List pane, locate the Remote Text Edit command and then add it to the new Rtext item under the Double Click Actions node. (Type remote text edit in the Search Command List text box.) Click and drag the Remote Text Edit command to the Rtext item under the Double Click Actions node. When the cursor is over the Rtext item, release the mouse button.

Click OK to save the changes and close the CUI Editor.

Double-click the remote text object that you created in the first five steps. The Edit RText dialog box is displayed with the DIESEL expression that was added to the remote text object.
```

#### 5.3.16 Other Elements

The AutoCAD user experience has changed and evolved over the years, and so have the elements of the user interface. The ribbon and Quick Access toolbar (QAT) for the most part have replaced the use of pull-down menus and toolbars that were the primary ways of accessing commands for over a decade. The user-interface elements that I have covered in this chapter are the main user-interface elements that are most frequently used and customized. There are a few others that are not as frequently customized or are basically retired from the product. These other user-interface elements include the following:

Mouse Buttons You can specify the actions assigned to each button on your pointing device, with the exception of the left or primary mouse button, which is always the pick button. In addition to customizing the basic click event performed by a mouse button, you can customize the click action taken when the Shift and Ctrl keys are held while pressing a mouse button.

Tablet Buttons and Menus You can specify the actions assigned to each button on your tablet's pointer device, with the exception of the primary mouse button, which is always the pick. Some tablet pointer devices support up to 16 buttons. In addition to customizing the basic click event performed by a mouse button, you can customize the click action taken when the Shift and Ctrl keys are held while pressing a mouse button. Tablet menus allow you to map which area of the tablet represents the digitizing and drawing areas, in addition to where you can click to start a command. To help users identify each of the areas and commands, you create an overlay that sits on top of the tablet.

Image Tile Menus Image tile menus (also known as icon tile menus) allow you to associate a slide image with a command macro. The image tile menu was one of the first user interfaces that allowed you to associate an image with a command macro. The images used for the menus were created with the mslide command. Multiple slide images can be combined into a slide library and used with the image tile menu. It is common to see image tile menus used to insert blocks, but they can be used to pass values to an AutoLISP or other custom program.

Screen Menus The screen menu is a user interface that is kind of like a stack of papers. Clicking an item on the screen menu can execute a command macro or jump to a different page in the screen menu. Until recently, the screen menu was one of the oldest active user-interface elements that you could use and customize, but it has recently been retired. The screen menu can be displayed and customized after the screenmenu system variable has been redefined using the redefine command in AutoCAD 2014. Earlier releases do not require you to redefine the screenmenu system variable.

Dashboard Panels The Dashboard palette was removed from the product in AutoCAD 2009. If you are migrating from an earlier release, you can convert a dashboard panel to a ribbon panel. Dashboard panels, if they exist in a customization file, can be converted on the Transfer tab of the CUI Editor.

Refer to the product Help system for additional information on how to customize these user-interface elements or migrate them from a previous release so they can be used in the latest release.

### 5.4 Setting Up Rollover Tooltips and the Quick Properties Palette

Rollover tooltips and the Quick Properties palette, shown in Figure 5.28, allow you to quickly query and change the property values of an object. Instead of having to select an object to view its properties, you can position the cursor over an object to see the current value of several properties for an object in a tooltip. Which properties are displayed for the rollover tooltip can be customized using the CUI Editor.

Figure 5.28 Rollover tooltip and Quick Properties panel displaying the properties for an arc

The Quick Properties palette (quickproperties command) is also a convenient way to query the property values of an object, but also to be able to edit values. You can specify which properties are displayed on the Quick Properties palette by using the CUI Editor, and you can control the appearance and behavior of the palette using the Quick Properties tab (see Figure 5.29) of the Drafting Settings dialog box (dsettings command).

NOTE: Some of the settings on the Quick Properties tab of the Drafting Settings dialog box can also be changed using the qpmode and qplocation system variables.

Figure 5.29 Controlling the appearance and behavior of the Quick Properties palette

Use the following steps to customize the properties displayed on the rollover tooltip (or Quick Properties palette) for a Hatch object:

1. Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

2. In the Customizations In pane of the CUI Editor, select the Rollover Tooltips (or Quick Properties) node.

3. In the Dynamic pane, select Hatch from the Object Type list (see Figure 5.30). If Hatch is not displayed, click Edit Object Type List at the top of the Object Type list. In the Edit Object Type List dialog box, click Hatch and then click OK.

4. In the Properties list, to the right of the Object Type list, click Area under the Geometry category.

5. Click OK to save the changes made.

6. Create a closed area and apply a hatch pattern to it.

7. Position the cursor over the hatch object, and you should see Area as a property on the rollover tooltip. If you customized the properties for the Quick Properties palette, select the hatch object and right-click. Click Quick Properties to display the Quick Properties palette if it is not already displayed.

1『

上面的信息直接套用到「块属性」的输入操作上，极大的提高了输入效率。对我的价值实在是太大了，再一次体现了「无用之学」的威力，完全是意外的收获。（2020-09-11）

1、首先命令「cui」进入「自定义用户界面」。在「鼠标悬停工具提示」和「快捷特性」里，找到「参考块」，只勾选「属性」。这样不管是快捷特性还是悬浮显示，都仅仅显示块的属性值。

2、选中一个块，右键，点最下面的「快捷特性」，点右上角 x 下面的那个「选项->设置」，进入「快捷特性」面板。关键的地方来了，勾选「选择时显示快捷特性选项板」。

设置好后，首先，鼠标停留在一个块上会自动显示出块属性的信息；其次，鼠标任意点一个块后，会自动弹出「快捷特性」面板，而且只有块属性的信息。

』

TIP: You can synchronize the properties set between rollover tooltips and the Quick Properties palette. Right-click over the Quick Properties or Rollover Tooltips nodes in the Customizations In pane of the CUI Editor, and click Synchronize With Rollover Tooltips or Synchronize With Quick properties. In the task dialog box that is displayed, click the link that represents the direction of the synchronization you want to perform.

1『这个同步的功能也很棒，已经使用，将鼠标悬浮跟快捷特性进行了同步。（2020-09-11）』

Figure 5.30 Modifying the properties displayed on the rollover tooltip for a Hatch object

### 5.5 Organizing the User Interface with Workspaces

Workspaces are used to control which user-interface elements are displayed and where they are positioned in the AutoCAD user interface. You can create and modify a workspace using the CUI Editor or directly manipulate elements in the user interface. If you show/hide user-interface elements or change their position from the AutoCAD user interface, you can save the changes to the current workspace or a new workspace with the wssave command. Directly manipulating user-interface elements is often easier than using the CUI Editor, but not all elements can be directly manipulated.

After you create a new element in the CUI Editor, you can control how and where that element is displayed with the Workspace Contents pane. Earlier in this chapter, I explained how to add a ribbon tab, pull-down menu, and toolbar to the current workspace. In earlier sections, I had you working with the current workspace only, but you can modify any workspace in the main customization (CUIx) file, create a new workspace, or even duplicate a workspace.

It is not uncommon to create multiple workspaces. For example, AutoCAD comes with several workspaces that are designed for people who are doing 2D drafting or 3D modeling. You could create separate workspaces for those who work on mechanical, architectural, or civil drawings within your company. You might also encourage users to create their own workspaces with their favorite tools, following your company standards.

These steps explain how to create a new workspace based on the Drafting & Annotation workspace that is defined in the acad.cuix file:

1. Display the CUI Editor if it is not open. On the ribbon, click Manage tab Customization panel User Interface.

2. In the Customizations In pane of the CUI Editor, expand the Workspaces node and select the Drafting & Annotation workspace.

3. Right-click over the Drafting & Annotation workspace node and select Duplicate.

4. In the Properties pane, enter Custom Workspace in the Name field.

5. Optionally, in the Properties pane, change any of the other available properties for the workspace as needed.

6. In the Workspace Contents pane, click Customize Workspace.

7. In the Customizations In pane, select the user-interface elements you want to display or deselect those you do not want displayed.

8. In the Workspace Contents pane, do any or all of the following, and then click Done: 
    
    - Select the Quick Access Toolbar node and specify if you want to display the QAT above or below the ribbon. 
    
    - Expand the Toolbars node and select the first toolbar. Change the settings in the Properties pane as needed. Do this for each toolbar that is under the Toolbars node.

    - Expand the Menus node and drag to reorder the pull-down menus for the menu bar.

    - Expand the Palettes node and select the first palette. Change the settings in the Properties pane as needed. Do this for each palette that is under the Palettes node.

    - Expand the Ribbon Tabs node and select the first tab. Change the settings in the Properties pane as needed. Do this for each tab that is under the Ribbon Tabs node.

    - Expand the first ribbon tab node under Ribbon Tabs, and select the first panel. Change the settings in the Properties pane as needed. Do this for each panel that is on the selected ribbon tab, and then do this for each tab that is under the Ribbon Tabs node.

9. Click OK to save the changes to the workspace.

You can also change the display state and position of user-interface elements from the AutoCAD user interface and update a workspace by doing the following:

1. With the CUI Editor closed, do any of the following: Quick Access toolbar: Right-click over a command or control, and then click Show Quick Access Toolbar Below/Above The Ribbon to move the QAT above or below the ribbon.

    - Ribbon tabs: Right-click over a tab and click Show Tabs, and then click the tab you want to show/hide that is associated with the current workspace. You can also click and drag a tab on the ribbon to change its display order.

    - Ribbon panels: Click a tab to set it as current and then right-click over the tab. Click Show Panel and then click the panel you want to show/hide that is associated with the tab. You can also click and drag a panel on the ribbon to change its display order, or even drag the panel outside of the ribbon to float the panel. When floating, the panel remains displayed even upon switching tabs.

    - Toolbars: On the ribbon, click View tab User Interface panel Toolbars drop-down menu <Customization Group Name> and then the name of the toolbar you want to show or hide. After a toolbar is displayed, drag it on the screen and along the inner edges of the application window to dock it.

    - Pull-down menus: On the Quick Access toolbar, click the Customization menu button located on the right side. Click Show/Hide Menu Bar to control the display of the menu bar and pull-down menus. The menubar system variable can also be used to display or hide the menu bar. You can't add or remove pull-down menus from the user interface unless you load a partial menu or use AutoLISP or a custom program.

    - Palettes: On the ribbon, click View tab Palettes and click the palettes you want to display as part of the workspace. After a palette is displayed, drag it on screen and along the edges of the application window to dock it.

    - Status bar: On the status bar, click the Application Status Bar Menu button and click Drawing Status Bar to control the state of the application and drawing-window status bars. You can also control the state of the status bar with the statusbar system variable.

2. On the QAT, from the Workspace drop-down list select Save Current As (or at the command prompt, type wssave and press Enter).

3. In the Save Workspace dialog box, select a workspace from the drop-down list to update an existing workspace or enter a name to create a new workspace. Click Save. If you selected a workspace name, click Replace.

TIP: The process for placing toolbars and palettes just where you want them can be tedious. After you finalize the position, use the Lock Toolbar/Window Positions control on the status bar to lock their position so they are not accidentally moved. You can also use the lockui system variable to lock toolbars and palettes in place.

After you have created a workspace, you must set it as current before the changes to the user interface will take place. Use any of the following methods to set a workspace as current:

```
Select a workspace from the Workspace drop-down list on the QAT, or choose one from the Workspace Switching icon on the status bar.

In the Customizations In pane of the CUI Editor, expand the Workspaces node and select the workspace you want to set as current. Right-click the workspace and select Set Current.

On the Workspace toolbar, select a workspace from the Workspace drop-down list.

Prior to launching AutoCAD, you can use the /w command-line switch with a Desktop shortcut to set a specific workspace as current. For more information on command-line switches, see Chapter 4,「Manipulating the Drawing Environment.」

While AutoCAD is running, you can use the wscurrent system variable to see which workspace is current and even switch workspaces.
```

TIP: If you want to retain any changes to the workspace that you make through the user interface before switching to a different workspace, make sure you change the When Switching Workspaces setting in the Workspace Settings dialog box (wssettings command). This dialog box also lets you specify the order in which workspaces appear on drop-down lists in the user interface.

### 5.6 Working with Customization Files

Customization (CUIx) files are used to store the definitions of the elements that make up most of the AutoCAD user interface. acad.cuix is the default customization file that ships with AutoCAD, and it's the file that you have been customizing throughout this chapter if you're using the default AutoCAD installation. You can create and load additional customization (CUIx) files that contain just your customization with the CUI Editor. I explain how to create and load CUIx files later in the「Creating CUIx Files」and「Loading CUIx Files」sections. When a CUIx file is loaded, you can also load any AutoLISP files that might be required for the command macros defined in the file. I discuss loading AutoLISP files that are related to a CUIx file later in this chapter in the「Loading AutoLISP Files」section.

Earlier AutoCAD releases shipped with files named acad.mnu and acad.cui, which were used to store the element definitions of the user interface. You can migrate user-interface elements from earlier releases using the Transfer tab of the CUI Editor. I explain how to transfer elements between two customization files in the「Transferring User-Interface Elements between CUIx Files」section.

The AutoCAD user interface supports three types of customization files:

1. Main. The main CUIx file should be writeable and typically contains most of, if not all, of the default AutoCAD user-interface elements. In most configurations, this is the acad.cuix file that ships with AutoCAD.

2. Enterprise. The enterprise CUIx file is read-only by design and typically contains your corporate customization, but it could also be the acad.cuix file that ships with AutoCAD. When the acad.cuix file is designated as the enterprise CUIx file, then your corporate customization is often designated as your main CUIx file. The enterprise CUIx file itself might not be marked as read-only, but the CUI Editor does not allow you to make changes to it.

3. Partial. Partial customization files, as the name implies, do not contain all of the elements that you might find in the standard AutoCAD user interface. The user-interface elements used by third-party utilities and plug-ins, and even the Express Tools user-interface elements, are often implemented with partial CUIx files. These typically contain a few toolbars, ribbon tabs and panels, and pull-down menus, but they can also contain dozens of additional user-interface elements.

No matter whether you use all three types of customization files or just a main CUIx file, consider storing your CUIx file in a centralized location so it can be shared with others. I recommend that you use a partial CUIx file at least for your personal and corporate customization so that you can share it with others in your company, and to make it easier to back up and transition to the latest release.

TIP: You can edit the elements of the enterprise CUIx file by setting it as the main customization file and by setting the main customization file as the enterprise CUIx file. To make this easier, you can create two different user profiles that invert the paths for the main and enterprise CUIx files.

#### 5.6.1 Creating CUIx Files

No matter whether you are creating a main, enterprise, or partial CUIx file, the process is exactly the same. The contents and how the file is being loaded are what differentiate one from another. While you can copy and rename a CUIx file through Windows Explorer or File Explorer, you should avoid doing so because it does not change the customization group name inside the file. The following steps show how to create a new CUIx file named myui.cuix:

1. On the ribbon, click Manage tab Customization panel User Interface.

2. In the CUI Editor, click the Transfer tab.

3. In the Customizations In pane, on the right click Create A New Customization File.

4. Click Save The Current Customization File.

5. In the Save As dialog box, browse to the folder that you created for this book and type myui in the File Name text box. Click Save.

If you want to create a new CUIx file from an existing CUIx file, you will want to open the file and then save it with a new name. Use these steps to open and save a CUIx file with a different name:

1. On the ribbon, click Manage tab Customization panel User Interface.

2. In the CUI Editor, click the Transfer tab.

3. On the right side of the Customizations In pane, click Open Customization File.

4. In the Open dialog box, browse to and select the CUIx file you want to open. Click Open.

5. Click Save The Current Customization File.

6. In the Save As dialog box, browse to the folder that you want to save the new file to and enter a new name in the File Name text box. Click Save.

#### 5.6.2 Loading CUIx Files

After you create a CUIx file or obtain a CUIx file from a third-party developer or consultant, you must load it so the elements defined in the file can be accessed from the AutoCAD user interface. How you plan to use a CUIx file determines how the file needs to be loaded. You can load a CUIx file using one of the following options:

1. Main Customization File. Click the Application Menu button and then click Options. In the Options dialog box, select the Files tab and expand the Customization Files node. Expand the Main Customization File node and select the path to the CUIx file. Click Browse. In the Select A File dialog box, browse to and select the CUIx file you want to load as the main customization file. Click Open, and then click OK to close the Options dialog box.

2. Enterprise Customization File. Click the Application Menu button and then click Options. In the Options dialog box, select the Files tab and expand the Customization Files node. Expand the Enterprise Customization File node and select the path to the CUIx file. Click Browse. In the Select A File dialog box, browse to and select the CUIx file you want to load as the enterprise customization file. Click Open, and then click OK to close the Options dialog box.

3. Partial Customization File. On the ribbon, click Manage tab Customization panel User Interface. In the CUI Editor, select the Customize tab, and in the Customizations In pane, click Load Partial Customization File. In the Open dialog box, browse to and select the CUIx file that you want to load. Click Open. The CUIx file is added to the Partial Customization Files node of the main customization file.

#### 5.6.3 Transferring User-Interface Elements between CUIx Files

The CUI Editor not only allows you to create and modify elements for the user interface and manage CUIx files, but also lets you copy or migrate elements between two CUIx files or an earlier menu source (MNS) or customization (CUI) file. You transfer elements between files using the Transfer tab. Load the files that you want to work with, and then drag elements between the available nodes in the Customization In panes. Transferring an element also transfers any associated commands, ribbon panels, and toolbars. When transferring elements, you can only drag and drop elements of the same type. So, there's no dragging ribbon tabs to a Quick Access toolbar (QAT).

#### 5.6.4 Loading AutoLISP Files

It is not uncommon that the commands in your CUIx files might use functions or commands defined in an AutoLISP file. There are a few different methods that you can use to make sure that the AutoLISP programs your user-interface elements rely on are loaded for use by your CUIx file. The following outlines the methods you can use to load an AutoLISP file for use with a CUIx file:

1. AutoCAD searches for an AutoLISP Menu (MNL) file that has the same name as a CUIx file that is being loaded. If the MNL file is located, AutoCAD loads it along with the CUIx file into each drawing that is created or opened while the CUIx file is loaded.

2. Using the CUI Editor, you can add AutoLISP (LSP) files to the LISP Files node. These files are loaded when the CUIx file is loaded and a new drawing is created or opened.

3. Using the Load/Unload Applications dialog box (appload command), you can manually load an AutoLISP (LSP) file or add it to the Startup Suite. The Startup Suite loads the files that are listed when a new drawing is created or an existing drawing file is opened.

1『 lsp 文件名跟 cuix 文件名保持一致。』

### 5.7 Controlling the Tools on the Status Bars

AutoCAD supports two status bars: drawing and application window. By default, both are combined into a single bar and displayed along the bottom of the application window. While you can control which tools are displayed, you can't create and place new tools on the status bar. Even though you can't add new tools, it can be helpful to hide those that you do not use, such as 3D Object Snap and Allow/Disallow Dynamic UCS if you do not work on 3D models.

Unlike other user-interface elements, the settings that control the display of the tools on the toolbar are not stored in the CUIx file or controlled by the current workspace, with the exception of the current status-bar state (statusbar system variable). To control which tools are displayed on the status bar, do one of the following:

1. Application Status Bar Menu. Click the Application Status Bar Menu button (see Figure 5.31) to control the display of the coordinates area and drafting aids on the status bar. You can also access controls related to layers, drawing views, workspaces, and display locking, among others. This menu allows you to display the Tray Settings dialog box and toggle the display of the drawing status bar.

2. Drawing Status Bar. Menu When the drawing status bar is displayed, it contains the controls related to annotation scaling and the system tray. Click the drawing status-bar menu to toggle which annotation scaling tools you want to display.

3. Tray Settings Dialog Box. Controls the display of icons and notifications for services that are running in the application or current drawing. You can also specify the duration that a notification is displayed for, or whether it is displayed until you close it. The actual enabling or disabling of a service is not handled in this dialog box; you must do that on a feature-by-feature basis. For example, you can use the xrefnotify system variable to control the display of xref notifications or the layernotify system variable to display alerts for unreconciled new layers.

Figure 5.31 Controlling the display of tools on the status bar
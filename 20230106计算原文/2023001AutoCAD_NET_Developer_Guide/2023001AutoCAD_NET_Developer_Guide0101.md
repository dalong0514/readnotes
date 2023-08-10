## 0101. About .NET and the AutoCAD .NET API (.NET)

2019073AutoCAD.NET开发指南

This introduction describes the concepts of exposing AutoCAD® objects through a managed .NET application programming interface (API). The AutoCAD .NET API allows you to automate tasks such as creating and modifying objects stored in the database of a drawing file or change the contents of a customization file. This guide covers using Microsoft® Visual Studio® 2019, and the programming languages Microsoft® Visual Basic® .NET (referred to in this guide as VB.NET) and Microsoft® Visual C#® with the AutoCAD .NET API.

### 1.1 Developer's Guide Organization (.NET)

This guide provides information on how to use the AutoCAD .NET API with Microsoft Visual Studio and the programming languages VB.NET and C#. Information specific to developing applications using Microsoft Visual Studio can be found under the topics “Getting Started with Microsoft Visual Studio” and “Develop Applications with VB.NET and C#.”

### 1.2 Overview of the AutoCAD .NET API (.NET)

The AutoCAD .NET API enables you to manipulate the application and drawing files programmatically with the assemblies or libraries that are exposed. With these objects exposed, they can be accessed by many different programming languages and environments.

There are several advantages to implementing a .NET API for AutoCAD:

1 Programmatic access to drawings is opened up to more programming environments. Before the .NET API, developers were limited to ActiveX® Automation and languages that supported COM, AutoLISP®, and C++ with ObjectARX.

2 Integrating with other Windows® based applications, such as Microsoft Excel and Word, is made dramatically easier by using an application’s native .NET API or exposed ActiveX/COM library.

3 The .NET Framework is designed for both 32-bit and 64-bit operating systems.

Note: Starting with AutoCAD 2020, 32-bit support is no longer available.

4 Allows access to advanced programming interfaces with a lower learning curve than those for more traditional programming languages such as C++.

Objects are the main building blocks of the AutoCAD .NET API. Each exposed object represents a precise part of the program or a drawing, and they are grouped into different assemblies and namespaces. There are many different types of objects in the AutoCAD .NET API. For example:

1 Graphical objects such as lines, arcs, text, and dimensions

2 Style settings such as text and dimension styles

3 Organizational structures such as layers, groups, and blocks

4 The drawing displays such as view and viewport

5 The drawing and application

#### Unmanaged to Managed Class Mappings

Most ObjectARX classes map to one managed wrapper class. Although there are exceptions, the first four letters of an ObjectARX class name frequently provide a clue to the corresponding managed namespace. The following table shows the most likely mapping of ObjectARX class prefixes to .NET namespaces.

ObjectARX class prefixes and .NET namespaces

| Unmanaged Prefix | Managed Namespace |
| --- | --- |
| AcAp | Autodesk.AutoCAD.ApplicationServices |
| AcBr | Autodesk.AutoCAD.BoundaryRepresentation |
| AcCm | Autodesk.AutoCAD.Colors |
| AcDb | Autodesk.AutoCAD.DatabaseServices |
| AcGe | Autodesk.AutoCAD.Geometry |
| AcGi | Autodesk.AutoCAD.GraphicsInterface |
| AcLy | Autodesk.AutoCAD.LayerManager |
| AcPl | Autodesk.AutoCAD.PlottingServices |
| AcRx | Autodesk.AutoCAD.Runtime |
| AcUt | Autodesk.AutoCAD.DatabaseServices/Autodesk.AutoCAD.ApplicationServices |

See “Mapping ObjectARX Classes to Managed Types” in the AutoCAD Managed Class Reference for a complete listing of direct class equivalences.

### 1.3 Components of the AutoCAD .NET API (.NET)

The AutoCAD .NET API is made up of different DLL files that contain a wide range of classes, structures, methods, and events that provide access to objects in a drawing file or the application. Each DLL file defines different namespaces which are used to organize the components of the libraries based on functionality.

The main DLL files of the AutoCAD .NET API that you will frequently use are:

1 AcCoreMgd.dll. Use when working within the editor, publishing and plotting, and defining commands and functions that can be called from AutoLISP.

2 AcDbMgd.dll. Use when working with objects stored in a drawing file.

3 AcMgd.dll. Use when working with the application and user interface.

4 AcCui.dll. Use when working with customization files.

#### Reference an AutoCAD .NET API DLL

Before classes, structures, methods, and events found in one of the AutoCAD .NET API related DLLs can be used, you must reference the DLL to a project. After a DLL is referenced to a project, you can utilize the namespaces and the components in the DLL file in your project.

Once a AutoCAD .NET API DLL is referenced, you must set the Copy Local property of the referenced DLL to False. The Copy Local property determines if Microsoft Visual Studio creates a copy of the referenced DLL file and places it in the same directory as the assembly file (or executable file) that is generated when building the project. Since the referenced files already ship with the product, creating copies of the referenced DLL files can cause unexpected results when you load your assembly file.

1『这几个库文件引用，复制设为 false，原来这里的文档里也有提到。这个设置最开始学习的时候接触到的，但一直不知道原因。（2023-08-09）』

An assembly file is the source code from an Intermediate Language (IL) based program and is executed by invoking the .NET runtime; called the CLR, Common Language Runtime. The CLR compiles an assembly into native code right before it is executed by the operating system or another application. The process of compiling at runtime just before execution is often referred to as Just-In-Time (JIT) compiling. You can pre-compile an assembly using NGEN to create a native executable. Using NGEN can make your assembly more secure since it cannot be viewed using an IL disassembler.

#### Location of AutoCAD .NET API DLL Files

The AutoCAD .NET API DLL files can be located at <drive>:\Program Files\Autodesk\<release> or as part of the latest ObjectARX SDK which can be downloaded from http://www.objectarx.com or the Autodesk Developer Network (ADN) website (https://www.autodesk.com/adn).

After the ObjectARX SDK is installed, the DLL files can be found in the inc folder under the main install folder.

Note: The DLLs in the ObjectARX SDK are simplified versions of the same files that ship with AutoCAD, as they do not contain dependencies on the AutoCAD user interface. It is recommended that you download and install the ObjectARX SDK, and then reference the DLL files that come with the SDK instead of those that are found in the install directory of AutoCAD or the AutoCAD-based program.

1『这里建议用 ObjectARX SDK 里的库，之前陶斯豪给的几个包应该就是这个。是把它放到本地自己的一个路径里。项目里引用的那几个库的时候直接从这里引用，而非从 AutoCAD 的安装路径那边引用。（2023-08-09）』

#### Procedures

To download and install the latest ObjectARX SDK

1 Launch your default Internet browser application and browse to http://www.objectarx.com.

2 On the Web page, click License & Download.

3 Fill in the required fields and select ObjectARX for AutoCAD <release>. Click Submit.
	
4 On the Download page, click Download Now to use the Download Manager or click Standard Download Method to use the default download method of your Internet browser.

5 Click Save or the option used to save the file to your local drive.

6 Specify a location to download the ObjectARX SDK package file.

7 Once the package file is downloaded, browse to the location you saved it to and double-click it.

The install wizard is displayed.

8 In the ObjectARX <Release> dialog box, specify a new install location or leave the default install location. Click Install.
The install wizard closes after it is finished if no problems were encountered.

To install the Managed .NET project wizard

1 Launch your default Internet browser application and browse to https://www.autodesk.com/developautocad.

2 Download and unzip the <release> .NET Wizards.zip file.

3 After browsing to the location of the unzipped files, double-click the <release> dotNET Wizards.msi file.

4 In the AutoCAD .NET Wizards dialog box, click Next.

5 On the Select Installation Folder page, click Browse to specify a new installation location for the wizard or leave the default location. Click Next.

6 Click Next again to confirm installation of the wizard.

7 Click Close to close the installer.

To reference an AutoCAD .NET API DLL

1 In Microsoft Visual Studio, click View menu => Solution Explorer to display the Solution Explorer if it is not already displayed.

2 In the Solution Explorer, on the toolbar along the top, click Show All Files.

3 Right-click the References node and click Add Reference.

4 In the Add Reference dialog box, Browse tab, select the DLL file that contains the library you want to use and click OK.

5 In the Solution Explorer, click the plus sign to the left the References node to expand it.

5 Select the referenced library from the References node.

6 Right-click over the selected reference and click Properties.

7 In the Properties window, click the Copy Local field and select False from the drop-down list.

### 1.4 Overview of Microsoft Visual Studio (.NET)

Microsoft Visual Studio is an object-oriented programming environment that runs independently of AutoCAD and other applications. While Microsoft Visual Studio is external to AutoCAD, it is able to interact with the AutoCAD through either the native AutoCAD .NET API or ActiveX/COM library.

#### Which Edition of Microsoft Visual Studio to Use (.NET)

Microsoft Visual Studio is available in multiple versions and editions.

If you are targeting AutoCAD 2021 or AutoCAD 2021-based programs, you should use:

Microsoft Visual Studio 2019

Microsoft .NET Framework 4.8

If you are targeting AutoCAD 2020 or AutoCAD 2020-based programs, or AutoCAD 2019 or AutoCAD 2019-based programs, you should use:

Microsoft Visual Studio 2017 with Update 2

Microsoft .NET Framework 4.7

If you are targeting AutoCAD 2017 or AutoCAD 2017-based programs, or AutoCAD 2018 or AutoCAD 2018-based programs, you should use:

Microsoft Visual Studio 2015 with Update 3

Microsoft .NET Framework 4.6

If you are targeting AutoCAD 2015 or AutoCAD 2015-based programs, or AutoCAD 2016 or AutoCAD 2016-based programs, you should use:

Microsoft Visual Studio 2012 or Microsoft Visual Studio 2013

Microsoft .NET Framework 4.5

If you are targeting AutoCAD 2012 or AutoCAD 2012-based programs through AutoCAD 2014 or AutoCAD 2014-based programs, you should use:

Microsoft Visual Studio 2010 or Microsoft Visual Studio 2012

Microsoft .NET Framework 4.0

If you are targeting AutoCAD 2010 or AutoCAD 2010-based programs, or AutoCAD 2011 or AutoCAD 2011-based programs, you should use:

Microsoft Visual Studio 2008 with Service Pack 1

Microsoft .NET Framework 3.5 with Service Pack 1

If you are targeting AutoCAD 2007 or AutoCAD 2007-based programs through AutoCAD 2009 or AutoCAD 2009-based programs, you should use:

Microsoft Visual Studio 2005

Microsoft .NET Framework 2.0 or later

Microsoft Visual Studio is offered in multiple editions: for free and for pay. The free products are part of Microsoft Visual Studio Express, while the for pay products vary by name and price due to the different development tools that are incorporated into them. Microsoft Visual Studio Professional provides improved debugging over the Microsoft Visual Studio Express products along with a number of other features. The most common edition of Microsoft Visual Studio used by developers is Microsoft Visual Studio Professional.

Note: While it is possible to use Microsoft Visual Studio Express with the AutoCAD .NET API, this guide assumes you are using one of the other product versions such as Microsoft Visual Studio Professional or Microsoft Visual Studio Ultimate.
There are four main advantages to using Microsoft Visual Studio:

1 Robust and accessible development environment that has a modest learning curve.

2 VB.NET syntax is similar to VBA, which makes it an ideal environment for those that already know VBA.

3 Visually intuitive and extensive dialog box creation tools.

4 Projects can be built as a standalone executable or DLL assembly which can then be loaded for execution.

For more information on the different editions of Microsoft Visual Studio, see https://www.visualstudio.com/ and https://www.visualstudio.com/vs/community/.

#### Dependencies and Restrictions (.NET)

Unlike ActiveX Automation, there are fewer issues with library conflicts when other applications are installed, reinstalled, or uninstalled. The reason for fewer compatibility issues is that the .NET Framework is a standardized platform. However, you can still run into dependency issues. To avoid dependency issues between AutoCAD and the .NET Framework, be sure to use the same or an earlier version of the .NET Framework with your VB.NET or C# project that the target release of AutoCAD uses.

#### Programming Differences Between C++ and .NET (.NET)

There are some distinct differences between ObjectARX classes and their .NET counterparts; these differences require some subtle but important code practice changes.

The following sections offer general suggestions for working with the managed wrapper classes.

Memory Management and Dispose Pattern

C++ uses destructors to clean up resources. ObjectARX managed wrappers implement the IDisposable interface to do the same. The managed wrappers derive from the common base class DisposableWrapper, whose purpose is to manage the unmanaged memory.

Because the underlying resources used by ObjectARX managed wrappers are unmanaged classes, you must actively call Dispose on the managed wrappers. Doing so releases the resources owned by base types all the way up the hierarchy. Do not rely on .NET garbage collection to free the memory used by unmanaged resources.

Object Identity

The ObjectARX managed wrappers do not guarantee that you receive the same .NET object every time you access a C++ object. For example, opening the same object in the database twice in succession yields two different wrappers. However, DisposableWrapper (the common base class for ObjectARX managed wrappers) overrides Equals and GetHashCode. Equals compares the underlying unmanaged pointers, and GetHashCode returns the underlying unmanaged pointer. This effectively ensures that .NET clients perceive these two different wrapper objects as identical.

Error Handling

ObjectARX uses the return value of functions to indicate error conditions. The preferred way of signaling error in .NET is to raise an exception. The ObjectARX managed wrappers translate ObjectARX error codes into exceptions. Some error codes are mapped to .NET native exceptions, while others are mapped to custom exception types exposed by the managed wrappers.

Get and Set Methods Versus Properties
Object properties are modeled as get and set methods in C++. On the other hand, .NET makes properties a primary abstraction of the execution environment. The ObjectARX managed wrappers map get and set methods to .NET properties appropriately.

Reactors Versus Events

ObjectARX uses reactors to model events. Because .NET makes events a primary abstraction, the ObjectARX managed wrappers map reactors to events.

Unmanaged reactors require two classes: the event source class and the abstract reactor class. The event source class is instantiated by the system and exposes the addReactor() and removeReactor() functions. The client derives a concrete reactor class from the abstract reactor, instantiates the concrete reactor, and adds it to the event source. The event source calls virtual functions in the concrete reactor when events occur.

The ObjectARX managed wrappers model the reactor pattern as one event source class with managed events.

Collections and Iteration

In ObjectARX, iteration methods are not standardized across classes. For the managed wrappers, two interfaces make iteration consistent. Collections implement IEnumerable. Iterators that are returned by GetEnumerator implement IEnumerator.

If you explicitly call GetEnumerator method on a dynamic object, then you need to dispose it explicitly. See the example code:

```cs
Database db = HostApplicationServices.WorkingDatabase;
dynamic dynamicDb = HostApplicationServices.WorkingDatabase;
var lineTypeTable = dynamicDb.LinetypeTableId;
var stEnumerator = lineTypeTable.GetEnumerator();
stEnumerator.Dispose();
```

Command Registration

ObjectARX allows extension applications to register commands with AutoCAD. This registration is implicit: the application must be run to find out what commands it wants to register.

.NET encourages applications to use declarative style to define their behavior. The ObjectARX managed wrappers make command registration declarative. Custom attributes are used to denote command methods. See Command Definition (.NET) for code examples and detailed information.

Global Functions

Global functions do not exist in the ObjectARX managed wrappers, so many of the ObjectARX global functions map to new .NET objects or to new properties on existing objects.

For example, one group of ObjectARX global functions is used by applications to interact with the AutoCAD command prompt. In the ObjectARX managed wrappers, a new CommandLinePrompt class encapsulates this functionality.

Another category of ObjectARX global functions returns pointers to instance objects. For example, ObjectARX uses acdbTransactionManagerPtr() to return a pointer to the AcDbTransactionManager. Functions like this have been mapped to object properties in .NET, so the database now has a TransactionManager property.

#### C++ Interoperability (.NET)

Your .NET application can include C++ portions, so you can also use ObjectARX APIs that do not have managed wrappers. The ObjectARX managed wrapper classes have a consistent property and method that enable you to go back and forth between the managed and unmanaged object.

A pointer to the underlying unmanaged object from a managed object can be obtained using the UnmanagedObject property. You can create a managed object from an unmanaged object with the DisposableWrapper.Create() method.

#### COM Interoperability (.NET)

Microsoft Visual Studio can utilize both native .NET and COM interfaces in the same project. By utilizing COM interop, you can migrate existing code that might have been written in Visual Basic 6 or VBA without having to completely rewrite it. To access the AutoCAD automation objects from a project created in Microsoft Visual Studio, create references to the following files:

1 The latest AutoCAD or AutoCAD-based Type Library, acax24enu.tlb , located at <drive>:\Program Files\Common Files\Autodesk Shared.

2 The AutoCAD/ObjectDBX Common 24.0 Type Library, axdb24enu.tlb, located at <drive>:\Program Files\Common Files\Autodesk Shared.

Note: The previous mentioned type libraries are also available as part of the ObjectARX SDK.

These references will make the following primary interop assemblies available:

1 Autodesk.AutoCAD.Interop.dll (for AutoCAD-specific types)

2 Autodesk.AutoCAD.Interop.Common.dll (for types shared by ObjectDBX™ host applications)

The interop assemblies are located in the global assembly cache; they map automation objects to their .NET counterparts.

After you reference the type libraries, you should import the Autodesk.AutoCAD.Interop and Autodesk.AutoCAD.Interop.Common namespaces into the code modules that will utilize the objects defined in the libraries, as in the following examples:

VB.NET
Imports Autodesk.AutoCAD.Interop
Imports Autodesk.AutoCAD.Interop.Common

C#
using Autodesk.AutoCAD.Interop;
using Autodesk.AutoCAD.Interop.Common;
can declare variables based on objects defined in the libraries, as in the following examples:

VB.NET
Dim objAcApp As AcadApplication
Dim objLine As AcadLine

C#
AcadApplication objAcApp;
AcadLine objLine;

The interop assemblies can be helpful in making the transition from VBA to VB.NET. However, in order to take full advantage of everything that .NET and the AutoCAD .NET API have to offer, you will need to rewrite your existing VBA code.

You can get a pointer to a COM object from the corresponding .NET object by using the following properties from the following objects:

ApplicationServices.Application.AcadApplication
DatabaseServices.Database.AcadDatabase
ApplicationServices.Document.AcadDocument

A COM object can be obtained from a .NET object using the FromAcadXxx static function. For example, Database.FromAcadDatabase gets the .NET database object from the COM database object.

Create and Reference the Application

AutoCAD .NET applications can utilize the same type library (acax24enu.tlb) as AutoCAD automation projects. The type library is located in <drive>:\Program Files\Common Files\Autodesk Shared.

AutoCAD .NET applications also use the same version-dependent ProgID for the CreateObject, GetObject, and GetInterfaceObject functions.

You can use the product ProgID to create a new instance of the AutoCAD application ("AutoCAD.Application"), and specify the major and minor number of the release to restrict your application to a specific release or all the releases that are binary compatible with each other.

For example,

CreateObject("AutoCAD.Application.24") attempts to create a new instance of AutoCAD 2021.
CreateObject("AutoCAD.Application.23.1") attempts to create a new instance of AutoCAD 2020, even if another release that shares the same major version of the product is installed.
CreateObject("AutoCAD.Application.23") attempts to create a new instance of AutoCAD 2019 or AutoCAD 2020.
CreateObject("AutoCAD.Application.22") attempts to create a new instance of AutoCAD 2018.
CreateObject("AutoCAD.Application.21") attempts to create a new instance of AutoCAD 2017.
CreateObject("AutoCAD.Application.20.1") attempts to create a new instance of AutoCAD 2016, even if another release that shares the same major version of the product is installed.
CreateObject("AutoCAD.Application.20") attempts to create a new instance of AutoCAD 2015 or AutoCAD 2016.

Note: You must have the corresponding release installed that you are trying to create an instance of.

If you are using ActiveX/COM from an in-process DLL (Class Library) and want to reference the AutoCAD application object, you can use Autodesk.AutoCAD.ApplicationServices.Application.AcadApplication property.

### 1.5 For More Information (.NET)

This guide assumes that you have working knowledge of either the VB.NET or C# programming languages, and does not attempt to duplicate or replace the abundance of documentation available on either of these programming languages. If you need more information on VB.NET or C#, and using Microsoft Visual Studio, see the Help system for Microsoft Visual Studio developed by Microsoft, available from the Help menu in Microsoft Visual Studio.

### 1.6 Sample Code (.NET)

This guide and the ObjectARX SDK together contain a large number of sample projects, subroutines, and functions that demonstrate the use of the classes, structures, methods, properties, and events that make up the AutoCAD .NET API.

You can also find sample projects that demonstrate some of the aspects of the AutoCAD .NET API on the Autodesk website at https://www.autodesk.com/developautocad. These sample projects show a wide range of functionality, from working with database objects to working with sheet sets.

Many of these samples show how to combine various aspects of the VB.NET and C# programming languages with the power of the AutoCAD .NET API to create custom applications.

Additionally, sample code in the help documentation related to the AutoCAD .NET API can be copied to the clipboard and pasted directly into an open code editor window in Microsoft Visual Studio, and then built and loaded in AutoCAD. At the top of most code samples in this guide are the namespaces that are required for that particular sample. Add those that are needed to top of the code module in your project.

Note: The AutoCAD .NET samples in the help documentation contain limited error handling and disposing of objects to keep the concepts simple and easy to read. You should apply additional error handling and checking when using any sample code in your project.

Procedures

To run the sample code from the Help files

1 In Microsoft Visual Studio, open a code editor window, add the proper namespaces and define a class if one does not already exist.

2 Copy the sample code from the Help file and paste the copied code into the defined class.

3 In Microsoft Visual Studio, click Build menu  Build <Project>.

4 In AutoCAD, at the Command prompt, enter netload.

5 In the Choose .NET Assembly dialog box, select the built assembly file. Click Open.

6 At the Command prompt, enter the name of the command defined inside the CommandMethod attribute.

### 1.7 Transition from Visual Basic for Applications (.NET)

AutoCAD continues to support VBA, but the VBA components must be enabled by downloading and installing them from https://www.autodesk.com/vba-download.

Based on your development needs, you might want to consider migrating your existing VBA projects to .NET. Switching to .NET would allow you to avoid the need to install the VBA components on each workstation. You can continue to use the AutoCAD ActiveX Automation library in .NET to help make your transition from VBA to VB.NET easier.

For information on migrating from VBA to VB.NET, see https://adndevblog.typepad.com/autocad/devtv/. Use the link to access the 'DevTV: AutoCAD VBA to VB.NET Migration Basics' video on migrating VBA code to VB.NET.

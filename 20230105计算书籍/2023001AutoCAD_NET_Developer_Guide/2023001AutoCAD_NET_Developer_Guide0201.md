## 0201. Getting Started with Microsoft Visual Studio (.NET)

2019073AutoCAD.NET开发指南

This chapter introduces you to the AutoCAD® .NET API and some of the basics of the Microsoft® Visual Studio® development environment. Along with an introduction to the development environment, you will also learn about the NETLOAD command in AutoCAD and some of the terminology used throughout this guide.

### 2.1 Understand Microsoft Visual Studio Projects (.NET)

Project files created with Microsoft Visual Studio are not specific to AutoCAD, but do contain specific project settings that you will need to be familiar with in order to create a DLL assembly file that can be loaded into AutoCAD. This guide discusses creating projects for Visual Basic® (VB) .NET and Visual C#® with and without the AutoCAD .NET Wizard.

A project is a collection of code and resource files; class modules, WPF windows, and Windows forms that work together to perform a given function. When a project is created, a solution is also created which contains the project you are creating. A solution is used to reference one or more projects. Usually you do not have to work with a solution directly unless you want to reference the exposed functionality of other projects.

An example of a multi-project solution is when you have a new project and an existing project that contain a set of methods, functions, and classes that you want to use with a new project.

A solution can contain any combination of VB.NET and C# projects. Using different types of projects in a single solution allows each developer to use the programming language of his or her choice.

Project and solution files have the following file extensions:

VBPROJ - Microsoft Visual Basic (VB) .NET project file

CSPROJ - Microsoft Visual C# project file

SLN - Microsoft Visual Studio solution file

### 2.2 Define the Components in a Project (.NET)

Each project can contain many different components. The different components of a project can contain class modules, forms, references, and resources.

Class Modules

Components that contain public and private procedures and functions. Class modules are used to define custom namespaces. Within a namespace, you define the procedures used for your program and define the structures to implement custom commands and functions that can be called from AutoLISP.

Forms

Form components contain custom dialog boxes you lay out for use with your project. Forms in your project are displayed using a procedure or function, unless you build a stand-alone application. Windows forms, WPF windows, and user controls are some of the form types that can be part of a project. For this guide, forms can mean either Windows forms and WPF windows.

References

References are used to indicate which projects or libraries your project uses.

Topics in this section

#### Per Document Data (.NET)

Global data can be temporally stored in memory at the document level.

When the AutoCAD program loads a managed application, it queries the application's assembly for one or more PerDocumentClass custom attributes. If instances of this attribute are found, an instance of each attribute's associated type is created for each document open in the AutoCAD drawing environment. New instances of the types are then created for any documents that are opened thereafter.

The type associated with a PerDocumentClass attribute must provide either a Public constructor that takes a document argument or a Public Static Create method that takes a document argument and returns an instance of the type. If the Create method exists, it will be used, otherwise the constructor will be used. The document that the type instance is being created for will be passed as the document argument so that the type instance knows with which document it is associated.

The following procedure describes how to use the PerDocumentClass attribute.

In the assembly context, declare a PerDocumentClass attribute for each class that you want to be instantiated for each document.

Pass the type of the class to the PerDocumentClass attribute.

Note: This attribute must be declared in the assembly context.

### 2.3 View Project Information (.NET)

The Solution Explorer, which displays the current solution and a list of all loaded projects, also displays the code, class, and form module files contained in each loaded project, and the references to the external libraries used by each project.

The Solution Explorer has its own toolbar, which can be used to open various project components for editing. Use the View Code button to open the code for a selected module in the Editor Window. Use the Properties button to set focus to the Properties window and the properties of the selected item.

The Solution Explorer is visible by default. If it is not visible, click View menu => Solution Explorer or press Ctrl+Alt+L.

### 2.4 Work with Microsoft Visual Studio Projects (.NET)

An open solution or project file can be viewed and accessed from the Solution Explorer. The Solution Explorer allows you to add new items and projects to the current solution and projects, unload a project from the current solution, change the properties of an opened solution or project, and add references to a project in the current solution, among many choices. All available tasks for working with the current solution or project can be accessed via the right-click menu of the Solution Explorer.

Procedures

To start Microsoft Visual Studio

Windows 8.1: On the Start screen, type visual. In the Search bar, click Visual Studio 2019.

Windows 10: On the Windows Start menu or screen, click All Apps => Visual Studio 2019.

#### Create a New Project (.NET)

New projects are created based on a project template. When creating a new project that will be built into a DLL assembly that will be loaded into AutoCAD, use the Class Library template that comes with Microsoft Visual Studio or one of the AutoCAD Managed project application templates that get installed with the AutoCAD .NET Wizard. Both types of templates are available for the VB.NET and C# programming languages. After a new project is created, you will need to reference the files that make up the AutoCAD .NET API.

Procedures

To create a new project using a standard template

1 In Microsoft Visual Studio, click File menu => New => Project (or click File menu => New Project).

2 In the New Project dialog box, Installed Templates tree, expand Other Languages => Visual Basic or Visual C# and select Windows.

3 Under Templates, select Class Library.

4 In the Name box, enter a name for the new project.

5 In the Location box, enter a location or click Browse to select a folder for the new project.

6 Optionally, from the Selection drop-down list, select Create New Solution, Add to Solution, or Create in New Instance to determine how the new project should be created in relation to the solution that is currently open.

7 Optionally, select the Create Directory for Solution check box to create a sub-folder before creating the new solution and project. Select the Add to Source Control check box to add the solution and project to a source control database.

8 In the Solution Name box, enter a name for the new solution that the project will be added to.

9 Click OK.

To create a new project using an AutoCAD Managed template

Before using one of the AutoCAD Managed templates, you must first download and install the latest release of the ObjectARX SDK.

1 In Microsoft Visual Studio, click File menu  New  Project (or click File menu => New Project).

2 In the New Project dialog box, Installed Templates tree, expand Other Languages => Visual Basic or Visual C# and select Autodesk.

3 Under Templates, select AutoCAD <release> VB Plug-in or AutoCAD <release> C Sharp Plug-in.

4 In the Name box, enter a name for the new project.

5 In the Location box, enter a location or click Browse to select a folder for the new project.

6 Optionally, from the Selection drop-down list, select Create New Solution, Add to Solution, or Create in New Instance to determine how the new project should be created in relation to the solution that is currently open.

7 Optionally, select the Create Directory for Solution check box to create a sub-folder before creating the new solution and project. Select the Add to Source Control check box to add the solution and project to a source control database.

8 In the Solution Name box, enter a name for the new solution that the project will be added to.

9 Click OK.

10 In the AutoCAD .NET Wizard Configurator dialog box, specify the libraries to reference to the project.

11 Click OK.

#### Open an Existing Project or Solution (.NET)

When you open a project or solution in Microsoft Visual Studio, the code editor and Windows Form Designer windows are opened in the same state they were in when the project was last saved. Once a project or solution is opened, use the Solution Explorer to navigate between the files of the opened project or solution.

Procedures

1 To open an existing project or solution file

2 In Microsoft Visual Studio, click File menu  Open  Project/Solution (or click File menu  Open Project).
In the Open Project dialog box, browse to and select the project file to open.

3 The Open Project dialog box will allow you to open a wide range of project files which include VB.NET and C# projects, Microsoft Visual Studio .NET solutions, and Microsoft Visual C++ projects. Use the Objects of Type drop-down list to control which type of projects or solutions you see in the file selection area of the Open Project dialog box.

Note: You cannot open a VBA project saved as a DVB file with Microsoft Visual Studio. If you are migrating from VBA to VB.NET or C#, you can copy your code from the AutoCAD VBA development environment to an open code editor window in Microsoft Visual Studio and make the necessary changes.

For information on migrating from VBA to VB.NET, see https://adndevblog.typepad.com/autocad/devtv/. Use the link to access the 'DevTV: AutoCAD VBA to VB.NET Migration Basics' video on migrating VBA code to VB.NET.

3 Click Open.

#### Save a Project or Solution (.NET)

Microsoft Visual Studio is a contextual based development environment, meaning that the current item selected determines the available features in the development environment. Controlling which changed files you save or how you want to save them is determined by the Solution Explorer.

Once a project or solution is selected from the Solution Explorer, you can save it with its current name, or perform a Save As on it to create a copy of the file. You can select one or more items at a time in the Solution Explorer by pressing and holding the Ctrl key before selecting an item. Most often, you will be saving all changed items at the same time.

#### Work with Multiple Projects in a Solution (.NET)

A solution can contain multiple projects. Working with multiple projects is not much different than working with a single project. Use the Solution Explorer to navigate between the projects in the current solution.

Add a project to a solution
You might add a project to a solution to copy code between projects. You might want to reference the procedures, functions and classes in one project and use them in another project. By adding multiple projects to a single solution, it allows you to use a project as a set of common utilities that you might use with more than one project.

Unload a project from a solution
Projects can be unloaded from a solution when they are no longer needed. If you no longer want a project to load with a solution, you can unload the project and then reference the compiled DLL assembly of the project instead. Working with the compiled DLL helps to prevent accidental edits to the source code.

### 2.5 Edit an Existing Project or Solution (.NET)

Once you have opened a project or solution into Microsoft Visual Studio, you can edit the projects, class modules, forms, and references using the common development environment. You can also debug and run projects from the common development environment.

### 2.6 Access and Search Referenced Libraries with the Object Browser (.NET)

The Object Browser is used to view the objects of a library referenced by the projects in a current solution. From the Object Browser, you can navigate through a referenced library like you would a directory structure. You can also use the Search menu and locate an object based on an entered keyword.

The scope of the libraries you view in the Object Browser is limited by the Browse menu drop-down list. You can limit the scope by the current solution, a specific release of the .NET Framework or a custom component list.

The left side of the Object Browser contains a navigation pane which displays the available libraries that you can navigate. The right side is divided into two halves: upper (Members pane) and lower (Description pane).

Procedures

To use the Object Browser

1 In Microsoft Visual Studio, click View menu  Object Browser (or press Ctrl+Alt+J).

The Object Browser should appear as a tab by default in the center of the development environment.

2 Optionally, from the Browse menu, select a scope in which you want to navigate or search for components.

3 Optionally, in the Search menu, enter or select a previous keyword that you want to filter the Objects pane by.

4 In the Objects pane, navigate to the object you want to view and select it.

5 In the Members pane, select one of the displayed members of the selected object to learn more about it.

### 2.7 Load an Assembly (.NET)

Once a solution and project are created, a namespace and class are defined, and one or more command or AutoLISP® function structures are implemented, you can use the NETLOAD command to load a .NET assembly.

Use the Debug Environment

Prior to loading a .NET assembly, you should determine if you need to use the Debug environment of Microsoft Visual Studio to test any logic defined in the procedures and functions you might have created. The Debug environment allows you to step through the code in the .NET assembly as it is being executed in real-time. As the code is being executed, you are able to check the values of variables and watch which logic paths of the program are executed.

For more information on using the Debug environment, see the documentation that comes with your development environment.

Procedures

To load a .NET Assembly through Debug Mode

Note: Debug features are not available in Microsoft Visual Studio Express.

1 In Microsoft Visual Studio, Solution Explorer, right-click the project you want to load. Click Properties.

2 In the <Project> Properties tab, click the Debug tab.

3 On the Debug tab, under Start Action, click Start External Program and then click the ellipsis button to the right of the text box.

4 In the Select File dialog box, browse to C:\Program Files\Autodesk\<release> and select acad.exe. Click Open.

5 With the project selected in the Solution Explorer, click Debug menu  Start Debugging.

6 In AutoCAD, at the Command prompt, enter netload.

7 In the Choose .NET Assembly dialog box, browse to the debug version of the assembly file. Click Open.

Tip: The location of the built assembly file is in the Output pane in Microsoft Visual Studio.

By default, the debug version is located under the \bin\debug folder; while the release version can be found under the \bin\release folder.

8 At the Command prompt, enter the name of the command or AutoLISP function and any required parameters.

To load a .NET assembly with NETLOAD

1 In Microsoft Visual Studio, with a solution or project open, click Build menu => Build Solution or Build <Project name>.

2 In AutoCAD, at the Command prompt, enter netload.

3 In the Choose .NET Assembly dialog box, browse to the built assembly file. Click Open.

Tip: The location of the built assembly file is in the Output pane in Microsoft Visual Studio.

By default, the debug version is located under the \bin\debug folder; while the release version can be found under the \bin\release folder.

At the Command prompt, enter the name of the command or AutoLISP function and any required parameters.

#### Application Initialization and Load-Time Optimization (.NET)

Managed applications can choose to perform initialization or termination tasks by implementing the optional Autodesk.AutoCAD.Runtime.IExtensionApplication interface.

The interface Autodesk.AutoCAD.Runtime.IExtensionApplication provides the Initialize() and Terminate() methods. Since managed applications cannot be manually unloaded, any implementation of the Terminate() method is called when the AutoCAD program closes.

If your application defines a large number of data types, you can optimize its load-time performance by implementing IExtensionApplication and using two optional custom attributes. These attributes—ExtensionApplication and CommandClass—help the AutoCAD program find the application's initialization routine and command handlers.

Any managed application can use these attributes. However, their optimizing effects are measurable only in larger applications.

Use the ExtensionApplication and CommandClass Attributes

When the AutoCAD program loads a managed application, it queries the application's assembly for an ExtensionApplication attribute. If this attribute is found, the AutoCAD program sets the attribute's associated type as the application's entry point. If no such attribute is found, AutoCAD searches all exported types for an IExtensionApplication implementation. If no implementation is found, the AutoCAD program skips the application-specific initialization step.

The ExtensionApplication attribute can be attached to only one type. The type to which it is attached must implement the IExtensionApplication interface.

In addition to searching for an implementation of IExtensionApplication in an application, the AutoCAD program queries the application's assembly for one or more CommandClass attributes. If instances of this attribute are found, the AutoCAD program searches only their associated types for command methods. Otherwise, it searches all exported types.

A CommandClass attribute may be declared for any type that defines an AutoCAD command handler. If an application uses the CommandClass attribute, it must declare an instance of this attribute for every type that contains an AutoCAD command handler method.

The following procedure describes how these attributes are used.

1 Define a type that implements Autodesk.AutoCAD.Runtime.IExtensionApplication.

If you do not need to perform initialization or termination tasks, provide blank implementations of the interface methods.

2 In the assembly context, declare an ExtensionApplication attribute.

3 Pass the type that implements the IExtensionApplication interface to the ExtensionApplication attribute.

4 In the assembly context, declare a CommandClass attribute for each class that defines AutoCAD command methods.

5 Pass the type of the command method's class to the CommandClass attribute.

Note: These attributes must be declared in the assembly context.

### 2.8 Exercises: Create Your First Project (.NET)

Now that you have learned the basics of using Microsoft Visual Studio, let's create a new project that defines a new command. Once the new command is defined, you will learn to load the .NET assembly into AutoCAD.
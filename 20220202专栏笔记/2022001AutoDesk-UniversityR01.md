## 目录

2022003An-Introduction-to-AutoCAD-NET-API-Using-CS.md

2022023AutoLISP-Has-a-New-Home-Get-to-Know-Visual-Studio-Code.md

## 2022003An-Introduction-to-AutoCAD-NET-API-Using-CS.md

[An Introduction to AutoCAD Software’s .NET API Using C# .NET | Autodesk University](https://www.autodesk.com/autodesk-university/class/Introduction-AutoCAD-Softwares-NET-API-Using-C-NET-2018)

SD219626-L

Josh Modglin InMotion Consulting

Learning Objectives

• Discover the AutoCAD .NET API.

• Learn how to create a command using AutoCAD software's .NET API.

• Discover general coding best practices with AutoCAD software's .NET API.

• Learn how to load an AutoCAD plug-in created using AutoCAD software's .NET API.

Description:

Are you familiar with Autodesk products, but you're new to programming? If so, this course can help you get up to speed with the basics of .NET programming, and how these concepts can be applied to AutoCAD software. We will look at how to work with the AutoCAD .NET API and the C# .NET programming language to create a plug-in — a module that loads into AutoCAD to extend its functionality.

About the Speaker:

Josh Modglin is recognized as a leader in the use, training, implementation, consultation, and customization of Autodesk, Inc.'s, Infrastructure software products. Josh started with AutoCAD Release 12 software over 20 years ago and he is now building Microsoft .NET applications for AutoCAD Civil 3D 2019 software. For years Josh has served as the technical editor for the best-selling book, Civil 3D Essentials. Josh recently has produced multiple training courses with LinkedIn. In addition to writing and working with the software, Josh has been a top-rated presenter at Autodesk University for 4 years. Josh currently serves as a managing partner for InMotion Consulting, a Technical Consulting Solution provider and a member of the Autodesk Developer Network. His passion for helping others in the use of Autodesk products is stronger than ever. 

### 01. Introduction

This class will guide to getting started using C# language and building an AutoCAD plug-in. We will not get a chance to cover everything in the API (Application Programming Interface). Nevertheless, the objective will be to get you comfortable in navigating the tools and functionality available to continue building your abilities.

#### 1.1 Some Key Points First

Before we really get into our AutoCAD plugin using C#.NET, it's good to know where we're going to work, our environment. For most of our code development we're going to be using Microsoft Visual Studio Community application to write our code. For everything we're going to do in this introductory course, Visual Studio's Community edition, the free version, will accomplish the tasks we need.

Within Visual Studio community, let's briefly walk around the interface.

Once you start Visual Studio you'll notice here that we have a start page. The start page is a tab. Any files for our projects that we open will display as a tab in the code window area.

Visual Studio is still menu based interface. The main menus you will use are File, View, Build, and Debug.

Besides the code window area, there are other windows. If you are familiar with the AutoCAD interface and then we're probably familiar with palettes. Windows works similar to palettes. You will utilize the Properties and Solution Explorer Window often. The Solution Explorer displays the associated files and data to the project we are working on. The Properties window will display property data for the current file tab.

Another window that is extremely valuable as we get started is the Error List window. It is shown docked at the bottom.

Now all of these windows you can turn on and off and control from the view menu pull down. Don't confine yourself to the windows presented here. There are other windows that you can also display. Each one of these windows interacts like an AutoCAD palette that you can work with.

That's a quick overview our user interface or our development environment.

Of course, Visual Studio is a Microsoft product. How do we work with the .NET API for AutoCAD products?

#### 1.2 Installing the SDK

To begin our very first AutoCAD .NET plugin project within Microsoft Visual Studio, we need to have the correct files that will reference the AutoCAD .NET Application Programming Interface, or API.

『

Why ObjectARX?

The .Net API is actually one part of a much larger and more powerful API available to work with AutoCAD, called ObjectARX.

"Mgd" as part of the dll name is a hint that the library is a .Net (managed) library file. Any “Mgd" (and a few other) file within the INC directory contain API functionality you can program with. Do not limit yourself to the three required DLLs.

』

How do we get the AutoCAD .NET API files that we need to work with? The API and associated documentation is available to download and install from Autodesk. Autodesk has packaged all of this information nicely into what they refer to as a Software Development Kit, or SDK. To download the SDK, go to:

[AutoCAD Platform Technologies | Autodesk Developer Network](https://www.autodesk.com/developer-network/platform-technologies/autocad)

This web page gets updated from time to time. At this time of this course, the location to download the SDK is mid-way down the page on the left side. The SDK is referred to as the ObjectARX SDK. Selecting this option will take you to another page which has a download option for the ObjectARX programming environment. Select this option and accept the conditions. You will then be presented with the supported ObjectARX SDK's to download. Select the version of AutoCAD you will be building your application for. This will download an executable. When extracted it will place a folder with the libraries needed on your computer. By default and throughout this course, the location is: C:\Autodesk\Autodesk_ObjectARX_2019_Win_64_and_32_Bit

1『看样子只是解压，这个 SDK 可以放到任意位置，下载的 2016 版的解压直接直接也移到 C:\Autodesk\ 下面。（2022-03-12）』

DotNet Wizard

There are three required libraries that need to be referenced into our Visual Studio project. The libraries we are going to reference will have the file extension DLL for the managed type work that we're going to do within .NET. DLL is another acryonym for Dynamic Link Library. The libraries we need to include are AcCoreMGD.dll, AcDbMgd.dll, and AcMgd.dll. All three are located in the inc directory of the SDK.

We will include a step-by-step to utilize these required libraries in this hand out. However, throughout our course we will utilize the AutoCAD DotNet Wizard. This installed application is available for download on the linked page above. It is currently listed under tools at the bottom of the page. This wizard will plug into our Visual Studio application and make setup of a project easier. We simply browse to our AutoCAD application and the location of our INC directory containing the required libraries and it will build the project for us.

### 02. Create your first Visual Studio Project

As previously mentioned we are going to walk through the manual process of creating a project. If you installed the DotNet Wizard, you will not need to perform the following steps.

Setup of a C# Visual Studio Project with AutoCAD API References:

1 Open Microsoft Visual Studio

2 From the File menu, New flyout, select Project…

3 From the New Project window, select the Visual C# > Windows Desktop > WPF Custom Control Library Set the following values:

• Name: MyFirstProject

• Location: …Exercise Files\

• Framework: .Net Framework 4.7

• Create Directory for solution: Unchecked Select Ok to create project

4 From Solution Explorer window, right-click on the References, and select Add Reference…

Note: If Solution Explorer is not open, you can open it from the View menu.

5 From the Reference Manager, select Browse…

6 From the Select the files to reference… window, browse to the SDK's INC directory. Using the CTRL key, multi-select the AcCoreMgd, AcDbMgd, and AcMgd dll files.

Select Add to add and close the window.

1-2『获得的信息：1）选的是 WPF 框架。2）那 3 个 dll 库文件是直接从 ObjectARX => inc 里加载的，之前自己是从 AutoCAD 安装目录下引用的。目前的感觉，安装 AutoCAD DotNet Wizard 目的也是生成的项目里自带这 3 个文件，ObjectARX 的目前也是。补充：果然，后面明确说了，DotNet wizard 的目的就是打包做了这些事情。ObjectARX、ObjectARX Wizards、AutoCAD .NET Wizards 三者关系的理解做一张信息数据卡片。（2022-03-12）』—— 已完成

7 Select Ok to close the Reference Manager window.

8 From the Solution Explorer, under your Project's References section, using CTRL key multi-select the library references added in step 6. Right-click and select Properties.

9 From the Properties window, set the Copy Local property to False.

10 From Solution Explorer, right-click on the project name, MyFirstProject, and select Properties.

11 From the Debug section, select the Start Action of Start external program. Set the path to the AutoCAD executable to launch when testing your code.

That is a lot of steps!! Thankfully, the DotNet wizard sets all these values for us.

### 03. Classes

Once we have our project setup, we will need to add classes to build our code in.

What is a Class?

To answer what a class is, we have to understand a little more about .Net. C#.Net is an object-oriented programming language. That means everything that you work with inside of C# is an object. A piece of text is not just characters, but it is a string object.

I know this may seem like a little thing, but it's important to remember as we build our own objects using classes. Now a class may seem to you simply as a chunk of code, but we use classes for everything we program within our project. A class really will house our methods, or the routines or functions that we're write, as well as the properties, the values that we're going to read and write too, as well. Everything that we use is really a container, so think of a class in two different ways. We can use a class as a custom object. Another way we can use a class is simply a container for our functions, or methods.

Layer (Object)

• CreateLayerMethod

• IsLayerFrozenProperty

Command (Container)

• HelloWorldCmdMethod

• CreateNewLineCmdMethod

Regardless of how we use a class, a class is always an object. Because it's an object of its own, that means every single time we want to use that class we have to create a new instance of it. In other words, when we go to McDonald's and we order a Big Mac, we know what comes with a Big Mac – what it contains. Yet each time you go and order a Big Mac, they have to create new instance for you to consume.

Thus, when we want to use a class, we have to create a new instance of the class – even when we treat it as a container of routines.

Through this course, we are simply going to use classes as containers to house our code – our commands that we write. Nevertheless, do not stop in your development there. Note the sample shown. We have a custom class named Layer. It contains not only special routines but also properties that are specific to that instance of the layer object.

#### 3.1 Create a Class for Commands

1 Open Microsoft Visual Studio.

2 From the File menu, Open flyout, select Project/Solution…

3 From the Open Project window, browse to the Exercise Files and select the 01-Create Class.sln

4 From Solution Explorer window, right-click on the project name and select Add > Class…

Note: If Solution Explorer is not open, you can open it from the View menu.

5 From the Add New Item window, confirm that Class is selected. Name the class Initialization Select Add to add the class and close the New Item window.

Note that the class file is opened and some code is already added for you. Using statements, Namespace, and the Class.

6 Below the last Using statement and above the namspace, add the following:

```cs
Using Autodesk.AutoCAD.Runtime;
```

After the phrase class Initialization, add 

```
: IExtensionApplication
```

Between the brackets the define the code of the Initialization class, add the following:

```
#region Initialization 

void IExtensionApplication.Initialize() { } 

void IExtensionApplication.Terminate() { } 
#endregion
```

The code between the Initialize routine brackets is code that will be called automatically when your program loads into AutoCAD.

We have created our project and we have created our class which will be used to store or contain our command methods. We have also added to our class the ability to do actions at the time our code Initializes or loads into AutoCAD or at the time that AutoCAD is closing. Let's create a command and learn a little more AutoCAD's API.

### 04. Create a Command

#### 4.1 Create a Command Method

1 Open Microsoft Visual Studio.

2 From the File menu, Open flyout, select Project/Solution…

3 From the Open Project window, browse to the Exercise Files and select the 02-Create Command.sln

4 If the Initialization class file is not open, from Solution Explorer window, double-click on the Initialization.cs file.

Note: If Solution Explorer is not open, you can open it from the View menu.

5 In between the #region Commands and #endregion lines, add the following:

```cs
[Autodesk.AutoCAD.Runtime.CommandMethod ("MyFirstCommand")]

public void cmdMyFirst() { }
```

Note: You may have to select the + symbol to the left to expand the Commands region.

6 That first line is a lot of typing. The power of the using statements at the top of the class file is to ‘shortcut' to specific namespaces. Namespaces could be considered ‘directories' to organize the classes and functions available within the API. Note that other AutoCAD API namespaces have been added as using statements.

Since the Autodesk.AutoCAD.Runtime namespace is listed above in a using statement, go back to the first line we added in step 5 and remove:

Autodesk.AutoCAD.Runtime.

7 Within the brackets below the public void cmdMyFirst() line, add the following:

```cs
Editor ed = Application.DocumentManager.MdiActiveDocument.Editor; 
ed.WriteMessage("\nI have created my first command");
```

The first line adds a variable. The variable name is ed and is an Editor type object. We have then assigned the value of the current drawing's editor to our variable. The next line calls a function to write a message to the command line. The message is the argument supplied.

We have created a function. A function is defined by the phrase, public void. The function then contains a name. The availability of the function is defined by the statement public. A function could be private which would make the function only visible to other functions within that class.

Connected to the function is an attribute called CommandMethod. The CommandMethod has arguments that can be supplied to the attribute. The arguments, or parameters, or listed in the parenthises. Currently we are only providing one argument which is the name of the command. This is what would be typed into the command line. When the command name, MyFirstCommand, is typed into the command line, the function cmdMyFirst runs.

In the process of creating our first command, we have been introduced to the Runtime, EditorInput, and ApplicationServices namespace. The ApplicationServices namespace stores the classes connected with the Application as a whole. The EditorInput contains classes and means to read and write information to the command line. It also contains all the means to request the user to provide us something – a coordinate picked on the screen, a selected object, etc.

Now that we have created our first command, let's test it by compiling our code and then loading the results into AutoCAD.

#### 4.2 Debugging Our Code

1 Open Microsoft Visual Studio.

2 From the File menu, Open flyout, select Project/Solution…

3 From the Open Project window, browse to the Exercise Files and select the 03-Debugging.sln

4 From the toolbar along the type, select the Start function.

Note: This will compile the code and launch AutoCAD per the property setting we defined when we created our project.

5 Within AutoCAD, type NETLOAD at the command line.

6 From the Choose .Net Assembly window, browse to the Exercise Files\03Debugging\bin\Debug directory.

Select the AU.dll

Select open to load the AU.dll into AutoCAD.

7 At the command line, type your command name MyFirstCommand.

8 Leaving AutoCAD open, go back to Visual Studio > Initialization class file. Just left of the the line number (20), pick on the gray bar. This adds a Breakpoint.

9 Go back to AutoCAD and retype MyFirstCommand.

10 From Visual Studio, note that the code stopped running at the breakpoint. For the locals window at the bottom of Visual Studio, select the arrow to the left of the ed variable to expand.

Note the many properties that are available to you.

11 From Visual Studio, select the F10 key.

Note that the code has run just one more line. This is a great way to iterate through the code one line at a time to troubleshoot.

12 From Visual Studio and the toolbar along the top, select the Continue function.

Note the code runs until the next breakpoint or completes.

### 05. Working with Transactions

Transactions are the means to make modifications and really, to even read information of an object that is found in the drawing database. Each object, including non-graphical objects such as Layers, Text Styles, etc. are assigned a unique Object Id each time the drawing is opened. Let's learn about transactions by using an analogy.

If you wanted to know how much money was in your bank, you still would have to provide the teller, or even the internet, your bank account number, a unique ID, so as to access your bank account. And even if you didn't want to transfer any money, you still would have to open up that account and it would take a transaction to do so. So even if you're looking at the information or modifying the information, a transaction is needed. And it's the same when it comes to working with AutoCAD's database transaction.

In this exercise, we are going to look at creating a line. To do so we will have to create a transaction, get the model space block definition (yes, each space is stored as a block definition in the drawing database), and add the new line to model space.

Most non-graphical objects, such as the block definitions, are stored in a table. Thus, to get the model space block definition, we have to find it's record (or row) in the Block Table.

Lastly, just because we make changes to tables and objects, if we don't commit those changes to the database, then the changes are not made.

#### 5.1 Create a Line

1 Open Microsoft Visual Studio.

2 From the File menu, Open flyout, select Project/Solution…

3 From the Open Project window, browse to the Exercise Files and select the 04-Create Line.sln

4 From the Initialization class, within the command brackets, add the following:

```cs
Database db = HostApplicationServices.WorkingDatabase; 
Transaction trans = db.TransactionManager.StartTransaction();
```

This gets us access to the drawing's database which contains the block table. We also have started a new transaction.

5 Right below the Transaction variable, add the following:

```cs
BlockTable blkTbl = trans.GetObject(db.BlockTableId, OpenMode.ForRead) as BlockTable; 
BlockTableRecord msBlkRec = trans.GetObject(blkTbl[BlockTableRecord.ModelSpace], OpenMode.ForWrite) as BlockTableRecord;
```

We have gotten the table containing all the blocks. We used the transaction to get this. To the object, we call the function GetObject and feed it the object's unique ID called an ObjectId. Another parameter we feed it is we are opening the object to modify or just read it.

6 To create our line, we have to provide the start point and end point. Thus we need to create two new Point3D objects with the coordinates. A Point3D object is part of the Autodesk.AutoCAD.Geometry namespace. Below the last line from step 5, add the following:

```cs
Point3d pnt1 = new Point3d(0, 0, 0); 
Point3d pnt2 = new Point3d(10, 10, 0); 
Line lineObj = new Line(pnt1, pnt2); 
msBlkRec.AppendEntity(lineObj); 
trans.AddNewlyCreatedDBObject(lineObj, true); 
trans.Commit();
```

In the last step, we created a new line using two point objects. We added the line to the model space block record. We told the transaction that we added something new and then we committed the changes which created the line.

We specified the coordinates of the start and end points in the code. What if we wanted to get information from the user?

#### 5.2 Get User Specified Information

1 Open Microsoft Visual Studio.

2 From the File menu, Open flyout, select Project/Solution…

3 From the Open Project window, browse to the Exercise Files and select the 05-Get User.sln

4 From the Initialization class, within the command and right below the comment to enter code below, add the following:

```cs
PromptPointOptions prPtOpt = new PromptPointOptions("\nSpecify start point: "); 
prPtOpt.AllowArbitraryInput = false; 
prPtOpt.AllowNone = true;
```

We are going to prompt the user for a coordinate point. The PromptPointOptions prompt allows us to control the information provided back to us. The variable prPtOpt stores this for use.

5 Below the code added in step 4, add the following:

```cs
Editor ed = Application.DocumentManager.MdiActiveDocument.Editor; 
PromptPointResult prPtRes1 = ed.GetPoint(prPtOpt); 
if (prPtRes1.Status != PromptStatus.OK) return; 
Point3d pnt1 = prPtRes1.Value;
```

We get the current drawing's Editor object. Using this object, we call the GetPoint function and feed it our PromptPointOptions variable. The GetPoint function returns a PromptPointResult object that we assign to the variable prPtRes1. The PromptPointResult has multiple properties. The Status property tells you if the user typed the Esc key or otherwise did not complete the prompt. If the prompt did not complete sucessfully, we are ending the command using the conditional If statement. Lastly, we assign the Value property to our Point3D pnt1 variable.

6 We are going to make some adjustments to the PromptPointOptions properties and then repeat portions of step 5 to get the end point. Below the code added in step 5, add the following:

```cs
prPtOpt.BasePoint = pnt1; 
prPtOpt.UseBasePoint = true; 
prPtOpt.UseDashedLine = true;
prPtOpt.Message = "\nSpecify end point:";
PromptPointResult prPtRes2 = ed.GetPoint(prPtOpt); 
if (prPtRes2.Status != PromptStatus.OK) return; 
Point3d pnt2 = prPtRes2.Value;
```

We made some modifications to three properties for the PromptPointOptions. These adjustments will draw a ‘construction' line from the base point of the first point the user specified to the next point picked.

We also adjusted the message from start to end point. Note that the backslash and n tell are the way to make sure the message is written to a new line on the command line.

### 06. Loading your AutoCAD Plug-in

Have you noticed that each time we have to load our plug-in assembly, we have had to type the command NETLOAD? How do you automate loading your plug-in into AutoCAD?

We will learn about the PackageContents and Bundle package. The PackageContents.xml contains the information of what is being loaded and where the files to load are located. For detailed information about the format of the XML, please review this article. 

1『上面的文章链接失效了。（2022-03-12）』

The XML and associated files are located in directory whose name ends with .bundle. The directory is located at C:\Program Files\Autodesk\ApplicationPlugins (there are alternate locations as well. See the options here.)

#### 6.1 Build Bundle Package

1 Open Windows Explorer and browse to the …Exercise files\06-Create Layer\bin\Debug directory.

2 Copy the AU.dll and paste into …Exercise files\AU.bundle

3 Copy the AU.bundle directory and paste into C:\Program Files\Autodesk\ApplicationPlugins.

4 Launch AutoCAD 2019.

5 In AutoCAD, from the command line, type MyFirstLayer.

6 Open the PackageContents.xml file and study the values set.

### 07. Conclusion

We really have just scratched the surface of what can be done. Yet we have covered a lot. We have learned:

• The Visual Studio Overview.

• Downloading and Installing the Software Development Kit so as to reference the AutoCAD API.

• What is a Class and created a Class.

• Created a Command.

• Worked in the Runtime, EditorInput, ApplicationServices, DatabaseServices, and Geometry namespace.

• What a Transaction is and how to use it.

• How to have our plug-in automatically load into AutoCAD.

### 08. Reference

[AutoCAD Platform Technologies | Autodesk Developer Network](https://www.autodesk.com/developer-network/platform-technologies/autocad)

PackageContents.xml Format 

Application PlugIn Locations 

LinkedIn Learning Course - Building AutoCAD Add-ins with C#

## 2022023AutoLISP-Has-a-New-Home-Get-to-Know-Visual-Studio-Code.md

[AutoLISP Has a New Home: Get to Know Visual Studio Code | Autodesk University](https://www.autodesk.com/autodesk-university/class/AutoLISP-Has-New-Home-Get-Know-Visual-Studio-Code-2020)

Description:

We have a new integrated development environment (IDE)! Let's familiarize ourselves with the most significant update to AutoLISP since receiving VL functions. In this session, you will learn how to create code efficiently using Code Snippets and IntelliSense, and how to debug your new or existing code in AutoCAD software using Visual Studio Code. Let's take advantage of what Visual Studio Code has to offer!

Key Learnings:

1 Learn how to implement Visual Studio Code for AutoLISP.

2 Learn how to develop code efficiently with IntelliSense and Code Snippets.

3 Learn how to create custom code snippets.

4 Learn how to debug AutoLISP code effectively.

Matt Worland:

I enjoy sharing my knowledge to elevate Design and Engineering teams to take their projects to the next level. I have been customizing and programming in AutoCAD products since the mid-90s. My passion for helping others was a perfect fit as an AutoCAD All-Star Mentor and a former member of Autodesk User Group International AUGI board of directors. From Drafter to CAD Manager, I have increased the efficiencies of the engineering and design teams I worked with. I now support, train, and customize Plant related products as a Senior Applications Engineer and Developer at ECE Design. When I am not helping others or learning new tricks in the office, I enjoy mountain biking, paddle boarding, or hiking in the mountains with my wife and children.

### 01. Visual Studio Code

Visual Studio Code is a free, open-source licensed; cross-platform source code editor developed by Microsoft. A Stack Overflow Survey ranked VS Code as the most popular developer environment tool. As it grows in popularity, more and more extensions have been added, including the AutoCAD AutoLISP extension. While the VL IDE has many tools, it is built on old technologies and has not been updated for over a decade. While not all VL IDE functions have been added to the AutoLISP extension, these first iterations have great features to benefit your AutoLISP development.

This handout covers many concepts in using Visual Studio Code. We work through installing and setting up VS Code to debugging AutoLISP files.

#### 1.1 Why use Visual Studio Code

• IntelliSense & Code Snippets significantly reduce coding time!

• Keyboard Shortcuts help you navigate and update your code.

• Extensions enhance your VS Code experience.

• Source Control manages your code in a safe environment.

• The AutoLISP extension is open-source, allowing you to enhance the extension for all!

• It is the future. As stated in the help documents, the VL IDE may be removed in a future release.

#### 1.2 Install Wizard

Setting up AutoCAD to use Visual Studio Code is an easy process. If you have not chosen a default editor, AutoCAD prompts you to choose one. To use Visual Studio Code, you select the top option.

Another dialog appears if you do not have Visual Studio Code and the AutoLISP Extension downloaded. Choose the download link for Visual Studio Code.

This navigates you out to Microsoft’s download site. Choose the download that best fits your Operating System. Below, I show the area for downloading onto a Windows computer

It directs you to another page to choose the correct version, architecture, and download type.

Once downloaded, follow the prompts for installation.

Now that VS Code is installed, we return to AutoCAD to download and install the AutoCAD AutoLISP Extension.

A new browser window appears with an install button.

A new prompt appears to open Visual Studio Code and you to install it there. Choose the Install button to add the extension to VS Code.

We have now installed Visual Studio Code and the AutoLISP Extension. You may close VS Code and return to AutoCAD. Here we can close out the download dialog.

AutoCAD sets LISPSYS = 1 when you choose VS Code for your default editor using their wizard. If you compile your code to be used in versions before AutoCAD 2021, you need to modify the variable to LISPSYS = 2.

1-2『 LISPSYS 这个系统变量的设置什么作用？待验证。补充：是很关键的信息，如果要用 AutoCAD 2021 之前的版本做测试，那么需设为 2。昨天不知道这个设置，专门去下载了安装了 AutoCAD 2021。补充：验证了下，只有 AutoCAD 2021 里有 LISPSYS 这个系统变量，老版本里压根没这个，无法设置。（2022-03-12）』

#### 1.3 Installing Manually

To download manually, go here: https://aka.ms/win32-x64-user-stable Once downloaded, follow the prompts for installation.

After launching VS Code, you need to use the Extensions Panel Ctrl + Shift + X to search for and install the AutoCAD AutoLISP Extension. There are several AutoLISP extensions available; make sure to select the extension from Autodesk.

The AutoLISP Extension tab appears, and you can get additional information about using the extension, creating GitHub issues, links to the Autodesk AutoLISP help, and more.

With Visual Studio Code and the AutoLISP extension installed, we need to let AutoCAD know we are ready to use our new editor. To do this, we need to change the LISPSYS variable.

To maintain and compile your code for use in AutoCAD 2020 and previous releases, you must use LISPSYS = 2.

If you do not need to compile code for AutoCAD 2020 and previous releases, you can set LISPSYS = 1.

At the AutoCAD command line, type LISPSYS and set the value to either 1 or 2.

You must restart AutoCAD when switching AutoLISP development environments.

For additional information on the LISPSYS variable, please visit AutoCAD’s cloud help: 

[LISPSYS (System Variable) | AutoCAD 2021 | Autodesk Knowledge Network](https://knowledge.autodesk.com/support/autocad/learn-explore/caas/CloudHelp/cloudhelp/2021/ENU/AutoCAD-Core/files/GUID-1853092D-6E6D-4A06-8956-AD2C3DF203A3-htm.html)

#### 1.4 Visual Studio Interface

You type VLIDE or VLISP at the command line to launch Visual Studio Code from within AutoCAD. You are greeted with the dialog shown below the first time you start Visual Studio Code with the AutoCAD AutoLISP Extension installed. You may check the ‘Don’t ask again for this extension’ box to start VS Code with an extension message each time it starts.

When you start VS Code from within AutoCAD, you receive the following message that reminds you how to debug your files.

#### 1.5 Workspace & AutoLISP Project Manager

#### 1.6 Keyboard Shortcuts

#### 1.7 Shortcuts to Explore

#### 1.8 Adding New Shortcuts

1『上面几节提供不了现在的自己多少有价值信息，细节详见原 PDF。（2022-03-12）』

### 02. IntelliSense & Code Snippets

Writing AutoLISP in VS Code is very similar to the VL IDE with some additional benefits. As you type a parenthesis, bracket, or quote, it completes the pair on the other side. It also has IntelliSense and Code Snippets. IntelliSense is like AutoCAD’s AutoComplete functionality. When you start typing in the Visual Studio Code Editor, IntelliSense finds matching functions or Code Snippets. Snippets are bits of code used to reduce the amount of typing. When you find the desired function or snippet, press Tab to select it.

Choosing the getvar function only finishes typing the function getvar. Using Snippets not only completes the word or function, but they can also add multiple lines of code. Choosing the getvar snippet adds parentheses, function, quotes, and a prompt. Here is a simple example:

```
(getvar "sysvar")
```

The snippet adds all the code needed for a getvar function and prompts you to type the variable’s name.

The ifp snippet has multiple lines and prompts, as shown below:

```
(if (testexpr)
    (progn 
        (thenexpr) 
    ) 
)
```

#### 2.1 Adding New Snippets

We can further customize VS Code by adding our snippets. The AutoCAD AutoLISP extension has its own snippets, use Ctrl + P to search for and open the snippets.json file.

Below is a list of the out of the box snippets.

```
(defun (defun c: abs alert alloc angle append apply arc ascii assoc atan atof atoi atomsfamily boundp

caddr car chr circle cons dcl defun defun c: distance entmake entmod eq equal expt foreach getcolor

getlayer getvar if ifp inters itoa lefttrim line nth open pline polar prin1 princ print prompt

readline repeat reverse search setq setvar ssget strcat substr tblsearch trim vgetlayer while writeline
```

While the help files state you can modify this file, a user file can also be updated. I try not to modify files that could be overwritten when an update is installed, but in either case, whichever file you change, make sure you back it up. Let’s review how to update the User Snippets file.

Select the Manage button and choose User Snippets.

#### 2.2 Snippets Structure

When you first open the autolisp.json file, you see a brief overview and example of creating a snippet. A snippet structure needs to be followed strictly. Make sure your brackets, quotes, colons, commas, and general layout match a previous example. In the example on the next page, we create a snippet to iterate every object in the Active Document.

A snippet is comprised of four parts: Name, Prefix, Body, and a Description.

The snippet’s name is “iterate active document” This name needs to be unique regarding all other snippets. If no description is given, the name will be used as the Description when viewed in the IntelliSense prompt.

The Prefix gets added to the IntelliSense list and displays as you are typing in the Editor. In this example, to insert our snippet we would begin typing vforActiveDocument.

The Body of the snippet contains the code that is placed in the Editor. Each line of the Body needs to be wrapped in quotes. If you have quotes or backslashes as part of your original code, you need to escape them with a backslash. Here is an example where we escape a quote and backslash.

```
"(prompt \"\\n${1:YourPrompt}\")",
```

Use \t to add a Tab into your final code.

The Body can also contain place holders. These place holders allow the user to tab through the code and fill out the needed areas. These can be helpful when prompting the user, or requesting a specific layer or block name for a selection set. Each place holder has an ID and the place holder text. The place holder begins with a dollar sign and wraps the ID and text in squiggly brackets. A colon separates the ID and text. Here is an example:

```
${1:YourPrompt}
```

The Description is shown when viewing the information from the IntelliSense prompt.

To ensure the proper formatting, please note the commas at the end of the Prefix, each line in the Body, and after the last bracket of the Body.

#### 2.3 Creating Files

Visual Studio Code is an editor for many programming languages. Since it is not primarily used for developing AutoLISP files, you need to add the correct extension; .LSP, .MNL, or .DCL. Suppose your primary purpose for Visual Studio Code is to write AutoLISP. In that case, you should set the default language in the settings. To open the settings, use the keyboard shortcut Ctrl + , Then in the settings search box, search for Default Language. Finally, in the Default Language text box, type autolisp.

#### 2.4 Formatting

The AutoLISP Extension in Visual Studio Code has some basic formatting options.

Use Alt + Shift + F to format your entire file. Use Ctrl + K, Ctrl + F to format a selection. Both options are available with a right-click.

### 03. Debugging

Troubleshooting and debugging code is an essential part of writing robust programs. The AutoCAD AutoLISP Extension has two out of the box debugging configurations. However, these are not automatic configurations. You need to select either the Attach or Launch configuration when using F5 to debug without setting up an automatic configuration.

Before debugging for the first time, make sure your AutoLISP Extension settings are correct. Below we cover the needed values for these settings.

#### 3.1 Attach

The AutoLISP Debug: Attach configuration allows you to attach the debug session to the currently running AutoCAD session.

The Attach Process setting tells Visual Studio Code which process to attach itself to. This setting is case sensitive and has different values depending on your operating system: 

Windows: acad 

Mac OS: AutoCAD

#### 3.2 Launch

The AutoLISP Debug: Launch configuration allows you to start a new AutoCAD session using startup switches. Startup switches change the default startup of AutoCAD. There are many switches, including, load a vertical application, choose a language, set a profile, start with a template, or run a script. You set these switches in the Launch Parameters text box. In the example below, AutoCAD Plant3D starts with the en-US language pack and the Plant3D_2021 profile.

The Launch Program tells VS Code the correct AutoCAD executable to launch. Using the out of the box default Debug Configurations are recommended by Autodesk.

1『上面关于 Attach 和 Launch 的设置，这个插件 GitHub 源码库里都有说明，之前就是按那边做的设置。（2022-03-12）』

#### 3.3 Define Configurations

In previous releases of the extension, you had to create your configurations. These were saved with your current working folder. In many cases, using the out of the box setup is sufficient. However, these configurations can still be used. They may be preferred when you need specific Launch Parameters for the current workspace. Once created, you select a default configuration to use every time you begin debugging. If needed, follow the steps below in creating workspace specific debug configurations.

Go to the Debug Side Bar, select create a launch.json file.

Choose a location to save the JSON data.

Now add the text between the square brackets to add a new Attach and Launch configuration:

1『设置内容详见原 PDF 文档。（2022-03-12）』

We now select the default configuration to be used with F5. Note: this text box was not available until creating the new launch.json file

We can now use F5 to start a debug session using our default workspace debugging configuration.

#### 3.4 Debug Side Bar

While debugging, the status bar of Visual Studio Code window turns to a different color. Your Side Bar also displays your Variables, Watch list, Call Stack, and Breakpoints.

Adding variables to your variables list when defining a function, adds them to the Variables Locals section of the Debug Side Bar.

There is also a Last Value variable that shows the value of the last evaluated variable or expression.

The watch list is persistent between VS Code sessions. You add variables and expressions to the list using the + button and typing your text or selecting the text in the Editor, Right-Clicking, and choosing Add to Watch The value is shown to the right of the text being watched. You can remove all watched items using the X button.

Call stack steps are shown in the Call Stack section.

Current breakpoints are displayed in the Breakpoints list. You can add new breakpoints using the + button. Disable all breakpoints using the double circle button. Remove all breakpoints using the X button.

#### 3.5 Breakpoints

Breakpoints are essential in debugging software. When a breakpoint is hit, Visual Studio Code stops the execution of code, and you can evaluate your currently set variables. In the Editor’s farthest left column, you can select a row, and Visual Studio Code adds a new breakpoint. Selecting an active breakpoint removes the breakpoint.

Right clicking an active breakpoint allows you to remove or disable the breakpoint.

```
• = Active breakpoint

• = Disabled breakpoint

• = Future breakpoint
```

#### 3.6 Debug Console

To immediately evaluate an expression or check a variable, you can use the Debug Console.

You can also evaluate selected text by right-clicking and choosing Evaluate in Debug Console.

The selected code is shown in the debug console and immediately run.

#### 3.7 Debug Commands

The debug commands become available when you begin a debug session.

F5 Start or Continue executing your debug code.

F10(Step Over) Use when you are confident the current line executes without error.

F11(Step In) Use when you need to evaluate each portion of a line.

Shift + F11(Step Out) Use when you are confident the remainder of a function executes without error.

Ctrl + Shift + F5 Use to restart your current debug session.

Shift + F5 Use to end your current debug session.

F9 Add a breakpoint at the current line.

### 04. Source Control Management

1『上面几节提供不了现在的自己多少有价值信息，细节详见原 PDF。（2022-03-12）』

### 05. Open Source Project

The AutoCAD AutoLISP Extension is open-source, allowing the community to drive and enhance its functionality. GitHub stores the project, and you can contribute by following the guidelines found in the contribution guide. Below are some helpful links if you would like to contribute.

[Opensource Announcement for AutoCAD AutoLISP Extension - AutoCAD DevBlog](https://adndevblog.typepad.com/autocad/2020/08/opensource-announcement-for-autocad-autolisp-extension.html)

[GitHub - Autodesk-AutoCAD/AutoLispExt: Visual Studio Code Extension for AutoCAD® AutoLISP](https://github.com/Autodesk-AutoCAD/AutoLispExt)

[AutoLispExt/CONTRIBUTING.md at main · Autodesk-AutoCAD/AutoLispExt](https://github.com/Autodesk-AutoCAD/AutoLispExt/blob/main/CONTRIBUTING.md)

### 06. Additional Information

The Autodesk team has done a great job of documenting how to use Visual Studio Code with AutoCAD. Review the help documents found here: 

[AutoCAD 2021 Developer and ObjectARX Help | Autodesk](https://help.autodesk.com/view/OARX/2021/ENU/)

There are many resources if you are new to Git. Check out these pages for additional information:

https://code.visualstudio.com/docs/editor/versioncontrol https://git-scm.com/doc https://git-scm.com/video/what-is-git https://training.github.com/downloads/github-git-cheat-sheet.pdf

To learn more about Source Control with AutoCAD, please visit this excellent class: https://www.autodesk.com/autodesk-university/class/Control-Your-Code-Introduction-SourceControl-Programmers-and-CAD-Managers-2018

This handout and other downloads are available from https://tinyurl.com/SD466922
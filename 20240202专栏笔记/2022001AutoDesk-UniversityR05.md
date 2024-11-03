## 目录

2022023AutoLISP-Has-a-New-Home-Get-to-Know-Visual-Studio-Code.md

2022024Programming-AutoCAD-with-CS-Best-Practices.md

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

## 2022024Programming-AutoCAD-with-CS-Best-Practices.md

[Programming AutoCAD® with C#: Best Practices | Autodesk University](https://www.autodesk.com/autodesk-university/class/Programming-AutoCADR-C-Best-Practices-2012)

Scott McFarlane – Woolpert, Inc.

CP4471

This class is for the AutoCAD C# developer who wants to improve code quality and maintainability. Learn how to apply good software design patterns to your AutoCAD code, and leverage the advanced features of the C# language. We will cover topics such as the single responsibility principle, reducing duplicate code, abstraction and dependency injection. We will touch on WPF and the Model-View-ViewModel pattern. We will also explore C# features such as LINQ and delegates, and where we can best apply them to the AutoCAD API. My hope is you will walk away with some basic techniques that will make your code more testable, extensible, maintainable, scalable, and reusable.

Learning Objectives:

At the end of this class, you will be able to:

1 Use delegates to reduce duplicate code.

2 Understand how LINQ can be used with the AutoCAD API.

3 Apply abstraction and dependency injection into your C# code.

4 Use WPF and the Model-View-ViewModel design pattern.

About the Speaker:

Scott is senior software engineer for the Infrastructure service line at Woolpert, Inc. He specializes in custom database applications that use Autodesk® software in the AEC, FM and GIS industries. He has more than 25 years of programming experience, and has been integrating databases with AutoCAD® software ever since it was possible. He is the author of AutoCAD Database Connectivity from Autodesk Press, as well as several articles. Scott has attended every AU, and has been a speaker since 1996. He also served two two-year terms on the AUGI® Board of Directors.

Scott can be reached at scott.mcfarlane@woolpert.com.

### 01. Introduction

My name is Scott McFarlane. If you're like me, your formal training or college degree was focused on some design-related discipline (I am a degreed architect). You probably also had a strong interest in computer programming, but no formal training. Sure, I took my share of computer programming courses in college with very useful programming languages such as Fortran and Assembler. But generally I consider myself self-taught when it comes to software development. I started using LISP within the first month I ever started using AutoCAD. From there I jumped on each AutoCAD API as it was added. Today, I'm pretty much exclusively a C#.NET developer when it comes to AutoCAD.

In recent years, I have become a "student" of software engineering, software design patterns, and best practices. These practices are the kinds of things I've been doing (in some form or another) for many years, yet these days they are formalized, studied and documented. Let me stress that I will forever be a "student" of these practices – continuously learning and adapting my software design style as my knowledge grows. In this class, while I try to offer a "better way" to solve certain problems, there is likely an "even better way" that I haven't explored. I always welcome discussion and debate on these subjects – so please feel free to ask questions during the class, track me down at the conference, or contact me after the conference is over.

#### 1.1 The Importance of High Quality Code 

Have you ever encountered an AutoCAD drawing (presumably from someone else!) that was a complete mess? No coherent layer naming, objects on the wrong layer, endpoints not snapped together, blocks exploded, text objects used where block attributes should be, etc. Drawings like this may plot just fine, but working with them inside of AutoCAD can be very difficult. Even more difficult (if not impossible) is trying to work with a messy drawing from a program!

Well, the same scrutiny can (and should) be applied to source code. Messy code can be hard to follow, difficult to maintain, and is prone to defects. Clean, well-structured, high-quality code is code that is not only easy to read and maintain, but is more testable, extensible, scalable, and reusable.

#### 1.2 Our Goal: Efficiency

This may be stating the obvious, but as coders, our #1 goal is efficiency. By "efficiency" I don't mean "quick and dirty". We need to be efficient, but at the same time produce clean, high-quality code. Some may see these two goals to be contradictory: How can I be efficient when so much time is spent producing clean code? I have come to realize that attention to quality up-front is like an investment – it will lead to saved time down the road. We have developed good habits to produce quality AutoCAD drawings, because we know that it will ultimately save us time down the road. We need to develop similar habits in our software development.

The most obvious way to be efficient in coding is to find ways to generalize common tasks and develop your own toolbox of reusable components that you can share from one project to the next.

### 02. Using Delegates to Reduce Duplicate Code

Let's start with one of the most common coding sequences in AutoCAD programming: working with the entities in the current drawing. In this section we will leverage a C# feature called delegates to separate the "boiler plate" code from the code that does the real work.

Consider the following code that finds all the circles in the drawing with a radius less than 1.0 and changes their color to red.

```cs
// using Autodesk.AutoCAD.ApplicationServices.Core;
using Autodesk.AutoCAD.ApplicationServices;
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.EditorInput;
using Autodesk.AutoCAD.Runtime;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace dataflow_cs
{
    public class Commands
    {
        [CommandMethod("Hello")] 
        public void Hello()
        {
            Editor editor = Application.DocumentManager.MdiActiveDocument.Editor;
            editor.WriteMessage("Hello, dalong");
        }

        [CommandMethod("ENTCOLOR1")]
        public void ChangeEntityColor1()
        {
            // Get the various active objects
            Document document = Application.DocumentManager.MdiActiveDocument;
            Database database = document.Database;
            // Create a new transaction
            Transaction tr = database.TransactionManager.StartTransaction();
            using (tr)
            {
                // Get the block table for the current database
                var blockTable =
                (BlockTable)tr.GetObject(database.BlockTableId, OpenMode.ForRead);
                // Get the model space block table record
                var modelSpace = (BlockTableRecord)tr.GetObject(blockTable[BlockTableRecord.ModelSpace], OpenMode.ForRead);
                RXClass circleClass = RXObject.GetClass(typeof(Circle));
                // Loop through the entities in model space
                foreach (ObjectId objectId in modelSpace)
                {
                    // Look for circles
                    if (objectId.ObjectClass.IsDerivedFrom(circleClass))
                    {
                        var circle = (Circle)tr.GetObject(objectId, OpenMode.ForRead);
                        if (circle.Radius < 1.0)
                        {
                            circle.UpgradeOpen();
                            circle.ColorIndex = 1;
                        }
                    }
                }
                tr.Commit();
            }
        }
    }
}
```

1『在自己项目「dataflow-cs」中测试完毕。（2022-03-21）』

The majority of this code is necessary for virtually any activity your code needs to perform on the entities in a drawing. In this section, we will explore how the use of delegates, along with extension methods, can greatly reduce the duplication of this code in other similar scenarios.

#### 2.1 The "Active" Static Class

Before we go any further, I would like to introduce a simple yet very useful static class called Active, which provides quick access to the most commonly used objects in the AutoCAD API.

```cs
        /// <summary> /// Provides easy access to several "active" objects in the AutoCAD
        /// runtime environment.
        /// </summary>
        public static class Active
        {
            /// <summary>
            /// Returns the active Editor object.
            /// </summary>
            public static Editor Editor
            {
                get { return Document.Editor; }
            }
            /// <summary>
            /// Returns the active Document object.
            /// </summary>
            public static Document Document
            {
                get { return Application.DocumentManager.MdiActiveDocument; }
            }
            /// <summary>
            /// Returns the active Database object.
            /// </summary>
            public static Database Database
            {
                get { return Document.Database; }
            }
            /// <summary>
            /// Sends a string to the command line in the active Editor
            /// </summary>
            /// <param name="message">The message to send.</param>
            public static void WriteMessage(string message)
            {
                Editor.WriteMessage(message);
            }
            /// <summary>
            /// Sends a string to the command line in the active Editor using String.Format.
            /// </summary>
            /// <param name="message">The message containing format specifications.</param>
            /// <param name="parameter">The variables to substitute into the format string.</param>
            public static void WriteMessage(string message, params object[] parameter)
            {
                Editor.WriteMessage(message, parameter);
            }
        }
```

So in other parts of your code, for example, you can access the active database using:

```cs
var db = Active.Database;
```

Let's modify the previous code sample to use our new Active static class.

```cs
        [CommandMethod("ENTCOLOR2")]
        public void ChangeEntityColor2()
        {

            using (var tr = Active.Database.TransactionManager.StartTransaction())
            {

                // Get the block table for the current database
                var blockTable = (BlockTable)tr.GetObject(Active.Database.BlockTableId, OpenMode.ForRead);
                // Get the model space block table record
                var modelSpace = (BlockTableRecord)tr.GetObject(blockTable[BlockTableRecord.ModelSpace], OpenMode.ForRead);
                RXClass circleClass = RXObject.GetClass(typeof(Circle));
                // Loop through the entities in model space
                foreach (ObjectId objectId in modelSpace)
                {
                    // Look for circles
                    if (objectId.ObjectClass.IsDerivedFrom(circleClass))
                    {
                        var circle = (Circle)tr.GetObject(objectId, OpenMode.ForRead);
                        if (circle.Radius < 1.0)
                        {
                            circle.UpgradeOpen();
                            circle.ColorIndex = 1;
                        }
                    }
                }
                tr.Commit();
            }
        }
```

There are a couple of techniques used in this code worth mentioning, but are beyond the scope of this class.

1 Use of the using keyword, which automatically calls Dispose() on the transaction object when it goes out of scope.

2 Use of the RXObject.GetClass method along with the ObjectId.ObjectClass method, which allows you to check for the type of object before you actually open it.

3 Use of the UpgradeOpen method, which allows you to only open an object for write when you know you need to.

1『上面几个 .NET AutoCAD 二次开发常用的函数，做一张信息数据卡片。（2022-03-21）』—— 已完成

#### 2.2 Introducing Delegates 

A delegate in .NET is an object that points to another method in your application that can be invoked at a later time. Delegates, like any other type of object, can be passed as arguments to other methods. Along with holding a pointer to a method, delegates also define the method signature, that is, the arguments (if any) and the return value (if any).

Let's look at the outer code block of our change color example, which is the part that is responsible for creating, committing and disposing of the Transaction object. This is an example of a code fragment that will be repeated any time you do anything with the drawing database.

```cs
using (var tr = Active.Database.TransactionManager.StartTransaction()) 
{ 
    tr.Commit(); 
}
```

The real work is performed within the using block (and before the Commit). Now consider the following delegate declaration. Note the use of the delegate keyword.

```cs
public delegate void TransactionFunc(Transaction tr);
```

This declaration defines a delegate (a method signature) that takes a single Transaction argument, and returns void (nothing). Now we can define a useful method that takes a TransactionFunc as an argument, and invokes the method within the Transaction block.

```cs
        public void UsingTransaction(TransactionFunc action)
        {
            using (var tr = CADActive.Database.TransactionManager.StartTransaction()) 
            { 
                // Invoke the method
                action(tr);
                tr.Commit();
            }
        }
```

To avoid having to explicitly declare delegates, the .NET System namespace includes two delegate classes that use generics: Action, which defines delegates that have no return value, and Func, which defines delegates that have a return value. There are multiple versions of each of these classes which support up to 16 method arguments:

`Action` – no parameters, no return value.

`Action<T> `– one parameter, no return value.

`Action<T1, T2>` – two parameters, no return value.

`Action<T1, T2, T3>` – three parameters, no return value.

Etc…

And,

`Func<TResult> `– no parameters, return value of the specified type.

`Func<T, TResult>` – one parameter, return value of the specified type.

`Func<T1, T2, TResult>` – two parameters, return value of the specified type.

`Func<T1, T2, T3, TResult>` – three parameters, return value of the specified type.

Etc…

So using the `Action<T>` class, we can replace the TransactionFunc delegate with its equivalent `Action<Transaction>` and then rewrite our UsingTransaction method as follows:

```cs
        public void UsingTransaction(Action<Transaction> action)
        {
            using (var tr = CADActive.Database.TransactionManager.StartTransaction())
            {
                // Invoke the method
                action(tr);
                tr.Commit();
            }
        }
```

To use this method, we first take the guts of our code, and put it into a method that has the correct signature:

```cs
        public void ChangeSmallCircleToRed(Transaction tr)
        {
            // Get the block table for the current database
            var blockTable = (BlockTable)tr.GetObject(CADActive.Database.BlockTableId, OpenMode.ForRead);
            // Get the model space block table record
            var modelSpace = (BlockTableRecord)tr.GetObject(blockTable[BlockTableRecord.ModelSpace], OpenMode.ForRead);
            RXClass circleClass = RXObject.GetClass(typeof(Circle));
            // Loop through the entities in model space
            foreach (ObjectId objectId in modelSpace)
            {
                // Look for circles
                if (objectId.ObjectClass.IsDerivedFrom(circleClass))
                {
                    var circle = (Circle)tr.GetObject(objectId, OpenMode.ForRead);
                    if (circle.Radius < 1.0)
                    {
                        circle.UpgradeOpen();
                        circle.ColorIndex = 1;
                    }
                }
            }
        }
```

Now we can define our command method as follows:

```cs
        [CommandMethod("ENTCOLOR3")]
        public void ChangeEntityColorWithDelegate()
        {
            UsingTransaction(ChangeSmallCircleToRed);
        }
```

So far, we haven't really saved ourselves many keystrokes with this example use of delegates since all it does is remove the transaction-related code, which really isn't that much code. So let's build on our UsingTransaction helper method idea, and strip out some of the boiler plate code related to obtaining the model space block table record.

Consider the following UsingModelSpace helper method:

```cs
public void UsingModelSpace(Action<Transaction, BlockTableRecord> action) 
{
    using (var tr = Active.Database.TransactionManager.StartTransaction()) 
    {
        // Get the block table for the current database
        var blockTable =
            (BlockTable)tr.GetObject( Active.Database.BlockTableId, OpenMode.ForRead);
        // Get the model space block table record 
        var modelSpace =
            (BlockTableRecord)tr.GetObject( blockTable[BlockTableRecord.ModelSpace], OpenMode.ForRead);
        // Invoke the method action(tr, modelSpace);
        tr.Commit();
    }
}
```

This method allows us to reduce the "circle color change" code to the following method:

```cs
public void ChangeSmallCirclesToRed2(Transaction tr, BlockTableRecord modelSpace) 
{ 
    RXClass circleClass = RXObject.GetClass(typeof(Circle));
    // Loop through the entities in model space 
    foreach (ObjectId objectId in modelSpace) 
    {
        // Look for circles 
        if (objectId.ObjectClass.IsDerivedFrom(circleClass)) 
        { 
            var circle =
                (Circle)tr.GetObject( objectId, OpenMode.ForRead);
            if (circle.Radius < 1.0) 
            {
                circle.UpgradeOpen();
                circle.ColorIndex = 1; 
            }
        }
    }
}
```

And our command method now looks like this:

```cs
[CommandMethod("ENTCOLOR4")] 
public void ChangeEntityColorWithDelegate2() 
{ 
    UsingModelSpace(ChangeSmallCirclesToRed2); 
}
```

Now we are starting to save some coding keystrokes, and reduce duplicate code in our applications. Let's take it one step further, and consider the common need to iterate model space and perform some action on all entities of a certain type. Our next helper method will do this, using generics to define the type of object we are looking for.

Here is the code:

```cs
public void ForEach<T>(Action<T> action) where T: Entity 
{
    using (var tr = Active.Database.TransactionManager.StartTransaction()) 
    {
        // Get the block table for the current database
        var blockTable =
            (BlockTable)tr.GetObject( Active.Database.BlockTableId, OpenMode.ForRead);
        // Get the model space block table record 
        var modelSpace =
            (BlockTableRecord)tr.GetObject( blockTable[BlockTableRecord.ModelSpace], OpenMode.ForRead);
        RXClass theClass = RXObject.GetClass(typeof(T));
        // Loop through the entities in model space 
        foreach (ObjectId objectId in modelSpace) 
        {
            // Look for entities of the correct type 
            if (objectId.ObjectClass.IsDerivedFrom(theClass)) 
            {
                var entity =
                    (T)tr.GetObject( objectId, OpenMode.ForRead);
                action(entity);
            }
        } 
        tr.Commit();
    }
}
```

Now our delegate and command methods are greatly simplified:

```cs
public void ProcessCircle(Circle circle) 
{

if (circle.Radius < 1.0) 
{
    circle.UpgradeOpen();
    circle.ColorIndex = 1; }
}

[CommandMethod("ENTCOLOR")] 
public void ChangeEntityColorWithForEach() 
{ 
    ForEach<Circle>(ProcessCircle); 
}
```

We can also avoid defining the actual delegate method by using an anonymous method. Anonymous methods allow you to define the body of a delegate in-line where the delegate object is expected. So the code for the command method would change to:

```cs
ForEach(
    delegate(Circle circle) 
    { 
        if (circle.Radius < 1.0) 
        { 
            circle.UpgradeOpen(); 
            circle.ColorIndex = 1; 
        } 
    }
);
```

Or, we can use lambda expression syntax like so:

```cs
ForEach<Circle>(
    circle => 
    { 
        if (circle.Radius < 1.0) 
        { 
            circle.UpgradeOpen(); 
            circle.ColorIndex = 1; 
        } 
    }
);
```

Now that we have this handy ForEach method, we can, for example, print the average length of all the lines in the drawing with just a few lines of code:

```cs
[CommandMethod("AVGLEN")] 
public void AverageLength() 
{
    var lengths = new List<double>();
    ForEach<Line>(line => lengths.Add(line.Length)); 
    Active.WriteMessage("\nThe average length is {0}." , lengths.Average());
}
```

One thing that I don't like about our ForEach method is that it always uses the "current" database. It would be better, and more useful, if we could pass it the database we want to work with. Even better, we could make it an extension method of the Database class. Extension methods allow you to define methods that act just like native methods of a class. Extension methods are defined as static methods of a static class. The static class itself is never actually used. It just acts as a container for the static extension methods.

The signature of an extension method always includes at least one argument, which is of the type to which you want the method to apply. You also prefix that argument with the this keyword. Here is our ForEach method, implemented as an extension method:

```cs
public static class ExtensionMethods 
{
    public static void ForEach<T>(this Database database, Action<T> action) where T : Entity 
    { 
        using (var tr = database.TransactionManager.StartTransaction()) 
        { 
            // Get the block table for the current database
            var blockTable =
                (BlockTable)tr.GetObject( database.BlockTableId, OpenMode.ForRead);
            // Get the model space block table record 
            var modelSpace =
                (BlockTableRecord)tr.GetObject( blockTable[BlockTableRecord.ModelSpace], OpenMode.ForRead);
            RXClass theClass = RXObject.GetClass(typeof(T));
            // Loop through the entities in model space 
            foreach (ObjectId objectId in modelSpace) 
            {
                // Look for entities of the correct type 
                if (objectId.ObjectClass.IsDerivedFrom(theClass)) 
                {
                    var entity =
                        (T)tr.GetObject( objectId, OpenMode.ForRead);
                    action(entity);
                }
            } 
            tr.Commit();
        }
    }
}
```

Now our "circle color change" code can be:

```cs
Active.Database.ForEach<Circle>(
    circle => 
    { 
        if (circle.Radius < 1.0) 
        { 
            circle.UpgradeOpen(); 
            circle.ColorIndex = 1; 
        } 
    }
);
```

### 03. Using LINQ with the AutoCAD API

LINQ, or Language Integrated Query, is another very powerful language feature of .NET that can be leveraged in AutoCAD programs. At its core, LINQ is a set of extension methods tied to the IEnumerable and `IEnumerable<T>` types. It also includes a series of keywords that allow you to write SQL-like queries against enumerable types.

Here is a very simple LINQ example:

```cs
IEnumerable<int> evenNumbers = from i in Enumerable.Range(0, 100) where i%2 == 0 select i;
```

The above uses the keyword syntax. This can also be written as a method chain:

```cs
IEnumerable<int> evenNumbers = Enumerable.Range(0, 100).Where(i => i%2 == 0);
```

LINQ is very powerful, and covering all aspects of it is beyond the scope of this class. The focus here will be to demonstrate how LINQ can be used in conjunction with the AutoCAD API. LINQ is all about querying collections of data, and the AutoCAD database (i.e. the drawing) is full of collections of data from symbol tables (layers, blocks, etc.) to entity collections and selection sets. Naturally, all of these "tables" in the AutoCAD database are exposed in the API through objects that implement IEnumerable.

To understand how the LINQ methods work, it is important to understand the distinction between an IEnumerable and other "collection" types. Consider the following declarations:

```cs
IEnumerable<int> a; 
List<int> b; 
int[] c;
```

What these three types have in common is that they all implement IEnumerable, which means that they can all be queried using LINQ. The key distinction between the IEnumerable and the other two types is that `List<int>` and `int[]` are themselves containers of data, where `IEnumerable<int>` is separate from its data. IEnumerable is an interface that says nothing more than "this object can be enumerated." It contains a single method, GetEnumerator() that returns an IEnumerator, which is defined as follows:

```cs
public interface IEnumerator 
{
    bool MoveNext();
    void Reset();
    object Current { get; } 
}
```

And `IEnumerator<T>` extends IEnumerator as follows:

```cs
public interface IEnumerator<T> : IEnumerator 
{ 
    new T Current { get; } 
}
```

The beauty of IEnumerator is that it allows you to sequentially iterate over the elements of a collection without exposing the underlying data structure. This is a common design pattern that is often referred to as the iterator pattern.

1-3『又是迭代器，很多语言里都引入了这个特性，说明真是好东西（迭代器模式）。第一次知道它是学 JS 的时候。（2022-03-13）』

IEnumerable and IEnumerator are an integral part of .NET languages. For example, the foreach statement in C# requires that the object being enumerated implements the IEnumerable interface.

#### 3.1 AutoCAD Database Object Enumerators 

One of the most common activities in an AutoCAD program that involves enumeration is looping through a collection of database objects. Some of the classes in the AutoCAD .NET API that implement IEnumerable for the purposes of enumerating database objects include:

1 SymbolTable (base class for all symbol tables)

2 AttributeCollection

3 BlockTableRecord

4 ObjectIdCollection

5 SelectionSet

2『 AutoCAD 数据库里的 5 大枚举数据集，做一张信息数据卡片。（2022-03-21）』—— 已完成

So how can we leverage the power of LINQ with these classes? Let's first look at the code presented earlier that finds all the circles in the drawing with a radius less than 1.0 and changes their color to red.

```cs
    public class Commands
    {
        [CommandMethod("ENTCOLOR1")]
        public void ChangeEntityColor1()
        {
            // Get the various active objects
            Document document = Application.DocumentManager.MdiActiveDocument;
            Database database = document.Database;
            // Create a new transaction
            Transaction tr = database.TransactionManager.StartTransaction();
            using (tr)
            {
                // Get the block table for the current database
                var blockTable =
                (BlockTable)tr.GetObject(database.BlockTableId, OpenMode.ForRead);
                // Get the model space block table record
                var modelSpace = (BlockTableRecord)tr.GetObject(blockTable[BlockTableRecord.ModelSpace], OpenMode.ForRead);
                RXClass circleClass = RXObject.GetClass(typeof(Circle));
                // Loop through the entities in model space
                foreach (ObjectId objectId in modelSpace)
                {
                    // Look for circles
                    if (objectId.ObjectClass.IsDerivedFrom(circleClass))
                    {
                        var circle = (Circle)tr.GetObject(objectId, OpenMode.ForRead);
                        if (circle.Radius < 1.0)
                        {
                            circle.UpgradeOpen();
                            circle.ColorIndex = 1;
                        }
                    }
                }
                tr.Commit();
            }
        }
    }
```

If you look closely at the foreach statement, you'll notice that the object being returned by the enumerator is an ObjectId. This means that if we were to convert part of that foreach statement into a LINQ expression, it might look like this:

```cs
IEnumerable<ObjectId> circleIds =
                            from ObjectId objectId in modelSpace 
                            where objectId.ObjectClass.IsDerivedFrom(circleClass) 
                            select objectId;

foreach (ObjectId objectId in circleIds) 
{
    var circle = (Circle)tr.GetObject(objectId, OpenMode.ForRead);
    if (circle.Radius < 1.0) 
    {
        circle.UpgradeOpen();
        circle.ColorIndex = 1; 
    }
}
```

We could take it a step further, and include the call to GetObject in the LINQ expression. That way the resulting enumerator will return a Circle.

```cs
IEnumerable<Circle> circles =
                        from ObjectId objectId in modelSpace 
                        where objectId.ObjectClass.IsDerivedFrom(circleClass) 
                        select (Circle)tr.GetObject(objectId, OpenMode.ForRead);

foreach (var circle in circles) 
{ 
    if (circle.Radius < 1.0) 
    { 
        circle.UpgradeOpen(); 
        circle.ColorIndex = 1; 
    } 
}
```

With some more advance LINQ, we can actually include the logic that checks the radius:

```cs
IEnumerable<Circle> circlesToMakeRed =
                        from ObjectId objectId in modelSpace 
                        where objectId.ObjectClass.IsDerivedFrom(circleClass) 
                        select (Circle)tr.GetObject(objectId, OpenMode.ForRead)
                            into circle
                            where circle.Radius < 1.0
                            select circle;

foreach (var circle in circlesToMakeRed) 
{
    circle.UpgradeOpen();
    circle.ColorIndex = 1; 
}
```

One of the most important things to understand about LINQ is that these expressions take an existing IEnumerable, and typically return a different IEnumerable. This means that none of the code you see in the LINQ expression is executed until you actually iterate through the resulting IEnumerable. In all the examples above, nothing really happens until the foreach statement is executed.

Ok. Now you're probably thinking, "The LINQ expression above is complete gibberish, and is much more difficult to read than the original foreach loop." You are absolutely right. Let's see if we can make use of LINQ in a way that actually makes sense.

#### 3.2 Creating a Better Database Object Enumerable 

What we really want is an enumerable for database objects that gives us the actual object, and not the ObjectId, and does it in a type-safe way. Then we can write code like this:

```cs
Active.Database.UsingModelSpace(
    (tr, ms) =>
        {
            var circles = ms.OfType<Circle>(tr) .Where(c => c.Radius < 1.0);
            foreach (var circle in circles) 
            {
                circle.UpgradeOpen();
                circle.ColorIndex = 1; 
            }
        });
```

Let's start with a generic IEnumerator class that wraps an `IEnumerator<ObjectId>` and gives us actual objects that derive from DBObject.

```cs
/// <summary> 
/// Generic <c>IEnumerator</c> implementation that wraps an <c>IEnumerator&lt;ObjectId&gt;</c> 
/// and instead gives us actual objects that derive from <c>DBObject</c>.
/// </summary> /// <typeparam name="T">A type that derives from <c>DBObject</c>.</typeparam> 
public class MyDbObjectEnumerator<T> : IEnumerator<T> where T : DBObject 
{

private readonly IEnumerator<ObjectId> _enumerator; private readonly OpenMode _openMode; private readonly RXClass _theClass; private readonly Transaction _transaction;

/// <summary> /// Initializes a new instance of the <see cref="MyDbObjectEnumerator{T}"/> class. /// </summary>

/// <param name="enumerator">The enumerator to wrap.</param>

/// <param name="tr">The current transaction.</param>

/// <param name="openMode">The open mode.</param>

public MyDbObjectEnumerator(IEnumerator<ObjectId> enumerator, Transaction tr, OpenMode openMode) { _enumerator = enumerator; _transaction = tr; _openMode = openMode; _theClass = RXObject.GetClass(typeof (T)); }

#region IEnumerator<T> Members

/// <summary> /// Performs application-defined tasks associated with freeing, releasing, /// or resetting unmanaged resources.

/// </summary> public void Dispose() { _enumerator.Dispose(); }

/// <summary> /// Advances the enumerator to the next element of the collection.

/// </summary> /// <returns> /// true if the enumerator was successfully advanced to the next element; /// false if the enumerator has passed the end of the collection.

/// </returns> public bool MoveNext() {

while (_enumerator.MoveNext()) {

if (_enumerator.Current.ObjectClass.IsDerivedFrom(_theClass))

return true; }

return false;

}

/// <summary> /// Sets the enumerator to its initial position, which is before the first /// element in the collection.

/// </summary> public void Reset() { _enumerator.Reset(); }

/// <summary> /// Gets the element in the collection at the current position of the enumerator. /// </summary> /// <returns> /// The element in the collection at the current position of the enumerator.

/// </returns>

public T Current { get { return (T) _transaction.GetObject(_enumerator.Current, _openMode); } }

/// <summary> /// Gets the current element in the collection. /// </summary> /// <returns> /// The current element in the collection.

/// </returns> object IEnumerator.Current { get { return Current; } }

#endregion

}
```

Next, we need an IEnumerable implementation that returns our custom enumerator.

```cs
/// <summary> 
/// An <c>IEnumerable</c> implementation that returns a <see cref="MyDbObjectEnumerator{T}"/>. 
/// </summary> 
/// <typeparam name="T">A type that derives from <c>DBObject</c>.</typeparam> 
public class MyDBObjectEnumerable<T> : IEnumerable<T> where T : DBObject 
{

private readonly IEnumerable<ObjectId> _enumerable; private readonly OpenMode _openMode; private readonly Transaction _transaction;

/// <summary> /// Initializes a new instance of the <see cref="MyDBObjectEnumerable{T}"/> class. /// </summary>

/// <param name="enumerable">The enumerable.</param>

/// <param name="tr">The current transaction.</param>

/// <param name="openMode">The open mode.</param>

public MyDBObjectEnumerable(IEnumerable<ObjectId> enumerable, Transaction tr, OpenMode openMode) { _enumerable = enumerable; _transaction = tr; _openMode = openMode; }

#region IEnumerable<T> Members

/// <summary> /// Returns an enumerator that iterates through the collection.

/// </summary> /// <returns> /// An <see cref="T:System.Collections.IEnumerator"/> object that can be used /// to iterate through the collection.

/// </returns> public IEnumerator<T> GetEnumerator() { return new MyDbObjectEnumerator<T>(_enumerable.GetEnumerator(), _transaction, _openMode); }

/// <summary> /// Returns an enumerator that iterates through a collection.

/// </summary> /// <returns> /// An <see cref="T:System.Collections.IEnumerator"/> object that can be used /// to iterate through the collection.

/// </returns> IEnumerator IEnumerable.GetEnumerator() { return GetEnumerator(); }

#endregion

}
```

And finally, to provide easy access to our new enumerable type, we can define extension methods as follows:

```cs
public static IEnumerable<T> OfType<T>(this IEnumerable<ObjectId> enumerable, 
Transaction tr, 
OpenMode openMode) 
where T : DBObject 
{ 
return new MyDBObjectEnumerable<T>(enumerable, tr, openMode); 
}
```

### 04. Abstraction and Dependency Injection

In a typical application, the components that make up the core business logic will often rely on other components to do their work. For example, if your application uses an external database, you might place your data access code into a separate component. Furthermore, you might separate your presentation tier into its own component. This is a very common practice, and is known as a multi-tiered architecture.

『原图里的展示，自上而下：User Interface => Business Logic => Data Access。』

You may also have additional components that perform specific "services" to your application, such as logging, exception handling, configuration, etc. These components all represent dependencies upon which other components rely.

Consider the following simple code example, which might represent some business logic code that uses a data tier, and a logging component.

```cs
public class Example1 
{
    public void DoTheWork() { 
        DataRepository dataRepository = new DataRepository(); 
        Logger logger = new Logger(); 
        logger.Log("Getting the data"); 
        DataSet theData = dataRepository.GetSomeData(); 
        // Do some work with the data...
        logger.Log("Done." );
    }
}
```

While it is good that we've separated the data access and logging code into their own components, there are still some issues with this example. First, this method is not only tightly coupled with its dependencies, it is also responsible for their creation. This results in the following issues:

1 This code is nearly impossible to reuse because it is so tightly coupled with its dependencies.

2 This code would have to be modified if there is a need to replace one of the dependent components with a new implementation.

3 This code is impossible to unit test, because it cannot be isolated from its dependencies.

Now examine the following alternative:

```cs
public class Example2 
{
    private readonly IDataRepository _dataRepository; 
    private readonly ILogger _logger; 
    public Example2(IDataRepository dataRepository, ILogger logger) {
        _dataRepository = dataRepository;
        _logger = logger; 
    } 
    public void DoTheWork() {
        _logger.Log("Getting the data" );
        DataSet theData = _dataRepository.GetSomeData();
        // Do some work with the data...
        _logger.Log("Done."); 
    }
}
```

Here, we've done two key things: 1) We've introduced abstraction by creating and developing against interfaces rather than specific concrete implementations, and 2) The class is no longer responsible for the creation of its dependencies – they are injected into it via the class constructor.

This illustrates the following key principles and design patterns of software engineering:

1 Separation of Concerns – This class is now only responsible for the specific job it was designed to do.

2 Abstraction – By using interfaces, we have established a set of protocols by which the components interact, separately from the classes themselves.

3 Inversion of Control – The class has relinquished control of the creation and initialization of its dependencies.

4 Dependency Injection – This pattern is based on Inversion of Control, and describes the way in which an object obtains references to its dependencies.

1『这节有关抽象和依赖注入的讲解，做一张主题卡片。（2022-03-13）』—— 已完成

#### 4.1 Abstraction in AutoCAD Applications

Depending on the nature of your AutoCAD application, you should consider how you might use abstraction to disconnect all or part of your business logic code from its dependency on the AutoCAD API.

Let's explore a simple example that demonstrates how we might accomplish this. Suppose we've been tasked to create an AutoCAD application that is a very simple quantity take-off application. Its goal is to count the number of inserts of each block (by name) in a drawing, and store the results to a database. If we examine the problem in a very abstract way, we can start by writing the core logic as follows:

```cs
public class BlockCounter 
{
    private readonly IDrawing _drawing; 
    private readonly IQuantityTakeoffDatabase _quantityTakeoffDatabase;
    
    public BlockCounter(IDrawing drawing, IQuantityTakeoffDatabase quantityTakeoffDatabase) 
    {
        _drawing = drawing;
        _quantityTakeoffDatabase = quantityTakeoffDatabase; 
    }
    
    public void CountTheBlocks() 
    {
        var quantityLineItems = new Dictionary<string, QuantityLineItem>();
        foreach (BlockRef blockRef in _drawing.GetAllBlockRefs()) 
        {
            if (quantityLineItems.ContainsKey(blockRef.Name)) 
                quantityLineItems[blockRef.Name].Quantity++; 
            else
                quantityLineItems.Add(
                    blockRef.Name,
                    new QuantityLineItem { BlockName = blockRef.Name, Quantity = 1 });
        }
        
        _quantityTakeoffDatabase.StoreQuantities(quantityLineItems.Values);
    }
}

public class BlockRef 
{
    public BlockRef(string name) 
    { 
        Name = name; 
    }
    public string Name { get; private set; }
}

public class QuantityLineItem 
{ 
    public string BlockName { get; set; 
}

public int Quantity 
{ 
    get; set; 
}

}

public interface IDrawing { 
    IEnumerable<BlockRef> GetAllBlockRefs(); 
}

public interface IQuantityTakeoffDatabase 
{ 
    void StoreQuantities(IEnumerable<QuantityLineItem> lineItems);
}
```

By thinking in abstract terms, we've simplified our dependency on the AutoCAD API into a single interface, IDrawing that has a single method, GetAllBlockRefs(). After all, the only thing we really need from AutoCAD is a way to get the blocks in a drawing. For each block all we care about is the name, so we define a BlockRef class, which is nothing more than a simple data structure that represents a block reference with the properties that we need. We've also abstracted the data access component into a single interface, IQuantityTakeoffDatabase. What remains is a BlockCounter class that contains the core logic behind our application, and it has no dependency on the AutoCAD API. This class can be compiled, tested and debugged in complete isolation – we don't even need to have AutoCAD on the development computer.

Obviously, in order to make our application actually work inside AutoCAD, we need to implement the IDrawing interface in a separate component that does reference the AutoCAD API.

Taking advantage of our ForEach method we defined earlier, our implementation of IDrawing becomes very easy to write.

```cs
public class Drawing : IDrawing 
{
    public IEnumerable<BlockRef> GetAllBlockRefs() 
    {
        var blocks = new List<BlockRef>();
        Active.Database.ForEach<BlockReference>( 
            blockRef => blocks.Add(new BlockRef(blockRef.Name)));
        return blocks;
    }
}
```

Next, we need an implementation of IQuantityTakeoffDatabase. For now, we'll create a mock implementation that simply spits out the quantity line items to the AutoCAD command window. Our final implementation of IQuantityTakeoffDatabase will reside in its own assembly, and will actually write the data to a database somewhere. The beauty of using abstraction is that we don't have to worry about that right now!

```cs
public class MockDatabase : IQuantityTakeoffDatabase 
{
    public void StoreQuantities(IEnumerable<QuantityLineItem> lineItems)
    {
        foreach (QuantityLineItem lineItem in lineItems) 
            Active.WriteMessage("{0}: {1}" , lineItem.BlockName, lineItem.Quantity);
    } 
}
```

Finally, we need a way to invoke the block counter in AutoCAD. The easiest way to do this is to define an AutoCAD command like so:

```cs
public static class Commands 
{
    [CommandMethod("CTB")] 
    public static void CountTheBlocks() 
    { 
        var counter = new BlockCounter(new Drawing(), new MockDatabase());
        counter.CountTheBlocks();
    }
}
```

At first glance, separating components and using abstraction to define how the components interact may seem like a lot more work. But in fact, it does not increase the amount of code that you write – it just affects how your code is organized. If you put yourself in the mindset of thinking abstractly about a problem, your code will become more reusable, maintainable, scalable, and testable.
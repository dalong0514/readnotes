## 记忆时间

## 卡片

### 0101. 主题卡 —— Abstraction and Dependency Injection

信息源自「2022024Programming-AutoCAD-with-CS-Best-Practices.md」

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

Depending on the nature of your AutoCAD application, you should consider how you might use abstraction to disconnect all or part of your business logic code from its dependency on the AutoCAD API.

Let's explore a simple example that demonstrates how we might accomplish this. Suppose we've been tasked to create an AutoCAD application that is a very simple quantity take-off application. Its goal is to count the number of inserts of each block (by name) in a drawing, and store the results to a database. If we examine the problem in a very abstract way, we can start by writing the core logic as follows:

### 0102. 主题卡 —— 对类的理解

信息源自「2022003An-Introduction-to-AutoCAD-NET-API-Using-CS.md」

What is a Class?

To answer what a class is, we have to understand a little more about .Net. C#.Net is an object-oriented programming language. That means everything that you work with inside of C# is an object. A piece of text is not just characters, but it is a string object.

I know this may seem like a little thing, but it's important to remember as we build our own objects using classes. Now a class may seem to you simply as a chunk of code, but we use classes for everything we program within our project. A class really will house our methods, or the routines or functions that we're write, as well as the properties, the values that we're going to read and write too, as well. Everything that we use is really a container, so think of a class in two different ways. We can use a class as a custom object. Another way we can use a class is simply a container for our functions, or methods.

2『这里对类的理解做一张主题卡片。（2022-03-22）』—— 已完成

Layer (Object)

• CreateLayerMethod

• IsLayerFrozenProperty

Command (Container)

• HelloWorldCmdMethod

• CreateNewLineCmdMethod

Regardless of how we use a class, a class is always an object. Because it's an object of its own, that means every single time we want to use that class we have to create a new instance of it. In other words, when we go to McDonald's and we order a Big Mac, we know what comes with a Big Mac – what it contains. Yet each time you go and order a Big Mac, they have to create new instance for you to consume.

Thus, when we want to use a class, we have to create a new instance of the class – even when we treat it as a container of routines.

Through this course, we are simply going to use classes as containers to house our code – our commands that we write. Nevertheless, do not stop in your development there. Note the sample shown. We have a custom class named Layer. It contains not only special routines but also properties that are specific to that instance of the layer object.

### 0201. 术语卡 —— Class Library

信息源自「2022020Create-Your-First-AutoCAD-Plug-In-Using-CS.md」

When creating plugins for Autodesk software, including Autocad, our main project type will be Class Library. This type of project compiles to a DLL file, not an EXE (or executable) file. A class library can't run on its own. It must be "hosted" by some other executable application. In our case, the "host" application will be Autocad.

1『想不到在这里知道了「类库」的概念，做一张术语卡片。（2022-03-13）』—— 已完成

### 0202. 术语卡 —— Transactions

信息源自「2022003An-Introduction-to-AutoCAD-NET-API-Using-CS.md」

Transactions are the means to make modifications and really, to even read information of an object that is found in the drawing database. Each object, including non-graphical objects such as Layers, Text Styles, etc. are assigned a unique Object Id each time the drawing is opened. Let's learn about transactions by using an analogy.

2『 Transactions 的概念，做一张术语卡片。（2002-03-22）』—— 已完成

If you wanted to know how much money was in your bank, you still would have to provide the teller, or even the internet, your bank account number, a unique ID, so as to access your bank account. And even if you didn't want to transfer any money, you still would have to open up that account and it would take a transaction to do so. So even if you're looking at the information or modifying the information, a transaction is needed. And it's the same when it comes to working with AutoCAD's database transaction.

In this exercise, we are going to look at creating a line. To do so we will have to create a transaction, get the model space block definition (yes, each space is stored as a block definition in the drawing database), and add the new line to model space.

Most non-graphical objects, such as the block definitions, are stored in a table. Thus, to get the model space block definition, we have to find it's record (or row) in the Block Table.

Lastly, just because we make changes to tables and objects, if we don't commit those changes to the database, then the changes are not made.

### 0203. 术语卡 ——

### 0301. 人名卡 ——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

### 0401. 金句卡 ——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 数据信息卡 —— ObjectARX、ObjectARX Wizards、AutoCAD .NET Wizards 三者关系

信息源自「2022003An-Introduction-to-AutoCAD-NET-API-Using-CS.md」

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

### 0502. 数据信息卡 —— 几个 .NET AutoCAD 二次开发常用的函数

信息源自「2022024Programming-AutoCAD-with-CS-Best-Practices.md」

There are a couple of techniques used in this code worth mentioning, but are beyond the scope of this class.

1 Use of the using keyword, which automatically calls Dispose() on the transaction object when it goes out of scope.

2 Use of the RXObject.GetClass method along with the ObjectId.ObjectClass method, which allows you to check for the type of object before you actually open it.

3 Use of the UpgradeOpen method, which allows you to only open an object for write when you know you need to.

1『上面几个 .NET AutoCAD 二次开发常用的函数，做一张信息数据卡片。（2022-03-21）』—— 已完成

### 0503. 数据信息卡 —— CommandMethod 是 Autodesk.AutoCAD.Runtime 库里的

信息源自「2022003An-Introduction-to-AutoCAD-NET-API-Using-CS.md」

```cs
[Autodesk.AutoCAD.Runtime.CommandMethod ("MyFirstCommand")]

public void cmdMyFirst() 
{ 
}
```

1『这里才知道，原来 CommandMethod 是 Autodesk.AutoCAD.Runtime 库里的一个函数。做一张信息数据卡片。（2022-03-22）』

### 0504. 数据信息卡 —— AutoCAD 的几个基础库的功能

信息源自「2022003An-Introduction-to-AutoCAD-NET-API-Using-CS.md」

```cs
using Autodesk.AutoCAD.DatabaseServices;
using Autodesk.AutoCAD.EditorInput;
using Autodesk.AutoCAD.Runtime;
```

In the process of creating our first command, we have been introduced to the Runtime, EditorInput, and ApplicationServices namespace. The ApplicationServices namespace stores the classes connected with the Application as a whole. The EditorInput contains classes and means to read and write information to the command line. It also contains all the means to request the user to provide us something – a coordinate picked on the screen, a selected object, etc.

2『 AutoCAD 的几个基础库的功能，做一张信息数据卡片。（2022-03-22）』

### 0601. 任意卡 —— 

